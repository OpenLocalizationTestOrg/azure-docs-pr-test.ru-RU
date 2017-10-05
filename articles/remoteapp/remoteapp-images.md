---
title: "Что входит в образы шаблонов Azure RemoteApp? | Документация Майкрософт"
description: "Узнайте об образах шаблона, которые поставляются с Azure RemoteApp."
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
ms.openlocfilehash: 9cd4e1a16a7c42bd00d9e543d7b62b72e9de3fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-in-the-azure-remoteapp-template-images"></a><span data-ttu-id="e9427-104">Что входит в образы шаблонов Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="e9427-104">What is in the Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e9427-105">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="e9427-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e9427-106">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="e9427-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e9427-107">Подписка на Azure RemoteApp включает три образа шаблонов:</span><span class="sxs-lookup"><span data-stu-id="e9427-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="e9427-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e9427-108">Windows Server 2012</span></span>
* <span data-ttu-id="e9427-109">Microsoft Office 365 профессиональный плюс (необходима подписка на Office 365);</span><span class="sxs-lookup"><span data-stu-id="e9427-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="e9427-110">Microsoft Office 2013 профессиональный плюс (только пробная версия)</span><span class="sxs-lookup"><span data-stu-id="e9427-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9427-111">Подписки Azure RemoteApp предоставляют доступ к программному обеспечению в образах, за исключением выпуска "Office 365 профессиональный плюс", требующего отдельной подписки, и выпуска Office 2013, который нельзя использовать в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e9427-111">Your Azure RemoteApp subscription grants you access to the software in the images, with the exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="e9427-112">Это означает, что вы можете представлять программы или приложения на образах шаблона своим пользователям для общего доступа.</span><span class="sxs-lookup"><span data-stu-id="e9427-112">This means that you can share the programs or apps on the template images with your users.</span></span> <span data-ttu-id="e9427-113">Например, если создать коллекцию, которая использует образ Windows Server 2012 R2, можно опубликовать System Center Endpoint Protection, чтобы пользователи могли получить к нему доступ через RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e9427-113">For example, if you create a collection that uses the Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users to access through RemoteApp.</span></span>
> 
> <span data-ttu-id="e9427-114">Дополнительные сведения см. в [статье о лицензировании RemoteApp](remoteapp-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="e9427-114">Check out the [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="e9427-115">Сведения о лицензировании Office см. в статье [Использование Office с Azure RemoteApp](remoteapp-o365.md).</span><span class="sxs-lookup"><span data-stu-id="e9427-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for the Office licensing info.</span></span>
> 
> 

<span data-ttu-id="e9427-116">Ниже описывает содержимое каждого образа.</span><span class="sxs-lookup"><span data-stu-id="e9427-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--the-vanilla-image"></a><span data-ttu-id="e9427-117">Windows Server 2012 R2 (стандартный образ)</span><span class="sxs-lookup"><span data-stu-id="e9427-117">Windows Server 2012 R2  ("the vanilla image")</span></span>
<span data-ttu-id="e9427-118">Этот образ основан на операционной системе Microsoft Windows Server 2012 R2 для центров обработки данных, и в нем установлены следующие роли и функции, обеспечивающие соответствие требованиям образов шаблонов Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="e9427-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has the following roles and features installed to meet the requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="e9427-119">.NET Framework 4.5, 3.5.1, 3.5</span><span class="sxs-lookup"><span data-stu-id="e9427-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="e9427-120">Возможности рабочего стола</span><span class="sxs-lookup"><span data-stu-id="e9427-120">Desktop Experience</span></span>
* <span data-ttu-id="e9427-121">Службы рукописного ввода</span><span class="sxs-lookup"><span data-stu-id="e9427-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="e9427-122">Media Foundation</span><span class="sxs-lookup"><span data-stu-id="e9427-122">Media Foundation</span></span>
* <span data-ttu-id="e9427-123">Узел сеансов удаленных рабочих столов</span><span class="sxs-lookup"><span data-stu-id="e9427-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="e9427-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="e9427-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="e9427-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="e9427-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="e9427-126">Поддержка WoW64</span><span class="sxs-lookup"><span data-stu-id="e9427-126">WoW64 Support</span></span>

<span data-ttu-id="e9427-127">В этом образе уже установлены следующие приложения:</span><span class="sxs-lookup"><span data-stu-id="e9427-127">This image also has the following applications installed:</span></span>

* <span data-ttu-id="e9427-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="e9427-128">Adobe Flash Player</span></span>
* <span data-ttu-id="e9427-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="e9427-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="e9427-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="e9427-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="e9427-131">Проигрыватель Windows Media (Microsoft)</span><span class="sxs-lookup"><span data-stu-id="e9427-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="e9427-132">Microsoft Office 365 профессиональный плюс (необходима подписка)</span><span class="sxs-lookup"><span data-stu-id="e9427-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="e9427-133">Приложение Office 365 пользуется наибольшим спросом, поэтому мы создали для него "специальный" образ.</span><span class="sxs-lookup"><span data-stu-id="e9427-133">Office 365 is the most requested application, so we created a "custom" image for you to work with.</span></span>

<span data-ttu-id="e9427-134">Этот образ является расширенной версией стандартного образа, и в нем, помимо компонентов образа Windows Server 2012 R2, установлены следующие компоненты Microsoft Office 365 профессиональный плюс:</span><span class="sxs-lookup"><span data-stu-id="e9427-134">This image is an extension of the vanilla image and has the following components of Microsoft Office 365 ProPlus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="e9427-135">Access</span><span class="sxs-lookup"><span data-stu-id="e9427-135">Access</span></span>
* <span data-ttu-id="e9427-136">Excel</span><span class="sxs-lookup"><span data-stu-id="e9427-136">Excel</span></span>
* <span data-ttu-id="e9427-137">Lync</span><span class="sxs-lookup"><span data-stu-id="e9427-137">Lync</span></span>
* <span data-ttu-id="e9427-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="e9427-138">OneNote</span></span>
* <span data-ttu-id="e9427-139">OneDrive для бизнеса (обратите внимание, что использование агента синхронизации не поддерживается в Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="e9427-139">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="e9427-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="e9427-140">Outlook</span></span>
* <span data-ttu-id="e9427-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="e9427-141">PowerPoint</span></span>
* <span data-ttu-id="e9427-142">Word</span><span class="sxs-lookup"><span data-stu-id="e9427-142">Word</span></span>
* <span data-ttu-id="e9427-143">Средства проверки правописания Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="e9427-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="e9427-144">В образ также входят Visio Pro и Project Pro.</span><span class="sxs-lookup"><span data-stu-id="e9427-144">The image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="e9427-145">Также установлены следующие приложения.</span><span class="sxs-lookup"><span data-stu-id="e9427-145">And the following applications, as well:</span></span>

* <span data-ttu-id="e9427-146">SQL Native Client</span><span class="sxs-lookup"><span data-stu-id="e9427-146">SQL Native client</span></span>
* <span data-ttu-id="e9427-147">Драйвер ODBC</span><span class="sxs-lookup"><span data-stu-id="e9427-147">ODBC Driver</span></span>
* <span data-ttu-id="e9427-148">Клиент интеллектуального анализа данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="e9427-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="e9427-149">Клиент MasterDataServices</span><span class="sxs-lookup"><span data-stu-id="e9427-149">MasterDataServices client</span></span>
* <span data-ttu-id="e9427-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="e9427-150">Microsoft Publisher</span></span>
* <span data-ttu-id="e9427-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="e9427-151">PowerQuery</span></span>
* <span data-ttu-id="e9427-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="e9427-152">PowerMap</span></span>

<span data-ttu-id="e9427-153">Полный набор функций приложений Office 365 профессиональный плюс доступен только пользователям плана Office 365 профессиональный плюс.</span><span class="sxs-lookup"><span data-stu-id="e9427-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="e9427-154">Дополнительные сведения о планах подписки на Office 365 см. в статье [Параметры планов Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9427-154">For more details on the Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="e9427-155">У вас еще остались вопросы?</span><span class="sxs-lookup"><span data-stu-id="e9427-155">Still have questions?</span></span> <span data-ttu-id="e9427-156">Ознакомьтесь со сведениями об [Office 365 + RemoteApp](remoteapp-o365.md).</span><span class="sxs-lookup"><span data-stu-id="e9427-156">Check out the [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="e9427-157">Ознакомьтесь также с новой статьей [Как использовать подписку Office 365 с удаленным приложением Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="e9427-157">Also check out the new article, [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="e9427-158">Обратите внимание, что для каждого продукта (Office 365 профессиональный плюс, Visio Pro и Project Pro) требуются отдельные лицензии.</span><span class="sxs-lookup"><span data-stu-id="e9427-158">Note that you need to license Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="e9427-159">Microsoft Office 2013 профессиональный плюс (только пробная версия)</span><span class="sxs-lookup"><span data-stu-id="e9427-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="e9427-160">Во время пробного периода вы можете тестировать службу с помощью образа Office 2013.</span><span class="sxs-lookup"><span data-stu-id="e9427-160">During the free trial period, you can test the service with the Office 2013 image.</span></span>

<span data-ttu-id="e9427-161">Этот образ является расширенной версией стандартного образа, и в нем, помимо компонентов образа Windows Server 2012 R2, установлены следующие компоненты Microsoft Office 2013 профессиональный плюс:</span><span class="sxs-lookup"><span data-stu-id="e9427-161">This image is an extension of the vanilla image and has the following components of Microsoft Office 2013 Professional Plus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="e9427-162">Access</span><span class="sxs-lookup"><span data-stu-id="e9427-162">Access</span></span>
* <span data-ttu-id="e9427-163">Excel</span><span class="sxs-lookup"><span data-stu-id="e9427-163">Excel</span></span>
* <span data-ttu-id="e9427-164">Lync</span><span class="sxs-lookup"><span data-stu-id="e9427-164">Lync</span></span>
* <span data-ttu-id="e9427-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="e9427-165">OneNote</span></span>
* <span data-ttu-id="e9427-166">OneDrive для бизнеса (обратите внимание, что использование агента синхронизации не поддерживается в Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="e9427-166">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="e9427-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="e9427-167">Outlook</span></span>
* <span data-ttu-id="e9427-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="e9427-168">PowerPoint</span></span>
* <span data-ttu-id="e9427-169">Project</span><span class="sxs-lookup"><span data-stu-id="e9427-169">Project</span></span>
* <span data-ttu-id="e9427-170">Visio</span><span class="sxs-lookup"><span data-stu-id="e9427-170">Visio</span></span>
* <span data-ttu-id="e9427-171">Word</span><span class="sxs-lookup"><span data-stu-id="e9427-171">Word</span></span>
* <span data-ttu-id="e9427-172">Средства проверки правописания Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="e9427-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9427-173">**Юридическая информация**. Этот образ не включает в себя лицензию Microsoft Office и *не может использоваться в производственных целях*.</span><span class="sxs-lookup"><span data-stu-id="e9427-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="e9427-174">Образ Office 2013 профессиональный плюс предназначен исключительно для пробного использования.</span><span class="sxs-lookup"><span data-stu-id="e9427-174">The Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="e9427-175">Если вам нужно использовать приложения Office в Azure RemoteApp в рабочей среде, используйте образ Office 365 профессиональный плюс.</span><span class="sxs-lookup"><span data-stu-id="e9427-175">If you want to use Office apps in Azure RemoteApp for production, you need to use the Office 365 ProPlus image.</span></span> <span data-ttu-id="e9427-176">Дополнительные сведения о лицензировании Office см. в статье [Использование Office с Azure RemoteApp](remoteapp-o365.md).</span><span class="sxs-lookup"><span data-stu-id="e9427-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

