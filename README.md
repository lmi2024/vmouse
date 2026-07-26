Клавиатурный эмулятор мыши
===

Экстремально простой эмулятор мыши для тех, у кого аллергия на реальную.

Написан на си, никаких зависимостей кроме ядра и стандартной библиотеки.

Пригоден в качестве one-shot утилиты.

---

Данный репозиторий является зеркалом текущего релиза [fossil репозитория](http://vmouse.plumbus.online).

---

# Лицензия

[GNU Affero GPL version 3 or later](http://www.gnu.org/licenses/agpl-3.0.html).

# Зависимости

- Ядро Linux 4.0+
- libc

# Что есть
- перемещение курсора при нажатии клавиш движения
- перемещение курсора с ускорением при удержании клавиш движения
- опциональный монопольный захват всех клавиатур системы
- нажатия ЛКМ, ПКМ
- конфигурация с помощью констант препроцессора

# Чего нет
- координатной сетки
- конфигурации после компиляции

# Установка

Готовые бинарные файлы не публикуются, предполагается, что пользователь в состоянии собрать программу с нужными ему опциями и флагами.

1. скачать и распаковать [архив истодного кода](https://github.com/lmi2024/vmouse/releases/download/latest/release.tar.gz)
    ```
    curl \
        -sL https://github.com/lmi2024/vmouse/releases/download/latest/release.tar.gz \
        | tar -xzf - --strip-components=1
    ```

1. если установлен [nix package manager](https://github.com/nixos/nix) и включены [flakes](https://nixos.wiki/wiki/Flakes)
    ```
    nix develop

    PATH="$PATH:$PWD/.redodist" \
    TARGET="$HOME/.local/bin/vmouse" \
    redo install
    ```

1. иначе необходим компилятор (clang/gcc/tcc/etc.) и ar (binutils)
    ```
    PATH="$PATH:$PWD/.redodist" \
    CC="tcc" \
    CFLAGS="" \
    LDFLAGS="" \
    TARGET="$HOME/.local/bin/vmouse" \
    redo install
    ```

    > для статической сборки необходим libc.a в системе и LDFLAGS="-static"

1. для запуска без прав суперпользователя необходимо, чтобы пользователь входил в группу input

    ```
    sudo usermod -aG input $USER
    ```

# Настройка

Любым удобным способом до/во время компиляция задать константы

```
#define UP                      KEY_UP
#define DOWN                    KEY_DOWN
#define LEFT                    KEY_LEFT
#define RIGHT                   KEY_RIGHT
#define LBUTTON                 KEY_1
#define RBUTTON                 KEY_2
#define GRAB                    1           /* монопольный захват клавиатур */
#define POLL_TIMEOUT_MS         30          /* максимальное время ожидания нажатий */
#define WAIT_KEYS_RELEASED_MS   200         /* задержка перед захватом клавиатур (если он требуется) */
```

# Альтернативы

1. [ydotool](https://github.com/ReimuNotMoe/ydotool)
1. [warpd](https://github.com/rvaiya/warpd)


# Используемые компоненты

## Система сборки [redo – bourne shell implementation of DJB redo](http://news.dieweltistgarnichtso.net/bin/redo-sh.html)

**Автор**: Copyright © 2014-2025 Ælla Chiana Moskopp (erle)

**Лицензия**: GNU Affero GPL version 3 or later <http://www.gnu.org/licenses/agpl-3.0.html>
