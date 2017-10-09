
1. <span data-ttu-id="47d18-101">Откройте проект hello в Android Studio.</span><span class="sxs-lookup"><span data-stu-id="47d18-101">Open hello project in Android Studio.</span></span>

2. <span data-ttu-id="47d18-102">В **обозревателя проектов** в Android Studio откройте файл ToDoActivity.java hello и добавьте следующие инструкции импорта hello:</span><span class="sxs-lookup"><span data-stu-id="47d18-102">In **Project Explorer** in Android Studio, open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="47d18-103">Добавьте следующий метод toohello hello **ToDoActivity** класса:</span><span class="sxs-lookup"><span data-stu-id="47d18-103">Add hello following method toohello **ToDoActivity** class:</span></span>

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

    <span data-ttu-id="47d18-104">Этот код создает метод toohandle hello процесс проверки подлинности Google.</span><span class="sxs-lookup"><span data-stu-id="47d18-104">This code creates a method toohandle hello Google authentication process.</span></span> <span data-ttu-id="47d18-105">Диалоговое окно отображает идентификатор hello hello проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="47d18-105">A dialog displays hello ID of hello authenticated user.</span></span> <span data-ttu-id="47d18-106">Вы сможете продолжить, только если проверка подлинности выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="47d18-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="47d18-107">При использовании поставщика удостоверений, отличные от Google, измените значение hello, переданный toohello **входа** tooone метод из hello следующие значения: _MicrosoftAccount_, _Facebook_, _Twitter_, или _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="47d18-107">If you are using an identity provider other than Google, change hello value passed toohello **login** method tooone of hello following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="47d18-108">В hello **onCreate** метод, добавить следующие строки кода после кода hello, которая создает hello hello `MobileServiceClient` объекта.</span><span class="sxs-lookup"><span data-stu-id="47d18-108">In hello **onCreate** method, add hello following line of code after hello code that instantiates hello `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="47d18-109">Этот вызов запускает процесс проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="47d18-109">This call starts hello authentication process.</span></span>

5. <span data-ttu-id="47d18-110">Переместить hello, остальной код после `authenticate();` в hello **onCreate** tooa метод новый **createTable** метод:</span><span class="sxs-lookup"><span data-stu-id="47d18-110">Move hello remaining code after `authenticate();` in hello **onCreate** method tooa new **createTable** method:</span></span>

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

6. <span data-ttu-id="47d18-111">tooensure перенаправление работает как ожидалось, добавить hello, следующий фрагмент _RedirectUrlActivity_ too_AndroidManifest.xml_:</span><span class="sxs-lookup"><span data-stu-id="47d18-111">tooensure redirection works as expected, add hello following snippet of _RedirectUrlActivity_ too_AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="47d18-112">Добавьте too_build.gradle_ redirectUriScheme приложения Android.</span><span class="sxs-lookup"><span data-stu-id="47d18-112">Add redirectUriScheme too_build.gradle_ of your Android application.</span></span>

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

8. <span data-ttu-id="47d18-113">Добавьте зависимости toohello com.android.support:customtabs:23.0.1 в ваш build.gradle:</span><span class="sxs-lookup"><span data-stu-id="47d18-113">Add com.android.support:customtabs:23.0.1 toohello dependencies in your build.gradle:</span></span>

      <span data-ttu-id="47d18-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span><span class="sxs-lookup"><span data-stu-id="47d18-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="47d18-115">Из hello **запуска** меню, нажмите кнопку **запуск приложения** toostart hello приложение и выполните вход с помощью поставщика удостоверений выбранной.</span><span class="sxs-lookup"><span data-stu-id="47d18-115">From hello **Run** menu, click **Run app** toostart hello app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="47d18-116">Hello упомянутые схема URL-адресов с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="47d18-116">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="47d18-117">Убедитесь, что все вхождения `{url_scheme_of_you_app}` используйте hello же регистр.</span><span class="sxs-lookup"><span data-stu-id="47d18-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use hello same case.</span></span>

<span data-ttu-id="47d18-118">Если вы успешно вошли, приложение hello выполняются без ошибок и необходимо быть внутренней службы может tooquery hello и вносить обновления toodata.</span><span class="sxs-lookup"><span data-stu-id="47d18-118">When you are successfully signed in, hello app should run without errors, and you should be able tooquery hello back-end service and make updates toodata.</span></span>
