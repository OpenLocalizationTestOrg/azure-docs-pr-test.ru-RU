---
title: "Включение протокола HTTPS для личного домена Azure CDN | Документация Майкрософт"
description: "Узнайте, как включить протокол HTTPS для конечной точки Azure CDN с личным доменом."
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
ms.openlocfilehash: b334ba6bbec1d0a7e23a514174bffae01c7fff05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="c286a-103">Включение протокола HTTPS для личного домена Azure CDN</span><span class="sxs-lookup"><span data-stu-id="c286a-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="c286a-104">Поддержка HTTPS для личных доменов Azure CDN позволяет доставлять защищенное содержимое через SSL, используя собственное имя домена для повышения безопасности данных в процессе передачи.</span><span class="sxs-lookup"><span data-stu-id="c286a-104">HTTPS support for Azure CDN custom domains enables you to deliver secure content via SSL using your own domain name to improve the security of data while in transit.</span></span> <span data-ttu-id="c286a-105">Включение одним щелчком и полноценное управление сертификатами без дополнительных затрат упрощает комплексный рабочий процесс включения поддержки протокола HTTPS для личного домена.</span><span class="sxs-lookup"><span data-stu-id="c286a-105">The end-to-end workflow to enable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="c286a-106">Крайне важно обеспечить неприкосновенность и целостность всех конфиденциальных данных веб-приложения в процессе их передачи.</span><span class="sxs-lookup"><span data-stu-id="c286a-106">It's critical to ensure the privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="c286a-107">С помощью протокола HTTPS обеспечивается шифрование конфиденциальных данных при их передаче через Интернет.</span><span class="sxs-lookup"><span data-stu-id="c286a-107">Using the HTTPS protocol ensures that your sensitive data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="c286a-108">Он обеспечивает доверие, аутентификацию и защиту веб-приложений от атак.</span><span class="sxs-lookup"><span data-stu-id="c286a-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="c286a-109">В настоящее время Azure CDN поддерживает HTTPS в конечной точке CDN.</span><span class="sxs-lookup"><span data-stu-id="c286a-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="c286a-110">Например, при создании конечной точки CDN из Azure CDN (например, https://contoso.azureedge.net) протокол HTTPS включен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c286a-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="c286a-111">Теперь благодаря поддержке HTTPS для личных доменов (например, https://www.contoso.com) вы можете также включить для них безопасную доставку.</span><span class="sxs-lookup"><span data-stu-id="c286a-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="c286a-112">Ниже приведены некоторые ключевые характеристики компонента HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c286a-112">Some of the key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="c286a-113">Никаких дополнительных затрат: вам не придется оплачивать приобретение или продление сертификата или платить за трафик, переданный по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c286a-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="c286a-114">Вы оплачиваете только исходящий трафик из сети CDN.</span><span class="sxs-lookup"><span data-stu-id="c286a-114">You just pay for GB egress from the CDN.</span></span>

