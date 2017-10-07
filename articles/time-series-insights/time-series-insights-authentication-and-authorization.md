---
title: "aaaConfigure проверки подлинности и авторизации в пользовательское приложение, которое вызывает hello API аналитики ряда времени Azure | Документы Microsoft"
description: "В этом учебнике описано, как tooconfigure проверки подлинности и авторизации в пользовательское приложение, которое вызывает hello API аналитики ряда времени Azure"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a>Проверка подлинности и авторизация для API Azure Time Series Insights

В этой статье объясняется, как пользовательское приложение, которое вызывает tooconfigure hello Azure времени серии аналитики API.

## <a name="service-principal"></a>Субъект-служба

В этом разделе объясняется, как tooconfigure tooaccess приложения hello времени серии аналитики API от имени приложения hello. приложение Hello можно запрашивать данные или публикация ссылочных данных в среде времени серии аналитики hello с учетными данными приложения и не hello учетные данные.

При наличии в приложение, работающее tooaccess аналитики ряда времени, необходимо установить приложение Azure Active Directory и назначить политики доступа hello данных в среде времени серии аналитики hello. Этот подход является более предпочтительным, чем toorunning приложение hello в своих собственных учетных данных, так как:

* Можно назначить разрешения toohello удостоверения приложения, которые отличаются от собственных разрешений. Как правило эти разрешения являются ограниченными tooexactly какие hello приложению toodo. Например можно разрешить tooonly приложения hello чтения данных в конкретной среде аналитики ряда времени.
* Если изменить ваши обязанности приложение hello toochange учетные данные, вам не нужно.
* При запуске сценария автоматической установки можно использовать сертификата или ключа tooautomate проверки подлинности приложения.

В этой статье показано, как их по очереди перебирает tooperform hello портал Azure. Этот раздел посвящен приложения одного клиента, где приложение hello предполагаемого toorun в организации только один. Обычно однотенантная архитектура используется для создания бизнес-приложений в рамках организации.

поток Hello установки состоит из трех шагов высокого уровня.

1. Создайте приложение в Azure Active Directory.
2. Разрешить этой среды аналитики ряда времени приложения hello tooaccess.
3. Идентификатор приложения hello и ключа tooacquire маркера toohello `"https://api.timeseries.azure.com/"` аудитории или ресурса. маркер Hello можно затем используется toocall hello API аналитики ряда времени.

Ниже приведены hello подробное описание действий:

1. В hello портал Azure, выберите **Azure Active Directory** > **регистрации приложения** > **Регистрация нового приложения**.

   ![Регистрация нового приложения в Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. Присвойте toobe hello имя, выберите тип приложения hello **веб-приложения и API**, выберите любой допустимый URI для **URL-адрес входа**и нажмите кнопку **создать**.

   ![Создание приложения hello в Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. Выберите только что созданный приложения и скопируйте его приложения tooyour идентификатор любого текстового редактора.

   ![Скопируйте идентификатор приложения hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. Выберите **ключей**, введите имя ключа hello, выберите hello истечения срока действия и нажмите кнопку **Сохранить**.

   ![Выбор ключей приложения](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Введите имя ключа hello и истечения срока действия и нажмите кнопку Сохранить](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. Скопируйте hello ключа tooyour любого текстового редактора.

   ![Скопируйте ключ приложения hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. Среда времени серии Insights hello, выберите **политикам доступа** и нажмите кнопку **добавить**.

   ![Добавить новый среда доступа к данным политики toohello аналитики ряда времени](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. В hello **Выбор пользователя** диалоговое окно, имя приложения hello вставить (из шага 2) или идентификатор приложения (из шага 3).

   ![Поиск приложений в диалоговом окне Выбор пользователя hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. Выберите hello роли (**чтения** для запроса данных, **участника** для запроса данных и изменения эталонных данных) и нажмите кнопку **ОК**.

   ![В диалоговом окне выберите роль hello выбирает читателя или участника](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. Сохранить политику hello, щелкнув **ОК**.

10. Используйте идентификатор приложения hello (из шага 3) и маркер hello tooacquire ключа (из шага 5) приложения от имени приложения hello. Hello маркера затем можно передать в hello `Authorization` заголовка, когда приложение вызывает hello hello API аналитики ряда времени.

    При использовании C# можно использовать следующий код tooacquire hello токен имени приложения hello hello. Полный пример см. в статье [Запрос данных из среды Azure Time Series Insights с помощью C##](time-series-insights-query-data-csharp.md).

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a>Дальнейшие действия

Используйте идентификатор приложения hello и ключ в приложении. Пример кода, вызывает hello API аналитики ряда времени, в разделе [запрос данных с помощью C#](time-series-insights-query-data-csharp.md).

## <a name="see-also"></a>См. также

* [Запрос API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) для hello полный Справочник по API-Интерфейс запросов
* [Создание службы субъекта в hello портал Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md)
