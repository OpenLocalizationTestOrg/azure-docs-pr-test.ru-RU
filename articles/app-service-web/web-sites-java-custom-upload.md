---
title: "aaaUpload пользовательского tooAzure приложения web Java"
description: "Этом учебнике показано, как tooupload пользовательские Java веб-приложения tooAzure веб-приложений служб приложений."
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
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a><span data-ttu-id="aeb0d-103">Отправка пользовательского tooAzure приложения web Java</span><span class="sxs-lookup"><span data-stu-id="aeb0d-103">Upload a custom Java web app tooAzure</span></span>
<span data-ttu-id="aeb0d-104">В этом разделе объясняется, как tooupload пользовательские Java веб-приложения слишком[службе приложений Azure] веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-104">This topic explains how tooupload a custom Java web app too[Azure App Service] Web Apps.</span></span> <span data-ttu-id="aeb0d-105">В состав входит информацию, которая применяется tooany Java веб-сайта или веб-приложения и также некоторые примеры для конкретных приложений.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-105">Included is information that applies tooany Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="aeb0d-106">Обратите внимание, что Azure предоставляет средства для создания веб-приложений Java, используя пользовательский Интерфейс для настройки портала Azure hello и hello Azure Marketplace, как описано в статье [Создание веб-приложения Java в службе приложений Azure](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aeb0d-106">Note that Azure provides a means for creating Java web apps using hello Azure Portal's configuration UI, and hello Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="aeb0d-107">Этот учебник предназначен для сценариев, в которых не требуется пользовательский Интерфейс конфигурации портала Azure hello toouse или hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-107">This tutorial is for scenarios in which you do not want toouse hello Azure Portal configuration UI or hello Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="aeb0d-108">Инструкции по настройке</span><span class="sxs-lookup"><span data-stu-id="aeb0d-108">Configuration guidelines</span></span>
<span data-ttu-id="aeb0d-109">Hello ниже описаны параметры hello, ожидаемый для пользовательских веб-приложений Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-109">hello following describes hello settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="aeb0d-110">динамически назначается Hello HTTP-порт, используемый hello процесса Java.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-110">hello HTTP port used by hello Java process is dynamically assigned.</span></span>  <span data-ttu-id="aeb0d-111">Hello процесс должен использовать порт hello из переменной среды hello `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-111">hello process must use hello port from hello environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="aeb0d-112">Все прослушивать порты Кроме hello один прослушиватель HTTP должен быть отключен.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-112">All listen ports other than hello single HTTP listener should be disabled.</span></span>  <span data-ttu-id="aeb0d-113">В Tomcat, который включает завершение hello, HTTPS и AJP портов.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-113">In Tomcat, that includes hello shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="aeb0d-114">контейнер Hello должен toobe настроен только для трафика IPv4.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-114">hello container needs toobe configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="aeb0d-115">Hello **запуска** команд для hello приложению toobe, заданными в конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-115">hello **startup** command for hello application needs toobe set in hello configuration.</span></span>
* <span data-ttu-id="aeb0d-116">Приложения, которым требуется разрешение на запись каталогов с помощью должны toobe, расположенный в каталоге содержимого hello Azure веб-приложения, который является **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-116">Applications that require directories with write permission need toobe located in hello Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="aeb0d-117">переменная среды Hello `HOME` ссылается tooD:\home.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-117">hello environmental variable `HOME` refers tooD:\home.</span></span>  

<span data-ttu-id="aeb0d-118">Переменные среды при необходимости можно задать в файле web.config hello.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-118">You can set environment variables as required in hello web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="aeb0d-119">Конфигурация httpPlatform в Web.config</span><span class="sxs-lookup"><span data-stu-id="aeb0d-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="aeb0d-120">Hello следующие данные описывают hello **httpPlatform** формат в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-120">hello following information describes hello **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="aeb0d-121">**arguments** (значение по умолчанию — "").</span><span class="sxs-lookup"><span data-stu-id="aeb0d-121">**arguments** (Default="").</span></span> <span data-ttu-id="aeb0d-122">Аргументы toohello исполняемый файл или сценарий, указанный в hello **processPath** параметр.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-122">Arguments toohello executable or script specified in hello **processPath** setting.</span></span>

<span data-ttu-id="aeb0d-123">Примеры (показаны с включенным **processPath** ):</span><span class="sxs-lookup"><span data-stu-id="aeb0d-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="aeb0d-124">**processPath** -toohello путь исполняемый файл или сценарий, который запускает процесс, прослушивающий для HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-124">**processPath** - Path toohello executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="aeb0d-125">Примеры:</span><span class="sxs-lookup"><span data-stu-id="aeb0d-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="aeb0d-126">**rapidFailsPerMinute** (значение по умолчанию — 10). Число вхождений hello процесс, указанный в **processPath** может быть toocrash в минуту.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-126">**rapidFailsPerMinute** (Default=10.) Number of times hello process specified in **processPath** is allowed toocrash per minute.</span></span> <span data-ttu-id="aeb0d-127">Если этот предел превышен, **HttpPlatformHandler** останавливает запуск процесса hello hello оставшейся части минуты hello.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching hello process for hello remainder of hello minute.</span></span>

<span data-ttu-id="aeb0d-128">**requestTimeout** (значение по умолчанию — "00:02:00"). Длительность, для которой **HttpPlatformHandler** будет ожидать ответа от процесса hello, прослушивающего `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from hello process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="aeb0d-129">**startupRetryCount** (значение по умолчанию — 10). Сколько раз **HttpPlatformHandler** попытается процесс toolaunch hello, указанный в **processPath**.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try toolaunch hello process specified in **processPath**.</span></span> <span data-ttu-id="aeb0d-130">Для получения дополнительных сведений ознакомьтесь с описанием **startupTimeLimit**.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="aeb0d-131">**startupTimeLimit** (значение по умолчанию — 10 секунд). Длительность, для которой **HttpPlatformHandler** будет ожидать hello исполняемый файл или сценарий toostart процесса, прослушивающего порт hello.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for hello executable/script toostart a process listening on hello port.</span></span>  <span data-ttu-id="aeb0d-132">При превышении этого предела **HttpPlatformHandler** будет прервать процесс hello и повторите toolaunch его еще раз **startupRetryCount** раз.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-132">If this time limit is exceeded, **HttpPlatformHandler** will kill hello process and try toolaunch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="aeb0d-133">**stdoutLogEnabled** (значение по умолчанию — "true"). Значение true, если **stdout** и **stderr** для hello процесс, указанный в hello **processPath** будет иметь значение toohello перенаправленный файл, указанный в  **stdoutLogFile** (см. **stdoutLogFile** раздел).</span><span class="sxs-lookup"><span data-stu-id="aeb0d-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for hello process specified in hello **processPath** setting will be redirected toohello file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="aeb0d-134">**stdoutLogFile** (значение по умолчанию — "d:\home\LogFiles\httpPlatformStdout.log"). Абсолютный путь к файлу для которого **stdout** и **stderr** из процесса hello, указанный в **processPath** будут регистрироваться.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from hello process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="aeb0d-135">`%HTTP_PLATFORM_PORT%`— Это специальный заполнитель, либо как часть должна toospecified **аргументы** или как часть hello **httpPlatform** **переменных среды** списка.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs toospecified either as part of **arguments** or as part of hello **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="aeb0d-136">Это будет заменен портом внутренними по **HttpPlatformHandler** , чтобы процесс hello заданные **processPath** мог прослушивать этот порт.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that hello process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="aeb0d-137">Развертывание</span><span class="sxs-lookup"><span data-stu-id="aeb0d-137">Deployment</span></span>
<span data-ttu-id="aeb0d-138">Веб-приложений на основе Java можно легко развернуть с помощью большинство означает приветствия, которые используются с hello Internet Information Services (IIS) на основе веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-138">Java based web apps can be deployed easily through most of hello same means that are used with hello Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="aeb0d-139">FTP, Git и Kudu все поддерживаются в качестве методов развертывания, как является встроенной функции SCM для веб-приложения "hello".</span><span class="sxs-lookup"><span data-stu-id="aeb0d-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is hello integrated SCM capability for web apps.</span></span> <span data-ttu-id="aeb0d-140">WebDeploy работает как протокол, однако, поскольку код Java разрабатывается не в Visual Studio, WebDeploy не подходит для развертывания веб-приложений Java.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="aeb0d-141">Примеры конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="aeb0d-141">Application configuration Examples</span></span>
<span data-ttu-id="aeb0d-142">Для следующих приложений, файл web.config и hello hello конфигурации приложения предоставляется как примеры tooshow как tooenable приложение Java на веб-приложений служб приложений.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-142">For hello following applications, a web.config file and hello application configuration is provided as examples tooshow how tooenable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="aeb0d-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="aeb0d-143">Tomcat</span></span>
<span data-ttu-id="aeb0d-144">Хотя существует две разновидности Tomcat, поставляемые с веб-приложений служб приложений, она по-прежнему вполне возможно, что tooupload клиента конкретные экземпляры.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible tooupload customer specific instances.</span></span> <span data-ttu-id="aeb0d-145">Ниже приведен пример установки Tomcat с другой виртуальной машиной Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="aeb0d-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

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
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="aeb0d-146">На hello Tomcat стороны существует несколько необходимые toobe внесены изменения в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-146">On hello Tomcat side, there are a few configuration changes that need toobe made.</span></span> <span data-ttu-id="aeb0d-147">Hello server.xml требуется изменить toobe tooset:</span><span class="sxs-lookup"><span data-stu-id="aeb0d-147">hello server.xml needs toobe edited tooset:</span></span>

* <span data-ttu-id="aeb0d-148">Порт завершения работы = -1.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-148">Shutdown port = -1</span></span>
* <span data-ttu-id="aeb0d-149">Порт соединителя HTTP = {port.http}.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="aeb0d-150">Адрес соединителя HTTP = "127.0.0.1".</span><span class="sxs-lookup"><span data-stu-id="aeb0d-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="aeb0d-151">Закомментируйте соединители HTTPS и AJP.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="aeb0d-152">параметр Hello IPv4 можно также задать в файле catalina.properties hello, где можно добавить`java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="aeb0d-152">hello IPv4 setting can also be set in hello catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="aeb0d-153">Вызовы Direct3d в веб-приложениях службы приложений не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="aeb0d-154">toodisable, добавьте следующий параметр Java приложения следует такие вызовы hello:`-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="aeb0d-154">toodisable those, add hello following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="aeb0d-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="aeb0d-155">Jetty</span></span>
<span data-ttu-id="aeb0d-156">Как hello случае для Tomcat, клиентам можно отправить свои собственные экземпляры для Jetty.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-156">As is hello case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="aeb0d-157">В случае выполнения hello полной установки Jetty hello hello конфигурация будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="aeb0d-157">In hello case of running hello full install of Jetty, hello configuration would look like this:</span></span>

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

<span data-ttu-id="aeb0d-158">Hello конфигурацию Jetty должен toobe колебаниями hello start.ini tooset `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-158">hello Jetty configuration needs toobe changed in hello start.ini tooset `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="aeb0d-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="aeb0d-159">Springboot</span></span>
<span data-ttu-id="aeb0d-160">В порядке tooget Springboot приложения, под управлением tooupload файл JAR или ВОЙНЫ и добавьте следующие файл web.config hello.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-160">In order tooget a Springboot application running you need tooupload your JAR or WAR file and add hello following web.config file.</span></span> <span data-ttu-id="aeb0d-161">файл web.config Hello попадают в папку wwwroot hello.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-161">hello web.config file goes into hello wwwroot folder.</span></span> <span data-ttu-id="aeb0d-162">В файле web.config hello Настройка hello аргументы toopoint tooyour JAR-файл, в hello следующий пример hello JAR-файл находится в папке wwwroot hello также.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-162">In hello web.config adjust hello arguments toopoint tooyour JAR file, in hello following example hello JAR file is located in hello wwwroot folder as well.</span></span>  

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


### <a name="hudson"></a><span data-ttu-id="aeb0d-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="aeb0d-163">Hudson</span></span>
<span data-ttu-id="aeb0d-164">Наш тест используется hello Hudson 3.1.2 war и hello Tomcat 7.0.50 экземпляр по умолчанию, но без использования действия tooset hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-164">Our test used hello Hudson 3.1.2 war and hello default Tomcat 7.0.50 instance but without using hello UI tooset things up.</span></span>  <span data-ttu-id="aeb0d-165">Поскольку Hudson — это программное средство построения, это желательно tooinstall ее на выделенный экземпляров, где hello **AlwaysOn** флаг можно установить на веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-165">Because Hudson is a software build tool, it is advised tooinstall it on dedicated instances where hello **AlwaysOn** flag can be set on hello web app.</span></span>

1. <span data-ttu-id="aeb0d-166">В корневом каталоге веб-приложения, например **d:\home\site\wwwroot**, создайте каталог **webapps** (если он отсутствует) и поместите файл Hudson.war в каталог **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="aeb0d-167">Скачайте инструмент apache maven 3.0.5 (совместимый с Hudson) и поместите его в каталог **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="aeb0d-168">Создайте файл web.config в **d:\home\site\wwwroot** и вставить hello согласно содержимому:</span><span class="sxs-lookup"><span data-stu-id="aeb0d-168">Create web.config in **d:\home\site\wwwroot** and paste hello following contents in it:</span></span>
   
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
   
    <span data-ttu-id="aeb0d-169">На этом этапе hello веб-приложения может быть перезапущен tootake hello изменения.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-169">At this point hello web app can be restarted tootake hello changes.</span></span>  <span data-ttu-id="aeb0d-170">Подключите toohttp://yourwebapp/hudson toostart Hudson.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-170">Connect toohttp://yourwebapp/hudson toostart Hudson.</span></span>
4. <span data-ttu-id="aeb0d-171">После Hudson настраивается, появится следующий экран приветствия:</span><span class="sxs-lookup"><span data-stu-id="aeb0d-171">After Hudson configures itself, you should see hello following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="aeb0d-173">Hello доступа к странице конфигурации Hudson: щелкните **управление Hudson**и нажмите кнопку **Настройка системы**.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-173">Access hello Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="aeb0d-174">Настройте hello JDK, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="aeb0d-174">Configure hello JDK as shown below:</span></span>
   
    ![Конфигурация Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="aeb0d-176">Настройте Maven, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-176">Configure Maven as shown below:</span></span>
   
    ![Конфигурация Maven](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="aeb0d-178">Сохраните параметры hello.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-178">Save hello settings.</span></span> <span data-ttu-id="aeb0d-179">Теперь продукт Hudson должен быть настроен и готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="aeb0d-180">Дополнительные сведения о Hudson см. на сайте [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="aeb0d-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="aeb0d-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="aeb0d-181">Liferay</span></span>
<span data-ttu-id="aeb0d-182">Liferay поддерживается в веб-приложениях службы приложений.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="aeb0d-183">Поскольку Liferay может потребоваться значительный объем, веб-приложения hello должен toorun в средних и крупных выделенный рабочий процесс, который может обеспечить достаточный объем памяти.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-183">Since Liferay can require significant memory, hello web app needs toorun on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="aeb0d-184">Liferay занимает несколько минут toostart.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-184">Liferay also takes several minutes toostart up.</span></span> <span data-ttu-id="aeb0d-185">По этой причине рекомендуется установить веб-приложение hello слишком**Always On**.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-185">For that reason, it is recommended that you set hello web app too**Always On**.</span></span>  

<span data-ttu-id="aeb0d-186">С помощью Liferay 6.1.2, объединенными Community Edition GA3 Tomcat, hello следующие файлы были изменены после загрузки Liferay:</span><span class="sxs-lookup"><span data-stu-id="aeb0d-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, hello following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="aeb0d-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="aeb0d-187">**Server.xml**</span></span>

* <span data-ttu-id="aeb0d-188">Измените завершении работы порта слишком-1.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-188">Change Shutdown port too-1.</span></span>
* <span data-ttu-id="aeb0d-189">Изменение соединителя HTTP слишком`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="aeb0d-189">Change HTTP connector too       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="aeb0d-190">Закомментируйте hello AJP соединителя.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-190">Comment out hello AJP connector.</span></span>

<span data-ttu-id="aeb0d-191">В hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** папки, создайте файл с именем **ext.properties портала**.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-191">In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="aeb0d-192">Этот файл должен toocontain одну строку, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="aeb0d-192">This file needs toocontain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="aeb0d-193">В hello же уровне каталога, что и папка hello tomcat 7.0.40 создать файл с именем **web.config** с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="aeb0d-193">At hello same directory level as hello tomcat-7.0.40 folder, create a file named **web.config** with hello following content:</span></span>

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

<span data-ttu-id="aeb0d-194">В разделе hello **httpPlatform** блок hello **requestTimeout** задано слишком "00: 10:00».</span><span class="sxs-lookup"><span data-stu-id="aeb0d-194">Under hello **httpPlatform** block, hello **requestTimeout** is set too“00:10:00”.</span></span>  <span data-ttu-id="aeb0d-195">Можно сократить, но то, скорее всего, toosee некоторые ошибки времени ожидания при Liferay начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-195">It can be reduced but then you are likely toosee some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="aeb0d-196">Если это значение изменяется, затем hello **connectionTimeout** в hello tomcat server.xml также может изменяться.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-196">If this value is changed, then hello **connectionTimeout** in hello tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="aeb0d-197">Стоит отметить, что varariable среде JRE_HOME hello указывается в hello выше web.config toopoint toohello JDK 64-разрядной.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-197">It is worth noting that hello JRE_HOME environnment varariable is specified in hello above web.config toopoint toohello 64-bit JDK.</span></span> <span data-ttu-id="aeb0d-198">по умолчанию Hello 32 бита, но поскольку Liferay может потребоваться высокая памяти, рекомендуется toouse hello JDK 64-разрядной.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-198">hello default is 32-bit, but since Liferay may require high levels of memory, it is recommended toouse hello 64-bit JDK.</span></span>

<span data-ttu-id="aeb0d-199">После внесения этих изменений перезапустите веб-сайт с Liferay, а затем откройте адрес http://ваше_веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="aeb0d-200">портал Liferay Hello доступен из корня приложения hello web.</span><span class="sxs-lookup"><span data-stu-id="aeb0d-200">hello Liferay portal is available from hello web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="aeb0d-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aeb0d-201">Next steps</span></span>
<span data-ttu-id="aeb0d-202">Дополнительные сведения о Liferay см. на сайте [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="aeb0d-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="aeb0d-203">Дополнительные сведения о Java см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).</span><span class="sxs-lookup"><span data-stu-id="aeb0d-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[службе приложений Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
