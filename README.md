# ML SecDevOps — настройка среды разработки

Документация описывает подготовку рабочей среды для выполнения
лабораторных и практических работ курса ML SecDevOps.

Поддерживаются две основные рабочие среды:

- Windows + WSL2 + Visual Studio
- macOS + Linux VM + CLion

Для работы с базами данных используются Docker-контейнеры
PostgreSQL и MySQL.

---

## Содержание

### Windows

1. [Установка WSL2](docs/01-wsl2-installation.md)
2. [Установка Visual Studio](docs/02-visual-studio-installation.md)
3. [Интеграция Visual Studio с WSL2](docs/03-visual-studio-wsl2.md)

### macOS

4. [Установка CLion](docs/04-clion-macos.md)
5. [Установка Linux VM](docs/05-linux-vm-macos.md)

### Linux / WSL2

6. [Установка Docker](docs/06-docker-linux.md)
7. [Запуск MySQL в Docker](docs/07-mysql-docker.md)
8. [Запуск PostgreSQL в Docker](docs/08-postgresql-docker.md)

---

## Используемое ПО

| Компонент | Назначение |
|---|---|
| WSL2 | Linux-окружение в Windows |
| Ubuntu | Linux-дистрибутив |
| Visual Studio 2022 | IDE для Windows |
| CLion | C/C++ IDE для macOS |
| Docker Engine | Контейнеризация |
| Docker Compose | Управление контейнерами |
| PostgreSQL | Реляционная СУБД |
| MySQL | Реляционная СУБД |

---

## Архитектура окружения

### Windows

Windows
└── Visual Studio
    └── WSL2
        └── Ubuntu
            └── Docker
                ├── PostgreSQL
                └── MySQL

### macOS

macOS
├── CLion
└── Linux VM
    └── Ubuntu
        └── Docker
            ├── PostgreSQL
            └── MySQL