---
title: "aaa \"Включить HTTPS для пользовательского домена Azure CDN | Документы Microsoft»"
description: "Узнайте, как tooenable HTTPS на конечной точке Azure CDN с помощью пользовательского домена."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="b873d-103">Включение протокола HTTPS для личного домена Azure CDN</span><span class="sxs-lookup"><span data-stu-id="b873d-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="b873d-104">HTTPS поддержку пользовательских доменов Azure CDN позволяет toodeliver защищенного содержимого через SSL с помощью собственного домена tooimprove имя hello безопасность данных во время передачи.</span><span class="sxs-lookup"><span data-stu-id="b873d-104">HTTPS support for Azure CDN custom domains enables you toodeliver secure content via SSL using your own domain name tooimprove hello security of data while in transit.</span></span> <span data-ttu-id="b873d-105">tooenable-сквозной рабочий процесс Hello HTTPS для пользовательского домена упрощено посредством включения одним щелчком, полное управление сертификатами и все с без дополнительных затрат.</span><span class="sxs-lookup"><span data-stu-id="b873d-105">hello end-to-end workflow tooenable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="b873d-106">Это критическое tooensure hello конфиденциальность и целостность данных всех вашего веб-приложения конфиденциальных данных во время передачи.</span><span class="sxs-lookup"><span data-stu-id="b873d-106">It's critical tooensure hello privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="b873d-107">С помощью hello, протокол HTTPS обеспечивает шифрование конфиденциальных данных при отправке по Интернету "hello".</span><span class="sxs-lookup"><span data-stu-id="b873d-107">Using hello HTTPS protocol ensures that your sensitive data is encrypted when it is sent across hello internet.</span></span> <span data-ttu-id="b873d-108">Он обеспечивает доверие, аутентификацию и защиту веб-приложений от атак.</span><span class="sxs-lookup"><span data-stu-id="b873d-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="b873d-109">В настоящее время Azure CDN поддерживает HTTPS в конечной точке CDN.</span><span class="sxs-lookup"><span data-stu-id="b873d-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="b873d-110">Например, при создании конечной точки CDN из Azure CDN (например, https://contoso.azureedge.net) протокол HTTPS включен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b873d-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="b873d-111">Теперь благодаря поддержке HTTPS для личных доменов (например, https://www.contoso.com) вы можете также включить для них безопасную доставку.</span><span class="sxs-lookup"><span data-stu-id="b873d-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="b873d-112">Ниже приведены некоторые ключевые атрибуты hello функции HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b873d-112">Some of hello key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="b873d-113">Никаких дополнительных затрат: вам не придется оплачивать приобретение или продление сертификата или платить за трафик, переданный по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b873d-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="b873d-114">Вы платите только за ГБ исходящих из hello CDN.</span><span class="sxs-lookup"><span data-stu-id="b873d-114">You just pay for GB egress from hello CDN.</span></span>

- <span data-ttu-id="b873d-115">Простое включение: один щелчок Подготовка доступна из hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b873d-115">Simple enablement: One click provisioning is available from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b873d-116">Также можно использовать API-интерфейса REST или другие функции hello tooenable средств разработчика.</span><span class="sxs-lookup"><span data-stu-id="b873d-116">You can also use REST API or other developer tools tooenable hello feature.</span></span>

- <span data-ttu-id="b873d-117">Полноценное управление сертификатами: закупка всех сертификатов и управление ими осуществляется без вашего участия.</span><span class="sxs-lookup"><span data-stu-id="b873d-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="b873d-118">Сертификаты будут автоматически подготовлены и обновить предыдущие tooexpiration.</span><span class="sxs-lookup"><span data-stu-id="b873d-118">Certificates are automatically provisioned and renewed prior tooexpiration.</span></span> <span data-ttu-id="b873d-119">Это полностью удаляет hello риск прерывания работы службы в результате срок действия сертификата истек.</span><span class="sxs-lookup"><span data-stu-id="b873d-119">This completely removes hello risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="b873d-120">Предыдущий tooenabling HTTPS поддерживает, должны уже установлен [личный домен Azure CDN](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b873d-120">Prior tooenabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-hello-feature"></a><span data-ttu-id="b873d-121">Шаг 1: Включение функции hello</span><span class="sxs-lookup"><span data-stu-id="b873d-121">Step 1: Enabling hello feature</span></span> 

