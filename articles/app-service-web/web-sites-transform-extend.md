---
title: "Дополнительные настройки и расширения веб-приложений службы приложений Azure"
description: "Используйте объявления преобразования XML-документов (XDT), чтобы преобразовать файл ApplicationHost.config в веб-приложении службы приложений Azure и добавить частные расширения. Это позволит выполнять дополнительные действия по администрированию."
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: 
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: 314d3a954e712b829e7cf5eb37b23b31670f976b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="bc87d-103">Дополнительные настройки и расширения веб-приложений службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="bc87d-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="bc87d-104">С помощью объявлений [преобразования документов XML](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) вы можете преобразовать файл [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) в веб-приложении в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="bc87d-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform the [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="bc87d-105">Объявления XDT можно также использовать для добавления частных расширений, которые обеспечивают пользовательские действия администрирования веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="bc87d-105">You can also use XDT declarations to add private extensions to enable custom web app administration actions.</span></span> <span data-ttu-id="bc87d-106">Статья содержит пример расширения для веб-приложения диспетчера PHP, позволяющего управлять параметрами PHP через веб-интерфейс.</span><span class="sxs-lookup"><span data-stu-id="bc87d-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="bc87d-107"><a id="transform"></a>Дополнительные настройки посредством ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="bc87d-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="bc87d-108">Платформа службы приложений представляет собой гибкое решение для управления настройками веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bc87d-108">The App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="bc87d-109">Хотя стандартный файл конфигурации IIS ApplicationHost.config недоступен для непосредственного редактирования в службе приложений, платформа поддерживает декларативную модель преобразования ApplicationHost.config, основанную на преобразовании XML-документа (XDT).</span><span class="sxs-lookup"><span data-stu-id="bc87d-109">Although the standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, the platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="bc87d-110">Чтобы использовать эту возможность преобразования, создайте файл ApplicationHost.xdt с содержимым XDT и поместите его в корневой каталог сайта (d:\home\site) в [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="bc87d-110">To leverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under the site root (d:\home\site) in the [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="bc87d-111">Возможно, вам понадобится перезапустить веб-приложение, чтобы изменения вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="bc87d-111">You may need to restart the Web App for changes to take effect.</span></span>

<span data-ttu-id="bc87d-112">В приведенном ниже примере с файлом applicationHost.xdt показано, как добавить новую пользовательскую переменную среды для веб-приложения, использующего PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="bc87d-112">The following applicationHost.xdt sample shows how to add a new custom environment variable to a web app that uses PHP 5.4.</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <fastCgi>
      <application>
        <environmentVariables>
          <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
        </environmentVariables>
      </application>
    </fastCgi>
  </system.webServer>
</configuration>
```

<span data-ttu-id="bc87d-113">Файл журнала с состоянием преобразования и соответствующими сведениями находится в папке LogFiles\Transform корневого каталога FTP.</span><span class="sxs-lookup"><span data-stu-id="bc87d-113">A log file with transform status and details is available from the FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="bc87d-114">Дополнительные примеры см. на странице [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="bc87d-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="bc87d-115">**Примечание.**</span><span class="sxs-lookup"><span data-stu-id="bc87d-115">**Note**</span></span><br />
<span data-ttu-id="bc87d-116">Элементы из списка модулей в `system.webServer` нельзя удалить или переупорядочить, однако можно добавлять элементы в этот список.</span><span class="sxs-lookup"><span data-stu-id="bc87d-116">Elements from the list of modules under `system.webServer` cannot be removed or reordered, but additions to the list are possible.</span></span>

## <span data-ttu-id="bc87d-117"><a id="extend"></a> Расширения для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="bc87d-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="bc87d-118"><a id="overview"></a> Обзор частных расширений для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="bc87d-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="bc87d-119">Служба приложений дает возможность использовать расширения веб-приложений для выполнения дополнительных действий по администрированию.</span><span class="sxs-lookup"><span data-stu-id="bc87d-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="bc87d-120">Некоторые функции платформы службы приложений реализованы в виде предустановленных расширений.</span><span class="sxs-lookup"><span data-stu-id="bc87d-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="bc87d-121">Предварительно установленные расширения платформы невозможно изменить, но вы можете создать и настроить частные расширения для своего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bc87d-121">While the pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="bc87d-122">Эта функциональная возможность основана на объявлениях XDT.</span><span class="sxs-lookup"><span data-stu-id="bc87d-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="bc87d-123">Вот основные шаги по созданию частного расширения веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bc87d-123">The key steps for creating a private web app extension are the following:</span></span>

1. <span data-ttu-id="bc87d-124">**Содержимое**расширения веб-приложения: создайте приложение, поддерживаемое службой приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="bc87d-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="bc87d-125">**Объявление**расширения веб-приложения: создайте файл ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="bc87d-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="bc87d-126">**Развертывание** расширения веб-приложения: разместите содержимое в папке SiteExtensions в каталоге `root`.</span><span class="sxs-lookup"><span data-stu-id="bc87d-126">Web app extension **deployment**: place content in the SiteExtensions folder under `root`</span></span>

<span data-ttu-id="bc87d-127">Внутренние ссылки веб-приложения должны указывать на путь, связанный с указанным в файле ApplicationHost.xdt путем приложения.</span><span class="sxs-lookup"><span data-stu-id="bc87d-127">Internal links for the web app should point to a path relative to the application path specified in the ApplicationHost.xdt file.</span></span> <span data-ttu-id="bc87d-128">При внесении любых изменений в файл ApplicationHost.xdt требуется перезапуск веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bc87d-128">Any change to the ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="bc87d-129">**Примечание**. Дополнительные сведения об этих ключевых элементах см. на странице [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="bc87d-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="bc87d-130">Ниже приводится подробный пример создания и активации частного расширения веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bc87d-130">A detailed example is included to illustrate the steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="bc87d-131">Исходный код для следующего примера диспетчера PHP можно загрузить по адресу [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="bc87d-131">The source code for the PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="bc87d-132"><a id="SiteSample"></a> Пример расширения сайта веб-приложения: диспетчер PHP</span><span class="sxs-lookup"><span data-stu-id="bc87d-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="bc87d-133">Диспетчер PHP является расширением веб-приложения, позволяющим администраторам сайтов без усилий просматривать и настраивать параметры PHP с помощью веб-интерфейса вместо непосредственного редактирования INI-файлов PHP.</span><span class="sxs-lookup"><span data-stu-id="bc87d-133">PHP Manager is a web app extension that allows web app administrators to easily view and configure their PHP settings using a web interface instead of having to modify PHP .ini files directly.</span></span> <span data-ttu-id="bc87d-134">К общими файлам конфигурации PHP относится файл php.ini, расположенный в папке с программными файлами, и файл .user.ini, расположенный в корневой папке веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bc87d-134">Common configuration files for PHP include the php.ini file located under Program Files and the .user.ini file located in the root folder of your web app.</span></span> <span data-ttu-id="bc87d-135">Поскольку файл php.ini нельзя напрямую редактировать в службе приложений Azure, расширение диспетчера PHP использует для внесения изменений файл .user.ini.</span><span class="sxs-lookup"><span data-stu-id="bc87d-135">Since the php.ini file is not directly editable on the App Service platform, the PHP Manager extension uses the .user.ini file to apply setting changes.</span></span>

#### <span data-ttu-id="bc87d-136"><a id="PHPwebapp"></a> Веб-приложение диспетчера PHP</span><span class="sxs-lookup"><span data-stu-id="bc87d-136"><a id="PHPwebapp"></a> The PHP Manager web application</span></span>
<span data-ttu-id="bc87d-137">Вот так выглядит домашняя страница развертывания диспетчера PHP.</span><span class="sxs-lookup"><span data-stu-id="bc87d-137">The following is the home page of the PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="bc87d-139">Как видно, расширение веб-приложения похоже на обычное веб-приложение, при этом в его корневую папку помещен дополнительный файл ApplicationHost.xdt (подробные сведения о файле ApplicationHost.xdt доступны в следующем разделе этой статьи).</span><span class="sxs-lookup"><span data-stu-id="bc87d-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in the root folder of the web app (more details about the ApplicationHost.xdt file are available in the next section of this article).</span></span>

<span data-ttu-id="bc87d-140">Расширение диспетчера PHP было создано с помощью шаблона веб-приложения Visual Studio ASP.NET 4 MVC.</span><span class="sxs-lookup"><span data-stu-id="bc87d-140">The PHP Manager extension was created using the Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="bc87d-141">В следующем представлении из обозревателя решений показана структура расширения диспетчера PHP.</span><span class="sxs-lookup"><span data-stu-id="bc87d-141">The following view from Solution Explorer shows the structure of the PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="bc87d-143">Для файлового ввода-вывода требуется единственная специальная логика — указать расположение каталога wwwroot в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="bc87d-143">The only special logic needed for file I/O is to indicate where the wwwroot directory of the web app is located.</span></span> <span data-ttu-id="bc87d-144">Как показано в следующем примере кода, переменная среды HOME задает путь к корневому каталогу веб-приложения, а путь к каталогу wwwroot можно сформировать, добавив site\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="bc87d-144">As the following code example shows, the environment variable "HOME" indicates the web app's root path, and the wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives the location of the .user.ini file, even if one doesn't exist yet
/// </summary>
private static string GetUserSettingsFilePath()
{
  var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
  if (rootPath == null)
  {
    rootPath = System.IO.Path.GetTempPath(); // For testing purposes
  };
  var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
  return userSettingsFile;
}
```


<span data-ttu-id="bc87d-145">После получения пути к каталогу можно использовать обычные операции файлового ввода-вывода для чтения и записи файлов.</span><span class="sxs-lookup"><span data-stu-id="bc87d-145">After you have the directory path, you can use regular file I/O operations to read and write to files.</span></span>

<span data-ttu-id="bc87d-146">При использовании расширений веб-приложения следует обратить внимание на обработку внутренних ссылок.</span><span class="sxs-lookup"><span data-stu-id="bc87d-146">One point of caution with web app extensions regards the handling of internal links.</span></span>  <span data-ttu-id="bc87d-147">Если в HTML-файлах присутствуют ссылки, задающие абсолютные пути к внутренним ссылкам веб-приложения, необходимо убедиться, что в начало этих ссылок добавляется имя расширения в качестве корневого каталога.</span><span class="sxs-lookup"><span data-stu-id="bc87d-147">If you have any links in your HTML files that give absolute paths to internal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="bc87d-148">Это необходимо, поскольку теперь корневой каталог для расширения имеет вид "/`[your-extension-name]`/" вместо обычного "/", поэтому необходимо соответствующим образом обновить все внутренние ссылки.</span><span class="sxs-lookup"><span data-stu-id="bc87d-148">This is needed because the root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="bc87d-149">Например, предположим, что в коде присутствует следующая ссылка:</span><span class="sxs-lookup"><span data-stu-id="bc87d-149">For example, suppose your code includes a link to the following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="bc87d-150">Если ссылка является частью расширения веб-приложения, ссылка должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bc87d-150">When the link is part of a web app extension, the link must be in the following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="bc87d-151">Это требование можно обойти двумя способами: либо использовать в веб-приложении только относительные пути, либо в случае с приложениями ASP.NET использовать метод `@Html.ActionLink` , который автоматически создает правильные ссылки.</span><span class="sxs-lookup"><span data-stu-id="bc87d-151">You can work around this requirement by either using only relative paths within your web application, or in the case of ASP.NET applications, by using the `@Html.ActionLink` method which creates the appropriate links for you.</span></span>

#### <span data-ttu-id="bc87d-152"><a id="XDT"></a> Файл applicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="bc87d-152"><a id="XDT"></a> The applicationHost.xdt file</span></span>
<span data-ttu-id="bc87d-153">Код расширения веб-приложения находится в каталоге %HOME%\SiteExtensions\[имя_вашего_расширения].</span><span class="sxs-lookup"><span data-stu-id="bc87d-153">The code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="bc87d-154">Мы назовем его корневым каталогом расширения.</span><span class="sxs-lookup"><span data-stu-id="bc87d-154">We'll call this the extension root.</span></span>  

<span data-ttu-id="bc87d-155">Чтобы зарегистрировать расширение веб-приложения в файле applicationHost.config, необходимо поместить файл с именем ApplicationHost.xdt в корневой каталог расширения.</span><span class="sxs-lookup"><span data-stu-id="bc87d-155">To register your web app extension with the applicationHost.config file, you need to place a file called ApplicationHost.xdt in the extension root.</span></span> <span data-ttu-id="bc87d-156">Содержимое файла ApplicationHost.xdt должно выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="bc87d-156">The content of the ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in the application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="bc87d-157">Имя, задаваемое в качестве имени расширения, должно совпадать с именем корневого каталога расширения.</span><span class="sxs-lookup"><span data-stu-id="bc87d-157">The name you select as your extension name should have the same name as your extension root folder.</span></span>

<span data-ttu-id="bc87d-158">Это аналогично добавлению пути нового приложения в список сайтов `system.applicationHost` на сайте SCM.</span><span class="sxs-lookup"><span data-stu-id="bc87d-158">This has the effect of adding a new application path to the `system.applicationHost` sites list under the SCM site.</span></span> <span data-ttu-id="bc87d-159">Сайт SCM является конечной точкой администрирования сайта и имеет специальные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="bc87d-159">The SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="bc87d-160">У него есть следующий URL-адрес `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="bc87d-160">It has the URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

```xml
<system.applicationHost>
  ...       
  <sites>
    <site name="~1[your-website]" id="1716402716">
      <bindings>
        <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
        <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
      </bindings>
      <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
      <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
      <logFile logSiteId="false" />
      <application path="/" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
      </application>
      <!-- Note the custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="bc87d-161"><a id="deploy"></a> Развертывание расширения веб-приложения</span><span class="sxs-lookup"><span data-stu-id="bc87d-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="bc87d-162">Чтобы установить расширение веб-приложения, скопируйте все файлы веб-приложения через протокол FTP в папку веб-приложения `\SiteExtensions\[your-extension-name]`. Речь идет о веб-приложении, для которого необходимо установить расширение.</span><span class="sxs-lookup"><span data-stu-id="bc87d-162">To install your web app extension, you can use FTP to copy all the files of your web application to the `\SiteExtensions\[your-extension-name]` folder of the web app on which you want to install the extension.</span></span>  <span data-ttu-id="bc87d-163">Не забудьте скопировать в эту папку и файл ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="bc87d-163">Be sure to copy the ApplicationHost.xdt file to this location as well.</span></span> <span data-ttu-id="bc87d-164">Перезапустите веб-приложение, чтобы включить расширение.</span><span class="sxs-lookup"><span data-stu-id="bc87d-164">Restart your web app to enable the extension.</span></span>

<span data-ttu-id="bc87d-165">Расширение веб-приложения должно стать доступным по следующему адресу:</span><span class="sxs-lookup"><span data-stu-id="bc87d-165">You should be able to see your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="bc87d-166">Обратите внимание, что этот URL-адрес похож на URL-адрес веб-приложения. Он отличается только использованием протокола HTTPS и наличием расширения SCM.</span><span class="sxs-lookup"><span data-stu-id="bc87d-166">Note that the URL looks just like the URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="bc87d-167">Вы можете отключить все частные расширения (кроме предустановленных) для веб-приложения. Это может потребоваться во время разработки или исследования. Для этого нужно добавить параметр приложения с ключом `WEBSITE_PRIVATE_EXTENSIONS` и значением `0`.</span><span class="sxs-lookup"><span data-stu-id="bc87d-167">It is possible to disable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with the key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="bc87d-168">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="bc87d-168">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="bc87d-169">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="bc87d-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="bc87d-170">Изменения</span><span class="sxs-lookup"><span data-stu-id="bc87d-170">What's changed</span></span>
* <span data-ttu-id="bc87d-171">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="bc87d-171">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

