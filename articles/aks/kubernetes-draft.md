---
title: "Использование Draft с AKS и реестром контейнеров Azure"
description: "Использование Draft с AKS и реестром контейнеров Azure"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: article
ms.date: 10/24/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: a77e214c1138ce936b2ec6c521950704e5beb3ff
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/16/2017
---
# <a name="use-draft-with-azure-container-service-aks"></a>Использование Draft со Службой контейнеров Azure (AKS)

Draft является инструментом с открытым кодом, который помогает упаковывать и запускать код в кластере Kubernetes. Draft нацелен на цикл итераций разработки по мере разработки кода, но перед фиксированием в системе управления версиями. С помощью Draft можно быстро повторно развернуть приложение в Kubernetes при изменении кода. Дополнительные сведения о черновике см. в разделе [черновики документации на Github][draft-documentation].

В этом документе описано использование Draft с кластером Kubernetes в AKS.

## <a name="prerequisites"></a>Технические условия

В действиях, описанных в этом документе, предполагается, что кластер AKS создан и с ним установлено соединение kubectl. При необходимости эти элементы в разделе [краткое руководство AKS][aks-quickstart].

Кроме того, необходим частный реестр Docker в реестре контейнеров Azure(ACR). Инструкции по развертыванию экземпляра записи управления Доступом см. в разделе [краткое руководство реестра контейнера Azure][acr-quickstart].

## <a name="install-helm"></a>Установка Helm

Интерфейс командной строки Helm — это клиент, который выполняется в системе разработки и позволяет запускать и останавливать приложения с помощью чартов Helm, а также управлять ими.

Чтобы установить интерфейс командной строки Helm на компьютере Mac, выполните команду `brew`. Дополнительные параметры установки, в разделе [Установка Helm][install-helm].

```console
brew install kubernetes-helm
```

Выходные данные:

```
==> Downloading https://homebrew.bintray.com/bottles/kubernetes-helm-2.6.2.sierra.bottle.1.tar.gz
######################################################################## 100.0%
==> Pouring kubernetes-helm-2.6.2.sierra.bottle.1.tar.gz
==> Caveats
Bash completion has been installed to:
  /usr/local/etc/bash_completion.d
==> Summary
🍺  /usr/local/Cellar/kubernetes-helm/2.6.2: 50 files, 132.4MB
```

## <a name="install-draft"></a>Установка Draft

CLI Draft — это клиент, который выполняется в системе разработки и позволяет быстро развертывать код в кластер Kubernetes.

Чтобы установить интерфейс командной строки Draft на компьютере Mac, выполните команду `brew`. Дополнительные параметры установки в разделе, [руководство по установке черновик][install-draft].

```console
brew install draft
```

Выходные данные:

```
==> Installing draft from azure/draft
==> Downloading https://azuredraft.blob.core.windows.net/draft/draft-v0.7.0-darwin-amd64.tar.gz
Already downloaded: /Users/neilpeterson/Library/Caches/Homebrew/draft-0.7.0.tar.gz
==> /usr/local/Cellar/draft/0.7.0/bin/draft init --client-only
🍺  /usr/local/Cellar/draft/0.7.0: 6 files, 61.2MB, built in 1 second
```

## <a name="configure-draft"></a>Настройка Draft

При настройке Draft необходимо указать реестр контейнеров. В этом примере используется реестр контейнеров Azure.

Выполните следующую команду для получения имени и имени сервера входа экземпляра ACR. Укажите в команде имя группы ресурсов, которая содержит экземпляр ACR.

```console
az acr list --resource-group <resource group> --query "[].{Name:name,LoginServer:loginServer}" --output table
```

Кроме того, необходим пароль экземпляра ACR.

Запустите следующую команду, чтобы получить пароль ACR. Укажите в команде имя нужного экземпляра ACR.

```console
az acr credential show --name <acr name> --query "passwords[0].value" --output table
```

Инициализируйте Draft с помощью команды `draft init`.

```console
draft init
```

Во время этого процесса вам будет предложено ввести учетные данные реестра контейнера. При использовании реестра контейнеров Azure URL-адресом реестра является имя сервера входа ACR, имя пользователя — именем экземпляра ACR, а пароль — паролем ACR.

```console
1. Enter your Docker registry URL (e.g. docker.io/myuser, quay.io/myuser, myregistry.azurecr.io): <ACR Login Server>
2. Enter your username: <ACR Name>
3. Enter your password: <ACR Password>
```

После завершения Draft настроен в кластере Kubernetes и готов к использованию.

```
Draft has been installed into your Kubernetes Cluster.
Happy Sailing!
```

## <a name="run-an-application"></a>Запуск приложения

Репозиторий Draft включает несколько примеров приложений, который могут использоваться для демонстрации Draft. Создайте клон репозитория.

```console
git clone https://github.com/Azure/draft
```

Перейдите в каталог примеров Java.

```console
cd draft/examples/java/
```

Чтобы запустить процесс, используйте команду `draft create`. Эта команда создает артефакты, которые используются для запуска приложения в кластере Kubernetes. Эти элементы включают файл Dockerfile, чарт Helm и файл `draft.toml`, который является файлом конфигурации Draft.

```console
draft create
```

Выходные данные:

```
--> Draft detected the primary language as Java with 92.205567% certainty.
--> Ready to sail
```

Чтобы запустить приложение в кластере Kubernetes, используйте команду `draft up`. Эта команда отправляет код приложения и файлы конфигурации в кластер Kubernetes. Затем запускается файл Docker, чтобы создать образ контейнера, отправить образ в реестр контейнеров и наконец запустить чарт Helm для запуска приложения.

