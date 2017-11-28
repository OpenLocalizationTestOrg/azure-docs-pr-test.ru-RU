---
title: "aaaAdd пользователя tooyour коллекции Azure RemoteApp | Документы Microsoft"
description: "Узнайте, каким образом пользователи tooadd tooyour коллекции Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a><span data-ttu-id="2b0b1-103">Как tooadd tooyour пользователя коллекции Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="2b0b1-103">How tooadd a user tooyour Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2b0b1-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="2b0b1-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="2b0b1-106">Прежде чем пользователи можно просмотреть и использовать приложения в Azure RemoteApp, у вас есть toogrant их доступа к коллекции tooyour.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-106">Before your users can see and use your apps in Azure RemoteApp, you have toogrant them access tooyour collection.</span></span> <span data-ttu-id="2b0b1-107">Это простая часть hello: на hello **доступ пользователя** введите hello сведения об учетной записи для пользователя hello и нажмите кнопку флажок hello.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-107">This is hello easy part: On hello **User Access** tab, enter hello account information for hello user, and then click hello check mark.</span></span>

<span data-ttu-id="2b0b1-108">Какие данные учетной записи требуются?</span><span class="sxs-lookup"><span data-stu-id="2b0b1-108">What account information do you need?</span></span> <span data-ttu-id="2b0b1-109">Зависит от типа hello коллекции был создан (облачной или гибридной) и при использовании Office 365 профессиональный плюс в этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-109">That depends on hello type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="2b0b1-110">Поддерживаемые удостоверения пользователей</span><span class="sxs-lookup"><span data-stu-id="2b0b1-110">Supported user identities</span></span>
<span data-ttu-id="2b0b1-111">типы другую коллекцию Hello (облако и гибридное) поддерживают, используя различные удостоверения пользователя для доступа к tooapplications.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-111">hello different collection types (cloud vs. hybrid) support using different user identities for access tooapplications.</span></span>  

<span data-ttu-id="2b0b1-112">Для гибридной коллекции RemoteApp требуется tooset инфраструктуры домена Active Directory локально, а клиент Azure Active Directory с помощью интеграции каталога (и при необходимости единый вход).</span><span class="sxs-lookup"><span data-stu-id="2b0b1-112">For a hybrid collection of RemoteApp, you need tooset up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="2b0b1-113">Кроме того вы должны toocreate некоторые объекты Active Directory из локального каталога hello.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-113">Additionally, you need toocreate some Active Directory objects in hello on-premises directory.</span></span>  

<span data-ttu-id="2b0b1-114">Для облака коллекции RemoteApp любой пользователь, имеющий поддерживает удостоверения Azure Active Directory могут быть предоставлены tooinclude tooRemoteApp доступ пользователя учетные записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access tooRemoteApp tooinclude Microsoft Accounts.</span></span>  <span data-ttu-id="2b0b1-115">См. в следующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-115">See hello table below.</span></span>

<span data-ttu-id="2b0b1-116">Пользователи Office 365 являются пользователями Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="2b0b1-117">При наличии у них гибридных, синхронизированных с каталогами учетных записей Azure Active Directory этим пользователям можно предоставить доступ путем гибридного развертывания RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="2b0b1-118">Эта таблица используется для быстрого перехода, для которого в коллекции и каковы требования к Active Directory hello поддерживается удостоверения.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-118">You can use this table as a quick reference for which identity is supported in your collection and what hello Active Directory requirements are.</span></span>

