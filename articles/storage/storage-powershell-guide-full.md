---
title: "aaaUsing Azure PowerShell с хранилищем Azure | Документы Microsoft"
description: "Узнайте, как toouse hello командлеты Azure PowerShell для toocreate хранилища Azure и управление учетными записями хранения; Работа с BLOB-объектов, таблиц, очередей и файлов; Настройка и запросов аналитики хранилища и создания подписей общего доступа."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="66aca-103">Использование Azure PowerShell со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="66aca-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="66aca-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="66aca-104">Overview</span></span>
<span data-ttu-id="66aca-105">Azure PowerShell — это модуль, предоставляет toomanage командлеты Azure через Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-105">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="66aca-106">Это оболочка командной строки на основе задач и язык сценариев, разработанные для администрирования системы.</span><span class="sxs-lookup"><span data-stu-id="66aca-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="66aca-107">С помощью PowerShell можно легко контроля и автоматизации администрирования hello служб Azure и приложений.</span><span class="sxs-lookup"><span data-stu-id="66aca-107">With PowerShell, you can easily control and automate hello administration of your Azure services and applications.</span></span> <span data-ttu-id="66aca-108">Например, можно использовать hello командлеты tooperform hello же задачи, которые можно выполнять через hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="66aca-108">For example, you can use hello cmdlets tooperform hello same tasks that you can perform through hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="66aca-109">В этом руководстве мы изучим как toouse hello [командлеты хранилища Azure](/powershell/module/azurerm.storage/#storage) tooperform различных задач разработки и администрирования хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-109">In this guide, we'll explore how toouse hello [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="66aca-110">Предполагается, что у вас есть опыт работы со [службой хранилища Azure](https://azure.microsoft.com/documentation/services/storage/) и [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="66aca-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="66aca-111">Hello руководство содержит ряд сценариев использования hello toodemonstrate PowerShell со службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-111">hello guide provides a number of scripts toodemonstrate hello usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="66aca-112">Необходимо обновить переменные сценария hello на основе конфигурации перед выполнением каждого сценария.</span><span class="sxs-lookup"><span data-stu-id="66aca-112">You should update hello script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="66aca-113">Первый раздел Hello в данном руководстве предоставляет быстрый обзор хранилища Azure и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-113">hello first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="66aca-114">Подробные сведения и инструкции, запуск из hello [предварительные требования для использования со службой хранилища Azure Azure PowerShell](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="66aca-114">For detailed information and instructions, start from hello [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="66aca-115">Приступая к работе со службой хранилища Azure и PowerShell в течение 5 минут</span><span class="sxs-lookup"><span data-stu-id="66aca-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="66aca-116">В этом разделе показано, как tooaccess хранилища Azure с помощью PowerShell в 5 минут.</span><span class="sxs-lookup"><span data-stu-id="66aca-116">This section shows you how tooaccess Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="66aca-117">**Новый tooAzure:** получить подписку Microsoft Azure и учетной записи Майкрософт, связанные с этой подпиской.</span><span class="sxs-lookup"><span data-stu-id="66aca-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="66aca-118">Сведения о способах приобретения Azure см. на страницах [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/), [Как приобрести Azure](https://azure.microsoft.com/pricing/purchase-options/) и [Предложения для участников](https://azure.microsoft.com/pricing/member-offers/) (для подписчиков MSDN, участников Microsoft Partner Network, BizSpark и других наших программ).</span><span class="sxs-lookup"><span data-stu-id="66aca-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="66aca-119">Дополнительные сведения о подписках Azure см. на странице [Назначение ролей администратора в Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx).</span><span class="sxs-lookup"><span data-stu-id="66aca-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="66aca-120">**После создания подписки Microsoft Azure и учетной записи:**</span><span class="sxs-lookup"><span data-stu-id="66aca-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="66aca-121">Загрузите и установите последние hello [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="66aca-121">Download and install hello latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="66aca-122">Начало интегрированная среда Windows PowerShell сценариев (ISE): На локальном компьютере перейдите toohello **запустить** меню.</span><span class="sxs-lookup"><span data-stu-id="66aca-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go toohello **Start** menu.</span></span> <span data-ttu-id="66aca-123">Тип **Администрирование** и нажмите кнопку toorun его.</span><span class="sxs-lookup"><span data-stu-id="66aca-123">Type **Administrative Tools** and click toorun it.</span></span> <span data-ttu-id="66aca-124">В hello **Администрирование** окно, щелкните правой кнопкой мыши **интегрированной среды Сценариев Windows PowerShell**, нажмите кнопку **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="66aca-124">In hello **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="66aca-125">В **интегрированной среды Сценариев Windows PowerShell**, нажмите кнопку **файл** > **New** toocreate новый файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="66aca-125">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="66aca-126">Теперь мы указываем, простой сценарий, который показывает основные tooaccess команд PowerShell хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-126">Now, we'll give you a simple script that shows basic PowerShell commands tooaccess Azure Storage.</span></span> <span data-ttu-id="66aca-127">сценарий Hello сначала запросит tooadd учетные данные вашей учетной записи Azure toohello учетная запись Azure локальной среде PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-127">hello script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment.</span></span> <span data-ttu-id="66aca-128">Затем сценарий hello присвоить значение по умолчанию hello подписки Azure и создать новую учетную запись хранения в Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-128">Then, hello script will set hello default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="66aca-129">Затем сценарий hello создать контейнер в этой новой учетной записи хранения и отправить существующий контейнер toothat образ файла (blob).</span><span class="sxs-lookup"><span data-stu-id="66aca-129">Next, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="66aca-130">После hello скрипт перечисляет все большие двоичные объекты в этом контейнере, создает новый каталог назначения на своем локальном компьютере и загрузите файл изображения hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-130">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>
5. <span data-ttu-id="66aca-131">В следующий раздел кода hello, выберите сценарий hello между hello примечания **#begin** и **#end**.</span><span class="sxs-lookup"><span data-stu-id="66aca-131">In hello following code section, select hello script between hello remarks **#begin** and **#end**.</span></span> <span data-ttu-id="66aca-132">Нажмите клавиши CTRL + C toocopy его toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="66aca-132">Press CTRL+C toocopy it toohello clipboard.</span></span>

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="66aca-133">В **интегрированной среды Сценариев Windows PowerShell**, нажмите клавиши CTRL + V toocopy hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="66aca-133">In **Windows PowerShell ISE**, press CTRL+V toocopy hello script.</span></span> <span data-ttu-id="66aca-134">Щелкните **Файл** > **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="66aca-134">Click **File** > **Save**.</span></span> <span data-ttu-id="66aca-135">В hello **Сохранить как** диалоговое окно, имя типа hello hello файла скрипта, такие как «mystoragescript».</span><span class="sxs-lookup"><span data-stu-id="66aca-135">In hello **Save As** dialog window, type hello name of hello script file, such as "mystoragescript."</span></span> <span data-ttu-id="66aca-136">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="66aca-136">Click **Save**.</span></span>
7. <span data-ttu-id="66aca-137">Теперь требуется переменных сценария hello tooupdate на основании параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="66aca-137">Now, you need tooupdate hello script variables based on your configuration settings.</span></span> <span data-ttu-id="66aca-138">Необходимо обновить hello **$SubscriptionName** переменных с собственной подписки.</span><span class="sxs-lookup"><span data-stu-id="66aca-138">You must update hello **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="66aca-139">Можно сохранить hello другие переменные, как указано в скрипте hello или обновлять их по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="66aca-139">You can keep hello other variables as specified in hello script or update them as you wish.</span></span>
   
   * <span data-ttu-id="66aca-140">Необходимо обновить переменную **$SubscriptionName**, используя данные собственной подписки.</span><span class="sxs-lookup"><span data-stu-id="66aca-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="66aca-141">Выполните одно из следующих трех способов toolocate hello именем подписки hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-141">Follow one of hello following three ways toolocate hello name of your subscription:</span></span>
     
    <span data-ttu-id="66aca-142">а.</span><span class="sxs-lookup"><span data-stu-id="66aca-142">a.</span></span> <span data-ttu-id="66aca-143">В **интегрированной среды Сценариев Windows PowerShell**, нажмите кнопку **файл** > **New** toocreate новый файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="66aca-143">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span> <span data-ttu-id="66aca-144">Следующие hello копирования сценариев toohello новый файл скрипта и нажмите кнопку **отладки** > **запуска**.</span><span class="sxs-lookup"><span data-stu-id="66aca-144">Copy hello following script toohello new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="66aca-145">Hello следующий сценарий будет запросить учетные данные вашей учетной записи Azure tooadd toohello учетная запись Azure локальной среде PowerShell и отобразите все подписки hello, подключенных toohello локальный сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-145">hello following script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment and then show all hello subscriptions that are connected toohello local PowerShell session.</span></span> <span data-ttu-id="66aca-146">Запишите имя hello hello подписки, которые должны toouse, однако при этом учебнике:</span><span class="sxs-lookup"><span data-stu-id="66aca-146">Take a note of hello name of hello subscription that you want toouse while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="66aca-147">b.</span><span class="sxs-lookup"><span data-stu-id="66aca-147">b.</span></span> <span data-ttu-id="66aca-148">Имя toolocate и скопируйте подписки в hello [портал Azure](https://portal.azure.com)в hello концентратора меню hello слева, нажмите кнопку **подписки**.</span><span class="sxs-lookup"><span data-stu-id="66aca-148">toolocate and copy your subscription name in hello [Azure portal](https://portal.azure.com), in hello Hub menu on hello left, click **Subscriptions**.</span></span> <span data-ttu-id="66aca-149">Скопируйте имя hello подписку, которую нужно toouse при выполнении скриптов hello в данном руководстве.</span><span class="sxs-lookup"><span data-stu-id="66aca-149">Copy hello name of subscription that you want toouse while running hello scripts in this guide.</span></span>
     
     ![Портал Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="66aca-151">c.</span><span class="sxs-lookup"><span data-stu-id="66aca-151">c.</span></span> <span data-ttu-id="66aca-152">Имя toolocate и скопируйте подписки в hello [классический портал Azure](https://manage.windowsazure.com/), прокрутите список вниз и нажмите кнопку **параметры** на hello левая сторона hello портала.</span><span class="sxs-lookup"><span data-stu-id="66aca-152">toolocate and copy your subscription name in hello [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="66aca-153">Нажмите кнопку **подписки** toosee список подписок.</span><span class="sxs-lookup"><span data-stu-id="66aca-153">Click **Subscriptions** toosee a list of your subscriptions.</span></span> <span data-ttu-id="66aca-154">Скопируйте hello имя подписки на toouse во время выполнения получает скрипты hello в данном руководстве.</span><span class="sxs-lookup"><span data-stu-id="66aca-154">Copy hello name of subscription that you want toouse while running hello scripts given in this guide.</span></span>
     
     ![классическом портале Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="66aca-156">**$StorageAccountName:** использовать hello с заданным именем в скрипте hello, или введите новое имя для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="66aca-156">**$StorageAccountName:** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="66aca-157">**Важно:** hello имя учетной записи хранения hello должно быть уникальным в Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-157">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="66aca-158">и состоять из символов нижнего регистра.</span><span class="sxs-lookup"><span data-stu-id="66aca-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="66aca-159">**$Location:** заданному «West US» hello в скрипте hello, или выберите другие расположения Azure, например Восток США, Северной Европе и т. д.</span><span class="sxs-lookup"><span data-stu-id="66aca-159">**$Location:** Use hello given "West US" in hello script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="66aca-160">**$ContainerName:** использовать hello с заданным именем в скрипте hello, или введите новое имя для контейнера.</span><span class="sxs-lookup"><span data-stu-id="66aca-160">**$ContainerName:** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="66aca-161">**$ImageToUpload:** введите рисунок tooa путь на локальном компьютере, например: «C:\Images\HelloWorld.png».</span><span class="sxs-lookup"><span data-stu-id="66aca-161">**$ImageToUpload:** Enter a path tooa picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="66aca-162">**$DestinationFolder:** файлы toostore путь локального каталога tooa загружаются из хранилища Azure, такие как ввод: «C:\DownloadImages».</span><span class="sxs-lookup"><span data-stu-id="66aca-162">**$DestinationFolder:** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="66aca-163">После обновления с помощью переменных сценария hello в файле «mystoragescript.ps1» hello, нажмите кнопку **файл** > **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="66aca-163">After updating hello script variables in hello "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="66aca-164">Нажмите кнопку **отладки** > **запуска** или нажмите клавишу **F5** toorun hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="66aca-164">Then, click **Debug** > **Run** or press **F5** toorun hello script.</span></span>  

<span data-ttu-id="66aca-165">После запуска сценария hello должно быть локальную целевую папку, которая содержит файл изображения загружаются hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-165">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="66aca-166">Следующий снимок экрана приветствия показан пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="66aca-166">hello following screenshot shows an example output:</span></span>

![Загрузка BLOB-объектов](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="66aca-168">Hello «Приступая к работе с хранилища Azure и PowerShell, в течение 5 минут» предоставляемые краткие сведения о том, как toouse Azure PowerShell со службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-168">hello "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how toouse Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="66aca-169">Подробные сведения и инструкции мы рекомендуем вам hello tooread следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="66aca-169">For detailed information and instructions, we encourage you tooread hello following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="66aca-170">Предварительные требования для использования Azure PowerShell со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="66aca-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="66aca-171">Необходимо подписки и учетной записи toorun hello командлеты PowerShell Azure в данном руководстве, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="66aca-171">You need an Azure subscription and account toorun hello PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="66aca-172">Azure PowerShell — это модуль, предоставляет toomanage командлеты Azure через Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-172">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="66aca-173">Сведения об установке и настройке Azure PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="66aca-173">For information on installing and setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="66aca-174">Рекомендуется загрузить и установить или обновить последнюю версию модуля Azure PowerShell toohello перед использованием в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="66aca-174">We recommend that you download and install or upgrade toohello latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="66aca-175">Можно запускать командлеты hello в консоли Windows PowerShell hello или hello Сценариев Windows PowerShell интегрированной среде ().</span><span class="sxs-lookup"><span data-stu-id="66aca-175">You can run hello cmdlets in hello standard Windows PowerShell console or hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="66aca-176">Например, tooopen **интегрированной среды Сценариев Windows PowerShell**откройте меню "Пуск" toohello, введите Администрирование и щелкните toorun его.</span><span class="sxs-lookup"><span data-stu-id="66aca-176">For example, tooopen **Windows PowerShell ISE**, go toohello Start menu, type Administrative Tools and click toorun it.</span></span> <span data-ttu-id="66aca-177">В "Администрирование" hello щелкните правой кнопкой мыши интегрированной среды Сценариев Windows PowerShell, запуск от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="66aca-177">In hello Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-toomanage-storage-accounts-in-azure"></a><span data-ttu-id="66aca-178">Как toomanage хранилища учетных записей в Azure</span><span class="sxs-lookup"><span data-stu-id="66aca-178">How toomanage storage accounts in Azure</span></span>

<span data-ttu-id="66aca-179">Давайте рассмотрим процесс управления учетными записями хранения в Azure с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-tooset-a-default-azure-subscription"></a><span data-ttu-id="66aca-180">Как tooset значение по умолчанию подписки Azure</span><span class="sxs-lookup"><span data-stu-id="66aca-180">How tooset a default Azure subscription</span></span>
<span data-ttu-id="66aca-181">toomanage хранилища Azure с помощью Azure PowerShell, необходимо tooauthenticate средой клиента в Azure через Azure Active Directory или проверку подлинности на основе сертификатов.</span><span class="sxs-lookup"><span data-stu-id="66aca-181">toomanage Azure Storage using Azure PowerShell, you need tooauthenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="66aca-182">Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) учебника.</span><span class="sxs-lookup"><span data-stu-id="66aca-182">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="66aca-183">В этом руководстве используется проверка подлинности Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-183">This guide uses hello Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="66aca-184">В интегрированной среде Сценариев Windows PowerShell введите следующие команды tooadd hello toohello учетная запись Azure локальной среде PowerShell:</span><span class="sxs-lookup"><span data-stu-id="66aca-184">In Windows PowerShell ISE, type hello following command tooadd your Azure account toohello local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="66aca-185">В окне «Вход tooMicrosoft Azure» hello, тип hello адрес электронной почты и пароль, связанный с вашей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="66aca-185">In hello "Sign in tooMicrosoft Azure" window, type hello email address and password associated with your account.</span></span> <span data-ttu-id="66aca-186">Azure выполняет проверку подлинности и сохраняет hello учетные данные и затем закрывает окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="66aca-186">Azure authenticates and saves hello credential information, and then closes hello window.</span></span>

3. <span data-ttu-id="66aca-187">Затем выполните hello, следующая команда tooview hello Azure учетные записи в локальной среде PowerShell и убедитесь, что ваша учетная запись:</span><span class="sxs-lookup"><span data-stu-id="66aca-187">Next, run hello following command tooview hello Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="66aca-188">Затем запустите следующий командлет tooview hello все подписки hello, подключенных toohello локальный сеанс PowerShell и убедитесь, что подписки:</span><span class="sxs-lookup"><span data-stu-id="66aca-188">Then, run hello following cmdlet tooview all hello subscriptions that are connected toohello local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="66aca-189">tooset значение по умолчанию подписка Azure, выполните командлет Select-AzureSubscription hello:</span><span class="sxs-lookup"><span data-stu-id="66aca-189">tooset a default Azure subscription, run hello Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="66aca-190">Проверьте имя hello подписки по умолчанию hello, выполнив командлет Get-AzureSubscription hello:</span><span class="sxs-lookup"><span data-stu-id="66aca-190">Verify hello name of hello default subscription by running hello Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="66aca-191">toosee все hello доступных командлетов PowerShell для хранилища Azure, выполните:</span><span class="sxs-lookup"><span data-stu-id="66aca-191">toosee all hello available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a><span data-ttu-id="66aca-192">Как toocreate новую учетную запись хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="66aca-192">How toocreate a new Azure storage account</span></span>
<span data-ttu-id="66aca-193">toouse хранилища Azure, потребуется учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="66aca-193">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="66aca-194">После настройки подписки tooyour tooconnect компьютера, можно создать новую учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-194">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

1. <span data-ttu-id="66aca-195">Выполните все hello доступные расположения toofind командлет Get-AzureLocation hello:</span><span class="sxs-lookup"><span data-stu-id="66aca-195">Run hello Get-AzureLocation cmdlet toofind all hello available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="66aca-196">Затем запустите toocreate командлет New-AzureStorageAccount hello новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="66aca-196">Next, run hello New-AzureStorageAccount cmdlet toocreate a new storage account.</span></span> <span data-ttu-id="66aca-197">Hello следующий пример создает новую учетную запись хранилища в центре обработки данных «West US» hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-197">hello following example creates a new storage account in hello "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="66aca-198">Hello имя учетной записи должно быть уникальным в Azure и должны быть строчными.</span><span class="sxs-lookup"><span data-stu-id="66aca-198">hello name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="66aca-199">Соглашения об именовании и ограничениях см. в статьях [Об учетных записях хранения Azure](storage-create-storage-account.md) и [Именование контейнеров, больших двоичных объектов, метаданных и ссылка на них](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="66aca-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a><span data-ttu-id="66aca-200">Как tooset учетную запись хранилища Azure по умолчанию</span><span class="sxs-lookup"><span data-stu-id="66aca-200">How tooset a default Azure storage account</span></span>
<span data-ttu-id="66aca-201">В подписке может иметься несколько учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="66aca-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="66aca-202">Можно выбрать один из них и задать его значение как hello учетной записи хранения по умолчанию для всех hello хранилища команды в hello же сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-202">You can choose one of them and set it as hello default storage account for all hello storage commands in hello same PowerShell session.</span></span> <span data-ttu-id="66aca-203">Это позволяет toorun hello Azure PowerShell хранения команд без указания контекста хранилища hello явным образом.</span><span class="sxs-lookup"><span data-stu-id="66aca-203">This enables you toorun hello Azure PowerShell storage commands without specifying hello storage context explicitly.</span></span>

1. <span data-ttu-id="66aca-204">tooset учетной записи хранения по умолчанию для вашей подписки, запустите командлет Set-AzureSubscription hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-204">tooset a default storage account for your subscription, you can run hello Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="66aca-205">Затем запустите tooverify командлет Get-AzureSubscription hello, учетной записи хранилища hello связан с вашей учетной записи подписки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="66aca-205">Next, run hello Get-AzureSubscription cmdlet tooverify that hello storage account is associated with your default subscription account.</span></span> <span data-ttu-id="66aca-206">Эта команда возвращает свойства подписки hello на hello текущей подписке, включая его текущей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="66aca-206">This command returns hello subscription properties on hello current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="66aca-207">Как toolist все Azure учетных записей хранения в подписке</span><span class="sxs-lookup"><span data-stu-id="66aca-207">How toolist all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="66aca-208">Каждая подписка Azure может содержать до too100 учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="66aca-208">Each Azure subscription can have up too100 storage accounts.</span></span> <span data-ttu-id="66aca-209">Hello наиболее актуальные сведения об ограничениях см. в разделе [подписки Azure и ограничения служб, квоты и ограничения](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="66aca-209">For hello most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="66aca-210">Выполните следующий командлет toofind hello имя и состояние hello учетных записей хранения в текущей подписке hello hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-210">Run hello following cmdlet toofind out hello name and status of hello storage accounts in hello current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a><span data-ttu-id="66aca-211">Как toocreate контекст хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="66aca-211">How toocreate an Azure storage context</span></span>
<span data-ttu-id="66aca-212">Контекст хранилища Azure — это объект в учетные данные хранилища hello tooencapsulate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-212">Azure storage context is an object in PowerShell tooencapsulate hello storage credentials.</span></span> <span data-ttu-id="66aca-213">Контекст хранилища во время выполнения все последующие командлет благодаря использованию вы tooauthenticate запрос без указания явно hello учетной записи хранилища и ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="66aca-213">Using a storage context while running any subsequent cmdlet enables you tooauthenticate your request without specifying hello storage account and its access key explicitly.</span></span> <span data-ttu-id="66aca-214">Контекст хранилища можно создать несколькими способами, например с помощью имени и ключа доступа учетной записи хранения, токена подписи общего доступа, строки подключения или анонимно.</span><span class="sxs-lookup"><span data-stu-id="66aca-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="66aca-215">Дополнительные сведения см. в описании [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="66aca-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="66aca-216">Используйте один из следующих трех способов toocreate hello контекст хранилища.</span><span class="sxs-lookup"><span data-stu-id="66aca-216">Use one of hello following three ways toocreate a storage context:</span></span>

* <span data-ttu-id="66aca-217">Запустите hello [Get AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind командлет out hello ключ доступа основного хранилища для вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-217">Run hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind out hello primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="66aca-218">Затем вызовите hello [New AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) toocreate командлет контекст хранилища:</span><span class="sxs-lookup"><span data-stu-id="66aca-218">Next, call hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="66aca-219">Создать маркер подписи общего доступа для контейнера хранилища Azure и использовать его toocreate контекст хранилища:</span><span class="sxs-lookup"><span data-stu-id="66aca-219">Generate a shared access signature token for an Azure storage container and use it toocreate a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="66aca-220">Дополнительные сведения см. в статьях [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) и [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="66aca-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="66aca-221">В некоторых случаях может потребоваться конечных точек службы hello toospecify при создании нового контекста хранилища.</span><span class="sxs-lookup"><span data-stu-id="66aca-221">In some cases, you may want toospecify hello service endpoints when you create a new storage context.</span></span> <span data-ttu-id="66aca-222">Это может потребоваться при вы зарегистрировали доменное имя для вашей учетной записи хранения со службой BLOB-объектов hello, или требуется toouse подписанный URL-адрес для доступа к ресурсам хранилища.</span><span class="sxs-lookup"><span data-stu-id="66aca-222">This might be necessary when you have registered a custom domain name for your storage account with hello Blob service or you want toouse a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="66aca-223">Набор конечных точек службы hello в строку подключения и использовать его toocreate новый контекст хранилища, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="66aca-223">Set hello service endpoints in a connection string and use it toocreate a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="66aca-224">Дополнительные сведения о том, как tooconfigure строки подключения хранилища, в разделе [Настройка строк подключения](storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="66aca-224">For more information on how tooconfigure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="66aca-225">Теперь, когда вы настроили на компьютере и узнали, как toomanage подписками и учетными записями хранения, с помощью Azure PowerShell, перейдите в следующий раздел toolearn toohello как большие двоичные объекты toomanage Azure и больших двоичных объектов моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="66aca-225">Now that you have set up your computer and learned how toomanage subscriptions and storage accounts using Azure PowerShell, go toohello next section toolearn how toomanage Azure blobs and blob snapshots.</span></span>

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="66aca-226">Как tooretrieve и повторное создание ключей хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="66aca-226">How tooretrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="66aca-227">Учетная запись хранилища Azure предоставляется с двумя ключами учетной записи.</span><span class="sxs-lookup"><span data-stu-id="66aca-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="66aca-228">Можно использовать следующий командлет tooretrieve hello ключей.</span><span class="sxs-lookup"><span data-stu-id="66aca-228">You can use hello following cmdlet tooretrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="66aca-229">Используйте следующий командлет tooretrieve определенного ключа hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-229">Use hello following cmdlet tooretrieve a specific key.</span></span> <span data-ttu-id="66aca-230">Допустимые значения: Primary и Secondary</span><span class="sxs-lookup"><span data-stu-id="66aca-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="66aca-231">Если вы хотите tooregenerate ключи, используйте следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-231">If you would like tooregenerate your keys, use hello following cmdlet.</span></span> <span data-ttu-id="66aca-232">Допустимые значения параметра -KeyType: Primary и Secondary</span><span class="sxs-lookup"><span data-stu-id="66aca-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a><span data-ttu-id="66aca-233">Как большие двоичные объекты toomanage Azure</span><span class="sxs-lookup"><span data-stu-id="66aca-233">How toomanage Azure blobs</span></span>
<span data-ttu-id="66aca-234">Хранилище Azure BLOB-объекта — это служба для хранения больших объемов неструктурированных данных, например текстовых или двоичных данных, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="66aca-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="66aca-235">В этом разделе предполагается, что вы уже знакомы с основными понятиями hello Azure Blob Storage Service.</span><span class="sxs-lookup"><span data-stu-id="66aca-235">This section assumes that you are already familiar with hello Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="66aca-236">Дополнительные сведения см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md) и [Понятия службы BLOB-объектов](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="66aca-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-toocreate-a-container"></a><span data-ttu-id="66aca-237">Как toocreate контейнера</span><span class="sxs-lookup"><span data-stu-id="66aca-237">How toocreate a container</span></span>
<span data-ttu-id="66aca-238">Каждый BLOB-объект в хранилище Azure должен находиться в контейнере.</span><span class="sxs-lookup"><span data-stu-id="66aca-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="66aca-239">Можно создать с помощью командлета New-AzureStorageContainer hello закрытый контейнер:</span><span class="sxs-lookup"><span data-stu-id="66aca-239">You can create a private container using hello New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="66aca-240">Существует три уровня анонимного доступа для чтения: **Отключено**, **Большой двоичный объект** и **Контейнер**.</span><span class="sxs-lookup"><span data-stu-id="66aca-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="66aca-241">tooprevent анонимный доступ к tooblobs параметр разрешения hello набора слишком**Off**.</span><span class="sxs-lookup"><span data-stu-id="66aca-241">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="66aca-242">По умолчанию hello новый контейнер является закрытым и может осуществляться только владельцем учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-242">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="66aca-243">анонимные открытый tooallow чтения tooblob доступ к ресурсам, но не toocontainer метаданные или toohello список больших двоичных объектов в контейнере hello, параметру hello разрешение слишком**большого двоичного объекта**.</span><span class="sxs-lookup"><span data-stu-id="66aca-243">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="66aca-244">полный открытый tooallow чтения tooblob доступ к ресурсам, метаданные контейнера и hello список больших двоичных объектов в контейнере hello, задайте параметр разрешение hello слишком**контейнер**.</span><span class="sxs-lookup"><span data-stu-id="66aca-244">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="66aca-245">Дополнительные сведения см. в разделе [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="66aca-245">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a><span data-ttu-id="66aca-246">Как tooupload большого двоичного объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="66aca-246">How tooupload a blob into a container</span></span>
<span data-ttu-id="66aca-247">Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="66aca-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="66aca-248">Дополнительные сведения см. в статье [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx) (Основные сведения о блочных, добавочных и страничных BLOB-объектах).</span><span class="sxs-lookup"><span data-stu-id="66aca-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="66aca-249">tooupload большие двоичные объекты в контейнере tooa, можно использовать hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) командлета.</span><span class="sxs-lookup"><span data-stu-id="66aca-249">tooupload blobs in tooa container, you can use hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="66aca-250">По умолчанию эта команда передает hello локальные файлы tooa блочного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="66aca-250">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="66aca-251">Тип hello toospecify для hello большого двоичного объекта, вы можете использовать параметр - BlobType hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-251">toospecify hello type for hello blob, you can use hello -BlobType parameter.</span></span>

<span data-ttu-id="66aca-252">Hello следующем примере выполняется hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) tooget командлет hello все файлы в указанной папке hello и передает их toohello следующий командлет с помощью оператора конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-252">hello following example runs hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget all hello files in hello specified folder, and then passes them toohello next cmdlet by using hello pipeline operator.</span></span> <span data-ttu-id="66aca-253">Hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) командлет отправляет hello локальные файлы tooyour контейнера:</span><span class="sxs-lookup"><span data-stu-id="66aca-253">hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads hello local files tooyour container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a><span data-ttu-id="66aca-254">Как toodownload большие двоичные объекты из контейнера</span><span class="sxs-lookup"><span data-stu-id="66aca-254">How toodownload blobs from a container</span></span>
<span data-ttu-id="66aca-255">Привет, в следующем примере показано, как toodownload большие двоичные объекты из контейнера.</span><span class="sxs-lookup"><span data-stu-id="66aca-255">hello following example demonstrates how toodownload blobs from a container.</span></span> <span data-ttu-id="66aca-256">пример Hello сначала устанавливает соединение tooAzure хранилища с помощью контекста учетной записи хранилища hello, который включает в себя имя учетной записи хранения hello и ее первичный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="66aca-256">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its primary access key.</span></span> <span data-ttu-id="66aca-257">Затем пример hello извлекает ссылку BLOB-объекта с помощью hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) командлета.</span><span class="sxs-lookup"><span data-stu-id="66aca-257">Then, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="66aca-258">Затем пример hello использует hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) командлет toodownload BLOB-объектов в hello локальной целевой папки.</span><span class="sxs-lookup"><span data-stu-id="66aca-258">Next, hello example uses hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs into hello local destination folder.</span></span>

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a><span data-ttu-id="66aca-259">Как toocopy большие двоичные объекты из одной tooanother контейнер хранилища</span><span class="sxs-lookup"><span data-stu-id="66aca-259">How toocopy blobs from one storage container tooanother</span></span>
<span data-ttu-id="66aca-260">Можно асинхронно копировать BLOB-объекты между учетными записями хранения и областями.</span><span class="sxs-lookup"><span data-stu-id="66aca-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="66aca-261">Hello следующем примере показано, как toocopy большие двоичные объекты из одного места хранения tooanother контейнера в двух разных учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="66aca-261">hello following example demonstrates how toocopy blobs from one storage container tooanother in two different storage accounts.</span></span> <span data-ttu-id="66aca-262">пример Hello сначала задает переменные для источника и назначения учетных записей хранилища, а затем создает контекст хранилища для каждой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="66aca-262">hello example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="66aca-263">Далее пример hello копирует BLOB-объектов из hello исходный контейнер toohello конечный контейнер с помощью hello [AzureStorageBlobCopy начала](/powershell/module/azure.storage/start-azurestorageblobcopy) командлета.</span><span class="sxs-lookup"><span data-stu-id="66aca-263">Next, hello example copies blobs from hello source container toohello destination container using hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="66aca-264">пример Hello предполагается, что hello источника и назначения и учетных записей хранилища контейнеры уже существуют.</span><span class="sxs-lookup"><span data-stu-id="66aca-264">hello example assumes that hello source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="66aca-265">Обратите внимание, что этот пример выполняет асинхронное копирование.</span><span class="sxs-lookup"><span data-stu-id="66aca-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="66aca-266">Можно отслеживать состояние hello каждой копии, выполнив hello [Get AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) командлета.</span><span class="sxs-lookup"><span data-stu-id="66aca-266">You can monitor hello status of each copy by running hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-toocopy-blobs-from-a-secondary-location"></a><span data-ttu-id="66aca-267">Как toocopy большие двоичные объекты из дополнительного расположения</span><span class="sxs-lookup"><span data-stu-id="66aca-267">How toocopy blobs from a secondary location</span></span>
<span data-ttu-id="66aca-268">Большие двоичные объекты можно скопировать из дополнительного расположения hello поддержкой RA-GRS учетной записи.</span><span class="sxs-lookup"><span data-stu-id="66aca-268">You can copy blobs from hello secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a><span data-ttu-id="66aca-269">Как toodelete большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="66aca-269">How toodelete a blob</span></span>
<span data-ttu-id="66aca-270">toodelete большого двоичного объекта сначала получить ссылку на большой двоичный объект, а затем вызвать командлет Remove-AzureStorageBlob hello на нем.</span><span class="sxs-lookup"><span data-stu-id="66aca-270">toodelete a blob, first get a blob reference and then call hello Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="66aca-271">Привет, следующий пример удаляет все большие двоичные объекты hello в данном контейнере.</span><span class="sxs-lookup"><span data-stu-id="66aca-271">hello following example deletes all hello blobs in a given container.</span></span> <span data-ttu-id="66aca-272">пример Hello сначала задает переменные для учетной записи хранения, а затем создает контекст хранилища.</span><span class="sxs-lookup"><span data-stu-id="66aca-272">hello example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="66aca-273">Далее пример hello извлекает ссылку BLOB-объекта с помощью hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) командлета и запускает hello [AzureStorageBlob удаление](/powershell/module/azure.storage/remove-azurestorageblob) командлет tooremove BLOB-объекты из контейнера в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-273">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs from a container in Azure storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a><span data-ttu-id="66aca-274">Как toomanage Azure BLOB-объектов моментальные снимки</span><span class="sxs-lookup"><span data-stu-id="66aca-274">How toomanage Azure blob snapshots</span></span>
<span data-ttu-id="66aca-275">Azure позволяет создать моментальный снимок BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="66aca-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="66aca-276">Моментальный снимок — это версия BLOB-объекта только для чтения, сделанная в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="66aca-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="66aca-277">После создания моментального снимка его можно читать, копировать или удалять, но нельзя изменять.</span><span class="sxs-lookup"><span data-stu-id="66aca-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="66aca-278">Моментальные снимки обеспечивают tooback способом копирования большого двоичного объекта, как оно отображается в момент времени.</span><span class="sxs-lookup"><span data-stu-id="66aca-278">Snapshots provide a way tooback up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="66aca-279">Дополнительные сведения см. в статье [Создание моментального снимка большого двоичного объекта](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="66aca-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-toocreate-a-blob-snapshot"></a><span data-ttu-id="66aca-280">Как toocreate снимка большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="66aca-280">How toocreate a blob snapshot</span></span>
<span data-ttu-id="66aca-281">toocreate snaphot большого двоичного объекта, сначала нужно получить ссылку на большой двоичный объект, а затем вызвать hello `ICloudBlob.CreateSnapshot` метода.</span><span class="sxs-lookup"><span data-stu-id="66aca-281">toocreate a snaphot of a blob, first get a blob reference and then call hello `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="66aca-282">Hello в примере сначала устанавливается переменных для учетной записи хранилища, а затем создает контекст хранилища.</span><span class="sxs-lookup"><span data-stu-id="66aca-282">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="66aca-283">Затем пример hello извлекает ссылку BLOB-объекта с помощью hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello командлета и выполняется [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate метод моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="66aca-283">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a><span data-ttu-id="66aca-284">Как моментальные снимки toolist большого двоичного объекта в</span><span class="sxs-lookup"><span data-stu-id="66aca-284">How toolist a blob's snapshots</span></span>
<span data-ttu-id="66aca-285">Можно создать любое количество моментальных снимков для BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="66aca-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="66aca-286">Можно перечислить hello моментальных снимков, связанных с вашей tootrack большого двоичного объекта вашей текущей моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="66aca-286">You can list hello snapshots associated with your blob tootrack your current snapshots.</span></span> <span data-ttu-id="66aca-287">Hello следующий пример использует предопределенные hello BLOB-объекта и вызывает метод [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) командлет toolist hello моментальные снимки большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="66aca-287">hello following example uses a predefined blob and calls hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist hello snapshots of that blob.</span></span>  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a><span data-ttu-id="66aca-288">Как toocopy моментальный снимок большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="66aca-288">How toocopy a snapshot of a blob</span></span>
<span data-ttu-id="66aca-289">Можно скопировать моментальный снимок hello toorestore моментального снимка большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="66aca-289">You can copy a snapshot of a blob toorestore hello snapshot.</span></span> <span data-ttu-id="66aca-290">Подробные сведения и ограничения см. в статье [Создание моментального снимка большого двоичного объекта](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="66aca-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="66aca-291">Hello в примере сначала устанавливается переменных для учетной записи хранилища, а затем создает контекст хранилища.</span><span class="sxs-lookup"><span data-stu-id="66aca-291">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="66aca-292">Затем пример hello определяет переменные имя контейнера и больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-292">Next, hello example defines hello container and blob name variables.</span></span> <span data-ttu-id="66aca-293">пример Hello извлекает ссылку BLOB-объекта с помощью hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) командлета и запускает hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate метод моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="66aca-293">hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span> <span data-ttu-id="66aca-294">Затем пример hello запускает hello [AzureStorageBlobCopy начала](/powershell/module/azure.storage/start-azurestorageblobcopy) командлет toocopy hello моментальный снимок большого двоичного объекта, используя объект ICloudBlob hello для hello исходного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="66aca-294">Then, hello example runs hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello snapshot of a blob using hello ICloudBlob object for hello source blob.</span></span> <span data-ttu-id="66aca-295">Убедитесь, что переменные hello tooupdate исходя из имеющейся конфигурации перед рабочего примера hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-295">Be sure tooupdate hello variables based on your configuration before running hello example.</span></span> <span data-ttu-id="66aca-296">Обратите внимание, что, hello, в следующем примере предполагается, что hello источника и назначения контейнеров и hello исходный большой двоичный объект уже существует.</span><span class="sxs-lookup"><span data-stu-id="66aca-296">Note that hello following example assumes that hello source and destination containers, and hello source blob already exist.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="66aca-297">Теперь, когда вы узнали, как большие двоичные объекты toomanage Azure и больших двоичных объектов моментальные снимки с помощью Azure PowerShell, перейдите toohello Далее раздел toolearn как toomanage таблиц, очередей и файлов.</span><span class="sxs-lookup"><span data-stu-id="66aca-297">Now that you have learned how toomanage Azure blobs and blob snapshots with Azure PowerShell, go toohello next section toolearn how toomanage tables, queues, and files.</span></span>

## <a name="how-toomanage-azure-tables-and-table-entities"></a><span data-ttu-id="66aca-298">Как toomanage Azure таблицы и таблицы сущностей</span><span class="sxs-lookup"><span data-stu-id="66aca-298">How toomanage Azure tables and table entities</span></span>
<span data-ttu-id="66aca-299">Служба хранилища Azure таблицы — в хранилище данных NoSQL, который можно использовать toostore и запрос большого набора нереляционных структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="66aca-299">Azure Table storage service is a NoSQL datastore, which you can use toostore and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="66aca-300">Основные компоненты службы hello Hello являются таблицы, сущности и свойства.</span><span class="sxs-lookup"><span data-stu-id="66aca-300">hello main components of hello service are tables, entities, and properties.</span></span> <span data-ttu-id="66aca-301">Таблица представляет собой коллекцию сущностей.</span><span class="sxs-lookup"><span data-stu-id="66aca-301">A table is a collection of entities.</span></span> <span data-ttu-id="66aca-302">Сущность — это набор свойств.</span><span class="sxs-lookup"><span data-stu-id="66aca-302">An entity is a set of properties.</span></span> <span data-ttu-id="66aca-303">Каждая сущность может содержать до too252 свойства, которые являются все пары имя значение.</span><span class="sxs-lookup"><span data-stu-id="66aca-303">Each entity can have up too252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="66aca-304">В этом разделе предполагается, что вы уже знакомы с основными понятиями hello службы хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-304">This section assumes that you are already familiar with hello Azure Table Storage Service concepts.</span></span> <span data-ttu-id="66aca-305">Дополнительные сведения см. в разделе [hello основные сведения о модели данных службы таблиц](http://msdn.microsoft.com/library/azure/dd179338.aspx) и [приступить к работе с хранилищем таблиц Azure, с помощью .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="66aca-305">For detailed information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="66aca-306">В следующих подразделах hello вы узнаете, как toomanage хранилище таблиц Azure службы с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-306">In hello following subsections, you'll learn how toomanage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="66aca-307">Hello сценарии включают **создание**, **удаление**, и **получение** **таблиц**, а также **добавление**, **запрос**, и **удаления сущностей таблицы**.</span><span class="sxs-lookup"><span data-stu-id="66aca-307">hello scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-toocreate-a-table"></a><span data-ttu-id="66aca-308">Как toocreate таблицы</span><span class="sxs-lookup"><span data-stu-id="66aca-308">How toocreate a table</span></span>
<span data-ttu-id="66aca-309">Каждая таблица должна находиться в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="66aca-310">Hello следующем примере показано, как toocreate таблица в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-310">hello following example demonstrates how toocreate a table in Azure Storage.</span></span> <span data-ttu-id="66aca-311">пример Hello сначала устанавливает соединение tooAzure хранилища с помощью контекста учетной записи хранилища hello, который включает в себя имя учетной записи хранения hello и ее ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="66aca-311">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="66aca-312">Затем он использует hello [New AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) toocreate командлет таблица в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-312">Next, it uses hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate a table in Azure Storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a><span data-ttu-id="66aca-313">Как tooretrieve таблицы</span><span class="sxs-lookup"><span data-stu-id="66aca-313">How tooretrieve a table</span></span>
<span data-ttu-id="66aca-314">Можно запрашивать и получить одну или все таблицы в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="66aca-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="66aca-315">Hello следующем примере показано, как в данной таблице с помощью tooretrieve hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) командлета.</span><span class="sxs-lookup"><span data-stu-id="66aca-315">hello following example demonstrates how tooretrieve a given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="66aca-316">Если вызвать командлет Get-AzureStorageTable hello без параметров, он получает все таблицы хранилища для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="66aca-316">If you call hello Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-toodelete-a-table"></a><span data-ttu-id="66aca-317">Как toodelete таблицы</span><span class="sxs-lookup"><span data-stu-id="66aca-317">How toodelete a table</span></span>
<span data-ttu-id="66aca-318">Можно удалить таблицу из учетной записи хранилища с помощью hello [AzureStorageTable удаление](/powershell/module/azure.storage/remove-azurestoragetable) командлета.</span><span class="sxs-lookup"><span data-stu-id="66aca-318">You can delete a table from a storage account by using hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a><span data-ttu-id="66aca-319">Как toomanage таблицу сущностей</span><span class="sxs-lookup"><span data-stu-id="66aca-319">How toomanage table entities</span></span>
<span data-ttu-id="66aca-320">В настоящее время Azure PowerShell предоставляет командлеты сущностей таблицы toomanage непосредственно.</span><span class="sxs-lookup"><span data-stu-id="66aca-320">Currently, Azure PowerShell does not provide cmdlets toomanage table entities directly.</span></span> <span data-ttu-id="66aca-321">tooperform операций в табличных объектах, можно использовать классы hello в hello [клиентская библиотека хранилища Azure для .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="66aca-321">tooperform operations on table entities, you can use hello classes given in hello [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-tooadd-table-entities"></a><span data-ttu-id="66aca-322">Как tooadd таблицу сущностей</span><span class="sxs-lookup"><span data-stu-id="66aca-322">How tooadd table entities</span></span>
<span data-ttu-id="66aca-323">tooadd таблица tooa объекта, сначала создайте объект, который определяет свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="66aca-323">tooadd an entity tooa table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="66aca-324">Сущность может иметь свойства too255, включая 3 системные свойства: **PartitionKey**, **RowKey**, и **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="66aca-324">An entity can have up too255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="66aca-325">Вы несете ответственность за вставки и обновления значения hello **PartitionKey** и **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="66aca-325">You are responsible for inserting and updating hello values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="66aca-326">Hello server управляет значение hello **Timestamp**, которую нельзя вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="66aca-326">hello server manages hello value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="66aca-327">Hello вместе **PartitionKey** и **RowKey** уникально идентифицируют каждую сущность в таблицу.</span><span class="sxs-lookup"><span data-stu-id="66aca-327">Together hello **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="66aca-328">**PartitionKey**: Определяет hello секции, хранящиеся в сущности hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-328">**PartitionKey**: Determines hello partition that hello entity is stored in.</span></span>
* <span data-ttu-id="66aca-329">**RowKey**: однозначно определяет сущность hello в секции hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-329">**RowKey**: Uniquely identifies hello entity within hello partition.</span></span>

<span data-ttu-id="66aca-330">Вы можете определить too252 пользовательские свойства для сущности.</span><span class="sxs-lookup"><span data-stu-id="66aca-330">You may define up too252 custom properties for an entity.</span></span> <span data-ttu-id="66aca-331">Дополнительные сведения см. в разделе [hello основные сведения о модели данных службы таблиц](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="66aca-331">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="66aca-332">Hello следующем примере показано, как таблицы tooa tooadd сущностей.</span><span class="sxs-lookup"><span data-stu-id="66aca-332">hello following example demonstrates how tooadd entities tooa table.</span></span> <span data-ttu-id="66aca-333">пример Hello показано, как tooretrieve hello таблицы сотрудников и добавить в нее несколько сущностей.</span><span class="sxs-lookup"><span data-stu-id="66aca-333">hello example shows how tooretrieve hello employee table and add several entities into it.</span></span> <span data-ttu-id="66aca-334">Во-первых, он устанавливает соединение tooAzure хранилища с помощью контекста учетной записи хранилища hello, который включает в себя имя учетной записи хранения hello и ее ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="66aca-334">First, it establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="66aca-335">Затем он извлекает hello таблицы с помощью hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) командлета.</span><span class="sxs-lookup"><span data-stu-id="66aca-335">Next, it retrieves hello given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="66aca-336">Здравствуйте, если таблица hello не существует, [New AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) командлета — toocreate используется таблица в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-336">If hello table does not exist, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used toocreate a table in Azure Storage.</span></span> <span data-ttu-id="66aca-337">Далее пример hello определяет пользовательскую функцию добавить сущность tooadd сущностей toohello таблицы путем указания каждой секции и ключ строки.</span><span class="sxs-lookup"><span data-stu-id="66aca-337">Next, hello example defines a custom function Add-Entity tooadd entities toohello table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="66aca-338">hello вызовов функции Hello добавить сущность [New-Object](http://technet.microsoft.com/library/hh849885.aspx) командлет hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) toocreate класс объекта сущности.</span><span class="sxs-lookup"><span data-stu-id="66aca-338">hello Add-Entity function calls hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class toocreate an entity object.</span></span> <span data-ttu-id="66aca-339">Позже, пример hello вызывает hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) метод для этой сущности объекта tooadd его tooa таблицы.</span><span class="sxs-lookup"><span data-stu-id="66aca-339">Later, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object tooadd it tooa table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a><span data-ttu-id="66aca-340">Как tooquery таблицу сущностей</span><span class="sxs-lookup"><span data-stu-id="66aca-340">How tooquery table entities</span></span>
<span data-ttu-id="66aca-341">tooquery таблицы, используйте hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) класса.</span><span class="sxs-lookup"><span data-stu-id="66aca-341">tooquery a table, use hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="66aca-342">Hello в примере предполагается, что вы уже запускали hello скрипта, данного в hello, как tooadd сущностей разделах данного руководства.</span><span class="sxs-lookup"><span data-stu-id="66aca-342">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="66aca-343">пример Hello сначала устанавливает соединение tooAzure хранилища с помощью контекста hello хранилища, который включает в себя имя учетной записи хранения hello и ее ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="66aca-343">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="66aca-344">Затем она попытается таблицы tooretrieve hello ранее созданные «сотрудники», с помощью hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) командлета.</span><span class="sxs-lookup"><span data-stu-id="66aca-344">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="66aca-345">Вызов hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) на hello Microsoft.WindowsAzure.Storage.Table.TableQuery класс создает новый объект запроса.</span><span class="sxs-lookup"><span data-stu-id="66aca-345">Calling hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="66aca-346">пример Hello ищет hello сущностей, которые имеют столбец «ID», значение которого равно 1, как указано в фильтр строк.</span><span class="sxs-lookup"><span data-stu-id="66aca-346">hello example looks for hello entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="66aca-347">Дополнительные сведения см. в статье [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx) (Запросы к таблицам и сущностям).</span><span class="sxs-lookup"><span data-stu-id="66aca-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="66aca-348">При выполнении этот запрос возвращает все сущности, которые соответствуют критериям фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-348">When you run this query, it returns all entities that match hello filter criteria.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a><span data-ttu-id="66aca-349">Как toodelete таблицу сущностей</span><span class="sxs-lookup"><span data-stu-id="66aca-349">How toodelete table entities</span></span>
<span data-ttu-id="66aca-350">Сущность можно удалить с помощью ее ключей раздела и строки.</span><span class="sxs-lookup"><span data-stu-id="66aca-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="66aca-351">Hello в примере предполагается, что вы уже запускали hello скрипта, данного в hello, как tooadd сущностей разделах данного руководства.</span><span class="sxs-lookup"><span data-stu-id="66aca-351">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="66aca-352">пример Hello сначала устанавливает соединение tooAzure хранилища с помощью контекста hello хранилища, который включает в себя имя учетной записи хранения hello и ее ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="66aca-352">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="66aca-353">Затем она попытается таблицы tooretrieve hello ранее созданные «сотрудники», с помощью hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) командлета.</span><span class="sxs-lookup"><span data-stu-id="66aca-353">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="66aca-354">Если hello таблица существует, пример hello вызывает hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve метод сущностью, основанной на значениях ключей секций и строк.</span><span class="sxs-lookup"><span data-stu-id="66aca-354">If hello table exists, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method tooretrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="66aca-355">Затем передайте hello сущности toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete метод.</span><span class="sxs-lookup"><span data-stu-id="66aca-355">Then, pass hello entity toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method toodelete.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a><span data-ttu-id="66aca-356">Как toomanage Azure помещает в очередь и очередь сообщений</span><span class="sxs-lookup"><span data-stu-id="66aca-356">How toomanage Azure queues and queue messages</span></span>
<span data-ttu-id="66aca-357">Хранилище Azure очереди — это служба для хранения большого количества сообщений, которые может осуществляться из любого места в Здравствуй, мир! через вызовы прошедшего проверку подлинности, протокол HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="66aca-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="66aca-358">В этом разделе предполагается, что вы уже знакомы с основными понятиями hello службы хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-358">This section assumes that you are already familiar with hello Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="66aca-359">Дополнительные сведения см. в статье [Приступая к работе с хранилищем очередей Azure с помощью .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="66aca-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="66aca-360">В этом разделе будет показано, как toomanage хранилища очередей Azure службы с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-360">This section will show you how toomanage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="66aca-361">Hello сценарии включают **Вставка** и **удаление** очередь сообщений, а также **создание**, **удаление**и **Получение очередей**.</span><span class="sxs-lookup"><span data-stu-id="66aca-361">hello scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-toocreate-a-queue"></a><span data-ttu-id="66aca-362">Как toocreate очереди</span><span class="sxs-lookup"><span data-stu-id="66aca-362">How toocreate a queue</span></span>
<span data-ttu-id="66aca-363">Hello следующий пример сначала устанавливает соединение tooAzure хранилища с помощью контекста учетной записи хранилища hello, который включает в себя имя учетной записи хранения hello и ее ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="66aca-363">hello following example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="66aca-364">Затем он вызывает [New AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) toocreate командлет очередь с именем «queuename».</span><span class="sxs-lookup"><span data-stu-id="66aca-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate a queue named 'queuename'.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="66aca-365">Сведения о соглашениях об именовании для службы очередей Azure см. в статье [Именование очередей и метаданных](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="66aca-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-tooretrieve-a-queue"></a><span data-ttu-id="66aca-366">Как tooretrieve очереди</span><span class="sxs-lookup"><span data-stu-id="66aca-366">How tooretrieve a queue</span></span>
<span data-ttu-id="66aca-367">Можно запрашивать и определенной очереди или список всех очередей hello в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="66aca-367">You can query and retrieve a specific queue or a list of all hello queues in a Storage account.</span></span> <span data-ttu-id="66aca-368">Hello следующем примере показано, как hello в указанной очереди с помощью tooretrieve [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) командлета.</span><span class="sxs-lookup"><span data-stu-id="66aca-368">hello following example demonstrates how tooretrieve a specified queue using hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="66aca-369">Если вы вызываете hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) командлет без параметров возвращает список всех очередей hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-369">If you call hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all hello queues.</span></span>

### <a name="how-toodelete-a-queue"></a><span data-ttu-id="66aca-370">Как toodelete очереди</span><span class="sxs-lookup"><span data-stu-id="66aca-370">How toodelete a queue</span></span>
<span data-ttu-id="66aca-371">toodelete очередь и все сообщения hello содержащихся в ней командлет Remove-AzureStorageQueue hello вызова.</span><span class="sxs-lookup"><span data-stu-id="66aca-371">toodelete a queue and all hello messages contained in it, call hello Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="66aca-372">Hello в следующем примере показано, как в указанной очереди с помощью toodelete hello командлет Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="66aca-372">hello following example shows how toodelete a specified queue using hello Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a><span data-ttu-id="66aca-373">Как tooinsert сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="66aca-373">How tooinsert a message into a queue</span></span>
<span data-ttu-id="66aca-374">tooinsert сообщения в существующую очередь, сначала создайте новый экземпляр hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) класса.</span><span class="sxs-lookup"><span data-stu-id="66aca-374">tooinsert a message into an existing queue, first create a new instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="66aca-375">Затем вызовите hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) метод.</span><span class="sxs-lookup"><span data-stu-id="66aca-375">Next, call hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="66aca-376">Для создания CloudQueueMessage можно использовать строку (в формате UTF-8) или массив байтов.</span><span class="sxs-lookup"><span data-stu-id="66aca-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="66aca-377">Hello в следующем примере показано, как очередь tooa tooadd сообщений.</span><span class="sxs-lookup"><span data-stu-id="66aca-377">hello following example demonstrates how tooadd message tooa queue.</span></span> <span data-ttu-id="66aca-378">пример Hello сначала устанавливает соединение tooAzure хранилища с помощью контекста учетной записи хранилища hello, который включает в себя имя учетной записи хранения hello и ее ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="66aca-378">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="66aca-379">Затем он извлекает hello указанной очереди с помощью hello [Get AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="66aca-379">Next, it retrieves hello specified queue using hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="66aca-380">Если hello очередь существует, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) командлета — используется toocreate экземпляр hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) класса.</span><span class="sxs-lookup"><span data-stu-id="66aca-380">If hello queue exists, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used toocreate an instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="66aca-381">Более поздней версии, пример hello вызывает hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) метод tooadd объекта этого сообщения оно tooa очереди.</span><span class="sxs-lookup"><span data-stu-id="66aca-381">Later, hello example calls hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object tooadd it tooa queue.</span></span> <span data-ttu-id="66aca-382">Ниже приведен код, который извлекает очереди и вставляет приветственное сообщение «MessageInfo».</span><span class="sxs-lookup"><span data-stu-id="66aca-382">Here is code which retrieves a queue and inserts hello message 'MessageInfo':</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a><span data-ttu-id="66aca-383">Как toode в очередь на hello следующего сообщения</span><span class="sxs-lookup"><span data-stu-id="66aca-383">How toode-queue at hello next message</span></span>
<span data-ttu-id="66aca-384">Код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="66aca-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="66aca-385">При вызове hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) метода, вы получаете следующее сообщение hello в очереди.</span><span class="sxs-lookup"><span data-stu-id="66aca-385">When you call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get hello next message in a queue.</span></span> <span data-ttu-id="66aca-386">Сообщение, возвращенное из **GetMessage** становится невидимой tooany другой код, чтение сообщений из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="66aca-386">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="66aca-387">toofinish удаление приветственное сообщение из очереди hello, необходимо также вызвать hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) метод.</span><span class="sxs-lookup"><span data-stu-id="66aca-387">toofinish removing hello message from hello queue, you must also call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="66aca-388">Это двухэтапный процесс удаления сообщения подтверждает, если tooprocess получит сообщение toohardware или ошибок программного обеспечения, другой экземпляр кода из-за сбоя программы hello одного сообщения и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="66aca-388">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="66aca-389">Вызовы кода **DeleteMessage** сразу после обработки сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-389">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a><span data-ttu-id="66aca-390">Как toomanage Azure файла, папки и файлы</span><span class="sxs-lookup"><span data-stu-id="66aca-390">How toomanage Azure file shares and files</span></span>
<span data-ttu-id="66aca-391">Хранилище файлов Azure предоставляет общее хранилище для приложений с помощью стандартного протокола SMB hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-391">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="66aca-392">Виртуальные машины Microsoft Azure и облачных служб можно совместно использовать данные файлов между компонентами приложения с помощью монтируемых хранилищ и локальных приложений можно открыть файл данных в общей папке посредством API хранилища файлов hello или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via hello File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="66aca-393">Подробнее о хранилище файлов Azure см. в статьях [Приступая к работе с хранилищем файлов Azure в Windows](storage-dotnet-how-to-use-files.md) и [API REST службы файлов](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="66aca-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-tooset-and-query-storage-analytics"></a><span data-ttu-id="66aca-394">Как tooset и запросов аналитики хранилища</span><span class="sxs-lookup"><span data-stu-id="66aca-394">How tooset and query storage analytics</span></span>
<span data-ttu-id="66aca-395">Можно использовать [аналитики хранилища Azure](storage-analytics.md) показатели toocollect учетных записей хранилища Azure, а также данные журналов о запросах, отправляемых tooyour учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="66aca-395">You can use [Azure Storage Analytics](storage-analytics.md) toocollect metrics for your Azure storage accounts and log data about requests sent tooyour storage account.</span></span> <span data-ttu-id="66aca-396">Можно использовать работоспособность hello toomonitor метрик хранилища учетной записи хранилища и toodiagnose ведения журнала хранилища и неполадок, связанных с вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="66aca-396">You can use storage metrics toomonitor hello health of a storage account, and storage logging toodiagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="66aca-397">Вы можете настроить отслеживание с помощью hello портал Azure или Windows PowerShell или программным путем с помощью клиентской библиотеки хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="66aca-397">You can configure monitoring using hello Azure portal or Windows PowerShell, or programmatically using hello storage client library.</span></span> <span data-ttu-id="66aca-398">Ведение журнала хранилища происходит на стороне сервера, а также позволяет toorecord подробные сведения об успешных и неудачных запросов в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="66aca-398">Storage logging happens server-side and enables you toorecord details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="66aca-399">Эти журналы включить сведения о toosee операций delete от вашей таблицы, очереди и больших двоичных объектов а также hello причин для невыполненных запросов, чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="66aca-399">These logs enable you toosee details of read, write, and delete operations against your tables, queues, and blobs as well as hello reasons for failed requests.</span></span>

<span data-ttu-id="66aca-400">toolearn tooenable и просмотр метрик хранилища данных, с помощью PowerShell, в статье [как tooenable метрик хранилища с помощью PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="66aca-400">toolearn how tooenable and view Storage Metrics data using PowerShell, see [How tooenable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="66aca-401">toolearn tooenable и извлечь ведения журнала хранилища данных с помощью PowerShell, в статье [как tooenable хранилища ведение журнала с помощью PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) и [поиск данных ведения журнала хранилища журнала](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="66aca-401">toolearn how tooenable and retrieve Storage Logging data using PowerShell, see [How tooenable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="66aca-402">Подробные сведения по использованию метрик хранилищ и ведению журналов хранилища проблемы tootroubleshoot хранилища см. в разделе [мониторинг, диагностика и устранение неполадок хранилища Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="66aca-402">For detailed information on using Storage Metrics and Storage Logging tootroubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="66aca-403">Способ совместного использования toomanage URL-адреса (SAS) и хранимой политикой доступа</span><span class="sxs-lookup"><span data-stu-id="66aca-403">How toomanage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="66aca-404">Подписи общего доступа являются важной частью hello модель безопасности для всех приложений, использующих хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-404">Shared access signatures are an important part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="66aca-405">Они могут использоваться для предоставления tooclients учетной записи хранилища tooyour ограниченные разрешения, не следует hello ключ учетной записи.</span><span class="sxs-lookup"><span data-stu-id="66aca-405">They are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="66aca-406">По умолчанию только владелец hello hello учетной записи хранения может обращаться к BLOB-объектов, таблиц и очередей в этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="66aca-406">By default, only hello owner of hello storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="66aca-407">Если служба или приложение, должен toomake эти ресурсы доступны tooother клиенты без предоставления ключа доступа, у вас есть три варианта:</span><span class="sxs-lookup"><span data-stu-id="66aca-407">If your service or application needs toomake these resources available tooother clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="66aca-408">Задайте контейнер разрешения toopermit анонимный доступ для чтения toohello контейнера и BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="66aca-408">Set a container's permissions toopermit anonymous read access toohello container and its blobs.</span></span> <span data-ttu-id="66aca-409">Такие разрешения нельзя задать для таблиц и очередей.</span><span class="sxs-lookup"><span data-stu-id="66aca-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="66aca-410">Используйте подпись общего доступа, которая предоставляет ограниченный доступ toocontainers права, большие двоичные объекты, очереди и таблицы для определенного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="66aca-410">Use a shared access signature that grants restricted access rights toocontainers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="66aca-411">Используйте tooobtain политики доступа дополнительный уровень контроля над подписями общего доступа к контейнеру и его большие двоичные объекты, очереди или таблицы.</span><span class="sxs-lookup"><span data-stu-id="66aca-411">Use a stored access policy tooobtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="66aca-412">Hello хранимая политика доступа позволяет время начала toochange hello, истечение срока действия и разрешения для подписи, или toorevoke ее после ее выдачи.</span><span class="sxs-lookup"><span data-stu-id="66aca-412">hello stored access policy allows you toochange hello start time, expiry time, or permissions for a signature, or toorevoke it after it has been issued.</span></span>

<span data-ttu-id="66aca-413">Подписанный URL-адрес может быть в одной из двух следующих форм.</span><span class="sxs-lookup"><span data-stu-id="66aca-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="66aca-414">**Ad hoc SAS**: при создании нерегламентированного SAS, hello время начала, время окончания срока действия, и разрешения для hello SAS указаны на hello универсальный код Ресурса SAS.</span><span class="sxs-lookup"><span data-stu-id="66aca-414">**Ad hoc SAS**: When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span> <span data-ttu-id="66aca-415">Этот тип подписанного URL-адреса можно создать для контейнера, большого двоичного объекта, таблицы или очереди, и его невозможно отозвать.</span><span class="sxs-lookup"><span data-stu-id="66aca-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="66aca-416">**SAS с хранимой политикой доступа**: определенной хранимой политики доступа на контейнер ресурсов контейнер больших двоичных объектов, таблицы или очереди - и его можно использовать toomanage ограничения для одного или нескольких подписей общего доступа.</span><span class="sxs-lookup"><span data-stu-id="66aca-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="66aca-417">При связывании подписанный URL-адрес с хранимой политикой доступа hello SAS наследует ограничения hello - hello время начала, время окончания и разрешения -, определенные для hello хранимые политики доступа.</span><span class="sxs-lookup"><span data-stu-id="66aca-417">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span> <span data-ttu-id="66aca-418">Подписанный URL-адрес этого типа можно отозвать.</span><span class="sxs-lookup"><span data-stu-id="66aca-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="66aca-419">Дополнительные сведения см. в разделе [с помощью общего доступа подписи (SAS)](storage-dotnet-shared-access-signature-part-1.md) и [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="66aca-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="66aca-420">В следующих разделах hello, вы узнаете, как toocreate политику доступа маркера и хранимые подпись общего доступа для таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-420">In hello next sections, you will learn how toocreate a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="66aca-421">Azure PowerShell предоставляет одинаковые командлеты для контейнеров, больших двоичных объектов и очередей.</span><span class="sxs-lookup"><span data-stu-id="66aca-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="66aca-422">hello загрузки сценариев hello toorun в этом разделе [Azure PowerShell версии 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="66aca-422">toorun hello scripts in this section, download hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="66aca-423">Как токен SAS toocreate на основе политик</span><span class="sxs-lookup"><span data-stu-id="66aca-423">How toocreate a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="66aca-424">Используйте toocreate командлет New-AzureStorageTableStoredAccessPolicy hello новой хранимой политики доступа.</span><span class="sxs-lookup"><span data-stu-id="66aca-424">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy.</span></span> <span data-ttu-id="66aca-425">Затем вызовите метод hello [New AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate командлет новый маркер подписи общего доступа на основе политик для таблицы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="66aca-425">Then, call hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="66aca-426">Как toocreate нерегламентированных (без отзыва) токена подписи коллективного доступа</span><span class="sxs-lookup"><span data-stu-id="66aca-426">How toocreate an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="66aca-427">Используйте hello [New AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate командлет новый нерегламентированных (без отзыва) токена подписи коллективного доступа для таблицы хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="66aca-427">Use hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a><span data-ttu-id="66aca-428">Как toocreate хранимой политики доступа</span><span class="sxs-lookup"><span data-stu-id="66aca-428">How toocreate a stored access policy</span></span>
<span data-ttu-id="66aca-429">Используйте toocreate командлет hello AzureStorageTableStoredAccessPolicy создать новую политику доступа для таблицы хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="66aca-429">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a><span data-ttu-id="66aca-430">Как tooupdate хранимой политики доступа</span><span class="sxs-lookup"><span data-stu-id="66aca-430">How tooupdate a stored access policy</span></span>
<span data-ttu-id="66aca-431">Используйте tooupdate командлета Set-AzureStorageTableStoredAccessPolicy hello существующую политику доступа для таблицы хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="66aca-431">Use hello Set-AzureStorageTableStoredAccessPolicy cmdlet tooupdate an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a><span data-ttu-id="66aca-432">Как toodelete хранимой политики доступа</span><span class="sxs-lookup"><span data-stu-id="66aca-432">How toodelete a stored access policy</span></span>
<span data-ttu-id="66aca-433">Используйте toodelete командлет Remove-AzureStorageTableStoredAccessPolicy hello хранимой политики доступа в таблице хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="66aca-433">Use hello Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="66aca-434">Как toouse хранилища Azure для государственных организаций США и Azure China</span><span class="sxs-lookup"><span data-stu-id="66aca-434">How toouse Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="66aca-435">Среда Azure — это независимое развертывание Microsoft Azure, такое как [Azure для государственных организаций в правительстве США](https://azure.microsoft.com/features/gov/), [AzureCloud для глобального Azure](https://portal.azure.com) и [AzureChinaCloud для Azure под управлением 21Vianet в Китае](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="66aca-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="66aca-436">Можно выполнить развертывание новых сред Azure для правительства США и Китая.</span><span class="sxs-lookup"><span data-stu-id="66aca-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="66aca-437">toouse хранилища Azure с AzureChinaCloud необходимо toocreate контекст хранилища, которая связана с AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="66aca-437">toouse Azure Storage with AzureChinaCloud, you need toocreate a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="66aca-438">Выполните эти шаги tooget, которого вы начали.</span><span class="sxs-lookup"><span data-stu-id="66aca-438">Follow these steps tooget you started:</span></span>

1. <span data-ttu-id="66aca-439">Запустите hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee командлет hello доступных сред Azure:</span><span class="sxs-lookup"><span data-stu-id="66aca-439">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="66aca-440">Добавьте tooWindows учетная запись Azure China PowerShell:</span><span class="sxs-lookup"><span data-stu-id="66aca-440">Add an Azure China account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="66aca-441">Создаете контекст хранилища для учетной записи AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="66aca-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="66aca-442">toouse хранилища Azure с [США ](https://azure.microsoft.com/features/gov/)следует определить новую среду и затем создать новый контекст хранилища с данной средой:</span><span class="sxs-lookup"><span data-stu-id="66aca-442">toouse Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="66aca-443">Запустите hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee командлет hello доступных сред Azure:</span><span class="sxs-lookup"><span data-stu-id="66aca-443">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="66aca-444">Добавьте правительства США учетной записи tooWindows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="66aca-444">Add an Azure US Government account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="66aca-445">Создайте контекст хранилища для учетной записи AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="66aca-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="66aca-446">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="66aca-446">For more information, see:</span></span>

* <span data-ttu-id="66aca-447">[Руководство для разработчиков Microsoft Azure для государственных организаций](../azure-government-developer-guide.md)</span><span class="sxs-lookup"><span data-stu-id="66aca-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="66aca-448">Обзор отличий при создании приложения в службе в Китае</span><span class="sxs-lookup"><span data-stu-id="66aca-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="66aca-449">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66aca-449">Next Steps</span></span>
<span data-ttu-id="66aca-450">В этом руководстве вы узнали, каким образом toomanage хранилища Azure с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66aca-450">In this guide, you've learned how toomanage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="66aca-451">Ниже приведены некоторые связанные статьи и ресурсы для их изучения.</span><span class="sxs-lookup"><span data-stu-id="66aca-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="66aca-452">Документация по хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="66aca-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="66aca-453">Командлеты PowerShell службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="66aca-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="66aca-454">Справочник по Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="66aca-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
