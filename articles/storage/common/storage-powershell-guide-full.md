---
title: "Использование Azure PowerShell со службой хранилища Azure | Документация Майкрософт"
description: "Узнайте, как использовать командлеты Azure PowerShell для службы хранилища Azure для создания и управления учетными записями хранения; для работы с большими двоичными объектами, таблицами, очередями и файлами; для настройки и запроса аналитики хранилища, а также для создания подписанных URL-адресов"
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
ms.openlocfilehash: 87a116111d085fe2913bf6f5f8751c3ff5f3c076
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="b5d4b-103">Использование Azure PowerShell со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="b5d4b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b5d4b-104">Overview</span></span>
<span data-ttu-id="b5d4b-105">Azure PowerShell — это модуль, предоставляющий командлеты для управления Azure с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-105">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="b5d4b-106">Это оболочка командной строки на основе задач и язык сценариев, разработанные для администрирования системы.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="b5d4b-107">С помощью PowerShell можно легко контролировать и автоматизировать администрирование служб и приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-107">With PowerShell, you can easily control and automate the administration of your Azure services and applications.</span></span> <span data-ttu-id="b5d4b-108">Например, с помощью командлетов можно выполнять те же задачи, которые доступны на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-108">For example, you can use the cmdlets to perform the same tasks that you can perform through the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="b5d4b-109">В этом руководстве вы узнаете, как использовать [командлеты службы хранилища Azure](/powershell/module/azurerm.storage/#storage) для выполнения различных задач, связанных с разработкой и администрированием, в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-109">In this guide, we'll explore how to use the [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) to perform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="b5d4b-110">Предполагается, что у вас есть опыт работы со [службой хранилища Azure](https://azure.microsoft.com/documentation/services/storage/) и [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="b5d4b-111">Руководство предоставляет несколько сценариев для демонстрации использования PowerShell с службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-111">The guide provides a number of scripts to demonstrate the usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="b5d4b-112">Перед выполнением каждого сценария необходимо обновить переменные сценария в зависимости от конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-112">You should update the script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="b5d4b-113">В первом разделе этого руководства содержится краткий обзор службы хранилища Azure и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-113">The first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="b5d4b-114">Для получения подробных сведений и инструкций начните с раздела [Предварительные требования для использования Azure PowerShell со службой хранилища Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-114">For detailed information and instructions, start from the [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="b5d4b-115">Приступая к работе со службой хранилища Azure и PowerShell в течение 5 минут</span><span class="sxs-lookup"><span data-stu-id="b5d4b-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="b5d4b-116">В этом разделе показано, как получить доступ к хранилищу Azure через PowerShell в течение 5 минут.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-116">This section shows you how to access Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="b5d4b-117">**Впервые используете Azure?** Получите подписку на Microsoft Azure и связанную с ней учетную запись Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="b5d4b-118">Сведения о способах приобретения Azure см. на страницах [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/), [Как приобрести Azure](https://azure.microsoft.com/pricing/purchase-options/) и [Предложения для участников](https://azure.microsoft.com/pricing/member-offers/) (для подписчиков MSDN, участников Microsoft Partner Network, BizSpark и других наших программ).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="b5d4b-119">Дополнительные сведения о подписках Azure см. на странице [Назначение ролей администратора в Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="b5d4b-120">**После создания подписки Microsoft Azure и учетной записи:**</span><span class="sxs-lookup"><span data-stu-id="b5d4b-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="b5d4b-121">[Скачайте и установите последнюю версию Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-121">Download and install the latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="b5d4b-122">Запустите интегрированную среду сценариев (ISE) Windows PowerShell. Для этого на локальном компьютере перейдите в меню **Пуск**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go to the **Start** menu.</span></span> <span data-ttu-id="b5d4b-123">Введите **Администрирование** и щелкните, чтобы запустить оснастку.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-123">Type **Administrative Tools** and click to run it.</span></span> <span data-ttu-id="b5d4b-124">В окне **Администрирование** щелкните правой кнопкой мыши **Windows PowerShell ISE** и выберите **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-124">In the **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="b5d4b-125">В окне **Windows PowerShell ISE** щелкните **Файл** > **Создать**, чтобы создать новый файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-125">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="b5d4b-126">Теперь мы предоставим вам простой сценарий, который показывает основные команды PowerShell для доступа к службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-126">Now, we'll give you a simple script that shows basic PowerShell commands to access Azure Storage.</span></span> <span data-ttu-id="b5d4b-127">Сначала сценарий запросит учетные данные учетной записи Azure для ее добавления в локальной среде PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-127">The script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment.</span></span> <span data-ttu-id="b5d4b-128">Затем сценарий установит подписку Azure по умолчанию и создаст новую учетную запись хранения в Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-128">Then, the script will set the default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="b5d4b-129">Затем сценарий создает новый контейнер в этой новой учетной записи хранения и передает существующий файл образа (BLOB) в этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-129">Next, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="b5d4b-130">После этого сценарий выводит список всех BLOB-объектов в этом контейнере, создает новый каталог назначения на локальном компьютере и загружает файл образа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-130">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>
5. <span data-ttu-id="b5d4b-131">В приведенном ниже разделе кода выберите скрипт между комментариями **#begin** и **#end**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-131">In the following code section, select the script between the remarks **#begin** and **#end**.</span></span> <span data-ttu-id="b5d4b-132">Нажмите клавиши CTRL+C, чтобы скопировать его в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-132">Press CTRL+C to copy it to the clipboard.</span></span>

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
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
       
    # Download blobs from the container:
    # Get a reference to a list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create the destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into the local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="b5d4b-133">В окне **Интегрированная среда сценариев Windows PowerShell**нажмите сочетание клавиш CTRL+V, чтобы вставить сценарий.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-133">In **Windows PowerShell ISE**, press CTRL+V to copy the script.</span></span> <span data-ttu-id="b5d4b-134">Щелкните **Файл** > **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-134">Click **File** > **Save**.</span></span> <span data-ttu-id="b5d4b-135">В диалоговом окне **Сохранить как** введите имя файла сценария, например "mystoragescript".</span><span class="sxs-lookup"><span data-stu-id="b5d4b-135">In the **Save As** dialog window, type the name of the script file, such as "mystoragescript."</span></span> <span data-ttu-id="b5d4b-136">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-136">Click **Save**.</span></span>
