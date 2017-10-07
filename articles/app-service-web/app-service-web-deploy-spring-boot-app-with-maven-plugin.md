---
title: "hello toouse aaaHow Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure Spring загрузки приложения"
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
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a>Как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure Spring загрузки приложения

Hello [Maven подключаемого модуля для веб-приложения Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) для [Apache Maven](http://maven.apache.org/) обеспечивает прозрачную интеграцию службы приложений Azure в проекты Maven и упрощает процесс hello для разработчиков toodeploy веб-приложений tooAzure службы приложений.

В этой статье демонстрируется использование hello Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure приложения загрузки Spring образца службы приложений.

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

## <a name="clone-hello-sample-spring-boot-web-app"></a>Клонирование hello образец Spring загрузки веб-приложения

В этом разделе представлены сведения о клонировании готового приложения Spring Boot и его тестировании на локальном компьютере.

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

1. Клон hello [Spring начальной загрузки] образец проекта в каталог hello, вы создали; например:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. Изменение каталога toohello завершения проекта; Например:
   ```shell
   cd gs-spring-boot/complete
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

1. Должно появиться сообщение, отображаемое после hello: **Greetings с Spring загрузки!**

## <a name="create-an-azure-service-principal"></a>Создание субъекта-службы Azure

В этом разделе создается Azure участника-службы, hello Maven подключаемый модуль использует при развертывании вашей tooAzure web app.

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
   > Вы будете использовать значения hello из этот ответ JSON, при настройке подключаемого модуля toodeploy hello Maven вашей tooAzure web app. Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, и `tttttttt` являются значения заполнителя, которые используются в этом примере toomake его проще toomap эти значения tootheir соответствующие элементы во время настройки вашей Maven `settings.xml` файл hello рядом раздел.
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a>Настройка Maven toouse, участниками службы Azure

В этом разделе используется hello значения из hello проверки подлинности участника tooconfigure службы Azure, Maven использует при развертывании вашей tooAzure web app.

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

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a>Необязательно: Настройка вашего pom.xml перед развертыванием вашей tooAzure web app

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
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

Имеется несколько значений, которые можно изменять для подключаемого модуля Maven hello и подробное описание каждого из этих элементов доступен в hello [Maven подключаемого модуля для веб-приложения Azure] документации. Существует ряд значений, на которые следует обратить внимание в этой статье.

Элемент | Описание
---|---|---
`<version>` | Указывает версию hello hello [Maven подключаемого модуля для веб-приложения Azure]. Необходимо проверить версию hello, перечисленные в hello [Maven центрального репозитория](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure, в которых используется hello последнюю версию.
`<authentication>` | Указывает hello сведения для проверки подлинности для Azure, который в данном примере содержит `<serverId>` элемент, содержащий `azure-auth`; Maven использует toolook, значение основного значениями hello службы Azure в вашей Maven *settings.xml* файл, который вы определили в предыдущем разделе этой статьи.
`<resourceGroup>` | Указывает hello целевой группы ресурсов, который является `maven-plugin` в этом примере. Группа ресурсов Hello создается во время развертывания, если он еще не существует.
`<appName>` | Указывает имя целевой hello для веб-приложения. В этом примере — имя целевого hello `maven-web-app-${maven.build.timestamp}`, где hello `${maven.build.timestamp}` в конфликт tooavoid примере добавляется суффикс. (метка времени hello необязателен; можно указать любую уникальную строку для имени приложения hello).
`<region>` | Указывает hello целевой области, которая в данном примере `westus`. (Полный список находится в hello [Maven подключаемого модуля для веб-приложения Azure] документации.)
`<javaVersion>` | Указывает версию среды выполнения Java hello веб-приложения. (Полный список находится в hello [Maven подключаемого модуля для веб-приложения Azure] документации.)
`<deploymentType>` | Тип развертывания для веб-приложения. Сейчас поддерживается только `ftp`, хотя поддержка других типов развертывания находится в разработке.
`<resources>` | Указывает ресурсы и получателям, которые Maven использует при развертывании вашей tooAzure web app. В этом примере два `<resource>` элементы указывают, что Maven развернет hello JAR-файл для веб-приложения и hello *web.config* файл из проекта загрузки Spring hello.

## <a name="build-and-deploy-your-web-app-tooazure"></a>Построение и развертывание вашей tooAzure web app

После настройки всех параметров hello в предыдущих подразделах этой статьи hello, вы являетесь toodeploy готовности вашей tooAzure web app. Таким образом, toodo используйте hello следующие шаги:

1. Из командной строки hello или окно терминала, который использовался ранее, перестройте hello JAR-файл с помощью Maven при внесении любого изменения toohello *pom.xml* файла; например:
   ```shell
   mvn clean package
   ```

1. Развертывание вашей tooAzure web app с помощью Maven; Например:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven развернет ваш веб tooAzure приложения; Если веб-приложение hello еще не существует, он будет создан.

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

* [Как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy контейнерного tooAzure приложения загрузки пружины](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [Создание субъекта-службы Azure с помощью Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Справочник по параметрам Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure интерфейс командной строки (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring начальной загрузки]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven подключаемого модуля для веб-приложения Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
