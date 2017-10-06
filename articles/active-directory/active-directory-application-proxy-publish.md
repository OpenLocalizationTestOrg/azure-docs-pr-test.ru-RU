---
title: "aaaPublish приложений с помощью прокси приложения Azure AD | Документы Microsoft"
description: "Опубликуйте облако toohello локальных приложений с помощью прокси приложения Azure AD в классическом портале hello."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Публикация приложений с помощью прокси приложения Azure AD

> [!div class="op_single_selector"]
> * [портале Azure](application-proxy-publish-azure-portal.md)
> * [классическом портале Azure](active-directory-application-proxy-publish.md)

Прокси приложения Azure AD поможет поддерживать удаленные работники путем публикации toobe локальных приложений, доступны через hello Интернета. К этому моменту уже должна [включен прокси приложения в классический портал Azure hello](active-directory-application-proxy-enable.md). В этой статье рассматриваются hello действия toopublish приложений, работающих в локальной сети и обеспечивают безопасный удаленный доступ из за пределов вашей сети. После завершения этой статьи вы будете готовы tooconfigure приложения hello личные сведения или требования безопасности.

> [!NOTE]
> Прокси приложения — это функция, которая доступна только в том случае, если вы обновили toohello Premium или Basic edition Azure Active Directory. Дополнительные сведения см. в разделе [Выпуски Azure Active Directory](active-directory-editions.md). Если вы хотите toouse прокси-сервера приложений, вы можете [публиковать приложения в Azure portal hello](application-proxy-publish-azure-portal.md).

## <a name="publish-an-app-using-hello-wizard"></a>Публикация приложения с помощью мастера hello
1. Войдите как администратор в hello [классический портал Azure](https://manage.windowsazure.com/).
2. Вернитесь к tooActive каталог и выберите каталог hello, где вы включили прокси приложения.
   
    ![Active Directory — значок](./media/active-directory-application-proxy-publish/ad_icon.png)
3. Нажмите кнопку hello **приложений** , а затем щелкните hello **добавить** кнопку hello нижней части экрана приветствия
   
    ![Добавить приложение](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. Выберите **Публикация приложения, которое будет доступно за пределами вашей сети**.
   
    ![Публикация приложения, которое будет доступно за пределами вашей сети](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. Укажите следующую информацию о своем приложении hello:
   
   * **Имя**: hello понятное имя для вашего приложения. Оно должно быть уникальным в рамках вашего каталога.
   * **Внутренний URL-адрес**: адрес hello, соединитель прокси приложения hello используется приложение hello tooaccess из частной сети. Вы можете предоставить определенный путь в hello внутреннего сервера toopublish, пока hello rest сервера hello не опубликован. Таким образом, вы можете опубликовать разные сайты на hello того же сервера и дайте каждой из них собственного имени и правила доступа.
     
     > [!TIP]
     > При публикации путь, убедитесь, что он включает все необходимые изображения hello, сценариев и стилей для вашего приложения. Например если приложение находится на https://yourapp/app и использует образы, расположенный в https://yourapp/media, https://yourapp/ следует опубликовать как путь hello.
     > 
     > 
   * **Метод предварительной проверки подлинности**: как прокси-сервер приложения проверяет пользователей до предоставления им доступа tooyour приложения. Выберите один из вариантов hello hello раскрывающегося меню.
     
     * Azure Active Directory: Прокси-сервер приложения перенаправляет пользователей toosign вход с помощью Azure AD, который выполняет проверку подлинности их разрешения для каталога hello и приложения.
     * Passthrough: Пользователи не имеют приложения hello tooaccess tooauthenticate.
     
     ![Свойства приложения](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. Мастер toofinish hello, щелкните флажок hello hello нижней части экрана приветствия. Теперь приложение Hello определено в Azure AD.

## <a name="assign-users-and-groups-toohello-application"></a>Назначение пользователей и групп toohello приложения
В заказ для пользователей, tooaccess опубликованного приложения, необходимо tooassign их по отдельности или в группах. (Помните tooassign самостоятельно доступ, слишком.) Каждый назначаемый пользователь должен иметь лицензию на поддержку Azure Basic или более высокого уровня. Вы можете назначать лицензии по отдельности или toogroups. Дополнительные сведения см. в разделе [назначения пользователей приложения tooan](active-directory-applications-guiding-developers-assigning-users.md). 

Для приложений, требующих предварительной проверки подлинности Присвоение пользователю предоставляет разрешение toouse hello приложения. Для приложений, которые не требуют предварительной проверки подлинности, присвоение пользователю означает, что этот пользователь hello можно обращаться из приложения hello hello панели доступа.

1. После завершения мастера добавления приложений hello вы видите hello краткое руководство страницу приложения. Выберите toomanage, кто имеет доступ приложения toohello, **пользователей и групп**.
   
    ![Снимок экрана быстрого запуска прокси приложения: назначение пользователей](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. Выполните поиск конкретных групп в каталоге или выберите вывод списка всех пользователей. Результаты поиска toodisplay hello, щелкните флажок hello.
   
      ![Снимок экрана поиска групп или пользователей](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. Выберите пользователя или группы tooassign toothis приложения и щелкните **назначить**. Вы являетесь задаваемые tooconfirm это действие.

> [!NOTE]
> Для приложений со встроенной проверкой подлинности Windows можно назначить только пользователей и группы, которые синхронизированы в локальной службе Active Directory. Для приложений, опубликованных с помощью прокси приложения Azure Active Directory, нельзя назначить пользователей, использующих для входа учетную запись Майкрософт, а также гостей. Убедитесь, что пользователям вход с учетными данными, которые являются частью hello домену, в котором выполняется публикация приложения hello.
> 
> 

## <a name="test-your-published-application"></a>Тестирование опубликованного приложения
После публикации приложения можно проверить его, перейдя по URL-адрес toohello, которые опубликованы. Удостоверьтесь в том, что оно доступно, правильно отображается и что все работает надлежащим образом. Если проблема сохранится, или выдается сообщение об ошибке, попробуйте hello [руководство по устранению неполадок](active-directory-application-proxy-troubleshoot.md).

## <a name="configure-your-application"></a>Настройка приложения
Можно изменить опубликованные приложения или настроить дополнительные параметры на странице настройки hello. На этой странице можно настроить приложения, изменение имени hello или передаче эмблемы. Также можно управлять правилами доступа как hello метод предварительной проверки подлинности или многофакторной проверки подлинности.

![Расширенная конфигурация](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

После публикации приложений с помощью Active Directory прокси приложения Azure, они отображаются в списке приложений hello в Azure AD, и управлять ими существует.

Если после публикации приложений отключить службы прокси приложения, приложения hello доступным за пределами частной сети. Пользователи могут по-прежнему доступ hello приложения локально обычным образом.

tooview приложения, а также делать убедитесь что он доступен, дважды щелкните имя приложения hello hello. Если прокси-служба приложения hello отключена и не удается найти приложение hello, появится предупреждение hello верхней части экрана приветствия.

toodelete приложение, выберите приложение hello списка и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия
* [Публикация приложений с помощью доменного имени](active-directory-application-proxy-custom-domains.md)
* [Включение единого входа](active-directory-application-proxy-sso-using-kcd.md)
* [Включение условного доступа](active-directory-application-proxy-conditional-access.md)
* [Работа с приложениями, поддерживающими утверждения](active-directory-application-proxy-claims-aware-apps.md)

Для получения hello последние новости и обновления, посетите hello [блога прокси приложения](http://blogs.technet.com/b/applicationproxyblog/)

