# Ascension of Ages 0.7.3.1 — Friends Pack

Готовая клиентская сборка для совместной игры.

## Версии

* Minecraft: **1.21.1**
* Ascension of Ages: **0.7.3.1**
* NeoForge: **21.1.247**
* Java: **21**
* Лаунчер: **TLauncher**
* Сеть: **Radmin VPN**

> **Важно:** не обновлять отдельные моды, NeoForge или другие компоненты сборки.
> В TLauncher галочка **«Обновить клиент» должна быть выключена**.

---

# 1. Установить Java 21

Открой PowerShell и выполни:

```powershell
winget install EclipseAdoptium.Temurin.21.JDK
```

После установки **закрой PowerShell и открой заново**.

Проверь:

```powershell
java -version
```

Должно быть что-то вроде:

```text
openjdk version "21..."
```

---

# 2. Скачать и распаковать сборку

Открой раздел **Releases** этого репозитория и скачай:

```text
Ascension-of-Ages-0.7.3.1.7z
```

По умолчанию файл должен оказаться здесь:

```text
C:\Users\<твой пользователь>\Downloads
```

## Проверить скачанный архив

В PowerShell:

```powershell
Get-FileHash `
  "$env:USERPROFILE\Downloads\Ascension-of-Ages-0.7.3.1.7z" `
  -Algorithm SHA256
```

Правильный SHA256:

```text
B5630C70097E4C0D2DDD0BF86B482E1E4815E2B45D6720844FB0AE75AA41355A
```

Если хэш совпадает — архив скачан правильно.

## Установить 7-Zip

```powershell
winget install 7zip.7zip
```

Если 7-Zip уже установлен, этот шаг можно пропустить.

## Создать папку игры

```powershell
New-Item `
  -ItemType Directory `
  -Path "C:\Minecraft\Ascension-of-Ages" `
  -Force
```

## Распаковать сборку

```powershell
& "C:\Program Files\7-Zip\7z.exe" x `
  "$env:USERPROFILE\Downloads\Ascension-of-Ages-0.7.3.1.7z" `
  -o"C:\Minecraft\Ascension-of-Ages" `
  -y
```

Дождись:

```text
Everything is Ok
```

## Проверить распаковку

```powershell
Get-ChildItem "C:\Minecraft\Ascension-of-Ages"
```

Должны быть папки:

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

Проверяем количество модов:

```powershell
(Get-ChildItem "C:\Minecraft\Ascension-of-Ages\mods\*.jar" -File).Count
```

Правильный результат:

```text
575
```

---

# 3. Установить NeoForge 21.1.247

Скачать официальный установщик:

```powershell
$installer = "$env:TEMP\neoforge-21.1.247-installer.jar"

Invoke-WebRequest `
  -Uri "https://maven.neoforged.net/releases/net/neoforged/neoforge/21.1.247/neoforge-21.1.247-installer.jar" `
  -OutFile $installer
```

Подготовить файл профиля:

```powershell
'{"profiles":{},"settings":{}}' |
  Set-Content `
    "C:\Minecraft\Ascension-of-Ages\launcher_profiles.json" `
    -Encoding ASCII
```

Установить NeoForge:

```powershell
java -jar "$env:TEMP\neoforge-21.1.247-installer.jar" `
  --install-client "C:\Minecraft\Ascension-of-Ages"
```

Установка может занять некоторое время.

В конце должно появиться:

```text
Successfully installed client into launcher.
```

---

# 4. Настроить TLauncher

Открой настройки TLauncher.

В качестве папки игры укажи:

```text
C:\Minecraft\Ascension-of-Ages
```

После изменения папки **полностью перезапусти TLauncher**.

В списке версий выбери:

```text
neoforge-21.1.247
```

Выдели игре:

```text
10240 MB RAM
```

Убедись, что:

```text
Обновить клиент
```

**ВЫКЛЮЧЕНО.**

После этого запускай игру.

> Первый запуск очень долгий. Экран **Ascension Awaits** может несколько минут выглядеть зависшим. Не закрывай игру сразу — сборка содержит 575 модов.

Если Windows спросит разрешение для **Java / OpenJDK / Minecraft** в брандмауэре — разреши доступ как минимум для **частных сетей**.

---

# 🇷🇺 Русская локализация — временно

> **Примечание:** русская локализация пока находится в финальной доработке, но основные книги и квесты уже переведены и ей можно пользоваться.
>
> После завершения проверки этот раздел будет обновлён.

Чтобы не пересобирать и заново не скачивать весь архив `Ascension-of-Ages-0.7.3.1.7z` из-за нескольких файлов локализации, русский перевод пока устанавливается отдельно из GitHub.

Репозиторий сборки для друзей:

```text
https://github.com/danilash/ascension-of-ages-friends
```

Актуальная локализация:

```text
https://github.com/danilash/ascension-of-ages-public/tree/russian-localization
```

## Установить локализацию

Полностью закрой Minecraft.

Открой PowerShell и выполни:

```powershell
$game = "C:\Minecraft\Ascension-of-Ages"

