---
title: "Требование назначения пользователей: Azure AD | Документация Майкрософт"
description: "Как требовать назначение пользователей для приложений Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 30b78cba-1e0f-472f-8314-f2250a9b91c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 079b806c041a4a21e9350342867aee581c57bf45
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="azure-ad-and-applications-require-user-assignment"></a>Azure AD и приложения: требование назначения пользователей
## <a name="requiring-user-assignment"></a>Требование назначения пользователей
1. Войдите на портал Azure с учетной записью администратора.
2. В главном меню выберите пункт **Все элементы** .
3. Выберите каталог, который используете для приложения.
4. Откройте вкладку **ПРИЛОЖЕНИЯ** .
5. Выберите приложение из списка приложений, связанных с данным каталогом.
6. Выберите вкладку **НАСТРОЙКА** .
7. Задайте для параметра **Для доступа к приложению требуется назначение пользователей** значение «Да».
8. Нажмите кнопку **Сохранить** , расположенную в нижней части экрана.

Теперь будет необходимо назначить пользователей и (или) группы для приложения. См. разделы [Назначение пользователей приложения](active-directory-applications-guiding-developers-assigning-users.md) и [Назначение групп для приложения](active-directory-applications-guiding-developers-assigning-groups.md).

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
