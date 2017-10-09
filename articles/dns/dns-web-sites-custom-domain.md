---
title: "aaaCreate пользовательские записи DNS для веб-приложения | Документы Microsoft"
description: "Порядок toocreate пользовательский домен DNS записей для веб-приложения с помощью Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="d7e94-103">Создание записей DNS для веб-приложения в пользовательском домене</span><span class="sxs-lookup"><span data-stu-id="d7e94-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="d7e94-104">Azure DNS toohost пользовательского домена можно использовать для развертывания веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="d7e94-104">You can use Azure DNS toohost a custom domain for your web apps.</span></span> <span data-ttu-id="d7e94-105">Например, вы создаете веб-приложение Azure и требуется вашей tooaccess пользователи его, либо используя в качестве полного доменного ИМЕНИ contoso.com или www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d7e94-105">For example, you are creating an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="d7e94-106">toodo, у вас есть toocreate две записи:</span><span class="sxs-lookup"><span data-stu-id="d7e94-106">toodo this, you have toocreate two records:</span></span>

* <span data-ttu-id="d7e94-107">Записи указывающего toocontoso.com корневой «A»</span><span class="sxs-lookup"><span data-stu-id="d7e94-107">A root "A" record pointing toocontoso.com</span></span>
* <span data-ttu-id="d7e94-108">Запись «» CNAME hello www имя, которое указывает toohello запись</span><span class="sxs-lookup"><span data-stu-id="d7e94-108">A "CNAME" record for hello www name that points toohello A record</span></span>

<span data-ttu-id="d7e94-109">Имейте в виду, что при создании записи для веб-приложения в Azure, записи, необходимо вручную обновить если приветствия hello базовый IP-адрес для изменения приложения hello web.</span><span class="sxs-lookup"><span data-stu-id="d7e94-109">Keep in mind that if you create an A record for a web app in Azure, hello A record must be manually updated if hello underlying IP address for hello web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d7e94-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="d7e94-110">Before you begin</span></span>

<span data-ttu-id="d7e94-111">Прежде чем начать, необходимо сначала создать зону DNS в Azure DNS и делегировать зону hello в tooAzure вашего регистратора DNS.</span><span class="sxs-lookup"><span data-stu-id="d7e94-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate hello zone in your registrar tooAzure DNS.</span></span>

