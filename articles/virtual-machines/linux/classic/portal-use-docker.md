---
title: "aaaUsing расширение ВМ Docker для Linux | Документы Microsoft"
description: "Описывает Docker и расширений виртуальных машин Azure hello и как toocreate виртуальных машинах Azure, которые являются узлами docker с помощью hello Azure CLI в классической модели развертывания."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a>Использование hello расширение ВМ Docker с hello классический портал Azure
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

[Docker](https://www.docker.com/) является одним из hello наиболее популярных виртуализации подходов, которые использует [контейнеров Linux](http://en.wikipedia.org/wiki/LXC) вместо виртуальных машин как способ разделения данных и вычисления на общих ресурсах. Можно использовать расширение ВМ Docker hello управляется [агент Azure Linux] toocreate виртуальной Машины Docker, на котором размещена любое число контейнеров для приложений в Azure.

> [!NOTE]
> В этом разделе описывается, как toocreate a виртуальной Машины Docker из hello классический портал Azure. toocreate виртуальной Машины Docker hello командной строки, в статье toosee [как toouse hello расширение ВМ Docker из hello Azure командной строки (CLI Azure)]. toosee общие обсуждения контейнеров и их преимущества, в разделе hello [Docker высокий уровень доски](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a>Создание новой виртуальной Машины из коллекции образов hello
Первым шагом Hello требуется Виртуальной машине Azure из образа Linux, который поддерживает расширение ВМ Docker, используя Ubuntu 14.04 LTS образ из коллекции образов hello в качестве образа сервера пример и Ubuntu 14.04 Desktop как клиент hello. На портале hello щелкните **+ создать** в hello левый нижний угол toocreate новый экземпляр виртуальной Машины и выберите изображение Ubuntu 14.04 LTS из доступные варианты hello или hello завершения коллекция изображений, как показано ниже.

> [!NOTE]
> В настоящее время только изображения Ubuntu 14.04 LTS, более свежие, чем июль 2014 г. поддерживает hello расширение ВМ Docker.
> 
> 

![Создание нового образа Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a>Создание сертификатов Docker
После hello будет создана виртуальная машина, убедитесь, что Docker установлен на клиентском компьютере. (Подробные инструкции по установке Docker см. по [этой ссылке](https://docs.docker.com/installation/#installation)).

Создать сертификат и ключ файлов для обмена данными Docker слишком в соответствии с hello[под управлением Docker с помощью протокола https] и помещать их в hello  **`~/.docker`**  каталог на клиентском компьютере.

> [!NOTE]
> в настоящее время Hello расширение ВМ Docker на портале hello требует учетные данные, закодированные методом base64.
> 
> 

В командной строке hello с помощью  **`base64`**  или другой избранного кодирования средство toocreate кодировке base64 разделы. Таким образом с простым набором файлов сертификатов и ключей может выглядеть примерно toothis:

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a>Добавить расширение ВМ Docker hello
tooadd hello расширение ВМ Docker найдите созданный экземпляр виртуальной Машины hello и прокрутите вниз слишком**расширения** и щелкните его toobring копирование расширений ВМ, как показано ниже.

> [!NOTE]
> Эта функция поддерживается в hello предварительной версии портала: https://portal.azure.com/
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a>Добавление расширения
Нажмите кнопку hello **+ добавить** toodisplay hello возможных расширений виртуальной Машины, можно добавить toothis виртуальной Машины.

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a>Выберите расширение ВМ Docker hello
Выберите hello расширение ВМ Docker, которая вызывает описание Docker hello и важных ссылок, а затем нажмите кнопку **создать** в процедуре установки hello toobegin нижней hello.

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a>Добавление файлов сертификатов и ключей.
В полях формы hello введите hello кодировке base64 версии вашего сертификата ЦС, сертификат сервера и ключа сервера, как показано в следующих график hello.

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> Обратите внимание, что (как hello предшествующий изображения) hello 2376 заполняется по умолчанию. Можно ввести любой конечной точки, но hello следующим шагом будет tooopen копирование hello совпадения конечной точки. При изменении по умолчанию hello, убедитесь, что tooopen копирование hello совпадения конечной точки в следующем шаге hello.
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a>Добавить hello Docker для взаимодействия
При просмотре hello группы ресурсов, вы создали, выберите hello связанные группы безопасности сети с ВМ и нажмите кнопку **правила для входящих подключений безопасности** tooview hello правила, как показано ниже.

![](media/portal-use-docker/AddingEndpoint.png)

Нажмите кнопку **+ добавить** tooadd другого правила, а в случае по умолчанию hello, введите имя для конечной точки hello (в этом примере **Docker**) и диапазон портов, 2376 «назначения». Задайте значение отображение hello протокола **TCP**и нажмите кнопку **ОК** toocreate hello правило.

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a>Тестирование клиента Docker и узла Docker в Azure
Найдите и скопируйте hello имя домена Виртуальной машины, а hello командной строки для клиентского компьютера, тип `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (где *dockerextension* заменяется hello дочерний домен для виртуальной Машины).

Hello результат должен выглядеть примерно toothis:

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

После завершения hello выше шаги, теперь у вас есть полнофункциональный узел Docker, работающих на Виртуальной машине Azure, настроить toobe подключен tooremotely с других клиентов.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Дальнейшие действия
Будут готовы toogo toohello [руководство пользователя по Docker] и использовать ВМ Docker. Tooautomate создании узлах Docker на виртуальных машинах Azure через интерфейс командной строки см [как toouse hello расширение ВМ Docker из hello Azure командной строки (CLI Azure)]

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[как toouse hello расширение ВМ Docker из hello Azure командной строки (CLI Azure)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[агент Azure Linux]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[под управлением Docker с помощью протокола https]:http://docs.docker.com/articles/https/
[руководство пользователя по Docker]:https://docs.docker.com/userguide/
