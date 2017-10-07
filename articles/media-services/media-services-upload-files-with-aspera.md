---
title: "aaaUpload файлы в учетную запись служб мультимедиа Azure с помощью Aspera | Документы Microsoft"
description: "Этот учебник поможет вам выполнить этапы hello передачи файлов в учетную запись хранилища, связанный с учетной записью служб мультимедиа, используя hello ** Aspera Server по запросу ** службы в Azure."
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
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="388ee-103">Отправка файлов в учетную запись служб мультимедиа с использованием hello службы Aspera Server по запросу в Azure</span><span class="sxs-lookup"><span data-stu-id="388ee-103">Upload files into a Media Services account using hello Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="388ee-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="388ee-104">Overview</span></span>

<span data-ttu-id="388ee-105">**Aspera** — это программное обеспечение для высокоскоростной передачи файлов.</span><span class="sxs-lookup"><span data-stu-id="388ee-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="388ee-106">**Aspera Server On Demand** для Azure позволяет быстро отправлять большие файлы непосредственно в хранилище BLOB-объектов Azure и скачивать их из него.</span><span class="sxs-lookup"><span data-stu-id="388ee-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="388ee-107">Сведения о **Aspera On Demand**, в разделе hello [Aspera облака](http://cloud.asperasoft.com/) сайта.</span><span class="sxs-lookup"><span data-stu-id="388ee-107">For information about **Aspera On Demand**, see hello [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="388ee-108">**Aspera Server по запросу** для Azure можно приобрести из hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="388ee-108">**Aspera Server On Demand** for Azure is available for purchase from hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="388ee-109">Чтобы toocomplete покупке **Aspera Server по запросу** Azure, войдите в Azure Marketplace со своего Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="388ee-109">In order toocomplete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="388ee-110">Этот учебник поможет вам выполнить этапы hello передачи файлов в учетную запись хранилища, связанный с учетной записью служб мультимедиа, используя hello **Aspera Server по запросу** службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="388ee-110">This tutorial walks you through hello steps of uploading files into a storage account that is associated with a Media Services account using hello **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="388ee-111">Можно найти пример, в котором показано, как функционирует toouse Azure со службами мультимедиа и Aspera [здесь](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span><span class="sxs-lookup"><span data-stu-id="388ee-111">You can find an example that shows how toouse Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="388ee-112">Имеется ограничение toohello максимальный размер файла поддерживается для обработки с помощью служб мультимедиа Azure media процессоров (MP).</span><span class="sxs-lookup"><span data-stu-id="388ee-112">There is a limit toohello maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="388ee-113">См. в разделе [это](media-services-quotas-and-limitations.md) сведения о hello ограничения размера файла.</span><span class="sxs-lookup"><span data-stu-id="388ee-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="388ee-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="388ee-114">Prerequisites</span></span> 

<span data-ttu-id="388ee-115">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="388ee-115">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="388ee-116">Учетная запись Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="388ee-116">A Windows Live ID</span></span>
* <span data-ttu-id="388ee-117">[Учетная запись Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="388ee-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="388ee-118">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="388ee-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="388ee-119">[Учетная запись служб мультимедиа Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="388ee-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="388ee-120">Покупка службы Aspera On Demand для Azure</span><span class="sxs-lookup"><span data-stu-id="388ee-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="388ee-121">После входа в Azure Marketplace, выполните эти шаги toocomplete приобретение Aspera On Demand for Azure.</span><span class="sxs-lookup"><span data-stu-id="388ee-121">Once you have logged into Azure Marketplace,  follow these basic steps toocomplete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="388ee-122">Выполните поисковый запрос Aspera и выберите Server On Demand.</span><span class="sxs-lookup"><span data-stu-id="388ee-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="388ee-124">Просмотрите планы hello подписки и нажмите кнопку «Зарегистрироваться»</span><span class="sxs-lookup"><span data-stu-id="388ee-124">Review hello subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="388ee-126">Заполните hello особенностей сервера для подписки по запросу.</span><span class="sxs-lookup"><span data-stu-id="388ee-126">Fill in hello specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="388ee-128">Щелкните hello **ценовую категорию** и выделите нужный месяц тома панели sub hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-128">Click on hello **Pricing Tier** and select your desired monthly volume in hello sub panel.</span></span> <span data-ttu-id="388ee-129">В hello **вопросам планирования** панель, выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="388ee-129">In hello **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="388ee-130">Затем в hello **выберите ценовую категорию** нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="388ee-130">Then, in hello **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="388ee-132">Щелкните **условия** tooview и примите условия hello панели sub hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-132">Click on **Legal terms** tooview and accept hello legal terms in hello sub panel.</span></span> <span data-ttu-id="388ee-133">Изучив hello условиями, нажмите кнопку **покупки**.</span><span class="sxs-lookup"><span data-stu-id="388ee-133">Once you have reviewed hello legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="388ee-135">Завершить покупку hello, щелкнув **создать**.</span><span class="sxs-lookup"><span data-stu-id="388ee-135">Complete hello purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="388ee-137">Hello панель мониторинга Azure будут сообщать, что Подготовка службы hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-137">hello Azure dashboard will announce that it is provisioning hello service.</span></span>  <span data-ttu-id="388ee-138">После завершения при подготовке hello новую подписку можно найти путем поиска в ресурсы для hello имя службы hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-138">Once it is completed with provisioning, you can find hello new subscription by searching in your resources for hello name of hello service.</span></span> <span data-ttu-id="388ee-139">Найденной службы hello, дважды щелкните его портала управления службами toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-139">Once you have found hello service, double click on it toolaunch hello service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="388ee-141">Запустите портал управления Aspera hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-141">Launch hello Aspera management portal.</span></span> <span data-ttu-id="388ee-142">После обнаружения новой службой Aspera портал управления access toohello, можно получить, щелкнув службу hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-142">Once you have found your new Aspera service, you can gain access toohello management portal, by clicking on hello service.</span></span>  <span data-ttu-id="388ee-143">Откроется новая панель.</span><span class="sxs-lookup"><span data-stu-id="388ee-143">A new panel will be launched.</span></span> <span data-ttu-id="388ee-144">Из этой новой панели необходимо tooclick на hello **имя ресурса** новой службы.</span><span class="sxs-lookup"><span data-stu-id="388ee-144">From within that new panel, you need tooclick on hello **Resource Name** of your new service.</span></span>  <span data-ttu-id="388ee-145">В следующий снимок экрана приветствия hello ресурс называется «AsperaTransferDemo».</span><span class="sxs-lookup"><span data-stu-id="388ee-145">In hello following screenshot, hello resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="388ee-146">После нажатия кнопки на имя ресурса hello, другой панели, будет запущен.</span><span class="sxs-lookup"><span data-stu-id="388ee-146">Once you click on hello resource name, another panel is launched.</span></span> <span data-ttu-id="388ee-147">На ней вы увидите кнопку "Управление".</span><span class="sxs-lookup"><span data-stu-id="388ee-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="388ee-148">Щелкните «Управление» связь toolaunch hello Aspera портала управления hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-148">Click on hello 'Manage' link toolaunch hello Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="388ee-150">Щелкнув hello управлять ссылку, отобразится страница регистрации toohello, который требуется tooaccess hello службы.</span><span class="sxs-lookup"><span data-stu-id="388ee-150">By clicking on hello manage link, you will get toohello registration page, which is required tooaccess hello service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="388ee-152">На этом этапе должен иметь доступ toohello Aspera портала управления службами, где можно создать ключи доступа, загрузите Aspera клиентов и лицензий, сведения об использовании и Дополнительные сведения о hello API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="388ee-152">At this point, you should have access toohello Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about hello APIs.</span></span>

    <span data-ttu-id="388ee-153">Hello следующем снимке экрана показано создание доступа hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-153">hello following screenshot shows hello access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="388ee-155">Hello следующем снимке экрана показано использование hello reporting интерфейсы hello портала.</span><span class="sxs-lookup"><span data-stu-id="388ee-155">hello following screenshot shows hello usage reporting interfaces in hello portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="388ee-157">Отправка файлов с помощью Aspera</span><span class="sxs-lookup"><span data-stu-id="388ee-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="388ee-158">Загрузите и установите программное обеспечение клиента Aspera hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-158">Download and install hello Aspera client software:</span></span>
    
    * <span data-ttu-id="388ee-159">[подключаемый модуль браузера](http://downloads.asperasoft.com/connect2/);</span><span class="sxs-lookup"><span data-stu-id="388ee-159">[Browser plugin](http://downloads.asperasoft.com/connect2/)</span></span>
    * <span data-ttu-id="388ee-160">[полнофункциональный клиент](http://downloads.asperasoft.com/en/downloads/2).</span><span class="sxs-lookup"><span data-stu-id="388ee-160">[Rich client](http://downloads.asperasoft.com/en/downloads/2)</span></span>

2. <span data-ttu-id="388ee-161">Выполните первую передачу.</span><span class="sxs-lookup"><span data-stu-id="388ee-161">Make your first transfer.</span></span> <span data-ttu-id="388ee-162">В порядке toouse hello Aspera клиента tootransfer с hello Aspera служба передачи необходимо toocomplete hello следующее:</span><span class="sxs-lookup"><span data-stu-id="388ee-162">In order toouse hello Aspera client tootransfer with hello Aspera transfer service, you need toocomplete hello following:</span></span> 

    1. <span data-ttu-id="388ee-163">Создайте ключ доступа, с помощью портала Aspera hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-163">Create an access key, using hello Aspera portal.</span></span>  
    2. <span data-ttu-id="388ee-164">Загрузку, установку и Aspera клиентских лицензий hello (программного обеспечения можно найти на портале Aspera hello).</span><span class="sxs-lookup"><span data-stu-id="388ee-164">Download, install, and license hello Aspera client (software can be found in hello Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="388ee-165">Прочитайте руководство для клиента Aspera hello сведения о конфигурации.</span><span class="sxs-lookup"><span data-stu-id="388ee-165">Please read hello Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="388ee-166">Получить некоторые сведения о вашей учетной записи хранилища, связанный с учетной записью мультимедиа Azure с помощью hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="388ee-166">Retrieve some information of your storage account that is associated with your Azure Media Account using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="388ee-167">В частности, имя и ключ и имя контейнера больших двоичных объектов хранилища hello toowhich требуется tooplace контента.</span><span class="sxs-lookup"><span data-stu-id="388ee-167">Specifically, name and key, and hello storage blob container name in toowhich you want tooplace your content.</span></span> 

        * <span data-ttu-id="388ee-168">сведения о хранилище hello tooget из портала hello: найти вашу учетную запись хранения, щелкайте клавиши доступа hello и копирования hello имя и hello ключ учетной записи.</span><span class="sxs-lookup"><span data-stu-id="388ee-168">tooget hello storage info from hello portal: find your storage account, click on hello Access keys and copy hello name and hello key of your account.</span></span>
        * <span data-ttu-id="388ee-169">Имя контейнера hello tooget: найти вашей учетной записи хранилища, выберите **большие двоичные объекты**выберите hello имя контейнера hello, tooupload содержимое hello в.</span><span class="sxs-lookup"><span data-stu-id="388ee-169">tooget hello container name: find your storage account, select **Blobs**, select hello name of hello container you want tooupload hello content into.</span></span> 

    <span data-ttu-id="388ee-170">Ниже приведен снимок экрана приветствия клиента Aspera hello **диспетчера соединений** где необходимо указать тип хранения «Azure» hello и учетные данные, а также контейнер больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="388ee-170">Below is hello screenshot of hello Aspera client **Connection Manager** where you must specify hello 'Azure' storage type and credentials as well as hello blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="388ee-172">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="388ee-172">Resources</span></span>

<span data-ttu-id="388ee-173">следующие ресурсы Hello, упомянутых в этой статье.</span><span class="sxs-lookup"><span data-stu-id="388ee-173">hello following resources were mentioned in this article.</span></span> 

* <span data-ttu-id="388ee-174">[подключаемый модуль Aspera Connect](http://downloads.asperasoft.com/connect2/);</span><span class="sxs-lookup"><span data-stu-id="388ee-174">[Connect Browser Plugin](http://downloads.asperasoft.com/connect2/)</span></span>
* <span data-ttu-id="388ee-175">[справочная документация по Aspera Connect](http://downloads.asperasoft.com/en/documentation/8);</span><span class="sxs-lookup"><span data-stu-id="388ee-175">[Connect Guide](http://downloads.asperasoft.com/en/documentation/8)</span></span>
* <span data-ttu-id="388ee-176">[клиент Aspera](http://downloads.asperasoft.com/en/downloads/2);</span><span class="sxs-lookup"><span data-stu-id="388ee-176">[Aspera Client](http://downloads.asperasoft.com/en/downloads/2)</span></span>
* <span data-ttu-id="388ee-177">[справочная документация по клиенту Aspera](http://downloads.asperasoft.com/en/documentation/2).</span><span class="sxs-lookup"><span data-stu-id="388ee-177">[Client Guide](http://downloads.asperasoft.com/en/documentation/2)</span></span>

## <a name="next-steps"></a><span data-ttu-id="388ee-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="388ee-178">Next steps</span></span>

<span data-ttu-id="388ee-179">Теперь вы можете [копировать большие двоичные объекты из учетной записи хранения в учетную запись AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="388ee-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="388ee-180">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="388ee-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="388ee-181">Отзывы</span><span class="sxs-lookup"><span data-stu-id="388ee-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

