# SoS — Survey Anomaly Detection

Я исследовал аномальных респондентов: реализовал обработку Parquet, расчёт OTS, робастные статистики и объяснение причин исключения.

## Запуск

```bash
python -m venv .venv
# Активируйте .venv для своей системы
pip install -r requirements.txt
python solution_NikitinAntonPavlovich_SHCT-111.py --input data_train
```

Все доступные параметры: `python solution_NikitinAntonPavlovich_SHCT-111.py --help`.

## Результаты

- `output/anomalies.csv`: пары респондент–дата для проверки.
- `output/anomaly_reasons.csv`: основания обнаруженных аномалий.
- `output/plots/`: графики OTS до и после обработки и дополнительная аналитика.
- `algorithm_description.md`: описание алгоритма и его допущений.

Дополнительные графики: запуск с `--make-analytics`. Запросы выбранного респондента: параметры `--query-subject` и `--query-date`. Анализ бренда: `--brand-id`.

В этом репозитории я сохраняю исходную версию исследования с данными и результатами. Для просмотра только кода и документации используйте [survey-anomaly-detection](https://github.com/anton-nikitin21/survey-anomaly-detection).

[Полное портфолио](https://github.com/anton-nikitin21)

## Автор

Антон Никитин — [anton-nikitin21](https://github.com/anton-nikitin21).
