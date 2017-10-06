---
title: "aaaHow toogrant разрешений tooa сторонних разрабатываемых приложений | Документы Microsoft"
description: "Как toogrant разрешения tooyour приложения, разработанного с помощью hello портала Azure AD или параметра URL-адреса"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a>Как tooa toogrant разрешения разработанного приложения

Требуется согласие toogrant приоритетным прерыванием в приложении или при запуске произошла ошибка, вы не согласие tooan приложения, выполните указанные ниже действия.

## <a name="how-tooperform-admin-consent-for-your-application"></a>Как tooperform согласие администратора для вашего приложения

Действует hello предоставления согласия toohello приложения для всех пользователей в вашей организации.

1. Перейдите toohello **регистрации приложения** колонки как **глобального администратора**, а затем выберите приложение hello.

2. Выберите **требуемые разрешения**и, наконец, появится hello **GRANT, предоставление разрешений** кнопку hello верхней части колонки hello.

Кроме того, можно создать запрос слишком*login.microsoftonline.com* с вашей конфигурации приложения и добавления на *& prompt = admin\_согласия*. После входа в систему с учетными данными администратора, приложение hello было предоставлено согласие для всех пользователей.

## <a name="how-tooforce-user-consent-for-your-application"></a>Как tooforce согласия пользователя для приложения

* Добавление на запросы проверки подлинности *& Запрос согласия =* , требующую tooconsent конечных пользователей каждый раз при проверке подлинности.

## <a name="next-steps"></a>Дальнейшие действия

[Запрос согласия и интеграция приложений tooAzureAD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[Согласие и разрешения для конвергированных приложений в Azure AD версии 2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[StackOverflow в AzureAD](http://stackoverflow.com/questions/tagged/azure-active-directory)
