---
title: "aaaOptions для переноса из Azure RemoteApp | Документы Microsoft"
description: "Сведения о способах hello миграция из Azure RemoteApp."
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
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="d161d-103">Варианты переноса из Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d161d-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d161d-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="d161d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d161d-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="d161d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="d161d-106">Если остановить с помощью Azure RemoteApp из-за hello [уведомления о выбывании](https://go.microsoft.com/fwlink/?linkid=821148) или из-за завершения пробного использования требуется toomigrate за пределами Azure RemoteApp tooanother приложения службы.</span><span class="sxs-lookup"><span data-stu-id="d161d-106">If you have stopped using Azure RemoteApp because of hello [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need toomigrate off of Azure RemoteApp tooanother app service.</span></span> <span data-ttu-id="d161d-107">Есть два подхода к миграции: с самостоятельным управлением развертыванием (это предложение называется инфраструктура как услуга [IaaS]) и полностью управляемым развертыванием (это предложение называется платформа как услуга или программное обеспечение как услуга [PaaS или SaaS]).</span><span class="sxs-lookup"><span data-stu-id="d161d-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="d161d-108">Предложение IaaS с самостоятельным обслуживанием — это управляемое, эксплуатируемое и принадлежащее вам решение, развернутое непосредственно на виртуальных машинах (ВМ) или физических системах.</span><span class="sxs-lookup"><span data-stu-id="d161d-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="d161d-109">В других hello завершить, полностью управляемая PaaS и SaaS, предложение, несколько таких как Azure RemoteApp — партнером предоставляет уровень службы на основе решение удаленного взаимодействия, которое обрабатывает оперативной и обслуживания, пока пользователь, как клиент hello не некоторых изображений и приложения управления.</span><span class="sxs-lookup"><span data-stu-id="d161d-109">At hello other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as hello customer, do some image and app management.</span></span>

<span data-ttu-id="d161d-110">[Просмотр hello Azure RemoteApp вебинары о вариантах переноса](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), или чтения на дополнительные сведения (в том числе примеры различных вариантов размещения hello).</span><span class="sxs-lookup"><span data-stu-id="d161d-110">[View hello Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of hello different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="d161d-111">Самостоятельно управляемые решения (IaaS)</span><span class="sxs-lookup"><span data-stu-id="d161d-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="d161d-112">**RDS в IaaS**</span><span class="sxs-lookup"><span data-stu-id="d161d-112">**RDS on IaaS**</span></span>
<span data-ttu-id="d161d-113">Вы можете выполнять собственные развертывания на основе сеансов служб удаленных рабочих столов (в Windows Server) с помощью RemoteApp или классических приложений в локальной или размещенной среде (включая виртуальные машины Azure).</span><span class="sxs-lookup"><span data-stu-id="d161d-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="d161d-114">RDS в развертываниях IaaS лучше всего подходит для более опытных клиентов, которые уже знакомы с технической стороной этого процесса.</span><span class="sxs-lookup"><span data-stu-id="d161d-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="d161d-115">Необходимо корпоративного лицензирования с помощью программы Software Assurance (SA) для доступа к лицензии служб удаленных рабочих СТОЛОВ клиента toouse этот параметр развертывания.</span><span class="sxs-lookup"><span data-stu-id="d161d-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses toouse this deployment option.</span></span>

<span data-ttu-id="d161d-116">Развертывать RDS на виртуальных машинах Azure проще, чем использовать шаблоны развертывания и исправления (см. [обзор](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/), а затем переходите к [скачиванию](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="d161d-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="d161d-117">Hello можно получить такие же возможности эластичного масштабирования развертывания Azure классической модели ресурсы (не модели ресурсов Azure) в Azure RemoteApp с помощью hello [автоматическое масштабирование сценария](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), хотя есть и другие шаги по настройке.</span><span class="sxs-lookup"><span data-stu-id="d161d-117">You can get hello same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using hello [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="d161d-118">При развертывании служб удаленных рабочих СТОЛОВ на виртуальных машинах Azure, поддержка обеспечивается [Azure поддерживает](https://azure.microsoft.com/support/plans/), hello же специалисты службы технической поддержки, поддерживаемые Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d161d-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), hello same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="d161d-119">Вы можно получить оценки затрат на основе существующих использования, обратившись в службу [поддержки Azure](https://azure.microsoft.com/support/plans/), или вы самостоятельно выполнять вычисления с помощью перспективные toobe калькулятора.</span><span class="sxs-lookup"><span data-stu-id="d161d-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon toobe released Cost Calculator.</span></span>  <span data-ttu-id="d161d-120">Кроме того, виртуальные машины серии N (в настоящее время в личной предварительной версии) позволяет добавлять vGPU - узнать больше о добавлении vGPU и о том, как слишком[использующих улучшения служб удаленных рабочих СТОЛОВ в Windows Server 2016](https://myignite.microsoft.com/videos/2794) в нашем Ignite сеанса.</span><span class="sxs-lookup"><span data-stu-id="d161d-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how too[harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="d161d-121">У нас есть руководствах по развертыванию шаг за шагом [Windows Server 2012 R2](http://aka.ms/rdsonazure) и [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist с развертыванием.</span><span class="sxs-lookup"><span data-stu-id="d161d-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist with your deployment.</span></span> <span data-ttu-id="d161d-122">Извлечение hello [удаленного рабочего стола блог](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) последние новости hello.</span><span class="sxs-lookup"><span data-stu-id="d161d-122">Check out hello [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for hello latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="d161d-123">**Citrix в IaaS**</span><span class="sxs-lookup"><span data-stu-id="d161d-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="d161d-124">Собственное развертывание Citrix на основе сеансов XenApp или XenDesktop можно реализовать в локальной или размещенной среде (включая виртуальные машины Azure).</span><span class="sxs-lookup"><span data-stu-id="d161d-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="d161d-125">Ознакомьтесь с руководством по Пошаговое руководство по развертыванию hello, [Citrix 7.6 XA в Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="d161d-125">Check out hello step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="d161d-126">Также см. дополнительные сведения о [Citrix в Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), включая сведения о калькуляторе стоимости.</span><span class="sxs-lookup"><span data-stu-id="d161d-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="d161d-127">Можно также найти [Citrix контакт](http://citrix.com/English/contact/index.asp) toodiscuss варианты с.</span><span class="sxs-lookup"><span data-stu-id="d161d-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="d161d-128">Полностью управляемые предложения (PaaS или SaaS)</span><span class="sxs-lookup"><span data-stu-id="d161d-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="d161d-129">Citrix XenApp Essentials (выпуск за апрель 2017 г.)</span><span class="sxs-lookup"><span data-stu-id="d161d-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="d161d-130">Теперь доступны на hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials — hello новой службы виртуализации приложения, объединяя hello power и гибкость hello Citrix облачной платформы с простыми hello, предписывающее, и простой в использовании концепции Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d161d-130">Available now on hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is hello new application virtualization service, combining hello power and flexibility of hello Citrix Cloud platform with hello simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="d161d-131">Клиенты Azure RemoteApp могут [зарегистрироваться для получения бесплатной пробной версии](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="d161d-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="d161d-132">Примечание. Бесплатно предоставляется только служба пользователей Citrix, вычислительные ресурсы и ресурсы службы хранилища Azure предоставляются за плату.</span><span class="sxs-lookup"><span data-stu-id="d161d-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="d161d-133">Дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="d161d-133">Learn More:</span></span>
- [<span data-ttu-id="d161d-134">Миграция из Azure RemoteApp tooCitrix XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="d161d-134">Migrate from Azure RemoteApp tooCitrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="d161d-135">Citrix и Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d161d-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="d161d-136">[Презентация по Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k)</span><span class="sxs-lookup"><span data-stu-id="d161d-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="d161d-137">Службы Citrix Cloud XenApp и XenDesktop</span><span class="sxs-lookup"><span data-stu-id="d161d-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="d161d-138">[Citrix облачной XenApp службы и службы XenDesktop](https://www.citrix.com/products/citrix-cloud/services.html) является наилучшим решением hello доставку hello и приложения и настольных компьютеров, а также расширенные функции управления и возможности мониторинга.</span><span class="sxs-lookup"><span data-stu-id="d161d-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is hello best solution for hello delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="d161d-139">Conexlink (имя платформы: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="d161d-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="d161d-140">[MyCloudIT](https://mycloudit.com) — это автоматизированная платформа для toosimplify ИТ компании, оптимизации и масштабировать миграции hello и Здравствуйте, доставки удаленные рабочие столы, удаленных приложений и инфраструктуры в облако Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d161d-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies toosimplify, optimize, and scale hello migration and delivery of remote desktops, remote applications, and infrastructure in hello Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="d161d-141">Платформа MyCloudIT Hello сокращает время развертывания на 95%, затраты на 30%, Azure и перемещает клиента по всей ИТ-инфраструктуры в облако hello в течение нескольких несколько нажатий клавиш.</span><span class="sxs-lookup"><span data-stu-id="d161d-141">hello MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into hello cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="d161d-142">Партнеры теперь могут управлять пользователи одной глобальной панели мониторинга, конечные пользователи службы вокруг Здравствуй, мир! как раньше и роста доходов без добавления дополнительных затрат или обучение Azure.</span><span class="sxs-lookup"><span data-stu-id="d161d-142">Partners can now manage customers from one global dashboard, service end users around hello world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="d161d-143">Основное расположение: Даллас, Техас, США.</span><span class="sxs-lookup"><span data-stu-id="d161d-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="d161d-144">Целевой регион: весь мир.</span><span class="sxs-lookup"><span data-stu-id="d161d-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="d161d-145">Статус партнера: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink).</span><span class="sxs-lookup"><span data-stu-id="d161d-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="d161d-146">Поставщик служб Microsoft Cloud: да.</span><span class="sxs-lookup"><span data-stu-id="d161d-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="d161d-147">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="d161d-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="d161d-148">Решения для миграции Azure RemoteApp: да, [см. дополнительные сведения](https://mycloudit.com/remote-app-microsoft/).</span><span class="sxs-lookup"><span data-stu-id="d161d-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="d161d-149">Брайан Гарутт (Brian Garoutte), вице-президент отдела по развитию бизнеса</span><span class="sxs-lookup"><span data-stu-id="d161d-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="d161d-150">Тел.: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="d161d-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="d161d-151">Эл. адрес: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="d161d-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="d161d-152">Frame</span><span class="sxs-lookup"><span data-stu-id="d161d-152">Frame</span></span>

<span data-ttu-id="d161d-153">ИТ-организаций enterprise и государственных организаций, управляемых поставщиков и ведущих поставщиков программного обеспечения выберите кадр toocreate и управлять их рабочих областей безопасности, определяемые программного обеспечения в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="d161d-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame toocreate and manage their secure, software-defined workspaces in hello cloud.</span></span> <span data-ttu-id="d161d-154">Из организаций малого toolarge кадра делает его очень легко toolet пользователей доступ к приложениям Windows в любом браузере с любого устройства.</span><span class="sxs-lookup"><span data-stu-id="d161d-154">From small toolarge organizations, Frame makes it incredibly easy toolet users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="d161d-155">Hello рамки платформы включает все, что администратор потребностей toodeploy приложения из облака hello, включая hello инфраструктуры Azure и лицензии служб удаленных рабочих СТОЛОВ (Совместная собственную учетную запись Azure и лицензии не обязательно).</span><span class="sxs-lookup"><span data-stu-id="d161d-155">hello Frame platform includes everything an admin needs toodeploy applications from hello cloud including hello Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="d161d-156">Узнайте больше об использовании [Frame в Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="d161d-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="d161d-157">Основное расположение: Сан-Матео, штат Калифорния, США.</span><span class="sxs-lookup"><span data-stu-id="d161d-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="d161d-158">Целевой регион: весь мир.</span><span class="sxs-lookup"><span data-stu-id="d161d-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="d161d-159">Партнер Майкрософт: да.</span><span class="sxs-lookup"><span data-stu-id="d161d-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="d161d-160">Телефон: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="d161d-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="d161d-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="d161d-161">Awingu</span></span>
<span data-ttu-id="d161d-162">Awingu представляет собой простое интерактивное рабочее пространство для устаревших приложений, служб SaaS и документов, работающее в браузере HTML5.</span><span class="sxs-lookup"><span data-stu-id="d161d-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="d161d-163">С его помощью можно безопасно предоставить любые приложения на устройстве любого типа.</span><span class="sxs-lookup"><span data-stu-id="d161d-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="d161d-164">Для служб SaaS доступен широкий диапазон возможностей единого входа.</span><span class="sxs-lookup"><span data-stu-id="d161d-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="d161d-165">Кроме того, в рабочую область могут быть тесно интегрированы разнообразные файловые системы (облачные).</span><span class="sxs-lookup"><span data-stu-id="d161d-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="d161d-166">Далее mobility toofull, широкие возможности интерактивное рабочее пространство Awingu даст оптимальной безопасности с детальные элементы управления (например загрузки или передачи данных), полное использование аудит многофакторной проверки подлинности (например многофакторной проверки Подлинности Azure), записи сеанса и многое другое.</span><span class="sxs-lookup"><span data-stu-id="d161d-166">Next toofull mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="d161d-167">Готовое решение Awingu поддерживает сеансы совместного использования документов и приложений, что обеспечивает оптимальную и безопасную совместную работу.</span><span class="sxs-lookup"><span data-stu-id="d161d-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="d161d-168">Решение Awingu является мультитенантым, поддерживает несколько каталогов AD и открытые API.</span><span class="sxs-lookup"><span data-stu-id="d161d-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="d161d-169">Его используют владельцы малого и крупного бизнеса, поставщики облачных служб и [независимые поставщики программного обеспечения](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="d161d-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="d161d-170">Эти клиенты предпочитают особенно hello простой в использовании, простота установки и низкой совокупной стоимости владения.</span><span class="sxs-lookup"><span data-stu-id="d161d-170">These customers especially appreciate hello easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="d161d-171">— Awingu все в одном [в hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) с 2 встроенные одновременных пользователей.</span><span class="sxs-lookup"><span data-stu-id="d161d-171">Awingu All-in-One is [available in hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="d161d-172">Дополнительные лицензии можно приобрести у [широкого диапазона распространителей и торговых посредников](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="d161d-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="d161d-173">Дополнительные сведения о [Awingu в качестве альтернативных tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="d161d-173">Learn more about [Awingu on as alternative tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="d161d-174">Основное расположение: Бельгия.</span><span class="sxs-lookup"><span data-stu-id="d161d-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="d161d-175">Регионы присутствия: Европа, Ближний Восток и Африка, Северная Америка и Бразилия.</span><span class="sxs-lookup"><span data-stu-id="d161d-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="d161d-176">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="d161d-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="d161d-177">**Международная контактная информация**:</span><span class="sxs-lookup"><span data-stu-id="d161d-177">**Global**:</span></span>
> 
> <span data-ttu-id="d161d-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="d161d-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="d161d-179">Эл. адрес: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="d161d-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="d161d-180">Телефон: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="d161d-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="d161d-181">**Штаб-квартира в Бельгии**:</span><span class="sxs-lookup"><span data-stu-id="d161d-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="d161d-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="d161d-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="d161d-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="d161d-183">9000 Gent</span></span>
> 
> <span data-ttu-id="d161d-184">Эл. адрес: [info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="d161d-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="d161d-185">Телефон: +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="d161d-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="d161d-186">**США**:</span><span class="sxs-lookup"><span data-stu-id="d161d-186">**USA**:</span></span>
> 
> <span data-ttu-id="d161d-187">7-й этаж, Ave 1177 из hello Americas,</span><span class="sxs-lookup"><span data-stu-id="d161d-187">7th floor, 1177 Ave of hello Americas,</span></span>
> 
> <span data-ttu-id="d161d-188">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="d161d-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="d161d-189">Эл. адрес: [info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="d161d-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="d161d-190">Поставщик размещенных служб Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d161d-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="d161d-191">Обычно партнеры предоставляют полностью управляемая размещенного рабочего стола Windows и приложения службы, которая может включать управление hello ресурсы Azure, операционных систем, приложений и службу технической поддержки с помощью hello партнера лицензионные соглашения с корпорацией Майкрософт и Помимо того, что лицензионного соглашения с поставщиком службы tooallow перепродажей лицензии доступа подписчика (SAL) других поставщиков программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="d161d-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing hello Azure resources, operating systems, applications, and helpdesk using hello partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement tooallow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="d161d-192">Hello следующая информация содержит сведения и контактные данные для некоторых поставщиков услуг размещения hello, специализирующихся на товарах заказчиков с их перемещением Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d161d-192">hello following information provides details and contact information for some of hello hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="d161d-193">Извлечение [hello текущий список поставщиков размещенной службы](http://aka.ms/rdsonazurecertified) , будут завершены hello служб удаленных рабочих СТОЛОВ в IaaS, обучение, оценка и путь.</span><span class="sxs-lookup"><span data-stu-id="d161d-193">Check out [hello current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed hello RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="d161d-194">Программа поставщиков услуг Citrix</span><span class="sxs-lookup"><span data-stu-id="d161d-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="d161d-195">Hello Citrix служебной программы поставщика упрощает для простоты hello toodeliver поставщиков службы виртуального облачных вычислений tooSMBs, обеспечивая их служб hello нужные им в простой модели оплаты по мере использования.</span><span class="sxs-lookup"><span data-stu-id="d161d-195">hello Citrix Service Provider Program makes it easy for service providers toodeliver hello simplicity of virtual cloud computing tooSMBs, offering them hello services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="d161d-196">Поставщики услуг Citrix роста бизнеса SPLA корпорации Майкрософт и разверните их инвестиции в платформу служб удаленных рабочих СТОЛОВ с любого устройства, Повсеместный доступ, hello широкая поддержка приложений, широкие возможности, повысить уровень безопасности и повышенную масштабируемость.</span><span class="sxs-lookup"><span data-stu-id="d161d-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, hello broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="d161d-197">Все это позволяет поставщикам услуг Citrix привлекать большее число подписчиков, повышать уровень удовлетворенности клиентов и снижать расходы.</span><span class="sxs-lookup"><span data-stu-id="d161d-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="d161d-198">[См. дополнительные сведения](http://www.citrix.com/products/service-providers.html) или [найдите партнера](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="d161d-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="d161d-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="d161d-199">Acuutech</span></span>
<span data-ttu-id="d161d-200">[Acuutech](http://www.acuutech.com) специализируется на предоставления размещенного рабочего стола решений, доставка полный рабочий стол и приложения ISV взаимодействий, построенная на технологии tooa глобального клиентской базы Microsoft Azure и в собственных центрах обработки данных.</span><span class="sxs-lookup"><span data-stu-id="d161d-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology tooa global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="d161d-201">Основное расположение: Лондон, Соединенное Королевство; Сингапур; Хьюстон, Техас.</span><span class="sxs-lookup"><span data-stu-id="d161d-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="d161d-202">Целевой регион: весь мир.</span><span class="sxs-lookup"><span data-stu-id="d161d-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="d161d-203">Статус партнера: Gold.</span><span class="sxs-lookup"><span data-stu-id="d161d-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="d161d-204">Поставщик служб Microsoft Cloud: да.</span><span class="sxs-lookup"><span data-stu-id="d161d-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="d161d-205">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="d161d-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="d161d-206">Решения для миграции Azure RemoteApp: да, [см. дополнительные сведения](http://www.acuutech.com/ara-migration/).</span><span class="sxs-lookup"><span data-stu-id="d161d-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="d161d-207">**Соединенное Королевство**:</span><span class="sxs-lookup"><span data-stu-id="d161d-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="d161d-208">5/6 York House, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="d161d-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="d161d-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="d161d-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="d161d-210">Тел.: +44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="d161d-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="d161d-211">**Сингапур**:</span><span class="sxs-lookup"><span data-stu-id="d161d-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="d161d-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="d161d-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="d161d-213">Hello земной шар, Сингапур 069532</span><span class="sxs-lookup"><span data-stu-id="d161d-213">hello Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="d161d-214">Тел.: +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="d161d-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="d161d-215">**Северная Америка**:</span><span class="sxs-lookup"><span data-stu-id="d161d-215">**North America**:</span></span>
>   
> <span data-ttu-id="d161d-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="d161d-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="d161d-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="d161d-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="d161d-218">Тел.: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="d161d-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="d161d-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="d161d-219">ASPEX</span></span>
<span data-ttu-id="d161d-220">[ASPEX](http://www.aspex.be/en) специализируется на независимые поставщики программного обеспечения, переход toohello облака и независимых поставщиков программного обеспечения "найти toooptimize их текущей настройки облака.</span><span class="sxs-lookup"><span data-stu-id="d161d-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning toohello Cloud and ISV‘ looking toooptimize their current cloud setups.</span></span> <span data-ttu-id="d161d-221">ASPEX предлагает множество управляемых служб и решений DevOps, а также предоставляет консультационные услуги.</span><span class="sxs-lookup"><span data-stu-id="d161d-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="d161d-222">Основное расположение: Антверпен, Бельгия.</span><span class="sxs-lookup"><span data-stu-id="d161d-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="d161d-223">Целевой регион: Западная Европа.</span><span class="sxs-lookup"><span data-stu-id="d161d-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="d161d-224">Статус партнера: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff).</span><span class="sxs-lookup"><span data-stu-id="d161d-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="d161d-225">Поставщик служб Microsoft Cloud: да.</span><span class="sxs-lookup"><span data-stu-id="d161d-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="d161d-226">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="d161d-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="d161d-227">Решения для миграции Azure RemoteApp: да, [см. дополнительные сведения](https://www.aspex.be/en/azure-remote-apps).</span><span class="sxs-lookup"><span data-stu-id="d161d-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="d161d-228">Тел.: +3232202198</span><span class="sxs-lookup"><span data-stu-id="d161d-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="d161d-229">Эл. адрес: [info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="d161d-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="d161d-230">Сайт: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="d161d-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="d161d-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="d161d-231">Caase.com</span></span>
<span data-ttu-id="d161d-232">[Caase.com](http://www.caase.com/) помогает предприятиям, местными властями, -налоговые структуры и учреждений здравоохранения с их пути к оптимальный способ работы в Microsoft Cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d161d-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in hello Microsoft Cloud.</span></span> <span data-ttu-id="d161d-233">Обеспечьте производительность и безопасность работы в любом месте и на любых устройствах с низкими затратами на ИТ.</span><span class="sxs-lookup"><span data-stu-id="d161d-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="d161d-234">Caase.com — настоящий специалист в области Microsoft Office 365, Azure, Enterprise Mobility and Security и Windows.</span><span class="sxs-lookup"><span data-stu-id="d161d-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="d161d-235">Консультации, услуги миграции, программы освоения, обучение, помощь в управлении и поддержка, предоставляемые компанией Caase.com, позволяют создать оптимизированную безопасную платформу для совместной работы сотрудников, партнеров и поставщиков клиента.</span><span class="sxs-lookup"><span data-stu-id="d161d-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="d161d-236">Caase.com — организованном hello hello удаленной рабочей области Azure (мобильных рабочему месту) и hello цифровой рабочему месту (социальных интрасети).</span><span class="sxs-lookup"><span data-stu-id="d161d-236">Caase.com is hello mastermind of hello Azure Remote Workspace (mobile workplace) and hello Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="d161d-237">Оба решения — обеспечить с помощью внедрения — являются hello foundation, что обеспечивает наличие hello наиболее удобную, успешно и действующие работу пользователей hello этих решений в их toohello маршрут Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="d161d-237">Both solutions – accomplished with adoption – are hello foundation which ensures that hello users of these solutions have hello most pleasant, successful and effective experience in their route toohello Microsoft Cloud.</span></span>
<span data-ttu-id="d161d-238">Этот текст на нидерландском языке и видеоролик доступны на странице по адресу http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="d161d-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="d161d-239">Целевой регион: весь мир, находится в Нидерландах</span><span class="sxs-lookup"><span data-stu-id="d161d-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="d161d-240">Статус партнера: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3).</span><span class="sxs-lookup"><span data-stu-id="d161d-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="d161d-241">Поставщик служб Microsoft Cloud: да.</span><span class="sxs-lookup"><span data-stu-id="d161d-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="d161d-242">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="d161d-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="d161d-243">Решения для миграции Azure RemoteApp: да, [см. дополнительные сведения](http://caase.com/diensten/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="d161d-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="d161d-244">Нидерланды:</span><span class="sxs-lookup"><span data-stu-id="d161d-244">Netherlands:</span></span>
> 
> <span data-ttu-id="d161d-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="d161d-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="d161d-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="d161d-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="d161d-247">Телефон: +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="d161d-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="d161d-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="d161d-248">Nerdio</span></span>
<span data-ttu-id="d161d-249">[Nerdio для Azure](http://getnerdio.com/nfa/) — это платформа автоматизации ИТ, обеспечивающая нелепо простой подготовки, управления и оптимизации завершения ИТ-сред в облако Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="d161d-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in hello Microsoft cloud.</span></span> <span data-ttu-id="d161d-250">Подготавливайте виртуальные рабочие столы, удаленные приложения и серверы буквально за пару часов.</span><span class="sxs-lookup"><span data-stu-id="d161d-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="d161d-251">Администрирование среды hello в три щелчка мышью или меньше с портала администрирования Nerdio.</span><span class="sxs-lookup"><span data-stu-id="d161d-251">Administer hello environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="d161d-252">Использование интеллектуальных автоматического масштабирования и сохранения 40 too60% в ресурсах Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="d161d-252">Use intelligent auto-scaling and save 40 too60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="d161d-253">Основное местоположение: Чикаго, штат Иллинойс. Целевой регион: весь мир. Статус партнера: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1). Поставщик служб Microsoft Cloud: да</span><span class="sxs-lookup"><span data-stu-id="d161d-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="d161d-254">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="d161d-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="d161d-255">Решения для миграции Azure RemoteApp: да</span><span class="sxs-lookup"><span data-stu-id="d161d-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="d161d-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="d161d-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="d161d-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="d161d-257">Suite 212</span></span>
> 
> <span data-ttu-id="d161d-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="d161d-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="d161d-259">США</span><span class="sxs-lookup"><span data-stu-id="d161d-259">USA</span></span>
> 
> <span data-ttu-id="d161d-260">(844) 4NERDIO ext. 6</span><span class="sxs-lookup"><span data-stu-id="d161d-260">(844) 4NERDIO ext. 6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="d161d-261">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="d161d-261">**SaaSplaza**</span></span>
<span data-ttu-id="d161d-262">[SaaSplaza](http://www.saasplaza.com/) предлагает полный портфель Microsoft Dynamics (NAV, AX, GP, SL, CRM) для частного и общедоступного облака (Azure).</span><span class="sxs-lookup"><span data-stu-id="d161d-262">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="d161d-263">Основное местоположение: Нидерланды.</span><span class="sxs-lookup"><span data-stu-id="d161d-263">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="d161d-264">Целевой регион: весь мир.</span><span class="sxs-lookup"><span data-stu-id="d161d-264">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="d161d-265">Статус партнера: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza).</span><span class="sxs-lookup"><span data-stu-id="d161d-265">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="d161d-266">Поставщик служб Microsoft Cloud: да.</span><span class="sxs-lookup"><span data-stu-id="d161d-266">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="d161d-267">Предлагаемые решения классических приложений и приложений RemoteApp на основе сеансов: да, оба варианта.</span><span class="sxs-lookup"><span data-stu-id="d161d-267">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="d161d-268">**Европа, Ближний Восток и Африка**:</span><span class="sxs-lookup"><span data-stu-id="d161d-268">**EMEA**:</span></span>
> 
> <span data-ttu-id="d161d-269">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="d161d-269">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="d161d-270">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="d161d-270">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="d161d-271">Hello Нидерланды</span><span class="sxs-lookup"><span data-stu-id="d161d-271">hello Netherlands</span></span>
> 
> <span data-ttu-id="d161d-272">Телефон: +31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="d161d-272">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="d161d-273">**Северная и Южная Америки**:</span><span class="sxs-lookup"><span data-stu-id="d161d-273">**Americas**:</span></span>
> 
> <span data-ttu-id="d161d-274">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="d161d-274">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="d161d-275">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="d161d-275">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="d161d-276">San Diego</span><span class="sxs-lookup"><span data-stu-id="d161d-276">San Diego</span></span>
> 
> <span data-ttu-id="d161d-277">США</span><span class="sxs-lookup"><span data-stu-id="d161d-277">United States</span></span>
> 
> <span data-ttu-id="d161d-278">Телефон: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="d161d-278">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="d161d-279">**Азиатско-тихоокеанский регион**:</span><span class="sxs-lookup"><span data-stu-id="d161d-279">**APAC**:</span></span>
> 
> <span data-ttu-id="d161d-280">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="d161d-280">105 Cecil Street</span></span>
>    
> <span data-ttu-id="d161d-281">\#11-08 hello восьмиугольник</span><span class="sxs-lookup"><span data-stu-id="d161d-281">\#11-08, hello Octagon</span></span>
> 
> <span data-ttu-id="d161d-282">Singapore 069534</span><span class="sxs-lookup"><span data-stu-id="d161d-282">Singapore 069534</span></span>
> 
> <span data-ttu-id="d161d-283">Сингапур</span><span class="sxs-lookup"><span data-stu-id="d161d-283">Singapore</span></span>
>   
> <span data-ttu-id="d161d-284">Телефон в Сингапуре: +65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="d161d-284">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="d161d-285">Телефон в Австралии: +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="d161d-285">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="d161d-286">Телефон в Новой Зеландии: +64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="d161d-286">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="d161d-287">Требуется дополнительная помощь?</span><span class="sxs-lookup"><span data-stu-id="d161d-287">Need more help?</span></span>
<span data-ttu-id="d161d-288">Все еще не можете определиться с выбором или возникли дополнительные вопросы?</span><span class="sxs-lookup"><span data-stu-id="d161d-288">Still need help choosing or have further questions?</span></span> <span data-ttu-id="d161d-289">Используйте один из следующих методов tooget справки hello.</span><span class="sxs-lookup"><span data-stu-id="d161d-289">Use one of hello following methods tooget help.</span></span> 

1. <span data-ttu-id="d161d-290">Напишите нам по адресу [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d161d-290">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="d161d-291">Обратитесь в [службу поддержки Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="d161d-291">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="d161d-292">Создайте [запрос в службу поддержке Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="d161d-292">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="d161d-293">Позвоните нам по</span><span class="sxs-lookup"><span data-stu-id="d161d-293">Call us.</span></span> <span data-ttu-id="d161d-294">[номеру телефона местного отдела продаж](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="d161d-294">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

