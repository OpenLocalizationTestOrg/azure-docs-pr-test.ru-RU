---
title: "aaaUpgrade tooAzure AD прокси приложения | Документы Microsoft"
description: "Выберите, какой прокси-сервер лучше всего подходит для обновления Microsoft Forefront или Unified Access Gateway."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a>Сравнение решений для удаленного доступа

Одним из двух решений для удаленного доступа, которые предоставляет Майкрософт, является прокси-служба приложения Azure Active Directory. Hello других — прокси веб-приложения hello локальную версию. Эти два решения заменяют более ранние продукты Майкрософт — Microsoft Forefront Threat Management Gateway (TMG) и Unified Access Gateway (UAG). Использование этой статьи toounderstand сравнение tooeach других эти четыре решения. Вы по-прежнему используется hello рекомендуется использовать TMG или UAG решений, использовать этот план toohelp статье вашей tooone миграции из hello прокси приложения. 


## <a name="feature-comparison"></a>Сравнение возможностей

Используйте этот toounderstand таблицы сравнение Threat Management Gateway (TMG), Unified Access Gateway (UAG), прокси-сервера веб-приложения (WAP) и прокси-сервера приложения Azure AD (AP) tooeach других.

| Функция | TMG | UAG | WAP | AP |
| ------- | --- | --- | --- | --- |
| Проверка подлинности на основе сертификата | Да | Да | - | - |
| Выборочная публикация браузерных приложений | Да | Да | Да | Да |
| Предварительная аутентификация и единый вход | Да | Да | Да | Да | 
| Брандмауэр уровня 2/3 | Да | Да | - | - |
| Возможности прокси-службы пересылки | Да | - | - | - |
| Возможности VPN | Да | Да | - | - |
| Расширенная поддержка протоколов | - | Да | Да, при запуске поверх HTTP | Да, при запуске поверх HTTP или через шлюз удаленных рабочих столов |
| Служит прокси-сервером ADFS | - | Да | Да | - |
| Единый портал для доступа к приложениям | - | Да | - | Да |
| Преобразование ссылки в текст ответа | Да | Да | - | Да | 
| Аутентификация с помощью заголовков | - | Да | - | Да, с использованием PingAccess | 
| Безопасность в масштабе облака | - | - | - | Да | 
| Условный доступ | - | Да | - | Да |
| Компоненты, не hello демилитаризованной зоны (DMZ) | - | - | - | Да |
| Без входящих соединений | - | - | - | Да |

В большинстве случаев рекомендуется приложения Azure AD в качестве hello современные решения. Прокси-служба веб-приложений предпочтительна только в ситуациях, когда требуется прокси-сервер для AD FS, а задействовать пользовательские домены в Azure Active Directory нет возможности. 

Прокси приложения Azure AD предлагает уникальные преимущества при сравнении toosimilar продуктов, включая:

- Расширение tooon локальных ресурсов Azure AD
   - Безопасность и защита в масштабе облака
   - Функции, например условного доступа и многофакторной проверки подлинности, легко tooenable
- Не componenet в демилитаризованной зоне hello
- Отсутствие необходимости во входящих соединениях
- Панель один доступа пользователи могут перейти toofor всех своих приложений, включая Office 365, Azure AD интегрированных приложений SaaS и в локальной веб-приложений. 


## <a name="next-steps"></a>Дальнейшие действия

- [Использовать приложения Azure AD tooprovide безопасного удаленного доступа tooon локальные приложения](active-directory-application-proxy-get-started.md)
- [Переход из Forefront TMG и UAG tooApplication прокси-сервера](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).
