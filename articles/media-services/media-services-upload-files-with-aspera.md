---
title: "Отправка файлов в учетную запись служб мультимедиа Azure с помощью Aspera | Документация Майкрософт"
description: "Этот учебник поможет выполнить необходимые действия по передаче файлов в учетную запись хранилища, связанный с учетной записью служб мультимедиа с помощью ** Aspera Server по запросу ** службы в Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: e3090da9b2c5b8f99545a1f7f9601bfd8d5221f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-the-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="d3473-103">Отправка файлов в учетную запись служб мультимедиа с помощью службы Aspera Server On Demand в Azure</span><span class="sxs-lookup"><span data-stu-id="d3473-103">Upload files into a Media Services account using the Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="d3473-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d3473-104">Overview</span></span>

<span data-ttu-id="d3473-105">**Aspera** — это программное обеспечение для высокоскоростной передачи файлов.</span><span class="sxs-lookup"><span data-stu-id="d3473-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="d3473-106">**Aspera Server On Demand** для Azure позволяет быстро отправлять большие файлы непосредственно в хранилище BLOB-объектов Azure и скачивать их из него.</span><span class="sxs-lookup"><span data-stu-id="d3473-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="d3473-107">Дополнительные сведения о службе **Aspera On Demand** см. на сайте [Aspera Cloud](http://cloud.asperasoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d3473-107">For information about **Aspera On Demand**, see the [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="d3473-108">**Aspera Server On Demand** для Azure можно приобрести в [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="d3473-108">**Aspera Server On Demand** for Azure is available for purchase from the [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="d3473-109">Чтобы купить **Aspera Server On Demand**, войдите в Azure Marketplace с помощью учетной записи Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="d3473-109">In order to complete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="d3473-110">Из этого руководства вы узнаете, как отправлять файлы в учетную запись хранилища, связанную с учетной записью служб мультимедиа, с помощью службы **Aspera Server On Demand** в Azure.</span><span class="sxs-lookup"><span data-stu-id="d3473-110">This tutorial walks you through the steps of uploading files into a storage account that is associated with a Media Services account using the **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="d3473-111">Пример, в котором показано, как пользоваться функциями Azure со службами мультимедиа и Aspera, вы можете найти [здесь](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span><span class="sxs-lookup"><span data-stu-id="d3473-111">You can find an example that shows how to use Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="d3473-112">Существует ограничение на максимальный размер файла, который могут обработать службы мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="d3473-112">There is a limit to the maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="d3473-113">Подробные сведения об этом см. [здесь](media-services-quotas-and-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d3473-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="d3473-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d3473-114">Prerequisites</span></span> 

<span data-ttu-id="d3473-115">Для работы с этим руководством необходимы указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="d3473-115">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="d3473-116">Учетная запись Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="d3473-116">A Windows Live ID</span></span>
* <span data-ttu-id="d3473-117">[Учетная запись Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d3473-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="d3473-118">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3473-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="d3473-119">[Учетная запись служб мультимедиа Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d3473-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="d3473-120">Покупка службы Aspera On Demand для Azure</span><span class="sxs-lookup"><span data-stu-id="d3473-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="d3473-121">Войдя в Azure Marketplace, выполните следующие действия, чтобы приобрести службу Aspera On Demand для Azure.</span><span class="sxs-lookup"><span data-stu-id="d3473-121">Once you have logged into Azure Marketplace,  follow these basic steps to complete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="d3473-122">Выполните поисковый запрос Aspera и выберите Server On Demand.</span><span class="sxs-lookup"><span data-stu-id="d3473-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="d3473-124">Просмотрите планы подписки и нажмите кнопку регистрации.</span><span class="sxs-lookup"><span data-stu-id="d3473-124">Review the subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="d3473-126">Укажите необходимые сведения для оформления подписки на службу Server on Demand.</span><span class="sxs-lookup"><span data-stu-id="d3473-126">Fill in the specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="d3473-128">Щелкните **Ценовая категория** и в открывшейся колонке выберите требуемый месячный объем.</span><span class="sxs-lookup"><span data-stu-id="d3473-128">Click on the **Pricing Tier** and select your desired monthly volume in the sub panel.</span></span> <span data-ttu-id="d3473-129">В колонке **Сведения о плане** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d3473-129">In the **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="d3473-130">Затем в колонке **Выбор ценовой категории** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d3473-130">Then, in the **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="d3473-132">Щелкните **Условия**, а затем в открывшейся колонке просмотрите и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="d3473-132">Click on **Legal terms** to view and accept the legal terms in the sub panel.</span></span> <span data-ttu-id="d3473-133">После этого нажмите кнопку **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="d3473-133">Once you have reviewed the legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="d3473-135">Завершите покупку, нажав кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d3473-135">Complete the purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="d3473-137">На панели мониторинга Azure отобразится уведомление о том, что выполняется подготовка службы.</span><span class="sxs-lookup"><span data-stu-id="d3473-137">The Azure dashboard will announce that it is provisioning the service.</span></span>  <span data-ttu-id="d3473-138">Когда она завершиться, новую подписку можно будет найти среди ресурсов путем поиска по имени службы.</span><span class="sxs-lookup"><span data-stu-id="d3473-138">Once it is completed with provisioning, you can find the new subscription by searching in your resources for the name of the service.</span></span> <span data-ttu-id="d3473-139">Найдя службу, дважды щелкните ее, чтобы открыть портал управления службами.</span><span class="sxs-lookup"><span data-stu-id="d3473-139">Once you have found the service, double click on it to launch the service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="d3473-141">Откройте портал управления Aspera.</span><span class="sxs-lookup"><span data-stu-id="d3473-141">Launch the Aspera management portal.</span></span> <span data-ttu-id="d3473-142">Обнаружив свою новую службу Aspera, щелкните ее, чтобы получить доступ к порталу управления.</span><span class="sxs-lookup"><span data-stu-id="d3473-142">Once you have found your new Aspera service, you can gain access to the management portal, by clicking on the service.</span></span>  <span data-ttu-id="d3473-143">Откроется новая панель.</span><span class="sxs-lookup"><span data-stu-id="d3473-143">A new panel will be launched.</span></span> <span data-ttu-id="d3473-144">На ней необходимо щелкнуть **имя ресурса** новой службы.</span><span class="sxs-lookup"><span data-stu-id="d3473-144">From within that new panel, you need to click on the **Resource Name** of your new service.</span></span>  <span data-ttu-id="d3473-145">На следующем снимке экрана имя ресурса — это AsperaTransferDemo.</span><span class="sxs-lookup"><span data-stu-id="d3473-145">In the following screenshot, the resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="d3473-146">Когда вы щелкните имя ресурса, откроется еще одна панель.</span><span class="sxs-lookup"><span data-stu-id="d3473-146">Once you click on the resource name, another panel is launched.</span></span> <span data-ttu-id="d3473-147">На ней вы увидите кнопку "Управление".</span><span class="sxs-lookup"><span data-stu-id="d3473-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="d3473-148">Нажмите эту кнопку, чтобы открыть портал управления Aspera.</span><span class="sxs-lookup"><span data-stu-id="d3473-148">Click on the 'Manage' link to launch the Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="d3473-150">Нажав кнопку "Управление", вы перейдете на страницу регистрации, которая необходима для доступа к службе.</span><span class="sxs-lookup"><span data-stu-id="d3473-150">By clicking on the manage link, you will get to the registration page, which is required to access the service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="d3473-152">На этом этапе у вас должен быть доступ к порталу управления службами Aspera, на котором можно создавать ключи доступа, скачивать клиенты и лицензии Aspera, просматривать данные об использовании и получать сведения об интерфейсах API.</span><span class="sxs-lookup"><span data-stu-id="d3473-152">At this point, you should have access to the Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about the APIs.</span></span>

    <span data-ttu-id="d3473-153">На снимке экрана ниже показан процесс получения доступа.</span><span class="sxs-lookup"><span data-stu-id="d3473-153">The following screenshot shows the access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="d3473-155">На следующем снимке экрана показаны интерфейсы отчетов об использовании на портале.</span><span class="sxs-lookup"><span data-stu-id="d3473-155">The following screenshot shows the usage reporting interfaces in the portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="d3473-157">Отправка файлов с помощью Aspera</span><span class="sxs-lookup"><span data-stu-id="d3473-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="d3473-158">Скачайте и установите клиентское программное обеспечение Aspera:</span><span class="sxs-lookup"><span data-stu-id="d3473-158">Download and install the Aspera client software:</span></span>
    
    * <span data-ttu-id="d3473-159">[подключаемый модуль браузера](http://downloads.asperasoft.com/connect2/);</span><span class="sxs-lookup"><span data-stu-id="d3473-159">[Browser plugin](http://downloads.asperasoft.com/connect2/)</span></span>
    * <span data-ttu-id="d3473-160">[полнофункциональный клиент](http://downloads.asperasoft.com/en/downloads/2).</span><span class="sxs-lookup"><span data-stu-id="d3473-160">[Rich client](http://downloads.asperasoft.com/en/downloads/2)</span></span>

2. <span data-ttu-id="d3473-161">Выполните первую передачу.</span><span class="sxs-lookup"><span data-stu-id="d3473-161">Make your first transfer.</span></span> <span data-ttu-id="d3473-162">Чтобы использовать клиент Aspera для передачи с помощью службы передачи Aspera, необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="d3473-162">In order to use the Aspera client to transfer with the Aspera transfer service, you need to complete the following:</span></span> 

    1. <span data-ttu-id="d3473-163">Создайте на портале Aspera ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="d3473-163">Create an access key, using the Aspera portal.</span></span>  
    2. <span data-ttu-id="d3473-164">Скачайте и установите клиент Aspera, а также активируйте лицензию (программное обеспечение можно найти на портале Aspera).</span><span class="sxs-lookup"><span data-stu-id="d3473-164">Download, install, and license the Aspera client (software can be found in the Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="d3473-165">Сведения о конфигурации содержатся в руководстве по клиенту Aspera, с которым рекомендуется ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="d3473-165">Please read the Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="d3473-166">С помощью [портала Azure](https://portal.azure.com/) получите некоторые данные вашей учетной записи хранения, связанной с учетной записью служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="d3473-166">Retrieve some information of your storage account that is associated with your Azure Media Account using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d3473-167">В частности, имя, ключ и имя контейнера хранилища BLOB-объектов, в котором необходимо разместить содержимое.</span><span class="sxs-lookup"><span data-stu-id="d3473-167">Specifically, name and key, and the storage blob container name in to which you want to place your content.</span></span> 

        * <span data-ttu-id="d3473-168">Для получения сведений о хранилище на портале сделайте следующее: найдите учетную запись хранения, щелкните ключи доступа и скопируйте имя и ключ своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d3473-168">To get the storage info from the portal: find your storage account, click on the Access keys and copy the name and the key of your account.</span></span>
        * <span data-ttu-id="d3473-169">Чтобы получить имя контейнера, сделайте вот что: найдите учетную запись хранения, щелкните **BLOB-объекты** и выберите имя контейнера, в который необходимо отправить содержимое.</span><span class="sxs-lookup"><span data-stu-id="d3473-169">To get the container name: find your storage account, select **Blobs**, select the name of the container you want to upload the content into.</span></span> 

    <span data-ttu-id="d3473-170">Ниже приведен снимок экрана **диспетчера подключений** в клиенте Aspera, в окне которого необходимо указать тип и учетные данные хранилища Azure, а также контейнер BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="d3473-170">Below is the screenshot of the Aspera client **Connection Manager** where you must specify the 'Azure' storage type and credentials as well as the blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="d3473-172">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="d3473-172">Resources</span></span>

<span data-ttu-id="d3473-173">В данной статье упоминались следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="d3473-173">The following resources were mentioned in this article.</span></span> 

* <span data-ttu-id="d3473-174">[подключаемый модуль Aspera Connect](http://downloads.asperasoft.com/connect2/);</span><span class="sxs-lookup"><span data-stu-id="d3473-174">[Connect Browser Plugin](http://downloads.asperasoft.com/connect2/)</span></span>
* <span data-ttu-id="d3473-175">[справочная документация по Aspera Connect](http://downloads.asperasoft.com/en/documentation/8);</span><span class="sxs-lookup"><span data-stu-id="d3473-175">[Connect Guide](http://downloads.asperasoft.com/en/documentation/8)</span></span>
* <span data-ttu-id="d3473-176">[клиент Aspera](http://downloads.asperasoft.com/en/downloads/2);</span><span class="sxs-lookup"><span data-stu-id="d3473-176">[Aspera Client](http://downloads.asperasoft.com/en/downloads/2)</span></span>
* <span data-ttu-id="d3473-177">[справочная документация по клиенту Aspera](http://downloads.asperasoft.com/en/documentation/2).</span><span class="sxs-lookup"><span data-stu-id="d3473-177">[Client Guide](http://downloads.asperasoft.com/en/documentation/2)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3473-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3473-178">Next steps</span></span>

<span data-ttu-id="d3473-179">Теперь вы можете [копировать большие двоичные объекты из учетной записи хранения в учетную запись AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="d3473-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d3473-180">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d3473-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d3473-181">Отзывы</span><span class="sxs-lookup"><span data-stu-id="d3473-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

