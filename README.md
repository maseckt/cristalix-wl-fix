# cristalix-wl-fix
Скрипт запуска Cristalix на Wayland с видеокартами NVIDIA.


## Требования
- **Java:** Установленная в системе JDK 21+ (Cristalix рекомендует [BellSoft Liberica JDK](https://bell-sw.com/pages/downloads/#jdk-21-lts)).


## Установка
1. Загрузите `cristalix.appimage` с [последнего релиза](https://github.com/maseckt/cristalix-wl-fix/releases/latest).
2. Выдайте файлу права на исполнение:
```sh
chmod +x cristalix.appimage
```
3. Запустите приложение:
```sh
./cristalix.appimage
```
Или используйте [GearLever](https://github.com/mijorus/gearlever), чтоб быстро добавить ярлык игры в `~/.local/share/applications/`.


## Дополнительные параметры
Скрипт умеет автоматически искать Java (в `/usr/lib/jvm/`), но вы можете явно указать путь к бинарнику Java, например для BellSoft Liberica:

```sh
./cristalix.appimage --jdk=/usr/lib/jvm/liberica-jdk-21/bin/java
```

## Сборка AppImage
Если вы хотите собрать AppImage самостоятельно из исходников:
1. Склонируйте исходники из репозитория:
```sh 
git clone https://github.com/maseckt/cristalix-wl-fix.git
```
2. Установите утилиту `appimagetool`. Например, в ArchLinux:
```sh
paru -S appimagetool-bin
```
или 
```sh
yay -S appimagetool-bin
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
