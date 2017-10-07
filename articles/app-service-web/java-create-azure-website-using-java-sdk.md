---
title: "aaaCreate веб-приложения в службе приложений Azure с помощью hello Azure SDK для Java"
description: "Узнайте, как toocreate веб-приложения в службе приложений Azure программно с помощью hello Azure SDK для Java."
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a>Создание веб-приложения в службе приложений Azure с помощью hello Azure SDK для Java
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a>Обзор
В этом пошаговом руководстве показано, как toocreate Azure SDK для Java-приложения, которое создает веб-приложения в [службе приложений Azure][Azure App Service], затем развернуть tooit приложения. Руководство состоит из двух частей:

* Часть 1 показано, как toobuild приложения Java, создает веб-приложения.
* Часть 2 показано, как toocreate простой JSP «Hello World» приложения, а затем код toodeploy tooApp службы для использования FTP клиента.

## <a name="prerequisites"></a>Предварительные требования
### <a name="software-installations"></a>Установка программного обеспечения
Hello AzureWebDemo кода приложения в этой статье было написано с помощью Java SDK Azure 0.7.0, которую можно установить с помощью hello [Web Platform Installer] [ Web Platform Installer] (WebPI). Кроме того, убедитесь, что toouse hello последнюю версию hello [средств Azure для Eclipse][Azure Toolkit for Eclipse]. После установки пакета SDK для hello, обновите hello зависимости в проект Eclipse, запустив **обновления индекса** в **репозиториев Maven**, затем снова добавьте hello последняя версия каждого пакета в hello  **Зависимости** окна. Можно проверить hello версии установленного программного обеспечения в Eclipse, щелкнув **Справка > сведения об установке**; вы должны иметь по крайней мере hello следующие версии:

* пакет для библиотек Microsoft Azure для Java 0.7.0.20150309;
* интегрированная среда разработки Eclipse для разработчиков Java EE 4.4.2.20150219.

### <a name="create-and-configure-cloud-resources-in-azure"></a>Создание и настройка облачных ресурсов в Azure
Перед началом этой процедуры требуется toohave Активная подписка Azure и настроить Active Directory (AD) в Azure по умолчанию.

### <a name="create-an-active-directory-ad-in-azure"></a>Создание Active Directory в Azure
Если Active Directory (AD) еще не установлен на подписки Azure, войдите на hello [классический портал Azure] [ Azure classic portal] с учетной записью Майкрософт. Если у вас несколько подписок, нажмите кнопку **подписки** и выберите hello каталог по умолчанию для подписки hello toouse требуется для этого проекта. Нажмите кнопку **применить** tooswitch toothat подписки представлении.

1. Выберите **Active Directory** hello меню в левой части. Щелкните **Создать > Каталог > Настраиваемое создание**.
2. В разделе **Добавить каталог** выберите **Создать каталог**.
3. В поле **Имя**введите имя каталога.
4. В поле **Домен** введите имя домена. Имя основного домена, которое включается по умолчанию в каталоге; имеет форму hello `<domain_name>.onmicrosoft.com`. Можно назвать его на основе имени каталога hello или другое имя домена, которое вы являетесь владельцем. Позже вы сможете добавить другое доменное имя, которое уже использует ваша организация.
5. В поле **Страна или регион**выберите свой языковой стандарт.

Дополнительную информацию об Active Directory см. в разделе [Что такое каталог Azure AD?][What is an Azure AD directory]

### <a name="create-a-management-certificate-for-azure"></a>Создание сертификата управления для Azure
Hello Azure SDK для Java использует tooauthenticate сертификаты управления подписками Azure. Они являются сертификатами X.509 v3, используется tooauthenticate клиентское приложение, которое использует API управления службами tooact hello от имени ресурсами подписки toomanage владелец подписки hello.

Hello кода в этой процедуре используется tooauthenticate самозаверяющий сертификат с Azure. Для выполнения этой процедуры нужно toocreate сертификат и передать его toohello [классический портал Azure] [ Azure classic portal] заранее. Включает в себя hello следующие шаги:

* Создайте PFX-файл, представляющий собой сертификат клиента, и сохраните его локально.
* Создайте сертификат управления (CER-файл) из PFX-файла hello.
* Отправьте tooyour файл CER hello подписки Azure.
* Преобразование hello PFX-файла в JKS, так как этот формат tooauthenticate, с помощью сертификатов использует Java.
* Напишите код проверки подлинности приложения hello, который ссылается на локальный файл JKS toohello.

