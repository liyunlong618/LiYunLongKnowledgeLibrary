```python
"""
Export FBX Action
"""

import unreal
import json
import umds
from unrels import UEBaseAction
from lsr.unrealls.userlib.actions import UEBaseAction
import lsr.protosar.core.parameter as pa

__all__ = ["AddSocket"]

class AddSocket(UEBaseAction):
    """
    Select A skeleton AND a skeletal mesh in scene,
    01 -> this node will clear all sockets first
    02 -> then generate new sockets with provided json file
    """
    _TAGS = ["UTIL"]

    @pa.file_param(ext="json")
    def socket_json(self):
        """
        Socket JSON file
        """
        pass

    def run(self):
        """Executes this action."""
        self.skm = umds.is_selection(True, types=["SkeletalMesh"])
        self.socket_data = {}
        self.lsr.lib = unreal.LSRLibrary()

        self.check_user_input()

        with open(self.socket_json.value, "r", encoding="utf-8") as f:
            self.socket_data = json.load(f)
            if not "sockets" in self.socket_data:
                self.display_dialog_message("Invalid socket json is provided")
                raise RuntimeError("Invalid socket json is provided")

        self.clear_all_sockets()
        self.add_sockets()

    def check_user_input(self):
        if not self.skm:
            self.display_dialog_message("No Skeletal Mesh is provided")
            raise RuntimeError("No Skeletal Mesh is provided")

        if not self.socket_json.value:
            self.display_dialog_message("No socket json is provided")
            raise RuntimeError("No socket json is provided")

    def clear_all_sockets(self):
        socket_list = []
        socket_list = [self.skm.get_socket_by_index(i) for i in range(self.skm[0].num_sockets())]

        self.lsr.lib.delete_selected_mesh_socket(self.skm[0], socket_list)

    def add_sockets(self):
        for socket in self.socket_data["sockets"]:
            socket_name = socket["socket_name"]
            socket_translation = socket["translation"]
            socket_rotation = socket["rotation"]
            parent_joint = socket["parent_joint"]

            socket_translation = [
                socket_translation[0] * -1,
                socket_translation[1],
                socket_translation[2],
            ]

            socket_rotation = [
                -socket_rotation[1],
                socket_rotation[2],
                socket_rotation[0],
            ]

            _socket = self.lsr.lib.add_skeletal_mesh_socket(
                self.skm[0], socket_name, parent_joint
            )
            _socket.set_editor_property("relative_location", socket_translation)
            _socket.set_editor_property("relative_rotation", socket_rotation)

```

