---
title: "hello toouse aaaHow Maven подключаемого модуля для веб-приложения Azure toodeploy приложении Spring загрузки в реестре контейнеров Azure tooAzure службы приложений"
description: "Этот учебник поможет вам хотя toodeploy действия hello приложение Spring загрузки в реестре контейнеров Azure tooAzure tooAzure службы приложений с помощью подключаемого модуля Maven."
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a>Как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy приложении Spring загрузки в реестре контейнеров Azure tooAzure службы приложений

Hello  **[Spring Framework]**  — это популярный открытая платформа Java разработчики могут создать web, мобильных устройств и приложения API. В этом учебнике используется образец приложения, созданного с использованием [загрузки Spring], управляемых соглашение случай использования Spring tooget быстро начать работу.

В этой статье показано, как toodeploy tooAzure приложения загрузки Spring образец реестра контейнера, а затем использовать hello Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure вашего приложения служб приложений.

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
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
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

   ![Локальный просмотр образца приложения][SB01]

## <a name="create-an-azure-service-principal"></a>Создание субъекта-службы Azure

В этом разделе создается Azure участника-службы, hello Maven подключаемый модуль использует при развертывании вашей tooAzure контейнера.

1. Откройте окно командной строки.

1. Вход в учетную запись Azure с помощью hello Azure CLI:
   ```azurecli
   az login
   ```
   Выполните hello инструкции toocomplete hello процесса входа.

1. Создайте субъект-службу Azure.
   ```azurecli
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

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Создайте в реестре контейнера Azure с помощью hello Azure CLI

1. Откройте окно командной строки.

1. Вход tooyour учетная запись Azure:
   ```azurecli
   az login
   ```

1. Создание группы ресурсов для hello ресурсы Azure, которая будет использоваться в этой статье:
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Замените `wingtiptoysresources` в этом примере уникальным именем для группы ресурсов.

1. Создайте реестра закрытый контейнер Azure в группе ресурсов hello Spring загрузки приложения: 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Замените `wingtiptoysregistry` в этом примере уникальным именем для реестра контейнеров.

1. Получить пароль hello для контейнера реестра:
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   В ответ Azure предоставит пароль, например:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a>Добавьте контейнер Azure реестра и параметры Maven tooyour основной службы Azure

1. Откройте ваш Maven `settings.xml` файл в текстовом редакторе; возможно, этот файл в пути, например hello следующие примеры:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Добавить параметры доступа реестра контейнера Azure hello в предыдущем разделе этой статьи toohello `<servers>` коллекции в hello *settings.xml* файла; например:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Описание
   Элемент | Описание
   ---|---|---
   `<id>` | Содержит имя hello реестра закрытый контейнер Azure.
   `<username>` | Содержит имя hello реестра закрытый контейнер Azure.
   `<password>` | Содержит пароль hello, полученный в предыдущем разделе hello данной статьи.

1. Добавить параметры основной службы Azure в предыдущем разделе этой статьи toohello `<servers>` коллекции в hello *settings.xml* файла; например:

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

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a>Сборка Docker на образ контейнера и передать ее реестра tooyour контейнер Azure

1. Перейдите в каталог проекта toohello завершения загрузки Spring приложения, (например) «*C:\SpringBoot\gs-spring-boot-docker\complete*«или»*/users/robert/SpringBoot/gs-spring-boot-docker/complete*») и откройте hello *pom.xml* -файл текстовый редактор.

1. Обновление hello `<properties>` коллекции в hello *pom.xml* файл со значение сервера hello входа для реестра контейнера Azure hello в предыдущем разделе этого учебника; например:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Описание
   Элемент | Описание
   ---|---|---
   `<azure.containerRegistry>` | Указывает имя hello реестра закрытый контейнер Azure.
   `<docker.image.prefix>` | Указывает URL-адрес hello реестра закрытый контейнер Azure, который является производным путем добавления «. azurecr.io» toohello имя контейнера закрытого реестра.

1. Убедитесь, что `<plugin>` для подключаемого модуля Docker hello в вашей *pom.xml* файл содержит необходимые свойства hello для hello server адрес и реестра имя входа из предыдущего шага hello в этом учебнике. Например:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   Описание
   Элемент | Описание
   ---|---|---
   `<serverId>` | Указывает свойство hello, которое содержит имя реестра закрытый контейнер Azure.
   `<registryUrl>` | Указывает свойство hello, которое содержит URL-адрес hello реестра закрытый контейнер Azure.

1. Перейдите в каталог проекта toohello завершения загрузки Spring приложения и запустите следующие команды toorebuild hello приложения hello push tooyour контейнера hello контейнер Azure реестра:

   ```
   mvn package docker:build -DpushImage 
   ```

1. Необязательно: Обзор toohello [портал Azure] и убедитесь, что образ контейнера Docker с именем **gs spring загрузки docker** в реестре контейнера.

   ![Проверка контейнера на портале Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a>Настройка вашего pom.xml затем построения и развертывания вашего tooAzure контейнера

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
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
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
`<resourceGroup>` | Указывает hello целевой группы ресурсов, который является `wingtiptoysresources` в этом примере. будет создана группа ресурсов Hello во время развертывания, если он еще не существует.
`<appName>` | Указывает имя целевой hello для веб-приложения. В этом примере — имя целевого hello `maven-linux-app-${maven.build.timestamp}`, где hello `${maven.build.timestamp}` в конфликт tooavoid примере добавляется суффикс. (метка времени hello необязателен; можно указать любую уникальную строку для имени приложения hello).
`<region>` | Указывает hello целевой области, которая в данном примере `westus`. (Полный список находится в hello [Maven подключаемого модуля для веб-приложения Azure] документации.)
`<containerSettings>` | Указывает свойства hello, содержащих имя hello и URL-адрес контейнера.
`<appSettings>` | Определяет все уникальные настройки для Maven toouse при развертывании вашей tooAzure web app. В этом примере `<property>` элемент содержит дочерние элементы, укажите порт приложения hello пары имя/значение.

> [!NOTE]
>
> номер порта hello toochange параметры Hello в этом примере необходимы только при изменении порта hello относительно значения по умолчанию hello.
>

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

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello различные технологии, описанные в этой статье, см. следующие статьи hello:

* [Maven подключаемого модуля для веб-приложения Azure]

* [Войдите в tooAzure из hello Azure CLI](/azure/xplat-cli-connect)

* [Создание субъекта-службы Azure с помощью Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Справочник по параметрам Maven](https://maven.apache.org/settings.html)

* [Подключаемый модуль Docker для Maven]

<!-- URL List -->

[Azure интерфейс командной строки (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[Maven подключаемого модуля для веб-приложения Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Подключаемый модуль Docker для Maven]: https://github.com/spotify/docker-maven-plugin
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[загрузки Spring]: http://projects.spring.io/spring-boot/
[загрузки Spring по началу работы Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
