---
title: "aaaProtect серверной части веб-API с Azure Active Directory и управление API | Документы Microsoft"
description: "Узнайте, как tooprotect серверной части веб-API с Azure Active Directory и управления API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="df602-103">Как tooprotect серверной части веб-API с Azure Active Directory и управления API</span><span class="sxs-lookup"><span data-stu-id="df602-103">How tooprotect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="df602-104">Здравствуйте, следуя видео показано, как toobuild серверной части веб-API и защитите его с использованием протокола OAuth 2.0 с Azure Active Directory и управления API.</span><span class="sxs-lookup"><span data-stu-id="df602-104">hello following video shows how toobuild a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="df602-105">В этой статье содержатся общие сведения и Дополнительные сведения о hello шагах в видео hello.</span><span class="sxs-lookup"><span data-stu-id="df602-105">This article provides an overview and additional information for hello steps in hello video.</span></span> <span data-ttu-id="df602-106">Посмотрев этот 24-минутный ролик, вы познакомитесь со следующими темами.</span><span class="sxs-lookup"><span data-stu-id="df602-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="df602-107">Создание серверной части веб-API и обеспечение ее безопасности при помощи AAD ― с 1:30</span><span class="sxs-lookup"><span data-stu-id="df602-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="df602-108">Импорт hello API управления API - начиная с 7:10</span><span class="sxs-lookup"><span data-stu-id="df602-108">Import hello API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="df602-109">Настройка hello разработчика портала toocall hello API — начиная с 9:09</span><span class="sxs-lookup"><span data-stu-id="df602-109">Configure hello Developer portal toocall hello API - starting at 9:09</span></span>
* <span data-ttu-id="df602-110">Настройка типа hello toocall классического приложения API — начиная с 18:08</span><span class="sxs-lookup"><span data-stu-id="df602-110">Configure a desktop application toocall hello API - starting at 18:08</span></span>
* <span data-ttu-id="df602-111">Настройка политики toopre JWT проверки-авторизации запросов — начиная с 20:47</span><span class="sxs-lookup"><span data-stu-id="df602-111">Configure a JWT validation policy toopre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="df602-112">Создание каталога Azure AD</span><span class="sxs-lookup"><span data-stu-id="df602-112">Create an Azure AD directory</span></span>
<span data-ttu-id="df602-113">toosecure резервного веб-API с помощью Azure Active Directory, следует сначала создать клиент AAD.</span><span class="sxs-lookup"><span data-stu-id="df602-113">toosecure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="df602-114">В этом видеоролике используется клиент с именем **APIMDemo** .</span><span class="sxs-lookup"><span data-stu-id="df602-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="df602-115">toocreate клиент AAD toohello входа [классический портал Azure](https://manage.windowsazure.com) и нажмите кнопку **New**->**службы приложений**->**Active Каталог**->**каталога**->**настраиваемое создание**.</span><span class="sxs-lookup"><span data-stu-id="df602-115">toocreate an AAD tenant, sign-in toohello [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="df602-117">В этом примере каталог с именем **APIMDemo** создается в домене по умолчанию с именем **DemoAPIM.onmicrosoft.com**. Этот каталог используется во всех hello видео.</span><span class="sxs-lookup"><span data-stu-id="df602-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**. This directory is used throughout hello video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="df602-119">Создание службы веб-API, защищенной с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df602-119">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="df602-120">На этом шаге создается внутренняя служба веб-API с помощью Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="df602-120">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="df602-121">На этом шаге hello видео начинается с 1:30.</span><span class="sxs-lookup"><span data-stu-id="df602-121">This step of hello video starts at 1:30.</span></span> <span data-ttu-id="df602-122">toocreate веб-API серверного проекта в Visual Studio щелкните **файл**->**New**->**проекта**и выберите **ASP.NET Web Приложение** из hello **Web** списка шаблонов.</span><span class="sxs-lookup"><span data-stu-id="df602-122">toocreate Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from hello **Web** templates list.</span></span> <span data-ttu-id="df602-123">В этом видео hello проект называется **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="df602-123">In this video hello project is named **APIMAADDemo**.</span></span> <span data-ttu-id="df602-124">Нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="df602-124">Click **OK** toocreate hello project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="df602-126">Нажмите кнопку **веб-API** из hello **выберите список шаблонов** toocreate проект веб-API.</span><span class="sxs-lookup"><span data-stu-id="df602-126">Click **Web API** from hello **Select a template list** toocreate a Web API project.</span></span> <span data-ttu-id="df602-127">Нажмите кнопку проверки подлинности Azure Directory tooconfigure **изменить аутентификацию**.</span><span class="sxs-lookup"><span data-stu-id="df602-127">tooconfigure Azure Directory Authentication click **Change Authentication**.</span></span>

![Новый проект][api-management-new-project]

