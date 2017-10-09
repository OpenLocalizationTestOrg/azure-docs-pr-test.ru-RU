---
title: "aaaSource интеграцию с системой управления в службе автоматизации Azure | Документы Microsoft"
description: "В этой статье описывается интеграция системы управления версиями с GitHub в службе автоматизации Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 224d7375-9887-44dd-b137-06ffe396a4b4
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 6ceee1de8065fafe85a13bbd7f585e74dbc96b47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Интеграция системы управления версиями в службе автоматизации Azure
Интеграция системы управления версиями позволяет tooassociate Runbook в хранилище управления версиями автоматизации учетной записи tooa GitHub. Система управления версиями позволяет tooeasily сотрудничать с рабочей группой, отслеживания изменений и отката версии tooearlier из модулей Runbook. Например система управления версиями позволяет вам toosync другой ветви в системе управления версиями tooyour разработки, тестирования или производственных учетные записи автоматизации, сделав его легко toopromote код, который был протестирован в рабочей среде tooyour разработки автоматизации Учетная запись.

Системы управления версиями позволяет toopush кода из элемента управления toosource автоматизации Azure или по запросу из источника управления tooAzure автоматизации модулей Runbook. Этой статье описывается, как контролировать tooset источник в среде автоматизации Azure. Мы начинается путем настройки службы автоматизации Azure tooaccess репозиторий GitHub и показывает, как различные операции, которые можно выполнять с помощью интеграции системы управления версиями. 

