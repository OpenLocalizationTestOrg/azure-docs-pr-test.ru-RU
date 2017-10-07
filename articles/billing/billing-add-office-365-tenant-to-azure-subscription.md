---
title: "Office 365 aaaUse клиента с подпиской Azure | Документы Microsoft"
description: "Узнайте, как tooadd Office 365 directory (клиент) tooan подписки Azure."
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a><span data-ttu-id="16cc8-103">Связать tooan клиента Office 365 подписки Azure</span><span class="sxs-lookup"><span data-stu-id="16cc8-103">Associate an Office 365 tenant tooan Azure subscription</span></span>
<span data-ttu-id="16cc8-104">Свяжите отдельные подписки Azure и Office 365, чтобы доступ к Office 365 hello клиента из подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="16cc8-104">Link your separate Azure and Office 365 subscriptions so that you can access hello Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="16cc8-105">toolink подписок, вход tooAzure с hello учетной записи администратора службы Azure, добавьте каталог и добавить клиент Azure Active Directory toohello учетные записи организации hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="16cc8-105">toolink your subscriptions, sign in tooAzure with hello Azure service administrator account, add a directory, and add hello Office 365 organizational accounts toohello Azure Active Directory tenant.</span></span>

<span data-ttu-id="16cc8-106">Если вам необходима подписка Office 365 для пользователей в экземпляре Azure Active Directory, или у вас есть учетная запись Office 365, но нет учетной записи Azure, то см. статью [Регистрация в Azure с помощью учетной записи Office 365](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="16cc8-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="16cc8-107">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="16cc8-107">Before you begin</span></span>
* <span data-ttu-id="16cc8-108">Необходимо иметь учетные данные администратора службы подписки Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="16cc8-108">You must have hello credentials of hello Azure subscription service administrator.</span></span> <span data-ttu-id="16cc8-109">Учетные записи соадминистратора нельзя выполнить некоторые шаги hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="16cc8-109">Co-administrator accounts can't do some of hello steps in this article.</span></span> <span data-ttu-id="16cc8-110">toochange администратором службы, в разделе [как tooadd или изменение роли администратора Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="16cc8-110">toochange your service administrator, see [How tooadd or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="16cc8-111">Необходимо иметь учетные данные глобального администратора клиента Office 365 hello hello.</span><span class="sxs-lookup"><span data-stu-id="16cc8-111">You must have hello credentials of a global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="16cc8-112">адрес электронной почты администратора службы hello Hello должен отсутствовать в hello клиента Office 365.</span><span class="sxs-lookup"><span data-stu-id="16cc8-112">hello email address of hello service administrator must not be in hello Office 365 tenant.</span></span>
* <span data-ttu-id="16cc8-113">адрес электронной почты администратора службы hello Hello не может совпадать с любым глобальным администратором Office 365 hello клиента.</span><span class="sxs-lookup"><span data-stu-id="16cc8-113">hello email address of hello service administrator must not match that of any global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="16cc8-114">Если вы используете адрес электронной почты учетной записи Майкрософт и учетная запись организации, временно измените администратора службы hello из вашей подписки Azure toouse другой учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="16cc8-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change hello service administrator of your Azure subscription toouse another Microsoft account.</span></span> <span data-ttu-id="16cc8-115">Можно создать учетную запись Майкрософт на hello [страницу регистрации учетной записи Майкрософт](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="16cc8-115">You can create a Microsoft account at hello [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-tooazure-subscription"></a><span data-ttu-id="16cc8-116">Привязка подписки tooAzure клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="16cc8-116">Link Office 365 tenant tooAzure subscription</span></span>
<span data-ttu-id="16cc8-117">toohello клиента Office 365 hello tooassociate подписки Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="16cc8-117">tooassociate hello Office 365 tenant toohello Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a><span data-ttu-id="16cc8-118">Шаг 1: Добавление tooyour клиента Office 365 подписки Azure</span><span class="sxs-lookup"><span data-stu-id="16cc8-118">Step 1: Add Office 365 tenant tooyour Azure subscription</span></span>

1. <span data-ttu-id="16cc8-119">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/) с учетными данными администратора службы hello.</span><span class="sxs-lookup"><span data-stu-id="16cc8-119">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>

    ![Снимок экрана входа в Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="16cc8-121">Выберите в левой области hello **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="16cc8-121">In hello left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="16cc8-122">Не должны видеть клиента hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="16cc8-122">You shouldn't see hello Office 365 tenant.</span></span> <span data-ttu-id="16cc8-123">Если вы видите его, пропустите слишком[шаг 2: изменение hello каталог, связанный с hello подписки Azure](#Step2).</span><span class="sxs-lookup"><span data-stu-id="16cc8-123">If you see it, skip too[Step 2: Change hello directory associated with hello Azure subscription](#Step2).</span></span>
   
   ![Снимок экрана записи Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="16cc8-125">Выберите **Создать** > **Каталог** > **Настраиваемое создание**.</span><span class="sxs-lookup"><span data-stu-id="16cc8-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Снимок экрана создания настраиваемого каталога Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="16cc8-127">На hello **добавить каталог** в разделе **КАТАЛОГА**выберите **использовать существующий каталог**.</span><span class="sxs-lookup"><span data-stu-id="16cc8-127">On hello **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="16cc8-128">Выберите **я готов toobe выходу из системы**и выберите **завершить** ![завершения значок](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="16cc8-128">Then select **I am ready toobe signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Снимок экрана с параметром "Использовать существующий каталог"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="16cc8-130">После выхода, войдите с использованием учетных данных глобального администратора hello вашего клиента Office 365.</span><span class="sxs-lookup"><span data-stu-id="16cc8-130">After you are signed out, sign in with hello global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Снимок экрана входа глобального администратора Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="16cc8-132">Выберите **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="16cc8-132">Select **Continue**.</span></span>
   
    ![Снимок экрана проверки](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="16cc8-134">Щелкните **Выйти сейчас**.</span><span class="sxs-lookup"><span data-stu-id="16cc8-134">Select **Sign out now**.</span></span>
   
    ![Снимок экрана выхода](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="16cc8-136">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/) с учетными данными администратора службы hello.</span><span class="sxs-lookup"><span data-stu-id="16cc8-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>
   
    ![Снимок экрана входа в Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="16cc8-138">Вы увидите клиента Office 365 на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="16cc8-138">You should see your Office 365 tenant in hello dashboard.</span></span>
   
    ![Снимок экрана панели мониторинга](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="16cc8-140"><a name="Step2"></a>Шаг 2: Изменение каталога hello, hello подписки Azure</span><span class="sxs-lookup"><span data-stu-id="16cc8-140"><a name="Step2"></a>Step 2: Change hello directory associated with hello Azure subscription</span></span>
   
1. <span data-ttu-id="16cc8-141">Выберите элемент **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="16cc8-141">Select **Settings**.</span></span>
   
    ![Снимок экрана со значком настройки на классическом портале Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="16cc8-143">Выберите свою подписку Azure и щелкните **Изменить каталог**.</span><span class="sxs-lookup"><span data-stu-id="16cc8-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Снимок экрана изменения каталога подписки Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="16cc8-145">Щелкните **Далее** ![значок "Далее"](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="16cc8-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![Снимок экрана: «Изменение hello связанный каталог»](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="16cc8-147">Просмотрите учетные записи для затронутых hello.</span><span class="sxs-lookup"><span data-stu-id="16cc8-147">Review hello affected accounts.</span></span> <span data-ttu-id="16cc8-148">Все соадминистраторы и [управление доступом на основе ролей (RBAC)](../active-directory/role-based-access-control-configure.md) пользователи с ограниченным доступом к в существующих группах ресурсов hello, удаляются.</span><span class="sxs-lookup"><span data-stu-id="16cc8-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in hello existing resource groups are removed.</span></span> <span data-ttu-id="16cc8-149">Предупреждение Hello упоминаются только hello удаление администраторов.</span><span class="sxs-lookup"><span data-stu-id="16cc8-149">hello warning you receive only mentions hello removal of co-administrators.</span></span>
      
    ![Снимок экрана, показывающий hello toobe удалены учетные записи соадминистратора.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Снимок экрана, показывающий toobe учетной записи пользователя примере удаляются.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="16cc8-152">Щелкните **Завершить** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="16cc8-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a><span data-ttu-id="16cc8-153">Шаг 3: Добавьте учетные записи организации Office 365 в качестве администраторов клиента Azure Active Directory toohello</span><span class="sxs-lookup"><span data-stu-id="16cc8-153">Step 3: Add your Office 365 organizational accounts as co-administrators toohello Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="16cc8-154">Выберите hello **АДМИНИСТРАТОРЫ** , а затем выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="16cc8-154">Select hello **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Снимок экрана вкладки настройки администраторов на классическом портале Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="16cc8-156">Укажите учетную запись организации вашего клиента Office 365, выберите hello подписки Azure и затем выберите **завершить** ![завершения значок](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="16cc8-156">Enter an organizational account of your Office 365 tenant, select hello Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Снимок экрана диалогового окна добавления соадминистратора Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="16cc8-158">Вернитесь к предыдущему окну toohello **АДМИНИСТРАТОРЫ** вкладки. Вы увидите hello учетная запись организации отображается в качестве соадминистратора.</span><span class="sxs-lookup"><span data-stu-id="16cc8-158">Go back toohello **ADMINISTRATORS** tab. You should see hello organizational account displayed as co-administrator.</span></span>
   
    ![Снимок экрана вкладки "Администраторы"](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="16cc8-160">Тест tooAzure доступ с помощью учетной записи соадминистратора hello.</span><span class="sxs-lookup"><span data-stu-id="16cc8-160">Test access tooAzure with hello co-administrator account.</span></span>
   
    <span data-ttu-id="16cc8-161">а.</span><span class="sxs-lookup"><span data-stu-id="16cc8-161">a.</span></span> <span data-ttu-id="16cc8-162">Выйдите из hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="16cc8-162">Sign out of hello Azure classic portal.</span></span>
   
    <span data-ttu-id="16cc8-163">b.</span><span class="sxs-lookup"><span data-stu-id="16cc8-163">b.</span></span> <span data-ttu-id="16cc8-164">Откройте hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="16cc8-164">Open hello [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="16cc8-165">c.</span><span class="sxs-lookup"><span data-stu-id="16cc8-165">c.</span></span> <span data-ttu-id="16cc8-166">Введите учетные данные hello hello совместного администратора, а затем выберите **входа**.</span><span class="sxs-lookup"><span data-stu-id="16cc8-166">Enter hello credentials of hello co-administrator, and then select **Sign in**.</span></span>
   
    ![Снимок экрана страницы входа в Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="16cc8-168">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="16cc8-168">Need help?</span></span> <span data-ttu-id="16cc8-169">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="16cc8-169">Contact support.</span></span>
<span data-ttu-id="16cc8-170">Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="16cc8-170">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>