1. <span data-ttu-id="d7e94-112">toocreate зоны DNS, следуйте указаниям hello [создать зону DNS](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="d7e94-112">toocreate a DNS zone, follow hello steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="d7e94-113">toodelegate вашей tooAzure DNS DNS, выполните действия hello в [делегирование DNS домена](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="d7e94-113">toodelegate your DNS tooAzure DNS, follow hello steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="d7e94-114">После создания зоны и делегирования его tooAzure DNS, затем можно создавать записи для вашего домена.</span><span class="sxs-lookup"><span data-stu-id="d7e94-114">After creating a zone and delegating it tooAzure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="d7e94-115">1. Создание записи A для пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="d7e94-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="d7e94-116">Запись — используется toomap имя tooits IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="d7e94-116">An A record is used toomap a name tooits IP address.</span></span> <span data-ttu-id="d7e94-117">В следующий пример hello мы назначит как tooan записи A IPv4-адрес:</span><span class="sxs-lookup"><span data-stu-id="d7e94-117">In hello following example we will assign @ as an A record tooan IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="d7e94-118">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="d7e94-118">Step 1</span></span>

<span data-ttu-id="d7e94-119">Создать запись и присвоить переменной $rs tooa</span><span class="sxs-lookup"><span data-stu-id="d7e94-119">Create an A record and assign tooa variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="d7e94-120">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="d7e94-120">Step 2</span></span>

<span data-ttu-id="d7e94-121">Добавление набора записей toohello ранее созданные значение hello IPv4 «@» с помощью назначен переменной hello $rs.</span><span class="sxs-lookup"><span data-stu-id="d7e94-121">Add hello IPv4 value toohello previously created record set "@" using hello $rs variable assigned.</span></span> <span data-ttu-id="d7e94-122">Присвоенное значение IPv4 Hello будет hello IP-адрес для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d7e94-122">hello IPv4 value assigned will be hello IP address for your web app.</span></span>

<span data-ttu-id="d7e94-123">toofind hello IP-адрес для веб-приложения, выполните действия hello в [настроить пользовательское доменное имя в службе приложений Azure](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d7e94-123">toofind hello IP address for a web app, follow hello steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="d7e94-124">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="d7e94-124">Step 3</span></span>

<span data-ttu-id="d7e94-125">Фиксация набора записей toohello изменения hello.</span><span class="sxs-lookup"><span data-stu-id="d7e94-125">Commit hello changes toohello record set.</span></span> <span data-ttu-id="d7e94-126">Используйте `Set-AzureRMDnsRecordSet` tooupload hello изменяет tooAzure toohello набора записей DNS:</span><span class="sxs-lookup"><span data-stu-id="d7e94-126">Use `Set-AzureRMDnsRecordSet` tooupload hello changes toohello record set tooAzure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="d7e94-127">2. Создание записи CNAME для личного домена</span><span class="sxs-lookup"><span data-stu-id="d7e94-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="d7e94-128">Если домен уже находится под управлением Azure DNS (см. [делегирование DNS домена](dns-domain-delegation.md), можно использовать следующий пример hello toocreate запись CNAME для contoso.azurewebsites.net hello.</span><span class="sxs-lookup"><span data-stu-id="d7e94-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use hello following hello example toocreate a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="d7e94-129">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="d7e94-129">Step 1</span></span>

<span data-ttu-id="d7e94-130">Откройте PowerShell и создайте новый набор записей типа CNAME и назначьте tooa переменной $rs.</span><span class="sxs-lookup"><span data-stu-id="d7e94-130">Open PowerShell and create a new CNAME record set and assign tooa variable $rs.</span></span> <span data-ttu-id="d7e94-131">В этом примере создается набор записей типа CNAME с «временем toolive» 600 секунд в зоне DNS с именем «contoso.com».</span><span class="sxs-lookup"><span data-stu-id="d7e94-131">This example will create a record set type CNAME with a "time toolive" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="d7e94-132">Следующий пример Hello — ответ hello.</span><span class="sxs-lookup"><span data-stu-id="d7e94-132">hello following example is hello response.</span></span>

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="d7e94-133">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="d7e94-133">Step 2</span></span>

<span data-ttu-id="d7e94-134">После создания набора записей CNAME hello toocreate необходимо значение псевдонима, которое будет указывать toohello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d7e94-134">Once hello CNAME record set is created, you need toocreate an alias value which will point toohello web app.</span></span>

<span data-ttu-id="d7e94-135">С помощью ранее назначены переменной «$rs» hello можно использовать команду PowerShell hello ниже toocreate hello псевдоним для contoso.azurewebsites.net приложения hello web.</span><span class="sxs-lookup"><span data-stu-id="d7e94-135">Using hello previously assigned variable "$rs" you can use hello PowerShell command below toocreate hello alias for hello web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="d7e94-136">Следующий пример Hello — ответ hello.</span><span class="sxs-lookup"><span data-stu-id="d7e94-136">hello following example is hello response.</span></span>

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="d7e94-137">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="d7e94-137">Step 3</span></span>

<span data-ttu-id="d7e94-138">Подтверждение изменений hello, с помощью hello `Set-AzureRMDnsRecordSet` командлета:</span><span class="sxs-lookup"><span data-stu-id="d7e94-138">Commit hello changes using hello `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="d7e94-139">Можно проверить правильность создания записи hello запросив hello «www.contoso.com» с помощью команды nslookup, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="d7e94-139">You can validate hello record was created correctly by querying hello "www.contoso.com" using nslookup, as shown below:</span></span>

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="d7e94-140">Создание записи awverify для веб-приложений</span><span class="sxs-lookup"><span data-stu-id="d7e94-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="d7e94-141">Если вы решите toouse записи для веб-приложения, вы должны проходить через tooensure процесс проверки вы hello собственный пользовательский домен.</span><span class="sxs-lookup"><span data-stu-id="d7e94-141">If you decide toouse an A record for your web app, you must go through a verification process tooensure you own hello custom domain.</span></span> <span data-ttu-id="d7e94-142">Для прохождения этой проверки требуется создать специальную запись CNAME с именем awverify.</span><span class="sxs-lookup"><span data-stu-id="d7e94-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="d7e94-143">Этот раздел применим только для записи tooA.</span><span class="sxs-lookup"><span data-stu-id="d7e94-143">This section applies tooA records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="d7e94-144">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="d7e94-144">Step 1</span></span>

<span data-ttu-id="d7e94-145">Создайте запись «awverify» hello.</span><span class="sxs-lookup"><span data-stu-id="d7e94-145">Create hello "awverify" record.</span></span> <span data-ttu-id="d7e94-146">В следующем примере hello мы создадим hello записи «aweverify» для contoso.com tooverify владения для пользовательского домена hello.</span><span class="sxs-lookup"><span data-stu-id="d7e94-146">In hello example below, we will create hello "aweverify" record for contoso.com tooverify ownership for hello custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="d7e94-147">Следующий пример Hello — ответ hello.</span><span class="sxs-lookup"><span data-stu-id="d7e94-147">hello following example is hello response.</span></span>

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="d7e94-148">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="d7e94-148">Step 2</span></span>

<span data-ttu-id="d7e94-149">После создания набора записей hello «awverify» назначьте псевдоним набора записей CNAME hello.</span><span class="sxs-lookup"><span data-stu-id="d7e94-149">Once hello record set "awverify" is created, assign hello CNAME record set alias.</span></span> <span data-ttu-id="d7e94-150">В следующем примере hello мы назначит tooawverify.contoso.azurewebsites.net псевдоним набора записей CNAMe hello.</span><span class="sxs-lookup"><span data-stu-id="d7e94-150">In hello example below, we will assign hello CNAMe record set alias tooawverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="d7e94-151">Следующий пример Hello — ответ hello.</span><span class="sxs-lookup"><span data-stu-id="d7e94-151">hello following example is hello response.</span></span>

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="d7e94-152">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="d7e94-152">Step 3</span></span>

<span data-ttu-id="d7e94-153">Подтверждение изменений hello, с помощью hello `Set-AzureRMDnsRecordSet cmdlet`, как показано в следующей команде hello.</span><span class="sxs-lookup"><span data-stu-id="d7e94-153">Commit hello changes using hello `Set-AzureRMDnsRecordSet cmdlet`, as shown in hello command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="d7e94-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7e94-154">Next steps</span></span>

<span data-ttu-id="d7e94-155">Следуйте указаниям hello [Настройка имени пользовательского домена для служб приложений](../app-service-web/web-sites-custom-domain-name.md) tooconfigure вашей toouse приложения web пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="d7e94-155">Follow hello steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure your web app toouse a custom domain.</span></span>
