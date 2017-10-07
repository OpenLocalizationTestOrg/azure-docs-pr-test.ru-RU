---
title: "aaaAzure многофакторной проверки Подлинности сервера Mobile App Web Service | Документы Microsoft"
description: "приложение для проверки подлинности Microsoft Hello предлагает параметр дополнительной проверки подлинности по каналу.  Она позволяет hello toousers toouse принудительной уведомления для многофакторной проверки Подлинности сервера."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 6c8d6fcc-70f4-4da4-9610-c76d66635b8b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 4175b68fcbf85ec3fd53d8edf4e07306c75a4c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-mobile-app-authentication-with-azure-multi-factor-authentication-server"></a>Включение аутентификации мобильных приложений с помощью сервера Многофакторной идентификации Azure

приложение для проверки подлинности Microsoft Hello предлагает параметр дополнительной проверки по каналу. Вместо автоматического телефонного звонка или SMS toohello пользователя во время входа, многофакторной проверки подлинности Azure отправляет приложением проверки подлинности Microsoft toohello уведомления на смартфоне или планшете пользователя hello. Hello пользователь просто касается **проверьте** (или вводит ПИН-код и нажимает кнопку «Проверить подлинность») в hello приложения toocomplete вход.

Использование мобильного приложения для двухфакторной проверки используется является предпочтительным, когда телефонная связь ненадежна. Если вы используете приложение hello как генератор токена OATH, он не требует любое соединение сети или Интернета.

В зависимости от среды, вы можете toodeploy hello мобильного приложения веб-службы на hello того же сервера как сервера Azure Multi-factor Authentication или на другом сервере с выходом в Интернет.

## <a name="requirements"></a>Требования

приложения для проверки подлинности Microsoft hello toouse hello требуются следующие сертификаты, чтобы hello приложение могло успешно взаимодействовать с веб-служба мобильного приложения:

