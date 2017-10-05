---
title: "Установка среды выполнения Функций Azure | Документация Майкрософт"
description: "Как установить среду выполнения Функций Azure."
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 1e4188313a87d07f396e5f8edc8969dd5da2c436
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="5c9ca-103">Установка предварительной версии среды выполнения Функций Azure</span><span class="sxs-lookup"><span data-stu-id="5c9ca-103">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="5c9ca-104">Если вы хотите установить предварительную версию среды выполнения Функций Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5c9ca-104">If you would like to install the Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="5c9ca-105">Убедитесь, что компьютер соответствует минимальным требованиям.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-105">Ensure your machine passes the minimum requirements</span></span>
1. <span data-ttu-id="5c9ca-106">Скачайте [установщик предварительной версии среды выполнения Функций Azure](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="5c9ca-106">Download the [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="5c9ca-107">Установка предварительной версии среды выполнения Функций Azure</span><span class="sxs-lookup"><span data-stu-id="5c9ca-107">Install the Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="5c9ca-108">Завершите настройку предварительной версии среды выполнения Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-108">Complete the configuration of the Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c9ca-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c9ca-109">Prerequisites</span></span>

<span data-ttu-id="5c9ca-110">Перед установкой предварительной версии среды выполнения Функций Azure вам понадобятся следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="5c9ca-110">Before you install the Azure Functions Runtime preview, you must have the following:</span></span>

1. <span data-ttu-id="5c9ca-111">Компьютер под управлением Microsoft Windows Server 2016 или обновление Microsoft Windows 10 для дизайнеров (Professional или Enterprise Edition).</span><span class="sxs-lookup"><span data-stu-id="5c9ca-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="5c9ca-112">Экземпляр SQL Server в вашей сети.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="5c9ca-113">Минимальное требование по выпуску — SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="5c9ca-114">Установка предварительной версии среды выполнения Функций Azure</span><span class="sxs-lookup"><span data-stu-id="5c9ca-114">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="5c9ca-115">Установщик предварительной версии среды выполнения Функций Azure поможет выполнить установку ролей управления и рабочих ролей этой версии.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-115">The Azure Functions Runtime preview installer guides you through the installation of the Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="5c9ca-116">Их можно установить на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-116">It is possible to install the Management and Worker role on the same machine.</span></span>  <span data-ttu-id="5c9ca-117">Тем не менее при добавлении дополнительных функций необходимо развернуть дополнительные рабочие роли на дополнительных компьютерах, чтобы масштабировать функции на несколько рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-117">However, as you add more Functions, you must deploy more worker roles on additional machines to be able to scale your functions onto multiple workers.</span></span>

## <a name="install-the-management-and-worker-role-on-the-same-machine"></a><span data-ttu-id="5c9ca-118">Установка ролей управления и рабочих ролей на одном компьютере</span><span class="sxs-lookup"><span data-stu-id="5c9ca-118">Install the Management and Worker Role on the same machine</span></span>

1. <span data-ttu-id="5c9ca-119">Запустите установщик предварительной версии среды выполнения Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-119">Run the Azure Functions Runtime Preview Installer.</span></span>

    ![Установщик предварительной версии среды выполнения Функций Azure][1]

1. <span data-ttu-id="5c9ca-121">Нажмите кнопку **Далее**, чтобы перейти на следующую страницу установщика.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-121">**Click Next** advance past the first stage of the installer</span></span>
1. <span data-ttu-id="5c9ca-122">Ознакомившись с условиями **лицензионного соглашения**, **установите флажок**, чтобы принять их, и нажмите кнопку **Далее** для перехода.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-122">Once you have read the terms of the **EULA**, **check the box** to accept the terms and **click Next** to advance.</span></span>
1. <span data-ttu-id="5c9ca-123">Теперь выберите роли, которые необходимо установить на этом компьютере (**роль управления Функций** или **рабочую роль Функций**), и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-123">Now select the roles you want to install on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Установщик предварительной версии среды выполнения Функций Azure. Выбор роли][3]

    > [!NOTE]
    > <span data-ttu-id="5c9ca-125">Вы можете установить **рабочую роль Функций** на других компьютерах. Для этого выполните следующие инструкции и выберите в установщике только **рабочую роль Функций**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-125">You can install the **Functions Worker Role** on many other machines to do so, follow these instructions, and only select **Functions Worker Role** in the installer.</span></span>

1. <span data-ttu-id="5c9ca-126">Нажмите кнопку **Далее**, чтобы установить **установщик среды выполнения Функций Azure**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-126">**Click Next** to have the **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="5c9ca-127">После завершения установщик запустит **инструмент настройки среды выполнения Функций Azure**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-127">Once complete the installer will launch the **Azure Functions Runtime Configuration tool**.</span></span>

    ![Установщик предварительной версии среды выполнения Функций Azure — завершение][5]

    > [!NOTE]
    > <span data-ttu-id="5c9ca-129">Если при установке на компьютере с **Windows 10** функция **Контейнер** не была включена ранее, **установщик среды выполнения Функций Azure** предложит перезагрузить компьютер для завершения установки.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-129">If you are installing on **Windows 10** and the **Container** feature has not been previously enabled, the **Azure Functions Runtime** Installer prompts you to reboot your machine to complete the install.</span></span>

## <a name="configure-the-azure-functions-runtime"></a><span data-ttu-id="5c9ca-130">Настройка среды выполнения Функций Azure</span><span class="sxs-lookup"><span data-stu-id="5c9ca-130">Configure the Azure Functions Runtime</span></span>

<span data-ttu-id="5c9ca-131">Для завершения установки среды выполнения Функций Azure необходимо выполнить настройку.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-131">To complete the Azure Functions Runtime installation you must complete the configuration.</span></span>

1. <span data-ttu-id="5c9ca-132">На странице **инструмента настройки среды выполнения Функций Azure** показано, какие роли установлены на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-132">The **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Инструмент настройки предварительной версии среды выполнения Функций Azure][6]

1. <span data-ttu-id="5c9ca-134">Щелкните вкладку **Базы данных**, введите **сведения о подключении для экземпляра SQL Server** и нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-134">Click the **Database** tab, enter the **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="5c9ca-135">Это необходимо, чтобы создать базу данных для поддержки среды выполнения в среде выполнения Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-135">This is required in order to the Azure Functions Runtime to create a database to support the Runtime.</span></span>
    
    ![Настройка базы данных предварительной версии среды выполнения Функций Azure][7]

1. <span data-ttu-id="5c9ca-137">Щелкните вкладку **Учетные данные**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-137">Click the **Credentials** tab.</span></span>  <span data-ttu-id="5c9ca-138">На этом экране необходимо создать две пары учетных данных для использования с общей папкой для размещения всех Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-138">On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="5c9ca-139">**Укажите имя пользователя и пароль** для **владельца общей папки** и **пользователя общей папки** и нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-139">**Specify Username and Password** combinations for the **File Share Owner** and for the **File Share User** and click **Apply**.</span></span>

    ![Учетные данные предварительной версии среды выполнения Функций Azure][8]

1. <span data-ttu-id="5c9ca-141">Щелкните вкладку **Общая папка**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-141">Click the **File Share** tab.</span></span>  <span data-ttu-id="5c9ca-142">На этом экране необходимо указать сведения о **расположении общей папки**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-142">In this screen you must specify the details of the **File Share location**.</span></span>  <span data-ttu-id="5c9ca-143">Она может быть создана автоматически, или вы можете использовать имеющуюся общую папку и нажать кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-143">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="5c9ca-144">Если вы выберете новое расположение общей папки, укажите каталог для использования в среде выполнения Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-144">If you select a new File Share location, you must specify a directory for use by the Azure Functions Runtime.</span></span>
    
    ![Предварительная версия среды выполнения Функций Azure — общая папка][9]

1. <span data-ttu-id="5c9ca-146">Щелкните вкладку **IIS**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-146">Click the **IIS** tab.</span></span>  <span data-ttu-id="5c9ca-147">На ней отображаются сведения о веб-сайтах в службах IIS, которые будут созданы при установке среды выполнения Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-147">This tab shows the details of the websites in IIS that the Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="5c9ca-148">Нажмите кнопку **Применить** для завершения.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-148">**Click Apply** to complete.</span></span>

    ![Предварительная версия среды выполнения Функций Azure — IIS][10]

1. <span data-ttu-id="5c9ca-150">Щелкните вкладку **Службы**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-150">Click the **Services** tab.</span></span>  <span data-ttu-id="5c9ca-151">На этой вкладке отображается состояние служб в установленной среде выполнения Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-151">This tab shows the status of the services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="5c9ca-152">Если после первоначальной настройки **служба активации узла Функций Azure** не запущена, нажмите кнопку **Запустить службу**.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-152">If after initial configuration the **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Предварительная версия среды выполнения Функций Azure — завершение настройки][11]

1. <span data-ttu-id="5c9ca-154">Наконец, перейдите на **портал среды выполнения Функций Azure** как `https://<machinename>/`.</span><span class="sxs-lookup"><span data-stu-id="5c9ca-154">Finally browse to the **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

    ![Портал предварительной версии среды выполнения Функций Azure][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png