```console
draft up
```

Выходные данные:

```
Draft Up Started: 'open-jaguar'
open-jaguar: Building Docker Image: SUCCESS ⚓  (28.0342s)
open-jaguar: Pushing Docker Image: SUCCESS ⚓  (7.0647s)
open-jaguar: Releasing Application: SUCCESS ⚓  (4.5056s)
open-jaguar: Build ID: 01BW3VVNZYQ5NQ8V1QSDGNVD0S
```

## <a name="test-the-application"></a>Тестирование приложения

Чтобы проверить приложение, используйте команду `draft connect`. Это команда прокси-подключения к модулю Kubernetes, позволяющая безопасное локальное подключение. По завершении доступ к приложению можно получить через предоставленный URL-адрес.

В некоторых случаях скачивание образа контейнера и запуск приложения может занять несколько минут. Если при доступе к приложению появляется ошибка, повторите попытку подключения.

```console
draft connect
```

Выходные данные:

```
Connecting to your app...SUCCESS...Connect to your app on localhost:46143
Starting log streaming...
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
== Spark has ignited ...
>> Listening on 0.0.0.0:4567
```

После завершения тестирования приложения используйте команду `Control+C` для остановки прокси-подключения.

## <a name="expose-application"></a>Предоставление приложения

При тестировании приложения в Kubernetes можно предоставить доступ к приложению через Интернет. Это можно сделать с помощью Kubernetes службы с типом [Подсистема балансировки нагрузки] [ kubernetes-service-loadbalancer] или [входящих контроллера][kubernetes-ingress]. В этом документе описано использование службы Kubernetes.


Сначала пакет Draft необходимо обновить, чтобы указать, что служба с типом `LoadBalancer` может быть создана. Чтобы сделать это, необходимо обновить тип службы в файле `values.yaml`.

```console
vi chart/java/values.yaml
```

Найдите свойство `service.type` и обновите значение с `ClusterIP` на `LoadBalancer`.

```yaml
replicaCount: 2
image:
  repository: openjdk
  tag: 8-jdk-alpine
  pullPolicy: IfNotPresent
service:
  name: java
  type: LoadBalancer
  externalPort: 80
  internalPort: 4567
resources:
  limits:
    cpu: 100m
    memory: 128Mi
  requests:
    cpu: 100m
    memory: 128Mi
  ```

Выполните команду `draft up` для повторного запуска приложения.

```console
draft up
```

Возвращение общедоступного IP-адреса службы может занять несколько минут. Для мониторинга выполнения используйте команду `kubectl get service` с контрольным значением.

```console
kubectl get service -w
```

Изначально для параметра *EXTERNAL-IP* службы отображается состояние `pending`.

```
deadly-squid-java   10.0.141.72   <pending>     80:32150/TCP   14m
```

Как только для параметра "EXTERNAL-IP" состояние `pending` изменится на `IP address`, используйте команду `Control+C`, чтобы остановить процесс отслеживания kubectl.

```
deadly-squid-java   10.0.141.72   52.175.224.118   80:32150/TCP   17m
```

Чтобы увидеть приложение, откройте в браузере внешний IP-адрес.

```console
curl 52.175.224.118
```

Выходные данные:

```
Hello World, I'm Java
```

## <a name="iterate-on-the-application"></a>Выполнение итерации приложения

Теперь, когда Draft настроен, а приложение выполняется в Kubernetes, можно настроить итерацию кода. Каждый раз, когда необходимо протестировать обновленный код, выполните команду `draft up`, чтобы обновить выполняющееся приложение.

Например, обновление приложения Java Hello World.

```console
vi src/main/java/helloworld/Hello.java
```

Обновите текст Hello World.

```java
package helloworld;

import static spark.Spark.*;

public class Hello {
    public static void main(String[] args) {
        get("/", (req, res) -> "Hello World, I'm Java - Draft Rocks!");
    }
}
```

Выполните команду `draft up` для повторного развертывания приложения.

```console
draft up
```

Выходные данные

```
Draft Up Started: 'deadly-squid'
deadly-squid: Building Docker Image: SUCCESS ⚓  (18.0813s)
deadly-squid: Pushing Docker Image: SUCCESS ⚓  (7.9394s)
deadly-squid: Releasing Application: SUCCESS ⚓  (6.5005s)
deadly-squid: Build ID: 01BWK8C8X922F5C0HCQ8FT12RR
```

Наконец просмотрите приложение, чтобы просмотреть обновления.

```console
curl 52.175.224.118
```

Выходные данные:

```
Hello World, I'm Java - Draft Rocks!
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о Draft см. в документации Draft на GitHub.

> [!div class="nextstepaction"]
> [Черновик документации][draft-documentation]

<!-- LINKS - external -->
[draft-documentation]: https://github.com/Azure/draft/tree/master/docs
[install-draft]: https://github.com/Azure/draft/blob/master/docs/install.md
[install-helm]: https://github.com/kubernetes/helm/blob/master/docs/install.md
[kubernetes-ingress]: https://kubernetes.io/docs/concepts/services-networking/ingress/
[kubernetes-service-loadbalancer]: https://kubernetes.io/docs/concepts/services-networking/service/#type-loadbalancer

<!-- LINKS - internal -->
[acr-quickstart]: ../container-registry/container-registry-get-started-azure-cli.md
[aks-quickstart]: ./kubernetes-walkthrough.md