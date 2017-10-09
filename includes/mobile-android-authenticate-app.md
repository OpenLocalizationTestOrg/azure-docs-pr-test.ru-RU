
1. Откройте проект hello в Android Studio.

2. В **обозревателя проектов** в Android Studio откройте файл ToDoActivity.java hello и добавьте следующие инструкции импорта hello:

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. Добавьте следующий метод toohello hello **ToDoActivity** класса:

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    Этот код создает метод toohandle hello процесс проверки подлинности Google. Диалоговое окно отображает идентификатор hello hello проверку подлинности пользователя. Вы сможете продолжить, только если проверка подлинности выполнена успешно.

    > [!NOTE]
    > При использовании поставщика удостоверений, отличные от Google, измените значение hello, переданный toohello **входа** tooone метод из hello следующие значения: _MicrosoftAccount_, _Facebook_, _Twitter_, или _windowsazureactivedirectory_.

4. В hello **onCreate** метод, добавить следующие строки кода после кода hello, которая создает hello hello `MobileServiceClient` объекта.

        authenticate();

    Этот вызов запускает процесс проверки подлинности hello.

5. Переместить hello, остальной код после `authenticate();` в hello **onCreate** tooa метод новый **createTable** метод:

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. tooensure перенаправление работает как ожидалось, добавить hello, следующий фрагмент _RedirectUrlActivity_ too_AndroidManifest.xml_:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. Добавьте too_build.gradle_ redirectUriScheme приложения Android.

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. Добавьте зависимости toohello com.android.support:customtabs:23.0.1 в ваш build.gradle:

      dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }

9. Из hello **запуска** меню, нажмите кнопку **запуск приложения** toostart hello приложение и выполните вход с помощью поставщика удостоверений выбранной.

> [!WARNING]
> Hello упомянутые схема URL-адресов с учетом регистра.  Убедитесь, что все вхождения `{url_scheme_of_you_app}` используйте hello же регистр.

Если вы успешно вошли, приложение hello выполняются без ошибок и необходимо быть внутренней службы может tooquery hello и вносить обновления toodata.
