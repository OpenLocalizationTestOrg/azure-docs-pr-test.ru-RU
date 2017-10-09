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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Использование библиотеки проверки подлинности Microsoft (MSAL) hello tooget маркер для hello Microsoft Graph API

Откройте `ViewController.swift` и замените код hello с:

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
### <a name="more-information"></a>Дополнительные сведения
#### <a name="getting-a-user-token-interactively"></a>Интерактивное получение маркера пользователя
Вызов hello `acquireToken` toosign пользователя в hello результаты метода в окне браузера, выполнении запроса. Приложения обычно требуют toosign пользователя в интерактивном режиме hello первый раз, они должны tooaccess защищенному ресурсу или при tooacquire операции в фоновом режиме, может произойти сбой маркера (например hello пользователя срок действия пароля истек).

#### <a name="getting-a-user-token-silently"></a>Автоматическое получение маркера пользователя
Hello `acquireTokenSilent` метод обрабатывает приобретения токена и обновления без вмешательства пользователя. После `acquireToken` выполняется для hello первый раз `acquireTokenSilent` tooobtain маркерами hello распространенным методом tooaccess защищенные ресурсы для последующих вызовов — как вызовы toorequest или обновить маркеры выполняются без вмешательства пользователя.

Со временем `acquireTokenSilent` завершится ошибкой, — например hello пользователя выполнен выход или изменил свой пароль на другом устройстве. Когда MSAL обнаруживает, что hello проблему можно устранить путем интерактивного вмешательства, в `MSALErrorCode.interactionRequired` исключение. Приложение может обработать это исключение двумя способами:

1.  Звонок от `acquireToken` немедленно, что приводит запроса hello toosign пользователя в. Этот шаблон обычно используется в веб-приложений там, где отсутствует не автономного содержимого в приложение hello для пользователя hello. Пример приложения Hello, созданные интерактивной программы установки использует этот шаблон: его можно просматривать в действие hello первый раз, когда выполняется приложение hello. Поскольку пользователь не использовали приложения hello `applicationContext.users().first` будет содержать значение null и ` MSALErrorCode.interactionRequired ` будет создано исключение. Здравствуйте код в образце hello, а затем обрабатывает hello исключения путем вызова `acquireToken` приведет к toosign пользователя hello в выполнении запроса.

2.  Приложения также может сделать пользователь toohello визуальный индикатор, интерактивный вход не требуется, поэтому hello пользователь может выбрать toosign нужное время hello в или приложение hello перезапустит `acquireTokenSilent` позднее. Это обычно используется при hello пользователя можно использовать другие функциональные возможности приложения hello без была прервана - например, отсутствуют автономного содержимого в приложение hello. В этом случае hello пользователь мог решать при хочет toosign в tooaccess hello защищенных ресурсов, toorefresh hello устаревшую информацию или приложения может решить tooretry `acquireTokenSilent` при восстановлении сети после станет временно недоступной.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Вызвать API Microsoft Graph hello hello токен, который был получен с помощью

Добавьте новый метод hello ниже слишком`ViewController.swift`. Этот метод является используется toomake `GET` запрос с использованием API-Интерфейс Microsoft Graph hello *заголовок авторизации HTTP*:

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
### <a name="making-a-rest-call-against-a-protected-api"></a>Вызов REST через защищенный API

В этом образце приложения hello `getContentWithToken()` в противном случае используется toomake HTTP `GET` запроса к защищенному ресурсу, требующий toohello содержимого токена и затем вернуться hello вызывающий объект. Этот метод добавляет маркер hello получена в hello *заголовок авторизации HTTP*. Для этого образца hello ресурсов — hello Microsoft Graph API *мне* конечной точки — которого отображаются сведения о профиле пользователя hello.
<!--end-collapse-->

## <a name="set-up-sign-out"></a>Настройка выхода

Добавьте следующий метод слишком hello`ViewController.swift` toosign выход пользователя hello:

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
### <a name="more-info-on-sign-out"></a>Дополнительные сведения о выходе

Hello `signoutButton` метод удаляет пользователя hello из hello кэш пользователя MSAL – эффективно сведения о том MSAL tooforget hello текущего пользователя, tooacquire будущих запроса маркера будет успешным, только если он станет toobe интерактивный.

Несмотря на то, что приложение hello в этом образце поддерживает один пользователь, MSAL поддерживает сценарии, где несколько учетных записей может быть подписана на hello одновременно — пример — приложение электронной почты которых у пользователя есть несколько учетных записей.
<!--end-collapse-->

## <a name="register-hello-callback"></a>Зарегистрировать обратный вызов hello

После аутентификации пользователя hello hello перенаправляет задней toohello приложение hello пользователя. Выполните действия hello ниже tooregister этого обратного вызова.

1.  Откройте `AppDelegate.swift` и импортируйте MSAL:

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Добавьте следующий метод tooyour hello <code>AppDelegate</code> класса toohandle обратные вызовы:
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

