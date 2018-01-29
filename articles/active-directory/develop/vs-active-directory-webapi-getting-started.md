---
title: "Приступая к работе с Azure AD в проектах WebApi в Visual Studio | Документация Майкрософт"
description: "Как начать использовать Azure Active Directory в проектах WebApi после подключения или создания Azure AD с помощью подключенных служб Visual Studio"
services: active-directory
documentationcenter: 
author: kraigb
manager: mtillman
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
ms.openlocfilehash: 3d510c193ab8c7e65340275017cb2dcd4c76def0
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a>Начало работы с Azure Active Directory и подключенными службами Visual Studio (проекты WebApi)
> [!div class="op_single_selector"]
> * [Приступая к работе](vs-active-directory-webapi-getting-started.md)
> * [Что произошло?](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a>Требование проверки подлинности для доступа к контроллерам
Ко всем контроллерам в проекте добавлен атрибут **Authorize** . Этот атрибут обеспечивает аутентификацию пользователей перед доступом к интерфейсам API, определяемым этими контроллерами. Для анонимного доступа к контроллеру удалить с него этот атрибут. Если необходимо задать разрешения на более детальном уровне, примените атрибут к каждому методу, требующему проверки подлинности, а не к классу контроллера.

## <a name="next-steps"></a>Дальнейшие действия
[Дополнительная информация о службе Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

