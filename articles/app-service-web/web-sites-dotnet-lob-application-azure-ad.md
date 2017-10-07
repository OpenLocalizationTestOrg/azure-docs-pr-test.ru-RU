---
title: "aaaCreate бизнес приложения Azure с проверкой подлинности Azure Active Directory | Документы Microsoft"
description: "Узнайте, как toocreate ASP.NET MVC для бизнес-приложения в службе приложений Azure, выполняющий проверку подлинности в Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a>Создание бизнес-приложения Azure с проверкой подлинности Azure Active Directory
В этой статье показано, как toocreate .NET из бизнес-приложения в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) с помощью hello [проверки подлинности и авторизации](../app-service/app-service-authentication-overview.md) компонентов. Здесь также показано, как toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery данных каталога в приложение hello.

Hello клиента Azure Active Directory, которая используется может быть каталогом только в Azure. Или может быть [синхронизированы с вашей локальной Active Directory](../active-directory/active-directory-aadconnect.md) toocreate входа единого для рабочих процессов, для локальных и удаленных. В этой статье используется каталог по умолчанию hello для учетной записи Azure.

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Что будет строиться
Будет создать простое приложение создание-чтение-обновления и удаления (CRUD) бизнес-в веб-приложениях службы приложений, который отслеживает рабочие элементы с hello следующие атрибуты:

* аутентификация пользователей в службе Azure Active Directory;
* запросы пользователей и групп каталога с помощью [API Graph Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)
* Используйте hello ASP.NET MVC *без проверки подлинности* шаблона

