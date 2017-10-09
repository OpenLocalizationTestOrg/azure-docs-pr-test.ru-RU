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
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="9a0d4-103">Включение синхронизации паролей tooAzure доменных служб Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a0d4-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="9a0d4-104">Выполняя предыдущие задачи, вы включили доменные службы Azure Active Directory для клиента Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a0d4-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="9a0d4-105">Следующая задача Hello-tooenable синхронизации хэшей учетные данные, необходимые для tooAzure проверки подлинности NT LAN Manager (NTLM) и Kerberos доменные службы AD.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="9a0d4-106">После настройки синхронизации учетных данных, пользователи могут входить в управляемый домен toohello со своими корпоративными учетными данными.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="9a0d4-107">этапы Hello отличаются для учетных записей пользователя только для облака учетные записи vs, которые синхронизируются из вашего локального каталога с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="9a0d4-108">Если клиент Azure AD имеет сочетание облако только пользователей и пользователей из локальной AD, необходимо tooperform оба шага.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="9a0d4-109">**Учетные записи пользователей только для облака**: [синхронизации паролей для облачных учетных записей пользователей tooyour управляемого домена](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="9a0d4-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="9a0d4-110">**Локальные учетные записи пользователей**: [синхронизировать пароли для учетных записей пользователей, синхронизированных из локальной AD tooyour управляемого домена](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="9a0d4-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="9a0d4-111">Задача 5: Включение пароль tooyour управляемого домена синхронизации учетных записей пользователя только для облака</span><span class="sxs-lookup"><span data-stu-id="9a0d4-111">Task 5: enable password synchronization tooyour managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="9a0d4-112">Пользователи tooauthenticate hello управляемого домена, доменных служб Active Directory Azure требуются учетные данные хэш-коды в формате, который подходит для проверки подлинности NTLM и Kerberos.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-112">tooauthenticate users on hello managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="9a0d4-113">Azure AD не создавать и хранить хэши учетных данных в формате hello, необходимый для проверки подлинности NTLM или Kerberos, пока не будет включена, Azure доменных служб Active Directory для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-113">Azure AD does not generate or store credential hashes in hello format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="9a0d4-114">Из очевидных соображений безопасности служба Azure AD не хранит пароли в формате открытого текста.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="9a0d4-115">Таким образом Azure AD не имеет tooautomatically способом создания этих учетных данных хэш NTLM или Kerberos на основе существующих учетных данных пользователей.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-115">Therefore, Azure AD does not have a way tooautomatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="9a0d4-116">Если ваша организация использует учетные записи пользователей, пользователей, которым необходим служб домена Active Directory toouse Azure необходимо изменить свои пароли.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-116">If your organization has cloud-only user accounts, users who need toouse Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="9a0d4-117">Учетная запись пользователя только для облака — учетная запись, созданная в Azure AD с помощью hello портал Azure или командлеты Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-117">A cloud-only user account is an account that was created in your Azure AD directory using either hello Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="9a0d4-118">Такие учетные записи пользователей не синхронизированы из локального каталога.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="9a0d4-119">Этот процесс изменения пароля приводит hello учетных данных хэш-коды, которые необходимы Azure доменных служб Active Directory для toobe проверки подлинности Kerberos и NTLM, созданные в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-119">This password change process causes hello credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication toobe generated in Azure AD.</span></span> <span data-ttu-id="9a0d4-120">Либо срок действия можно hello пароли для всех пользователей в hello клиентов, которым требуется служб домена Active Directory Azure toouse или предложите им toochange свои пароли.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-120">You can either expire hello passwords for all users in hello tenant who need toouse Azure Active Directory Domain Services or instruct them toochange their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="9a0d4-121">Включение создания хэшей учетных данных NTLM и Kerberos для облачных учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="9a0d4-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="9a0d4-122">Ниже приведены hello указания по созданию tooprovide пользователей, чтобы они могли изменять свои пароли.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-122">Here are hello instructions you need tooprovide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="9a0d4-123">Go toohello [панели доступа Azure AD](http://myapps.microsoft.com) страницы для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-123">Go toohello [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Запуск панели доступа Azure AD hello](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="9a0d4-125">В hello правом верхнем углу щелкните свое имя и выберите **профиль** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="9a0d4-125">In hello top right corner, click on your name and select **Profile** from hello menu.</span></span>

    ![Выбор параметра "Профиль"](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="9a0d4-127">На hello **профиль** щелкните **Смена пароля**.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-127">On hello **Profile** page, click on **Change password**.</span></span>

    ![Выбор параметра "Изменение пароля"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="9a0d4-129">Если hello **Смена пароля** параметр не отображается в окне приветствия панели доступа, убедитесь, что ваша организация настроил [управление паролями в Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="9a0d4-129">If hello **Change password** option is not displayed in hello Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="9a0d4-130">На hello **смены пароля** введите текущий пароль (старая), введите новый пароль и затем подтвердите его.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-130">On hello **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Создание виртуальной сети для доменных служб Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="9a0d4-132">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-132">Click **submit**.</span></span>

<span data-ttu-id="9a0d4-133">Через несколько минут после вы изменили свой пароль, новый пароль hello, можно использовать в доменных службах Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-133">A few minutes after you have changed your password, hello new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="9a0d4-134">Через несколько дополнительных минут (обычно около 20 в минутах), вы сможете войти в toocomputers, которые присоединены к домену toohello управляемого домена с помощью пароля hello только что изменен.</span><span class="sxs-lookup"><span data-stu-id="9a0d4-134">After a few more minutes (typically, about 20 minutes), you can sign in toocomputers that are joined toohello managed domain by using hello newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="9a0d4-135">Похожий контент</span><span class="sxs-lookup"><span data-stu-id="9a0d4-135">Related Content</span></span>
* [<span data-ttu-id="9a0d4-136">Как tooupdate свой пароль</span><span class="sxs-lookup"><span data-stu-id="9a0d4-136">How tooupdate your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="9a0d4-137">Приступая к работе с компонентами управления паролями</span><span class="sxs-lookup"><span data-stu-id="9a0d4-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="9a0d4-138">Включить синхронизацию паролей для клиента tooAzure доменных служб Active Directory для синхронизированных Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a0d4-138">Enable password synchronization tooAzure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="9a0d4-139">Администрирование управляемого домена доменных служб Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a0d4-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="9a0d4-140">К домену Windows виртуальной машины tooan управляемых доменных служб Active Directory Azure</span><span class="sxs-lookup"><span data-stu-id="9a0d4-140">Join a Windows virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="9a0d4-141">К домену Red Hat Enterprise Linux виртуальной машины tooan управляемых доменных служб Active Directory Azure</span><span class="sxs-lookup"><span data-stu-id="9a0d4-141">Join a Red Hat Enterprise Linux virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
