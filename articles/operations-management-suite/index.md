---
title: "aaaAzure документации Operations Management Suite (OMS) — учебные материалы | Документы Microsoft"
description: "Microsoft Operations Management Suite (OMS) — это облачное решение Майкрософт для управления ИТ-средой, которое помогает управлять локальной и облачной инфраструктурой и защищать ее. В этой статье приведены различные службы hello включены в OMS, а также ссылки tootheir подробные содержимого."
services: operations-management-suite
author: carolz
manager: carolz
layout: LandingPage
ms.assetid: 
ms.service: operations-management-suite
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing-page
ms.date: 01/23/2017
ms.author: carolz
ms.openlocfilehash: 11a8f5ecb3d84aed90554510fc1bb43320fdebb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Что такое Operations Management Suite (OMS)?
Microsoft Operations Management Suite (OMS) — это облачное решение Майкрософт для управления ИТ-средой, которое помогает управлять локальной и облачной инфраструктурой и защищать ее.  Набор OMS реализован как облачная служба, поэтому время, затрачиваемое на подготовку к работе, минимально, как и вложения в службы инфраструктуры.  Новые возможности предоставляются автоматически, что обеспечивает экономию затрат на текущее обслуживание и обновление.

Кроме tooproviding ценных на собственный, OMS можно интегрировать с компонентами System Center, такими как System Center Operations Manager tooextend существующие инвестиции в инфраструктуру управления в облаке hello.  System Center и OMS могут работать вместе возможности управления полную гибридную tooprovide.

Привет, в следующих разделах обеспечивают общее описание различных значимых направлений OMS и hello служб, которые их реализуют hello.  Обзор hello различным компонентам OMS можно ссылаться tooOMS архитектуры перед Просмотр hello подробная документация для каждого.

## <a name="insight-and-analyticsmediaoperations-management-suite-overviewicon-insight-analyticspng-insight-and-analytics"></a>![Анализ и аналитика](media/operations-management-suite-overview/icon-insight-analytics.png) Анализ и аналитика
Служба [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) помогает собирать и сопоставлять данные журналов и производительности, созданные операционными системами и приложениями, а также выполнять поиск и определенные действия на их основе. Он предоставляет в реальном времени оперативной аналитики с помощью интегрированной возможности поиска и настраиваемых панелей мониторинга tooreadily анализа миллионов записей во всех рабочих нагрузках и серверах независимо от их физического расположения.

Можно легко добавить решения tooLog Analytics, определение toobe данные собираются и hello логику для их анализа.  Решения могут располагать дополнительными функциями, автоматически доставляемыми tooagents с минимальными настройками или вообще без.  В дополнение к этому toousing средства анализа в состав отдельных решений, можно применять настраиваемые поиски по всему набору данных hello в порядке toocorrelate данных между системами и приложениями.  

## <a name="automation--controlmediaoperations-management-suite-overviewicon-automation-controlpng-automation--control"></a>![Автоматизация и контроль](media/operations-management-suite-overview/icon-automation-control.png) Автоматизация и контроль
Служба автоматизации Azure позволяет автоматизировать административные процессы с помощью [runbooks](../automation/automation-runbook-types.md) , которые основаны на PowerShell и выполняются в облаке Azure hello.  Модули Runbook могут получать доступ к любому продукту или службе, которыми можно управлять с помощью PowerShell, включая ресурсы в других облачных средах, таких как Amazon Web Services (AWS).  Модули Runbook также можно выполнить на сервере в локальные данные Центр ресурсов локального toomanage.

Служба автоматизации Azure предоставляет функции управления конфигурацией с помощью [PowerShell DSC](../automation/automation-dsc-overview.md).  Можно создать и контролировать ресурсы DSC, размещенные в Azure и применить их toocloud и локальных систем toodefine и автоматической реализации их конфигураций.

## <a name="protection-and-recoverymediaoperations-management-suite-overviewicon-protection-recoverypng-protection-and-disaster-recovery"></a>![Защита и восстановление](media/operations-management-suite-overview/icon-protection-recovery.png) Защита данных и аварийное восстановление
[Служба архивации Azure](http://azure.microsoft.com/documentation/services/backup) защищает данные приложений и хранит их в течение нескольких лет без каких-либо капитальных затрат и с минимальными операционными затратами.  Она может архивировать данные с физических и виртуальных серверов Windows в рабочих нагрузок tooapplication сложения, например SQL Server и SharePoint.  Он также может использоваться с System Center Data Protection Manager (DPM) tooreplicate защищенных данных tooAzure для обеспечения избыточности и долговременного хранения.

[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) поддерживает tooyour бесперебойной работе и стратегии аварийного восстановления (BCDR), управляя операциями репликации, отработки отказа и восстановления виртуальных машин Hyper-V в локальной среде, виртуальных машин VMware и физических Windows / Серверы Linux. Можно реплицировать машины tooa вторичный центр обработки данных или расширить центр обработки данных, копируя их tooAzure. Azure Site Recovery также предоставляет простые процедуры отработки отказа и восстановления для рабочих нагрузок. Она интегрируется с механизмами аварийного восстановления, такими как SQL Server AlwaysOn, и предоставляет планы восстановления для простой отработки отказа рабочих нагрузок, которые распределены между несколькими компьютерами.

## <a name="oms-security-and-compliancemediaoperations-management-suite-overviewicon-security-compliancepng-security-and-compliance"></a>![Безопасность и соответствие требованиям OMS](media/operations-management-suite-overview/icon-security-compliance.png) Служба "Безопасность и соответствие требованиям"
Безопасность и соответствие требованиям помогает определить, оценивать и нейтрализовывать риски безопасности tooyour инфраструктуры.  Эти функции OMS реализуются в нескольких решениях в службе анализа журналов, анализируют данные журналов и конфигурации из систем tooassist агента можно в обеспечении безопасности hello вашей среды.

* Hello [решения безопасности и аудита](oms-security-getting-started.md) осуществляет сбор и анализ событий безопасности в управляемых системах tooidentify подозрительной активности.
* Hello [антивирусное решение](../log-analytics/log-analytics-malware.md) сообщает hello состояние защиты от вредоносных программ в управляемых системах.  
* решение для системных обновлений Hello выполняет анализ обновлений безопасности hello и других обновлений в управляемых системах, позволяющий легко определять системы требующие применения исправлений.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)
* Дополнительные сведения о [службе автоматизации Azure](../automation/automation-intro.md)
* Дополнительные сведения о [службе архивации Azure](http://azure.microsoft.com/documentation/services/backup).
* Дополнительные сведения об [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

