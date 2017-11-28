---
title: "Используйте набор средств Marketplace создавать и публиковать элементы marketplace | Документы Microsoft"
description: "Узнайте, как быстро создать элементы marketplace с публикацией Toolkit"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: ByronR
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/14/2017
ms.author: helaw
ms.openlocfilehash: 5b2c04d2cbc06e1572dc2e40712f6cf9d886aa1e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
#  <a name="add-marketplace-items-using-publishing-tool"></a><span data-ttu-id="4d785-103">Добавить элементы marketplace, с помощью средства публикации</span><span class="sxs-lookup"><span data-stu-id="4d785-103">Add marketplace items using publishing tool</span></span>
<span data-ttu-id="4d785-104">Добавление содержимого к [Azure Marketplace стека](azure-stack-marketplace.md) доступны для вас и ваших клиентов для развертывания решения.</span><span class="sxs-lookup"><span data-stu-id="4d785-104">Adding your content to the [Azure Stack Marketplace](azure-stack-marketplace.md) makes your solutions available to you and your tenants for deployment.</span></span>  <span data-ttu-id="4d785-105">Набор средств Marketplace создает файлы пакетов Azure Marketplace (.azpkg), исходя из расширения виртуальных Машин или шаблонов диспетчера ресурсов Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="4d785-105">The Marketplace Toolkit creates Azure Marketplace Packages (.azpkg) files based on your IaaS Azure Resource Manager templates or VM Extensions.</span></span>  <span data-ttu-id="4d785-106">Marketplace Toolkit также можно использовать для публикации .azpkg файлы, созданные с помощью программы или с помощью [вручную](azure-stack-create-and-publish-marketplace-item.md) действия.</span><span class="sxs-lookup"><span data-stu-id="4d785-106">You can also use the Marketplace Toolkit to publish .azpkg files, either created with the tool or using [manual](azure-stack-create-and-publish-marketplace-item.md) steps.</span></span>  <span data-ttu-id="4d785-107">В этом разделе поможет загрузить средство, создание marketplace элемента на основе шаблона виртуальной Машины и затем публикации этого элемента стек в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4d785-107">This topic guides you through downloading the tool, creating a marketplace item based on a VM template, and then publishing that item to the Azure Stack Marketplace.</span></span>     


