---
title: "Примеры преобразований потока данных, поддерживаемых в средстве подготовки данных службы машинного обучения Azure | Документация Майкрософт"
description: "В этой статье приведены примеры преобразований потока данных, поддерживаемых в средстве подготовки данных службы машинного обучения Azure."
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.custom: 
ms.devlang: 
ms.topic: article
ms.date: 09/11/2017
ms.openlocfilehash: 4a716c1934258e687eb48ecb4077c6be7b269c1f
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/04/2018
---
# <a name="sample-of-custom-data-flow-transforms-python"></a>Пример пользовательских преобразований потока данных (Python) 
Имя преобразования в меню — **Преобразование потока данных (скрипт)**. Перед ознакомлением с этим приложением см. [общие сведения о расширяемости Python](data-prep-python-extensibility-overview.md).

## <a name="transform-frame"></a>Преобразование блока данных
### <a name="create-a-new-column-dynamically"></a>Динамическое создание столбца 
Динамическое создание столбца **city2** и сопоставление нескольких разных версий Сан-Франциско с одной в существующем столбце городов.
```python
    df.loc[(df['city'] == 'San Francisco') | (df['city'] == 'SF') | (df['city'] == 'S.F.') | (df['city'] == 'SAN FRANCISCO'), 'city2'] = 'San Francisco'
```

### <a name="add-new-aggregates"></a>Добавление новых статистических выражений
Создание блока данных на основе первого и последнего статистических выражений, вычисляемых для столбца результатов. Они сгруппированы по столбцу **risk_category**.
```python
    df = df.groupby(['risk_category'])['Score'].agg(['first','last'])
```
### <a name="winsorize-a-column"></a>Винсоризация столбца 
Изменение данных в соответствии с формулой для сокращения выбросов в столбце.
```python
    import scipy.stats as stats
    df['Last Order'] = stats.mstats.winsorize(df['Last Order'].values, limits=0.4)
```

## <a name="transform-data-flow"></a>Преобразование потока данных
### <a name="fill-down"></a>Заполнение по направлению вниз 
Заполнение по направлению вниз выполняется на основе двух преобразований. Предполагается, что данные выглядят так:


|Состояние         |City       |
|--------------|-----------|
|Вашингтон    |Редмонд    |
|              |Бельвью   |
|              |Иссакуа   |
|              |Сиэтл;    |
|Калифорния    |Лос-Анджелес|
|              |San Diego  |
|              |Сан-Хосе   |
|Техас         |Даллас     |
|              |Сан-Антонио|
|              |Хьюстон    |

Прежде всего создайте преобразование "Добавление столбцов (скрипт)", содержащее следующий код:
```python
    row['State'] if len(row['State']) > 0 else None
```
Теперь создайте преобразование "Преобразование потока данных (скрипт)", содержащее следующий код:
```python
    df = df.fillna( method='pad')
```

Теперь данные выглядят так:

|Состояние         |Новое_состояние         |City       |
|--------------|--------------|-----------|
|Вашингтон    |Вашингтон    |Редмонд    |
|              |Вашингтон    |Бельвью   |
|              |Вашингтон    |Иссакуа   |
|              |Вашингтон    |Сиэтл;    |
|Калифорния    |Калифорния    |Лос-Анджелес|
|              |Калифорния    |San Diego  |
|              |Калифорния    |Сан-Хосе   |
|Техас         |Техас         |Даллас     |
|              |Техас         |Сан-Антонио|
|              |Техас         |Хьюстон    |


### <a name="min-max-normalization"></a>Мин макс нормализации
```python
    df["NewCol"] = (df["Col1"]-df["Col1"].mean())/df["Col1"].std()
```