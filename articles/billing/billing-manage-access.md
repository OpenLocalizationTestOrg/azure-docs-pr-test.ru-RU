---
title: "Управление доступом к счетам Azure с помощью ролей | Документы Майкрософт"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: c70904097f139bc2178feed83f1cf1274f3c738d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-access-to-billing-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="33ad5-102">Управление доступом к сведениям о счетах Azure с помощью управления доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="33ad5-102">Manage access to billing information for Azure using role-based access control</span></span>

<span data-ttu-id="33ad5-103">Вы можете предоставить членам группы доступ к информации о счетах Azure, назначив своей подписке одну из следующих ролей пользователя: администратор учетной записи, администратор служб, соадминистратор, владелец, участник, читатель и читатель счетов.</span><span class="sxs-lookup"><span data-stu-id="33ad5-103">You can grant access for Azure billing information to members of your team by assigning one of the following user roles to your subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="33ad5-104">Они получат доступ к счетам на [портале Azure](https://portal.azure.com/) и смогут использовать [API-интерфейсы выставления счетов](billing-usage-rate-card-overview.md) для программного получения счетов (после выражения согласия) и сведений об использовании.</span><span class="sxs-lookup"><span data-stu-id="33ad5-104">They would have access to billing information in the [Azure portal](https://portal.azure.com/), and they can use the [Billing APIs](billing-usage-rate-card-overview.md) to programmatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="33ad5-105">Дополнительные сведения о том, кто может назначать роли и какие роли за что отвечают, см. в статье [Роли в Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="33ad5-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="33ad5-106"><a name="opt-in"></a> Допуск дополнительных пользователей к счетам</span><span class="sxs-lookup"><span data-stu-id="33ad5-106"><a name="opt-in"></a> Allowing additional users to access invoices</span></span>

<span data-ttu-id="33ad5-107">Администратор учетной записи должен дать согласие на доступ других пользователей к счетам через [портал Azure](https://portal.azure.com/), а также API-интерфейс.</span><span class="sxs-lookup"><span data-stu-id="33ad5-107">The Account Administrator must opt in using the [Azure portal](https://portal.azure.com/) allow access to invoices for other users and via API.</span></span>

1. <span data-ttu-id="33ad5-108">Являясь администратором учетной записи, выберите свою подписку в [колонке подписок](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="33ad5-108">As the Account Administrator, select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="33ad5-109">Выберите **Счета** и **Access to invoices** (Доступ к счетам).</span><span class="sxs-lookup"><span data-stu-id="33ad5-109">Select **Invoices** and then **Access to invoices**.</span></span>

    ![На снимке экрана показано, как делегировать доступ к счетам](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="33ad5-111">**Включите** доступ, а затем сохраните изменения, чтобы позволить пользователям в ролях, связанными с подпиской, скачать счет.</span><span class="sxs-lookup"><span data-stu-id="33ad5-111">Turn **On** the access followed by saving the changes, to allow users in subscription scoped roles to download invoice.</span></span>

    ![На снимке экрана показано, как включать и выключать делегирование доступа к счету](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="33ad5-113">Предоставление согласия позволяет администратору служб, соадминистратору, владельцу, участнику, читателю и читателю счетов в подписке скачивать счета в формате PDF на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="33ad5-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on the subscription to download PDF invoices in the Azure portal.</span></span> <span data-ttu-id="33ad5-114">Но счета, созданные до декабря 2016 года, сейчас доступны только администратору учетной записи.</span><span class="sxs-lookup"><span data-stu-id="33ad5-114">However, invoices older than December 2016 are available only to the Account Administrator for now.</span></span>

<span data-ttu-id="33ad5-115">Администратор учетной записи также может настроить отправку счетов по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="33ad5-115">The Account Administrator can also configure to have invoices sent via email.</span></span> <span data-ttu-id="33ad5-116">Дополнительные сведения см. в статье [Получение счета по электронной почте](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="33ad5-116">To learn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-to-the-billing-reader-role"></a><span data-ttu-id="33ad5-117">Добавление пользователей в роль читателя счетов</span><span class="sxs-lookup"><span data-stu-id="33ad5-117">Adding users to the Billing Reader role</span></span>

<span data-ttu-id="33ad5-118">Роль читателя счетов имеет доступ только для чтения к сведениям о счетах подписки на портале Azure, но не может обращаться к службам, таким как виртуальные машины и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="33ad5-118">The Billing Reader role has read-only access to subscription billing information in Azure portal, and no access to services such as VMs and storage accounts.</span></span> <span data-ttu-id="33ad5-119">Назначьте эту роль пользователю, которому требуется доступ к сведениям о счетах в подписке, но не нужно управлять службами Azure.</span><span class="sxs-lookup"><span data-stu-id="33ad5-119">Assign the Billing Reader role to someone that needs access to the subscription billing information but not the ability to manage Azure services.</span></span> <span data-ttu-id="33ad5-120">Эта роль подходит для сотрудников организации, отвечающих за управление финансами и затратами для подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="33ad5-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="33ad5-121">Выберите свою подписку в [колонке подписок](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="33ad5-121">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="33ad5-122">Выберите **Управление доступом (IAM)** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="33ad5-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Снимок экрана, показывающий IAM в колонке подписки](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="33ad5-124">Выберите **Читатель счетов** на странице **Выбор роли**.</span><span class="sxs-lookup"><span data-stu-id="33ad5-124">Choose **Billing Reader** in the **Select a role** page.</span></span>

    ![Снимок экрана, показывающий роль читателя счетов во всплывающем окне](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="33ad5-126">Введите адрес электронной почты пользователя, которого хотите пригласить, и нажмите кнопку **ОК**, чтобы отправить приглашение.</span><span class="sxs-lookup"><span data-stu-id="33ad5-126">Type the email for the user you want to invite, then click **OK** to send the invitation.</span></span>

    ![Снимок экрана, показывающий ввод электронной почты для приглашения](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="33ad5-128">Следуйте инструкциям в приглашении электронной почты, чтобы войти в систему в качестве читателя счетов.</span><span class="sxs-lookup"><span data-stu-id="33ad5-128">Follow instructions in the invite email to log in as a Billing Reader.</span></span>

    ![Снимок экрана, показывающий, что читатель счетов может видеть на портале Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="33ad5-130">Средство чтения счетов находится на стадии предварительной версии и пока не поддерживает корпоративные подписки (EA) и облачные среды, не являющиеся глобальными.</span><span class="sxs-lookup"><span data-stu-id="33ad5-130">The Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-to-other-roles"></a><span data-ttu-id="33ad5-131">Добавление других ролей для пользователей</span><span class="sxs-lookup"><span data-stu-id="33ad5-131">Adding users to other roles</span></span>

<span data-ttu-id="33ad5-132">Пользователи с другими ролями, такими как владелец или участник, получают доступ не только к счетам, но и к службам Azure.</span><span class="sxs-lookup"><span data-stu-id="33ad5-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="33ad5-133">Сведения об управлении ролями см. в статье [Добавление или изменение ролей администратора Azure, управляющих подписками и службами](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="33ad5-133">To manage these roles, see [Add or change Azure administrator roles that manage the subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-the-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="33ad5-134">Кто может получить доступ к [Центру управления учетной записью Azure](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="33ad5-134">Who can access the [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="33ad5-135">Только администратор учетной записи может войти в Центр управления учетной записью.</span><span class="sxs-lookup"><span data-stu-id="33ad5-135">Only the Account Administrator can log in to the Account center.</span></span> <span data-ttu-id="33ad5-136">Администратор учетной записи является полноправным владельцем подписки.</span><span class="sxs-lookup"><span data-stu-id="33ad5-136">The Account Administrator is the legal owner of the subscription.</span></span> <span data-ttu-id="33ad5-137">По умолчанию пользователь, который зарегистрировал или приобрел подписку Azure, является администратором учетной записи, если только [право владения подпиской не было передано](billing-subscription-transfer.md) кому-то другому.</span><span class="sxs-lookup"><span data-stu-id="33ad5-137">By default, the person who signed up for or bought the Azure subscription is the Account Administrator, unless the [subscription ownership was transferred](billing-subscription-transfer.md) to somebody else.</span></span> <span data-ttu-id="33ad5-138">Администратор учетной записи может создавать и отменять подписки, менять адрес выставления счетов и политики доступа для подписки.</span><span class="sxs-lookup"><span data-stu-id="33ad5-138">The Account Administrator can create subscriptions, cancel subscriptions, change the billing address for a subscription, and manage access policies for the subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="33ad5-139">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="33ad5-139">Need help?</span></span> <span data-ttu-id="33ad5-140">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="33ad5-140">Contact support.</span></span>

<span data-ttu-id="33ad5-141">Если у вас есть дополнительные вопросы, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), которая поможет быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="33ad5-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
