---
title: "aaaHow tooConfigure TLS взаимной проверки подлинности для веб-приложения"
description: "Узнайте, как при tooconfigure веб-приложение клиента toouse сертификат проверки подлинности TLS."
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: cd1d15d3-2d9e-4502-9f11-a306dac4453a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: naziml
ms.openlocfilehash: 8aeb9b35058fac50b8b38f6428207ad4a82d8637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-tls-mutual-authentication-for-web-app"></a><span data-ttu-id="7f3a6-103">Как tooConfigure TLS взаимной проверки подлинности для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="7f3a6-103">How tooConfigure TLS Mutual Authentication for Web App</span></span>
## <a name="overview"></a><span data-ttu-id="7f3a6-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="7f3a6-104">Overview</span></span>
<span data-ttu-id="7f3a6-105">Вы можете ограничить доступ tooyour веб-приложение Azure, позволяя разные типы проверки подлинности для него.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-105">You can restrict access tooyour Azure web app by enabling different types of authentication for it.</span></span> <span data-ttu-id="7f3a6-106">Одним из способов toodo случае tooauthenticate, с помощью сертификата клиента при получении запроса hello через TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-106">One way toodo so is tooauthenticate using a client certificate when hello request is over TLS/SSL.</span></span> <span data-ttu-id="7f3a6-107">Этот механизм называется TLS взаимной проверки подлинности или проверка подлинности сертификата клиента и в этой статье подробно рассматриваются как toosetup вашей web app toouse проверка подлинности сертификата клиента.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-107">This mechanism is called TLS mutual authentication or client certificate authentication and this article will detail how toosetup your web app toouse client certificate authentication.</span></span>

> <span data-ttu-id="7f3a6-108">**Примечание.** Если для доступа к сайту используется протокол HTTP, а не HTTPS, вы не получите сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-108">**Note:** If you access your site over HTTP and not HTTPS, you will not receive any client certificate.</span></span> <span data-ttu-id="7f3a6-109">Поэтому если приложению требуются клиентские сертификаты не следует разрешать запросы tooyour приложения по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-109">So if your application requires client certificates you should not allow requests tooyour application over HTTP.</span></span>
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a><span data-ttu-id="7f3a6-110">Настройка веб-приложения для проверки подлинности сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="7f3a6-110">Configure Web App for Client Certificate Authentication</span></span>
<span data-ttu-id="7f3a6-111">toosetup вашей веб-приложения toorequire клиентских сертификатов, необходимые tooadd hello clientCertEnabled сайта для веб-приложения и задать для него tootrue.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-111">toosetup your web app toorequire client certificates you need tooadd hello clientCertEnabled site setting for your web app and set it tootrue.</span></span> <span data-ttu-id="7f3a6-112">Этот параметр не доступен через интерфейс управления hello в hello портала и hello API-интерфейса REST понадобится использовать toobe tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-112">This setting is not currently available through hello management experience in hello Portal, and hello REST API will need toobe used tooaccomplish this.</span></span>

