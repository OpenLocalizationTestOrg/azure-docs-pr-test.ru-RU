---
title: "aaaUse hello Marketplace toolkit toocreate и публиковать элементы marketplace | Документы Microsoft"
description: "Узнайте, как создать элементы marketplace tooquickly hello публикации Toolkit"
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
ms.openlocfilehash: c1cf9ad1da44787901297eec12faf2a3dea82a6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#  <a name="add-marketplace-items-using-publishing-tool"></a><span data-ttu-id="d2e49-103">Добавить элементы marketplace, с помощью средства публикации</span><span class="sxs-lookup"><span data-stu-id="d2e49-103">Add marketplace items using publishing tool</span></span>
<span data-ttu-id="d2e49-104">Добавление к содержимого toohello [Azure Marketplace стека](azure-stack-marketplace.md) делает доступными tooyou вашего решения и клиенты для развертывания.</span><span class="sxs-lookup"><span data-stu-id="d2e49-104">Adding your content toohello [Azure Stack Marketplace](azure-stack-marketplace.md) makes your solutions available tooyou and your tenants for deployment.</span></span>  <span data-ttu-id="d2e49-105">Hello Marketplace Toolkit создает файлы пакетов Azure Marketplace (.azpkg), исходя из расширения виртуальных Машин или шаблонов диспетчера ресурсов Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="d2e49-105">hello Marketplace Toolkit creates Azure Marketplace Packages (.azpkg) files based on your IaaS Azure Resource Manager templates or VM Extensions.</span></span>  <span data-ttu-id="d2e49-106">Можно также использовать файлы .azpkg toopublish Marketplace Toolkit hello, либо созданных с помощью средства hello или с помощью [вручную](azure-stack-create-and-publish-marketplace-item.md) действия.</span><span class="sxs-lookup"><span data-stu-id="d2e49-106">You can also use hello Marketplace Toolkit toopublish .azpkg files, either created with hello tool or using [manual](azure-stack-create-and-publish-marketplace-item.md) steps.</span></span>  <span data-ttu-id="d2e49-107">В этом разделе поможет загрузке программы hello, создание marketplace элемента на основе шаблона виртуальной Машины и затем публикации toohello этого элемента стек Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d2e49-107">This topic guides you through downloading hello tool, creating a marketplace item based on a VM template, and then publishing that item toohello Azure Stack Marketplace.</span></span>     


