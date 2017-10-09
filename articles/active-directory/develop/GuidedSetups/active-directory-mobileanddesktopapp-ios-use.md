---
title: "iOS v2 aaaAzure AD Приступая к работе - Используйте | Документы Microsoft"
description: "В этой статье описано, как приложения iOS (Swift) могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2."
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
ms.openlocfilehash: 22e67850e2e0b14b6d68815d8f23e18ce2e878ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="3098c-103">Использование библиотеки проверки подлинности Microsoft (MSAL) hello tooget маркер для hello Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="3098c-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="3098c-104">Откройте `ViewController.swift` и замените код hello с:</span><span class="sxs-lookup"><span data-stu-id="3098c-104">Open `ViewController.swift` and replace hello code with:</span></span>

```swift
import UIKit
import MSAL

class ViewController: UIViewController, UITextFieldDelegate, URLSessionDelegate {
    
    let kClientID = "Your_Application_Id_Here"
    let kAuthority = "https://login.microsoftonline.com/common/v2.0"

    let kGraphURI = "https://graph.microsoft.com/v1.0/me/"
    let kScopes: [String] = ["https://graph.microsoft.com/user.read"]
    
    var accessToken = String()
    var applicationContext = MSALPublicClientApplication.init()

    @IBOutlet weak var loggingText: UITextView!
    @IBOutlet weak var signoutButton: UIButton!

     // This button will invoke hello call toohello Microsoft Graph API. It uses the
     // built in Swift libraries toocreate a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check toosee if we have a current logged in user. If we don't, then we need toosign someone in.
            // We throw an interactionRequired so that we trigger hello interactive signin.
            
            if  try self.applicationContext.users().isEmpty {
                throw NSError.init(domain: "MSALErrorDomain", code: MSALErrorCode.interactionRequired.rawValue, userInfo: nil)
            } else {
            
            // Acquire a token for an existing user silently
            
            try self.applicationContext.acquireTokenSilent(forScopes: self.kScopes, user: applicationContext.users().first) { (result, error) in
    
                    if error == nil {
                        self.accessToken = (result?.accessToken)!
                        self.loggingText.text = "Refreshing token silently)"
                        self.loggingText.text = "Refreshed Access token is \(self.accessToken)"
                        
                        self.signoutButton.isEnabled = true;
                        self.getContentWithToken()
    
                    } else {
                        self.loggingText.text = "Could not acquire token silently: \(error ?? "No error information" as! Error)"
    
                    }
                }
            }
        }  catch let error as NSError {
            
            // interactionRequired means we need tooask hello user toosign-in. This usually happens
            // when hello user's Refresh Token is expired or if hello user has changed their password
            // among other possible reasons.
            
            if error.code == MSALErrorCode.interactionRequired.rawValue {
                
                self.applicationContext.acquireToken(forScopes: self.kScopes) { (result, error) in
                        if error == nil {
                            self.accessToken = (result?.accessToken)!
                            self.loggingText.text = "Access token is \(self.accessToken)"
                            self.signoutButton.isEnabled = true;
                            self.getContentWithToken()
                            
                        } else  {
                            self.loggingText.text = "Could not acquire token: \(error ?? "No error information" as! Error)"
                        }
                }
                
            }
            
        } catch {
            
            // This is hello catch all error.
            
            self.loggingText.text = "Unable tooacquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable toocreate Application Context. Error: \(error)"
        }
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        
        if self.accessToken.isEmpty {
            signoutButton.isEnabled = false; 
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="3098c-105">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="3098c-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="3098c-106">Интерактивное получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="3098c-106">Getting a user token interactively</span></span>
<span data-ttu-id="3098c-107">Вызов hello `acquireToken` toosign пользователя в hello результаты метода в окне браузера, выполнении запроса.</span><span class="sxs-lookup"><span data-stu-id="3098c-107">Calling hello `acquireToken` method results in a browser window prompting hello user toosign in.</span></span> <span data-ttu-id="3098c-108">Приложения обычно требуют toosign пользователя в интерактивном режиме hello первый раз, они должны tooaccess защищенному ресурсу или при tooacquire операции в фоновом режиме, может произойти сбой маркера (например hello пользователя срок действия пароля истек).</span><span class="sxs-lookup"><span data-stu-id="3098c-108">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="3098c-109">Автоматическое получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="3098c-109">Getting a user token silently</span></span>
<span data-ttu-id="3098c-110">Hello `acquireTokenSilent` метод обрабатывает приобретения токена и обновления без вмешательства пользователя.</span><span class="sxs-lookup"><span data-stu-id="3098c-110">hello `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="3098c-111">После `acquireToken` выполняется для hello первый раз `acquireTokenSilent` tooobtain маркерами hello распространенным методом tooaccess защищенные ресурсы для последующих вызовов — как вызовы toorequest или обновить маркеры выполняются без вмешательства пользователя.</span><span class="sxs-lookup"><span data-stu-id="3098c-111">After `acquireToken` is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>