<span data-ttu-id="7f3a6-113">Можно использовать hello [ARMClient средство](https://github.com/projectkudu/ARMClient) toomake его легко toocraft hello вызова интерфейса API REST.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-113">You can use hello [ARMClient tool](https://github.com/projectkudu/ARMClient) toomake it easy toocraft hello REST API call.</span></span> <span data-ttu-id="7f3a6-114">После входа в систему средства hello требуется hello tooissue следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7f3a6-114">After you log in with hello tool you will need tooissue hello following command:</span></span>

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

<span data-ttu-id="7f3a6-115">заменяя все содержимое {} для веб-приложения и создание файла с именем enableclientcert.json с hello, следуя JSON содержимого:</span><span class="sxs-lookup"><span data-stu-id="7f3a6-115">replacing everything in {} with information for your web app and creating a file called enableclientcert.json with hello following JSON content:</span></span>

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

<span data-ttu-id="7f3a6-116">Убедитесь, что значение hello toochange toowherever «местоположение» является веб-приложения, которые находятся например North Central US или Запад США и т. д.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-116">Make sure toochange hello value of "location" toowherever your web app is located e.g. North Central US or West US etc.</span></span>

<span data-ttu-id="7f3a6-117">Можно также использовать https://resources.azure.com tooflip hello `clientCertEnabled` свойство слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-117">You can also use https://resources.azure.com tooflip hello `clientCertEnabled` property too`true`.</span></span>

> <span data-ttu-id="7f3a6-118">**Примечание:** при запуске ARMClient из Powershell для hello JSON-файла с обратной кавычки потребуется hello tooescape символа @ ".</span><span class="sxs-lookup"><span data-stu-id="7f3a6-118">**Note:** If you run ARMClient from Powershell, you will need tooescape hello @ symbol for hello JSON file with a back tick \`.</span></span>
> 
> 

## <a name="accessing-hello-client-certificate-from-your-web-app"></a><span data-ttu-id="7f3a6-119">Доступ к hello клиентского сертификата из вашего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="7f3a6-119">Accessing hello Client Certificate From Your Web App</span></span>
<span data-ttu-id="7f3a6-120">Если используется ASP.NET и настройки проверки подлинности сертификата клиента toouse приложения hello сертификат будет доступно hello **HttpRequest.ClientCertificate** свойство.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-120">If you are using ASP.NET and configure your app toouse client certificate authentication, hello certificate will be available through hello **HttpRequest.ClientCertificate** property.</span></span> <span data-ttu-id="7f3a6-121">Для других стеки приложения будут доступны в приложения с помощью значение в кодировке base64 в заголовке запроса «X ARR ClientCert» hello hello сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-121">For other application stacks, hello client cert will be available in your app through a base64 encoded value in hello "X-ARR-ClientCert" request header.</span></span> <span data-ttu-id="7f3a6-122">Приложение может создать сертификат из этого значения и использовать его для проверки подлинности и авторизации.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-122">Your application can create a certificate from this value and then use it for authentication and authorization purposes in your application.</span></span>

## <a name="special-considerations-for-certificate-validation"></a><span data-ttu-id="7f3a6-123">Дополнительные рекомендации для проверки сертификата</span><span class="sxs-lookup"><span data-stu-id="7f3a6-123">Special Considerations for Certificate Validation</span></span>
<span data-ttu-id="7f3a6-124">Hello сертификат клиента, который отправляется toohello приложения не проходит через проверку платформой hello веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-124">hello client certificate that is sent toohello application does not go through any validation by hello Azure Web Apps platform.</span></span> <span data-ttu-id="7f3a6-125">Проверку этого сертификата лежит hello hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-125">Validating this certificate is hello responsibility of hello web app.</span></span> <span data-ttu-id="7f3a6-126">Ниже приведен пример кода ASP.NET, который проверяет свойства сертификата для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7f3a6-126">Here is sample ASP.NET code that validates certificate properties for authentication purposes.</span></span>

    using System;
    using System.Collections.Specialized;
    using System.Security.Cryptography.X509Certificates;
    using System.Web;

    namespace ClientCertificateUsageSample
    {
        public partial class cert : System.Web.UI.Page
        {
            public string certHeader = "";
            public string errorString = "";
            private X509Certificate2 certificate = null;
            public string certThumbprint = "";
            public string certSubject = "";
            public string certIssuer = "";
            public string certSignatureAlg = "";
            public string certIssueDate = "";
            public string certExpiryDate = "";
            public bool isValidCert = false;

            //
            // Read hello certificate from hello header into an X509Certificate2 object
            // Display properties of hello certificate on hello page
            //
            protected void Page_Load(object sender, EventArgs e)
            {
                NameValueCollection headers = base.Request.Headers;
                certHeader = headers["X-ARR-ClientCert"];
                if (!String.IsNullOrEmpty(certHeader))
                {
                    try
                    {
                        byte[] clientCertBytes = Convert.FromBase64String(certHeader);
                        certificate = new X509Certificate2(clientCertBytes);
                        certSubject = certificate.Subject;
                        certIssuer = certificate.Issuer;
                        certThumbprint = certificate.Thumbprint;
                        certSignatureAlg = certificate.SignatureAlgorithm.FriendlyName;
                        certIssueDate = certificate.NotBefore.ToShortDateString() + " " + certificate.NotBefore.ToShortTimeString();
                        certExpiryDate = certificate.NotAfter.ToShortDateString() + " " + certificate.NotAfter.ToShortTimeString();
                    }
                    catch (Exception ex)
                    {
                        errorString = ex.ToString();
                    }
                    finally 
                    {
                        isValidCert = IsValidClientCertificate();
                        if (!isValidCert) Response.StatusCode = 403;
                        else Response.StatusCode = 200;
                    }
                }
                else
                {
                    certHeader = "";
                }
            }

            //
            // This is a SAMPLE verification routine. Depending on your application logic and security requirements, 
            // you should modify this method
            //
            private bool IsValidClientCertificate()
            {
                // In this example we will only accept hello certificate as a valid certificate if all hello conditions below are met:
                // 1. hello certificate is not expired and is active for hello current time on server.
                // 2. hello subject name of hello certificate has hello common name nildevecc
                // 3. hello issuer name of hello certificate has hello common name nildevecc and organization name Microsoft Corp
                // 4. hello thumbprint of hello certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained tooa Trusted Root Authority (or revoked) on hello server 
                // and it allows for self signed certificates
                //

                if (certificate == null || !String.IsNullOrEmpty(errorString)) return false;

                // 1. Check time validity of certificate
                if (DateTime.Compare(DateTime.Now, certificate.NotBefore) < 0 || DateTime.Compare(DateTime.Now, certificate.NotAfter) > 0) return false;

                // 2. Check subject name of certificate
                bool foundSubject = false;
                string[] certSubjectData = certificate.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certSubjectData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundSubject = true;
                        break;
                    }
                }
                if (!foundSubject) return false;

                // 3. Check issuer name of certificate
                bool foundIssuerCN = false, foundIssuerO = false;
                string[] certIssuerData = certificate.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certIssuerData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundIssuerCN = true;
                        if (foundIssuerO) break;
                    }

                    if (String.Compare(s.Trim(), "O=Microsoft Corp") == 0)
                    {
                        foundIssuerO = true;
                        if (foundIssuerCN) break;
                    }
                }

                if (!foundIssuerCN || !foundIssuerO) return false;

                // 4. Check thumprint of certificate
                if (String.Compare(certificate.Thumbprint.Trim().ToUpper(), "30757A2E831977D8BD9C8496E4C99AB26CB9622B") != 0) return false;

                // If you also want tootest if hello certificate chains tooa Trusted Root Authority you can uncomment hello code below
                //
                //X509Chain certChain = new X509Chain();
                //certChain.Build(certificate);
                //bool isValidCertChain = true;
                //foreach (X509ChainElement chElement in certChain.ChainElements)
                //{
                //    if (!chElement.Certificate.Verify())
                //    {
                //        isValidCertChain = false;
                //        break;
                //    }
                //}
                //if (!isValidCertChain) return false;

                return true;
            }
        }
    }
