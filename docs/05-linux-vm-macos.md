# 05. Установка Linux VM на MacBook Apple Silicon

[← Предыдущая](04-clion-macos.md) · [Содержание](../README.md) · [Следующая →](06-docker-linux.md)


## Почему ARM64 и UTM

Apple Silicon использует архитектуру ARM64. ARM64-образ Ubuntu виртуализируется нативно и работает быстрее, чем эмуляция x86_64. UTM доступен как графическая оболочка над Apple Virtualization/QEMU. Если преподаватель требует VMware Fusion или Parallels, логика установки остаётся аналогичной, но названия экранов отличаются.

## Требования

- MacBook с Apple Silicon;
- UTM с официального сайта или Mac App Store;
- ISO Ubuntu Server ARM64 LTS;
- ориентировочно 4 vCPU, 8 ГБ RAM и 40–60 ГБ диска (уменьшите RAM, если хосту её недостаточно).

## 1. Загрузка компонентов

1. Установите [UTM](https://mac.getutm.app/).
2. Загрузите **Ubuntu Server for ARM** (`arm64`) с официального сайта Ubuntu.
3. Не используйте образ `amd64/x86_64` для этой инструкции.

## 2. Создание VM

1. Нажмите **Create a New Virtual Machine**.
2. Выберите **Virtualize**, затем **Linux**.
3. Подключите загруженный ARM64 ISO.
4. Задайте ресурсы, например: 4 CPU, 8192 MB RAM, 60 GB disk.
5. Сеть оставьте в режиме Shared/NAT — VM получит Интернет через macOS.
6. Назовите VM, например `ubuntu-mlsecdevops`.

## 3. Установка Ubuntu

Запустите VM и следуйте мастеру:

1. выберите язык и раскладку;
2. оставьте DHCP, если статический адрес не требуется;
3. используйте весь виртуальный диск;
4. создайте пользователя;
5. при необходимости установите OpenSSH Server;
6. завершите установку и перезагрузите VM;
7. отключите установочный ISO, если VM снова загружается в installer.

## 4. Обновление и проверка

```bash
sudo apt update
sudo apt upgrade -y
sudo reboot
```

После перезагрузки:

```bash
uname -m
cat /etc/os-release
ip address
ping -c 3 ubuntu.com
```

Ожидаемая архитектура:

```text
aarch64
```

## 5. Необязательный SSH-доступ

Если OpenSSH не был выбран при установке:

```bash
sudo apt install -y openssh-server
sudo systemctl enable --now ssh
hostname -I
```

С macOS:

```bash
ssh <linux-user>@<vm-ip>
```

## Возможные проблемы

- **VM медленная:** убедитесь, что используется Virtualize + ARM64, а не Emulate + x86_64.
- **Нет сети:** проверьте Shared Network/NAT и DHCP внутри Ubuntu.
- **Повторно открывается installer:** извлеките ISO из виртуального CD/DVD.
- **Docker-образ не поддерживает ARM64:** используйте multi-arch образ либо явно ищите ARM64-вариант. Официальные MySQL и PostgreSQL образы из следующих глав поддерживают распространённые платформы; проверяйте текущий manifest выбранного тега.

## Источники

- [UTM — Linux virtual machines](https://docs.getutm.app/guides/ubuntu/)
- [Ubuntu — загрузка Ubuntu Server for ARM](https://ubuntu.com/download/server/arm)