По завершении этой процедуры сертификат CER hello будет находиться в вашей подписке Azure и сертификат JKS hello будет находиться на локальном диске. Дополнительную информацию о сертификатах управления см. в разделе [Создание и передача сертификата управления для Azure][Create and Upload a Management Certificate for Azure].

#### <a name="create-a-certificate"></a>Создание сертификата
toocreate собственный самозаверяющий сертификат, откройте консоль командной строки в операционной системе и выполните hello, следующие команды.

> **Примечание:** hello компьютера, на котором выполняется эта команда должен иметь hello JDK установлен. Кроме того keytool toohello hello пути зависит от hello расположение установки hello JDK. Дополнительные сведения см. в разделе [ключ и сертификат средство управления (keytool)] [ Key and Certificate Management Tool (keytool)] в hello Java онлайн-документации.
> 
> 

toocreate hello PFX-файл:

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

toocreate hello CER-файл:

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

Описание:

* `<java-install-dir>`— toohello hello каталог, в которой установлены Java.
* `<keystore-id>`Идентификатор записи hello хранилища ключей (например, `AzureRemoteAccess`).
* `<cert-store-dir>`— toohello hello каталог, в котором нужно toostore сертификаты (например `C:/Certificates`).
* `<cert-file-name>`— Имя файла сертификата hello hello (например `AzureWebDemoCert`).
* `<password>`Выберите сертификат hello tooprotect; паролем hello он должен быть по крайней мере 6 символов. Вы можете вовсе не указывать пароль, хотя это не рекомендуется.
* `<dname>`— toobe hello различающееся имя X.500, связанный с псевдонимом и используется в качестве издателя hello и «тема» в hello самозаверяющий сертификат.

Дополнительные сведения см. в статье [Общие сведения о сертификатах для облачных служб Azure][Create and Upload a Management Certificate for Azure].

#### <a name="upload-hello-certificate"></a>Отправка сертификата hello
tooupload tooAzure самозаверяющий сертификат, откройте toohello **параметры** hello классическом портале, а затем щелкните hello **сертификаты управления** вкладки. Нажмите кнопку **отправить** внизу hello hello страницы и перейдите в расположение toohello hello CER-файл был создан.

#### <a name="convert-hello-pfx-file-into-jks"></a>Преобразовать в JKS hello PFX-файла
Hello командной строки Windows (работы в качестве администратора), каталог toohello компакт-диск, содержащий hello сертификаты и запуск hello следующую команду, где `<java-install-dir>` — hello каталог, в котором установлен Java на компьютере:

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. При появлении запроса введите пароль ключей hello назначения; Это будет пароль hello для файла JKS hello.
2. При появлении запроса введите пароль ключей hello источника; Это будет пароль hello, указанное для hello PFX-файла.

два пароля Hello toobe hello же нет. Вы можете вовсе не указывать пароль, хотя это не рекомендуется.

## <a name="build-a-web-app-creation-application"></a>Сборка приложения для создания веб-приложения
### <a name="create-hello-eclipse-workspace-and-maven-project"></a>Создание hello рабочей области Eclipse и Maven проекта
В этом разделе создайте рабочую область и проект для hello веб-приложения создания приложения с именем AzureWebDemo Maven.

1. Создайте проект Maven. Щелкните **File > New > Maven Project** (Файл > Создать > Проект Maven). На странице **New Maven Project** (Новый проект Maven) выберите **Create a simple project** (Создать простой проект) и **Use default workspace location** (Использовать расположение рабочей области по умолчанию).
2. На второй странице hello объекта **новый проект Maven**, укажите hello ниже:
   
   * идентификатор группы — `com.<username>.azure.webdemo`
   * идентификатор артефакта — AzureWebDemo;
   * версия— 0.0.1-SNAPSHOT;
   * упаковка — JAR;
   * имя — AzureWebDemo.
     
     Нажмите кнопку **Готово**
