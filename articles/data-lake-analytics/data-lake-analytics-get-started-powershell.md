---
title: "Начало работы с Azure Data Lake Analytics с помощью Azure PowerShell | Документация Майкрософт"
description: "Используйте Azure PowerShell для создания учетной записи Data Lake Analytics, создания задания Data Lake Analytics с помощью U-SQL и его отправки. "
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
ms.openlocfilehash: 4f73e27c733edae658d1ea3bdabe48076328279b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="82dcd-103">Начало работы с Azure Data Lake Analytics с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="82dcd-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="82dcd-104">Узнайте, как использовать Azure PowerShell для создания учетных записей Azure Data Lake Analytics, а затем отправлять и выполнять задания U-SQL.</span><span class="sxs-lookup"><span data-stu-id="82dcd-104">Learn how to use Azure PowerShell to create Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="82dcd-105">Дополнительные сведения о Data Lake Analytics см. в [обзоре Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82dcd-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82dcd-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="82dcd-106">Prerequisites</span></span>

<span data-ttu-id="82dcd-107">Перед началом работы с этим руководством необходимо иметь следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="82dcd-107">Before you begin this tutorial, you must have the following information:</span></span>

* <span data-ttu-id="82dcd-108">**Учетная запись Azure Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="82dcd-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="82dcd-109">См. раздел [Начало работы с Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="82dcd-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="82dcd-110"><seg>
  **Рабочая станция с Azure PowerShell**.</seg></span><span class="sxs-lookup"><span data-stu-id="82dcd-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="82dcd-111">См. статью [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="82dcd-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="82dcd-112">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="82dcd-112">Log in to Azure</span></span>

<span data-ttu-id="82dcd-113">Для работы с руководством необходим опыт работы с Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82dcd-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="82dcd-114">В частности вам нужно знать, как выполнить вход в Azure.</span><span class="sxs-lookup"><span data-stu-id="82dcd-114">In particular, you need to know how to log in to Azure.</span></span> <span data-ttu-id="82dcd-115">Если вам нужна помощь, см. раздел [Начало работы с Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="82dcd-115">See the [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="82dcd-116">Вход в систему с использованием имени подписки:</span><span class="sxs-lookup"><span data-stu-id="82dcd-116">To log in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="82dcd-117">Вместо имени подписки для входа можно использовать ее идентификатор:</span><span class="sxs-lookup"><span data-stu-id="82dcd-117">Instead of the subscription name, you can also use a subscription id to log in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="82dcd-118">При успешном выполнении этой команды выходные данные будут выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="82dcd-118">If  successful, the output of this command looks like the following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-the-tutorial"></a><span data-ttu-id="82dcd-119">Подготовка к работе с руководством</span><span class="sxs-lookup"><span data-stu-id="82dcd-119">Preparing for the tutorial</span></span>

<span data-ttu-id="82dcd-120">В этом руководстве во фрагментах кода PowerShell для хранения информации используются следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="82dcd-120">The PowerShell snippets in this tutorial use these variables to store this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="82dcd-121">Получение сведений об учетной записи Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="82dcd-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="82dcd-122">Отправка задания U-SQL</span><span class="sxs-lookup"><span data-stu-id="82dcd-122">Submit a U-SQL job</span></span>

<span data-ttu-id="82dcd-123">Создайте переменную для хранения скрипта U-SQL PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82dcd-123">Create a PowerShell variable to hold the U-SQL script.</span></span>

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
    TO "/data.csv"
    USING Outputters.Csv();

"@
```

<span data-ttu-id="82dcd-124">Отправьте скрипт.</span><span class="sxs-lookup"><span data-stu-id="82dcd-124">Submit the script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="82dcd-125">Или же можно сохранить скрипт в файл, а затем отправить его с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="82dcd-125">Alternatively, you could save the script as a file and submit with the following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="82dcd-126">Получите состояние конкретного задания.</span><span class="sxs-lookup"><span data-stu-id="82dcd-126">Get the status of a specific job.</span></span> <span data-ttu-id="82dcd-127">Продолжайте использовать этот командлет, пока задание не будет выполнено.</span><span class="sxs-lookup"><span data-stu-id="82dcd-127">Keep using this cmdlet until you see the job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="82dcd-128">Вместо того чтобы снова и снова вызывать командлет Get-AdlAnalyticsJob, пока задание не будет завершено, можно использовать командлет Wait-AdlJob.</span><span class="sxs-lookup"><span data-stu-id="82dcd-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use the Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="82dcd-129">Загрузите выходной файл.</span><span class="sxs-lookup"><span data-stu-id="82dcd-129">Download the output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="82dcd-130">См. также</span><span class="sxs-lookup"><span data-stu-id="82dcd-130">See also</span></span>
* <span data-ttu-id="82dcd-131">Для просмотра учебника с помощью других средств используйте вкладки-селекторы в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="82dcd-131">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="82dcd-132">Для знакомства с U-SQL см. статью о [начале работы с языком U-SQL для Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="82dcd-132">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="82dcd-133">Задачи управления описываются в руководстве по [управлению Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="82dcd-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
