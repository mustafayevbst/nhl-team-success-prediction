# NHL: предсказание успешности команды в следующем сезоне

Автор: Мустафаев Ниджат
Дата: 06.10.2026

## Задача

По итогам сезона `t` предсказать, окажется ли команда выше медианы по доле побед в сезоне `t+1`. Основная метрика ROC-AUC, дополнительно F1 и accuracy при пороге 0.5.

## Источники и инструменты

- Данные: https://www.scrapethissite.com/pages/forms/
- Python 3, Jupyter Notebook
- pandas, numpy, matplotlib, requests
- scikit-learn: Pipeline, SimpleImputer, StandardScaler, LogisticRegression, DummyClassifier
- Ассистент Claude для консультаций по коду и тексту

## Структура репозитория

- `nhl_team_success.ipynb` - ноутбук с решением и результатами
- `data/hockey_raw.csv` - исходная выгрузка с сайта
- `requirements.txt` - зависимости проекта

## Как воспроизвести

1. Установить зависимости: `pip install -r requirements.txt`.
2. Открыть ноутбук и запустить ячейки сверху вниз.
3. Раздел 1.1 заново собирает данные и сохраняет `data/hockey_raw.csv`.

## Кратко о решении

- Собрано 582 строки, 24 страницы, годы 1990-2011.
- Target: 1, если win_rate команды в `t+1` строго выше медианы всех команд в `t+1`.
- Split по `target_year`: train до 2005, validation 2006-2008, test 2009-2011.
- Финальная модель: логистическая регрессия с признаками `win_rate` и `goal_diff_pg`.
- Метрики: validation ROC-AUC 0.771, test ROC-AUC 0.759.