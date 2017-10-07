---
title: "aaaAuthenticate с Mobile Engagement API-интерфейс REST - Ручная настройка"
description: "Описывает, как настроить проверку подлинности для API-интерфейс REST Mobile Engagement в toomanually"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a>Проверка подлинности с помощью интерфейсов REST API Служб мобильного взаимодействия — настройка вручную
Это приложение документации слишком[аутентификация с помощью API-интерфейсов REST Mobile Engagement](mobile-engagement-api-authentication.md). Убедитесь, что вы прочитали первый контекст tooget hello. Описывает способ toodo hello однократно для настройки проверки подлинности для hello с помощью API-интерфейсов REST Mobile Engagement hello портала Azure. 

> [!NOTE]
> Приведенные ниже инструкции Hello основаны на этой [руководство по Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) и настраивать для требования проверки подлинности для API-интерфейсов Mobile Engagement. Поэтому tooit см. Если требуется, чтобы toounderstand hello описанные ниже шаги подробно. 
> 
> 

1. Tooyour входа учетной записи Azure через hello [классический портал](https://manage.windowsazure.com/).
2. Выберите **Active Directory** hello левой панели.
   
     ![выбор Active Directory][1]
3. Выберите hello **по умолчанию Active Directory** на портале Azure. 
   
     ![выбор каталога][2]
   
   > [!IMPORTANT]
   > Такой подход работает только в том случае, если вы работаете в Active Directory учетной записи по умолчанию hello и не будет работать, если вы выполняете это в Active Directory, созданной в вашей учетной записи. 
   > 
   > 
4. Щелкните tooview hello приложений в каталоге, **приложений**.
   
     ![просмотр приложений][3]
5. Нажмите кнопку **Добавить**. 
   
     ![добавление приложения][4]
6. Нажмите кнопку **Добавить приложение, которое разрабатывает моя организация**
   
     ![новое приложение][5]
7. Введите имя приложения hello и выберите hello типа приложения как **веб-приложение и/или WEB API** и нажмите кнопку Далее hello.
   
     ![указание имени приложения][6]
8. В полях **URL-адрес входа** и **URI кода приложения** можно указать любые фиктивные URL-адреса. Они не используются в нашем сценарии и URL-адреса hello сами не проверяются.  
   
     ![свойства приложения][7]
9. В конце этого hello имеется приложение AAD с именем hello, указанным ранее hello следующим образом. Это имя **AD\_APP\_NAME**. Запомните его.  
   
     ![имя приложения][8]
10. Щелкните имя приложения hello, нажмите кнопку на **Настройка**.
    
      ![настройка приложения][9]
11. Запишите идентификатор КЛИЕНТА, который будет использоваться в качестве hello **КЛИЕНТА\_идентификатор** API вызывает. 
    
     ![настройка приложения][10]
12. Прокрутите вниз toohello **ключей** и добавьте раздел длительностью предпочтительно 2 года (срок действия) и нажмите кнопку **Сохранить**. 
    
     ![настройка приложения][11]
13. Немедленно скопируйте hello значение, которое отображается для ключа hello, как он доступен только теперь и не сохраняются, поэтому не будет отображаться в дальнейшем, когда-либо. При утере, она будет создана toogenerate новый ключ. Это будет hello **CLIENT_SECRET** API вызывает. 
    
     ![настройка приложения][12]
    
    > [!IMPORTANT]
    > Этот ключ истекает в конце hello длительность hello, поэтому убедитесь, что toorenew, когда наступает время hello в противном случае API проверки подлинности работать не будет больше заданной. Если вам кажется, что ключ был скомпрометирован, удалите его и создайте заново.
    > 
    > 
14. Щелкните **Просмотр конечных ТОЧЕК** кнопки теперь которого будет открыть hello **конечные точки приложения** диалоговое окно. 
    
    ![][13]
15. Из диалогового окна конечные точки приложения hello, скопируйте hello **конечная точка МАРКЕРА OAUTH 2.0**. 
    
    ![][14]
16. Эта конечная точка будет находиться в следующие формы, где hello GUID в URL-АДРЕСЕ hello hello вашей **TENANT_ID** поэтому запомните или запишите его: 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. Теперь мы продолжится tooconfigure hello разрешения для этого приложения. Для этого необходимо будет tooopen копирование hello [портал Azure](https://portal.azure.com). 
18. Щелкните **групп ресурсов** и найти hello **мобильного охвата** группы ресурсов.  
    
    ![][15]
19. Щелкните hello **Mobile Engagement** ресурсов группы и перейдите toohello **параметры** здесь колонку. 
    
    ![][16]
20. Щелкните **пользователей** в hello колонку параметров и выберите команду **добавить** tooadd пользователя. 
    
    ![][17]
21. Нажмите кнопку **Выбрать роль**
    
    ![][18]
22. Нажмите кнопку **Владелец**
    
    ![][19]
23. Найдите имя своего приложения hello **AD\_приложения\_имя** в поле поиска hello. Здесь оно не отображается по умолчанию. После обнаружения, выберите его и щелкните **выберите** hello нижней части колонки hello. 
    
    ![][20]
24. На hello **Добавление доступа к** колонки, он будет отображаться как **1 пользователь, 0 групп**. Нажмите кнопку **ОК** об этом изменении hello tooconfirm колонку. 
    
    ![][21]

Hello необходимые конфигурации AAD успешно завершена, и являются все hello toocall набор API-интерфейсов. 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



