---
title: "Требования к данным для самостоятельного сброса пароля Azure AD | Документация Майкрософт"
description: "Требования к данным для самостоятельного сброса пароля Azure AD и информация о том, как их выполнить"
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
ms.openlocfilehash: 2d1afd2d1265b371e0d311ed70fffbc55874b0a7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="8c907-103">Развертывание сброса пароля без регистрации пользователя</span><span class="sxs-lookup"><span data-stu-id="8c907-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="8c907-104">Для развертывания функции самостоятельного сброса пароля нужно указать данные аутентификации.</span><span class="sxs-lookup"><span data-stu-id="8c907-104">Deploying Self-Service Password Reset (SSPR) requires authentication data to be present.</span></span> <span data-ttu-id="8c907-105">Хотя в некоторых организациях пользователи вводят свои данные аутентификации самостоятельно, в других используется синхронизация существующих данных в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c907-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer to synchronize with existing data in Active Directory.</span></span> <span data-ttu-id="8c907-106">Если правильно отформатировать данные в локальном каталоге и настроить [Azure AD Connect, используя стандартные параметры](./connect/active-directory-aadconnect-get-started-express.md), эти данные становятся доступным для Azure AD и функции самостоятельного сброса паролей без участия пользователя.</span><span class="sxs-lookup"><span data-stu-id="8c907-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available to Azure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="8c907-107">Для правильной работы все номера телефонов должны быть в формате "+код страны – номер телефона". Например: +1 4255551234.</span><span class="sxs-lookup"><span data-stu-id="8c907-107">Any phone numbers must be in the format +CountryCode PhoneNumber Example: +1 4255551234 to work properly.</span></span>

> [!NOTE]
> <span data-ttu-id="8c907-108">Функция сброса пароля не поддерживает добавочные номера.</span><span class="sxs-lookup"><span data-stu-id="8c907-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="8c907-109">Даже добавочные номера в формате +1 4255551234X12345 будут удаляться.</span><span class="sxs-lookup"><span data-stu-id="8c907-109">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="8c907-110">Заполненные поля</span><span class="sxs-lookup"><span data-stu-id="8c907-110">Fields populated</span></span>

<span data-ttu-id="8c907-111">Если вы используете параметры по умолчанию, в Azure AD Connect выполняются следующие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="8c907-111">If you use the default settings in Azure AD Connect the following mappings are made.</span></span>

| <span data-ttu-id="8c907-112">Локальная служба AD</span><span class="sxs-lookup"><span data-stu-id="8c907-112">On-premises AD</span></span> | <span data-ttu-id="8c907-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c907-113">Azure AD</span></span> | <span data-ttu-id="8c907-114">Контактные данные проверки подлинности Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c907-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8c907-115">TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="8c907-115">telephoneNumber</span></span> | <span data-ttu-id="8c907-116">Рабочий телефон</span><span class="sxs-lookup"><span data-stu-id="8c907-116">Office phone</span></span> | <span data-ttu-id="8c907-117">Дополнительный телефон</span><span class="sxs-lookup"><span data-stu-id="8c907-117">Alternate phone</span></span> |
| <span data-ttu-id="8c907-118">mobile</span><span class="sxs-lookup"><span data-stu-id="8c907-118">mobile</span></span> | <span data-ttu-id="8c907-119">Мобильный телефон</span><span class="sxs-lookup"><span data-stu-id="8c907-119">Mobile phone</span></span> | <span data-ttu-id="8c907-120">Номер телефона</span><span class="sxs-lookup"><span data-stu-id="8c907-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="8c907-121">Контрольные вопросы и ответы на них</span><span class="sxs-lookup"><span data-stu-id="8c907-121">Security questions and answers</span></span>

