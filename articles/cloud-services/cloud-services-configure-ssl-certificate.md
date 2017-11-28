---
title: "Настройка SSL для облачной службы (классический вариант) | Документация Майкрософт"
description: "Узнайте, как определить конечную точку HTTPS для веб-роли и как передать SSL-сертификат, чтобы обеспечить безопасность приложения."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: edb9aaf6dae11c9b8a171b22bc8a17003f80d86b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="5ae2c-103">Настройка SSL для приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="5ae2c-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ae2c-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5ae2c-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="5ae2c-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="5ae2c-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="5ae2c-106">SSL-шифрование — это наиболее распространенный метод обеспечения безопасности данных, отправленных через Интернет.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-106">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="5ae2c-107">В этой теме, посвященной общим задачам, обсуждается, как определить конечную точку HTTPS для веб-роли и как передать SSL-сертификат, чтобы обеспечить безопасность приложения.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-107">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="5ae2c-108">Процедуры в этом задании применяются для облачных служб Azure. Информацию о процедурах для служб приложений см. в [данной](../app-service-web/web-sites-configure-ssl-certificate.md) статье.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-108">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="5ae2c-109">В этой задаче используется рабочее развертывание.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-109">This task uses a production deployment.</span></span> <span data-ttu-id="5ae2c-110">Сведения об использовании промежуточного развертывания приведены в конце данного раздела.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-110">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="5ae2c-111">Если вы еще не создали облачную службу, сначала прочтите [эту](cloud-services-how-to-create-deploy.md) статью.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="5ae2c-112">Шаг 1. Получение SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="5ae2c-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="5ae2c-113">Чтобы настроить протокол SSL для приложения, сначала необходимо получить SSL-сертификат, подписанный центром сертификации, то есть доверенным сторонним поставщиком, который выдает сертификаты для этой цели.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-113">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="5ae2c-114">Если у вас еще нет сертификата, нужно получить его в компании, продающей SSL-сертификаты.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-114">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="5ae2c-115">Сертификат должен отвечать следующим требованиям для SSL-сертификатов в Azure:</span><span class="sxs-lookup"><span data-stu-id="5ae2c-115">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="5ae2c-116">Сертификат должен содержать закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-116">The certificate must contain a private key.</span></span>
* <span data-ttu-id="5ae2c-117">Сертификат должен быть создан для обмена ключами, которые можно экспортировать в файл обмена личной информацией (PFX-файл).</span><span class="sxs-lookup"><span data-stu-id="5ae2c-117">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="5ae2c-118">Имя субъекта сертификата должно совпадать с именем домена, которое используется для обращения к облачной службе.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-118">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="5ae2c-119">Не удается получить SSL-сертификат от центра сертификации (ЦС) в домене cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-119">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="5ae2c-120">Необходимо получить имя пользовательского домена для использования при получении доступа к службе.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-120">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="5ae2c-121">При запросе сертификата из ЦС имя субъекта сертификата должно соответствовать имени личного домена, который используется для доступа к вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-121">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="5ae2c-122">Например, если вы используете домен **contoso.com**, необходимо запросить сертификат из центра сертификации для ***.contoso.com** или **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="5ae2c-123">Сертификат должен использовать как минимум 2048-разрядное шифрование.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-123">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="5ae2c-124">В целях тестирования вы можете [создать](cloud-services-certs-create.md) и использовать самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="5ae2c-125">Самозаверяющий сертификат не прошел аутентификацию через ЦС, и можно использовать домен cloudapp.net в качестве URL-адреса веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-125">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="5ae2c-126">Например, в приведенной ниже задаче используется самозаверяющий сертификат, в котором задано общее имя **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-126">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="5ae2c-127">Далее необходимо включить сведения о сертификате в файлы определения службы и конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-127">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="5ae2c-128">Шаг 2. Изменение файлов определения службы и конфигурации</span><span class="sxs-lookup"><span data-stu-id="5ae2c-128">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="5ae2c-129">Ваше приложение должно быть настроено для использования сертификата и также необходимо добавить конечную точку HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-129">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="5ae2c-130">Для этого следует обновить файлы определения службы и конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-130">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="5ae2c-131">В среде разработки откройте файл определения службы (CSDEF), добавьте раздел **Certificates** внутри раздела **WebRole** и добавьте следующие сведения о сертификате (и промежуточных сертификатах).</span><span class="sxs-lookup"><span data-stu-id="5ae2c-131">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>
   
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
   
   <span data-ttu-id="5ae2c-132">В разделе **Certificates** определяется имя сертификата, его расположение и имя хранилища, в котором он находится.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-132">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>
   
   <span data-ttu-id="5ae2c-133">Разрешениям (атрибуту`permisionLevel`) можно присвоить одно из приведенных ниже значений.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-133">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>
   
   | <span data-ttu-id="5ae2c-134">Значение разрешения</span><span class="sxs-lookup"><span data-stu-id="5ae2c-134">Permission Value</span></span> | <span data-ttu-id="5ae2c-135">Описание</span><span class="sxs-lookup"><span data-stu-id="5ae2c-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="5ae2c-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="5ae2c-136">limitedOrElevated</span></span> |<span data-ttu-id="5ae2c-137">**(По умолчанию).** Все процессы роли могут получить доступ к закрытому ключу.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-137">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="5ae2c-138">elevated</span><span class="sxs-lookup"><span data-stu-id="5ae2c-138">elevated</span></span> |<span data-ttu-id="5ae2c-139">Доступ к закрытому ключу могут получить только процессы повышенного уровня.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-139">Only elevated processes can access the private key.</span></span> |