> [!NOTE]
> Система управления версиями поддерживает извлечение и отправку [модулей Runbook рабочих процессов PowerShell](automation-runbook-types.md#powershell-workflow-runbooks), а также [модулей Runbook PowerShell](automation-runbook-types.md#powershell-runbooks). [Графические модули Runbook](automation-runbook-types.md#graphical-runbooks) пока не поддерживаются.<br><br>
> 
> 

Существует два простых шагов требуется tooconfigure систему управления версиями для вашей учетной записи автоматизации и только один, если у вас уже есть учетная запись GitHub. К ним относятся:

## <a name="step-1--create-a-github-repository"></a>Шаг 1. Создание репозитория GitHub
Если уже имеется учетная запись GitHub и репозитория, который будет toolink tooAzure автоматизации, а затем существующих tooyour входа учетную запись и начать с шага 2 ниже. В противном случае перейдите слишком[GitHub](https://github.com/), зарегистрировать новую учетную запись и [создать новый репозиторий](https://help.github.com/articles/create-a-repo/).

## <a name="step-2--set-up-source-control-in-azure-automation"></a>Шаг 2. Настройка системы управления версиями в службе автоматизации Azure
1. Из колонки hello учетной записи автоматизации в hello портал Azure, щелкните **задайте копии системы управления версиями.** 
   
    ![Настройка системы управления версиями](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. Hello **системы управления версиями** открывает колонку, где можно настроить сведений о своей учетной записи GitHub. Ниже приведен список параметров tooconfigure hello.  
   
   | **Параметр** | **Описание** |
   |:--- |:--- |
   | Выбор источника |Выберите источник hello. В настоящее время поддерживается только **GitHub** . |
   | Авторизация |Нажмите кнопку hello **авторизовать** кнопку toogrant автоматизации Azure access tooyour репозитории GitHub. Если вы уже вошли в tooyour учетной записи GitHub в другом окне, а затем hello используются учетные данные этой учетной записи. Авторизация прошла успешно, hello колонки будут отображены свое имя пользователя GitHub под **авторизации свойство**. |
   | Выберите репозиторий |Выберите репозиторий GitHub из hello список доступных репозиториев. |
   | Выберите ветвь |Выберите ветвь из списка доступных ветвей hello. Здравствуйте, только **master** ветвь отображается, если вы еще не создали все ветви. |
   | Путь к папке Runbook |путь к папке runbook Hello указывает путь hello в репозитории GitHub hello требуется toopush или кода по запросу. Он должен быть указан в формате hello **папки/имя папки/имя вложенной папки**. Только модули в путь к папке hello runbook будет синхронизирован tooyour учетной записи автоматизации. Модули Runbook в подпапках hello hello путь к папке runbook будут **не** синхронизируются. Используйте  **/**  toosync все hello модулей Runbook в репозиторий hello. |
3. Например, ваш репозиторий называется **PowerShellScripts**, и он содержит папку **RootFolder** с вложенной папкой **SubFolder**. Можно использовать следующие строки toosync hello каждый уровень папки:
   
   1. toosync Runbook из **репозитория**, путь к папке runbook*/*
   2. toosync Runbook из **RootFolder**, путь к папке runbook */RootFolder*
   3. toosync Runbook из **вложенную папку**, путь к папке runbook */RootFolder/вложенную папку*.
4. После настройки параметров hello, они отображаются на hello **колонке задайте копии системы управления версиями.**  
   
    ![Колонка "Настройка"](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. После того как вы нажмете кнопку "ОК", интеграция системы управления версиями будет настроена для вашей учетной записи службы автоматизации. Теперь нужно добавить в нее сведения из учетной записи GitHub. Теперь можно нажать на этой части tooview все системы управления версиями синхронизации журнал заданий.  
   
    ![Значения репозитория](media/automation-source-control-integration/automation_03_RepoValues.png)
6. После настройки системы управления версиями hello следующие ресурсы автоматизации будет создана в вашей учетной записи автоматизации:  
   Два [ресурса переменных](automation-variables.md).  
   
   * переменная приветствия **Microsoft.Azure.Automation.SourceControl.Connection** содержит значения hello hello строки соединения, как показано ниже.  
     
     | **Параметр** | **Значение** |
     |:--- |:--- |
     | Имя |Microsoft.Azure.Automation.SourceControl.Connection |
     | Тип |Строка |
     | Значение |{"Branch":\<*имя ветви*>,"RunbookFolderPath":\<*путь к папке с модулями Runbook*>,"ProviderType":\<*для GitHub значение равно 1*>,"Repository":\<*имя репозитория*>,"Username":\<*имя пользователя GitHub*>} |

    * переменная приветствия **Microsoft.Azure.Automation.SourceControl.OAuthToken**, содержит безопасное зашифрованное значение hello вашей OAuthToken.  

    |**Параметр**            |**Значение** |
    |:---|:---|
    | Имя  | Microsoft.Azure.Automation.SourceControl.OAuthToken |
    | Тип | Unknown(Encrypted) |
    | Значение | <*Зашифрованное значение OAuthToken*> |  

    ![Переменные](media/automation-source-control-integration/automation_04_Variables.png)  

    * **Автоматизация системы управления версиями** добавляется в качестве tooyour прав учетной записи GitHub. приложение hello tooview: домашней странице GitHub перейдите tooyour **профиль** > **параметры** > **приложений**. Это приложение позволяет toosync автоматизации Azure вашей tooan репозитория GitHub учетной записи автоматизации.  

    ![Приложение Git](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>Использование системы управления версиями в службе автоматизации
### <a name="check-in-a-runbook-from-azure-automation-toosource-control"></a>Возврат runbook из системы управления toosource автоматизации Azure
Возврат Runbook можно toopush hello внесенные изменения tooa runbook в автоматизации Azure в репозитории управления версиями. Ниже приведены шаги hello toocheck в runbook.

1. Находясь в своей учетной записи службы автоматизации, [создайте текстовый модуль Runbook](automation-first-runbook-textual.md) или [измените существующий](automation-edit-textual-runbook.md). Этот модуль может быть модулем Runbook рабочего процесса PowerShell или сценария PowerShell.  
2. После изменения модуля runbook, сохраните его и нажмите кнопку **возврат** из hello **изменить** колонку.  
   
    ![Кнопка "Возврат"](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > Возврат из службы автоматизации Azure будет перезаписан hello код, который в настоящий момент в свою систему управления версиями. — Hello инструкция эквивалент командной строки Git в toocheck **добавить git + принудительной фиксации git + git**  

1. При нажатии кнопки **возврата**, выводится сообщение с подтверждением, нажмите кнопку Да toocontinue.  
   
    ![Сообщение возврата](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. Возврат начинается hello runbook управления источника: **MicrosoftAzureAutomationAccountToGitHubV1 синхронизации**. Этот runbook подключается tooGitHub и передает изменения с репозиторием tooyour автоматизации Azure. Здравствуйте tooview возврат журнал заданий, вернитесь к предыдущему окну toohello **интеграции системы управления версиями** и нажмите кнопку tooopen hello синхронизации репозитория колонку. В этой колонке будут показаны все задания из системы управления версиями.  Выберите задание hello tooview и щелкните tooview hello сведения.  
   
    ![Модуль Runbook для возврата](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > Модули Runbook системы управления версиями — это особые модули Runbook службы автоматизации, недоступные для просмотра и изменения. Они не включаются в список модулей Runbook, однако в списке заданий отображаются задачи синхронизации.
   > 
   > 
3. Имя Hello hello изменить runbook отправляется как входной параметр toohello возврата runbook. Вы можете [просмотра сведений о задании hello](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) , развернув runbook в **синхронизации репозитория** колонку.  
   
    ![Входные данные для возврата](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. После завершения задания hello tooview hello изменения, обновите репозиторий GitHub.  Должна существовать фиксации в репозиторий с сообщение фиксации: **Updated *имя Runbook* в службе автоматизации Azure.**  

### <a name="sync-runbooks-from-source-control-tooazure-automation"></a>Синхронизация Runbook из исходного элемента управления tooAzure автоматизации
Кнопка "Синхронизация" Hello в колонке hello репозитория синхронизации позволяет toopull все hello Runbook в путь к папке hello runbook из вашего репозитория tooyour учетной записи автоматизации. Hello одного репозитория может быть синхронизирован toomore чем одну учетную запись автоматизации. Ниже приведены шаги toosync hello runbook.

1. Hello учетной записи автоматизации, где Настройка системы управления версиями, откройте hello **колонке синхронизации интеграции или репозиторий системы управления источника** и нажмите кнопку **синхронизации** то вам будет предложено с подтверждением сообщение, нажмите кнопку **Да** toocontinue.  
   
    ![Кнопка "Синхронизация"](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. Синхронизация начинается hello runbook: **MicrosoftAzureAutomationAccountFromGitHubV1 синхронизации**. Этот runbook подключается tooGitHub и запрашивает изменения hello из вашего репозитория tooAzure автоматизации. Вы увидите новое задание hello **синхронизации репозитория** колонку для этого действия. tooview сведения о задании синхронизации hello, щелкните задание сведения tooopen hello колонку.  
   
    ![Модуль Runbook для синхронизации](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > Синхронизация из системы управления версиями перезаписывает hello черновик Runbook hello, существующие в вашей учетной записи автоматизации для **все** Runbook, которые в настоящее время система управления версиями. Hello является инструкция toosync эквивалент командной строки Git **получение git**


## <a name="troubleshooting-source-control-problems"></a>Устранение неполадок с системой управления версиями
Если имеются ошибки с заданием возврата или синхронизации, состояние задания hello следует приостановить и можно просмотреть дополнительные сведения об ошибке hello в колонке задания hello.  Hello **все журналы** часть отобразит все hello PowerShell потоки, связанные с этим заданием. Это обеспечит вам с подробными сведениями hello требовалась toohelp устранения неполадок с возвратом или синхронизации. Он также будет показано hello последовательность действий, возникших во время синхронизации или проверку в runbook.  

![Образ AllLogs](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>Отключение системы управления версиями
toodisconnect из вашей учетной записи GitHub, откройте колонку синхронизации репозитория hello и щелкните **Disconnect**. После отключения системы управления версиями модулей Runbook, которые были ранее синхронизированы по-прежнему останется в вашей учетной записи автоматизации, но колонке синхронизации репозитория hello не будет включен.  

  ![Кнопка "Отключить"](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об интеграции системы управления версиями см. в разделе hello следующие ресурсы:  

* [Azure Automation: Source Control Integration in Azure Automation](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [Vote for your favorite source control system](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Azure Automation: Integrating Runbook Source Control using Visual Studio Team Services](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

