---
title: "Проблема при создании приложения прокси приложения | Документы Майкрософт"
description: "Сведения об устранении неполадок при создании приложений прокси приложения на портале администрирования Azure AD."
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
ms.openlocfilehash: fe56f56162ba7186f1b660a5b44fcef38f1dee9d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="problem-creating-an-application-proxy-application"></a>Проблема при создании приложения прокси приложения 

Ниже приведены некоторые наиболее распространенные проблемы, возникающие при создании приложения прокси приложения.

## <a name="recommended-documents"></a>Рекомендуемые документы 

Дополнительные сведения о создании приложения прокси приложения на портале администрирования см. в статье [Публикация приложений с помощью прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Если при создании приложения по инструкциям из этого документа возникает ошибка, см. описание ошибки для получения сведений о ее исправлении. Большинство сообщений об ошибках включают в себя предлагаемое исправление. 

## <a name="specific-things-to-check"></a>Что нужно проверить

Чтобы избежать распространенных ошибок, проверьте следующее:

-   Используется учетная запись администратора с разрешением на создание приложения прокси приложения.

-   Внутренний URL-адрес является уникальным.

-   Внешний URL-адрес является уникальным.

-   URL-адрес начинается с http или https и заканчивается на "/".

-   URL-адрес должен включать имя домена, а не IP-адрес.

Сообщение об ошибке при создании приложения должно отображаться в правом верхнем углу. Для просмотра сообщений об ошибках также можно выбрать значок уведомления.

   ![Уведомление](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a>Дальнейшие действия
[Включение прокси приложения на портале Azure](active-directory-application-proxy-enable.md)
