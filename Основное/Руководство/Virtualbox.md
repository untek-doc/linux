Инфа об образе:

    VBoxManage showhdinfo "/home/common/VirtualBox VMs/Sandbox/Sandbox.vdi"

Сгенерировать новый UUID у образа:

    VBoxManage internalcommands sethduuid "/home/common/VirtualBox VMs/Sandbox/Sandbox.vdi"

## Проброс портов

| Имя | Протокол | IP хоста  | Порт хоста | IP гостя  | Порт гостя |
| --- | -------- | --------- | ---------- | --------- | ---------- |
| SSH | TCP      | 127.0.0.1 | 2222       | 10.2.0.15 | 22         |
Ссылка на источник: https://losst.ru/probros-portov-virtualbox?ysclid=l6j6ey8vbo193726231#%D0%9F%D1%80%D0%BE%D0%B1%D1%80%D0%BE%D1%81_%D0%BF%D0%BE%D1%80%D1%82%D0%BE%D0%B2_%D0%B2_VirtualBox