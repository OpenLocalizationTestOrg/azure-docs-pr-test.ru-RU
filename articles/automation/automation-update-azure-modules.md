---
title: "aaaUpdate Azure модули в службе автоматизации Azure | Документы Microsoft"
description: "В этой статье описывается, как можно обновить общие модули Azure PowerShell, предоставленные по умолчанию в службе автоматизации Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a>Как tooupdate модули Azure PowerShell в службе автоматизации Azure

наиболее распространенные модули Azure PowerShell Hello предоставляются по умолчанию в каждой учетной записи автоматизации.  Hello Azure команды обновления регулярно hello модули Azure, в учетной записи автоматизации hello мы предоставляют вы tooupdate hello модули в учетной записи hello Если доступны новые версии с портала hello.  

Так как модули регулярно обновляются по группе продуктов hello, изменения могут происходить с помощью командлетов hello включены, что может отрицательно повлиять на модули Runbook в зависимости от типа hello изменения, например переименование параметра или полностью исключения устаревшего командлета. модули Runbook и hello, влияющие на tooavoid процессов они автоматизации, тестирования и проверки перед продолжением настоятельно рекомендуется.  Если выделенной учетной записи автоматизации, предназначенные для этой цели нет, рекомендуется создать один, благодаря чему можно протестировать различных сценариях и перестановок во время разработки hello из модулей Runbook, в добавление tooiterative изменения, такие как обновление hello Модули PowerShell.  После проверки результатов hello и применены необходимые изменения, продолжить согласование hello миграции все модули Runbook, необходимые изменения и выполнить обновление hello, как описано ниже в рабочей среде.     

## <a name="updating-azure-modules"></a>Обновление модулей Azure

1. В модулях hello колонке вашей учетной записи автоматизации, существует вариант называется **модули Azure обновления**.  Он всегда включен.<br><br> ![Параметр Update Azure Modules (Обновление модулей Azure) в колонке "Модули"](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. Нажмите кнопку **модули Azure обновления** и появляется подтверждение уведомление с вопросом, следует ли toocontinue.<br><br> ![Уведомление об обновлении модулей Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. Нажмите кнопку **Да** и начнется процесс обновления модуля hello.  процесс обновления Hello занимает около 15-20 минут tooupdate hello следующие модули:

  * Таблицы Azure
  * Azure.Storage;
  * AzureRm.Automation;
  * AzureRm.Compute;
  * AzureRm.Profile;
  * AzureRm.Resources;
  * AzureRm.Sql;
  * AzureRm.Storage.

    Модули hello, копирование toodate, процесс hello будет завершен через несколько секунд.  После завершения процесса обновления hello вы получите уведомление.<br><br> ![Состояние обновления Update Azure Modules (Обновление модулей Azure)](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> Службы автоматизации Azure будет использовать последнюю модули hello в вашей учетной записи автоматизации при запуске нового запланированного задания.    

При использовании командлетов из этих модулей Azure PowerShell в вашей toomanage модулей Runbook Azure ресурсов, то обычно tooperform этот процесс обновления каждый месяц или т tooassure, у вас есть hello последних модулей.

## <a name="next-steps"></a>Дальнейшие действия

* toolearn Дополнительные сведения о модулях интеграции и как пользовательские модули toofurther toocreate интегрировать автоматизации с других систем, служб и решений, в разделе [модули интеграции](automation-integration-modules.md).

* Рассмотрите возможность использования интеграции управления источника [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) или [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally управления и контроля версий портфеля автоматизации runbook и конфигурации.  
