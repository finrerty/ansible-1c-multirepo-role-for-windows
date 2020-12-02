# ansible-1c-multirepo-role-for-windows
Очень простая роль для удобного создания, обновления и декларативного описания любого количества 1с хранилищ разных версий на сервере Windows

## С чего начать
Для установки роли достаточно зайти в папку ansible/roles и склонировать этот репозиторий

## Системные требования
Для корректной работы роли на управляемой машине требуется Windows Server 2012 R2 или новее, а так же настроенная служба WinRM.

## Описание роли
Данная роль позволяет в рамках одного очень просто и быстро установить как одну службу сервера хранилищ, так и несколько служб разных версий на разных портах

Для этого необходимо:
1) Создать плейбук для запуска роли на определённых хостах
```
- name: Your amazing Servers for 1c repository
  hosts: 1c_repo
  become: true
  become_method: runas
  become_user: Administrator
  roles:
    - ansible-1c-multirepo-role-for-windows
```
2) Настроить необходимые значения переменных в файле defaults/main.yml или в других связанных с хостом расположениях.
```
download_url: https://downloads.1c.ru/   # ресурс, с которого будет осуществляться загрузка платформы
url_username: %your_username%            # логин и пароль данного ресурса
url_password: %your_password%
platform_architecture: 64-bit            # архитектура приложения
platform_version:                        # необходимая версия платформы, можно оставить как одну, так и указать несколько
  - 8.3.18.1208
  - 8.3.14.1854
setup_archive_filename:                  # название архива с платформой
  - windows64full_8_3_18_1208.rar
  - windows64full_8_3_14_1854.rar
repo_srv_name:                           # название службы
  - '1C:Enterprise 8.3 Configuration Repository Server'
  - '2542_1C:Enterprise 8.3 Configuration Repository Server'
repository_port:                         # порт каждой службы
  - 1542
  - 2542
installation_path: C:\Program Files\1cv8 # путь установки платформы
```
