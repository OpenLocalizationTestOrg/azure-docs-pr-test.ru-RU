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
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a><span data-ttu-id="ddf31-103">Использование автоматизации Azure tootrigger задания (личной предварительной версии)</span><span class="sxs-lookup"><span data-stu-id="ddf31-103">Use Azure Automation tootrigger a job (Private Preview)</span></span>

<span data-ttu-id="ddf31-104">Статьях описывается способ автоматизации Azure toouse tootrigger задания данных StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="ddf31-104">This articles describes how toouse Azure Automation tootrigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddf31-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ddf31-105">Prerequisites</span></span>

<span data-ttu-id="ddf31-106">Перед началом работы убедитесь, что у вас есть следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="ddf31-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="ddf31-107">Azure PowerShell установлен.</span><span class="sxs-lookup"><span data-stu-id="ddf31-107">Azure Powershell installed.</span></span> <span data-ttu-id="ddf31-108">[Скачать Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="ddf31-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="ddf31-109">Параметры tooinitialize hello преобразования данных задания конфигурации (tooobtain эти параметры включены здесь инструкции).</span><span class="sxs-lookup"><span data-stu-id="ddf31-109">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="ddf31-110">Определение задания, которое правильно настроено в гибридном ресурсе данных в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ddf31-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="ddf31-111">Загрузить `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) файл из репозитория github hello.</span><span class="sxs-lookup"><span data-stu-id="ddf31-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from hello github repository.</span></span>
*   <span data-ttu-id="ddf31-112">Загрузить `Get-ConfigurationParams.ps1` [сценария](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) из репозитория github hello.</span><span class="sxs-lookup"><span data-stu-id="ddf31-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from hello github repository.</span></span>
*   <span data-ttu-id="ddf31-113">Загрузить `Trigger-DataTransformation-Job.ps1` [сценария](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) из репозитория github hello.</span><span class="sxs-lookup"><span data-stu-id="ddf31-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="ddf31-114">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="ddf31-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a><span data-ttu-id="ddf31-115">Получить разрешения Azure Active Directory для определения задания для задания toorun hello автоматизации hello</span><span class="sxs-lookup"><span data-stu-id="ddf31-115">Get Azure Active Directory permissions for hello automation job toorun hello job definition</span></span>

1. <span data-ttu-id="ddf31-116">параметры конфигурации tooretrieve hello для Active Directory hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ddf31-116">tooretrieve hello configuration parameters for Active Directory, do hello following steps:</span></span>

    1. <span data-ttu-id="ddf31-117">Откройте Windows PowerShell на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ddf31-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="ddf31-118">Убедитесь, что среда [Azure PowerShell](https://azure.microsoft.com/downloads/) установлена.</span><span class="sxs-lookup"><span data-stu-id="ddf31-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="ddf31-119">Запустите hello `Get-ConfigurationParams.ps1` сценария (в папке hello загруженный выше).</span><span class="sxs-lookup"><span data-stu-id="ddf31-119">Run hello `Get-ConfigurationParams.ps1` script (in hello folder you downloaded above).</span></span> <span data-ttu-id="ddf31-120">Введите следующую команду в окне PowerShell hello hello:</span><span class="sxs-lookup"><span data-stu-id="ddf31-120">Type hello following command in hello PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="ddf31-121">Hello ActiveDirectoryKey считается пароль, который можно использовать в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="ddf31-121">hello ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="ddf31-122">Введите выбранный пароль.</span><span class="sxs-lookup"><span data-stu-id="ddf31-122">Enter a password of your choice.</span></span> <span data-ttu-id="ddf31-123">AppName может быть любой строкой.</span><span class="sxs-lookup"><span data-stu-id="ddf31-123">AppName can be any string.</span></span>

2. <span data-ttu-id="ddf31-124">Этот скрипт выводит следующие значения, которые должны использоваться во время запуска runbook службы автоматизации hello hello.</span><span class="sxs-lookup"><span data-stu-id="ddf31-124">This script outputs hello following values that should be used while triggering hello automation runbook.</span></span> <span data-ttu-id="ddf31-125">Запишите эти значения:</span><span class="sxs-lookup"><span data-stu-id="ddf31-125">Make a note of these values.</span></span>

    - <span data-ttu-id="ddf31-126">идентификатор клиента</span><span class="sxs-lookup"><span data-stu-id="ddf31-126">Client ID</span></span>
    - <span data-ttu-id="ddf31-127">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="ddf31-127">Tenant ID</span></span>
    - <span data-ttu-id="ddf31-128">Active Directory ключ (аналогично hello один на введенный выше)</span><span class="sxs-lookup"><span data-stu-id="ddf31-128">Active Directory key (same as hello one entered above)</span></span>
    - <span data-ttu-id="ddf31-129">Идентификатор подписки</span><span class="sxs-lookup"><span data-stu-id="ddf31-129">Subscription ID</span></span>

### <a name="set-up-hello-automation-account"></a><span data-ttu-id="ddf31-130">Настройка учетной записи автоматизации hello</span><span class="sxs-lookup"><span data-stu-id="ddf31-130">Set up hello Automation Account</span></span>

1. <span data-ttu-id="ddf31-131">Войдите в систему tooAzure и открыть учетную запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ddf31-131">Log on tooAzure and open your Automation account.</span></span>
2. <span data-ttu-id="ddf31-132">Нажмите кнопку **активы** плитки tooopen hello списка ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ddf31-132">Click **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="ddf31-133">Нажмите кнопку **модули** плитки tooopen hello список модулей.</span><span class="sxs-lookup"><span data-stu-id="ddf31-133">Click **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="ddf31-134">Нажмите кнопку **+ добавить модуль** кнопки и hello колонке добавить модуль будет запущен.</span><span class="sxs-lookup"><span data-stu-id="ddf31-134">Click **+ Add a module** button and hello Add module blade is launched.</span></span>

    ![Параметры учетной записи службы автоматизации](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="ddf31-136">После выбора hello `DataTransformationApp.zip` файла с локального компьютера, нажмите кнопку **ОК** tooimport hello модуля.</span><span class="sxs-lookup"><span data-stu-id="ddf31-136">After you have selected hello `DataTransformationApp.zip` file from your local computer, click **OK** tooimport hello module.</span></span>

   <span data-ttu-id="ddf31-137">Учетную запись tooyour модуля, импортирующий автоматизации Azure, он извлекает метаданные о модуле hello.</span><span class="sxs-lookup"><span data-stu-id="ddf31-137">When Azure Automation imports a module tooyour account, it extracts metadata about hello module.</span></span> <span data-ttu-id="ddf31-138">Эта операция может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ddf31-138">This operation may take a couple of minutes.</span></span>

   ![Параметры учетной записи службы автоматизации](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="ddf31-140">Вы получаете уведомление развертываемого модуля hello и еще одно уведомление после завершения процесса hello.</span><span class="sxs-lookup"><span data-stu-id="ddf31-140">You receive a notification that hello module is being deployed and another notification when hello process is complete.</span></span>  <span data-ttu-id="ddf31-141">Можно также проверить состояние hello в **модули** плитки.</span><span class="sxs-lookup"><span data-stu-id="ddf31-141">You can also check hello status in **Modules** tile.</span></span>

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a><span data-ttu-id="ddf31-142">tooimport hello runbook, которое запускает определение задания hello</span><span class="sxs-lookup"><span data-stu-id="ddf31-142">tooimport hello runbook that triggers hello job definition</span></span>

1. <span data-ttu-id="ddf31-143">Откройте в hello портал Azure, ваша учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ddf31-143">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="ddf31-144">Нажмите кнопку **Runbooks** плитки tooopen hello список модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="ddf31-144">Click **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="ddf31-145">Щелкните **+ Add a runbook** (+ Добавить модуль Runbook) и **Импортировать существующий Runbook**.</span><span class="sxs-lookup"><span data-stu-id="ddf31-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Импорт существующего модуля Runbook](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="ddf31-147">Нажмите кнопку **файл Runbook** и tooimport файла выберите hello `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="ddf31-147">Click **Runbook file** and select hello file tooimport `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="ddf31-148">Нажмите кнопку **создать** tooimport hello runbook.</span><span class="sxs-lookup"><span data-stu-id="ddf31-148">Click **Create** tooimport hello runbook.</span></span> <span data-ttu-id="ddf31-149">новый модуль runbook Hello отображается в списке hello модули Runbook для hello учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ddf31-149">hello new runbook appears in hello list of runbooks for hello Automation account.</span></span>
7. <span data-ttu-id="ddf31-150">Щелкните модуль Runbook **Trigger-DataTransformation-Job** и нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="ddf31-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="ddf31-151">Щелкните **Опубликовать** и при появлении запроса на подтверждение щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="ddf31-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="toorun-hello-runbook"></a><span data-ttu-id="ddf31-152">toorun hello runbook:</span><span class="sxs-lookup"><span data-stu-id="ddf31-152">toorun hello runbook:</span></span>
1. <span data-ttu-id="ddf31-153">Откройте в hello портал Azure, ваша учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ddf31-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="ddf31-154">Нажмите кнопку hello **Runbooks** плитки tooopen hello список модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="ddf31-154">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="ddf31-155">Щелкните **Trigger-DataTransformation-Job**.</span><span class="sxs-lookup"><span data-stu-id="ddf31-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="ddf31-156">Нажмите кнопку **запустить** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="ddf31-156">Click **Start** toostart hello runbook.</span></span>

   ![Запуск модуля Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="ddf31-158">В hello **запустить runbook** колонки, введите все параметры hello.</span><span class="sxs-lookup"><span data-stu-id="ddf31-158">In hello **Start runbook** blade, enter all hello parameters.</span></span> <span data-ttu-id="ddf31-159">Нажмите кнопку **ОК** toosubmit hello преобразования данных задания.</span><span class="sxs-lookup"><span data-stu-id="ddf31-159">Click **OK** toosubmit hello Data Transformation job.</span></span>

   ![Запуск модуля Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="ddf31-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ddf31-161">Next steps</span></span>

<span data-ttu-id="ddf31-162">[Использовать пользовательский Интерфейс диспетчера данных StorSimple tootransform данные](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="ddf31-162">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
