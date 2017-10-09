---
title: "aaaAzure многофакторной проверки подлинности - принцип работы"
description: "Azure Multi-factor Authentication помогает toodata защиты доступа и приложений удовлетворением спроса на простой процесс входа в систему. Эта служба предлагает дополнительную защиту за счет дополнительного способа проверки подлинности и, используя ряд простых способов проверки подлинности, обеспечивает строгую проверку."
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
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="465d5-104">Принципы работы службы Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="465d5-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="465d5-105">безопасность Hello двухшаговую проверку заключается в ее многоуровневом подходе.</span><span class="sxs-lookup"><span data-stu-id="465d5-105">hello security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="465d5-106">Нарушения нескольких факторов проверки подлинности представляет нетривиальную задачу для злоумышленников.</span><span class="sxs-lookup"><span data-stu-id="465d5-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="465d5-107">Даже если злоумышленник узнал пароль пользователя toolearn hello, он бесполезен без наличия доверенного устройства hello.</span><span class="sxs-lookup"><span data-stu-id="465d5-107">Even if an attacker manages toolearn hello user's password, it is useless without also having possession of hello trusted device.</span></span> 

![Подтверждение](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="465d5-109">Azure Multi-factor Authentication помогает toodata защиты доступа и приложений удовлетворением спроса на простой процесс входа в систему.</span><span class="sxs-lookup"><span data-stu-id="465d5-109">Azure Multi-Factor Authentication helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="465d5-110">Эта служба предлагает дополнительную защиту за счет дополнительного способа проверки подлинности и, используя ряд простых способов проверки подлинности, обеспечивает строгую проверку.</span><span class="sxs-lookup"><span data-stu-id="465d5-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="465d5-111">Методы, доступные для двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="465d5-111">Methods available for two-step verification</span></span>
<span data-ttu-id="465d5-112">При входе в систему пользователь дополнительную проверку отправляется toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="465d5-112">When a user signs in, an additional verification is sent toohello user.</span></span>  <span data-ttu-id="465d5-113">Здесь представлены Hello список методов, которые могут использоваться для второй проверку.</span><span class="sxs-lookup"><span data-stu-id="465d5-113">hello following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="465d5-114">Метод проверки</span><span class="sxs-lookup"><span data-stu-id="465d5-114">Verification Method</span></span> | <span data-ttu-id="465d5-115">Описание</span><span class="sxs-lookup"><span data-stu-id="465d5-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="465d5-116">Телефонный звонок</span><span class="sxs-lookup"><span data-stu-id="465d5-116">Phone call</span></span> |<span data-ttu-id="465d5-117">Вызов помещается tooa зарегистрированных телефон пользователя.</span><span class="sxs-lookup"><span data-stu-id="465d5-117">A call is placed tooa user’s registered phone.</span></span> <span data-ttu-id="465d5-118">Hello пользователь вводит ПИН-код, при необходимости, а затем нажимает клавишу # hello.</span><span class="sxs-lookup"><span data-stu-id="465d5-118">hello user enters a PIN if necessary then presses hello # key.</span></span> |
| <span data-ttu-id="465d5-119">Текстовое сообщение</span><span class="sxs-lookup"><span data-stu-id="465d5-119">Text message</span></span> |<span data-ttu-id="465d5-120">Текстовое сообщение отправляется tooa на мобильный телефон пользователя с шестизначным кодом.</span><span class="sxs-lookup"><span data-stu-id="465d5-120">A text message is sent tooa user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="465d5-121">Hello пользователь введет этот код на странице входа hello.</span><span class="sxs-lookup"><span data-stu-id="465d5-121">hello user enters this code on hello sign-in page.</span></span> |
| <span data-ttu-id="465d5-122">Уведомление от мобильного приложения</span><span class="sxs-lookup"><span data-stu-id="465d5-122">Mobile app notification</span></span> |<span data-ttu-id="465d5-123">Запрос на проверку отправляется смартфона tooa пользователя.</span><span class="sxs-lookup"><span data-stu-id="465d5-123">A verification request is sent tooa user’s smart phone.</span></span> <span data-ttu-id="465d5-124">Hello пользователь вводит ПИН-код, при необходимости, а затем выбирает **проверьте** на мобильное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="465d5-124">hello user enters a PIN if necessary then selects **Verify** on hello mobile app.</span></span> |
| <span data-ttu-id="465d5-125">Код проверки в мобильном приложении</span><span class="sxs-lookup"><span data-stu-id="465d5-125">Mobile app verification code</span></span> |<span data-ttu-id="465d5-126">мобильное приложение Hello, на котором работает пользователя со смартфона, отображает код проверки, который изменяет каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="465d5-126">hello mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="465d5-127">Hello пользователь находит hello самый последний код и вводит его hello-на страницу входа.</span><span class="sxs-lookup"><span data-stu-id="465d5-127">hello user finds hello most recent code and enters it on hello sign-in page.</span></span> |
| <span data-ttu-id="465d5-128">OATH-токены сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="465d5-128">Third-party OATH tokens</span></span> | <span data-ttu-id="465d5-129">Сервер Azure Multi-factor Authentication может быть настроенный tooaccept сторонние проверки методов.</span><span class="sxs-lookup"><span data-stu-id="465d5-129">Azure Multi-Factor Authentication Server can be configured tooaccept third-party verification methods.</span></span> |

<span data-ttu-id="465d5-130">Azure Multi-Factor Authentication предоставляет методы выборочной проверки для облака и сервера.</span><span class="sxs-lookup"><span data-stu-id="465d5-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="465d5-131">Это означает, что можно выбрать, какие методы доступны пользователям: телефонный звонок, текст, уведомление от приложения или код приложения.</span><span class="sxs-lookup"><span data-stu-id="465d5-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="465d5-132">Дополнительные сведения см. в разделе [Выбор методов проверки](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="465d5-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="465d5-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="465d5-133">Next steps</span></span>

- <span data-ttu-id="465d5-134">Узнайте о разных hello [версии и методы использования многофакторной проверки подлинности Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="465d5-134">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="465d5-135">Выберите ли toodeploy многофакторной проверки Подлинности Azure [в облаке hello или в локальной среде](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="465d5-135">Choose whether toodeploy Azure MFA [in hello cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="465d5-136">Ознакомьтесь с ответами на часто задаваемые вопросы в статье [Часто задаваемые вопросы о Многофакторной идентификации Azure](multi-factor-authentication-faq.md).</span><span class="sxs-lookup"><span data-stu-id="465d5-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>