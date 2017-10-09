---
title: "aaaFind out когда конкретного пользователя будет доступ tooaccess приложения | Документы Microsoft"
description: "Как toofind out ли критически важными пользователь быть может tooaccess приложения вы настроили для подготовки пользователей в Azure AD"
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
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a>Узнать, когда конкретного пользователя будет доступ tooaccess приложения
При использовании автоматической подготовки пользователей Azure AD будет автоматически подготавливать и обновлять учетные записи пользователей в приложении на основе [назначений пользователей и групп](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) с установленным интервалом времени, обычно каждые 10 минут.

## <a name="how-long-does-it-take"></a>Сколько времени это занимает?

Hello время, необходимое для данного пользователя toobe подготовить главным образом зависит ли первоначальную синхронизацию «full» уже существует.

Здравствуйте, первой синхронизации между Azure AD и приложения может занять от tooseveral часов 20 минут, в зависимости от размера каталога hello Azure AD и hello количество пользователей в области для подготовки hello. 

Последующие синхронизации после начальной синхронизации hello выполняться быстрее (например, в течение 10 минут), как подготовка службы hello хранит водяных знаков, которые представляют Привет состояние обеих систем после начальной синхронизации hello, повышая производительность последующих синхронизаций.

## <a name="how-toocheck-hello-status-of-a-user"></a>Как toocheck hello состояния пользователя

состояние подготовки hello toosee для выбранного пользователя, обратитесь к hello журналы аудита в Azure AD.

Hello подготовки журналы аудита можно получить в hello в hello портале Azure **Azure Active Directory &gt; корпоративных приложений &gt; \[имя_приложения\] &gt; журналы аудита**вкладки. Фильтр hello входе hello **подготовку учетных записей** tooonly категории разделе hello подготовки события для этого приложения. Можно выполнить поиск пользователя на основании hello «сопоставления ID», настроенную для их в сопоставления атрибутов hello. 

Например, если пользователь настроил hello «имя участника-пользователя» или «адрес электронной почты» как hello сопоставления атрибута на стороне hello Azure AD и пользователя hello подготовки не имеет значение «audrey@contoso.com«, затем аудита hello поиска в журналах»audrey@contoso.com"и затем просмотрите возвращены записи.

Подготовка аудита Hello регистрирует записи Здравствуйте, все операции, выполняемые hello подготовки службы, включая:

* Получение сведений о назначенных пользователях, которые находятся в области для подготовки, в Azure AD
* Запрос hello целевое приложение hello наличие этих пользователей
* Сравнение объектов пользователя hello между системой hello
* Добавление, обновление или отключение учетной записи пользователя hello в целевой системе hello, на основе сравнения hello

## <a name="next-steps"></a>Дальнейшие действия
[Автоматизировать подготовку пользователей и их отзыва tooSaaS приложений с Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''