- <span data-ttu-id="c286a-115">Простое включение: на [портале Azure](https://portal.azure.com) доступна подготовка одним щелчком.</span><span class="sxs-lookup"><span data-stu-id="c286a-115">Simple enablement: One click provisioning is available from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c286a-116">Для включения этого компонента можно также использовать REST API или другие средства разработки.</span><span class="sxs-lookup"><span data-stu-id="c286a-116">You can also use REST API or other developer tools to enable the feature.</span></span>

- <span data-ttu-id="c286a-117">Полноценное управление сертификатами: закупка всех сертификатов и управление ими осуществляется без вашего участия.</span><span class="sxs-lookup"><span data-stu-id="c286a-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="c286a-118">Сертификаты автоматически подготавливаются и продлеваются до истечения их срока действия.</span><span class="sxs-lookup"><span data-stu-id="c286a-118">Certificates are automatically provisioned and renewed prior to expiration.</span></span> <span data-ttu-id="c286a-119">Это полностью устраняет риски прерывания работы службы в результате истечения срока действия сертификата.</span><span class="sxs-lookup"><span data-stu-id="c286a-119">This completely removes the risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="c286a-120">Перед включением поддержки протокола HTTPS необходимо установить [личный домен Azure CDN](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="c286a-120">Prior to enabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-the-feature"></a><span data-ttu-id="c286a-121">Шаг 1. Включение компонента</span><span class="sxs-lookup"><span data-stu-id="c286a-121">Step 1: Enabling the feature</span></span> 

1. <span data-ttu-id="c286a-122">На [портале Azure](https://portal.azure.com) перейдите к профилю CDN категории "Стандартный" или "Премиум" от Verizon.</span><span class="sxs-lookup"><span data-stu-id="c286a-122">In the [Azure portal](https://portal.azure.com), browse to your Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="c286a-123">В списке конечных точек щелкните ту из них, которая содержит личный домен.</span><span class="sxs-lookup"><span data-stu-id="c286a-123">In the list of endpoints, click the endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="c286a-124">Щелкните личный домен, для которого требуется включить HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c286a-124">Click the custom domain for which you want to enable HTTPS.</span></span>

    ![Колонка "Конечная точка"](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="c286a-126">Щелкните **Включить**, чтоб включить поддержку протокола HTTPS и сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="c286a-126">Click **On** to enable HTTPS and save the change.</span></span>

    ![Диалоговое окно "Настраиваемый HTTPS"](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="c286a-128">Шаг 2. Проверка домена</span><span class="sxs-lookup"><span data-stu-id="c286a-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="c286a-129">Чтобы поддержка HTTPS стала активной для личного домена, необходимо выполнить его проверку.</span><span class="sxs-lookup"><span data-stu-id="c286a-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="c286a-130">Для подтверждения домена у вас есть 6 рабочих дней.</span><span class="sxs-lookup"><span data-stu-id="c286a-130">You have 6 business days to approve the domain.</span></span> <span data-ttu-id="c286a-131">Если подтверждение не поступит в течение этого срока, запрос будет отменен.</span><span class="sxs-lookup"><span data-stu-id="c286a-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="c286a-132">После включения HTTPS для личного домена наш поставщик сертификата HTTPS DigiCert проверит владельца домена, обратившись к тому, кто его зарегистрировал, по электронной почте (по умолчанию) или по телефону в соответствии со сведениями о зарегистрировавшихся пользователях в базе данных WHOIS.</span><span class="sxs-lookup"><span data-stu-id="c286a-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting the registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="c286a-133">DigiCert также отправляет проверочное электронное сообщение на приведенные ниже адреса.</span><span class="sxs-lookup"><span data-stu-id="c286a-133">DigiCert will also send the verification email to the below addresses.</span></span> <span data-ttu-id="c286a-134">Если сведения о регистрируемом пользователе Whois являются частными, убедитесь, что возможно утверждение непосредственно с одного из этих адресов.</span><span class="sxs-lookup"><span data-stu-id="c286a-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="c286a-135">admin@<доменное_имя.com> administrator@<доменное_имя.com></span><span class="sxs-lookup"><span data-stu-id="c286a-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="c286a-136">webmaster@<доменное_имя.com></span><span class="sxs-lookup"><span data-stu-id="c286a-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="c286a-137">hostmaster@<доменное_имя.com></span><span class="sxs-lookup"><span data-stu-id="c286a-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="c286a-138">postmaster@<доменное_имя.com></span><span class="sxs-lookup"><span data-stu-id="c286a-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="c286a-139">При получении сообщения электронной почты, возможны два варианта проверки:</span><span class="sxs-lookup"><span data-stu-id="c286a-139">Upon receiving the email, you have two verification options:</span></span>

1. <span data-ttu-id="c286a-140">Можно утвердить все будущие заказы, оформленные с использованием одной и той же учетной записи для одного корневого домена, например consoto.com.</span><span class="sxs-lookup"><span data-stu-id="c286a-140">You can approve all future orders placed through the same account for the same root domain, e.g. consoto.com.</span></span> <span data-ttu-id="c286a-141">Это рекомендуется, если в будущем для корневого домена планируется добавить другие личные домены.</span><span class="sxs-lookup"><span data-stu-id="c286a-141">This is a recommended approach if you are planning to add additional custom domains in the future for the same root domain.</span></span>
 
2. <span data-ttu-id="c286a-142">Можно просто утвердить конкретное имя узла, которое используется в данном запросе.</span><span class="sxs-lookup"><span data-stu-id="c286a-142">You can just approve the specific host name used in this request.</span></span> <span data-ttu-id="c286a-143">Для последующих запросов потребуются дополнительные утверждения.</span><span class="sxs-lookup"><span data-stu-id="c286a-143">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="c286a-144">Пример сообщения электронной почты:</span><span class="sxs-lookup"><span data-stu-id="c286a-144">Example email:</span></span>
    
    ![Диалоговое окно "Настраиваемый HTTPS"](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="c286a-146">После утверждения DigiCert добавит имя личного домена в сертификат SAN.</span><span class="sxs-lookup"><span data-stu-id="c286a-146">After approval, DigiCert will add your custom domain name to the SAN certificate.</span></span> <span data-ttu-id="c286a-147">Сертификат будет действителен в течение года, и будет автоматически продлен до истечения его срока действия.</span><span class="sxs-lookup"><span data-stu-id="c286a-147">The certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a><span data-ttu-id="c286a-148">Шаг 3. Начало использования компонента после распространения данных</span><span class="sxs-lookup"><span data-stu-id="c286a-148">Step 3: Wait for the propagation then start using your feature</span></span>

<span data-ttu-id="c286a-149">Активация компонента HTTPS для личного домена после проверки доменного имени займет не больше 6–8 часов.</span><span class="sxs-lookup"><span data-stu-id="c286a-149">After the domain name is validated it will take up to 6-8 hours for the custom domain HTTPS feature to be active.</span></span> <span data-ttu-id="c286a-150">По завершении процесса для состояния "Настраиваемый HTTPS" на портале Azure будет установлено значение "Включено".</span><span class="sxs-lookup"><span data-stu-id="c286a-150">After the process is complete, the "custom HTTPS" status in the Azure portal will be set to "Enabled".</span></span> <span data-ttu-id="c286a-151">Теперь компонент HTTPS можно использовать для личного домена.</span><span class="sxs-lookup"><span data-stu-id="c286a-151">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="c286a-152">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="c286a-152">Frequently asked questions</span></span>

1. <span data-ttu-id="c286a-153">*Кто является поставщиком сертификата и какой тип сертификата используется?*</span><span class="sxs-lookup"><span data-stu-id="c286a-153">*Who is the certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="c286a-154">Мы используем сертификат альтернативного имени субъекта (SAN), предоставленный DigiCert.</span><span class="sxs-lookup"><span data-stu-id="c286a-154">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="c286a-155">С помощью одного сертификата SAN можно защитить несколько полных доменных имен.</span><span class="sxs-lookup"><span data-stu-id="c286a-155">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="c286a-156">*Могу ли я использовать выделенный сертификат?*</span><span class="sxs-lookup"><span data-stu-id="c286a-156">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="c286a-157">Сейчас это невозможно, но мы планируем добавить такую возможность.</span><span class="sxs-lookup"><span data-stu-id="c286a-157">Not currently, but it's on the roadmap.</span></span>

3. <span data-ttu-id="c286a-158">*Что делать, если я не получу сообщение электронной почты для проверки домена от DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="c286a-158">*What if I don't receive the domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="c286a-159">Если вы не получите электронное сообщение в течение 24 часов, обратитесь в корпорацию Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c286a-159">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="c286a-160">*Не окажется ли сертификат SAN менее безопасным, чем выделенный сертификат?*</span><span class="sxs-lookup"><span data-stu-id="c286a-160">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="c286a-161">Для сертификата SAN используются те же стандарты безопасности и шифрования, что и для выделенного сертификата.</span><span class="sxs-lookup"><span data-stu-id="c286a-161">A SAN cert follows the same encryption and security standards as a dedicated cert.</span></span> <span data-ttu-id="c286a-162">Чтобы дополнительно обезопасить сервер, для всех выданных сертификатов SSL используется алгоритм SHA-256.</span><span class="sxs-lookup"><span data-stu-id="c286a-162">All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="c286a-163">*Можно ли использовать личный домен HTTPS с Azure CDN от Akamai?*</span><span class="sxs-lookup"><span data-stu-id="c286a-163">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="c286a-164">На данный момент этот компонент доступен только для Azure CDN от Verizon.</span><span class="sxs-lookup"><span data-stu-id="c286a-164">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="c286a-165">Мы работаем над тем, чтобы в ближайшие месяцы обеспечить его поддержку в Azure CDN от Akamai.</span><span class="sxs-lookup"><span data-stu-id="c286a-165">We are working on supporting this feature with Azure CDN from Akamai in the coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c286a-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c286a-166">Next steps</span></span>

- <span data-ttu-id="c286a-167">Узнайте, как настроить [личный домен в конечной точке Azure CDN](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="c286a-167">Learn how to set up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


