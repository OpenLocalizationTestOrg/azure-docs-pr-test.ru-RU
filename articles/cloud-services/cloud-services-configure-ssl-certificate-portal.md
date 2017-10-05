---
title: "Настройка SSL для облачной службы | Документация Майкрософт"
description: "Узнайте, как определить конечную точку HTTPS для веб-роли и как передать SSL-сертификат, чтобы обеспечить безопасность приложения. В этих примерах используется портал Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: e5c8c3b098772c0586712305a577b24a6f0d924c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="b3111-104">Настройка SSL для приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="b3111-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3111-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b3111-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="b3111-106">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="b3111-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="b3111-107">SSL-шифрование — это наиболее распространенный метод обеспечения безопасности данных, отправленных через Интернет.</span><span class="sxs-lookup"><span data-stu-id="b3111-107">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="b3111-108">В этой теме, посвященной общим задачам, обсуждается, как определить конечную точку HTTPS для веб-роли и как передать SSL-сертификат, чтобы обеспечить безопасность приложения.</span><span class="sxs-lookup"><span data-stu-id="b3111-108">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="b3111-109">Процедуры в этом задании применяются для облачных служб Azure. Информацию о процедурах для служб приложений см. в [этом разделе](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="b3111-109">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="b3111-110">В этой задаче используется рабочее развертывание.</span><span class="sxs-lookup"><span data-stu-id="b3111-110">This task uses a production deployment.</span></span> <span data-ttu-id="b3111-111">Сведения об использовании промежуточного развертывания приведены в конце данного раздела.</span><span class="sxs-lookup"><span data-stu-id="b3111-111">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="b3111-112">Если вы еще не создали облачную службу, сначала прочтите [эту статью](cloud-services-how-to-create-deploy-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="b3111-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="b3111-113">Шаг 1. Получение SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="b3111-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="b3111-114">Чтобы настроить протокол SSL для приложения, сначала необходимо получить SSL-сертификат, подписанный центром сертификации, то есть доверенным сторонним поставщиком, который выдает сертификаты для этой цели.</span><span class="sxs-lookup"><span data-stu-id="b3111-114">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="b3111-115">Если у вас еще нет сертификата, нужно получить его в компании, продающей SSL-сертификаты.</span><span class="sxs-lookup"><span data-stu-id="b3111-115">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="b3111-116">Сертификат должен отвечать следующим требованиям для SSL-сертификатов в Azure:</span><span class="sxs-lookup"><span data-stu-id="b3111-116">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="b3111-117">Сертификат должен содержать закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="b3111-117">The certificate must contain a private key.</span></span>
* <span data-ttu-id="b3111-118">Сертификат должен быть создан для обмена ключами, которые можно экспортировать в файл обмена личной информацией (PFX-файл).</span><span class="sxs-lookup"><span data-stu-id="b3111-118">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="b3111-119">Имя субъекта сертификата должно совпадать с именем домена, которое используется для обращения к облачной службе.</span><span class="sxs-lookup"><span data-stu-id="b3111-119">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="b3111-120">Не удается получить SSL-сертификат от центра сертификации (ЦС) в домене cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="b3111-120">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="b3111-121">Необходимо получить имя пользовательского домена для использования при получении доступа к службе.</span><span class="sxs-lookup"><span data-stu-id="b3111-121">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="b3111-122">При запросе сертификата из ЦС имя субъекта сертификата должно соответствовать имени личного домена, который используется для доступа к вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="b3111-122">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="b3111-123">Например, если вы используете домен **contoso.com**, необходимо запросить сертификат из центра сертификации для ***.contoso.com** или **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b3111-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="b3111-124">Сертификат должен использовать как минимум 2048-разрядное шифрование.</span><span class="sxs-lookup"><span data-stu-id="b3111-124">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="b3111-125">В целях тестирования вы можете [создать](cloud-services-certs-create.md) и использовать самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="b3111-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="b3111-126">Самозаверяющий сертификат не прошел аутентификацию через ЦС, и можно использовать домен cloudapp.net в качестве URL-адреса веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="b3111-126">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="b3111-127">Например, в приведенной ниже задаче используется самозаверяющий сертификат, в котором задано общее имя **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="b3111-127">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="b3111-128">Далее необходимо включить сведения о сертификате в файлы определения службы и конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="b3111-128">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="b3111-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="b3111-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="b3111-130">Шаг 2. Изменение файлов определения службы и конфигурации</span><span class="sxs-lookup"><span data-stu-id="b3111-130">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="b3111-131">Ваше приложение должно быть настроено для использования сертификата и также необходимо добавить конечную точку HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b3111-131">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="b3111-132">Для этого следует обновить файлы определения службы и конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="b3111-132">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="b3111-133">В среде разработки откройте файл определения службы (CSDEF), добавьте раздел **Certificates** внутри раздела **WebRole** и добавьте следующие сведения о сертификате (и промежуточных сертификатах).</span><span class="sxs-lookup"><span data-stu-id="b3111-133">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by the CA root, you
            must include all the intermediate certificates
            here. You must list them here, even if they are
            not bound to any endpoints. Failing to list any of
            the intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="b3111-134">В разделе **Certificates** определяется имя сертификата, его расположение и имя хранилища, в котором он находится.</span><span class="sxs-lookup"><span data-stu-id="b3111-134">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>

   <span data-ttu-id="b3111-135">Разрешениям (атрибуту`permisionLevel`) можно присвоить одно из приведенных ниже значений.</span><span class="sxs-lookup"><span data-stu-id="b3111-135">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>

   | <span data-ttu-id="b3111-136">Значение разрешения</span><span class="sxs-lookup"><span data-stu-id="b3111-136">Permission Value</span></span> | <span data-ttu-id="b3111-137">Описание</span><span class="sxs-lookup"><span data-stu-id="b3111-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="b3111-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="b3111-138">limitedOrElevated</span></span> |<span data-ttu-id="b3111-139">**(По умолчанию).** Все процессы роли могут получить доступ к закрытому ключу.</span><span class="sxs-lookup"><span data-stu-id="b3111-139">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="b3111-140">elevated</span><span class="sxs-lookup"><span data-stu-id="b3111-140">elevated</span></span> |<span data-ttu-id="b3111-141">Доступ к закрытому ключу могут получить только процессы повышенного уровня.</span><span class="sxs-lookup"><span data-stu-id="b3111-141">Only elevated processes can access the private key.</span></span> |

