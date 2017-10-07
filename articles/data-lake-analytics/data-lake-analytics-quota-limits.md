---
title: "aaaAzure квоты аналитика Озера данных | Документы Microsoft"
description: "Узнайте, как tooadjust, увеличение квоты ограничений в учетные записи аналитики Озера данных Azure (ADLA)."
services: data-lake-analytics
keywords: "Аналитика озера данных Azure"
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a>Квота Azure Data Lake Analytics

Узнайте, как tooadjust, увеличение квоты ограничений в учетные записи аналитики Озера данных Azure (ADLA). Зная ее ограничения, вы сможете понять поведение задания U-SQL. Все квоты, мягкое, поэтому можно увеличить дисковое пространство, занимаемое hello по достижении toous.

## <a name="azure-subscriptions-limits"></a>Ограничения подписок Azure

**Максимальное количество учетных записей Azure Data Lake Analytics в одной подписке:** 5.

 Это максимальное число hello ADLA учетные записи, которые можно создать для каждой подписки. Если учетная запись ADLA toocreate шестом, будет формировать ошибку «В области под именем подписки достигнуто hello максимальное количество аналитики Озера данных учетных записей (5)». В этом случае удалите все неиспользуемые учетные записи ADLA или связаться с toous [отправив запрос в службу поддержки](#increase-maximum-quota-limits).

## <a name="adla-account-limits"></a>Ограничения учетной записи Azure Data Lake Analytics

**Максимальное количество единиц аналитики на учетную запись:** 250.

Это максимальное число hello Сиднейское, которые могут выполняться параллельно в вашей учетной записи. Если общее количество единиц аналитики по всем выполняемым заданиям превысит это ограничение, новые задания будут автоматически помещаться в очередь. Например:

* Если имеется только одно задание с 250 Сиднейское при отправке второе задание он будет ожидать в очереди заданий hello до завершения первого задания hello.
* Если уже имеется пять заданий, выполняемых каждой используется 50 Сиднейское при отправке шестой задание, которое требуется 20 Сиднейское ожидает в очереди заданий hello до 20 Сиднейское доступны.

**Максимальное число одновременно выполняемых заданий U-SQL на учетную запись:** 20.

Это hello максимальное количество заданий, которые могут одновременно работать в вашей учетной записи. При достижении этого значения новые задания автоматически помещаются в очередь.

## <a name="adjust-adla-quota-limits-per-account"></a>Корректировка квот Azure Data Lake Analytics для учетной записи

1. Войдите на toohello [портал Azure](https://portal.azure.com).
2. Выберите существующую учетную запись ADLA.
3. Щелкните **Свойства**.
4. Настройка **параллелизма** и **одновременно выполняемых заданий** toosuit вашим потребностям.

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a>Увеличение максимальной квоты

1. Откройте запрос на поддержку на портале Azure.

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. Выберите тип проблемы hello **квоты**.
3. Выберите **подписку**, которая не является пробной.
4. Выберите тип квоты **Data Lake Analytics**.

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. В колонке hello проблема объясняется лимита запрошенное увеличение с **сведения** почему нужно это дополнительная емкость.

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. Проверьте свои контактные данные и создать запрос на получение поддержки hello.

Корпорация Майкрософт не рассмотрит вашу заявку и пытается tooaccommodate бизнесу необходимо как можно быстрее.

## <a name="next-steps"></a>Дальнейшие действия

* [Обзор аналитики озера данных Microsoft Azure](data-lake-analytics-overview.md)
* [Управление аналитикой озера данных Azure с помощью Azure PowerShell](data-lake-analytics-manage-use-powershell.md)
* [Устранение неполадок с заданиями аналитики озера данных Azure с помощью портала Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