<span data-ttu-id="df602-129">Нажмите кнопку **учетные записи организации**и укажите hello **домена** клиента AAD.</span><span class="sxs-lookup"><span data-stu-id="df602-129">Click **Organizational Accounts**, and specify hello **Domain** of your AAD tenant.</span></span> <span data-ttu-id="df602-130">В этом примере hello домен является **DemoAPIM.onmicrosoft.com**. hello домена каталога можно получить из hello **домены** вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="df602-130">In this example hello domain is **DemoAPIM.onmicrosoft.com**. hello domain of your directory can be obtained from hello **Domains** tab of your directory.</span></span>

![Домены][api-management-aad-domains]

<span data-ttu-id="df602-132">Настройте параметры требуемого hello в hello **изменить аутентификацию** диалоговое окно и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="df602-132">Configure hello desired settings in hello **Change Authentication** dialog box and click **OK**.</span></span>

![Изменить проверку подлинности][api-management-change-authentication]

<span data-ttu-id="df602-134">При нажатии кнопки **ОК** Visual Studio попытается tooregister приложения с каталогом Azure AD и может быть запрос toosign в средой Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="df602-134">When you click **OK** Visual Studio will attempt tooregister your application with your Azure AD directory and you may be prompted toosign in by Visual Studio.</span></span> <span data-ttu-id="df602-135">Войдите с помощью учетной записи администратора вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="df602-135">Sign in using an administrative account for your directory.</span></span>

![Войдите в Studio tooVisual][api-management-sign-in-vidual-studio]

<span data-ttu-id="df602-137">tooconfigure этот проект как hello Azure веб-API проверьте поле для **узлов в облаке hello** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="df602-137">tooconfigure this project as an Azure Web API check hello box for **Host in hello cloud** and then click **OK**.</span></span>

![Новый проект][api-management-new-project-cloud]

<span data-ttu-id="df602-139">Может быть запрос toosign в tooAzure и настройте hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="df602-139">You may be prompted toosign in tooAzure, and then you can configure hello Web App.</span></span>

![Настройка][api-management-configure-web-app]

<span data-ttu-id="df602-141">В этом примере создается новый **план службы приложений** с именем **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="df602-141">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="df602-142">Нажмите кнопку **ОК** tooconfigure hello веб-приложения и создайте проект hello.</span><span class="sxs-lookup"><span data-stu-id="df602-142">Click **OK** tooconfigure hello Web App and create hello project.</span></span>

## <a name="add-hello-code-toohello-web-api-project"></a><span data-ttu-id="df602-143">Добавление проекта веб-API toohello кода hello</span><span class="sxs-lookup"><span data-stu-id="df602-143">Add hello code toohello Web API project</span></span>
<span data-ttu-id="df602-144">Hello следующим шагом в видео hello добавляет проект веб-API toohello кода hello.</span><span class="sxs-lookup"><span data-stu-id="df602-144">hello next step in hello video adds hello code toohello Web API project.</span></span> <span data-ttu-id="df602-145">Этот шаг начинается с отметки времени 4:35.</span><span class="sxs-lookup"><span data-stu-id="df602-145">This step starts at 4:35.</span></span>

<span data-ttu-id="df602-146">Hello веб-API в этом примере реализуется базовой службы калькулятора с помощью модели и контроллера.</span><span class="sxs-lookup"><span data-stu-id="df602-146">hello Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="df602-147">Щелкните правой кнопкой мыши модель hello tooadd для службы hello **моделей** в **обозревателе решений** и выберите **добавить**, **класса**.</span><span class="sxs-lookup"><span data-stu-id="df602-147">tooadd hello model for hello service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="df602-148">Имя класса hello `CalcInput` и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="df602-148">Name hello class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="df602-149">Добавьте следующее hello `using` инструкции toohello вверху hello `CalcInput.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="df602-149">Add hello following `using` statement toohello top of hello `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="df602-150">Замените класс создан hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="df602-150">Replace hello generated class with hello following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="df602-151">Щелкните правой кнопкой мыши **Контроллеры** в **обозревателе решений** и выберите **Добавить**->**Контроллер**.</span><span class="sxs-lookup"><span data-stu-id="df602-151">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="df602-152">Выберите элемент **Контроллер Web API 2 – пустой** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="df602-152">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="df602-153">Тип **CalcController** hello контроллера имя и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="df602-153">Type **CalcController** for hello Controller name and click **Add**.</span></span>

![Добавление контролера][api-management-add-controller]

<span data-ttu-id="df602-155">Добавьте следующее hello `using` инструкции toohello вверху hello `CalcController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="df602-155">Add hello following `using` statement toohello top of hello `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="df602-156">Замените класс контроллера hello создается после кода hello.</span><span class="sxs-lookup"><span data-stu-id="df602-156">Replace hello generated controller class with hello following code.</span></span> <span data-ttu-id="df602-157">Этот код реализует hello `Add`, `Subtract`, `Multiply`, и `Divide` операций hello базовый API-Интерфейс калькулятора.</span><span class="sxs-lookup"><span data-stu-id="df602-157">This code implements hello `Add`, `Subtract`, `Multiply`, and `Divide` operations of hello Basic Calculator API.</span></span>

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

