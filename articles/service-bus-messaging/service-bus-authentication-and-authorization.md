---
title: "aaaAzure шины службы проверки подлинности и авторизации | Документы Microsoft"
description: "Проверка подлинности приложений tooService шины с помощью проверки подлинности подписи общего доступа (SAS)."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 18bad0ed-1cee-4a5c-a377-facc4785c8c9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: sethm
ms.openlocfilehash: 898a2144c99d8fac074b6d85604f710bf512e71e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-and-authorization"></a>Аутентификация и авторизация в служебной шине

Приложения могут проходить проверку подлинности Service Bus с помощью подписи общего доступа (SAS) tooAzure проверки подлинности. Общие tooService подписи доступа проверки подлинности позволяет приложениям tooauthenticate шины с помощью клавиши доступа, настроенной на приветствия имен или сущности hello, с которым связаны определенные права. Затем можно использовать этот ключа toogenerate токена подписи коллективного доступа, что клиенты могут использовать tooauthenticate tooService шины.

> [!IMPORTANT]
> Вместо службы контроля доступа Azure Active Directory (также называется просто службой контроля доступа или ACS) следует использовать подписанный URL-адрес, так как ACS объявляется нерекомендуемой. Подписанный URL-адрес представляет собой простую, гибкую и удобную в использовании схему аутентификации в служебной шине. Приложения могут использовать SAS в сценариях, в которых они не обязательно toomanage понятие hello авторизованным «пользователем». Дополнительные сведения см. в [этой записи блога](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/).

## <a name="shared-access-signature-authentication"></a>Проверка подлинности с помощью подписанного URL-адреса

[Проверка подлинности SAS](service-bus-sas.md) позволяет вам toogrant ресурсам пользователя доступ tooService шины с определенными правами. Проверка подлинности SAS в Service Bus включается конфигурация hello криптографического ключа со связанными правами для ресурса Service Bus. Клиенты получают доступ toothat ресурсов, предоставляя маркер SAS, который состоит из hello ресурса (URI) для вызываемой и срока действия подписана hello настроен ключ.

Ключи для SAS можно настроить в пространстве имен служебной шины. ключ Hello применяется tooall сущностей обмена сообщениями в этом пространстве имен. Также можно настроить ключи для очередей и разделов служебной шины. Кроме того, SAS поддерживается в [ретрансляторе Azure](../service-bus-relay/relay-authentication-and-authorization.md).

toouse SAS, можно настроить [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) объектов на пространство имен, очередь или раздел. Это правило включает hello следующие элементы:

* *KeyName* , определяющее правило hello.
* *PrimaryKey* является toosign и проверки токенов SAS используется криптографический ключ.
* *SecondaryKey* toosign и проверки токенов SAS используется криптографический ключ.
* *Права* представляющий hello коллекция прослушивания, отправку или управление предоставлены права.

Правила авторизации, настроенные на уровне пространства имен hello могут предоставлять доступ tooall сущности в пространстве имен для клиентов с токенами, подписанными соответствующим ключом hello. Копирование too12 такие правила авторизации можно настроить на пространство имен Service Bus, очередь или раздел. По умолчанию правило [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) со всеми правами настраивается для каждого пространства имен в ходе первоначальной подготовки.

tooaccess сущность hello клиенту требуется токен SAS, созданный с помощью определенного [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Hello маркер SAS создается с использованием HMAC-SHA256 строки ресурса, состоящий из ресурсов hello доступа toowhich URI запрашивается приветствия и срока действия с криптографическим ключом, связанным с правилом авторизации hello.

Поддержка проверки подлинности SAS для Service Bus включены hello Azure .NET SDK версии 2.0 и более поздней версии. SAS включает в себя поддержку правила [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Все интерфейсы API, которые принимают строку подключения в качестве параметра, поддерживают строки подключения SAS.

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о SAS см. в статье [Аутентификация служебной шины с помощью подписанных URL-адресов](service-bus-sas.md).
- [Изменение пространства имен tooACS включено.](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- Соответствующую информацию об аутентификации и авторизации с помощью ретранслятора Azure см. в разделе [Проверка подлинности и авторизация в ретрансляторе Azure](../service-bus-relay/relay-authentication-and-authorization.md). 

