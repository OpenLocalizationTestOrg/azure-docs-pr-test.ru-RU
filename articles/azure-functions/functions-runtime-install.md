---
title: "aaaAzure установки среды выполнения функции | Документы Microsoft"
description: "Как tooInstall hello среды выполнения функций Azure"
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
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="fe081-103">Установка hello предварительной версии Azure функции среды выполнения</span><span class="sxs-lookup"><span data-stu-id="fe081-103">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="fe081-104">При желании tooinstall hello среды выполнения функций Azure preview, необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fe081-104">If you would like tooinstall hello Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="fe081-105">Убедитесь, что компьютер передает hello минимальные требования</span><span class="sxs-lookup"><span data-stu-id="fe081-105">Ensure your machine passes hello minimum requirements</span></span>
1. <span data-ttu-id="fe081-106">Загрузите hello [установщик предварительного выполнения функций Azure](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="fe081-106">Download hello [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="fe081-107">Установка среды выполнения функций Azure preview hello</span><span class="sxs-lookup"><span data-stu-id="fe081-107">Install hello Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="fe081-108">Полный hello конфигурации предварительной версии среды выполнения Azure функции hello</span><span class="sxs-lookup"><span data-stu-id="fe081-108">Complete hello configuration of hello Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe081-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fe081-109">Prerequisites</span></span>

<span data-ttu-id="fe081-110">Перед установкой предварительной версии среды выполнения Azure функции hello, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="fe081-110">Before you install hello Azure Functions Runtime preview, you must have hello following:</span></span>

1. <span data-ttu-id="fe081-111">Компьютер под управлением Microsoft Windows Server 2016 или обновление Microsoft Windows 10 для дизайнеров (Professional или Enterprise Edition).</span><span class="sxs-lookup"><span data-stu-id="fe081-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="fe081-112">Экземпляр SQL Server в вашей сети.</span><span class="sxs-lookup"><span data-stu-id="fe081-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="fe081-113">Минимальное требование по выпуску — SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="fe081-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="fe081-114">Установка hello предварительной версии Azure функции среды выполнения</span><span class="sxs-lookup"><span data-stu-id="fe081-114">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="fe081-115">Установщик предварительной версии среды выполнения Azure функции Hello поможет выполнить установку hello предварительной версии среды выполнения Azure функции hello управления и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="fe081-115">hello Azure Functions Runtime preview installer guides you through hello installation of hello Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="fe081-116">Возможные tooinstall hello управления и рабочей роли в hello же компьютере.</span><span class="sxs-lookup"><span data-stu-id="fe081-116">It is possible tooinstall hello Management and Worker role on hello same machine.</span></span>  <span data-ttu-id="fe081-117">Тем не менее как добавить дополнительные функции, необходимо развернуть дополнительные рабочие роли на возможности tooscale toobe дополнительных компьютеров функций на несколько рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="fe081-117">However, as you add more Functions, you must deploy more worker roles on additional machines toobe able tooscale your functions onto multiple workers.</span></span>

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a><span data-ttu-id="fe081-118">Установите на hello hello управления и рабочая роль одном компьютере</span><span class="sxs-lookup"><span data-stu-id="fe081-118">Install hello Management and Worker Role on hello same machine</span></span>

1. <span data-ttu-id="fe081-119">Запустите установщик предварительной версии среды выполнения Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="fe081-119">Run hello Azure Functions Runtime Preview Installer.</span></span>

    ![Установщик предварительной версии среды выполнения Функций Azure][1]

1. <span data-ttu-id="fe081-121">**Нажмите кнопку Далее** Авансовая за первый этап hello установщика hello</span><span class="sxs-lookup"><span data-stu-id="fe081-121">**Click Next** advance past hello first stage of hello installer</span></span>
1. <span data-ttu-id="fe081-122">После прочтения hello условия hello **лицензионное соглашение**, **флажок hello** tooaccept hello условия и **нажмите кнопку Далее** tooadvance.</span><span class="sxs-lookup"><span data-stu-id="fe081-122">Once you have read hello terms of hello **EULA**, **check hello box** tooaccept hello terms and **click Next** tooadvance.</span></span>
1. <span data-ttu-id="fe081-123">Теперь выберите hello ролей требуется tooinstall на этом компьютере **роль функций управления** и/или **функции рабочей роли** и **нажмите кнопку Далее.**</span><span class="sxs-lookup"><span data-stu-id="fe081-123">Now select hello roles you want tooinstall on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Установщик предварительной версии среды выполнения Функций Azure. Выбор роли][3]

    > [!NOTE]
    > <span data-ttu-id="fe081-125">Вы можете установить hello **функции рабочей роли** на многих других машин toodo таким образом, выполните следующие действия и выбрать только **функции рабочей роли** в установщике hello.</span><span class="sxs-lookup"><span data-stu-id="fe081-125">You can install hello **Functions Worker Role** on many other machines toodo so, follow these instructions, and only select **Functions Worker Role** in hello installer.</span></span>

1. <span data-ttu-id="fe081-126">**Нажмите кнопку Далее** toohave hello **установщика среды выполнения Azure функции** устанавливается на компьютере.</span><span class="sxs-lookup"><span data-stu-id="fe081-126">**Click Next** toohave hello **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="fe081-127">После завершения hello установщика запустит hello **средство настройки среды выполнения Azure функции**.</span><span class="sxs-lookup"><span data-stu-id="fe081-127">Once complete hello installer will launch hello **Azure Functions Runtime Configuration tool**.</span></span>

    ![Установщик предварительной версии среды выполнения Функций Azure — завершение][5]

    > [!NOTE]
    > <span data-ttu-id="fe081-129">Если вы устанавливаете на **Windows 10** и hello **контейнера** функция не включена ранее, hello **выполнения функции Azure** установщик предложит tooreboot Установите hello toocomplete вашего компьютера.</span><span class="sxs-lookup"><span data-stu-id="fe081-129">If you are installing on **Windows 10** and hello **Container** feature has not been previously enabled, hello **Azure Functions Runtime** Installer prompts you tooreboot your machine toocomplete hello install.</span></span>

## <a name="configure-hello-azure-functions-runtime"></a><span data-ttu-id="fe081-130">Настройка среды выполнения Azure функции hello</span><span class="sxs-lookup"><span data-stu-id="fe081-130">Configure hello Azure Functions Runtime</span></span>

<span data-ttu-id="fe081-131">Здравствуйте, toocomplete установки среды выполнения функции Azure, необходимо выполнить настройку hello.</span><span class="sxs-lookup"><span data-stu-id="fe081-131">toocomplete hello Azure Functions Runtime installation you must complete hello configuration.</span></span>

1. <span data-ttu-id="fe081-132">Hello **средство настройки среды выполнения Azure функции** показывает, какие роли установлены на компьютере.</span><span class="sxs-lookup"><span data-stu-id="fe081-132">hello **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Инструмент настройки предварительной версии среды выполнения Функций Azure][6]

