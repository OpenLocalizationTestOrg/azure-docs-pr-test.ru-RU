---
title: "aaaGet к выполнению аналитики Озера данных Azure, с помощью Azure PowerShell | Документы Microsoft"
description: "Использовать Azure PowerShell toocreate учетную запись аналитики Озера данных, создайте задание аналитики Озера данных с помощью U-SQL и отправка задания hello. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a>Начало работы с Azure Data Lake Analytics с помощью Azure PowerShell
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Узнайте, как toouse toocreate Azure PowerShell аналитики Озера данных Azure учетные записи и затем отправьте и запуска заданий U-SQL. Дополнительные сведения о Data Lake Analytics см. в [обзоре Azure Data Lake Analytics](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Предварительные требования

Прежде чем начать работу с учебником, необходимо иметь hello следующую информацию:

* **Учетная запись Azure Data Lake Analytics**. См. раздел [Начало работы с Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).
* **Рабочая станция с Azure PowerShell**. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

## <a name="log-in-tooazure"></a>Войдите в tooAzure

Для работы с руководством необходим опыт работы с Azure PowerShell. В частности, необходимы tooknow как toolog в tooAzure. В разделе hello [Приступая к работе с Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) Если вам нужна помощь.

toolog систему с именем подписки:

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

Вместо имени подписки hello можно также использовать toolog идентификатор подписки в:

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

В случае успешного выполнения hello выходные данные этой команды выглядит следующим образом после текста hello.

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a>Подготовка для учебника hello

фрагменты кода PowerShell Hello в этом учебнике используйте эти переменные toostore эти сведения.

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a>Получение сведений об учетной записи Data Lake Analytics

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a>Отправка задания U-SQL

Создайте сценарий PowerShell переменной toohold hello U-SQL.

```
$script = @"
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

"@
```

Отправьте скрипт hello.

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

Кроме того можно сохранить как файл скрипта hello и отправить с hello следующую команду:

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


Получите состояние hello определенного задания. Продолжать использовать этот командлет, пока вы увидите, что выполнена hello.

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

Вместо вызова Get AdlAnalyticsJob снова и снова до завершения задания, можно использовать командлет Wait-AdlJob hello.

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

Загрузите hello выходного файла.

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a>См. также
* toosee hello же учебника при помощи других средств, щелкните селекторы вкладку hello на hello вверху страницы приветствия.
* в разделе toolearn U-SQL [Приступая к работе с Azure аналитика Озера данных U-SQL языка](data-lake-analytics-u-sql-get-started.md).
* Задачи управления описываются в руководстве по [управлению Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-manage-use-portal.md).
