---
title: "Принципы работы Azure Multi-Factor Authentication"
description: "Azure Multi-Factor Authentication помогает защитить доступ к данным и приложениям, при этом не усложняя процесс входа пользователя в систему. Эта служба предлагает дополнительную защиту за счет дополнительного способа проверки подлинности и, используя ряд простых способов проверки подлинности, обеспечивает строгую проверку."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 6fee02885cc76b3a4fdad11e8702f623d6fe6597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="4be4b-104">Принципы работы службы Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="4be4b-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="4be4b-105">Безопасность двухшаговой проверки подлинности заключается в многоуровневом подходе.</span><span class="sxs-lookup"><span data-stu-id="4be4b-105">The security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="4be4b-106">Нарушения нескольких факторов проверки подлинности представляет нетривиальную задачу для злоумышленников.</span><span class="sxs-lookup"><span data-stu-id="4be4b-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="4be4b-107">Даже если злоумышленнику удается получить пароль пользователя, им нельзя воспользоваться без доверенного устройства.</span><span class="sxs-lookup"><span data-stu-id="4be4b-107">Even if an attacker manages to learn the user's password, it is useless without also having possession of the trusted device.</span></span> 

![Подтверждение](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="4be4b-109">Azure Multi-Factor Authentication помогает защитить доступ к данным и приложениям, при этом не усложняя процесс входа пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="4be4b-109">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="4be4b-110">Эта служба предлагает дополнительную защиту за счет дополнительного способа проверки подлинности и, используя ряд простых способов проверки подлинности, обеспечивает строгую проверку.</span><span class="sxs-lookup"><span data-stu-id="4be4b-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="4be4b-111">Методы, доступные для двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="4be4b-111">Methods available for two-step verification</span></span>
<span data-ttu-id="4be4b-112">При входе в систему пользователю отправляется запрос дополнительной проверки.</span><span class="sxs-lookup"><span data-stu-id="4be4b-112">When a user signs in, an additional verification is sent to the user.</span></span>  <span data-ttu-id="4be4b-113">Ниже приведены методы, которые могут использоваться для такой второй проверки.</span><span class="sxs-lookup"><span data-stu-id="4be4b-113">The following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="4be4b-114">Метод проверки</span><span class="sxs-lookup"><span data-stu-id="4be4b-114">Verification Method</span></span> | <span data-ttu-id="4be4b-115">Описание</span><span class="sxs-lookup"><span data-stu-id="4be4b-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4be4b-116">Телефонный звонок</span><span class="sxs-lookup"><span data-stu-id="4be4b-116">Phone call</span></span> |<span data-ttu-id="4be4b-117">Вызов направляется на зарегистрированный телефон пользователя.</span><span class="sxs-lookup"><span data-stu-id="4be4b-117">A call is placed to a user’s registered phone.</span></span> <span data-ttu-id="4be4b-118">При необходимости пользователь вводит ПИН-код и нажимает клавишу #.</span><span class="sxs-lookup"><span data-stu-id="4be4b-118">The user enters a PIN if necessary then presses the # key.</span></span> |
| <span data-ttu-id="4be4b-119">Текстовое сообщение</span><span class="sxs-lookup"><span data-stu-id="4be4b-119">Text message</span></span> |<span data-ttu-id="4be4b-120">На мобильный телефон пользователя отправляется текстовое сообщение с шестизначным кодом,</span><span class="sxs-lookup"><span data-stu-id="4be4b-120">A text message is sent to a user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="4be4b-121">который нужно ввести на странице входа.</span><span class="sxs-lookup"><span data-stu-id="4be4b-121">The user enters this code on the sign-in page.</span></span> |
| <span data-ttu-id="4be4b-122">Уведомление от мобильного приложения</span><span class="sxs-lookup"><span data-stu-id="4be4b-122">Mobile app notification</span></span> |<span data-ttu-id="4be4b-123">На смартфон пользователя отправляется запрос о выполнении проверки.</span><span class="sxs-lookup"><span data-stu-id="4be4b-123">A verification request is sent to a user’s smart phone.</span></span> <span data-ttu-id="4be4b-124">При необходимости пользователь вводит ПИН-код, а затем выбирает **Проверка** в мобильном приложении.</span><span class="sxs-lookup"><span data-stu-id="4be4b-124">The user enters a PIN if necessary then selects **Verify** on the mobile app.</span></span> |
| <span data-ttu-id="4be4b-125">Код проверки в мобильном приложении</span><span class="sxs-lookup"><span data-stu-id="4be4b-125">Mobile app verification code</span></span> |<span data-ttu-id="4be4b-126">В мобильное приложение, запущенное на смартфоне пользователя, отправляется код проверки, который изменяется каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="4be4b-126">The mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="4be4b-127">Пользователь находит последний полученный код и вводит его на странице входа.</span><span class="sxs-lookup"><span data-stu-id="4be4b-127">The user finds the most recent code and enters it on the sign-in page.</span></span> |
| <span data-ttu-id="4be4b-128">OATH-токены сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="4be4b-128">Third-party OATH tokens</span></span> | <span data-ttu-id="4be4b-129">На сервере Многофакторной идентификации можно реализовать сторонние методы проверки.</span><span class="sxs-lookup"><span data-stu-id="4be4b-129">Azure Multi-Factor Authentication Server can be configured to accept third-party verification methods.</span></span> |

<span data-ttu-id="4be4b-130">Azure Multi-Factor Authentication предоставляет методы выборочной проверки для облака и сервера.</span><span class="sxs-lookup"><span data-stu-id="4be4b-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="4be4b-131">Это означает, что можно выбрать, какие методы доступны пользователям: телефонный звонок, текст, уведомление от приложения или код приложения.</span><span class="sxs-lookup"><span data-stu-id="4be4b-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="4be4b-132">Дополнительные сведения см. в разделе [Выбор методов проверки](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="4be4b-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4be4b-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4be4b-133">Next steps</span></span>

- <span data-ttu-id="4be4b-134">Ознакомьтесь с разными [версиями и методами использования службы Многофакторной идентификации Azure](multi-factor-authentication-versions-plans.md).</span><span class="sxs-lookup"><span data-stu-id="4be4b-134">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="4be4b-135">Развертывание Azure MFA [в облаке или локально](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="4be4b-135">Choose whether to deploy Azure MFA [in the cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="4be4b-136">Ознакомьтесь с ответами на часто задаваемые вопросы в статье [Часто задаваемые вопросы о Многофакторной идентификации Azure](multi-factor-authentication-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4be4b-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>