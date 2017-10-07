---
title: "aaaHow toocreate и развертывание облачной службы | Документы Microsoft"
description: "Узнайте, как toocreate и развернуть облачную службу с помощью портала Azure hello."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a><span data-ttu-id="b725b-103">Как toocreate и развертывание облачной службы</span><span class="sxs-lookup"><span data-stu-id="b725b-103">How toocreate and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b725b-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b725b-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="b725b-105">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="b725b-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="b725b-106">Hello Azure предоставляет два способа для вас toocreate и развертывание облачной службы: *быстрое создание* и *настраиваемое создание*.</span><span class="sxs-lookup"><span data-stu-id="b725b-106">hello Azure portal provides two ways for you toocreate and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="b725b-107">В этой статье объясняется, как toouse hello toocreate метод быстрое создание новой облачной службы, а затем используйте **отправить** tooupload и развернуть пакет облачной службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="b725b-107">This article explains how toouse hello Quick Create method toocreate a new cloud service and then use **Upload** tooupload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="b725b-108">При использовании этого метода hello портал Azure делает доступных ссылок, удобный для выполнения всех требований, при переходе.</span><span class="sxs-lookup"><span data-stu-id="b725b-108">When you use this method, hello Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="b725b-109">Если вы готовы toodeploy вашей облачной службы при его создании, это можно сделать из hello одновременно с помощью настраиваемое создание.</span><span class="sxs-lookup"><span data-stu-id="b725b-109">If you're ready toodeploy your cloud service when you create it, you can do both at hello same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="b725b-110">Если планируется toopublish облачной службы из Visual Studio Team Services (VSTS), использовать функцию быстрого запуска и затем настроить публикацию VSTS с панели мониторинга быстрый запуск Azure или hello hello.</span><span class="sxs-lookup"><span data-stu-id="b725b-110">If you plan toopublish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from hello Azure Quickstart or hello dashboard.</span></span> <span data-ttu-id="b725b-111">Дополнительные сведения см. в разделе [tooAzure непрерывной поставки с помощью Visual Studio Team Services][TFSTutorialForCloudService], или получить справки для hello **быстрый запуск** страницы.</span><span class="sxs-lookup"><span data-stu-id="b725b-111">For more information, see [Continuous Delivery tooAzure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for hello **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="b725b-112">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="b725b-112">Concepts</span></span>
<span data-ttu-id="b725b-113">Три компонента находятся необходимые toodeploy приложения как облачной службы в Azure:</span><span class="sxs-lookup"><span data-stu-id="b725b-113">Three components are required toodeploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="b725b-114">**Определение службы.**</span><span class="sxs-lookup"><span data-stu-id="b725b-114">**Service Definition**</span></span>  
  <span data-ttu-id="b725b-115">облако Hello для файла определения службы (.csdef) определяет модель службы hello, включая hello число ролей.</span><span class="sxs-lookup"><span data-stu-id="b725b-115">hello cloud service definition file (.csdef) defines hello service model, including hello number of roles.</span></span>
* <span data-ttu-id="b725b-116">**Конфигурация службы.**</span><span class="sxs-lookup"><span data-stu-id="b725b-116">**Service Configuration**</span></span>  
  <span data-ttu-id="b725b-117">файл конфигурации облачной службы Hello (.cscfg) предоставляет параметры конфигурации для hello облачной службы и отдельных ролей, включая hello число экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="b725b-117">hello cloud service configuration file (.cscfg) provides configuration settings for hello cloud service and individual roles, including hello number of role instances.</span></span>
* <span data-ttu-id="b725b-118">**Пакет службы.**</span><span class="sxs-lookup"><span data-stu-id="b725b-118">**Service Package**</span></span>  
  <span data-ttu-id="b725b-119">Hello пакета службы (cspkg-файл) содержит код приложения hello и конфигурации и файл определения службы hello.</span><span class="sxs-lookup"><span data-stu-id="b725b-119">hello service package (.cspkg) contains hello application code and configurations and hello service definition file.</span></span>

