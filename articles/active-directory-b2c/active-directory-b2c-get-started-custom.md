---
title: "Azure Active Directory B2C: начало работы с настраиваемыми политиками | Документы Майкрософт"
description: "Как tooget работу с Azure Active Directory B2C пользовательских политик"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a>Azure Active Directory B2C: начало работы с настраиваемыми политиками

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

После выполнения шагов hello в этой статье, настраиваемой политики будет поддерживать «локальная учетная запись» зарегистрироваться или войти через адрес электронной почты и пароль. Кроме того, будет подготовлена среда для добавления поставщиков удостоверений (например, Facebook или Azure Active Directory). Мы рекомендуем вам toocomplete использует следующие действия перед чтением о других hello платформы качества идентификации B2C Azure Active Directory (Azure AD).

## <a name="prerequisites"></a>Предварительные требования

Прежде чем продолжить, убедитесь, что у вас есть клиент Azure AD B2C, который является контейнером для всех пользователей, приложений, политик и т. д. Если у еще его нет, то необходимо слишком[создание клиента Azure AD B2C](active-directory-b2c-get-started.md). Настоятельно рекомендуем toocomplete hello все разработчики пошаговые руководства по Azure AD B2C встроенные политики и настроить свои приложения с помощью встроенных политик перед продолжением. Приложения будут работать с обоими типами политик, сделав незначительное изменение toohello политики имя tooinvoke hello пользовательскую политику.

>[!NOTE]
>tooaccess редактирования пользовательской политики, необходимо, чтобы клиент связанного tooyour действительной подписки Azure. Если вы еще не [вашей tooan клиента Azure AD B2C подписки Azure связаны](active-directory-b2c-how-to-enable-billing.md) или подписка Azure отключена, hello Identity Framework качества кнопка будет недоступна.

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a>Добавить подписывания и шифрования клиента tooyour B2C ключи для использования с пользовательской политики

1. Откройте hello **Identity Framework качества** колонки в параметрах клиента Azure AD B2C.
2. Выберите **ключей политики** ключей tooview hello, доступных в клиенте.
3. Создайте B2C_1A_TokenSigningKeyContainer, если он не существует:<br>
    а. Выберите **Добавить**. <br>
    b. Выберите **Создать**.<br>
    c. Для параметра **Имя** используйте значение `TokenSigningKeyContainer`. <br> 
    префикс Hello `B2C_1A_` могут быть добавлены автоматически.<br>
    d. Для параметра **Тип ключа** используйте значение **RSA**.<br>
    д. Для **даты**, используйте значения по умолчанию hello. <br>
    f. Для параметра **Использование ключа** задайте значение **Подпись**.<br>
    ж. Нажмите кнопку **Создать**.<br>
4. Создайте B2C_1A_TokenEncryptionKeyContainer, если он не существует:<br>
 а. Выберите **Добавить**.<br>
 b. Выберите **Создать**.<br>
 c. Для параметра **Имя** используйте значение `TokenEncryptionKeyContainer`. <br>
   префикс Hello `B2C_1A`_ могут быть добавлены автоматически.<br>
 d. Для параметра **Тип ключа** используйте значение **RSA**.<br>
 д. Для **даты**, используйте значения по умолчанию hello.<br>
 f. Для параметра **Использование ключа** задайте значение **Шифрование**.<br>
 g. Нажмите кнопку **Создать**.<br>
5. Создайте B2C_1A_FacebookSecret. <br>
Если уже имеется секрет приложения Facebook, добавьте его в качестве ключа tooyour политики клиента. В противном случае необходимо создать ключ hello с значение-заполнитель, чтобы политик прошел проверку.<br>
 а. Выберите **Добавить**.<br>
 b. В пункте **Параметры** используйте вариант **Вручную**.<br>
 c. Для параметра **Имя** используйте значение `FacebookSecret`. <br>
 префикс Hello `B2C_1A_` могут быть добавлены автоматически.<br>
 d. В hello **секрет** введите ваш FacebookSecret от developers.facebook.com или `0` как заполнитель. *Это не идентификатор приложения Facebook.* <br>
 д. Для параметра **Использование ключа** задайте значение **Подпись**. <br>
 Е. Выберите **Создать** и подтвердите создание.

## <a name="register-identity-experience-framework-applications"></a>Регистрация приложений инфраструктуры процедур идентификации

Azure AD B2C требует tooregister два дополнительных приложений, которые используются toosign engine hello вверх и регистрация пользователей.

>[!NOTE]
>Необходимо создать два приложения, разрешить вход с использованием локальных учетных записей: IdentityExperienceFramework (веб-приложение) и ProxyIdentityExperienceFramework (собственное приложение) с делегировать разрешения IdentityExperienceFramework приложение hello. Локальные учетные записи хранятся только в клиенте. Пользователи подписаться на уникальный почтовый адрес и пароль сочетания tooaccess приложений клиент зарегистрирован.

### <a name="create-hello-identityexperienceframework-application"></a>Создание приложения hello IdentityExperienceFramework