2. <span data-ttu-id="b3111-142">В файле определения службы добавьте элемент **InputEndpoint** в раздел **Endpoints**, чтобы включить протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b3111-142">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="b3111-143">В файле определения службы добавьте элемент **Binding** в раздел **Sites**.</span><span class="sxs-lookup"><span data-stu-id="b3111-143">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="b3111-144">Этот элемент добавляет привязку HTTPS для сопоставления конечной точки с вашим сайтом:</span><span class="sxs-lookup"><span data-stu-id="b3111-144">This element adds an HTTPS binding to map the endpoint to your site:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   <span data-ttu-id="b3111-145">Все необходимые изменения внесены в файл определения службы, но еще нужно добавить сведения о сертификате в сам файл конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="b3111-145">All the required changes to the service definition file have been completed; but, you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="b3111-146">В файле конфигурации службы (CSCFG-файл) ServiceConfiguration.Cloud.cscfg в разделе **Certificates** добавьте значения из своего сертификата.</span><span class="sxs-lookup"><span data-stu-id="b3111-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="b3111-147">Следующий пример кода содержит в разделе **Certificates** все значения, кроме значения thumbprint.</span><span class="sxs-lookup"><span data-stu-id="b3111-147">The following code sample provides details of the **Certificates** section, except for the thumbprint value.</span></span>

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="b3111-148">(В этом примере для алгоритма отпечатка используется обозначение **sha1**.</span><span class="sxs-lookup"><span data-stu-id="b3111-148">(This example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="b3111-149">Укажите соответствующее значение для алгоритма отпечатка своего сертификата.)</span><span class="sxs-lookup"><span data-stu-id="b3111-149">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="b3111-150">Теперь, когда файлы определения службы и конфигурации службы обновлены, создайте пакет развертывания для передачи в Azure.</span><span class="sxs-lookup"><span data-stu-id="b3111-150">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="b3111-151">Если используется **cspack**, не используйте флаг **/generateConfigurationFile**, так как это приведет к перезаписи сведений о сертификате, которые вы только что добавили.</span><span class="sxs-lookup"><span data-stu-id="b3111-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="b3111-152">Шаг 3. Отправка сертификата</span><span class="sxs-lookup"><span data-stu-id="b3111-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="b3111-153">Подключитесь к порталу Azure и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b3111-153">Connect to the Azure portal and...</span></span>

1. <span data-ttu-id="b3111-154">В разделе портала **Все ресурсы** выберите облачную службу.</span><span class="sxs-lookup"><span data-stu-id="b3111-154">In the **All resources** section of the Portal, select your cloud service.</span></span>

    ![Публикация облачной службы](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="b3111-156">Щелкните **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="b3111-156">Click **Certificates**.</span></span>

    ![Щелкните значок «сертификаты»](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="b3111-158">Щелкните **Отправить** в верхней части области сертификатов.</span><span class="sxs-lookup"><span data-stu-id="b3111-158">Click **Upload** at the top of the certificates area.</span></span>

    ![Щелкните элемент "Отправить"](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="b3111-160">Укажите **файл** и **пароль**, а затем нажмите кнопку **Отправить** в нижней части области ввода данных.</span><span class="sxs-lookup"><span data-stu-id="b3111-160">Provide the **File**, **Password**, then click **Upload** at the bottom of the data entry area.</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="b3111-161">Шаг 4. Подключение к экземпляру роли с использованием HTTPS</span><span class="sxs-lookup"><span data-stu-id="b3111-161">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="b3111-162">Теперь, когда развертывание готово и работает в Azure, вы можете подключиться к нему, используя HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b3111-162">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="b3111-163">Щелкните **URL-адрес сайта**, чтобы открыть веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="b3111-163">Click the **Site URL** to open up the web browser.</span></span>

   ![Щелкните URL-адрес сайта](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="b3111-165">В веб-браузере измените ссылку, указав **https** вместо **http**, и перейдите на страницу.</span><span class="sxs-lookup"><span data-stu-id="b3111-165">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b3111-166">Если используется самозаверяющий сертификат, то при переходе к конечной точке HTTPS, связанной с самозаверяющим сертификатом, в браузере может появиться сообщение об ошибке сертификата.</span><span class="sxs-lookup"><span data-stu-id="b3111-166">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="b3111-167">Эту проблему можно устранить, воспользовавшись сертификатом, подписанным доверенным центром сертификации. Пока это не будет сделано, вы можете игнорировать данную ошибку.</span><span class="sxs-lookup"><span data-stu-id="b3111-167">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="b3111-168">(Другой способ — добавить самозаверяющий сертификат в используемое хранилище сертификатов доверенного центра сертификации.)</span><span class="sxs-lookup"><span data-stu-id="b3111-168">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Предварительный просмотр сайта](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="b3111-170">Если вы хотите использовать SSL для промежуточного развертывания вместо производственного, вам нужно сначала определить URL-адрес, используемый для промежуточного развертывания.</span><span class="sxs-lookup"><span data-stu-id="b3111-170">If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="b3111-171">После развертывания облачной службы URL-адрес промежуточной среды определяется по **идентификатору развертывания`https://deployment-id.cloudapp.net/` GUID и имеет следующий формат:**</span><span class="sxs-lookup"><span data-stu-id="b3111-171">Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="b3111-172">Создайте сертификат с общим именем, значение которого равно URL-адресу на основе GUID (например, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="b3111-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="b3111-173">С помощью портала добавьте этот сертификат в промежуточную облачную службу.</span><span class="sxs-lookup"><span data-stu-id="b3111-173">Use the portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="b3111-174">Затем добавьте сведения об этом сертификате в CSDEF- и CSCFG-файлы, перепакуйте приложение и обновите промежуточное развертывание для использования нового пакета.</span><span class="sxs-lookup"><span data-stu-id="b3111-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="b3111-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b3111-175">Next steps</span></span>
* <span data-ttu-id="b3111-176">[Общая настройка облачной службы](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b3111-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="b3111-177">Узнайте, как [развернуть облачную службу](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b3111-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="b3111-178">Настройте [пользовательское доменное имя](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b3111-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="b3111-179">[Управляйте облачной службой](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b3111-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
