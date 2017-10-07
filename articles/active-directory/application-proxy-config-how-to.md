---
title: "aaaHow tooconfigure приложение прокси приложения | Документы Microsoft"
description: "Узнайте, как toocreate Настройка приложения прокси приложения в рамках простой процедуры"
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
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a>Как tooconfigure приложения прокси приложения

В этой статье помогут toounderstand как tooconfigure приложение прокси приложения в Azure AD tooexpose toohello приложений вашей локальной облака.

## <a name="recommended-documents"></a>Рекомендуемые документы 

toolearn о начальной конфигурации hello и создание приложения прокси приложения с помощью портала администрирования hello выполните hello [публикация приложений с помощью прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Дополнительные сведения о настройке соединителей см. в разделе [включить прокси приложения в Azure portal hello](active-directory-application-proxy-enable.md).

Сведения об отправке сертификатов и пользовательских доменах см. в разделе [Работа с пользовательскими доменами в прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).

## <a name="create-hello-applicationsetting-hello-urls"></a>Создание URL-адреса для параметра/приложения hello hello

Если вы следуете hello шагов в hello [публикация приложений с помощью прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) документация и являются сообщение об ошибке, создание приложения hello см. сведения об ошибке hello сведения и предложения по приложение hello toofix. Большинство сообщений об ошибках включают в себя предлагаемое исправление. tooavoid распространенные ошибки, проверьте:

-   Вы являетесь администратором с toocreate разрешений приложения прокси приложения

-   Hello внутренний URL-адрес является уникальным

-   Hello внешний URL-адрес является уникальным

-   Здравствуйте, URL-адреса, начинающиеся с http или https, а заканчивают комментарий сочетанием «/»

-   Hello URL-адрес должен быть имени домена, а не IP-адрес

сообщение об ошибке Hello должны отображаться в правом верхнем углу hello, при создании приложения hello. Можно также выбрать hello уведомления значок toosee hello сообщения об ошибках.

   ![Уведомление](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>Настройка соединителей и групп соединителей

Если возникают неполадки при настройке приложения из-за предупреждения о соединители hello и группы соединителей см. инструкции о включении прокси приложения для сведений о том, как toodownload соединители. Следует toolearn больше о соединителях см hello [соединители документации](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).

Если соединителях находятся в неактивном состоянии, это означает, которых не удается tooreach hello службы. Часто это потому, что все необходимые hello порты не открыты. toosee список необходимых портах разделе hello предварительным hello включении документации по прокси-сервера приложения.

## <a name="upload-certificates-for-custom-domains"></a>Отправка сертификатов для пользовательских доменов

Пользовательские домены позволяют toospecify hello домен вашей внешние URL-адреса. пользовательские домены toouse, потребуется tooupload hello сертификат для этого домена. Сведения об использовании сертификатов и пользовательских доменов см. в разделе [Работа с пользовательскими доменами в прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains). 

При возникновении проблем при загрузке сертификата, найдите сообщения об ошибке hello в портал hello Дополнительные сведения о hello проблема с сертификатом hello. Распространенные проблемы, связанные с сертификатами, включают следующие:

-   Срок действия сертификата истек.

-   Сертификат является самозаверяющим.

-   В сертификате отсутствует закрытый ключ hello

Отображение сообщений об ошибках Hello в hello правом верхнем углу попытке tooupload hello сертификата. Можно также выбрать hello уведомления значок toosee hello сообщения об ошибках.

   ![Уведомление](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>Дальнейшие действия
[Публикация приложений с помощью прокси приложения Azure AD](application-proxy-publish-azure-portal.md)
