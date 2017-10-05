---
title: "Облачные службы и сертификаты управления | Документация Майкрософт"
description: "Узнайте, как создавать и использовать сертификаты с помощью Microsoft Azure"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: f760bfd93b19c43d12889b5dd38015c5eba0a8ac
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a><span data-ttu-id="87517-103">Общие сведения о сертификатах для облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="87517-103">Certificates overview for Azure Cloud Services</span></span>
<span data-ttu-id="87517-104">Сертификаты используются в Azure для облачных служб ([сертификаты службы](#what-are-service-certificates)), а также для проверки подлинности с помощью API управления ([сертификаты управления](#what-are-management-certificates) при использовании классического портала Azure, а не портала более новой версии).</span><span class="sxs-lookup"><span data-stu-id="87517-104">Certificates are used in Azure for cloud services ([service certificates](#what-are-service-certificates)) and for authenticating with the management API ([management certificates](#what-are-management-certificates) when using the Azure classic portal and not the non-classic Azure portal).</span></span> <span data-ttu-id="87517-105">В этой статье приводится общий обзор этих двух типов сертификатов, а также описывается процесс их [создания](#create) и [развертывания](#deploy) в Azure.</span><span class="sxs-lookup"><span data-stu-id="87517-105">This topic gives a general overview of both certificate types, how to [create](#create) and [deploy](#deploy) them to Azure.</span></span>

<span data-ttu-id="87517-106">Сертификаты, используемые в Azure, являются сертификатами x.509 v3; они могут быть заверены другим доверенным сертификатом или быть самозаверяющими.</span><span class="sxs-lookup"><span data-stu-id="87517-106">Certificates used in Azure are x.509 v3 certificates and can be signed by another trusted certificate or they can be self-signed.</span></span> <span data-ttu-id="87517-107">Поскольку самозаверяющий сертификат подписывает его автор, он не считается надежным по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="87517-107">A self-signed certificate is signed by its own creator, therefore it is not trusted by default.</span></span> <span data-ttu-id="87517-108">Большинство браузеров может игнорировать эту проблему.</span><span class="sxs-lookup"><span data-stu-id="87517-108">Most browsers can ignore this problem.</span></span> <span data-ttu-id="87517-109">Самозаверяющие сертификаты должны использоваться только при разработке и тестировании облачных служб.</span><span class="sxs-lookup"><span data-stu-id="87517-109">You should only use self-signed certificates when developing and testing your cloud services.</span></span> 

<span data-ttu-id="87517-110">Сертификаты, используемые в Azure, могут содержать закрытый или открытый ключ.</span><span class="sxs-lookup"><span data-stu-id="87517-110">Certificates used by Azure can contain a private or a public key.</span></span> <span data-ttu-id="87517-111">Сертификаты имеют отпечаток, служащий для их однозначной идентификации.</span><span class="sxs-lookup"><span data-stu-id="87517-111">Certificates have a thumbprint that provides a means to identify them in an unambiguous way.</span></span> <span data-ttu-id="87517-112">Этот отпечаток включен в [файл конфигурации](cloud-services-configure-ssl-certificate.md) Azure для определения сертификата, который будет использоваться облачной службой.</span><span class="sxs-lookup"><span data-stu-id="87517-112">This thumbprint is used in the Azure [configuration file](cloud-services-configure-ssl-certificate.md) to identify which certificate a cloud service should use.</span></span> 

## <a name="what-are-service-certificates"></a><span data-ttu-id="87517-113">Что такое сертификаты службы</span><span class="sxs-lookup"><span data-stu-id="87517-113">What are service certificates?</span></span>
<span data-ttu-id="87517-114">Сертификаты службы присоединяются к облачным службам, обеспечивая безопасное взаимодействие со службой.</span><span class="sxs-lookup"><span data-stu-id="87517-114">Service certificates are attached to cloud services and enable secure communication to and from the service.</span></span> <span data-ttu-id="87517-115">Например, при развертывании веб-роли вам нужно указать сертификат, который может выполнять проверку подлинности доступной конечной точки HTTPS.</span><span class="sxs-lookup"><span data-stu-id="87517-115">For example, if you deployed a web role, you would want to supply a certificate that can authenticate an exposed HTTPS endpoint.</span></span> <span data-ttu-id="87517-116">Сертификаты службы, определенные в определении службы, автоматически развертываются в виртуальной машине с запущенным экземпляром роли.</span><span class="sxs-lookup"><span data-stu-id="87517-116">Service certificates, defined in your service definition, are automatically deployed to the virtual machine that is running an instance of your role.</span></span> 

<span data-ttu-id="87517-117">Сертификаты службы можно передать на классический портал Azure с помощью этого портала или классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="87517-117">You can upload service certificates to Azure classic portal either using the Azure classic portal or by using the classic deployment model.</span></span> <span data-ttu-id="87517-118">Эти сертификаты связаны с конкретной облачной службой.</span><span class="sxs-lookup"><span data-stu-id="87517-118">Service certificates are associated with a specific cloud service.</span></span> <span data-ttu-id="87517-119">Они назначаются для развертывания в файле определения службы.</span><span class="sxs-lookup"><span data-stu-id="87517-119">They are assigned to a deployment in the service definition file.</span></span>

<span data-ttu-id="87517-120">Сертификатами службы можно управлять отдельно от служб. Это могут делать разные пользователи.</span><span class="sxs-lookup"><span data-stu-id="87517-120">Service certificates can be managed separately from your services, and may be managed by different individuals.</span></span> <span data-ttu-id="87517-121">Например, разработчик может передать пакет служб, который ссылается на сертификат, ранее загруженный ИТ-менеджером в Azure.</span><span class="sxs-lookup"><span data-stu-id="87517-121">For example, a developer may upload a service package that refers to a certificate that an IT manager has previously uploaded to Azure.</span></span> <span data-ttu-id="87517-122">ИТ-менеджер может управлять сертификатом, а также обновлять его (изменяя конфигурацию службы) без необходимости загрузки нового пакета службы.</span><span class="sxs-lookup"><span data-stu-id="87517-122">An IT manager can manage and renew that certificate (changing the configuration of the service) without needing to upload a new service package.</span></span> <span data-ttu-id="87517-123">Такое обновление возможно, поскольку логическое имя сертификата, а также имя хранилища и расположение сертификата указаны в файле определения службы, а отпечаток сертификата указан в файле конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="87517-123">Updating without a new service package is possible because the logical name, store name, and location of the certificate is in the service definition file and while the certificate thumbprint is specified in the service configuration file.</span></span> <span data-ttu-id="87517-124">Чтобы обновить сертификат, необходимо просто загрузить новый сертификат и изменить значение отпечатка в файле конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="87517-124">To update the certificate, it's only necessary to upload a new certificate and change the thumbprint value in the service configuration file.</span></span>

>[!Note]
><span data-ttu-id="87517-125">Статья [Часто задаваемые вопросы об облачных службах](cloud-services-faq.md) содержит полезную информацию о сертификатах.</span><span class="sxs-lookup"><span data-stu-id="87517-125">The [Cloud Services FAQ](cloud-services-faq.md) article has some helpful information about certificates.</span></span>

## <a name="what-are-management-certificates"></a><span data-ttu-id="87517-126">Что такое сертификаты управления</span><span class="sxs-lookup"><span data-stu-id="87517-126">What are management certificates?</span></span>
<span data-ttu-id="87517-127">Сертификаты управления позволяют выполнять проверку подлинности с помощью классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="87517-127">Management certificates allow you to authenticate with the classic deployment model.</span></span> <span data-ttu-id="87517-128">Многие программы и инструменты (например, Visual Studio или пакет SDK Azure) будут использовать эти сертификаты для автоматизации настройки и развертывания разных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="87517-128">Many programs and tools (such as Visual Studio or the Azure SDK) use these certificates to automate configuration and deployment of various Azure services.</span></span> <span data-ttu-id="87517-129">Фактически они не связаны с облачными службами.</span><span class="sxs-lookup"><span data-stu-id="87517-129">These are not really related to cloud services.</span></span> 

> [!WARNING]
> <span data-ttu-id="87517-130">Будьте осторожны!</span><span class="sxs-lookup"><span data-stu-id="87517-130">Be careful!</span></span> <span data-ttu-id="87517-131">Эти типы сертификатов позволяют каждому, кто прошел проверку подлинности, управлять подпиской, с которой они связаны.</span><span class="sxs-lookup"><span data-stu-id="87517-131">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span></span> 
> 
> 

### <a name="limitations"></a><span data-ttu-id="87517-132">Ограничения</span><span class="sxs-lookup"><span data-stu-id="87517-132">Limitations</span></span>
<span data-ttu-id="87517-133">Существует ограничение в 100 сертификатов управления на одну подписку.</span><span class="sxs-lookup"><span data-stu-id="87517-133">There is a limit of 100 management certificates per subscription.</span></span> <span data-ttu-id="87517-134">Существует ограничение в 100 сертификатов управления для всех подписок в рамках конкретного идентификатора пользователя администратора службы.</span><span class="sxs-lookup"><span data-stu-id="87517-134">There is also a limit of 100 management certificates for all subscriptions under a specific service administrator’s user ID.</span></span> <span data-ttu-id="87517-135">Если идентификатор пользователя администратора учетной записи уже используется для добавления 100 сертификатов управления и есть потребность в большем количестве сертификатов, можно добавить соадминистратора для добавления дополнительных сертификатов.</span><span class="sxs-lookup"><span data-stu-id="87517-135">If the user ID for the account administrator has already been used to add 100 management certificates and there is a need for more certificates, you can add a co-administrator to add the additional certificates.</span></span> 

<span data-ttu-id="87517-136">Перед добавлением более 100 сертификатов убедитесь, что существующий сертификат можно использовать повторно.</span><span class="sxs-lookup"><span data-stu-id="87517-136">Before adding more than 100 certificates, see if you can reuse an existing certificate.</span></span> <span data-ttu-id="87517-137">Использование соадминистраторов может усложнить процесс управления сертификатами.</span><span class="sxs-lookup"><span data-stu-id="87517-137">Using co-administrators adds potentially unneeded complexity to your certificate management process.</span></span>

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="87517-138">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="87517-138">Create a new self-signed certificate</span></span>
<span data-ttu-id="87517-139">Можно использовать любое доступное средство для создания самозаверяющего сертификата при условии, что оно соответствует следующим параметрам.</span><span class="sxs-lookup"><span data-stu-id="87517-139">You can use any tool available to create a self-signed certificate as long as they adhere to these settings:</span></span>

* <span data-ttu-id="87517-140">Используется сертификат X.509.</span><span class="sxs-lookup"><span data-stu-id="87517-140">An X.509 certificate.</span></span>
* <span data-ttu-id="87517-141">Содержит закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="87517-141">Contains a private key.</span></span>
* <span data-ttu-id="87517-142">Создано для обмена ключами (PFX-файл).</span><span class="sxs-lookup"><span data-stu-id="87517-142">Created for key exchange (.pfx file).</span></span>
* <span data-ttu-id="87517-143">Имя субъекта должно совпадать с именем домена, которое используется для обращения к облачной службе.</span><span class="sxs-lookup"><span data-stu-id="87517-143">Subject name must match the domain used to access the cloud service.</span></span>

    > <span data-ttu-id="87517-144">Вы не можете приобрести SSL-сертификат для домена cloudapp.net (или для любого другого домена, относящегося к Azure), поэтому имя субъекта сертификата должно совпадать с пользовательским именем домена, которое используется для доступа к вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="87517-144">You cannot acquire an SSL certificate for the cloudapp.net (or for any Azure-related) domain; the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="87517-145">Например, **contoso.net**, а не **contoso.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="87517-145">For example, **contoso.net**, not **contoso.cloudapp.net**.</span></span>

* <span data-ttu-id="87517-146">Минимум 2048-разрядное шифрование.</span><span class="sxs-lookup"><span data-stu-id="87517-146">Minimum of 2048-bit encryption.</span></span>
* <span data-ttu-id="87517-147">**Только сертификат службы**: клиентский сертификат должен находиться в *личном* хранилище сертификатов.</span><span class="sxs-lookup"><span data-stu-id="87517-147">**Service Certificate Only**: Client-side certificate must reside in the *Personal* certificate store.</span></span>

<span data-ttu-id="87517-148">Существует два простых способа создания сертификатов в Windows: с помощью служебной программы `makecert.exe` или службы IIS.</span><span class="sxs-lookup"><span data-stu-id="87517-148">There are two easy ways to create a certificate on Windows, with the `makecert.exe` utility, or IIS.</span></span>

### <a name="makecertexe"></a><span data-ttu-id="87517-149">Makecert.exe</span><span class="sxs-lookup"><span data-stu-id="87517-149">Makecert.exe</span></span>
<span data-ttu-id="87517-150">Эта программа устарела и в данном документе не описывается.</span><span class="sxs-lookup"><span data-stu-id="87517-150">This utility has been deprecated and is no longer documented here.</span></span> <span data-ttu-id="87517-151">Дополнительные сведения см. в [этой статье в библиотеке MSDN](https://msdn.microsoft.com/library/windows/desktop/aa386968).</span><span class="sxs-lookup"><span data-stu-id="87517-151">For more information, see [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa386968).</span></span>

### <a name="powershell"></a><span data-ttu-id="87517-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="87517-152">PowerShell</span></span>
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> <span data-ttu-id="87517-153">Если вы хотите использовать сертификат, указав IP-адрес, а не домен, задайте этот IP-адрес в параметре -DnsName.</span><span class="sxs-lookup"><span data-stu-id="87517-153">If you want to use the certificate with an IP address instead of a domain, use the IP address in the -DnsName parameter.</span></span>


<span data-ttu-id="87517-154">Если вы хотите использовать этот [сертификат на портале управления](../azure-api-management-certs.md), экспортируйте его в **CER-файл** .</span><span class="sxs-lookup"><span data-stu-id="87517-154">If you want to use this [certificate with the management portal](../azure-api-management-certs.md), export it to a **.cer** file:</span></span>

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a><span data-ttu-id="87517-155">Internet Information Services (IIS)</span><span class="sxs-lookup"><span data-stu-id="87517-155">Internet Information Services (IIS)</span></span>
<span data-ttu-id="87517-156">В Интернете вы найдете множество информации о том, как это сделать с помощью IIS.</span><span class="sxs-lookup"><span data-stu-id="87517-156">There are many pages on the internet that cover how to do this with IIS.</span></span> <span data-ttu-id="87517-157">[этой странице](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) .</span><span class="sxs-lookup"><span data-stu-id="87517-157">[Here](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) is a great one I found that I think explains it well.</span></span> 

### <a name="java"></a><span data-ttu-id="87517-158">Java</span><span class="sxs-lookup"><span data-stu-id="87517-158">Java</span></span>
<span data-ttu-id="87517-159">Для [создания сертификата](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate)можно использовать Java.</span><span class="sxs-lookup"><span data-stu-id="87517-159">You can use Java to [create a certificate](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).</span></span>

### <a name="linux"></a><span data-ttu-id="87517-160">Linux</span><span class="sxs-lookup"><span data-stu-id="87517-160">Linux</span></span>
<span data-ttu-id="87517-161">В [этой](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) статье рассматривается создание сертификатов с использованием SSH.</span><span class="sxs-lookup"><span data-stu-id="87517-161">[This](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article describes how to create certificates with SSH.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87517-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="87517-162">Next steps</span></span>
<span data-ttu-id="87517-163">[Передайте сертификат вашей службы на классический портал Azure](cloud-services-configure-ssl-certificate.md) (или [на портал Azure](cloud-services-configure-ssl-certificate-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="87517-163">[Upload your service certificate to the Azure classic portal](cloud-services-configure-ssl-certificate.md) (or the [Azure portal](cloud-services-configure-ssl-certificate-portal.md)).</span></span>

<span data-ttu-id="87517-164">Передайте на классический портал Azure [сертификат API управления](../azure-api-management-certs.md) .</span><span class="sxs-lookup"><span data-stu-id="87517-164">Upload a [management API certificate](../azure-api-management-certs.md) to the Azure classic portal.</span></span> <span data-ttu-id="87517-165">Портал Azure не использует сертификаты управления для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="87517-165">The Azure portal does not use management certificates for authentication.</span></span>

