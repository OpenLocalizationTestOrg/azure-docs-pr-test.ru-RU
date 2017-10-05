---
title: "Использование клиента Office 365 с подпиской Azure | Документация Майкрософт"
description: "Узнайте, как добавить каталог (клиент) Office 365 в подписку Azure."
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
ms.openlocfilehash: 7affb4a83cdb8ababef60e786a3c824e7477ed68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="associate-an-office-365-tenant-to-an-azure-subscription"></a><span data-ttu-id="01ec8-103">Связывание клиента Office 365 с подпиской Azure</span><span class="sxs-lookup"><span data-stu-id="01ec8-103">Associate an Office 365 tenant to an Azure subscription</span></span>
<span data-ttu-id="01ec8-104">Свяжите отдельные подписки Azure и Office 365, чтобы иметь доступ к клиенту Office 365 из подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="01ec8-104">Link your separate Azure and Office 365 subscriptions so that you can access the Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="01ec8-105">Чтобы связать подписки, войдите в Azure, используя учетную запись администратора служб Azure, добавьте каталог, а затем добавьте учетные записи организации Office 365 в клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="01ec8-105">To link your subscriptions, sign in to Azure with the Azure service administrator account, add a directory, and add the Office 365 organizational accounts to the Azure Active Directory tenant.</span></span>

