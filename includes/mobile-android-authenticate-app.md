
1. <span data-ttu-id="b17a0-101">Откройте проект в Android Studio.</span><span class="sxs-lookup"><span data-stu-id="b17a0-101">Open the project in Android Studio.</span></span>

2. <span data-ttu-id="b17a0-102">В **обозревателе проектов** в Android Studio откройте файл ToDoActivity.java и добавьте следующие операторы import:</span><span class="sxs-lookup"><span data-stu-id="b17a0-102">In **Project Explorer** in Android Studio, open the ToDoActivity.java file and add the following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="b17a0-103">Добавьте в класс **ToDoActivity** следующий метод:</span><span class="sxs-lookup"><span data-stu-id="b17a0-103">Add the following method to the **ToDoActivity** class:</span></span>

        // You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using the Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check the request code matches the one we send in the login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check the error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    <span data-ttu-id="b17a0-104">Этот код создает метод для обработки процесса проверки подлинности Google.</span><span class="sxs-lookup"><span data-stu-id="b17a0-104">This code creates a method to handle the Google authentication process.</span></span> <span data-ttu-id="b17a0-105">В диалоговом окне отображается идентификатор пользователя, прошедшего проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b17a0-105">A dialog displays the ID of the authenticated user.</span></span> <span data-ttu-id="b17a0-106">Вы сможете продолжить, только если проверка подлинности выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="b17a0-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b17a0-107">Если вы используете поставщик удостоверений, отличный от Google, измените значение, переданное в методе **login**, на одно из следующих значений: _MicrosoftAccount_, _Facebook_, _Twitter_ или _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="b17a0-107">If you are using an identity provider other than Google, change the value passed to the **login** method to one of the following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="b17a0-108">Добавьте в метод **onCreate** следующую строку после кода, который формирует экземпляр объекта `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="b17a0-108">In the **onCreate** method, add the following line of code after the code that instantiates the `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="b17a0-109">Этот вызов запускает процесс проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b17a0-109">This call starts the authentication process.</span></span>

5. <span data-ttu-id="b17a0-110">Переместите оставшийся код после `authenticate();` в методе **onCreate** в новый метод **createTable**.</span><span class="sxs-lookup"><span data-stu-id="b17a0-110">Move the remaining code after `authenticate();` in the **onCreate** method to a new **createTable** method:</span></span>

        private void createTable() {

            // Get the table instance to use.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter to bind the items with the view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load the items from Azure.
            refreshItemsFromTable();
        }

6. <span data-ttu-id="b17a0-111">Чтобы убедиться, что перенаправление работает должным образом, добавьте в файл _AndroidManifest.xml_ следующий фрагмент _RedirectUrlActivity_:</span><span class="sxs-lookup"><span data-stu-id="b17a0-111">To ensure redirection works as expected, add the following snippet of _RedirectUrlActivity_ to _AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="b17a0-112">Добавьте redirectUriScheme к _build.gradle_ приложения Android.</span><span class="sxs-lookup"><span data-stu-id="b17a0-112">Add redirectUriScheme to _build.gradle_ of your Android application.</span></span>

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

8. <span data-ttu-id="b17a0-113">Добавьте com.android.support:customtabs:23.0.1 к зависимостям в build.gradle:</span><span class="sxs-lookup"><span data-stu-id="b17a0-113">Add com.android.support:customtabs:23.0.1 to the dependencies in your build.gradle:</span></span>

      <span data-ttu-id="b17a0-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span><span class="sxs-lookup"><span data-stu-id="b17a0-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="b17a0-115">В меню **Запуск** щелкните **Запуск приложения**, чтобы запустить приложение и выполнить вход с помощью выбранного поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="b17a0-115">From the **Run** menu, click **Run app** to start the app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="b17a0-116">Упомянутая схема URL-адреса чувствительная к регистру.</span><span class="sxs-lookup"><span data-stu-id="b17a0-116">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="b17a0-117">Убедитесь, что во всех вхождениях `{url_scheme_of_you_app}` используется один и тот же регистр.</span><span class="sxs-lookup"><span data-stu-id="b17a0-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use the same case.</span></span>

<span data-ttu-id="b17a0-118">После входа мобильное приложение должно работать без ошибок, а у вас должна быть возможность отправлять запросы в серверную службу и обновлять данные.</span><span class="sxs-lookup"><span data-stu-id="b17a0-118">When you are successfully signed in, the app should run without errors, and you should be able to query the back-end service and make updates to data.</span></span>
