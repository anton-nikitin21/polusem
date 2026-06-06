# Поиск аномальных респондентов SoS

Решение запускается одной командой и создает папку `output/` с обязательными файлами:

```powershell
cd "C:\Users\user\Desktop\anomaly_solution_repo"
python .\solution_NikitinAntonPavlovich_SHCT-111.py
```

Эта команда работает, если папка `data_train` лежит рядом со скриптом, как в текущем репозитории:

```text
anomaly_solution_repo/
├── data_train/
├── solution_NikitinAntonPavlovich_SHCT-111.py
└── README.md
```

Если данные лежат в другом месте, укажите реальный путь к папке с parquet-файлами:

```powershell
cd "C:\Users\user\Desktop\anomaly_solution_repo"
python .\solution_NikitinAntonPavlovich_SHCT-111.py --input "C:\Users\user\Downloads\data_train"
```

## Выходные файлы

- `output/anomalies.csv` - уникальные пары `SubjectID, researchdate` для удаления.
- `output/anomaly_reasons.csv` - причины с колонками `SubjectID, researchdate, BrandID, Brand, CategoryDelivery, daily_ots, score, threshold, reason`.
- `output/plots/total_ots_before_after.png` - общий OTS до и после удаления по дням.
- `output/plots/category_ots_change.png` - изменение OTS по `CategoryDelivery`, %.
- `output/plots/daily_anomaly_count.png` - количество аномальных респондентов по дням.

## Дополнительные аналитические возможности

Построить графики до/после по демографии, ресурсам и категориям:

```powershell
cd "C:\Users\user\Desktop\anomaly_solution_repo"
python .\solution_NikitinAntonPavlovich_SHCT-111.py --make-analytics
```

Выгрузить поисковые запросы выбранного аномального респондента за день:

```powershell
cd "C:\Users\user\Desktop\anomaly_solution_repo"
python .\solution_NikitinAntonPavlovich_SHCT-111.py --query-subject 1729388589032331985 --query-date 2025-06-05
```

Построить изменение OTS по дням для выбранного бренда:

```powershell
cd "C:\Users\user\Desktop\anomaly_solution_repo"
python .\solution_NikitinAntonPavlovich_SHCT-111.py --brand-id 198484
```

## Примечания к данным

В файлах встречается колонка `CategoryNameDelivery`; скрипт приводит ее к требуемому имени `CategoryDelivery`. Для расчета `daily_ots = Weight(i, k) * count_rows(i, j, k)` используется медианный дневной вес по паре `SubjectID, researchdate`, потому что в небольшой части строк один respondent-day имеет два значения `Weight`. Это детерминированное правило не зависит от порядка строк.
