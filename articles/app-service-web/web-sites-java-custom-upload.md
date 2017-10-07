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
# <a name="upload-a-custom-java-web-app-tooazure"></a>Отправка пользовательского tooAzure приложения web Java
В этом разделе объясняется, как tooupload пользовательские Java веб-приложения слишком[службе приложений Azure] веб-приложений. В состав входит информацию, которая применяется tooany Java веб-сайта или веб-приложения и также некоторые примеры для конкретных приложений.

Обратите внимание, что Azure предоставляет средства для создания веб-приложений Java, используя пользовательский Интерфейс для настройки портала Azure hello и hello Azure Marketplace, как описано в статье [Создание веб-приложения Java в службе приложений Azure](web-sites-java-get-started.md). Этот учебник предназначен для сценариев, в которых не требуется пользовательский Интерфейс конфигурации портала Azure hello toouse или hello Azure Marketplace.  

## <a name="configuration-guidelines"></a>Инструкции по настройке
Hello ниже описаны параметры hello, ожидаемый для пользовательских веб-приложений Java в Azure.

* динамически назначается Hello HTTP-порт, используемый hello процесса Java.  Hello процесс должен использовать порт hello из переменной среды hello `HTTP_PLATFORM_PORT`.
* Все прослушивать порты Кроме hello один прослушиватель HTTP должен быть отключен.  В Tomcat, который включает завершение hello, HTTPS и AJP портов.
* контейнер Hello должен toobe настроен только для трафика IPv4.
* Hello **запуска** команд для hello приложению toobe, заданными в конфигурации hello.
* Приложения, которым требуется разрешение на запись каталогов с помощью должны toobe, расположенный в каталоге содержимого hello Azure веб-приложения, который является **D:\home**.  переменная среды Hello `HOME` ссылается tooD:\home.  

Переменные среды при необходимости можно задать в файле web.config hello.

## <a name="webconfig-httpplatform-configuration"></a>Конфигурация httpPlatform в Web.config
Hello следующие данные описывают hello **httpPlatform** формат в файле web.config.

**arguments** (значение по умолчанию — ""). Аргументы toohello исполняемый файл или сценарий, указанный в hello **processPath** параметр.

Примеры (показаны с включенным **processPath** ):

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -toohello путь исполняемый файл или сценарий, который запускает процесс, прослушивающий для HTTP-запросов.

Примеры:

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute** (значение по умолчанию — 10). Число вхождений hello процесс, указанный в **processPath** может быть toocrash в минуту. Если этот предел превышен, **HttpPlatformHandler** останавливает запуск процесса hello hello оставшейся части минуты hello.

**requestTimeout** (значение по умолчанию — "00:02:00"). Длительность, для которой **HttpPlatformHandler** будет ожидать ответа от процесса hello, прослушивающего `%HTTP_PLATFORM_PORT%`.

**startupRetryCount** (значение по умолчанию — 10). Сколько раз **HttpPlatformHandler** попытается процесс toolaunch hello, указанный в **processPath**. Для получения дополнительных сведений ознакомьтесь с описанием **startupTimeLimit**.

**startupTimeLimit** (значение по умолчанию — 10 секунд). Длительность, для которой **HttpPlatformHandler** будет ожидать hello исполняемый файл или сценарий toostart процесса, прослушивающего порт hello.  При превышении этого предела **HttpPlatformHandler** будет прервать процесс hello и повторите toolaunch его еще раз **startupRetryCount** раз.

**stdoutLogEnabled** (значение по умолчанию — "true"). Значение true, если **stdout** и **stderr** для hello процесс, указанный в hello **processPath** будет иметь значение toohello перенаправленный файл, указанный в  **stdoutLogFile** (см. **stdoutLogFile** раздел).

**stdoutLogFile** (значение по умолчанию — "d:\home\LogFiles\httpPlatformStdout.log"). Абсолютный путь к файлу для которого **stdout** и **stderr** из процесса hello, указанный в **processPath** будут регистрироваться.

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`— Это специальный заполнитель, либо как часть должна toospecified **аргументы** или как часть hello **httpPlatform** **переменных среды** списка. Это будет заменен портом внутренними по **HttpPlatformHandler** , чтобы процесс hello заданные **processPath** мог прослушивать этот порт.
> 
> 

## <a name="deployment"></a>Развертывание
Веб-приложений на основе Java можно легко развернуть с помощью большинство означает приветствия, которые используются с hello Internet Information Services (IIS) на основе веб-приложений.  FTP, Git и Kudu все поддерживаются в качестве методов развертывания, как является встроенной функции SCM для веб-приложения "hello". WebDeploy работает как протокол, однако, поскольку код Java разрабатывается не в Visual Studio, WebDeploy не подходит для развертывания веб-приложений Java.

## <a name="application-configuration-examples"></a>Примеры конфигурации приложений
Для следующих приложений, файл web.config и hello hello конфигурации приложения предоставляется как примеры tooshow как tooenable приложение Java на веб-приложений служб приложений.

### <a name="tomcat"></a>Tomcat
Хотя существует две разновидности Tomcat, поставляемые с веб-приложений служб приложений, она по-прежнему вполне возможно, что tooupload клиента конкретные экземпляры. Ниже приведен пример установки Tomcat с другой виртуальной машиной Java (JVM).

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

На hello Tomcat стороны существует несколько необходимые toobe внесены изменения в конфигурации. Hello server.xml требуется изменить toobe tooset:

* Порт завершения работы = -1.
* Порт соединителя HTTP = {port.http}.
* Адрес соединителя HTTP = "127.0.0.1".
* Закомментируйте соединители HTTPS и AJP.
* параметр Hello IPv4 можно также задать в файле catalina.properties hello, где можно добавить`java.net.preferIPv4Stack=true`

Вызовы Direct3d в веб-приложениях службы приложений не поддерживаются. toodisable, добавьте следующий параметр Java приложения следует такие вызовы hello:`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Как hello случае для Tomcat, клиентам можно отправить свои собственные экземпляры для Jetty. В случае выполнения hello полной установки Jetty hello hello конфигурация будет выглядеть следующим образом:

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

