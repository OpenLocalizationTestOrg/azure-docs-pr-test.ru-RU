---
title: "Требования к данным для самостоятельного сброса пароля Azure AD | Документация Майкрософт"
description: "Сброс данных требования для самостоятельного пароля Azure AD и как toosatisfy их"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="42f50-103">Развертывание сброса пароля без регистрации пользователя</span><span class="sxs-lookup"><span data-stu-id="42f50-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="42f50-104">Развертывание самостоятельного сброса пароля (SSPR) требуется наличие toobe данных проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="42f50-104">Deploying Self-Service Password Reset (SSPR) requires authentication data toobe present.</span></span> <span data-ttu-id="42f50-105">В некоторых организациях есть их пользователям вводить свои данные проверки подлинности самостоятельно, но многие организации предпочитают toosynchronize с существующие данные в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42f50-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer toosynchronize with existing data in Active Directory.</span></span> <span data-ttu-id="42f50-106">Если имеются правильно отформатированные данные в ваш локальный каталог и настроить [Azure AD Connect, используя стандартные параметры](./connect/active-directory-aadconnect-get-started-express.md), что данных становится доступной tooAzure AD и SSPR, без необходимости участия пользователя.</span><span class="sxs-lookup"><span data-stu-id="42f50-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available tooAzure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="42f50-107">Все телефонные номера должен быть в формате hello + CountryCode PhoneNumber пример: 4255551234 + 1 toowork должным образом.</span><span class="sxs-lookup"><span data-stu-id="42f50-107">Any phone numbers must be in hello format +CountryCode PhoneNumber Example: +1 4255551234 toowork properly.</span></span>

> [!NOTE]
> <span data-ttu-id="42f50-108">Функция сброса пароля не поддерживает добавочные номера.</span><span class="sxs-lookup"><span data-stu-id="42f50-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="42f50-109">Даже в формате 12345 hello 4255551234 + 1 X расширения будут удалены перед установкой hello.</span><span class="sxs-lookup"><span data-stu-id="42f50-109">Even in hello +1 4255551234X12345 format, extensions are removed before hello call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="42f50-110">Заполненные поля</span><span class="sxs-lookup"><span data-stu-id="42f50-110">Fields populated</span></span>

<span data-ttu-id="42f50-111">Сопоставление производится, если используются параметры по умолчанию hello в Azure AD Connect hello следующие.</span><span class="sxs-lookup"><span data-stu-id="42f50-111">If you use hello default settings in Azure AD Connect hello following mappings are made.</span></span>

| <span data-ttu-id="42f50-112">Локальная служба AD</span><span class="sxs-lookup"><span data-stu-id="42f50-112">On-premises AD</span></span> | <span data-ttu-id="42f50-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="42f50-113">Azure AD</span></span> | <span data-ttu-id="42f50-114">Контактные данные проверки подлинности Azure AD</span><span class="sxs-lookup"><span data-stu-id="42f50-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="42f50-115">TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="42f50-115">telephoneNumber</span></span> | <span data-ttu-id="42f50-116">Рабочий телефон</span><span class="sxs-lookup"><span data-stu-id="42f50-116">Office phone</span></span> | <span data-ttu-id="42f50-117">Дополнительный телефон</span><span class="sxs-lookup"><span data-stu-id="42f50-117">Alternate phone</span></span> |
| <span data-ttu-id="42f50-118">mobile</span><span class="sxs-lookup"><span data-stu-id="42f50-118">mobile</span></span> | <span data-ttu-id="42f50-119">Мобильный телефон</span><span class="sxs-lookup"><span data-stu-id="42f50-119">Mobile phone</span></span> | <span data-ttu-id="42f50-120">Номер телефона</span><span class="sxs-lookup"><span data-stu-id="42f50-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="42f50-121">Контрольные вопросы и ответы на них</span><span class="sxs-lookup"><span data-stu-id="42f50-121">Security questions and answers</span></span>

