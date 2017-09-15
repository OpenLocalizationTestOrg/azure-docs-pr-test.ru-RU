---
title: "Приступая к работе с Azure AD версии 2 для iOS. Использование | Документы Майкрософт"
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
ms.openlocfilehash: 2ac1117a31a101705539a1f75520ce8de43809a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="d4cc2-103">Использование библиотеки проверки подлинности Майкрософт для получения маркера для API Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="d4cc2-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="d4cc2-104">Откройте файл `ViewController.swift` и замените код на следующий:</span><span class="sxs-lookup"><span data-stu-id="d4cc2-104">Open `ViewController.swift` and replace the code with:</span></span>

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

     // This button will invoke the call to the Microsoft Graph API. It uses the
     // built in Swift libraries to create a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check to see if we have a current logged in user. If we don't, then we need to sign someone in.
            // We throw an interactionRequired so that we trigger the interactive signin.
            
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
            
            // interactionRequired means we need to ask the user to sign-in. This usually happens
            // when the user's Refresh Token is expired or if the user has changed their password
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
            
            // This is the catch all error.
            
            self.loggingText.text = "Unable to acquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable to create Application Context. Error: \(error)"
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
### <a name="more-information"></a><span data-ttu-id="d4cc2-105">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="d4cc2-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="d4cc2-106">Интерактивное получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="d4cc2-106">Getting a user token interactively</span></span>
<span data-ttu-id="d4cc2-107">При вызове метода `acquireToken` откроется окно браузера, в котором пользователю предлагается выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-107">Calling the `acquireToken` method results in a browser window prompting the user to sign in.</span></span> <span data-ttu-id="d4cc2-108">Приложениям обычно требуется, чтобы пользователь выполнял вход интерактивно при первом доступе к защищенному ресурсу или при сбое автоматической операции для получения маркера (например, срок действия пароля пользователя истек).</span><span class="sxs-lookup"><span data-stu-id="d4cc2-108">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="d4cc2-109">Автоматическое получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="d4cc2-109">Getting a user token silently</span></span>
<span data-ttu-id="d4cc2-110">Метод `acquireTokenSilent` обрабатывает получение и обновление маркера без участия пользователя.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-110">The `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="d4cc2-111">После первого выполнения метода `acquireToken` обычно используется метод `acquireTokenSilent`, чтобы получить маркеры для доступа к защищенным ресурсам для последующих вызовов (например, автоматическое выполнение запросов или обновлений маркеров).</span><span class="sxs-lookup"><span data-stu-id="d4cc2-111">After `acquireToken` is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>

<span data-ttu-id="d4cc2-112">В конечном счете в `acquireTokenSilent` произойдет сбой, например в случае выхода пользователя из системы или смены пароля на другом устройстве.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-112">Eventually, `acquireTokenSilent` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="d4cc2-113">Когда MSAL обнаруживает, что эту проблему можно решить, запросив интерактивное действие, возникает исключение `MSALErrorCode.interactionRequired`.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-113">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="d4cc2-114">Приложение может обработать это исключение двумя способами:</span><span class="sxs-lookup"><span data-stu-id="d4cc2-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="d4cc2-115">Вызвать `acquireToken` немедленно, в результате чего пользователю будет предложено выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-115">Make a call against `acquireToken` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="d4cc2-116">Этот шаблон обычно используется в интерактивных приложениях, где пользователю недоступно автономное содержимое.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-116">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="d4cc2-117">В примере приложения, созданного в ходе интерактивной настройки, используется следующий шаблон: вы увидите его в действии при первом запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-117">The sample application generated by this guided setup uses this pattern: you can see it in action the first time you execute the application.</span></span> <span data-ttu-id="d4cc2-118">Так как приложение еще не использовалось, `applicationContext.users().first` будет содержать значение null и будет выдано исключение ` MSALErrorCode.interactionRequired `.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-118">Because no user ever used the application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="d4cc2-119">Код в примере обработает исключение, вызвав `acquireToken`, в результате чего пользователю будет предложено войти.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-119">The code in the sample then handles the exception by calling `acquireToken` resulting in prompting the user to sign in.</span></span>

