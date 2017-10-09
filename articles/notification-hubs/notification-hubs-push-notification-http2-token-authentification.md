---
title: "aaaToken (HTTP/2) проверка подлинности на основе для APNS в концентраторов уведомлений Azure | Документы Microsoft"
description: "В этом разделе объясняется, как tooleverage hello нового токена проверки подлинности для APNS"
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a>Проверка подлинности на основе токенов (HTTP/2) для APNS
## <a name="overview"></a>Обзор
В этой статье указаны как проверку подлинности на основе протокола hello новый toouse APNS HTTP/2 с маркером.

Hello основные преимущества использования нового протокола hello:
-   Создания токенов — относительно оскорблять свободного (сравниваемых toocertificates)
-   У токенов отсутствует срок окончания действия. Вы управляете их созданием и отзывом.
-   Полезные данные теперь можно вверх too4 КБ
- Синхронная обратная связь.
-   Вы используете Apple последнюю протокола — сертификаты по-прежнему использовать двоичный протокол hello, которая помечена для об устаревании

Этот новый механизм можно реализовать в два этапа за несколько минут:
1.  Получить hello из портала учетной записи разработчика Apple hello
2.  Настройка центра уведомлений с новыми данными hello

Концентраторы уведомлений сейчас все набор toouse hello новый системой проверки подлинности в APNS. 

Если для APNS вы использовали учетные данные сертификата, обратите внимание на следующее:
- свойства токена Hello перезаписать сертификат в нашей системе
- но приложение продолжает работать tooreceive уведомления без проблем.

## <a name="obtaining-authentication-information-from-apple"></a>Получение сведений о проверке подлинности от Apple
tooenable маркер проверки подлинности на основе необходимые hello следующие свойства из вашей учетной записи разработчика Apple.
### <a name="key-identifier"></a>Идентификатор ключа
Идентификатор ключа Hello можно получить на странице «Ключи» hello в учетной записи разработчика Apple

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a>Идентификатор и имя приложения
Имя приложения Hello доступна через страницу идентификаторы приложений hello в hello учетную запись разработчика. 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

Идентификатор приложения Hello доступна через hello страница сведений членства в hello учетную запись разработчика.
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a>Токен проверки подлинности
После создания маркера для приложения можно скачать Hello токена проверки подлинности. Подробнее о как toogenerate это маркер, см. в слишком[документации разработчика Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a>Настройка аутентификация токены toouse концентратора уведомлений
### <a name="configure-via-hello-azure-portal"></a>Настройка с использованием hello портал Azure
tooenable маркер проверки подлинности hello портала вход toohello портал Azure на основе и перейти tooyour концентратора уведомлений > служб Notification Services > Панель APNS. 

Там есть новое свойство *Режим проверки подлинности*. При выборе маркер позволяет tooupdate концентратор с hello соответствующих токенов свойств.

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- Введите свойства hello, полученный от учетной записи разработчика Apple 
- Выберите режим приложения (Production (Рабочий) или Sandbox (Песочница)). 
- Нажмите кнопку Сохранить tooupdate APNS учетные данные. 

### <a name="configure-via-management-api-rest"></a>Настройка с помощью API управления (REST)

Можно использовать наши [API-интерфейсы управления](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate аутентификация токены toouse концентратора уведомлений.
В зависимости от приложения hello, которую вы настраиваете "песочницы" производственного приложения или (указанный в учетной записи разработчика Apple) используйте один из hello соответствующие конечные точки.

- Конечная точка для "песочницы": [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device).
- Конечная точка рабочего приложения: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device).

> [!IMPORTANT]
> Для проверки подлинности на основе токенов требуется версия API **2017-04 или более поздняя**.
> 
> 

Ниже приведен пример tooupdate запрос PUT концентратора с проверкой подлинности на основе маркеров:


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a>Настройка с использованием hello .NET SDK
Можно настроить на токена проверки подлинности на основе toouse концентратора с помощью наших [последнюю версию пакета SDK для клиента](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8). 

Ниже приведен пример кода, иллюстрирующие правильное использование hello.


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a>Возврат toousing сертификат проверки подлинности на основе
Можно вернуться в любое время toousing сертификат проверки подлинности на основе с помощью любого предыдущего сертификата hello метода и передача вместо свойства токена hello. Ранее, действие перезаписывает hello сохраненные учетные данные.
