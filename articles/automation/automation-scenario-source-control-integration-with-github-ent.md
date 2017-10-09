---
title: "aaaAzure автоматизации интеграция системы управления версиями с GitHub Enterprise | Документы Microsoft"
description: "Описывает hello подробные сведения о том, как интеграция tooconfigure с GitHub Enterprise для системы управления версиями модулей автоматизации Runbook."
services: automation
documentationCenter: 
authors: mgoedtel
manager: jwhit
editor: 
ms.assetid: e01d817c-7d38-421c-adf5-647a4b526eb4
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: magoedte
ms.openlocfilehash: 915d36ccabb72fdee1dba663049a0b331249cd73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a>Сценарий службы автоматизации Azure: интеграция системы управления версиями службы автоматизации с GitHub Enterprise

Автоматизация в настоящее время поддерживает интеграции системы управления версиями, позволяющую tooassociate Runbook в хранилище управления версиями автоматизации учетной записи tooa GitHub.  Тем не менее пользователи, установившие [GitHub Enterprise](https://enterprise.github.com/home) toosupport их DevOps рекомендациям, также требуется toouse его жизненного цикла hello toomanage модулей Runbook, которые разработаны tooautomate бизнес-процессов и управления службами операции.  

В этом случае у вас компьютер Windows в центре обработки данных настроен в качестве гибридной рабочей роли Runbook с модулями Azure Resource Manager hello и установлены инструменты Git.  Hello гибридного рабочий компьютер имеет клон hello локального репозитория Git.  При запуске hello runbook в гибридной рабочей роли hello hello Git directory синхронизируется и содержимое файла hello runbook импортируются в hello учетной записи автоматизации.

В этой статье описывается как tooset конфигурации в среде автоматизации Azure. Мы начнем с Настройка автоматизации с учетными данными безопасности hello, модули Runbook требуется toosupport этот сценарий и развертывание гибридной рабочей роли Runbook в данных центра toorun hello runbooks и доступ к вашей toosynchronize репозитория GitHub Enterprise модули Runbook с вашей учетной записи автоматизации.  


## <a name="getting-hello-scenario"></a>Начало сценария hello

Этот сценарий состоит из двух Runbook PowerShell, которые можно импортировать напрямую из hello [коллекции модулей Runbook](automation-runbook-gallery.md) в hello портал Azure или загрузить с hello [коллекции PowerShell](https://www.powershellgallery.com).

### <a name="runbooks"></a>Модули Runbook

Модуль Runbook | Описание| 
--------|------------|
Export-RunAsCertificateToHybridWorker | Runbook экспортирует запуска от имени сертификата из учетной записи tooa гибридная рабочая роль автоматизации модулей Runbook в рабочем процессе hello для проверки подлинности с помощью Azure в модулях Runbook tooimport заказа в hello учетной записи автоматизации.| 
Sync-LocalGitFolderToAutomationAccount | Синхронизация Runbook hello локальной папке Git на компьютере гибридного hello, а затем импортировать файлов runbook hello (*.ps1) в учетной записи автоматизации hello.|

### <a name="credentials"></a>Учетные данные

Учетные данные | Описание|
-----------|------------|
GitHRWCredential | Ресурс учетных данных для создания toocontain hello пользователя и пароль для пользователя разрешения toohello гибридной рабочей роли.|

## <a name="installing-and-configuring-this-scenario"></a>Установка и настройка данного сценария

### <a name="prerequisites"></a>Предварительные требования

1. runbook Hello синхронизации LocalGitFolderToAutomationAccount осуществляется с использованием hello [учетная запись запуска от имени Azure](automation-sec-configure-azure-runas-account.md). 

2. Также требуется рабочая область Microsoft Operations Management Suite (OMS) с hello решение автоматизации Azure включена и настроена.  Если у вас та, которая связана с tooinstall учетная запись, используемая для автоматизации hello и настроить такой сценарий, он создается и настраивается автоматически при выполнении hello **New OnPremiseHybridWorker.ps1** сценария гибридной hello рабочий процесс Runbook.        

    > [!NOTE]
    > В настоящее время hello следующие регионы поддерживают только автоматизации интеграция с OMS - **Юго-Восточная Австралия**, **восточная часть США 2**, **Юго-Восточная Азия**, и **Западная Европа**. 

3. Компьютер, который можно использовать как выделенный гибридную рабочую роль Runbook, также будут размещаться программного обеспечения GitHub hello и хранить файлы runbook hello (*runbook*.ps1) в исходной папке на toosynchronize системы hello файла между GitHub и Учетная запись автоматизации.

### <a name="import-and-publish-hello-runbooks"></a>Импорт и публикации Runbook hello

tooimport hello *экспорта RunAsCertificateToHybridWorker* и *LocalGitFolderToAutomationAccount синхронизации* Runbook из hello коллекции модулей Runbook из вашей учетной записи автоматизации в hello портал Azure следуйте процедурам hello в [импорта Runbook из коллекции модулей Runbook hello](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal). Публикации Runbook hello, после они были успешно импортированы в вашей учетной записи автоматизации.

### <a name="deploy-and-configure-hybrid-runbook-worker"></a>Развертывание и настройка гибридной рабочей роли Runbook

Если у вас гибридная рабочая роль Runbook, уже развернутых в центре обработки данных, следует ознакомьтесь с требованиями к hello и действуйте hello автоматической установки с помощью процедуры hello в [Azure Automation гибридных рабочих ролей Runbook - автоматизации установки и конфигурация](automation-hybrid-runbook-worker.md#automated-deployment).  После hello гибридной рабочей роли был успешно установлен на компьютере, выполните hello следующие toocomplete действия, его конфигурации toosupport этот сценарий.

1. Войдите на toohello компьютере размещения hello гибридной рабочей роли Runbook с помощью учетной записи с правами локального администратора и создание файлов каталога toohold hello Git runbook.  Клон hello внутренней Git toohello каталог-репозиторий.
2. Если вы еще нет учетной записи запуска от имени созданной или toocreate новый для этой цели, из портала Azure hello перейдите tooAutomation учетные записи, выберите учетную запись автоматизации и создать [актива учетных данных](automation-credentials.md) , содержит hello пользователя и пароль для пользователя с разрешениями toohello гибридной рабочей роли.  
3. Из учетной записи автоматизации [редактирование hello runbook](automation-edit-textual-runbook.md)**экспорта RunAsCertificateToHybridWorker** и измените значение переменной hello hello *$Password* с надежный пароль.    После изменения значения hello щелкните **публикации** toohave hello черновик hello runbook публикации. 
5. Запустить hello runbook **экспорта RunAsCertificateToHybridWorker**и в hello **запустить Runbook** колонки в параметре hello **параметры запуска** выберите параметр hello **Гибридной рабочей роли** и в группу hello раскрывающегося списка выберите hello гибридных рабочих ролей с ранее созданный для этого сценария.  

    Выполняется экспорт сертификата toohello гибридной рабочей роли Runbook на hello работника для проверки подлинности с Azure с помощью hello запуска от имени соединения в порядке toomanage ресурсов Azure (в частности, для этого сценария - Импорт модулей Runbook toohello учетную запись автоматизации).

4. Из учетной записи автоматизации, выберите hello группу гибридных рабочих ролей, созданную ранее и [указать учетную запись запуска от имени](automation-hrw-run-runbooks.md#runas-account) hello группу гибридных рабочих ролей и выбрал hello учетных данных ОС просто или уже создана.  Это гарантирует, что этого модуля hello синхронизации можно выполнить команды Git. 
5. Запустить hello runbook **синхронизации LocalGitFolderToAutomationAccount**, предоставляют hello следующие обязательные значения входных параметров и в hello **запустить Runbook** колонки в параметре hello **запуска Параметры** выберите параметр hello **гибридной рабочей роли** и в группу hello раскрывающегося списка выберите hello гибридных рабочих ролей с ранее созданный для этого сценария:
    * *Группа ресурсов* - hello имя вашей группы ресурсов, связанных с вашей учетной записи автоматизации
    * *AutomationAccountName* — hello имя учетной записи автоматизации
    * *GitPath* - hello локальную папку или файл на hello гибридную рабочую роль Runbook где Git Настройка toopull последние изменения в

    Это будет синхронизировать hello локальной папке Git на компьютере рабочей гибридного hello и затем импортировать hello ps1-файлы из hello исходный каталог toohello учетной записи автоматизации.

    ![Start Sync-LocalGitFolderToAutomationAccount Runbook](media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. Просмотреть сводные данные задания для hello runbook, выбрав его из hello **Runbooks** колонки в вашей учетной записи автоматизации и выберите hello **заданий** плитки.  Подтвердите успешное завершение, выбрав hello **все журналы** плитки и рецензирования hello подробный журнал потока.  

## <a name="next-steps"></a>Дальнейшие действия

-  в разделе tooknow Дополнительные сведения о типах runbook, их преимущества и ограничения, [типов runbook службы автоматизации Azure](automation-runbook-types.md)
-  Дополнительные сведения о функции поддержки скриптов PowerShell см. в статье [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Встроенная поддержка скриптов PowerShell в службе автоматизации Azure).