1. <span data-ttu-id="fe081-134">Нажмите кнопку hello **базы данных** введите hello **сведения о соединении для экземпляра SQL Server** и **нажмите кнопку Применить**.</span><span class="sxs-lookup"><span data-stu-id="fe081-134">Click hello **Database** tab, enter hello **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="fe081-135">Это необходимо в порядке toohello toocreate среды выполнения Azure функции hello toosupport базы данных времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="fe081-135">This is required in order toohello Azure Functions Runtime toocreate a database toosupport hello Runtime.</span></span>
    
    ![Настройка базы данных предварительной версии среды выполнения Функций Azure][7]

1. <span data-ttu-id="fe081-137">Нажмите кнопку hello **учетные данные** вкладки.  На этом экране необходимо создать две пары учетных данных для использования с общей папкой для размещения всех Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="fe081-137">Click hello **Credentials** tab.  On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="fe081-138">**Укажите имя пользователя и пароль** комбинации для hello **владельца общей папки** и для hello **пользователя общего файлового ресурса** и нажмите кнопку **применить**.</span><span class="sxs-lookup"><span data-stu-id="fe081-138">**Specify Username and Password** combinations for hello **File Share Owner** and for hello **File Share User** and click **Apply**.</span></span>

    ![Учетные данные предварительной версии среды выполнения Функций Azure][8]

1. <span data-ttu-id="fe081-140">Нажмите кнопку hello **общей папки** вкладки.  На этом экране необходимо указать подробности hello hello **расположение общей папки**.</span><span class="sxs-lookup"><span data-stu-id="fe081-140">Click hello **File Share** tab.  In this screen you must specify hello details of hello **File Share location**.</span></span>  <span data-ttu-id="fe081-141">Она может быть создана автоматически, или вы можете использовать имеющуюся общую папку и нажать кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="fe081-141">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="fe081-142">Если выбрать новое расположение общей папки, необходимо указать каталог для использования с hello среды выполнения функций Azure.</span><span class="sxs-lookup"><span data-stu-id="fe081-142">If you select a new File Share location, you must specify a directory for use by hello Azure Functions Runtime.</span></span>
    
    ![Предварительная версия среды выполнения Функций Azure — общая папка][9]

1. <span data-ttu-id="fe081-144">Нажмите кнопку hello **IIS** вкладки.  На этой вкладке отображаются подробные сведения об hello hello веб-сайтов в службах IIS, создаваемых установки среды выполнения Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="fe081-144">Click hello **IIS** tab.  This tab shows hello details of hello websites in IIS that hello Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="fe081-145">**Нажмите кнопку Применить** toocomplete.</span><span class="sxs-lookup"><span data-stu-id="fe081-145">**Click Apply** toocomplete.</span></span>

    ![Предварительная версия среды выполнения Функций Azure — IIS][10]

1. <span data-ttu-id="fe081-147">Нажмите кнопку hello **служб** вкладки.  На этой вкладке отображается состояние hello служб hello в установке среды выполнения функций Azure.</span><span class="sxs-lookup"><span data-stu-id="fe081-147">Click hello **Services** tab.  This tab shows hello status of hello services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="fe081-148">Если после начальной настройки hello **службы активации узла Azure функции** не запущена, нажмите **запуск службы**</span><span class="sxs-lookup"><span data-stu-id="fe081-148">If after initial configuration hello **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Предварительная версия среды выполнения Функций Azure — завершение настройки][11]

1. <span data-ttu-id="fe081-150">Наконец Обзор toohello **портала среды выполнения Azure функции** как`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="fe081-150">Finally browse toohello **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

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