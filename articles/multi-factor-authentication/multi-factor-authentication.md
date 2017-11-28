---
title: "aaaLearn о двухшаговой проверке в многофакторной проверки Подлинности Azure | Документы Microsoft"
description: "Что такое Azure Multi-factor Authentication, зачем использовать многофакторную проверку Подлинности, Дополнительные сведения о hello многофакторной проверки подлинности клиента и различные методы hello и доступных версий. "
keywords: "Введение tooMFA Обзор многофакторной проверки подлинности, что такое mfa"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="2aca5-104">Что такое Azure Multi-factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="2aca5-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="2aca5-105">Двухшаговая проверка — это метод проверки подлинности, требующий более одного метода проверки и добавляющий важный второй уровень безопасности toouser входов и транзакций.</span><span class="sxs-lookup"><span data-stu-id="2aca5-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security toouser sign-ins and transactions.</span></span> <span data-ttu-id="2aca5-106">Для работы требуется любые два или более hello следующие методы проверки:</span><span class="sxs-lookup"><span data-stu-id="2aca5-106">It works by requiring any two or more of hello following verification methods:</span></span>

* <span data-ttu-id="2aca5-107">Что-то, что известно вам (обычно это пароль).</span><span class="sxs-lookup"><span data-stu-id="2aca5-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="2aca5-108">Что-то, что у вас есть (доверенное устройство, которое непросто дублируется, такое как телефон).</span><span class="sxs-lookup"><span data-stu-id="2aca5-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="2aca5-109">Что-то, относящееся непосредственно к вам (биометрические данные).</span><span class="sxs-lookup"><span data-stu-id="2aca5-109">Something you are (biometrics)</span></span>

<span data-ttu-id="2aca5-110"><center>![Имя пользователя и пароль](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Сертификаты](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Смартфон](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Смарт-карта](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Виртуальная смарт-карта](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Имя пользователя и пароль](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="2aca5-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="2aca5-111">Многофакторная идентификация (MFA) Azure — решение Майкрософт для двухшаговой проверки.</span><span class="sxs-lookup"><span data-stu-id="2aca5-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="2aca5-112">Azure MFA помогает toodata защиты доступа и приложений удовлетворением спроса на простой процесс входа в систему.</span><span class="sxs-lookup"><span data-stu-id="2aca5-112">Azure MFA helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="2aca5-113">Служба обеспечивает строгую аутентификацию с помощью различных способов проверки — телефонного звонка, текстового сообщения или проверки в мобильном приложении.</span><span class="sxs-lookup"><span data-stu-id="2aca5-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="2aca5-114">Что такое Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="2aca5-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="2aca5-115">Сегодня Интернетом пользуется все больше и больше людей.</span><span class="sxs-lookup"><span data-stu-id="2aca5-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="2aca5-116">С помощью смартфонов, планшетных ПК, ноутбуки и компьютеров пользователей есть несколько вариантов на том, как они будут tooconnect и оставаться на связи в любое время.</span><span class="sxs-lookup"><span data-stu-id="2aca5-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going tooconnect and stay connected at any time.</span></span> <span data-ttu-id="2aca5-117">Пользователи могут получать доступ к своим учетным записям и приложениям практически из любого места. Это позволяет выполнять большие объемы работы и предоставлять более высокий уровень обслуживания клиентов.</span><span class="sxs-lookup"><span data-stu-id="2aca5-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="2aca5-118">Azure многофакторная проверка подлинности — легко toouse, масштабируемых, и надежные решения, предоставляет второй метод проверки подлинности, пользователи всегда защищены.</span><span class="sxs-lookup"><span data-stu-id="2aca5-118">Azure Multi-Factor Authentication is an easy toouse, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![Легко tooUse](./media/multi-factor-authentication/simple.png) | ![масштабируемость,](./media/multi-factor-authentication/scalable.png) | ![Постоянная защита](./media/multi-factor-authentication/protected.png) | ![Надежность](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="2aca5-123">**Легко toouse**</span><span class="sxs-lookup"><span data-stu-id="2aca5-123">**Easy toouse**</span></span> |<span data-ttu-id="2aca5-124">**Масштабируемость**</span><span class="sxs-lookup"><span data-stu-id="2aca5-124">**Scalable**</span></span> |<span data-ttu-id="2aca5-125">**Постоянная защита**</span><span class="sxs-lookup"><span data-stu-id="2aca5-125">**Always Protected**</span></span> |<span data-ttu-id="2aca5-126">**Надежность**</span><span class="sxs-lookup"><span data-stu-id="2aca5-126">**Reliable**</span></span> |

* <span data-ttu-id="2aca5-127">**Легко tooUse** -многофакторной проверки подлинности Azure — простой tooset копирование и использование.</span><span class="sxs-lookup"><span data-stu-id="2aca5-127">**Easy tooUse** - Azure Multi-Factor Authentication is simple tooset up and use.</span></span> <span data-ttu-id="2aca5-128">Hello дополнительной защиты, входящий в состав многофакторной проверки подлинности Azure позволяет пользователям toomanage свои собственные устройства.</span><span class="sxs-lookup"><span data-stu-id="2aca5-128">hello extra protection that comes with Azure Multi-Factor Authentication allows users toomanage their own devices.</span></span> <span data-ttu-id="2aca5-129">И главное, что в большинстве случаев это можно настроить несколькими щелчками мыши.</span><span class="sxs-lookup"><span data-stu-id="2aca5-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="2aca5-130">**Масштабируемая** -многофакторной проверки подлинности Azure использует hello возможностей облачных hello и интегрируется с локальным AD и пользовательские приложения.</span><span class="sxs-lookup"><span data-stu-id="2aca5-130">**Scalable** - Azure Multi-Factor Authentication uses hello power of hello cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="2aca5-131">Такая защита распространяется даже tooyour большого объема, критически важных сценариях.</span><span class="sxs-lookup"><span data-stu-id="2aca5-131">This protection is even extended tooyour high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="2aca5-132">**Всегда защищено** -многофакторной проверки подлинности Azure предоставляет надежную проверку подлинности с помощью hello высоким стандартам отрасли.</span><span class="sxs-lookup"><span data-stu-id="2aca5-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using hello highest industry standards.</span></span>
* <span data-ttu-id="2aca5-133">**Надежность**. Мы гарантируем 99,9 % доступность многофакторной идентификации Azure.</span><span class="sxs-lookup"><span data-stu-id="2aca5-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="2aca5-134">Hello служба считается недоступным в случае неудачного tooreceive или процесс проверки запросов для двухшаговой проверки hello.</span><span class="sxs-lookup"><span data-stu-id="2aca5-134">hello service is considered unavailable when it is unable tooreceive or process verification requests for hello two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="2aca5-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2aca5-135">Next steps</span></span>

- <span data-ttu-id="2aca5-136">Узнайте о [принципах работы службы Многофакторной идентификации](multi-factor-authentication-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="2aca5-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="2aca5-137">Узнайте о разных hello [версии и методы использования многофакторной проверки подлинности Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="2aca5-137">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
