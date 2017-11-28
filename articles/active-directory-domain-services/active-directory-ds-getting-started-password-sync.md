---
title: "Доменные службы Azure Active Directory. Включение синхронизации паролей | Документация Майкрософт"
description: "Приступая к работе с доменными службами Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 4b6da997f44860dccb2aa2571ce099ab2d0231f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="6d275-103">Включение синхронизации паролей с доменными службами Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d275-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="6d275-104">Выполняя предыдущие задачи, вы включили доменные службы Azure Active Directory для клиента Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d275-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="6d275-105">Следующая задача — включить синхронизацию необходимых хэшей учетных данных, чтобы проверить подлинность NTLM и Kerberos в доменных службах Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d275-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="6d275-106">Когда синхронизация учетных данных настроена, пользователи могут входить в управляемый домен с помощью учетных данных организации.</span><span class="sxs-lookup"><span data-stu-id="6d275-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="6d275-107">Этапы настройки различаются для облачных учетных записей пользователей и учетных записей пользователей, синхронизированных из локального каталога с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6d275-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="6d275-108">Если клиент Azure AD содержит и пользователей в облаке, и пользователей из локального каталога AD, необходимо выполнить оба этапа.</span><span class="sxs-lookup"><span data-stu-id="6d275-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="6d275-109">**Учетные записи пользователей в облаке.** [Синхронизация паролей учетных записей пользователей в облаке с управляемым доменом](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="6d275-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="6d275-110">**Локальные учетные записи пользователей.** [Синхронизация паролей учетных записей пользователей, синхронизированных из локального каталога AD, с управляемым доменом](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="6d275-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="6d275-111">Задача 5. Включение синхронизации паролей учетных записей пользователей в облаке с управляемым доменом</span><span class="sxs-lookup"><span data-stu-id="6d275-111">Task 5: enable password synchronization to your managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="6d275-112">Чтобы выполнять аутентификацию пользователей в управляемом домене, доменным службам Azure Active Directory нужны хэши учетных данных в формате, который подходит для аутентификации NTLM и Kerberos.</span><span class="sxs-lookup"><span data-stu-id="6d275-112">To authenticate users on the managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="6d275-113">Пока вы не включите доменные службы Azure Active Directory для клиента, служба Azure AD не будет создавать и хранить хэши учетных данных в формате, требуемом для проверки подлинности NTLM или Kerberos.</span><span class="sxs-lookup"><span data-stu-id="6d275-113">Azure AD does not generate or store credential hashes in the format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="6d275-114">Из очевидных соображений безопасности служба Azure AD не хранит пароли в формате открытого текста.</span><span class="sxs-lookup"><span data-stu-id="6d275-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="6d275-115">Поэтому она не может автоматически создавать хэши учетных данных NTLM и Kerberos на основании имеющихся учетных данных пользователей.</span><span class="sxs-lookup"><span data-stu-id="6d275-115">Therefore, Azure AD does not have a way to automatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="6d275-116">Если у вашей организации есть только учетные записи пользователей в облаке, пользователи, которые хотят воспользоваться доменными службами Azure Active Directory, должны изменить свои пароли.</span><span class="sxs-lookup"><span data-stu-id="6d275-116">If your organization has cloud-only user accounts, users who need to use Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="6d275-117">Облачная учетная запись пользователей — это учетная запись, созданная в каталоге Azure AD с помощью портала Azure или командлетов Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d275-117">A cloud-only user account is an account that was created in your Azure AD directory using either the Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="6d275-118">Такие учетные записи пользователей не синхронизированы из локального каталога.</span><span class="sxs-lookup"><span data-stu-id="6d275-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="6d275-119">Для этого необходимо сформировать в Azure AD хэши учетных данных, необходимые доменным службам Azure Active Directory для аутентификации Kerberos и NTLM.</span><span class="sxs-lookup"><span data-stu-id="6d275-119">This password change process causes the credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span></span> <span data-ttu-id="6d275-120">Вы можете либо принудительно сделать так, чтобы срок действия паролей для всех пользователей в клиенте доменных служб Azure Active Directory истек, либо отправить пользователям инструкции по изменению паролей.</span><span class="sxs-lookup"><span data-stu-id="6d275-120">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="6d275-121">Включение создания хэшей учетных данных NTLM и Kerberos для облачных учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="6d275-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="6d275-122">Инструкции по изменению паролей, которые необходимо отправить пользователям, приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="6d275-122">Here are the instructions you need to provide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="6d275-123">Перейдите на корпоративную страницу с [панелью доступа Azure AD](http://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6d275-123">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Запуск панели доступа Azure AD](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="6d275-125">В правом верхнем углу щелкните свое имя, а затем в открывшемся меню выберите **Профиль**.</span><span class="sxs-lookup"><span data-stu-id="6d275-125">In the top right corner, click on your name and select **Profile** from the menu.</span></span>

    ![Выбор параметра "Профиль"](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="6d275-127">На странице **Профиль** щелкните **Изменение пароля**.</span><span class="sxs-lookup"><span data-stu-id="6d275-127">On the **Profile** page, click on **Change password**.</span></span>

    ![Выбор параметра "Изменение пароля"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="6d275-129">Если параметр **Изменить пароль** не отображается в окне панели доступа, убедитесь, что для вашей организации настроено [управление паролями в Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6d275-129">If the **Change password** option is not displayed in the Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="6d275-130">На странице **изменения пароля** введите старый пароль, затем введите новый пароль и подтвердите его.</span><span class="sxs-lookup"><span data-stu-id="6d275-130">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Создание виртуальной сети для доменных служб Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="6d275-132">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="6d275-132">Click **submit**.</span></span>

<span data-ttu-id="6d275-133">Новый пароль вступает в силу в доменных службах Azure Active Directory через несколько минут после изменения.</span><span class="sxs-lookup"><span data-stu-id="6d275-133">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="6d275-134">Входить на компьютеры, подключенные к управляемому домену, с помощью нового пароля можно через некоторое время (обычно это 20 минут).</span><span class="sxs-lookup"><span data-stu-id="6d275-134">After a few more minutes (typically, about 20 minutes), you can sign in to computers that are joined to the managed domain by using the newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="6d275-135">Похожий контент</span><span class="sxs-lookup"><span data-stu-id="6d275-135">Related Content</span></span>
* [<span data-ttu-id="6d275-136">Как изменить свой пароль</span><span class="sxs-lookup"><span data-stu-id="6d275-136">How to update your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="6d275-137">Приступая к работе с компонентами управления паролями</span><span class="sxs-lookup"><span data-stu-id="6d275-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="6d275-138">Включение синхронизации паролей с доменными службами Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d275-138">Enable password synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="6d275-139">Администрирование управляемого домена доменных служб Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d275-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="6d275-140">Присоединение виртуальной машины Windows Server к управляемому домену</span><span class="sxs-lookup"><span data-stu-id="6d275-140">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="6d275-141">Присоединение виртуальной машины Red Hat Enterprise Linux 7 к управляемому домену</span><span class="sxs-lookup"><span data-stu-id="6d275-141">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
