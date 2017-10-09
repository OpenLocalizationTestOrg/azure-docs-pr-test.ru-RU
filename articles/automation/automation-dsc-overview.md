---
title: "Общие сведения о DSC автоматизации aaaAzure | Документы Microsoft"
description: "Обзор DSC службы автоматизации Azure, условий использования и известных проблем"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "PowerShell DSC, настройка требуемого состояния, PowerShell DSC для Azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a>Обзор DSC службы автоматизации Azure

Azure Automation DSC — это служба Azure, который позволяет вам toowrite, управления и компиляции конфигурации требуемого состояния (DSC) PowerShell [конфигурации](https://msdn.microsoft.com/powershell/dsc/configurations), Импорт [ресурсов DSC](https://msdn.microsoft.com/powershell/dsc/resources)и назначение узлы tootarget конфигураций в облаке hello.

## <a name="why-use-azure-automation-dsc"></a>Преимущества Azure Automation DSC

Azure Automation DSC обеспечивает ряд преимуществ по сравнению с использованием DSC за пределами Azure.

### <a name="built-in-pull-server"></a>Встроенный опрашивающий сервер

Служба автоматизации Azure обеспечивает [опрашивающего сервера DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) , чтобы целевые узлы автоматически получать конфигураций, соответствуют toohello требуемого состояния и выдавать отчеты об их соответствии.
Hello встроенных опрашивающего сервера в службе автоматизации Azure устраняет необходимость tooset hello вверх и ведение опрашивающего сервера.
Служба автоматизации Azure можно выбрать целевую виртуальных или физических Windows или Linux машин, в облаке hello или локальной.

### <a name="management-of-all-your-dsc-artifacts"></a>Управление всеми артефактами DSC

Переводит Azure Automation DSC hello же уровень управления слишком[настройки требуемого состояния PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) как автоматизации Azure предоставляет для создания сценариев PowerShell.

Из hello портал Azure или из PowerShell можно управлять все вашей DSC конфигураций, ресурсов и целевой узлы.

![Снимок экрана: колонка hello автоматизации Azure](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>Импорт данных отчетов в Log Analytics

Узлы, которые управляются с помощью DSC службы автоматизации Azure отправить подробное состояние данных toohello Встроенные запросу сервера отчетов.
Эта рабочая область данных tooyour анализа журналов Microsoft Operations Management Suite (OMS) можно настроить toosend DSC службы автоматизации Azure.
tooyour данных состояния toosend DSC рабочей областью аналитики журналов, в статье toolearn [вперед DSC службы автоматизации Azure reporting tooOMS данных аналитики журналов](automation-dsc-diagnostics.md).

## <a name="introduction-video"></a>Видео: общие сведения

Предпочитаете просмотра tooreading? Рассмотрим следующие видео от мая 2015 г., при первом объявлении Azure Automation DSC hello.

>[!NOTE]
>Хотя правильность hello основные понятия и жизненный цикл, рассматриваемые в этом видео, Azure Automation DSC изменилась во многом так, как это видео было записано.
>Теперь стал общедоступным, имеет гораздо более сложные пользовательский Интерфейс в hello портал Azure и поддерживает множество дополнительных возможностей.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>Дальнейшие действия

* toolearn toobe tooonboard узлов управляются с помощью Azure Automation DSC. в разделе [адаптации машин для управления с помощью DSC службы автоматизации Azure](automation-dsc-onboarding.md)
* tooget к работе с Azure Automation DSC. в разделе [Приступая к работе с Azure Automation DSC](automation-dsc-getting-started.md)
* разделе toolearn о компиляции конфигурации DSC, в котором можно задать их узлы tootarget [компиляции конфигурации в DSC службы автоматизации Azure](automation-dsc-compile.md)
* Справочник по командлетам PowerShell для Azure Automation DSC приводится в статье [Azure​RM.​Automation](/powershell/module/azurerm.automation/#automation).
* Сведения о ценах см. на [странице с ценами на Azure Automation DSC](https://azure.microsoft.com/pricing/details/automation/).
* см. пример использования в конвейере непрерывного развертывания Azure Automation DSC toosee [tooIaaS непрерывного развертывания виртуальных машин с помощью DSC службы автоматизации Azure и Chocolatey](automation-dsc-cd-chocolatey.md)
