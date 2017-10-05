---
title: "Добавление пользователя в коллекцию Azure RemoteApp | Документация Майкрософт"
description: "Узнайте о том, как добавить пользователя в коллекцию Azure RemoteApp"
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
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a><span data-ttu-id="6eea6-103">Добавление пользователя в коллекцию Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="6eea6-103">How to add a user to your Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6eea6-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="6eea6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6eea6-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="6eea6-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6eea6-106">Прежде чем пользователи смогут видеть и использовать ваши приложения в Azure RemoteApp, необходимо предоставить им доступ к вашей коллекции.</span><span class="sxs-lookup"><span data-stu-id="6eea6-106">Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection.</span></span> <span data-ttu-id="6eea6-107">Это просто: на вкладке **Доступ пользователя** введите данные учетной записи пользователя, а затем установите флажок.</span><span class="sxs-lookup"><span data-stu-id="6eea6-107">This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.</span></span>

<span data-ttu-id="6eea6-108">Какие данные учетной записи требуются?</span><span class="sxs-lookup"><span data-stu-id="6eea6-108">What account information do you need?</span></span> <span data-ttu-id="6eea6-109">Это зависит от типа созданной коллекции (облачной или гибридной) и того, используется ли Office 365 профессиональный плюс в этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="6eea6-109">That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="6eea6-110">Поддерживаемые удостоверения пользователей</span><span class="sxs-lookup"><span data-stu-id="6eea6-110">Supported user identities</span></span>
<span data-ttu-id="6eea6-111">Разные типы коллекций (облачные или гибридные) поддерживают использование разных удостоверений пользователей для доступа к приложениям.</span><span class="sxs-lookup"><span data-stu-id="6eea6-111">The different collection types (cloud vs. hybrid) support using different user identities for access to applications.</span></span>  

<span data-ttu-id="6eea6-112">Для гибридной коллекции RemoteApp необходимо настроить локальную инфраструктуру доменов Active Directory и клиент Azure Active Directory с интеграцией каталогов (при желании можно настроить и единый вход).</span><span class="sxs-lookup"><span data-stu-id="6eea6-112">For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="6eea6-113">Кроме того, в локальном каталоге необходимо создать несколько объектов Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6eea6-113">Additionally, you need to create some Active Directory objects in the on-premises directory.</span></span>  

<span data-ttu-id="6eea6-114">Что касается облачной коллекции RemoteApp, любому пользователю с поддержкой удостоверений Azure Active Directory можно предоставить доступ к RemoteApp, чтобы включить учетные записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6eea6-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.</span></span>  <span data-ttu-id="6eea6-115">См. таблицу ниже.</span><span class="sxs-lookup"><span data-stu-id="6eea6-115">See the table below.</span></span>

<span data-ttu-id="6eea6-116">Пользователи Office 365 являются пользователями Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6eea6-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="6eea6-117">При наличии у них гибридных, синхронизированных с каталогами учетных записей Azure Active Directory этим пользователям можно предоставить доступ путем гибридного развертывания RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6eea6-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="6eea6-118">С помощью этой таблицы можно быстро проверить, какие удостоверения поддерживаются в вашей коллекции, а также в чем состоят требования к Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6eea6-118">You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.</span></span>