<span data-ttu-id="8c907-122">Контрольные вопросы и ответы на них надежно хранятся в клиенте Azure AD. Эти данные доступны пользователям только на [портале регистрации SSPR](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="8c907-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible to users via the [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="8c907-123">Администраторы не могут видеть или изменять содержимое вопросов и ответов других пользователей.</span><span class="sxs-lookup"><span data-stu-id="8c907-123">Administrators can't see or modify the contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="8c907-124">Что происходит, когда пользователь проходит регистрацию?</span><span class="sxs-lookup"><span data-stu-id="8c907-124">What happens when a user registers</span></span>

<span data-ttu-id="8c907-125">Когда пользователь регистрируется, на странице регистрации будут заполнены следующие поля:</span><span class="sxs-lookup"><span data-stu-id="8c907-125">When a user registers, the registration page sets the following fields:</span></span>

* <span data-ttu-id="8c907-126">Телефон для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="8c907-126">Authentication Phone</span></span>
* <span data-ttu-id="8c907-127">Адрес электронной почты для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="8c907-127">Authentication Email</span></span>
* <span data-ttu-id="8c907-128">Контрольные вопросы и ответы на них</span><span class="sxs-lookup"><span data-stu-id="8c907-128">Security Questions and Answers</span></span>

<span data-ttu-id="8c907-129">Если вы указали значения для полей **Мобильный телефон** или **Запасной адрес электронной почты**, пользователи могут использовать их для сброса паролей, даже если они еще не прошли регистрацию в службе.</span><span class="sxs-lookup"><span data-stu-id="8c907-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values to reset their passwords, even if they haven't registered for the service.</span></span> <span data-ttu-id="8c907-130">Кроме того, эти значения будут отображаться для пользователей при первой регистрации, и они смогут изменить их при необходимости.</span><span class="sxs-lookup"><span data-stu-id="8c907-130">In addition, users see those values when registering for the first time, and modify them if they wish.</span></span> <span data-ttu-id="8c907-131">После успешной регистрации эти значения будут храниться в полях **Телефон для проверки подлинности** и **Адрес электронной почты для проверки подлинности** (их нельзя будет изменить).</span><span class="sxs-lookup"><span data-stu-id="8c907-131">After they successfully register, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="8c907-132">Установка и считывание данных аутентификации с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c907-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="8c907-133">С помощью PowerShell можно заполнить следующие поля</span><span class="sxs-lookup"><span data-stu-id="8c907-133">The following fields can be set using PowerShell</span></span>

* <span data-ttu-id="8c907-134">Запасной адрес электронной почты</span><span class="sxs-lookup"><span data-stu-id="8c907-134">Alternate Email</span></span>
* <span data-ttu-id="8c907-135">Мобильный телефон</span><span class="sxs-lookup"><span data-stu-id="8c907-135">Mobile Phone</span></span>
* <span data-ttu-id="8c907-136">Рабочий телефон — его можно указать, только если это значение не синхронизируется с локальным каталогом</span><span class="sxs-lookup"><span data-stu-id="8c907-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="8c907-137">Использование PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="8c907-137">Using PowerShell V1</span></span>

<span data-ttu-id="8c907-138">Чтобы начать работу, необходимо [скачать и установить модуль Azure AD PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="8c907-138">To get started, you need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="8c907-139">После его установки вы можете выполнить следующие процедуры по настройке каждого поля.</span><span class="sxs-lookup"><span data-stu-id="8c907-139">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="8c907-140">Настройка данных аутентификации с помощью PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="8c907-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="8c907-141">Чтение данных аутентификации с помощью PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="8c907-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-the-commands-that-follow"></a><span data-ttu-id="8c907-142">Телефон и адрес электронной почты для аутентификации можно прочитать только с помощью следующих команд PowerShell V1:</span><span class="sxs-lookup"><span data-stu-id="8c907-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using the commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="8c907-143">Использование PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="8c907-143">Using PowerShell V2</span></span>

<span data-ttu-id="8c907-144">Чтобы начать работу, необходимо [скачать и установить модуль Azure AD PowerShell V2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="8c907-144">To get started, you need to [download and install the Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="8c907-145">После его установки вы можете выполнить следующие процедуры по настройке каждого поля.</span><span class="sxs-lookup"><span data-stu-id="8c907-145">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

<span data-ttu-id="8c907-146">Чтобы быстро установить одну из последних версий PowerShell, поддерживающую Install-Module, выполните приведенные ниже команды (первая строка просто проверяет наличие PowerShell).</span><span class="sxs-lookup"><span data-stu-id="8c907-146">To install quickly from recent versions of PowerShell that support Install-Module, run these commands (the first line simply checks to see if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="8c907-147">Настройка данных аутентификации с помощью PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="8c907-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="8c907-148">Чтение данных аутентификации с помощью PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="8c907-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="8c907-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8c907-149">Next steps</span></span>

<span data-ttu-id="8c907-150">Дополнительные сведения о сбросе пароля с помощью Azure AD см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="8c907-150">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="8c907-151">[**Быстрое начало работы с самостоятельным сбросом пароля в Azure AD**](active-directory-passwords-getting-started.md). Запуск и выполнение службы самостоятельного управления паролями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c907-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="8c907-152">[**Licensing requirements for Azure AD self-service password reset**](active-directory-passwords-licensing.md) (Требования к лицензированию самостоятельного сброса пароля в Azure AD). Сведения о настройке лицензирования Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c907-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="8c907-153">[**Развертывание функции сброса паролей для пользователей**](active-directory-passwords-best-practices.md). Рекомендации по планированию и развертыванию SSPR для пользователей.</span><span class="sxs-lookup"><span data-stu-id="8c907-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="8c907-154">[**Настройка компонентов управления паролями в соответствии с требованиями организации**](active-directory-passwords-customize.md). Сведения о настройке интерфейса и параметров использования SSPR для организации.</span><span class="sxs-lookup"><span data-stu-id="8c907-154">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="8c907-155">[**Политики и ограничения для паролей в Azure Active Directory**](active-directory-passwords-policy.md). Общие сведения и информация об установке политик паролей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c907-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="8c907-156">[**Reporting options for Azure AD password management**](active-directory-passwords-reporting.md) (Параметры отчетов для управления паролями Azure AD). Определяйте, кто и когда использовал функцию SSPR.</span><span class="sxs-lookup"><span data-stu-id="8c907-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="8c907-157">[**Как работает управление паролями в Azure Active Directory**](active-directory-passwords-how-it-works.md). Сведения о принципе работы управления паролями.</span><span class="sxs-lookup"><span data-stu-id="8c907-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="8c907-158">[**Вопросы и ответы об управлении паролями**](active-directory-passwords-faq.md). Как?</span><span class="sxs-lookup"><span data-stu-id="8c907-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="8c907-159">Почему?</span><span class="sxs-lookup"><span data-stu-id="8c907-159">Why?</span></span> <span data-ttu-id="8c907-160">Что?</span><span class="sxs-lookup"><span data-stu-id="8c907-160">What?</span></span> <span data-ttu-id="8c907-161">Где?</span><span class="sxs-lookup"><span data-stu-id="8c907-161">Where?</span></span> <span data-ttu-id="8c907-162">Кто?</span><span class="sxs-lookup"><span data-stu-id="8c907-162">Who?</span></span> <span data-ttu-id="8c907-163">Когда?</span><span class="sxs-lookup"><span data-stu-id="8c907-163">When?</span></span> <span data-ttu-id="8c907-164">Здесь приведены ответы на интересующие вас вопросы.</span><span class="sxs-lookup"><span data-stu-id="8c907-164">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="8c907-165">[**Устранение неполадок, связанных с управлением паролями**](active-directory-passwords-troubleshoot.md). Сведения об устранении распространенных проблем с SSPR.</span><span class="sxs-lookup"><span data-stu-id="8c907-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
