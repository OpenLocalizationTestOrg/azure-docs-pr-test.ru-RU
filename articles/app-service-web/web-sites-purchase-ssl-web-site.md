---
title: "aaaAdd SSL-сертификатов tooyour приложение службы приложений Azure | Документы Microsoft"
description: "Узнайте, как tooadd SSL-сертификат tooyour приложением служб приложений."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="314c0-103">Приобретение и настройка сертификата SSL для службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="314c0-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="314c0-104">В этом руководстве вы защитите свое веб-приложение, приобретя SSL-сертификат для **[службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714)**, безопасно сохранив его в [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) и сопоставив с личным доменом.</span><span class="sxs-lookup"><span data-stu-id="314c0-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-tooazure"></a><span data-ttu-id="314c0-105">Шаг 1. вход tooAzure</span><span class="sxs-lookup"><span data-stu-id="314c0-105">Step 1 - Log in tooAzure</span></span>

<span data-ttu-id="314c0-106">Войдите в toohello портал Azure по адресу http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="314c0-106">Log in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="314c0-107">Шаг 2. Размещение заказа на SSL-сертификат</span><span class="sxs-lookup"><span data-stu-id="314c0-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="314c0-108">Можно разместить заказ SSL-сертификат, создав новую [сертификат службы приложения](https://portal.azure.com/#create/Microsoft.SSL) в hello **портал Azure**.</span><span class="sxs-lookup"><span data-stu-id="314c0-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In hello **Azure portal**.</span></span>

![Создание сертификата](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="314c0-110">Введите понятное **имя** для протокола SSL сертификатов и введите hello **имя домена**</span><span class="sxs-lookup"><span data-stu-id="314c0-110">Enter a friendly **Name** for your SSL certificate and enter hello **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="314c0-111">Это одна из наиболее важных частей hello hello процесса покупки.</span><span class="sxs-lookup"><span data-stu-id="314c0-111">This is one of hello most critical parts of hello purchase process.</span></span> <span data-ttu-id="314c0-112">Убедитесь, что tooenter Исправьте имя узла (пользовательский домен), которые должны tooprotect с помощью этого сертификата.</span><span class="sxs-lookup"><span data-stu-id="314c0-112">Make sure tooenter correct host name (custom domain) that you want tooprotect with this certificate.</span></span> <span data-ttu-id="314c0-113">**Нет** Добавление hello имени узла с веб-публикации.</span><span class="sxs-lookup"><span data-stu-id="314c0-113">**DO NOT** append hello Host name with WWW.</span></span> 
>

<span data-ttu-id="314c0-114">Выберите **подписку**, **группу ресурсов** и **SKU сертификата**.</span><span class="sxs-lookup"><span data-stu-id="314c0-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="314c0-115">Сертификаты службы приложений может использоваться только в другие службы приложения hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="314c0-115">App Service Certificates can only be used by other App Services within hello same subscription.</span></span>  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a><span data-ttu-id="314c0-116">Шаг 3 — хранить hello сертификат в хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="314c0-116">Step 3 - Store hello certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="314c0-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) — это служба Azure, которая помогает защитить криптографические ключи и секреты, используемые облачными приложениями и службами.</span><span class="sxs-lookup"><span data-stu-id="314c0-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="314c0-118">После завершения hello покупки SSL-сертификат необходимо tooopen [сертификатов службы приложений](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) колонки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="314c0-118">Once hello SSL Certificate purchase is complete, you need tooopen [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![Вставьте изображение готово toostore в кв](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="314c0-120">Вы заметите, что состояние сертификата — **«Ожидающие выдачи»** имеется несколько дополнительных действий необходимо toocomplete перед началом использования этого сертификата.</span><span class="sxs-lookup"><span data-stu-id="314c0-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need toocomplete before you can start using this certificate.</span></span>

