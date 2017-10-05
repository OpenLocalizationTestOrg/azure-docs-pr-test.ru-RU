---
title: "Часто задаваемые вопросы о ролях облачных служб Azure | Документация Майкрософт"
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
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="91d93-104">Часто задаваемые вопросы об облачных службах</span><span class="sxs-lookup"><span data-stu-id="91d93-104">Cloud Services FAQ</span></span>
<span data-ttu-id="91d93-105">В этой статье содержатся ответы на некоторые часто задаваемые вопросы об облачных службах Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="91d93-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="91d93-106">Вы также можете посетить страницу [Часто задаваемые вопросы о поддержке Azure](http://go.microsoft.com/fwlink/?LinkID=185083) , где содержатся общие сведения о расценках и поддержке Azure.</span><span class="sxs-lookup"><span data-stu-id="91d93-106">You can also visit the [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="91d93-107">Сведения о размерах приводятся в статье [Размеры для облачных служб](cloud-services-sizes-specs.md) .</span><span class="sxs-lookup"><span data-stu-id="91d93-107">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="91d93-108">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="91d93-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="91d93-109">Где следует разместить мой сертификат?</span><span class="sxs-lookup"><span data-stu-id="91d93-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="91d93-110">**My**</span><span class="sxs-lookup"><span data-stu-id="91d93-110">**My**</span></span>  
  <span data-ttu-id="91d93-111">Сертификаты приложений с закрытым ключом (\*.pfx, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="91d93-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="91d93-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="91d93-112">**CA**</span></span>  
  <span data-ttu-id="91d93-113">— в это хранилище помещаются все промежуточные сертификаты (политики и вложенные ЦС).</span><span class="sxs-lookup"><span data-stu-id="91d93-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="91d93-114">**ROOT**</span><span class="sxs-lookup"><span data-stu-id="91d93-114">**ROOT**</span></span>  
  <span data-ttu-id="91d93-115">— корневое хранилище ЦС, сюда следует поместить основной сертификат корневого ЦС.</span><span class="sxs-lookup"><span data-stu-id="91d93-115">The root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="91d93-116">Не удается удалить сертификат с истекшим сроком действия</span><span class="sxs-lookup"><span data-stu-id="91d93-116">I can't remove expired certificate</span></span>
<span data-ttu-id="91d93-117">Azure не позволяет удалить сертификат, пока он используется.</span><span class="sxs-lookup"><span data-stu-id="91d93-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="91d93-118">Сначала следует удалить развертывание, в котором используется этот сертификат, или задать для этого развертывания другой или обновленный сертификат.</span><span class="sxs-lookup"><span data-stu-id="91d93-118">You need to either delete the deployment that uses the certificate, or update the deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="91d93-119">Удаление сертификата с истекшим сроком действия</span><span class="sxs-lookup"><span data-stu-id="91d93-119">Delete an expired certificate</span></span>
<span data-ttu-id="91d93-120">Если сертификат не используется, его можно удалить с помощью командлета PowerShell [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) .</span><span class="sxs-lookup"><span data-stu-id="91d93-120">As long as the certificate is not in use, you can use the [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet to remove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="91d93-121">Истек срок действия сертификатов с именем "Службы управления Windows Azure для расширений"</span><span class="sxs-lookup"><span data-stu-id="91d93-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="91d93-122">Эти сертификаты создаются каждый раз, когда к облачной службе добавляется расширение, например расширение удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="91d93-122">These certificates are created whenever an extension is added to the cloud service such as the Remote Desktop extension.</span></span> <span data-ttu-id="91d93-123">Сертификаты используются только для шифрования и расшифровки закрытой конфигурации расширения.</span><span class="sxs-lookup"><span data-stu-id="91d93-123">These certificates are only used for encrypting and decrypting the private configuration of the extension.</span></span> <span data-ttu-id="91d93-124">Не страшно, если срок их действия истечет.</span><span class="sxs-lookup"><span data-stu-id="91d93-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="91d93-125">Дата действия сертификата не проверяется.</span><span class="sxs-lookup"><span data-stu-id="91d93-125">The expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="91d93-126">Удаленные сертификаты снова появляются</span><span class="sxs-lookup"><span data-stu-id="91d93-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="91d93-127">Такое обычно происходит из-за используемых средств, например Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="91d93-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="91d93-128">Всякий раз при подключении через средство, которое использует сертификат, этот сертификат снова передается в Azure.</span><span class="sxs-lookup"><span data-stu-id="91d93-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded to Azure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="91d93-129">Мои сертификаты исчезают</span><span class="sxs-lookup"><span data-stu-id="91d93-129">My certificates keep disappearing</span></span>
<span data-ttu-id="91d93-130">При перезапуске экземпляра виртуальной машины все локальные изменения будут утеряны.</span><span class="sxs-lookup"><span data-stu-id="91d93-130">When the virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="91d93-131">Используйте [задачи запуска](cloud-services-startup-tasks.md) , чтобы устанавливать сертификаты на виртуальную машину при каждом запуске роли.</span><span class="sxs-lookup"><span data-stu-id="91d93-131">Use a [startup task](cloud-services-startup-tasks.md) to install certificates to the virtual machine each time the role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a><span data-ttu-id="91d93-132">Не удается найти мои сертификаты управления на портале</span><span class="sxs-lookup"><span data-stu-id="91d93-132">I cannot find my management certificates in the portal</span></span>
<span data-ttu-id="91d93-133">[Сертификаты управления](../azure-api-management-certs.md) доступны только на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="91d93-133">[Management certificates](../azure-api-management-certs.md) are only available in the Azure Classic Portal.</span></span> <span data-ttu-id="91d93-134">Текущий портал Azure не использует сертификаты управления.</span><span class="sxs-lookup"><span data-stu-id="91d93-134">The current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="91d93-135">Как можно отключить сертификат управления?</span><span class="sxs-lookup"><span data-stu-id="91d93-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="91d93-136">[Сертификаты управления](../azure-api-management-certs.md) нельзя отключить.</span><span class="sxs-lookup"><span data-stu-id="91d93-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="91d93-137">Если вы больше не хотите их использовать, то можете удалить их на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="91d93-137">You delete them through the Azure Classic Portal when you do not want them to be used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="91d93-138">Как можно создать SSL-сертификат для конкретного IP-адреса?</span><span class="sxs-lookup"><span data-stu-id="91d93-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="91d93-139">Следуйте указаниям в [учебнике по созданию сертификата](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="91d93-139">Follow the directions in the [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="91d93-140">Используйте IP-адрес в качестве DNS-имени.</span><span class="sxs-lookup"><span data-stu-id="91d93-140">Use the IP address as the DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="91d93-141">Безопасность</span><span class="sxs-lookup"><span data-stu-id="91d93-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="91d93-142">Отключение SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="91d93-142">Disable SSL 3.0</span></span>
<span data-ttu-id="91d93-143">Для отключения SSL 3.0 и использования безопасности TLS создайте задачу запуска, описанную в этой записи блога: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/.</span><span class="sxs-lookup"><span data-stu-id="91d93-143">To disable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-to-your-website"></a><span data-ttu-id="91d93-144">Добавление **nosniff** на веб-сайт</span><span class="sxs-lookup"><span data-stu-id="91d93-144">Add **nosniff** to your website</span></span>
<span data-ttu-id="91d93-145">Чтобы помешать клиентам сканировать типы MIME, добавьте соответствующий параметр в файл *web.config*.</span><span class="sxs-lookup"><span data-stu-id="91d93-145">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="91d93-146">Его можно также добавить как параметр в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="91d93-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="91d93-147">Используйте следующую команду из статьи [Распространенные задачи запуска](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe).</span><span class="sxs-lookup"><span data-stu-id="91d93-147">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="91d93-148">Настройка IIS для веб-роли</span><span class="sxs-lookup"><span data-stu-id="91d93-148">Customize IIS for a web role</span></span>
<span data-ttu-id="91d93-149">Используйте сценарий запуска IIS из статьи [Распространенные задачи запуска](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe).</span><span class="sxs-lookup"><span data-stu-id="91d93-149">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="91d93-150">Масштабирование</span><span class="sxs-lookup"><span data-stu-id="91d93-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="91d93-151">Не удается выполнить масштабирование на более чем X экземпляров</span><span class="sxs-lookup"><span data-stu-id="91d93-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="91d93-152">В вашей подписке Azure есть ограничение на количество используемых ядер.</span><span class="sxs-lookup"><span data-stu-id="91d93-152">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="91d93-153">При использовании всех доступных ядер масштабирование не сработает.</span><span class="sxs-lookup"><span data-stu-id="91d93-153">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="91d93-154">Например, если установлено ограничение в 100 ядер, это означает, что в облачной службе можно создать 100 экземпляров виртуальной машины размера A1 или 50 экземпляров виртуальной машины размера A2.</span><span class="sxs-lookup"><span data-stu-id="91d93-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="91d93-155">Сеть</span><span class="sxs-lookup"><span data-stu-id="91d93-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="91d93-156">Не удается зарезервировать IP-адрес в облачной службе с несколькими виртуальными IP-адресами</span><span class="sxs-lookup"><span data-stu-id="91d93-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="91d93-157">Сначала убедитесь, что экземпляр виртуальной машины, для который вы пытаетесь зарезервировать IP-адрес, включен.</span><span class="sxs-lookup"><span data-stu-id="91d93-157">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span></span> <span data-ttu-id="91d93-158">Во-вторых, убедитесь, что вы используете зарезервированные IP-адреса и для промежуточного, и для рабочего развертываний.</span><span class="sxs-lookup"><span data-stu-id="91d93-158">Second, make sure that you're using Reserved IPs for bother the staging and production deployments.</span></span> <span data-ttu-id="91d93-159">**Не изменяйте** параметры во время обновления развертывания.</span><span class="sxs-lookup"><span data-stu-id="91d93-159">**Do not** change the settings while the deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="91d93-160">Удаленный рабочий стол</span><span class="sxs-lookup"><span data-stu-id="91d93-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="91d93-161">Как использовать удаленный рабочий стол при наличии NSG?</span><span class="sxs-lookup"><span data-stu-id="91d93-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="91d93-162">Добавьте в NSG правила, разрешающие передачу трафика через порты **3389** и **20000**.</span><span class="sxs-lookup"><span data-stu-id="91d93-162">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="91d93-163">Удаленный рабочий стол использует порт **3389**.</span><span class="sxs-lookup"><span data-stu-id="91d93-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="91d93-164">В экземплярах облачной службы реализована балансировка нагрузки, поэтому вы не можете напрямую управлять подключением к экземпляру.</span><span class="sxs-lookup"><span data-stu-id="91d93-164">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="91d93-165">Агенты *RemoteForwarder* и *RemoteAccess* управляют трафиком RDP и позволяют клиенту отправлять файлы cookie по RDP и указывать отдельный экземпляр для подключения.</span><span class="sxs-lookup"><span data-stu-id="91d93-165">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="91d93-166">Агентам *RemoteForwarder* и *RemoteAccess* требуется, чтобы порт **20000*** был открыт. При использовании группы безопасности сети он может быть заблокирован.</span><span class="sxs-lookup"><span data-stu-id="91d93-166">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
