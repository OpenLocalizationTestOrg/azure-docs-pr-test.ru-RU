---
title: "Обратите внимание, aaaGuest ОС семейства 1 вывода из эксплуатации | Документы Microsoft"
description: "Предоставляет сведения о, когда произошло hello Azure гостевой ОС семейства 1 вывода из эксплуатации и каким образом toodetermine в случае возникновения"
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
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="71f94-103">Уведомление о прекращении использования семейства версий 1 гостевой ОС</span><span class="sxs-lookup"><span data-stu-id="71f94-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="71f94-104">Выбытие Hello ОС семейства 1 было объявлено 1 июня 2013 г.</span><span class="sxs-lookup"><span data-stu-id="71f94-104">hello retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="71f94-105">**2 сентября 2014 г.** hello гостевой операционной системы Azure (Гостевая ОС) семейства 1.x, основанное на ОС Windows Server 2008 hello, была официально выведена из использования.</span><span class="sxs-lookup"><span data-stu-id="71f94-105">**Sept 2, 2014** hello Azure Guest operating system (Guest OS) Family 1.x, which is based on hello Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="71f94-106">Все попытки toodeploy новых служб или обновления существующих служб с использованием семейства 1, будут завершаться сообщение об ошибке, информирующее, что hello что гостевой ОС семейства 1 был списан.</span><span class="sxs-lookup"><span data-stu-id="71f94-106">All attempts toodeploy new services or upgrade existing services using Family 1 will fail with an error message informing you that hello Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="71f94-107">**3 ноября 2014 г.** Закончилась расширенная поддержка и полностью прекращено использование семейства версий 1 гостевой ОС.</span><span class="sxs-lookup"><span data-stu-id="71f94-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="71f94-108">Будут затронуты все службы, использующие семейство версий 1.</span><span class="sxs-lookup"><span data-stu-id="71f94-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="71f94-109">Эти службы могут быть остановлены в любом момент.</span><span class="sxs-lookup"><span data-stu-id="71f94-109">We may stop those services at any time.</span></span> <span data-ttu-id="71f94-110">Нет никакой гарантии, что ваши службы будут toorun, пока вы не обновите их сами вручную.</span><span class="sxs-lookup"><span data-stu-id="71f94-110">There is no guarantee your services will continue toorun unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="71f94-111">Если у вас есть дополнительные вопросы, посетите hello [форумы по облачным службам](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) или [обратитесь в службу поддержки Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="71f94-111">If you have additional questions, visit hello [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="71f94-112">Влияет ли это на вас?</span><span class="sxs-lookup"><span data-stu-id="71f94-112">Are you affected?</span></span>
<span data-ttu-id="71f94-113">Облачные службы могут измениться, если выполнено одно из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="71f94-113">Your Cloud Services are affected if any one of hello following applies:</span></span>

1. <span data-ttu-id="71f94-114">Имеет значение «osFamily = «1» явно указано в файле ServiceConfiguration.cscfg hello для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="71f94-114">You have a value of "osFamily = "1" explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="71f94-115">У вас значение osFamily, явно указано в файле ServiceConfiguration.cscfg hello для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="71f94-115">You do not have a value for osFamily explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="71f94-116">В настоящее время hello система использует значение по умолчанию hello, «1» в этом случае.</span><span class="sxs-lookup"><span data-stu-id="71f94-116">Currently, hello system uses hello default value of "1" in this case.</span></span>
3. <span data-ttu-id="71f94-117">Hello портал Azure в гостевой операционной системе семейство указано как «Windows Server 2008».</span><span class="sxs-lookup"><span data-stu-id="71f94-117">hello Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="71f94-118">toofind какие облачные службы запускают какое семейство ОС, можно запустить hello, выполнив сценарий в Azure PowerShell, но сначала необходимо [настроить Azure PowerShell](/powershell/azureps-cmdlets-docs) первой.</span><span class="sxs-lookup"><span data-stu-id="71f94-118">toofind which of your cloud services are running which OS Family, you can run hello following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="71f94-119">Дополнительные сведения о сценарии hello см. в разделе [Azure гостевой ОС семейства 1 завершение срока службы: Июнь 2014 г.](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="71f94-119">For more information on hello script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="71f94-120">Облачные службы будет оказывать воздействие семейства гостевых ОС 1, если hello osFamily столбца в выходных данных скрипта hello пуст или содержит значение «1».</span><span class="sxs-lookup"><span data-stu-id="71f94-120">Your cloud services will be impacted by OS Family 1 retirement if hello osFamily column in hello script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="71f94-121">Рекомендации в случае, если на вас это влияет</span><span class="sxs-lookup"><span data-stu-id="71f94-121">Recommendations if you are affected</span></span>
<span data-ttu-id="71f94-122">Мы рекомендуем перенести tooone роли вашей облачной службы из hello поддерживаемых семейств гостевых ОС:</span><span class="sxs-lookup"><span data-stu-id="71f94-122">We recommend you migrate your Cloud Service roles tooone of hello supported Guest OS Families:</span></span>

<span data-ttu-id="71f94-123">**Семейство версий 4.x гостевой ОС** — Windows Server 2012 R2 *(рекомендуется)*</span><span class="sxs-lookup"><span data-stu-id="71f94-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="71f94-124">Убедитесь, что приложение использует пакет SDK 2.1 или более поздней версии с платформой .NET Framework 4.0, 4.5 или 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="71f94-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="71f94-125">Задать файл ServiceConfiguration.cscfg слишком «4» в hello атрибут osFamily hello и повторного развертывания облачной службы.</span><span class="sxs-lookup"><span data-stu-id="71f94-125">Set hello osFamily attribute too“4” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="71f94-126">**Семейство версий 3.x гостевой ОС** — Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="71f94-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="71f94-127">Убедитесь, что приложение использует пакет SDK 1.8 или более поздней версии с платформой .NET Framework 4.0 или 4.5.</span><span class="sxs-lookup"><span data-stu-id="71f94-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="71f94-128">Задать файл ServiceConfiguration.cscfg слишком «3» в hello атрибут osFamily hello и повторного развертывания облачной службы.</span><span class="sxs-lookup"><span data-stu-id="71f94-128">Set hello osFamily attribute too“3” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="71f94-129">**Семейство версий 2.x гостевой ОС** — Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="71f94-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="71f94-130">Убедитесь, что приложение использует пакет SDK 1.3 или более поздней версии с платформой .NET Framework 3.5 или 4.0.</span><span class="sxs-lookup"><span data-stu-id="71f94-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="71f94-131">Задать файл ServiceConfiguration.cscfg слишком «2» в hello атрибут osFamily hello и повторного развертывания облачной службы.</span><span class="sxs-lookup"><span data-stu-id="71f94-131">Set hello osFamily attribute too"2" in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="71f94-132">Расширенная поддержка семейства версий 1 гостевой ОС окончена 3 ноября 2014 г.</span><span class="sxs-lookup"><span data-stu-id="71f94-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="71f94-133">Облачные службы в семействе версий 1 гостевой ОС более не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="71f94-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="71f94-134">Миграцию с семейства 1, как только возможно tooavoid службы перебоев в работе.</span><span class="sxs-lookup"><span data-stu-id="71f94-134">Migrate off family 1 as soon as possible tooavoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="71f94-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="71f94-135">Next steps</span></span>
<span data-ttu-id="71f94-136">Просмотрите hello последней [выпусками гостевых ОС](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="71f94-136">Review hello latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
