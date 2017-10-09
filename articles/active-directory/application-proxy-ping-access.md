---
title: "aaaHeader проверки подлинности на основе PingAccess для прокси приложения Azure AD | Документы Microsoft"
description: "Публикация приложений с помощью прокси приложения и PingAccess toosupport заголовок проверки подлинности на основе."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a>Аутентификация на основе заголовка для единого входа с использованием прокси приложения и PingAccess

Прокси приложения с Azure Active Directory и PingAccess партнерство вместе tooprovide клиентов Azure Active Directory с tooeven доступа нескольких приложений. PingAccess расширяет hello [существующие предложения прокси приложения](active-directory-application-proxy-get-started.md) tooapplications tooinclude единого входа, использовать заголовки для проверки подлинности.

## <a name="what-is-pingaccess-for-azure-ad"></a>Что такое PingAccess для Azure AD?

PingAccess для Azure Active Directory — это предложение PingAccess, позволяющий toogive пользователям доступ и один tooapplications входа, использовать заголовки для проверки подлинности. Прокси приложения обрабатывает эти приложения, как и любой другой с помощью Azure AD tooauthenticate access и затем передачу трафика через службу соединителя hello. PingAccess располагается перед приложения hello и преобразует hello токен доступа из Azure AD в заголовок, чтобы приложение hello получает hello проверки подлинности в формате hello, который может считывать.

Пользователи не будут Обратите внимание на то что-то иначе при входе в toouse корпоративных приложений. Они по-прежнему смогут работать в любом расположении и на любом устройстве. 

Поскольку соединителей прокси приложения hello направлять трафик tooall приложения, независимо от их типа проверки подлинности, они автоматически, а также продолжим tooload баланс.

## <a name="how-do-i-get-access"></a>Как мне получить доступ?

Так как этот сценарий предоставляется при совместном использовании Azure Active Directory и PingAccess, вам понадобятся лицензии для двух этих служб. Однако подписок Azure Active Directory Premium включает основные PingAccess лицензии, которая закрывает too20 приложений. Если вам требуется toopublish более 20 приложений на основе заголовка, вы можете приобрести дополнительную лицензию PingAccess. 

Дополнительные сведения см. в разделе [Выпуски Azure Active Directory](active-directory-editions.md).

## <a name="publish-your-application-in-azure"></a>Публикация приложения в Azure