<span data-ttu-id="b725b-120">Дополнительные сведения об этих и как toocreate пакета [здесь](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="b725b-120">You can learn more about these and how toocreate a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="b725b-121">Подготовка приложения</span><span class="sxs-lookup"><span data-stu-id="b725b-121">Prepare your app</span></span>
<span data-ttu-id="b725b-122">Перед развертыванием облачной службы необходимо создать пакет hello облачной службы (cspkg-файл) с кодом приложения и файл конфигурации облачной службы (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="b725b-122">Before you can deploy a cloud service, you must create hello cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="b725b-123">Hello Azure SDK предоставляет средства для подготовки этих требуемые файлы развертывания.</span><span class="sxs-lookup"><span data-stu-id="b725b-123">hello Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="b725b-124">Можно установить пакет SDK для hello из hello [загрузки Azure](https://azure.microsoft.com/downloads/) страницы на языке hello, в котором вы предпочитаете toodevelop код вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="b725b-124">You can install hello SDK from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page, in hello language in which you prefer toodevelop your application code.</span></span>

<span data-ttu-id="b725b-125">Перед экспортом пакета службы необходимо отдельно настроить три компонента облачной службы:</span><span class="sxs-lookup"><span data-stu-id="b725b-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="b725b-126">Если требуется, чтобы toodeploy облачной службы, которая использует протокол Secure Sockets Layer (SSL) для шифрования данных, [настройки приложения](cloud-services-configure-ssl-certificate-portal.md#modify) для SSL.</span><span class="sxs-lookup"><span data-stu-id="b725b-126">If you want toodeploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="b725b-127">Если нужно экземпляров toorole подключения удаленного рабочего стола tooconfigure, [настроить роли hello](cloud-services-role-enable-remote-desktop-new-portal.md) для удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="b725b-127">If you want tooconfigure Remote Desktop connections toorole instances, [configure hello roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="b725b-128">Если вы хотите tooconfigure подробного мониторинга для облачной службы, включение диагностики Azure для hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="b725b-128">If you want tooconfigure verbose monitoring for your cloud service, enable Azure Diagnostics for hello cloud service.</span></span> <span data-ttu-id="b725b-129">*Минимальный мониторинг* (по умолчанию hello уровень мониторинга) использует счетчики производительности, собранных из операционных систем узлов hello для экземпляров роли (виртуальных машин).</span><span class="sxs-lookup"><span data-stu-id="b725b-129">*Minimal monitoring* (hello default monitoring level) uses performance counters gathered from hello host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="b725b-130">*Подробный мониторинг* собирает дополнительные метрики на основе данных производительности в рамках hello экземпляры роли tooenable более тщательного анализа проблем, возникающих во время обработки приложения.</span><span class="sxs-lookup"><span data-stu-id="b725b-130">*Verbose monitoring* gathers additional metrics based on performance data within hello role instances tooenable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="b725b-131">в разделе диагностики Azure tooenable, toofind о том, как [включение диагностики в Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b725b-131">toofind out how tooenable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="b725b-132">необходимо toocreate облачную службу с развертываниями веб-ролей или рабочих ролей [создать пакет службы hello](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="b725b-132">toocreate a cloud service with deployments of web roles or worker roles, you must [create hello service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b725b-133">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="b725b-133">Before you begin</span></span>
* <span data-ttu-id="b725b-134">Если вы не установили hello Azure SDK, нажмите кнопку **установить пакет Azure SDK** tooopen hello [страницу загрузок Azure](https://azure.microsoft.com/downloads/)и загрузите hello пакета SDK для hello язык, в котором toodevelop кода.</span><span class="sxs-lookup"><span data-stu-id="b725b-134">If you haven't installed hello Azure SDK, click **Install Azure SDK** tooopen hello [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download hello SDK for hello language in which you prefer toodevelop your code.</span></span> <span data-ttu-id="b725b-135">(Чтобы иметь возможность toodo это более поздней версии.)</span><span class="sxs-lookup"><span data-stu-id="b725b-135">(You'll have an opportunity toodo this later.)</span></span>
* <span data-ttu-id="b725b-136">Если все экземпляры ролей, требуется сертификат, создайте сертификаты hello.</span><span class="sxs-lookup"><span data-stu-id="b725b-136">If any role instances require a certificate, create hello certificates.</span></span> <span data-ttu-id="b725b-137">В облачных службах используется PFX-файл с закрытым ключом.</span><span class="sxs-lookup"><span data-stu-id="b725b-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="b725b-138">Можно передать tooAzure сертификаты hello, как создать и развернуть облачную службу hello.</span><span class="sxs-lookup"><span data-stu-id="b725b-138">You can upload hello certificates tooAzure as you create and deploy hello cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="b725b-139">Создание и развертывание</span><span class="sxs-lookup"><span data-stu-id="b725b-139">Create and deploy</span></span>
1. <span data-ttu-id="b725b-140">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b725b-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b725b-141">Нажмите кнопку **Создать > вычислений**, а затем прокрутите экран вниз tooand щелкните **облачной службы**.</span><span class="sxs-lookup"><span data-stu-id="b725b-141">Click **New > Compute**, and then scroll down tooand click **Cloud Service**.</span></span>

    ![Публикация облачной службы](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="b725b-143">В новых hello **облачной службы** колонки, введите значение для hello **DNS-имя**.</span><span class="sxs-lookup"><span data-stu-id="b725b-143">In hello new **Cloud Service** blade, enter a value for hello **DNS name**.</span></span>
4. <span data-ttu-id="b725b-144">Создайте новую **группу ресурсов** или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="b725b-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="b725b-145">Выберите **расположение**.</span><span class="sxs-lookup"><span data-stu-id="b725b-145">Select a **Location**.</span></span>
6. <span data-ttu-id="b725b-146">Щелкните **Пакет**.</span><span class="sxs-lookup"><span data-stu-id="b725b-146">Click **Package**.</span></span> <span data-ttu-id="b725b-147">После этого откроется hello **загрузки пакета** колонку.</span><span class="sxs-lookup"><span data-stu-id="b725b-147">This will open hello **Upload a package** blade.</span></span> <span data-ttu-id="b725b-148">Заполните необходимые hello.</span><span class="sxs-lookup"><span data-stu-id="b725b-148">Fill in hello required fields.</span></span> <span data-ttu-id="b725b-149">Если какая-либо из ролей содержит отдельный экземпляр, убедитесь, что установлен флажок **Развернуть, даже если одна или несколько ролей содержат отдельный экземпляр** .</span><span class="sxs-lookup"><span data-stu-id="b725b-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="b725b-150">Убедитесь, что установлен флажок **Запустить развертывание** .</span><span class="sxs-lookup"><span data-stu-id="b725b-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="b725b-151">Нажмите кнопку **ОК** которого будет закрыт hello **загрузки пакета** колонку.</span><span class="sxs-lookup"><span data-stu-id="b725b-151">Click **OK** which will close hello **Upload a package** blade.</span></span>
9. <span data-ttu-id="b725b-152">Если у вас tooadd все сертификаты, щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="b725b-152">If you do not have any certificates tooadd, click **Create**.</span></span>

    ![Публикация облачной службы](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="b725b-154">Загрузить сертификат</span><span class="sxs-lookup"><span data-stu-id="b725b-154">Upload a certificate</span></span>
<span data-ttu-id="b725b-155">Если пакет развертывания был [настроить сертификаты toouse](cloud-services-configure-ssl-certificate-portal.md#modify), теперь можно отправить сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="b725b-155">If your deployment package was [configured toouse certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload hello certificate now.</span></span>

1. <span data-ttu-id="b725b-156">Выберите **сертификаты**и на hello **Добавление сертификатов** колонке выберите PFX-файл сертификата SSL hello, а затем введите hello **пароль** для сертификата hello</span><span class="sxs-lookup"><span data-stu-id="b725b-156">Select **Certificates**, and on hello **Add certificates** blade, select hello SSL certificate .pfx file, and then provide hello **Password** for hello certificate,</span></span>
2. <span data-ttu-id="b725b-157">Нажмите кнопку **сертификат присоединения**и нажмите кнопку **ОК** на hello **добавить сертификаты** колонку.</span><span class="sxs-lookup"><span data-stu-id="b725b-157">Click **Attach certificate**, and then click **OK** on hello **Add certificates** blade.</span></span>
3. <span data-ttu-id="b725b-158">Нажмите кнопку **создать** на hello **облачной службы** колонку.</span><span class="sxs-lookup"><span data-stu-id="b725b-158">Click **Create** on hello **Cloud Service** blade.</span></span> <span data-ttu-id="b725b-159">При развертывании hello достиг hello **готовности** состояние, можно продолжить toohello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="b725b-159">When hello deployment has reached hello **Ready** status, you can proceed toohello next steps.</span></span>

    ![Публикация облачной службы](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="b725b-161">Проверка успешного завершения развертывания</span><span class="sxs-lookup"><span data-stu-id="b725b-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="b725b-162">Щелкните экземпляр службы hello облака.</span><span class="sxs-lookup"><span data-stu-id="b725b-162">Click hello cloud service instance.</span></span>

    <span data-ttu-id="b725b-163">Hello состояния должен показать, что служба hello **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="b725b-163">hello status should show that hello service is **Running**.</span></span>
2. <span data-ttu-id="b725b-164">В разделе **Essentials**, нажмите кнопку hello **URL-адрес сайта** tooopen вашей облачной службы в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="b725b-164">Under **Essentials**, click hello **Site URL** tooopen your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="b725b-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b725b-166">Next steps</span></span>
* <span data-ttu-id="b725b-167">[Общая настройка облачной службы](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b725b-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="b725b-168">Настройка [пользовательского имени домена](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b725b-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="b725b-169">[Управление облачной службой](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b725b-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="b725b-170">Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b725b-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
