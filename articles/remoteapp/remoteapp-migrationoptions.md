---
title: "Варианты миграции из Azure RemoteApp | Документация Майкрософт"
description: "Узнайте о вариантах миграции из Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9ab63124e2521ee1922d15c1e388c54d50eb8301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="255b2-103">Варианты переноса из Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="255b2-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="255b2-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="255b2-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="255b2-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="255b2-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="255b2-106">Если вы перестали использовать Azure RemoteApp из-за [уведомления о прекращении использования](https://go.microsoft.com/fwlink/?linkid=821148) или завершения работы с ознакомительной версией, необходимо перейти от Azure RemoteApp к другой службе приложений.</span><span class="sxs-lookup"><span data-stu-id="255b2-106">If you have stopped using Azure RemoteApp because of the [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need to migrate off of Azure RemoteApp to another app service.</span></span> <span data-ttu-id="255b2-107">Есть два подхода к миграции: с самостоятельным управлением развертыванием (это предложение называется инфраструктура как услуга [IaaS]) и полностью управляемым развертыванием (это предложение называется платформа как услуга или программное обеспечение как услуга [PaaS или SaaS]).</span><span class="sxs-lookup"><span data-stu-id="255b2-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="255b2-108">Предложение IaaS с самостоятельным обслуживанием — это управляемое, эксплуатируемое и принадлежащее вам решение, развернутое непосредственно на виртуальных машинах (ВМ) или физических системах.</span><span class="sxs-lookup"><span data-stu-id="255b2-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="255b2-109">Альтернативное предложение PaaS или SaaS с полным управлением — это в некоторой степени аналог Azure RemoteApp. Партнер предоставляет уровень службы на основе удаленного решения, которое обрабатывает рабочие данные и обеспечивает обслуживание, в то время как клиент (вы) управляет образами и приложениями.</span><span class="sxs-lookup"><span data-stu-id="255b2-109">At the other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as the customer, do some image and app management.</span></span>

<span data-ttu-id="255b2-110">[Просмотрите вебинары об Azure RemoteApp, посвященные параметрам миграции](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), или ознакомьтесь с дополнительными сведениями, включая примеры разных вариантов размещения.</span><span class="sxs-lookup"><span data-stu-id="255b2-110">[View the Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of the different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="255b2-111">Самостоятельно управляемые решения (IaaS)</span><span class="sxs-lookup"><span data-stu-id="255b2-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="255b2-112">**RDS в IaaS**</span><span class="sxs-lookup"><span data-stu-id="255b2-112">**RDS on IaaS**</span></span>
<span data-ttu-id="255b2-113">Вы можете выполнять собственные развертывания на основе сеансов служб удаленных рабочих столов (в Windows Server) с помощью RemoteApp или классических приложений в локальной или размещенной среде (включая виртуальные машины Azure).</span><span class="sxs-lookup"><span data-stu-id="255b2-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="255b2-114">RDS в развертываниях IaaS лучше всего подходит для более опытных клиентов, которые уже знакомы с технической стороной этого процесса.</span><span class="sxs-lookup"><span data-stu-id="255b2-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="255b2-115">Использование этого варианта развертывания предусматривает корпоративное лицензирование в рамках программы Software Assurance (SA) для получения лицензий на клиентский доступ с помощью RDS.</span><span class="sxs-lookup"><span data-stu-id="255b2-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses to use this deployment option.</span></span>

<span data-ttu-id="255b2-116">Развертывать RDS на виртуальных машинах Azure проще, чем использовать шаблоны развертывания и исправления (см. [обзор](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/), а затем переходите к [скачиванию](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="255b2-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="255b2-117">Такие же возможности эластичного масштабирования доступны при использовании ресурсов классической модели развертывания Azure (не ресурсов модели ресурсов Azure) в Azure RemoteApp с помощью [скрипта автомасштабирования](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76). Но этот вариант предусматривает дополнительные шаги по настройке.</span><span class="sxs-lookup"><span data-stu-id="255b2-117">You can get the same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using the [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="255b2-118">Развертывание RDS на виртуальных машинах Azure сопровождается [поддержкой Azure](https://azure.microsoft.com/support/plans/), предоставляемой теми же специалистами, которые оказывают помощь при работе с Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="255b2-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), the same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="255b2-119">Вы можете оценить затраты на основе текущих показателей использования, обратившись в [службу поддержки Azure](https://azure.microsoft.com/support/plans/). А после выхода калькулятора стоимости (ожидается в ближайшем времени) вы сможете самостоятельно выполнять такие вычисления.</span><span class="sxs-lookup"><span data-stu-id="255b2-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon to be released Cost Calculator.</span></span>  <span data-ttu-id="255b2-120">Кроме того, используя виртуальные машины серии N (сейчас доступны в режиме личной предварительной версии), вы можете добавить vGPU. Узнать больше о добавлении vGPU, а также о том, как [использовать оптимизированные возможности RDS в Windows Server 2016](https://myignite.microsoft.com/videos/2794) можно из нашей презентации Ignite.</span><span class="sxs-lookup"><span data-stu-id="255b2-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how to [harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="255b2-121">Чтобы помочь вам, мы также создали пошаговые руководства по развертыванию [Windows Server 2012 R2](http://aka.ms/rdsonazure) и [Windows Server 2016](http://aka.ms/rdsonazure2016).</span><span class="sxs-lookup"><span data-stu-id="255b2-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) to assist with your deployment.</span></span> <span data-ttu-id="255b2-122">Последние новости можно узнать в [блоге, посвященном операциям с удаленным рабочим столом](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services).</span><span class="sxs-lookup"><span data-stu-id="255b2-122">Check out the [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for the latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="255b2-123">**Citrix в IaaS**</span><span class="sxs-lookup"><span data-stu-id="255b2-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="255b2-124">Собственное развертывание Citrix на основе сеансов XenApp или XenDesktop можно реализовать в локальной или размещенной среде (включая виртуальные машины Azure).</span><span class="sxs-lookup"><span data-stu-id="255b2-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="255b2-125">Дополнительные сведения см. в пошаговом руководстве по развертыванию [Citrix ХА 7.6 в Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx).</span><span class="sxs-lookup"><span data-stu-id="255b2-125">Check out the step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="255b2-126">Также см. дополнительные сведения о [Citrix в Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), включая сведения о калькуляторе стоимости.</span><span class="sxs-lookup"><span data-stu-id="255b2-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="255b2-127">Вы также можете воспользоваться [контактными данными Citrix](http://citrix.com/English/contact/index.asp), чтобы непосредственно обсудить все интересующие вас варианты.</span><span class="sxs-lookup"><span data-stu-id="255b2-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) to discuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="255b2-128">Полностью управляемые предложения (PaaS или SaaS)</span><span class="sxs-lookup"><span data-stu-id="255b2-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="255b2-129">Citrix XenApp Essentials (выпуск за апрель 2017 г.)</span><span class="sxs-lookup"><span data-stu-id="255b2-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="255b2-130">Решение Citrix XenApp Essentials теперь доступно в [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials). Citrix XenApp Essentials — это новая служба виртуализации приложений, объединившая в себе мощь и гибкость облачной платформы Citrix с простой, процедурной и удобной в использовании концепцией Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="255b2-130">Available now on the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is the new application virtualization service, combining the power and flexibility of the Citrix Cloud platform with the simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="255b2-131">Клиенты Azure RemoteApp могут [зарегистрироваться для получения бесплатной пробной версии](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="255b2-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="255b2-132">Примечание. Бесплатно предоставляется только служба пользователей Citrix, вычислительные ресурсы и ресурсы службы хранилища Azure предоставляются за плату.</span><span class="sxs-lookup"><span data-stu-id="255b2-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="255b2-133">Дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="255b2-133">Learn More:</span></span>
- [<span data-ttu-id="255b2-134">Миграция из Azure RemoteApp в Citrix XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="255b2-134">Migrate from Azure RemoteApp to Citrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="255b2-135">Citrix и Майкрософт</span><span class="sxs-lookup"><span data-stu-id="255b2-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="255b2-136">[Презентация по Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k)</span><span class="sxs-lookup"><span data-stu-id="255b2-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="255b2-137">Службы Citrix Cloud XenApp и XenDesktop</span><span class="sxs-lookup"><span data-stu-id="255b2-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="255b2-138">[Службы Citrix Cloud XenApp и XenDesktop](https://www.citrix.com/products/citrix-cloud/services.html) — это наилучшее решение для доставки и приложений и рабочих столов, предоставляющее расширенные возможности управления и мониторинга.</span><span class="sxs-lookup"><span data-stu-id="255b2-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is the best solution for the delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="255b2-139">Conexlink (имя платформы: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="255b2-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="255b2-140">[MyCloudIT](https://mycloudit.com) — это платформа автоматизации для ИТ-компаний, которая помогает упростить, оптимизировать и масштабировать миграцию и доставку удаленных рабочих столов и приложений, а также инфраструктуры в облако Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="255b2-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies to simplify, optimize, and scale the migration and delivery of remote desktops, remote applications, and infrastructure in the Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="255b2-141">Платформа MyCloudIT на 95 % сокращает время развертывания, на 30 % снижает расходы на использование решений Azure, а также выполняет быструю миграцию всей клиентской ИТ-инфраструктуры в облако.</span><span class="sxs-lookup"><span data-stu-id="255b2-141">The MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into the cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="255b2-142">Теперь партнеры могут управлять клиентами из единой глобальной панели мониторинга в рамках эффективной стратегии обслуживая пользователей во всем мире, увеличивая свои доходы без дополнительных вложений, необходимых для прохождения обучающих программ Azure.</span><span class="sxs-lookup"><span data-stu-id="255b2-142">Partners can now manage customers from one global dashboard, service end users around the world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="255b2-143">Основное расположение: Даллас, Техас, США.</span><span class="sxs-lookup"><span data-stu-id="255b2-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="255b2-144">Целевой регион: весь мир.</span><span class="sxs-lookup"><span data-stu-id="255b2-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="255b2-145">Статус партнера: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink).</span><span class="sxs-lookup"><span data-stu-id="255b2-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="255b2-146">Поставщик служб Microsoft Cloud: да.</span><span class="sxs-lookup"><span data-stu-id="255b2-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="255b2-147">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="255b2-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="255b2-148">Решения для миграции Azure RemoteApp: да, [см. дополнительные сведения](https://mycloudit.com/remote-app-microsoft/).</span><span class="sxs-lookup"><span data-stu-id="255b2-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="255b2-149">Брайан Гарутт (Brian Garoutte), вице-президент отдела по развитию бизнеса</span><span class="sxs-lookup"><span data-stu-id="255b2-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="255b2-150">Тел.: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="255b2-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="255b2-151">Эл. адрес: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="255b2-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="255b2-152">Frame</span><span class="sxs-lookup"><span data-stu-id="255b2-152">Frame</span></span>

<span data-ttu-id="255b2-153">ИТ-организации на предприятиях и в правительственных учреждениях, поставщики управляемых услуг и ведущие поставщики программного обеспечения выбирают Frame для создания безопасных программно-определяемых рабочих областей в облаке и управления ими.</span><span class="sxs-lookup"><span data-stu-id="255b2-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame to create and manage their secure, software-defined workspaces in the cloud.</span></span> <span data-ttu-id="255b2-154">Применение Frame в организациях любого размера невероятно упрощает предоставление пользователям доступа к приложениям для Windows в любом браузере на любом устройстве.</span><span class="sxs-lookup"><span data-stu-id="255b2-154">From small to large organizations, Frame makes it incredibly easy to let users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="255b2-155">Платформа Frame содержит все инструменты, необходимые администратору для развертывания приложений из облака, включая инфраструктуру Azure и лицензии RDS (использовать собственную учетную запись Azure и лицензии не обязательно).</span><span class="sxs-lookup"><span data-stu-id="255b2-155">The Frame platform includes everything an admin needs to deploy applications from the cloud including the Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="255b2-156">Узнайте больше об использовании [Frame в Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="255b2-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="255b2-157">Основное расположение: Сан-Матео, штат Калифорния, США.</span><span class="sxs-lookup"><span data-stu-id="255b2-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="255b2-158">Целевой регион: весь мир.</span><span class="sxs-lookup"><span data-stu-id="255b2-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="255b2-159">Партнер Майкрософт: да.</span><span class="sxs-lookup"><span data-stu-id="255b2-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="255b2-160">Телефон: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="255b2-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="255b2-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="255b2-161">Awingu</span></span>
<span data-ttu-id="255b2-162">Awingu представляет собой простое интерактивное рабочее пространство для устаревших приложений, служб SaaS и документов, работающее в браузере HTML5.</span><span class="sxs-lookup"><span data-stu-id="255b2-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="255b2-163">С его помощью можно безопасно предоставить любые приложения на устройстве любого типа.</span><span class="sxs-lookup"><span data-stu-id="255b2-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="255b2-164">Для служб SaaS доступен широкий диапазон возможностей единого входа.</span><span class="sxs-lookup"><span data-stu-id="255b2-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="255b2-165">Кроме того, в рабочую область могут быть тесно интегрированы разнообразные файловые системы (облачные).</span><span class="sxs-lookup"><span data-stu-id="255b2-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="255b2-166">Наряду с полной мобильностью, многофункциональное интерактивное рабочее пространство Awingu обеспечит оптимальную безопасность благодаря детализированному контролю (например, скачивания и передачи данных), полноценному аудиту, Многофакторной идентификации (например, Azure MFA), записи сеансов и многим другим функциям.</span><span class="sxs-lookup"><span data-stu-id="255b2-166">Next to full mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="255b2-167">Готовое решение Awingu поддерживает сеансы совместного использования документов и приложений, что обеспечивает оптимальную и безопасную совместную работу.</span><span class="sxs-lookup"><span data-stu-id="255b2-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="255b2-168">Решение Awingu является мультитенантым, поддерживает несколько каталогов AD и открытые API.</span><span class="sxs-lookup"><span data-stu-id="255b2-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="255b2-169">Его используют владельцы малого и крупного бизнеса, поставщики облачных служб и [независимые поставщики программного обеспечения](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="255b2-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="255b2-170">Эти клиенты особенно ценят удобство использования, простоту установки и низкую совокупную стоимость владения.</span><span class="sxs-lookup"><span data-stu-id="255b2-170">These customers especially appreciate the easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="255b2-171">Решение Awingu All-in-One [доступно на сайте в Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) с двумя встроенными параллельно работающими пользователями.</span><span class="sxs-lookup"><span data-stu-id="255b2-171">Awingu All-in-One is [available in the Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="255b2-172">Дополнительные лицензии можно приобрести у [широкого диапазона распространителей и торговых посредников](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="255b2-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="255b2-173">Узнайте больше об [использовании Awingu в качестве альтернативы Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="255b2-173">Learn more about [Awingu on as alternative to Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="255b2-174">Основное расположение: Бельгия.</span><span class="sxs-lookup"><span data-stu-id="255b2-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="255b2-175">Регионы присутствия: Европа, Ближний Восток и Африка, Северная Америка и Бразилия.</span><span class="sxs-lookup"><span data-stu-id="255b2-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="255b2-176">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="255b2-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="255b2-177">**Международная контактная информация**:</span><span class="sxs-lookup"><span data-stu-id="255b2-177">**Global**:</span></span>
> 
> <span data-ttu-id="255b2-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="255b2-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="255b2-179">Эл. адрес: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="255b2-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="255b2-180">Телефон: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="255b2-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="255b2-181">**Штаб-квартира в Бельгии**:</span><span class="sxs-lookup"><span data-stu-id="255b2-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="255b2-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="255b2-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="255b2-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="255b2-183">9000 Gent</span></span>
> 
> <span data-ttu-id="255b2-184">Эл. адрес: [info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="255b2-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="255b2-185">Телефон: +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="255b2-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="255b2-186">**США**:</span><span class="sxs-lookup"><span data-stu-id="255b2-186">**USA**:</span></span>
> 
> <span data-ttu-id="255b2-187">7th floor, 1177 Ave of the Americas,</span><span class="sxs-lookup"><span data-stu-id="255b2-187">7th floor, 1177 Ave of the Americas,</span></span>
> 
> <span data-ttu-id="255b2-188">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="255b2-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="255b2-189">Эл. адрес: [info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="255b2-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="255b2-190">Поставщик размещенных служб Майкрософт</span><span class="sxs-lookup"><span data-stu-id="255b2-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="255b2-191">Партнеры, предоставляющие услуги размещения, обычно предлагают не только полностью управляемые размещенные классические приложения Windows, но и службу приложений. Эта служба позволяет управлять ресурсами Azure, операционными системами, приложениями и службами технической поддержки в рамках партнерских лицензионных соглашений с корпорацией Майкрософт и другими поставщиками программного обеспечения. Кроме того, в рамках лицензионного соглашения поставщика услуг такие партнеры могут заниматься перепродажей лицензий подписчика (SAL).</span><span class="sxs-lookup"><span data-stu-id="255b2-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing the Azure resources, operating systems, applications, and helpdesk using the partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement to allow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="255b2-192">Ниже приведены подробные сведения о некоторых поставщиках услуг размещения (включая контактные данные). Все они помогают пользователям выполнять миграцию Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="255b2-192">The following information provides details and contact information for some of the hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="255b2-193">Ознакомьтесь с [текущим списком сертифицированных поставщиков размещенных служб](http://aka.ms/rdsonazurecertified), которые оказывают услуги, связанные с RDS в IaaS.</span><span class="sxs-lookup"><span data-stu-id="255b2-193">Check out [the current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed the RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="255b2-194">Программа поставщиков услуг Citrix</span><span class="sxs-lookup"><span data-stu-id="255b2-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="255b2-195">Эта программа Citrix упрощает поставщикам услуг процесс предоставления вычислительных ресурсов виртуального облака для малого и среднего бизнеса, предлагая соответствующие службы с оплатой по мере использования.</span><span class="sxs-lookup"><span data-stu-id="255b2-195">The Citrix Service Provider Program makes it easy for service providers to deliver the simplicity of virtual cloud computing to SMBs, offering them the services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="255b2-196">Поставщики услуг Citrix развивают свой бизнес в рамках соглашения Microsoft SPLA и увеличивают инвестиции в платформу RDS, реализуя поддержку разных устройств и приложений, удобный интерфейс, а также обеспечивая повсеместный доступ, защиту и масштабируемость.</span><span class="sxs-lookup"><span data-stu-id="255b2-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, the broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="255b2-197">Все это позволяет поставщикам услуг Citrix привлекать большее число подписчиков, повышать уровень удовлетворенности клиентов и снижать расходы.</span><span class="sxs-lookup"><span data-stu-id="255b2-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="255b2-198">[См. дополнительные сведения](http://www.citrix.com/products/service-providers.html) или [найдите партнера](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="255b2-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="255b2-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="255b2-199">Acuutech</span></span>
<span data-ttu-id="255b2-200">[Acuutech](http://www.acuutech.com) специализируется на предоставлении размещенных классических решений, предоставляя участникам глобальной клиентской базы не только все связанные функции и возможности приложений от независимых поставщиков программного обеспечения на основе технологии Майкрософт из Azure, но также собственные центры обработки данных.</span><span class="sxs-lookup"><span data-stu-id="255b2-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology to a global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="255b2-201">Основное расположение: Лондон, Соединенное Королевство; Сингапур; Хьюстон, Техас.</span><span class="sxs-lookup"><span data-stu-id="255b2-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="255b2-202">Целевой регион: весь мир.</span><span class="sxs-lookup"><span data-stu-id="255b2-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="255b2-203">Статус партнера: Gold.</span><span class="sxs-lookup"><span data-stu-id="255b2-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="255b2-204">Поставщик служб Microsoft Cloud: да.</span><span class="sxs-lookup"><span data-stu-id="255b2-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="255b2-205">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="255b2-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="255b2-206">Решения для миграции Azure RemoteApp: да, [см. дополнительные сведения](http://www.acuutech.com/ara-migration/).</span><span class="sxs-lookup"><span data-stu-id="255b2-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="255b2-207">**Соединенное Королевство**:</span><span class="sxs-lookup"><span data-stu-id="255b2-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="255b2-208">5/6 York House, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="255b2-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="255b2-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="255b2-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="255b2-210">Тел.: +44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="255b2-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="255b2-211">**Сингапур**:</span><span class="sxs-lookup"><span data-stu-id="255b2-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="255b2-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="255b2-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="255b2-213">The Globe, Singapore 069532</span><span class="sxs-lookup"><span data-stu-id="255b2-213">The Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="255b2-214">Тел.: +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="255b2-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="255b2-215">**Северная Америка**:</span><span class="sxs-lookup"><span data-stu-id="255b2-215">**North America**:</span></span>
>   
> <span data-ttu-id="255b2-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="255b2-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="255b2-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="255b2-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="255b2-218">Тел.: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="255b2-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="255b2-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="255b2-219">ASPEX</span></span>
<span data-ttu-id="255b2-220">[ASPEX](http://www.aspex.be/en) специализируется на миграции продуктов от независимых поставщиков программного обеспечения в облако, помогая таким поставщикам оптимизировать текущие настройки облака.</span><span class="sxs-lookup"><span data-stu-id="255b2-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning to the Cloud and ISV‘ looking to optimize their current cloud setups.</span></span> <span data-ttu-id="255b2-221">ASPEX предлагает множество управляемых служб и решений DevOps, а также предоставляет консультационные услуги.</span><span class="sxs-lookup"><span data-stu-id="255b2-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="255b2-222">Основное расположение: Антверпен, Бельгия.</span><span class="sxs-lookup"><span data-stu-id="255b2-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="255b2-223">Целевой регион: Западная Европа.</span><span class="sxs-lookup"><span data-stu-id="255b2-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="255b2-224">Статус партнера: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff).</span><span class="sxs-lookup"><span data-stu-id="255b2-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="255b2-225">Поставщик служб Microsoft Cloud: да.</span><span class="sxs-lookup"><span data-stu-id="255b2-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="255b2-226">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="255b2-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="255b2-227">Решения для миграции Azure RemoteApp: да, [см. дополнительные сведения](https://www.aspex.be/en/azure-remote-apps).</span><span class="sxs-lookup"><span data-stu-id="255b2-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="255b2-228">Тел.: +3232202198</span><span class="sxs-lookup"><span data-stu-id="255b2-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="255b2-229">Эл. адрес: [info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="255b2-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="255b2-230">Сайт: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="255b2-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="255b2-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="255b2-231">Caase.com</span></span>
<span data-ttu-id="255b2-232">[Caase.com](http://www.caase.com/) помогает предприятиям, местным государственным организациям, неправительственным органам и учреждениям здравоохранения повысить эффективность работы с Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="255b2-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in the Microsoft Cloud.</span></span> <span data-ttu-id="255b2-233">Обеспечьте производительность и безопасность работы в любом месте и на любых устройствах с низкими затратами на ИТ.</span><span class="sxs-lookup"><span data-stu-id="255b2-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="255b2-234">Caase.com — настоящий специалист в области Microsoft Office 365, Azure, Enterprise Mobility and Security и Windows.</span><span class="sxs-lookup"><span data-stu-id="255b2-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="255b2-235">Консультации, услуги миграции, программы освоения, обучение, помощь в управлении и поддержка, предоставляемые компанией Caase.com, позволяют создать оптимизированную безопасную платформу для совместной работы сотрудников, партнеров и поставщиков клиента.</span><span class="sxs-lookup"><span data-stu-id="255b2-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="255b2-236">Caase.com предлагает решения Azure Remote Workspace (мобильное рабочее место) и Digital Workplace (социальная интрасеть).</span><span class="sxs-lookup"><span data-stu-id="255b2-236">Caase.com is the mastermind of the Azure Remote Workspace (mobile workplace) and the Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="255b2-237">Эти решения, а также сопутствующие услуги по их освоению, являются фундаментом, который обеспечивает успешный и эффективный переход пользователей к работе с Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="255b2-237">Both solutions – accomplished with adoption – are the foundation which ensures that the users of these solutions have the most pleasant, successful and effective experience in their route to the Microsoft Cloud.</span></span>
<span data-ttu-id="255b2-238">Этот текст на нидерландском языке и видеоролик доступны на странице по адресу http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="255b2-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="255b2-239">Целевой регион: весь мир, находится в Нидерландах</span><span class="sxs-lookup"><span data-stu-id="255b2-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="255b2-240">Статус партнера: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3).</span><span class="sxs-lookup"><span data-stu-id="255b2-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="255b2-241">Поставщик служб Microsoft Cloud: да.</span><span class="sxs-lookup"><span data-stu-id="255b2-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="255b2-242">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="255b2-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="255b2-243">Решения для миграции Azure RemoteApp: да, [см. дополнительные сведения](http://caase.com/diensten/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="255b2-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="255b2-244">Нидерланды:</span><span class="sxs-lookup"><span data-stu-id="255b2-244">Netherlands:</span></span>
> 
> <span data-ttu-id="255b2-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="255b2-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="255b2-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="255b2-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="255b2-247">Телефон: +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="255b2-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="255b2-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="255b2-248">Nerdio</span></span>
<span data-ttu-id="255b2-249">[Nerdio для Azure](http://getnerdio.com/nfa/) — это платформа автоматизации ИТ, обеспечивающая невероятно простой процесс подготовки, администрирования и оптимизации готовых ИТ-сред в облаке Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="255b2-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in the Microsoft cloud.</span></span> <span data-ttu-id="255b2-250">Подготавливайте виртуальные рабочие столы, удаленные приложения и серверы буквально за пару часов.</span><span class="sxs-lookup"><span data-stu-id="255b2-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="255b2-251">Управляйте средой в несколько щелчков с помощью портала администрирования Nerdio.</span><span class="sxs-lookup"><span data-stu-id="255b2-251">Administer the environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="255b2-252">Используйте интеллектуальное автоматическое масштабирование и экономьте от 40 до 60 % на ресурсах Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="255b2-252">Use intelligent auto-scaling and save 40 to 60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="255b2-253">Основное местоположение: Чикаго, штат Иллинойс. Целевой регион: весь мир. Статус партнера: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1). Поставщик служб Microsoft Cloud: да</span><span class="sxs-lookup"><span data-stu-id="255b2-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="255b2-254">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="255b2-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="255b2-255">Решения для миграции Azure RemoteApp: да</span><span class="sxs-lookup"><span data-stu-id="255b2-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="255b2-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="255b2-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="255b2-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="255b2-257">Suite 212</span></span>
> 
> <span data-ttu-id="255b2-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="255b2-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="255b2-259">США</span><span class="sxs-lookup"><span data-stu-id="255b2-259">USA</span></span>
> 
> <span data-ttu-id="255b2-260">(844) 4NERDIO ext.</span><span class="sxs-lookup"><span data-stu-id="255b2-260">(844) 4NERDIO ext.</span></span> <span data-ttu-id="255b2-261">6</span><span class="sxs-lookup"><span data-stu-id="255b2-261">6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="255b2-262">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="255b2-262">**SaaSplaza**</span></span>
<span data-ttu-id="255b2-263">[SaaSplaza](http://www.saasplaza.com/) предлагает полный портфель Microsoft Dynamics (NAV, AX, GP, SL, CRM) для частного и общедоступного облака (Azure).</span><span class="sxs-lookup"><span data-stu-id="255b2-263">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="255b2-264">Основное местоположение: Нидерланды.</span><span class="sxs-lookup"><span data-stu-id="255b2-264">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="255b2-265">Целевой регион: весь мир.</span><span class="sxs-lookup"><span data-stu-id="255b2-265">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="255b2-266">Статус партнера: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza).</span><span class="sxs-lookup"><span data-stu-id="255b2-266">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="255b2-267">Поставщик служб Microsoft Cloud: да.</span><span class="sxs-lookup"><span data-stu-id="255b2-267">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="255b2-268">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="255b2-268">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="255b2-269">**Европа, Ближний Восток и Африка**:</span><span class="sxs-lookup"><span data-stu-id="255b2-269">**EMEA**:</span></span>
> 
> <span data-ttu-id="255b2-270">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="255b2-270">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="255b2-271">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="255b2-271">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="255b2-272">The Netherlands</span><span class="sxs-lookup"><span data-stu-id="255b2-272">The Netherlands</span></span>
> 
> <span data-ttu-id="255b2-273">Телефон: +31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="255b2-273">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="255b2-274">**Северная и Южная Америки**:</span><span class="sxs-lookup"><span data-stu-id="255b2-274">**Americas**:</span></span>
> 
> <span data-ttu-id="255b2-275">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="255b2-275">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="255b2-276">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="255b2-276">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="255b2-277">San Diego</span><span class="sxs-lookup"><span data-stu-id="255b2-277">San Diego</span></span>
> 
> <span data-ttu-id="255b2-278">США</span><span class="sxs-lookup"><span data-stu-id="255b2-278">United States</span></span>
> 
> <span data-ttu-id="255b2-279">Телефон: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="255b2-279">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="255b2-280">**Азиатско-тихоокеанский регион**:</span><span class="sxs-lookup"><span data-stu-id="255b2-280">**APAC**:</span></span>
> 
> <span data-ttu-id="255b2-281">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="255b2-281">105 Cecil Street</span></span>
>    
> <span data-ttu-id="255b2-282">\#11-08, The Octagon</span><span class="sxs-lookup"><span data-stu-id="255b2-282">\#11-08, The Octagon</span></span>
> 
> <span data-ttu-id="255b2-283">Singapore 069534</span><span class="sxs-lookup"><span data-stu-id="255b2-283">Singapore 069534</span></span>
> 
> <span data-ttu-id="255b2-284">Сингапур</span><span class="sxs-lookup"><span data-stu-id="255b2-284">Singapore</span></span>
>   
> <span data-ttu-id="255b2-285">Телефон в Сингапуре: +65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="255b2-285">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="255b2-286">Телефон в Австралии: +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="255b2-286">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="255b2-287">Телефон в Новой Зеландии: +64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="255b2-287">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="255b2-288">Требуется дополнительная помощь?</span><span class="sxs-lookup"><span data-stu-id="255b2-288">Need more help?</span></span>
<span data-ttu-id="255b2-289">Все еще не можете определиться с выбором или возникли дополнительные вопросы?</span><span class="sxs-lookup"><span data-stu-id="255b2-289">Still need help choosing or have further questions?</span></span> <span data-ttu-id="255b2-290">Получить справку можно с помощью одного из указанных ниже методов.</span><span class="sxs-lookup"><span data-stu-id="255b2-290">Use one of the following methods to get help.</span></span> 

1. <span data-ttu-id="255b2-291">Напишите нам по адресу [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="255b2-291">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="255b2-292">Обратитесь в [службу поддержки Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="255b2-292">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="255b2-293">Создайте [запрос в службу поддержке Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="255b2-293">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="255b2-294">Позвоните нам по</span><span class="sxs-lookup"><span data-stu-id="255b2-294">Call us.</span></span> <span data-ttu-id="255b2-295">[номеру телефона местного отдела продаж](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="255b2-295">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

