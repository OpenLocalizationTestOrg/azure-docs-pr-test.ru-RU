---
title: "tooAzure доступа aaaManage выставления счетов с помощью ролей | Документы Microsoft"
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
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="38cab-102">Управление сведениями о toobilling доступ для Azure с помощью управления доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="38cab-102">Manage access toobilling information for Azure using role-based access control</span></span>

<span data-ttu-id="38cab-103">Можно предоставить доступ для Azure выставления счетов toomembers сведений рабочей группы путем назначения одной hello следующие подписки tooyour роли пользователя: учетная запись администратора, администратор службы, соадминистратора, владельца, участника, чтения и чтения выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="38cab-103">You can grant access for Azure billing information toomembers of your team by assigning one of hello following user roles tooyour subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="38cab-104">Они бы toobilling доступа к данным в hello [портал Azure](https://portal.azure.com/), и они могут использовать hello [выставления счетов API-интерфейсы](billing-usage-rate-card-overview.md) tooprogrammatically получения счета (один раз согласился входящий) и сведения об использовании.</span><span class="sxs-lookup"><span data-stu-id="38cab-104">They would have access toobilling information in hello [Azure portal](https://portal.azure.com/), and they can use hello [Billing APIs](billing-usage-rate-card-overview.md) tooprogrammatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="38cab-105">Дополнительные сведения о том, кто может назначать роли и какие роли за что отвечают, см. в статье [Роли в Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="38cab-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="38cab-106"><a name="opt-in"></a>Разрешение дополнительных пользователей tooaccess счетов</span><span class="sxs-lookup"><span data-stu-id="38cab-106"><a name="opt-in"></a> Allowing additional users tooaccess invoices</span></span>

<span data-ttu-id="38cab-107">Hello администратора учетной записи необходимо явно включить с помощью hello [портал Azure](https://portal.azure.com/) разрешить tooinvoices доступ для других пользователей, а также через API.</span><span class="sxs-lookup"><span data-stu-id="38cab-107">hello Account Administrator must opt in using hello [Azure portal](https://portal.azure.com/) allow access tooinvoices for other users and via API.</span></span>

1. <span data-ttu-id="38cab-108">Здравствуйте, администратор учетной записи, выберите подписку из hello [колонке подписки](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="38cab-108">As hello Account Administrator, select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="38cab-109">Выберите **счета** и затем **доступ к tooinvoices**.</span><span class="sxs-lookup"><span data-stu-id="38cab-109">Select **Invoices** and then **Access tooinvoices**.</span></span>

    ![Снимок экрана показано, как toodelegate доступ к tooinvoices](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="38cab-111">Включить **на** hello доступа следуют сохранения изменений hello, tooallow пользователей в счет toodownload выделенных ролях подписки.</span><span class="sxs-lookup"><span data-stu-id="38cab-111">Turn **On** hello access followed by saving hello changes, tooallow users in subscription scoped roles toodownload invoice.</span></span>

    ![Снимок экрана показывает tooinvoice доступ включен выключен toodelegate](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="38cab-113">Включения защиты позволяет администратору службы, соадминистратора, владельца, участника, чтения и чтения выставления счетов hello подписки toodownload PDF счета в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="38cab-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on hello subscription toodownload PDF invoices in hello Azure portal.</span></span> <span data-ttu-id="38cab-114">Однако накладные старше декабря 2016 являются toohello доступны только администратор учетной записи сейчас.</span><span class="sxs-lookup"><span data-stu-id="38cab-114">However, invoices older than December 2016 are available only toohello Account Administrator for now.</span></span>

<span data-ttu-id="38cab-115">Hello администратора учетной записи можно также настроить toohave счета, отправляемых по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="38cab-115">hello Account Administrator can also configure toohave invoices sent via email.</span></span> <span data-ttu-id="38cab-116">toolearn более, в разделе [получить ваш счет в сообщении электронной почты](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="38cab-116">toolearn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-toohello-billing-reader-role"></a><span data-ttu-id="38cab-117">Добавление роли чтения выставления счетов toohello пользователей</span><span class="sxs-lookup"><span data-stu-id="38cab-117">Adding users toohello Billing Reader role</span></span>

<span data-ttu-id="38cab-118">Hello выставления счетов чтения роль имеет доступ только для чтения toosubscription данные для выставления счетов на портале Azure, а не tooservices доступа, таких как виртуальные машины и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="38cab-118">hello Billing Reader role has read-only access toosubscription billing information in Azure portal, and no access tooservices such as VMs and storage accounts.</span></span> <span data-ttu-id="38cab-119">Назначьте toosomeone роль чтения выставления счетов hello, требуется доступ к toohello данные для подписки выставления счетов, но не hello toomanage возможности Azure службы.</span><span class="sxs-lookup"><span data-stu-id="38cab-119">Assign hello Billing Reader role toosomeone that needs access toohello subscription billing information but not hello ability toomanage Azure services.</span></span> <span data-ttu-id="38cab-120">Эта роль подходит для сотрудников организации, отвечающих за управление финансами и затратами для подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="38cab-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="38cab-121">Выберите подписку из hello [колонке подписки](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="38cab-121">Select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="38cab-122">Выберите **Управление доступом (IAM)** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="38cab-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Снимок экрана показывает IAM в колонке подписки hello](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="38cab-124">Выберите **выставления счетов чтения** в hello **выберите роль** страницы.</span><span class="sxs-lookup"><span data-stu-id="38cab-124">Choose **Billing Reader** in hello **Select a role** page.</span></span>

    ![Снимок экрана показывает чтения выставление счетов в представлении всплывающее окно приветствия](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="38cab-126">Введите hello электронной почты для пользователя hello tooinvite и нажмите щелкните **ОК** toosend hello приглашения.</span><span class="sxs-lookup"><span data-stu-id="38cab-126">Type hello email for hello user you want tooinvite, then click **OK** toosend hello invitation.</span></span>

    ![Снимок экрана, показывающий tooinvite tooenter электронной почты пользователя](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="38cab-128">Следуйте инструкциям в toolog hello приглашение по электронной почте, в качестве читателя выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="38cab-128">Follow instructions in hello invite email toolog in as a Billing Reader.</span></span>

    ![Снимок экрана, показывающий, что hello чтения выставления счетов можно увидеть на портале Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="38cab-130">Функция выставления счетов чтения Hello находится в предварительной версии и пока не поддерживает подписки enterprise (EA) или неглобальной облака.</span><span class="sxs-lookup"><span data-stu-id="38cab-130">hello Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-tooother-roles"></a><span data-ttu-id="38cab-131">Добавление ролей пользователей tooother</span><span class="sxs-lookup"><span data-stu-id="38cab-131">Adding users tooother roles</span></span>

<span data-ttu-id="38cab-132">Пользователи с другими ролями, такими как владелец или участник, получают доступ не только к счетам, но и к службам Azure.</span><span class="sxs-lookup"><span data-stu-id="38cab-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="38cab-133">см. Эти роли toomanage [добавить или изменить роли Администратор Azure, управлять hello подписки или службы](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="38cab-133">toomanage these roles, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="38cab-134">Кто имеет доступ к hello [центр учетных записей](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="38cab-134">Who can access hello [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="38cab-135">Toohello центр учетных записей можно выполнить только hello учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="38cab-135">Only hello Account Administrator can log in toohello Account center.</span></span> <span data-ttu-id="38cab-136">Hello учетная запись администратора является владельцем юридических hello hello подписки.</span><span class="sxs-lookup"><span data-stu-id="38cab-136">hello Account Administrator is hello legal owner of hello subscription.</span></span> <span data-ttu-id="38cab-137">По умолчанию hello пользователя, который зарегистрировал или купил hello подписки Azure — hello учетной записи администратора, если не hello [владельца подписки был передан](billing-subscription-transfer.md) toosomebody else.</span><span class="sxs-lookup"><span data-stu-id="38cab-137">By default, hello person who signed up for or bought hello Azure subscription is hello Account Administrator, unless hello [subscription ownership was transferred](billing-subscription-transfer.md) toosomebody else.</span></span> <span data-ttu-id="38cab-138">Hello учетной записи администратора можно создавать подписки, отмены подписки, изменить hello адрес для выставления счетов для подписки и управление политиками доступа для hello подписки.</span><span class="sxs-lookup"><span data-stu-id="38cab-138">hello Account Administrator can create subscriptions, cancel subscriptions, change hello billing address for a subscription, and manage access policies for hello subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="38cab-139">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="38cab-139">Need help?</span></span> <span data-ttu-id="38cab-140">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="38cab-140">Contact support.</span></span>

<span data-ttu-id="38cab-141">Если у вас есть дополнительные вопросы, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="38cab-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
