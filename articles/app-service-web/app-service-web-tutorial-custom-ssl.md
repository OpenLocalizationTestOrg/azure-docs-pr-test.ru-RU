---
title: "aaaBind существующие пользовательские SSL-сертификатов tooAzure веб-приложений | Документы Microsoft"
description: "Узнайте tootoobind пользовательские SSL сертификат tooyour веб-приложения, внутреннего сервера мобильного приложения или приложения API в службе приложений Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a><span data-ttu-id="5d149-103">Привязать существующий пользовательский SSL сертификат tooAzure веб-приложений</span><span class="sxs-lookup"><span data-stu-id="5d149-103">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>

<span data-ttu-id="5d149-104">Веб-приложения Azure — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="5d149-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="5d149-105">В этом учебнике показано, как toobind пользовательские SSL сертификат слишком приобретенные у доверенного центра сертификации, который[веб-приложениях Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5d149-105">This tutorial shows you how toobind a custom SSL certificate that you purchased from a trusted certificate authority too[Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="5d149-106">После завершения вы будете иметь доступ tooaccess веб-приложения в конечной точки HTTPS hello своего пользовательского домена DNS.</span><span class="sxs-lookup"><span data-stu-id="5d149-106">When you're finished, you'll be able tooaccess your web app at hello HTTPS endpoint of your custom DNS domain.</span></span>

![Веб-приложение с настраиваемым SSL-сертификатом](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="5d149-108">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="5d149-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5d149-109">Выбор более высокой ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="5d149-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="5d149-110">Привязка к пользовательской tooApp сертификат SSL службы</span><span class="sxs-lookup"><span data-stu-id="5d149-110">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="5d149-111">Принудительное использование HTTPS для приложения.</span><span class="sxs-lookup"><span data-stu-id="5d149-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="5d149-112">Автоматизация привязки SSL-сертификата с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="5d149-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="5d149-113">Если вам требуется tooget пользовательский сертификат SSL, можно получить в hello портал Azure напрямую и привязать его tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5d149-113">If you need tooget a custom SSL certificate, you can get one in hello Azure portal directly and bind it tooyour web app.</span></span> <span data-ttu-id="5d149-114">Выполните hello [сертификатов службы приложений учебника](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="5d149-114">Follow hello [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d149-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5d149-115">Prerequisites</span></span>

<span data-ttu-id="5d149-116">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="5d149-116">toocomplete this tutorial:</span></span>

- <span data-ttu-id="5d149-117">[Создано приложение службы приложений](/azure/app-service/).</span><span class="sxs-lookup"><span data-stu-id="5d149-117">[Create an App Service app](/azure/app-service/)</span></span>
- [<span data-ttu-id="5d149-118">Сопоставление пользовательских веб-приложения tooyour DNS имя</span><span class="sxs-lookup"><span data-stu-id="5d149-118">Map a custom DNS name tooyour web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="5d149-119">Получен SSL-сертификат из доверенного центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="5d149-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="5d149-120">Требования к SSL-сертификату</span><span class="sxs-lookup"><span data-stu-id="5d149-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="5d149-121">toouse сертификатов в службе приложений hello сертификат должен удовлетворять все hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="5d149-121">toouse a certificate in App Service, hello certificate must meet all hello following requirements:</span></span>

* <span data-ttu-id="5d149-122">должен быть подписан доверенным центром сертификации;</span><span class="sxs-lookup"><span data-stu-id="5d149-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="5d149-123">должен быть экспортирован в PFX-файл, защищенный паролем;</span><span class="sxs-lookup"><span data-stu-id="5d149-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="5d149-124">должен содержать закрытый ключ длиной не менее 2048 битов;</span><span class="sxs-lookup"><span data-stu-id="5d149-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="5d149-125">Содержит все промежуточные сертификаты в цепочке сертификатов hello</span><span class="sxs-lookup"><span data-stu-id="5d149-125">Contains all intermediate certificates in hello certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="5d149-126">**Сертификаты с шифрованием на основе эллиптических кривых (ECC)** можно использовать со службой приложений, но это не описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5d149-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="5d149-127">Работа с вашего центра сертификации на toocreate ECC hello точные действия сертификатов.</span><span class="sxs-lookup"><span data-stu-id="5d149-127">Work with your certificate authority on hello exact steps toocreate ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="5d149-128">Подготовка веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5d149-128">Prepare your web app</span></span>

<span data-ttu-id="5d149-129">toobind пользовательские SSL-сертификатов tooyour веб-приложения вашей [план служб приложений](https://azure.microsoft.com/pricing/details/app-service/) должен находиться в hello **основные**, **Стандартная**, или **Premium** уровня.</span><span class="sxs-lookup"><span data-stu-id="5d149-129">toobind a custom SSL certificate tooyour web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in hello **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="5d149-130">На этом шаге вы убедитесь, что веб-приложения в hello поддерживается ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="5d149-130">In this step, you make sure that your web app is in hello supported pricing tier.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="5d149-131">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="5d149-131">Log in tooAzure</span></span>

<span data-ttu-id="5d149-132">Откройте hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5d149-132">Open hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-tooyour-web-app"></a><span data-ttu-id="5d149-133">Перейдите tooyour веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5d149-133">Navigate tooyour web app</span></span>

<span data-ttu-id="5d149-134">Hello в левом меню, щелкните **службы приложений**и щелкните имя веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5d149-134">From hello left menu, click **App Services**, and then click hello name of your web app.</span></span>

![Выбор веб-приложения](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="5d149-136">Выбран на странице управления hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5d149-136">You have landed in hello management page of your web app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="5d149-137">Проверьте hello ценовой категории</span><span class="sxs-lookup"><span data-stu-id="5d149-137">Check hello pricing tier</span></span>

<span data-ttu-id="5d149-138">В левой навигационной hello приложения веб-страницы, прокрутите toohello **параметры** , выберите **масштаб (план службы приложений)**.</span><span class="sxs-lookup"><span data-stu-id="5d149-138">In hello left-hand navigation of your web app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Меню увеличения масштаба](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="5d149-140">Убедитесь том, что веб-приложения не hello toomake **Free** или **Shared** уровня.</span><span class="sxs-lookup"><span data-stu-id="5d149-140">Check toomake sure that your web app is not in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="5d149-141">Текущая ценовая категория веб-приложения выделена синей рамкой.</span><span class="sxs-lookup"><span data-stu-id="5d149-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="5d149-143">Пользовательские SSL не поддерживается в hello **Free** или **Shared** уровня.</span><span class="sxs-lookup"><span data-stu-id="5d149-143">Custom SSL is not supported in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="5d149-144">Если вам требуется tooscale вверх, выполните действия hello в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="5d149-144">If you need tooscale up, follow hello steps in hello next section.</span></span> <span data-ttu-id="5d149-145">В противном случае закройте hello **выберите ценовую категорию** страницы и пропуска слишком[отправка и привязать SSL-сертификат](#upload).</span><span class="sxs-lookup"><span data-stu-id="5d149-145">Otherwise, close hello **Choose your pricing tier** page and skip too[Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="5d149-146">Изменение уровня плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5d149-146">Scale up your App Service plan</span></span>

<span data-ttu-id="5d149-147">Выберите один из hello **основные**, **Стандартная**, или **Premium** уровней.</span><span class="sxs-lookup"><span data-stu-id="5d149-147">Select one of hello **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="5d149-148">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5d149-148">Click **Select**.</span></span>

![Выбор ценовой категории](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="5d149-150">При появлении hello после уведомления hello шкалы операция завершена.</span><span class="sxs-lookup"><span data-stu-id="5d149-150">When you see hello following notification, hello scale operation is complete.</span></span>

![Уведомление об увеличении масштаба](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="5d149-152">Привязка SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="5d149-152">Bind your SSL certificate</span></span>

<span data-ttu-id="5d149-153">Вам будут готовы tooupload веб-приложения tooyour сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="5d149-153">You are ready tooupload your SSL certificate tooyour web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="5d149-154">Объединение промежуточных сертификатов</span><span class="sxs-lookup"><span data-stu-id="5d149-154">Merge intermediate certificates</span></span>

<span data-ttu-id="5d149-155">Если ваш центр сертификации дает несколько сертификатов в цепочке сертификатов hello, требуются сертификаты toomerge hello в порядке.</span><span class="sxs-lookup"><span data-stu-id="5d149-155">If your certificate authority gives you multiple certificates in hello certificate chain, you need toomerge hello certificates in order.</span></span> 

<span data-ttu-id="5d149-156">toodo это, откройте каждого сертификата полученный в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="5d149-156">toodo this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="5d149-157">Создание файла для объединенных сертификат hello, с именем _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="5d149-157">Create a file for hello merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="5d149-158">В текстовом редакторе скопируйте содержимое hello каждый сертификат в этот файл.</span><span class="sxs-lookup"><span data-stu-id="5d149-158">In a text editor, copy hello content of each certificate into this file.</span></span> <span data-ttu-id="5d149-159">порядок Hello сертификатов должен выглядеть hello следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="5d149-159">hello order of your certificates should look like hello following template:</span></span>

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a><span data-ttu-id="5d149-160">Экспорт сертификата tooPFX</span><span class="sxs-lookup"><span data-stu-id="5d149-160">Export certificate tooPFX</span></span>

<span data-ttu-id="5d149-161">Экспорт объединенных SSL-сертификат с закрытым ключом hello, ваш запрос на сертификат, созданный с.</span><span class="sxs-lookup"><span data-stu-id="5d149-161">Export your merged SSL certificate with hello private key that your certificate request was generated with.</span></span>

<span data-ttu-id="5d149-162">Если запрос сертификата был создан с помощью OpenSSL, то вы создали файл закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="5d149-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="5d149-163">tooexport tooPFX ваш сертификат, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="5d149-163">tooexport your certificate tooPFX, run hello following command.</span></span> <span data-ttu-id="5d149-164">Замените заполнители hello  _&lt;файла закрытого ключа >_ и  _&lt;слияние сертификат файл->_.</span><span class="sxs-lookup"><span data-stu-id="5d149-164">Replace hello placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="5d149-165">При появлении запроса определите пароль для экспорта.</span><span class="sxs-lookup"><span data-stu-id="5d149-165">When prompted, define an export password.</span></span> <span data-ttu-id="5d149-166">Этот пароль будет использоваться при отправке вашего SSL сертификат tooApp службы позже.</span><span class="sxs-lookup"><span data-stu-id="5d149-166">You'll use this password when uploading your SSL certificate tooApp Service later.</span></span>

<span data-ttu-id="5d149-167">Если используется IIS или _Certreq.exe_ toogenerate запроса на сертификат, установить hello сертификат tooyour локальный компьютер и затем [экспорта сертификата tooPFX hello](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="5d149-167">If you used IIS or _Certreq.exe_ toogenerate your certificate request, install hello certificate tooyour local machine, and then [export hello certificate tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="5d149-168">Передача SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="5d149-168">Upload your SSL certificate</span></span>

<span data-ttu-id="5d149-169">tooupload SSL-сертификат, нажмите кнопку **SSL-сертификаты** в hello слева навигации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5d149-169">tooupload your SSL certificate, click **SSL certificates** in hello left navigation of your web app.</span></span>

<span data-ttu-id="5d149-170">Щелкните **Отправить сертификат**.</span><span class="sxs-lookup"><span data-stu-id="5d149-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="5d149-171">В разделе **PFX-файл сертификата** выберите свой PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="5d149-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="5d149-172">В **пароль сертификата**, введите пароль hello, созданный при экспорте hello PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="5d149-172">In **Certificate password**, type hello password that you created when you exported hello PFX file.</span></span>

<span data-ttu-id="5d149-173">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="5d149-173">Click **Upload**.</span></span>

![Передача сертификата](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="5d149-175">По завершении отправке сертификата службы приложений он появится в hello **SSL-сертификаты** страницы.</span><span class="sxs-lookup"><span data-stu-id="5d149-175">When App Service finishes uploading your certificate, it appears in hello **SSL certificates** page.</span></span>

![Сертификат добавлен](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="5d149-177">Привязка SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="5d149-177">Bind your SSL certificate</span></span>

<span data-ttu-id="5d149-178">В hello **привязки SSL** щелкните **добавить привязку**.</span><span class="sxs-lookup"><span data-stu-id="5d149-178">In hello **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="5d149-179">В hello **Добавление привязки SSL** используйте hello раскрывающихся списках tooselect hello домена имя toosecure и toouse сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="5d149-179">In hello **Add SSL Binding** page, use hello dropdowns tooselect hello domain name toosecure, and hello certificate toouse.</span></span>

> [!NOTE]
> <span data-ttu-id="5d149-180">Если переданы свой сертификат, но не видите hello имена доменов в hello **Hostname** раскрывающийся список, обновите страницу браузера hello.</span><span class="sxs-lookup"><span data-stu-id="5d149-180">If you have uploaded your certificate but don't see hello domain name(s) in hello **Hostname** dropdown, try refreshing hello browser page.</span></span>
>
>

<span data-ttu-id="5d149-181">В **тип SSL**выберите ли toouse  **[Указание имени сервера (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  или SSL на основе IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="5d149-181">In **SSL Type**, select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="5d149-182">**SSL на основе SNI** позволяет добавить несколько привязок SSL на основе SNI.</span><span class="sxs-lookup"><span data-stu-id="5d149-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="5d149-183">Этот параметр позволяет нескольким toosecure сертификаты SSL несколько доменов на hello же IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5d149-183">This option allows multiple SSL certificates toosecure multiple domains on hello same IP address.</span></span> <span data-ttu-id="5d149-184">Большинство современных браузеров (включая Internet Explorer, Chrome, Firefox и Opera) поддерживает SNI (более подробную информацию о поддержки браузеров можно найти в статье [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication) (Указание имени сервера)).</span><span class="sxs-lookup"><span data-stu-id="5d149-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="5d149-185">**SSL на основе IP-адреса** позволяет добавить только одну привязку SSL на основе IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="5d149-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="5d149-186">Этот параметр позволяет только один toosecure сертификат SSL выделенный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5d149-186">This option allows only one SSL certificate toosecure a dedicated public IP address.</span></span> <span data-ttu-id="5d149-187">toosecure несколько доменов, необходимо защитить их с помощью hello же SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="5d149-187">toosecure multiple domains, you must secure them all using hello same SSL certificate.</span></span> <span data-ttu-id="5d149-188">Этот вариант hello традиционных для привязки SSL.</span><span class="sxs-lookup"><span data-stu-id="5d149-188">This is hello traditional option for SSL binding.</span></span>

<span data-ttu-id="5d149-189">Щелкните **Добавить привязку**.</span><span class="sxs-lookup"><span data-stu-id="5d149-189">Click **Add Binding**.</span></span>

![Привязка SSL-сертификата](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="5d149-191">По завершении отправке сертификата службы приложений он появится в hello **привязки SSL** разделы.</span><span class="sxs-lookup"><span data-stu-id="5d149-191">When App Service finishes uploading your certificate, it appears in hello **SSL bindings** sections.</span></span>

![Сертификат, привязанный tooweb приложения](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="5d149-193">Переназначение записи A для SSL на основе IP-адреса</span><span class="sxs-lookup"><span data-stu-id="5d149-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="5d149-194">Если вы не используете SSL на основе IP в веб-приложении, пропустите слишком[теста HTTPS для пользовательского домена](#test).</span><span class="sxs-lookup"><span data-stu-id="5d149-194">If you don't use IP-based SSL in your web app, skip too[Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="5d149-195">По умолчанию веб-приложение использует общий общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5d149-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="5d149-196">После привязки сертификата с помощью SSL на основе IP-адреса служба приложений создает выделенный IP-адрес для вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5d149-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="5d149-197">Если веб-приложение A записей tooyour сопоставлена, обновления реестра домена этот новый, выделенный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5d149-197">If you have mapped an A record tooyour web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="5d149-198">Веб-приложения **пользовательский домен** страница обновляется при hello нового, выделенного IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5d149-198">Your web app's **Custom domain** page is updated with hello new, dedicated IP address.</span></span> <span data-ttu-id="5d149-199">[Скопируйте этот IP-адрес](app-service-web-tutorial-custom-domain.md#info), затем [преобразования hello запись](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis новый IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5d149-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap hello A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="5d149-200">Тестирование HTTPS</span><span class="sxs-lookup"><span data-stu-id="5d149-200">Test HTTPS</span></span>

<span data-ttu-id="5d149-201">Все, что теперь покинул toodo — toomake, убедившись в наличии HTTPS для вашего домена.</span><span class="sxs-lookup"><span data-stu-id="5d149-201">All that's left toodo now is toomake sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="5d149-202">В различных браузерах Обзор слишком`https://<your.custom.domain>` toosee, он обслуживающего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5d149-202">In various browsers, browse too`https://<your.custom.domain>` toosee that it serves up your web app.</span></span>

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="5d149-204">Если веб-приложение выдает ошибки проверки сертификата, вероятно, вы используете самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="5d149-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="5d149-205">Если это не так hello, вы может были пропущены промежуточные сертификаты при экспорте сертификата toohello PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="5d149-205">If that's not hello case, you may have left out intermediate certificates when you export your certificate toohello PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="5d149-206">Принудительное использование HTTPS</span><span class="sxs-lookup"><span data-stu-id="5d149-206">Enforce HTTPS</span></span>

<span data-ttu-id="5d149-207">Служба приложений *не* принуждает использовать протокол HTTPS, чтобы кто угодно мог обратиться к веб-приложению с помощью протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="5d149-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="5d149-208">tooenforce HTTPS для веб-приложения, определите правило подстановки в hello _web.config_ файла для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5d149-208">tooenforce HTTPS for your web app, define a rewrite rule in hello _web.config_ file for your web app.</span></span> <span data-ttu-id="5d149-209">Приложение службы использует этот файл, независимо от языковой платформе hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5d149-209">App Service uses this file, regardless of hello language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="5d149-210">Для каждого языка используется определенное перенаправление запросов.</span><span class="sxs-lookup"><span data-stu-id="5d149-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="5d149-211">ASP.NET MVC можно использовать hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) фильтра вместо правило подстановки hello в _web.config_.</span><span class="sxs-lookup"><span data-stu-id="5d149-211">ASP.NET MVC can use hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of hello rewrite rule in _web.config_.</span></span>

<span data-ttu-id="5d149-212">Если вы разработчик для .NET, то этот файл должен быть вам в общем и целом знаком.</span><span class="sxs-lookup"><span data-stu-id="5d149-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="5d149-213">Он находится в корне hello решения.</span><span class="sxs-lookup"><span data-stu-id="5d149-213">It is in hello root of your solution.</span></span>

<span data-ttu-id="5d149-214">Кроме того, если вы программируете на PHP, Node.js, Python или Java, существует вероятность того, что этот файл создан от вашего имени в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="5d149-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="5d149-215">Подключения конечной точки FTP tooyour веб-приложения в соответствии с инструкциями hello в [развертывание вашего приложения tooAzure службы приложений с помощью FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="5d149-215">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="5d149-216">Этот файл должен находиться в каталоге _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="5d149-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="5d149-217">Если нет, создайте _web.config_ файл в этой папке с hello следующий XML-код:</span><span class="sxs-lookup"><span data-stu-id="5d149-217">If not, create a _web.config_ file in this folder with hello following XML:</span></span>

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="5d149-218">Для существующей _web.config_ файл, скопировать весь hello `<rule>` элемент в вашей _web.config_ `configuration/system.webServer/rewrite/rules` элемент.</span><span class="sxs-lookup"><span data-stu-id="5d149-218">For an existing _web.config_ file, copy hello entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="5d149-219">Если существуют другие `<rule>` элементов в вашей _web.config_, скопировать hello месте `<rule>` перед hello других элемент `<rule>` элементов.</span><span class="sxs-lookup"><span data-stu-id="5d149-219">If there are other `<rule>` elements in your _web.config_, place hello copied `<rule>` element before hello other `<rule>` elements.</span></span>

<span data-ttu-id="5d149-220">Это правило возвращает toohello HTTP 301 (постоянное перенаправление) по протоколу HTTPS, каждый раз, когда пользователь hello делает веб-приложение tooyour запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="5d149-220">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="5d149-221">Например, он перенаправляет `http://contoso.com` слишком`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="5d149-221">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

<span data-ttu-id="5d149-222">Дополнительные сведения о модуль переопределения URL-адреса IIS hello. в разделе hello [переопределения URL-адресов](http://www.iis.net/downloads/microsoft/url-rewrite) документации.</span><span class="sxs-lookup"><span data-stu-id="5d149-222">For more information on hello IIS URL Rewrite module, see hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="5d149-223">Принудительное использование HTTPS для веб-приложений на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="5d149-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="5d149-224">Служба приложений на платформе Linux *не* принуждает использовать протокол HTTPS, чтобы кто угодно мог обратиться к веб-приложению с помощью протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="5d149-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="5d149-225">tooenforce HTTPS для веб-приложения, определите правило подстановки в hello _.htaccess_ файла для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5d149-225">tooenforce HTTPS for your web app, define a rewrite rule in hello _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="5d149-226">Подключения конечной точки FTP tooyour веб-приложения в соответствии с инструкциями hello в [развертывание вашего приложения tooAzure службы приложений с помощью FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="5d149-226">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="5d149-227">В _/home/site/wwwroot_, создайте _.htaccess_ файл с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="5d149-227">In _/home/site/wwwroot_, create an _.htaccess_ file with hello following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="5d149-228">Это правило возвращает toohello HTTP 301 (постоянное перенаправление) по протоколу HTTPS, каждый раз, когда пользователь hello делает веб-приложение tooyour запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="5d149-228">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="5d149-229">Например, он перенаправляет `http://contoso.com` слишком`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="5d149-229">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="5d149-230">Автоматизация с помощью сценариев</span><span class="sxs-lookup"><span data-stu-id="5d149-230">Automate with scripts</span></span>

<span data-ttu-id="5d149-231">Можно автоматизировать привязки SSL для веб-приложения с помощью скриптов, с помощью hello [Azure CLI](/cli/azure/install-azure-cli) или [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5d149-231">You can automate SSL bindings for your web app with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="5d149-232">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="5d149-232">Azure CLI</span></span>

<span data-ttu-id="5d149-233">Hello, следующая команда отправляет экспортированного PFX-файла и возвращает отпечаток hello.</span><span class="sxs-lookup"><span data-stu-id="5d149-233">hello following command uploads an exported PFX file and gets hello thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="5d149-234">Hello следующая команда добавляет привязки на основе SNI SSL, с помощью отпечатка hello из предыдущей команды hello.</span><span class="sxs-lookup"><span data-stu-id="5d149-234">hello following command adds an SNI-based SSL binding, using hello thumbprint from hello previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="5d149-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d149-235">Azure PowerShell</span></span>

<span data-ttu-id="5d149-236">Hello следующая команда отправляет экспортированного PFX-файла и добавляет привязку на основе SNI SSL.</span><span class="sxs-lookup"><span data-stu-id="5d149-236">hello following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="5d149-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5d149-237">Next steps</span></span>

<span data-ttu-id="5d149-238">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="5d149-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5d149-239">Выбор более высокой ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="5d149-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="5d149-240">Привязка к пользовательской tooApp сертификат SSL службы</span><span class="sxs-lookup"><span data-stu-id="5d149-240">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="5d149-241">Принудительное использование HTTPS для приложения.</span><span class="sxs-lookup"><span data-stu-id="5d149-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="5d149-242">Автоматизация привязки SSL-сертификата с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="5d149-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="5d149-243">Как переместить следующий учебник toolearn toohello toouse сети доставки содержимого Azure.</span><span class="sxs-lookup"><span data-stu-id="5d149-243">Advance toohello next tutorial toolearn how toouse Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d149-244">Добавление сети доставки содержимого (CDN) tooan службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="5d149-244">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
