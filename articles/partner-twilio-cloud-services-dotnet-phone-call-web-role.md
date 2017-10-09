---
title: "aaaHow toomake телефонный звонок от Twilio (.NET) | Документы Microsoft"
description: "Узнайте, как toomake телефонного звонка и SMS отправки сообщений с hello Twilio API службы в Azure. Примеры программного кода написаны в .NET."
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 857d89961c563a51fef944f4a72828036af79b43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="5ddfa-104">Как toomake вызвать с использованием Twilio в веб-роли в Azure телефон</span><span class="sxs-lookup"><span data-stu-id="5ddfa-104">How toomake a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="5ddfa-105">В этом руководстве показано, как toouse Twilio toomake вызов веб-страницы размещена в Azure.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-105">This guide demonstrates how toouse Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="5ddfa-106">полученное приложение Hello приглашения пользователя toomake hello вызов с hello заданным числом и сообщения, как показано на следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-106">hello resulting application prompts hello user toomake a call with hello given number and message, as shown in hello following screenshot.</span></span>

![Форма звонка Azure с использованием службы Twilio и ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="5ddfa-108"><a name="twilio-prereqs"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5ddfa-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="5ddfa-109">Вам потребуется следующее hello toodo toouse hello кода в этом разделе:</span><span class="sxs-lookup"><span data-stu-id="5ddfa-109">You will need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="5ddfa-110">Получения учетной записи Twilio и проверки подлинности маркера из hello [консоли Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-110">Acquire a Twilio account and authentication token from hello [Twilio Console][twilio_console].</span></span> <span data-ttu-id="5ddfa-111">tooget запущена с Twilio входа в [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-111">tooget started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="5ddfa-112">Ценовая политика описывается на странице [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="5ddfa-113">Сведения об API, предоставляемые Twilio hello см. в разделе [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-113">For information about hello API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="5ddfa-114">Добавить hello *библиотеки Twilio .NET* tooyour веб-роли.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-114">Add hello *Twilio .NET libary* tooyour web role.</span></span> <span data-ttu-id="5ddfa-115">В разделе **tooadd hello Twilio библиотеки tooyour проект веб-роли**далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-115">See **tooadd hello Twilio libraries tooyour web role project**, later in this topic.</span></span>

<span data-ttu-id="5ddfa-116">Для этого вам потребуется знание процесса, позволяющего создать базовую [веб-роль в Azure][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="5ddfa-117"><a name="howtocreateform"></a>Практическое руководство. Создание веб-формы для осуществления вызова</span><span class="sxs-lookup"><span data-stu-id="5ddfa-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="5ddfa-118"><a id="use_nuget"></a>tooadd hello Twilio библиотеки tooyour проект веб-роли:</span><span class="sxs-lookup"><span data-stu-id="5ddfa-118"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour web role project:</span></span>

1. <span data-ttu-id="5ddfa-119">Откройте решение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="5ddfa-120">Щелкните правой кнопкой мыши **References**(Ссылки).</span><span class="sxs-lookup"><span data-stu-id="5ddfa-120">Right-click **References**.</span></span>
3. <span data-ttu-id="5ddfa-121">Выберите **Управление пакетами NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="5ddfa-122">Щелкните **Online**(В сети).</span><span class="sxs-lookup"><span data-stu-id="5ddfa-122">Click **Online**.</span></span>
5. <span data-ttu-id="5ddfa-123">В hello поиска online введите *twilio*.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-123">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="5ddfa-124">Нажмите кнопку **установить** hello Twilio пакета.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-124">Click **Install** on hello Twilio package.</span></span>

<span data-ttu-id="5ddfa-125">Hello, следующий код показывает, как данные пользователя tooretrieve подключения формы toocreate веб-узла.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-125">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="5ddfa-126">В этом примере создается веб-роль ASP.NET с именем **TwilioCloud**.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <span data-ttu-id="5ddfa-127"><a id="howtocreatecode"></a>Как: Создание вызова hello toomake кода hello</span><span class="sxs-lookup"><span data-stu-id="5ddfa-127"><a id="howtocreatecode"></a>How to: Create hello code toomake hello call</span></span>
<span data-ttu-id="5ddfa-128">Hello следующий код, который вызывается, когда пользователь hello завершает hello формы, создает сообщение о вызове hello и приводит к возникновению ошибки вызова hello.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-128">hello following code, which is called when hello user completes hello form, creates hello call message and generates hello call.</span></span> <span data-ttu-id="5ddfa-129">В этом примере кода hello выполняется в обработчике событий onclick hello hello кнопки в форме hello.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-129">In this example, hello code is run in hello onclick event handler of hello button on hello form.</span></span> <span data-ttu-id="5ddfa-130">(Использование учетной записи Twilio и проверки подлинности маркера вместо значения заполнителей hello, назначенный слишком`accountSID` и `authToken` в следующем примере кода hello.)</span><span class="sxs-lookup"><span data-stu-id="5ddfa-130">(Use your Twilio account and authentication token instead of hello placeholder values assigned too`accountSID` and `authToken` in hello code below.)</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // hello placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of hello Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve hello account, used later tooretrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve hello values entered by hello user.
                var too= PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using hello Twilio message and hello user-entered
                // text. You must replace spaces in hello user's text with '%20'
                // toomake hello text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display hello endpoint, API version, and hello URL for hello message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"hello URL is {url}");

                // Place hello call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="5ddfa-131">вызов Hello и отображения конечной точки Twilio hello, версия API и состояние вызова hello.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-131">hello call is made, and hello Twilio endpoint, API version, and hello call status are displayed.</span></span> <span data-ttu-id="5ddfa-132">следующие выходные данные снимке экрана показано из образца, Hello.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-132">hello following screenshot shows output from a sample run.</span></span>

![Ответ на звонок Azure с использованием службы Twilio и ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="5ddfa-134">Дополнительные сведения о TwiML см. на странице [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="5ddfa-135">Дополнительные сведения о команде &lt;Say&gt; и других командах Twilio см. на странице [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="5ddfa-136"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ddfa-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="5ddfa-137">Этот код был предоставлен tooshow вы основные функциональные возможности с использованием Twilio в веб-роли ASP.NET в Azure.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-137">This code was provided tooshow you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="5ddfa-138">Перед развертыванием tooAzure в рабочей среде, вы можете tooadd дополнительные обработки ошибок или других компонентов.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-138">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="5ddfa-139">Например:</span><span class="sxs-lookup"><span data-stu-id="5ddfa-139">For example:</span></span>

* <span data-ttu-id="5ddfa-140">Вместо использования веб-формы, может использовать хранилище больших двоичных объектов Azure или номера телефонов toostore экземпляр базы данных SQL Azure и вызовите текста.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance toostore phone numbers and call text.</span></span> <span data-ttu-id="5ddfa-141">Сведения об использовании большие двоичные объекты в Azure см. в разделе [как toouse hello службы хранилища больших двоичных объектов Azure в .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-141">For information about using Blobs in Azure, see [How toouse hello Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="5ddfa-142">Сведения об использовании базы данных SQL см. в разделе [как toouse базы данных SQL Azure в приложениях .NET][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-142">For information about using SQL Database, see [How toouse Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="5ddfa-143">Можно использовать `RoleEnvironment.getConfigurationSettings` идентификатор учетной записи Twilio tooretrieve hello и проверки подлинности токена из параметров конфигурации развертывания, вместо жестко запрограммированных значений hello в форме.</span><span class="sxs-lookup"><span data-stu-id="5ddfa-143">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in your form.</span></span> <span data-ttu-id="5ddfa-144">Сведения о hello `RoleEnvironment` см. в описании [имен Microsoft.WindowsAzure.ServiceRuntime][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-144">For information about hello `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="5ddfa-145">Прочитать рекомендации по безопасности Twilio hello в [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-145">Read hello Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="5ddfa-146">Дополнительные сведения о службе Twilio см. на странице [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="5ddfa-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="5ddfa-147"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="5ddfa-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="5ddfa-148">Как toouse Twilio для возможности голоса и SMS из Azure</span><span class="sxs-lookup"><span data-stu-id="5ddfa-148">How toouse Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
