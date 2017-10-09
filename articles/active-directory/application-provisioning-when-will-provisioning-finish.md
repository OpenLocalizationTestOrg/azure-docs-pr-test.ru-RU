---
title: "Подготовка приложения Azure AD tooan коллекции aaaUser — ведения часа или более | Документы Microsoft"
description: "Как toofind out почему подготовки tooyour приложения может выполняться дольше, чем ожидалось"
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
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a>Подготовка приложения Azure AD tooan коллекции пользователей — ведения часов или более

При первом включении автоматической инициализации приложения, hello начальной синхронизации может занять от tooseveral часов 20 минут, в зависимости от размера каталога Azure AD hello и hello количество пользователей в области для подготовки hello. 

Последующие синхронизации после начальной синхронизации hello выполняться быстрее, как hello подготовки службы хранит водяных знаков, которые представляют Привет состояние обеих систем после начальной синхронизации hello, повышая производительность последующих синхронизаций.

## <a name="how-tooimprove-provisioning-performance"></a>Как tooimprove подготовки производительности

Если начальная синхронизация hello занимает несколько часов, есть один вопрос, можно сделать tooimprove производительности:

-   **Фильтры области.** Фильтры области позволяют toofine настраивать hello данные, которые hello подготовки служба извлекает из Azure AD с помощью фильтрации пользователей на основе значений конкретного атрибута. Дополнительные сведения о фильтрах области см. в статье [Подготовка приложений на основе атрибутов с использованием фильтров области](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

## <a name="next-steps"></a>Дальнейшие действия
[Автоматизировать подготовку пользователей и их отзыва tooSaaS приложений с Azure Active Directory](active-directory-saas-app-provisioning.md)

