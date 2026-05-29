# os-mysql-to-sheets

## Краткое описание

Выгрузка данных из MySQL в Google Sheets для воронок ОС: функция готовит таблицы для операционной работы и контроля показателей.

## Назначение

Выгрузки из БД cploud для воронок ОС

## Параметры функции

- ID функции: `d4epvu78s1sm9ji56omk`
- Каталог Yandex Cloud: `sl`
- Статус: `ACTIVE`
- Runtime: `python314`
- Entry point: `index.handler`
- Версий в экспорте: `4`
- HTTP URL: `https://functions.yandexcloud.net/d4epvu78s1sm9ji56omk`

## Триггеры

- `os-leads-export` (`a1s6aorfma2qk07k4ov3`), статус: `ACTIVE`, cron: `0 */4 ? * * *`

## Переменные окружения

Значения не хранятся в sanitized-экспорте. Реальные значения находятся только в raw/, эту папку нельзя коммитить в GitHub.

- `GOOGLE_CLIENT_EMAIL`
- `GOOGLE_PRIVATE_KEY`

Пример .env:

```dotenv
GOOGLE_CLIENT_EMAIL=<set-value>
GOOGLE_PRIVATE_KEY=<set-value>
```

## Локальный запуск

```powershell
cd .\yc-export-author-gilach\sanitized\functions\os-mysql-to-sheets
# Положи исходники функции в эту папку: index.py, requirements.txt и остальные файлы.
# Создай .env по примеру выше и event.json с тестовым событием.
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python -c "import json, index; event=json.load(open('event.json', encoding='utf-8')); print(index.handler(event, None))"
```

Если локально нет версии Python, совпадающей с runtime `python314`, используй ближайшую совместимую версию только после проверки зависимостей.

Минимальный event.json для ручной проверки:

```json
{}
```

## Деплой новой версии

Перед деплоем проверь, что в папке лежат исходники функции и файл с зависимостями (`package.json` для Node.js или `requirements.txt` для Python).

```powershell
yc serverless function version create --function-id d4epvu78s1sm9ji56omk --runtime python314 --entrypoint index.handler --source-path . --execution-timeout 60s
```

Если функции нужны переменные окружения, передавай их через `--environment` или настрой через консоль/секреты. Не коммить реальные токены, пароли, webhook URL и сертификаты в GitHub.

## Файлы экспорта

- `function.json` - описание функции.
- `versions.json` - версии функции с замаскированными значениями переменных окружения.