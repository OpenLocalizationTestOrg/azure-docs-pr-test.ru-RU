---
title: "Многоуровневая защита паролей в Azure AD | Документация Майкрософт"
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
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a><span data-ttu-id="5b0b8-103">Многоуровневый подход к безопасности паролей Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b0b8-103">A multi-tiered approach to Azure AD password security</span></span>

<span data-ttu-id="5b0b8-104">В этой статье приведены рекомендации для пользователей и администраторов по защите учетных записей Azure Active Directory (Azure AD) и Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-104">This article discusses some best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="5b0b8-105">Администраторы Azure AD могут сбрасывать пароли пользователей, используя руководство в статье [Сброс пароля пользователя в общедоступной предварительной версии Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5b0b8-105">Azure AD administrators can reset user passwords using the guidance in the article [Reset the password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="5b0b8-106">Пользователи могут сбросить пароль, следуя инструкциям в статье [Я не помню свой пароль Azure AD](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="5b0b8-106">Users can reset their own password using the guidance in the article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="5b0b8-107">Требования к паролю</span><span class="sxs-lookup"><span data-stu-id="5b0b8-107">Password requirements</span></span>

<span data-ttu-id="5b0b8-108">Для защиты паролей в Azure AD используются следующие распространенные методы:</span><span class="sxs-lookup"><span data-stu-id="5b0b8-108">Azure AD incorporates the following common approaches to securing passwords:</span></span>

* <span data-ttu-id="5b0b8-109">настройка требований к длине пароля;</span><span class="sxs-lookup"><span data-stu-id="5b0b8-109">Password length requirements</span></span>
* <span data-ttu-id="5b0b8-110">настройка требований к сложности пароля;</span><span class="sxs-lookup"><span data-stu-id="5b0b8-110">Password complexity requirements</span></span>
* <span data-ttu-id="5b0b8-111">регулярная и периодическая смена пароля.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="5b0b8-112">Сведения о сбросе пароля в Azure Active Directory см. в статье [Самостоятельный сброс пароля в Azure AD для ИТ-специалистов](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="5b0b8-112">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="5b0b8-113">Защита паролей в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b0b8-113">Azure AD password protections</span></span>

<span data-ttu-id="5b0b8-114">Azure AD и система учетных записей Майкрософт используют проверенные методы, чтобы обеспечить защиту паролей пользователей и администраторов. Эти методы описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-114">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="5b0b8-115">Динамическая блокировка паролей</span><span class="sxs-lookup"><span data-stu-id="5b0b8-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="5b0b8-116">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="5b0b8-116">Smart Password Lockout</span></span>

<span data-ttu-id="5b0b8-117">Сведения об управлении паролями на основе проведенных исследований см. в [рекомендациях для управления паролями](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="5b0b8-117">For information about password management based on current research, see the whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="5b0b8-118">Динамическая блокировка паролей</span><span class="sxs-lookup"><span data-stu-id="5b0b8-118">Dynamically banned passwords</span></span>

<span data-ttu-id="5b0b8-119">Azure AD и учетные записи Майкрософт обеспечивают защиту паролей, динамически запрещая все часто используемые пароли.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="5b0b8-120">Команда защиты идентификации Azure регулярно анализирует списки заблокированных паролей, чтобы запретить пользователям использовать стандартные пароли.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="5b0b8-121">Эта служба доступна для всех клиентов Azure AD и службы учетных записей Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-121">This service is available to Azure AD and the Microsoft Account Service customers.</span></span>

<span data-ttu-id="5b0b8-122">Администраторы должны следить за тем, чтобы пользователи создавали пароли, которые содержат уникальное сочетание букв, цифр и символов или слов.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-122">When creating passwords, it is important for administrators to encourage users to choose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="5b0b8-123">Такой подход делает подбор пароля практически невозможным, но помогает пользователям запоминать пароли.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-123">This approach helps to make user passwords nearly impossible to be compromised but easier for users to remember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="5b0b8-124">Нарушение безопасности паролей</span><span class="sxs-lookup"><span data-stu-id="5b0b8-124">Password breaches</span></span>

<span data-ttu-id="5b0b8-125">Корпорация Майкрософт всегда старается идти на шаг впереди киберпреступников.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-125">Microsoft is always working to stay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="5b0b8-126">Команда защиты идентификации Azure AD постоянно анализирует часто используемые пароли.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-126">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="5b0b8-127">Киберпреступники также применяют подобные методы (такие как создание [радужной таблицы](https://en.wikipedia.org/wiki/Rainbow_table) для взлома хэшей паролей) для подготовки своих атак.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-127">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="5b0b8-128">Корпорация Майкрософт постоянно анализирует [утечки данных](https://www.privacyrights.org/data-breaches), чтобы поддерживать динамически обновляемый список паролей, что позволяет блокировать уязвимые пароли, прежде чем они станут потенциальной угрозой для клиентов Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span></span> <span data-ttu-id="5b0b8-129">Дополнительные сведения о нашей текущей деятельности по обеспечению безопасности см. в этом [отчете корпорации Майкрософт](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b0b8-129">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="5b0b8-130">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="5b0b8-130">Smart Password Lockout</span></span>

<span data-ttu-id="5b0b8-131">Когда Azure AD обнаружит, что потенциальный киберпреступник пытается взломать пароль пользователя, учетная запись пользователя будет автоматически заблокирована с помощью Smart Password Lockout.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-131">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span></span> <span data-ttu-id="5b0b8-132">Azure AD позволяет определить риск, связанный с конкретным сеансом входа.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-132">Azure AD is designed to determine the risk associated with specific login sessions.</span></span> <span data-ttu-id="5b0b8-133">Используя самые актуальные данные безопасности, мы применяем семантику блокировки, позволяющую остановить киберугрозы.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-133">Then using the most up-to-date security data, we apply lockout semantics to stop cyber threats.</span></span>

<span data-ttu-id="5b0b8-134">Если пользователь заблокирован в Azure AD, его экран будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5b0b8-134">If a user is locked out of Azure AD, their screen looks similar to the one that follows:</span></span>

  ![Блокировка в Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="5b0b8-136">Для других учетных записей Майкрософт экран будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5b0b8-136">For other Microsoft accounts, their screen looks similar to the one that follows:</span></span>

  ![Блокировка учетной записи Майкрософт](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="5b0b8-138">Сведения о сбросе пароля в Azure Active Directory см. в статье [Самостоятельный сброс пароля в Azure AD для ИТ-специалистов](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="5b0b8-138">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="5b0b8-139">Если вы являетесь администратором Azure AD, возможно, вам понадобится использовать [Windows Hello](https://www.microsoft.com/windows/windows-hello), чтобы избежать создания традиционных паролей пользователями.</span><span class="sxs-lookup"><span data-stu-id="5b0b8-139">If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="5b0b8-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5b0b8-140">Next steps</span></span>

* [<span data-ttu-id="5b0b8-141">Как изменить свой пароль</span><span class="sxs-lookup"><span data-stu-id="5b0b8-141">How to update your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="5b0b8-142">Основы управления удостоверениями Azure</span><span class="sxs-lookup"><span data-stu-id="5b0b8-142">The fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="5b0b8-143">Приступая к работе с Azure</span><span class="sxs-lookup"><span data-stu-id="5b0b8-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


