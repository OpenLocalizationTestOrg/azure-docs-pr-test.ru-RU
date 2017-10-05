---
title: "Уведомление о прекращении использования семейства версий 1 гостевой операционной системы | Документация Майкрософт"
description: "Содержит сведения о времени прекращения использования семейства версий 1 гостевой операционной системы и о том, как определить, повлияло ли это на вас"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: 3178a09dab1cb972a3460d54dc9908fb95cce68b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="a22de-103">Уведомление о прекращении использования семейства версий 1 гостевой ОС</span><span class="sxs-lookup"><span data-stu-id="a22de-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="a22de-104">О прекращении использования семейства версий 1 операционной системы было впервые объявлено 1 июня 2013 г.</span><span class="sxs-lookup"><span data-stu-id="a22de-104">The retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="a22de-105">**2 сентября 2014 г.** Официально прекращено использование семейства версий 1.x гостевой ОС Azure, основанной на ОС Windows Server 2008.</span><span class="sxs-lookup"><span data-stu-id="a22de-105">**Sept 2, 2014** The Azure Guest operating system (Guest OS) Family 1.x, which is based on the Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="a22de-106">Все попытки развертывать новые и обновлять существующие службы, используя операционную систему из семейства версий 1, приведут к сбою с ошибкой, в которой сообщается о прекращении использования семейства версий 1 гостевой ОС.</span><span class="sxs-lookup"><span data-stu-id="a22de-106">All attempts to deploy new services or upgrade existing services using Family 1 will fail with an error message informing you that the Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="a22de-107">**3 ноября 2014 г.** Закончилась расширенная поддержка и полностью прекращено использование семейства версий 1 гостевой ОС.</span><span class="sxs-lookup"><span data-stu-id="a22de-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="a22de-108">Будут затронуты все службы, использующие семейство версий 1.</span><span class="sxs-lookup"><span data-stu-id="a22de-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="a22de-109">Эти службы могут быть остановлены в любом момент.</span><span class="sxs-lookup"><span data-stu-id="a22de-109">We may stop those services at any time.</span></span> <span data-ttu-id="a22de-110">Не гарантируется, что службы будут работать далее, если самостоятельно не обновить их вручную.</span><span class="sxs-lookup"><span data-stu-id="a22de-110">There is no guarantee your services will continue to run unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="a22de-111">С дополнительными вопросами обращайтесь на [форумы облачных служб](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) или в [службу поддержки Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="a22de-111">If you have additional questions, visit the [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="a22de-112">Влияет ли это на вас?</span><span class="sxs-lookup"><span data-stu-id="a22de-112">Are you affected?</span></span>
<span data-ttu-id="a22de-113">Это влияет на ваши облачные службы в одном из следующих случаев:</span><span class="sxs-lookup"><span data-stu-id="a22de-113">Your Cloud Services are affected if any one of the following applies:</span></span>

1. <span data-ttu-id="a22de-114">Если явным образом указано значение "osFamily = "1" в файле ServiceConfiguration.cscfg облачной службы.</span><span class="sxs-lookup"><span data-stu-id="a22de-114">You have a value of "osFamily = "1" explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="a22de-115">Если не указано явным образом значение для osFamily в файле ServiceConfiguration.cscfg облачной службы.</span><span class="sxs-lookup"><span data-stu-id="a22de-115">You do not have a value for osFamily explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="a22de-116">В настоящий момент в такой ситуации системой используется значение по умолчанию, равное "1".</span><span class="sxs-lookup"><span data-stu-id="a22de-116">Currently, the system uses the default value of "1" in this case.</span></span>
3. <span data-ttu-id="a22de-117">На портале Azure в качестве семейства операционных систем на виртуальной машине указано "Windows Server 2008".</span><span class="sxs-lookup"><span data-stu-id="a22de-117">The Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="a22de-118">Чтобы узнать, какие облачные службы работают под управлением какого семейства ОС, можно запустить указанный ниже скрипт в Azure PowerShell, однако сначала необходимо [настроить Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a22de-118">To find which of your cloud services are running which OS Family, you can run the following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="a22de-119">Дополнительные сведения об этом скрипте см. в записи блога [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx) (Окончание срока жизни семейства версий 1 гостевой ОС Azure, июнь 2014 г.).</span><span class="sxs-lookup"><span data-stu-id="a22de-119">For more information on the script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="a22de-120">Прекращение использования семейства версий 1 операционной системы повлияет на облачные службы, если столбец "osFamily" в выходных данных скрипта является пустым или содержит значение "1".</span><span class="sxs-lookup"><span data-stu-id="a22de-120">Your cloud services will be impacted by OS Family 1 retirement if the osFamily column in the script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="a22de-121">Рекомендации в случае, если на вас это влияет</span><span class="sxs-lookup"><span data-stu-id="a22de-121">Recommendations if you are affected</span></span>
<span data-ttu-id="a22de-122">Рекомендуется перенести роли облачных служб в одно из поддерживаемых семейств версий гостевой ОС:</span><span class="sxs-lookup"><span data-stu-id="a22de-122">We recommend you migrate your Cloud Service roles to one of the supported Guest OS Families:</span></span>

<span data-ttu-id="a22de-123">**Семейство версий 4.x гостевой ОС** — Windows Server 2012 R2 *(рекомендуется)*</span><span class="sxs-lookup"><span data-stu-id="a22de-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="a22de-124">Убедитесь, что приложение использует пакет SDK 2.1 или более поздней версии с платформой .NET Framework 4.0, 4.5 или 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="a22de-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="a22de-125">Задайте для атрибута "osFamily" значение "4" в файле ServiceConfiguration.cscfg и повторно разверните облачную службу.</span><span class="sxs-lookup"><span data-stu-id="a22de-125">Set the osFamily attribute to “4” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="a22de-126">**Семейство версий 3.x гостевой ОС** — Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a22de-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="a22de-127">Убедитесь, что приложение использует пакет SDK 1.8 или более поздней версии с платформой .NET Framework 4.0 или 4.5.</span><span class="sxs-lookup"><span data-stu-id="a22de-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="a22de-128">Задайте для атрибута osFamily значение «3» в файле ServiceConfiguration.cscfg и повторно разверните облачную службу.</span><span class="sxs-lookup"><span data-stu-id="a22de-128">Set the osFamily attribute to “3” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="a22de-129">**Семейство версий 2.x гостевой ОС** — Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="a22de-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="a22de-130">Убедитесь, что приложение использует пакет SDK 1.3 или более поздней версии с платформой .NET Framework 3.5 или 4.0.</span><span class="sxs-lookup"><span data-stu-id="a22de-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="a22de-131">Задайте для атрибута "osFamily" значение "2" в файле ServiceConfiguration.cscfg и повторно разверните облачную службу.</span><span class="sxs-lookup"><span data-stu-id="a22de-131">Set the osFamily attribute to "2" in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="a22de-132">Расширенная поддержка семейства версий 1 гостевой ОС окончена 3 ноября 2014 г.</span><span class="sxs-lookup"><span data-stu-id="a22de-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="a22de-133">Облачные службы в семействе версий 1 гостевой ОС более не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="a22de-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="a22de-134">Переходите от использования операционной системы семейства 1 к ОС другого семейства, чтобы избежать прерывания работы службы.</span><span class="sxs-lookup"><span data-stu-id="a22de-134">Migrate off family 1 as soon as possible to avoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a22de-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a22de-135">Next steps</span></span>
<span data-ttu-id="a22de-136">Просмотрите последние [выпуски гостевой ОС](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="a22de-136">Review the latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
