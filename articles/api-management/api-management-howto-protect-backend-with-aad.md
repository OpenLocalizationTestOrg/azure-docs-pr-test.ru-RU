---
title: "Защита серверной части веб-API с помощью Azure Active Directory и службы управления API | Документация Майкрософт"
description: "Информация о защите внутренней службы веб-API с помощью Azure Active Directory и управления API"
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
ms.openlocfilehash: 0dfb4102904c2e972e6617fd3851fb1c50147357
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-protect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="dd5bd-103">Защита внутренней службы веб-API с помощью Azure Active Directory и управления API</span><span class="sxs-lookup"><span data-stu-id="dd5bd-103">How to protect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="dd5bd-104">На следующих видео показано, как собрать внутреннюю службу веб-API и защитить ее, используя протокол OAuth 2.0 с Azure Active Directory и управлением API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-104">The following video shows how to build a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="dd5bd-105">Эта статья содержит обзор инструкций на видео и дополнительные сведения к ним.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-105">This article provides an overview and additional information for the steps in the video.</span></span> <span data-ttu-id="dd5bd-106">Посмотрев этот 24-минутный ролик, вы познакомитесь со следующими темами.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="dd5bd-107">Создание серверной части веб-API и обеспечение ее безопасности при помощи AAD ― с 1:30</span><span class="sxs-lookup"><span data-stu-id="dd5bd-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="dd5bd-108">Импорт API в управление API ― с 7:10</span><span class="sxs-lookup"><span data-stu-id="dd5bd-108">Import the API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="dd5bd-109">Настройка портала разработчика на вызов API ― с 9:09</span><span class="sxs-lookup"><span data-stu-id="dd5bd-109">Configure the Developer portal to call the API - starting at 9:09</span></span>
* <span data-ttu-id="dd5bd-110">Настройка классического приложения для вызова API ― с 18:08</span><span class="sxs-lookup"><span data-stu-id="dd5bd-110">Configure a desktop application to call the API - starting at 18:08</span></span>
* <span data-ttu-id="dd5bd-111">Настройка политики проверки JWT для предварительной авторизации запросов ― с 20:47</span><span class="sxs-lookup"><span data-stu-id="dd5bd-111">Configure a JWT validation policy to pre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="dd5bd-112">Создание каталога Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd5bd-112">Create an Azure AD directory</span></span>
<span data-ttu-id="dd5bd-113">Для защиты внутренней службы веб-API с помощью Azure Active Directory сначала необходимо установить клиент AAD.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-113">To secure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="dd5bd-114">В этом видеоролике используется клиент с именем **APIMDemo** .</span><span class="sxs-lookup"><span data-stu-id="dd5bd-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="dd5bd-115">Чтобы создать клиент AAD, войдите на [классический портал Azure](https://manage.windowsazure.com) и нажмите кнопку **Создать**->**Службы приложений**->**Active Directory**->**Каталог**->**Настраиваемое создание**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-115">To create an AAD tenant, sign-in to the [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="dd5bd-117">В этом примере каталог с именем **APIMDemo** создается в домене по умолчанию с именем **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="dd5bd-118">Этот каталог используется в видео.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-118">This directory is used throughout the video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="dd5bd-120">Создание службы веб-API, защищенной с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd5bd-120">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="dd5bd-121">На этом шаге создается внутренняя служба веб-API с помощью Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-121">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="dd5bd-122">Этот шаг начинается на видео с отметки времени 1:30.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-122">This step of the video starts at 1:30.</span></span> <span data-ttu-id="dd5bd-123">Для создания проекта внутренней службы веб-API в Visual Studio выберите **Файл**->**Создать**->**Проект** и в списке **веб**-шаблонов выберите **Веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-123">To create Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from the **Web** templates list.</span></span> <span data-ttu-id="dd5bd-124">В этом видео проекту присвоено имя **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-124">In this video the project is named **APIMAADDemo**.</span></span> <span data-ttu-id="dd5bd-125">Нажмите кнопку **ОК** , чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-125">Click **OK** to create the project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="dd5bd-127">Чтобы создать проект веб-API, в списке **Выбор шаблона** выберите **Веб-API**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-127">Click **Web API** from the **Select a template list** to create a Web API project.</span></span> <span data-ttu-id="dd5bd-128">Чтобы настроить проверку подлинности Azure Active Directory, щелкните **Изменить проверку подлинности**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-128">To configure Azure Directory Authentication click **Change Authentication**.</span></span>

![Новый проект][api-management-new-project]

<span data-ttu-id="dd5bd-130">Выберите **Учетные записи организации** и укажите **домен** клиента AAD.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-130">Click **Organizational Accounts**, and specify the **Domain** of your AAD tenant.</span></span> <span data-ttu-id="dd5bd-131">В этом примере используется домен **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-131">In this example the domain is **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="dd5bd-132">Домен каталога можно найти на вкладке **Домены** вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-132">The domain of your directory can be obtained from the **Domains** tab of your directory.</span></span>

![Домены][api-management-aad-domains]

<span data-ttu-id="dd5bd-134">Настройте нужные параметры в диалоговом окне **Изменить способ проверки подлинности** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-134">Configure the desired settings in the **Change Authentication** dialog box and click **OK**.</span></span>

![Изменить проверку подлинности][api-management-change-authentication]

<span data-ttu-id="dd5bd-136">После того как вы нажмете кнопку **ОК** , Visual Studio попытается зарегистрировать приложение с каталогом Azure AD, и вам будет предложено войти в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-136">When you click **OK** Visual Studio will attempt to register your application with your Azure AD directory and you may be prompted to sign in by Visual Studio.</span></span> <span data-ttu-id="dd5bd-137">Войдите с помощью учетной записи администратора вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-137">Sign in using an administrative account for your directory.</span></span>

![Вход в Visual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="dd5bd-139">Чтобы настроить этот проект как веб-API Azure, установите флажок рядом с параметром **Разместить в облаке** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-139">To configure this project as an Azure Web API check the box for **Host in the cloud** and then click **OK**.</span></span>

![Новый проект][api-management-new-project-cloud]

<span data-ttu-id="dd5bd-141">Может появиться запрос на вход в Azure, после входа вы сможете настроить веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-141">You may be prompted to sign in to Azure, and then you can configure the Web App.</span></span>

![Настройка][api-management-configure-web-app]

<span data-ttu-id="dd5bd-143">В этом примере создается новый **план службы приложений** с именем **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-143">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="dd5bd-144">Нажмите кнопку **ОК** , чтобы настроить веб-приложение и создать проект.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-144">Click **OK** to configure the Web App and create the project.</span></span>

## <a name="add-the-code-to-the-web-api-project"></a><span data-ttu-id="dd5bd-145">Добавление кода в проект веб-API</span><span class="sxs-lookup"><span data-stu-id="dd5bd-145">Add the code to the Web API project</span></span>
<span data-ttu-id="dd5bd-146">На следующем шаге в видео добавляется код в проект веб-API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-146">The next step in the video adds the code to the Web API project.</span></span> <span data-ttu-id="dd5bd-147">Этот шаг начинается с отметки времени 4:35.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-147">This step starts at 4:35.</span></span>

<span data-ttu-id="dd5bd-148">Веб-API в этом примере реализует простую службу «Калькулятор» с помощью модели и контроллера.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-148">The Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="dd5bd-149">Чтобы добавить модель в службу, щелкните правой кнопкой мыши **Модели** в **обозревателе решений** и выберите **Добавить**, **Класс**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-149">To add the model for the service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="dd5bd-150">Присвойте классу имя `CalcInput` и нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-150">Name the class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="dd5bd-151">Добавьте следующий оператор `using` в верхнюю часть файла `CalcInput.cs`:</span><span class="sxs-lookup"><span data-stu-id="dd5bd-151">Add the following `using` statement to the top of the `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="dd5bd-152">Замените созданный класс следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="dd5bd-152">Replace the generated class with the following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="dd5bd-153">Щелкните правой кнопкой мыши **Контроллеры** в **обозревателе решений** и выберите **Добавить**->**Контроллер**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-153">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="dd5bd-154">Выберите элемент **Контроллер Web API 2 – пустой** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-154">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="dd5bd-155">Введите имя контроллера **CalcController** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-155">Type **CalcController** for the Controller name and click **Add**.</span></span>

![Добавление контролера][api-management-add-controller]

<span data-ttu-id="dd5bd-157">Добавьте следующий оператор `using` в верхнюю часть файла `CalcController.cs`:</span><span class="sxs-lookup"><span data-stu-id="dd5bd-157">Add the following `using` statement to the top of the `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="dd5bd-158">Замените созданный контроллер следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="dd5bd-158">Replace the generated controller class with the following code.</span></span> <span data-ttu-id="dd5bd-159">Этот код реализует операции `Add`, `Subtract`, `Multiply` и `Divide` простого API «Калькулятор».</span><span class="sxs-lookup"><span data-stu-id="dd5bd-159">This code implements the `Add`, `Subtract`, `Multiply`, and `Divide` operations of the Basic Calculator API.</span></span>

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

<span data-ttu-id="dd5bd-160">Нажмите клавишу **F6** , чтобы построить и проверить решение.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-160">Press **F6** to build and verify the solution.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="dd5bd-161">Публикация проекта в Azure</span><span class="sxs-lookup"><span data-stu-id="dd5bd-161">Publish the project to Azure</span></span>
<span data-ttu-id="dd5bd-162">На этом этапе проект Visual Studio публикуется в Azure.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-162">In this step the Visual Studio project is published to Azure.</span></span> <span data-ttu-id="dd5bd-163">Этот шаг начинается на видео с отметки времени 5:45.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-163">This step of the video starts at 5:45.</span></span>

<span data-ttu-id="dd5bd-164">Чтобы опубликовать проект в Azure, щелкните правой кнопкой мыши проект **APIMAADDemo** в Visual Studio и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-164">To publish the project to Azure, right-click the **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="dd5bd-165">Сохраните параметры по умолчанию в диалоговом окне **веб-публикации** и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-165">Keep the default settings in the **Publish Web** dialog box and click **Publish**.</span></span>

![Веб-публикация][api-management-web-publish]

## <a name="grant-permissions-to-the-azure-ad-backend-service-application"></a><span data-ttu-id="dd5bd-167">Предоставление разрешений для приложения внутренней службы Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd5bd-167">Grant permissions to the Azure AD backend service application</span></span>
<span data-ttu-id="dd5bd-168">Новое приложение для внутренней службы создается в каталоге Azure AD как часть процесса настройки и публикации проекта веб-API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-168">A new application for the backend service is created in your Azure AD directory as part of the configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="dd5bd-169">На этом шаге видео, который начинается с отметки времени 6:13, разрешения предоставляются для внутренней службы веб-API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-169">In this step of the video, starting at 6:13, permissions are granted to the Web API backend.</span></span>

![Приложение][api-management-aad-backend-app]

<span data-ttu-id="dd5bd-171">Щелкните имя приложения, чтобы настроить необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-171">Click the name of the application to configure the required permissions.</span></span> <span data-ttu-id="dd5bd-172">На вкладке **Настройка** прокрутите страницу вниз до раздела **Разрешения для других приложений**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-172">Navigate to the **Configure** tab and scroll down to the **permissions to other applications** section.</span></span> <span data-ttu-id="dd5bd-173">Щелкните раскрывающийся список **Разрешения приложений** рядом с **Microsoft** **Azure Active Directory**, установите флажок рядом с разрешением **Чтение данных каталога** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-173">Click the **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check the box for **Read directory data**, and click **Save**.</span></span>

![Добавление разрешений][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="dd5bd-175">Если приложение **Microsoft** **Azure Active Directory** не указано в списке разрешений для других приложений, нажмите кнопку **Добавить приложение** и добавьте его из списка.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-175">If **Windows** **Azure Active Directory** is not listed under permissions to other applications, click **Add application** and add it from the list.</span></span>
> 
> 

<span data-ttu-id="dd5bd-176">Запишите **URI идентификатора приложения** , чтобы использовать его на следующем шаге во время настройки приложения Azure AD для портала разработчика управления API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-176">Make a note of the **App Id URI** for use in a subsequent step when an Azure AD application is configured for the API Management developer portal.</span></span>

![URI идентификатора приложения][api-management-aad-sso-uri]

## <a name="import-the-web-api-into-api-management"></a><span data-ttu-id="dd5bd-178">Импорт веб-API в управление API</span><span class="sxs-lookup"><span data-stu-id="dd5bd-178">Import the Web API into API Management</span></span>
<span data-ttu-id="dd5bd-179">Интерфейсы API настраиваются на портале издателя API, который доступен на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-179">APIs are configured from the API publisher portal, which is accessed through the Azure Portal.</span></span> <span data-ttu-id="dd5bd-180">Чтобы открыть его, щелкните **Publisher portal** (Портал издателя) на панели инструментов своей службы управления API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-180">To reach it, click **Publisher portal** from the toolbar of your API Management service.</span></span> <span data-ttu-id="dd5bd-181">Если экземпляр службы управления API еще не создан, выполните инструкции из раздела [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Manage your first API].</span><span class="sxs-lookup"><span data-stu-id="dd5bd-181">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API][Manage your first API] tutorial.</span></span>

![Портал издателя][api-management-management-console]

<span data-ttu-id="dd5bd-183">Операции можно [добавить в API-интерфейсы вручную](api-management-howto-add-operations.md)или импортировать их.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-183">Operations can be [added to APIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="dd5bd-184">В этом видео операции импортируются в формате Swagger начиная с отметки времени 6:40.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-184">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="dd5bd-185">Создайте файл `calcapi.json` с приведенным ниже содержимым и сохраните его на компьютер.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-185">Create a file named `calcapi.json` with following contents and save it to your computer.</span></span> <span data-ttu-id="dd5bd-186">Убедитесь, что атрибут `host` указывает на серверную часть веб-API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-186">Ensure that the `host` attribute points to your Web API backend.</span></span> <span data-ttu-id="dd5bd-187">В этом примере используется `"host": "apimaaddemo.azurewebsites.net"` .</span><span class="sxs-lookup"><span data-stu-id="dd5bd-187">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

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

<span data-ttu-id="dd5bd-188">Чтобы импортировать API калькулятора, щелкните **API** в расположенном слева меню **Управление API**, а затем выберите **Импорт API**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-188">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![Кнопка импорта API][api-management-import-api]

<span data-ttu-id="dd5bd-190">Выполните следующие действия, чтобы настроить API калькулятора.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-190">Perform the following steps to configure the calculator API.</span></span>

1. <span data-ttu-id="dd5bd-191">Щелкните **Из файла**, перейдите к сохраненному файлу `calculator.json` и установите переключатель **Swagger**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-191">Click **From file**, browse to the `calculator.json` file you saved, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="dd5bd-192">В текстовом поле **Web API URL suffix** (Суффикс URL-адреса веб-API) введите **calc**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-192">Type **calc** into the **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="dd5bd-193">Щелкните в поле **Products (optional)** (Продукты (необязательно)) и выберите **Starter**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-193">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="dd5bd-194">Щелкните **Сохранить** , чтобы импортировать API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-194">Click **Save** to import the API.</span></span>

![Добавление нового API][api-management-import-new-api]

<span data-ttu-id="dd5bd-196">После импорта API на портале издателя выводится страница сводных данных для API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-196">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

## <a name="call-the-api-unsuccessfully-from-the-developer-portal"></a><span data-ttu-id="dd5bd-197">Неудавшийся вызов API с портала разработчика</span><span class="sxs-lookup"><span data-stu-id="dd5bd-197">Call the API unsuccessfully from the developer portal</span></span>
<span data-ttu-id="dd5bd-198">На этом этапе API импортирован в управление API, но его еще нельзя успешно вызвать с портала разработчика, поскольку внутренняя служба защищена с помощью проверки подлинности Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-198">At this point, the API has been imported into API Management, but cannot yet be called successfully from the developer portal because the backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="dd5bd-199">Это продемонстрировано на видео на отметке времени 7:40 следующим образом.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-199">This is demonstrated in the video starting at 7:40 using the following steps.</span></span>

<span data-ttu-id="dd5bd-200">Выберите **Портал разработчика** справа вверху на портале издателя.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-200">Click **Developer portal** from the top-right side of the publisher portal.</span></span>

![Портал разработчика][api-management-developer-portal-menu]

<span data-ttu-id="dd5bd-202">Щелкните **Интерфейсы API** и выберите API **Калькулятор**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-202">Click **APIs** and click the **Calculator** API.</span></span>

![Портал разработчика][api-management-dev-portal-apis]

<span data-ttu-id="dd5bd-204">Щелкните **Попробовать**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-204">Click **Try it**.</span></span>

![Попробовать][api-management-dev-portal-try-it]

<span data-ttu-id="dd5bd-206">Нажмите кнопку **Отправить**. Состояние ответа должно быть **401 — Не санкционировано**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-206">Click **Send** and note the response status of **401 Unauthorized**.</span></span>

![Отправка][api-management-dev-portal-send-401]

<span data-ttu-id="dd5bd-208">Запрос не авторизован, поскольку внутренняя служба API защищена службой Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-208">The request is unauthorized because the backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="dd5bd-209">Для успешного вызова API портал разработчика необходимо настроить, чтобы авторизовать разработчиков, использующих OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-209">Before successfully calling the API the developer portal must be configured to authorize developers using OAuth 2.0.</span></span> <span data-ttu-id="dd5bd-210">Этот процесс описывается в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-210">This process is described in the following sections.</span></span>

## <a name="register-the-developer-portal-as-an-aad-application"></a><span data-ttu-id="dd5bd-211">Регистрация портала разработчика как приложения AAD</span><span class="sxs-lookup"><span data-stu-id="dd5bd-211">Register the developer portal as an AAD application</span></span>
<span data-ttu-id="dd5bd-212">Чтобы настроить портал разработчика для авторизации разработчиков, использующих OAuth 2.0, сначала необходимо зарегистрировать портал разработчика как приложение AAD.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-212">The first step in configuring the developer portal to authorize developers using OAuth 2.0 is to register the developer portal as an AAD application.</span></span> <span data-ttu-id="dd5bd-213">На видео этот процесс показан с отметки времени 8:27.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-213">This is demonstrated starting at 8:27 in the video.</span></span>

<span data-ttu-id="dd5bd-214">Перейдите к клиенту Azure AD, который использовался в первом шаге этого видео (в нашем примере это клиент **APIMDemo**), и откройте вкладку **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-214">Navigate to the Azure AD tenant from the first step of this video, in this example **APIMDemo** and navigate to the **Applications** tab.</span></span>

![Новое приложение][api-management-aad-new-application-devportal]

<span data-ttu-id="dd5bd-216">Нажмите кнопку **Добавить**, чтобы создать приложение Azure Active Directory, а затем установите флажок **Добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-216">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Новое приложение][api-management-new-aad-application-menu]

<span data-ttu-id="dd5bd-218">Выберите **Веб-приложение и/или веб-API**, введите имя и нажмите стрелку «Далее».</span><span class="sxs-lookup"><span data-stu-id="dd5bd-218">Choose **Web application and/or Web API**, enter a name, and click the next arrow.</span></span> <span data-ttu-id="dd5bd-219">В этом примере используется **APIMDeveloperPortal** .</span><span class="sxs-lookup"><span data-stu-id="dd5bd-219">In this example **APIMDeveloperPortal** is used.</span></span>

![Новое приложение][api-management-aad-new-application-devportal-1]

<span data-ttu-id="dd5bd-221">В поле **URL-адрес входа** введите URL-адрес службы управления API и добавьте `/signin`.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-221">For **Sign-on URL** enter the URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="dd5bd-222">В этом примере используется `https://contoso5.portal.azure-api.net/signin` .</span><span class="sxs-lookup"><span data-stu-id="dd5bd-222">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="dd5bd-223">В поле **App Id URL** (URL-адрес идентификатора приложения) введите URL-адрес службы управления API и добавьте несколько уникальных символов.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-223">For **App Id URL** enter the URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="dd5bd-224">Это могут быть любые знаки. В данном примере используется `https://contoso5.portal.azure-api.net/dp`.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-224">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="dd5bd-225">Настроив нужные **свойства приложения**, установите флажок для создания приложения.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-225">When the  desired **App properties** are configured, click the check mark to create the application.</span></span>

![Новое приложение][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="dd5bd-227">Настройка сервера авторизации OAuth 2.0 в управлении API</span><span class="sxs-lookup"><span data-stu-id="dd5bd-227">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="dd5bd-228">На следующем шаге будет настроен сервер авторизации OAuth 2.0 в управлении API</span><span class="sxs-lookup"><span data-stu-id="dd5bd-228">The next step is to configure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="dd5bd-229">Этот шаг показан в видео начиная с отметки времени 9:43.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-229">This step is demonstrated in the video starting at 9:43.</span></span>

<span data-ttu-id="dd5bd-230">В меню "Управление API" слева выберите пункт **Безопасность**, перейдите на вкладку **OAuth 2.0** и щелкните ссылку **Add authorization server** (Добавить сервер авторизации).</span><span class="sxs-lookup"><span data-stu-id="dd5bd-230">Click **Security** from the API Management menu on the left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Добавление сервера авторизации][api-management-add-authorization-server]

<span data-ttu-id="dd5bd-232">В полях **Имя** и **Описание** введите имя и (при желании) описание.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-232">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> <span data-ttu-id="dd5bd-233">Эти поля служат для идентификации сервера авторизации OAuth 2.0 в текущем экземпляре службы управления API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-233">These fields are used to identify the OAuth 2.0 authorization server within the API Management service instance.</span></span> <span data-ttu-id="dd5bd-234">В этом примере используется **демоверсия сервера авторизации** .</span><span class="sxs-lookup"><span data-stu-id="dd5bd-234">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="dd5bd-235">Позже, когда вы укажете сервер OAuth 2.0 проверки подлинности для API, вам нужно будет выбрать это имя.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-235">Later when you specify an OAuth 2.0 server to be used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="dd5bd-236">В поле **Client registration page URL** (URL-адрес страницы регистрации клиента) введите значение заполнителя, например `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-236">For the **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="dd5bd-237">**URL-адрес страницы регистрации клиента** указывает на страницу, на которой пользователи могут создавать и настраивать собственные учетные записи для поставщиков OAuth 2.0, поддерживающих пользовательское управление учетными записями.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-237">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="dd5bd-238">В этом примере пользователи не создают и не настраивают собственные учетные записи, поэтому используется заполнитель.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-238">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Добавление сервера авторизации][api-management-add-authorization-server-1]

<span data-ttu-id="dd5bd-240">Затем укажите **URL-адрес конечной точки авторизации** и **URL-адрес конечной точки маркера**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-240">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Сервер авторизации][api-management-add-authorization-server-1a]

<span data-ttu-id="dd5bd-242">Эти значения можно получить на странице **Конечные точки приложения** для приложения AAD, которое вы создали для портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-242">These values can be retrieved from the **App Endpoints** page of the AAD application you created for the developer portal.</span></span> <span data-ttu-id="dd5bd-243">Для доступа к конечным точкам откройте вкладку **Настройка** приложения AAD и нажмите кнопку **Просмотр конечных точек**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-243">To access the endpoints navigate to the **Configure** tab for the AAD application and click **View endpoints**.</span></span>

![Приложение][api-management-aad-devportal-application]

![Просмотреть конечные точки][api-management-aad-view-endpoints]

<span data-ttu-id="dd5bd-246">Скопируйте значение **Конечная точка авторизации OAuth 2.0** и вставьте его в текстовое поле **Authorization endpoint URL** (URL-адрес конечной точки авторизации).</span><span class="sxs-lookup"><span data-stu-id="dd5bd-246">Copy the **OAuth 2.0 authorization endpoint** and paste it into the **Authorization endpoint URL** textbox.</span></span>

![Добавление сервера авторизации][api-management-add-authorization-server-2]

<span data-ttu-id="dd5bd-248">Скопируйте значение **Конечная точка маркера OAuth 2.0** и вставьте его в текстовое поле **Token endpoint URL** (URL-адрес конечной точки маркера).</span><span class="sxs-lookup"><span data-stu-id="dd5bd-248">Copy the **OAuth 2.0 token endpoint** and paste it into the **Token endpoint URL** textbox.</span></span>

![Добавление сервера авторизации][api-management-add-authorization-server-2a]

<span data-ttu-id="dd5bd-250">После вставки конечной точки маркера добавьте дополнительный параметр текста с именем **resource**, для которого в качестве значения используйте **URI идентификатора приложения** из приложения AAD для внутренней службы, которая была создана во время публикации проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-250">In addition to pasting in the token endpoint, add an additional body parameter named **resource** and for the value use the **App Id URI** from the AAD application for the backend service that was created when the Visual Studio project was published.</span></span>

![URI идентификатора приложения][api-management-aad-sso-uri]

<span data-ttu-id="dd5bd-252">Затем укажите учетные данные клиента.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-252">Next, specify the client credentials.</span></span> <span data-ttu-id="dd5bd-253">Это учетные данные для ресурса, к которому требуется доступ. В данном случае этим ресурсом является портал разработчика.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-253">These are the credentials for the resource you want to access, in this case the developer portal.</span></span>

![Учетные данные клиента][api-management-client-credentials]

<span data-ttu-id="dd5bd-255">Чтобы получить **идентификатор клиента**, перейдите на вкладку **Настройка** приложения AAD для портала разработчика и скопируйте **идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-255">To get the **Client Id**, navigate to the **Configure** tab of the AAD application for the developer portal and copy the **Client Id**.</span></span>

<span data-ttu-id="dd5bd-256">Чтобы получить **секрет клиента**, щелкните раскрывающийся список **Выбрать длительность** в разделе **Ключи** и укажите интервал.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-256">To get the **Client Secret** click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="dd5bd-257">В данном примере используется интервал 1 год.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-257">In this example 1 year is used.</span></span>

![идентификатор клиента][api-management-aad-client-id]

<span data-ttu-id="dd5bd-259">Нажмите кнопку **Сохранить** , чтобы сохранить конфигурацию и отобразить ключ.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-259">Click **Save** to save the configuration and display the key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="dd5bd-260">Запишите этот ключ.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-260">Make a note of this key.</span></span> <span data-ttu-id="dd5bd-261">После закрытия окна конфигурации Azure Active Directory нельзя будет снова отобразить ключ.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-261">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="dd5bd-262">Скопируйте ключ в буфер обмена, вернитесь на портал издателя, вставьте ключ в текстовое поле **Секрет клиента** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-262">Copy the key to the clipboard, switch back to the publisher portal, paste the key into the **Client Secret** textbox, and click **Save**.</span></span>

![Добавление сервера авторизации][api-management-add-authorization-server-3]

<span data-ttu-id="dd5bd-264">Сразу после указания учетных данных клиента необходимо предоставить код авторизации.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-264">Immediately following the client credentials is an authorization code grant.</span></span> <span data-ttu-id="dd5bd-265">Скопируйте этот код авторизации и вернитесь в приложение портала разработчика Azure AD. Вставьте код авторизации в поле **URL-адрес ответа** и нажмите кнопку **Сохранить** еще раз.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-265">Copy this authorization code and switch back to your Azure AD developer portal application configure page, and paste the authorization grant into the **Reply URL** field, and click **Save** again.</span></span>

![URL-адрес ответа][api-management-aad-reply-url]

<span data-ttu-id="dd5bd-267">Следующим шагом является настройка разрешений для приложения портала разработчика AAD.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-267">The next step is to configure the permissions for the developer portal AAD application.</span></span> <span data-ttu-id="dd5bd-268">Щелкните **Разрешения приложения** и установите флажок для параметра **Чтение данных каталога**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-268">Click **Application Permissions** and check the box for **Read directory data**.</span></span> <span data-ttu-id="dd5bd-269">Нажмите кнопку **Сохранить**, чтобы сохранить это изменение, а затем нажмите кнопку **Добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-269">Click **Save** to save this change, and then click **Add application**.</span></span>

![Добавление разрешений][api-management-add-devportal-permissions]

<span data-ttu-id="dd5bd-271">Щелкните значок поиска, введите **APIM** в поле "Начинается с", выберите **APIMAADDemo** и щелкните значок флажка, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-271">Click the search icon, type **APIM** into the Starting with box, select **APIMAADDemo**, and click the check mark to save.</span></span>

![Добавление разрешений][api-management-aad-add-app-permissions]

<span data-ttu-id="dd5bd-273">Щелкните **Делегированные разрешения** для **APIMAADDemo** и установите флажок рядом с параметром **Доступ APIMAADDemo**. Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-273">Click **Delegated Permissions** for **APIMAADDemo** and check the box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="dd5bd-274">Теперь приложение портала разработчика имеет доступ к внутренней службе.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-274">This allows the developer portal application to access the backend service.</span></span>

![Добавление разрешений][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-the-calculator-api"></a><span data-ttu-id="dd5bd-276">Включение авторизации пользователей OAuth 2.0 для API «Калькулятор».</span><span class="sxs-lookup"><span data-stu-id="dd5bd-276">Enable OAuth 2.0 user authorization for the Calculator API</span></span>
<span data-ttu-id="dd5bd-277">Теперь, когда сервер OAuth 2.0 настроен, можно указать его параметры безопасности для API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-277">Now that the OAuth 2.0 server is configured, you can specify it in the security settings for your API.</span></span> <span data-ttu-id="dd5bd-278">Этот шаг показан в видео начиная с отметки времени 14:30.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-278">This step is demonstrated in the video starting at 14:30.</span></span>

<span data-ttu-id="dd5bd-279">Выберите пункт **Интерфейсы API** в меню слева и щелкните **Калькулятор**, чтобы просмотреть и настроить соответствующие параметры.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-279">Click **APIs** in the left menu, and click  **Calculator** to view and configure its settings.</span></span>

![API «Калькулятор»][api-management-calc-api]

<span data-ttu-id="dd5bd-281">Откройте вкладку **Безопасность**, установите флажок **OAuth 2.0**, выберите нужный сервер авторизации в раскрывающемся списке **Сервер авторизации** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-281">Navigate to the **Security** tab, check the **OAuth 2.0** checkbox, select the desired authorization server from the **Authorization server** drop-down, and click **Save**.</span></span>

![API «Калькулятор»][api-management-enable-aad-calculator]

## <a name="successfully-call-the-calculator-api-from-the-developer-portal"></a><span data-ttu-id="dd5bd-283">Успешный вызов API «Калькулятор» с портала разработчика</span><span class="sxs-lookup"><span data-stu-id="dd5bd-283">Successfully call the Calculator API from the developer portal</span></span>
<span data-ttu-id="dd5bd-284">Теперь, когда для API-интерфейса настроена авторизация OAuth 2.0, из центра разработчика можно успешно вызывать его операции.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-284">Now that the OAuth 2.0 authorization is configured on the API, its operations can be successfully called from the developer center.</span></span> <span data-ttu-id="dd5bd-285">Этот шаг показан в видео начиная с отметки времени 15:00.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-285">THis step is demonstrated in the video starting at 15:00.</span></span>

<span data-ttu-id="dd5bd-286">На портале разработчика вернитесь к операции **Добавление двух целых** службы "Калькулятор" и нажмите кнопку **Попробовать**.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-286">Navigate back to the **Add two integers** operation of the calculator service in the developer portal and click **Try it**.</span></span> <span data-ttu-id="dd5bd-287">Обратите внимание на новый элемент в разделе **Авторизация** , который соответствует только что добавленному серверу авторизации.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-287">Note the new item in the **Authorization** section corresponding to the authorization server you just added.</span></span>

![API «Калькулятор»][api-management-calc-authorization-server]

<span data-ttu-id="dd5bd-289">Выберите **Код авторизации** из раскрывающегося списка и введите данные учетной записи, которую будете использовать.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-289">Select **Authorization code** from the authorization drop-down list and enter the credentials of the account to use.</span></span> <span data-ttu-id="dd5bd-290">Если вы уже вошли с помощью учетной записи, запрос на ввод учетных данных не появится.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-290">If you are already signed in with the account you may not be prompted.</span></span>

![API «Калькулятор»][api-management-devportal-authorization-code]

<span data-ttu-id="dd5bd-292">Нажмите кнопку **Отправить**. **Состояние ответа** должно быть **200 ОК**. Кроме того, примите к сведению результаты операции в содержимом ответа.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-292">Click **Send** and note the **Response status** of **200 OK** and the results of the operation in the response content.</span></span>

![API «Калькулятор»][api-management-devportal-response]

## <a name="configure-a-desktop-application-to-call-the-api"></a><span data-ttu-id="dd5bd-294">Настройка классического приложения для вызова API</span><span class="sxs-lookup"><span data-stu-id="dd5bd-294">Configure a desktop application to call the API</span></span>
<span data-ttu-id="dd5bd-295">Следующая процедура на видео начинается с отметки времени 16:30. Она настраивает простое классическое приложение для вызова API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-295">The next procedure in the video starts at 16:30 and configures a simple desktop application to call the API.</span></span> <span data-ttu-id="dd5bd-296">Первым шагом является регистрация классического приложения в Azure AD и предоставление ему доступа к каталогу и внутренней службе.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-296">The first step is to register the desktop application in Azure AD and give it access to the directory and to the backend service.</span></span> <span data-ttu-id="dd5bd-297">Начиная с отметки времени 18:25 видео, можно увидеть, как классическое приложение вызывает операцию API «Калькулятор».</span><span class="sxs-lookup"><span data-stu-id="dd5bd-297">At 18:25 there is a demonstration of the desktop application calling an operation on the calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-to-pre-authorize-requests"></a><span data-ttu-id="dd5bd-298">Настройка политики проверки JWT для запросов предварительной авторизации</span><span class="sxs-lookup"><span data-stu-id="dd5bd-298">Configure a JWT validation policy to pre-authorize requests</span></span>
<span data-ttu-id="dd5bd-299">Последняя процедура в видеоролике начинается с отметки 20:48. В ней показано, как использовать политику [Проверка JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) для предварительной авторизации запросов путем проверки маркеров доступа каждого входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-299">The final procedure in the video starts at 20:48 and shows you how to use the [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy to pre-authorize requests by validating the access tokens of each incoming request.</span></span> <span data-ttu-id="dd5bd-300">Если запрос не прошел проверку JWT, он блокируется управлением API и не передается во внутреннюю службу.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-300">If the request is not validated by the Validate JWT policy, the request is blocked by API Management and is not passed along to the backend.</span></span>

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

<span data-ttu-id="dd5bd-301">Другой пример настройки и использования этой политики см. в видео [Облачное покрытие, эпизод 177: другие функции управления API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) с отметки времени 13:50.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-301">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="dd5bd-302">Перемотайте вперед до отметки времени 15:00, чтобы просмотреть политики, настроенные в редакторе политик, и до 18:50, чтобы просмотреть демонстрацию вызова операции с портала разработчика с обязательным маркером авторизации и без него.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-302">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd5bd-303">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd5bd-303">Next steps</span></span>
* <span data-ttu-id="dd5bd-304">См. другие [видео](https://azure.microsoft.com/documentation/videos/index/?services=api-management) об управлении API.</span><span class="sxs-lookup"><span data-stu-id="dd5bd-304">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="dd5bd-305">Другие способы защиты внутренней службы см. в разделе [Взаимная аутентификация на основе сертификатов](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="dd5bd-305">For other ways to secure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

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