Эта статья предназначена для тех, кто публикации приложения в этом сценарии для hello первый раз. Он рассматривается как tooget работу с приложением и PingAccess, кроме toohello шаги публикации. Если вы уже настроены обе службы, но хотите hello публикации действия в памяти, можно пропустить установки соединителя hello и переместить слишком[добавить вашего приложения tooAzure AD с помощью прокси приложения](#add-your-app-to-Azure-AD-with-Application-Proxy).

>[!NOTE]
>Так как этот сценарий предполагает партнерство между Azure AD и PingAccess, некоторые инструкции hello существуют на hello сайта Ping удостоверений.

### <a name="install-an-application-proxy-connector"></a>Установка соединителя прокси приложения

Если вы уже есть прокси приложения включен, а также установлен соединитель, можно пропустить этот раздел и перейти слишком[добавить вашего приложения tooAzure AD с помощью прокси приложения](#add-your-app-to-azure-ad-with-application-proxy).

Соединитель прокси приложения Hello является сервером Windows служба, которая направляет трафик hello из вашего tooyour удаленные сотрудники опубликованных приложений. Более подробные инструкции по установке см. в разделе [включить прокси приложения в Azure portal hello](active-directory-application-proxy-enable.md).

1. Войдите в toohello [портал Azure](https://portal.azure.com) роли глобального администратора.
2. Выберите **Azure Active Directory** > **Прокси приложения**.
3. Выберите **скачать соединитель** загрузки соединитель прокси приложения hello toostart. Следуйте инструкциям по установке hello.

   ![Включите прокси приложения и загрузить соединитель hello](./media/application-proxy-ping-access/install-connector.png)

4. Загрузка hello connector автоматически следует включить прокси приложения для каталога, но если не вы можете выбрать **включите прокси приложения**.


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a>Добавить tooAzure вашего приложения AD с помощью прокси приложения

Существуют два действия, необходимые tootake в hello портал Azure. Во-первых необходимо toopublish приложения с помощью прокси приложения. Затем необходимо toocollect некоторые сведения о приложение hello, который можно использовать во время действия PingAccess hello.

Выполните эти шаги toopublish приложения. Более подробное пошаговое руководство по этапам 1–8 приведено в разделе [Публикация приложений с помощью прокси приложения Azure AD](application-proxy-publish-azure-portal.md).

1. Если не был в последний раздел hello войдите toohello [портал Azure](https://portal.azure.com) роли глобального администратора.
2. Выберите **Azure Active Directory** > **Корпоративные приложения**.
3. Выберите **добавить** hello верхней части колонки hello.
4. Выберите **Локальное приложение**.
5. Заполните поля требуется hello со сведениями о нового приложения. Используйте следующие рекомендации для параметров hello hello.
   - **Внутренний URL-адрес**: обычно предоставляют hello URL-адрес, которое знакомит вас приложения toohello входа на странице при работе на hello корпоративной сети. В этом сценарии hello соединитель должен hello tootreat PingAccess прокси-сервера как hello обложке приложение hello. Используйте следующий формат: `https://<host name of your PA server>:<port>`. порт Hello — 3000 по умолчанию, но его можно настроить в PingAccess.
   - **Метод предварительной аутентификации** — выберите Azure Active Directory.
   - **Преобразование URL-адреса в заголовок** — выберите значение "Нет".

   >[!NOTE]
   >Если это первое приложение, используйте порт 3000 toostart и вернуться tooupdate этот параметр при изменении конфигурации PingAccess. Если это второй или более поздней версии приложения, это потребуется toomatch hello прослушивателя, настроенного в PingAccess. Узнайте больше о [прослушивателях в PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).

6. Выберите **добавить** hello нижней части колонки hello. Приложение добавляется, и откроется меню быстрого запуска "hello".
7. Выберите в меню быстрого запуска hello **назначение пользователей для тестирования**и добавьте по крайней мере один пользователь toohello приложения. Убедитесь, что эта учетная запись теста имеет доступ toohello локального приложения.
8. Выберите **назначить** назначение toosave hello тестового пользователя.
9. На панели управления приложения hello выберите **единого входа**.
10. Выберите **входа на базе заголовок** hello раскрывающегося меню. Щелкните **Сохранить**.

   >[!TIP]
   >Если вы впервые используете основано на заголовках единого входа необходимо tooinstall PingAccess. toomake убедитесь, что ваша подписка Azure автоматически связывается с установленной PingAccess использование hello связи на этой странице-toodownload PingAccess. Теперь откройте сайт загрузки hello или продолжить toothis страницу позже. 

   ![Выбор единого входа на основе заголовка](./media/application-proxy-ping-access/sso-header.PNG)

11. Закройте колонку приложения hello Enterprise или прокрутить меню "все hello способом toohello левой tooreturn toohello Azure Active Directory".
12. Щелкните **Регистрация приложений**.

   ![Выбор "Регистрация приложений"](./media/application-proxy-ping-access/app-registrations.png)

13. Приложения hello выберите только что добавленный, затем **URL-адреса ответа**.

   ![Выбор "URL-адреса ответа"](./media/application-proxy-ping-access/reply-urls.png)

14. Проверьте, toosee ли hello внешний URL-адрес, назначенный tooyour приложение на шаге 5 в списке URL-адреса ответа hello. В противном случае добавьте этот URL-адрес.
15. В колонке параметров приложения hello, выберите **требуемые разрешения**.

  ![Выбор "Необходимые разрешения"](./media/application-proxy-ping-access/required-permissions.png)

16. Выберите **Добавить**. Hello API, выберите **Windows Azure Active Directory**, затем **выберите**. Разрешения hello выберите **чтения и записи всех приложений** и **вход и чтение профиля пользователя**, затем **выберите** и **сделать**.  

  ![Выбор разрешений](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a>Собирать сведения о шагах PingAccess hello

1. В колонке параметров приложения щелкните **Свойства**. 

  ![Выбор "Свойства"](./media/application-proxy-ping-access/properties.png)

2. Сохранить hello **идентификатор приложения** значение. Используется для hello идентификатор клиента при настройке PingAccess.
3. В колонке параметров приложения hello, выберите **ключей**.

  ![Выбор "Ключи"](./media/application-proxy-ping-access/Keys.png)

4. Создайте ключ, введите описание ключа и выбрав дату окончания срока действия hello раскрывающееся меню.
5. Щелкните **Сохранить**. Отображается идентификатор GUID в hello **значение** поле.

  Сохраните это значение, как будет toosee может его снова после закрыть это окно.

  ![Создание ключа](./media/application-proxy-ping-access/create-keys.png)

6. Закройте колонку регистрации приложения hello или прокрутить меню "все hello способом toohello левой tooreturn toohello Azure Active Directory".
7. Выберите **Свойства**.
8. Сохранить hello **каталог с Идентификатором** GUID.

### <a name="optional---update-graphapi-toosend-custom-fields"></a>Необязательно: обновление GraphAPI toosend настраиваемые поля

Список маркеров безопасности, отправляемых Azure AD для проверки подлинности, см. в [справочнике по маркерам Azure AD](./develop/active-directory-token-and-claims.md). Пользовательское утверждение, отправляющий других токенов, используйте поле приложения hello tooset GraphAPI *acceptMappedClaims* слишком**True**. Эту конфигурацию можно использовать Azure AD Graph Explorer или Microsoft Graph toomake. 

В этом примере используется Graph Explorer.

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a>Скачивание PingAccess и настройка приложения

Теперь, когда вы выполнили все действия установки hello Azure Active Directory, можно переместить на tooconfiguring PingAccess. 

Hello подробное описание процедуры hello PingAccess частью данного сценария продолжить в hello документации удостоверение Ping [PingAccess настройки для Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).

Эти шаги содержат пошаговые инструкции процессе hello Получение учетной записи PingAccess, если у вас его еще нет, установка hello PingAccess сервера и создание подключение к поставщику Azure AD OIDC с помощью hello каталог с Идентификатором, скопированный из hello портал Azure. Затем используйте hello приложения идентификатор и ключ значения toocreate веб-сессию на PingAccess. После этого вы сможете настроить сопоставление удостоверений и создать виртуальный узел, сайт и приложение.

### <a name="test-your-app"></a>Тестирование приложения

Когда вы завершите выполнение этих шагов, ваше приложение будет настроено и запущено. tootest, откройте браузер и перейдите toohello внешний URL-адрес, созданный при публикации приложения hello в Azure. Войдите с помощью hello тестовой учетной записи, назначенной toohello приложение.

## <a name="next-steps"></a>Дальнейшие действия

- [Настройка PingAccess для Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [Как прокси приложения Azure AD предоставляет единый вход?](application-proxy-sso-overview.md)
- [Устранение неполадок прокси-сервера приложений](active-directory-application-proxy-troubleshoot.md)
