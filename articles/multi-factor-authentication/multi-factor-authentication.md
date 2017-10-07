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
# <a name="what-is-azure-multi-factor-authentication"></a>Что такое Azure Multi-factor Authentication?
Двухшаговая проверка — это метод проверки подлинности, требующий более одного метода проверки и добавляющий важный второй уровень безопасности toouser входов и транзакций. Для работы требуется любые два или более hello следующие методы проверки:

* Что-то, что известно вам (обычно это пароль).
* Что-то, что у вас есть (доверенное устройство, которое непросто дублируется, такое как телефон).
* Что-то, относящееся непосредственно к вам (биометрические данные).

<center>![Имя пользователя и пароль](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Сертификаты](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Смартфон](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Смарт-карта](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Виртуальная смарт-карта](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Имя пользователя и пароль](./media/multi-factor-authentication/cert.png)</center>

Многофакторная идентификация (MFA) Azure — решение Майкрософт для двухшаговой проверки. Azure MFA помогает toodata защиты доступа и приложений удовлетворением спроса на простой процесс входа в систему. Служба обеспечивает строгую аутентификацию с помощью различных способов проверки — телефонного звонка, текстового сообщения или проверки в мобильном приложении.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a>Что такое Azure Multi-Factor Authentication?
Сегодня Интернетом пользуется все больше и больше людей. С помощью смартфонов, планшетных ПК, ноутбуки и компьютеров пользователей есть несколько вариантов на том, как они будут tooconnect и оставаться на связи в любое время. Пользователи могут получать доступ к своим учетным записям и приложениям практически из любого места. Это позволяет выполнять большие объемы работы и предоставлять более высокий уровень обслуживания клиентов.

Azure многофакторная проверка подлинности — легко toouse, масштабируемых, и надежные решения, предоставляет второй метод проверки подлинности, пользователи всегда защищены.

| ![Легко tooUse](./media/multi-factor-authentication/simple.png) | ![масштабируемость,](./media/multi-factor-authentication/scalable.png) | ![Постоянная защита](./media/multi-factor-authentication/protected.png) | ![Надежность](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| **Легко toouse** |**Масштабируемость** |**Постоянная защита** |**Надежность** |

* **Легко tooUse** -многофакторной проверки подлинности Azure — простой tooset копирование и использование. Hello дополнительной защиты, входящий в состав многофакторной проверки подлинности Azure позволяет пользователям toomanage свои собственные устройства. И главное, что в большинстве случаев это можно настроить несколькими щелчками мыши.
* **Масштабируемая** -многофакторной проверки подлинности Azure использует hello возможностей облачных hello и интегрируется с локальным AD и пользовательские приложения. Такая защита распространяется даже tooyour большого объема, критически важных сценариях.
* **Всегда защищено** -многофакторной проверки подлинности Azure предоставляет надежную проверку подлинности с помощью hello высоким стандартам отрасли.
* **Надежность**. Мы гарантируем 99,9 % доступность многофакторной идентификации Azure. Hello служба считается недоступным в случае неудачного tooreceive или процесс проверки запросов для двухшаговой проверки hello.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a>Дальнейшие действия

- Узнайте о [принципах работы службы Многофакторной идентификации](multi-factor-authentication-how-it-works.md).

- Узнайте о разных hello [версии и методы использования многофакторной проверки подлинности Azure](multi-factor-authentication-versions-plans.md)