<span data-ttu-id="01ec8-106">Если вам необходима подписка Office 365 для пользователей в экземпляре Azure Active Directory, или у вас есть учетная запись Office 365, но нет учетной записи Azure, то см. статью [Регистрация в Azure с помощью учетной записи Office 365](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="01ec8-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="01ec8-107">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="01ec8-107">Before you begin</span></span>
* <span data-ttu-id="01ec8-108">Необходимо иметь учетные данные администратора служб подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="01ec8-108">You must have the credentials of the Azure subscription service administrator.</span></span> <span data-ttu-id="01ec8-109">Учетная запись соадминистратора не позволяет выполнить некоторые действия, описанные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="01ec8-109">Co-administrator accounts can't do some of the steps in this article.</span></span> <span data-ttu-id="01ec8-110">Чтобы изменить администратора службы, см. статью [Добавление или изменение ролей администратора Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="01ec8-110">To change your service administrator, see [How to add or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="01ec8-111">Необходимо иметь учетные данные глобального администратора клиента Office 365.</span><span class="sxs-lookup"><span data-stu-id="01ec8-111">You must have the credentials of a global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="01ec8-112">Адрес электронной почты администратора служб не должен содержаться на клиенте Office 365.</span><span class="sxs-lookup"><span data-stu-id="01ec8-112">The email address of the service administrator must not be in the Office 365 tenant.</span></span>
* <span data-ttu-id="01ec8-113">Адрес электронной почты администратора служб не должен совпадать с адресом электронной почты любого из глобальных администраторов клиента Office 365.</span><span class="sxs-lookup"><span data-stu-id="01ec8-113">The email address of the service administrator must not match that of any global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="01ec8-114">Если вы используете электронный адрес, который одновременно представляет учетную запись Майкрософт и учетную запись организации, то временно измените роль администратора служб своей подписки Azure, чтобы использовать другую учетную запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="01ec8-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change the service administrator of your Azure subscription to use another Microsoft account.</span></span> <span data-ttu-id="01ec8-115">Учетную запись Майкрософт можно создать на [странице регистрации учетных записей Майкрософт](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="01ec8-115">You can create a Microsoft account at the [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-to-azure-subscription"></a><span data-ttu-id="01ec8-116">Связывание клиента Office 365 с подпиской Azure</span><span class="sxs-lookup"><span data-stu-id="01ec8-116">Link Office 365 tenant to Azure subscription</span></span>
<span data-ttu-id="01ec8-117">Чтобы связать клиент Office 365 с подпиской Azure, выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="01ec8-117">To associate the Office 365 tenant to the Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-to-your-azure-subscription"></a><span data-ttu-id="01ec8-118">Шаг 1. Добавление клиента Office 365 в подписку Azure</span><span class="sxs-lookup"><span data-stu-id="01ec8-118">Step 1: Add Office 365 tenant to your Azure subscription</span></span>

1. <span data-ttu-id="01ec8-119">Войдите на [классический портал Azure](https://manage.windowsazure.com/), используя учетные данные администратора службы.</span><span class="sxs-lookup"><span data-stu-id="01ec8-119">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>

    ![Снимок экрана входа в Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="01ec8-121">В области слева выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01ec8-121">In the left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="01ec8-122">Клиент Office 365 отображаться не должен.</span><span class="sxs-lookup"><span data-stu-id="01ec8-122">You shouldn't see the Office 365 tenant.</span></span> <span data-ttu-id="01ec8-123">Если он отображается, то перейдите к разделу [Шаг 2. Изменение каталога, связанного с подпиской Azure](#Step2).</span><span class="sxs-lookup"><span data-stu-id="01ec8-123">If you see it, skip to [Step 2: Change the directory associated with the Azure subscription](#Step2).</span></span>
   
   ![Снимок экрана записи Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="01ec8-125">Выберите **Создать** > **Каталог** > **Настраиваемое создание**.</span><span class="sxs-lookup"><span data-stu-id="01ec8-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Снимок экрана создания настраиваемого каталога Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="01ec8-127">На странице **Добавить каталог** в разделе **Каталог** выберите **Использовать существующий каталог**.</span><span class="sxs-lookup"><span data-stu-id="01ec8-127">On the **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="01ec8-128">Выберите **Я готов к выходу из системы** и щелкните **Завершить** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="01ec8-128">Then select **I am ready to be signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Снимок экрана с параметром "Использовать существующий каталог"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="01ec8-130">После выхода из системы войдите в нее с помощью учетных данных глобального администратора клиента Office 365.</span><span class="sxs-lookup"><span data-stu-id="01ec8-130">After you are signed out, sign in with the global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Снимок экрана входа глобального администратора Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="01ec8-132">Выберите **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="01ec8-132">Select **Continue**.</span></span>
   
    ![Снимок экрана проверки](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="01ec8-134">Щелкните **Выйти сейчас**.</span><span class="sxs-lookup"><span data-stu-id="01ec8-134">Select **Sign out now**.</span></span>
   
    ![Снимок экрана выхода](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="01ec8-136">Войдите на [классический портал Azure](https://manage.windowsazure.com/), используя учетные данные администратора службы.</span><span class="sxs-lookup"><span data-stu-id="01ec8-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>
   
    ![Снимок экрана входа в Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="01ec8-138">Клиент Office 365 должен отображаться на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="01ec8-138">You should see your Office 365 tenant in the dashboard.</span></span>
   
    ![Снимок экрана панели мониторинга](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="01ec8-140"><a name="Step2"></a>Шаг 2. Изменение каталога, связанного с подпиской Azure</span><span class="sxs-lookup"><span data-stu-id="01ec8-140"><a name="Step2"></a>Step 2: Change the directory associated with the Azure subscription</span></span>
   
1. <span data-ttu-id="01ec8-141">Выберите элемент **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="01ec8-141">Select **Settings**.</span></span>
   
    ![Снимок экрана со значком настройки на классическом портале Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="01ec8-143">Выберите свою подписку Azure и щелкните **Изменить каталог**.</span><span class="sxs-lookup"><span data-stu-id="01ec8-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Снимок экрана изменения каталога подписки Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="01ec8-145">Щелкните **Далее** ![значок "Далее"](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="01ec8-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![Снимок экрана диалогового окна "Изменить связанный каталог"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="01ec8-147">Проверьте учетные записи, затронутые этим изменением.</span><span class="sxs-lookup"><span data-stu-id="01ec8-147">Review the affected accounts.</span></span> <span data-ttu-id="01ec8-148">Все соадминистраторы и пользователи [управления доступом на основе ролей (RBAC)](../active-directory/role-based-access-control-configure.md), имеющие назначенные права доступа в существующих группах ресурсов, также удаляются.</span><span class="sxs-lookup"><span data-stu-id="01ec8-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in the existing resource groups are removed.</span></span> <span data-ttu-id="01ec8-149">В предупреждении, которое вы получите, упоминается только об удалении соадминистраторов.</span><span class="sxs-lookup"><span data-stu-id="01ec8-149">The warning you receive only mentions the removal of co-administrators.</span></span>
      
    ![Снимок экрана, показывающий удаляемые учетные записи администратора.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Снимок экрана, показывающий пример удаляемой учетной записи.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="01ec8-152">Щелкните **Завершить** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="01ec8-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-to-the-azure-active-directory-tenant"></a><span data-ttu-id="01ec8-153">Шаг 3. Добавление учетных записей Office 365 организации в качестве соадминистраторов в клиент Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01ec8-153">Step 3: Add your Office 365 organizational accounts as co-administrators to the Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="01ec8-154">Откройте вкладку **Администраторы**, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="01ec8-154">Select the **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Снимок экрана вкладки настройки администраторов на классическом портале Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="01ec8-156">Укажите в клиенте Office 365 корпоративную учетную запись, выберите подписку Azure и щелкните **Завершить** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="01ec8-156">Enter an organizational account of your Office 365 tenant, select the Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Снимок экрана диалогового окна добавления соадминистратора Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="01ec8-158">Вернитесь на вкладку **Администраторы**.</span><span class="sxs-lookup"><span data-stu-id="01ec8-158">Go back to the **ADMINISTRATORS** tab.</span></span> <span data-ttu-id="01ec8-159">На ней должна отображаться учетная запись организации как соадминистратор.</span><span class="sxs-lookup"><span data-stu-id="01ec8-159">You should see the organizational account displayed as co-administrator.</span></span>
   
    ![Снимок экрана вкладки "Администраторы"](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="01ec8-161">Проверьте возможность доступа к Azure с помощью учетной записи соадминистратора.</span><span class="sxs-lookup"><span data-stu-id="01ec8-161">Test access to Azure with the co-administrator account.</span></span>
   
    <span data-ttu-id="01ec8-162">а.</span><span class="sxs-lookup"><span data-stu-id="01ec8-162">a.</span></span> <span data-ttu-id="01ec8-163">Выйдите с классического портала Azure.</span><span class="sxs-lookup"><span data-stu-id="01ec8-163">Sign out of the Azure classic portal.</span></span>
   
    <span data-ttu-id="01ec8-164">b.</span><span class="sxs-lookup"><span data-stu-id="01ec8-164">b.</span></span> <span data-ttu-id="01ec8-165">Откройте [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="01ec8-165">Open the [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="01ec8-166">c.</span><span class="sxs-lookup"><span data-stu-id="01ec8-166">c.</span></span> <span data-ttu-id="01ec8-167">Введите учетные данные соадминистратора и щелкните **Вход**.</span><span class="sxs-lookup"><span data-stu-id="01ec8-167">Enter the credentials of the co-administrator, and then select **Sign in**.</span></span>
   
    ![Снимок экрана страницы входа в Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="01ec8-169">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="01ec8-169">Need help?</span></span> <span data-ttu-id="01ec8-170">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="01ec8-170">Contact support.</span></span>
<span data-ttu-id="01ec8-171">Если вам все еще нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), которая поможет быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="01ec8-171">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>


