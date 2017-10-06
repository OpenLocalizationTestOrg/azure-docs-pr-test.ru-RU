---
title: "API (Python) — руководство по функциям управления службами hello toouse aaaHow"
description: "Узнайте, как tooprogrammatically выполнять общие задачи управления службы из Python."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a><span data-ttu-id="788a1-103">Как toouse управления службами с Python</span><span class="sxs-lookup"><span data-stu-id="788a1-103">How toouse Service Management from Python</span></span>
<span data-ttu-id="788a1-104">В этом руководстве показано, как tooprogrammatically выполнять общие задачи управления службы из Python.</span><span class="sxs-lookup"><span data-stu-id="788a1-104">This guide shows you how tooprogrammatically perform common service management tasks from Python.</span></span> <span data-ttu-id="788a1-105">Hello **ServiceManagementService** класса в hello [Azure SDK для Python](https://github.com/Azure/azure-sdk-for-python) поддерживает программный доступ toomuch hello службы связанных с управлением функциональных возможностей, доступных в hello [Классический портал azure] [ management-portal] (такие как **создание, обновление и удаление облачных служб, развертывания, службы управления данными и виртуальные машины**).</span><span class="sxs-lookup"><span data-stu-id="788a1-105">hello **ServiceManagementService** class in hello [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access toomuch of hello service management-related functionality that is available in hello [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="788a1-106">Эту функцию можно использовать для построения приложений, требующих управления tooservice программный доступ.</span><span class="sxs-lookup"><span data-stu-id="788a1-106">This functionality can be useful in building applications that need programmatic access tooservice management.</span></span>

## <span data-ttu-id="788a1-107"><a name="WhatIs"> </a>Что такое управление службами</span><span class="sxs-lookup"><span data-stu-id="788a1-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="788a1-108">Hello API управления службами предоставляет программный доступ toomuch функций службы управления hello через hello [классический портал Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="788a1-108">hello Service Management API provides programmatic access toomuch of hello service management functionality available through hello [Azure classic portal][management-portal].</span></span> <span data-ttu-id="788a1-109">Hello Azure SDK для Python позволяет toomanage облачных служб и учетных записей хранилища.</span><span class="sxs-lookup"><span data-stu-id="788a1-109">hello Azure SDK for Python allows you toomanage your cloud services and storage accounts.</span></span>

<span data-ttu-id="788a1-110">API управления службами hello toouse требуется слишком[создать учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="788a1-110">toouse hello Service Management API, you need too[create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="788a1-111"><a name="Concepts"> </a>Основные понятия</span><span class="sxs-lookup"><span data-stu-id="788a1-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="788a1-112">Hello Azure SDK для Python упаковывает hello [API управления службами Azure][svc-mgmt-rest-api], который представляет собой API REST.</span><span class="sxs-lookup"><span data-stu-id="788a1-112">hello Azure SDK for Python wraps hello [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="788a1-113">Все операции API выполняются по SSL и проходят взаимную проверку подлинности с использованием сертификатов X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="788a1-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="788a1-114">Служба управления Hello может осуществляться из службы, работающей в Azure, или непосредственно через hello Интернет из любого приложения, способного отправить HTTPS-запрос и получить HTTPS-ответ.</span><span class="sxs-lookup"><span data-stu-id="788a1-114">hello management service may be accessed from within a service running in Azure, or directly over hello Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="788a1-115"><a name="Installation"> </a>Установка</span><span class="sxs-lookup"><span data-stu-id="788a1-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="788a1-116">Доступны все функции hello, описанных в этой статье в hello `azure-servicemanagement-legacy` пакет, который можно установить с помощью PIP-адрес.</span><span class="sxs-lookup"><span data-stu-id="788a1-116">All hello features described in this article are available in hello `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="788a1-117">Дополнительные сведения об установке (например, при наличии нового tooPython) см. в этой статье: [Установка Python и hello Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="788a1-117">For more information about installation (for example, if you are new tooPython), see this article: [Installing Python and hello Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="788a1-118"><a name="Connect"></a>Как: подключение tooservice management</span><span class="sxs-lookup"><span data-stu-id="788a1-118"><a name="Connect"> </a>How to: Connect tooservice management</span></span>
<span data-ttu-id="788a1-119">Конечная точка службы управления toohello tooconnect, требуются идентификатор подписки Azure и действительный сертификат управления.</span><span class="sxs-lookup"><span data-stu-id="788a1-119">tooconnect toohello Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="788a1-120">Вы можете получить идентификатор подписки через hello [классический портал Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="788a1-120">You can obtain your subscription ID through hello [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="788a1-121">Теперь стало возможно toouse сертификаты, созданные с помощью OpenSSL, при работе в Windows.</span><span class="sxs-lookup"><span data-stu-id="788a1-121">It is now possible toouse certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="788a1-122">Для этого требуется Python 2.7.4 или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="788a1-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="788a1-123">Корпорация Майкрософт рекомендует пользователям toouse OpenSSL вместо PFX-файл, учитывая, что поддержка для PFX-файл, скорее всего сертификаты будут удалены в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="788a1-123">We recommend users toouse OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in hello future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="788a1-124">Сертификаты управления в Windows/Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="788a1-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="788a1-125">Можно использовать [OpenSSL](http://www.openssl.org/) toocreate своего сертификата управления.</span><span class="sxs-lookup"><span data-stu-id="788a1-125">You can use [OpenSSL](http://www.openssl.org/) toocreate your management certificate.</span></span>  <span data-ttu-id="788a1-126">Действительно нужны два сертификата toocreate, один для сервера hello ( `.cer` файл) и один для клиента hello ( `.pem` файла).</span><span class="sxs-lookup"><span data-stu-id="788a1-126">You actually need toocreate two certificates, one for hello server (a `.cer` file) and one for hello client (a `.pem` file).</span></span> <span data-ttu-id="788a1-127">toocreate hello `.pem` файл, выполните:</span><span class="sxs-lookup"><span data-stu-id="788a1-127">toocreate hello `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="788a1-128">toocreate hello `.cer` сертификатов, выполните:</span><span class="sxs-lookup"><span data-stu-id="788a1-128">toocreate hello `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="788a1-129">Дополнительные сведения о сертификатах Azure см. в статье [Общие сведения о сертификатах для облачных служб Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="788a1-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="788a1-130">Полное описание параметров OpenSSL документации hello в [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="788a1-130">For a complete description of OpenSSL parameters, see hello documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="788a1-131">После создания этих файлов необходимо tooupload hello `.cer` файл tooAzure с помощью действия «Отправка» hello вкладка «Параметры» hello hello [классический портал Azure][management-portal], и необходимо записать toomake где был сохранен hello `.pem` файла.</span><span class="sxs-lookup"><span data-stu-id="788a1-131">After you have created these files, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal], and you need toomake note of where you saved hello `.pem` file.</span></span>

<span data-ttu-id="788a1-132">После получения Идентификатором подписки, сертификат создан и загружен hello `.cer` tooAzure файл конечную toohello управления Azure можно соединить, передавая идентификатор подписки hello и hello путь toohello `.pem` файл слишком**ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="788a1-132">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello path toohello `.pem` file too**ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="788a1-133">В предыдущих примере hello `sms` — **ServiceManagementService** объекта.</span><span class="sxs-lookup"><span data-stu-id="788a1-133">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="788a1-134">Hello **ServiceManagementService** класса — основной класс, используемый toomanage hello служб Azure.</span><span class="sxs-lookup"><span data-stu-id="788a1-134">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="788a1-135">Управление сертификатами в Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="788a1-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="788a1-136">Вы можете создать самозаверяющий сертификат управления на своем компьютере с помощью программы `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="788a1-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="788a1-137">Откройте **командную строку Visual Studio** как **администратора** и использовать hello следующую команду, заменив *AzureCertificate* с именем сертификата hello хотелось бы toouse.</span><span class="sxs-lookup"><span data-stu-id="788a1-137">Open a **Visual Studio command prompt** as an **administrator** and use hello following command, replacing *AzureCertificate* with hello certificate name you would like toouse.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="788a1-138">Команда Hello создает hello `.cer` файл и помещает его в hello **личных** хранилище сертификатов.</span><span class="sxs-lookup"><span data-stu-id="788a1-138">hello command creates hello `.cer` file, and installs it in hello **Personal** certificate store.</span></span> <span data-ttu-id="788a1-139">Дополнительные сведения см. в статье [Общие сведения о сертификатах для облачных служб Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="788a1-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="788a1-140">После создания сертификата hello требуется tooupload hello `.cer` файл tooAzure с помощью действия «Отправка» hello вкладка «Параметры» hello hello [классический портал Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="788a1-140">After you have created hello certificate, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="788a1-141">После получения Идентификатором подписки, сертификат создан и загружен hello `.cer` tooAzure файл toohello конечную управления Azure можно соединить, передавая идентификатор подписки hello и hello расположение сертификата hello в вашей **Личные** хранилище сертификатов слишком**ServiceManagementService** (опять же, замените *AzureCertificate* с именем hello сертификата):</span><span class="sxs-lookup"><span data-stu-id="788a1-141">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello location of hello certificate in your **Personal** certificate store too**ServiceManagementService** (again, replace *AzureCertificate* with hello name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="788a1-142">В предыдущих примере hello `sms` — **ServiceManagementService** объекта.</span><span class="sxs-lookup"><span data-stu-id="788a1-142">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="788a1-143">Hello **ServiceManagementService** класса — основной класс, используемый toomanage hello служб Azure.</span><span class="sxs-lookup"><span data-stu-id="788a1-143">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

## <span data-ttu-id="788a1-144"><a name="ListAvailableLocations"> </a>Практическое руководство. Отображение списка доступных расположений</span><span class="sxs-lookup"><span data-stu-id="788a1-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="788a1-145">toolist hello расположений, доступных для размещения служб, использовать hello **списка\_расположения** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-145">toolist hello locations that are available for hosting services, use hello **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="788a1-146">При создании облачной службы или службы хранилища необходимо tooprovide допустимое расположение.</span><span class="sxs-lookup"><span data-stu-id="788a1-146">When you create a cloud service or storage service you need tooprovide a valid location.</span></span> <span data-ttu-id="788a1-147">Hello **списка\_расположения** метод всегда возвращает текущий список доступных расположений hello.</span><span class="sxs-lookup"><span data-stu-id="788a1-147">hello **list\_locations** method always returns an up-to-date list of hello currently available locations.</span></span> <span data-ttu-id="788a1-148">На момент написания этой статьи приведены hello доступных расположений.</span><span class="sxs-lookup"><span data-stu-id="788a1-148">As of this writing, hello available locations are:</span></span>

* <span data-ttu-id="788a1-149">Западная Европа</span><span class="sxs-lookup"><span data-stu-id="788a1-149">West Europe</span></span>
* <span data-ttu-id="788a1-150">Северная Европа</span><span class="sxs-lookup"><span data-stu-id="788a1-150">North Europe</span></span>
* <span data-ttu-id="788a1-151">Юго-Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="788a1-151">Southeast Asia</span></span>
* <span data-ttu-id="788a1-152">Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="788a1-152">East Asia</span></span>
* <span data-ttu-id="788a1-153">Центральный регион США</span><span class="sxs-lookup"><span data-stu-id="788a1-153">Central US</span></span>
* <span data-ttu-id="788a1-154">Северо-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="788a1-154">North Central US</span></span>
* <span data-ttu-id="788a1-155">Южно-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="788a1-155">South Central US</span></span>
* <span data-ttu-id="788a1-156">Запад США</span><span class="sxs-lookup"><span data-stu-id="788a1-156">West US</span></span>
* <span data-ttu-id="788a1-157">Восток США</span><span class="sxs-lookup"><span data-stu-id="788a1-157">East US</span></span>
* <span data-ttu-id="788a1-158">Восточная часть Японии</span><span class="sxs-lookup"><span data-stu-id="788a1-158">Japan East</span></span>
* <span data-ttu-id="788a1-159">Западная часть Японии</span><span class="sxs-lookup"><span data-stu-id="788a1-159">Japan West</span></span>
* <span data-ttu-id="788a1-160">Южная Бразилия</span><span class="sxs-lookup"><span data-stu-id="788a1-160">Brazil South</span></span>
* <span data-ttu-id="788a1-161">Восточная часть Австралии</span><span class="sxs-lookup"><span data-stu-id="788a1-161">Australia East</span></span>
* <span data-ttu-id="788a1-162">Юго-Восточная часть Австралии</span><span class="sxs-lookup"><span data-stu-id="788a1-162">Australia Southeast</span></span>

## <span data-ttu-id="788a1-163"><a name="CreateCloudService"> </a>Практическое руководство. Создание облачной службы</span><span class="sxs-lookup"><span data-stu-id="788a1-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="788a1-164">При создании приложения и запустите его в Azure, hello код и конфигурация вместе называются Azure [облачная служба] [ cloud service] (известный как *размещенной службы* в более ранних версий Выпуски Azure).</span><span class="sxs-lookup"><span data-stu-id="788a1-164">When you create an application and run it in Azure, hello code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="788a1-165">Hello **создания\_размещенных\_службы** метод позволяет toocreate новую размещенную службу, указав имя размещенной службы (которое должно быть уникальным в Azure), метки (автоматически кодировке toobase64) Описание и расположение.</span><span class="sxs-lookup"><span data-stu-id="788a1-165">hello **create\_hosted\_service** method allows you toocreate a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded toobase64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="788a1-166">Вы можете вывести список всех hello размещенных служб для вашей подписки с hello **списка\_размещенных\_служб** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-166">You can list all hello hosted services for your subscription with hello **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="788a1-167">Если требуется tooget сведения о конкретной размещенной службы, это можно сделать, передав имя toohello hello размещенной службы **получить\_размещенных\_службы\_свойства** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-167">If you want tooget information about a particular hosted service, you can do so by passing hello hosted service name toohello **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="788a1-168">После создания облачной службы можно развернуть службы toohello кода с hello **создания\_развертывания** метод.</span><span class="sxs-lookup"><span data-stu-id="788a1-168">After you have created a cloud service, you can deploy your code toohello service with hello **create\_deployment** method.</span></span>

## <span data-ttu-id="788a1-169"><a name="DeleteCloudService"> </a>Практическое руководство. Удаление облачной службы</span><span class="sxs-lookup"><span data-stu-id="788a1-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="788a1-170">Можно удалить облачную службу, передавая имя toohello hello службы **удаление\_размещенных\_службы** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-170">You can delete a cloud service by passing hello service name toohello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="788a1-171">Прежде чем можно будет удалить службу, необходимо сначала удалить все развертывания для службы hello.</span><span class="sxs-lookup"><span data-stu-id="788a1-171">Before you can delete a service, all deployments for hello service must first be deleted.</span></span> <span data-ttu-id="788a1-172">(Дополнительные сведения см. в разделе [Практическое руководство. Удаление развертывания](#DeleteDeployment).)</span><span class="sxs-lookup"><span data-stu-id="788a1-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="788a1-173"><a name="DeleteDeployment"> </a>Практическое руководство. Удаление развертывания</span><span class="sxs-lookup"><span data-stu-id="788a1-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="788a1-174">toodelete развертывания, используйте hello **удаление\_развертывания** метод.</span><span class="sxs-lookup"><span data-stu-id="788a1-174">toodelete a deployment, use hello **delete\_deployment** method.</span></span> <span data-ttu-id="788a1-175">Hello следующем примере показано как toodelete развертывания с именем `v1`.</span><span class="sxs-lookup"><span data-stu-id="788a1-175">hello following example shows how toodelete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="788a1-176"><a name="CreateStorageService"> </a>Практическое руководство. Создание службы хранилища</span><span class="sxs-lookup"><span data-stu-id="788a1-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="788a1-177">Объект [службы хранилища](../storage/common/storage-create-storage-account.md) предоставляет вам доступ tooAzure [большие двоичные объекты](../storage/blobs/storage-python-how-to-use-blob-storage.md), [таблиц](../cosmos-db/table-storage-how-to-use-python.md), и [очереди](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="788a1-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="788a1-178">toocreate службы хранилища, необходимо имя для службы hello (от 3 до 24 символов нижнего регистра и уникальным в пределах Azure), описание, метку (вверх too100 символов, автоматически кодировке toobase64) и расположение.</span><span class="sxs-lookup"><span data-stu-id="788a1-178">toocreate a storage service, you need a name for hello service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up too100 characters, automatically encoded toobase64), and a location.</span></span> <span data-ttu-id="788a1-179">Hello в следующем примере показано, как службы toocreate хранилища, указав местоположение.</span><span class="sxs-lookup"><span data-stu-id="788a1-179">hello following example shows how toocreate a storage service by specifying a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="788a1-180">Обратите внимание, в предыдущих пример hello состояния hello hello **создания\_хранения\_учетной записи** операции можно получить, передав hello результата, возвращаемого методом **создания\_хранилища \_учетной записи** toohello **получить\_операции\_состояние** метод.</span><span class="sxs-lookup"><span data-stu-id="788a1-180">Note in hello preceding example that hello status of hello **create\_storage\_account** operation can be retrieved by passing hello result returned by **create\_storage\_account** toohello **get\_operation\_status** method.</span></span>  

<span data-ttu-id="788a1-181">Можно составить список учетных записей хранилища и их свойства с hello **списка\_хранения\_учетные записи** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-181">You can list your storage accounts and their properties with hello **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="788a1-182"><a name="DeleteStorageService"> </a>Практическое руководство. Удаление службы хранилища</span><span class="sxs-lookup"><span data-stu-id="788a1-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="788a1-183">Служба хранилища можно удалить, передав toohello имя службы хранилища hello **удаление\_хранения\_учетной записи** метод.</span><span class="sxs-lookup"><span data-stu-id="788a1-183">You can delete a storage service by passing hello storage service name toohello **delete\_storage\_account** method.</span></span> <span data-ttu-id="788a1-184">Удаление службы хранилища удаляет все данные, хранящиеся в службе hello (больших двоичных объектов, таблиц и очередей).</span><span class="sxs-lookup"><span data-stu-id="788a1-184">Deleting a storage service deletes all data stored in hello service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="788a1-185"><a name="ListOperatingSystems"> </a>Практическое руководство. Список доступных операционных систем</span><span class="sxs-lookup"><span data-stu-id="788a1-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="788a1-186">toolist hello операционных систем, доступных для размещения служб, использовать hello **списка\_операционной\_систем** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-186">toolist hello operating systems that are available for hosting services, use hello **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="788a1-187">Кроме того, можно использовать hello **списка\_операционной\_системы\_семейства** метод, который группирует hello операционных систем семейства:</span><span class="sxs-lookup"><span data-stu-id="788a1-187">Alternatively, you can use hello **list\_operating\_system\_families** method, which groups hello operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="788a1-188"><a name="CreateVMImage"> </a>Практическое руководство. Создание образа операционной системы</span><span class="sxs-lookup"><span data-stu-id="788a1-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="788a1-189">tooadd репозиторием изображения toohello образа операционной системы используйте hello **добавить\_ОС\_изображения** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-189">tooadd an operating system image toohello image repository, use hello **add\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="788a1-190">образы операционной системы toolist hello, которые недоступны, используйте hello **списка\_ОС\_изображения** метод.</span><span class="sxs-lookup"><span data-stu-id="788a1-190">toolist hello operating system images that are available, use hello **list\_os\_images** method.</span></span> <span data-ttu-id="788a1-191">Сюда входят все образы платформ и пользовательские образы.</span><span class="sxs-lookup"><span data-stu-id="788a1-191">It includes all platform images and user images:</span></span>

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <span data-ttu-id="788a1-192"><a name="DeleteVMImage"> </a>Практическое руководство. Удаление образа операционной системы</span><span class="sxs-lookup"><span data-stu-id="788a1-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="788a1-193">toodelete пользовательский образ, используйте hello **удаление\_ОС\_изображения** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-193">toodelete a user image, use hello **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="788a1-194"><a name="CreateVM"> </a>Практическое руководство. Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="788a1-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="788a1-195">toocreate виртуальной машины, необходимо сначала toocreate [облачная служба](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="788a1-195">toocreate a virtual machine, you first need toocreate a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="788a1-196">Затем создайте hello развертывания виртуальной машины, с помощью hello **создания\_виртуальных\_машины\_развертывания** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-196">Then create hello virtual machine deployment using hello **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <span data-ttu-id="788a1-197"><a name="DeleteVM"> </a>Практическое руководство. Удаление виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="788a1-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="788a1-198">toodelete виртуальной машины, сначала удалите hello развертывания с помощью hello **удаление\_развертывания** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-198">toodelete a virtual machine, you first delete hello deployment using hello **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="788a1-199">Hello облачной службы могут быть удалены с помощью hello **удаление\_размещенных\_службы** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-199">hello cloud service can then be deleted using hello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="788a1-200">Практическое руководство. Создание виртуальной машины из записанного образа виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="788a1-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="788a1-201">toocapture образ ВМ, сначала вызвать метод hello **захвата\_ВМ\_изображения** метод:</span><span class="sxs-lookup"><span data-stu-id="788a1-201">toocapture a VM image, you first call hello **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

<span data-ttu-id="788a1-202">Далее, toomake в том, что успешно захвачены hello образ, используйте hello **списка\_ВМ\_изображения** api и убедитесь, что выбранное изображение отображается в результатах hello:</span><span class="sxs-lookup"><span data-stu-id="788a1-202">Next, toomake sure that you have successfully captured hello image, use hello **list\_vm\_images** api, and make sure your image is displayed in hello results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="788a1-203">toofinally Создание hello виртуальной машины с помощью hello записанный образ, используйте hello **создания\_виртуальных\_машины\_развертывания** как до, но на этот раз передать hello vm_image_name вместо</span><span class="sxs-lookup"><span data-stu-id="788a1-203">toofinally create hello virtual machine using hello captured image, use hello **create\_virtual\_machine\_deployment** method as before, but this time pass in hello vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

<span data-ttu-id="788a1-204">Дополнительные сведения о toolearn toocapture виртуальной машины Linux. в статье [как tooCapture виртуальной машины Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="788a1-204">toolearn more about how toocapture a Linux Virtual Machine, see [How tooCapture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="788a1-205">Дополнительные сведения о toolearn toocapture виртуальной машины Windows. в статье [как tooCapture виртуальной машине.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="788a1-205">toolearn more about how toocapture a Windows Virtual Machine, see [How tooCapture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="788a1-206"><a name="What's Next"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="788a1-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="788a1-207">Теперь, когда вы узнали основы hello управления службами, можно получить доступ к hello [полный набор API справочную документацию по hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) и выполнения сложных задач легко toomanage приложения python.</span><span class="sxs-lookup"><span data-stu-id="788a1-207">Now that you've learned hello basics of service management, you can access hello [Complete API reference documentation for hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily toomanage your python application.</span></span>

<span data-ttu-id="788a1-208">Дополнительные сведения см. в разделе hello [центре разработчиков Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="788a1-208">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
