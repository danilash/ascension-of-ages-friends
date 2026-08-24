# Ascension of Ages 0.7.3.1

Готовая клиентская сборка для совместной игры.

## Что используется

* Minecraft: **1.21.1**
* NeoForge: **21.1.247**
* Java: **21**
* Ascension of Ages: **0.7.3.1**
* Лаунчер: **TLauncher**
* Сеть: **Radmin VPN**

Важно: не обновлять отдельные моды и не менять версию NeoForge.

## 1. Установить Java 21

Открыть PowerShell и выполнить:

```powershell
winget install EclipseAdoptium.Temurin.21.JDK
```

После установки закрыть PowerShell, открыть заново и проверить:

```powershell
java -version
```

Должно быть:

```text
openjdk version "21..."
```

## 2. Скачать и распаковать сборку

Скачай файл:

`Ascension-of-Ages-0.7.3.1.7z`

из раздела **Releases** репозитория.

По умолчанию браузер сохранит его в папку:

```text
C:\Users\<твой пользователь>\Downloads
```

### Установить 7-Zip

Открой **PowerShell** и выполни:

```powershell
winget install 7zip.7zip
```

Если 7-Zip уже установлен, этот шаг можно пропустить.

### Создать отдельную папку для сборки

```powershell
New-Item -ItemType Directory `
  -Path "C:\Minecraft\Ascension-of-Ages" `
  -Force
```

### Распаковать сборку

```powershell
& "C:\Program Files\7-Zip\7z.exe" x `
  "$env:USERPROFILE\Downloads\Ascension-of-Ages-0.7.3.1.7z" `
  -o"C:\Minecraft\Ascension-of-Ages" `
  -y
```

Дождись сообщения:

```text
Everything is Ok
```

### Проверить результат

```powershell
Get-ChildItem "C:\Minecraft\Ascension-of-Ages"
```

Должны присутствовать папки примерно такого вида:

```text
assets
config
configureddefaults
data
defaultconfigs
kubejs
mods
resourcepacks
shaderpacks
```

Проверить количество модов:

```powershell
(Get-ChildItem "C:\Minecraft\Ascension-of-Ages\mods\*.jar" -File).Count
```

Правильный результат:

```text
575
```

Если получилось `575`, сборка распакована правильно.


## 3. Скачать NeoForge 21.1.247

В PowerShell:

```powershell
$installer = "$env:TEMP\neoforge-21.1.247-installer.jar"

Invoke-WebRequest `
  -Uri "https://maven.neoforged.net/releases/net/neoforged/neoforge/21.1.247/neoforge-21.1.247-installer.jar" `
  -OutFile $installer
```

## 4. Подготовить профиль для NeoForge

Выполнить:

```powershell
'{"profiles":{},"settings":{}}' |
    Set-Content "C:\Minecraft\Ascension-of-Ages\launcher_profiles.json"
```

Затем:

```powershell
java -jar "$env:TEMP\neoforge-21.1.247-installer.jar" `
  --install-client "C:\Minecraft\Ascension-of-Ages"
```

В конце должно появиться:

```text
Successfully installed client into launcher.
```

## 5. Настроить TLauncher

Открыть настройки TLauncher.

Указать папку игры:

```text
C:\Minecraft\Ascension-of-Ages
```

Перезапустить TLauncher.

В списке версий выбрать:

```text
neoforge-21.1.247
```

Выделить игре около:

```text
10240 MB RAM
```

Галочка:

```text
Обновить клиент
```

должна быть **ВЫКЛЮЧЕНА**.

После этого запустить Minecraft.

Первый запуск может занимать несколько минут.

## 6. Проверка сборки

В папке:

```text
C:\Minecraft\Ascension-of-Ages\mods
```

должно быть **575 `.jar` файлов**.

Можно проверить:

```powershell
(Get-ChildItem "C:\Minecraft\Ascension-of-Ages\mods\*.jar" -File).Count
```

Ожидаемый результат:

```text
575
```

## 7. Игра через Radmin VPN

Все подключаются к одной сети Radmin VPN.

Хост создаёт мир и выбирает:

**Esc → Открыть для сети**

Minecraft покажет порт, например:

```text
Local game hosted on port 52341
```

Остальные открывают:

**Сетевая игра → Прямое подключение**

и вводят Radmin-IP хоста вместе с портом:

```text
26.x.x.x:52341
```

## Если что-то не работает

Сначала прислать вывод:

```powershell
java -version
```

```powershell
(Get-ChildItem "C:\Minecraft\Ascension-of-Ages\mods\*.jar" -File).Count
```

и скрин выбранной версии в TLauncher.

Правильная версия:

```text
neoforge-21.1.247
```
