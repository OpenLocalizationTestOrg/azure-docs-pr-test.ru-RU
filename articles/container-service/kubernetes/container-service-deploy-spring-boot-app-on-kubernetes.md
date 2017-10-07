---
title: "aaaDeploy приложении Spring загрузки на Kubernetes в службе контейнера Azure | Документы Microsoft"
description: "Этот учебник поможет вам хотя toodeploy действия hello приложение загрузки Spring Kubernetes кластера в Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a>Развертывание приложения загрузки Spring в кластере Kubernetes в hello контейнера службы Azure

Hello  **[Spring Framework]**  — это популярный открытая платформа Java разработчики могут создать web, мобильных устройств и приложения API. В этом учебнике используется образец приложения, созданного с использованием [загрузки Spring], управляемых соглашение случай использования Spring tooget быстро начать работу.

**[Kubernetes]**  и  **[Docker]**  открытая решений, помогающих разработчикам автоматизировать развертывания hello, масштабирования и управления приложениями под управлением в контейнерах.

Этот учебник поможет на то, что объединение toodevelop эти две технологии популярных, открытым исходным кодом и развертывание tooMicrosoft приложения загрузки Spring Azure. В частности, использовать  *[загрузки Spring]*  для разработки приложений,  *[Kubernetes]*  для развертывания контейнера и hello [Контейнера службы azure (ACS)] toohost приложения.

### <a name="prerequisites"></a>Предварительные требования

* Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* Hello [Azure интерфейс командной строки (CLI)].
* Актуальная версия [Java Developer Kit (JDK)].
* Средство сборки [Maven] (версия 3) от Apache.
* Клиент [Git].
* Клиент [Docker].

> [!NOTE]
>
> Из-за требований к виртуализации toohello этого учебника не может следовать за hello действия, описанные в этой статье на виртуальной машине; необходимо использовать физический компьютер с включенными возможностями виртуализации.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Создать hello Spring загрузки на веб-приложение Docker начало работы

Hello следующие шаги содержат пошаговые инструкции для построения Spring загрузки веб-приложения и локального тестирования.

1. Откройте командную строку и создать toohold локальный каталог, приложение и перейдите в каталог toothat; Например:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- или --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Клон hello [загрузки Spring по началу работы Docker] образец проекта в каталог hello.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Изменение каталога toohello завершения проекта.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Используйте Maven toobuild и пример приложения hello выполнения.
   ```
   mvn package spring-boot:run
   ```

1. Веб-приложения hello теста путем просмотра toohttp://localhost:8080 или hello следующий `curl` команды:
   ```
   curl http://localhost:8080
   ```

