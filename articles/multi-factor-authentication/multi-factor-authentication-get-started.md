---
title: "aaaChoose между многофакторной проверки Подлинности Azure облачной или сервером | Документы Microsoft"
description: "Выберите hello многофакторной проверки подлинности безопасности решение, которое вам подходит предлагая, какие am, находится ли попытки toosecure, а где мои пользователи.  После этого выберите облако, сервер службы MFA или службы AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a>Выбор решения hello многофакторной проверки подлинности Azure для вас
Так как существует несколько видов многофакторной проверки подлинности Azure (MFA), мы необходимо ответить на несколько вопросов toofigure, какие версии имеет правильную один toouse hello.  Эти вопросы приведены ниже.

* [Что я хочу попытки toosecure](#what-am-i-trying-to-secure)
* [Где находятся пользователи hello](#where-are-the-users-located)
* [Какие функции мне нужны?](#what-featured-do-i-need)

Hello следующих разделах представлены рекомендации по определению, каждый из этих ответов.

## <a name="what-am-i-trying-toosecure"></a>Что я хочу попытки toosecure?
toodetermine hello правильный двухшаговой проверки решения, сначала мы необходимо ответить hello вопрос о том, что при попытке toosecure со второй метод проверки подлинности.  Это приложение в службе Azure?  Или в системе удаленного доступа?  Определяя, мы пытаемся toosecure, мы может ответить на вопрос: hello целей toobe включена многофакторная проверка подлинности.  

| Что такое идет toosecure | Многофакторной проверки Подлинности в облаке hello | Сервер MFA |
| --- |:---:|:---:|
| Приложения Майкрософт, получающие данные напрямую из источника |● |● |
| Приложений SaaS в коллекцию приложений hello |● |  |
| Веб-приложения, опубликованные через прокси приложения Azure AD |● |  |
| Приложения IIS, опубликованные не через прокси приложения Azure AD | |● |
| Удаленный доступ, например VPN или RDG | ● | ● |

## <a name="where-are-hello-users-located"></a>Где находятся пользователи hello
Далее просмотрев, где находятся пользователи помогает toouse правильным решением toodetermine hello, ли в облаке hello или локально с помощью hello многофакторной проверки Подлинности сервера.

| Местонахождение пользователей | Многофакторной проверки Подлинности в облаке hello | Сервер MFA |
| --- |:---:|:---:|
| Azure Active Directory |● | |
| Azure AD и локальная служба AD с использованием федерации в AD FS |● |● |
| Azure AD и локальная служба AD с использованием DirSync, Azure AD Sync, Azure AD Connect без синхронизации паролей |● |● |
| Azure AD и локальная служба AD с использованием DirSync, Azure AD Sync, Azure AD Connect с синхронизацией паролей |● | |
| Локальная служба Active Directory | |● |

## <a name="what-features-do-i-need"></a>Какие функции мне нужны?
Hello приведенной ниже таблице сравниваются функции hello, доступные с многофакторной проверки подлинности в облаке hello и hello многофакторной проверки подлинности сервера.

| Функция | Многофакторной проверки Подлинности в облаке hello | Сервер MFA |
| --- |:---:|:---:|
| Уведомление от мобильного приложения в качестве второго фактора | ● | ● |
| Код подтверждения мобильного приложения в качестве второго фактора | ● | ● |
| Телефонный вызов в качестве второго фактора | ● | ● |
| Одностороннее SMS в качестве второго фактора | ● | ● |
| Двустороннее SMS в качестве второго фактора | | ● |
| Маркеры оборудования в качестве второго фактора | | ● |
| Пароли приложений для клиентов Office 365, которые не поддерживают MFA | ● | |
| Администраторский контроль над методами проверки подлинности | ● | ● |
| Режим ПИН-кода | | ● |
| Предупреждение о мошенничестве |● | ● |
| Отчеты службы "Многофакторная идентификация Microsoft Azure" |● | ● |
| Разовый обход | | ● |
| Настраиваемые приветствия для телефонных вызовов | ● | ● |
| Настройка идентификатора вызывающей стороны для телефонных звонков | ● | ● |
| Надежные IP-адреса | ● | ● |
| Запоминание данных MFA для доверенных устройств | ● | |
| Условный доступ | ● | ● |
| Кэш |  | ● |

## <a name="next-steps"></a>Дальнейшие действия

Теперь, после определения ли toouse облачных многофакторной проверки подлинности и hello многофакторной проверки Подлинности сервер локально, мы можете начать настройке и использовании Azure Multi-factor Authentication. **Выберите значок hello, представляющий вашего сценария**

<center>




[![Облако](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Сервер](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center>
