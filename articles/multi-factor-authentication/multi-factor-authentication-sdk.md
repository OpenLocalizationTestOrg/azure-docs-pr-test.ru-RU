---
title: "пакет средств разработки программного обеспечения aaaMFA для пользовательских приложений | Документы Microsoft"
description: "В этой статье показано, как toodownload и использование hello Azure SDK многофакторной проверки Подлинности tooenable двухшаговую проверку для пользовательских приложений."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a>Построение Multi-Factor Authentication в пользовательских приложениях (SDK)

Hello Azure многофакторной проверки подлинности Software Development Kit (SDK) предназначена для создания двухшаговую проверку непосредственно в hello входа или транзакции обрабатывает приложений в клиенте Azure AD.

Hello SDK многофакторной проверки подлинности доступна для C#, Visual Basic (.NET), Java, Perl, PHP и Ruby. Hello SDK предоставляет тонкую оболочку вокруг двухшаговую проверку. Он включает все необходимые toowrite кода, включая файлы с комментариями исходным кодом, файлы примеров и подробный файл ReadMe. Каждый пакет SDK также включает сертификат и закрытый ключ для шифрования транзакций, которые являются уникальными tooyour поставщика многофакторной проверки подлинности. При условии, что после создания поставщика можно загрузить hello SDK на столько языках и форматах необходимое.

Структура Hello hello API-интерфейсы в hello SDK многофакторной проверки подлинности проста. Убедитесь в одной функции вызова API tooan с параметрами варианта многофакторной hello (как режим верификации) и пользовательские данные (например hello телефонных номеров toocall или номера toovalidate hello ПИН-код). Hello API переводят вызов функции hello в web services запросов toohello облачной службы Azure Multi-factor Authentication. Все вызовы должны включать ссылку toohello закрытый сертификат, который включается в каждый пакет SDK.

Поскольку hello API-интерфейсы не имеют доступа toousers зарегистрировано в Azure Active Directory, необходимо предоставить сведения о пользователе в файл или базу данных. Кроме того hello API-интерфейсы не предоставляют функции управления регистрации или пользователя, поэтому требуется toobuild эти процессы в приложение.

> [!IMPORTANT]
> toodownload Здравствуйте SDK, необходимо toocreate поставщик многофакторной проверки подлинности Azure, даже если лицензий Azure MFA, Azure Active Directory Premium или EMS. Если создать поставщик многофакторной проверки подлинности Azure для этой цели с уже лицензий, убедитесь, что toocreate hello поставщика с hello **на включенного пользователя** модели. Свяжите hello поставщика toohello каталог, содержащий hello лицензий Azure MFA, Azure AD Premium или EMS. Эта конфигурация гарантирует, что оплата начисляется только при наличии нескольких уникальных пользователей, с помощью пакета SDK, чем hello число лицензий, которыми вы владеете hello.


## <a name="download-hello-sdk"></a>Загрузите пакет SDK для hello
Загрузка hello SDK Azure Multi-factor Authentication требуется [поставщик многофакторной проверки подлинности Azure](multi-factor-authentication-get-started-auth-provider.md).  Для этого нужна полная версия подписки Azure, даже если у вас уже есть лицензии Azure MFA, AAD Premium или Enterprise Mobility Suite.  hello toodownload SDK, перейдите toohello портал управления многофакторной. Можно получить доступ к порталу hello либо управление hello поставщик многофакторной проверки подлинности непосредственно, либо щелкнув hello **«Go toohello портала»** ссылку на странице параметров hello многофакторной проверки Подлинности службы.

### <a name="download-from-hello-azure-classic-portal"></a>Загрузить hello классический портал Azure
1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com) с правами администратора.
2. В левой части экрана приветствия выберите **Active Directory**.
3. В верхнем выберите hello страницы Active Directory hello **поставщики многофакторной проверки подлинности**
4. Внизу hello выберите **управление**. Откроется новая страница.
5. Щелкните hello слева, внизу hello **SDK**.
   <center>![Загрузить](./media/multi-factor-authentication-sdk/download.png)</center>
6. Выберите язык hello и ссылкам один hello загрузки.
7. Сохраните hello загрузки.

### <a name="download-from-hello-service-settings"></a>Загрузить параметры службы hello
1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com) с правами администратора.
2. В левой части экрана приветствия выберите **Active Directory**.
3. Дважды щелкните свой экземпляр Azure AD.
4. В верхней щелкните hello **Настройка**
5. В разделе многофакторной идентификации выберите **Управление параметрами службы**
   .![Скачивание](./media/multi-factor-authentication-sdk/download2.png)
