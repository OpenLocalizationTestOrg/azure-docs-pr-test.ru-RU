---
title: "Проверка подлинности Azure Active Directory tooconfigure aaaHow для приложения службы приложений"
description: "Узнайте, как проверка подлинности Azure Active Directory tooconfigure для приложения службы приложений."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: 6ec6a46c-bce4-47aa-b8a3-e133baef22eb
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5b1d73f8fdf5831a266d900cd07f4e3b0917a7f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-azure-active-directory-login"></a>Как tooconfigure вход Azure Active Directory toouse приложения служб приложений
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

В этом разделе показано, как toouse tooconfigure службы приложений Azure Active Directory Azure, как поставщик проверки подлинности.

## <a name="express"> </a>Настройка Azure Active Directory с помощью стандартных параметров
1. В hello [портал Azure], перейдите tooyour приложения. Щелкните **Параметры**, а затем — **Аутентификация или авторизация**.
2. Если hello проверки подлинности и авторизации не включена, включать hello слишком**на**.
3. Щелкните **Azure Active Directory**, а затем в разделе **Режим управления** выберите **Экспресс**.
4. Нажмите кнопку **ОК** tooregister приложения hello в Azure Active Directory. При этом будет создана новая регистрация. Если вместо этого требуется toochoose существующую регистрацию, нажмите кнопку **выбрать существующее приложение** и выполните поиск hello имя ранее созданной регистрации в клиенте.
   Щелкните tooselect регистрации hello ее и команду **ОК**. Нажмите кнопку **ОК** в колонке параметров hello Azure Active Directory.
   
   ![][0]
   
   По умолчанию приложение службы обеспечивает проверку подлинности, но не ограничивает содержимого узла tooyour авторизованный доступ и API-интерфейсы. Авторизация пользователей должна быть включена в код приложения.
5. (Необязательно) toorestrict доступа tooyour сайта tooonly пользователь аутентификацию в Azure Active Directory, установить **tootake действия, если запрос не прошел проверку подлинности** слишком**войти с использованием Azure Active Directory**. Это требует проверку подлинности всех запросов, и все запросы без проверки подлинности, перенаправленный tooAzure Active Directory для проверки подлинности.
6. Щелкните **Сохранить**.

Теперь вы находитесь готов toouse Azure Active Directory для проверки подлинности в приложении.

## <a name="advanced"> </a>(Альтернативный способ) Ручная настройка расширенных параметров Azure Active Directory
Вы также можете tooprovide параметры конфигурации вручную. Это решение hello предпочтительно, если вы хотите toouse клиента AAD hello отличается от клиента hello, с которым вы входите в Azure. Конфигурация toocomplete hello, необходимо сначала создать регистрацию в Azure Active Directory и затем необходимо предоставить некоторые tooApp сведения hello регистрации службы.

### <a name="register"> </a>Регистрация приложения в Azure Active Directory
1. Войдите на toohello [портал Azure]и перейдите tooyour приложения. Скопируйте свой **URL-адрес**. Вы воспользуетесь этой tooconfigure приложения Azure Active Directory.
2. Войдите в toohello [классический портал Azure] и перейдите в слишком**Active Directory**.
   
    ![][2]
3. Выберите свой каталог, а затем выберите hello **приложений** вкладку вверху hello. Нажмите кнопку **добавить** в нижней hello toocreate Регистрация нового приложения.
4. Выберите команду **Добавить приложение, разрабатываемое моей организацией**.
5. В мастер приложения hello, введите **имя** для вашего приложения и нажмите кнопку hello **веб-приложение и/или Web API** типа. Нажмите кнопку toocontinue.
6. В hello **URL-адрес входа** вставьте скопированный ранее URL-адрес приложения hello. Введите этот же URL-адрес в hello **URI идентификатора приложения** поле. Нажмите кнопку toocontinue.
7. После добавления приложения hello щелкните hello **Настройка** вкладки. Изменить hello **URL-адрес ответа** под **единого входа** URL-адрес приложения дополненная путь hello для hello toobe */.auth/login/aad/callback*. Например, `https://contoso.azurewebsites.net/.auth/login/aad/callback`. Убедитесь, что вы используете hello схему HTTPS.
   
    ![][3]
