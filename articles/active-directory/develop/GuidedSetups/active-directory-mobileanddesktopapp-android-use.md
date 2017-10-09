---
title: "aaaAzure AD v2 Android Приступая к работе - Используйте | Документы Microsoft"
description: "Получение маркера доступа для приложения Android и вызов API Microsoft Graph или API, которые требуют маркер доступа, из конечной точки Azure Active Directory версии 2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 4480d89eb7638fe7d588c8cebd2b1e3c9d4c6e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="aba57-103">Использование библиотеки проверки подлинности Microsoft (MSAL) hello tooget маркер для hello Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="aba57-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

1.  <span data-ttu-id="aba57-104">Откройте `MainActivity` (выберите `app` > `java` > `{domain}.{appname}`).</span><span class="sxs-lookup"><span data-stu-id="aba57-104">Open: `MainActivity` (under `app` > `java` > `{domain}.{appname}`)</span></span>
2.  <span data-ttu-id="aba57-105">Добавьте следующие импорты hello:</span><span class="sxs-lookup"><span data-stu-id="aba57-105">Add hello following imports:</span></span>

```java
import android.app.Activity;
import android.content.Intent;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import com.android.volley.*;
import com.android.volley.toolbox.JsonObjectRequest;
import com.android.volley.toolbox.Volley;
import org.json.JSONObject;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import com.microsoft.identity.client.*;
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="aba57-106">Замените hello `MainActivity` класса ниже:</span><span class="sxs-lookup"><span data-stu-id="aba57-106">Replace hello `MainActivity` class with below:</span></span>
</li>
</ol>

```java
public class MainActivity extends AppCompatActivity {

    final static String CLIENT_ID = "[Enter hello application Id here]";
    final static String SCOPES [] = {"https://graph.microsoft.com/User.Read"};
    final static String MSGRAPH_URL = "https://graph.microsoft.com/v1.0/me";

    /* UI & Debugging Variables */
    private static final String TAG = MainActivity.class.getSimpleName();
    Button callGraphButton;
    Button signOutButton;

    /* Azure AD Variables */
    private PublicClientApplication sampleApp;
    private AuthenticationResult authResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        callGraphButton = (Button) findViewById(R.id.callGraph);
        signOutButton = (Button) findViewById(R.id.clearCache);

        callGraphButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onCallGraphClicked();
            }
        });

        signOutButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onSignOutClicked();
            }
        });

  /* Configure your sample app and save state for this activity */
        sampleApp = null;
        if (sampleApp == null) {
            sampleApp = new PublicClientApplication(
                    this.getApplicationContext(),
                    CLIENT_ID);
        }

  /* Attempt tooget a user and acquireTokenSilent
   * If this fails we do an interactive request
   */
        List<User> users = null;

        try {
            users = sampleApp.getUsers();

            if (users != null && users.size() == 1) {
          /* We have 1 user */

                sampleApp.acquireTokenSilentAsync(SCOPES, users.get(0), getAuthSilentCallback());
            } else {
          /* We have no user */

          /* Let's do an interactive request */
                sampleApp.acquireToken(this, SCOPES, getAuthInteractiveCallback());
            }
        } catch (MsalClientException e) {
            Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

        } catch (IndexOutOfBoundsException e) {
            Log.d(TAG, "User at this position does not exist: " + e.toString());
        }

    }

