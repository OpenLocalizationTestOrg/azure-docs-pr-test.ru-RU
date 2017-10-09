---
title: "aaaAzure AD многоуровневого безопасности пароля | Документы Microsoft"
description: "В этой статье объясняется, как Azure AD применяет надежные пароли и защищает пароли пользователей от киберпреступников."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a><span data-ttu-id="f05bd-103">Защита паролем многоуровневый подход tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="f05bd-103">A multi-tiered approach tooAzure AD password security</span></span>

<span data-ttu-id="f05bd-104">В этой статье обсуждаются некоторые рекомендации, можно выполнить как пользователь или администратор tooprotect Azure Active Directory (Azure AD) либо учетная запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f05bd-104">This article discusses some best practices you can follow as a user or as an administrator tooprotect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="f05bd-105">Azure AD администраторы могут сбросить пароли пользователей, с помощью инструкции hello в статье hello [Сброс hello пароля для пользователя в Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f05bd-105">Azure AD administrators can reset user passwords using hello guidance in hello article [Reset hello password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="f05bd-106">Пользователи могут сбросить свой пароль, с помощью инструкции hello в статье hello [справки пользователь забыл свой пароль Azure AD](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="f05bd-106">Users can reset their own password using hello guidance in hello article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="f05bd-107">Требования к паролю</span><span class="sxs-lookup"><span data-stu-id="f05bd-107">Password requirements</span></span>

<span data-ttu-id="f05bd-108">Azure AD включает hello следующих распространенных простых паролей toosecuring подходов:</span><span class="sxs-lookup"><span data-stu-id="f05bd-108">Azure AD incorporates hello following common approaches toosecuring passwords:</span></span>

* <span data-ttu-id="f05bd-109">настройка требований к длине пароля;</span><span class="sxs-lookup"><span data-stu-id="f05bd-109">Password length requirements</span></span>
* <span data-ttu-id="f05bd-110">настройка требований к сложности пароля;</span><span class="sxs-lookup"><span data-stu-id="f05bd-110">Password complexity requirements</span></span>
* <span data-ttu-id="f05bd-111">регулярная и периодическая смена пароля.</span><span class="sxs-lookup"><span data-stu-id="f05bd-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="f05bd-112">Сведения о в Azure Active Directory сброса пароля см. в разделе hello [Azure AD самостоятельный сброс пароля для ИТ-специалистов hello](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="f05bd-112">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="f05bd-113">Защита паролей в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f05bd-113">Azure AD password protections</span></span>

<span data-ttu-id="f05bd-114">Azure AD и система учетных записей Майкрософт использовать проверенные отрасли hello подходы tooensure безопасного защиты пользователей и администраторов паролей, включая:</span><span class="sxs-lookup"><span data-stu-id="f05bd-114">Azure AD and hello Microsoft Account System use industry proven approaches tooensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="f05bd-115">Динамическая блокировка паролей</span><span class="sxs-lookup"><span data-stu-id="f05bd-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="f05bd-116">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="f05bd-116">Smart Password Lockout</span></span>

<span data-ttu-id="f05bd-117">Сведения об управлении паролями, основаны на текущем исследованиях. в разделе Технический документ hello [пароль руководство](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="f05bd-117">For information about password management based on current research, see hello whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="f05bd-118">Динамическая блокировка паролей</span><span class="sxs-lookup"><span data-stu-id="f05bd-118">Dynamically banned passwords</span></span>

<span data-ttu-id="f05bd-119">Azure AD и учетные записи Майкрософт обеспечивают защиту паролей, динамически запрещая все часто используемые пароли.</span><span class="sxs-lookup"><span data-stu-id="f05bd-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="f05bd-120">Команда защиты идентификации Azure идентификатор Hello регулярно анализирует списки запрещенных пароль, предотвращая Выбор часто используемые паролей пользователями.</span><span class="sxs-lookup"><span data-stu-id="f05bd-120">hello Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="f05bd-121">Эта служба является доступной tooAzure AD и клиентов службы учетных записей Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="f05bd-121">This service is available tooAzure AD and hello Microsoft Account Service customers.</span></span>

<span data-ttu-id="f05bd-122">При создании паролей, очень важно для администраторов tooencourage пользователей toochoose пароль фраз, которые содержат уникальное сочетание буквы, цифры, символы или слова.</span><span class="sxs-lookup"><span data-stu-id="f05bd-122">When creating passwords, it is important for administrators tooencourage users toochoose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="f05bd-123">Такой подход помогает скомпрометирован toobe практически невозможно, но упрощает для пользователей tooremember пароли пользователей toomake.</span><span class="sxs-lookup"><span data-stu-id="f05bd-123">This approach helps toomake user passwords nearly impossible toobe compromised but easier for users tooremember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="f05bd-124">Нарушение безопасности паролей</span><span class="sxs-lookup"><span data-stu-id="f05bd-124">Password breaches</span></span>

<span data-ttu-id="f05bd-125">Корпорация Майкрософт всегда работает один шаг toostay до кибер злоумышленники.</span><span class="sxs-lookup"><span data-stu-id="f05bd-125">Microsoft is always working toostay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="f05bd-126">Команда Azure AD Identity Protection Hello постоянно анализирует пароли, которые широко используются.</span><span class="sxs-lookup"><span data-stu-id="f05bd-126">hello Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="f05bd-127">Кибер-также используют злоумышленники аналогичные tooinform стратегии их атаки, такие как построение [радуги таблицы](https://en.wikipedia.org/wiki/Rainbow_table) для взлома хэши паролей.</span><span class="sxs-lookup"><span data-stu-id="f05bd-127">Cyber-criminals also use similar strategies tooinform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="f05bd-128">Корпорация Майкрософт постоянно анализирует [утечки данных](https://www.privacyrights.org/data-breaches) toomaintain список обновляется динамически запрещенное пароль, который обеспечивает заблокированные пароли уязвимы прежде чем они станут реальную угрозы tooAzure AD клиентов.</span><span class="sxs-lookup"><span data-stu-id="f05bd-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) toomaintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat tooAzure AD customers.</span></span> <span data-ttu-id="f05bd-129">Дополнительные сведения о текущем усилия по безопасности см. в разделе hello [этого отчета](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="f05bd-129">For more information about our current security efforts, see hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="f05bd-130">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="f05bd-130">Smart Password Lockout</span></span>

<span data-ttu-id="f05bd-131">Когда Azure AD обнаруживает потенциальные toohack при атаках кибер в пароля пользователя, мы заблокировать учетную запись пользователя hello смарт-блокировка пароль.</span><span class="sxs-lookup"><span data-stu-id="f05bd-131">When Azure AD detects a potential cyber-criminal trying toohack into a user password, we lock hello user account with Smart Password Lockout.</span></span> <span data-ttu-id="f05bd-132">Azure AD предназначен toodetermine hello рисков, связанных с сеансами конкретного имени входа.</span><span class="sxs-lookup"><span data-stu-id="f05bd-132">Azure AD is designed toodetermine hello risk associated with specific login sessions.</span></span> <span data-ttu-id="f05bd-133">Затем с помощью hello самые последние данные безопасности, мы применяем угроз кибер toostop семантику блокировки.</span><span class="sxs-lookup"><span data-stu-id="f05bd-133">Then using hello most up-to-date security data, we apply lockout semantics toostop cyber threats.</span></span>

<span data-ttu-id="f05bd-134">Если пользователь заблокирован из Azure AD, их экран выглядит примерно toohello том, что следует:</span><span class="sxs-lookup"><span data-stu-id="f05bd-134">If a user is locked out of Azure AD, their screen looks similar toohello one that follows:</span></span>

  ![Блокировка в Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="f05bd-136">Для других учетных записей Майкрософт их экран выглядит примерно toohello том, что следует:</span><span class="sxs-lookup"><span data-stu-id="f05bd-136">For other Microsoft accounts, their screen looks similar toohello one that follows:</span></span>

  ![Блокировка учетной записи Майкрософт](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="f05bd-138">Сведения о в Azure Active Directory сброса пароля см. в разделе hello [Azure AD самостоятельный сброс пароля для ИТ-специалистов hello](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="f05bd-138">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="f05bd-139">Если вы являетесь администратором Azure AD, вы можете toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid наличие пользователей создавать традиционные пароли полностью.</span><span class="sxs-lookup"><span data-stu-id="f05bd-139">If you are an Azure AD administrator, you may want toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="f05bd-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f05bd-140">Next steps</span></span>

* [<span data-ttu-id="f05bd-141">Как tooupdate свой пароль</span><span class="sxs-lookup"><span data-stu-id="f05bd-141">How tooupdate your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="f05bd-142">Основные принципы управления удостоверениями Azure Hello</span><span class="sxs-lookup"><span data-stu-id="f05bd-142">hello fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="f05bd-143">Приступая к работе с Azure</span><span class="sxs-lookup"><span data-stu-id="f05bd-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