2. <span data-ttu-id="5ae2c-140">В файле определения службы добавьте элемент **InputEndpoint** в раздел **Endpoints**, чтобы включить протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-140">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>
   
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

3. <span data-ttu-id="5ae2c-141">В файле определения службы добавьте элемент **Binding** в раздел **Sites**.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-141">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="5ae2c-142">Этот раздел добавляет привязку HTTPS для сопоставления конечной точки с вашим сайтом.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-142">This section adds an HTTPS binding to map the endpoint to your site:</span></span>
   
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
   
   <span data-ttu-id="5ae2c-143">Все необходимые изменения внесены в файл определения службы, но еще нужно добавить сведения о сертификате в сам файл конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-143">All the required changes to the service definition file have been completed, but you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="5ae2c-144">В файле конфигурации службы (CSCFG), ServiceConfiguration.Cloud.cscfg, добавьте раздел **Certificates** в раздел **Role**, заменив приведенный ниже пример значения отпечатка сертификата значением отпечатка своего сертификата.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within the **Role** section, replacing the sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="5ae2c-145">(В предыдущем примере для алгоритма отпечатка используется обозначение **sha1**.)</span><span class="sxs-lookup"><span data-stu-id="5ae2c-145">(The preceding example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="5ae2c-146">Укажите соответствующее значение для алгоритма отпечатка своего сертификата.)</span><span class="sxs-lookup"><span data-stu-id="5ae2c-146">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="5ae2c-147">Теперь, когда файлы определения службы и конфигурации службы обновлены, создайте пакет развертывания для передачи в Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-147">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="5ae2c-148">Если используется **cspack**, не используйте флаг **/generateConfigurationFile**, так как он приведет к перезаписи сведений о сертификате, которые вы добавили.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="5ae2c-149">Шаг 3. Отправка сертификата</span><span class="sxs-lookup"><span data-stu-id="5ae2c-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="5ae2c-150">Ваш пакет развертывания был обновлен для использования сертификата, и была добавлена конечная точка HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-150">Your deployment package has been updated to use the certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="5ae2c-151">Теперь можно передать пакет и сертификат в Azure через классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-151">Now you can upload the package and certificate to Azure with the Azure classic portal.</span></span>

