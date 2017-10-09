---
title: "tootrigger автоматизации Azure aaaUse задание | Документы Microsoft"
description: "Узнайте, как toouse автоматизации Azure для запуска заданий диспетчера данных StorSimple (личной предварительной версии)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a>Использование автоматизации Azure tootrigger задания (личной предварительной версии)

Статьях описывается способ автоматизации Azure toouse tootrigger задания данных StorSimple Manager.

## <a name="prerequisites"></a>Предварительные требования

Перед началом работы убедитесь, что у вас есть следующие компоненты:

*   Azure PowerShell установлен. [Скачать Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Параметры tooinitialize hello преобразования данных задания конфигурации (tooobtain эти параметры включены здесь инструкции).
*   Определение задания, которое правильно настроено в гибридном ресурсе данных в группе ресурсов.
*   Загрузить `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) файл из репозитория github hello.
*   Загрузить `Get-ConfigurationParams.ps1` [сценария](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) из репозитория github hello.
*   Загрузить `Trigger-DataTransformation-Job.ps1` [сценария](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) из репозитория github hello.

## <a name="step-by-step"></a>Пошаговое руководство

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a>Получить разрешения Azure Active Directory для определения задания для задания toorun hello автоматизации hello

1. параметры конфигурации tooretrieve hello для Active Directory hello следующие действия:

    1. Откройте Windows PowerShell на локальном компьютере. Убедитесь, что среда [Azure PowerShell](https://azure.microsoft.com/downloads/) установлена.
    1. Запустите hello `Get-ConfigurationParams.ps1` сценария (в папке hello загруженный выше). Введите следующую команду в окне PowerShell hello hello:

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        Hello ActiveDirectoryKey считается пароль, который можно использовать в дальнейшем. Введите выбранный пароль. AppName может быть любой строкой.

2. Этот скрипт выводит следующие значения, которые должны использоваться во время запуска runbook службы автоматизации hello hello. Запишите эти значения:

    - идентификатор клиента
    - Tenant ID
    - Active Directory ключ (аналогично hello один на введенный выше)
    - Идентификатор подписки

### <a name="set-up-hello-automation-account"></a>Настройка учетной записи автоматизации hello

1. Войдите в систему tooAzure и открыть учетную запись автоматизации.
2. Нажмите кнопку **активы** плитки tooopen hello списка ресурсов.
3. Нажмите кнопку **модули** плитки tooopen hello список модулей.
4. Нажмите кнопку **+ добавить модуль** кнопки и hello колонке добавить модуль будет запущен.

    ![Параметры учетной записи службы автоматизации](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. После выбора hello `DataTransformationApp.zip` файла с локального компьютера, нажмите кнопку **ОК** tooimport hello модуля.

   Учетную запись tooyour модуля, импортирующий автоматизации Azure, он извлекает метаданные о модуле hello. Эта операция может занять несколько минут.

   ![Параметры учетной записи службы автоматизации](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. Вы получаете уведомление развертываемого модуля hello и еще одно уведомление после завершения процесса hello.  Можно также проверить состояние hello в **модули** плитки.

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a>tooimport hello runbook, которое запускает определение задания hello

1. Откройте в hello портал Azure, ваша учетная запись автоматизации.
2. Нажмите кнопку **Runbooks** плитки tooopen hello список модулей Runbook.
3. Щелкните **+ Add a runbook** (+ Добавить модуль Runbook) и **Импортировать существующий Runbook**.

   ![Импорт существующего модуля Runbook](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. Нажмите кнопку **файл Runbook** и tooimport файла выберите hello `Trigger-DataTransformation-Job.ps1`.
5. Нажмите кнопку **создать** tooimport hello runbook. новый модуль runbook Hello отображается в списке hello модули Runbook для hello учетной записи автоматизации.
7. Щелкните модуль Runbook **Trigger-DataTransformation-Job** и нажмите кнопку **Изменить**.
8. Щелкните **Опубликовать** и при появлении запроса на подтверждение щелкните **Да**.


### <a name="toorun-hello-runbook"></a>toorun hello runbook:
1. Откройте в hello портал Azure, ваша учетная запись автоматизации.
2. Нажмите кнопку hello **Runbooks** плитки tooopen hello список модулей Runbook.
3. Щелкните **Trigger-DataTransformation-Job**.
4. Нажмите кнопку **запустить** toostart hello runbook.

   ![Запуск модуля Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. В hello **запустить runbook** колонки, введите все параметры hello. Нажмите кнопку **ОК** toosubmit hello преобразования данных задания.

   ![Запуск модуля Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a>Дальнейшие действия

[Использовать пользовательский Интерфейс диспетчера данных StorSimple tootransform данные](storsimple-data-manager-ui.md).