//
// App callbacks for MSAL
// ======================
// getActivity() - returns activity so we can acquireToken within a callback
// getAuthSilentCallback() - callback defined toohandle acquireTokenSilent() case
// getAuthInteractiveCallback() - callback defined toohandle acquireToken() case
//

    public Activity getActivity() {
        return this;
    }

    /* Callback method for acquireTokenSilent calls 
     * Looks if tokens are in hello cache (refreshes if necessary and if we don't forceRefresh)
     * else errors that we need toodo an interactive request.
     */
    private AuthenticationCallback getAuthSilentCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call Graph now */
                Log.d(TAG, "Successfully authenticated");

            /* Store hello authResult */
                authResult = authenticationResult;

            /* call graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                } else if (exception instanceof MsalUiRequiredException) {
                /* Tokens expired or no session, retry with interactive */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }


    /* Callback used for interactive request.  If succeeds we use hello access
         * token toocall hello Microsoft Graph. Does not check cache
         */
    private AuthenticationCallback getAuthInteractiveCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call graph now */
                Log.d(TAG, "Successfully authenticated");
                Log.d(TAG, "ID Token: " + authenticationResult.getIdToken());

            /* Store hello auth result */
                authResult = authenticationResult;

            /* call Graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }

    /* Set hello UI for successful token acquisition data */
    private void updateSuccessUI() {
        callGraphButton.setVisibility(View.INVISIBLE);
        signOutButton.setVisibility(View.VISIBLE);
        findViewById(R.id.welcome).setVisibility(View.VISIBLE);
        ((TextView) findViewById(R.id.welcome)).setText("Welcome, " +
                authResult.getUser().getName());
        findViewById(R.id.graphData).setVisibility(View.VISIBLE);
    }

    /* Use MSAL tooacquireToken for hello end-user
     * Callback will call Graph api w/ access token & update UI
     */
    private void onCallGraphClicked() {
        sampleApp.acquireToken(getActivity(), SCOPES, getAuthInteractiveCallback());
    }

    /* Handles hello redirect from hello System Browser */
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        sampleApp.handleInteractiveRequestRedirect(requestCode, resultCode, data);
    }

}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="aba57-107">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="aba57-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="aba57-108">Интерактивное получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="aba57-108">Getting a user token interactive</span></span>
<span data-ttu-id="aba57-109">Вызов hello `AcquireTokenAsync` toosign пользователя в hello результаты метода в окне запроса.</span><span class="sxs-lookup"><span data-stu-id="aba57-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="aba57-110">Приложения обычно требуют toosign пользователя в интерактивном режиме hello первый раз, они должны tooaccess защищенному ресурсу или при tooacquire операции в фоновом режиме, может произойти сбой маркера (например hello пользователя срок действия пароля истек).</span><span class="sxs-lookup"><span data-stu-id="aba57-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="aba57-111">Автоматическое получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="aba57-111">Getting a user token silently</span></span>
<span data-ttu-id="aba57-112">`AcquireTokenSilentAsync` обрабатывает получение и обновление маркера без участия пользователя.</span><span class="sxs-lookup"><span data-stu-id="aba57-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="aba57-113">После `AcquireTokenAsync` выполняется для hello первый раз `AcquireTokenSilentAsync` tooobtain токены hello распространенным методом tooaccess защищенные ресурсы для последующих вызовов — как вызовы toorequest или обновить маркеры выполняются без вмешательства пользователя.</span><span class="sxs-lookup"><span data-stu-id="aba57-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello method commonly used tooobtain tokens tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="aba57-114">Со временем `AcquireTokenSilentAsync` завершится ошибкой, — например hello пользователя выполнен выход или изменил свой пароль на другом устройстве.</span><span class="sxs-lookup"><span data-stu-id="aba57-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="aba57-115">Когда MSAL обнаруживает, что hello проблему можно устранить путем интерактивного вмешательства, в `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="aba57-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="aba57-116">Приложение может обработать это исключение двумя способами:</span><span class="sxs-lookup"><span data-stu-id="aba57-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="aba57-117">Звонок от `AcquireTokenAsync` немедленно, в результате запроса пользователя hello в toosign.</span><span class="sxs-lookup"><span data-stu-id="aba57-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="aba57-118">Этот шаблон обычно используется в веб-приложений там, где отсутствует не автономного содержимого в приложение hello для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="aba57-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="aba57-119">Hello образец созданные эта интерактивная программа установки использует этот шаблон: его можно просматривать в действие hello первый раз, когда выполняется образец hello: так как пользователь не использовали приложения hello `PublicClientApp.Users.FirstOrDefault` будет содержать значение null и `MsalUiRequiredException` будет создано исключение.</span><span class="sxs-lookup"><span data-stu-id="aba57-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="aba57-120">Здравствуйте код в образце hello, а затем обрабатывает hello исключения путем вызова `AcquireTokenAsync` приведет к подтверждения пользователя hello в toosign.</span><span class="sxs-lookup"><span data-stu-id="aba57-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>
2.  <span data-ttu-id="aba57-121">Приложения также может сделать пользователь toohello визуальный индикатор, интерактивный вход не требуется, поэтому hello пользователь может выбрать toosign нужное время hello в или приложение hello перезапустит `AcquireTokenSilentAsync` позднее.</span><span class="sxs-lookup"><span data-stu-id="aba57-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="aba57-122">Обычно это используется hello пользователя может tooaccess функциональных возможностей приложения hello без была прервана — например, отсутствуют автономного содержимого в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="aba57-122">This is commonly used when hello user is able tooaccess functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="aba57-123">В этом случае hello пользователь мог решать при хочет toosign в tooaccess hello защищенных ресурсов, toorefresh hello устаревшую информацию или приложения может решить tooretry `AcquireTokenSilentAsync` при восстановлении сети после станет временно недоступной.</span><span class="sxs-lookup"><span data-stu-id="aba57-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="aba57-124">Вызвать API Microsoft Graph hello hello токен, который был получен с помощью</span><span class="sxs-lookup"><span data-stu-id="aba57-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>
1.  <span data-ttu-id="aba57-125">Добавьте следующие методы в hello hello `MainActivity` класса:</span><span class="sxs-lookup"><span data-stu-id="aba57-125">Add hello following methods into hello `MainActivity` class:</span></span>