3. Откройте файл pom.xml hello новый проект в обозревателе проектов. Выберите hello **зависимости** вкладки. Так как это новый проект, здесь еще нет списка пакетов.
4. Просмотреть репозитории Привет открыть Maven. Щелкните **Window > Show View > Other > Maven > Maven Repositories** (Окно > Показать представление > Другие > Maven > Репозитории Maven) и нажмите кнопку **OK**. Hello **Maven репозиториев** представление появится внизу hello hello интегрированной среды разработки.
5. Откройте **глобального репозиториев**, щелкните правой кнопкой мыши hello **центра** репозитория, а затем выберите **перестроение индекса**.
   
    ![][1]
   
    Этот шаг может занять несколько минут в зависимости от скорости подключения к hello. Перестроение индекса hello, вы увидите hello пакетов Microsoft Azure в hello **центра** Maven репозитория.
6. На вкладке **Dependencies** (Зависимости) щелкните **Add** (Добавить). В поле **Enter Group ID…** (Введите идентификатор группы…) введите `azure-management`. Выберите пакеты hello для базового управления и веб-приложений служб приложений.
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > **Примечание:** при обновлении зависимости hello после выпуска новой версии необходимо toore-добавить всех hello зависимых элементов в этом списке.
   > После нажатия кнопки **добавить** и выберите каждой зависимости, он отображается с hello новый номер версии в hello **зависимости** списка.
   > 
   > 

Нажмите кнопку **ОК**. Здравствуйте пакетов Azure, а затем отображаются в hello **зависимости** списка.

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a>Написание кода Java tooCreate веб-приложения с вызовом hello Azure SDK
Затем напишите hello код, который вызывает API в hello Azure SDK для Java toocreate hello веб-приложения служб приложений.

1. Создайте точки кода Java класс toocontain hello основные элементы. В обозревателе решений, правой кнопкой мыши узел проекта hello и выберите **Создать > класс**.
2. В **новый класс Java**, имя класса hello `WebCreator` и проверьте hello **открытый методе static void main** флажок. Выбор Hello должен выглядеть следующим образом:
   
    ![][2]
3. Нажмите кнопку **Готово** Hello WebCreator.java файл появится в обозревателе проектов.

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a>Вызов веб-приложение службы приложения hello tooCreate Azure API
#### <a name="add-necessary-imports"></a>Добавление необходимых операций импорта
В WebCreator.java добавьте следующие импорты; hello Эти операции импорта предоставляют доступ tooclasses в hello библиотеки управления для использования API-интерфейсов Azure:

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-hello-main-entry-point-class"></a>Определите класс точки hello основные элементы
Для этого приложения, так как hello hello AzureWebDemo приложения служит toocreate веб-приложение службы приложения, name hello основной класс `WebAppCreator`. Этот класс предоставляет hello основные элементы точки кода, который вызывает hello API управления службами Azure toocreate hello веб-приложения.

Добавьте следующие определения параметров для hello веб-приложения и веб-пространства hello. Необходимо будет tooprovide свои собственные подписки Azure код и сведения о сертификате.

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

Описание:

* `<subscription-id>`— Идентификатор подписки Azure hello, которой требуется toocreate hello ресурсов.
* `<certificate-store-path>`— hello путь и имя файла toohello JKS файл в каталоге хранилища локальный сертификат. (например, `C:/Certificates/CertificateName.jks` — для Linux, а `C:\Certificates\CertificateName.jks` — для Windows);
* `<certificate-password>`— пароль hello, указываемое при создании сертификата JKS.
* `webAppName`можно использовать любое имя выбранного; в этой процедуре используется имя hello `WebDemoWebApp`. Hello полное имя домена — hello `webAppName` с hello `domainName` добавляются, поэтому в этом случае hello полное имя домена — `webdemowebapp.azurewebsites.net`.
* `domainName` следует указать, как показано выше;
* `webSpaceName`должен иметь одно из значений hello, определенных в hello [WebSpaceNames] [ WebSpaceNames] класса.
* `appServicePlanName` следует указать, как показано выше;

> **Примечание:** каждый раз при запуске этого приложения, вы должны значение hello toochange `webAppName` и `appServicePlanName` (или удалить веб-приложение hello на портале Azure hello) перед запуском приложения hello еще раз. В противном случае выполнение завершится ошибкой, так как hello того же ресурса уже существует в Azure.
> 
> 

#### <a name="define-hello-web-creation-method"></a>Определение метода создания hello web
Далее следует определите метод toocreate hello веб-приложения. Этот метод `createWebApp`, определяет параметры hello hello веб-приложения и веб-пространства hello. Он также создает и настраивает hello веб-приложений приложения служб управления клиента, который определяется hello [WebSiteManagementClient] [ WebSiteManagementClient] объекта. клиент управления Hello — ключа toocreating веб-приложений. Он предоставляет веб-служб RESTful, позволяющие приложениям toomanage веб-приложения (выполнение операций, таких как создание, update и delete) путем вызова API управления службами hello.

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