<span data-ttu-id="314c0-121">Нажмите кнопку **конфигурация сертификата** в колонке свойства сертификата и нажмите кнопку **шаг 1: хранилище** toostore этот сертификат в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="314c0-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** toostore this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="314c0-122">Из **состояния хранилища ключей** колонке нажмите кнопку **репозитория хранилища ключей** toochoose существующего хранилища ключей toostore этот сертификат **или создать новое хранилище ключей** toocreate новый ключ в хранилище внутри же подписке и группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="314c0-122">From **Key Vault Status** Blade, click **Key Vault Repository** toochoose an existing Key Vault toostore this certificate **OR Create New Key Vault** toocreate new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="314c0-123">Расходы на хранение этого сертификата в Azure Key Vault будут минимальными.</span><span class="sxs-lookup"><span data-stu-id="314c0-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="314c0-124">Дополнительные сведения см. в разделе с **[ценами на Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="314c0-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="314c0-125">После выбора toostore hello репозитория хранилища ключ этого сертификата в, hello **хранилища** параметр должен показывать ход.</span><span class="sxs-lookup"><span data-stu-id="314c0-125">Once you have selected hello Key Vault Repository toostore this certificate in, hello **Store** option should show success.</span></span>

![Вставить изображение с успешным сохранением в Key Vault](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a><span data-ttu-id="314c0-127">Шаг 4. Проверка hello владельца домена</span><span class="sxs-lookup"><span data-stu-id="314c0-127">Step 4 - Verify hello Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="314c0-128">Сертификаты службы приложений поддерживают три типа проверки домена: проверка через домен, по почте и вручную.</span><span class="sxs-lookup"><span data-stu-id="314c0-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="314c0-129">Эти механизмы описаны более подробно hello [расширенный раздел](#advanced).</span><span class="sxs-lookup"><span data-stu-id="314c0-129">These are explained in more details in hello [Advanced section](#advanced).</span></span>

<span data-ttu-id="314c0-130">Из hello же **настройку сертификата** колонки, который использовался в шаге 3, нажмите кнопку **шаг 2: проверка**.</span><span class="sxs-lookup"><span data-stu-id="314c0-130">From hello same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="314c0-131">**Проверка домена** это наиболее удобный процесс hello **, только если** у вас есть  **[приобретенному личного домена службы приложений Azure.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="314c0-131">**Domain Verification** This is hello most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="314c0-132">Щелкните **проверьте** кнопку toocomplete этот шаг.</span><span class="sxs-lookup"><span data-stu-id="314c0-132">Click on **Verify** button toocomplete this step.</span></span>

![Вставить изображение с проверкой через домен](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="314c0-134">После нажатия кнопки **проверьте**, использовать hello **обновление** кнопки до hello **проверьте** параметр должен показывать ход.</span><span class="sxs-lookup"><span data-stu-id="314c0-134">After clicking **Verify**, use hello **Refresh** button until hello **Verify** option should show success.</span></span>

![Вставить изображение с успешной проверкой в Key Vault](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a><span data-ttu-id="314c0-136">Шаг 5 – назначить tooApp сертификата службы приложений</span><span class="sxs-lookup"><span data-stu-id="314c0-136">Step 5 - Assign Certificate tooApp Service App</span></span>

> [!NOTE]
> <span data-ttu-id="314c0-137">Перед выполнением действия hello в этом разделе, нужно, чтобы связанные пользовательское доменное имя вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="314c0-137">Before performing hello steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="314c0-138">Дополнительные сведения см. в разделе **[Сопоставление имени личного домена с приложением Azure](app-service-web-tutorial-custom-domain.md)**.</span><span class="sxs-lookup"><span data-stu-id="314c0-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="314c0-139">В hello  **[портал Azure](https://portal.azure.com/)**, нажмите кнопку hello **службы приложений** параметр hello левой части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="314c0-139">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="314c0-140">Щелкните имя hello toowhich вашего приложения требуется tooassign этот сертификат.</span><span class="sxs-lookup"><span data-stu-id="314c0-140">Click hello name of your app toowhich you want tooassign this certificate.</span></span>

<span data-ttu-id="314c0-141">В hello **параметры**, нажмите кнопку **SSL-сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="314c0-141">In hello **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="314c0-142">Нажмите кнопку **импорта сертификата службы приложения** и hello выберите сертификат, который вы приобрели.</span><span class="sxs-lookup"><span data-stu-id="314c0-142">Click **Import App Service Certificate** and select hello certificate that you just purchased.</span></span>

![вставить изображение для импорта сертификата](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="314c0-144">В hello **привязки ssl** статьи щелкните на **добавления привязок**и используется имя hello раскрывающихся списках tooselect hello домена toosecure с протоколом SSL, а hello toouse сертификат.</span><span class="sxs-lookup"><span data-stu-id="314c0-144">In hello **ssl bindings** section Click on **Add bindings**, and use hello dropdowns tooselect hello domain name toosecure with SSL, and hello certificate toouse.</span></span> <span data-ttu-id="314c0-145">Можно также выбрать, будет ли toouse  **[Указание имени сервера (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  или SSL на основе IP.</span><span class="sxs-lookup"><span data-stu-id="314c0-145">You may also select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![вставить изображение для привязок SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="314c0-147">Нажмите кнопку **Добавление привязки** toosave hello изменения и включить SSL.</span><span class="sxs-lookup"><span data-stu-id="314c0-147">Click **Add Binding** toosave hello changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="314c0-148">Если вы выбрали **SSL на основе IP** и личный домен настраивается с помощью записи, необходимо выполнить следующие дополнительные шаги hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps.</span></span> <span data-ttu-id="314c0-149">Эти механизмы описаны более подробно hello [расширенный раздел](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="314c0-149">These are explained in more details in hello [Advanced section](#Advanced).</span></span>

<span data-ttu-id="314c0-150">На этом этапе вы должен быть доступ toovisit приложения с использованием `HTTPS://` вместо `HTTP://` tooverify, hello сертификат был настроен правильно.</span><span class="sxs-lookup"><span data-stu-id="314c0-150">At this point, you should be able toovisit your app using `HTTPS://` instead of `HTTP://` tooverify that hello certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="314c0-151">Шаг 6. Задачи управления</span><span class="sxs-lookup"><span data-stu-id="314c0-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="314c0-152">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="314c0-152">Azure CLI</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a><span data-ttu-id="314c0-153">PowerShell</span><span class="sxs-lookup"><span data-stu-id="314c0-153">PowerShell</span></span>

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a><span data-ttu-id="314c0-154">Расширенная</span><span class="sxs-lookup"><span data-stu-id="314c0-154">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="314c0-155">Проверка принадлежности домена</span><span class="sxs-lookup"><span data-stu-id="314c0-155">Verifying Domain Ownership</span></span>

<span data-ttu-id="314c0-156">Сертификаты службы приложений поддерживают еще два типа проверки домена: проверка по почте и вручную.</span><span class="sxs-lookup"><span data-stu-id="314c0-156">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="314c0-157">Проверка по почте</span><span class="sxs-lookup"><span data-stu-id="314c0-157">Mail Verification</span></span>

<span data-ttu-id="314c0-158">Уже было отправлено письмо с подтверждением toohello адреса электронной почты, связанной с этим доменом пользовательских.</span><span class="sxs-lookup"><span data-stu-id="314c0-158">Verification email has already been sent toohello Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="314c0-159">этап проверки электронной почты toocomplete hello, открыть сообщение hello и щелкните ссылку проверки hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-159">toocomplete hello Email verification step, open hello email and click hello verification link.</span></span>

![Вставить изображение с проверкой по почте](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="314c0-161">При необходимости проверочное сообщение hello tooresend щелкните hello **отправить повторно** кнопки.</span><span class="sxs-lookup"><span data-stu-id="314c0-161">If you need tooresend hello verification email, click hello **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="314c0-162">Проверка вручную</span><span class="sxs-lookup"><span data-stu-id="314c0-162">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="314c0-163">Проверка веб-страницы HTML (работает только с номером SKU сертификата уровня "Стандартный").</span><span class="sxs-lookup"><span data-stu-id="314c0-163">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="314c0-164">Создайте HTML-файл **starfield.html**.</span><span class="sxs-lookup"><span data-stu-id="314c0-164">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="314c0-165">Содержимое этого файла должно быть hello точное имя hello токена проверки домена.</span><span class="sxs-lookup"><span data-stu-id="314c0-165">Content of this file should be hello exact name of hello Domain Verification Token.</span></span> <span data-ttu-id="314c0-166">(Вы можете скопировать hello маркер из hello колонке состояния проверки домена)</span><span class="sxs-lookup"><span data-stu-id="314c0-166">(You can copy hello token from hello Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="314c0-167">Отправить файл в корне hello hello веб-сервере с доменом`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="314c0-167">Upload this file at hello root of hello web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="314c0-168">Нажмите кнопку **обновление** tooupdate состояние сертификата hello после завершения проверки.</span><span class="sxs-lookup"><span data-stu-id="314c0-168">Click **Refresh** tooupdate hello certificate status after verification is completed.</span></span> <span data-ttu-id="314c0-169">Он может занять несколько минут для проверки toocomplete.</span><span class="sxs-lookup"><span data-stu-id="314c0-169">It might take few minutes for verification toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="314c0-170">Убедитесь в терминалов с использованием `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello ответ должен содержать hello `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="314c0-170">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello response should contain hello `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="314c0-171">Проверка записей типа TXT DNS</span><span class="sxs-lookup"><span data-stu-id="314c0-171">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="314c0-172">В диспетчере DNS, создайте запись TXT на hello `@` дочерний домен с toohello равно значение токена проверки домена.</span><span class="sxs-lookup"><span data-stu-id="314c0-172">Using your DNS manager, Create a TXT record on hello `@` subdomain with value equal toohello Domain Verification Token.</span></span>
1. <span data-ttu-id="314c0-173">Нажмите кнопку **«Обновить»** tooupdate hello состояние сертификата после завершения проверки.</span><span class="sxs-lookup"><span data-stu-id="314c0-173">Click **“Refresh”** tooupdate hello Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="314c0-174">Требуется toocreate TXT-запись на `@.<domain>` со значением `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="314c0-174">You need toocreate a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-tooapp-service-app"></a><span data-ttu-id="314c0-175">Назначьте tooApp сертификата службы приложений</span><span class="sxs-lookup"><span data-stu-id="314c0-175">Assign Certificate tooApp Service App</span></span>

<span data-ttu-id="314c0-176">Если вы выбрали **SSL на основе IP** и личный домен настраивается с помощью записи, необходимо выполнить следующие дополнительные шаги hello:</span><span class="sxs-lookup"><span data-stu-id="314c0-176">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps:</span></span>

<span data-ttu-id="314c0-177">После настройки SSL-привязку на основе IP, выделенный IP-адрес назначается tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="314c0-177">After you have configured an IP based SSL binding, a dedicated IP address is assigned tooyour app.</span></span> <span data-ttu-id="314c0-178">Этот IP-адрес можно найти на hello **пользовательский домен** в разделе параметров приложения, сразу над hello **имена узлов** раздела.</span><span class="sxs-lookup"><span data-stu-id="314c0-178">You can find this IP address on hello **Custom domain** page under settings of your app, right above hello **Hostnames** section.</span></span> <span data-ttu-id="314c0-179">Он указывается как **Внешний IP-адрес**</span><span class="sxs-lookup"><span data-stu-id="314c0-179">It is listed as **External IP Address**</span></span>

![вставить изображение для SSL на основе IP](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="314c0-181">Обратите внимание, что этот IP-адрес отличается от hello виртуальный IP-адрес используется ранее tooconfigure hello A-запись для домена.</span><span class="sxs-lookup"><span data-stu-id="314c0-181">Note that this IP address is different than hello virtual IP address used previously tooconfigure hello A record for your domain.</span></span> <span data-ttu-id="314c0-182">Если для пользователя настроен toouse SNI SSL на основе или не настроена toouse SSL, не будет приведено адреса для данной записи.</span><span class="sxs-lookup"><span data-stu-id="314c0-182">If you are configured toouse SNI based SSL, or are not configured toouse SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="314c0-183">С помощью инструментов hello регистратора доменных имен, измените запись для вашего личного домена имя toopoint toohello IP-адрес из предыдущего шага hello hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-183">Using hello tools provided by your domain name registrar, modify hello A record for your custom domain name toopoint toohello IP address from hello previous step.</span></span>

## <a name="rekey-and-sync-hello-certificate"></a><span data-ttu-id="314c0-184">Повторное создание ключа и синхронизировать hello сертификата</span><span class="sxs-lookup"><span data-stu-id="314c0-184">Rekey and Sync hello Certificate</span></span>

<span data-ttu-id="314c0-185">Если в дальнейшем tooRekey свой сертификат, выберите **повторное создание ключа и синхронизировать** меню **свойства сертификата** колонку.</span><span class="sxs-lookup"><span data-stu-id="314c0-185">If you ever need tooRekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="314c0-186">Нажмите кнопку **повторное создание ключа** кнопку tooinitiate hello процесса.</span><span class="sxs-lookup"><span data-stu-id="314c0-186">Click **Rekey** Button tooinitiate hello process.</span></span> <span data-ttu-id="314c0-187">Этот процесс может занять toocomplete 1 – 10 минут.</span><span class="sxs-lookup"><span data-stu-id="314c0-187">This process can take 1-10 minutes toocomplete.</span></span>

![вставить изображение для повторного создания ключа SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="314c0-189">Смена ключей сертификата откатывается hello сертификата на новый сертификат, выданный центром сертификации hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-189">Rekeying your certificate rolls hello certificate with a new certificate issued from hello certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="314c0-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="314c0-190">Next Steps</span></span>

* [<span data-ttu-id="314c0-191">Добавление сети доставки содержимого</span><span class="sxs-lookup"><span data-stu-id="314c0-191">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)