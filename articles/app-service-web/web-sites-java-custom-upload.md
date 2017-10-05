---
title: "Отправка пользовательского веб-приложения Java в Azure"
description: "В этом учебнике объясняется, как отправить пользовательское веб-приложение Java в веб-приложения службы приложений Azure."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 9c8f9ee7780859f7640ac82d6ebce85082170ad7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-custom-java-web-app-to-azure"></a><span data-ttu-id="17e2a-103">Отправка пользовательского веб-приложения Java в Azure</span><span class="sxs-lookup"><span data-stu-id="17e2a-103">Upload a custom Java web app to Azure</span></span>
<span data-ttu-id="17e2a-104">В этом разделе объясняется, как отправить пользовательское веб-приложение Java в веб-приложения [службы приложений Azure] .</span><span class="sxs-lookup"><span data-stu-id="17e2a-104">This topic explains how to upload a custom Java web app to [Azure App Service] Web Apps.</span></span> <span data-ttu-id="17e2a-105">Информация, приведенная здесь, применима к любому веб-сайту или веб-приложению Java, также даны несколько примеров для конкретных приложений.</span><span class="sxs-lookup"><span data-stu-id="17e2a-105">Included is information that applies to any Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="17e2a-106">Обратите внимание, что Azure предоставляет средства для создания веб-приложений Java с помощью пользовательского интерфейса настройки портала Azure, как описано в разделе [Создание веб-приложения Java в службе приложений Azure](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="17e2a-106">Note that Azure provides a means for creating Java web apps using the Azure Portal's configuration UI, and the Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="17e2a-107">Этот учебник предназначен для ситуаций, в которых не требуется использовать пользовательский интерфейс настройки портала Azure или Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="17e2a-107">This tutorial is for scenarios in which you do not want to use the Azure Portal configuration UI or the Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="17e2a-108">Инструкции по настройке</span><span class="sxs-lookup"><span data-stu-id="17e2a-108">Configuration guidelines</span></span>
<span data-ttu-id="17e2a-109">Ниже описаны параметры, которые следует задать для пользовательских веб-приложений Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="17e2a-109">The following describes the settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="17e2a-110">HTTP-порт, используемый процессом Java, назначается динамически.</span><span class="sxs-lookup"><span data-stu-id="17e2a-110">The HTTP port used by the Java process is dynamically assigned.</span></span>  <span data-ttu-id="17e2a-111">Процесс должен использовать порт из переменной среды `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="17e2a-111">The process must use the port from the environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="17e2a-112">Все прослушивающие порты, кроме одного прослушивателя HTTP, должны быть отключены.</span><span class="sxs-lookup"><span data-stu-id="17e2a-112">All listen ports other than the single HTTP listener should be disabled.</span></span>  <span data-ttu-id="17e2a-113">В Tomcat сюда относятся порты завершения работы, HTTPS и AJP.</span><span class="sxs-lookup"><span data-stu-id="17e2a-113">In Tomcat, that includes the shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="17e2a-114">Контейнер должен быть настроен на использование исключительно трафика IPv4.</span><span class="sxs-lookup"><span data-stu-id="17e2a-114">The container needs to be configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="17e2a-115">В конфигурации для приложения необходимо задать команду **startup** .</span><span class="sxs-lookup"><span data-stu-id="17e2a-115">The **startup** command for the application needs to be set in the configuration.</span></span>
* <span data-ttu-id="17e2a-116">Приложения, которым требуются каталоги с разрешением на запись, должны находиться в каталоге контента веб-приложения Azure, которым является каталог **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="17e2a-116">Applications that require directories with write permission need to be located in the Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="17e2a-117">Переменная среды `HOME` ссылается на D:\home.</span><span class="sxs-lookup"><span data-stu-id="17e2a-117">The environmental variable `HOME` refers to D:\home.</span></span>  

<span data-ttu-id="17e2a-118">При необходимости можно задать переменные среды в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="17e2a-118">You can set environment variables as required in the web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="17e2a-119">Конфигурация httpPlatform в Web.config</span><span class="sxs-lookup"><span data-stu-id="17e2a-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="17e2a-120">Ниже приведена информация о формате **httpPlatform** , используемом в web.config.</span><span class="sxs-lookup"><span data-stu-id="17e2a-120">The following information describes the **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="17e2a-121">**arguments** (значение по умолчанию — "").</span><span class="sxs-lookup"><span data-stu-id="17e2a-121">**arguments** (Default="").</span></span> <span data-ttu-id="17e2a-122">Аргументы для исполняемого файла или скрипта, указанного в параметре **processPath** .</span><span class="sxs-lookup"><span data-stu-id="17e2a-122">Arguments to the executable or script specified in the **processPath** setting.</span></span>

<span data-ttu-id="17e2a-123">Примеры (показаны с включенным **processPath** ):</span><span class="sxs-lookup"><span data-stu-id="17e2a-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="17e2a-124">**processPath** — путь к исполняемому файлу или скрипту, который запустит процесс прослушивания для HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="17e2a-124">**processPath** - Path to the executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="17e2a-125">Примеры:</span><span class="sxs-lookup"><span data-stu-id="17e2a-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="17e2a-126">**rapidFailsPerMinute** (значение по умолчанию — 10). Допустимое количество сбоев в минуту для процесса, указанного в **processPath**.</span><span class="sxs-lookup"><span data-stu-id="17e2a-126">**rapidFailsPerMinute** (Default=10.) Number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="17e2a-127">Если этот предел превышен, **HttpPlatformHandler** остановит запуск процесса в течение оставшейся части минуты.</span><span class="sxs-lookup"><span data-stu-id="17e2a-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching the process for the remainder of the minute.</span></span>

<span data-ttu-id="17e2a-128">**requestTimeout** (значение по умолчанию — "00:02:00"). Период ожидания **HttpPlatformHandler** ответа от процесса, прослушивающего `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="17e2a-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from the process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="17e2a-129">**startupRetryCount** (значение по умолчанию — 10). Допустимое число попыток **HttpPlatformHandler** запустить процесс, указанный в **processPath**.</span><span class="sxs-lookup"><span data-stu-id="17e2a-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try to launch the process specified in **processPath**.</span></span> <span data-ttu-id="17e2a-130">Для получения дополнительных сведений ознакомьтесь с описанием **startupTimeLimit**.</span><span class="sxs-lookup"><span data-stu-id="17e2a-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="17e2a-131">**startupTimeLimit** (значение по умолчанию — 10 секунд). Период ожидания **HttpPlatformHandler** запуска исполняемым файлом или сценарием процесса прослушивания порта.</span><span class="sxs-lookup"><span data-stu-id="17e2a-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for the executable/script to start a process listening on the port.</span></span>  <span data-ttu-id="17e2a-132">Если этот предел достигнут, **HttpPlatformHandler** завершает этот процесс и пробует запустить его столько раз, сколько указано в **startupRetryCount**.</span><span class="sxs-lookup"><span data-stu-id="17e2a-132">If this time limit is exceeded, **HttpPlatformHandler** will kill the process and try to launch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="17e2a-133">**stdoutLogEnabled** (значение по умолчанию — "true"). Если значение равно true, то **stdout** и **stderr** для процесса, указанного в параметре **processPath**, будут перенаправлены в файл, указанный в **stdoutLogFile** (ознакомьтесь с разделом **stdoutLogFile**).</span><span class="sxs-lookup"><span data-stu-id="17e2a-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for the process specified in the **processPath** setting will be redirected to the file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="17e2a-134">**stdoutLogFile** (значение по умолчанию — "d:\home\LogFiles\httpPlatformStdout.log"). Абсолютный путь к файлу, для которого будет вестись журнал **stdout** и **stderr** из процесса, указанного в **processPath**.</span><span class="sxs-lookup"><span data-stu-id="17e2a-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from the process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="17e2a-135">`%HTTP_PLATFORM_PORT%` — специальный заполнитель, который должен быть указан как часть **arguments** или как часть списка **httpPlatform** **environmentVariables**.</span><span class="sxs-lookup"><span data-stu-id="17e2a-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs to specified either as part of **arguments** or as part of the **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="17e2a-136">**HttpPlatformHandler** заменит это значение на сформированный системой порт, чтобы указанный в **processPath** процесс мог прослушивать этот порт.</span><span class="sxs-lookup"><span data-stu-id="17e2a-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that the process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="17e2a-137">Развертывание</span><span class="sxs-lookup"><span data-stu-id="17e2a-137">Deployment</span></span>
<span data-ttu-id="17e2a-138">Веб-приложения на основе Java можно легко развернуть с помощью большинства средств, которые используются для веб-приложений на основе служб IIS.</span><span class="sxs-lookup"><span data-stu-id="17e2a-138">Java based web apps can be deployed easily through most of the same means that are used with the Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="17e2a-139">Полностью поддерживаются механизмы развертывания FTP, Git и Kudu, а также встроенная функция SCM для веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="17e2a-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is the integrated SCM capability for web apps.</span></span> <span data-ttu-id="17e2a-140">WebDeploy работает как протокол, однако, поскольку код Java разрабатывается не в Visual Studio, WebDeploy не подходит для развертывания веб-приложений Java.</span><span class="sxs-lookup"><span data-stu-id="17e2a-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="17e2a-141">Примеры конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="17e2a-141">Application configuration Examples</span></span>
<span data-ttu-id="17e2a-142">Для следующих приложений в качестве примера приводится файл web.config и конфигурация приложения, чтобы показать, как обеспечить работу приложений Java в веб-приложениях службы приложений.</span><span class="sxs-lookup"><span data-stu-id="17e2a-142">For the following applications, a web.config file and the application configuration is provided as examples to show how to enable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="17e2a-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="17e2a-143">Tomcat</span></span>
<span data-ttu-id="17e2a-144">Хотя существует два варианта Tomcat, поставляемых с веб-приложениями службы приложений, по-прежнему доступна возможность отправки экземпляров, настроенных для определенного клиента.</span><span class="sxs-lookup"><span data-stu-id="17e2a-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible to upload customer specific instances.</span></span> <span data-ttu-id="17e2a-145">Ниже приведен пример установки Tomcat с другой виртуальной машиной Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="17e2a-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default to %programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="17e2a-146">На стороне Tomcat необходимо внести несколько изменений в конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="17e2a-146">On the Tomcat side, there are a few configuration changes that need to be made.</span></span> <span data-ttu-id="17e2a-147">В server.xml необходимо задать следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="17e2a-147">The server.xml needs to be edited to set:</span></span>

* <span data-ttu-id="17e2a-148">Порт завершения работы = -1.</span><span class="sxs-lookup"><span data-stu-id="17e2a-148">Shutdown port = -1</span></span>
* <span data-ttu-id="17e2a-149">Порт соединителя HTTP = {port.http}.</span><span class="sxs-lookup"><span data-stu-id="17e2a-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="17e2a-150">Адрес соединителя HTTP = "127.0.0.1".</span><span class="sxs-lookup"><span data-stu-id="17e2a-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="17e2a-151">Закомментируйте соединители HTTPS и AJP.</span><span class="sxs-lookup"><span data-stu-id="17e2a-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="17e2a-152">Параметр IPv4 можно также задать в файле catalina.properties, добавив в него `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="17e2a-152">The IPv4 setting can also be set in the catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="17e2a-153">Вызовы Direct3d в веб-приложениях службы приложений не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="17e2a-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="17e2a-154">Если ваше приложение выполняет такие вызовы, то для их отключения добавьте следующий параметр Java: `-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="17e2a-154">To disable those, add the following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="17e2a-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="17e2a-155">Jetty</span></span>
<span data-ttu-id="17e2a-156">Как в случае с Tomcat, клиенты могут отправлять собственные экземпляры для Jetty.</span><span class="sxs-lookup"><span data-stu-id="17e2a-156">As is the case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="17e2a-157">Если выполняется полная установка Jetty, конфигурация будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="17e2a-157">In the case of running the full install of Jetty, the configuration would look like this:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="17e2a-158">Необходимо изменить конфигурацию Jetty в файле start.ini, чтобы задать `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="17e2a-158">The Jetty configuration needs to be changed in the start.ini to set `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="17e2a-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="17e2a-159">Springboot</span></span>
<span data-ttu-id="17e2a-160">Чтобы запустить приложение Springboot, необходимо отправить JAR- или WAR-файл и добавить следующий файл web.config.</span><span class="sxs-lookup"><span data-stu-id="17e2a-160">In order to get a Springboot application running you need to upload your JAR or WAR file and add the following web.config file.</span></span> <span data-ttu-id="17e2a-161">Файл web.config необходимо поместить в папку wwwroot.</span><span class="sxs-lookup"><span data-stu-id="17e2a-161">The web.config file goes into the wwwroot folder.</span></span> <span data-ttu-id="17e2a-162">Настройте аргументы в файле web.config, чтобы он указывал на JAR-файл. В следующем примере JAR-файл также расположен в папке wwwroot.</span><span class="sxs-lookup"><span data-stu-id="17e2a-162">In the web.config adjust the arguments to point to your JAR file, in the following example the JAR file is located in the wwwroot folder as well.</span></span>  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a><span data-ttu-id="17e2a-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="17e2a-163">Hudson</span></span>
<span data-ttu-id="17e2a-164">В нашем тесте использовался WAR-файл Hudson 3.1.2 и экземпляр Tomcat 7.0.50 по умолчанию, но не использовался пользовательский интерфейс настройки.</span><span class="sxs-lookup"><span data-stu-id="17e2a-164">Our test used the Hudson 3.1.2 war and the default Tomcat 7.0.50 instance but without using the UI to set things up.</span></span>  <span data-ttu-id="17e2a-165">Поскольку Hudson представляет собой средство построения программного обеспечения, рекомендуется установить его на выделенных экземплярах, где в веб-приложении можно установить флаг **AlwaysOn** .</span><span class="sxs-lookup"><span data-stu-id="17e2a-165">Because Hudson is a software build tool, it is advised to install it on dedicated instances where the **AlwaysOn** flag can be set on the web app.</span></span>

1. <span data-ttu-id="17e2a-166">В корневом каталоге веб-приложения, например **d:\home\site\wwwroot**, создайте каталог **webapps** (если он отсутствует) и поместите файл Hudson.war в каталог **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="17e2a-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="17e2a-167">Скачайте инструмент apache maven 3.0.5 (совместимый с Hudson) и поместите его в каталог **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="17e2a-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="17e2a-168">Создайте файл web.config в каталоге **d:\home\site\wwwroot** и вставьте в него следующее содержимое.</span><span class="sxs-lookup"><span data-stu-id="17e2a-168">Create web.config in **d:\home\site\wwwroot** and paste the following contents in it:</span></span>
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    <span data-ttu-id="17e2a-169">На данном этапе можно перезапустить веб-приложение для вступления изменений в силу.</span><span class="sxs-lookup"><span data-stu-id="17e2a-169">At this point the web app can be restarted to take the changes.</span></span>  <span data-ttu-id="17e2a-170">Подключитесь к узлу http://ваше_веб-приложение/hudson для запуска Hudson.</span><span class="sxs-lookup"><span data-stu-id="17e2a-170">Connect to http://yourwebapp/hudson to start Hudson.</span></span>
4. <span data-ttu-id="17e2a-171">После самонастройки Hudson должен появиться следующий экран:</span><span class="sxs-lookup"><span data-stu-id="17e2a-171">After Hudson configures itself, you should see the following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="17e2a-173">Перейдите на страницу конфигурации Hudson: выберите **Manage Hudson** (Управление Hudson) и щелкните **Configure System** (Настройка системы).</span><span class="sxs-lookup"><span data-stu-id="17e2a-173">Access the Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="17e2a-174">Настройте JDK, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="17e2a-174">Configure the JDK as shown below:</span></span>
   
    ![Конфигурация Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="17e2a-176">Настройте Maven, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="17e2a-176">Configure Maven as shown below:</span></span>
   
    ![Конфигурация Maven](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="17e2a-178">Сохраните параметры.</span><span class="sxs-lookup"><span data-stu-id="17e2a-178">Save the settings.</span></span> <span data-ttu-id="17e2a-179">Теперь продукт Hudson должен быть настроен и готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="17e2a-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="17e2a-180">Дополнительные сведения о Hudson см. на сайте [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="17e2a-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="17e2a-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="17e2a-181">Liferay</span></span>
<span data-ttu-id="17e2a-182">Liferay поддерживается в веб-приложениях службы приложений.</span><span class="sxs-lookup"><span data-stu-id="17e2a-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="17e2a-183">Поскольку для работы Liferay может потребоваться значительный объем памяти, веб-приложение должно выполняться в выделенном рабочем процессе среднего или крупного размера, который может предоставить достаточный объем памяти.</span><span class="sxs-lookup"><span data-stu-id="17e2a-183">Since Liferay can require significant memory, the web app needs to run on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="17e2a-184">Запуск Liferay занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="17e2a-184">Liferay also takes several minutes to start up.</span></span> <span data-ttu-id="17e2a-185">По этой причине рекомендуется установить для веб-приложения значение **Всегда включено**.</span><span class="sxs-lookup"><span data-stu-id="17e2a-185">For that reason, it is recommended that you set the web app to **Always On**.</span></span>  

<span data-ttu-id="17e2a-186">После загрузки Liferay следующие файлы были изменены с помощью Liferay 6.1.2 Community Edition GA3 из одного пакета с Tomcat:</span><span class="sxs-lookup"><span data-stu-id="17e2a-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, the following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="17e2a-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="17e2a-187">**Server.xml**</span></span>

* <span data-ttu-id="17e2a-188">Измените порт завершения работы на -1.</span><span class="sxs-lookup"><span data-stu-id="17e2a-188">Change Shutdown port to -1.</span></span>
* <span data-ttu-id="17e2a-189">Измените соединитель HTTP на такой: `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="17e2a-189">Change HTTP connector to       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="17e2a-190">Закомментируйте соединитель AJP.</span><span class="sxs-lookup"><span data-stu-id="17e2a-190">Comment out the AJP connector.</span></span>

<span data-ttu-id="17e2a-191">В папке **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** создайте файл **portal-ext.properties**.</span><span class="sxs-lookup"><span data-stu-id="17e2a-191">In the **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="17e2a-192">Этот файл должен содержать одну строку, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="17e2a-192">This file needs to contain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="17e2a-193">На том же уровне структуры каталогов, где находится папка tomcat-7.0.40, создайте файл с именем **web.config** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="17e2a-193">At the same directory level as the tomcat-7.0.40 folder, create a file named **web.config** with the following content:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="17e2a-194">В разделе **httpPlatform** для параметра **requestTimeout** задано значение "00:10:00".</span><span class="sxs-lookup"><span data-stu-id="17e2a-194">Under the **httpPlatform** block, the **requestTimeout** is set to “00:10:00”.</span></span>  <span data-ttu-id="17e2a-195">Его можно уменьшить, однако в этом случае повышается вероятность возникновения ошибок времени ожидания при начальной загрузке Liferay.</span><span class="sxs-lookup"><span data-stu-id="17e2a-195">It can be reduced but then you are likely to see some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="17e2a-196">При изменении этого значения следует также изменить параметр **connectionTimeout** в файле server.xml на стороне tomcat.</span><span class="sxs-lookup"><span data-stu-id="17e2a-196">If this value is changed, then the **connectionTimeout** in the tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="17e2a-197">Следует отметить, что переменная среды JRE_HOME в приведенном выше файле web.config указывает на 64-разрядную версию JDK.</span><span class="sxs-lookup"><span data-stu-id="17e2a-197">It is worth noting that the JRE_HOME environnment varariable is specified in the above web.config to point to the 64-bit JDK.</span></span> <span data-ttu-id="17e2a-198">По умолчанию используется 32-разрядная версия, но поскольку Liferay может потребоваться большой объем памяти, рекомендуется использовать 64-разрядную версию JDK.</span><span class="sxs-lookup"><span data-stu-id="17e2a-198">The default is 32-bit, but since Liferay may require high levels of memory, it is recommended to use the 64-bit JDK.</span></span>

<span data-ttu-id="17e2a-199">После внесения этих изменений перезапустите веб-сайт с Liferay, а затем откройте адрес http://ваше_веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="17e2a-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="17e2a-200">Портал Liferay доступен из корневого каталога веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="17e2a-200">The Liferay portal is available from the web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="17e2a-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17e2a-201">Next steps</span></span>
<span data-ttu-id="17e2a-202">Дополнительные сведения о Liferay см. на сайте [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="17e2a-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="17e2a-203">Дополнительные сведения о Java см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).</span><span class="sxs-lookup"><span data-stu-id="17e2a-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[службы приложений Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
