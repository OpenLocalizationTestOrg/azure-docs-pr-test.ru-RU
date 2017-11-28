---
title: "Создание пользовательских записей DNS для веб-приложения | Документация Майкрософт"
description: "Как создать записи DNS личного домена для веб-приложения с помощью Azure DNS."
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
ms.openlocfilehash: b054a41ecd69ee1c802d8403fe4b25128f016e3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="75767-103">Создание записей DNS для веб-приложения в пользовательском домене</span><span class="sxs-lookup"><span data-stu-id="75767-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="75767-104">Службу Azure DNS можно использовать для размещения пользовательского домена для ваших веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="75767-104">You can use Azure DNS to host a custom domain for your web apps.</span></span> <span data-ttu-id="75767-105">Например, вы создаете веб-приложение Azure и хотите, чтобы пользователи получали к нему доступ, вводя полное доменное имя contoso.com или www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="75767-105">For example, you are creating an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="75767-106">Для этого необходимо создать две записи:</span><span class="sxs-lookup"><span data-stu-id="75767-106">To do this, you have to create two records:</span></span>

* <span data-ttu-id="75767-107">корневую запись A, указывающую на contoso.com;</span><span class="sxs-lookup"><span data-stu-id="75767-107">A root "A" record pointing to contoso.com</span></span>
* <span data-ttu-id="75767-108">запись CNAME для имени www, которая указывает на запись A.</span><span class="sxs-lookup"><span data-stu-id="75767-108">A "CNAME" record for the www name that points to the A record</span></span>

<span data-ttu-id="75767-109">Помните, что если создать запись A для веб-приложения в Azure, ее необходимо обновить вручную, если основной IP-адрес веб-приложения изменится.</span><span class="sxs-lookup"><span data-stu-id="75767-109">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="75767-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="75767-110">Before you begin</span></span>

<span data-ttu-id="75767-111">Прежде чем начать, нужно создать зону DNS в Azure DNS и делегировать зону у вашего регистратора в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="75767-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span></span>