```java
/* Use Volley toomake an HTTP request toohello /me endpoint from MS Graph using an access token */
private void callGraphAPI() {
    Log.d(TAG, "Starting volley request toograph");

    /* Make sure we have a token toosend toograph */
    if (authResult.getAccessToken() == null) {return;}

    RequestQueue queue = Volley.newRequestQueue(this);
    JSONObject parameters = new JSONObject();

    try {
        parameters.put("key", "value");
    } catch (Exception e) {
        Log.d(TAG, "Failed tooput parameters: " + e.toString());
    }
    JsonObjectRequest request = new JsonObjectRequest(Request.Method.GET, MSGRAPH_URL,
            parameters,new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            /* Successfully called graph, process data and send tooUI */
            Log.d(TAG, "Response: " + response.toString());

            updateGraphUI(response);
        }
    }, new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            Log.d(TAG, "Error: " + error.toString());
        }
    }) {
        @Override
        public Map<String, String> getHeaders() throws AuthFailureError {
            Map<String, String> headers = new HashMap<>();
            headers.put("Authorization", "Bearer " + authResult.getAccessToken());
            return headers;
        }
    };

    Log.d(TAG, "Adding HTTP GET tooQueue, Request: " + request.toString());

    request.setRetryPolicy(new DefaultRetryPolicy(
            3000,
            DefaultRetryPolicy.DEFAULT_MAX_RETRIES,
            DefaultRetryPolicy.DEFAULT_BACKOFF_MULT));
    queue.add(request);
}

/* Sets hello Graph response */
private void updateGraphUI(JSONObject graphResponse) {
    TextView graphText = (TextView) findViewById(R.id.graphData);
    graphText.setText(graphResponse.toString());
}
```
<!--start-collapse-->
### <a name="more-information-about-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="aba57-126">Дополнительные сведения о вызове REST через защищенный API</span><span class="sxs-lookup"><span data-stu-id="aba57-126">More information about making a REST call against a protected API</span></span>

<span data-ttu-id="aba57-127">В этом образце приложения `callGraphAPI` вызовы `getAccessToken` и затем делает HTTP `GET` запроса к ресурсу, который требуется маркер и возвращает содержимое hello.</span><span class="sxs-lookup"><span data-stu-id="aba57-127">In this sample application, `callGraphAPI` calls `getAccessToken` and then makes an HTTP `GET` request against a resource that requires a token and returns hello content.</span></span> <span data-ttu-id="aba57-128">Этот метод добавляет маркер hello получена в hello *заголовок авторизации HTTP*.</span><span class="sxs-lookup"><span data-stu-id="aba57-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="aba57-129">Для этого образца hello ресурсов — hello Microsoft Graph API *мне* конечной точки — которого отображаются сведения о профиле пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="aba57-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="setup-sign-out"></a><span data-ttu-id="aba57-130">Настройка выхода</span><span class="sxs-lookup"><span data-stu-id="aba57-130">Setup Sign-out</span></span>

1.  <span data-ttu-id="aba57-131">Добавьте следующие методы в hello hello `MainActivity` класса:</span><span class="sxs-lookup"><span data-stu-id="aba57-131">Add hello following methods into hello `MainActivity` class:</span></span>

```java
/* Clears a user's tokens from hello cache.
 * Logically similar too"sign out" but only signs out of this app.
 */
private void onSignOutClicked() {

    /* Attempt tooget a user and remove their cookies from cache */
    List<User> users = null;

    try {
        users = sampleApp.getUsers();

        if (users == null) {
            /* We have no users */

        } else if (users.size() == 1) {
            /* We have 1 user */
            /* Remove from token cache */
            sampleApp.remove(users.get(0));
            updateSignedOutUI();

        }
        else {
            /* We have multiple users */
            for (int i = 0; i < users.size(); i++) {
                sampleApp.remove(users.get(i));
            }
        }

        Toast.makeText(getBaseContext(), "Signed Out!", Toast.LENGTH_SHORT)
                .show();

    } catch (MsalClientException e) {
        Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

    } catch (IndexOutOfBoundsException e) {
        Log.d(TAG, "User at this position does not exist: " + e.toString());
    }
}

/* Set hello UI for signed-out user */
private void updateSignedOutUI() {
    callGraphButton.setVisibility(View.VISIBLE);
    signOutButton.setVisibility(View.INVISIBLE);
    findViewById(R.id.welcome).setVisibility(View.INVISIBLE);
    findViewById(R.id.graphData).setVisibility(View.INVISIBLE);
    ((TextView) findViewById(R.id.graphData)).setText("No Data");
}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="aba57-132">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="aba57-132">More information</span></span>

<span data-ttu-id="aba57-133">`onSignOutClicked`выше удаляет hello пользователя из кэша MSAL пользователя — фактически сведения о MSAL tooforget hello текущего пользователя, tooacquire будущих запроса маркера будет успешным, только если он станет toobe интерактивный.</span><span class="sxs-lookup"><span data-stu-id="aba57-133">`onSignOutClicked` above removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="aba57-134">Несмотря на то, что приложение hello в этом образце поддерживает один пользователь, MSAL поддерживает сценарии, где может быть несколько учетных записей, выполнившего вход в hello одновременно — пример — приложение электронной почты которых у пользователя есть несколько учетных записей.</span><span class="sxs-lookup"><span data-stu-id="aba57-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->
