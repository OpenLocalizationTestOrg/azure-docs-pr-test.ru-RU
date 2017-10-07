---
title: "aaaGet работает с аналитики Озера данных Azure, с помощью портала Azure | Документы Microsoft"
description: "Узнайте, как создать задание аналитики Озера данных с помощью U-SQL toouse hello Azure портала toocreate учетную запись аналитики Озера данных и отправить задание hello. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a>Начало работы с Azure Data Lake Analytics с помощью портала Azure
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Узнайте, как toouse hello учетных записей Azure портала toocreate аналитики Озера данных Azure, определить задания в [U-SQL](data-lake-analytics-u-sql-get-started.md)и служба аналитики Озера данных toohello задания отправки. Дополнительные сведения о Data Lake Analytics см. в [обзоре Azure Data Lake Analytics](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Предварительные требования

Прежде чем приступать к изучению этого руководства, необходимо оформить **подписку Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-data-lake-analytics-account"></a>Создание учетной записи аналитики озера данных

Теперь вы создадите аналитики Озера данных и хранилище Озера данных учетной записи в hello же время.  Этот шаг является простым и только занимает около toofinish 60 секунд.

1. Войдите на toohello [портал Azure](https://portal.azure.com).
2. Щелкните **Создать** >  **Данные+аналитика** > **Data Lake Analytics**.
3. Выберите значения для hello следующих элементов:
   * **Имя**: имя учетной записи Data Lake Analytics (разрешены только строчные буквы и цифры).
   * **Подписки**: выберите hello подписку Azure, используемую для hello Analytics учетной записи.
   * **Группа ресурсов**: выберите существующую группу ресурсов Azure или создайте новую группу. Обычно приложения состоят из множества компонентов, например веб-приложения, базы данных, сервера базы данных, хранилища и служб сторонних поставщиков.
   * **Расположение.** Выберите центр данных Azure для учетной записи аналитики Озера данных hello.
   * **Хранилище Озера данных**: следуйте toocreate hello инструкция новую учетную запись хранилища Озера данных, или выберите существующий. 
4. При необходимости выберите ценовую категорию для учетной записи Data Lake Analytics.
5. Щелкните **Создать**. 


## <a name="your-first-u-sql-script"></a>Первый скрипт U-SQL

После текста Hello является очень простой скрипт U-SQL. Он осуществляет — определить небольшой набор данных в рамках скрипта hello, а затем написать этот набор данных в хранилище Озера данных по умолчанию toohello как файл с именем `/data.csv`.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a>Отправка задания U-SQL

1. Hello учетной записи аналитики Озера данных, щелкните **новое задание**.
2. Вставьте текст hello hello скрипт U-SQL, показанном выше. 
3. Щелкните **Отправить задание**.   
4. Подождите, пока изменения состояния задания hello слишком**успешно**.
5. Если не удалось выполнить задание hello, см. раздел [монитора и диагностика заданий аналитики Озера данных](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).
6. Нажмите кнопку hello **вывода** , а затем щелкните `data.csv`. 

## <a name="see-also"></a>См. также

* tooget к разработке приложений U-SQL, в разделе [сценариев разработки U-SQL, с помощью средства Озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* в разделе toolearn U-SQL [Приступая к работе с Azure аналитика Озера данных U-SQL языка](data-lake-analytics-u-sql-get-started.md).
* Задачи управления описываются в руководстве по [управлению Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-manage-use-portal.md).
