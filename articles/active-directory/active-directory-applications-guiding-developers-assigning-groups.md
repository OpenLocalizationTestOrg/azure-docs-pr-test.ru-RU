---
title: "Назначение групп для приложений Azure AD | Документация Майкрософт"
description: "Как реализовать назначение групп для приложений Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: e0b0b87a454db96747f024e81882fe83d62fdbe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a>Назначение групп Azure Active Directory для приложения
Прежде чем назначить пользователей и группы для приложения, необходимо настроить требование назначения пользователей. Чтобы узнать, как настроить требование назначения пользователей, см. статью [Azure AD и приложения: требование назначения пользователей](active-directory-applications-guiding-developers-requiring-user-assignment.md).

В этой статье предполагается, что вы уже создали в Active Directory группу, которая используется для этого приложения.

## <a name="assigning-groups-to-an-application"></a>Назначение групп для приложения
1. Войдите на портал Azure с учетной записью администратора.
2. В главном меню выберите пункт **Все элементы** .
3. Выберите каталог, который используете для приложения.
4. Откройте вкладку **ПРИЛОЖЕНИЯ** .
5. Выберите приложение из списка приложений, связанных с данным каталогом.
6. Откройте вкладку **ПОЛЬЗОВАТЕЛИ И ГРУППЫ** .
7. Отфильтруйте список групп в Active Directory с помощью раскрывающегося списка **Группы** .
8. Выберите группу.
9. Щелкните **НАЗНАЧИТЬ**.
10. Щелкните **Да** при появлении запроса.

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