| <span data-ttu-id="2b0b1-119">Учетные записи пользователей</span><span class="sxs-lookup"><span data-stu-id="2b0b1-119">User accounts</span></span> | <span data-ttu-id="2b0b1-120">Облако</span><span class="sxs-lookup"><span data-stu-id="2b0b1-120">Cloud</span></span> | <span data-ttu-id="2b0b1-121">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="2b0b1-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b0b1-122">Учетная запись Майкрософт</span><span class="sxs-lookup"><span data-stu-id="2b0b1-122">Microsoft Account</span></span> |<span data-ttu-id="2b0b1-123">Да</span><span class="sxs-lookup"><span data-stu-id="2b0b1-123">Yes</span></span> |<span data-ttu-id="2b0b1-124">Нет</span><span class="sxs-lookup"><span data-stu-id="2b0b1-124">No</span></span> |
| <span data-ttu-id="2b0b1-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="2b0b1-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="2b0b1-126">Только облако Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b0b1-126">Azure AD cloud only</span></span> |<span data-ttu-id="2b0b1-127">Да</span><span class="sxs-lookup"><span data-stu-id="2b0b1-127">Yes</span></span> |<span data-ttu-id="2b0b1-128">Нет</span><span class="sxs-lookup"><span data-stu-id="2b0b1-128">No</span></span> |
| <span data-ttu-id="2b0b1-129">ADsync с синхронизацией паролей</span><span class="sxs-lookup"><span data-stu-id="2b0b1-129">ADsync with password sync</span></span> |<span data-ttu-id="2b0b1-130">Да</span><span class="sxs-lookup"><span data-stu-id="2b0b1-130">Yes</span></span> |<span data-ttu-id="2b0b1-131">Да</span><span class="sxs-lookup"><span data-stu-id="2b0b1-131">Yes</span></span> |
| <span data-ttu-id="2b0b1-132">ADsync без синхронизации паролей</span><span class="sxs-lookup"><span data-stu-id="2b0b1-132">ADsync without password sync</span></span> |<span data-ttu-id="2b0b1-133">Да</span><span class="sxs-lookup"><span data-stu-id="2b0b1-133">Yes</span></span> |<span data-ttu-id="2b0b1-134">Нет</span><span class="sxs-lookup"><span data-stu-id="2b0b1-134">No</span></span> |
| <span data-ttu-id="2b0b1-135">ADsync с AD FS</span><span class="sxs-lookup"><span data-stu-id="2b0b1-135">ADsync with AD FS</span></span> |<span data-ttu-id="2b0b1-136">Да</span><span class="sxs-lookup"><span data-stu-id="2b0b1-136">Yes</span></span> |<span data-ttu-id="2b0b1-137">Да</span><span class="sxs-lookup"><span data-stu-id="2b0b1-137">Yes</span></span> |
| <span data-ttu-id="2b0b1-138">[Сторонние поставщики удостоверений, поддерживаемые Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (например, Ping)</span><span class="sxs-lookup"><span data-stu-id="2b0b1-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="2b0b1-139">Да</span><span class="sxs-lookup"><span data-stu-id="2b0b1-139">Yes</span></span> |<span data-ttu-id="2b0b1-140">Да</span><span class="sxs-lookup"><span data-stu-id="2b0b1-140">Yes</span></span> |
| <span data-ttu-id="2b0b1-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="2b0b1-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="2b0b1-142">Да</span><span class="sxs-lookup"><span data-stu-id="2b0b1-142">Yes</span></span> |<span data-ttu-id="2b0b1-143">Да</span><span class="sxs-lookup"><span data-stu-id="2b0b1-143">Yes</span></span> |

<span data-ttu-id="2b0b1-144">[Узнайте больше](remoteapp-ad.md) о настройке Active Directory для RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="2b0b1-145">Hello Azure Active Directory-пользователи должны принадлежать hello клиенте, связанном с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-145">hello Azure Active Directory users must be from hello tenant that's associated with your subscription.</span></span> <span data-ttu-id="2b0b1-146">(Можно просматривать и изменять подписки на hello **параметры** вкладка на портале hello.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-146">(You can view and modify your subscription on hello **Settings** tab in hello portal.</span></span> <span data-ttu-id="2b0b1-147">В разделе [клиента Azure Active Directory hello изменений, используемой RemoteApp](remoteapp-changetenant.md) подробнее.)</span><span class="sxs-lookup"><span data-stu-id="2b0b1-147">See [Change hello Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="2b0b1-148">Данные учетных записей пользователей для Office 365 профессиональный плюс</span><span class="sxs-lookup"><span data-stu-id="2b0b1-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="2b0b1-149">Если вы используете Office 365 профессиональный плюс образ шаблона hello в коллекции *или* при создании настраиваемого образа, который использует Office 365, можно только tooadd пользователей Azure Active Directory, которые имеются подписки Office 365 для hello домен по умолчанию подписки.</span><span class="sxs-lookup"><span data-stu-id="2b0b1-149">If you are using hello Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed tooadd Azure Active Directory users that have Office 365 subscriptions for hello default domain of your subscription.</span></span> <span data-ttu-id="2b0b1-150">Дополнительные сведения см. в статье [Использование Office с Azure RemoteApp](remoteapp-o365.md).</span><span class="sxs-lookup"><span data-stu-id="2b0b1-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

