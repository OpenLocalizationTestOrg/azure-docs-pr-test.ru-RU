---
title: "aaaOperations архитектура Management Suite (OMS) | Документы Microsoft"
description: "Microsoft Operations Management Suite (OMS) — это облачное решение Майкрософт для управления ИТ-средой, которое помогает управлять локальной и облачной инфраструктурой и защищать ее.  В этой статье приведены различные службы hello включены в OMS, а также ссылки tootheir подробные содержимого."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: fa3227aa9c19219009ebe363b7fd2d6565cec59c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="oms-architecture"></a>Архитектура OMS
[Operations Management Suite](https://azure.microsoft.com/documentation/services/operations-management-suite/) — это набор облачных служб для управления локальными и облачными средами.  Эта статья описывает hello различные локальные и облачные компоненты OMS и их высокоуровневая облачная вычислительная архитектура.  Можно ссылаться toohello документации для каждой службы, для получения дополнительных сведений.

## <a name="log-analytics"></a>Служба Log Analytics
Все данные, собранные [анализа журналов](https://azure.microsoft.com/documentation/services/log-analytics/) сохраняются в репозитории OMS hello, размещаемой в Azure.  Подключенные источники создавать данные, собранные в репозиторий OMS hello.  На данный момент поддерживается три типа подключенных источников.

* Агент, установленный на [Windows](../log-analytics/log-analytics-windows-agents.md) или [Linux](../log-analytics/log-analytics-linux-agents.md) tooOMS непосредственно подключен компьютер.
* Группу управления System Center Operations Manager (SCOM) [подключен tooLog Analytics](../log-analytics/log-analytics-om-agents.md) .  SCOM агенты по-прежнему toocommunicate с серверами управления, которые пересылают события и данные производительности tooLog Analytics.
* [Учетная запись хранения Azure](../log-analytics/log-analytics-azure-storage.md), выполняющая сбор данных [системы диагностики Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) из рабочей роли, веб-роли или с виртуальной машины в Azure.

Источники данных определяют hello данных, которые служба аналитики журналов собирает из подключенных источников, включая журналы событий и счетчики производительности.  Добавить tooOMS функциональные возможности решения и можно легко добавить tooyour рабочей области из hello [Коллекция решений OMS](../log-analytics/log-analytics-add-solutions.md).  Некоторые решения может потребоваться прямое подключение tooLog аналитика с агентов SCOM, пока другие модули могут потребовать дополнительных агента toobe установлен.

Служба аналитики журналов имеет Интернет порталом, что можно использовать ресурсы toomanage OMS, добавления и настройки решений OMS и просматривать и анализировать данные в репозиторий OMS hello.

![Общая архитектура Log Analytics](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a>Служба автоматизации Azure
[Модули Runbook Azure Automation](http://azure.microsoft.com/documentation/services/automation) выполняются в облаке Azure hello и можно получить доступ к ресурсам, находящимся в Azure, в других облачных службах, или hello общедоступный Интернет.  Вы также можете выделить специальные локальные компьютеры в центре обработки данных, используя [гибридную рабочую роль Runbook](../automation/automation-hybrid-runbook-worker.md), чтобы модули Runbook могли обращаться к локальным ресурсам.

[Конфигурации DSC](../automation/automation-dsc-overview.md) хранятся в службе автоматизации Azure может быть напрямую применяются tooAzure виртуальных машин.  Другие физические и виртуальные машины могут запрашивать конфигурации с опрашивающего сервера DSC службы автоматизации Azure hello.

Служба автоматизации Azure имеет решение OMS, которое отображает статистические данные, а также связи toolaunch hello портал Azure для выполнения любых операций.

![Общая архитектура службы автоматизации Azure](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a>Служба архивации Azure
Защищенные данные в [службе архивации Azure](http://azure.microsoft.com/documentation/services/backup) хранятся в хранилище архивации, расположенном в определенном географическом регионе.  Hello данные реплицируются в hello в одном регионе и, в зависимости от типа хранилища hello, также могут быть реплицированной tooanother регион для дальнейшего обеспечения избыточности.

Служба архивации Azure предполагает три основные сценария.

* Компьютер Windows с агентом службы архивации Azure.  Это позволяет toobackup файлы и папки с любого сервера или клиента непосредственно tooyour резервное хранилище Azure.  
* System Center Data Protection Manager (DPM) или сервер службы архивации Microsoft Azure. Это позволяет вам tooleverage DPM или сервер службы архивации Microsoft Azure toobackup файлов и папок в дополнение к этому tooapplication рабочих нагрузок, таких как SQL и SharePoint toolocal хранилища и затем реплицировать tooyour резервное хранилище Azure.
* Расширения виртуальной машины Azure.  Это позволяет виртуальным машинам Azure toobackup tooyour резервное хранилище Azure.

Служба архивации Azure имеет решение OMS, которое отображает статистические данные, а также связи toolaunch hello портал Azure для выполнения любых операций.

![Общая архитектура службы архивации Azure](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) обеспечивает оркестрацию репликации, отработки отказа и восстановления виртуальных машин и физических серверов. Данные репликации передаются между узлами Hyper-V, гипервизорами VMware и физических серверов в центрах обработки данных основного и дополнительного или между hello центра обработки данных и хранилищем Azure.  Azure Site Recovery хранит метаданные в хранилищах, расположенных в определенном географическом регионе Azure. Нет реплицированных данных хранит hello службы Site Recovery.

Azure Site Recovery предполагает три основных сценария репликации.

**Репликация виртуальных машин Hyper-V**

* Если виртуальные машины Hyper-V управляются в облаках VMM, можно реплицировать tooa удаленного центра или tooAzure хранилища данных.  Репликация tooAzure — через безопасное подключение к Интернету.  Дополнительный ЦОД tooa репликации превышает hello локальной сети.
* Если виртуальных машин Hyper-V не управляются VMM, можно реплицировать только tooAzure для хранения данных.  Репликация tooAzure — через безопасное подключение к Интернету.

**Репликация виртуальных машин VMWare**

* Можно реплицировать VMware виртуальные машины tooa дополнительный центр обработки данных под управлением VMware или tooAzure хранилище.  TooAzure репликации может произойти через сеть сеть VPN или Azure ExpressRoute либо через безопасное подключение к Интернету. Дополнительный ЦОД tooa репликации производится по каналу данных InMage Scout hello.

**Репликация физических серверов Windows и Linux** 

* Можно реплицировать физические серверы tooa вторичного центра обработки данных или tooAzure хранилища. TooAzure репликации может произойти через сеть сеть VPN или Azure ExpressRoute либо через безопасное подключение к Интернету. Дополнительный ЦОД tooa репликации производится по каналу данных InMage Scout hello.  Azure Site Recovery существует решение OMS, которое отображает определенные статистические данные, но hello портала Azure необходимо использовать для выполнения любых операций.

![Общая архитектура Azure Site Recovery](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)
* Дополнительные сведения о [службе автоматизации Azure](https://azure.microsoft.com/documentation/services/automation)
* Дополнительные сведения о [службе архивации Azure](http://azure.microsoft.com/documentation/services/backup).
* Дополнительные сведения об [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

