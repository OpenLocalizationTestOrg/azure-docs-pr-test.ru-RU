---
title: "aaaAzure Service Fabric шаблонов и сценариев | Документы Microsoft"
description: "Рекомендации и проверенные toodesign повторно используемых шаблонов разработки и работы вашей микрослужбами на Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a>Шаблоны и сценарии использования Service Fabric
Если вы рассматриваете возможность создания крупномасштабных микрослужбами, с помощью Azure Service Fabric, сведения из hello специалисты, которые разрабатываются и создаются эта платформа как услуга (PaaS). Приступая к работе с правильной архитектуры и затем Узнайте, как toooptimize ресурсы для приложения. Hello [Service Fabric шаблоны и методики](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) курс содержит ответы на вопросы hello, наиболее часто задаваемые реальных клиентами о Service Fabric сценариев и области приложения.
 
Узнайте, как toodesign, разработки и эксплуатации вашей микрослужбами на Service Fabric, с использованием рекомендаций и проверенные, многократно используемых шаблонов. Получите общие сведения о Service Fabric, а затем подробнее изучите разделы, посвященные оптимизации и безопасности кластера, переносу устаревших приложений, масштабированию в Интернете вещей, размещению игровых ядер и другим темам. Посмотрите на непрерывной поставки для различных рабочих нагрузок и даже получить hello сведения о поддержке Linux и контейнеры. 

## <a name="introduction"></a>Введение
Рекомендации и общие сведения о выборе между платформой как услугой (PaaS) и инфраструктурой как услугой (IaaS). Получение сведений о hello на следующие принципы разработки проверенные приложений.

<table><tr><th>Видео</th><th>В формате PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Введение tooService структуры</a></td></tr>
</table>

## <a name="cluster-planning-and-management"></a>Планирование кластера и управление им
Получите сведения о планировании ресурсов, оптимизации и безопасности кластера в контексте Azure Service Fabric.

<table><tr><th>Видео</th><th>В формате PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Планирование кластера и управление им</a></td></tr>
</table>

## <a name="hyper-scale-web"></a>Гипермасштабируемые веб-службы
Ознакомьтесь с основными понятиями гипермасштабируемых веб-служб, включая доступность и надежность, гипермасштабирование и управление состоянием.

<table><tr><th>Видео</th><th>В формате PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Гипермасштабируемые веб-службы</a></td></tr>
</table>

## <a name="iot"></a>Интернет вещей
Изучите hello Интернета вещей (IoT) в контексте hello Azure Service Fabric, включая hello Azure IoT конвейера, поддержки нескольких клиентов и IoT в масштабе.

<table><tr><th>Видео</th><th>В формате PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Интернет вещей</a></td></tr>
</table>

## <a name="gaming"></a>Игры
Рассмотрите пошаговые и интерактивные игры, а также узнайте о размещении существующих игровых ядер.

<table><tr><th>Видео</th><th>В формате PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Игры</a></td></tr>
</table>

## <a name="continuous-delivery"></a>Непрерывная доставка
Ознакомьтесь с основными понятиями, такими как непрерывная интеграция и непрерывная доставка с помощью Visual Studio Team Services, рабочий процесс сборки/пакета/публикации, настройка в нескольких средах, а также пакет и общая папка службы.

<table><tr><th>Видео</th><th>В формате PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Непрерывная доставка</a></td></tr>
</table>

## <a name="migration"></a>Миграция
Дополнительные сведения о миграции из облачной службы, кроме toomigration прежних версий приложений.

<table><tr><th>Видео</th><th>В формате PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Миграция</a></td></tr>
</table>

## <a name="containers-and-linux-support"></a>Контейнеры и поддержка Linux
Получить вопрос toohello ответов hello, «почему контейнеры?» Дополнительные сведения о предварительной версии hello для контейнеров Windows, Linux поддерживает и orchestration контейнеров Linux. Кроме того, узнайте, как приложения tooLinux toomigrate .NET Core.

<table><tr><th>Видео</th><th>В формате PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Контейнеры и поддержка Linux</a></td></tr>
</table>

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали о Service Fabric шаблонов и сценариев, Дополнительные сведения о том, как слишком[создания кластеров и управление ими](service-fabric-deploy-anywhere.md), [перенос облачных служб приложений tooService структуры](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [Настройка непрерывной поставки](service-fabric-set-up-continuous-integration.md), и [развернуть контейнеры](service-fabric-containers-overview.md).
