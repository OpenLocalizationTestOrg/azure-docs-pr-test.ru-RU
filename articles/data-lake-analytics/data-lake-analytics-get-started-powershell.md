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
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="08eec-103">Начало работы с Azure Data Lake Analytics с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="08eec-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="08eec-104">Узнайте, как toouse toocreate Azure PowerShell аналитики Озера данных Azure учетные записи и затем отправьте и запуска заданий U-SQL.</span><span class="sxs-lookup"><span data-stu-id="08eec-104">Learn how toouse Azure PowerShell toocreate Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="08eec-105">Дополнительные сведения о Data Lake Analytics см. в [обзоре Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08eec-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08eec-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="08eec-106">Prerequisites</span></span>

<span data-ttu-id="08eec-107">Прежде чем начать работу с учебником, необходимо иметь hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="08eec-107">Before you begin this tutorial, you must have hello following information:</span></span>

* <span data-ttu-id="08eec-108">**Учетная запись Azure Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="08eec-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="08eec-109">См. раздел [Начало работы с Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="08eec-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="08eec-110">**Рабочая станция с Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="08eec-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="08eec-111">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08eec-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="08eec-112">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="08eec-112">Log in tooAzure</span></span>

<span data-ttu-id="08eec-113">Для работы с руководством необходим опыт работы с Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08eec-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="08eec-114">В частности, необходимы tooknow как toolog в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="08eec-114">In particular, you need tooknow how toolog in tooAzure.</span></span> <span data-ttu-id="08eec-115">В разделе hello [Приступая к работе с Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) Если вам нужна помощь.</span><span class="sxs-lookup"><span data-stu-id="08eec-115">See hello [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="08eec-116">toolog систему с именем подписки:</span><span class="sxs-lookup"><span data-stu-id="08eec-116">toolog in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="08eec-117">Вместо имени подписки hello можно также использовать toolog идентификатор подписки в:</span><span class="sxs-lookup"><span data-stu-id="08eec-117">Instead of hello subscription name, you can also use a subscription id toolog in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="08eec-118">В случае успешного выполнения hello выходные данные этой команды выглядит следующим образом после текста hello.</span><span class="sxs-lookup"><span data-stu-id="08eec-118">If  successful, hello output of this command looks like hello following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a><span data-ttu-id="08eec-119">Подготовка для учебника hello</span><span class="sxs-lookup"><span data-stu-id="08eec-119">Preparing for hello tutorial</span></span>

<span data-ttu-id="08eec-120">фрагменты кода PowerShell Hello в этом учебнике используйте эти переменные toostore эти сведения.</span><span class="sxs-lookup"><span data-stu-id="08eec-120">hello PowerShell snippets in this tutorial use these variables toostore this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="08eec-121">Получение сведений об учетной записи Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="08eec-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="08eec-122">Отправка задания U-SQL</span><span class="sxs-lookup"><span data-stu-id="08eec-122">Submit a U-SQL job</span></span>

<span data-ttu-id="08eec-123">Создайте сценарий PowerShell переменной toohold hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="08eec-123">Create a PowerShell variable toohold hello U-SQL script.</span></span>

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

<span data-ttu-id="08eec-124">Отправьте скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="08eec-124">Submit hello script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="08eec-125">Кроме того можно сохранить как файл скрипта hello и отправить с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="08eec-125">Alternatively, you could save hello script as a file and submit with hello following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="08eec-126">Получите состояние hello определенного задания.</span><span class="sxs-lookup"><span data-stu-id="08eec-126">Get hello status of a specific job.</span></span> <span data-ttu-id="08eec-127">Продолжать использовать этот командлет, пока вы увидите, что выполнена hello.</span><span class="sxs-lookup"><span data-stu-id="08eec-127">Keep using this cmdlet until you see hello job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="08eec-128">Вместо вызова Get AdlAnalyticsJob снова и снова до завершения задания, можно использовать командлет Wait-AdlJob hello.</span><span class="sxs-lookup"><span data-stu-id="08eec-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use hello Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="08eec-129">Загрузите hello выходного файла.</span><span class="sxs-lookup"><span data-stu-id="08eec-129">Download hello output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="08eec-130">См. также</span><span class="sxs-lookup"><span data-stu-id="08eec-130">See also</span></span>
* <span data-ttu-id="08eec-131">toosee hello же учебника при помощи других средств, щелкните селекторы вкладку hello на hello вверху страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="08eec-131">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="08eec-132">в разделе toolearn U-SQL [Приступая к работе с Azure аналитика Озера данных U-SQL языка](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="08eec-132">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="08eec-133">Задачи управления описываются в руководстве по [управлению Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="08eec-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
