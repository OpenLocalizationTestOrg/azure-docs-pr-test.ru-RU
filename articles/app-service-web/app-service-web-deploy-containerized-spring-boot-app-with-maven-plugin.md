---
title: "hello toouse aaaHow Maven подключаемого модуля для веб-приложения Azure toodeploy контейнерного tooAzure приложения загрузки пружины"
description: "Узнайте, как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure Spring загрузки приложения."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: e7e760d4ef5bd4c92a4126a50a2b12e5c8f2b4a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a>Как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy контейнерного tooAzure приложения загрузки пружины

Hello [Maven подключаемого модуля для веб-приложения Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) для [Apache Maven](http://maven.apache.org/) обеспечивает прозрачную интеграцию службы приложений Azure в проекты Maven и упрощает процесс hello для разработчиков toodeploy веб-приложений tooAzure службы приложений.

В этой статье демонстрируется использование hello Maven подключаемого модуля для веб-приложения Azure toodeploy Spring загрузки примера приложения в tooAzure контейнера Docker приложения службы.

> [!NOTE]
>
> Hello Maven подключаемого модуля для веб-приложения Azure в настоящее время доступна в предварительной версии. Сейчас поддерживается только FTP-публикации, несмотря на то, что дополнительные функции планируются для будущих hello.
>

## <a name="prerequisites"></a>Предварительные требования

В порядке toocomplete hello шагов в этом учебнике требуется hello toohave следующие предварительные требования:

* Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* Hello [Azure интерфейс командной строки (CLI)].
* Актуальный [пакет разработчиков Java (JDK)] версии 1.7 или более поздней.
* Средство сборки [Maven] (версия 3) от Apache.
* Клиент [Git].
* Клиент [Docker].

> [!NOTE]
>
> Из-за требований к виртуализации toohello этого учебника не может следовать за hello действия, описанные в этой статье на виртуальной машине; необходимо использовать физический компьютер с включенными возможностями виртуализации.
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a>Образец hello клон Spring загрузки на Docker веб-приложения

В этом разделе представлены сведения о клонировании контейнерного приложения Spring Boot и его тестировании на локальном компьютере.

1. Откройте командную строку или окно терминала и создайте toohold локальный каталог Spring загрузки приложения и перейдите в каталог toothat; Например:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- или --
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Клон hello [загрузки Spring по началу работы Docker] образец проекта в каталог hello, вы создали; например:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. Изменение каталога toohello завершения проекта; Например:
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. Построение hello JAR-файл с помощью Maven; Например:
   ```shell
   mvn clean package
   ```

1. При создании веб-приложения hello запустите веб-приложение hello, с помощью Maven; Например:
   ```shell
   mvn spring-boot:run
   ```

1. Тестирование веб-приложения hello путем просмотра tooit локально с помощью веб-браузера. Например можно использовать следующую команду, если у вас есть доступные перелистывание hello:
   ```shell
   curl http://localhost:8080
   ```

1. Должно появиться сообщение, отображаемое после hello: **Docker Здравствуй, мир!**

## <a name="create-an-azure-service-principal"></a>Создание субъекта-службы Azure

В этом разделе создается Azure участника-службы, hello Maven подключаемый модуль использует при развертывании вашей tooAzure контейнера.

1. Откройте окно командной строки.

1. Вход в учетную запись Azure с помощью hello Azure CLI:
   ```shell
   az login
   ```
   Выполните hello инструкции toocomplete hello процесса входа.

1. Создайте субъект-службу Azure.
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Где `uuuuuuuu` — имя пользователя hello и `pppppppp` hello пароль для hello участника-службы.

1. Azure в ответ отправляет похожа на следующий пример hello JSON:
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > Вы будете использовать значения hello из этот ответ JSON, при настройке подключаемого модуля toodeploy hello Maven вашей tooAzure контейнера. Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, и `tttttttt` являются значения заполнителя, которые используются в этом примере toomake его проще toomap эти значения tootheir соответствующие элементы во время настройки вашей Maven `settings.xml` файл hello рядом раздел.
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a>Настройка Maven toouse, участниками службы Azure

В этом разделе используется hello значения из hello проверки подлинности участника tooconfigure службы Azure, Maven будет использовать при развертывании вашей tooAzure контейнера.

1. Откройте ваш Maven `settings.xml` файл в текстовом редакторе; возможно, этот файл в пути, например hello следующие примеры:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Добавить параметры основной службы Azure hello в предыдущем разделе этого учебника toohello `<servers>` коллекции в hello *settings.xml* файла; например:

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Описание
   Элемент | Описание
   ---|---|---
   `<id>` | Задает уникальное имя, которое Maven использует toolook копию параметров безопасности при развертывании вашей tooAzure web app.
   `<client>` | Содержит hello `appId` значение из участника-службы.
   `<tenant>` | Содержит hello `tenant` значение из участника-службы.
   `<key>` | Содержит hello `password` значение из участника-службы.
   `<environment>` | Определяет hello целевой Azure облачной среды, которая представляет `AZURE` в этом примере. (Полный список сред доступен в hello [Maven подключаемого модуля для веб-приложения Azure] документации)

1. Сохраните и закройте hello *settings.xml* файла.

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a>ДОПОЛНИТЕЛЬНО Развертывание вашей локальной tooDocker файл Docker Hub

При наличии учетной записи Docker, можно построить вашей Docker локально образ контейнера и принудительно отправить его tooDocker концентратора. toodo таким образом, используйте следующие шаги hello.

1. Откройте hello `pom.xml` файл для загрузки Spring приложения в текстовом редакторе.

1. Найдите hello `<imageName>` дочерний элемент элемента hello `<containerSettings>` элемента.

1. Обновление hello `${docker.image.prefix}` значение с Docker имя учетной записи:
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. Выберите один из следующих методов развертывания hello.

   * Построение образа контейнера локально с Maven, а затем использовать Docker toopush вашего контейнера tooDocker концентратора:
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * Если у вас есть hello [подключаемый модуль Docker для Maven] установлен, можно автоматически создавать и hello вашей tooDocker образ контейнера концентратора с помощью `-DpushImage` параметр:
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a>Необязательно: Настройка вашего pom.xml перед развертыванием вашей tooAzure контейнера

Откройте hello `pom.xml` файл для загрузки Spring приложения в текстовом редакторе, а затем найдите hello `<plugin>` элемент для `azure-webapp-maven-plugin`. Этот элемент должен быть похож на следующий пример hello.

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Имеется несколько значений, которые можно изменять для подключаемого модуля Maven hello и подробное описание каждого из этих элементов доступен в hello [Maven подключаемого модуля для веб-приложения Azure] документации. Существует ряд значений, на которые следует обратить внимание в этой статье.

Элемент | Описание
---|---|---
`<version>` | Указывает версию hello hello [Maven подключаемого модуля для веб-приложения Azure]. Необходимо проверить версию hello, перечисленные в hello [Maven центрального репозитория](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure, в которых используется hello последнюю версию.
`<authentication>` | Указывает hello сведения для проверки подлинности для Azure, который в данном примере содержит `<serverId>` элемент, содержащий `azure-auth`; Maven использует toolook, значение основного значениями hello службы Azure в вашей Maven *settings.xml* файл, который вы определили в предыдущем разделе этой статьи.
`<resourceGroup>` | Указывает hello целевой группы ресурсов, который является `maven-plugin` в этом примере. будет создана группа ресурсов Hello во время развертывания, если он еще не существует.
`<appName>` | Указывает имя целевой hello для веб-приложения. В этом примере — имя целевого hello `maven-linux-app-${maven.build.timestamp}`, где hello `${maven.build.timestamp}` в конфликт tooavoid примере добавляется суффикс. (метка времени hello необязателен; можно указать любую уникальную строку для имени приложения hello).
`<region>` | Указывает hello целевой области, которая в данном примере `westus`. (Полный список находится в hello [Maven подключаемого модуля для веб-приложения Azure] документации.)
`<appSettings>` | Определяет все уникальные настройки для Maven toouse при развертывании вашей tooAzure web app. В этом примере `<property>` элемент содержит дочерние элементы, укажите порт приложения hello пары имя/значение.

> [!NOTE]
>
> номер порта hello toochange параметры Hello в этом примере необходимы только при изменении порта hello относительно значения по умолчанию hello.
>

## <a name="build-and-deploy-your-container-tooazure"></a>Построение и развертывание вашей tooAzure контейнера

После настройки всех параметров hello в предыдущих подразделах этой статьи hello, вы являетесь toodeploy готовности вашей tooAzure контейнера. Таким образом, toodo используйте hello следующие шаги:

1. Из командной строки hello или окно терминала, который использовался ранее, перестройте hello JAR-файл с помощью Maven при внесении любого изменения toohello *pom.xml* файла; например:
   ```shell
   mvn clean package
   ```

1. Развертывание вашей tooAzure web app с помощью Maven; Например:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven развернет ваш веб tooAzure приложения; Если веб-приложение hello еще не существует, он будет создан.

> [!NOTE]
>
> Если область hello, которое задается в hello `<region>` элемент вашей *pom.xml* файла не имеет достаточного количества доступных серверов при запуске развертывания, может появиться ошибка примерно toohello, в следующем примере:
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> В этом случае можно указать, что другой регион и повторно запустите hello toodeploy команда Maven приложения.
>
>

При развертывании веб-узла можно будет toomanage его с помощью hello [портал Azure].

* Веб-приложение будет указано в разделе **Службы приложений**:

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* И hello URL-адрес для веб-приложения будут указаны в hello **Обзор** веб-приложения:

   ![Определение hello URL-адрес для веб-приложения][AP02]

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello различные технологии, описанные в этой статье, см. следующие статьи hello:

* [Maven подключаемого модуля для веб-приложения Azure]

* [Войдите в tooAzure из hello Azure CLI](/azure/xplat-cli-connect)

* [Как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure приложения загрузки Spring службы приложений](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [Создание субъекта-службы Azure с помощью Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Справочник по параметрам Maven](https://maven.apache.org/settings.html)

* [подключаемый модуль Docker для Maven]

<!-- URL List -->

[Azure интерфейс командной строки (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[подключаемый модуль Docker для Maven]: https://github.com/spotify/docker-maven-plugin
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[загрузки Spring по началу работы Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Maven подключаемого модуля для веб-приложения Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
