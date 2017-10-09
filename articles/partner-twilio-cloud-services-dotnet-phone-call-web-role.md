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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a>Как toomake вызвать с использованием Twilio в веб-роли в Azure телефон
В этом руководстве показано, как toouse Twilio toomake вызов веб-страницы размещена в Azure. полученное приложение Hello приглашения пользователя toomake hello вызов с hello заданным числом и сообщения, как показано на следующий снимок экрана приветствия.

![Форма звонка Azure с использованием службы Twilio и ASP.NET][twilio_dotnet_basic_form]

## <a name="twilio-prereqs"></a>Предварительные требования
Вам потребуется следующее hello toodo toouse hello кода в этом разделе:

1. Получения учетной записи Twilio и проверки подлинности маркера из hello [консоли Twilio][twilio_console]. tooget запущена с Twilio входа в [https://www.twilio.com/try-twilio][try_twilio]. Ценовая политика описывается на странице [http://www.twilio.com/pricing][twilio_pricing]. Сведения об API, предоставляемые Twilio hello см. в разделе [http://www.twilio.com/voice/api][twilio_api].
2. Добавить hello *библиотеки Twilio .NET* tooyour веб-роли. В разделе **tooadd hello Twilio библиотеки tooyour проект веб-роли**далее в этом разделе.

Для этого вам потребуется знание процесса, позволяющего создать базовую [веб-роль в Azure][azure_webroles_get_started].

## <a name="howtocreateform"></a>Практическое руководство. Создание веб-формы для осуществления вызова
<a id="use_nuget"></a>tooadd hello Twilio библиотеки tooyour проект веб-роли:

1. Откройте решение в Visual Studio.
2. Щелкните правой кнопкой мыши **References**(Ссылки).
3. Выберите **Управление пакетами NuGet...**.
4. Щелкните **Online**(В сети).
5. В hello поиска online введите *twilio*.
6. Нажмите кнопку **установить** hello Twilio пакета.

Hello, следующий код показывает, как данные пользователя tooretrieve подключения формы toocreate веб-узла. В этом примере создается веб-роль ASP.NET с именем **TwilioCloud**.

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

## <a id="howtocreatecode"></a>Как: Создание вызова hello toomake кода hello
Hello следующий код, который вызывается, когда пользователь hello завершает hello формы, создает сообщение о вызове hello и приводит к возникновению ошибки вызова hello. В этом примере кода hello выполняется в обработчике событий onclick hello hello кнопки в форме hello. (Использование учетной записи Twilio и проверки подлинности маркера вместо значения заполнителей hello, назначенный слишком`accountSID` и `authToken` в следующем примере кода hello.)

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

вызов Hello и отображения конечной точки Twilio hello, версия API и состояние вызова hello. следующие выходные данные снимке экрана показано из образца, Hello.

![Ответ на звонок Azure с использованием службы Twilio и ASP.NET][twilio_dotnet_basic_form_output]

Дополнительные сведения о TwiML см. на странице [http://www.twilio.com/docs/api/twiml][twiml]. Дополнительные сведения о команде &lt;Say&gt; и других командах Twilio см. на странице [http://www.twilio.com/docs/api/twiml/say][twilio_say].

## <a id="nextsteps"></a>Дальнейшие действия
Этот код был предоставлен tooshow вы основные функциональные возможности с использованием Twilio в веб-роли ASP.NET в Azure. Перед развертыванием tooAzure в рабочей среде, вы можете tooadd дополнительные обработки ошибок или других компонентов. Например:

* Вместо использования веб-формы, может использовать хранилище больших двоичных объектов Azure или номера телефонов toostore экземпляр базы данных SQL Azure и вызовите текста. Сведения об использовании большие двоичные объекты в Azure см. в разделе [как toouse hello службы хранилища больших двоичных объектов Azure в .NET][howto_blob_storage_dotnet]. Сведения об использовании базы данных SQL см. в разделе [как toouse базы данных SQL Azure в приложениях .NET][howto_sql_azure_dotnet].
* Можно использовать `RoleEnvironment.getConfigurationSettings` идентификатор учетной записи Twilio tooretrieve hello и проверки подлинности токена из параметров конфигурации развертывания, вместо жестко запрограммированных значений hello в форме. Сведения о hello `RoleEnvironment` см. в описании [имен Microsoft.WindowsAzure.ServiceRuntime][azure_runtime_ref_dotnet].
* Прочитать рекомендации по безопасности Twilio hello в [https://www.twilio.com/docs/security][twilio_docs_security].
* Дополнительные сведения о службе Twilio см. на странице [https://www.twilio.com/docs][twilio_docs].

## <a name="seealso"></a>Дополнительные материалы
* [Как toouse Twilio для возможности голоса и SMS из Azure](twilio-dotnet-how-to-use-for-voice-sms.md)

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
