# Virtualbox

Инфа об образе:

    VBoxManage showhdinfo "/home/common/VirtualBox VMs/Sandbox/Sandbox.vdi"

Сгенерировать новый UUID у образа:

    VBoxManage internalcommands sethduuid "/home/common/VirtualBox VMs/Sandbox/Sandbox.vdi"

Проброс портов:

SSH | TCP | 127.0.0.1 | 2222 | 10.2.0.15 | 22
