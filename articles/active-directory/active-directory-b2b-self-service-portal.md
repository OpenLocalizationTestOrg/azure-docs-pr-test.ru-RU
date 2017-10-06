---
title: "портал регистрации aaaSelf службы для совместной работы Azure Active Directory B2B | Документы Microsoft"
description: "Совместная работа Azure Active Directory B2B поддерживает связей между компаниями, позволяя корпоративным приложениям доступа tooselectively деловых партнеров"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="2f357-103">Самостоятельная регистрация на портале для службы совместной работы Azure AD B2B</span><span class="sxs-lookup"><span data-stu-id="2f357-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="2f357-104">Клиент может выполнить много с hello встроенных функций, предоставляемых через наших ИТ-администратору [портал Azure](https://portal.azure.com) и на нашем [панели доступа приложения](https://myapps.microsoft.com) для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="2f357-104">Customers can do a lot with hello built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="2f357-105">Но мы также помнить, что бизнеса требуется рабочего процесса адаптации hello toocustomize для B2B пользователей toofit их с требованиями организации.</span><span class="sxs-lookup"><span data-stu-id="2f357-105">But we are also aware that businesses need toocustomize hello onboarding workflow for B2B users toofit their organization’s needs.</span></span> <span data-ttu-id="2f357-106">Они могут это сделать с помощью [нашего интерфейса API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="2f357-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="2f357-107">Обсуждая этот вопрос с нашими клиентами, мы выяснили, что есть одна общая потребность, которая преобладает над всеми остальными.</span><span class="sxs-lookup"><span data-stu-id="2f357-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="2f357-108">Hello приглашении организации может не знать заранее, кто hello пребывание, требуется доступ к ресурсам tootheir отдельных внешними участниками.</span><span class="sxs-lookup"><span data-stu-id="2f357-108">hello inviting organization may not know ahead of time who hello individual external collaborators are who need access tootheir resources.</span></span> <span data-ttu-id="2f357-109">Нужно было способом для пользователей от компаний-партнеров слишком зарегистрироваться сами набор политик, hello приглашении организации элементов управления.</span><span class="sxs-lookup"><span data-stu-id="2f357-109">They wanted a way for users from partner companies too sign themselves up with a set of policies that hello inviting organization controls.</span></span> <span data-ttu-id="2f357-110">Такой сценарий можно реализовать с помощью наших API-интерфейсов, что мы и сделали в опубликованном на GitHub проекте: [пример проекта на портале GitHub](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="2f357-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="2f357-111">Наш проект Github показан способ организации можно использовать нашими API и предоставляют возможность регистрации на основе политик, самообслуживания для их доверенных партнеров, с помощью правила, определяющие приложения hello, они могут получить доступ.</span><span class="sxs-lookup"><span data-stu-id="2f357-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine hello apps they can access.</span></span> <span data-ttu-id="2f357-112">Партнер пользователи могут получить tooresources доступ, им необходимы, безопасно, без необходимости hello приглашении освоить toomanually организации их.</span><span class="sxs-lookup"><span data-stu-id="2f357-112">Partner users can get access tooresources when they need them, securely, without requiring hello inviting organization toomanually onboard them.</span></span> <span data-ttu-id="2f357-113">Можно легко развернуть проект hello в подписку Azure по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="2f357-113">You can easily deploy hello project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="2f357-114">Код "как есть"</span><span class="sxs-lookup"><span data-stu-id="2f357-114">As-is code</span></span>

<span data-ttu-id="2f357-115">Помните, что этот код предоставляется для использования toodemonstrate образец hello Azure Active Directory B2B приглашения API.</span><span class="sxs-lookup"><span data-stu-id="2f357-115">Remember that this code is made available as a sample toodemonstrate usage of hello Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="2f357-116">Перед развертыванием в рабочем сценарии его должна настроить и проверить ваша команда разработчиков или ваш партнер.</span><span class="sxs-lookup"><span data-stu-id="2f357-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f357-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f357-117">Next steps</span></span>

<span data-ttu-id="2f357-118">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="2f357-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="2f357-119">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="2f357-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="2f357-120">Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?</span><span class="sxs-lookup"><span data-stu-id="2f357-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="2f357-121">Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f357-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="2f357-122">элементы Hello hello электронное приглашение B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="2f357-122">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="2f357-123">Активация приглашения службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="2f357-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="2f357-124">Руководство по лицензированию службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="2f357-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="2f357-125">Устранение неполадок службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="2f357-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="2f357-126">Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="2f357-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="2f357-127">Многофакторная идентификация для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="2f357-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="2f357-128">Добавление пользователей службы совместной работы B2B без приглашения</span><span class="sxs-lookup"><span data-stu-id="2f357-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="2f357-129">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f357-129">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)