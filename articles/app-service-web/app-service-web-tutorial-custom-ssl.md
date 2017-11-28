---
title: "Привязывание существующего настраиваемого SSL-сертификата к веб-приложениям Azure | Документация Майкрософт"
description: "Узнайте, как привязать настраиваемый SSL-сертификат к веб-приложению, серверной части мобильного приложения или приложению API в службе приложений Azure."
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
ms.openlocfilehash: 15c31ae5451a31dff2df08047ee43e75edacc127
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-to-azure-web-apps"></a><span data-ttu-id="be4b5-103">Привязывание существующего настраиваемого SSL-сертификата к веб-приложениям Azure</span><span class="sxs-lookup"><span data-stu-id="be4b5-103">Bind an existing custom SSL certificate to Azure Web Apps</span></span>

<span data-ttu-id="be4b5-104">Веб-приложения Azure — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="be4b5-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="be4b5-105">В этом руководстве показано, как привязать SSL-сертификат, приобретенный в доверенном центре сертификации, к [веб-приложениям Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be4b5-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="be4b5-106">Завершив работу с этим руководством, вы сможете обращаться к своему веб-приложению через конечную точку HTTPS личного домена DNS.</span><span class="sxs-lookup"><span data-stu-id="be4b5-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span></span>

![Веб-приложение с настраиваемым SSL-сертификатом](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="be4b5-108">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="be4b5-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="be4b5-109">Выбор более высокой ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="be4b5-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="be4b5-110">Привязывание пользовательского SSL-сертификата к службе приложений.</span><span class="sxs-lookup"><span data-stu-id="be4b5-110">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="be4b5-111">Принудительное использование HTTPS для приложения.</span><span class="sxs-lookup"><span data-stu-id="be4b5-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="be4b5-112">Автоматизация привязки SSL-сертификата с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="be4b5-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="be4b5-113">Если необходимо, вы можете получить SSL-сертификат непосредственно на портале Azure и привязать его к веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="be4b5-113">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span></span> <span data-ttu-id="be4b5-114">Следуйте указаниям в [руководстве по сертификатам службы приложений](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="be4b5-114">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be4b5-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="be4b5-115">Prerequisites</span></span>

<span data-ttu-id="be4b5-116">Для работы с этим руководством:</span><span class="sxs-lookup"><span data-stu-id="be4b5-116">To complete this tutorial:</span></span>

- <span data-ttu-id="be4b5-117">[Создано приложение службы приложений](/azure/app-service/).</span><span class="sxs-lookup"><span data-stu-id="be4b5-117">[Create an App Service app](/azure/app-service/)</span></span>
- <span data-ttu-id="be4b5-118">[С вашим веб-приложением сопоставлено настраиваемое DNS-имя](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="be4b5-118">[Map a custom DNS name to your web app](app-service-web-tutorial-custom-domain.md)</span></span>
- <span data-ttu-id="be4b5-119">Получен SSL-сертификат из доверенного центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="be4b5-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="be4b5-120">Требования к SSL-сертификату</span><span class="sxs-lookup"><span data-stu-id="be4b5-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="be4b5-121">Чтобы сертификат можно было использовать в службе приложений, он:</span><span class="sxs-lookup"><span data-stu-id="be4b5-121">To use a certificate in App Service, the certificate must meet all the following requirements:</span></span>

* <span data-ttu-id="be4b5-122">должен быть подписан доверенным центром сертификации;</span><span class="sxs-lookup"><span data-stu-id="be4b5-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="be4b5-123">должен быть экспортирован в PFX-файл, защищенный паролем;</span><span class="sxs-lookup"><span data-stu-id="be4b5-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="be4b5-124">должен содержать закрытый ключ длиной не менее 2048 битов;</span><span class="sxs-lookup"><span data-stu-id="be4b5-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="be4b5-125">должен содержать все промежуточные сертификаты из цепочки сертификатов.</span><span class="sxs-lookup"><span data-stu-id="be4b5-125">Contains all intermediate certificates in the certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="be4b5-126">**Сертификаты с шифрованием на основе эллиптических кривых (ECC)** можно использовать со службой приложений, но это не описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="be4b5-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="be4b5-127">Чтобы создать сертификаты ECC, обратитесь к своему центру сертификации за конкретными указаниями.</span><span class="sxs-lookup"><span data-stu-id="be4b5-127">Work with your certificate authority on the exact steps to create ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="be4b5-128">Подготовка веб-приложения</span><span class="sxs-lookup"><span data-stu-id="be4b5-128">Prepare your web app</span></span>

<span data-ttu-id="be4b5-129">Для привязки SSL-сертификата к веб-приложению ваш [план службы приложений](https://azure.microsoft.com/pricing/details/app-service/) должен находиться в ценовой категории **Базовый**, **Стандартный** или **Премиум**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-129">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="be4b5-130">На этом шаге следует убедиться, что веб-приложение находится в поддерживаемой ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="be4b5-130">In this step, you make sure that your web app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="be4b5-131">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="be4b5-131">Log in to Azure</span></span>

<span data-ttu-id="be4b5-132">Откройте [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="be4b5-132">Open the [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-to-your-web-app"></a><span data-ttu-id="be4b5-133">Переход к веб-приложению</span><span class="sxs-lookup"><span data-stu-id="be4b5-133">Navigate to your web app</span></span>

<span data-ttu-id="be4b5-134">В меню слева выберите **Службы приложений**, а затем щелкните имя своего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="be4b5-134">From the left menu, click **App Services**, and then click the name of your web app.</span></span>

![Выбор веб-приложения](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="be4b5-136">Вы попадете на страницу управления веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="be4b5-136">You have landed in the management page of your web app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="be4b5-137">Проверка ценовой категории</span><span class="sxs-lookup"><span data-stu-id="be4b5-137">Check the pricing tier</span></span>

<span data-ttu-id="be4b5-138">В левой области навигации страницы веб-приложения перейдите к разделу **Параметры** и выберите **Увеличить масштаб (план службы приложений)**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-138">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Меню увеличения масштаба](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="be4b5-140">Убедитесь, что веб-приложение не находится в ценовой категории **Бесплатный** или **Общий**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-140">Check to make sure that your web app is not in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="be4b5-141">Текущая ценовая категория веб-приложения выделена синей рамкой.</span><span class="sxs-lookup"><span data-stu-id="be4b5-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="be4b5-143">Настраиваемые SSL-сертификаты не поддерживаются в ценовых категориях **Бесплатный** или **Общий**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-143">Custom SSL is not supported in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="be4b5-144">Если вам нужно перевести приложение в другую ценовую категорию, выполните действия в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="be4b5-144">If you need to scale up, follow the steps in the next section.</span></span> <span data-ttu-id="be4b5-145">В противном случае закройте страницу **Выбор ценовой категории** и перейдите к разделу [Привязка SSL-сертификата](#upload).</span><span class="sxs-lookup"><span data-stu-id="be4b5-145">Otherwise, close the **Choose your pricing tier** page and skip to [Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="be4b5-146">Изменение уровня плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="be4b5-146">Scale up your App Service plan</span></span>

<span data-ttu-id="be4b5-147">Выберите одну из категорий: **Базовый**, **Стандартный** или **Премиум**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-147">Select one of the **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="be4b5-148">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-148">Click **Select**.</span></span>

![Выбор ценовой категории](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="be4b5-150">Если вы увидите уведомление ниже, значит уровень плана службы приложений изменен.</span><span class="sxs-lookup"><span data-stu-id="be4b5-150">When you see the following notification, the scale operation is complete.</span></span>

![Уведомление об увеличении масштаба](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="be4b5-152">Привязка SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="be4b5-152">Bind your SSL certificate</span></span>

<span data-ttu-id="be4b5-153">Все готово к передаче SSL-сертификата для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="be4b5-153">You are ready to upload your SSL certificate to your web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="be4b5-154">Объединение промежуточных сертификатов</span><span class="sxs-lookup"><span data-stu-id="be4b5-154">Merge intermediate certificates</span></span>

<span data-ttu-id="be4b5-155">Если цепочка сертификатов из центра сертификации содержит несколько сертификатов, их необходимо объединить по порядку.</span><span class="sxs-lookup"><span data-stu-id="be4b5-155">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span></span> 

<span data-ttu-id="be4b5-156">Чтобы сделать это, откройте каждый полученный сертификат в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="be4b5-156">To do this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="be4b5-157">Создайте файл для объединенных сертификатов и присвойте ему имя _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="be4b5-157">Create a file for the merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="be4b5-158">В текстовом редакторе скопируйте содержимое каждого сертификата в этот файл.</span><span class="sxs-lookup"><span data-stu-id="be4b5-158">In a text editor, copy the content of each certificate into this file.</span></span> <span data-ttu-id="be4b5-159">Сертификаты должны быть упорядочены примерно так:</span><span class="sxs-lookup"><span data-stu-id="be4b5-159">The order of your certificates should look like the following template:</span></span>

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

### <a name="export-certificate-to-pfx"></a><span data-ttu-id="be4b5-160">Экспорт сертификата в PFX-файл</span><span class="sxs-lookup"><span data-stu-id="be4b5-160">Export certificate to PFX</span></span>

<span data-ttu-id="be4b5-161">Экспортируйте объединенный SSL-сертификат с закрытым ключом, с помощью которого был создан запрос сертификата.</span><span class="sxs-lookup"><span data-stu-id="be4b5-161">Export your merged SSL certificate with the private key that your certificate request was generated with.</span></span>

<span data-ttu-id="be4b5-162">Если запрос сертификата был создан с помощью OpenSSL, то вы создали файл закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="be4b5-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="be4b5-163">Чтобы экспортировать сертификат в PFX-файл, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="be4b5-163">To export your certificate to PFX, run the following command.</span></span> <span data-ttu-id="be4b5-164">Замените заполнители _&lt;private-key-file>_ и _&lt;merged-certificate-file>_.</span><span class="sxs-lookup"><span data-stu-id="be4b5-164">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="be4b5-165">При появлении запроса определите пароль для экспорта.</span><span class="sxs-lookup"><span data-stu-id="be4b5-165">When prompted, define an export password.</span></span> <span data-ttu-id="be4b5-166">Позже этот пароль потребуется при передаче SSL-сертификата в службу приложений.</span><span class="sxs-lookup"><span data-stu-id="be4b5-166">You'll use this password when uploading your SSL certificate to App Service later.</span></span>

<span data-ttu-id="be4b5-167">Если вы создали запрос на сертификат с помощью IIS или _Certreq.exe_, установите сертификат на локальный компьютер, а затем [экспортируйте его в PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="be4b5-167">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="be4b5-168">Передача SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="be4b5-168">Upload your SSL certificate</span></span>

<span data-ttu-id="be4b5-169">Чтобы передать SSL-сертификат, щелкните **SSL-сертификаты** в левой области навигации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="be4b5-169">To upload your SSL certificate, click **SSL certificates** in the left navigation of your web app.</span></span>

<span data-ttu-id="be4b5-170">Щелкните **Отправить сертификат**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="be4b5-171">В разделе **PFX-файл сертификата** выберите свой PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="be4b5-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="be4b5-172">В поле **Пароль сертификата** введите пароль, созданный при экспорте PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="be4b5-172">In **Certificate password**, type the password that you created when you exported the PFX file.</span></span>

<span data-ttu-id="be4b5-173">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-173">Click **Upload**.</span></span>

![Передача сертификата](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="be4b5-175">По завершении передачи сертификата службой приложений он появится на странице **SSL-сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-175">When App Service finishes uploading your certificate, it appears in the **SSL certificates** page.</span></span>

![Сертификат добавлен](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="be4b5-177">Привязка SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="be4b5-177">Bind your SSL certificate</span></span>

<span data-ttu-id="be4b5-178">В разделе **SSL-привязки** щелкните **Добавить привязку**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-178">In the **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="be4b5-179">На странице **Добавление привязки SSL** в раскрывающихся списках выберите доменное имя для защиты и используемый сертификат.</span><span class="sxs-lookup"><span data-stu-id="be4b5-179">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span></span>

> [!NOTE]
> <span data-ttu-id="be4b5-180">Если вы передали сертификат, но в раскрывающемся списке **Имя узла** отсутствуют доменные имена, попробуйте обновить страницу браузера.</span><span class="sxs-lookup"><span data-stu-id="be4b5-180">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span></span>
>
>

<span data-ttu-id="be4b5-181">В разделе **Тип SSL** можно выбрать SSL на основе **[указания имени сервера (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** или IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="be4b5-181">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="be4b5-182">**SSL на основе SNI** позволяет добавить несколько привязок SSL на основе SNI.</span><span class="sxs-lookup"><span data-stu-id="be4b5-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="be4b5-183">Этот параметр позволяет использовать несколько SSL-сертификатов для защиты нескольких доменов с одним IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="be4b5-183">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span></span> <span data-ttu-id="be4b5-184">Большинство современных браузеров (включая Internet Explorer, Chrome, Firefox и Opera) поддерживает SNI (более подробную информацию о поддержки браузеров можно найти в статье [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication) (Указание имени сервера)).</span><span class="sxs-lookup"><span data-stu-id="be4b5-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="be4b5-185">**SSL на основе IP-адреса** позволяет добавить только одну привязку SSL на основе IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="be4b5-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="be4b5-186">Этот параметр позволяет использовать только один SSL-сертификат для защиты выделенного общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="be4b5-186">This option allows only one SSL certificate to secure a dedicated public IP address.</span></span> <span data-ttu-id="be4b5-187">Чтобы защитить несколько доменов, необходимо использовать один и тот же SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="be4b5-187">To secure multiple domains, you must secure them all using the same SSL certificate.</span></span> <span data-ttu-id="be4b5-188">Это традиционный вариант привязки SSL.</span><span class="sxs-lookup"><span data-stu-id="be4b5-188">This is the traditional option for SSL binding.</span></span>

<span data-ttu-id="be4b5-189">Щелкните **Добавить привязку**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-189">Click **Add Binding**.</span></span>

![Привязка SSL-сертификата](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="be4b5-191">По завершении передачи сертификата службой приложений он появится в разделах **SSL-привязки**.</span><span class="sxs-lookup"><span data-stu-id="be4b5-191">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span></span>

![Сертификат, привязанный к веб-приложению](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="be4b5-193">Переназначение записи A для SSL на основе IP-адреса</span><span class="sxs-lookup"><span data-stu-id="be4b5-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="be4b5-194">Если вы не используете SSL на основе IP-адреса в веб-приложении, перейдите к разделу [Тестирование протокола HTTPS для личного домена](#test).</span><span class="sxs-lookup"><span data-stu-id="be4b5-194">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="be4b5-195">По умолчанию веб-приложение использует общий общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="be4b5-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="be4b5-196">После привязки сертификата с помощью SSL на основе IP-адреса служба приложений создает выделенный IP-адрес для вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="be4b5-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="be4b5-197">Если с веб-приложением сопоставлена запись A, обновите реестр домена, указав этот новый выделенный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="be4b5-197">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="be4b5-198">Он появится на странице **Личный домен** вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="be4b5-198">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span></span> <span data-ttu-id="be4b5-199">[Скопируйте этот IP-адрес](app-service-web-tutorial-custom-domain.md#info), затем [переназначьте его записи A](app-service-web-tutorial-custom-domain.md#map-an-a-record).</span><span class="sxs-lookup"><span data-stu-id="be4b5-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="be4b5-200">Тестирование HTTPS</span><span class="sxs-lookup"><span data-stu-id="be4b5-200">Test HTTPS</span></span>

<span data-ttu-id="be4b5-201">Нам осталось только убедиться, что протокол HTTPS для личного домена функционирует.</span><span class="sxs-lookup"><span data-stu-id="be4b5-201">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="be4b5-202">В разных браузерах перейдите по адресу `https://<your.custom.domain>`, чтобы узнать, как он обслуживает ваше веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="be4b5-202">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span></span>

![Переход к приложению Azure на портале](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="be4b5-204">Если веб-приложение выдает ошибки проверки сертификата, вероятно, вы используете самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="be4b5-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="be4b5-205">Если это не так, возможно, вы пропустили промежуточные сертификаты при экспорте сертификата в PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="be4b5-205">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="be4b5-206">Принудительное использование HTTPS</span><span class="sxs-lookup"><span data-stu-id="be4b5-206">Enforce HTTPS</span></span>

<span data-ttu-id="be4b5-207">Служба приложений *не* принуждает использовать протокол HTTPS, чтобы кто угодно мог обратиться к веб-приложению с помощью протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="be4b5-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="be4b5-208">Чтобы принудительно использовать HTTPS для веб-приложения, определите для него правило перезаписи в файле _web.config_.</span><span class="sxs-lookup"><span data-stu-id="be4b5-208">To enforce HTTPS for your web app, define a rewrite rule in the _web.config_ file for your web app.</span></span> <span data-ttu-id="be4b5-209">Служба приложений использует этот файл независимо от используемой языковой платформы веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="be4b5-209">App Service uses this file, regardless of the language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="be4b5-210">Для каждого языка используется определенное перенаправление запросов.</span><span class="sxs-lookup"><span data-stu-id="be4b5-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="be4b5-211">ASP.NET MVC может использовать фильтр [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) вместо правила перезаписи в файле _web.config_.</span><span class="sxs-lookup"><span data-stu-id="be4b5-211">ASP.NET MVC can use the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of the rewrite rule in _web.config_.</span></span>

<span data-ttu-id="be4b5-212">Если вы разработчик для .NET, то этот файл должен быть вам в общем и целом знаком.</span><span class="sxs-lookup"><span data-stu-id="be4b5-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="be4b5-213">Он находится в корневом каталоге решения.</span><span class="sxs-lookup"><span data-stu-id="be4b5-213">It is in the root of your solution.</span></span>

<span data-ttu-id="be4b5-214">Кроме того, если вы программируете на PHP, Node.js, Python или Java, существует вероятность того, что этот файл создан от вашего имени в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="be4b5-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="be4b5-215">Подключитесь к конечной точке FTP веб-приложения, следуя указаниям в разделе [Развертывание приложения в службе приложений Azure с помощью FTP или FTPS](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="be4b5-215">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="be4b5-216">Этот файл должен находиться в каталоге _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="be4b5-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="be4b5-217">Если это не так, создайте в этой папке файл _web.config_ со следующим кодом XML:</span><span class="sxs-lookup"><span data-stu-id="be4b5-217">If not, create a _web.config_ file in this folder with the following XML:</span></span>

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

<span data-ttu-id="be4b5-218">Для имеющегося файла _web.config_ скопируйте весь элемент `<rule>` в элемент `configuration/system.webServer/rewrite/rules` в файле _web.config_.</span><span class="sxs-lookup"><span data-stu-id="be4b5-218">For an existing _web.config_ file, copy the entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="be4b5-219">При наличии уже других элементов `<rule>` в файле _web.config_ поместите скопированный элемент `<rule>` перед другими элементами `<rule>`.</span><span class="sxs-lookup"><span data-stu-id="be4b5-219">If there are other `<rule>` elements in your _web.config_, place the copied `<rule>` element before the other `<rule>` elements.</span></span>

<span data-ttu-id="be4b5-220">Это правило возвращает ответ "HTTP 301" (постоянное перенаправление) для протокола HTTPS всякий раз, когда пользователь отправляет HTTP-запрос к вашему веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="be4b5-220">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="be4b5-221">Например, оно перенаправляет `http://contoso.com` в `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="be4b5-221">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

<span data-ttu-id="be4b5-222">Дополнительные сведения о модуле переопределения URL-адресов IIS см. в документации по [модулю переопределения URL-адресов](http://www.iis.net/downloads/microsoft/url-rewrite).</span><span class="sxs-lookup"><span data-stu-id="be4b5-222">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="be4b5-223">Принудительное использование HTTPS для веб-приложений на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="be4b5-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="be4b5-224">Служба приложений на платформе Linux *не* принуждает использовать протокол HTTPS, чтобы кто угодно мог обратиться к веб-приложению с помощью протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="be4b5-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="be4b5-225">Чтобы принудительно использовать HTTPS для веб-приложения, определите для него правило перезаписи в файле _.htaccess_.</span><span class="sxs-lookup"><span data-stu-id="be4b5-225">To enforce HTTPS for your web app, define a rewrite rule in the _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="be4b5-226">Подключитесь к конечной точке FTP веб-приложения, следуя указаниям в разделе [Развертывание приложения в службе приложений Azure с помощью FTP или FTPS](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="be4b5-226">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="be4b5-227">В папке _/home/site/wwwroot_ создайте файл _.htaccess_ со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="be4b5-227">In _/home/site/wwwroot_, create an _.htaccess_ file with the following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="be4b5-228">Это правило возвращает ответ "HTTP 301" (постоянное перенаправление) для протокола HTTPS всякий раз, когда пользователь отправляет HTTP-запрос к вашему веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="be4b5-228">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="be4b5-229">Например, оно перенаправляет `http://contoso.com` в `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="be4b5-229">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="be4b5-230">Автоматизация с помощью сценариев</span><span class="sxs-lookup"><span data-stu-id="be4b5-230">Automate with scripts</span></span>

<span data-ttu-id="be4b5-231">Управлением привязками SSL для веб-приложения можно автоматизировать с помощью сценариев, воспользовавшись [Azure CLI](/cli/azure/install-azure-cli) или [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="be4b5-231">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="be4b5-232">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="be4b5-232">Azure CLI</span></span>

<span data-ttu-id="be4b5-233">Следующая команда передает экспортированный PFX-файл и возвращает отпечаток.</span><span class="sxs-lookup"><span data-stu-id="be4b5-233">The following command uploads an exported PFX file and gets the thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="be4b5-234">Следующая команда добавляет привязку SSL на основе SNI с помощью отпечатка из предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="be4b5-234">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="be4b5-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="be4b5-235">Azure PowerShell</span></span>

<span data-ttu-id="be4b5-236">Следующая команда передает экспортированный PFX-файл и добавляет привязку SSL на основе SNI.</span><span class="sxs-lookup"><span data-stu-id="be4b5-236">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="be4b5-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be4b5-237">Next steps</span></span>

<span data-ttu-id="be4b5-238">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="be4b5-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="be4b5-239">Выбор более высокой ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="be4b5-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="be4b5-240">Привязывание пользовательского SSL-сертификата к службе приложений.</span><span class="sxs-lookup"><span data-stu-id="be4b5-240">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="be4b5-241">Принудительное использование HTTPS для приложения.</span><span class="sxs-lookup"><span data-stu-id="be4b5-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="be4b5-242">Автоматизация привязки SSL-сертификата с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="be4b5-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="be4b5-243">Перейдите к следующему руководству, чтобы научиться использовать сеть доставки содержимого Azure.</span><span class="sxs-lookup"><span data-stu-id="be4b5-243">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="be4b5-244">Добавление сети доставки содержимого (CDN) в службу приложений Azure</span><span class="sxs-lookup"><span data-stu-id="be4b5-244">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
