---
title: "Гибридные рабочие роли Runbook службы автоматизации Azure для Linux | Документация Майкрософт"
description: "В этой статье содержатся сведения об установке гибридной рабочей роли Runbook в службе автоматизации Azure, которая позволяет запускать модули Runbook на компьютерах под управлением Linux в локальном центре обработки данных или облачной среде."
services: automation
documentationcenter: 
author: georgewallace
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/07/2017
ms.author: magoedte
ms.openlocfilehash: 938e4f4fa3326db23ea4c2b499c783de78dcfa76
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="how-to-deploy-a-linux-hybrid-runbook-worker"></a>Развертывание гибридной рабочей роли Runbook для Linux

Модули runbook в службе автоматизации Azure не могут получить доступ к ресурсам в других облаках или локальной среде, так как они выполняются в облаке Azure. Гибридная рабочая роль Runbook службы автоматизации Azure позволяет выполнять модули runbook непосредственно на компьютере, размещающем роль, для работы с ресурсами в среде, что позволяет управлять этими локальными ресурсами. Для хранения модулей runbook и управления ими используется служба автоматизации Azure, затем они передаются на один или несколько целевых компьютеров.

Эта функция проиллюстрирована на рисунке ниже.<br>  

![Обзор гибридного компонента Runbook Worker](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Технический обзор гибридной рабочей роли Runbook приведен в разделе [Общие сведения об архитектуре автоматизации](automation-offering-get-started.md#automation-architecture-overview). Перед началом развертывания гибридной рабочей роли Runbook ознакомьтесь со следующими сведениями о [требованиях к оборудованию и программному обеспечению](automation-offering-get-started.md#hybrid-runbook-worker) и [сведениями о подготовке сети](automation-offering-get-started.md#network-planning).  После успешного развертывания рабочей роли Runbook ознакомьтесь с [запуском модулей runbook в гибридной рабочей роли Runbook](automation-hrw-run-runbooks.md), чтобы узнать, как настроить модули runbook для автоматизации процессов в локальном центре обработки данных или другой облачной среде.     

## <a name="hybrid-runbook-worker-groups"></a>Группы гибридных компонентов Runbook Worker
Каждый гибридный компонент Runbook Worker является членом группы гибридных компонентов Runbook Worker, которая указывается при установке агента.  Группа может включать одного агента, но в нее можно установить несколько агентов для обеспечения высокого уровня доступности.

Когда вы запускаете модуль runbook в гибридной рабочей роли Runbook, вы выбираете группу для его выполнения.  Члены группы самостоятельно определят, какая из служб рабочей роли будет обслуживать этот запрос.  Указание конкретного компонента Worker для выполнения конкретной задачи не предусмотрено.

## <a name="installing-linux-hybrid-runbook-worker"></a>Установка гибридной рабочей роли Runbook Linux
Для установки и настройки гибридной рабочей роли Runbook на компьютере под управлением Linux используется очень простая процедура, позволяющая вручную установить и настроить роль.   Для этого необходимо включить решение **гибридной рабочей роли службы автоматизации** в рабочей области OMS, а затем выполнить несколько команд для регистрации компьютера в качестве рабочей роли и его добавления в новую или имеющуюся группу. 

Прежде чем продолжить, необходимо записать рабочую область Log Analytics, к которой привязана ваша учетная запись службы автоматизации, а также первичный ключ для учетной записи службы автоматизации.  Эти данные можно найти на портале, выбрав учетную запись службы автоматизации, а затем указав **Workspace** в качестве идентификатора рабочей области и **Keys** в качестве первичного ключа.  

1.  Включите решение "Гибридная рабочая роль службы автоматизации" в OMS. Для этого нужно:

   1. Из коллекции решений на [портале OMS](https://mms.microsoft.com) включите решение **Гибридная рабочая роль службы автоматизации**.
   2. Выполните следующий командлет:

        ```powershell
         $null = Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName  <ResourceGroupName> -WorkspaceName <WorkspaceName> -IntelligencePackName  "AzureAutomation" -Enabled $true
        ```

2.  Выполните следующую команду, изменив значения параметров *-w*, *-k*, *-g* и *-e*. Для параметра *-g* замените значение именем группы гибридной рабочей роли Runbook, к которой требуется присоединить новую гибридную рабочую роль Runbook Linux. Если имя уже существует в учетной записи службы автоматизации, группа гибридной рабочей роли Runbook будет создана с этим именем.
    
    ```
    sudo python /opt/microsoft/omsconfig/modules/nxOMSAutomationWorker/DSCResources/MSFT_nxOMSAutomationWorkerResource/automationworker/scripts/onboarding.py --register -w <OMSworkspaceId> -k <AutomationSharedKey> -g <hybridgroupname> -e <automationendpoint>
    ```
3. После выполнения команды в колонке "Группы гибридных рабочих ролей" на портале Azure отобразится новая группа и число элементов в ней с учетом только что добавленных.  Вы можете выбрать группу из списка на вкладке **Группы гибридных рабочих ролей** и щелкнуть колонку **Гибридные рабочие роли**.  В колонке **Гибридные рабочие роли** отображается список элементов группы.  


## <a name="turning-off-signature-validation"></a>Отключение проверки подписи 
По умолчанию для гибридных рабочих ролей Runbook Linux требуется проверка подписи. При выполнении модуля runbook для рабочей роли вы увидите сообщение об ошибке проверки подписи. Чтобы отключить проверку подписи, выполните следующую команду, заменив второй параметр своим идентификатором рабочей области OMS:

    ```
    sudo python /opt/microsoft/omsconfig/modules/nxOMSAutomationWorker/DSCResources/MSFT_nxOMSAutomationWorkerResource/automationworker/scripts/require_runbook_signature.py --false <OMSworkspaceId>
    ```
   
## <a name="next-steps"></a>Следующие шаги

* Ознакомьтесь с [запуском модулей runbook в гибридной рабочей роли Runbook](automation-hrw-run-runbooks.md), чтобы узнать, как настроить модули runbook для автоматизации процессов в локальном центре обработки данных или другой облачной среде.
* Инструкции по удалению гибридных рабочих ролей Runbook см. в статье [Удаление гибридных рабочих ролей Runbook в службе автоматизации Azure](automation-remove-hrw.md).
