---
title: "aaaIntegrate автоматизации Azure с системой управления версиями Visual Stuido Team Services | Документы Microsoft"
description: "В этой статье описан сценарий настройки интеграции учетной записи службы автоматизации Azure с системой управления версиями Visual Studio Team Services."
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: "azure powershell, VSTS, система управления версиями, служба автоматизации"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Сценарий службы автоматизации Azure: интеграция системы управления версиями службы автоматизации с Visual Studio Team Services

В этом сценарии у вас есть проект Visual Studio Team Services, что вы используете toomanage Runbook автоматизации Azure или конфигураций DSC в системе управления версиями.
В этой статье описывается как toointegrate VSTS с среде автоматизации Azure, так что непрерывной интеграции происходит для каждого возврата.

## <a name="getting-hello-scenario"></a>Начало сценария hello

Этот сценарий состоит из двух Runbook PowerShell, которые можно импортировать напрямую из hello [коллекции модулей Runbook](automation-runbook-gallery.md) в hello портал Azure или загрузить с hello [коллекции PowerShell](https://www.powershellgallery.com).

### <a name="runbooks"></a>Модули Runbook

Модуль Runbook | Описание| 
--------|------------|
Sync-VSTS | Импорт модулей Runbook или конфигураций из системы управления версиями VSTS, когда выполняется возврат. При запуске вручную, он импортируется и опубликовать все модули Runbook и конфигурации в hello учетной записи автоматизации.| 
Sync-VSTSGit | Импорт модулей Runbook или конфигураций из системы управления версиями Git VSTS, когда выполняется возврат. При запуске вручную, он импортируется и опубликовать все модули Runbook и конфигурации в hello учетной записи автоматизации.|

### <a name="variables"></a>Переменные

Переменная | Описание|
-----------|------------|
VSToken | Безопасный контейнер переменной будет создан, содержащий hello VSTS личный маркер доступа. Вы узнаете, как toocreate VSTS personal получать доступ к маркера на hello [страницу проверки подлинности VSTS](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview). 
## <a name="installing-and-configuring-this-scenario"></a>Установка и настройка данного сценария

Создание [личный маркер доступа](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) в VSTS, который будет использоваться модули Runbook toosync hello или конфигураций в вашу учетную запись автоматизации.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

Создание [переменной $secure](automation-variables.md) в ваш hello toohold учетной записи автоматизации личных доступа токен hello runbook для проверки подлинности, модули Runbook hello tooVSTS и синхронизации или конфигураций в hello учетной записи автоматизации. Можно назвать ее VSToken. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Импорт runbook hello, будут синхронизироваться модулей Runbook или конфигураций в учетной записи автоматизации hello. Можно использовать hello [VSTS пример модуля runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) или hello [VSTS с Git пример runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) из hello PowerShellGallery.com в зависимости от того, если использовать VSTS исходный элемент управления или VSTS с Git и развернуть tooyour учетной записи автоматизации.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

Теперь можно [опубликовать](automation-creating-importing-runbook.md#publishing-a-runbook) этот модуль Runbook, чтобы затем создать объект webhook. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

Создание [веб-перехватчика](automation-webhooks.md) для этой runbook VSTS синхронизации и заполните параметры hello, как показано ниже. Убедитесь, что скопируйте URL-адрес веб-перехватчика hello, как он понадобится для службы обработчик в VSTS. Hello VSAccessTokenVariableName является именем hello (VSToken) безопасный переменной hello, созданный ранее toohold hello личный маркер доступа. 

Интеграция с VSTS (синхронизации VSTS.ps1) займет hello следующие параметры.
### <a name="sync-vsts-parameters"></a>Параметры Sync-VSTS

Параметр | Описание| 
--------|------------|
WebhookData | Этот элемент будет содержать hello возврат сведений, полученных от службы ловушек hello VSTS. Этот параметр следует оставить пустым.| 
ResourceGroup | Это имя hello hello группы ресурсов, учетная запись автоматизации hello.|
AutomationAccountName | Имя учетной записи автоматизации hello, будут синхронизироваться с VSTS Hello.|
VSFolder | Имя папки hello в VSTS, где существует Runbook hello и конфигураций.|
VSAccount | Имя учетной записи Visual Studio Team Services hello Hello.| 
VSAccessTokenVariableName | Имя Hello hello безопасного переменной (VSToken), содержащей hello VSTS личный маркер доступа.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

Если вы используете VSTS с GIT (синхронизации VSTSGit.ps1), необходимое hello следующие параметры.

Параметр | Описание|
--------|------------|
WebhookData | Этот элемент будет содержать hello возврат сведений, полученных от службы ловушек hello VSTS. Этот параметр следует оставить пустым.| ResourceGroup | Имя группы ресурсов hello, учетная запись автоматизации hello этот hello.|
AutomationAccountName | Имя учетной записи автоматизации hello, будут синхронизироваться с VSTS Hello.|
VSAccount | Имя учетной записи Visual Studio Team Services hello Hello.|
VSProject | Hello имя проекта hello в VSTS, где существует Runbook hello и конфигураций.|
GitRepo | Имя репозитория Git hello Hello.|
GitBranch | Имя Hello hello ветви в репозитории VSTS.|
Папка | Имя Hello hello папки в ветвь VSTS Git.|
VSAccessTokenVariableName | Имя Hello hello безопасного переменной (VSToken), содержащей hello VSTS личный маркер доступа.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

Создайте обработчик службы в VSTS для папки toohello возвратов, запускающее этот веб-перехватчик при возврате кода. Выберите веб-обработчиков как hello toointegrate службы с при создании новой подписки. Дополнительные сведения о перехватчиках события см. в статье [Integrate with service hooks](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started) (Интеграция с перехватчиками события).
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

Должна теперь быть может toodo всех регистраций модулей Runbook и конфигураций в VSTS, и они были автоматически синхронизироваться бы в вашу учетную запись автоматизации.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

Если запустить этот runbook вручную не запустилась, VSTS, параметр webhookdata hello можно оставить пустым, и он будет выполнять полной синхронизации в указанной папке VSTS hello.

При необходимости сценарий hello toouninstall удалить hello службы ловушек из VSTS, удалить hello runbook и переменной VSToken hello.