6. На странице настройки службы hello hello нижней части экрана приветствия щелкните **портала toohello Go**. Откроется новая страница.
   ![Загрузить](./media/multi-factor-authentication-sdk/download3a.png)
7. Щелкните hello слева, внизу hello **SDK**.
8. Выберите язык hello и ссылкам один hello загрузки.
9. Сохраните hello загрузки.

## <a name="whats-in-hello-sdk"></a>Возможности hello SDK
Hello SDK включает hello следующих элементов:

* **README**. Объясняет, как toouse hello многофакторной проверки подлинности API-интерфейсы в новом или существующем приложении.
* **Исходные файлы** для Многофакторной идентификации
* **Сертификат клиента** использовать toocommunicate с hello служба многофакторной проверки подлинности
* **Закрытый ключ** для hello сертификата
* **Результаты вызова.** Список кодов результатов вызова. tooopen этот файл, используйте приложение с форматирования текста, например WordPad. Используйте hello tootest кодов результатов вызова и устранение неполадок реализации hello многофакторной проверки подлинности в приложении. Они отличаются от кодов состояния проверки подлинности.
* **Примеры.** Пример кода для базовой рабочей реализации процесса Multi-Factor Authentication.

> [!WARNING]
> сертификат клиента Hello имеет уникальный закрытый сертификат, созданный специально для вас. Не показывайте никому и не теряйте этот файл. Это вашей безопасности hello ключа tooensuring взаимодействия со службой hello многофакторной проверки подлинности.

## <a name="code-sample"></a>Пример кода
Этот пример кода показывает, как hello toouse API-интерфейсы в hello Azure Multi-factor Authentication SDK tooadd стандартный режим голосового вызова приложения tooyour проверки. Стандартный режим — это телефонный звонок, на который пользователь отвечает tooby нажатие клавиши # hello hello.

В этом примере используется hello C# .NET 2.0 SDK Multi-factor Authentication в простое приложение ASP.NET с серверной логикой на C#, но hello процесс похож на других языках. Поскольку hello SDK включает исходные файлы, не исполняемые файлы, можно создать файлы hello и ссылаться на них или включить их в самом приложении.

> [!NOTE]
> При реализации многофакторной проверки подлинности, следует используйте дополнительные методы hello (телефонный звонок или текстовое сообщение), как вторичная и третичная проверка toosupplement ваш основной способ проверки подлинности (имя пользователя и пароль). Эти методы не предназначены для использования в качестве основных способов проверки подлинности.

### <a name="code-sample-overview"></a>Обзор примера кода
Этот пример кода для демонстрации простого веб-приложения использует телефонный звонок с проверкой подлинности # ключа ответа tooverify hello пользователя. В рамках Multi-Factor Authentication фактор телефонного вызова называется стандартным режимом.

Hello клиентский код не включает какие-либо элементы зависящие от многофакторной проверки подлинности. Поскольку hello дополнительные факторы проверки подлинности не зависят от основной проверки подлинности hello, их можно добавить без изменения hello существующего интерфейса входа. Hello API-интерфейсы в hello SDK Multi-factor Authentication позволяют настроить взаимодействие с пользователем hello, но может не потребоваться toochange ничего вообще.

Hello серверный код добавляет стандартный режим проверки подлинности на шаге 2. Он создает объект PfAuthParams с параметрами hello, которые требуются для верификации в стандартном режиме: имя пользователя, телефонные номера, а также режим и hello путь toohello сертификат клиента (CertFilePath), который является обязательным для каждого вызова. Демонстрацию всех параметров в PfAuthParams см. в разделе файла пример hello в hello SDK.

Затем код hello передает функции hello PfAuthParams объекта toohello pf_authenticate(). Возвращаемое значение Hello указывает успешность hello hello проверки подлинности. Здравствуйте, параметры, callStatus и кода ошибки, содержат сведения о результате дополнительный вызов. коды результатов звонков Hello описаны в файле результатов вызова hello в hello SDK.

Такая минимальная реализация может занимать несколько строк. Однако в готовый код следует включить более сложную обработку ошибок, дополнительный код базы данных и улучшенный пользовательский интерфейс.

### <a name="web-client-code"></a>Код веб-клиента
Hello ниже приведен код веб-клиента для демонстрационной страницы.

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a>Серверный код
В следующий серверный код hello многофакторной проверки подлинности настраивается и запускается на шаге 2. Стандартный режим (MODE_STANDARD) — отвечает пользователь hello toowhich телефонный звонок, нажав клавишу # hello.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
