# cristalix-wl-fix
Скрипт запуска Cristalix, исправляющий проблемы на Wayland с видеокартами NVIDIA.

Данный скрипт загружает [оффициальный лаунчер Cristalix](https://cristalix.gg/content/launcher/Cristalix.jar) и применяет переменную `__GL_THREADED_OPTIMIZATIONS=0`, чтоб игра работала с Wayland на вашей NVIDIA 

## Требования
- **Java:** Установленная в системе JDK 21+ (Например, Cristalix рекомендует [BellSoft Liberica JDK](https://bell-sw.com/pages/downloads/#jdk-21-lts)).

## Установка
### `.AppImage`
1. Загрузите `cristalix.appimage` с [последнего релиза](https://github.com/maseckt/cristalix-wl-fix/releases/latest).
2. Выдайте файлу права на исполнение:
```sh
chmod +x cristalix.appimage
```
3. Запустите файл:
```sh
./cristalix.appimage
```
Если хотите быстро сделать ярлык в `~/.local/share/applications/`, воспользуйтесь [GearLever](https://github.com/mijorus/gearlever).

### `.pkg.tar.zst` (ArchLinux)
1. Загрузите `cristalix-wl-fix-1.0.0-1-any.pkg.tar.zst`.
2.  Установите пакет:
```sh
sudo pacman -U cristalix-wl-fix-1.0.0-1-any.pkg.tar.zst
```
3. Запустите скрипт:
```sh
cristalix
```
(Или из вашего меню приложений)

## Дополнительные параметры
Вы можете явно указать путь к бинарнику Java, вместо дефултной (из `/usr/lib/jvm/`), например для BellSoft Liberica:

```sh
./cristalix.appimage --jdk=/usr/lib/jvm/liberica-jdk-21/bin/java
```

## Важное примечание
При потере фокуса окна композитор замораживает отправку frame-событий. При включенном VSync графический поток блокируется, за ним засыпает основной поток Java, а внутренний тайм-аут (`Watchdog`) убивает клиент, считая это намертво зависшим процессом.

Начиная с версии `1.0.1`, вертикальная синхронизация принудительно отключена. Переменные `vblank_mode=0` и `__GL_SYNC_TO_VBLANK=0` интегрированы в обертку для обхода этих архитектурных ограничений Wayland + Xwayland.

## Сборка
### AppImage
Для сборки AppImage самостоятельно из исходников:
1. Склонируйте исходники из репозитория:
```sh 
git clone https://github.com/maseckt/cristalix-wl-fix.git
```
2. Установите утилиту `appimagetool`. Например, в ArchLinux:
```sh
paru/yay -S appimagetool-bin
```
3. Перейдите в директорию, где лежит склонированный репозиторий и дайте права на исполнение скрипту:
```sh
chmod +x Cristalix.AppDir/AppRun
```
4. Соберите AppImage при помощи `appimagetool`:
```sh
ARCH=x86_64 appimagetool Cristalix.AppDir cristalix.appimage
```


## Проблемы
При возникновении каких-либо проблем, обязательно пишите в [Issues](https://github.com/maseckt/cristalix-wl-fix/issues)!

<details>
<summary><b>Если вы используете оконный менеджер</b></summary>
  Если вы используете оконный менеджер, окно лаунчера может не очень красиво растягиваться.
  
  Чтобы исправить эту проблему, сделайте окно в режиме `float` с размерами `1220x650`.
  
  Пример для Hyprland 0.55+:
  ```lua
  hl.window_rule({
    name   = "Cristalix-float",
    match  = {
        title = "^(Cristalix)$",
               xwayland = true
    },
    float  = true,
    size   = {1220, 650},
    center = true
})
  ```
  Для Hyprland 0.54
  ```conf
  windowrule {
    name = Cristalix-float
    match:title = ^(Cristalix)$
    match:xwayland = 1
    float = on
    size = 1220 650
    center = on
  }
  ```
</details>
