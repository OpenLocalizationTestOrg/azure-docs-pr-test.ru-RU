---
title: "пользовательское доменное имя в облачных службах aaaConfigure | Документы Microsoft"
description: "Узнайте, как tooexpose вашей Azure toohello данным или приложению Интернета на пользовательский домен, настроив параметры DNS.  В этих примерах используются hello портал Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: a0f3186b6022fbc4570ef1ce4b921426842bde76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="1b9f4-104">Настройка пользовательского доменного имени для облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="1b9f4-104">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b9f4-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="1b9f4-105">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="1b9f4-106">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="1b9f4-106">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="1b9f4-107">При создании облачной службы Azure назначает его поддомен tooa **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-107">When you create a Cloud Service, Azure assigns it tooa subdomain of **cloudapp.net**.</span></span> <span data-ttu-id="1b9f4-108">Например, если облачная служба имеет имя «contoso», пользователи будут быть может tooaccess приложения на URL-адрес: http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-108">For example, if your Cloud Service is named "contoso", your users will be able tooaccess your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="1b9f4-109">Azure также назначает виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-109">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="1b9f4-110">Однако приложение можно сделать доступным и на своем собственном домене, например **contoso.com**. В этой статье объясняется, как tooreserve или настроить пользовательское доменное имя для веб-ролей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-110">However, you can also expose your application on your own domain name, such as **contoso.com**. This article explains how tooreserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="1b9f4-111">Вы уже знаете, что такое записи CNAME и A?</span><span class="sxs-lookup"><span data-stu-id="1b9f4-111">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="1b9f4-112">[Переход за объяснение hello](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="1b9f4-112">[Jump past hello explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="1b9f4-113">Hello процедуры в этой задаче применяются tooAzure облачных служб.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-113">hello procedures in this task apply tooAzure Cloud Services.</span></span> <span data-ttu-id="1b9f4-114">Для получения сведений о службах приложений см. [эту статью](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="1b9f4-114">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="1b9f4-115">Для получения сведений об учетных записях хранения см. [эту статью](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="1b9f4-115">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

<p/>

> [!TIP]
> <span data-ttu-id="1b9f4-116">Быстрее--начните использовать новый Azure hello [интерактивной Пошаговое руководство](http://support.microsoft.com/kb/2990804)!</span><span class="sxs-lookup"><span data-stu-id="1b9f4-116">Get going faster--use hello NEW Azure [guided walkthrough](http://support.microsoft.com/kb/2990804)!</span></span>  <span data-ttu-id="1b9f4-117">С его помощью вы без труда сможете связать пользовательское доменное имя И защитить обмен данными (SSL) с облачными службами Azure или веб-сайтами Azure.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-117">It makes associating a custom domain name AND securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="1b9f4-118">Что такое записи CNAME и A</span><span class="sxs-lookup"><span data-stu-id="1b9f4-118">Understand CNAME and A records</span></span>
<span data-ttu-id="1b9f4-119">Запись CNAME (псевдоним записи или) и-записи и обеспечения tooassociate доменное имя с конкретным сервером (или службы в этом случае) тем не менее они работают по-разному.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-119">CNAME (or alias records) and A records both allow you tooassociate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="1b9f4-120">Существуют некоторые специальные рекомендации при использовании Azure облачных службах, которые следует учесть, прежде чем решить, какие toouse записей.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which toouse.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="1b9f4-121">Запись CNAME, или запись псевдонима</span><span class="sxs-lookup"><span data-stu-id="1b9f4-121">CNAME or Alias record</span></span>
<span data-ttu-id="1b9f4-122">Запись CNAME сопоставляет *конкретных* домена, таких как **contoso.com** или **www.contoso.com**, tooa канонического имени домена.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, tooa canonical domain name.</span></span> <span data-ttu-id="1b9f4-123">В этом случае hello канонического имени домена — hello **.cloudapp [myapp] .net** приложения размещенного доменное имя в Azure.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-123">In this case, hello canonical domain name is hello **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="1b9f4-124">После создания hello CNAME создает псевдоним hello **.cloudapp [myapp] .net**.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-124">Once created, hello CNAME creates an alias for hello **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="1b9f4-125">запись CNAME Hello разрешит toohello IP-адрес вашего **.cloudapp [myapp] .net** службы автоматически, поэтому при изменении IP-адрес hello hello облачной службы, у вас tootake какие-либо действия.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-125">hello CNAME entry will resolve toohello IP address of your **[myapp].cloudapp.net** service automatically, so if hello IP address of hello cloud service changes, you do not have tootake any action.</span></span>

> [!NOTE]
> <span data-ttu-id="1b9f4-126">Некоторые регистраторов возможна только поддомены toomap при использовании записи CNAME, например www.contoso.com и не корневых имен, например contoso.com. Дополнительные сведения о записи CNAME в разделе документации hello вашего регистратора [hello запись CNAME-запись в Википедии](http://en.wikipedia.org/wiki/CNAME_record), или hello [IETF доменных имен - реализацию и спецификация](http://tools.ietf.org/html/rfc1035) документ.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-126">Some domain registrars only allow you toomap subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see hello documentation provided by your registrar, [hello Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or hello [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="1b9f4-127">Запись А</span><span class="sxs-lookup"><span data-stu-id="1b9f4-127">A record</span></span>
<span data-ttu-id="1b9f4-128">*A* запись сопоставляет домен, таких как **contoso.com** или **www.contoso.com**, *или подстановочный домен* например  **\*. contoso.com**, tooan IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-128">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, tooan IP address.</span></span> <span data-ttu-id="1b9f4-129">В случае hello облачной службы Azure hello виртуального IP-адреса службы hello.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-129">In hello case of an Azure Cloud Service, hello virtual IP of hello service.</span></span> <span data-ttu-id="1b9f4-130">Поэтому hello основным преимуществом записи CNAME-запись, можно настроить одну строку, в которой используется подстановочный знак, таких как \* **. contoso.com**, который будет обрабатывать запросы для нескольких поддоменов например  **Mail.contoso.com**, **login.contoso.com**, или **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-130">So hello main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="1b9f4-131">Поскольку записи сопоставлена tooa статический IP-адрес автоматически разрешить изменения toohello IP-адрес облачной службы.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-131">Since an A record is mapped tooa static IP address, it cannot automatically resolve changes toohello IP address of your Cloud Service.</span></span> <span data-ttu-id="1b9f4-132">Hello IP-адрес, используемый облачной службы выделяется hello первом развертывании tooan пустой слот (производственной или промежуточной.) При удалении развертывания hello для слота hello hello IP-адрес, выпускаемых Azure и любой интервал toohello будущих развертываний могут предоставить новый IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-132">hello IP address used by your Cloud Service is allocated hello first time you deploy tooan empty slot (either production or staging.) If you delete hello deployment for hello slot, hello IP address is released by Azure and any future deployments toohello slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="1b9f4-133">К счастью hello IP-адрес освобождаемой данного развертывания (рабочий или промежуточный) сохраняется, если переключаться между промежуточной и производственной среде или выполнение обновления на месте существующего развертывания.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-133">Conveniently, hello IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="1b9f4-134">Дополнительные сведения о выполнении этих действий см. в разделе [как toomanage облачные службы](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="1b9f4-134">For more information on performing these actions, see [How toomanage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="1b9f4-135">Добавление записи CNAME для пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="1b9f4-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="1b9f4-136">toocreate запись CNAME, необходимо добавить новую запись в таблице hello DNS для личного домена с помощью средств hello регистратора.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-136">toocreate a CNAME record, you must add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="1b9f4-137">Каждый регистратор имеет похожие, но немного другой метод указания запись CNAME, но принципы приветствия hello таким же.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="1b9f4-138">Используйте один из этих методов toofind hello **. cloudapp.net** имя домена, назначенное tooyour облачной службы.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-138">Use one of these methods toofind hello **.cloudapp.net** domain name assigned tooyour cloud service.</span></span>
   
   * <span data-ttu-id="1b9f4-139">Toohello входа [портал Azure]выберите облачную службу, просмотрите hello **Essentials** статьи и найдите hello **URL-адрес сайта** входа.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-139">Login toohello [Azure portal], select your cloud service, look at hello **Essentials** section and then find hello **Site URL** entry.</span></span>
     
       ![Отображение URL-адрес сайта hello раздел быстрый обзор][csurl]
     
       <span data-ttu-id="1b9f4-141">**OR**</span><span class="sxs-lookup"><span data-stu-id="1b9f4-141">**OR**</span></span>
   * <span data-ttu-id="1b9f4-142">Установка и настройка [Azure Powershell](/powershell/azure/overview), а затем hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1b9f4-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="1b9f4-143">Сохраните hello доменного имени, используемого в hello URL-адрес, возвращенный любого метода, как он потребуется при создании записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-143">Save hello domain name used in hello URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="1b9f4-144">Войдите на веб-сайте регистратора DNS tooyour и переход на страницу toohello управления DNS.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-144">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="1b9f4-145">Найдите ссылки или области hello узла помечены как **доменное имя**, **DNS**, или **управление сервером имен**.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-145">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="1b9f4-146">Теперь найдите место, где можно выбрать или ввести CNAME.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="1b9f4-147">Имеется запись hello tooselect тип из раскрывающегося списка или перейдите tooan страница «Дополнительные параметры».</span><span class="sxs-lookup"><span data-stu-id="1b9f4-147">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span> <span data-ttu-id="1b9f4-148">Следует искать слова hello **CNAME**, **псевдоним**, или **поддомены**.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-148">You should look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="1b9f4-149">Необходимо также указать домен hello или поддомен псевдоним для hello CNAME, таких как **www** Если требуется псевдоним для toocreate **www.customdomain.com**. Если требуется toocreate псевдоним для hello корневого домена, он имеет отметку hello "**@**" символа в средствах вашего регистратора DNS.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-149">You must also provide hello domain or subdomain alias for hello CNAME, such as **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate an alias for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="1b9f4-150">Затем необходимо предоставить каноническое имя узла, которым в данном случае является домен **cloudapp.net** вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="1b9f4-151">Например, следующая запись CNAME hello перенаправляет весь трафик от **www.contoso.com** слишком**contoso.cloudapp.net**, hello пользовательское доменное имя развернутого приложения:</span><span class="sxs-lookup"><span data-stu-id="1b9f4-151">For example, hello following CNAME record forwards all traffic from **www.contoso.com** too**contoso.cloudapp.net**, hello custom domain name of your deployed application:</span></span>

| <span data-ttu-id="1b9f4-152">Псевдоним/Имя узла/Поддомен</span><span class="sxs-lookup"><span data-stu-id="1b9f4-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="1b9f4-153">Канонический домен</span><span class="sxs-lookup"><span data-stu-id="1b9f4-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="1b9f4-154">www</span><span class="sxs-lookup"><span data-stu-id="1b9f4-154">www</span></span> |<span data-ttu-id="1b9f4-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="1b9f4-155">contoso.cloudapp.net</span></span> |

> [!NOTE]
> <span data-ttu-id="1b9f4-156">Посетитель из **www.contoso.com** не увидите hello true узла (contoso.cloudapp.net), поэтому hello процессом перенаправления является невидимым toothe конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-156">A visitor of **www.contoso.com** will never see hello true host (contoso.cloudapp.net), so hello forwarding process is invisible toothe end user.</span></span>
> 
> <span data-ttu-id="1b9f4-157">Hello приведенном выше примере применяется только tootraffic на hello **www** дочерний домен.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-157">hello example above only applies tootraffic at hello **www** subdomain.</span></span> <span data-ttu-id="1b9f4-158">Поскольку с записями CNAME нельзя использовать подстановочные знаки, необходимо создать один CNAME для каждого домена или поддомена.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="1b9f4-159">Следует ли toodirect трафик из дочерних доменов, например *. contoso.com, адрес cloudapp.net tooyour, можно настроить **перенаправления URL-адреса** или **вперед URL-адрес** запись в параметры DNS или создать запись.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-159">If you want toodirect  traffic from subdomains, such as *.contoso.com, tooyour cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="1b9f4-160">Добавление записи A для пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="1b9f4-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="1b9f4-161">toocreate A-записи, необходимо сначала найти hello виртуальный IP-адрес облачной службы.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-161">toocreate an A record, you must first find hello virtual IP address of your cloud service.</span></span> <span data-ttu-id="1b9f4-162">Добавьте новую запись в таблице hello DNS для личного домена, с помощью инструментов hello регистратора.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-162">Then add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="1b9f4-163">Каждый регистратор имеет похожие, но немного другой метод указания записи, но принципы приветствия hello таким же.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-163">Each registrar has a similar but slightly different method of specifying an A record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="1b9f4-164">Используйте одну из hello следующие методы tooget hello IP-адрес облачной службы.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-164">Use one of hello following methods tooget hello IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="1b9f4-165">Toohello входа [портал Azure]выберите облачную службу, просмотрите hello **Essentials** статьи и найдите hello **открытый IP-адреса** входа.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-165">Login toohello [Azure portal], select your cloud service, look at hello **Essentials** section and then find hello **Public IP addresses** entry.</span></span>
     
       ![быстрый обзор раздела, показывающая hello виртуальных IP-адресов][vip]
     
       <span data-ttu-id="1b9f4-167">**OR**</span><span class="sxs-lookup"><span data-stu-id="1b9f4-167">**OR**</span></span>
   * <span data-ttu-id="1b9f4-168">Установка и настройка [Azure Powershell](/powershell/azure/overview), а затем hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1b9f4-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="1b9f4-169">Сохраните hello IP-адрес, так как он потребуется при создании записи.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-169">Save hello IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="1b9f4-170">Войдите на веб-сайте регистратора DNS tooyour и переход на страницу toohello управления DNS.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-170">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="1b9f4-171">Найдите ссылки или области hello узла помечены как **доменное имя**, **DNS**, или **управление сервером имен**.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-171">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="1b9f4-172">Теперь найдите место, где можно выбрать или ввести запись А.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-172">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="1b9f4-173">Имеется запись hello tooselect тип из раскрывающегося списка или перейдите tooan страница «Дополнительные параметры».</span><span class="sxs-lookup"><span data-stu-id="1b9f4-173">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span>
4. <span data-ttu-id="1b9f4-174">Выберите или введите домен hello или поддомен, который будет использовать эту запись A.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-174">Select or enter hello domain or subdomain that will use this A record.</span></span> <span data-ttu-id="1b9f4-175">Например, выберите **www** Если требуется псевдоним для toocreate **www.customdomain.com**. Toocreate входа подстановочный знак для все поддомены, введите "***".</span><span class="sxs-lookup"><span data-stu-id="1b9f4-175">For example, select **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate a wildcard entry for all subdomains, enter '*****'.</span></span> <span data-ttu-id="1b9f4-176">Так будут охвачены все поддомены, такие как **mail.customdomain.com**, **login.customdomain.com** и **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-176">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="1b9f4-177">Если требуется toocreate A записи для hello корневого домена, его могут быть указаны как hello "**@**" символа в средствах вашего регистратора DNS.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-177">If you want toocreate an A record for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="1b9f4-178">Введите IP-адрес hello облачной службы в hello в предоставленные поля.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-178">Enter hello IP address of your cloud service in hello provided field.</span></span> <span data-ttu-id="1b9f4-179">Это связывает hello записи домена, используемого в записи hello hello IP-адрес развертывания облачной службы.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-179">This associates hello domain entry used in hello A record with hello IP address of your cloud service deployment.</span></span>

<span data-ttu-id="1b9f4-180">Например, следующая запись hello перенаправляет весь трафик от **contoso.com** слишком**137.135.70.239**, IP-адрес развернутое приложение hello:</span><span class="sxs-lookup"><span data-stu-id="1b9f4-180">For example, hello following A record forwards all traffic from **contoso.com** too**137.135.70.239**, hello IP address of your deployed application:</span></span>

| <span data-ttu-id="1b9f4-181">Имя узла/Поддомен</span><span class="sxs-lookup"><span data-stu-id="1b9f4-181">Host name/Subdomain</span></span> | <span data-ttu-id="1b9f4-182">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="1b9f4-182">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="1b9f4-183">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="1b9f4-183">137.135.70.239</span></span> |

<span data-ttu-id="1b9f4-184">В этом примере показано создание записи A для hello корневого домена.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-184">This example demonstrates creating an A record for hello root domain.</span></span> <span data-ttu-id="1b9f4-185">При желании toocreate toocover входа подстановочные все поддомены, необходимо ввести "***" как поддомен hello.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-185">If you wish toocreate a wildcard entry toocover all subdomains, you would enter '*****' as hello subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="1b9f4-186">IP-адреса в Azure по умолчанию являются динамическими.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-186">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="1b9f4-187">Возможно, вы захотите toouse [зарезервированные IP-адреса](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure, IP-адрес не изменяется.</span><span class="sxs-lookup"><span data-stu-id="1b9f4-187">You will probably want toouse a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1b9f4-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b9f4-188">Next steps</span></span>
* [<span data-ttu-id="1b9f4-189">Как tooManage облачных служб</span><span class="sxs-lookup"><span data-stu-id="1b9f4-189">How tooManage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="1b9f4-190">Как tooMap содержимого CDN tooa пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="1b9f4-190">How tooMap CDN Content tooa Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="1b9f4-191">[Общая настройка облачной службы](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1b9f4-191">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="1b9f4-192">Узнайте, каким образом слишком[развертывание облачной службы](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1b9f4-192">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="1b9f4-193">Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1b9f4-193">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[портал Azure]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