## <a name="prerequisites"></a><span data-ttu-id="d2e49-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d2e49-108">Prerequisites</span></span>
 - <span data-ttu-id="d2e49-109">Необходимо работать на узле hello Azure стека, набор средств hello или [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) подключения hello машине, где выполняется средство hello.</span><span class="sxs-lookup"><span data-stu-id="d2e49-109">You must run hello toolkit on hello Azure Stack host or have [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) connectivity from hello machine where you run hello tool.</span></span>

 - <span data-ttu-id="d2e49-110">Загрузите hello [быстрый запуск Azure стека шаблоны](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) и извлечения.</span><span class="sxs-lookup"><span data-stu-id="d2e49-110">Download hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) and extract.</span></span>

 - <span data-ttu-id="d2e49-111">Загрузите hello [средство упаковки коллекции Azure](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span><span class="sxs-lookup"><span data-stu-id="d2e49-111">Download hello [Azure Gallery Packaging tool](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span></span> 

 - <span data-ttu-id="d2e49-112">Публикация toohello marketplace требуется значков и эскизов файла.</span><span class="sxs-lookup"><span data-stu-id="d2e49-112">Publishing toohello marketplace requires icons and a thumbnail file.</span></span>  <span data-ttu-id="d2e49-113">Можно использовать собственные или сохранить hello [пример](azure-stack-marketplace-publisher.md#support-files) файлы локально в этом примере.</span><span class="sxs-lookup"><span data-stu-id="d2e49-113">You can use your own, or save hello [sample](azure-stack-marketplace-publisher.md#support-files) files locally for this example.</span></span>

## <a name="download-hello-tool"></a><span data-ttu-id="d2e49-114">Загрузите средство hello</span><span class="sxs-lookup"><span data-stu-id="d2e49-114">Download hello tool</span></span>
<span data-ttu-id="d2e49-115">Hello Marketplace набор средств может быть [загрузить из репозитория hello Azure Tools стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="d2e49-115">hello Marketplace Toolkit can be [downloaded from hello Azure Stack Tools repo](azure-stack-powershell-download.md).</span></span>


##  <a name="create-marketplace-items"></a><span data-ttu-id="d2e49-116">Создание элементов marketplace</span><span class="sxs-lookup"><span data-stu-id="d2e49-116">Create marketplace items</span></span>
<span data-ttu-id="d2e49-117">В этом разделе используется toocreate Marketplace Toolkit hello marketplace элементов пакета в формате .azpkg.</span><span class="sxs-lookup"><span data-stu-id="d2e49-117">In this section, you use hello Marketplace Toolkit toocreate a marketplace item package in .azpkg format.</span></span>  

### <a name="provide-marketplace-information-with-wizard"></a><span data-ttu-id="d2e49-118">Укажите сведения о marketplace с помощью мастера</span><span class="sxs-lookup"><span data-stu-id="d2e49-118">Provide marketplace information with wizard</span></span>
1. <span data-ttu-id="d2e49-119">Запустите hello Marketplace Toolkit из сеанса PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d2e49-119">Run hello Marketplace Toolkit from a PowerShell session:</span></span>
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. <span data-ttu-id="d2e49-120">Нажмите кнопку hello **решения** вкладки.  Этот экран принимает сведения об элементе marketplace.</span><span class="sxs-lookup"><span data-stu-id="d2e49-120">Click hello **Solution** tab.  This screen accepts information about your marketplace item.</span></span> <span data-ttu-id="d2e49-121">Введите сведения об элементе, как он tooappear рынке hello.</span><span class="sxs-lookup"><span data-stu-id="d2e49-121">Enter information about your item as you want it tooappear in hello marketplace.</span></span>  <span data-ttu-id="d2e49-122">Можно также указать [файл параметров](azure-stack-marketplace-publisher.md#use-a-parameters-file) tooprepopulate hello формы.</span><span class="sxs-lookup"><span data-stu-id="d2e49-122">You can also specify a [parameters file](azure-stack-marketplace-publisher.md#use-a-parameters-file) tooprepopulate hello form.</span></span>  
    
    ![Снимок экрана: первый экран Marketplace Toolkit](./media/azure-stack-marketplace-publisher/image7.png)
3. <span data-ttu-id="d2e49-124">Нажмите кнопку **Обзор** и выберите файл изображения для каждого поля, значок и экрана.</span><span class="sxs-lookup"><span data-stu-id="d2e49-124">Click **Browse** and select an image file for each icon and screenshot field.</span></span>  <span data-ttu-id="d2e49-125">Можно использовать собственные значки или hello значков образец hello [файлы поддержки](azure-stack-marketplace-publisher.md#support-files) раздела.</span><span class="sxs-lookup"><span data-stu-id="d2e49-125">You can use your own icons, or hello sample icons in hello [support files](azure-stack-marketplace-publisher.md#support-files) section.</span></span>
4. <span data-ttu-id="d2e49-126">После заполнения всех полей, выберите «Предварительная версия решения» для решения hello в рамках hello Marketplace для предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="d2e49-126">Once all fields are populated, select "Preview Solution" for a preview of hello solution within hello Marketplace.</span></span>  <span data-ttu-id="d2e49-127">Проверьте и измените текст hello, изображения и экрана перед нажатием кнопки **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d2e49-127">You can revise and edit hello text, images, and screenshot before clicking **Next**.</span></span>  

### <a name="import-template-and-create-package"></a><span data-ttu-id="d2e49-128">Импорт шаблона и создания пакета</span><span class="sxs-lookup"><span data-stu-id="d2e49-128">Import template and create package</span></span>
<span data-ttu-id="d2e49-129">В этом разделе Импорт шаблона hello и работать с входными данными для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="d2e49-129">In this section, you import hello template and work with input for your solution.</span></span>

1.  <span data-ttu-id="d2e49-130">Нажмите кнопку **Обзор** и выберите hello *azuredeploy.json* из папки 101-Simple-Windows-VM hello hello загружены шаблоны.</span><span class="sxs-lookup"><span data-stu-id="d2e49-130">Click **Browse** and select hello *azuredeploy.json* from hello 101-Simple-Windows-VM folder in hello downloaded templates.</span></span>

    ![Снимок экрана второй экран Marketplace Toolkit](./media/azure-stack-marketplace-publisher/image8.png)
2.  <span data-ttu-id="d2e49-132">Hello мастер развертывания не будет заполнен *основные* шаг и входных данных элементов для каждого параметра, указанной в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="d2e49-132">hello Deployment Wizard is populated with a *Basic* step and input items for each parameter specified in hello template.</span></span>  <span data-ttu-id="d2e49-133">Можно добавить дополнительные шаги и перемещение между шагами входных данных.</span><span class="sxs-lookup"><span data-stu-id="d2e49-133">You can add additional steps and move inputs between steps.</span></span>  <span data-ttu-id="d2e49-134">В качестве примера можно привести действия «Конфигурация интерфейсный» и «Конфигурация серверной части» для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="d2e49-134">As an example, you may want "Front-End Configuration" and "Back-End Configuration" steps for your solution.</span></span>
3.  <span data-ttu-id="d2e49-135">Укажите путь tooAzureGalleryPackager.exe hello.</span><span class="sxs-lookup"><span data-stu-id="d2e49-135">Specify hello path tooAzureGalleryPackager.exe.</span></span>  
4.  <span data-ttu-id="d2e49-136">Нажмите кнопку **создать** и hello Marketplace Toolkit упаковывает решение в файл .azpkg.</span><span class="sxs-lookup"><span data-stu-id="d2e49-136">Click **Create** and hello Marketplace Toolkit packages your solution into an .azpkg file.</span></span>  <span data-ttu-id="d2e49-137">После завершения мастера hello отображает tooyour решения hello путь к файлу и предоставьте hello toocontinue параметр, публикацию вашего пакета tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="d2e49-137">Once complete, hello wizard displays hello path tooyour solution file and give you hello option toocontinue publishing your package tooAzure Stack.</span></span>


## <a name="publish-marketplace-items"></a><span data-ttu-id="d2e49-138">Публикация элементов marketplace</span><span class="sxs-lookup"><span data-stu-id="d2e49-138">Publish marketplace items</span></span>
<span data-ttu-id="d2e49-139">В этом разделе публикации tooyour элемент marketplace hello Azure Marketplace стека.</span><span class="sxs-lookup"><span data-stu-id="d2e49-139">In this section, you publish hello marketplace item tooyour Azure Stack Marketplace.</span></span>

![Снимок экрана: первый экран Marketplace Toolkit](./media/azure-stack-marketplace-publisher/image9.png)

1.  <span data-ttu-id="d2e49-141">Hello мастеру toopublish сведения о решении:</span><span class="sxs-lookup"><span data-stu-id="d2e49-141">hello wizard requires information toopublish your solution:</span></span>
    
    |<span data-ttu-id="d2e49-142">Поле</span><span class="sxs-lookup"><span data-stu-id="d2e49-142">Field</span></span>|<span data-ttu-id="d2e49-143">Описание</span><span class="sxs-lookup"><span data-stu-id="d2e49-143">Description</span></span>|
    |-----|-----|
    | <span data-ttu-id="d2e49-144">Имя администратора службы</span><span class="sxs-lookup"><span data-stu-id="d2e49-144">Service Admin Name</span></span> | <span data-ttu-id="d2e49-145">Учетная запись администратора службы.</span><span class="sxs-lookup"><span data-stu-id="d2e49-145">Service Administrator account.</span></span>  <span data-ttu-id="d2e49-146">Пример:ServiceAdmin@mydomain.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="d2e49-146">Example:  ServiceAdmin@mydomain.onmicrosoft.com</span></span> |
    | <span data-ttu-id="d2e49-147">Пароль</span><span class="sxs-lookup"><span data-stu-id="d2e49-147">Password</span></span> | <span data-ttu-id="d2e49-148">Пароль для учетной записи администратора службы.</span><span class="sxs-lookup"><span data-stu-id="d2e49-148">Password for Service Administrator account.</span></span> |
    | <span data-ttu-id="d2e49-149">Конечная точка API</span><span class="sxs-lookup"><span data-stu-id="d2e49-149">API Endpoint</span></span> | <span data-ttu-id="d2e49-150">Конечная точка Azure стека диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d2e49-150">Azure Stack Azure Resource Manager endpoint.</span></span>  <span data-ttu-id="d2e49-151">Пример: management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="d2e49-151">Example: management.local.azurestack.external</span></span> |
2.  <span data-ttu-id="d2e49-152">Нажмите кнопку **публикации** и публикации журнал hello отображается.</span><span class="sxs-lookup"><span data-stu-id="d2e49-152">Click **Publish** and hello publishing log is displayed.</span></span>
3.  <span data-ttu-id="d2e49-153">Вы — теперь может toodeploy вашей опубликованные элементы через портал Azure стека hello.</span><span class="sxs-lookup"><span data-stu-id="d2e49-153">You are now able toodeploy your published item via hello Azure Stack portal.</span></span>


## <a name="use-a-parameters-file"></a><span data-ttu-id="d2e49-154">Использовать файл параметров</span><span class="sxs-lookup"><span data-stu-id="d2e49-154">Use a parameters file</span></span>
<span data-ttu-id="d2e49-155">Также можно использовать параметры файла toocomplete hello marketplace сведения об элементе.</span><span class="sxs-lookup"><span data-stu-id="d2e49-155">You can also use a parameters file toocomplete hello marketplace item information.</span></span>  

<span data-ttu-id="d2e49-156">Hello Marketplace набор средств включает *solution.parameters.ps1* toocreate можно использовать свой собственный файл параметров.</span><span class="sxs-lookup"><span data-stu-id="d2e49-156">hello Marketplace Toolkit includes a *solution.parameters.ps1* you can use toocreate your own parameters file.</span></span>


## <a name="support-files"></a><span data-ttu-id="d2e49-157">Файлы поддержки</span><span class="sxs-lookup"><span data-stu-id="d2e49-157">Support files</span></span>
| <span data-ttu-id="d2e49-158">Описание</span><span class="sxs-lookup"><span data-stu-id="d2e49-158">Description</span></span> | <span data-ttu-id="d2e49-159">Образец</span><span class="sxs-lookup"><span data-stu-id="d2e49-159">Sample</span></span> |
| ----- | ----- |
| <span data-ttu-id="d2e49-160">значок .png 40 x 40</span><span class="sxs-lookup"><span data-stu-id="d2e49-160">40x40 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| <span data-ttu-id="d2e49-161">значок .png 90 x 90</span><span class="sxs-lookup"><span data-stu-id="d2e49-161">90x90 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| <span data-ttu-id="d2e49-162">значок .png 115 x 115</span><span class="sxs-lookup"><span data-stu-id="d2e49-162">115x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| <span data-ttu-id="d2e49-163">значок .png 255 x 115</span><span class="sxs-lookup"><span data-stu-id="d2e49-163">255x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| <span data-ttu-id="d2e49-164">эскиз .png 533 х 324</span><span class="sxs-lookup"><span data-stu-id="d2e49-164">533x324 .png thumbnail</span></span> | ![](./media/azure-stack-marketplace-publisher/image5.png) |


