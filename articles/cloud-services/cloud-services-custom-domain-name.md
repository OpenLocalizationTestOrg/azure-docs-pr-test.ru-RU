---
title: "пользовательское доменное имя в облачных службах aaaConfigure | Документы Microsoft"
description: "Узнайте, как tooexpose Azure приложения или данные для пользовательского домена путем настройки параметров DNS."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 71e553a73b40a8d0512b4d40173500561841772c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="e1f2c-103">Настройка пользовательского доменного имени для облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="e1f2c-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1f2c-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="e1f2c-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="e1f2c-105">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="e1f2c-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="e1f2c-106">При создании облачной службы Azure назначает его tooa дочерним доменом cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-106">When you create a Cloud Service, Azure assigns it tooa subdomain of cloudapp.net.</span></span> <span data-ttu-id="e1f2c-107">Например, если облачная служба имеет имя «contoso», пользователи будут быть может tooaccess приложения на URL-адрес: http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-107">For example, if your Cloud Service is named "contoso", your users will be able tooaccess your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="e1f2c-108">Azure также назначает виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="e1f2c-109">Однако вы можете сделать свое приложение доступным на своем собственном имени домена, например contoso.com. В этой статье объясняется, как tooreserve или настроить пользовательское доменное имя для веб-ролей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how tooreserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="e1f2c-110">Вы уже знаете, что такое записи CNAME и A?</span><span class="sxs-lookup"><span data-stu-id="e1f2c-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="e1f2c-111">[Переход за объяснение hello](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="e1f2c-111">[Jump past hello explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="e1f2c-112">Приступите к работе быстрее!</span><span class="sxs-lookup"><span data-stu-id="e1f2c-112">Get going faster!</span></span> <span data-ttu-id="e1f2c-113">Используйте hello Azure [интерактивной Пошаговое руководство](http://support.microsoft.com/kb/2990804).</span><span class="sxs-lookup"><span data-stu-id="e1f2c-113">Use hello Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="e1f2c-114">С его помощью вы без труда сможете связать имя личного домена и защитить обмен данными (SSL) с облачными службами Azure или веб-сайтами Azure.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="e1f2c-115">Hello процедуры в этой задаче применяются tooAzure облачных служб.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-115">hello procedures in this task apply tooAzure Cloud Services.</span></span> <span data-ttu-id="e1f2c-116">Для получения сведений о службах приложений см. [эту статью](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="e1f2c-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="e1f2c-117">Для получения сведений об учетных записях хранения см. [эту статью](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="e1f2c-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="e1f2c-118">Что такое записи CNAME и A</span><span class="sxs-lookup"><span data-stu-id="e1f2c-118">Understand CNAME and A records</span></span>
<span data-ttu-id="e1f2c-119">Запись CNAME (псевдоним записи или) и-записи и обеспечения tooassociate доменное имя с конкретным сервером (или службы в этом случае) тем не менее они работают по-разному.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-119">CNAME (or alias records) and A records both allow you tooassociate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="e1f2c-120">Существуют некоторые специальные рекомендации при использовании Azure облачных службах, которые следует учесть, прежде чем решить, какие toouse записей.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which toouse.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="e1f2c-121">Запись CNAME, или запись псевдонима</span><span class="sxs-lookup"><span data-stu-id="e1f2c-121">CNAME or Alias record</span></span>
<span data-ttu-id="e1f2c-122">Запись CNAME сопоставляет *конкретных* домена, таких как **contoso.com** или **www.contoso.com**, tooa канонического имени домена.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, tooa canonical domain name.</span></span> <span data-ttu-id="e1f2c-123">В этом случае hello канонического имени домена — hello **.cloudapp [myapp] .net** приложения размещенного доменное имя в Azure.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-123">In this case, hello canonical domain name is hello **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="e1f2c-124">После создания hello CNAME создает псевдоним hello **.cloudapp [myapp] .net**.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-124">Once created, hello CNAME creates an alias for hello **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="e1f2c-125">запись CNAME Hello разрешит toohello IP-адрес вашего **.cloudapp [myapp] .net** службы автоматически, поэтому при изменении IP-адрес hello hello облачной службы, у вас tootake какие-либо действия.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-125">hello CNAME entry will resolve toohello IP address of your **[myapp].cloudapp.net** service automatically, so if hello IP address of hello cloud service changes, you do not have tootake any action.</span></span>

> [!NOTE]
> <span data-ttu-id="e1f2c-126">Некоторые регистраторов возможна только поддомены toomap при использовании записи CNAME, например www.contoso.com и не корневых имен, например contoso.com. Дополнительные сведения о записи CNAME в разделе документации hello вашего регистратора [hello запись CNAME-запись в Википедии](http://en.wikipedia.org/wiki/CNAME_record), или hello [IETF доменных имен - реализацию и спецификация](http://tools.ietf.org/html/rfc1035) документ.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-126">Some domain registrars only allow you toomap subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see hello documentation provided by your registrar, [hello Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or hello [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="e1f2c-127">Запись А</span><span class="sxs-lookup"><span data-stu-id="e1f2c-127">A record</span></span>
<span data-ttu-id="e1f2c-128">Запись сопоставляет домен, таких как **contoso.com** или **www.contoso.com**, *или подстановочный домен* например  **\*. contoso.com**, tooan IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, tooan IP address.</span></span> <span data-ttu-id="e1f2c-129">В случае hello облачной службы Azure hello виртуального IP-адреса службы hello.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-129">In hello case of an Azure Cloud Service, hello virtual IP of hello service.</span></span> <span data-ttu-id="e1f2c-130">Поэтому hello основным преимуществом записи CNAME-запись, можно настроить одну строку, в которой используется подстановочный знак, таких как \* **. contoso.com**, который будет обрабатывать запросы для нескольких поддоменов например  **Mail.contoso.com**, **login.contoso.com**, или **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-130">So hello main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="e1f2c-131">Поскольку записи сопоставлена tooa статический IP-адрес автоматически разрешить изменения toohello IP-адрес облачной службы.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-131">Since an A record is mapped tooa static IP address, it cannot automatically resolve changes toohello IP address of your Cloud Service.</span></span> <span data-ttu-id="e1f2c-132">Hello IP-адрес, используемый облачной службы выделяется hello первом развертывании tooan пустой слот (производственной или промежуточной.) При удалении развертывания hello для слота hello hello IP-адрес, выпускаемых Azure и любой интервал toohello будущих развертываний могут предоставить новый IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-132">hello IP address used by your Cloud Service is allocated hello first time you deploy tooan empty slot (either production or staging.) If you delete hello deployment for hello slot, hello IP address is released by Azure and any future deployments toohello slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="e1f2c-133">К счастью hello IP-адрес освобождаемой данного развертывания (рабочий или промежуточный) сохраняется, если переключаться между промежуточной и производственной среде или выполнение обновления на месте существующего развертывания.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-133">Conveniently, hello IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="e1f2c-134">Дополнительные сведения о выполнении этих действий см. в разделе [как toomanage облачные службы](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="e1f2c-134">For more information on performing these actions, see [How toomanage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="e1f2c-135">Добавление записи CNAME для пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="e1f2c-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="e1f2c-136">toocreate запись CNAME, необходимо добавить новую запись в таблице hello DNS для личного домена с помощью средств hello регистратора.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-136">toocreate a CNAME record, you must add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="e1f2c-137">Каждый регистратор имеет похожие, но немного другой метод указания запись CNAME, но принципы приветствия hello таким же.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="e1f2c-138">Используйте один из этих методов toofind hello **. cloudapp.net** имя домена, назначенное tooyour облачной службы.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-138">Use one of these methods toofind hello **.cloudapp.net** domain name assigned tooyour cloud service.</span></span>
   
   * <span data-ttu-id="e1f2c-139">Toohello входа [классический портал Azure]выберите облачную службу, выберите **мониторинга**и затем найти hello **URL-адрес сайта** запись в hello **быстрый обзор**  раздел.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-139">Login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Site URL** entry in hello **quick glance** section.</span></span>
     
       ![Отображение URL-адрес сайта hello раздел быстрый обзор][csurl]
     
       <span data-ttu-id="e1f2c-141">**OR**</span><span class="sxs-lookup"><span data-stu-id="e1f2c-141">**OR**</span></span>  
   * <span data-ttu-id="e1f2c-142">Установка и настройка [Azure Powershell](/powershell/azure/overview), а затем hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e1f2c-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="e1f2c-143">Сохраните hello доменного имени, используемого в hello URL-адрес, возвращенный любого метода, как он потребуется при создании записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-143">Save hello domain name used in hello URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="e1f2c-144">Войдите на веб-сайте регистратора DNS tooyour и переход на страницу toohello управления DNS.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-144">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="e1f2c-145">Найдите ссылки или области hello узла помечены как **доменное имя**, **DNS**, или **управление сервером имен**.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-145">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="e1f2c-146">Теперь найдите место, где можно выбрать или ввести CNAME.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="e1f2c-147">Имеется запись hello tooselect тип из раскрывающегося списка или перейдите tooan страница «Дополнительные параметры».</span><span class="sxs-lookup"><span data-stu-id="e1f2c-147">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span> <span data-ttu-id="e1f2c-148">Следует искать слова hello **CNAME**, **псевдоним**, или **поддомены**.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-148">You should look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="e1f2c-149">Необходимо также указать домен hello или поддомен псевдоним для hello CNAME, таких как **www** Если требуется псевдоним для toocreate **www.customdomain.com**. Если требуется toocreate псевдоним для hello корневого домена, он имеет отметку hello "**@**" символа в средствах вашего регистратора DNS.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-149">You must also provide hello domain or subdomain alias for hello CNAME, such as **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate an alias for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="e1f2c-150">Затем необходимо предоставить каноническое имя узла, которым в данном случае является домен **cloudapp.net** вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="e1f2c-151">Например, следующая запись CNAME hello перенаправляет весь трафик от **www.contoso.com** слишком**contoso.cloudapp.net**, hello пользовательское доменное имя развернутого приложения:</span><span class="sxs-lookup"><span data-stu-id="e1f2c-151">For example, hello following CNAME record forwards all traffic from **www.contoso.com** too**contoso.cloudapp.net**, hello custom domain name of your deployed application:</span></span>

| <span data-ttu-id="e1f2c-152">Псевдоним/Имя узла/Поддомен</span><span class="sxs-lookup"><span data-stu-id="e1f2c-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="e1f2c-153">Канонический домен</span><span class="sxs-lookup"><span data-stu-id="e1f2c-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="e1f2c-154">www</span><span class="sxs-lookup"><span data-stu-id="e1f2c-154">www</span></span> |<span data-ttu-id="e1f2c-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="e1f2c-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="e1f2c-156">Посетитель из **www.contoso.com** не увидите hello true узла (contoso.cloudapp.net), поэтому hello процессом перенаправления является невидимым toothe конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-156">A visitor of **www.contoso.com** will never see hello true host (contoso.cloudapp.net), so hello forwarding process is invisible toothe end user.</span></span>

> [!NOTE]
> <span data-ttu-id="e1f2c-157">Hello приведенном выше примере применяется только tootraffic на hello **www** дочерний домен.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-157">hello example above only applies tootraffic at hello **www** subdomain.</span></span> <span data-ttu-id="e1f2c-158">Поскольку с записями CNAME нельзя использовать подстановочные знаки, необходимо создать один CNAME для каждого домена или поддомена.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="e1f2c-159">Если необходимо, toodirect трафик из дочерних доменов, таких как \*. contoso.com, адрес cloudapp.net tooyour, можно настроить **перенаправления URL-адреса** или **вперед URL-адрес** запись в параметры DNS или Создание записи.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-159">If you want toodirect  traffic from subdomains, such as \*.contoso.com, tooyour cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="e1f2c-160">Добавление записи A для пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="e1f2c-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="e1f2c-161">toocreate A-записи, необходимо сначала найти hello виртуальный IP-адрес облачной службы.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-161">toocreate an A record, you must first find hello virtual IP address of your cloud service.</span></span> <span data-ttu-id="e1f2c-162">Добавьте новую запись в таблице hello DNS для личного домена, с помощью инструментов hello регистратора.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-162">Then add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="e1f2c-163">Каждый регистратор имеет похожие, но немного другой метод указания записи, но принципы приветствия hello таким же.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-163">Each registrar has a similar but slightly different method of specifying an A record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="e1f2c-164">Используйте одну из hello следующие методы tooget hello IP-адрес облачной службы.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-164">Use one of hello following methods tooget hello IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="e1f2c-165">toohello входа [классический портал Azure]выберите облачную службу, выберите **мониторинга**и затем найти hello **открытый виртуальный IP-адресов (VIP) адрес** запись в hello **быстрый обзор** раздела.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-165">login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Public Virtual IP (VIP) address** entry in hello **quick glance** section.</span></span>
     
       ![быстрый обзор раздела, показывающая hello виртуальных IP-адресов][vip]
     
       <span data-ttu-id="e1f2c-167">**OR**</span><span class="sxs-lookup"><span data-stu-id="e1f2c-167">**OR**</span></span>  
   * <span data-ttu-id="e1f2c-168">Установка и настройка [Azure Powershell](/powershell/azure/overview), а затем hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e1f2c-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="e1f2c-169">Если имеется несколько конечных точек, связанных с облачной службой, вы получите несколько строк, содержащих hello IP-адрес, но отображать все hello же адрес.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing hello IP address, but all should display hello same address.</span></span>
     
     <span data-ttu-id="e1f2c-170">Сохраните hello IP-адрес, так как он потребуется при создании записи.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-170">Save hello IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="e1f2c-171">Войдите на веб-сайте регистратора DNS tooyour и переход на страницу toohello управления DNS.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-171">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="e1f2c-172">Найдите ссылки или области hello узла помечены как **доменное имя**, **DNS**, или **управление сервером имен**.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-172">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="e1f2c-173">Теперь найдите место, где можно выбрать или ввести запись А.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="e1f2c-174">Имеется запись hello tooselect тип из раскрывающегося списка или перейдите tooan страница «Дополнительные параметры».</span><span class="sxs-lookup"><span data-stu-id="e1f2c-174">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span>
4. <span data-ttu-id="e1f2c-175">Выберите или введите домен hello или поддомен, который будет использовать эту запись A.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-175">Select or enter hello domain or subdomain that will use this A record.</span></span> <span data-ttu-id="e1f2c-176">Например, выберите **www** Если требуется псевдоним для toocreate **www.customdomain.com**. Toocreate входа подстановочный знак для все поддомены, введите "__*__".</span><span class="sxs-lookup"><span data-stu-id="e1f2c-176">For example, select **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="e1f2c-177">Так будут охвачены все поддомены, такие как **mail.customdomain.com**, **login.customdomain.com** и **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="e1f2c-178">Если требуется toocreate A записи для hello корневого домена, его могут быть указаны как hello "**@**" символа в средствах вашего регистратора DNS.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-178">If you want toocreate an A record for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="e1f2c-179">Введите IP-адрес hello облачной службы в hello в предоставленные поля.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-179">Enter hello IP address of your cloud service in hello provided field.</span></span> <span data-ttu-id="e1f2c-180">Это связывает hello записи домена, используемого в записи hello hello IP-адрес развертывания облачной службы.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-180">This associates hello domain entry used in hello A record with hello IP address of your cloud service deployment.</span></span>

<span data-ttu-id="e1f2c-181">Например, следующая запись hello перенаправляет весь трафик от **contoso.com** слишком**137.135.70.239**, IP-адрес развернутое приложение hello:</span><span class="sxs-lookup"><span data-stu-id="e1f2c-181">For example, hello following A record forwards all traffic from **contoso.com** too**137.135.70.239**, hello IP address of your deployed application:</span></span>

| <span data-ttu-id="e1f2c-182">Имя узла/Поддомен</span><span class="sxs-lookup"><span data-stu-id="e1f2c-182">Host name/Subdomain</span></span> | <span data-ttu-id="e1f2c-183">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="e1f2c-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="e1f2c-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="e1f2c-184">137.135.70.239</span></span> |

<span data-ttu-id="e1f2c-185">В этом примере показано создание записи A для hello корневого домена.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-185">This example demonstrates creating an A record for hello root domain.</span></span> <span data-ttu-id="e1f2c-186">При желании toocreate toocover входа подстановочные все поддомены, необходимо ввести "__*__" как поддомен hello.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-186">If you wish toocreate a wildcard entry toocover all subdomains, you would enter '__*__' as hello subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="e1f2c-187">IP-адреса в Azure по умолчанию являются динамическими.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="e1f2c-188">Возможно, вы захотите toouse [зарезервированные IP-адреса](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure, IP-адрес не изменяется.</span><span class="sxs-lookup"><span data-stu-id="e1f2c-188">You will probably want toouse a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e1f2c-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1f2c-189">Next steps</span></span>
* [<span data-ttu-id="e1f2c-190">Как tooManage облачных служб</span><span class="sxs-lookup"><span data-stu-id="e1f2c-190">How tooManage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="e1f2c-191">Как tooMap содержимого CDN tooa пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="e1f2c-191">How tooMap CDN Content tooa Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="e1f2c-192">[Общая настройка облачной службы](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e1f2c-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="e1f2c-193">Узнайте, каким образом слишком[развертывание облачной службы](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e1f2c-193">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="e1f2c-194">Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="e1f2c-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[классический портал Azure]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
