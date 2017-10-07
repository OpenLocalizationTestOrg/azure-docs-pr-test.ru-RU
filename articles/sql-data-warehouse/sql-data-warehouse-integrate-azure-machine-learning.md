---
title: "aaaUse машинного обучения Azure с хранилищем данных SQL | Документы Microsoft"
description: "Учебник по использованию машинного обучения Azure с хранилищем данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a>Использование машинного обучения Azure с хранилищем данных SQL
Машинное обучение Azure является службой полностью управляемая прогнозирующего анализа, можно использовать toocreate прогнозных моделей для данных в хранилище данных SQL, а затем опубликовать как готовые к использованию веб-службы. Вы можете основы hello прогнозирующего анализа и машинное обучение, считывая [tooMachine введение обучения в Azure][Introduction tooMachine Learning on Azure].  Затем рассказывается, как toocreate, обучение, оценки и тестирования модели машинного обучения с помощью hello [создать эксперимент учебника][Create experiment tutorial].

В этой статье вы узнаете, как после с помощью hello hello toodo [студии машинного обучения Azure][Azure Machine Learning Studio]:

* Чтение данных из вашей базы данных toocreate, обучения и оценки прогнозной модели
* Запись tooyour базы данных

## <a name="read-data-from-sql-data-warehouse"></a>Чтение данных из хранилища данных SQL
Мы будет считывать данные из таблицы Product базы данных AdventureWorksDW hello.

### <a name="step-1"></a>Шаг 1
Запустите новый эксперимент, установив + NEW hello нижней части окна студии машинного обучения hello выберите ЭКСПЕРИМЕНТА, а затем выберите пустой поэкспериментировать. По умолчанию выберите hello поэкспериментировать имя hello верхней части холста hello и переименуйте его toosomething осмысленное, например, велосипед цена прогноза.

### <a name="step-2"></a>Шаг 2
Найдите модуль считывания hello в палитре hello наборов данных и модули hello левой стороны холст эксперимента hello. Перетащите холст эксперимента toohello модуль hello.
![][drag_reader]

### <a name="step-3"></a>Шаг 3.
Выберите модуль чтения hello и заполните hello панели «Свойства».

1. Выберите базу данных SQL Azure в качестве hello источника данных.
2. Имя сервера базы данных: имя сервера типа hello. Можно использовать hello [портал Azure] [ Azure portal] toofind это.

![][server_name]

1. Имя базы данных: имя типа hello базы данных на сервере hello, только что указали.
2. Имя учетной записи пользователя сервера: Введите hello имя пользователя учетной записи, которая имеет разрешения на доступ к базе данных hello.
3. Пароль учетной записи пользователя сервера: указать пароль hello для hello указанную учетную запись пользователя.
4. Принимать любой сертификат сервера: используйте этот параметр (менее безопасный), если требуется, чтобы tooskip Просмотр сертификата сайта hello перед чтением данных.
5. Запрос базы данных: Введите инструкцию SQL, описывающий hello данные tooread. В этом случае будет считывать данные из таблицы продукта, с помощью приветствия при следующем запросе.

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a>Шаг 4.
1. Запустите эксперимент hello командой выполнить под холст эксперимента hello.
2. По завершении эксперимента hello модуль считывания hello будет tooindicate Зеленый флажок, который успешно завершена. Обратите внимание также hello завершен текущий статус в правом верхнем углу hello.

![][run]

1. toosee hello импортированных данных щелкните порт вывода hello внизу hello автомобиль hello набора данных и выберите визуализировать.

## <a name="create-train-and-score-a-model"></a>Создание, обучение и оценка модели
Теперь этот набор данных можно использовать для выполнения следующих задач.

* Создание модели: обработка данных и задание параметров
* Обучение модели hello: Выбор и применение алгоритма обучения
* Оценка и тестирования hello модели: прогнозирования новая цена велосипеда

![][model]

Дополнительные о toocreate, обучение, оценки и тестирования машинного обучения модели используйте hello toolearn [создать эксперимент учебника][Create experiment tutorial].

## <a name="write-data-tooazure-sql-data-warehouse"></a>Запись данных tooAzure хранилище данных SQL
Мы напишем hello результирующий набор tooProductPriceForecast таблицы базы данных AdventureWorksDW hello.

### <a name="step-1"></a>Шаг 1
Найдите модуль записи hello в палитре hello наборов данных и модули hello левой стороны холст эксперимента hello. Перетащите холст эксперимента toohello модуль hello.

![][drag_writer]

### <a name="step-2"></a>Шаг 2
Выберите модуль записи hello и заполните hello панели «Свойства».

1. Выберите базы данных SQL Azure в качестве назначения данных hello.
2. Имя сервера базы данных: имя сервера типа hello. Можно использовать hello [портал Azure] [ Azure portal] toofind это.
3. Имя базы данных: имя типа hello базы данных на сервере hello, только что указали.
4. Имя учетной записи пользователя сервера: Введите hello имя пользователя учетной записи, которая имеет разрешения на запись для базы данных hello.
5. Пароль учетной записи пользователя сервера: указать пароль hello для hello указанную учетную запись пользователя.
6. Принимать любой сертификат сервера (небезопасно): выберите этот параметр, если вы не хотите tooview hello сертификата.
7. Список с разделителями запятыми столбцов toobe сохранен: предоставлять список столбцов набора данных или результат hello, которые должны toooutput.
8. Имя таблицы данных: укажите имя hello hello данных таблицы.
9. Список с разделителями запятыми столбцов datatable: Укажите имена toouse hello столбец в новой таблице hello. Hello имена столбцов может отличаться от hello из них в hello исходный набор данных, но необходимо перечислить hello одинаковое количество столбцов здесь, определяемый для hello выходной таблицы.
10. Количество строк, записываемых за одну операцию SQL Azure: можно настроить hello количество строк, которые записываются tooa базы данных SQL за одну операцию.

![][writer_properties]

### <a name="step-3"></a>Шаг 3.
1. Запустите эксперимент hello командой выполнить под холст эксперимента hello.
2. По завершении эксперимента hello всех модулей будет tooindicate Зеленый флажок, который успешно завершена.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
