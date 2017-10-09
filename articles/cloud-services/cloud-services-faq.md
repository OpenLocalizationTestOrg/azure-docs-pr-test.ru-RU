---
title: "aaaAzure облачные службы ролей часто задаваемые вопросы | Документы Microsoft"
description: "Часто задаваемые вопросы об облачных службах Azure. Ответы на некоторые распространенные вопросы о сертификатах, веб-ролях и рабочих ролях."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="9cef3-104">Часто задаваемые вопросы об облачных службах</span><span class="sxs-lookup"><span data-stu-id="9cef3-104">Cloud Services FAQ</span></span>
<span data-ttu-id="9cef3-105">В этой статье содержатся ответы на некоторые часто задаваемые вопросы об облачных службах Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9cef3-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="9cef3-106">Также можно посетить hello [вопросы и ответы поддержки Azure](http://go.microsoft.com/fwlink/?LinkID=185083) Общие сведения Azure цены и поддержки.</span><span class="sxs-lookup"><span data-stu-id="9cef3-106">You can also visit hello [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="9cef3-107">Кроме того, можно обратиться к hello [страницы размер виртуальной Машины облачных служб](cloud-services-sizes-specs.md) для сведений о размере.</span><span class="sxs-lookup"><span data-stu-id="9cef3-107">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="9cef3-108">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="9cef3-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="9cef3-109">Где следует разместить мой сертификат?</span><span class="sxs-lookup"><span data-stu-id="9cef3-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="9cef3-110">**My**</span><span class="sxs-lookup"><span data-stu-id="9cef3-110">**My**</span></span>  
  <span data-ttu-id="9cef3-111">Сертификаты приложений с закрытым ключом (\*.pfx, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="9cef3-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="9cef3-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="9cef3-112">**CA**</span></span>  
  <span data-ttu-id="9cef3-113">— в это хранилище помещаются все промежуточные сертификаты (политики и вложенные ЦС).</span><span class="sxs-lookup"><span data-stu-id="9cef3-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="9cef3-114">**ROOT**</span><span class="sxs-lookup"><span data-stu-id="9cef3-114">**ROOT**</span></span>  
  <span data-ttu-id="9cef3-115">Hello корневого центра сертификации магазина, поэтому следует здесь срок действия вашего сертификата корневого ЦС.</span><span class="sxs-lookup"><span data-stu-id="9cef3-115">hello root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="9cef3-116">Не удается удалить сертификат с истекшим сроком действия</span><span class="sxs-lookup"><span data-stu-id="9cef3-116">I can't remove expired certificate</span></span>
<span data-ttu-id="9cef3-117">Azure не позволяет удалить сертификат, пока он используется.</span><span class="sxs-lookup"><span data-stu-id="9cef3-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="9cef3-118">Необходимо tooeither delete hello, использующего сертификат hello, или обновление hello развертывания с помощью различных или обновленного сертификата.</span><span class="sxs-lookup"><span data-stu-id="9cef3-118">You need tooeither delete hello deployment that uses hello certificate, or update hello deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="9cef3-119">Удаление сертификата с истекшим сроком действия</span><span class="sxs-lookup"><span data-stu-id="9cef3-119">Delete an expired certificate</span></span>
<span data-ttu-id="9cef3-120">При условии, что сертификат hello не используется, можно использовать hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove командлет PowerShell сертификат.</span><span class="sxs-lookup"><span data-stu-id="9cef3-120">As long as hello certificate is not in use, you can use hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="9cef3-121">Истек срок действия сертификатов с именем "Службы управления Windows Azure для расширений"</span><span class="sxs-lookup"><span data-stu-id="9cef3-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="9cef3-122">Эти сертификаты создаются каждый раз, когда расширение добавляется toohello облачной службы, например hello расширения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="9cef3-122">These certificates are created whenever an extension is added toohello cloud service such as hello Remote Desktop extension.</span></span> <span data-ttu-id="9cef3-123">Эти сертификаты используются только для шифрования и расшифровки hello закрытой конфигурации расширения hello.</span><span class="sxs-lookup"><span data-stu-id="9cef3-123">These certificates are only used for encrypting and decrypting hello private configuration of hello extension.</span></span> <span data-ttu-id="9cef3-124">Не страшно, если срок их действия истечет.</span><span class="sxs-lookup"><span data-stu-id="9cef3-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="9cef3-125">Дата окончания срока действия Hello не проверяется.</span><span class="sxs-lookup"><span data-stu-id="9cef3-125">hello expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="9cef3-126">Удаленные сертификаты снова появляются</span><span class="sxs-lookup"><span data-stu-id="9cef3-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="9cef3-127">Такое обычно происходит из-за используемых средств, например Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9cef3-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="9cef3-128">Всякий раз при подключении с помощью инструмента, использует сертификат, он будет повторно отправленного tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9cef3-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded tooAzure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="9cef3-129">Мои сертификаты исчезают</span><span class="sxs-lookup"><span data-stu-id="9cef3-129">My certificates keep disappearing</span></span>
<span data-ttu-id="9cef3-130">При перезапуске экземпляра виртуальной машины hello, все локальные изменения будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="9cef3-130">When hello virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="9cef3-131">Используйте [задачи запуска](cloud-services-startup-tasks.md) tooinstall сертификаты toohello виртуальная машина запустится, каждая роль hello времени.</span><span class="sxs-lookup"><span data-stu-id="9cef3-131">Use a [startup task](cloud-services-startup-tasks.md) tooinstall certificates toohello virtual machine each time hello role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a><span data-ttu-id="9cef3-132">Не удается найти сертификаты управления портала hello</span><span class="sxs-lookup"><span data-stu-id="9cef3-132">I cannot find my management certificates in hello portal</span></span>
<span data-ttu-id="9cef3-133">[Сертификаты управления](../azure-api-management-certs.md) доступны только в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9cef3-133">[Management certificates](../azure-api-management-certs.md) are only available in hello Azure Classic Portal.</span></span> <span data-ttu-id="9cef3-134">Hello текущей версией портала Azure не использует сертификаты управления.</span><span class="sxs-lookup"><span data-stu-id="9cef3-134">hello current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="9cef3-135">Как можно отключить сертификат управления?</span><span class="sxs-lookup"><span data-stu-id="9cef3-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="9cef3-136">[Сертификаты управления](../azure-api-management-certs.md) нельзя отключить.</span><span class="sxs-lookup"><span data-stu-id="9cef3-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="9cef3-137">Будут удалены через hello классический портал Azure не их следует использовать toobe.</span><span class="sxs-lookup"><span data-stu-id="9cef3-137">You delete them through hello Azure Classic Portal when you do not want them toobe used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="9cef3-138">Как можно создать SSL-сертификат для конкретного IP-адреса?</span><span class="sxs-lookup"><span data-stu-id="9cef3-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="9cef3-139">Следуйте приведенным инструкциям hello hello [создать сертификат Учебник](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="9cef3-139">Follow hello directions in hello [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="9cef3-140">Используйте IP-адрес hello как hello DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="9cef3-140">Use hello IP address as hello DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="9cef3-141">Безопасность</span><span class="sxs-lookup"><span data-stu-id="9cef3-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="9cef3-142">Отключение SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="9cef3-142">Disable SSL 3.0</span></span>
<span data-ttu-id="9cef3-143">toodisable SSL 3.0 и использовать средства безопасности TLS, создать задачу запуска, который описан в этой записи блога: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="9cef3-143">toodisable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-tooyour-website"></a><span data-ttu-id="9cef3-144">Добавить **nosniff** tooyour веб-сайта</span><span class="sxs-lookup"><span data-stu-id="9cef3-144">Add **nosniff** tooyour website</span></span>
<span data-ttu-id="9cef3-145">Клиенты tooprevent из сканирование hello типов MIME, добавьте параметр в вашей *web.config* файла.</span><span class="sxs-lookup"><span data-stu-id="9cef3-145">tooprevent clients from sniffing hello MIME types, add a setting in your *web.config* file.</span></span>

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

<span data-ttu-id="9cef3-146">Его можно также добавить как параметр в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="9cef3-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="9cef3-147">Используйте следующие hello команды с hello [общие задачи запуска](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) статьи.</span><span class="sxs-lookup"><span data-stu-id="9cef3-147">Use hello following command with hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="9cef3-148">Настройка IIS для веб-роли</span><span class="sxs-lookup"><span data-stu-id="9cef3-148">Customize IIS for a web role</span></span>
<span data-ttu-id="9cef3-149">Используйте сценарий запуска IIS hello из hello [общие задачи запуска](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) статьи.</span><span class="sxs-lookup"><span data-stu-id="9cef3-149">Use hello IIS startup script from hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="9cef3-150">Масштабирование</span><span class="sxs-lookup"><span data-stu-id="9cef3-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="9cef3-151">Не удается выполнить масштабирование на более чем X экземпляров</span><span class="sxs-lookup"><span data-stu-id="9cef3-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="9cef3-152">Подписки Azure имеет ограничение на количество ядер, которые можно использовать в hello.</span><span class="sxs-lookup"><span data-stu-id="9cef3-152">Your Azure Subscription has a limit on hello number of cores you can use.</span></span> <span data-ttu-id="9cef3-153">Масштабирование не будет работать при использовании всех доступных ядер hello.</span><span class="sxs-lookup"><span data-stu-id="9cef3-153">Scaling will not work if you have used all hello cores available.</span></span> <span data-ttu-id="9cef3-154">Например, если установлено ограничение в 100 ядер, это означает, что в облачной службе можно создать 100 экземпляров виртуальной машины размера A1 или 50 экземпляров виртуальной машины размера A2.</span><span class="sxs-lookup"><span data-stu-id="9cef3-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="9cef3-155">Сеть</span><span class="sxs-lookup"><span data-stu-id="9cef3-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="9cef3-156">Не удается зарезервировать IP-адрес в облачной службе с несколькими виртуальными IP-адресами</span><span class="sxs-lookup"><span data-stu-id="9cef3-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="9cef3-157">Во-первых убедитесь, что этот экземпляр виртуальной машины hello, который вы пытаетесь tooreserve hello IP-адрес для включен.</span><span class="sxs-lookup"><span data-stu-id="9cef3-157">First, make sure that hello virtual machine instance that you're trying tooreserve hello IP for is turned on.</span></span> <span data-ttu-id="9cef3-158">Во-вторых убедитесь, что вы используете зарезервированных IP-адресов для беспокойства hello промежуточного и рабочего развертываний.</span><span class="sxs-lookup"><span data-stu-id="9cef3-158">Second, make sure that you're using Reserved IPs for bother hello staging and production deployments.</span></span> <span data-ttu-id="9cef3-159">**Нет** изменить параметры hello, пока обновление развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="9cef3-159">**Do not** change hello settings while hello deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="9cef3-160">Удаленный рабочий стол</span><span class="sxs-lookup"><span data-stu-id="9cef3-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="9cef3-161">Как использовать удаленный рабочий стол при наличии NSG?</span><span class="sxs-lookup"><span data-stu-id="9cef3-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="9cef3-162">Добавление правила toohello NSG, разрешить трафик через порты **3389** и **20000**.</span><span class="sxs-lookup"><span data-stu-id="9cef3-162">Add rules toohello NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="9cef3-163">Удаленный рабочий стол использует порт **3389**.</span><span class="sxs-lookup"><span data-stu-id="9cef3-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="9cef3-164">Экземпляров облачной службы, распределяются, поэтому не может напрямую управлять какой экземпляр tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="9cef3-164">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="9cef3-165">Hello *RemoteForwarder* и *RemoteAccess* агенты управления трафиком протокола удаленного рабочего СТОЛА и разрешить toosend клиента hello куки-файл протокола удаленного рабочего СТОЛА и tooconnect отдельного экземпляра, чтобы указать.</span><span class="sxs-lookup"><span data-stu-id="9cef3-165">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="9cef3-166">Hello *RemoteForwarder* и *RemoteAccess* агенты имеют этот порт **20000*** открыть, который может блокироваться, если у вас есть NSG.</span><span class="sxs-lookup"><span data-stu-id="9cef3-166">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
