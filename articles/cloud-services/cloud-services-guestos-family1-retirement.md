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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="guest-os-family-1-retirement-notice"></a>Уведомление о прекращении использования семейства версий 1 гостевой ОС
О прекращении использования семейства версий 1 операционной системы было впервые объявлено 1 июня 2013 г.

**2 сентября 2014 г.** Официально прекращено использование семейства версий 1.x гостевой ОС Azure, основанной на ОС Windows Server 2008. Все попытки развертывать новые и обновлять существующие службы, используя операционную систему из семейства версий 1, приведут к сбою с ошибкой, в которой сообщается о прекращении использования семейства версий 1 гостевой ОС.

**3 ноября 2014 г.** Закончилась расширенная поддержка и полностью прекращено использование семейства версий 1 гостевой ОС. Будут затронуты все службы, использующие семейство версий 1. Эти службы могут быть остановлены в любом момент. Не гарантируется, что службы будут работать далее, если самостоятельно не обновить их вручную.

С дополнительными вопросами обращайтесь на [форумы облачных служб](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) или в [службу поддержки Azure](https://azure.microsoft.com/support/options/).

## <a name="are-you-affected"></a>Влияет ли это на вас?
Это влияет на ваши облачные службы в одном из следующих случаев:

1. Если явным образом указано значение "osFamily = "1" в файле ServiceConfiguration.cscfg облачной службы.
2. Если не указано явным образом значение для osFamily в файле ServiceConfiguration.cscfg облачной службы. В настоящий момент в такой ситуации системой используется значение по умолчанию, равное "1".
3. На портале Azure в качестве семейства операционных систем на виртуальной машине указано "Windows Server 2008".

Чтобы узнать, какие облачные службы работают под управлением какого семейства ОС, можно запустить указанный ниже скрипт в Azure PowerShell, однако сначала необходимо [настроить Azure PowerShell](/powershell/azureps-cmdlets-docs). Дополнительные сведения об этом скрипте см. в записи блога [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx) (Окончание срока жизни семейства версий 1 гостевой ОС Azure, июнь 2014 г.).

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

Прекращение использования семейства версий 1 операционной системы повлияет на облачные службы, если столбец "osFamily" в выходных данных скрипта является пустым или содержит значение "1".

## <a name="recommendations-if-you-are-affected"></a>Рекомендации в случае, если на вас это влияет
Рекомендуется перенести роли облачных служб в одно из поддерживаемых семейств версий гостевой ОС:

**Семейство версий 4.x гостевой ОС** — Windows Server 2012 R2 *(рекомендуется)*

1. Убедитесь, что приложение использует пакет SDK 2.1 или более поздней версии с платформой .NET Framework 4.0, 4.5 или 4.5.1.
2. Задайте для атрибута "osFamily" значение "4" в файле ServiceConfiguration.cscfg и повторно разверните облачную службу.

**Семейство версий 3.x гостевой ОС** — Windows Server 2012

1. Убедитесь, что приложение использует пакет SDK 1.8 или более поздней версии с платформой .NET Framework 4.0 или 4.5.
2. Задайте для атрибута osFamily значение «3» в файле ServiceConfiguration.cscfg и повторно разверните облачную службу.

**Семейство версий 2.x гостевой ОС** — Windows Server 2008 R2

1. Убедитесь, что приложение использует пакет SDK 1.3 или более поздней версии с платформой .NET Framework 3.5 или 4.0.
2. Задайте для атрибута "osFamily" значение "2" в файле ServiceConfiguration.cscfg и повторно разверните облачную службу.

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a>Расширенная поддержка семейства версий 1 гостевой ОС окончена 3 ноября 2014 г.
Облачные службы в семействе версий 1 гостевой ОС более не поддерживаются. Переходите от использования операционной системы семейства 1 к ОС другого семейства, чтобы избежать прерывания работы службы.  

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите последние [выпуски гостевой ОС](cloud-services-guestos-update-matrix.md).