Hello код будет выводить код состояния HTTP hello hello ответа об успехе или неудаче и в случае успешного выполнения будет выводить имя hello hello веб-приложение создано.

#### <a name="define-hello-main-method"></a>Определите метод main() hello
Укажите код метода main() hello вызовов createWebApp() toocreate hello веб-приложения.

Наконец, вызовите `createWebApp` из `main`:

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a>Проверка создания веб-приложения и приложение hello
tooverify, приложение работает, нажмите кнопку **запуска > запустить**. По завершении работы приложения hello появятся следующие выходные данные в консоли Eclipse hello hello:

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

Войдите на классический портал Azure hello и щелкните **веб-приложений**. новое веб-приложение Hello должно отображаться в списке веб-приложения hello в течение нескольких минут.

## <a name="deploying-an-application-toohello-web-app"></a>Развертывание приложения toohello веб-приложения
После запуска AzureWebDemo и создать новое веб-приложение hello, журнала hello классический портал, щелкните **веб-приложений**и выберите **WebDemoWebApp** в hello **веб-приложений** списка. Нажмите кнопку на странице панели мониторинга веб-приложения hello **Обзор** (или выберите URL-адрес hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit. Так как содержимое не была toohello опубликованных веб-приложения еще вы увидите страницу пустым заполнителем.

Затем будет создать приложение «Hello World» и развернуть его toohello веб-приложение.

### <a name="create-a-jsp-hello-world-application"></a>Создание приложения JSP Hello World
#### <a name="create-hello-application"></a>Создание приложения hello
В порядке toodemonstrate как hello toodeploy toohello веб-приложение, следуя процедуре показано, как toocreate простого приложения «Hello World» Java и отправьте его toohello приложения службы веб-приложения, создать ваше приложение.

1. Щелкните **File > New > Dynamic Web Project** (Файл > Создать > Динамический веб-проект). Назовите его `JSPHello`. Необязательно toochange другие параметры в этом диалоговом окне. Нажмите кнопку **Готово**
   
    ![][3]
2. В обозревателе проектов разверните hello **JSPHello** щелкните правой кнопкой мыши проект **WebContent**, нажмите кнопку **Создать > JSP-файл**. В диалоговом окне приветствия Создание JSP-файла, имя нового файла hello `index.jsp`. Щелкните **Далее**.
3. В hello **Выбор шаблона JSP** диалоговое окно, выберите **новый JSP-файл (html)** и нажмите кнопку **Готово**.
4. В index.jsp, добавьте следующий код в hello hello `<head>` и `<body>` тег разделы:
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a>Запустите приложение Hello World hello в localhost
Для запуска этого приложения tooconfigure необходимо несколько свойств.

1. Щелкните правой кнопкой мыши hello **JSPHello** проект и выберите **свойства**.
2. В hello **свойства** диалоговое окно: выберите **путь построения Java**выберите hello **заказа и экспортировать** установите флажок **JRE системная библиотека**, нажмите кнопку **Копирование** toomove его toohello вверху списка hello.
   
    ![][4]
3. Кроме того, в hello **свойства** диалоговое окно: выберите **целевых сред выполнения** и нажмите кнопку **New**.
4. В hello **новой среды выполнения сервера** диалоговое окно, выберите сервер, такие как **v7.0 Apache Tomcat** и нажмите кнопку **Далее**. В hello **сервера Tomcat** диалогового окна, набор **имя** слишком`Apache Tomcat v7.0`и задайте **каталог установки Tomcat** toohello каталога, в котором установлена версия hello Вы хотите toouse сервера Tomcat.
   
    ![][5]
   
    Нажмите кнопку **Готово**
5. Затем вернитесь toohello **целевых сред выполнения** страница hello **свойства** диалогового окна. Выберите **Apache Tomcat v7.0** и нажмите кнопку **OK**.
   
    ![][6]
6. В hello Eclipse **запуска** меню, нажмите кнопку **запуска**. В hello **запуска от имени** диалогового окна выберите **выполняются на сервере**. В hello **выполняются на сервере** диалогового окна выберите **Tomcat v7.0 сервера**:
   
    ![][7]
   
    Нажмите кнопку **Готово**
7. Здравствуйте, когда приложение будет работать, вы увидите hello **JSPHello** страницы отображаются в окне localhost в Eclipse (`http://localhost:8080/JSPHello/`), параметры отображения hello следующего сообщения:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a>Экспорт приложения hello как WAR
Экспортируйте файлы веб-проекта hello веб-архив (WAR), чтобы ее можно было развернуть toohello веб-приложения. Hello следующие файлы веб-проекта находятся в папке WebContent hello:

    META-INF
    WEB-INF
    index.jsp

1. Щелкните правой кнопкой мыши папку WebContent hello и выберите **Экспорт**.
2. В hello **экспорта выберите** диалоговое окно, нажмите кнопку **Web > WAR** файла, после чего нажмите кнопку **Далее**.
3. В hello **Экспорт WAR** диалоговое окно, выберите каталог src hello в текущем проекте hello и включать имя hello hello WAR-файл в конце hello. Например:
   
    `<project-path>/JSPHello/src/JSPHello.war`

Дополнительные сведения о развертывании WAR-файлы см. в разделе [добавить tooAzure приложения Java веб-приложений служб приложения](web-sites-java-add-app.md).

### <a name="deploying-hello-hello-world-application-using-ftp"></a>Развертывание FTP с помощью приложения Hello World hello
Выберите приложение hello toopublish клиента FTP сторонних разработчиков. Эта процедура описывает два варианта: hello Kudu консоли встроены в Azure; и FileZilla популярным средством удобны, графический пользовательский интерфейс.

> **Примечание:** hello набора средств Azure для Eclipse поддерживает учетные записи toostorage развертывания и облачных служб, однако в настоящее время не поддерживает приложения tooweb развертывания. Вы можете развернуть toostorage учетные записи и облачные службы, используя проект развертывания Azure, как описано в [Создание приложения Hello World для Azure в Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), но не tooweb приложений. Используете другие методы, например FTP или GitHub tootransfer файлы tooyour веб-приложения.
> 
> **Примечание:** не рекомендуется использовать FTP из командной строки Windows hello (hello FTP.EXE программа, поставляемая с Windows). FTP-клиенты, использующие active FTP, таких как FTP.EXE, часто при сбое toowork брандмауэры. Активный режим FTP Указывает внутренний адрес Локальных сетей, toowhich FTP-сервер может завершиться неудачей tooconnect.
> 
> 

Дополнительные сведения о веб-службы приложений tooan развертывания приложения с помощью протокола FTP. в разделе hello следующие вопросы:

* [Развертывание с помощью служебной программы FTP](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a>"Настройка учетных данных для развертывания"
Убедитесь, что вы запустили hello **AzureWebDemo** toocreate приложения веб-приложения. Расположение файлов toothis будут перенесены.

1. Войдите на классический портал hello и щелкните **веб-приложений**. Убедитесь, что **WebDemoWebApp** отображается в списке hello веб-приложений и убедитесь, что он работает. Нажмите кнопку **WebDemoWebApp** tooopen его **мониторинга** страницы.
2. На hello **мониторинга** в разделе **быстрый обзор**, нажмите кнопку **настроить учетные данные развертывания** (Если вы уже есть учетные данные развертывания, эта функция считывает  **Сброс учетных данных развертывания**).
   
    Учетные данные развертывания связаны с учетной записью Майкрософт. Необходимо toospecify имя пользователя и пароль, которые можно использовать toodeploy, с помощью Git и FTP. Эти учетные данные toodeploy tooany веб-приложения можно использовать во все подписки Azure, связанный с учетной записью Майкрософт. Учетные данные Git и FTP-развертывания в диалоговом окне приветствия, записей hello имя пользователя и пароль для использования в будущем.

#### <a name="get-ftp-connection-information"></a>Получение информации о подключении по FTP
toouse FTP toodeploy приложения файлы toohello только что созданный веб-приложения, необходимо tooobtain сведения о соединении. Существует два способа tooobtain сведения о соединении. Одним из способов toovisit hello веб-приложения **мониторинга** страницы; hello другим способом является профиль публикации toodownload hello веб-приложения. профиль публикации Hello XML-файл, предоставляющий сведения, например учетных данных имя входа и узла FTP для веб-приложения в службе приложений Azure. Во всех подписках, связанных с hello учетная запись Azure, не только этого класса, можно использовать это имя пользователя и пароль toodeploy tooany веб-приложение.

сведения о соединении tooobtain FTP из колонки веб-приложения hello в hello [портала Azure][Azure Portal]:

1. В разделе **Essentials**, найдите и скопируйте hello **имя узла FTP**. Это URI следующего слишком`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.
2. В разделе **Основные компоненты** найдите и скопируйте **имя пользователя FTP или развертывания**. Этот файл может иметь форму hello *webappname\deployment-username*, например `WebDemoWebApp\deployer77`.

сведения о соединении с FTP tooobtain из hello профиль публикации:

1. В колонке hello веб-приложение, нажмите кнопку **получение профиля публикации**. Будет загружен файл .publishsettings tooyour локального диска.
2. Откройте файл PUBLISHSETTINGS hello в редакторе XML или текстовом редакторе и найдите hello `<publishProfile>` элемента, содержащего `publishMethod="FTP"`. Он должен выглядеть hello следующим образом:
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. Обратите внимание, что веб-приложение hello `publishProfile` сопоставление параметров настройки диспетчера сайта FileZilla toohello следующим образом:

* `publishUrl`Здравствуйте, таким же, как **имя узла FTP**, hello значение, заданное в **узла**.
* `publishMethod="FTP"`означает, что вы значение **протокола** слишком**FTP - File Transfer Protocol**, и **шифрования** слишком**использовать обычный FTP**.
* `userName`и `userPWD` являются ключевыми для hello фактических значений имя пользователя и пароль, указанный при сбросе hello учетные данные развертывания. `userName`Здравствуйте, таким же, как **развертывание / пользователь FTP**. Они сопоставляют слишком**пользователя** и **пароль** в FileZilla.
* `ftpPassiveMode="True"`означает, что этот узел hello FTP использует пассивный FTP-ПОРТ передача; Выберите **пассивный** на hello **параметры передачи** вкладки.

#### <a name="configure-hello-web-app-toohost-a-java-application"></a>Настройка веб-приложения hello toohost приложения Java
Прежде чем публиковать приложение hello, необходимо toochange несколько параметров конфигурации, чтобы hello веб-приложения можно разместить приложение Java.

1. Hello классического портала, go toohello веб-приложения **мониторинга** и нажмите кнопку **Настройка**. На hello **Настройка** укажите следующие параметры hello.
2. В **версии Java** по умолчанию hello — **Off**; выберите версии Java hello ориентировано приложение, например 1.7.0_51. После этого, также убедитесь, что **контейнера Web** задано tooa версию сервера Tomcat.
3. В **документов по умолчанию**добавьте index.jsp и переместите его вверх toohello вверху списка hello. (файл по умолчанию hello для веб-приложений — hostingstart.html).
4. Щелкните **Сохранить**.

#### <a name="publish-your-application-using-kudu"></a>Публикация приложения с помощью Kudu
Одним из способов toopublish приложения hello — toouse hello, Kudu отладки консоли, встроенные в Azure. Kudu известен toobe стабильное и согласованное с веб-приложений служб приложений и сервера Tomcat. Для доступа к консоли hello hello веб-приложения путем просмотра URL-адрес tooa hello следующие формы:

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. Для выполнения этой процедуры hello Kudu консоли расположен в hello URL-адреса; Поиск расположения toothis:
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. Hello в верхнем меню, выберите **консоли отладки > CMD**.
3. В командной строке консоли hello перейдите слишком`/site/wwwroot` (или нажмите кнопку `site`, затем `wwwroot` в представлении каталога hello вверху hello hello страницы):
   
    `cd /site/wwwroot`
4. После того как вы укажете значение для **Версия Java**, сервер Tomcat должен создать каталог веб-приложений. В командной строке консоли hello перейдите toohello каталог веб-приложений:
   
    `mkdir webapps`
   
    `cd webapps`
5. Перетащите JSPHello.war из `<project-path>/JSPHello/src/` и поместите его в представление каталога Kudu hello в папке `/site/wwwroot/webapps`. Не перетаскивайте его toohello область «Перетащите. сюда tooupload "и" zip», так как Tomcat будет распакуйте его.
   
   ![][8]

В первом JSPHello.war отображается в области directory hello сама по себе:

  ![][9]

За короткий промежуток времени (возможно не более 5 минут) сервера Tomcat будет Распакуйте hello WAR-файл в распакованную JSPHello каталог. Щелкните hello КОРНЕВОЙ каталог toosee ли index.jsp была распаковываются и скопированных туда. Если Да, перейдите toosee directory задней toohello веб-приложений ли hello распаковать JSPHello создать каталог. Если эти элементы не отображаются, подождите, а затем повторите процедуру.

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a>Публикация приложения с помощью FileZilla (необязательно)
Другое средство, вы можете использовать приложение hello toopublish — FileZilla популярных FTP-клиент сторонних удобны, графический пользовательский интерфейс. Скачать и установить FileZilla можно на веб-сайте [http://filezilla-project.org/](http://filezilla-project.org/). Дополнительные сведения об использовании клиента hello см. в разделе hello [документации FileZilla](https://wiki.filezilla-project.org/Documentation) и на запись в блоге [клиентов FTP - часть 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).

1. В FileZilla щелкните **File > Site Manager** (Файл > Диспетчер сайтов).
2. В hello **диспетчер сайта** диалоговое окно, нажмите кнопку **новый сайт**. Новый пустой FTP-узел будет отображаться в **выберите запись** приглашением tooprovide имя. Укажите имя `AzureWebDemo-FTP`для использования в этой процедуре.
   
    На hello **Общие** укажите hello следующие параметры:
   
   * **Узел:** ввод hello **имя узла FTP** , скопированный из панели мониторинга hello.
   * **Порт:** (оставьте это поле оставить пустым, как это передачи пассивный и hello server определит порт toouse hello.)
   * **Протокол:** протокол передачи файлов FTP.
   * **Шифрование:** используйте простой FTP.
   * **Тип входа:** обычный.
   * **Пользователь:** ввод hello развертывания или FTP, скопированный из панели мониторинга hello пользователя. Это hello полное FTP имя пользователя, который имеет форму hello *webappname\username*.
   * **Пароль:** введите пароль hello, указанное при задании учетных данных развертывания hello.
     
     На hello **параметры передачи** выберите **пассивный**.
3. Щелкните **Подключить**. Если успешно, FileZilla элемента будет отображаться консоли `Status: Connected` сообщений и проблемы `LIST` команда содержимое каталога toolist hello.
4. В hello **локального** находится панель сайта выберите hello исходного каталога, в какой файл JSPHello.war hello; hello путь будет выглядеть аналогично toohello следующее:
   
    `<project-path>/JSPHello/src/`
5. В hello **удаленного** узла панели, выберите hello конечную папку. Будет развернут файл toohello hello WAR `webapps` каталог в корневом каталоге веб-приложения hello. Перейдите в слишком`/site/wwwroot`, щелкните правой кнопкой мыши `wwwroot`и выберите **создать каталог**. Имя каталога hello `webapps` и введите этот каталог.
6. Передача JSPHello.war слишком`/site/wwwroot/webapps`. Выберите JSPHello.war в hello **локального** список файлов, щелкните его правой кнопкой мыши и выберите **отправить**. Вы должны увидеть его в `/site/wwwroot/webapps`.
7. После копирования каталога веб-приложений toohello JSPHello.war сервера Tomcat будет автоматически распаковать (Распакуйте) hello файлы в hello WAR-файла. Хотя сервера Tomcat начинается немедленно при распаковке, может занять длительное время (возможно, часы) для tooappear файлы hello в клиенте hello FTP.

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a>Запустите приложение Hello World hello на hello веб-приложения
1. После отправки hello WAR-файл и проверить, что создал распакованы сервера Tomcat `JSPHello` каталога, Обзор слишком`http://webdemowebapp.azurewebsites.net/JSPHello` toorun приложения hello.
   
   > **Примечание:** при нажатии кнопки **Обзор** из классического портала hello, может появиться веб-страница по умолчанию hello, о том, «этого веб-приложения на основе Java успешно создан.» Может потребоваться toorefresh hello веб-страницы в порядок вывода приложения hello tooview вместо веб-страницы по умолчанию hello.
   > 
   > 
2. При запуске приложения hello, вы увидите веб-страницу с hello следующие выходные данные:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a>Очистка ресурсов Azure
Эта процедура создает веб-приложение службы приложений. Вам будет выставлен счет для hello ресурса при условии, что он существует. Если планируется использование hello веб-приложения для тестирования или разработки toocontinue, рассмотрите возможность остановки или удаления. За остановленное веб-приложение все равно взимается небольшая плата, зато его можно перезапустить в любое время. Удаление веб-приложения будут удалены все данные, отправленные tooit.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
