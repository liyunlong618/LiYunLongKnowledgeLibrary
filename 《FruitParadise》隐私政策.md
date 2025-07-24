# **《FruitParadise》隐私政策**



**最近更新：2025年7月24日**

## 一、信息收集清单

| 信息类型        | 使用目的                  | 使用场景                  | 拒绝影响               |
|-----------------|---------------------------|---------------------------|------------------------|
| 设备标识符      | 账号系统生成              | 用户注册/登录             | 无法使用账号功能       |
| 存储权限        | 游戏存档保存              | 进度保存/资源下载         | 无法保存游戏进度       |
| 传感器数据      | 游戏操作优化              | 体感游戏功能              | 部分操作方式受限       |
| 网络信息        | 服务器连接                | 所有在线功能              | 无法使用在线服务       |

## 二、权限使用说明

### 1. 必需权限
- **READ_PHONE_STATE**  
  用途：生成唯一设备标识符用于游客账号系统  
  拒绝后果：无法使用账号相关功能

- **WRITE_EXTERNAL_STORAGE**  
  用途：保存游戏截图和录像至相册  
  拒绝后果：无法使用截图分享功能

### 2. 可选权限
- **ACCESS_COARSE_LOCATION**  
  用途：基于位置的社交功能（如附近玩家）  
  拒绝后果：无法使用位置相关功能

- **BODY_SENSORS**  
  用途：运动类小游戏操作  
  拒绝后果：相关小游戏需改用触控操作

## 三、数据使用方式

```java
// 实际代码中的权限声明对应关系
String[] permissionsToCheck = {
    Manifest.permission.READ_PHONE_STATE,       // 设备标识
    Manifest.permission.WRITE_EXTERNAL_STORAGE, // 存储
    Manifest.permission.ACCESS_COARSE_LOCATION, // 位置
    Manifest.permission.BODY_SENSORS            // 传感器
};
```

## 四、第三方共享清单

| SDK名称   | 使用目的 | 共享信息       | 隐私链接                       |
| --------- | -------- | -------------- | ------------------------------ |
| UnLua     | 脚本系统 | 无个人信息收集 | [查看](https://unlua.io/)      |
| Metasound | 音频处理 | 设备音频配置   | [查看](https://epicgames.com/) |

## 五、用户权利保障

1. **撤回同意**
    通过游戏设置 → 隐私设置 → 关闭数据收集开关
3. **投诉反馈渠道**
    客服QQ：840597647（工作日9:00-22:00）

## 六、技术保护措施

```
<!-- 实际配置中的安全措施 -->
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```

## 七、政策更新提示

当本政策更新时，您将在游戏中看到：

```
// 隐私弹窗更新逻辑
if (policyUpdated) {
    ShowPrivacyDialog();  // 重新弹出隐私协议
}
```

## 八、联系我们

**隐私专员邮箱**：840597647@qq.com
 **官方B站账号**：[我要一个大杯的个人空间-我要一个大杯个人主页-哔哩哔哩视频](https://space.bilibili.com/83334537?spm_id_from=333.1387.0.0)