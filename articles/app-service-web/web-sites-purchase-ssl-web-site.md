---
title: "Добавление SSL-сертификата в приложение службы приложений Azure | Документация Майкрософт"
description: "Сведения о добавлении SSL-сертификата в приложение службы приложений."
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
ms.openlocfilehash: 191dd7240ad15b4936a72bc27a2d0162350f3afb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="ba309-103">Приобретение и настройка сертификата SSL для службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="ba309-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="ba309-104">В этом руководстве вы защитите свое веб-приложение, приобретя SSL-сертификат для **[службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714)**, безопасно сохранив его в [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) и сопоставив с личным доменом.</span><span class="sxs-lookup"><span data-stu-id="ba309-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-to-azure"></a><span data-ttu-id="ba309-105">Шаг 1. Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="ba309-105">Step 1 - Log in to Azure</span></span>

<span data-ttu-id="ba309-106">Войдите на портал Azure по адресу http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="ba309-106">Log in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="ba309-107">Шаг 2. Размещение заказа на SSL-сертификат</span><span class="sxs-lookup"><span data-stu-id="ba309-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="ba309-108">Заказ на SSL-сертификат можно разместить, создав новый [сертификат службы приложения](https://portal.azure.com/#create/Microsoft.SSL) на **портале Azure**.</span><span class="sxs-lookup"><span data-stu-id="ba309-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In the **Azure portal**.</span></span>

