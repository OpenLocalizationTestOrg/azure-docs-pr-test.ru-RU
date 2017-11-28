---
title: "Лицензирование: Azure AD SSPR | Документация Майкрософт"
description: "Требования к лицензированию самостоятельного сброса пароля в Azure AD"
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
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="a49b0-103">Требования к лицензированию самостоятельного сброса пароля в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a49b0-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="a49b0-104">Чтобы toofunction сброса пароля Azure AD вы **необходимо наличие по крайней мере один лицензии в вашей организации**.</span><span class="sxs-lookup"><span data-stu-id="a49b0-104">In order for Azure AD Password Reset toofunction, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="a49b0-105">Не выполняют лицензирования на hello интерфейса для сброса пароля пользователя.</span><span class="sxs-lookup"><span data-stu-id="a49b0-105">We do not enforce per-user licensing on hello password reset experience.</span></span> <span data-ttu-id="a49b0-106">соответствие toomaintain лицензионном соглашении корпорации Майкрософт, необходимо tooassign лицензий tooany пользователей, которые используют функции premium.</span><span class="sxs-lookup"><span data-stu-id="a49b0-106">toomaintain compliance with your Microsoft licensing agreement, you need tooassign licenses tooany users that use premium features.</span></span>

* <span data-ttu-id="a49b0-107">**Полностью облачные пользователи.** Любой платный номер SKU Office 365 (O365) или Azure AD Basic.</span><span class="sxs-lookup"><span data-stu-id="a49b0-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="a49b0-108">**Облачные пользователи** или **локальные пользователи.** Azure AD Premium P1 или P2, Enterprise Mobility + Security (EMS) или Secure Productive Enterprise (SPE).</span><span class="sxs-lookup"><span data-stu-id="a49b0-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="a49b0-109">Лицензии, необходимые для компонента обратной записи паролей</span><span class="sxs-lookup"><span data-stu-id="a49b0-109">Licenses required for password writeback</span></span>

<span data-ttu-id="a49b0-110">toouse обратной записи паролей, необходимо иметь одно из следующих лицензии, назначенные в вашем клиенте hello.</span><span class="sxs-lookup"><span data-stu-id="a49b0-110">toouse password writeback, you must have one of hello following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="a49b0-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="a49b0-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="a49b0-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="a49b0-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="a49b0-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="a49b0-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="a49b0-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="a49b0-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="a49b0-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="a49b0-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="a49b0-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="a49b0-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="a49b0-117">Office 365 автономный планов лицензирования **не поддерживают обратную запись паролей** и требует выполнения одного из предыдущих планы для этой функции toowork hello.</span><span class="sxs-lookup"><span data-stu-id="a49b0-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of hello preceding plans for this functionality toowork.</span></span>

<span data-ttu-id="a49b0-118">Дополнительно лицензирования, включая затраты на можно найти на следующих страницах hello</span><span class="sxs-lookup"><span data-stu-id="a49b0-118">Additional licensing info including costs can be found on hello following pages</span></span>