Hello конфигурацию Jetty должен toobe колебаниями hello start.ini tooset `java.net.preferIPv4Stack=true`.

### <a name="springboot"></a>Springboot
В порядке tooget Springboot приложения, под управлением tooupload файл JAR или ВОЙНЫ и добавьте следующие файл web.config hello. файл web.config Hello попадают в папку wwwroot hello. В файле web.config hello Настройка hello аргументы toopoint tooyour JAR-файл, в hello следующий пример hello JAR-файл находится в папке wwwroot hello также.  

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


### <a name="hudson"></a>Hudson
Наш тест используется hello Hudson 3.1.2 war и hello Tomcat 7.0.50 экземпляр по умолчанию, но без использования действия tooset hello пользовательского интерфейса.  Поскольку Hudson — это программное средство построения, это желательно tooinstall ее на выделенный экземпляров, где hello **AlwaysOn** флаг можно установить на веб-приложения hello.

1. В корневом каталоге веб-приложения, например **d:\home\site\wwwroot**, создайте каталог **webapps** (если он отсутствует) и поместите файл Hudson.war в каталог **d:\home\site\wwwroot\webapps**.
2. Скачайте инструмент apache maven 3.0.5 (совместимый с Hudson) и поместите его в каталог **d:\home\site\wwwroot**.
3. Создайте файл web.config в **d:\home\site\wwwroot** и вставить hello согласно содержимому:
   
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
   
    На этом этапе hello веб-приложения может быть перезапущен tootake hello изменения.  Подключите toohttp://yourwebapp/hudson toostart Hudson.
4. После Hudson настраивается, появится следующий экран приветствия:
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. Hello доступа к странице конфигурации Hudson: щелкните **управление Hudson**и нажмите кнопку **Настройка системы**.
6. Настройте hello JDK, как показано ниже:
   
    ![Конфигурация Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. Настройте Maven, как показано ниже.
   
    ![Конфигурация Maven](./media/web-sites-java-custom-upload/maven.png)
8. Сохраните параметры hello. Теперь продукт Hudson должен быть настроен и готов к использованию.

Дополнительные сведения о Hudson см. на сайте [http://hudson-ci.org](http://hudson-ci.org).

### <a name="liferay"></a>Liferay
Liferay поддерживается в веб-приложениях службы приложений. Поскольку Liferay может потребоваться значительный объем, веб-приложения hello должен toorun в средних и крупных выделенный рабочий процесс, который может обеспечить достаточный объем памяти. Liferay занимает несколько минут toostart. По этой причине рекомендуется установить веб-приложение hello слишком**Always On**.  

С помощью Liferay 6.1.2, объединенными Community Edition GA3 Tomcat, hello следующие файлы были изменены после загрузки Liferay:

**Server.xml**

* Измените завершении работы порта слишком-1.
* Изменение соединителя HTTP слишком`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* Закомментируйте hello AJP соединителя.

В hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** папки, создайте файл с именем **ext.properties портала**. Этот файл должен toocontain одну строку, как показано ниже:

    liferay.home=%HOME%/site/wwwroot/liferay

В hello же уровне каталога, что и папка hello tomcat 7.0.40 создать файл с именем **web.config** с hello после содержимого:

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

В разделе hello **httpPlatform** блок hello **requestTimeout** задано слишком "00: 10:00».  Можно сократить, но то, скорее всего, toosee некоторые ошибки времени ожидания при Liferay начальной загрузки.  Если это значение изменяется, затем hello **connectionTimeout** в hello tomcat server.xml также может изменяться.  

Стоит отметить, что varariable среде JRE_HOME hello указывается в hello выше web.config toopoint toohello JDK 64-разрядной. по умолчанию Hello 32 бита, но поскольку Liferay может потребоваться высокая памяти, рекомендуется toouse hello JDK 64-разрядной.

После внесения этих изменений перезапустите веб-сайт с Liferay, а затем откройте адрес http://ваше_веб-приложение. портал Liferay Hello доступен из корня приложения hello web. 

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о Liferay см. на сайте [http://www.liferay.com](http://www.liferay.com).

Дополнительные сведения о Java см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[службе приложений Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
