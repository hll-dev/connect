# ConnectGo Desktop

Официальный публичный канал выпусков ConnectGo для macOS, Linux и Windows. В
этом репозитории находятся только пользовательская документация и опубликованные
release-assets; исходный код приложения здесь не публикуется.

[Последний опубликованный выпуск](https://github.com/hll-dev/connect/releases/latest)

> Устанавливайте только версию, которая видна как опубликованный GitHub Release.
> Если раздел Releases пуст, публичной версии ConnectGo Desktop ещё нет, а ссылки
> на файлы ниже закономерно возвращают `404`. Не скачивайте сборки из других
> источников.

## Скачать версию 0.1.0

Файлы станут доступны только после публикации release
`connectgo-desktop-v0.1.0`:

- macOS, Apple Silicon и Intel:
  [`ConnectGo_0.1.0_universal.dmg`](https://github.com/hll-dev/connect/releases/download/connectgo-desktop-v0.1.0/ConnectGo_0.1.0_universal.dmg)
- Linux x86_64:
  [`ConnectGo_0.1.0_amd64.AppImage`](https://github.com/hll-dev/connect/releases/download/connectgo-desktop-v0.1.0/ConnectGo_0.1.0_amd64.AppImage)
- Windows x64:
  [`ConnectGo_0.1.0_x64-setup.exe`](https://github.com/hll-dev/connect/releases/download/connectgo-desktop-v0.1.0/ConnectGo_0.1.0_x64-setup.exe)

Windows MSI, Linux DEB/RPM и сборки Linux ARM64 в этот выпуск не входят.

## Системные требования и установка

- **macOS 12 или новее, Apple Silicon или Intel:** откройте DMG и перенесите
  `ConnectGo.app` в «Программы».
- **Linux x86_64:** требуется окружение с WebKitGTK 4.1 и рабочим FUSE 2
  (`libfuse2`, `/dev/fuse`). Сделайте AppImage исполняемым:
  `chmod +x ConnectGo_0.1.0_amd64.AppImage`, затем запустите его.
- **Windows 10/11 x64:** запустите NSIS-файл
  `ConnectGo_0.1.0_x64-setup.exe`. Проверенный WebView2 Fixed Version Runtime
  входит в установщик; отдельный online-bootstrapper не нужен.

Для входа, поиска, чата, актуальных расчётов, диктовки и обновлений требуется
HTTPS-доступ к сервисам Connect и GitHub.

## Что работает без сети

Интерфейс, локальные JS/CSS и базовые маршруты находятся внутри приложения и
запускаются без загрузки сайта. При плохой или отсутствующей сети приложение не
должно показывать ложный успешный результат: серверные функции переходят в
состояние ошибки/повтора. Авторизация, ответы поиска и чата, актуальные данные,
распознавание речи и проверка обновлений требуют сети.

## Автоматические обновления

Приложение проверяет публичный
[`latest.json`](https://github.com/hll-dev/connect/releases/latest/download/latest.json),
не блокируя запуск локального интерфейса. Обновление скачивается только после
подтверждения пользователя и устанавливается только после проверки встроенной
криптографической подписи. На macOS и Linux новая версия требует перезапуска; на
Windows установщик завершает приложение сам.

До появления второй опубликованной версии реальный переход `0.1.0 → 0.1.1` ещё
невозможно подтвердить на публичном канале; первый выпуск подтверждает только
контракт metadata/signature и установку свежего пакета.

## Проверка файла

В каждом выпуске публикуется
[`SHA256SUMS`](https://github.com/hll-dev/connect/releases/latest/download/SHA256SUMS).
Сравните SHA-256 скачанного файла со строкой его точного имени:

- macOS: `shasum -a 256 ConnectGo_0.1.0_universal.dmg`
- Linux: `sha256sum ConnectGo_0.1.0_amd64.AppImage`
- Windows PowerShell:
  `Get-FileHash .\ConnectGo_0.1.0_x64-setup.exe -Algorithm SHA256`

Несовпавший файл не запускайте.

## Конфиденциальность

Вход выполняется через Connect ID в системном браузере; OIDC-токены
desktop-приложение хранит только в памяти, а не в Web Storage. Несекретные
настройки и черновики могут храниться локально в отдельном WebView приложения.
Для входа, поиска, чата, актуальных данных и диктовки приложение обращается к
сервисам Connect; для проверки обновлений — к GitHub Releases. Микрофон
запрашивается только после действия пользователя; аудио передаётся для
распознавания при использовании диктовки и не включается в release-логи.

## Поддержка

Для проблем установки и обновления создайте
[публичный issue](https://github.com/hll-dev/connect/issues/new) и укажите версию
ConnectGo, ОС, архитектуру, шаги воспроизведения и фактический результат.

Issues публичны. Не публикуйте персональные данные, содержимое запросов или
чатов, аудио, пароли, токены и полные диагностические логи. Сведения об
уязвимости отправляйте только через
[приватный security report](https://github.com/hll-dev/connect/security/advisories/new),
а не через публичный issue.