1. <span data-ttu-id="5ae2c-152">Войдите на [классический портал Azure][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="5ae2c-152">Log in to the [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="5ae2c-153">Выберите **Облачные службы** на панели навигации слева.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-153">Click **Cloud Services** on the left-side navigation pane.</span></span>
3. <span data-ttu-id="5ae2c-154">Выберите необходимую облачную службу.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-154">Click the desired cloud service.</span></span>
4. <span data-ttu-id="5ae2c-155">Перейдите на вкладку **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-155">Click the **Certificates** tab.</span></span>
   
    ![Перейдите на вкладку «Сертификаты»](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="5ae2c-157">Нажмите кнопку **Отправить** .</span><span class="sxs-lookup"><span data-stu-id="5ae2c-157">Click the **Upload** button.</span></span>
   
    ![Передать](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="5ae2c-159">Укажите **файл**, **пароль**, а затем щелкните галочку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-159">Provide the **File**, **Password**, then click **Complete** (the checkmark).</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="5ae2c-160">Шаг 4. Подключение к экземпляру роли с использованием HTTPS</span><span class="sxs-lookup"><span data-stu-id="5ae2c-160">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="5ae2c-161">Теперь, когда развертывание готово и работает в Azure, вы можете подключиться к нему, используя HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-161">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="5ae2c-162">Выберите свое развертывание на классическом портале Azure и щелкните ссылку в разделе **URL-адрес сайта**.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-162">In the Azure classic portal, select your deployment, then click the link under **Site URL**.</span></span>
   
   ![Определение URL-адреса сайта][2]
2. <span data-ttu-id="5ae2c-164">В веб-браузере измените ссылку, указав **https** вместо **http**, и перейдите на страницу.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-164">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5ae2c-165">Если используется самозаверяющий сертификат, то при переходе к конечной точке HTTPS, связанной с самозаверяющим сертификатом, в браузере может появиться сообщение об ошибке сертификата.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-165">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="5ae2c-166">Эту проблему можно устранить, воспользовавшись сертификатом, подписанным доверенным центром сертификации. Пока это не будет сделано, вы можете игнорировать данную ошибку.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-166">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="5ae2c-167">(Другой способ — добавить самозаверяющий сертификат в используемое хранилище сертификатов доверенного центра сертификации.)</span><span class="sxs-lookup"><span data-stu-id="5ae2c-167">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Пример веб-сайта SSL][3]

<span data-ttu-id="5ae2c-169">Если вы хотите использовать протокол SSL для промежуточного развертывания вместо рабочего, то вам нужно сначала определить URL-адрес, используемый для промежуточного развертывания.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-169">If you want to use SSL for a staging deployment instead of a production deployment, you first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="5ae2c-170">Разверните свою облачную службу в промежуточной среде, не включая сертификат или сведения о сертификате.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-170">Deploy your cloud service to the staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="5ae2c-171">Выполнив развертывание, можно определить URL-адрес на основе GUID, который приведен в поле **URL-адрес сайта** на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-171">Once deployed, you can determine the GUID-based URL, which is listed in the Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="5ae2c-172">Создайте сертификат с общим именем, значение которого равно URL-адресу на основе GUID (например, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="5ae2c-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="5ae2c-173">С помощью классического портала Azure добавьте этот сертификат в промежуточную облачную службу.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-173">Use the Azure classic portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="5ae2c-174">Затем добавьте сведения об этом сертификате в CSDEF- и CSCFG-файлы, перепакуйте приложение и обновите промежуточное развертывание для использования нового пакета.</span><span class="sxs-lookup"><span data-stu-id="5ae2c-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ae2c-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ae2c-175">Next steps</span></span>
* <span data-ttu-id="5ae2c-176">[Общая настройка облачной службы](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5ae2c-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="5ae2c-177">Узнайте, как [развернуть облачную службу](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5ae2c-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="5ae2c-178">Настройте [пользовательское доменное имя](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="5ae2c-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="5ae2c-179">[Управляйте облачной службой](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="5ae2c-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
