---
title: "веб-приложения служб приложений aaaAzure дополнительные конфигурации и расширения"
description: "Используйте файл ApplicationHost.config hello tootransform объявления Transformation(XDT) документа XML в вашей службе приложений Azure веб-приложение и tooadd закрытые расширения tooenable администрирования пользовательских действий."
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
ms.openlocfilehash: 873347ac13113d1ac989cba29128382c81dcfcca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="23ea1-103">Дополнительные настройки и расширения веб-приложений службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="23ea1-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="23ea1-104">С помощью [преобразование XML-документов](http://msdn.microsoft.com/library/dd465326.aspx) объявления (XDT), можно преобразовать hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) файла в веб-приложения в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="23ea1-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="23ea1-105">Можно также использовать XDT объявления tooadd закрытые расширения tooenable серверные приложения действия администрирования.</span><span class="sxs-lookup"><span data-stu-id="23ea1-105">You can also use XDT declarations tooadd private extensions tooenable custom web app administration actions.</span></span> <span data-ttu-id="23ea1-106">Статья содержит пример расширения для веб-приложения диспетчера PHP, позволяющего управлять параметрами PHP через веб-интерфейс.</span><span class="sxs-lookup"><span data-stu-id="23ea1-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="23ea1-107"><a id="transform"></a>Дополнительные настройки посредством ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="23ea1-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="23ea1-108">Hello платформы службы приложений обеспечивает гибкость и управления для настройки веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="23ea1-108">hello App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="23ea1-109">Несмотря на то, что файл конфигурации IIS ApplicationHost.config Стандартная hello недоступен для прямого редактирования в службе приложений, платформа hello поддерживает декларативную модель ApplicationHost.config преобразования для преобразования документа XML (XDT) на основе.</span><span class="sxs-lookup"><span data-stu-id="23ea1-109">Although hello standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, hello platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="23ea1-110">tooleverage этой функциональности преобразования, создайте файл ApplicationHost.xdt с XDT содержимого и поместите hello сайта (d:\home\site) в корне hello [Kudu консоли](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="23ea1-110">tooleverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under hello site root (d:\home\site) in hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="23ea1-111">Для изменения эффекта tootake может потребоваться hello toorestart веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="23ea1-111">You may need toorestart hello Web App for changes tootake effect.</span></span>

<span data-ttu-id="23ea1-112">Следующий образец applicationHost.xdt Hello показано, как tooadd новой переменной tooa настраиваемой среды веб-приложения, использующего PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="23ea1-112">hello following applicationHost.xdt sample shows how tooadd a new custom environment variable tooa web app that uses PHP 5.4.</span></span>

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

<span data-ttu-id="23ea1-113">Файл журнала с состоянием преобразования и подробные сведения можно получить на hello FTP корне LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="23ea1-113">A log file with transform status and details is available from hello FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="23ea1-114">Дополнительные примеры см. на странице [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="23ea1-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="23ea1-115">**Примечание.**</span><span class="sxs-lookup"><span data-stu-id="23ea1-115">**Note**</span></span><br />
<span data-ttu-id="23ea1-116">Элементы из списка модулей в hello `system.webServer` нельзя удалить или переупорядочить, но возможны список toohello дополнения.</span><span class="sxs-lookup"><span data-stu-id="23ea1-116">Elements from hello list of modules under `system.webServer` cannot be removed or reordered, but additions toohello list are possible.</span></span>

## <span data-ttu-id="23ea1-117"><a id="extend"></a> Расширения для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="23ea1-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="23ea1-118"><a id="overview"></a> Обзор частных расширений для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="23ea1-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="23ea1-119">Служба приложений дает возможность использовать расширения веб-приложений для выполнения дополнительных действий по администрированию.</span><span class="sxs-lookup"><span data-stu-id="23ea1-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="23ea1-120">Некоторые функции платформы службы приложений реализованы в виде предустановленных расширений.</span><span class="sxs-lookup"><span data-stu-id="23ea1-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="23ea1-121">Хотя нельзя изменить hello предварительно установленные расширения, можно создавать и настраивать частных расширений веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="23ea1-121">While hello pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="23ea1-122">Эта функциональная возможность основана на объявлениях XDT.</span><span class="sxs-lookup"><span data-stu-id="23ea1-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="23ea1-123">Hello основные шаги для создания расширения частного веб-приложения, hello следующее:</span><span class="sxs-lookup"><span data-stu-id="23ea1-123">hello key steps for creating a private web app extension are hello following:</span></span>

1. <span data-ttu-id="23ea1-124">**Содержимое**расширения веб-приложения: создайте приложение, поддерживаемое службой приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="23ea1-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="23ea1-125">**Объявление**расширения веб-приложения: создайте файл ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="23ea1-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="23ea1-126">Веб-расширение приложения **развертывания**: размещение содержимого во вложенной папке SiteExtensions hello`root`</span><span class="sxs-lookup"><span data-stu-id="23ea1-126">Web app extension **deployment**: place content in hello SiteExtensions folder under `root`</span></span>

<span data-ttu-id="23ea1-127">Внутренние ссылки для веб-приложения hello должна указывать приложения tooa путь toohello относительный путь, указанный в файл ApplicationHost.xdt hello.</span><span class="sxs-lookup"><span data-stu-id="23ea1-127">Internal links for hello web app should point tooa path relative toohello application path specified in hello ApplicationHost.xdt file.</span></span> <span data-ttu-id="23ea1-128">Любое изменение toohello ApplicationHost.xdt файла требуется повторный запуск приложения web.</span><span class="sxs-lookup"><span data-stu-id="23ea1-128">Any change toohello ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="23ea1-129">**Примечание**. Дополнительные сведения об этих ключевых элементах см. на странице [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="23ea1-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="23ea1-130">Подробный пример — включить tooillustrate hello шаги для создания и включения расширения частного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="23ea1-130">A detailed example is included tooillustrate hello steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="23ea1-131">Здравствуйте, исходный код для примера hello диспетчер PHP, следующим образом можно загрузить из [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="23ea1-131">hello source code for hello PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="23ea1-132"><a id="SiteSample"></a> Пример расширения сайта веб-приложения: диспетчер PHP</span><span class="sxs-lookup"><span data-stu-id="23ea1-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="23ea1-133">Диспетчер PHP представляет расширение веб-приложения, которая позволяет веб-приложения администраторы tooeasily представление и настройки параметров PHP с помощью веб-интерфейса вместо toomodify PHP INI-файлов напрямую.</span><span class="sxs-lookup"><span data-stu-id="23ea1-133">PHP Manager is a web app extension that allows web app administrators tooeasily view and configure their PHP settings using a web interface instead of having toomodify PHP .ini files directly.</span></span> <span data-ttu-id="23ea1-134">Общие файлы конфигурации для PHP включаемый файл php.ini hello, расположенную в Program Files и hello. user.ini файл, расположенный в корневой папке веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="23ea1-134">Common configuration files for PHP include hello php.ini file located under Program Files and hello .user.ini file located in hello root folder of your web app.</span></span> <span data-ttu-id="23ea1-135">Так как файл php.ini hello не может быть изменено непосредственно на hello платформы службы приложений, hello расширения PHP Manager использует hello. tooapply файл user.ini изменения параметров.</span><span class="sxs-lookup"><span data-stu-id="23ea1-135">Since hello php.ini file is not directly editable on hello App Service platform, hello PHP Manager extension uses hello .user.ini file tooapply setting changes.</span></span>

#### <span data-ttu-id="23ea1-136"><a id="PHPwebapp"></a>Диспетчер PHP веб-приложение Hello</span><span class="sxs-lookup"><span data-stu-id="23ea1-136"><a id="PHPwebapp"></a> hello PHP Manager web application</span></span>
<span data-ttu-id="23ea1-137">Hello Вот hello домашнюю страницу приветствия диспетчер PHP развертывания:</span><span class="sxs-lookup"><span data-stu-id="23ea1-137">hello following is hello home page of hello PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="23ea1-139">Как видите, расширение веб-приложения — так же, как обычный веб-приложения, но с ApplicationHost.xdt файла помещен в корневую папку hello hello веб-приложения (Дополнительные сведения о файле ApplicationHost.xdt hello доступны в следующем разделе hello объекта Статья).</span><span class="sxs-lookup"><span data-stu-id="23ea1-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in hello root folder of hello web app (more details about hello ApplicationHost.xdt file are available in hello next section of this article).</span></span>

<span data-ttu-id="23ea1-140">расширения диспетчера PHP Hello был создан с помощью шаблона Visual Studio ASP.NET MVC 4 веб-приложение hello.</span><span class="sxs-lookup"><span data-stu-id="23ea1-140">hello PHP Manager extension was created using hello Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="23ea1-141">Hello следующее представление из обозревателя решений показана структура hello hello расширения диспетчера PHP.</span><span class="sxs-lookup"><span data-stu-id="23ea1-141">hello following view from Solution Explorer shows hello structure of hello PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="23ea1-143">Hello только специальные логику, необходимую для файлового ввода-вывода — tooindicate где hello wwwroot веб-приложения hello расположен каталог.</span><span class="sxs-lookup"><span data-stu-id="23ea1-143">hello only special logic needed for file I/O is tooindicate where hello wwwroot directory of hello web app is located.</span></span> <span data-ttu-id="23ea1-144">Как hello следующем примере кода показано, hello переменной среды «HOME» указывает hello корневой путь веб-приложения и путь wwwroot hello могут создаваться путем добавления «site\wwwroot»:</span><span class="sxs-lookup"><span data-stu-id="23ea1-144">As hello following code example shows, hello environment variable "HOME" indicates hello web app's root path, and hello wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives hello location of hello .user.ini file, even if one doesn't exist yet
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


<span data-ttu-id="23ea1-145">После того как вы hello путь к каталогу, можно использовать обычным файлом tooread операций ввода-вывода и записи toofiles.</span><span class="sxs-lookup"><span data-stu-id="23ea1-145">After you have hello directory path, you can use regular file I/O operations tooread and write toofiles.</span></span>

<span data-ttu-id="23ea1-146">Обработка hello внутренних ссылок согласно указаниям одну точку осторожны с расширений веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="23ea1-146">One point of caution with web app extensions regards hello handling of internal links.</span></span>  <span data-ttu-id="23ea1-147">Если все ссылки в HTML-файлах, предоставляющие абсолютные пути toointernal ссылки на веб-приложения, необходимо убедиться, что эти ссылки добавляются с вашим именем расширения в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="23ea1-147">If you have any links in your HTML files that give absolute paths toointernal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="23ea1-148">Это необходимо, поскольку теперь hello корневой элемент для модуля «/`[your-extension-name]`/ «а просто «/», поэтому все внутренние ссылки должны обновляться соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="23ea1-148">This is needed because hello root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="23ea1-149">Например предположим, что код включает в себя следующие toohello ссылку:</span><span class="sxs-lookup"><span data-stu-id="23ea1-149">For example, suppose your code includes a link toohello following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="23ea1-150">При связи hello расширение веб-приложения hello ссылки должны быть hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="23ea1-150">When hello link is part of a web app extension, hello link must be in hello following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="23ea1-151">Это требование можно обойти, используя только относительные пути в веб-приложения или в hello регистр приложений ASP.NET с помощью hello `@Html.ActionLink` метод, который создает соответствующие связи hello.</span><span class="sxs-lookup"><span data-stu-id="23ea1-151">You can work around this requirement by either using only relative paths within your web application, or in hello case of ASP.NET applications, by using hello `@Html.ActionLink` method which creates hello appropriate links for you.</span></span>

#### <span data-ttu-id="23ea1-152"><a id="XDT"></a>файл applicationHost.xdt Hello</span><span class="sxs-lookup"><span data-stu-id="23ea1-152"><a id="XDT"></a> hello applicationHost.xdt file</span></span>
<span data-ttu-id="23ea1-153">Hello код для расширения вашего веб-приложения, находится в разделе %HOME%\SiteExtensions\[ваше имя расширения].</span><span class="sxs-lookup"><span data-stu-id="23ea1-153">hello code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="23ea1-154">Мы назовем этого корня расширения hello.</span><span class="sxs-lookup"><span data-stu-id="23ea1-154">We'll call this hello extension root.</span></span>  

<span data-ttu-id="23ea1-155">tooregister вашей расширение веб-приложения с помощью файла applicationHost.config hello, необходимо tooplace файл с именем ApplicationHost.xdt в корневом каталоге расширения hello.</span><span class="sxs-lookup"><span data-stu-id="23ea1-155">tooregister your web app extension with hello applicationHost.config file, you need tooplace a file called ApplicationHost.xdt in hello extension root.</span></span> <span data-ttu-id="23ea1-156">Hello содержимое файла ApplicationHost.xdt hello должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="23ea1-156">hello content of hello ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in hello application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="23ea1-157">Hello, выбранных в качестве расширения имени, должны иметь hello точно такое же имя в корневой папке расширения.</span><span class="sxs-lookup"><span data-stu-id="23ea1-157">hello name you select as your extension name should have hello same name as your extension root folder.</span></span>

<span data-ttu-id="23ea1-158">Действует hello добавления новых toohello путь приложения `system.applicationHost` список сайтов на сайте SCM hello.</span><span class="sxs-lookup"><span data-stu-id="23ea1-158">This has hello effect of adding a new application path toohello `system.applicationHost` sites list under hello SCM site.</span></span> <span data-ttu-id="23ea1-159">сайт SCM Hello является конечную точку администрирования сайта с помощью определенных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="23ea1-159">hello SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="23ea1-160">Она содержит URL-адрес hello `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="23ea1-160">It has hello URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

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
      <!-- Note hello custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="23ea1-161"><a id="deploy"></a> Развертывание расширения веб-приложения</span><span class="sxs-lookup"><span data-stu-id="23ea1-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="23ea1-162">tooinstall расширение веб-приложения FTP toocopy можно использовать все файлы hello вашей toohello приложения web `\SiteExtensions\[your-extension-name]` папки веб-приложения hello, на котором будет tooinstall hello расширения.</span><span class="sxs-lookup"><span data-stu-id="23ea1-162">tooinstall your web app extension, you can use FTP toocopy all hello files of your web application toohello `\SiteExtensions\[your-extension-name]` folder of hello web app on which you want tooinstall hello extension.</span></span>  <span data-ttu-id="23ea1-163">Быть убедиться, что toocopy hello ApplicationHost.xdt toothis расположение файла также.</span><span class="sxs-lookup"><span data-stu-id="23ea1-163">Be sure toocopy hello ApplicationHost.xdt file toothis location as well.</span></span> <span data-ttu-id="23ea1-164">Перезапустите расширения hello tooenable вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="23ea1-164">Restart your web app tooenable hello extension.</span></span>

<span data-ttu-id="23ea1-165">Необходимо будет toosee расширения вашего веб-приложения на:</span><span class="sxs-lookup"><span data-stu-id="23ea1-165">You should be able toosee your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="23ea1-166">Обратите внимание, что приветствия URL-адрес выглядит так же, как hello URL-адрес веб-приложения, за исключением того, что он использует протокол HTTPS и содержит «.scm».</span><span class="sxs-lookup"><span data-stu-id="23ea1-166">Note that hello URL looks just like hello URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="23ea1-167">Это возможно toodisable всех частных (не было предварительно установлено) расширения для веб-приложения во время разработки и исследования путем добавления параметров приложения с ключом hello `WEBSITE_PRIVATE_EXTENSIONS` и значение `0`.</span><span class="sxs-lookup"><span data-stu-id="23ea1-167">It is possible toodisable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with hello key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="23ea1-168">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="23ea1-168">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="23ea1-169">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="23ea1-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="23ea1-170">Изменения</span><span class="sxs-lookup"><span data-stu-id="23ea1-170">What's changed</span></span>
* <span data-ttu-id="23ea1-171">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="23ea1-171">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