## <a name="prerequisites"></a><span data-ttu-id="4d785-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4d785-108">Prerequisites</span></span>
 - <span data-ttu-id="4d785-109">Необходимо выполнить набор средств на узле стек Azure или иметь [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) подключения на машине, где запускается средство.</span><span class="sxs-lookup"><span data-stu-id="4d785-109">You must run the toolkit on the Azure Stack host or have [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) connectivity from the machine where you run the tool.</span></span>

 - <span data-ttu-id="4d785-110">Загрузить [быстрый запуск Azure стека шаблоны](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) и извлечения.</span><span class="sxs-lookup"><span data-stu-id="4d785-110">Download the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) and extract.</span></span>

 - <span data-ttu-id="4d785-111">Загрузить [средство упаковки коллекции Azure](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span><span class="sxs-lookup"><span data-stu-id="4d785-111">Download the [Azure Gallery Packaging tool](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span></span> 

 - <span data-ttu-id="4d785-112">Публикации в Marketplace необходимо значков и эскизов файла.</span><span class="sxs-lookup"><span data-stu-id="4d785-112">Publishing to the marketplace requires icons and a thumbnail file.</span></span>  <span data-ttu-id="4d785-113">Можно использовать собственные или сохранить [пример](azure-stack-marketplace-publisher.md#support-files) файлы локально в этом примере.</span><span class="sxs-lookup"><span data-stu-id="4d785-113">You can use your own, or save the [sample](azure-stack-marketplace-publisher.md#support-files) files locally for this example.</span></span>

## <a name="download-the-tool"></a><span data-ttu-id="4d785-114">Загрузите средство</span><span class="sxs-lookup"><span data-stu-id="4d785-114">Download the tool</span></span>
<span data-ttu-id="4d785-115">Может быть Marketplace Toolkit [загружаются из репозитория средства Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="4d785-115">The Marketplace Toolkit can be [downloaded from the Azure Stack Tools repo](azure-stack-powershell-download.md).</span></span>


##  <a name="create-marketplace-items"></a><span data-ttu-id="4d785-116">Создание элементов marketplace</span><span class="sxs-lookup"><span data-stu-id="4d785-116">Create marketplace items</span></span>
<span data-ttu-id="4d785-117">В этом разделе использовать Marketplace набор средств для создания пакета элементов marketplace в формате .azpkg.</span><span class="sxs-lookup"><span data-stu-id="4d785-117">In this section, you use the Marketplace Toolkit to create a marketplace item package in .azpkg format.</span></span>  

### <a name="provide-marketplace-information-with-wizard"></a><span data-ttu-id="4d785-118">Укажите сведения о marketplace с помощью мастера</span><span class="sxs-lookup"><span data-stu-id="4d785-118">Provide marketplace information with wizard</span></span>
1. <span data-ttu-id="4d785-119">Запустите Marketplace Toolkit из сеанса PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4d785-119">Run the Marketplace Toolkit from a PowerShell session:</span></span>
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. <span data-ttu-id="4d785-120">Нажмите кнопку **решения** вкладки.  Этот экран принимает сведения об элементе marketplace.</span><span class="sxs-lookup"><span data-stu-id="4d785-120">Click the **Solution** tab.  This screen accepts information about your marketplace item.</span></span> <span data-ttu-id="4d785-121">Введите сведения об элементе, как он отображается на рынке.</span><span class="sxs-lookup"><span data-stu-id="4d785-121">Enter information about your item as you want it to appear in the marketplace.</span></span>  <span data-ttu-id="4d785-122">Можно также указать [файл параметров](azure-stack-marketplace-publisher.md#use-a-parameters-file) нужно заполнить форму.</span><span class="sxs-lookup"><span data-stu-id="4d785-122">You can also specify a [parameters file](azure-stack-marketplace-publisher.md#use-a-parameters-file) to prepopulate the form.</span></span>  
    
    ![Снимок экрана: первый экран Marketplace Toolkit](./media/azure-stack-marketplace-publisher/image7.png)
3. <span data-ttu-id="4d785-124">Нажмите кнопку **Обзор** и выберите файл изображения для каждого поля, значок и экрана.</span><span class="sxs-lookup"><span data-stu-id="4d785-124">Click **Browse** and select an image file for each icon and screenshot field.</span></span>  <span data-ttu-id="4d785-125">Можно использовать собственные значки или значки в образце [файлы поддержки](azure-stack-marketplace-publisher.md#support-files) раздела.</span><span class="sxs-lookup"><span data-stu-id="4d785-125">You can use your own icons, or the sample icons in the [support files](azure-stack-marketplace-publisher.md#support-files) section.</span></span>
4. <span data-ttu-id="4d785-126">После заполнения всех полей, выберите «Предварительная версия решения» для предварительного просмотра этого решения в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4d785-126">Once all fields are populated, select "Preview Solution" for a preview of the solution within the Marketplace.</span></span>  <span data-ttu-id="4d785-127">Проверьте и измените текст, изображения и экрана перед нажатием кнопки **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4d785-127">You can revise and edit the text, images, and screenshot before clicking **Next**.</span></span>  

### <a name="import-template-and-create-package"></a><span data-ttu-id="4d785-128">Импорт шаблона и создания пакета</span><span class="sxs-lookup"><span data-stu-id="4d785-128">Import template and create package</span></span>
<span data-ttu-id="4d785-129">В этом разделе импортировать шаблон и работать с входными данными для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="4d785-129">In this section, you import the template and work with input for your solution.</span></span>

1.  <span data-ttu-id="4d785-130">Нажмите кнопку **Обзор** и выберите *azuredeploy.json* из папки 101-Simple-Windows-VM в загруженный шаблон.</span><span class="sxs-lookup"><span data-stu-id="4d785-130">Click **Browse** and select the *azuredeploy.json* from the 101-Simple-Windows-VM folder in the downloaded templates.</span></span>

    ![Снимок экрана второй экран Marketplace Toolkit](./media/azure-stack-marketplace-publisher/image8.png)
2.  <span data-ttu-id="4d785-132">Мастер развертывания не будет заполнен *основные* шаг и входных данных элементов для каждого параметра, указанного в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="4d785-132">The Deployment Wizard is populated with a *Basic* step and input items for each parameter specified in the template.</span></span>  <span data-ttu-id="4d785-133">Можно добавить дополнительные шаги и перемещение между шагами входных данных.</span><span class="sxs-lookup"><span data-stu-id="4d785-133">You can add additional steps and move inputs between steps.</span></span>  <span data-ttu-id="4d785-134">В качестве примера можно привести действия «Конфигурация интерфейсный» и «Конфигурация серверной части» для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="4d785-134">As an example, you may want "Front-End Configuration" and "Back-End Configuration" steps for your solution.</span></span>
3.  <span data-ttu-id="4d785-135">Укажите путь к AzureGalleryPackager.exe.</span><span class="sxs-lookup"><span data-stu-id="4d785-135">Specify the path to AzureGalleryPackager.exe.</span></span>  
4.  <span data-ttu-id="4d785-136">Нажмите кнопку **создать** и Marketplace Toolkit упаковывает решение в файл .azpkg.</span><span class="sxs-lookup"><span data-stu-id="4d785-136">Click **Create** and the Marketplace Toolkit packages your solution into an .azpkg file.</span></span>  <span data-ttu-id="4d785-137">После завершения мастера отображает путь к файлу решения и дают возможность продолжить публикацию пакета стек Azure.</span><span class="sxs-lookup"><span data-stu-id="4d785-137">Once complete, the wizard displays the path to your solution file and give you the option to continue publishing your package to Azure Stack.</span></span>


## <a name="publish-marketplace-items"></a><span data-ttu-id="4d785-138">Публикация элементов marketplace</span><span class="sxs-lookup"><span data-stu-id="4d785-138">Publish marketplace items</span></span>
<span data-ttu-id="4d785-139">В этом разделе вы опубликовать элемент marketplace стека в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4d785-139">In this section, you publish the marketplace item to your Azure Stack Marketplace.</span></span>

![Снимок экрана: первый экран Marketplace Toolkit](./media/azure-stack-marketplace-publisher/image9.png)

1.  <span data-ttu-id="4d785-141">Мастеру необходимы сведения для публикации решения:</span><span class="sxs-lookup"><span data-stu-id="4d785-141">The wizard requires information to publish your solution:</span></span>
    
    |<span data-ttu-id="4d785-142">Поле</span><span class="sxs-lookup"><span data-stu-id="4d785-142">Field</span></span>|<span data-ttu-id="4d785-143">Описание</span><span class="sxs-lookup"><span data-stu-id="4d785-143">Description</span></span>|
    |-----|-----|
    | <span data-ttu-id="4d785-144">Имя администратора службы</span><span class="sxs-lookup"><span data-stu-id="4d785-144">Service Admin Name</span></span> | <span data-ttu-id="4d785-145">Учетная запись администратора службы.</span><span class="sxs-lookup"><span data-stu-id="4d785-145">Service Administrator account.</span></span>  <span data-ttu-id="4d785-146">Пример:ServiceAdmin@mydomain.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="4d785-146">Example:  ServiceAdmin@mydomain.onmicrosoft.com</span></span> |
    | <span data-ttu-id="4d785-147">Пароль</span><span class="sxs-lookup"><span data-stu-id="4d785-147">Password</span></span> | <span data-ttu-id="4d785-148">Пароль для учетной записи администратора службы.</span><span class="sxs-lookup"><span data-stu-id="4d785-148">Password for Service Administrator account.</span></span> |
    | <span data-ttu-id="4d785-149">Конечная точка API</span><span class="sxs-lookup"><span data-stu-id="4d785-149">API Endpoint</span></span> | <span data-ttu-id="4d785-150">Конечная точка Azure стека диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="4d785-150">Azure Stack Azure Resource Manager endpoint.</span></span>  <span data-ttu-id="4d785-151">Пример: management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="4d785-151">Example: management.local.azurestack.external</span></span> |
2.  <span data-ttu-id="4d785-152">Нажмите кнопку **публикации** и отображается журнал публикации.</span><span class="sxs-lookup"><span data-stu-id="4d785-152">Click **Publish** and the publishing log is displayed.</span></span>
3.  <span data-ttu-id="4d785-153">Теперь имеется возможность развернуть опубликованный элемент через портал Azure стека.</span><span class="sxs-lookup"><span data-stu-id="4d785-153">You are now able to deploy your published item via the Azure Stack portal.</span></span>


## <a name="use-a-parameters-file"></a><span data-ttu-id="4d785-154">Использовать файл параметров</span><span class="sxs-lookup"><span data-stu-id="4d785-154">Use a parameters file</span></span>
<span data-ttu-id="4d785-155">Также можно использовать файл параметров для выполнения сведения об элементе marketplace.</span><span class="sxs-lookup"><span data-stu-id="4d785-155">You can also use a parameters file to complete the marketplace item information.</span></span>  

<span data-ttu-id="4d785-156">Включает набор средств Marketplace *solution.parameters.ps1* можно использовать для создания файлов параметров.</span><span class="sxs-lookup"><span data-stu-id="4d785-156">The Marketplace Toolkit includes a *solution.parameters.ps1* you can use to create your own parameters file.</span></span>


## <a name="support-files"></a><span data-ttu-id="4d785-157">Файлы поддержки</span><span class="sxs-lookup"><span data-stu-id="4d785-157">Support files</span></span>
| <span data-ttu-id="4d785-158">Описание</span><span class="sxs-lookup"><span data-stu-id="4d785-158">Description</span></span> | <span data-ttu-id="4d785-159">Образец</span><span class="sxs-lookup"><span data-stu-id="4d785-159">Sample</span></span> |
| ----- | ----- |
| <span data-ttu-id="4d785-160">значок .png 40 x 40</span><span class="sxs-lookup"><span data-stu-id="4d785-160">40x40 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| <span data-ttu-id="4d785-161">значок .png 90 x 90</span><span class="sxs-lookup"><span data-stu-id="4d785-161">90x90 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| <span data-ttu-id="4d785-162">значок .png 115 x 115</span><span class="sxs-lookup"><span data-stu-id="4d785-162">115x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| <span data-ttu-id="4d785-163">значок .png 255 x 115</span><span class="sxs-lookup"><span data-stu-id="4d785-163">255x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| <span data-ttu-id="4d785-164">эскиз .png 533 х 324</span><span class="sxs-lookup"><span data-stu-id="4d785-164">533x324 .png thumbnail</span></span> | ![](./media/azure-stack-marketplace-publisher/image5.png) |