<span data-ttu-id="3098c-112">Со временем `acquireTokenSilent` завершится ошибкой, — например hello пользователя выполнен выход или изменил свой пароль на другом устройстве.</span><span class="sxs-lookup"><span data-stu-id="3098c-112">Eventually, `acquireTokenSilent` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="3098c-113">Когда MSAL обнаруживает, что hello проблему можно устранить путем интерактивного вмешательства, в `MSALErrorCode.interactionRequired` исключение.</span><span class="sxs-lookup"><span data-stu-id="3098c-113">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="3098c-114">Приложение может обработать это исключение двумя способами:</span><span class="sxs-lookup"><span data-stu-id="3098c-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="3098c-115">Звонок от `acquireToken` немедленно, что приводит запроса hello toosign пользователя в.</span><span class="sxs-lookup"><span data-stu-id="3098c-115">Make a call against `acquireToken` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="3098c-116">Этот шаблон обычно используется в веб-приложений там, где отсутствует не автономного содержимого в приложение hello для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="3098c-116">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="3098c-117">Пример приложения Hello, созданные интерактивной программы установки использует этот шаблон: его можно просматривать в действие hello первый раз, когда выполняется приложение hello.</span><span class="sxs-lookup"><span data-stu-id="3098c-117">hello sample application generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello application.</span></span> <span data-ttu-id="3098c-118">Поскольку пользователь не использовали приложения hello `applicationContext.users().first` будет содержать значение null и ` MSALErrorCode.interactionRequired ` будет создано исключение.</span><span class="sxs-lookup"><span data-stu-id="3098c-118">Because no user ever used hello application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="3098c-119">Здравствуйте код в образце hello, а затем обрабатывает hello исключения путем вызова `acquireToken` приведет к toosign пользователя hello в выполнении запроса.</span><span class="sxs-lookup"><span data-stu-id="3098c-119">hello code in hello sample then handles hello exception by calling `acquireToken` resulting in prompting hello user toosign in.</span></span>

2.  <span data-ttu-id="3098c-120">Приложения также может сделать пользователь toohello визуальный индикатор, интерактивный вход не требуется, поэтому hello пользователь может выбрать toosign нужное время hello в или приложение hello перезапустит `acquireTokenSilent` позднее.</span><span class="sxs-lookup"><span data-stu-id="3098c-120">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="3098c-121">Это обычно используется при hello пользователя можно использовать другие функциональные возможности приложения hello без была прервана - например, отсутствуют автономного содержимого в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="3098c-121">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="3098c-122">В этом случае hello пользователь мог решать при хочет toosign в tooaccess hello защищенных ресурсов, toorefresh hello устаревшую информацию или приложения может решить tooretry `acquireTokenSilent` при восстановлении сети после станет временно недоступной.</span><span class="sxs-lookup"><span data-stu-id="3098c-122">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="3098c-123">Вызвать API Microsoft Graph hello hello токен, который был получен с помощью</span><span class="sxs-lookup"><span data-stu-id="3098c-123">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="3098c-124">Добавьте новый метод hello ниже слишком`ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="3098c-124">Add hello new method below too`ViewController.swift`.</span></span> <span data-ttu-id="3098c-125">Этот метод является используется toomake `GET` запрос с использованием API-Интерфейс Microsoft Graph hello *заголовок авторизации HTTP*:</span><span class="sxs-lookup"><span data-stu-id="3098c-125">This method is used toomake a `GET` request against hello Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify hello Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set hello Authorization header for hello request. We use Bearer tokens, so we specify Bearer + hello token we got from hello result
    request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")
    let urlSession = URLSession(configuration: sessionConfig, delegate: self, delegateQueue: OperationQueue.main)
    
    urlSession.dataTask(with: request) { data, response, error in
        let result = try? JSONSerialization.jsonObject(with: data!, options: [])
                    if result != nil {
                
                self.loggingText.text = result.debugDescription
            }
        }.resume()
}
```