If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Дальнейшее действие](#next).

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Необходимые элементы
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Требуется hello следующие toocomplete этого учебника:

* Клиент Azure Active Directory с пользователями в различных группах
* Разрешения приложений toocreate на приветствия клиента Azure Active Directory
* Visual Studio 2013 с обновлением 4 или более поздней версии.
* [Пакет Azure SDK версии 2.8.1 или более поздней.](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a>Создание и развертывание приложения web tooAzure
1. В Visual Studio выберите **Файл** > **Создать** > **Проект**.
2. Выберите **Веб-приложение ASP.NET**, введите имя проекта и нажмите кнопку **ОК**.
3. Выберите hello **MVC** шаблон, затем измените hello проверки подлинности слишком**без проверки подлинности**. Убедитесь, что **узлов в облаке hello** выбран и нажмите кнопку **ОК**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. В hello **Создание приложения службы** диалоговое окно, нажмите кнопку **добавить учетную запись** (а затем **добавить учетную запись** в раскрывающемся списке hello) toolog в tooyour учетная запись Azure.
5. После этого перейдите на страницу "Настройка" веб-приложения. Создать группу ресурсов и новый план служб приложений, щелкнув соответствующий hello **New** кнопки. Нажмите кнопку **Обзор дополнительных служб Azure** toocontinue.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. В hello **службы** щелкните  **+**  tooadd базы данных SQL для вашего приложения. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. В **Настройка базы данных SQL**, нажмите кнопку **New** toocreate экземпляр SQL Server.
8. Настройте экземпляр SQL Server на вкладке **Настроить SQL Server**. Нажмите кнопку **ОК**, **ОК**, и **создать** tookick отключить создание приложения hello в Azure.
9. В **активности службы приложения Azure**, можно увидеть, когда будет завершено создание приложения hello. Нажмите кнопку  **публикации &lt;* appname*> toothis веб-приложения сейчас **, нажмите кнопку **публикации**. 
   
    После завершения выполнения Visual Studio, он открывается hello опубликовать приложение в браузере hello. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a>Настройка проверки подлинности и доступа к каталогу
1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello в левом меню, щелкните **службы приложений** > **&lt;*appname*> ** > **проверки подлинности и авторизации**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. Чтобы включить аутентификацию Azure Active Directory, щелкните **Включено** > **Azure Active Directory** > **Экспресс** > **OК**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. Нажмите кнопку **Сохранить** hello панели команд.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    После сохранения параметров проверки подлинности hello повторите перемещение tooyour приложение еще раз в браузере hello. Параметры по умолчанию обеспечивают проверку подлинности для всего приложения hello. Если вы не выполнили вход, вы несете перенаправленный tooa экран входа. После входа откроется приложение, защищенное по протоколу HTTPS. Далее необходимо tooenable доступа к данным toodirectory. 
5. Перейдите toohello [классический портал](https://manage.windowsazure.com).
6. Hello в левом меню, щелкните **Active Directory** > **каталог по умолчанию** > **приложений**  >   **&lt;* appname*> **.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    Это приложение hello Azure Active Directory, служба приложения создала для вас tooenable hello авторизации и проверки подлинности.
7. Нажмите кнопку **пользователей** и **группы** toomake, что у некоторых пользователей и групп в каталоге hello. Если пользователи и группы отсутствуют, создайте несколько тестовых пользователей и групп.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. Нажмите кнопку **Настройка** tooconfigure этого приложения.
9. Прокрутите вниз toohello **ключей** раздел и добавить ключ, выбрав длительность. Затем щелкните раскрывающийся список **Делегированные разрешения** и выберите разрешение **Чтение данных каталога**. 
   Щелкните **Сохранить**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. После сохранения параметров пролистать назад toohello **ключей** и нажмите кнопку hello **копирования** ключ клиента hello toocopy кнопки. 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > Если покинуть эту страницу сейчас, не будет возможности tooaccess, когда-либо еще раз ключа этого клиента.
    > 
    > 
11. Далее необходимо tooconfigure веб-приложения с данным ключом. Войдите в toohello [обозревателя ресурсов Azure](https://resources.azure.com) с учетной записью Azure.
12. В начале hello страницы приветствия, нажмите кнопку **чтения и записи** toomake изменения в hello обозревателя ресурсов Azure.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. Найти hello параметры проверки подлинности для приложения, расположенный в подписки >  **&lt;* имя_подписки*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **поставщики** > **Microsoft.Web**  >  **сайтов** > **&lt;*appname*> ** > **config**  >  **authsettings**.
14. Нажмите кнопку **Изменить**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. В области редактирования hello, задайте hello `clientSecret` и `additionalLoginParams` свойства следующим образом.
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. Нажмите кнопку **поместить** на hello top toosubmit изменения.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. Теперь tootest, если у вас имеется разрешение hello маркера hello tooaccess Azure Active Directory Graph API, перейдя в  **https://&lt;*appname*>.azurewebsites.net/.auth/me** в вашей Обозреватель. Если вы настроили все правильно, вы увидите hello `access_token` свойство в hello ответ JSON.
    
    Hello `~/.auth/me` URL-адрес находится под управлением приложения проверки подлинности службы или toogive авторизации, вы все hello сведения, связанные с проверкой подлинности tooyour сеанса. Дополнительные сведения см. в статье [Проверка подлинности и авторизация в службе приложений Azure](../app-service/app-service-authentication-overview.md).
    
    > [!NOTE]
    > Hello `access_token` имеет срок действия. Тем не менее функция аутентификации и авторизации в службе приложений обеспечивает обновление маркера с использованием `~/.auth/refresh`. Дополнительные сведения о том, как toouse, в разделе [маркер службы App Store](https://cgillum.tech/2016/03/07/app-service-token-store/).
    > 
    > 

В следующем разделе описываются действия, выполняемые с данными каталога.

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a>Добавить функциональные возможности бизнес-приложение tooyour
Теперь необходимо создать простое приложения CRUD для отслеживания рабочих элементов.  

1. В папке ~\Models hello, создайте файл класса с именем WorkItem.cs и замените `public class WorkItem {...}` с hello, следующий код:
   
     using System.ComponentModel.DataAnnotations;
   
     public class WorkItem   {
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     }
   
     public enum WorkItemStatus   {
   
         Open,
         Investigating,
         Resolved,
         Closed
     }
2. Построение проекта toomake hello новая логика формирование шаблонов модели доступен toohello, в Visual Studio.
3. Добавить новый элемент формирования шаблонов `WorkItemsController` toohello ~\Controllers папку (щелкните правой кнопкой мыши **контроллеров**, слишком точки**добавить**и выберите **новый элемент формирования шаблонов**). 
4. Выберите **Контроллер MVC 5 с представлениями, использующий Entity Framework** и щелкните **Добавить**.
5. Выберите hello созданной модели, нажмите кнопку  **+**  и затем **добавить** tooadd контекст данных, а затем нажмите кнопку **добавить**.
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. В ~\Views\WorkItems\Create.cshtml (автоматического формирования шаблонов элемента), найти hello `Html.BeginForm` вспомогательный метод и внесите следующие выделенные изменения hello:  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   Обратите внимание, что `token` и `tenant` используются hello `AadPicker` toomake объекта, вызывает Azure Active Directory Graph API. Объект `AadPicker` добавим позже.     
   
   > [!NOTE]
   > Точно так же можно получить `token` и `tenant` из hello на стороне клиента с `~/.auth/me`, но может быть вызов дополнительного сервера. Например:
   > 
   > $.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });
   > 
   > 
7. Внести аналогичные изменения с hello ~ \Views\WorkItems\Edit.cshtml.
8. Hello `AadPicker` объект определен в сценарии необходимые tooadd tooyour проекта. Щелкните правой кнопкой мыши папку ~\Scripts hello, укажите слишком**добавить**и нажмите кнопку **файл JavaScript**. Тип `AadPickerLibrary` hello имя файла и нажмите кнопку **ОК**.
9. Копировать содержимое hello [здесь](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) в ~ \Scripts\AadPickerLibrary.js.
   
   В сценарии hello hello `AadPicker` вызывает [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch для пользователей и групп, соответствующих входных данных hello.  
10. ~\Scripts\AadPickerLibrary.js также использует hello [мини-приложение автозаполнения пользовательского интерфейса jQuery](https://jqueryui.com/autocomplete/). Поэтому необходимо tooadd jQuery UI tooyour проекта. Щелкните проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.
11. Hello диспетчера пакетов NuGet, нажмите кнопку Обзор, тип **пользовательского интерфейса jquery** в hello панель поиска и нажмите кнопку **jQuery.UI.Combined**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. Hello правой панели щелкните **установить**, нажмите кнопку **ОК** tooproceed.
13. Откройте ~\App_Start\BundleConfig.cs и внесите следующие выделенные изменения hello.  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    Существуют дополнительные toomanage способов высокопроизводительных JavaScript и CSS-файлов в приложении. Однако для простоты мы будем просто toopiggyback на пакеты hello, загруженных в каждом представлении.
14. Наконец, в ~ \Global.asax, добавить следующие строки кода в hello hello `Application_Start()` метод. `Ctrl`+`.`на каждое разрешение имен ошибка слишком ее устранению.
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > Необходимо эту строку кода, так как использует шаблона MVC по умолчанию hello <code>[ValidateAntiForgeryToken]</code> оформления на некоторых действиях hello. Из-за toohello поведение, описываемого [Аллен Brock](https://twitter.com/BrockLAllen) в [MVC 4, AntiForgeryToken и утверждений](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) вашей HTTP POST возможен сбой проверки маркера защиты от подделки, поскольку:
    > 
    > * Azure Active Directory не отправляет http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, требуемой по умолчанию токен борьбы с фальсификацией hello.
    > * Если Azure Active Directory — каталог, синхронизированные с AD FS, hello AD FS доверия по умолчанию не отправляет hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider утверждения, несмотря на то, что можно вручную настроить AD FS toosend Это утверждение.
    > 
    > `ClaimTypes.NameIdentifies`Указывает hello утверждения `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, который поддерживает Azure Active Directory.  
    > 
    > 
15. Теперь опубликуйте изменения. Щелкните свой проект правой кнопкой мыши и выберите **Опубликовать**.
16. Нажмите кнопку **параметры**, убедитесь в отсутствии tooyour строку подключения базы данных SQL, выберите **обновление базы данных** toomake hello изменений схемы в модели и нажмите кнопку **публикации** .
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. В браузере hello перейдите toohttps: / /&lt;*appname*>.azurewebsites.net/workitems и нажмите кнопку **создать новый**.
18. Нажмите кнопку в hello **AssignedToName** поле. В раскрывающемся списке должны отобразиться пользователи и группы из клиента Azure Active Directory. Введите toofilter или использовать hello `Up` или `Down` или щелкните tooselect hello пользователя или группы. 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. Нажмите кнопку **создать** toosave hello изменения. Нажмите кнопку **изменить** hello создания рабочего элемента tooobserve hello такое же поведение.

Поздравляем, теперь бизнес-приложение с доступом к каталогу запущено в Azure! Нет hello Graph API гораздо больше возможностей. Ознакомьтесь со [справочником по API Graph Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).

<a name="next"></a>

## <a name="next-step"></a>Дальнейшее действие
Если управление доступом на основе ролей (RBAC) требуется для бизнес-приложения в azure, см. раздел [WebApp RoleClaims DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) образец hello группы Azure Active Directory. Там показано, как tooenable роли для приложения Azure Active Directory и затем авторизовать пользователей с hello `[Authorize]` оформления.

Если бизнес-приложения требуется доступ к данным tooon организациями, см. раздел [доступа к локальным ресурсам с помощью гибридных подключений в службе приложений Azure](web-sites-hybrid-connection-get-started.md).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Дополнительные ресурсы
* [Проверка подлинности и авторизация в службе приложений Azure](../app-service/app-service-authentication-overview.md)
* [Проверка подлинности в приложении Azure с помощью локального каталога Active Directory](web-sites-authentication-authorization.md)
* [Создание веб-приложения .NET MVC в службе приложений Azure с аутентификацией AD FS](web-sites-dotnet-lob-application-adfs.md)
* [Проверка подлинности службы приложения и hello API Azure AD Graph](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [Примеры и документация Microsoft Azure Active Directory](https://github.com/AzureADSamples)
* [Поддерживаемые типы маркеров и утверждений](http://msdn.microsoft.com/library/azure/dn195587.aspx)
