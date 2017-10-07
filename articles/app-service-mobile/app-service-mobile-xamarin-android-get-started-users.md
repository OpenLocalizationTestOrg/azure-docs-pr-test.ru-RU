---
title: "aaaGet запущена с использованием проверки подлинности для мобильных приложений в Xamarin Android"
description: "Узнайте, как toouse мобильные приложения tooauthenticate пользователей приложения Xamarin Android с помощью различных поставщиков удостоверений, включая AAD, Google, Facebook, Twitter и Майкрософт."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a>Добавить приложение Xamarin.Android tooyour проверки подлинности
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

В этом разделе показано, как пользователи tooauthenticate мобильного приложения из клиентского приложения. В этом учебнике добавьте проект краткое руководство toohello проверки подлинности, с помощью поставщика удостоверений, который поддерживается модулем мобильных приложений Azure. После успешного проверку подлинности и авторизации в мобильное приложение hello, отображается значение идентификатора пользователя hello.

Этот учебник основывается на примеры использования мобильного приложения hello. Также в первую очередь необходимо пройти учебник hello [Создание приложения Xamarin.Android]. Если вы не используете hello загружен быстрый запуск сервера проекта, необходимо добавить проект tooyour пакета расширения проверки подлинности hello. Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register"></a>Регистрация приложения для проверки подлинности и настройка служб приложений
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений

Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения. Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello. В этом учебнике мы используем схема URL-адресов hello _appname_ на протяжении. Тем не менее можно использовать любую схему URL-адресов на свой выбор. Он должен быть уникальным tooyour мобильного приложения. tooenable hello перенаправления на стороне сервера hello:

1. В hello [Azure портал] выберите приложение службы.

2. Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.

3. В hello **допускается внешний URL-адреса перенаправления**, введите `url_scheme_of_your_app://easyauth.callback`.  Hello **url_scheme_of_your_app** в данной строке — hello схема URL-адресов для мобильного приложения.  Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).  Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.

4. Нажмите кнопку **ОК**.

5. Щелкните **Сохранить**.

## <a name="permissions"></a>Ограничить разрешения пользователей tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

В Visual Studio или Xamarin Studio Запустите клиентский проект hello на устройстве или эмуляторе. Убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello. Это происходит потому, что приложение hello пытается tooaccess серверной части мобильное приложение как локальный пользователь. Hello *TodoItem* таблица теперь требует проверки подлинности.

Далее можно обновить ресурсов toorequest hello клиентского приложения из внутреннего сервера мобильного приложения hello с прошедшим проверку пользователем.

## <a name="add-authentication"></a>Добавить приложение toohello проверки подлинности
приложение Hello — hello tootap пользователей обновленные toorequire **входа** кнопку и пройти проверку подлинности перед отображением данных.

1. Добавьте следующий код toohello hello **TodoActivity** класса:
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    Это создает новый tooauthenticate метод пользователя и метод обработчика нового **входа** кнопки. Hello в приведенном выше примере кода hello происходит проверка подлинности с помощью имени входа для Facebook. Диалоговое окно является используется toodisplay hello ИД пользователя после проверки подлинности.
   
   > [!NOTE]
   > При использовании поставщика удостоверений, отличные от Facebook, измените значение hello передано слишком**LoginAsync** выше tooone hello следующее: *MicrosoftAccount*, *Twitter*, *Google*, или *WindowsAzureActiveDirectory*.
   > 
   > 
2. В hello **OnCreate** метода, delete или hello вне комментария, следующей строкой кода:
   
        OnRefreshItemsSelected ();
3. В файле Activity_To_Do.axml hello, добавьте следующее hello *LoginUser* кнопку определение перед hello существующих *AddItem* кнопки:
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. Добавьте следующие файл ресурсов Strings.xml toohello элемент hello:
   
        <string name="login_button_text">Sign in</string>
5. Откройте файл AndroidManifest.xml hello, добавьте следующий код внутри hello `<application>` XML-элемента:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. В Visual Studio и Xamarin Studio Запустите клиентский проект hello на устройстве или эмуляторе и войдите с помощью поставщика удостоверений для выбранного. После успешного входа в систему, приложение hello будет отображен идентификатор входа в систему, а hello список элементов todo и делает данные toohello обновлений.

<!-- URLs. -->
[Создание приложения Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md