8. Щелкните **Сохранить**. А затем копировать hello **идентификатор клиента** для приложения hello. Вы настроите вашего приложения toouse это позже.
9. В нижней панели команд hello, нажмите кнопку **Просмотр конечных точек**и затем копировать hello **документа метаданных федерации** URL-адрес и загрузки, документ или перейдите tooit в браузере.
10. В корневой hello **EntityDescriptor** элемент, должно быть **entityID** виде hello `https://sts.windows.net/` следуют клиента определенной tooyour GUID (называемые «идентификатор клиента»). Скопируйте это значение — оно будет использоваться в качестве вашего **URL-адреса издателя**. Вы настроите вашего приложения toouse это позже.

### <a name="secrets"></a>Tooyour приложения добавьте Azure Active Directory сведения
1. Вернитесь в hello [портал Azure], перейдите tooyour приложения. Щелкните **Параметры**, а затем — **Аутентификация или авторизация**.
2. Если не включена функция проверки подлинности и авторизации hello, включите параметр hello слишком**на**.
3. Щелкните **Azure Active Directory**, а затем в разделе **Режим управления** выберите **Дополнительно**. Вставить в hello идентификатор клиента и URL-адрес издателя значение которого был получен. Нажмите кнопку **ОК**.
   
   ![][1]
   
   По умолчанию приложение службы обеспечивает проверку подлинности, но не ограничивает содержимого узла tooyour авторизованный доступ и API-интерфейсы. Авторизация пользователей должна быть включена в код приложения.
4. (Необязательно) toorestrict доступа tooyour сайта tooonly пользователь аутентификацию в Azure Active Directory, установить **tootake действия, если запрос не прошел проверку подлинности** слишком**войти с использованием Azure Active Directory**. Это требует проверку подлинности всех запросов, и все запросы без проверки подлинности, перенаправленный tooAzure Active Directory для проверки подлинности.
5. Щелкните **Сохранить**.

Теперь вы находитесь готов toouse Azure Active Directory для проверки подлинности в приложении.

## <a name="optional-configure-a-native-client-application"></a>(Необязательно.) Настройка собственного клиентского приложения
Azure Active Directory можно также tooregister собственных клиентов, который предоставляет больший контроль над разрешениями для сопоставления. Это необходимо при желании tooperform входа, с использованием библиотеки, например hello **библиотеку аутентификации Active Directory**.

1. Перейдите в слишком**Active Directory** в hello [классический портал Azure].
2. Выберите свой каталог, а затем выберите hello **приложений** вкладку вверху hello. Нажмите кнопку **добавить** в нижней hello toocreate Регистрация нового приложения.
3. Выберите команду **Добавить приложение, разрабатываемое моей организацией**.
4. В мастер приложения hello, введите **имя** для вашего приложения и нажмите кнопку hello **собственное клиентское приложение** типа. Нажмите кнопку toocontinue.
5. В hello **URI перенаправления** введите свой сайт */.auth/login/done* конечную точку, используя hello схему HTTPS. Это значение должно быть примерно слишком*https://contoso.azurewebsites.net/.auth/login/done*. Создание приложения Windows, вместо этого использовать hello [пакета SID](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) как hello URI.
6. После добавления собственное приложение hello щелкните hello **Настройка** вкладки. Найти hello **идентификатор клиента** и запомните или запишите это значение.
7. Страница приветствия прокрутки вниз toohello **разрешения приложений tooother** и нажмите кнопку **добавить приложение**.
8. Поиск веб-приложения hello, ранее зарегистрированы и щелкните значок "плюс" hello. Щелкните флажок tooclose hello hello-диалоговое окно. Если веб-приложение hello не удается найти перейдите tooits регистрации и добавить новый URL-адрес ответа (например, hello HTTP версия текущего URL-адреса), нажмите кнопку Сохранить, а затем повторите эти шаги - приложения hello должно отображаться в списке hello.
9. На только что добавили новую запись hello, откройте hello **делегированные разрешения** раскрывающийся список и выберите **доступа (appName)**. Нажмите кнопку **Сохранить**.

Теперь вы настроили собственное клиентское приложение, у которого есть доступ к вашему приложению службы приложений.

## <a name="related-content"> </a>Связанная информация
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-express-settings.png
[1]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-advanced-settings.png
[2]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-navigate-aad.png
[3]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-aad-app-configure.png

<!-- URLs. -->

[портал Azure]: https://portal.azure.com/
[классический портал Azure]: https://manage.windowsazure.com/
[alternative method]:#advanced