![Создание сертификата](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="ba309-110">Введите понятное **имя** для SSL-сертификата, а также **доменное имя**.</span><span class="sxs-lookup"><span data-stu-id="ba309-110">Enter a friendly **Name** for your SSL certificate and enter the **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="ba309-111">Это один из наиболее важных этапов процесса покупки.</span><span class="sxs-lookup"><span data-stu-id="ba309-111">This is one of the most critical parts of the purchase process.</span></span> <span data-ttu-id="ba309-112">Не забудьте ввести правильное имя узла (пользовательский домен), который необходимо защитить с помощью этого сертификата.</span><span class="sxs-lookup"><span data-stu-id="ba309-112">Make sure to enter correct host name (custom domain) that you want to protect with this certificate.</span></span> <span data-ttu-id="ba309-113">**НЕ** добавляйте к имени узла префикс WWW.</span><span class="sxs-lookup"><span data-stu-id="ba309-113">**DO NOT** append the Host name with WWW.</span></span> 
>

<span data-ttu-id="ba309-114">Выберите **подписку**, **группу ресурсов** и **SKU сертификата**.</span><span class="sxs-lookup"><span data-stu-id="ba309-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="ba309-115">Сертификаты службы приложений доступны лишь другим службам приложений в той же подписке.</span><span class="sxs-lookup"><span data-stu-id="ba309-115">App Service Certificates can only be used by other App Services within the same subscription.</span></span>  
>

## <a name="step-3---store-the-certificate-in-azure-key-vault"></a><span data-ttu-id="ba309-116">Шаг 3. Сохранение сертификата в Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ba309-116">Step 3 - Store the certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="ba309-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) — это служба Azure, которая помогает защитить криптографические ключи и секреты, используемые облачными приложениями и службами.</span><span class="sxs-lookup"><span data-stu-id="ba309-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="ba309-118">После завершения покупки SSL-сертификата нужно открыть колонку ресурса [Сертификаты службы приложений](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders).</span><span class="sxs-lookup"><span data-stu-id="ba309-118">Once the SSL Certificate purchase is complete, you need to open [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![вставить изображение для готовности к размещению в хранилище ключей](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="ba309-120">Вы увидите, что состояние сертификата — **Ожидание выдачи**. Это связано с тем, что нужно выполнить еще некоторые действия, прежде чем вы сможете воспользоваться этим сертификатом.</span><span class="sxs-lookup"><span data-stu-id="ba309-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate.</span></span>

<span data-ttu-id="ba309-121">Щелкните **Конфигурация сертификата** в колонке "Свойства сертификата" и затем **Шаг 1. Хранилище**, чтобы сохранить этот сертификат в Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ba309-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** to store this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="ba309-122">В колонке **Состояние Key Vault** щелкните **Репозиторий Key Vault**, чтобы выбрать существующее Key Vault для сохранения этого сертификата, или щелкните **Создать новое Key Vault**, чтобы создать Key Vault в той же подписке и группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ba309-122">From **Key Vault Status** Blade, click **Key Vault Repository** to choose an existing Key Vault to store this certificate **OR Create New Key Vault** to create new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="ba309-123">Расходы на хранение этого сертификата в Azure Key Vault будут минимальными.</span><span class="sxs-lookup"><span data-stu-id="ba309-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="ba309-124">Дополнительные сведения см. в разделе с **[ценами на Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="ba309-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="ba309-125">После выбора репозитория Key Vault для сохранения сертификата на элементе **Хранилище** должны появиться сведения об успешном выполнении.</span><span class="sxs-lookup"><span data-stu-id="ba309-125">Once you have selected the Key Vault Repository to store this certificate in, the **Store** option should show success.</span></span>

![Вставить изображение с успешным сохранением в Key Vault](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-the-domain-ownership"></a><span data-ttu-id="ba309-127">Шаг 4. Проверка владельца домена</span><span class="sxs-lookup"><span data-stu-id="ba309-127">Step 4 - Verify the Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="ba309-128">Сертификаты службы приложений поддерживают три типа проверки домена: проверка через домен, по почте и вручную.</span><span class="sxs-lookup"><span data-stu-id="ba309-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="ba309-129">Подробнее они описаны в разделе [Дополнительно](#advanced).</span><span class="sxs-lookup"><span data-stu-id="ba309-129">These are explained in more details in the [Advanced section](#advanced).</span></span>

<span data-ttu-id="ba309-130">В той же колонке **Конфигурация сертификата**, которую вы использовали в шаге 3, щелкните **Шаг 2. Проверка**.</span><span class="sxs-lookup"><span data-stu-id="ba309-130">From the same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="ba309-131">**Проверка домена**. Этот метод наиболее удобен, **только если** вы **[приобрели личный домен в службе приложений Azure](custom-dns-web-site-buydomains-web-app.md)**.</span><span class="sxs-lookup"><span data-stu-id="ba309-131">**Domain Verification** This is the most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="ba309-132">Нажмите кнопку **Проверить**, чтобы завершить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="ba309-132">Click on **Verify** button to complete this step.</span></span>

![Вставить изображение с проверкой через домен](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="ba309-134">После нажатия кнопки **Проверить** нажимайте кнопку **Обновить** до тех пор, пока для операции **Проверить** не появятся сведения об успешном выполнении.</span><span class="sxs-lookup"><span data-stu-id="ba309-134">After clicking **Verify**, use the **Refresh** button until the **Verify** option should show success.</span></span>

![Вставить изображение с успешной проверкой в Key Vault](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-to-app-service-app"></a><span data-ttu-id="ba309-136">Шаг 5. Назначение сертификата приложению службы приложений</span><span class="sxs-lookup"><span data-stu-id="ba309-136">Step 5 - Assign Certificate to App Service App</span></span>

> [!NOTE]
> <span data-ttu-id="ba309-137">Прежде чем выполнять действия, описанные в этом разделе, необходимо связать личное доменное имя с приложением.</span><span class="sxs-lookup"><span data-stu-id="ba309-137">Before performing the steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="ba309-138">Дополнительные сведения см. в разделе **[Сопоставление имени личного домена с приложением Azure](app-service-web-tutorial-custom-domain.md)**.</span><span class="sxs-lookup"><span data-stu-id="ba309-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="ba309-139">На **[портале Azure](https://portal.azure.com/)** щелкните **Служба приложений** в левой части страницы.</span><span class="sxs-lookup"><span data-stu-id="ba309-139">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="ba309-140">Щелкните имя приложения, которому вы хотите назначить этот сертификат.</span><span class="sxs-lookup"><span data-stu-id="ba309-140">Click the name of your app to which you want to assign this certificate.</span></span>

<span data-ttu-id="ba309-141">В разделе **Параметры** щелкните **SSL-сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="ba309-141">In the **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="ba309-142">Щелкните **Импортировать сертификат службы приложений** и выберите сертификат, который вы приобрели.</span><span class="sxs-lookup"><span data-stu-id="ba309-142">Click **Import App Service Certificate** and select the certificate that you just purchased.</span></span>

![вставить изображение для импорта сертификата](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="ba309-144">В разделе **SSL-привязки** щелкните **Add bindings** (Добавить привязки), а затем в раскрывающихся списках выберите имя домена для защиты с применением SSL, а также используемый сертификат.</span><span class="sxs-lookup"><span data-stu-id="ba309-144">In the **ssl bindings** section Click on **Add bindings**, and use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span></span> <span data-ttu-id="ba309-145">Также можно выбрать SSL на основе **[указания имени сервера (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** или IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="ba309-145">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![вставить изображение для привязок SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="ba309-147">Чтобы сохранить изменения и активировать SSL, щелкните **Добавить привязку** .</span><span class="sxs-lookup"><span data-stu-id="ba309-147">Click **Add Binding** to save the changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="ba309-148">Если вы выбрали **SSL на основе IP-адреса** и личный домен настроен с помощью записи А, нужно выполнить приведенные ниже шаги.</span><span class="sxs-lookup"><span data-stu-id="ba309-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps.</span></span> <span data-ttu-id="ba309-149">Подробнее они описаны в разделе [Дополнительно](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="ba309-149">These are explained in more details in the [Advanced section](#Advanced).</span></span>

<span data-ttu-id="ba309-150">На этом этапе приложение должно открываться с использованием `HTTPS://`, а не `HTTP://`, что подтверждает правильность настройки сертификата.</span><span class="sxs-lookup"><span data-stu-id="ba309-150">At this point, you should be able to visit your app using `HTTPS://` instead of `HTTP://` to verify that the certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="ba309-151">Шаг 6. Задачи управления</span><span class="sxs-lookup"><span data-stu-id="ba309-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="ba309-152">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="ba309-152">Azure CLI</span></span>

<span data-ttu-id="ba309-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Привязка SSL-сертификата к веб-приложению")]</span><span class="sxs-lookup"><span data-stu-id="ba309-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span> 

### <a name="powershell"></a><span data-ttu-id="ba309-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba309-154">PowerShell</span></span>

<span data-ttu-id="ba309-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Привязка SSL-сертификата к веб-приложению")]</span><span class="sxs-lookup"><span data-stu-id="ba309-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="advanced"></a><span data-ttu-id="ba309-156">Расширенная</span><span class="sxs-lookup"><span data-stu-id="ba309-156">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="ba309-157">Проверка принадлежности домена</span><span class="sxs-lookup"><span data-stu-id="ba309-157">Verifying Domain Ownership</span></span>

<span data-ttu-id="ba309-158">Сертификаты службы приложений поддерживают еще два типа проверки домена: проверка по почте и вручную.</span><span class="sxs-lookup"><span data-stu-id="ba309-158">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="ba309-159">Проверка по почте</span><span class="sxs-lookup"><span data-stu-id="ba309-159">Mail Verification</span></span>

<span data-ttu-id="ba309-160">Проверочное сообщение уже было отправлено по адресам электронной почты, связанным с этим пользовательским доменом.</span><span class="sxs-lookup"><span data-stu-id="ba309-160">Verification email has already been sent to the Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="ba309-161">Чтобы завершить шаг проверки по электронной почте, откройте сообщение и щелкните ссылку для проверки.</span><span class="sxs-lookup"><span data-stu-id="ba309-161">To complete the Email verification step, open the email and click the verification link.</span></span>

![Вставить изображение с проверкой по почте](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="ba309-163">Если необходимо повторно отправить проверочное сообщение, нажмите кнопку **Переотправить сообщение электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="ba309-163">If you need to resend the verification email, click the **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="ba309-164">Проверка вручную</span><span class="sxs-lookup"><span data-stu-id="ba309-164">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba309-165">Проверка веб-страницы HTML (работает только с номером SKU сертификата уровня "Стандартный").</span><span class="sxs-lookup"><span data-stu-id="ba309-165">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="ba309-166">Создайте HTML-файл **starfield.html**.</span><span class="sxs-lookup"><span data-stu-id="ba309-166">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="ba309-167">Содержимое этого файла должно полностью совпадать с именем токена проверки домена.</span><span class="sxs-lookup"><span data-stu-id="ba309-167">Content of this file should be the exact name of the Domain Verification Token.</span></span> <span data-ttu-id="ba309-168">(Токен можно скопировать из колонки состояния проверки домена.)</span><span class="sxs-lookup"><span data-stu-id="ba309-168">(You can copy the token from the Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="ba309-169">Отправьте этот файл в корень веб-сервера, на котором размещается ваш домен `/.well-known/pki-validation/starfield.html`.</span><span class="sxs-lookup"><span data-stu-id="ba309-169">Upload this file at the root of the web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="ba309-170">Нажмите кнопку **Обновить**, чтобы обновить состояние сертификата после завершения проверки.</span><span class="sxs-lookup"><span data-stu-id="ba309-170">Click **Refresh** to update the certificate status after verification is completed.</span></span> <span data-ttu-id="ba309-171">Проверка может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ba309-171">It might take few minutes for verification to complete.</span></span>

> [!TIP]
> <span data-ttu-id="ba309-172">Проверьте терминал с помощью `curl -G http://<domain>/.well-known/pki-validation/starfield.html`, ответ должен содержать `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="ba309-172">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` the response should contain the `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="ba309-173">Проверка записей типа TXT DNS</span><span class="sxs-lookup"><span data-stu-id="ba309-173">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="ba309-174">С помощью диспетчера DNS создайте запись типа TXT в поддомене `@` со значением, идентичным токену проверки домена.</span><span class="sxs-lookup"><span data-stu-id="ba309-174">Using your DNS manager, Create a TXT record on the `@` subdomain with value equal to the Domain Verification Token.</span></span>
1. <span data-ttu-id="ba309-175">Нажмите кнопку **Обновить**, чтобы обновить состояние сертификата после завершения проверки.</span><span class="sxs-lookup"><span data-stu-id="ba309-175">Click **“Refresh”** to update the Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="ba309-176">Нужно создать запись типа TXT в `@.<domain>` со значением `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="ba309-176">You need to create a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-to-app-service-app"></a><span data-ttu-id="ba309-177">Назначение сертификата приложению службы приложений</span><span class="sxs-lookup"><span data-stu-id="ba309-177">Assign Certificate to App Service App</span></span>

<span data-ttu-id="ba309-178">Если выбран **вариант SSL-подключения на основе IP** и пользовательский домен настроен с помощью записи А, необходимо выполнить следующие дополнительные шаги:</span><span class="sxs-lookup"><span data-stu-id="ba309-178">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps:</span></span>

<span data-ttu-id="ba309-179">После настройки привязки SSL-подключения на основе IP вашему веб-приложению будет предоставлен выделенный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="ba309-179">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="ba309-180">Этот IP-адрес можно найти на странице **Личный домен** в разделе параметров приложения прямо над разделом **Имена узлов**.</span><span class="sxs-lookup"><span data-stu-id="ba309-180">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span></span> <span data-ttu-id="ba309-181">Он указывается как **Внешний IP-адрес**</span><span class="sxs-lookup"><span data-stu-id="ba309-181">It is listed as **External IP Address**</span></span>

![вставить изображение для SSL на основе IP](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="ba309-183">Обратите внимание, что этот IP-адрес отличается от виртуального IP-адреса, который использовался ранее для настройки записи A для вашего домена.</span><span class="sxs-lookup"><span data-stu-id="ba309-183">Note that this IP address is different than the virtual IP address used previously to configure the A record for your domain.</span></span> <span data-ttu-id="ba309-184">Если выбрано использование SSL-подключения на основе SNI или если не настроено использование SSL, адрес для этой записи не указывается.</span><span class="sxs-lookup"><span data-stu-id="ba309-184">If you are configured to use SNI based SSL, or are not configured to use SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="ba309-185">С помощью средств, предоставляемых регистратором имени домена, измените запись A для имени пользовательского домена, указав IP-адрес из предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="ba309-185">Using the tools provided by your domain name registrar, modify the A record for your custom domain name to point to the IP address from the previous step.</span></span>

## <a name="rekey-and-sync-the-certificate"></a><span data-ttu-id="ba309-186">Повторное создание ключей и синхронизация сертификата</span><span class="sxs-lookup"><span data-stu-id="ba309-186">Rekey and Sync the Certificate</span></span>

<span data-ttu-id="ba309-187">Если вам когда-либо придется повторно назначить ключ сертификата, выберите **Повторное создание ключей и синхронизация** в колонке **Свойства сертификата**.</span><span class="sxs-lookup"><span data-stu-id="ba309-187">If you ever need to Rekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="ba309-188">Для запуска процесса нажмите кнопку **Повторное создание ключей**.</span><span class="sxs-lookup"><span data-stu-id="ba309-188">Click **Rekey** Button to initiate the process.</span></span> <span data-ttu-id="ba309-189">Этот процесс может занять от 1 до 10 минут.</span><span class="sxs-lookup"><span data-stu-id="ba309-189">This process can take 1-10 minutes to complete.</span></span>

![вставить изображение для повторного создания ключа SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="ba309-191">При создании ключа развертывается новый сертификат, выданный центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="ba309-191">Rekeying your certificate rolls the certificate with a new certificate issued from the certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba309-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba309-192">Next Steps</span></span>

* [<span data-ttu-id="ba309-193">Добавление сети доставки содержимого</span><span class="sxs-lookup"><span data-stu-id="ba309-193">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)