___________________________________________________________________________________________
###### [GoMenu](../UE_EditorMenu.md)
___________________________________________________________________________________________
# 编辑器中子类查找父类蓝图中添加的组件并设置
___________________________________________________________________________________________


## 目录

[TOC]

___________________________________________________________________________________________

#### 批量设置移除SM的简单碰撞

```cpp
// 获取当前选中的资产
TArray<UObject*> SelectedObjects = UEditorUtilityLibrary::GetSelectedAssets();

// 分离 StaticMeshes 和 Blueprints
TArray<UStaticMesh*> SelectedStaticMeshes;
TArray<UBlueprint*> SelectedBlueprints;

for (UObject* SelectedObject : SelectedObjects)
{
    if (UStaticMesh* SM = Cast<UStaticMesh>(SelectedObject))
    {
        SelectedStaticMeshes.Add(SM);
    }
    else if (UBlueprint* BP = Cast<UBlueprint>(SelectedObject))
    {
        SelectedBlueprints.Add(BP);
    }
}

if (SelectedStaticMeshes.Num() == 0 && SelectedBlueprints.Num() == 0)
{
    UE_LOG(LogTemp, Warning, TEXT("未选中任何 StaticMesh 或 Blueprint 资产。"));
    return;
}

// 处理 StaticMeshes
for (UStaticMesh* StaticMesh : SelectedStaticMeshes)
{
    for (const auto& Pair : StaticMeshToComponentMap)
    {
        if (StaticMesh->GetName().Contains(Pair.Key))
        {
            if (UBodySetup* BodySetup = StaticMesh->GetBodySetup())
            {
                // 移除简单碰撞
                BodySetup->RemoveSimpleCollision();

                // 设置碰撞复杂性为复杂碰撞
                BodySetup->CollisionTraceFlag = ECollisionTraceFlag::CTF_UseComplexAsSimple;

                // 标记静态网格体为已修改并重新构建
                StaticMesh->MarkPackageDirty();
                StaticMesh->Build();

                // 保存静态网格体包
                UPackage* Package = StaticMesh->GetOutermost();
                FString PackageName = Package->GetName();
                FString PackageFileName = FPackageName::LongPackageNameToFilename(PackageName, FPackageName::GetAssetPackageExtension());
                UPackage::SavePackage(Package, StaticMesh, EObjectFlags::RF_Public | EObjectFlags::RF_Standalone, *PackageFileName);

                UE_LOG(LogTemp, Log, TEXT("移除简单碰撞，设置复杂碰撞，并保存: %s"), *StaticMesh->GetName());
            }
        }
    }
}
```

------

### 获取选中的BP和SM文件，根据映射静态表TMap，Editor下动态配置BP的StaticMesh组件的SM

```CPP
// 获取当前选中的资产
TArray<UObject*> SelectedObjects = UEditorUtilityLibrary::GetSelectedAssets();

for (UObject* SelectedObject : SelectedObjects)
{
    // 处理蓝图类（BP）
    if (UBlueprint* BlueprintAsset = Cast<UBlueprint>(SelectedObject))
    {
        UE_LOG(LogTemp, Log, TEXT("Blueprint asset selected: %s"), *BlueprintAsset->GetName());

        // 获取蓝图的类默认对象 (CDO)
        UBlueprintGeneratedClass* OuterBPClass = Cast<UBlueprintGeneratedClass>(BlueprintAsset->GeneratedClass);
        if (OuterBPClass && OuterBPClass->InheritableComponentHandler)
        {
            // 遍历所有可继承的组件
            for (auto RecordIt = OuterBPClass->InheritableComponentHandler->CreateRecordIterator(); RecordIt; ++RecordIt)
            {
                if (RecordIt->ComponentClass->IsChildOf(UStaticMeshComponent::StaticClass()))
                {
                    if (UStaticMeshComponent* TargetComObj = Cast<UStaticMeshComponent>(RecordIt->ComponentTemplate))
                    {
                        for (const auto& Pair : StaticMeshToComponentMap)
                        {
                            // 如果组件名字匹配
                            if (TargetComObj->GetName().Contains(Pair.Value.ToString()))
                            {
                                UStaticMesh* FoundMesh = nullptr;
                                for (UObject* Obj : SelectedObjects)
                                {
                                    if (UStaticMesh* Mesh = Cast<UStaticMesh>(Obj))
                                    {
                                        if (Mesh->GetName().Contains(Pair.Key))
                                        {
                                            FoundMesh = Mesh;
                                            break;
                                        }
                                    }
                                }

                                if (FoundMesh)
                                {
                                    // 设置静态网格体
                                    TargetComObj->SetStaticMesh(FoundMesh);
                                    UE_LOG(LogTemp, Log, TEXT("Set static mesh component %s to mesh %s"), *TargetComObj->GetName(), *FoundMesh->GetName());

                                    // 标记蓝图为已修改
                                    BlueprintAsset->MarkPackageDirty();
                                }
                            }
                        }
                    }
                }
            }
        }

        // 保存蓝图更改
        FString PackageName = BlueprintAsset->GetOutermost()->GetName();
        FString PackageFileName = FPackageName::LongPackageNameToFilename(PackageName, FPackageName::GetAssetPackageExtension());
        UPackage::SavePackage(BlueprintAsset->GetOutermost(), BlueprintAsset, EObjectFlags::RF_Public | EObjectFlags::RF_Standalone, *PackageFileName);

        UE_LOG(LogTemp, Log, TEXT("Saved blueprint asset: %s"), *BlueprintAsset->GetName());
    }
}

UE_LOG(LogTemp, Log, TEXT("Batch collision modification and save complete."));

```