2.  <span data-ttu-id="d4cc2-120">Приложения также могут визуально уведомить пользователя, что требуется интерактивный вход, чтобы пользователь мог выбрать подходящее время для входа или приложение могло повторить метод `acquireTokenSilent` ​​позднее.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-120">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="d4cc2-121">Обычно это применимо для тех случаев, когда пользователь может использовать другие функции приложения, на которые это не влияет, например, когда в приложении есть автономное содержимое.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-121">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="d4cc2-122">В этом случае пользователь может решить, когда он хочет войти, чтобы получить доступ к защищенному ресурсу или обновить устаревшие данные, или ваше приложение может решить повторить `acquireTokenSilent` при восстановлении сети ​​после временной недоступности.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-122">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="d4cc2-123">Вызов API Microsoft Graph с помощью полученного маркера</span><span class="sxs-lookup"><span data-stu-id="d4cc2-123">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="d4cc2-124">Добавьте указанный ниже новый метод в файл `ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-124">Add the new method below to `ViewController.swift`.</span></span> <span data-ttu-id="d4cc2-125">Этот метод используется для выполнения запроса `GET` к API Microsoft Graph с использованием *Заголовка авторизации HTTP*:</span><span class="sxs-lookup"><span data-stu-id="d4cc2-125">This method is used to make a `GET` request against the Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify the Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set the Authorization header for the request. We use Bearer tokens, so we specify Bearer + the token we got from the result
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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="d4cc2-126">Вызов REST через защищенный API</span><span class="sxs-lookup"><span data-stu-id="d4cc2-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="d4cc2-127">В этом примере приложения метод `getContentWithToken()` выполняет HTTP-запрос `GET` к защищенному ресурсу, требующему маркер, а затем возвращает содержимое вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-127">In this sample application, the `getContentWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="d4cc2-128">Этот метод добавляет полученный маркер в *заголовок авторизации HTTP*.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-128">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="d4cc2-129">В этом примере ресурс — это конечная точка *me* API Microsoft Graph, которая отображает сведения о профиле пользователя.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-129">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="d4cc2-130">Настройка выхода</span><span class="sxs-lookup"><span data-stu-id="d4cc2-130">Set up sign-out</span></span>

<span data-ttu-id="d4cc2-131">Добавьте следующий метод в файл `ViewController.swift` для выхода пользователя:</span><span class="sxs-lookup"><span data-stu-id="d4cc2-131">Add the following method to `ViewController.swift` to sign out the user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from the cache for this application for the provided user
        // first parameter:   The user to remove from the cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="d4cc2-132">Дополнительные сведения о выходе</span><span class="sxs-lookup"><span data-stu-id="d4cc2-132">More info on sign-out</span></span>

<span data-ttu-id="d4cc2-133">Метод `signoutButton` удаляет пользователя из кэша пользователей MSAL. Фактически это заставляет MSAL забыть о текущем пользователе, поэтому будущие запросы на получение маркеров будут успешными только в том случае, если будут выполняться автоматически.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-133">The `signoutButton` method removes the user from the MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>

<span data-ttu-id="d4cc2-134">Несмотря на то, что приложение в этом примере поддерживает одного пользователя, MSAL поддерживает сценарии, в которых несколько пользователей могут войти в систему одновременно, например для приложения электронной почты, в котором у пользователя есть несколько учетных записей.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-134">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-the-callback"></a><span data-ttu-id="d4cc2-135">Регистрация обратного вызова</span><span class="sxs-lookup"><span data-stu-id="d4cc2-135">Register the callback</span></span>

<span data-ttu-id="d4cc2-136">После проверки подлинности пользователь перенаправляет пользователя обратно в приложение.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-136">Once the user authenticates, the browser redirects the user back to the application.</span></span> <span data-ttu-id="d4cc2-137">Чтобы зарегистрировать обратный вызов, выполните указанные ниже действия:</span><span class="sxs-lookup"><span data-stu-id="d4cc2-137">Follow the steps below to register this callback:</span></span>

1.  <span data-ttu-id="d4cc2-138">Откройте `AppDelegate.swift` и импортируйте MSAL:</span><span class="sxs-lookup"><span data-stu-id="d4cc2-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="d4cc2-139">Добавьте следующий метод в класс <code>AppDelegate</code> для обработки обратных вызовов:</span><span class="sxs-lookup"><span data-stu-id="d4cc2-139">Add the following method to your <code>AppDelegate</code> class to handle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if the URL matches the redirect URI for a pending AppAuth
// authorization request and if so, will look for the code in the response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

