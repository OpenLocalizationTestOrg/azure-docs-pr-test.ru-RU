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
# <a name="guest-os-family-1-retirement-notice"></a>Уведомление о прекращении использования семейства версий 1 гостевой ОС
Выбытие Hello ОС семейства 1 было объявлено 1 июня 2013 г.

**2 сентября 2014 г.** hello гостевой операционной системы Azure (Гостевая ОС) семейства 1.x, основанное на ОС Windows Server 2008 hello, была официально выведена из использования. Все попытки toodeploy новых служб или обновления существующих служб с использованием семейства 1, будут завершаться сообщение об ошибке, информирующее, что hello что гостевой ОС семейства 1 был списан.

**3 ноября 2014 г.** Закончилась расширенная поддержка и полностью прекращено использование семейства версий 1 гостевой ОС. Будут затронуты все службы, использующие семейство версий 1. Эти службы могут быть остановлены в любом момент. Нет никакой гарантии, что ваши службы будут toorun, пока вы не обновите их сами вручную.

Если у вас есть дополнительные вопросы, посетите hello [форумы по облачным службам](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) или [обратитесь в службу поддержки Azure](https://azure.microsoft.com/support/options/).

## <a name="are-you-affected"></a>Влияет ли это на вас?
Облачные службы могут измениться, если выполнено одно из следующих hello.

1. Имеет значение «osFamily = «1» явно указано в файле ServiceConfiguration.cscfg hello для облачной службы.
2. У вас значение osFamily, явно указано в файле ServiceConfiguration.cscfg hello для облачной службы. В настоящее время hello система использует значение по умолчанию hello, «1» в этом случае.
3. Hello портал Azure в гостевой операционной системе семейство указано как «Windows Server 2008».

toofind какие облачные службы запускают какое семейство ОС, можно запустить hello, выполнив сценарий в Azure PowerShell, но сначала необходимо [настроить Azure PowerShell](/powershell/azureps-cmdlets-docs) первой. Дополнительные сведения о сценарии hello см. в разделе [Azure гостевой ОС семейства 1 завершение срока службы: Июнь 2014 г.](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

Облачные службы будет оказывать воздействие семейства гостевых ОС 1, если hello osFamily столбца в выходных данных скрипта hello пуст или содержит значение «1».

## <a name="recommendations-if-you-are-affected"></a>Рекомендации в случае, если на вас это влияет
Мы рекомендуем перенести tooone роли вашей облачной службы из hello поддерживаемых семейств гостевых ОС:

**Семейство версий 4.x гостевой ОС** — Windows Server 2012 R2 *(рекомендуется)*

1. Убедитесь, что приложение использует пакет SDK 2.1 или более поздней версии с платформой .NET Framework 4.0, 4.5 или 4.5.1.
2. Задать файл ServiceConfiguration.cscfg слишком «4» в hello атрибут osFamily hello и повторного развертывания облачной службы.

**Семейство версий 3.x гостевой ОС** — Windows Server 2012

1. Убедитесь, что приложение использует пакет SDK 1.8 или более поздней версии с платформой .NET Framework 4.0 или 4.5.
2. Задать файл ServiceConfiguration.cscfg слишком «3» в hello атрибут osFamily hello и повторного развертывания облачной службы.

**Семейство версий 2.x гостевой ОС** — Windows Server 2008 R2

1. Убедитесь, что приложение использует пакет SDK 1.3 или более поздней версии с платформой .NET Framework 3.5 или 4.0.
2. Задать файл ServiceConfiguration.cscfg слишком «2» в hello атрибут osFamily hello и повторного развертывания облачной службы.

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a>Расширенная поддержка семейства версий 1 гостевой ОС окончена 3 ноября 2014 г.
Облачные службы в семействе версий 1 гостевой ОС более не поддерживаются. Миграцию с семейства 1, как только возможно tooavoid службы перебоев в работе.  

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите hello последней [выпусками гостевых ОС](cloud-services-guestos-update-matrix.md).