1. Должно появиться сообщение, отображаемое после hello: **Docker Здравствуй, мир!**

   ![Локальный просмотр образца приложения][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Создайте в реестре контейнера Azure с помощью hello Azure CLI

1. Откройте окно командной строки.

1. Вход tooyour учетная запись Azure:
   ```azurecli
   az login
   ```

1. Создание группы ресурсов для hello Azure ресурсы, используемые в этом учебнике.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Создание реестра закрытый контейнер Azure в группе ресурсов hello. Пример приложения hello помещает учебника Hello как реестра toothis образа Docker на последующих этапах. Замените `wingtiptoysregistry` уникальным именем для реестра.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a>Принудительная реестр контейнера toohello приложения

1. Перейдите в каталог toohello конфигурации для установки Maven (по умолчанию ~/.m2/ или C:\Users\username\.m2) и откройте hello *settings.xml* файл в текстовом редакторе.

1. Получить пароль hello для контейнера реестра из hello Azure CLI.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Добавить ваш реестра контейнера Azure идентификатора и пароля tooa новый `<server>` коллекции в hello *settings.xml* файла.
Hello `id` и `username` являются hello имя реестра hello. Используйте hello `password` значение из предыдущей команды hello (без кавычек).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Перейдите в каталог проекта toohello завершения загрузки Spring приложения (например, «*C:\SpringBoot\gs-spring-boot-docker\complete*«или»*/users/robert/SpringBoot/gs-spring-boot-docker / Полный*») и откройте hello *pom.xml* файл в текстовом редакторе.

1. Обновление hello `<properties>` коллекции в hello *pom.xml* файл со значение сервера hello входа для реестра контейнера Azure.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Обновление hello `<plugins>` коллекции в hello *pom.xml* файл, который hello `<plugin>` содержит hello server адрес и реестра имя входа для реестра контейнера Azure.

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Перейдите в каталог проекта toohello завершения загрузки Spring приложения и выполните hello, следующая команда toobuild hello Docker контейнера и принудительной hello изображения toohello реестра:

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  Может появиться сообщение об ошибке, аналогичные tooone следующие hello при Maven помещает hello tooAzure изображения:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Если возникли ошибки, вход tooAzure из командной строки Docker hello.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Затем принудительно отправьте контейнер:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a>Создание кластера Kubernetes на службы ACS с помощью hello Azure CLI

1. Создайте кластер Kubernetes в службе контейнеров Azure. Hello следующая команда создает *kubernetes* кластера в hello *wingtiptoys kubernetes* ресурсов группы с *wingtiptoys containerservice* как кластер hello имя, и *wingtiptoys kubernetes* как префикс DNS hello:
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   Эта команда может занять некоторое время toocomplete.

1. Установить `kubectl` с помощью Azure CLI "hello". Пользователи Linux, возможно, tooprefix к этой команде `sudo` с момента развертывает hello Kubernetes CLI слишком`/usr/local/bin`.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Загрузка сведений о конфигурации кластера hello кластера можно управлять из веб-интерфейса Kubernetes hello и `kubectl`. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a>Развертывание кластера Kubernetes tooyour изображение hello

Этот учебник развертывает приложения hello с использованием `kubectl`, подождите, пока вы tooexplore hello развертывания hello Kubernetes веб-интерфейсе.

### <a name="deploy-with-hello-kubernetes-web-interface"></a>Развертывание веб-интерфейсе Kubernetes hello

1. Откройте окно командной строки.

1. Откройте веб-сайт конфигурации hello для кластера Kubernetes в браузере по умолчанию:
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Когда веб-сайт конфигурации Kubernetes hello откроется в браузере, щелкните ссылку hello слишком**развертывание контейнерного приложения**:

   ![Веб-сайт конфигурации Kubernetes][KB01]

1. Здравствуйте, когда **развертывание контейнерного приложения** отображается страница, укажите hello следующие параметры:

   а. Выберите **Specify app details below** (Указать сведения о приложении ниже).

   b. Введите имя приложения Spring загрузки для hello **имя приложения**, например: «*gs spring загрузки docker*».

   c. Введите имя входа образа сервера и контейнера из более ранних версий для hello **образ контейнера**, например: «*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*».

   d. Выберите **внешних** для hello **службы**.

   д. Указать на внешние и внутренние порты hello **порт** и **целевой порт** текстовые поля.

   ![Веб-сайт конфигурации Kubernetes][KB02]


1. Нажмите кнопку **развернуть** toodeploy hello контейнера.

   ![Развертывание контейнера][KB05]

1. После развертывания приложение Spring Boot отобразится в списке **Службы**.

   ![Службы Kubernetes][KB06]

1. Если щелкнуть ссылку hello для **внешние конечные точки**, вы увидите Spring загрузки приложения в Azure.

   ![Службы Kubernetes][KB07]

   ![Просмотр примера приложения в Azure][SB02]


### <a name="deploy-with-kubectl"></a>Развертывание с помощью kubectl

1. Откройте окно командной строки.

1. Запустите контейнер в кластере Kubernetes hello с помощью hello `kubectl run` команды. Присвойте имя службы для приложения в Kubernetes и hello имя полного образа. Например:
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   В этой команде:

   * Имя контейнера Hello `gs-spring-boot-docker` указывается сразу после hello `run` команды

   * Hello `--image` указывает hello вместе серверу входа в систему и имя образа, как`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. Предоставлять кластера Kubernetes извне с помощью hello `kubectl expose` команды. Укажите имя службы, hello приложение общедоступный TCP порт, используемый tooaccess hello и hello внутренней целевой порт, который прослушивается приложения. Например:
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   В этой команде:

   * Имя контейнера Hello `gs-spring-boot-docker` указывается сразу после hello `expose deployment` команды

   * Hello `--type` параметр указывает, hello кластер использует подсистему балансировки нагрузки

   * Hello `--port` указывает hello общедоступный TCP-порт 80. Доступ к приложение hello через этот порт.

   * Hello `--target-port` указывает hello внутренней TCP-порт 8080. Подсистема балансировки нагрузки Hello пересылает приложения tooyour запросы через этот порт.

1. После развертывания приложение hello кластера toohello hello внешний IP-адрес запроса и открыть его в веб-браузере:

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Просмотр примера приложения в Azure][SB02]


## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об использовании Spring загрузки в Azure см. следующие статьи hello:

* [Развертывание приложения загрузки Spring toohello службе приложений Azure](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Развертывание приложения загрузки Spring в Linux в hello контейнера службы Azure](container-service-deploy-spring-boot-app-on-linux.md)

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].

Дополнительные сведения о hello Spring загрузки Docker образец проекта в разделе [загрузки Spring по началу работы Docker].

Hello следующие ссылки предоставляют дополнительные сведения о создании приложений Spring загрузки.

* Дополнительные сведения о создании простого приложения загрузки Spring hello Spring Initializr на https://start.spring.io/ см.

Hello следующие ссылки предоставляют дополнительные сведения об использовании Kubernetes с Azure:

* [Развертывание кластера Kubernetes для контейнеров Linux](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [С помощью hello Kubernetes веб-интерфейсом пользователя с помощью контейнера службы Azure](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Дополнительные сведения об использовании интерфейса командной строки Kubernetes доступен в hello **kubectl** руководство пользователя по <https://kubernetes.io/docs/user-guide/kubectl/>.

веб-сайт Kubernetes Hello имеет несколько статей, в которых рассматривается использование изображений в частных реестрах:

* [Configure Service Accounts for Pods] (Настройка учетных записей службы для модулей Pod)
* [Namespaces] (Пространства имен)
* [Pull an Image from a Private Registry] (Извлечение образа из частного реестра)

Дополнительные примеры по как toouse Docker пользовательских образов с помощью Azure в разделе [с помощью пользовательского образа Docker для веб-приложения Azure в Linux].

<!-- URL List -->

[Azure интерфейс командной строки (CLI)]: /cli/azure/overview
[Контейнера службы azure (ACS)]: https://azure.microsoft.com/services/container-service/
[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[с помощью пользовательского образа Docker для веб-приложения Azure в Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[загрузки Spring]: http://projects.spring.io/spring-boot/
[загрузки Spring по началу работы Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configure Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Настройка учетных записей службы для модулей Pod)
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/ (Пространства имен)
[Pull an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Извлечение образа из частного реестра)

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