* Требуется использовать сервер Многофакторной идентификации Azure 6.0 или более поздней версии.
* Необходимо установить веб-службу мобильного приложения на веб-сервере с выходом в Интернет, на котором выполняются службы Microsoft® [Internet Information Services (IIS) 7.x или более поздней версией](http://www.iis.net/).
* Установить, зарегистрировать и задать tooAllowed ASP.NET v4.0.30319
* К обязательным службам роли относятся ASP.NET и совместимость с метабазой IIS 6.
* Веб-служба мобильного приложения должна быть доступна через общедоступный URL-адрес.
* Веб-служба мобильного приложения должна быть защищена сертификатом SSL.
* Установить hello SDK Azure многофакторной проверки подлинности веб-службы в IIS 7.x или более поздней версии на hello **же сервере, что hello Azure многофакторной проверки подлинности сервера**
* SSL-сертификат, защищенный Hello Azure многофакторной проверки подлинности Web Service SDK.
* Веб-служба мобильного приложения могут подключаться toohello SDK веб-службы Azure многофакторной проверки подлинности по протоколу SSL
* Веб-служба мобильного приложения могут проходить проверку подлинности toohello SDK веб-службы Azure многофакторной проверки Подлинности с использованием учетных данных учетной записи службы, которая является членом группы безопасности «Администраторы PhoneFactor» hello hello. Эта учетная запись службы и группа присутствуют в Active Directory, если hello сервера Azure Multi-factor Authentication на сервере, присоединенном к домену. Эта учетная запись службы и группа существуют локально на приветствия сервера Azure Multi-factor Authentication, если это не присоединены к домену tooa домена.

## <a name="install-hello-mobile-app-web-service"></a>Установка веб-службы мобильного приложения hello

Перед установкой веб-служба мобильного приложения hello, следует учитывать приведенные ниже сведения hello.

* Требуется учетная запись службы, которая принадлежит к группе PhoneFactor Admins. Эта учетная запись может быть так же, как hello один используется для установки пользовательского портала hello hello.
* Это полезно tooopen веб-браузер на веб-сервере с выходом в Интернет hello и перехода toohello URL-адрес SDK веб-службы, который был введен в файл web.config hello hello. Если hello браузера может успешно получить toohello веб-службы, он запросит ввести учетные данные. Введите hello имя пользователя и пароль, которые были введены в файл web.config hello точно, как в файле hello. Убедитесь, что не отображаются предупреждения или ошибки сертификата.
* Если обратный прокси-сервер или брандмауэр сидели веб-сервера веб-служба мобильного приложения hello и выполнении SSL разгрузки, можно изменить файл web.config веб-служба мобильного приложения hello, поэтому hello веб-служба мобильного приложения могут использовать http вместо https. Протокол SSL по-прежнему необходим из hello мобильное приложение toohello брандмауэру или обратному прокси. Добавьте следующие ключевые toohello hello \<appSettings\> раздела:

        <add key="SSL_REQUIRED" value="false"/>

### <a name="install-hello-web-service-sdk"></a>Установка SDK веб-службы hello

В любом случае, если hello Azure многофакторной проверки подлинности Web Service SDK — **не** уже установлен на приветствия сервера Azure Multi-factor Authentication (MFA), полный hello шаги ниже.

1. Откройте консоль hello многофакторной проверки подлинности сервера.
2. Go toohello **Web Service SDK** и выберите **установить SDK веб-службы**.
3. Полный hello выполнить установку с помощью значения по умолчанию hello, если не требуется toochange их для какой-либо причине.
4. Привязки сайта toohello SSL-сертификат в службах IIS.

Если у вас есть вопросы о настройке SSL-сертификат на сервере IIS, см. в статье hello [как tooSet настройку SSL в IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Hello Web Service SDK должен быть защищен сертификатом SSL. Для этой цели подходит самозаверяющий сертификат. Импортируйте сертификат hello в хранилище «Доверенные корневые центры сертификации» hello hello локальной учетной записи компьютера на веб-сервере пользовательского портала hello, чтобы она доверяет этому сертификату при инициализации подключения SSL hello.

![Настройка конфигурации сервера MFA, вкладка "SDK веб-службы"](./media/multi-factor-authentication-get-started-server-webservice/sdk.png)

### <a name="install-hello-service"></a>Установите службу hello

1. **На hello многофакторной проверки Подлинности сервера**, укажите путь установки toohello.
2. Перейдите toohello папка, где hello установленных по умолчанию hello сервера Azure MFA **C:\Program Files\Azure Multi-factor Authentication**.
3. Найдите файл установки hello **MultiFactorAuthenticationMobileAppWebServiceSetup64**. Если сервер hello **не** с выходом в Интернет, toohello копирования hello установки файловый сервер с выходом в Интернет.
4. Если hello сервер многофакторной проверки Подлинности является **не** toohello Интернет-коммутатора **-сервере**.
5. Запустите hello **MultiFactorAuthenticationMobileAppWebServiceSetup64** установить файл с правами администратора, если требуется изменить hello сайта и изменить hello виртуальных каталогов tooa короткое имя, если вы хотите.
6. После завершения установки hello, Обзор слишком**C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService** (или в другой каталог на основе имени виртуального каталога hello) и измените файл Web.Config hello.

   * Найти ключ hello **«WEB_SERVICE_SDK_AUTHENTICATION_USERNAME»** и измените **значение = "»** слишком**значение = «Домен\пользователь»** где учетной записи службы, которая входит в домен Группа «Администраторы PhoneFactor».
   * Найти раздел hello **«WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD»** и измените **значение = "»** слишком**значение = «Password»** здесь пароль — пароль hello для hello службы Учетная запись указана в предыдущую строку hello.
   * Найти hello **pfMobile App Web Service_pfwssdk_PfWsSdk** задание и измените значение hello с **http://localhost: 4898/pfwssdk.asmx** toohello URL SDK веб-службы (пример: https://mfa.contoso.com/ MultiFactorAuthWebServiceSdk/PfWsSdk.asmx).
   * Сохраните файл Web.Config hello и закройте Блокнот.

   > [!NOTE]
   > Поскольку для этого подключения используется SSL, необходимо ссылаться hello Web Service SDK по **полное доменное имя (FQDN)** и **не IP-адресом**. Hello SSL-сертификат будет выдан для hello полное доменное имя и hello URL-адрес должен соответствовать hello имя на сертификате hello.

7. Если hello веб-сайта, веб-служба мобильного приложения был установлен в группе уже не было привязано подписанного общедоступным сертификатом, установите hello сертификат на сервере hello, откройте диспетчер служб IIS и привяжите веб-сайт toohello hello сертификата.
8. Откройте веб-браузер на любом компьютере и перейдите toohello URL-адрес, где установлена веб-служба мобильного приложения (пример: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService). Убедитесь, что не отображаются предупреждения или ошибки сертификата.

## <a name="configure-hello-mobile-app-settings-in-hello-azure-multi-factor-authentication-server"></a>Настройка параметров мобильного приложения hello в hello Azure многофакторной проверки подлинности сервера

Теперь, когда веб-служба мобильного приложения hello установлен, необходимо toowork сервера Azure Multi-factor Authentication hello tooconfigure с портала hello.

1. В консоли hello многофакторной проверки подлинности сервера щелкните значок пользовательского портала hello. Если пользователям разрешается toocontrol своими методами проверки подлинности, проверка **мобильное приложение** на hello "Параметры", в разделе **пользователи tooselect метод**. Без эта функция включена, конечным пользователям не требуется toocontact поддержки toocomplete активацию для мобильного приложения hello.
2. Проверьте hello **разрешить пользователям tooactivate мобильное приложение** поле.
3. Проверьте hello **разрешить регистрацию пользователей** поле.
4. Нажмите кнопку hello **мобильное приложение** значок.
5. Введите URL-адрес hello, используемая с hello виртуальный каталог, который был создан при установке MultiFactorAuthenticationMobileAppWebServiceSetup64 (пример: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService/) в поле hello  **URL-адрес службы Mobile App Web:**.
6. Заполнение hello **имя учетной записи** поле hello компании или организации toodisplay имя в hello мобильных приложений для этой учетной записи.
   ![Настройка сервера MFA, параметры для мобильного приложения](./media/multi-factor-authentication-get-started-server-webservice/mobile.png)

## <a name="next-steps"></a>Дальнейшие действия

- [Расширенные сценарии с использованием Многофакторной идентификации Azure и VPN сторонних поставщиков](multi-factor-authentication-advanced-vpn-configurations.md).