1. <span data-ttu-id="75767-112">Чтобы создать зону DNS, выполните действия, описанные в разделе [Создание зоны DNS](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="75767-112">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="75767-113">Для делегирования DNS в Azure DNS выполните действия, описанные в статье [Делегирование домена в Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="75767-113">To delegate your DNS to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="75767-114">После создания зоны и ее делегирования в Azure DNS можно создать записи для личного домена.</span><span class="sxs-lookup"><span data-stu-id="75767-114">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="75767-115">1. Создание записи A для пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="75767-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="75767-116">Запись A используется для сопоставления имени с IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="75767-116">An A record is used to map a name to its IP address.</span></span> <span data-ttu-id="75767-117">В примере ниже мы назначим @ как запись A IPv4-адресу.</span><span class="sxs-lookup"><span data-stu-id="75767-117">In the following example we will assign @ as an A record to an IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="75767-118">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="75767-118">Step 1</span></span>

<span data-ttu-id="75767-119">Создайте запись A и назначьте ее переменной $rs.</span><span class="sxs-lookup"><span data-stu-id="75767-119">Create an A record and assign to a variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="75767-120">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="75767-120">Step 2</span></span>

<span data-ttu-id="75767-121">Добавьте значение IPv4 в ранее созданный набор записей @ с помощью назначенной переменной $rs.</span><span class="sxs-lookup"><span data-stu-id="75767-121">Add the IPv4 value to the previously created record set "@" using the $rs variable assigned.</span></span> <span data-ttu-id="75767-122">Присвоенное значение IPv4 будет IP-адресом вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="75767-122">The IPv4 value assigned will be the IP address for your web app.</span></span>

<span data-ttu-id="75767-123">Чтобы найти IP-адрес для веб-приложения, выполните действия, описанные в статье [Настройка личного доменного имени для службы приложений Azure](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="75767-123">To find the IP address for a web app, follow the steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="75767-124">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="75767-124">Step 3</span></span>

<span data-ttu-id="75767-125">Зафиксируйте изменения в наборе записей.</span><span class="sxs-lookup"><span data-stu-id="75767-125">Commit the changes to the record set.</span></span> <span data-ttu-id="75767-126">Выполните командлет `Set-AzureRMDnsRecordSet`, чтобы передать изменения набора записей в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="75767-126">Use `Set-AzureRMDnsRecordSet` to upload the changes to the record set to Azure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="75767-127">2) Создание записи CNAME для личного домена</span><span class="sxs-lookup"><span data-stu-id="75767-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="75767-128">Если вашим доменом уже управляет Azure DNS (см. статью [Делегирование домена в Azure DNS](dns-domain-delegation.md)), можно использовать следующий пример, чтобы создать запись CNAME для contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="75767-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following the example to create a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="75767-129">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="75767-129">Step 1</span></span>

<span data-ttu-id="75767-130">Откройте PowerShell, создайте набор записей CNAME и назначьте его переменной $rs.</span><span class="sxs-lookup"><span data-stu-id="75767-130">Open PowerShell and create a new CNAME record set and assign to a variable $rs.</span></span> <span data-ttu-id="75767-131">В этом примере будет создан набор записей CNAME со сроком жизни 600 секунд в зоне DNS contoso.com.</span><span class="sxs-lookup"><span data-stu-id="75767-131">This example will create a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="75767-132">Ниже приведен пример ответа.</span><span class="sxs-lookup"><span data-stu-id="75767-132">The following example is the response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="75767-133">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="75767-133">Step 2</span></span>

<span data-ttu-id="75767-134">После создания набора записей CNAME вам необходимо создать значение псевдонима, которое будет указывать на веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="75767-134">Once the CNAME record set is created, you need to create an alias value which will point to the web app.</span></span>

<span data-ttu-id="75767-135">Используя ранее назначенную переменную $rs, можно выполнить следующую команду PowerShell, чтобы создать псевдоним для доменного имени contoso.azurewebsites.net веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="75767-135">Using the previously assigned variable "$rs" you can use the PowerShell command below to create the alias for the web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="75767-136">Ниже приведен пример ответа.</span><span class="sxs-lookup"><span data-stu-id="75767-136">The following example is the response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="75767-137">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="75767-137">Step 3</span></span>

<span data-ttu-id="75767-138">Зафиксируйте изменения с помощью командлета `Set-AzureRMDnsRecordSet` .</span><span class="sxs-lookup"><span data-stu-id="75767-138">Commit the changes using the `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="75767-139">Вы можете проверить, была ли запись правильно создана, запросив www.contoso.com с помощью nslookup, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="75767-139">You can validate the record was created correctly by querying the "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="75767-140">Создание записи awverify для веб-приложений</span><span class="sxs-lookup"><span data-stu-id="75767-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="75767-141">Если вы решили использовать запись A для веб-приложения, вам необходимо пройти проверку и подтвердить, что именно вы являетесь владельцем данного пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="75767-141">If you decide to use an A record for your web app, you must go through a verification process to ensure you own the custom domain.</span></span> <span data-ttu-id="75767-142">Для прохождения этой проверки требуется создать специальную запись CNAME с именем awverify.</span><span class="sxs-lookup"><span data-stu-id="75767-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="75767-143">Этот раздел относится только к записям A.</span><span class="sxs-lookup"><span data-stu-id="75767-143">This section applies to A records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="75767-144">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="75767-144">Step 1</span></span>

<span data-ttu-id="75767-145">Создайте запись awverify.</span><span class="sxs-lookup"><span data-stu-id="75767-145">Create the "awverify" record.</span></span> <span data-ttu-id="75767-146">В следующем примере мы создадим запись awverify для contoso.com, чтобы проверить владельца для личного домена.</span><span class="sxs-lookup"><span data-stu-id="75767-146">In the example below, we will create the "aweverify" record for contoso.com to verify ownership for the custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="75767-147">Ниже приведен пример ответа.</span><span class="sxs-lookup"><span data-stu-id="75767-147">The following example is the response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="75767-148">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="75767-148">Step 2</span></span>

<span data-ttu-id="75767-149">После создания набора записей awverify назначьте псевдоним набора записей CNAME.</span><span class="sxs-lookup"><span data-stu-id="75767-149">Once the record set "awverify" is created, assign the CNAME record set alias.</span></span> <span data-ttu-id="75767-150">В приведенном ниже примере в качестве псевдонима набора записей CNAME мы назначим awverify.contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="75767-150">In the example below, we will assign the CNAMe record set alias to awverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="75767-151">Ниже приведен пример ответа.</span><span class="sxs-lookup"><span data-stu-id="75767-151">The following example is the response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="75767-152">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="75767-152">Step 3</span></span>

<span data-ttu-id="75767-153">Зафиксируйте изменения с помощью командлета `Set-AzureRMDnsRecordSet cmdlet`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="75767-153">Commit the changes using the `Set-AzureRMDnsRecordSet cmdlet`, as shown in the command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="75767-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="75767-154">Next steps</span></span>

<span data-ttu-id="75767-155">Следуйте указаниям в разделе [Настройка личного доменного имени для службы приложений Azure](../app-service-web/web-sites-custom-domain-name.md) , чтобы настроить веб-приложение для использования личного домена.</span><span class="sxs-lookup"><span data-stu-id="75767-155">Follow the steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) to configure your web app to use a custom domain.</span></span>
