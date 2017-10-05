---
title: "Создание и развертывание облачной службы | Документация Майкрософт"
description: "Узнайте, как создать и развернуть облачную службу с помощью портала Azure."
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
ms.openlocfilehash: e5ce666f1d826c7901c9fd5e7fafe6171139c3ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="5b9ad-103">Создание и развертывание облачной службы</span><span class="sxs-lookup"><span data-stu-id="5b9ad-103">How to create and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b9ad-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5b9ad-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="5b9ad-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="5b9ad-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="5b9ad-106">Портал Azure предоставляет два способа создания и развертывания облачной службы: *быстрое создание* и *настраиваемое создание*.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-106">The Azure portal provides two ways for you to create and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="5b9ad-107">В этой статье описывается быстрое создание облачной службы с последующим развертыванием соответствующего ей пакета в Azure с помощью функции **Отправка** .</span><span class="sxs-lookup"><span data-stu-id="5b9ad-107">This article explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="5b9ad-108">При выборе этого способа на портале Azure отображаются все необходимые для работы ссылки.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-108">When you use this method, the Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="5b9ad-109">Чтобы одновременно выполнить развертывание создаваемой облачной службы, воспользуйтесь функцией Настраиваемое создание.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="5b9ad-110">Если вы планируете опубликовать облачную службу из Visual Studio Team Services (VSTS), воспользуйтесь функцией «Быстрое создание», а затем настройте публикацию VSTS на странице «Быстрый запуск» Azure или на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from the Azure Quickstart or the dashboard.</span></span> <span data-ttu-id="5b9ad-111">Дополнительные сведения см. в статье [Непрерывная доставка в Azure с использованием Visual Studio Team Services][TFSTutorialForCloudService], а также в справке для страницы **Быстрый запуск**.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-111">For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for the **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="5b9ad-112">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="5b9ad-112">Concepts</span></span>
<span data-ttu-id="5b9ad-113">Для развертывания приложения в качестве облачной службы в Azure необходимы три компонента:</span><span class="sxs-lookup"><span data-stu-id="5b9ad-113">Three components are required to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="5b9ad-114">**Определение службы.**</span><span class="sxs-lookup"><span data-stu-id="5b9ad-114">**Service Definition**</span></span>  
  <span data-ttu-id="5b9ad-115">Файл определения облачной службы с расширением CSDEF, в котором определяется модель службы, включая число ролей.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="5b9ad-116">**Конфигурация службы.**</span><span class="sxs-lookup"><span data-stu-id="5b9ad-116">**Service Configuration**</span></span>  
  <span data-ttu-id="5b9ad-117">Файл с расширением CSCFG, в котором задаются значения для любых параметров конфигурации облачной службы и отдельных ролей, включая число экземпляров ролей.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="5b9ad-118">**Пакет службы.**</span><span class="sxs-lookup"><span data-stu-id="5b9ad-118">**Service Package**</span></span>  
  <span data-ttu-id="5b9ad-119">Пакет службы (с расширением CSPKG) содержит код и конфигурации приложений, а также файл определения службы.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="5b9ad-120">Дополнительные сведения об этих компонентах и создании пакета см. [здесь](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="5b9ad-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="5b9ad-121">Подготовка приложения</span><span class="sxs-lookup"><span data-stu-id="5b9ad-121">Prepare your app</span></span>
<span data-ttu-id="5b9ad-122">Перед развертыванием облачной службы необходимо создать пакет облачной службы (CSPKG-файл) на основе кода приложения и файл конфигурации облачной службы (CSCFG).</span><span class="sxs-lookup"><span data-stu-id="5b9ad-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="5b9ad-123">Инструменты для подготовки необходимых файлов развертывания находятся в пакете SDK для Azure.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-123">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="5b9ad-124">Этот пакет можно установить со страницы [Загрузки Azure](https://azure.microsoft.com/downloads/) на языке, выбранном для разработки кода приложения.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="5b9ad-125">Перед экспортом пакета службы необходимо отдельно настроить три компонента облачной службы:</span><span class="sxs-lookup"><span data-stu-id="5b9ad-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="5b9ad-126">Если в развертываемой облачной службе будет применяться SSL-шифрование данных, [настройте приложение](cloud-services-configure-ssl-certificate-portal.md#modify) для поддержки SSL.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="5b9ad-127">Если будут использоваться подключения к удаленному рабочему столу для экземпляров роли, [настройте роли](cloud-services-role-enable-remote-desktop-new-portal.md) для удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="5b9ad-128">Чтобы включить подробный мониторинг для веб-службы, настройте для нее систему диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-128">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="5b9ad-129">*Минимальный мониторинг* (по умолчанию) реализуется на основе счетчиков производительности основной операционной системы, собирающих данные для экземпляров ролей (виртуальные машины).</span><span class="sxs-lookup"><span data-stu-id="5b9ad-129">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="5b9ad-130">*В рамках подробного мониторинга* для более тщательного анализа проблем обработки приложений отслеживаются дополнительные метрики в экземплярах ролей.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-130">*Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="5b9ad-131">Дополнительные сведения о включении диагностики в Azure см. в статье [Включение системы диагностики Azure в облачных службах Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5b9ad-131">To find out how to enable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="5b9ad-132">Чтобы создать облачную службу с развертыванием веб-ролей или рабочих ролей, необходимо [создать соответствующий пакет службы](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="5b9ad-132">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5b9ad-133">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="5b9ad-133">Before you begin</span></span>
* <span data-ttu-id="5b9ad-134">Если пакет SDK для Azure не установлен, щелкните **Install Azure SDK** (Установить пакет Azure SDK). Откроется [страница загрузок Azure](https://azure.microsoft.com/downloads/), откуда можно скачать пакет SDK для языка, выбранного для разработки кода приложения.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-134">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="5b9ad-135">(Также это можно сделать позднее.)</span><span class="sxs-lookup"><span data-stu-id="5b9ad-135">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="5b9ad-136">Для экземпляров роли с сертификатами создайте сертификаты.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-136">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="5b9ad-137">В облачных службах используется PFX-файл с закрытым ключом.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="5b9ad-138">Сертификаты можно отправить в Azure при создании или развертывании облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-138">You can upload the certificates to Azure as you create and deploy the cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="5b9ad-139">Создание и развертывание</span><span class="sxs-lookup"><span data-stu-id="5b9ad-139">Create and deploy</span></span>
1. <span data-ttu-id="5b9ad-140">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5b9ad-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5b9ad-141">Щелкните **Создать > Вычисления**, затем прокрутите вниз и щелкните **Облачная служба**.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-141">Click **New > Compute**, and then scroll down to and click **Cloud Service**.</span></span>

    ![Публикация облачной службы](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="5b9ad-143">В колонке новой **облачной службы** введите **DNS-имя**.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-143">In the new **Cloud Service** blade, enter a value for the **DNS name**.</span></span>
4. <span data-ttu-id="5b9ad-144">Создайте новую **группу ресурсов** или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="5b9ad-145">Выберите **расположение**.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-145">Select a **Location**.</span></span>
6. <span data-ttu-id="5b9ad-146">Щелкните **Пакет**.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-146">Click **Package**.</span></span> <span data-ttu-id="5b9ad-147">Откроется колонка **Отправить пакет** .</span><span class="sxs-lookup"><span data-stu-id="5b9ad-147">This will open the **Upload a package** blade.</span></span> <span data-ttu-id="5b9ad-148">Заполните обязательные поля.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-148">Fill in the required fields.</span></span> <span data-ttu-id="5b9ad-149">Если какая-либо из ролей содержит отдельный экземпляр, убедитесь, что установлен флажок **Развернуть, даже если одна или несколько ролей содержат отдельный экземпляр** .</span><span class="sxs-lookup"><span data-stu-id="5b9ad-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="5b9ad-150">Убедитесь, что установлен флажок **Запустить развертывание** .</span><span class="sxs-lookup"><span data-stu-id="5b9ad-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="5b9ad-151">Нажмите кнопку **ОК**. После этого колонка **Отправить пакет** закроется.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-151">Click **OK** which will close the **Upload a package** blade.</span></span>
9. <span data-ttu-id="5b9ad-152">Если у вас нет сертификатов, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-152">If you do not have any certificates to add, click **Create**.</span></span>

    ![Публикация облачной службы](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="5b9ad-154">Загрузить сертификат</span><span class="sxs-lookup"><span data-stu-id="5b9ad-154">Upload a certificate</span></span>
<span data-ttu-id="5b9ad-155">Если пакет развертывания был [настроен для использования сертификатов](cloud-services-configure-ssl-certificate-portal.md#modify), теперь можно передать сертификат.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-155">If your deployment package was [configured to use certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload the certificate now.</span></span>

1. <span data-ttu-id="5b9ad-156">Выберите **Сертификаты** и в колонке **Добавить сертификаты** выберите PFX-файл SSL-сертификата и укажите **пароль** сертификата.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-156">Select **Certificates**, and on the **Add certificates** blade, select the SSL certificate .pfx file, and then provide the **Password** for the certificate,</span></span>
2. <span data-ttu-id="5b9ad-157">Щелкните **Присоединить сертификат** и нажмите кнопку **ОК** в колонке **Добавить сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-157">Click **Attach certificate**, and then click **OK** on the **Add certificates** blade.</span></span>
3. <span data-ttu-id="5b9ad-158">Щелкните **Создать** в колонке **Облачная служба**.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-158">Click **Create** on the **Cloud Service** blade.</span></span> <span data-ttu-id="5b9ad-159">Когда развертывание получит статус **Готово** можно выполнять следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-159">When the deployment has reached the **Ready** status, you can proceed to the next steps.</span></span>

    ![Публикация облачной службы](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="5b9ad-161">Проверка успешного завершения развертывания</span><span class="sxs-lookup"><span data-stu-id="5b9ad-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="5b9ad-162">Щелкните экземпляр облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-162">Click the cloud service instance.</span></span>

    <span data-ttu-id="5b9ad-163">В строке состояния должна отображаться информация о том, что служба **Запущена**.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-163">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="5b9ad-164">В разделе **Основное** щелкните **URL-адрес сайта**, чтобы открыть облачную службу в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="5b9ad-164">Under **Essentials**, click the **Site URL** to open your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="5b9ad-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5b9ad-166">Next steps</span></span>
* <span data-ttu-id="5b9ad-167">[Общая настройка облачной службы](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5b9ad-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="5b9ad-168">Настройка [пользовательского имени домена](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5b9ad-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="5b9ad-169">[Управление облачной службой](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5b9ad-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="5b9ad-170">Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5b9ad-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
