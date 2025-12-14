# S03 – eda_cli: мини-EDA для CSV

Небольшое CLI-приложение для базового анализа CSV-файлов.
Используется в рамках Семинара 03 курса «Инженерия ИИ».

## Требования

- Python 3.11+
- [uv](https://docs.astral.sh/uv/) установлен в систему

## Инициализация проекта

В корне проекта (S03):

```bash
uv sync
```

Эта команда:

- создаст виртуальное окружение `.venv`;
- установит зависимости из `pyproject.toml`;
- установит сам проект `eda-cli` в окружение.

## Запуск CLI

### Краткий обзор

```bash
uv run eda-cli overview data/example.csv
```

Параметры:

- `--sep` – разделитель (по умолчанию `,`);
- `--encoding` – кодировка (по умолчанию `utf-8`).

### Полный EDA-отчёт

```bash
uv run eda-cli report data/example.csv --out-dir reports
```

В результате в каталоге `reports/` появятся:

- `report.md` – основной отчёт в Markdown;
- `summary.csv` – таблица по колонкам;
- `missing.csv` – пропуски по колонкам;
- `correlation.csv` – корреляционная матрица (если есть числовые признаки);
- `top_categories/*.csv` – top-k категорий по строковым признакам;
- `hist_*.png` – гистограммы числовых колонок;
- `missing_matrix.png` – визуализация пропусков;
- `correlation_heatmap.png` – тепловая карта корреляций.

Параметры (дополнительно к overview)

- `--title` - заголовок отчёта (по умолчанию `Общий большой EDA-отчёт для набора данных`)
- `--min-missing-share` - порог пропусков, при котором колонка считается проблемной (по умолчанию `0.03`).
- `--graphics/--no-graphics` - необходимо ли создавать графики для отчёта (по умолчанию `--graphics`)
- `--help` - показывает список возможных команд

Примеры запуска:
```bash
uv run eda-cli report data/example.csv --out-dir reports --min-missing-share 0.01 --no-graphics
uv run eda-cli report data/example.csv --out-dir reports --title Это очень важный отчёт
uv run eda-cli report --help
```

## Тесты

```bash
uv run pytest -q
```