7. <span data-ttu-id="b5d4b-137">Теперь необходимо обновить переменные сценария на основе заданных параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-137">Now, you need to update the script variables based on your configuration settings.</span></span> <span data-ttu-id="b5d4b-138">Необходимо обновить переменную **$SubscriptionName** данными собственной подписки.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-138">You must update the **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="b5d4b-139">Можно сохранить значения других переменных, как указано в сценарии или обновлять их по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-139">You can keep the other variables as specified in the script or update them as you wish.</span></span>
   
   * <span data-ttu-id="b5d4b-140">Необходимо обновить переменную **$SubscriptionName**, используя данные собственной подписки.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="b5d4b-141">Ниже представлены три способа найти название вашей подписки. Можно воспользоваться любым из них.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-141">Follow one of the following three ways to locate the name of your subscription:</span></span>
     
    <span data-ttu-id="b5d4b-142">а.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-142">a.</span></span> <span data-ttu-id="b5d4b-143">В окне **Windows PowerShell ISE** щелкните **Файл** > **Создать**, чтобы создать новый файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-143">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span> <span data-ttu-id="b5d4b-144">Скопируйте следующий скрипт в новый файл и выберите **Отладка** > **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-144">Copy the following script to the new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="b5d4b-145">Следующий сценарий сначала запросит учетные данные учетной записи Azure для добавления в учетной записи Azure в локальную среду PowerShell, и отобразит все подписки, которые подключены к локальному сеансу PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-145">The following script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment and then show all the subscriptions that are connected to the local PowerShell session.</span></span> <span data-ttu-id="b5d4b-146">Запишите имя подписки, которая будет использоваться при выполнении этого учебника:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-146">Take a note of the name of the subscription that you want to use while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="b5d4b-147">b.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-147">b.</span></span> <span data-ttu-id="b5d4b-148">Чтобы найти и скопировать имя подписки на [портале Azure](https://portal.azure.com), в расположенном слева главном меню щелкните элемент **Подписки**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-148">To locate and copy your subscription name in the [Azure portal](https://portal.azure.com), in the Hub menu on the left, click **Subscriptions**.</span></span> <span data-ttu-id="b5d4b-149">Скопируйте имя подписки, которая будет использоваться при выполнении сценариев в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-149">Copy the name of subscription that you want to use while running the scripts in this guide.</span></span>
     
     ![Портал Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="b5d4b-151">c.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-151">c.</span></span> <span data-ttu-id="b5d4b-152">Чтобы найти и скопировать имя подписки на [классическом портале Azure](https://manage.windowsazure.com/), выполните прокрутку вниз и выберите элемент **Параметры** в левой части портала.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-152">To locate and copy your subscription name in the [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on the left side of the portal.</span></span> <span data-ttu-id="b5d4b-153">Щелкните элемент **Подписки** для просмотра списка подписок.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-153">Click **Subscriptions** to see a list of your subscriptions.</span></span> <span data-ttu-id="b5d4b-154">Скопируйте имя подписки, которая будет использоваться при выполнении сценариев, указанных в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-154">Copy the name of subscription that you want to use while running the scripts given in this guide.</span></span>
     
     ![классическом портале Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="b5d4b-156">**$StorageAccountName**: используйте заданное имя в скрипте или введите новое имя для вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-156">**$StorageAccountName:** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="b5d4b-157">**Важно!** Имя учетной записи хранения в Azure должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-157">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="b5d4b-158">и состоять из символов нижнего регистра.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="b5d4b-159">**$Location**: используйте заданное в скрипте значение West US или выберите другое расположение Azure, например East US, North Europe и т. д.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-159">**$Location:** Use the given "West US" in the script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="b5d4b-160">**$ContainerName** : используйте заданное в сценарии имя или введите новое имя для своего контейнера.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-160">**$ContainerName:** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="b5d4b-161">**$ImageToUpload**: введите путь к изображению на локальном компьютере (например, C:\Images\HelloWorld.png).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-161">**$ImageToUpload:** Enter a path to a picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="b5d4b-162">**$DestinationFolder**: введите путь к локальному каталогу для хранения файлов, скачанных из службы хранилища Azure (например, C:\DownloadImages).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-162">**$DestinationFolder:** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="b5d4b-163">После обновления переменных скриптов в файле mystoragescript.ps1 щелкните **Файл** > **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-163">After updating the script variables in the "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="b5d4b-164">Для выполнения скрипта щелкните **Отладка** > **Выполнить** или нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-164">Then, click **Debug** > **Run** or press **F5** to run the script.</span></span>  

<span data-ttu-id="b5d4b-165">После выполнения сценария появится локальная целевая папка, которая содержит загруженный файл образа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-165">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="b5d4b-166">На следующем снимке экрана показан пример вывода:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-166">The following screenshot shows an example output:</span></span>

![Загрузка BLOB-объектов](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="b5d4b-168">В разделе «Приступая к работе со службой хранилища Azure и PowerShell в течение 5 минут» предоставляется краткое введение по использованию Azure PowerShell со службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-168">The "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how to use Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="b5d4b-169">С подробными сведениями и инструкциями мы рекомендуем вам ознакомиться в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-169">For detailed information and instructions, we encourage you to read the following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="b5d4b-170">Предварительные требования для использования Azure PowerShell со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="b5d4b-171">Требуется подписка Azure и учетная запись для запуска командлетов PowerShell, приведенных в этом руководстве, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-171">You need an Azure subscription and account to run the PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="b5d4b-172">Azure PowerShell — это модуль, предоставляющий командлеты для управления Azure с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-172">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="b5d4b-173">Сведения об установке и настройке Azure PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-173">For information on installing and setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="b5d4b-174">Рекомендуется загрузить и установить (или обновить до последней версии) модуль Azure PowerShell перед использованием в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-174">We recommend that you download and install or upgrade to the latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="b5d4b-175">Вы можете запустить командлеты на стандартной консоли Windows PowerShell или в интегрированной среде сценариев Windows PowerShell (ISE).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-175">You can run the cmdlets in the standard Windows PowerShell console or the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="b5d4b-176">Например, чтобы открыть среду **Windows PowerShell ISE**, перейдите в меню "Пуск", введите "Администрирование" и щелкните, чтобы запустить оснастку.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-176">For example, to open **Windows PowerShell ISE**, go to the Start menu, type Administrative Tools and click to run it.</span></span> <span data-ttu-id="b5d4b-177">В окне «Администрирование» щелкните правой кнопкой мыши Windows PowerShell ISE и выберите «Запуск от имени администратора».</span><span class="sxs-lookup"><span data-stu-id="b5d4b-177">In the Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-to-manage-storage-accounts-in-azure"></a><span data-ttu-id="b5d4b-178">Управление учетными записями хранения в Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-178">How to manage storage accounts in Azure</span></span>

<span data-ttu-id="b5d4b-179">Давайте рассмотрим процесс управления учетными записями хранения в Azure с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-to-set-a-default-azure-subscription"></a><span data-ttu-id="b5d4b-180">Как задать значение по умолчанию для подписки Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-180">How to set a default Azure subscription</span></span>
<span data-ttu-id="b5d4b-181">Для управления службой хранилища Azure с помощью Azure PowerShell необходимо выполнить проверку подлинности в клиентской среде с помощью проверки подлинности Azure Active Directory или проверки подлинности на основе сертификатов.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-181">To manage Azure Storage using Azure PowerShell, you need to authenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="b5d4b-182">Подробные сведения см. в руководстве [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-182">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="b5d4b-183">В этом руководстве используется проверка подлинности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-183">This guide uses the Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="b5d4b-184">В интегрированной среде сценариев Azure PowerShell введите следующую команду, чтобы добавить учетную запись Azure в локальную среду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-184">In Windows PowerShell ISE, type the following command to add your Azure account to the local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="b5d4b-185">В окне "Вход в Microsoft Azure" введите адрес электронной почты и пароль, связанные с вашей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-185">In the "Sign in to Microsoft Azure" window, type the email address and password associated with your account.</span></span> <span data-ttu-id="b5d4b-186">Azure выполняет проверку подлинности и сохраняет учетные данные, а затем закрывает окно.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-186">Azure authenticates and saves the credential information, and then closes the window.</span></span>

3. <span data-ttu-id="b5d4b-187">Затем выполните следующую команду, чтобы просмотреть учетные записи Azure в локальной среде PowerShell и убедитесь, что ваша учетная запись имеется в списке:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-187">Next, run the following command to view the Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="b5d4b-188">Затем выполните следующий командлет, чтобы просмотреть все подписки, которые подключены к локальному сеансу PowerShell и убедитесь, что подписка есть в списке:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-188">Then, run the following cmdlet to view all the subscriptions that are connected to the local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="b5d4b-189">Чтобы задать подписку Azure по умолчанию, выполните командлет Select-AzureSubscription.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-189">To set a default Azure subscription, run the Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="b5d4b-190">Проверьте имя подписки по умолчанию, выполнив командлет Get-AzureSubscription:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-190">Verify the name of the default subscription by running the Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="b5d4b-191">Чтобы просмотреть все доступные командлеты PowerShell для службы хранилища Azure, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-191">To see all the available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a><span data-ttu-id="b5d4b-192">Создание новой учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-192">How to create a new Azure storage account</span></span>
<span data-ttu-id="b5d4b-193">Для использования службы хранилища Azure потребуется учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-193">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="b5d4b-194">После настройки компьютера для подключения к подписке можно создать новую учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-194">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

1. <span data-ttu-id="b5d4b-195">Выполните командлет Get-AzureLocation, чтобы найти все доступные расположения:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-195">Run the Get-AzureLocation cmdlet to find all the available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="b5d4b-196">Затем выполните командлет New-AzureStorageAccount для создания новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-196">Next, run the New-AzureStorageAccount cmdlet to create a new storage account.</span></span> <span data-ttu-id="b5d4b-197">Этот пример создает новую учетную запись хранения в центре обработки данных «Запад США».</span><span class="sxs-lookup"><span data-stu-id="b5d4b-197">The following example creates a new storage account in the "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="b5d4b-198">Имя для учетной записи хранения является уникальным в пределах Azure и должно содержать только строчные буквы.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-198">The name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="b5d4b-199">Соглашения об именовании и ограничениях см. в статьях [Об учетных записях хранения Azure](../storage-create-storage-account.md) и [Именование контейнеров, больших двоичных объектов, метаданных и ссылка на них](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-199">For naming conventions and restrictions, see [About Azure Storage Accounts](../storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a><span data-ttu-id="b5d4b-200">Как задать учетную запись хранения Azure по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b5d4b-200">How to set a default Azure storage account</span></span>
<span data-ttu-id="b5d4b-201">В подписке может иметься несколько учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="b5d4b-202">Можно выбрать одну из них и установить ее в качестве учетной записи хранения по умолчанию для всех команд хранилища в одном сеансе PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-202">You can choose one of them and set it as the default storage account for all the storage commands in the same PowerShell session.</span></span> <span data-ttu-id="b5d4b-203">Это позволяет выполнять команды службы хранилища Azure PowerShell без явного указания контекста хранилища.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-203">This enables you to run the Azure PowerShell storage commands without specifying the storage context explicitly.</span></span>

1. <span data-ttu-id="b5d4b-204">Чтобы задать учетную запись по умолчанию для подписки, можно запустить командлет Set-AzureSubscription.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-204">To set a default storage account for your subscription, you can run the Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="b5d4b-205">Затем выполните командлет Get-AzureSubscription и убедитесь, что учетная запись хранения связана с вашей учетной записью в подписке по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-205">Next, run the Get-AzureSubscription cmdlet to verify that the storage account is associated with your default subscription account.</span></span> <span data-ttu-id="b5d4b-206">Эта команда возвращает свойства подписки для текущей подписки, включая ее текущую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-206">This command returns the subscription properties on the current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="b5d4b-207">Получение списка всех учетных записей хранения Azure в подписке</span><span class="sxs-lookup"><span data-stu-id="b5d4b-207">How to list all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="b5d4b-208">Каждая подписка Azure может включать до 100 учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-208">Each Azure subscription can have up to 100 storage accounts.</span></span> <span data-ttu-id="b5d4b-209">Актуальные сведения об ограничениях см. в статье [Подписка Azure, границы, квоты и ограничения службы](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-209">For the most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="b5d4b-210">Выполните следующий командлет, чтобы узнать имена и состояние учетных записей хранения в текущей подписке.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-210">Run the following cmdlet to find out the name and status of the storage accounts in the current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a><span data-ttu-id="b5d4b-211">Создание контекста службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-211">How to create an Azure storage context</span></span>
<span data-ttu-id="b5d4b-212">Контекст службы хранилища Azure — это объект в PowerShell для инкапсуляции учетных данных хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-212">Azure storage context is an object in PowerShell to encapsulate the storage credentials.</span></span> <span data-ttu-id="b5d4b-213">Использование контекста хранилища при запуске любого последующего командлета позволяет проводить проверку подлинности запроса без явного указания учетной записи хранения и ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-213">Using a storage context while running any subsequent cmdlet enables you to authenticate your request without specifying the storage account and its access key explicitly.</span></span> <span data-ttu-id="b5d4b-214">Контекст хранилища можно создать несколькими способами, например с помощью имени и ключа доступа учетной записи хранения, токена подписи общего доступа, строки подключения или анонимно.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="b5d4b-215">Дополнительные сведения см. в описании [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="b5d4b-216">Используйте один из следующих трех способов создания контекста хранилища:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-216">Use one of the following three ways to create a storage context:</span></span>

* <span data-ttu-id="b5d4b-217">Запустите командлет [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) , чтобы найти основной ключ доступа к хранилищу для вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-217">Run the [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet to find out the primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="b5d4b-218">Затем вызовите командлет [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) для создания контекста хранилища:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-218">Next, call the [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet to create a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="b5d4b-219">Создайте токен подписи общего доступа для контейнера службы хранилища Azure и используйте его для создания контекста хранилища:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-219">Generate a shared access signature token for an Azure storage container and use it to create a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="b5d4b-220">Дополнительные сведения см. в статьях [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) и [Использование подписанных URL-адресов (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="b5d4b-221">В некоторых случаях может потребоваться указать конечные точки службы при создании нового контекста хранилища.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-221">In some cases, you may want to specify the service endpoints when you create a new storage context.</span></span> <span data-ttu-id="b5d4b-222">Это может потребоваться при регистрации имени пользовательского домена для учетной записи службы BLOB-объектов или использовании подписанного URL-адреса для доступа к ресурсам хранилища.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-222">This might be necessary when you have registered a custom domain name for your storage account with the Blob service or you want to use a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="b5d4b-223">Установите конечные точки службы в строке соединения и используйте ее для создания нового контекста хранилища, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-223">Set the service endpoints in a connection string and use it to create a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="b5d4b-224">Дополнительные сведения о том, как настроить строку подключения хранилища, см. [здесь](../storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-224">For more information on how to configure a storage connection string, see [Configuring Connection Strings](../storage-configure-connection-string.md).</span></span>

<span data-ttu-id="b5d4b-225">Вы настроили компьютер и узнали, как управлять подписками и учетными записями хранения с помощью Azure PowerShell. Теперь переходите к следующему разделу, чтобы научиться управлять BLOB-объектами и моментальными снимками BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-225">Now that you have set up your computer and learned how to manage subscriptions and storage accounts using Azure PowerShell, go to the next section to learn how to manage Azure blobs and blob snapshots.</span></span>

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="b5d4b-226">Получение и повторное создание ключей к хранилищу данных Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-226">How to retrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="b5d4b-227">Учетная запись хранилища Azure предоставляется с двумя ключами учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="b5d4b-228">Для получения ключей можно использовать следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-228">You can use the following cmdlet to retrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="b5d4b-229">Для получения конкретного ключа используйте следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-229">Use the following cmdlet to retrieve a specific key.</span></span> <span data-ttu-id="b5d4b-230">Допустимые значения: Primary и Secondary</span><span class="sxs-lookup"><span data-stu-id="b5d4b-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="b5d4b-231">Для повторного создания ключей используйте следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-231">If you would like to regenerate your keys, use the following cmdlet.</span></span> <span data-ttu-id="b5d4b-232">Допустимые значения параметра -KeyType: Primary и Secondary</span><span class="sxs-lookup"><span data-stu-id="b5d4b-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a><span data-ttu-id="b5d4b-233">Управление BLOB-объектами Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-233">How to manage Azure blobs</span></span>
<span data-ttu-id="b5d4b-234">Хранилище BLOB-объектов Azure — это служба хранения большого количества неструктурированных данных, таких как текстовые или бинарные файлы, к которым можно получить доступ практически из любой точки мира по протоколу HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="b5d4b-235">В этом разделе предполагается, что вы уже знакомы с понятиями службы хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-235">This section assumes that you are already familiar with the Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="b5d4b-236">Дополнительные сведения см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../blobs/storage-dotnet-how-to-use-blobs.md) и [Понятия службы BLOB-объектов](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-236">For detailed information, see [Get started with Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-to-create-a-container"></a><span data-ttu-id="b5d4b-237">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="b5d4b-237">How to create a container</span></span>
<span data-ttu-id="b5d4b-238">Каждый BLOB-объект в хранилище Azure должен находиться в контейнере.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="b5d4b-239">Можно создать закрытый контейнер, используя командлет New-AzureStorageContainer:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-239">You can create a private container using the New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="b5d4b-240">Существует три уровня анонимного доступа для чтения: **Отключено**, **Большой двоичный объект** и **Контейнер**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="b5d4b-241">Чтобы запретить анонимный доступ к большому двоичному объекту, присвойте параметру разрешение **Отключено**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-241">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="b5d4b-242">По умолчанию новый контейнер является закрытым, доступ к нему может осуществляться только владельцем учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-242">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="b5d4b-243">Чтобы разрешить анонимный общий доступ на чтение к ресурсам больших двоичных объектов, но не к метаданным контейнера или списку больших двоичных объектов в контейнере, присвойте параметру разрешение **Большой двоичный объект**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-243">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="b5d4b-244">Чтобы разрешить полный общий доступ на чтение к ресурсам больших двоичных объектов, метаданным контейнера и списку больших двоичных объектов в контейнере, присвойте параметру разрешение **Контейнер**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-244">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="b5d4b-245">Дополнительные сведения см. в статье [Управление анонимным доступом на чтение к контейнерам и большим двоичным объектам](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-245">For more information, see [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="b5d4b-246">Передача BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="b5d4b-246">How to upload a blob into a container</span></span>
<span data-ttu-id="b5d4b-247">Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="b5d4b-248">Дополнительные сведения см. в статье [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx) (Основные сведения о блочных, добавочных и страничных BLOB-объектах).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="b5d4b-249">Можно использовать командлет [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) , чтобы загрузить большие двоичные объекты в контейнер.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-249">To upload blobs in to a container, you can use the [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="b5d4b-250">По умолчанию эта команда отправляет локальные файлы в BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-250">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="b5d4b-251">Чтобы указать тип BLOB-объекта можно использовать параметр -BlobType.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-251">To specify the type for the blob, you can use the -BlobType parameter.</span></span>

<span data-ttu-id="b5d4b-252">В следующем примере выполняется [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) для получения всех файлов в указанной папке и передачи их в следующий командлет с помощью оператора конвейера.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-252">The following example runs the [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet to get all the files in the specified folder, and then passes them to the next cmdlet by using the pipeline operator.</span></span> <span data-ttu-id="b5d4b-253">Командлет [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) загружает локальные файлы в контейнер:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-253">The [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads the local files to your container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a><span data-ttu-id="b5d4b-254">Скачивание BLOB-объектов из контейнера</span><span class="sxs-lookup"><span data-stu-id="b5d4b-254">How to download blobs from a container</span></span>
<span data-ttu-id="b5d4b-255">Следующий пример демонстрирует загрузку BLOB-объектов из контейнера.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-255">The following example demonstrates how to download blobs from a container.</span></span> <span data-ttu-id="b5d4b-256">Сначала пример устанавливает соединение со службой хранилища Azure, используя контекст учетной записи хранения, который включает имя учетной записи хранения и ее первичный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-256">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its primary access key.</span></span> <span data-ttu-id="b5d4b-257">Затем в примере извлекается ссылка на большой двоичный объект с помощью командлета [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) .</span><span class="sxs-lookup"><span data-stu-id="b5d4b-257">Then, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="b5d4b-258">Затем в примере используется командлет [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) , чтобы скачать большие двоичные объекты в локальную целевую папку.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-258">Next, the example uses the [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet to download blobs into the local destination folder.</span></span>

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a><span data-ttu-id="b5d4b-259">Копирование BLOB-объектов из одного контейнера хранилища в другой</span><span class="sxs-lookup"><span data-stu-id="b5d4b-259">How to copy blobs from one storage container to another</span></span>
<span data-ttu-id="b5d4b-260">Можно асинхронно копировать BLOB-объекты между учетными записями хранения и областями.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="b5d4b-261">Следующий пример демонстрирует копирование BLOB-объектов из одного контейнера хранилища в другой в двух разных учетных записях хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-261">The following example demonstrates how to copy blobs from one storage container to another in two different storage accounts.</span></span> <span data-ttu-id="b5d4b-262">В примере сначала задаются переменные источника и назначения учетных записей хранения и затем создается контекст хранилища для каждой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-262">The example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="b5d4b-263">Далее в примере копируются большие двоичные объекты из контейнера-источника в целевой контейнер с помощью командлета [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) .</span><span class="sxs-lookup"><span data-stu-id="b5d4b-263">Next, the example copies blobs from the source container to the destination container using the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="b5d4b-264">В примере предполагается, что учетные записи хранения и контейнеры источника и назначения уже существуют.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-264">The example assumes that the source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="b5d4b-265">Обратите внимание, что этот пример выполняет асинхронное копирование.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="b5d4b-266">Отслеживать состояние каждой копии можно, запустив командлет [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) .</span><span class="sxs-lookup"><span data-stu-id="b5d4b-266">You can monitor the status of each copy by running the [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-to-copy-blobs-from-a-secondary-location"></a><span data-ttu-id="b5d4b-267">Копирование больших двоичных объектов из дополнительного расположения</span><span class="sxs-lookup"><span data-stu-id="b5d4b-267">How to copy blobs from a secondary location</span></span>
<span data-ttu-id="b5d4b-268">Большие двоичные объекты можно копировать из дополнительного расположения учетной записи с поддержкой RA-GRS.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-268">You can copy blobs from the secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a><span data-ttu-id="b5d4b-269">Удаление BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="b5d4b-269">How to delete a blob</span></span>
<span data-ttu-id="b5d4b-270">Чтобы удалить BLOB-объект, сначала нужно получить ссылку на него, а затем вызвать командлет Remove-AzureStorageBlob с этой ссылкой.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-270">To delete a blob, first get a blob reference and then call the Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="b5d4b-271">Следующий пример удаляет все BLOB-объекты в данном контейнере.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-271">The following example deletes all the blobs in a given container.</span></span> <span data-ttu-id="b5d4b-272">В примере сначала устанавливаются переменные для учетной записи хранения, затем создается контекст хранилища.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-272">The example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="b5d4b-273">Далее в примере извлекается ссылка на большой двоичный объект с помощью командлета [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) и выполняется командлет [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob), чтобы удалить большие двоичные объекты из контейнера в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-273">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet to remove blobs from a container in Azure storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a><span data-ttu-id="b5d4b-274">Управление моментальными снимками BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-274">How to manage Azure blob snapshots</span></span>
<span data-ttu-id="b5d4b-275">Azure позволяет создать моментальный снимок BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="b5d4b-276">Моментальный снимок — это версия BLOB-объекта только для чтения, сделанная в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="b5d4b-277">После создания моментального снимка его можно читать, копировать или удалять, но нельзя изменять.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="b5d4b-278">Моментальные снимки обеспечивают способ резервного копирования BLOB-объекта в том виде, в котором он находится в данный момент времени.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-278">Snapshots provide a way to back up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="b5d4b-279">Дополнительные сведения см. в статье [Создание моментального снимка большого двоичного объекта](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-to-create-a-blob-snapshot"></a><span data-ttu-id="b5d4b-280">Создание моментального снимка BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="b5d4b-280">How to create a blob snapshot</span></span>
<span data-ttu-id="b5d4b-281">Для создания моментального снимка большого двоичного объекта сначала нужно получить ссылку на него, а затем вызвать метод `ICloudBlob.CreateSnapshot` для этой ссылки.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-281">To create a snaphot of a blob, first get a blob reference and then call the `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="b5d4b-282">В следующем примере сначала устанавливаются переменные для учетной записи хранения и затем создается контекст хранилища.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-282">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="b5d4b-283">Далее в примере извлекается ссылка на большой двоичный объект с помощью командлета [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) и выполняется метод [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) для создания моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-283">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a><span data-ttu-id="b5d4b-284">Получение списка моментальных снимков больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="b5d4b-284">How to list a blob's snapshots</span></span>
<span data-ttu-id="b5d4b-285">Можно создать любое количество моментальных снимков для BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="b5d4b-286">Можно вывести список моментальных снимков, связанных с BLOB-объектом, для отслеживания текущих моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-286">You can list the snapshots associated with your blob to track your current snapshots.</span></span> <span data-ttu-id="b5d4b-287">В следующем примере используется стандартный большой двоичный объект и вызывается командлет [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) для вывода списка моментальных снимков этого объекта.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-287">The following example uses a predefined blob and calls the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet to list the snapshots of that blob.</span></span>  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a><span data-ttu-id="b5d4b-288">Копирование моментального снимка BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="b5d4b-288">How to copy a snapshot of a blob</span></span>
<span data-ttu-id="b5d4b-289">Для восстановления моментального снимка BLOB-объекта можно скопировать моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-289">You can copy a snapshot of a blob to restore the snapshot.</span></span> <span data-ttu-id="b5d4b-290">Подробные сведения и ограничения см. в статье [Создание моментального снимка большого двоичного объекта](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="b5d4b-291">В следующем примере сначала устанавливаются переменные для учетной записи хранения и затем создается контекст хранилища.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-291">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="b5d4b-292">Далее в примере определяются переменные имен контейнера и BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-292">Next, the example defines the container and blob name variables.</span></span> <span data-ttu-id="b5d4b-293">В примере извлекается ссылка на большой двоичный объект с помощью командлета [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) и выполняется метод [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) для создания моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-293">The example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span> <span data-ttu-id="b5d4b-294">Затем в примере выполняется командлет [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) для копирования моментального снимка большого двоичного объекта. При этом в качестве исходного большого двоичного объекта используется объект ICloudBlob.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-294">Then, the example runs the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet to copy the snapshot of a blob using the ICloudBlob object for the source blob.</span></span> <span data-ttu-id="b5d4b-295">Не забудьте обновить переменные в зависимости от конфигурации до запуска примера.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-295">Be sure to update the variables based on your configuration before running the example.</span></span> <span data-ttu-id="b5d4b-296">Обратите внимание, что в следующем примере предполагается, что контейнеры источника и назначения и BLOB-объект источника уже существуют.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-296">Note that the following example assumes that the source and destination containers, and the source blob already exist.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="b5d4b-297">Вы узнали, как управлять BLOB-объектами и моментальными снимками BLOB-объектов Azure с помощью Azure PowerShell. Теперь переходите к следующему разделу, чтобы научиться управлять таблицами, очередями и файлами.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-297">Now that you have learned how to manage Azure blobs and blob snapshots with Azure PowerShell, go to the next section to learn how to manage tables, queues, and files.</span></span>

## <a name="how-to-manage-azure-tables-and-table-entities"></a><span data-ttu-id="b5d4b-298">Управление таблицами и сущности таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-298">How to manage Azure tables and table entities</span></span>
<span data-ttu-id="b5d4b-299">Служба хранилища таблиц Azure — хранилище данных NoSQL, которое можно использовать для хранения и запросов огромных наборов структурированных нереляционных данных.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-299">Azure Table storage service is a NoSQL datastore, which you can use to store and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="b5d4b-300">Основными компонентами службы являются таблицы, сущности и свойства.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-300">The main components of the service are tables, entities, and properties.</span></span> <span data-ttu-id="b5d4b-301">Таблица представляет собой коллекцию сущностей.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-301">A table is a collection of entities.</span></span> <span data-ttu-id="b5d4b-302">Сущность — это набор свойств.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-302">An entity is a set of properties.</span></span> <span data-ttu-id="b5d4b-303">Каждая сущность может иметь до 252 свойств. Все они являются парами "имя — значение".</span><span class="sxs-lookup"><span data-stu-id="b5d4b-303">Each entity can have up to 252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="b5d4b-304">В этом разделе предполагается, что вы уже знакомы с понятиями хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-304">This section assumes that you are already familiar with the Azure Table Storage Service concepts.</span></span> <span data-ttu-id="b5d4b-305">Дополнительные сведения см. в статьях [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) (Общие сведения о модели данных службы таблиц) и [Приступая к работе с хранилищем таблиц Azure с помощью .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-305">For detailed information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span>

<span data-ttu-id="b5d4b-306">В следующих подразделах рассматривается управление службой хранилища таблиц Azure с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-306">In the following subsections, you'll learn how to manage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="b5d4b-307">Сценарии включают **создание**, **удаление** и **извлечение** **таблиц**, а также **добавление**, **запрос** и **удаление объектов таблиц**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-307">The scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-to-create-a-table"></a><span data-ttu-id="b5d4b-308">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="b5d4b-308">How to create a table</span></span>
<span data-ttu-id="b5d4b-309">Каждая таблица должна находиться в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="b5d4b-310">Следующий пример демонстрирует создание таблицы в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-310">The following example demonstrates how to create a table in Azure Storage.</span></span> <span data-ttu-id="b5d4b-311">Сначала в примере устанавливается соединение со службой хранилища Azure, используя контекст учетной записи хранения, который включает имя учетной записи хранения и ее ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-311">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="b5d4b-312">Затем используется командлет [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) , чтобы создать таблицу в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-312">Next, it uses the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet to create a table in Azure Storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a><span data-ttu-id="b5d4b-313">Получение таблицы</span><span class="sxs-lookup"><span data-stu-id="b5d4b-313">How to retrieve a table</span></span>
<span data-ttu-id="b5d4b-314">Можно запрашивать и получить одну или все таблицы в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="b5d4b-315">Следующий пример демонстрирует извлечение указанной таблицы с помощью командлета [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="b5d4b-315">The following example demonstrates how to retrieve a given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="b5d4b-316">При вызове командлета Get-AzureStorageTable без параметров он получает все таблицы хранилища для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-316">If you call the Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-to-delete-a-table"></a><span data-ttu-id="b5d4b-317">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="b5d4b-317">How to delete a table</span></span>
<span data-ttu-id="b5d4b-318">Можно удалить таблицу из учетной записи хранения с помощью командлета [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="b5d4b-318">You can delete a table from a storage account by using the [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a><span data-ttu-id="b5d4b-319">Управление сущностями таблицы</span><span class="sxs-lookup"><span data-stu-id="b5d4b-319">How to manage table entities</span></span>
<span data-ttu-id="b5d4b-320">В настоящее время Azure PowerShell предоставляет командлеты для непосредственного управления сущностями таблицы.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-320">Currently, Azure PowerShell does not provide cmdlets to manage table entities directly.</span></span> <span data-ttu-id="b5d4b-321">Для выполнения операций над сущностями в таблице можно использовать классы в [клиентской библиотеке службы хранилища Azure для .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-321">To perform operations on table entities, you can use the classes given in the [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-to-add-table-entities"></a><span data-ttu-id="b5d4b-322">Добавление сущностей таблицы</span><span class="sxs-lookup"><span data-stu-id="b5d4b-322">How to add table entities</span></span>
<span data-ttu-id="b5d4b-323">Чтобы добавить сущность в таблицу, необходимо сначала создать объект, который определяет свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-323">To add an entity to a table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="b5d4b-324">Сущность может иметь до 255 свойств, включая 3 системных свойства: **PartitionKey**, **RowKey** и **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-324">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="b5d4b-325">Вы отвечаете за вставку и обновление значений **PartitionKey** и **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-325">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="b5d4b-326">Сервер управляет значением **Timestamp**, которое не может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-326">The server manages the value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="b5d4b-327">Вместе **PartitionKey** и **RowKey** однозначно идентифицируют каждую сущность в пределах таблицы.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-327">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="b5d4b-328">**PartitionKey**— определяет раздел, в котором хранится сущность.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-328">**PartitionKey**: Determines the partition that the entity is stored in.</span></span>
* <span data-ttu-id="b5d4b-329">**RowKey**— уникально определяет сущность в разделе.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-329">**RowKey**: Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="b5d4b-330">Можно определить до 252 свойств для сущности.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-330">You may define up to 252 custom properties for an entity.</span></span> <span data-ttu-id="b5d4b-331">Дополнительные сведения см. в статье [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) (Общие сведения о модели данных службы таблиц).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-331">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="b5d4b-332">Следующий пример демонстрирует добавление сущности в таблицу.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-332">The following example demonstrates how to add entities to a table.</span></span> <span data-ttu-id="b5d4b-333">В примере показано получение таблицы «employee» и добавление в нее нескольких сущностей.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-333">The example shows how to retrieve the employee table and add several entities into it.</span></span> <span data-ttu-id="b5d4b-334">Во-первых, устанавливается соединение со службой хранилища Azure с помощью контекста учетной записи хранения, который включает имя учетной записи хранения и ее ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-334">First, it establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="b5d4b-335">Затем заданная таблица извлекается с помощью командлета [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="b5d4b-335">Next, it retrieves the given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="b5d4b-336">Если таблица не существует, то используется командлет [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) для создания таблицы в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-336">If the table does not exist, the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used to create a table in Azure Storage.</span></span> <span data-ttu-id="b5d4b-337">Далее в примере определяется пользовательская функция Add-Entity для добавления сущностей в таблицу путем указания раздела и ключа строки каждой сущности.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-337">Next, the example defines a custom function Add-Entity to add entities to the table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="b5d4b-338">Функция Add-Entity вызывает командлет [New-Object](http://technet.microsoft.com/library/hh849885.aspx) с классом [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) для создания объекта сущности.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-338">The Add-Entity function calls the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class to create an entity object.</span></span> <span data-ttu-id="b5d4b-339">Позже в примере вызывается метод [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) этого объекта сущности для добавления в таблицу.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-339">Later, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object to add it to a table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity to a table.
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

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a><span data-ttu-id="b5d4b-340">Запрос сущностей таблицы</span><span class="sxs-lookup"><span data-stu-id="b5d4b-340">How to query table entities</span></span>
<span data-ttu-id="b5d4b-341">Для запроса к таблице используется класс [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-341">To query a table, use the [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="b5d4b-342">В следующем примере предполагается, что уже был запущен сценарий, приведенный в разделе о добавлении раздела сущностей данного руководства.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-342">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="b5d4b-343">Сначала пример устанавливает соединение со службой хранилища Azure, используя контекст хранилища, который включает имя учетной записи хранения и ее ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-343">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="b5d4b-344">Затем предпринимается попытка получить ранее созданную таблицу "Employees" с помощью командлета [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-344">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="b5d4b-345">Вызов [New-Object](http://technet.microsoft.com/library/hh849885.aspx) в классе Microsoft.WindowsAzure.Storage.Table.TableQuery создает новый объект запроса.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-345">Calling the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="b5d4b-346">В примере выполняется поиск сущностей, которые содержат столбец "ID", значение которого равно 1, как указано в фильтре строк.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-346">The example looks for the entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="b5d4b-347">Дополнительные сведения см. в статье [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx) (Запросы к таблицам и сущностям).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="b5d4b-348">При выполнении этого запроса он возвращает все сущности, которые соответствуют условиям фильтра.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-348">When you run this query, it returns all entities that match the filter criteria.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a><span data-ttu-id="b5d4b-349">Удаление сущностей таблицы</span><span class="sxs-lookup"><span data-stu-id="b5d4b-349">How to delete table entities</span></span>
<span data-ttu-id="b5d4b-350">Сущность можно удалить с помощью ее ключей раздела и строки.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="b5d4b-351">В следующем примере предполагается, что уже был запущен сценарий, приведенный в разделе о добавлении раздела сущностей данного руководства.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-351">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="b5d4b-352">Сначала пример устанавливает соединение со службой хранилища Azure, используя контекст хранилища, который включает имя учетной записи хранения и ее ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-352">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="b5d4b-353">Затем предпринимается попытка получить ранее созданную таблицу "Employees" с помощью командлета [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-353">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="b5d4b-354">Если таблица существует, в примере вызывается метод [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) для получения сущности, основываясь на значениях ключа раздела и строки.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-354">If the table exists, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method to retrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="b5d4b-355">Затем передайте сущность в метод [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) для удаления.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-355">Then, pass the entity to the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method to delete.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a><span data-ttu-id="b5d4b-356">Управление очередями Azure и очередями сообщений</span><span class="sxs-lookup"><span data-stu-id="b5d4b-356">How to manage Azure queues and queue messages</span></span>
<span data-ttu-id="b5d4b-357">Хранилище очередей Azure — это служба для хранения большого количества сообщений, к которым можно получить доступ практически из любой точки мира с помощью вызовов с проверкой подлинности по протоколам HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="b5d4b-358">В этом разделе предполагается, что вы уже знакомы с понятиями службы хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-358">This section assumes that you are already familiar with the Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="b5d4b-359">Дополнительные сведения см. в статье [Приступая к работе с хранилищем очередей Azure с помощью .NET](../storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-359">For detailed information, see [Get started with Azure Queue storage using .NET](../storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="b5d4b-360">В этом разделе показано, как управлять службой хранилища очередей Azure с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-360">This section will show you how to manage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="b5d4b-361">Сценарии использования включают **вставку** и **удаление** сообщений очереди, а также **создание**, **удаление** и **получение очередей**.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-361">The scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-to-create-a-queue"></a><span data-ttu-id="b5d4b-362">Как создать очередь</span><span class="sxs-lookup"><span data-stu-id="b5d4b-362">How to create a queue</span></span>
<span data-ttu-id="b5d4b-363">Сначала в этом примере устанавливается соединение со службой хранилища Azure, используя контекст учетной записи хранения, который включает имя учетной записи хранения и ее ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-363">The following example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="b5d4b-364">Затем вызывается командлет [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue), чтобы создать очередь с именем "queuename".</span><span class="sxs-lookup"><span data-stu-id="b5d4b-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet to create a queue named 'queuename'.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="b5d4b-365">Сведения о соглашениях об именовании для службы очередей Azure см. в статье [Именование очередей и метаданных](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-to-retrieve-a-queue"></a><span data-ttu-id="b5d4b-366">Получение очереди</span><span class="sxs-lookup"><span data-stu-id="b5d4b-366">How to retrieve a queue</span></span>
<span data-ttu-id="b5d4b-367">Можно запрашивать и получать указанную очередь или список всех очередей в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-367">You can query and retrieve a specific queue or a list of all the queues in a Storage account.</span></span> <span data-ttu-id="b5d4b-368">Следующий пример демонстрирует извлечение указанной очереди с помощью командлета [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) .</span><span class="sxs-lookup"><span data-stu-id="b5d4b-368">The following example demonstrates how to retrieve a specified queue using the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="b5d4b-369">При вызове командлета [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) без параметров возвращается список всех очередей.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-369">If you call the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all the queues.</span></span>

### <a name="how-to-delete-a-queue"></a><span data-ttu-id="b5d4b-370">Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="b5d4b-370">How to delete a queue</span></span>
<span data-ttu-id="b5d4b-371">Для удаления очереди и всех сообщений, содержащихся в ней, вызовите командлет Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-371">To delete a queue and all the messages contained in it, call the Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="b5d4b-372">В следующем примере показан способ удаления указанной очереди, используя командлет Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-372">The following example shows how to delete a specified queue using the Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="b5d4b-373">Вставка сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="b5d4b-373">How to insert a message into a queue</span></span>
<span data-ttu-id="b5d4b-374">Чтобы вставить сообщение в существующую очередь, сначала необходимо создать новый экземпляр класса [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b5d4b-374">To insert a message into an existing queue, first create a new instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="b5d4b-375">Затем вызовите метод [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b5d4b-375">Next, call the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="b5d4b-376">Для создания CloudQueueMessage можно использовать строку (в формате UTF-8) или массив байтов.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="b5d4b-377">Следующий пример демонстрирует добавление сообщений в очередь.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-377">The following example demonstrates how to add message to a queue.</span></span> <span data-ttu-id="b5d4b-378">Сначала в примере устанавливается соединение со службой хранилища Azure, используя контекст учетной записи хранения, который включает имя учетной записи хранения и ее ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-378">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="b5d4b-379">Затем извлекается указанная очередь с помощью командлета [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b5d4b-379">Next, it retrieves the specified queue using the [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="b5d4b-380">Если очередь существует, командлет [New-Object](http://technet.microsoft.com/library/hh849885.aspx) используется для создания экземпляра класса [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-380">If the queue exists, the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used to create an instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="b5d4b-381">Позже в примере вызывается метод [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) для этого объекта сообщения, чтобы добавить его в очередь.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-381">Later, the example calls the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object to add it to a queue.</span></span> <span data-ttu-id="b5d4b-382">Ниже приведен код, который извлекает очередь и вставляет сообщение "MessageInfo".</span><span class="sxs-lookup"><span data-stu-id="b5d4b-382">Here is code which retrieves a queue and inserts the message 'MessageInfo':</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a><span data-ttu-id="b5d4b-383">Удаление следующего сообщения из очереди</span><span class="sxs-lookup"><span data-stu-id="b5d4b-383">How to de-queue at the next message</span></span>
<span data-ttu-id="b5d4b-384">Код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="b5d4b-385">При вызове метода [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) вы получаете следующее сообщение в очереди.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-385">When you call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get the next message in a queue.</span></span> <span data-ttu-id="b5d4b-386">Сообщение, возвращаемое методом **GetMessage** , становится невидимым для другого кода, считывающего сообщения из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-386">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="b5d4b-387">Чтобы завершить удаление сообщения из очереди, необходимо вызвать метод [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b5d4b-387">To finish removing the message from the queue, you must also call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="b5d4b-388">Этот двухэтапный процесс удаления сообщения позволяет удостовериться, что если коду не удастся обработать сообщение из-за сбоя оборудования или программного обеспечения, другой экземпляр кода сможет получить то же сообщение и повторить попытку.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-388">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="b5d4b-389">Код вызывает метод **DeleteMessage** сразу после обработки сообщения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-389">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a><span data-ttu-id="b5d4b-390">Управление общими папками и файлами Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-390">How to manage Azure file shares and files</span></span>
<span data-ttu-id="b5d4b-391">Хранилище файлов Azure предоставляет общее хранилище для приложений с помощью стандартного протокола SMB.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-391">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="b5d4b-392">Виртуальные машины Microsoft Azure и облачные службы могут совместно использовать файл данных между компонентами приложения через подключенные общие ресурсы, локальные приложения могут обращаться к данным файлов в общей папке через API хранилища файлов или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via the File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="b5d4b-393">Подробнее о хранилище файлов Azure см. в статьях [Приступая к работе с хранилищем файлов Azure в Windows](../storage-dotnet-how-to-use-files.md) и [API REST службы файлов](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-to-set-and-query-storage-analytics"></a><span data-ttu-id="b5d4b-394">Установка и запросы к аналитике хранилища</span><span class="sxs-lookup"><span data-stu-id="b5d4b-394">How to set and query storage analytics</span></span>
<span data-ttu-id="b5d4b-395">Можно воспользоваться [аналитикой службы хранилища Azure](../storage-analytics.md) для сбора метрик из учетных записей хранения Azure и ведения журналов с данными о запросах, отправленных в вашу учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-395">You can use [Azure Storage Analytics](../storage-analytics.md) to collect metrics for your Azure storage accounts and log data about requests sent to your storage account.</span></span> <span data-ttu-id="b5d4b-396">Метрики хранилища можно использовать для наблюдения за работоспособностью учетной записи хранения и ведения журнала хранилища для диагностики и устранения проблем, связанных с вашей учетной записью хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-396">You can use storage metrics to monitor the health of a storage account, and storage logging to diagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="b5d4b-397">Вы можете настроить мониторинг с помощью портала Azure или Windows PowerShell или программно, с помощью клиентской библиотеки хранилища.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-397">You can configure monitoring using the Azure portal or Windows PowerShell, or programmatically using the storage client library.</span></span> <span data-ttu-id="b5d4b-398">Ведение журналов хранилища производится на стороне сервера и позволяет записывать сведения об успешных и неудачных запросах в вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-398">Storage logging happens server-side and enables you to record details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="b5d4b-399">Эти журналы позволяют просмотреть подробные сведения об операциях чтения, записи и удаления для таблиц, очередей и BLOB-объектов, а также причины неудачных запросов.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-399">These logs enable you to see details of read, write, and delete operations against your tables, queues, and blobs as well as the reasons for failed requests.</span></span>

<span data-ttu-id="b5d4b-400">Сведения о том, как включить и просмотреть метрики хранилища данных с помощью PowerShell, представлены в статье [Включение метрик хранилища с помощью PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-400">To learn how to enable and view Storage Metrics data using PowerShell, see [How to enable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="b5d4b-401">Сведения о том, как включить и получить журнал хранилища данных с помощью PowerShell, см. в статьях [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) (Включение ведения журнала хранилища с помощью PowerShell) и [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata) (Поиск данных журнала хранилища).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-401">To learn how to enable and retrieve Storage Logging data using PowerShell, see [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="b5d4b-402">Подробнее об использовании метрик хранилища и ведения журнала для устранения неполадок хранилища см. в статье [Мониторинг, диагностика и устранение неполадок службы хранилища Microsoft Azure](../storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-402">For detailed information on using Storage Metrics and Storage Logging to troubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="b5d4b-403">Как управлять подписанными URL-адресами (SAS) и хранимыми политиками доступа</span><span class="sxs-lookup"><span data-stu-id="b5d4b-403">How to manage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="b5d4b-404">Подписанные URL-адреса являются важной частью модели обеспечения безопасности для любого приложения, использующего хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-404">Shared access signatures are an important part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="b5d4b-405">Их удобно применять в целях предоставления ограниченных разрешений для вашей учетной записи хранения тем клиентам, которые нельзя передавать ключ учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-405">They are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="b5d4b-406">По умолчанию только владелец учетной записи хранения может обращаться к большим двоичным объектам, таблицам и очередям в пределах этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-406">By default, only the owner of the storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="b5d4b-407">Если вашей службе или приложению нужно сделать эти ресурсы доступными другим клиентам без совместного использования ключа доступа, вы можете воспользоваться следующими тремя вариантами:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-407">If your service or application needs to make these resources available to other clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="b5d4b-408">Задайте такие разрешения контейнера, которые предоставляют анонимный доступ для чтения контейнера и его больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-408">Set a container's permissions to permit anonymous read access to the container and its blobs.</span></span> <span data-ttu-id="b5d4b-409">Такие разрешения нельзя задать для таблиц и очередей.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="b5d4b-410">Используйте подписанный URL-адрес, обеспечивающий ограниченные права доступа к контейнерам, большим двоичным объектам, очередям и таблицам в заданный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-410">Use a shared access signature that grants restricted access rights to containers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="b5d4b-411">Используйте хранимую политику доступа, чтобы получить дополнительный уровень контроля над подписанными URL-адресами для контейнера, его больших двоичных объектов, очереди или таблицы.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-411">Use a stored access policy to obtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="b5d4b-412">С помощью хранимой политики доступа можно изменить время начала, срок действия и разрешения для подписи, а также отозвать подпись после ее выдачи.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-412">The stored access policy allows you to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.</span></span>

<span data-ttu-id="b5d4b-413">Подписанный URL-адрес может быть в одной из двух следующих форм.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="b5d4b-414">**Нерегламентированная SAS:**при создании нерегламентированной SAS время начала, время окончания срока действия и разрешения для SAS указываются в универсальном коде ресурса (URI) SAS.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-414">**Ad hoc SAS**: When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span> <span data-ttu-id="b5d4b-415">Этот тип подписанного URL-адреса можно создать для контейнера, большого двоичного объекта, таблицы или очереди, и его невозможно отозвать.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="b5d4b-416">**SAS с хранимой политикой доступа:** хранимая политика доступа определяется в контейнере ресурсов, контейнере больших двоичных объектов, таблице или очереди. Ее можно использовать для управления ограничениями одного или нескольких подписанных URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="b5d4b-417">При сопоставлении подписи общего доступа с хранимой политикой доступа эта подпись наследует ограничения (время начала, время окончания и разрешения), определенные для данной хранимой политики доступа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-417">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span> <span data-ttu-id="b5d4b-418">Подписанный URL-адрес этого типа можно отозвать.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="b5d4b-419">Дополнительные сведения см. в статьях [Использование подписанных URL-адресов (SAS)](../storage-dotnet-shared-access-signature-part-1.md) и [Управление анонимным доступом на чтение к контейнерам и большим двоичным объектам](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-419">For more information, see [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="b5d4b-420">В следующих разделах вы узнаете, как создать маркер подписанного URL-адреса и хранимую политику доступа для таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-420">In the next sections, you will learn how to create a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="b5d4b-421">Azure PowerShell предоставляет одинаковые командлеты для контейнеров, больших двоичных объектов и очередей.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="b5d4b-422">Для выполнения сценариев в этом разделе скачайте [Azure PowerShell версии 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) или более поздней.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-422">To run the scripts in this section, download the [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="b5d4b-423">Как создать маркер подписанного URL-адреса на основе политики</span><span class="sxs-lookup"><span data-stu-id="b5d4b-423">How to create a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="b5d4b-424">Используйте командлет New-AzureStorageTableStoredAccessPolicy для создания новой хранимой политики доступа.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-424">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy.</span></span> <span data-ttu-id="b5d4b-425">Затем вызовите командлет [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) , чтобы создать новый токен подписанного URL-адреса на основе политики для таблицы службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-425">Then, call the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="b5d4b-426">Как создать маркер однорангового (неотзываемого) подписанного URL-адреса</span><span class="sxs-lookup"><span data-stu-id="b5d4b-426">How to create an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="b5d4b-427">Воспользуйтесь командлетом [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken), чтобы создать новый специализированный (неотзываемый) маркер подписанного URL-адреса для таблицы службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-427">Use the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a><span data-ttu-id="b5d4b-428">Как создать хранимую политику доступа</span><span class="sxs-lookup"><span data-stu-id="b5d4b-428">How to create a stored access policy</span></span>
<span data-ttu-id="b5d4b-429">Используйте командлет New-AzureStorageTableStoredAccessPolicy для создания новой хранимой политики доступа для таблицы хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-429">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a><span data-ttu-id="b5d4b-430">Как обновить хранимую политику доступа</span><span class="sxs-lookup"><span data-stu-id="b5d4b-430">How to update a stored access policy</span></span>
<span data-ttu-id="b5d4b-431">Используйте командлет Set-AzureStorageTableStoredAccessPolicy для обновления существующей хранимой политики доступа для таблицы хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-431">Use the Set-AzureStorageTableStoredAccessPolicy cmdlet to update an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a><span data-ttu-id="b5d4b-432">Как удалить хранимую политику доступа</span><span class="sxs-lookup"><span data-stu-id="b5d4b-432">How to delete a stored access policy</span></span>
<span data-ttu-id="b5d4b-433">Используйте командлет Remove-AzureStorageTableStoredAccessPolicy для удаления хранимой политики доступа в таблице хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-433">Use the Remove-AzureStorageTableStoredAccessPolicy cmdlet to delete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="b5d4b-434">Использование службы хранилища Azure для правительства США и Azure в Китае</span><span class="sxs-lookup"><span data-stu-id="b5d4b-434">How to use Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="b5d4b-435">Среда Azure — это независимое развертывание Microsoft Azure, такое как [Azure для государственных организаций в правительстве США](https://azure.microsoft.com/features/gov/), [AzureCloud для глобального Azure](https://portal.azure.com) и [AzureChinaCloud для Azure под управлением 21Vianet в Китае](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="b5d4b-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="b5d4b-436">Можно выполнить развертывание новых сред Azure для правительства США и Китая.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="b5d4b-437">Для использования службы хранилища Azure с AzureChinaCloud необходимо создать контекст хранилища, связанный с AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-437">To use Azure Storage with AzureChinaCloud, you need to create a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="b5d4b-438">Выполните следующие действия, чтобы приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-438">Follow these steps to get you started:</span></span>

1. <span data-ttu-id="b5d4b-439">Запустите командлет [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) , чтобы просмотреть доступные среды Azure:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-439">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="b5d4b-440">Добавьте учетную запись Azure Китай в Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-440">Add an Azure China account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="b5d4b-441">Создаете контекст хранилища для учетной записи AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="b5d4b-442">Для использования службы хранилища Azure с [Azure для правительства США ](https://azure.microsoft.com/features/gov/)следует определить новую среду и затем создать новый контекст хранилища с данной средой:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-442">To use Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="b5d4b-443">Запустите командлет [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) , чтобы просмотреть доступные среды Azure:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-443">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="b5d4b-444">Добавьте учетную запись Azure для правительства США (AzureUSGovernment) в Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-444">Add an Azure US Government account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="b5d4b-445">Создайте контекст хранилища для учетной записи AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="b5d4b-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="b5d4b-446">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="b5d4b-446">For more information, see:</span></span>

* <span data-ttu-id="b5d4b-447">[Руководство для разработчиков Microsoft Azure для государственных организаций](../../azure-government/documentation-government-developer-guide.md)</span><span class="sxs-lookup"><span data-stu-id="b5d4b-447">[Microsoft Azure Government Developer Guide](../../azure-government/documentation-government-developer-guide.md).</span></span>
* [<span data-ttu-id="b5d4b-448">Обзор отличий при создании приложения в службе в Китае</span><span class="sxs-lookup"><span data-stu-id="b5d4b-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="b5d4b-449">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5d4b-449">Next Steps</span></span>
<span data-ttu-id="b5d4b-450">В этом руководстве вы узнали, как управлять службой хранилища Azure с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-450">In this guide, you've learned how to manage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="b5d4b-451">Ниже приведены некоторые связанные статьи и ресурсы для их изучения.</span><span class="sxs-lookup"><span data-stu-id="b5d4b-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="b5d4b-452">Документация по хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="b5d4b-453">Командлеты PowerShell службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="b5d4b-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="b5d4b-454">Справочник по Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5d4b-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
