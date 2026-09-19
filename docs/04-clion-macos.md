# 04. Установка CLion на MacBook

[← Предыдущая](03-visual-studio-wsl2.md) · [Содержание](../README.md) · [Следующая →](05-linux-vm-macos.md)

## Требования

- Mac с Apple Silicon (M1–M4);
- поддерживаемая версия macOS;
- учётная запись и лицензия JetBrains либо доступное право на образовательную лицензию;
- доступ в Интернет.

## 1. Установка Xcode Command Line Tools

Откройте Terminal:

```bash
xcode-select --install
```

После установки проверьте:

```bash
clang --version
xcode-select -p
uname -m
```

Ожидаемая архитектура — `arm64`.

## 2. Установка CLion

Рекомендуемый вариант — JetBrains Toolbox:

1. Загрузите `.dmg` **для Apple Silicon** с сайта JetBrains Toolbox.
2. Перетащите Toolbox в каталог `Applications`.
3. Запустите Toolbox, войдите в JetBrains Account.
4. Найдите CLion и нажмите **Install**.

Можно установить CLion напрямую: загрузить Apple Silicon `.dmg`, открыть его и перетащить CLion в `Applications`.

## 3. Проверка toolchain

В CLion откройте **Settings → Build, Execution, Deployment → Toolchains**. Для macOS должны определиться:

- C compiler: Apple Clang;
- C++ compiler: Apple Clang++;
- CMake: bundled или системный;
- Build Tool: bundled Ninja;
- Debugger: bundled LLDB.


## 4. Тестовый проект

Создайте проект **C++ Executable**. Пример `main.cpp`:

```cpp
#include <iostream>

int main()
{
    std::cout << "Hello from macOS ARM64!\n";
    return 0;
}
```

Нажмите **Run**. Ожидаемый вывод:

```text
Hello from macOS ARM64!
```

Затем установите breakpoint и запустите **Debug**, чтобы проверить LLDB.

## Возможные проблемы

- **Скачана Intel-версия:** удалите её и установите вариант Apple Silicon.
- **Clang не найден:** повторите `xcode-select --install`; после обновления macOS инструменты иногда нужно переустановить.
- **Toolchain отмечен красным:** проверьте пути в настройках и перезапустите CLion после установки Command Line Tools.
- **Нет лицензии:** проверьте условия [JetBrains Student Pack](https://www.jetbrains.com/community/education/#students).

## Источники

- [JetBrains — установка CLion](https://www.jetbrains.com/help/clion/installation-guide.html)
- [JetBrains — настройка CLion на macOS](https://www.jetbrains.com/help/clion/quick-tutorial-on-configuring-clion-on-macos.html)

