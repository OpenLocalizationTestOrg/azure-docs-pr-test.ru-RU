---
title: "Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure"
description: "Сведения о развертываний приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure."
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
ms.openlocfilehash: 883040590291cee94daa227fbc6715ad4be0b393
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a>Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure

[Подключаемый модуль Maven для веб-приложений Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) для [Apache Maven](http://maven.apache.org/) обеспечивает эффективную интеграцию службы приложений Azure в проекты Maven и упрощает процесс развертывания веб-приложений в службе приложений Azure.

В этой статье демонстрируется использование подключаемого модуля Maven для веб-приложений Azure с целью развертывания примера приложения Spring Boot в контейнере Docker в службах приложений Azure.

> [!NOTE]
>
> Подключаемый модуль Maven для веб-приложений Azure в настоящее время доступен в предварительной версии. Сейчас поддерживается только FTP-публикация, но на будущее запланированы дополнительные функции.
>

## <a name="prerequisites"></a>Предварительные требования

Для работы с этим руководством требуется следующее.

* Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* [Интерфейс командной строки Azure (CLI)].
* Актуальный [пакет разработчиков Java (JDK)] версии 1.7 или более поздней.
* Средство сборки [Maven] (версия 3) от Apache.
* Клиент [Git].
* Клиент [Docker].

> [!NOTE]
>
> С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a>Клонирование примера "Приложение Spring Boot в веб-приложении Docker"

В этом разделе представлены сведения о клонировании контейнерного приложения Spring Boot и его тестировании на локальном компьютере.

1. Откройте командную строку или окно терминала и создайте локальный каталог для размещения приложения Spring Boot, после чего перейдите в этот каталог, например:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- или --
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Клонируйте образец проекта [Spring Boot on Docker Getting Started] (Запуск Spring Boot в Docker) в созданный каталог, например:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. Перейдите в каталог готового проекта, например:
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. Выполните сборку файла JAR с помощью Maven, например:
   ```shell
   mvn clean package
   ```

1. При создании веб-приложения запустите веб-приложение с помощью Maven; например:
   ```shell
   mvn spring-boot:run
   ```

1. Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера. Например, если имеется Curl, можно использовать следующую команду:
   ```shell
   curl http://localhost:8080
   ```

1. Должно появиться следующее сообщение: **Hello Docker World**.

## <a name="create-an-azure-service-principal"></a>Создание субъекта-службы Azure

В этом разделе представлен порядок создания субъекта-службы Azure, которого подключаемый модуль Maven использует при развертывании контейнера в Azure.

1. Откройте окно командной строки.

1. Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.
   ```shell
   az login
   ```
   Для завершения процесса входа следуйте инструкциям.

1. Создайте субъект-службу Azure.
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Где `uuuuuuuu` — это имя пользователя и `pppppppp` — пароль для субъекта-службы.

1. В ответ Azure предоставит код JSON, аналогичный приведенному ниже.
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
   > При настройке подключаемого модуля Maven для развертывания контейнера в Azure используйте значения из этого ответа JSON. `aaaaaaaa`, `uuuuuuuu`, `pppppppp` и `tttttttt` являются значениями заполнителя, которые используются в этом примере с целью упростить сопоставление этих значений с соответствующими им элементами во время настройки файла Maven `settings.xml` в следующем разделе.
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a>Настройка Maven для использования субъекта-службы

В этом разделе с помощью значений из субъекта службы Azure выполняется настройка проверки подлинности, используемой Maven при развертывании контейнера в Azure.

1. Откройте файл Maven `settings.xml` в текстовом редакторе; этот файл может находиться по пути, аналогичному указанному в следующих примерах.
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Добавьте параметры субъекта-службы Azure из предыдущего раздела этого учебника в коллекцию `<servers>` в файле *settings.xml*, например:

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
   `<id>` | Задает уникальное имя, которое Maven использует для поиска параметров безопасности при развертывании веб-приложения в Azure.
   `<client>` | Содержит значение `appId` из субъекта-службы.
   `<tenant>` | Содержит значение `tenant` из субъекта-службы.
   `<key>` | Содержит значение `password` из субъекта-службы.
   `<environment>` | Определяет целевую облачную среду Azure, которой в этом примере является `AZURE`. (Полный список сред см. в документации по [подключаемому модулю Maven для веб-приложений Azure].)

1. Сохраните и закройте файл *settings.xml*.

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a>НЕОБЯЗАТЕЛЬНО. Развертывание локального файла Docker в центр Docker

При наличии учетной записи Docker образ контейнера Docker можно создать локально и принудительно отправить его в центр Docker. Для этого выполните следующие действия.

1. Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе.

1. Найдите дочерний элемент `<imageName>` элемента `<containerSettings>`.

1. Обновите значение `${docker.image.prefix}`, указав имя учетной записи Docker:
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. Выберите один из следующих способов развертывания.

   * Создайте образ контейнера локально с помощью Maven, а затем используйте Docker для принудительной отправки контейнера в центр Docker.
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * Если установлен [подключаемый модуль Docker для Maven], можно автоматически создать и отправить образа контейнера в центр Docker с помощью параметра `-DpushImage`.
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a>НЕОБЯЗАТЕЛЬНО. Настройка pom.xml перед развертыванием веб-приложения в Azure

Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе, а затем найдите элемент `<plugin>` для `azure-webapp-maven-plugin`. Этот элемент должен выглядеть примерно следующим образом.

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

Существует несколько значений, которые можно изменить для подключаемого модуля Maven. Подробное описание каждого из этих элементов см. в документации по [подключаемому модулю Maven для веб-приложений Azure]. Существует ряд значений, на которые следует обратить внимание в этой статье.

Элемент | Описание
---|---|---
`<version>` | Версия [подключаемому модулю Maven для веб-приложений Azure]. Обратитесь к списку версий в [центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22), чтобы убедиться, что вы используете актуальную версию.
`<authentication>` | Сведения для проверки подлинности для Azure, в которых в данном примере содержится элемент `<serverId>`, который, в свою очередь, содержит `azure-auth`; Maven использует это значение для поиска значений субъекта-службы Azure в файле Maven *settings.xml*, который вы определили в предыдущем разделе этой статьи.
`<resourceGroup>` | Целевая группа ресурсов, которой в этом примере является `maven-plugin`. Если эта группа ресурсов не существует, она будет создана во время развертывания.
`<appName>` | Целевое имя веб-приложения. В этом примере целевое имя — `maven-linux-app-${maven.build.timestamp}`, к которому в этом примере добавлен суффикс `${maven.build.timestamp}`, чтобы избежать конфликтов. (Метку времени добавлять необязательно; можно указать любую уникальную строку для имени приложения.)
`<region>` | Целевой регион, которым в данном примере является `westus`. (Полный список см. в документации по [подключаемому модулю Maven для веб-приложений Azure].)
`<appSettings>` | Любые уникальные настройки для Maven, которые следует использовать при развертывании веб-приложения в Azure. В этом примере элемент `<property>` содержит пару "имя/значение" дочерних элементов, которая задает порт для вашего приложения.

> [!NOTE]
>
> Параметры для изменения номера порта в этом примере необходимы только в случае, если требуется изменить порт по умолчанию.
>

## <a name="build-and-deploy-your-container-to-azure"></a>Создание и развертывание контейнера в Azure

После настройки всех параметров в предыдущих разделах этой статьи можно приступать к развертыванию контейнера в Azure. Для этого выполните следующие действия.

1. В командной строке или в окне терминала, которые вы использовали ранее, перестройте JAR-файл, используя Maven, если вы внесли изменения в файл *pom.xml*; например:
   ```shell
   mvn clean package
   ```

1. Разверните веб-приложение в Azure с помощью Maven; например:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven выполнит развертывание веб-приложения в Azure; если веб-приложение еще не существует, оно будет создано.

> [!NOTE]
>
> Если при запуске развертывания в регионе, который задан в элементе `<region>` в файле *pom.xml*, нет достаточного количества доступных серверов, может появиться сообщение об ошибке, аналогичное приведенному ниже.
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> В этом случае можно указать другой регион и повторно выполнить команду Maven для развертывания приложения.
>
>

После развертывания веб-приложения вы сможете управлять им с помощью [портала Azure].

* Веб-приложение будет указано в разделе **Службы приложений**:

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* URL-адрес веб-приложения будет указан в разделе **Обзор** для вашего веб-приложения:

   ![Определение URL-адреса для веб-приложения][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.

* [подключаемому модулю Maven для веб-приложений Azure]

* [Вход в Azure из интерфейса командной строки Azure](/azure/xplat-cli-connect)

* [Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure в службе приложений Azure](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [Создание субъекта-службы Azure с помощью Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Справочник по параметрам Maven](https://maven.apache.org/settings.html)

* [подключаемый модуль Docker для Maven]

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[портала Azure]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[подключаемый модуль Docker для Maven]: https://github.com/spotify/docker-maven-plugin
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[подключаемому модулю Maven для веб-приложений Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