<span data-ttu-id="df602-158">Нажмите клавишу **F6** toobuild и проверить решение hello.</span><span class="sxs-lookup"><span data-stu-id="df602-158">Press **F6** toobuild and verify hello solution.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="df602-159">Публикация проекта tooAzure hello</span><span class="sxs-lookup"><span data-stu-id="df602-159">Publish hello project tooAzure</span></span>
<span data-ttu-id="df602-160">В этом шаге hello Visual Studio проект является опубликованным tooAzure.</span><span class="sxs-lookup"><span data-stu-id="df602-160">In this step hello Visual Studio project is published tooAzure.</span></span> <span data-ttu-id="df602-161">На этом шаге hello видео начинается 5:45.</span><span class="sxs-lookup"><span data-stu-id="df602-161">This step of hello video starts at 5:45.</span></span>

<span data-ttu-id="df602-162">toopublish Здравствуйте tooAzure проекта, щелкните правой кнопкой мыши hello **APIMAADDemo** проекта в Visual Studio и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="df602-162">toopublish hello project tooAzure, right-click hello **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="df602-163">Оставьте параметры по умолчанию hello в hello **веб-публикация** диалоговое окно и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="df602-163">Keep hello default settings in hello **Publish Web** dialog box and click **Publish**.</span></span>

