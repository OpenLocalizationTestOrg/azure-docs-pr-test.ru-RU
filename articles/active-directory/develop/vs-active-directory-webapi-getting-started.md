---
title: "aaaGet работы с Azure AD в проектах Visual Studio WebApi | Документы Microsoft"
description: "Запуск с помощью Azure Active Directory в проектах WebApi после подключения tooor создания Azure AD с помощью Visual Studio tooget подключенные службы"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 21413a71a2fd61f31268bf6d5e4d86b8be5bd16a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a>Начало работы с Azure Active Directory и подключенными службами Visual Studio (проекты WebApi)
> [!div class="op_single_selector"]
> * [Приступая к работе](vs-active-directory-webapi-getting-started.md)
> * [Что произошло?](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a>Требование проверки подлинности tooaccess контроллеров
Все контроллеры в проекте были снабженных hello **авторизовать** атрибута. Этот атрибут требуется hello toobe пользователя, доступ к API-интерфейсы hello определяются эти контроллеры только после проверки подлинности. tooallow hello контроллера toobe доступна анонимно, удалите этот атрибут из контроллера hello. Tooset hello разрешения на более детальном уровне, применить метод tooeach атрибут hello, требующей авторизации вместо применения его toohello класс контроллера.

## <a name="next-steps"></a>Дальнейшие действия
[Дополнительная информация о службе Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

