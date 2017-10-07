---
title: "aaaAzure ретрансляции, проверка подлинности и авторизация | Документы Microsoft"
description: "Общие сведения о проверке подлинности подписанного URL-адреса (SAS) в ретрансляторе Azure"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: b27914672ce968da2bddba8dafc5683ebf3834ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-authentication-and-authorization"></a>Проверка подлинности и авторизация в ретрансляторе Azure
Приложения могут проходить проверку tooAzure ретрансляции с использованием проверки подлинности подписи общего доступа (SAS). Аналогичные слишком[сообщений Service Bus](../service-bus-messaging/service-bus-authentication-and-authorization.md), проверка подлинности SAS позволяет toohello tooauthenticate приложений службы ретрансляции в Azure, с помощью ключа доступа, настроенного в пространстве имен ретрансляции hello. Затем можно использовать этот ключа toogenerate токена подписи коллективного доступа, что клиенты могут использовать службу ретрансляции toohello tooauthenticate.

## <a name="shared-access-signature-authentication"></a>Проверка подлинности с помощью подписанного URL-адреса
[Проверка подлинности SAS](../service-bus-messaging/service-bus-sas.md) позволяет вам toogrant ресурсам пользователя доступ tooAzure ретрансляции с определенными правами. Проверка подлинности SAS включается конфигурация hello криптографического ключа со связанными правами для ресурса. Клиенты получают доступ toothat ресурсов, предоставляя маркер SAS, который состоит из hello ресурса (URI) для вызываемой и срока действия подписана hello настроен ключ.

Ключи для SAS можно настроить в пространстве имен ретранслятора. В отличие от обмена сообщениями в служебной шине, при [гибридных подключениях в ретрансляторе](relay-hybrid-connections-protocol.md) поддерживаются неавторизованные и анонимные отправители. Можно включить анонимный доступ для hello объекта при его создании, как показано в следующих из портала hello снимок экрана приветствия:

![][0]

toouse SAS, можно настроить [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) объекта в пространстве имен ретрансляции, которая состоит из следующих hello:

* *KeyName* , определяющее правило hello.
* *PrimaryKey* является toosign и проверки токенов SAS используется криптографический ключ.
* *SecondaryKey* toosign и проверки токенов SAS используется криптографический ключ.
* *Права* представляющий hello коллекция прослушивания, отправку или управление предоставлены права.

Правила авторизации, настроенные на уровне пространства имен hello могут предоставлять доступ tooall подключений ретрансляции в пространстве имен для клиентов с токенами, подписанными соответствующим ключом hello. Копирование too12 такие правила авторизации можно настроить в пространстве имен ретрансляции. По умолчанию правило [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) со всеми правами настраивается для каждого пространства имен в ходе первоначальной подготовки.

tooaccess сущность hello клиенту требуется токен SAS, созданный с помощью определенного [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Hello маркер SAS создается с использованием HMAC-SHA256 строки ресурса, состоящий из ресурсов hello доступа toowhich URI запрашивается приветствия и срока действия с криптографическим ключом, связанным с правилом авторизации hello.

Поддержка проверки подлинности SAS для ретрансляции Azure включены hello Azure .NET SDK версии 2.0 и более поздней версии. SAS включает в себя поддержку правила [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Все интерфейсы API, которые принимают строку подключения в качестве параметра, поддерживают строки подключения SAS.

## <a name="next-steps"></a>Дальнейшие действия
- Дополнительные сведения о SAS см. в статье [Аутентификация служебной шины с помощью подписанных URL-адресов](../service-bus-messaging/service-bus-sas.md).
- . В разделе hello [руководство по Azure ретрансляции гибридные подключения протокола](relay-hybrid-connections-protocol.md) подробные сведения о hello возможность гибридных подключений.
- Соответствующую информацию о проверке подлинности и авторизации с помощью обмена сообщениями в служебной шине см. в [этой статье](../service-bus-messaging/service-bus-authentication-and-authorization.md). 

[0]: ./media/relay-authentication-and-authorization/hcanon.png