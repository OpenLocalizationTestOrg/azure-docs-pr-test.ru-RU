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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Дополнительные настройки и расширения веб-приложений службы приложений Azure
С помощью [преобразование XML-документов](http://msdn.microsoft.com/library/dd465326.aspx) объявления (XDT), можно преобразовать hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) файла в веб-приложения в службе приложений Azure. Можно также использовать XDT объявления tooadd закрытые расширения tooenable серверные приложения действия администрирования. Статья содержит пример расширения для веб-приложения диспетчера PHP, позволяющего управлять параметрами PHP через веб-интерфейс.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>Дополнительные настройки посредством ApplicationHost.config
Hello платформы службы приложений обеспечивает гибкость и управления для настройки веб-приложения. Несмотря на то, что файл конфигурации IIS ApplicationHost.config Стандартная hello недоступен для прямого редактирования в службе приложений, платформа hello поддерживает декларативную модель ApplicationHost.config преобразования для преобразования документа XML (XDT) на основе.

tooleverage этой функциональности преобразования, создайте файл ApplicationHost.xdt с XDT содержимого и поместите hello сайта (d:\home\site) в корне hello [Kudu консоли](https://github.com/projectkudu/kudu/wiki/Kudu-console). Для изменения эффекта tootake может потребоваться hello toorestart веб-приложения.

Следующий образец applicationHost.xdt Hello показано, как tooadd новой переменной tooa настраиваемой среды веб-приложения, использующего PHP 5.4.

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

Файл журнала с состоянием преобразования и подробные сведения можно получить на hello FTP корне LogFiles\Transform.

Дополнительные примеры см. на странице [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).

**Примечание.**<br />
Элементы из списка модулей в hello `system.webServer` нельзя удалить или переупорядочить, но возможны список toohello дополнения.

## <a id="extend"></a> Расширения для веб-приложения
### <a id="overview"></a> Обзор частных расширений для веб-приложения
Служба приложений дает возможность использовать расширения веб-приложений для выполнения дополнительных действий по администрированию. Некоторые функции платформы службы приложений реализованы в виде предустановленных расширений. Хотя нельзя изменить hello предварительно установленные расширения, можно создавать и настраивать частных расширений веб-приложения. Эта функциональная возможность основана на объявлениях XDT. Hello основные шаги для создания расширения частного веб-приложения, hello следующее:

1. **Содержимое**расширения веб-приложения: создайте приложение, поддерживаемое службой приложений Azure.
2. **Объявление**расширения веб-приложения: создайте файл ApplicationHost.xdt.
3. Веб-расширение приложения **развертывания**: размещение содержимого во вложенной папке SiteExtensions hello`root`

Внутренние ссылки для веб-приложения hello должна указывать приложения tooa путь toohello относительный путь, указанный в файл ApplicationHost.xdt hello. Любое изменение toohello ApplicationHost.xdt файла требуется повторный запуск приложения web.

**Примечание**. Дополнительные сведения об этих ключевых элементах см. на странице [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).

Подробный пример — включить tooillustrate hello шаги для создания и включения расширения частного веб-приложения. Здравствуйте, исходный код для примера hello диспетчер PHP, следующим образом можно загрузить из [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).

### <a id="SiteSample"></a> Пример расширения сайта веб-приложения: диспетчер PHP
Диспетчер PHP представляет расширение веб-приложения, которая позволяет веб-приложения администраторы tooeasily представление и настройки параметров PHP с помощью веб-интерфейса вместо toomodify PHP INI-файлов напрямую. Общие файлы конфигурации для PHP включаемый файл php.ini hello, расположенную в Program Files и hello. user.ini файл, расположенный в корневой папке веб-приложения hello. Так как файл php.ini hello не может быть изменено непосредственно на hello платформы службы приложений, hello расширения PHP Manager использует hello. tooapply файл user.ini изменения параметров.

#### <a id="PHPwebapp"></a>Диспетчер PHP веб-приложение Hello
Hello Вот hello домашнюю страницу приветствия диспетчер PHP развертывания:

![TransformSitePHPUI][TransformSitePHPUI]

Как видите, расширение веб-приложения — так же, как обычный веб-приложения, но с ApplicationHost.xdt файла помещен в корневую папку hello hello веб-приложения (Дополнительные сведения о файле ApplicationHost.xdt hello доступны в следующем разделе hello объекта Статья).

расширения диспетчера PHP Hello был создан с помощью шаблона Visual Studio ASP.NET MVC 4 веб-приложение hello. Hello следующее представление из обозревателя решений показана структура hello hello расширения диспетчера PHP.

![TransformSiteSolEx][TransformSiteSolEx]

Hello только специальные логику, необходимую для файлового ввода-вывода — tooindicate где hello wwwroot веб-приложения hello расположен каталог. Как hello следующем примере кода показано, hello переменной среды «HOME» указывает hello корневой путь веб-приложения и путь wwwroot hello могут создаваться путем добавления «site\wwwroot»:

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


После того как вы hello путь к каталогу, можно использовать обычным файлом tooread операций ввода-вывода и записи toofiles.

Обработка hello внутренних ссылок согласно указаниям одну точку осторожны с расширений веб-приложения.  Если все ссылки в HTML-файлах, предоставляющие абсолютные пути toointernal ссылки на веб-приложения, необходимо убедиться, что эти ссылки добавляются с вашим именем расширения в корневом каталоге. Это необходимо, поскольку теперь hello корневой элемент для модуля «/`[your-extension-name]`/ «а просто «/», поэтому все внутренние ссылки должны обновляться соответствующим образом. Например предположим, что код включает в себя следующие toohello ссылку:

`"<a href="/Home/Settings">PHP Settings</a>"`

При связи hello расширение веб-приложения hello ссылки должны быть hello следующие формы:

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

Это требование можно обойти, используя только относительные пути в веб-приложения или в hello регистр приложений ASP.NET с помощью hello `@Html.ActionLink` метод, который создает соответствующие связи hello.

#### <a id="XDT"></a>файл applicationHost.xdt Hello
Hello код для расширения вашего веб-приложения, находится в разделе %HOME%\SiteExtensions\[ваше имя расширения]. Мы назовем этого корня расширения hello.  

tooregister вашей расширение веб-приложения с помощью файла applicationHost.config hello, необходимо tooplace файл с именем ApplicationHost.xdt в корневом каталоге расширения hello. Hello содержимое файла ApplicationHost.xdt hello должна выглядеть следующим образом:

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

Hello, выбранных в качестве расширения имени, должны иметь hello точно такое же имя в корневой папке расширения.

Действует hello добавления новых toohello путь приложения `system.applicationHost` список сайтов на сайте SCM hello. сайт SCM Hello является конечную точку администрирования сайта с помощью определенных учетных данных. Она содержит URL-адрес hello `https://[your-site-name].scm.azurewebsites.net`.  

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

### <a id="deploy"></a> Развертывание расширения веб-приложения
tooinstall расширение веб-приложения FTP toocopy можно использовать все файлы hello вашей toohello приложения web `\SiteExtensions\[your-extension-name]` папки веб-приложения hello, на котором будет tooinstall hello расширения.  Быть убедиться, что toocopy hello ApplicationHost.xdt toothis расположение файла также. Перезапустите расширения hello tooenable вашего веб-приложения.

Необходимо будет toosee расширения вашего веб-приложения на:

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

Обратите внимание, что приветствия URL-адрес выглядит так же, как hello URL-адрес веб-приложения, за исключением того, что он использует протокол HTTPS и содержит «.scm».

Это возможно toodisable всех частных (не было предварительно установлено) расширения для веб-приложения во время разработки и исследования путем добавления параметров приложения с ключом hello `WEBSITE_PRIVATE_EXTENSIONS` и значение `0`.

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