* <span data-ttu-id="a49b0-119">[Сайт с ценами на Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="a49b0-119">[Azure Active Directory Pricing site](https://azure.microsoft.com/pricing/details/active-directory/)</span></span>
* <span data-ttu-id="a49b0-120">[Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security).</span><span class="sxs-lookup"><span data-stu-id="a49b0-120">[Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)</span></span>
* <span data-ttu-id="a49b0-121">[Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="a49b0-121">[Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)</span></span>

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="a49b0-122">Включение группового и пользовательского лицензирования</span><span class="sxs-lookup"><span data-stu-id="a49b0-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="a49b0-123">Azure AD теперь поддерживает групповые лицензирования допускающему лицензии tooassign администраторов в массовой tooa группы пользователей, а не их назначения по одному.</span><span class="sxs-lookup"><span data-stu-id="a49b0-123">Azure AD now supports group-based licensing allowing administrators tooassign licenses in bulk tooa group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="a49b0-124">Назначение лицензий группе пользователей в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a49b0-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="a49b0-125">Некоторые службы Майкрософт недоступны во всех расположениях.</span><span class="sxs-lookup"><span data-stu-id="a49b0-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="a49b0-126">Перед tooa пользователя можно назначить лицензию, Здравствуйте, администратор должен указать свойство «Место использования» hello hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="a49b0-126">Before a license can be assigned tooa user, hello administrator must specify hello “Usage location” property on hello user.</span></span> <span data-ttu-id="a49b0-127">Назначение лицензий можно сделать записью > профиль > раздел параметров hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a49b0-127">Assignment of licenses can be done under User > Profile > Settings section in hello Azure portal.</span></span> <span data-ttu-id="a49b0-128">**При использовании Назначение группы лицензирования, все пользователи, не указано место использования наследуют hello расположение каталога hello.**</span><span class="sxs-lookup"><span data-stu-id="a49b0-128">**When using group license assignment, any users without a usage location specified inherit hello location of hello directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="a49b0-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a49b0-129">Next steps</span></span>

<span data-ttu-id="a49b0-130">Привет, следующие ссылки предоставляют дополнительную информацию об пароль с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="a49b0-130">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="a49b0-131">[**Быстрое начало работы с самостоятельным сбросом пароля в Azure AD**](active-directory-passwords-getting-started.md). Запуск и выполнение службы самостоятельного управления паролями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a49b0-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="a49b0-132">[**Данные** ](active-directory-passwords-data.md) — понять hello данные, которые не требуется и как она используется для управления паролями</span><span class="sxs-lookup"><span data-stu-id="a49b0-132">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="a49b0-133">[**Развертывание** ](active-directory-passwords-best-practices.md) -планирование и развертывание SSPR tooyour пользователей с помощью hello рекомендации по следующему адресу</span><span class="sxs-lookup"><span data-stu-id="a49b0-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="a49b0-134">[**Настройка** ](active-directory-passwords-customize.md) -настроить hello внешний вид и поведение hello SSPR взаимодействие с вашей компании.</span><span class="sxs-lookup"><span data-stu-id="a49b0-134">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="a49b0-135">[**Reporting options for Azure AD password management**](active-directory-passwords-reporting.md) (Параметры отчетов для управления паролями Azure AD). Определяйте, кто и когда использовал функцию SSPR.</span><span class="sxs-lookup"><span data-stu-id="a49b0-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="a49b0-136">[**Технические глубокое погружение** ](active-directory-passwords-how-it-works.md) -перейдите за занавесом toounderstand hello принцип работы</span><span class="sxs-lookup"><span data-stu-id="a49b0-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="a49b0-137">[**Вопросы и ответы об управлении паролями**](active-directory-passwords-faq.md). Как?</span><span class="sxs-lookup"><span data-stu-id="a49b0-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="a49b0-138">Почему?</span><span class="sxs-lookup"><span data-stu-id="a49b0-138">Why?</span></span> <span data-ttu-id="a49b0-139">Что?</span><span class="sxs-lookup"><span data-stu-id="a49b0-139">What?</span></span> <span data-ttu-id="a49b0-140">Где?</span><span class="sxs-lookup"><span data-stu-id="a49b0-140">Where?</span></span> <span data-ttu-id="a49b0-141">Кто?</span><span class="sxs-lookup"><span data-stu-id="a49b0-141">Who?</span></span> <span data-ttu-id="a49b0-142">Когда?</span><span class="sxs-lookup"><span data-stu-id="a49b0-142">When?</span></span> <span data-ttu-id="a49b0-143">-Ответы tooquestions требуется, чтобы tooask</span><span class="sxs-lookup"><span data-stu-id="a49b0-143">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="a49b0-144">[**Устранение неполадок** ](active-directory-passwords-troubleshoot.md) -Узнайте, как tooresolve распространенные проблемы, мы увидим с SSPR</span><span class="sxs-lookup"><span data-stu-id="a49b0-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