1. В hello [портал Azure](https://portal.azure.com), для переключения в hello [контекст клиента Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md).
2. Откройте hello **Azure Active Directory** колонке (не hello **Azure AD B2C** колонке). Может потребоваться tooselect **более служб** toofind его.
3. Щелкните **Регистрация приложений**.
4. Выберите **Регистрация нового приложения**.
   * Для параметра **Имя** используйте значение `IdentityExperienceFramework`.
   * Для параметра **Тип приложения** используйте значение **Веб-приложение/API**.
   * Для параметра **URL-адрес входа** используйте адрес `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, где `yourtenant` — это доменное имя клиента Azure AD B2C.
5. Нажмите кнопку **Создать**.
6. После его создания, выберите только что созданный hello приложение **IdentityExperienceFramework**.<br>
   * Выберите **Свойства**.<br>
   * Скопируйте идентификатор приложения hello и сохраните его на более поздний срок.

### <a name="create-hello-proxyidentityexperienceframework-application"></a>Создание приложения hello ProxyIdentityExperienceFramework

1. Щелкните **Регистрация приложений**.
1. Выберите **Регистрация нового приложения**.
   * Для параметра **Имя** используйте значение `ProxyIdentityExperienceFramework`.
   * Для параметра **Тип приложения** используйте значение **Встроенное**.
   * Для параметра **URI перенаправления**, используйте адрес `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, где `yourtenant` — это ваш клиент Azure AD B2C.
1. Нажмите кнопку **Создать**.
1. Как только будет создана, выберите приложение hello **ProxyIdentityExperienceFramework**.<br>
   * Выберите **Свойства**. <br>
   * Скопируйте идентификатор приложения hello и сохраните его на более поздний срок.
1. Выберите **Необходимые разрешения**.
1. Выберите **Добавить**.
1. Выберите **Выбор API**.
1. Поиск имени hello IdentityExperienceFramework. Выберите **IdentityExperienceFramework** в hello результатов и нажмите кнопку **выберите**.
1. Установите флажок "hello" рядом слишком**IdentityExperienceFramework доступа**и нажмите кнопку **выберите**.
1. Нажмите кнопку **Готово**.
1. Выберите **Предоставление разрешений**, затем **Да** для подтверждения.

## <a name="download-starter-pack-and-modify-policies"></a>Скачивание начального пакета и изменение политик

Настраиваемые политики — это набор XML-файлы, требующие клиента Azure AD B2C tooyour toobe отправлен. Мы предоставляем tooget пакеты начального вам быстро. Каждый пакет начального в hello после списка содержит hello наименьшее количество технические профилей и поездок пользователя требуется tooachieve hello сценария, описанных:
 * LocalAccounts. Позволяет использовать hello локальных учетных записей.
 * SocialAccounts. Позволяет использовать hello только учетные записи социальных сетей (или федерации).
 * **SocialAndLocalAccounts**. Этот файл используется для пошагового руководства hello.
 * SocialAndLocalAccountsWithMFA. Сюда включены параметры локальной идентификации, многофакторной идентификации и идентификации с помощью социальных сетей.

Каждый начальный пакет содержит:

* Hello [основного файла](active-directory-b2c-overview-custom.md#policy-files) hello политики. Несколько изменений, которые требуется toohello базового.
* Hello [файла расширения](active-directory-b2c-overview-custom.md#policy-files) hello политики.  В этот файл вносится большинство изменений конфигурации.
* [Файлы проверяющей стороны](active-directory-b2c-overview-custom.md#policy-files) — это файлы, которые вызывает приложение для выполнения определенных задач.

>[!NOTE]
>Если редактор XML по своему поддерживает проверки, проверка файлов hello по схеме TrustFrameworkPolicy_0.3.0.0.xsd XML hello, расположенный в корневом каталоге hello пакета начального приветствия. При проверке по схеме XML определяются ошибки перед отправкой.

 Давайте приступим.

1. Скачайте пакет active-directory-b2c-custom-policy-starterpack из репозитория GitHub. [Загрузите ZIP-файл hello](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) или выполнения

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. Откройте папку SocialAndLocalAccounts hello.  базовый файл Hello (TrustFrameworkBase.xml) в этой папке содержит содержимое, необходимых для учетных записей локальных и социального и ресурсы. содержимое социальных Hello не влияет на шаги hello начало локальных учетных записей и выполнения.
3. Откройте файл TrustFrameworkBase.xml. Если вам нужен редактор XML, [попробуйте Visual Studio Code](https://code.visualstudio.com/download) — упрощенный кроссплатформенный редактор.
4. В корневом каталоге hello `TrustFrameworkPolicy` элемент, обновление hello `TenantId` и `PublicPolicyUri` атрибуты, заменив `yourtenant.onmicrosoft.com` с hello доменное имя вашего клиента Azure AD B2C:
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   >`PolicyId`— Имя политики hello, которое будет отображаться в портале hello и hello имя, по которому этот файл политики ссылаются другие файлы политики.

5. Сохраните файл hello.
6. Откройте файл TrustFrameworkExtensions.xml. Сделать hello и те же два изменения, заменив `yourtenant.onmicrosoft.com` с вашим клиентом Azure AD B2C. Сделать hello же замены в hello `<TenantId>` элемент для всех трех изменения. Сохраните файл hello.
7. Откройте файл SignUpOrSignIn.xml. Внести аналогичные изменения hello, заменив `yourtenant.onmicrosoft.com` с вашим клиентом Azure AD B2C в трех местах. Сохраните файл hello.
8. Сброс пароля открытым hello и профиль редактировать файлы. Внести аналогичные изменения hello, заменив `yourtenant.onmicrosoft.com` с вашим клиентом Azure AD B2C в трех местах в каждом файле. Сохраните файлы hello.

### <a name="add-hello-application-ids-tooyour-custom-policy"></a>Добавление настраиваемой политики удостоверения приложения tooyour hello
Добавление файла расширения toohello идентификаторы приложения hello (`TrustFrameworkExtensions.xml`):

1. В файле расширения hello (TrustFrameworkExtensions.xml) найдите элемент hello `<TechnicalProfile Id="login-NonInteractive">`.
2. Замените оба экземпляра `IdentityExperienceFrameworkAppId` с Идентификатором hello приложения hello Identity Framework качества приложения, созданного ранее. Пример:

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. Замените оба экземпляра `ProxyIdentityExperienceFrameworkAppId` с Идентификатором hello приложения Framework качества удостоверение прокси-сервера, ранее созданную приложения hello.
4. Сохраните файл расширений.

## <a name="upload-hello-policies-tooyour-tenant"></a>Отправка hello политики tooyour клиента

1. В hello [портал Azure](https://portal.azure.com), для переключения в hello [контекст клиента Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)и откройте hello **Azure AD B2C** колонку.
2. Выберите **Инфраструктура процедур идентификации**.
3. Щелкните **Отправить политику**.

    >[!WARNING]
    >файлы пользовательской политики Hello необходимо отправить в hello следующий порядок:

1. Отправьте файл TrustFrameworkBase.xml.
2. Отправьте файл TrustFrameworkExtensions.xml.
3. Отправьте файл SignUpOrSignin.xml.
4. Отправьте другие файлы политики.

При загрузке файла hello имя файла политики hello добавляется символ `B2C_1A_`.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Тестирование настраиваемой политики hello с использованием выполнить

1. Откройте **параметры Azure AD B2C** и перейти слишком**возможности платформы идентификации**.

   >[!NOTE]
   >**Теперь запустите** требует по крайней мере одно приложение toobe предварительно зарегистрирован на приветствия клиента. Приложения должны быть зарегистрированы в клиенте hello B2C, либо с помощью hello **приложений** пунктов меню в Azure AD B2C или с помощью платформы идентификации качества tooinvoke hello встроенные и пользовательские политики. Каждое приложение необходимо зарегистрировать один раз.<br><br>
   toolearn приложений tooregister. в статье hello Azure AD B2C [приступить к работе](active-directory-b2c-get-started.md) статьи или hello [регистрацию приложения](active-directory-b2c-app-registration.md) статьи.  

2. Откройте B2C_1A_signup_signin, hello проверяющей стороны (RP) настраиваемой политики загруженный. Выберите **Запустить сейчас**.

3. Должно быть toosign доступ с помощью адреса электронной почты.

4. Выполните вход с hello учетную запись, у вас есть tooconfirm hello правильную конфигурацию.

>[!NOTE]
>Часто причина ошибки при входе заключается в неправильной настройке приложения IdentityExperienceFramework.


## <a name="next-steps"></a>Дальнейшие действия

### <a name="add-facebook-as-an-identity-provider"></a>Добавление Facebook в качестве поставщика удостоверений
tooset копирование Facebook:
1. [Настройте приложение Facebook на сайте developers.facebook.com](active-directory-b2c-setup-fb-app.md).
2. [Добавление клиента секретный tooyour Azure AD B2C приложения Facebook hello](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).
3. В файле политики TrustFrameworkExtensions hello, замените значение hello `client_id` с Идентификатором приложения Facebook hello:

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. Отправьте hello TrustFrameworkExtensions.xml политики файл tooyour клиента.
5. Тест с помощью **запустить сейчас** или путем вызова hello политики непосредственно из зарегистрированного приложения.

### <a name="add-azure-active-directory-as-an-identity-provider"></a>Добавление Azure Active Directory в качестве поставщика удостоверений
Hello основного файла уже используется данного руководства по началу работы содержит часть содержимого hello, который необходим для добавления других поставщиков удостоверений. Сведения о настройке входа в систему см. в разделе hello [Azure Active Directory B2C: Войдите, используя учетные записи Azure AD](active-directory-b2c-setup-aad-custom.md) статьи.

Общие сведения о настраиваемых политик в Azure AD B2C, использующих hello Identity Framework качества разделе hello [Azure Active Directory B2C: настраиваемые политики](active-directory-b2c-overview-custom.md) статьи. 