<span data-ttu-id="42f50-122">Вопросы и ответы, надежно сохранены в клиенте Azure AD и являются только доступный toousers через hello [портал регистрации SSPR](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="42f50-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible toousers via hello [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="42f50-123">Администраторы не может просматривать или изменять содержимое hello другим пользователям вопросов и ответов.</span><span class="sxs-lookup"><span data-stu-id="42f50-123">Administrators can't see or modify hello contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="42f50-124">Что происходит, когда пользователь проходит регистрацию?</span><span class="sxs-lookup"><span data-stu-id="42f50-124">What happens when a user registers</span></span>

<span data-ttu-id="42f50-125">Когда пользователь регистрирует, страница регистрации hello задает hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="42f50-125">When a user registers, hello registration page sets hello following fields:</span></span>

* <span data-ttu-id="42f50-126">Телефон для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="42f50-126">Authentication Phone</span></span>
* <span data-ttu-id="42f50-127">Адрес электронной почты для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="42f50-127">Authentication Email</span></span>
* <span data-ttu-id="42f50-128">Контрольные вопросы и ответы на них</span><span class="sxs-lookup"><span data-stu-id="42f50-128">Security Questions and Answers</span></span>

<span data-ttu-id="42f50-129">При указании значения для **мобильный телефон** или **запасной адрес электронной почты**, пользователи могут сразу же использовать эти значения tooreset свои пароли, даже если они еще не зарегистрированы для службы hello.</span><span class="sxs-lookup"><span data-stu-id="42f50-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values tooreset their passwords, even if they haven't registered for hello service.</span></span> <span data-ttu-id="42f50-130">Кроме того пользователи см. Эти значения при регистрации для hello впервые и при желании измените их.</span><span class="sxs-lookup"><span data-stu-id="42f50-130">In addition, users see those values when registering for hello first time, and modify them if they wish.</span></span> <span data-ttu-id="42f50-131">После успешной регистрации, эти значения будут сохраняться в hello **телефон для аутентификации** и **электронной почты для проверки подлинности** соответственно.</span><span class="sxs-lookup"><span data-stu-id="42f50-131">After they successfully register, these values will be persisted in hello **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="42f50-132">Установка и считывание данных аутентификации с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="42f50-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="42f50-133">Hello следующие поля можно задать с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="42f50-133">hello following fields can be set using PowerShell</span></span>

* <span data-ttu-id="42f50-134">Запасной адрес электронной почты</span><span class="sxs-lookup"><span data-stu-id="42f50-134">Alternate Email</span></span>
* <span data-ttu-id="42f50-135">Мобильный телефон</span><span class="sxs-lookup"><span data-stu-id="42f50-135">Mobile Phone</span></span>
* <span data-ttu-id="42f50-136">Рабочий телефон — его можно указать, только если это значение не синхронизируется с локальным каталогом</span><span class="sxs-lookup"><span data-stu-id="42f50-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="42f50-137">Использование PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="42f50-137">Using PowerShell V1</span></span>

<span data-ttu-id="42f50-138">tooget работы, необходимо слишком[Загрузите и установите модуль Azure AD PowerShell hello](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="42f50-138">tooget started, you need too[download and install hello Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="42f50-139">После его установки, вы можете использовать hello описанных ниже tooconfigure каждого поля.</span><span class="sxs-lookup"><span data-stu-id="42f50-139">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="42f50-140">Настройка данных аутентификации с помощью PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="42f50-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="42f50-141">Чтение данных аутентификации с помощью PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="42f50-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a><span data-ttu-id="42f50-142">Телефон для аутентификации и электронной почты для проверки подлинности могут быть прочитаны только с помощью Powershell V1 hello с помощью команды ниже</span><span class="sxs-lookup"><span data-stu-id="42f50-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using hello commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="42f50-143">Использование PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="42f50-143">Using PowerShell V2</span></span>

<span data-ttu-id="42f50-144">tooget работы, необходимо слишком[загрузить и установить модуль PowerShell Azure AD V2 hello](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="42f50-144">tooget started, you need too[download and install hello Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="42f50-145">После его установки, вы можете использовать hello описанных ниже tooconfigure каждого поля.</span><span class="sxs-lookup"><span data-stu-id="42f50-145">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

<span data-ttu-id="42f50-146">tooinstall быстро из последних версий PowerShell, поддерживающие Install-Module, выполняемых команд (первая строка hello просто проверяет toosee Если уже установлена):</span><span class="sxs-lookup"><span data-stu-id="42f50-146">tooinstall quickly from recent versions of PowerShell that support Install-Module, run these commands (hello first line simply checks toosee if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="42f50-147">Настройка данных аутентификации с помощью PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="42f50-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="42f50-148">Чтение данных аутентификации с помощью PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="42f50-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="42f50-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="42f50-149">Next steps</span></span>

<span data-ttu-id="42f50-150">Привет, следующие ссылки предоставляют дополнительную информацию об пароль с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="42f50-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="42f50-151">[**Быстрое начало работы с самостоятельным сбросом пароля в Azure AD**](active-directory-passwords-getting-started.md). Запуск и выполнение службы самостоятельного управления паролями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42f50-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="42f50-152">[**Licensing requirements for Azure AD self-service password reset**](active-directory-passwords-licensing.md) (Требования к лицензированию самостоятельного сброса пароля в Azure AD). Сведения о настройке лицензирования Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42f50-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="42f50-153">[**Развертывание** ](active-directory-passwords-best-practices.md) -планирование и развертывание SSPR tooyour пользователей с помощью hello рекомендации по следующему адресу</span><span class="sxs-lookup"><span data-stu-id="42f50-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="42f50-154">[**Настройка** ](active-directory-passwords-customize.md) -настроить hello внешний вид и поведение hello SSPR взаимодействие с вашей компании.</span><span class="sxs-lookup"><span data-stu-id="42f50-154">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="42f50-155">[**Политики и ограничения для паролей в Azure Active Directory**](active-directory-passwords-policy.md). Общие сведения и информация об установке политик паролей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42f50-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="42f50-156">[**Reporting options for Azure AD password management**](active-directory-passwords-reporting.md) (Параметры отчетов для управления паролями Azure AD). Определяйте, кто и когда использовал функцию SSPR.</span><span class="sxs-lookup"><span data-stu-id="42f50-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="42f50-157">[**Технические глубокое погружение** ](active-directory-passwords-how-it-works.md) -перейдите за занавесом toounderstand hello принцип работы</span><span class="sxs-lookup"><span data-stu-id="42f50-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="42f50-158">[**Вопросы и ответы об управлении паролями**](active-directory-passwords-faq.md). Как?</span><span class="sxs-lookup"><span data-stu-id="42f50-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="42f50-159">Почему?</span><span class="sxs-lookup"><span data-stu-id="42f50-159">Why?</span></span> <span data-ttu-id="42f50-160">Что?</span><span class="sxs-lookup"><span data-stu-id="42f50-160">What?</span></span> <span data-ttu-id="42f50-161">Где?</span><span class="sxs-lookup"><span data-stu-id="42f50-161">Where?</span></span> <span data-ttu-id="42f50-162">Кто?</span><span class="sxs-lookup"><span data-stu-id="42f50-162">Who?</span></span> <span data-ttu-id="42f50-163">Когда?</span><span class="sxs-lookup"><span data-stu-id="42f50-163">When?</span></span> <span data-ttu-id="42f50-164">-Ответы tooquestions требуется, чтобы tooask</span><span class="sxs-lookup"><span data-stu-id="42f50-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="42f50-165">[**Устранение неполадок** ](active-directory-passwords-troubleshoot.md) -Узнайте, как tooresolve распространенные проблемы, мы увидим с SSPR</span><span class="sxs-lookup"><span data-stu-id="42f50-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