New-Item -ItemType Directory -Force `
  "$game\kubejs\assets\kubejs\lang" | Out-Null

New-Item -ItemType Directory -Force `
  "$game\kubejs\assets\aoa\lang" | Out-Null

New-Item -ItemType Directory -Force `
  "$game\config\ftbquests\quests\lang" | Out-Null

Invoke-WebRequest `
  -Uri "https://raw.githubusercontent.com/danilash/ascension-of-ages-public/russian-localization/kubejs/assets/kubejs/lang/ru_ru.json" `
  -OutFile "$game\kubejs\assets\kubejs\lang\ru_ru.json"

Invoke-WebRequest `
  -Uri "https://raw.githubusercontent.com/danilash/ascension-of-ages-public/russian-localization/kubejs/assets/aoa/lang/ru_ru.json" `
  -OutFile "$game\kubejs\assets\aoa\lang\ru_ru.json"

Invoke-WebRequest `
  -Uri "https://raw.githubusercontent.com/danilash/ascension-of-ages-public/russian-localization/config/ftbquests/quests/lang/ru_ru.snbt" `
  -OutFile "$game\config\ftbquests\quests\lang\ru_ru.snbt"
```

Команды сразу скачают актуальные файлы локализации в установленную сборку.

## Проверить установку

В PowerShell:

```powershell
Get-Item `
  "C:\Minecraft\Ascension-of-Ages\kubejs\assets\kubejs\lang\ru_ru.json", `
  "C:\Minecraft\Ascension-of-Ages\kubejs\assets\aoa\lang\ru_ru.json", `
  "C:\Minecraft\Ascension-of-Ages\config\ftbquests\quests\lang\ru_ru.snbt"
```

Должны отобразиться все три файла.

После этого запусти Minecraft и выбери:

**Настройки → Язык → Русский**

Рекомендуется после смены языка один раз полностью перезапустить игру.

Русская локализация сейчас включает:

* стартовую книгу;
* книги всех эпох;
* FTB Quests.

Некоторые названия модов, машин, предметов и боссов специально оставлены на английском, чтобы их можно было без проблем найти в EMI.

## Обновить локализацию

Если вышло обновление перевода, Minecraft нужно закрыть и просто **повторно выполнить блок команд из пункта «Установить локализацию»**.

Старые файлы будут заменены актуальными версиями из ветки `russian-localization`.

---

# 5. Игра через Radmin VPN

Все игроки должны подключиться к одной сети в Radmin VPN.

Хост заходит в мир и выбирает:

**Esc → Открыть для сети**

Minecraft покажет сообщение примерно такого вида:

```text
Local game hosted on port 52341
```

Порт при следующем запуске мира может быть другим.

Посмотри свой IP в Radmin VPN. Он выглядит примерно так:

```text
26.x.x.x
```

Другие игроки открывают:

**Сетевая игра → Прямое подключение**

и вводят:

```text
26.x.x.x:52341
```

где:

```text
26.x.x.x
```

— Radmin-IP хоста, а:

```text
52341
```

— порт, который Minecraft показал после открытия мира для сети.

---

# Если не работает

Проверить Java:

```powershell
java -version
```

Нужна:

```text
Java 21
```

Проверить моды:

```powershell
(Get-ChildItem "C:\Minecraft\Ascension-of-Ages\mods\*.jar" -File).Count
```

Должно быть:

```text
575
```

Проверить NeoForge:

В TLauncher должна быть выбрана версия:

```text
neoforge-21.1.247
```

Проверить соединение с хостом через Radmin VPN:

```powershell
ping 26.x.x.x
```

Если игра вылетает — прислать:

```text
C:\Minecraft\Ascension-of-Ages\logs\latest.log
```

Если появился crash-report — также прислать последний файл из:

```text
C:\Minecraft\Ascension-of-Ages\crash-reports
```
