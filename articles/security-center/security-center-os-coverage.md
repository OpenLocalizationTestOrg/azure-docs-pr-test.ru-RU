---
title: "aaaSupported платформ в центр безопасности Azure | Документы Microsoft"
description: "В этом документе содержится список операционных систем Windows и Linux, поддерживаемых в центре безопасности Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: f73e04970749271fc9d75836f4f468b0a4953f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="supported-platforms-in-azure-security-center"></a>Поддерживаемые платформы в центре безопасности Azure
Наблюдение за состоянием системы безопасности и рекомендации, доступные для виртуальных машин (ВМ), созданных с помощью классической hello и модели развертывания диспетчера ресурсов.

> [!NOTE]
> Дополнительные сведения о hello [классический и модели развертывания диспетчера ресурсов](../azure-classic-rm.md) для ресурсов Azure.
>
>

## <a name="supported-platforms-for-windows-vms"></a>Поддерживаемые платформы для виртуальных машин Windows
Поддерживаемые операционные системы Windows:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

> [!NOTE]
>
* Оценки уязвимости ОС пока не доступны для Windows Server 2016.
* Обнаружения анализа аварийного завершения поддерживаются только для Windows Server 2012 и Windows Server 2012 R2.
>
>

## <a name="supported-platforms-for-linux-vms"></a>Поддерживаемые платформы для виртуальных машин Linux
Поддерживаемые операционные системы Linux:

* Ubuntu версии 12.04, 14.04, 16.04, 16.10.
* Debian версии 7, 8.
* CentOS версии 6.\*, 7.*.
* Red Hat Enterprise Linux (RHEL) версии 6.\*, 7.*.
* SUSE Linux Enterprise Server (SLES) версии 11 с пакетом обновления 4 или выше, 12.*
* Oracle Linux версии 6.\*, 7.*.

> [!NOTE]
> Аналитика поведения виртуальной машины еще не доступна для операционных систем Linux.
>
>

## <a name="vms-and-cloud-services"></a>Виртуальные машины и облачные службы
Также поддерживаются виртуальные машины, запущенные в облачной службе. Мониторинг выполняется только для облачных служб и рабочих ролей, запущенных в слотах рабочей среды. toolearn Дополнительные сведения о облачной службы в разделе [Обзор облачных служб](../cloud-services/cloud-services-choose-me.md).

## <a name="next-steps"></a>Дальнейшие действия

- [Планирование центр безопасности Azure и руководство по использованию](security-center-planning-and-operations-guide.md) — Узнайте как tooplan и понять центра безопасности Azure tooadopt вопросы проектирования hello
- [Типы оповещений системы безопасности в центре безопасности Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-alerts-type.md#virtual-machine-behavioral-analysis) — дополнительные сведения об анализе поведения виртуальных машин и анализе памяти аварийного дампа в центре безопасности.
- [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска
- [Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — в этом блоге можно найти публикации, посвященные безопасности и соответствию требованиям в Azure.