![Веб-публикация][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a><span data-ttu-id="df602-165">Предоставление разрешений приложения-службы внутренних toohello Azure AD</span><span class="sxs-lookup"><span data-stu-id="df602-165">Grant permissions toohello Azure AD backend service application</span></span>
<span data-ttu-id="df602-166">Новое приложение hello серверной службы создается в каталоге Azure AD как часть настройки hello и процесс публикации проекта веб-API.</span><span class="sxs-lookup"><span data-stu-id="df602-166">A new application for hello backend service is created in your Azure AD directory as part of hello configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="df602-167">На этом шаге hello видео начиная с 6:13, разрешения предоставляются серверной части toohello веб-API.</span><span class="sxs-lookup"><span data-stu-id="df602-167">In this step of hello video, starting at 6:13, permissions are granted toohello Web API backend.</span></span>

![Приложение][api-management-aad-backend-app]

<span data-ttu-id="df602-169">Щелкните имя hello hello приложения tooconfigure hello необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="df602-169">Click hello name of hello application tooconfigure hello required permissions.</span></span> <span data-ttu-id="df602-170">Перейдите toohello **Настройка** вкладку и прокрутите вниз toohello **tooother разрешения приложений** раздела.</span><span class="sxs-lookup"><span data-stu-id="df602-170">Navigate toohello **Configure** tab and scroll down toohello **permissions tooother applications** section.</span></span> <span data-ttu-id="df602-171">Нажмите кнопку hello **разрешения приложения** раскрывающегося списка рядом с **Windows** **Azure Active Directory**, установите флажок "hello" для **читать данные каталога**и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df602-171">Click hello **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check hello box for **Read directory data**, and click **Save**.</span></span>

![Добавление разрешений][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="df602-173">Если **Windows** **Azure Active Directory** — не указан в списке разрешения tooother приложений, щелкните **добавить приложение** и добавьте его из списка hello.</span><span class="sxs-lookup"><span data-stu-id="df602-173">If **Windows** **Azure Active Directory** is not listed under permissions tooother applications, click **Add application** and add it from hello list.</span></span>
> 
> 

<span data-ttu-id="df602-174">Запишите hello **URI идентификатора приложения** для использования на следующем шаге при настройке приложения Azure AD портал разработчика управления API hello.</span><span class="sxs-lookup"><span data-stu-id="df602-174">Make a note of hello **App Id URI** for use in a subsequent step when an Azure AD application is configured for hello API Management developer portal.</span></span>

![URI идентификатора приложения][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a><span data-ttu-id="df602-176">Импортировать hello веб-API в службе управления API</span><span class="sxs-lookup"><span data-stu-id="df602-176">Import hello Web API into API Management</span></span>
<span data-ttu-id="df602-177">API-интерфейсы настроены из портала издателя hello API, который можно получить с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="df602-177">APIs are configured from hello API publisher portal, which is accessed through hello Azure Portal.</span></span> <span data-ttu-id="df602-178">tooreach его, нажмите кнопку **портал издателя** из инструментов hello службы управления API.</span><span class="sxs-lookup"><span data-stu-id="df602-178">tooreach it, click **Publisher portal** from hello toolbar of your API Management service.</span></span> <span data-ttu-id="df602-179">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [управление первый API] [ Manage your first API] учебника.</span><span class="sxs-lookup"><span data-stu-id="df602-179">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API][Manage your first API] tutorial.</span></span>

![Портал издателя][api-management-management-console]

<span data-ttu-id="df602-181">Операции могут быть [вручную добавить tooAPIs](api-management-howto-add-operations.md), или они могут быть импортированы.</span><span class="sxs-lookup"><span data-stu-id="df602-181">Operations can be [added tooAPIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="df602-182">В этом видео операции импортируются в формате Swagger начиная с отметки времени 6:40.</span><span class="sxs-lookup"><span data-stu-id="df602-182">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="df602-183">Создайте файл с именем `calcapi.json` с следующие содержимое и сохраните его tooyour компьютера.</span><span class="sxs-lookup"><span data-stu-id="df602-183">Create a file named `calcapi.json` with following contents and save it tooyour computer.</span></span> <span data-ttu-id="df602-184">Убедитесь, что hello `host` атрибут указывает серверной части tooyour веб-API.</span><span class="sxs-lookup"><span data-stu-id="df602-184">Ensure that hello `host` attribute points tooyour Web API backend.</span></span> <span data-ttu-id="df602-185">В этом примере используется `"host": "apimaaddemo.azurewebsites.net"` .</span><span class="sxs-lookup"><span data-stu-id="df602-185">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

<span data-ttu-id="df602-186">Калькулятор hello tooimport API, нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **импорта API**.</span><span class="sxs-lookup"><span data-stu-id="df602-186">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Кнопка импорта API][api-management-import-api]

<span data-ttu-id="df602-188">Выполните следующие шаги tooconfigure hello калькулятора API hello.</span><span class="sxs-lookup"><span data-stu-id="df602-188">Perform hello following steps tooconfigure hello calculator API.</span></span>

1. <span data-ttu-id="df602-189">Нажмите кнопку **из файла**, Обзор toohello `calculator.json` файл был сохранен и нажмите кнопку hello **Swagger** переключатель.</span><span class="sxs-lookup"><span data-stu-id="df602-189">Click **From file**, browse toohello `calculator.json` file you saved, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="df602-190">Тип **calc** в hello **суффикс URL-адрес API** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="df602-190">Type **calc** into hello **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="df602-191">Нажмите кнопку в hello **продуктов (необязательно)** и выберите **начальный**.</span><span class="sxs-lookup"><span data-stu-id="df602-191">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="df602-192">Нажмите кнопку **Сохранить** tooimport hello API.</span><span class="sxs-lookup"><span data-stu-id="df602-192">Click **Save** tooimport hello API.</span></span>

![Добавление нового API][api-management-import-new-api]

<span data-ttu-id="df602-194">После импорта hello API hello сводной страницы для hello API отображается в портал издателя hello.</span><span class="sxs-lookup"><span data-stu-id="df602-194">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a><span data-ttu-id="df602-195">Вызвать hello API неудачно с портала разработчиков hello</span><span class="sxs-lookup"><span data-stu-id="df602-195">Call hello API unsuccessfully from hello developer portal</span></span>
<span data-ttu-id="df602-196">На этом этапе hello API была импортирована в API управления, но еще невозможен успешно с портала разработчиков hello поскольку hello серверная служба защищена с помощью проверки подлинности Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df602-196">At this point, hello API has been imported into API Management, but cannot yet be called successfully from hello developer portal because hello backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="df602-197">Это показано в видео hello, начиная с 7:40 с помощью hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="df602-197">This is demonstrated in hello video starting at 7:40 using hello following steps.</span></span>

<span data-ttu-id="df602-198">Нажмите кнопку **портал разработчиков** из hello правой верхней части портала издателя hello.</span><span class="sxs-lookup"><span data-stu-id="df602-198">Click **Developer portal** from hello top-right side of hello publisher portal.</span></span>

![Портал разработчика][api-management-developer-portal-menu]

<span data-ttu-id="df602-200">Нажмите кнопку **API-интерфейсы** и нажмите кнопку hello **калькулятора** API.</span><span class="sxs-lookup"><span data-stu-id="df602-200">Click **APIs** and click hello **Calculator** API.</span></span>

![Портал разработчика][api-management-dev-portal-apis]

<span data-ttu-id="df602-202">Щелкните **Попробовать**.</span><span class="sxs-lookup"><span data-stu-id="df602-202">Click **Try it**.</span></span>

![Попробовать][api-management-dev-portal-try-it]

<span data-ttu-id="df602-204">Нажмите кнопку **отправки** и записать состояние ответа hello **проверки подлинности 401**.</span><span class="sxs-lookup"><span data-stu-id="df602-204">Click **Send** and note hello response status of **401 Unauthorized**.</span></span>

![Отправка][api-management-dev-portal-send-401]

<span data-ttu-id="df602-206">Hello запрос не авторизован, так как API внутреннего сервера hello защищен службой Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df602-206">hello request is unauthorized because hello backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="df602-207">До успешного вызова hello API портал разработчика hello должен иметь настроенное tooauthorize разработчиков, использующих OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="df602-207">Before successfully calling hello API hello developer portal must be configured tooauthorize developers using OAuth 2.0.</span></span> <span data-ttu-id="df602-208">Этот процесс описан в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="df602-208">This process is described in hello following sections.</span></span>

## <a name="register-hello-developer-portal-as-an-aad-application"></a><span data-ttu-id="df602-209">Зарегистрировать портал разработчиков hello как приложение AAD</span><span class="sxs-lookup"><span data-stu-id="df602-209">Register hello developer portal as an AAD application</span></span>
<span data-ttu-id="df602-210">Hello первым шагом в настройке hello разработчика tooauthorize портала разработчиков, использующих OAuth 2.0 — портал разработчиков hello tooregister как приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="df602-210">hello first step in configuring hello developer portal tooauthorize developers using OAuth 2.0 is tooregister hello developer portal as an AAD application.</span></span> <span data-ttu-id="df602-211">Это продемонстрировано начиная с 8:27 в видео hello.</span><span class="sxs-lookup"><span data-stu-id="df602-211">This is demonstrated starting at 8:27 in hello video.</span></span>

<span data-ttu-id="df602-212">Клиент Azure AD toohello из hello первым шагом этого видео, в этом примере перейдите **APIMDemo** и перейдите toohello **приложений** вкладки.</span><span class="sxs-lookup"><span data-stu-id="df602-212">Navigate toohello Azure AD tenant from hello first step of this video, in this example **APIMDemo** and navigate toohello **Applications** tab.</span></span>

![Новое приложение][api-management-aad-new-application-devportal]

<span data-ttu-id="df602-214">Нажмите кнопку hello **добавить** toocreate новое приложение Azure Active Directory, а кнопку **добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="df602-214">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Новое приложение][api-management-new-aad-application-menu]

<span data-ttu-id="df602-216">Выберите **веб-приложение или веб-API**, введите имя и щелкните стрелку hello.</span><span class="sxs-lookup"><span data-stu-id="df602-216">Choose **Web application and/or Web API**, enter a name, and click hello next arrow.</span></span> <span data-ttu-id="df602-217">В этом примере используется **APIMDeveloperPortal** .</span><span class="sxs-lookup"><span data-stu-id="df602-217">In this example **APIMDeveloperPortal** is used.</span></span>

![Новое приложение][api-management-aad-new-application-devportal-1]

<span data-ttu-id="df602-219">Для **URL-адрес входа** введите hello URL-адрес службы управления API и добавьте `/signin`.</span><span class="sxs-lookup"><span data-stu-id="df602-219">For **Sign-on URL** enter hello URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="df602-220">В этом примере используется `https://contoso5.portal.azure-api.net/signin` .</span><span class="sxs-lookup"><span data-stu-id="df602-220">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="df602-221">Для **URL ИД приложения** введите hello URL-адрес службы управления API и добавьте несколько уникальных знаков.</span><span class="sxs-lookup"><span data-stu-id="df602-221">For **App Id URL** enter hello URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="df602-222">Это могут быть любые знаки. В данном примере используется `https://contoso5.portal.azure-api.net/dp`.</span><span class="sxs-lookup"><span data-stu-id="df602-222">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="df602-223">При необходимости hello **свойства приложения** будут настроены, нажмите кнопку приложения hello toocreate флажок hello.</span><span class="sxs-lookup"><span data-stu-id="df602-223">When hello  desired **App properties** are configured, click hello check mark toocreate hello application.</span></span>

![Новое приложение][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="df602-225">Настройка сервера авторизации OAuth 2.0 в управлении API</span><span class="sxs-lookup"><span data-stu-id="df602-225">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="df602-226">Hello следующим шагом является tooconfigure сервера авторизации OAuth 2.0 в службе управления API.</span><span class="sxs-lookup"><span data-stu-id="df602-226">hello next step is tooconfigure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="df602-227">Здесь демонстрируется hello видео, начиная с 9:43.</span><span class="sxs-lookup"><span data-stu-id="df602-227">This step is demonstrated in hello video starting at 9:43.</span></span>

<span data-ttu-id="df602-228">Нажмите кнопку **безопасности** меню управления API hello hello левой части экрана выберите **OAuth 2.0**и нажмите кнопку **добавьте авторизацию** сервера.</span><span class="sxs-lookup"><span data-stu-id="df602-228">Click **Security** from hello API Management menu on hello left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Добавление сервера авторизации][api-management-add-authorization-server]

<span data-ttu-id="df602-230">Введите имя и описание (необязательно) в hello **имя** и **описание** поля.</span><span class="sxs-lookup"><span data-stu-id="df602-230">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> <span data-ttu-id="df602-231">Эти поля обязательны для сервера авторизации OAuth 2.0 hello используется tooidentify в пределах экземпляра службы управления API hello.</span><span class="sxs-lookup"><span data-stu-id="df602-231">These fields are used tooidentify hello OAuth 2.0 authorization server within hello API Management service instance.</span></span> <span data-ttu-id="df602-232">В этом примере используется **демоверсия сервера авторизации** .</span><span class="sxs-lookup"><span data-stu-id="df602-232">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="df602-233">Позже при указании сервера toobe OAuth 2.0, используемый для проверки подлинности для API будет выбрать это имя.</span><span class="sxs-lookup"><span data-stu-id="df602-233">Later when you specify an OAuth 2.0 server toobe used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="df602-234">Для hello **URL-адрес страницы регистрации клиента** введите значение заполнителя, например `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="df602-234">For hello **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="df602-235">Hello **URL-адрес страницы регистрации клиента** точки toohello страницы, что у пользователей, можно использовать toocreate и настроить свои собственные учетные записи для поставщиков OAuth 2.0, которые поддерживают управление учетными записями пользователей.</span><span class="sxs-lookup"><span data-stu-id="df602-235">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="df602-236">В этом примере пользователи не создают и не настраивают собственные учетные записи, поэтому используется заполнитель.</span><span class="sxs-lookup"><span data-stu-id="df602-236">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Добавление сервера авторизации][api-management-add-authorization-server-1]

<span data-ttu-id="df602-238">Затем укажите **URL-адрес конечной точки авторизации** и **URL-адрес конечной точки маркера**.</span><span class="sxs-lookup"><span data-stu-id="df602-238">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Сервер авторизации][api-management-add-authorization-server-1a]

<span data-ttu-id="df602-240">Эти значения могут быть получены из hello **конечные точки приложения** страница hello AAD приложения, созданного для hello портал разработчиков.</span><span class="sxs-lookup"><span data-stu-id="df602-240">These values can be retrieved from hello **App Endpoints** page of hello AAD application you created for hello developer portal.</span></span> <span data-ttu-id="df602-241">конечные точки hello tooaccess перейдите toohello **Настройка** для AAD приложения hello и нажмите кнопку **просмотреть конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="df602-241">tooaccess hello endpoints navigate toohello **Configure** tab for hello AAD application and click **View endpoints**.</span></span>

![Приложение][api-management-aad-devportal-application]

![Просмотреть конечные точки][api-management-aad-view-endpoints]

<span data-ttu-id="df602-244">Копировать hello **конечная точка авторизации OAuth 2.0** и вставьте его в hello **URL-адрес конечной точки авторизации** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="df602-244">Copy hello **OAuth 2.0 authorization endpoint** and paste it into hello **Authorization endpoint URL** textbox.</span></span>

![Добавление сервера авторизации][api-management-add-authorization-server-2]

<span data-ttu-id="df602-246">Копировать hello **конечная точка маркера OAuth 2.0** и вставьте его в hello **токен URL-адрес конечной точки** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="df602-246">Copy hello **OAuth 2.0 token endpoint** and paste it into hello **Token endpoint URL** textbox.</span></span>

![Добавление сервера авторизации][api-management-add-authorization-server-2a]

<span data-ttu-id="df602-248">Кроме toopasting в конечную точку токена hello, добавить дополнительный текст параметр с именем **ресурсов** используйте для значение hello hello **URI идентификатора приложения** из AAD приложения hello серверной службы, которая была hello создается, когда проект Visual Studio hello был опубликован.</span><span class="sxs-lookup"><span data-stu-id="df602-248">In addition toopasting in hello token endpoint, add an additional body parameter named **resource** and for hello value use hello **App Id URI** from hello AAD application for hello backend service that was created when hello Visual Studio project was published.</span></span>

![URI идентификатора приложения][api-management-aad-sso-uri]

<span data-ttu-id="df602-250">Затем укажите учетные данные клиента hello.</span><span class="sxs-lookup"><span data-stu-id="df602-250">Next, specify hello client credentials.</span></span> <span data-ttu-id="df602-251">Hello учетные данные для hello ресурс, tooaccess, в этом случае hello портал разработчиков.</span><span class="sxs-lookup"><span data-stu-id="df602-251">These are hello credentials for hello resource you want tooaccess, in this case hello developer portal.</span></span>

![Учетные данные клиента][api-management-client-credentials]

<span data-ttu-id="df602-253">tooget hello **идентификатор клиента**, перейдите toohello **Настройка** вкладка hello приложения AAD для разработчика hello портала и скопируйте hello **идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="df602-253">tooget hello **Client Id**, navigate toohello **Configure** tab of hello AAD application for hello developer portal and copy hello **Client Id**.</span></span>

<span data-ttu-id="df602-254">tooget hello **секрет клиента** щелкните hello **выберите длительность** раскрывающееся меню в hello **ключей** статьи и указать интервал.</span><span class="sxs-lookup"><span data-stu-id="df602-254">tooget hello **Client Secret** click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="df602-255">В данном примере используется интервал 1 год.</span><span class="sxs-lookup"><span data-stu-id="df602-255">In this example 1 year is used.</span></span>

![Идентификатор клиента][api-management-aad-client-id]

<span data-ttu-id="df602-257">Нажмите кнопку **Сохранить** toosave hello конфигурации и отображения hello ключ.</span><span class="sxs-lookup"><span data-stu-id="df602-257">Click **Save** toosave hello configuration and display hello key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="df602-258">Запишите этот ключ.</span><span class="sxs-lookup"><span data-stu-id="df602-258">Make a note of this key.</span></span> <span data-ttu-id="df602-259">После закрытия окна конфигурации hello Azure Active Directory hello ключ не будет отображаться в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="df602-259">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="df602-260">Hello ключа toohello Копировать буфер, портал издателя задней toohello коммутатора, вставьте ключ hello в hello **секрет клиента** в текстовое поле и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df602-260">Copy hello key toohello clipboard, switch back toohello publisher portal, paste hello key into hello **Client Secret** textbox, and click **Save**.</span></span>

![Добавление сервера авторизации][api-management-add-authorization-server-3]

<span data-ttu-id="df602-262">Сразу после hello учетных данных клиента является предоставления кода авторизации.</span><span class="sxs-lookup"><span data-stu-id="df602-262">Immediately following hello client credentials is an authorization code grant.</span></span> <span data-ttu-id="df602-263">Скопируйте этот код авторизации и задней tooyour коммутатора приложения портала Azure AD разработчик страницы и вставьте предоставления авторизации hello в hello **URL-адрес ответа** , а щелкните **Сохранить** еще раз.</span><span class="sxs-lookup"><span data-stu-id="df602-263">Copy this authorization code and switch back tooyour Azure AD developer portal application configure page, and paste hello authorization grant into hello **Reply URL** field, and click **Save** again.</span></span>

![URL-адрес ответа][api-management-aad-reply-url]

<span data-ttu-id="df602-265">Hello следующим шагом является tooconfigure hello разрешения для портала разработчиков hello AAD приложения.</span><span class="sxs-lookup"><span data-stu-id="df602-265">hello next step is tooconfigure hello permissions for hello developer portal AAD application.</span></span> <span data-ttu-id="df602-266">Нажмите кнопку **разрешения приложения** и установите флажок "hello" для **читать данные каталога**.</span><span class="sxs-lookup"><span data-stu-id="df602-266">Click **Application Permissions** and check hello box for **Read directory data**.</span></span> <span data-ttu-id="df602-267">Нажмите кнопку **Сохранить** toosave это изменить и нажмите кнопку **добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="df602-267">Click **Save** toosave this change, and then click **Add application**.</span></span>

![Добавление разрешений][api-management-add-devportal-permissions]

<span data-ttu-id="df602-269">Щелкните значок поиска hello, тип **APIM** в hello начиная с выбора **APIMAADDemo**и щелкните флажок toosave hello.</span><span class="sxs-lookup"><span data-stu-id="df602-269">Click hello search icon, type **APIM** into hello Starting with box, select **APIMAADDemo**, and click hello check mark toosave.</span></span>

![Добавление разрешений][api-management-aad-add-app-permissions]

<span data-ttu-id="df602-271">Нажмите кнопку **делегированные разрешения** для **APIMAADDemo** и установите флажок "hello" для **APIMAADDemo доступа**и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df602-271">Click **Delegated Permissions** for **APIMAADDemo** and check hello box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="df602-272">Это позволяет hello разработчика приложения портала tooaccess hello серверной службы.</span><span class="sxs-lookup"><span data-stu-id="df602-272">This allows hello developer portal application tooaccess hello backend service.</span></span>

![Добавление разрешений][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a><span data-ttu-id="df602-274">Включение авторизации пользователя OAuth 2.0 для hello калькулятора API</span><span class="sxs-lookup"><span data-stu-id="df602-274">Enable OAuth 2.0 user authorization for hello Calculator API</span></span>
<span data-ttu-id="df602-275">Теперь, когда hello OAuth 2.0 сервер настроен, можно указать его в hello параметры безопасности для API.</span><span class="sxs-lookup"><span data-stu-id="df602-275">Now that hello OAuth 2.0 server is configured, you can specify it in hello security settings for your API.</span></span> <span data-ttu-id="df602-276">Здесь демонстрируется hello видео, начиная с 14:30.</span><span class="sxs-lookup"><span data-stu-id="df602-276">This step is demonstrated in hello video starting at 14:30.</span></span>

<span data-ttu-id="df602-277">Нажмите кнопку **API-интерфейсы** в hello в левом меню и нажмите кнопку **калькулятора** tooview и настроить его параметры.</span><span class="sxs-lookup"><span data-stu-id="df602-277">Click **APIs** in hello left menu, and click  **Calculator** tooview and configure its settings.</span></span>

![API «Калькулятор»][api-management-calc-api]

<span data-ttu-id="df602-279">Перейдите toohello **безопасности** проверьте hello **OAuth 2.0** флажок, выберите hello требуемой авторизации сервера из hello **сервер авторизации** раскрывающегося списка и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df602-279">Navigate toohello **Security** tab, check hello **OAuth 2.0** checkbox, select hello desired authorization server from hello **Authorization server** drop-down, and click **Save**.</span></span>

![API «Калькулятор»][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a><span data-ttu-id="df602-281">Успешно вызовите hello API калькулятора с портала разработчиков hello</span><span class="sxs-lookup"><span data-stu-id="df602-281">Successfully call hello Calculator API from hello developer portal</span></span>
<span data-ttu-id="df602-282">Теперь, когда на hello API настроено авторизации hello OAuth 2.0, из центра разработчиков hello его операции могут вызываться успешно.</span><span class="sxs-lookup"><span data-stu-id="df602-282">Now that hello OAuth 2.0 authorization is configured on hello API, its operations can be successfully called from hello developer center.</span></span> <span data-ttu-id="df602-283">Здесь демонстрируется hello видео, начиная с 15:00.</span><span class="sxs-lookup"><span data-stu-id="df602-283">THis step is demonstrated in hello video starting at 15:00.</span></span>

<span data-ttu-id="df602-284">Перейдите назад toohello **добавьте два целых числа** операции службы калькулятора hello в портал разработчиков hello и нажмите кнопку **опробовать**.</span><span class="sxs-lookup"><span data-stu-id="df602-284">Navigate back toohello **Add two integers** operation of hello calculator service in hello developer portal and click **Try it**.</span></span> <span data-ttu-id="df602-285">Примечание hello новый элемент в hello **авторизации** соответствующий сервер авторизации toohello, только что добавленные статьи.</span><span class="sxs-lookup"><span data-stu-id="df602-285">Note hello new item in hello **Authorization** section corresponding toohello authorization server you just added.</span></span>

![API «Калькулятор»][api-management-calc-authorization-server]

<span data-ttu-id="df602-287">Выберите **код авторизации** из авторизации hello раскрывающемся списке и введите учетные данные учетной записи toouse hello hello.</span><span class="sxs-lookup"><span data-stu-id="df602-287">Select **Authorization code** from hello authorization drop-down list and enter hello credentials of hello account toouse.</span></span> <span data-ttu-id="df602-288">Если вы уже вошли в учетную запись hello не потребуется.</span><span class="sxs-lookup"><span data-stu-id="df602-288">If you are already signed in with hello account you may not be prompted.</span></span>

![API «Калькулятор»][api-management-devportal-authorization-code]

<span data-ttu-id="df602-290">Нажмите кнопку **отправки** и Примечание hello **состояние ответа** из **200 ОК** и hello результатов операции hello в ответ содержимого hello.</span><span class="sxs-lookup"><span data-stu-id="df602-290">Click **Send** and note hello **Response status** of **200 OK** and hello results of hello operation in hello response content.</span></span>

![API «Калькулятор»][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a><span data-ttu-id="df602-292">Настройка типа hello toocall классического приложения API</span><span class="sxs-lookup"><span data-stu-id="df602-292">Configure a desktop application toocall hello API</span></span>
<span data-ttu-id="df602-293">Hello Далее процедура hello видео начинается с 16:30 и настраивает hello toocall простое классическое приложение API.</span><span class="sxs-lookup"><span data-stu-id="df602-293">hello next procedure in hello video starts at 16:30 and configures a simple desktop application toocall hello API.</span></span> <span data-ttu-id="df602-294">Первым шагом Hello — tooregister hello классическое приложение в Azure AD и присвойте ему доступа toohello каталога и toohello серверной службы.</span><span class="sxs-lookup"><span data-stu-id="df602-294">hello first step is tooregister hello desktop application in Azure AD and give it access toohello directory and toohello backend service.</span></span> <span data-ttu-id="df602-295">В 18:25 отсутствует Демонстрация классического приложения hello вызова операции калькулятора hello API.</span><span class="sxs-lookup"><span data-stu-id="df602-295">At 18:25 there is a demonstration of hello desktop application calling an operation on hello calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a><span data-ttu-id="df602-296">Настройка политики toopre JWT проверки-авторизации запросов</span><span class="sxs-lookup"><span data-stu-id="df602-296">Configure a JWT validation policy toopre-authorize requests</span></span>
<span data-ttu-id="df602-297">Hello заключительную процедуру в видео hello начинается с 20:48 и показано, как toouse hello [проверка JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) toopre политики-авторизации запросов путем проверки hello токены доступа для каждого входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="df602-297">hello final procedure in hello video starts at 20:48 and shows you how toouse hello [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy toopre-authorize requests by validating hello access tokens of each incoming request.</span></span> <span data-ttu-id="df602-298">Если запрос hello не проверяется по hello политики проверки JWT, запрос hello заблокирован управления API и не будут передаваться toohello серверной части.</span><span class="sxs-lookup"><span data-stu-id="df602-298">If hello request is not validated by hello Validate JWT policy, hello request is blocked by API Management and is not passed along toohello backend.</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

<span data-ttu-id="df602-299">Другой демонстрации настройки и использования этой политики см. [177 серии охватывают облачные: более функции API-Интерфейсов управления](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too13:50 Перемотка вперед.</span><span class="sxs-lookup"><span data-stu-id="df602-299">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="df602-300">Перемотка вперед too15:00 toosee hello политики, настроенные в редакторе hello политики и затем too18:50 демонстрацию вызова операции из портала разработчиков hello как с и без hello требуется маркер авторизации.</span><span class="sxs-lookup"><span data-stu-id="df602-300">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df602-301">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df602-301">Next steps</span></span>
* <span data-ttu-id="df602-302">См. другие [видео](https://azure.microsoft.com/documentation/videos/index/?services=api-management) об управлении API.</span><span class="sxs-lookup"><span data-stu-id="df602-302">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="df602-303">Для других способов toosecure безопасности внутренней службы. в разделе [взаимной проверки подлинности сертификатов](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="df602-303">For other ways toosecure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