1. <span data-ttu-id="b873d-122">В hello [портал Azure](https://portal.azure.com), Обзор tooyour Verizon стандартного или расширенного профиля CDN.</span><span class="sxs-lookup"><span data-stu-id="b873d-122">In hello [Azure portal](https://portal.azure.com), browse tooyour Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="b873d-123">В списке hello конечных точек выберите hello конечной точки, содержащий пользовательский домен.</span><span class="sxs-lookup"><span data-stu-id="b873d-123">In hello list of endpoints, click hello endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="b873d-124">Щелкните hello пользовательский домен, для которого требуется tooenable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b873d-124">Click hello custom domain for which you want tooenable HTTPS.</span></span>

    ![Колонка "Конечная точка"](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="b873d-126">Нажмите кнопку **на** tooenable HTTPS и сохранить изменение hello.</span><span class="sxs-lookup"><span data-stu-id="b873d-126">Click **On** tooenable HTTPS and save hello change.</span></span>

    ![Диалоговое окно "Настраиваемый HTTPS"](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="b873d-128">Шаг 2. Проверка домена</span><span class="sxs-lookup"><span data-stu-id="b873d-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="b873d-129">Чтобы поддержка HTTPS стала активной для личного домена, необходимо выполнить его проверку.</span><span class="sxs-lookup"><span data-stu-id="b873d-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="b873d-130">У вас есть 6 дней tooapprove hello предметной.</span><span class="sxs-lookup"><span data-stu-id="b873d-130">You have 6 business days tooapprove hello domain.</span></span> <span data-ttu-id="b873d-131">Если подтверждение не поступит в течение этого срока, запрос будет отменен.</span><span class="sxs-lookup"><span data-stu-id="b873d-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="b873d-132">После включения HTTPS на личный домен, наш поставщик сертификата HTTPS DigiCert проверка владения доменом, обратившись в службу hello адресную для домена, в зависимости от WHOIS адресную информацию, по электронной почте (по умолчанию) или по телефону.</span><span class="sxs-lookup"><span data-stu-id="b873d-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting hello registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="b873d-133">DigiCert отправляет hello проверки электронной почты toohello ниже адреса.</span><span class="sxs-lookup"><span data-stu-id="b873d-133">DigiCert will also send hello verification email toohello below addresses.</span></span> <span data-ttu-id="b873d-134">Если сведения о регистрируемом пользователе Whois являются частными, убедитесь, что возможно утверждение непосредственно с одного из этих адресов.</span><span class="sxs-lookup"><span data-stu-id="b873d-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="b873d-135">admin@<доменное_имя.com> administrator@<доменное_имя.com></span><span class="sxs-lookup"><span data-stu-id="b873d-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="b873d-136">webmaster@<доменное_имя.com></span><span class="sxs-lookup"><span data-stu-id="b873d-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="b873d-137">hostmaster@<доменное_имя.com></span><span class="sxs-lookup"><span data-stu-id="b873d-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="b873d-138">postmaster@<доменное_имя.com></span><span class="sxs-lookup"><span data-stu-id="b873d-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="b873d-139">При получении электронной почты hello, есть два способа проверки:</span><span class="sxs-lookup"><span data-stu-id="b873d-139">Upon receiving hello email, you have two verification options:</span></span>

1. <span data-ttu-id="b873d-140">Вы можете утвердить все будущие заказов через hello учетную запись для hello одного корневого домена, например consoto.com. Это рекомендуемый подход, если вы планируете tooadd дополнительных пользовательских доменов в будущем для hello hello же корневого домена.</span><span class="sxs-lookup"><span data-stu-id="b873d-140">You can approve all future orders placed through hello same account for hello same root domain, e.g. consoto.com. This is a recommended approach if you are planning tooadd additional custom domains in hello future for hello same root domain.</span></span>
 
2. <span data-ttu-id="b873d-141">Можно просто одобрите hello определенного имени узла в этом запросе.</span><span class="sxs-lookup"><span data-stu-id="b873d-141">You can just approve hello specific host name used in this request.</span></span> <span data-ttu-id="b873d-142">Для последующих запросов потребуются дополнительные утверждения.</span><span class="sxs-lookup"><span data-stu-id="b873d-142">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="b873d-143">Пример сообщения электронной почты:</span><span class="sxs-lookup"><span data-stu-id="b873d-143">Example email:</span></span>
    
    ![Диалоговое окно "Настраиваемый HTTPS"](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="b873d-145">После утверждения DigiCert добавите сертификат SAN toohello имя пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="b873d-145">After approval, DigiCert will add your custom domain name toohello SAN certificate.</span></span> <span data-ttu-id="b873d-146">Hello сертификат будет действителен в течение одного года и будет автоматически обновлен до его действия истек.</span><span class="sxs-lookup"><span data-stu-id="b873d-146">hello certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a><span data-ttu-id="b873d-147">Шаг 3: Дождитесь распространения hello, а затем начать использовать функции</span><span class="sxs-lookup"><span data-stu-id="b873d-147">Step 3: Wait for hello propagation then start using your feature</span></span>

<span data-ttu-id="b873d-148">После проверки имени домена hello займет too6 8 часов для hello пользовательского домена HTTPS функция toobe active.</span><span class="sxs-lookup"><span data-stu-id="b873d-148">After hello domain name is validated it will take up too6-8 hours for hello custom domain HTTPS feature toobe active.</span></span> <span data-ttu-id="b873d-149">После завершения процесса hello hello «пользовательские HTTPS» в hello портал Azure состояние слишком «Enabled».</span><span class="sxs-lookup"><span data-stu-id="b873d-149">After hello process is complete, hello "custom HTTPS" status in hello Azure portal will be set too"Enabled".</span></span> <span data-ttu-id="b873d-150">Теперь компонент HTTPS можно использовать для личного домена.</span><span class="sxs-lookup"><span data-stu-id="b873d-150">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="b873d-151">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="b873d-151">Frequently asked questions</span></span>

1. <span data-ttu-id="b873d-152">*Кто является поставщиком сертификата hello и типа используемого сертификата используется?*</span><span class="sxs-lookup"><span data-stu-id="b873d-152">*Who is hello certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="b873d-153">Мы используем сертификат альтернативного имени субъекта (SAN), предоставленный DigiCert.</span><span class="sxs-lookup"><span data-stu-id="b873d-153">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="b873d-154">С помощью одного сертификата SAN можно защитить несколько полных доменных имен.</span><span class="sxs-lookup"><span data-stu-id="b873d-154">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="b873d-155">*Могу ли я использовать выделенный сертификат?*</span><span class="sxs-lookup"><span data-stu-id="b873d-155">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="b873d-156">В настоящее время не, но его на hello стратегия.</span><span class="sxs-lookup"><span data-stu-id="b873d-156">Not currently, but it's on hello roadmap.</span></span>

3. <span data-ttu-id="b873d-157">*Что делать, если проверочное сообщение hello домена не выводится из DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="b873d-157">*What if I don't receive hello domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="b873d-158">Если вы не получите электронное сообщение в течение 24 часов, обратитесь в корпорацию Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b873d-158">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="b873d-159">*Не окажется ли сертификат SAN менее безопасным, чем выделенный сертификат?*</span><span class="sxs-lookup"><span data-stu-id="b873d-159">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="b873d-160">Cert SAN, что же стандартов шифрование и безопасность, что выделенный cert hello следующим образом. Чтобы дополнительно обезопасить сервер, для всех выданных сертификатов SSL используется алгоритм SHA-256.</span><span class="sxs-lookup"><span data-stu-id="b873d-160">A SAN cert follows hello same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="b873d-161">*Можно ли использовать личный домен HTTPS с Azure CDN от Akamai?*</span><span class="sxs-lookup"><span data-stu-id="b873d-161">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="b873d-162">На данный момент этот компонент доступен только для Azure CDN от Verizon.</span><span class="sxs-lookup"><span data-stu-id="b873d-162">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="b873d-163">Мы работаем над поддержка этой функции в Azure CDN с Akamai в ближайшие месяцы hello.</span><span class="sxs-lookup"><span data-stu-id="b873d-163">We are working on supporting this feature with Azure CDN from Akamai in hello coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b873d-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b873d-164">Next steps</span></span>

- <span data-ttu-id="b873d-165">Узнайте, как tooset копирование [пользовательский домен на конечную точку Azure CDN](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="b873d-165">Learn how tooset up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


