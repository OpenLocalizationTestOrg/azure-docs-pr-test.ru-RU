---
title: "aaaConfigure SSL для облачной службы (классические) | Документы Microsoft"
description: "Узнайте, как toospecify конечной точки HTTPS для веб-роли и как tooupload SSL сертификат toosecure приложения."
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
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="441a6-103">Настройка SSL для приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="441a6-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="441a6-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="441a6-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="441a6-105">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="441a6-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="441a6-106">Безопасное шифрование Socket Layer (SSL) — наиболее часто используемые hello способ защиты данных, передаваемых через hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="441a6-106">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="441a6-107">Продолжение вводимых рассматриваются как toospecify конечной точки HTTPS для веб-роли и как tooupload SSL сертификат toosecure приложения.</span><span class="sxs-lookup"><span data-stu-id="441a6-107">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="441a6-108">Hello процедуры в этой задаче применяются tooAzure облачные службы; Службы приложений. в разделе [это](../app-service-web/web-sites-configure-ssl-certificate.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="441a6-108">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="441a6-109">В этой задаче используется рабочее развертывание.</span><span class="sxs-lookup"><span data-stu-id="441a6-109">This task uses a production deployment.</span></span> <span data-ttu-id="441a6-110">В конце hello в этом разделе предоставляются сведения об использовании промежуточного развертывания.</span><span class="sxs-lookup"><span data-stu-id="441a6-110">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="441a6-111">Если вы еще не создали облачную службу, сначала прочтите [эту](cloud-services-how-to-create-deploy.md) статью.</span><span class="sxs-lookup"><span data-stu-id="441a6-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="441a6-112">Шаг 1. Получение SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="441a6-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="441a6-113">tooconfigure SSL для приложения, необходимо сначала tooget SSL-сертификат, подписанный по сертификации (ЦС), доверенным сторонним, выдающий сертификаты для этой цели.</span><span class="sxs-lookup"><span data-stu-id="441a6-113">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="441a6-114">Если вы не сделали этого, необходимо один tooobtain компания продает SSL-сертификаты.</span><span class="sxs-lookup"><span data-stu-id="441a6-114">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="441a6-115">Hello сертификат должен удовлетворять hello следующие требования к SSL-сертификаты в Azure.</span><span class="sxs-lookup"><span data-stu-id="441a6-115">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="441a6-116">Hello сертификат должен содержать закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="441a6-116">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="441a6-117">необходимо создать сертификат Hello для обмена ключами, tooa экспортируемый файл обмена личной информацией (PFX-файл).</span><span class="sxs-lookup"><span data-stu-id="441a6-117">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="441a6-118">Hello имя субъекта сертификата должно соответствовать hello домен, используемый tooaccess hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="441a6-118">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="441a6-119">Не удается получить SSL-сертификат из сертификата центром сертификации (ЦС) для домена cloudapp.net hello.</span><span class="sxs-lookup"><span data-stu-id="441a6-119">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="441a6-120">Для этого нужно получить имя пользовательского домена toouse при обращении к службе.</span><span class="sxs-lookup"><span data-stu-id="441a6-120">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="441a6-121">Когда вы запрашиваете сертификат из центра сертификации, имя субъекта сертификата hello должно соответствовать hello доменное имя, используемое tooaccess приложения.</span><span class="sxs-lookup"><span data-stu-id="441a6-121">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="441a6-122">Например, если вы используете домен **contoso.com**, необходимо запросить сертификат из центра сертификации для ***.contoso.com** или **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="441a6-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="441a6-123">Hello сертификата необходимо использовать не менее 2048-битное шифрование.</span><span class="sxs-lookup"><span data-stu-id="441a6-123">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="441a6-124">В целях тестирования вы можете [создать](cloud-services-certs-create.md) и использовать самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="441a6-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="441a6-125">Самозаверяющий сертификат не прошел проверку подлинности через ЦС и hello cloudapp.net домен можно использовать как URL-адрес веб-сайта hello.</span><span class="sxs-lookup"><span data-stu-id="441a6-125">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="441a6-126">Например, hello следующей задаче используется самозаверяющий сертификат, в которой hello — общее имя (CN) в сертификате hello **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="441a6-126">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="441a6-127">После этого необходимо включить сведения о сертификате hello в определение службы и файлы конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="441a6-127">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="441a6-128">Шаг 2: Измените файлы определения и конфигурации службы hello</span><span class="sxs-lookup"><span data-stu-id="441a6-128">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="441a6-129">Приложение должно быть настроенный toouse hello сертификата и необходимо добавить конечную точку HTTPS.</span><span class="sxs-lookup"><span data-stu-id="441a6-129">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="441a6-130">В результате hello определение службы и файлы конфигурации службы необходимо обновить toobe.</span><span class="sxs-lookup"><span data-stu-id="441a6-130">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="441a6-131">В среде разработки, откройте hello файл определения службы (CSDEF), добавьте **сертификаты** раздела в hello **WebRole** статьи и включите следующую информацию hello сертификат (и промежуточные сертификаты):</span><span class="sxs-lookup"><span data-stu-id="441a6-131">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="441a6-132">Hello **сертификаты** раздел определяет имя hello нашей сертификата, его расположение и имя hello hello хранилища, где он расположен.</span><span class="sxs-lookup"><span data-stu-id="441a6-132">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>
   
   <span data-ttu-id="441a6-133">Разрешения (`permisionLevel` атрибут) может быть tooone набор из hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="441a6-133">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>
   
   | <span data-ttu-id="441a6-134">Значение разрешения</span><span class="sxs-lookup"><span data-stu-id="441a6-134">Permission Value</span></span> | <span data-ttu-id="441a6-135">Описание</span><span class="sxs-lookup"><span data-stu-id="441a6-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="441a6-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="441a6-136">limitedOrElevated</span></span> |<span data-ttu-id="441a6-137">**(По умолчанию)**  Всем процессам роли можно получить доступ к закрытым ключом hello.</span><span class="sxs-lookup"><span data-stu-id="441a6-137">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="441a6-138">elevated</span><span class="sxs-lookup"><span data-stu-id="441a6-138">elevated</span></span> |<span data-ttu-id="441a6-139">Только процессов с повышенными правами можно получить доступ к закрытым ключом hello.</span><span class="sxs-lookup"><span data-stu-id="441a6-139">Only elevated processes can access hello private key.</span></span> |
2. <span data-ttu-id="441a6-140">В файле определения службы добавьте **InputEndpoint** элемент в пределах hello **конечные точки** статьи tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="441a6-140">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>
   
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

3. <span data-ttu-id="441a6-141">В файле определения службы добавьте **привязки** элемент в пределах hello **сайтов** раздела.</span><span class="sxs-lookup"><span data-stu-id="441a6-141">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="441a6-142">В этом разделе добавляет toomap привязки HTTPS сайта tooyour конечной точки:</span><span class="sxs-lookup"><span data-stu-id="441a6-142">This section adds an HTTPS binding toomap the endpoint tooyour site:</span></span>
   
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
   
   <span data-ttu-id="441a6-143">Файл определения всех hello необходимые изменения toohello службы будет завершена, но по-прежнему требуются сведения сертификата hello tooadd для файла конфигурации службы hello.</span><span class="sxs-lookup"><span data-stu-id="441a6-143">All hello required changes toohello service definition file have been completed, but you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="441a6-144">В файле конфигурации службы (CSCFG), ServiceConfiguration.Cloud.cscfg, добавьте **сертификаты** раздела в hello **роли** раздел, заменив значение отпечатка образец hello, показано ниже с помощью который сертификата:</span><span class="sxs-lookup"><span data-stu-id="441a6-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within hello **Role** section, replacing hello sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="441a6-145">(hello предшествующий в этом примере используется **sha1** для hello алгоритм отпечатка.</span><span class="sxs-lookup"><span data-stu-id="441a6-145">(hello preceding example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="441a6-146">Укажите соответствующее значение hello алгоритм отпечатка вашего сертификата).</span><span class="sxs-lookup"><span data-stu-id="441a6-146">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="441a6-147">Теперь, когда hello определения и обновления файлов конфигурации службы были обновлены, пакет развертывания для передачи tooAzure.</span><span class="sxs-lookup"><span data-stu-id="441a6-147">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="441a6-148">Если используется **cspack**, не используйте флаг **/generateConfigurationFile**, так как он приведет к перезаписи сведений о сертификате, которые вы добавили.</span><span class="sxs-lookup"><span data-stu-id="441a6-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="441a6-149">Шаг 3. Отправка сертификата</span><span class="sxs-lookup"><span data-stu-id="441a6-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="441a6-150">Пакет развертывания был toouse обновленный сертификат hello и добавлена конечная точка HTTPS.</span><span class="sxs-lookup"><span data-stu-id="441a6-150">Your deployment package has been updated toouse hello certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="441a6-151">Теперь можно отправить hello пакета и сертификата tooAzure hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="441a6-151">Now you can upload hello package and certificate tooAzure with hello Azure classic portal.</span></span>

1. <span data-ttu-id="441a6-152">Войдите в toohello [классический портал Azure][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="441a6-152">Log in toohello [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="441a6-153">Нажмите кнопку **облачные службы** на панели навигации слева hello.</span><span class="sxs-lookup"><span data-stu-id="441a6-153">Click **Cloud Services** on hello left-side navigation pane.</span></span>
3. <span data-ttu-id="441a6-154">Щелкните hello требуемого облачную службу.</span><span class="sxs-lookup"><span data-stu-id="441a6-154">Click hello desired cloud service.</span></span>
4. <span data-ttu-id="441a6-155">Нажмите кнопку hello **сертификаты** вкладки.</span><span class="sxs-lookup"><span data-stu-id="441a6-155">Click hello **Certificates** tab.</span></span>
   
    ![Откройте вкладку сертификатов hello](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="441a6-157">Нажмите кнопку hello **отправить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="441a6-157">Click hello **Upload** button.</span></span>
   
    ![Отправить](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="441a6-159">Укажите hello **файл**, **пароль**, нажмите кнопку **завершить** (hello флажок).</span><span class="sxs-lookup"><span data-stu-id="441a6-159">Provide hello **File**, **Password**, then click **Complete** (hello checkmark).</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="441a6-160">Шаг 4: Экземпляр роли toohello подключения по протоколу HTTPS</span><span class="sxs-lookup"><span data-stu-id="441a6-160">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="441a6-161">Теперь, когда развертывание работает в Azure, можно подключить tooit, с помощью протокола HTTPS.</span><span class="sxs-lookup"><span data-stu-id="441a6-161">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="441a6-162">В hello классический портал Azure, выберите развертывание, а затем щелкните ссылку hello в **URL-адрес сайта**.</span><span class="sxs-lookup"><span data-stu-id="441a6-162">In hello Azure classic portal, select your deployment, then click hello link under **Site URL**.</span></span>
   
   ![Определение URL-адреса сайта][2]
2. <span data-ttu-id="441a6-164">В веб-браузере изменить ссылку toouse hello **https** вместо **http**, а затем на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="441a6-164">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="441a6-165">Если вы используете самозаверяющий сертификат, при просмотре конечной точки HTTPS tooan, связанной с самозаверяющим сертификатом hello может появиться сообщение об ошибке сертификата в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="441a6-165">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="441a6-166">Использовать сертификат, подписанный доверенным центром сертификации избавиться от этой проблемы; в hello временем, ошибку можно игнорировать hello.</span><span class="sxs-lookup"><span data-stu-id="441a6-166">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="441a6-167">(Другой вариант — tooadd hello самозаверяющий сертификат toohello доверенный сертификат центра хранилище сертификатов пользователя).</span><span class="sxs-lookup"><span data-stu-id="441a6-167">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Пример веб-сайта SSL][3]

<span data-ttu-id="441a6-169">Если требуется toouse SSL для промежуточного развертывания вместо развертывания в рабочей среде, необходимо сначала toodetermine hello URL-адреса для hello промежуточное развертывание.</span><span class="sxs-lookup"><span data-stu-id="441a6-169">If you want toouse SSL for a staging deployment instead of a production deployment, you first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="441a6-170">Развертывание облачной службы toohello промежуточной среде без включения сертификат или никаких сведений о сертификате.</span><span class="sxs-lookup"><span data-stu-id="441a6-170">Deploy your cloud service toohello staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="441a6-171">После развертывания, можно определить hello GUID URL-адрес, который указан в hello классический портал Azure **URL-адрес сайта** поля.</span><span class="sxs-lookup"><span data-stu-id="441a6-171">Once deployed, you can determine hello GUID-based URL, which is listed in hello Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="441a6-172">Создайте сертификат с hello общие имя (CN) равно toohello на основе GUID URL-адрес (например, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="441a6-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="441a6-173">Используйте hello Azure классического портала tooadd hello сертификат tooyour промежуточное облачной службы.</span><span class="sxs-lookup"><span data-stu-id="441a6-173">Use hello Azure classic portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="441a6-174">Добавьте hello сертификат сведения tooyour CSDEF и CSCFG-файлы, упакуйте приложение и обновить новый пакет hello toouse промежуточное развертывание.</span><span class="sxs-lookup"><span data-stu-id="441a6-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="441a6-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="441a6-175">Next steps</span></span>
* <span data-ttu-id="441a6-176">[Общая настройка облачной службы](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="441a6-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="441a6-177">Узнайте, каким образом слишком[развертывание облачной службы](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="441a6-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="441a6-178">Настройте [пользовательское доменное имя](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="441a6-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="441a6-179">[Управляйте облачной службой](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="441a6-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