<!--start-collapse-->
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="3098c-126">Вызов REST через защищенный API</span><span class="sxs-lookup"><span data-stu-id="3098c-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="3098c-127">В этом образце приложения hello `getContentWithToken()` в противном случае используется toomake HTTP `GET` запроса к защищенному ресурсу, требующий toohello содержимого токена и затем вернуться hello вызывающий объект.</span><span class="sxs-lookup"><span data-stu-id="3098c-127">In this sample application, hello `getContentWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="3098c-128">Этот метод добавляет маркер hello получена в hello *заголовок авторизации HTTP*.</span><span class="sxs-lookup"><span data-stu-id="3098c-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="3098c-129">Для этого образца hello ресурсов — hello Microsoft Graph API *мне* конечной точки — которого отображаются сведения о профиле пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="3098c-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="3098c-130">Настройка выхода</span><span class="sxs-lookup"><span data-stu-id="3098c-130">Set up sign-out</span></span>

<span data-ttu-id="3098c-131">Добавьте следующий метод слишком hello`ViewController.swift` toosign выход пользователя hello:</span><span class="sxs-lookup"><span data-stu-id="3098c-131">Add hello following method too`ViewController.swift` toosign out hello user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from hello cache for this application for hello provided user
        // first parameter:   hello user tooremove from hello cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="3098c-132">Дополнительные сведения о выходе</span><span class="sxs-lookup"><span data-stu-id="3098c-132">More info on sign-out</span></span>

<span data-ttu-id="3098c-133">Hello `signoutButton` метод удаляет пользователя hello из hello кэш пользователя MSAL – эффективно сведения о том MSAL tooforget hello текущего пользователя, tooacquire будущих запроса маркера будет успешным, только если он станет toobe интерактивный.</span><span class="sxs-lookup"><span data-stu-id="3098c-133">hello `signoutButton` method removes hello user from hello MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>

<span data-ttu-id="3098c-134">Несмотря на то, что приложение hello в этом образце поддерживает один пользователь, MSAL поддерживает сценарии, где несколько учетных записей может быть подписана на hello одновременно — пример — приложение электронной почты которых у пользователя есть несколько учетных записей.</span><span class="sxs-lookup"><span data-stu-id="3098c-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-hello-callback"></a><span data-ttu-id="3098c-135">Зарегистрировать обратный вызов hello</span><span class="sxs-lookup"><span data-stu-id="3098c-135">Register hello callback</span></span>

<span data-ttu-id="3098c-136">После аутентификации пользователя hello hello перенаправляет задней toohello приложение hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="3098c-136">Once hello user authenticates, hello browser redirects hello user back toohello application.</span></span> <span data-ttu-id="3098c-137">Выполните действия hello ниже tooregister этого обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="3098c-137">Follow hello steps below tooregister this callback:</span></span>

1.  <span data-ttu-id="3098c-138">Откройте `AppDelegate.swift` и импортируйте MSAL:</span><span class="sxs-lookup"><span data-stu-id="3098c-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="3098c-139">Добавьте следующий метод tooyour hello <code>AppDelegate</code> класса toohandle обратные вызовы:</span><span class="sxs-lookup"><span data-stu-id="3098c-139">Add hello following method tooyour <code>AppDelegate</code> class toohandle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if hello URL matches hello redirect URI for a pending AppAuth
// authorization request and if so, will look for hello code in hello response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

