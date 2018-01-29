---
title: "Справочник по API модели сбора данных для Машинного обучения Azure | Документация Майкрософт"
description: "Справочник по API модели сбора данных для Машинного обучения Azure."
services: machine-learning
author: aashishb
ms.author: aashishb
manager: neerajkh
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 09/12/2017
ms.openlocfilehash: 7a0fda8a44d13bcaba84b4124d9b693c05874154
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="azure-machine-learning-model-data-collection-api-reference"></a>Справочник по API модели сбора данных для Машинного обучения Azure

Функция сбора данных модели позволяет архивировать входные данные и прогнозы модели из веб-службы машинного обучения. Ознакомьтесь с [руководством по сбору данных модели](how-to-use-model-data-collection.md), чтобы узнать, как установить `azureml.datacollector` на компьютере под управлением Windows или Linux.

В этом справочном руководстве по API используется поэтапный подход к сбору входных данных и прогнозов модели из веб-службы машинного обучения.

## <a name="enable-model-data-collection-in-azure-ml-workbench-environment"></a>Включение сбора данных модели в среде Azure ML Workbench

 Найдите в проекте в папке aml_config файл conda\_dependencies.yml и включите в файл conda\_dependencies.yml модуль azureml.datacollector в разделе общедоступного IP-адреса, как показано ниже. Обратите внимание, что это только подраздел полного файла conda\_dependencies.yml:

    dependencies:
      - python=3.5.2
      - pip:
        - azureml.datacollector==0.1.0a13

>[!NOTE] 
>В настоящее время можно использовать модуль сборщика данных в среде Azure ML Workbench, запустив его в режиме docker. Локальный режим может не работать для всех сред.




## <a name="enable-model-data-collection-in-the-scoring-file"></a>Включение сбора данных модели в файле оценки

В файле оценки, который используется для ввода в эксплуатацию, импортируйте модуль сборщика данных и класс ModelDataCollector:

    from azureml.datacollector import ModelDataCollector


## <a name="model-data-collector-instantiation"></a>Установка сборщика данных модели
Создайте экземпляр ModelDataCollector:

dc = ModelDataCollector(model_name, identifier='default', feature_names=None, model_management_account_id='unknown', webservice_name='unknown', model_id='unknown', model_version='unknown')

Сведения о классе и параметрах:

### <a name="class"></a>Класс
| Имя | Описание |
|--------------------|--------------------|
| ModelDataCollector | Класс в пространстве имен azureml.datacollector. Экземпляр этого класса будет использоваться для сбора данных модели. Один файл оценки может содержать несколько ModelDataCollectors. Каждый экземпляр должен использоваться для сбора данных в одно отдельное расположение в файле оценки, чтобы схема собранных данных оставалась согласованной (то есть входные данные и прогнозирование).|


### <a name="parameters"></a>Параметры

| Имя | Тип | Описание |
|-------------|------------|-------------------------|
| model_name | string | Имя модели, для которой собираются данные. |
| Идентификатор | string | Расположение в коде, которое идентифицирует данные, т. е. RawInput или Prediction. |
| feature_names | Список строк | Список имен функций, которые становятся заголовками СSV-файла при поступлении. |
| model_management_account_id | string | Идентификатор учетной записи управления моделями, в котором хранится модель. Заполняется автоматически при введении в эксплуатацию моделей через Машинное обучение Azure. |
| webservice_name | string | Имя веб-службы, в которую в настоящее время выполняется развертывание этой модели. Заполняется автоматически при введении в эксплуатацию моделей через Машинное обучение Azure. |
| model_id | string | Уникальный идентификатор для этой модели в контексте учетной записи управления модели. Заполняется автоматически при введении в эксплуатацию моделей через Машинное обучение Azure. |
| model_version | string | Номер версии этой модели в контексте учетной записи управления моделями. Заполняется автоматически при введении в эксплуатацию моделей через Машинное обучение Azure. |



 

## <a name="collecting-the-model-data"></a>Сбор данных модели

Вы можете собирать данные модели с помощью экземпляра ModelDataCollector, созданного ранее.

    dc.collect(input_data, user_correlation_id="")

Подробности о методе и параметрах:

### <a name="method"></a>Метод
| Имя | Описание |
|--------------------|--------------------|
| collect | Используется для сбора данных для входных данных или прогноза модели.|


### <a name="parameters"></a>Параметры

| Имя | Тип | Описание |
|-------------|------------|-------------------------|
| input_data | несколько типов | Собираемые данные (сейчас принимает такие типы данных, как numpy.array, pandas.DataFrame, pyspark.sql.DataFrame). Для кадров данных, если есть заголовок с именами функций, эта информация будет включена в пункте назначения данных (без необходимости явно передавать имена функций в конструкторе ModelDataCollector). |
| user_correlation_id | string | Дополнительный идентификатор сопоставления, который может быть предоставлен пользователю для сопоставления прогноза. |

