---
title: "aaaWhat находится в образах шаблона hello Azure RemoteApp? | Документация Майкрософт"
description: "Дополнительные сведения об образах шаблона hello, входящий в состав Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a><span data-ttu-id="23772-104">Что такое hello образы шаблонов Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="23772-104">What is in hello Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="23772-105">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="23772-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="23772-106">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="23772-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="23772-107">Подписка на Azure RemoteApp включает три образа шаблонов:</span><span class="sxs-lookup"><span data-stu-id="23772-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="23772-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="23772-108">Windows Server 2012</span></span>
* <span data-ttu-id="23772-109">Microsoft Office 365 профессиональный плюс (необходима подписка на Office 365);</span><span class="sxs-lookup"><span data-stu-id="23772-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="23772-110">Microsoft Office 2013 профессиональный плюс (только пробная версия)</span><span class="sxs-lookup"><span data-stu-id="23772-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23772-111">Подписки Azure RemoteApp предоставляет вам доступ к программному обеспечению toohello в образах hello, за исключением hello Office 365 профессиональный плюс, требующий отдельной подписки, и Office 2013, который не может использоваться в производственной среде.</span><span class="sxs-lookup"><span data-stu-id="23772-111">Your Azure RemoteApp subscription grants you access toohello software in hello images, with hello exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="23772-112">Это означает, что могут обмениваться hello программ или приложений на образы шаблонов hello с пользователями.</span><span class="sxs-lookup"><span data-stu-id="23772-112">This means that you can share hello programs or apps on hello template images with your users.</span></span> <span data-ttu-id="23772-113">Например при создании коллекции, использующего образ Windows Server 2012 R2 hello, System Center Endpoint Protection можно опубликовать для пользователей tooaccess через RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="23772-113">For example, if you create a collection that uses hello Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users tooaccess through RemoteApp.</span></span>
> 
> <span data-ttu-id="23772-114">Извлечение hello [сведения о лицензировании удаленных приложений RemoteApp](remoteapp-licensing.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="23772-114">Check out hello [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="23772-115">И [Office с помощью Azure RemoteApp.](remoteapp-o365.md) для hello сведения о лицензировании Office.</span><span class="sxs-lookup"><span data-stu-id="23772-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for hello Office licensing info.</span></span>
> 
> 

<span data-ttu-id="23772-116">Ниже описывает содержимое каждого образа.</span><span class="sxs-lookup"><span data-stu-id="23772-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--hello-vanilla-image"></a><span data-ttu-id="23772-117">Windows Server 2012 R2 («hello соответствующего ванили образ»)</span><span class="sxs-lookup"><span data-stu-id="23772-117">Windows Server 2012 R2  ("hello vanilla image")</span></span>
<span data-ttu-id="23772-118">Этот образ основан на операционной системе Microsoft Windows Server 2012 R2 Datacenter и имеет hello установлены следующие роли и компоненты toomeet hello требованиям к образам шаблона Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="23772-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has hello following roles and features installed toomeet hello requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="23772-119">.NET Framework 4.5, 3.5.1, 3.5</span><span class="sxs-lookup"><span data-stu-id="23772-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="23772-120">Возможности рабочего стола</span><span class="sxs-lookup"><span data-stu-id="23772-120">Desktop Experience</span></span>
* <span data-ttu-id="23772-121">Службы рукописного ввода</span><span class="sxs-lookup"><span data-stu-id="23772-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="23772-122">Media Foundation</span><span class="sxs-lookup"><span data-stu-id="23772-122">Media Foundation</span></span>
* <span data-ttu-id="23772-123">Узел сеансов удаленных рабочих столов</span><span class="sxs-lookup"><span data-stu-id="23772-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="23772-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="23772-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="23772-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="23772-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="23772-126">Поддержка WoW64</span><span class="sxs-lookup"><span data-stu-id="23772-126">WoW64 Support</span></span>

<span data-ttu-id="23772-127">Этот образ также имеет следующие приложения, установленные hello:</span><span class="sxs-lookup"><span data-stu-id="23772-127">This image also has hello following applications installed:</span></span>

* <span data-ttu-id="23772-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="23772-128">Adobe Flash Player</span></span>
* <span data-ttu-id="23772-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="23772-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="23772-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="23772-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="23772-131">Проигрыватель Windows Media (Microsoft)</span><span class="sxs-lookup"><span data-stu-id="23772-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="23772-132">Microsoft Office 365 профессиональный плюс (необходима подписка)</span><span class="sxs-lookup"><span data-stu-id="23772-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="23772-133">Office 365 hello наиболее запрошенное приложение, поэтому мы создали «custom» образ для вас toowork с.</span><span class="sxs-lookup"><span data-stu-id="23772-133">Office 365 is hello most requested application, so we created a "custom" image for you toowork with.</span></span>

<span data-ttu-id="23772-134">Этот образ является расширением соответствующего ванили изображения hello и hello следующие компоненты Microsoft Office 365 профессиональный плюс; установлен в дополнение к этому toohello компонентами, описанными в образ Windows Server 2012 R2 hello:</span><span class="sxs-lookup"><span data-stu-id="23772-134">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 365 ProPlus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="23772-135">Access</span><span class="sxs-lookup"><span data-stu-id="23772-135">Access</span></span>
* <span data-ttu-id="23772-136">Excel</span><span class="sxs-lookup"><span data-stu-id="23772-136">Excel</span></span>
* <span data-ttu-id="23772-137">Lync</span><span class="sxs-lookup"><span data-stu-id="23772-137">Lync</span></span>
* <span data-ttu-id="23772-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="23772-138">OneNote</span></span>
* <span data-ttu-id="23772-139">OneDrive для бизнеса (Обратите внимание, что агент синхронизации hello не поддерживается для использования с Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="23772-139">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="23772-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="23772-140">Outlook</span></span>
* <span data-ttu-id="23772-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="23772-141">PowerPoint</span></span>
* <span data-ttu-id="23772-142">Word</span><span class="sxs-lookup"><span data-stu-id="23772-142">Word</span></span>
* <span data-ttu-id="23772-143">Средства проверки правописания Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="23772-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="23772-144">изображение Hello также Visio Pro и Pro проекта.</span><span class="sxs-lookup"><span data-stu-id="23772-144">hello image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="23772-145">И hello приложений, а также следующие:</span><span class="sxs-lookup"><span data-stu-id="23772-145">And hello following applications, as well:</span></span>

* <span data-ttu-id="23772-146">SQL Native Client</span><span class="sxs-lookup"><span data-stu-id="23772-146">SQL Native client</span></span>
* <span data-ttu-id="23772-147">Драйвер ODBC</span><span class="sxs-lookup"><span data-stu-id="23772-147">ODBC Driver</span></span>
* <span data-ttu-id="23772-148">Клиент интеллектуального анализа данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="23772-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="23772-149">Клиент MasterDataServices</span><span class="sxs-lookup"><span data-stu-id="23772-149">MasterDataServices client</span></span>
* <span data-ttu-id="23772-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="23772-150">Microsoft Publisher</span></span>
* <span data-ttu-id="23772-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="23772-151">PowerQuery</span></span>
* <span data-ttu-id="23772-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="23772-152">PowerMap</span></span>

<span data-ttu-id="23772-153">Полный набор функций приложений Office 365 профессиональный плюс доступен только пользователям плана Office 365 профессиональный плюс.</span><span class="sxs-lookup"><span data-stu-id="23772-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="23772-154">Дополнительные сведения о подписке Office 365 hello планов в разделе [планы службы Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span><span class="sxs-lookup"><span data-stu-id="23772-154">For more details on hello Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="23772-155">У вас еще остались вопросы?</span><span class="sxs-lookup"><span data-stu-id="23772-155">Still have questions?</span></span> <span data-ttu-id="23772-156">Извлечение hello [Office 365 + RemoteApp](remoteapp-o365.md) сведения.</span><span class="sxs-lookup"><span data-stu-id="23772-156">Check out hello [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="23772-157">Прочитайте статью hello [как toouse подписки Office 365 в Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="23772-157">Also check out hello new article, [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="23772-158">Обратите внимание, что Office 365 профессиональный плюс toolicense Visio Pro и проект Pro отдельно - все их собственной лицензии.</span><span class="sxs-lookup"><span data-stu-id="23772-158">Note that you need toolicense Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="23772-159">Microsoft Office 2013 профессиональный плюс (только пробная версия)</span><span class="sxs-lookup"><span data-stu-id="23772-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="23772-160">Во время hello бесплатного пробного периода можно протестировать службу hello с изображением hello Office 2013.</span><span class="sxs-lookup"><span data-stu-id="23772-160">During hello free trial period, you can test hello service with hello Office 2013 image.</span></span>

<span data-ttu-id="23772-161">Этот образ является расширением соответствующего ванили изображения hello и hello следующие компоненты Microsoft Office 2013 профессиональный плюс установлен в дополнение к этому toohello компонентами, описанными в образ Windows Server 2012 R2 hello:</span><span class="sxs-lookup"><span data-stu-id="23772-161">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 2013 Professional Plus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="23772-162">Access</span><span class="sxs-lookup"><span data-stu-id="23772-162">Access</span></span>
* <span data-ttu-id="23772-163">Excel</span><span class="sxs-lookup"><span data-stu-id="23772-163">Excel</span></span>
* <span data-ttu-id="23772-164">Lync</span><span class="sxs-lookup"><span data-stu-id="23772-164">Lync</span></span>
* <span data-ttu-id="23772-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="23772-165">OneNote</span></span>
* <span data-ttu-id="23772-166">OneDrive для бизнеса (Обратите внимание, что агент синхронизации hello не поддерживается для использования с Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="23772-166">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="23772-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="23772-167">Outlook</span></span>
* <span data-ttu-id="23772-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="23772-168">PowerPoint</span></span>
* <span data-ttu-id="23772-169">Project</span><span class="sxs-lookup"><span data-stu-id="23772-169">Project</span></span>
* <span data-ttu-id="23772-170">Visio</span><span class="sxs-lookup"><span data-stu-id="23772-170">Visio</span></span>
* <span data-ttu-id="23772-171">Word</span><span class="sxs-lookup"><span data-stu-id="23772-171">Word</span></span>
* <span data-ttu-id="23772-172">Средства проверки правописания Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="23772-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23772-173">**Юридическая информация**. Этот образ не включает в себя лицензию Microsoft Office и *не может использоваться в производственных целях*.</span><span class="sxs-lookup"><span data-stu-id="23772-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="23772-174">изображение Office 2013 профессиональный плюс Hello предназначено только для пробного использования.</span><span class="sxs-lookup"><span data-stu-id="23772-174">hello Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="23772-175">Следует toouse приложений Office в Azure RemoteApp для рабочей среды необходимо toouse hello Office 365 профессиональный плюс изображения.</span><span class="sxs-lookup"><span data-stu-id="23772-175">If you want toouse Office apps in Azure RemoteApp for production, you need toouse hello Office 365 ProPlus image.</span></span> <span data-ttu-id="23772-176">Дополнительные сведения о лицензировании Office см. в статье [Использование Office с Azure RemoteApp](remoteapp-o365.md).</span><span class="sxs-lookup"><span data-stu-id="23772-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