| <span data-ttu-id="6eea6-119">Учетные записи пользователей</span><span class="sxs-lookup"><span data-stu-id="6eea6-119">User accounts</span></span> | <span data-ttu-id="6eea6-120">Облако</span><span class="sxs-lookup"><span data-stu-id="6eea6-120">Cloud</span></span> | <span data-ttu-id="6eea6-121">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="6eea6-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6eea6-122">Учетная запись Майкрософт</span><span class="sxs-lookup"><span data-stu-id="6eea6-122">Microsoft Account</span></span> |<span data-ttu-id="6eea6-123">Да</span><span class="sxs-lookup"><span data-stu-id="6eea6-123">Yes</span></span> |<span data-ttu-id="6eea6-124">Нет</span><span class="sxs-lookup"><span data-stu-id="6eea6-124">No</span></span> |
| <span data-ttu-id="6eea6-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="6eea6-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="6eea6-126">Только облако Azure AD</span><span class="sxs-lookup"><span data-stu-id="6eea6-126">Azure AD cloud only</span></span> |<span data-ttu-id="6eea6-127">Да</span><span class="sxs-lookup"><span data-stu-id="6eea6-127">Yes</span></span> |<span data-ttu-id="6eea6-128">Нет</span><span class="sxs-lookup"><span data-stu-id="6eea6-128">No</span></span> |
| <span data-ttu-id="6eea6-129">ADsync с синхронизацией паролей</span><span class="sxs-lookup"><span data-stu-id="6eea6-129">ADsync with password sync</span></span> |<span data-ttu-id="6eea6-130">Да</span><span class="sxs-lookup"><span data-stu-id="6eea6-130">Yes</span></span> |<span data-ttu-id="6eea6-131">Да</span><span class="sxs-lookup"><span data-stu-id="6eea6-131">Yes</span></span> |
| <span data-ttu-id="6eea6-132">ADsync без синхронизации паролей</span><span class="sxs-lookup"><span data-stu-id="6eea6-132">ADsync without password sync</span></span> |<span data-ttu-id="6eea6-133">Да</span><span class="sxs-lookup"><span data-stu-id="6eea6-133">Yes</span></span> |<span data-ttu-id="6eea6-134">Нет</span><span class="sxs-lookup"><span data-stu-id="6eea6-134">No</span></span> |
| <span data-ttu-id="6eea6-135">ADsync с AD FS</span><span class="sxs-lookup"><span data-stu-id="6eea6-135">ADsync with AD FS</span></span> |<span data-ttu-id="6eea6-136">Да</span><span class="sxs-lookup"><span data-stu-id="6eea6-136">Yes</span></span> |<span data-ttu-id="6eea6-137">Да</span><span class="sxs-lookup"><span data-stu-id="6eea6-137">Yes</span></span> |
| <span data-ttu-id="6eea6-138">[Сторонние поставщики удостоверений, поддерживаемые Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (например, Ping)</span><span class="sxs-lookup"><span data-stu-id="6eea6-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="6eea6-139">Да</span><span class="sxs-lookup"><span data-stu-id="6eea6-139">Yes</span></span> |<span data-ttu-id="6eea6-140">Да</span><span class="sxs-lookup"><span data-stu-id="6eea6-140">Yes</span></span> |
| <span data-ttu-id="6eea6-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="6eea6-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="6eea6-142">Да</span><span class="sxs-lookup"><span data-stu-id="6eea6-142">Yes</span></span> |<span data-ttu-id="6eea6-143">Да</span><span class="sxs-lookup"><span data-stu-id="6eea6-143">Yes</span></span> |

<span data-ttu-id="6eea6-144">[Узнайте больше](remoteapp-ad.md) о настройке Active Directory для RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6eea6-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="6eea6-145">Пользователи Azure Active Directory должны относиться к клиенту, связанному с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="6eea6-145">The Azure Active Directory users must be from the tenant that's associated with your subscription.</span></span> <span data-ttu-id="6eea6-146">(Вы можете просмотреть и изменить связанную подписку на вкладке **Параметры** на портале.</span><span class="sxs-lookup"><span data-stu-id="6eea6-146">(You can view and modify your subscription on the **Settings** tab in the portal.</span></span> <span data-ttu-id="6eea6-147">Дополнительные сведения см. в статье [Смена клиента Azure Active Directory в Azure RemoteApp](remoteapp-changetenant.md).)</span><span class="sxs-lookup"><span data-stu-id="6eea6-147">See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="6eea6-148">Данные учетных записей пользователей для Office 365 профессиональный плюс</span><span class="sxs-lookup"><span data-stu-id="6eea6-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="6eea6-149">При работе с образом шаблона Office 365 профессиональный плюс *или* пользовательским образом шаблона, использующим Office 365, разрешается добавлять только тех пользователей Azure Active Directory, у которых есть подписки Office 365 для домена организации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6eea6-149">If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription.</span></span> <span data-ttu-id="6eea6-150">Дополнительные сведения см. в статье [Использование Office с Azure RemoteApp](remoteapp-o365.md).</span><span class="sxs-lookup"><span data-stu-id="6eea6-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

