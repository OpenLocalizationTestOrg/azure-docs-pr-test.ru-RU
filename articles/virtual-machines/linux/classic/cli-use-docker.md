---
title: "hello aaaUsing расширение ВМ Docker для Linux в Azure"
description: "Описывает Docker и расширения виртуальных машин Azure hello и показано, как tooprogrammatically создать виртуальные машины в Azure, которые узлы docker из командной строки hello, с помощью hello Azure CLI."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a>С помощью hello расширение ВМ Docker из hello Azure командной строки (CLI Azure)
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Сведения об использовании hello расширение ВМ Docker с моделью hello диспетчера ресурсов см. в разделе [здесь](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Описывается, как toocreate виртуальную Машину с hello расширение ВМ Docker из hello службы режим управления (asm) в Azure CLI на любой платформе. [Docker](https://www.docker.com/) является одним из hello наиболее популярных виртуализации подходов, которые использует [контейнеров Linux](http://en.wikipedia.org/wiki/LXC) вместо виртуальных машин как способ разделения данных и вычисления на общих ресурсах. Можно использовать расширение ВМ Docker hello и hello [агент Azure Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate виртуальной Машины Docker, на котором размещена любое число контейнеров для приложений в Azure. toosee общие обсуждения контейнеров и их преимущества, в разделе hello [Docker высокий уровень доски](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a>Как toouse hello расширение ВМ Docker с помощью Azure
расширение виртуальной Машины Docker hello toouse с Azure, необходимо установить версию hello [интерфейса командной строки Azure](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) выше, чем 0.8.6 (как для этой записи hello текущей версии 0.10.0). Hello Azure CLI можно установить на Mac, Linux и Windows.

Hello полный процесс toouse Docker в Azure очень простой:

* Установите на компьютере hello, из которого нужно toocontrol Azure hello Azure CLI и его зависимости (в Windows, это будет дистрибутив Linux, выполняющийся как виртуальная машина)
* Использовать toocreate команды Azure CLI Docker hello узла виртуальной Машины Docker в Azure
* Используйте hello локального Docker команды toomanage в контейнеры Docker в ВМ Docker в Azure.

### <a name="install-hello-azure-command-line-interface-azure-cli"></a>Установка hello Azure командной строки (CLI Azure)
tooinstall и настроить hello Azure CLI см. в разделе [как tooinstall hello интерфейса командной строки Azure](../../../cli-install-nodejs.md). Установка tooconfirm hello, тип `azure` hello командной строки и через некоторое короткое время вы увидите доступные tooyou команды hello Azure CLI ASCII-графики, который содержит список hello basic. Если установки hello работал правильно, можно будет tootype `azure help vm` и увидеть, что одной из команд hello в списке «docker».

> [!NOTE]
> Docker содержит средства для Windows, [машины Docker](https://docs.docker.com/installation/windows/), который можно также использовать tooautomate hello создание клиента docker, можно использовать toowork с виртуальными машинами Azure в качестве узлов docker.
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a>Подключение hello Azure CLI tootooyour учетной записи Azure
Прежде чем использовать hello Azure CLI необходимо связать учетные данные учетной записи Azure с hello Azure CLI для конкретной платформы. Здравствуйте, раздел [как tooconnect tooyour подписки Azure](../../../xplat-cli-connect.md) объясняет, как загрузить и импортировать tooeither вашей **.publishsettings** файл или связать с ИД организации в Azure CLI.

> [!NOTE]
> Существуют некоторые отличия в поведении при использовании одной или hello других методов проверки подлинности, следует убедиться, что документ hello tooread выше toounderstand hello различаются по функциональности.
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a>Установка Docker и использовать расширение ВМ Docker hello Azure
Выполните hello [инструкции по установке Docker](https://docs.docker.com/installation/#installation) tooinstall Docker на локальном компьютере.

toouse Docker с виртуальной машины Azure hello Linux изображение, используемое для hello виртуальной Машины должен иметь hello [агент ВМ Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) установлен. В настоящее время это обеспечивается только двумя типами образов:

* Ubuntu образ из коллекции образов Azure hello или
* Настраиваемое изображение Linux, созданного с помощью hello агента ВМ Azure Linux установлен и настроен. В разделе [агент ВМ Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Дополнительные сведения о том, как toobuild пользовательские виртуальной Машины Linux с hello агента ВМ Azure.

### <a name="using-hello-azure-image-gallery"></a>С помощью коллекции образов Azure hello
В Bash или сеанс используйте следующую команду Azure CLI toolocate hello самый последний Ubuntu образ в коллекции toouse hello виртуальной Машины, введя hello

`azure vm image list | grep Ubuntu-14_04`

и выберите одно из имен изображения hello, такие как `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, и используйте hello следующая команда toocreate новой виртуальной Машины с помощью данного образа.

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

Описание:

* *&lt;имя виртуальной машины cloudservice&gt;*  — имя hello hello виртуальной Машины, которая станет hello компьютер указанный контейнер Docker в Azure
* *&lt;имя пользователя&gt;*  пользователя hello корневого пользователя по умолчанию hello hello виртуальной Машины
* *&lt;пароль&gt;*  — пароль hello hello *username* учетную запись, которая соответствует стандартам hello сложности для Azure

> [!NOTE]
> В настоящее время пароль должен быть по крайней мере 8 символов, содержать одной прописной и одну прописную букву, число и специальный символ, такой как один из hello следующие символы: `!@#$%^&+=`. Нет, период hello в конце hello hello предшествующий предложения не специальный символ.
> 
> 

При успешном выполнении команды hello, вы увидите нечто похожее на следующее hello, в зависимости от hello точные аргументы и параметры, которые вы использовали:

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> Создание виртуальной машины может занять несколько минут, но после того, как он был инициализирован (значение hello `ReadyRole`) hello запуска управляющей программы (hello службу Docker) Docker, можно подключить toohello узла контейнера Docker.
> 
> 

hello tootest Docker виртуальных Машин, созданных в Azure, тип

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

где  *&lt;vm-name--использовалась&gt;*  является именем hello hello виртуальной машины, который использовался при вызове слишком`azure vm docker create`. Вы увидите, что-нибудь подобное toohello следующее, что указывает, что узел Docker ВМ работает в Azure и ожидания команды. 

Теперь можно попробовать tooconnect использует информацию tooobtain клиента docker (в некоторых настроек клиента Docker, например, на Mac, может возникнуть toouse `sudo`):

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

Просто toobe убедиться, что все работы, можно изучить hello виртуальной Машины для hello расширения Docker:

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a>Проверка подлинности виртуальной машины узла Docker
Кроме hello hello toocreating ВМ Docker `azure vm docker create` команда также автоматически создает необходимые сертификаты tooallow hello клиентского компьютера tooconnect toohello контейнер Azure узла Docker с помощью протокола HTTPS и hello сертификаты хранятся на обоих Hello клиентского и главного компьютеров соответствующим образом. При последующих попытках существующих сертификатов hello повторно и совместно с новым узлом hello.

По умолчанию сертификаты помещаются в `~/.docker`, и Docker будут toorun настроенный порт **2376**. Если вы хотите toouse другой порт или каталог, то можно использовать один из следующих hello `azure vm docker create` tooconfigure параметры командной строки к Docker контейнера узла виртуальной Машины toouse другой порт или разные сертификаты при подключении клиентов:

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

Hello управляющая программа Docker на узле hello является настроенным toolisten для и пройти проверку подлинности клиентских подключений на hello указанный порт, используя hello сертификаты, созданные hello `azure vm docker create` команды. Hello клиентский компьютер должен иметь эти сертификаты toogain доступа toohello Docker узла.

> [!NOTE]
> Узел сети, работающих без эти сертификаты будут уязвимыми tooanyone, можно tooconnect toohello машины. Перед изменением конфигурации по умолчанию hello, убедитесь, что вы понимаете hello рисков tooyour компьютеры и приложения.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* Будут готовы toogo toohello [руководство пользователя по Docker] и использовать ВМ Docker. . в разделе toocreate поддержкой Docker виртуальной Машины в новый портал hello, [как toouse hello расширение ВМ Docker с hello портала].
* Hello расширение ВМ Docker Azure также поддерживает Docker Compose, использующий декларативный tootake файл YAML приложении моделируется разработчика любой среде и создания согласованного развертывания. В разделе [начало работы с Docker и составлять toodefine и запустите приложение контейнера несколькими на виртуальной машине Azure].  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[как toouse hello расширение ВМ Docker с hello портала]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[руководство пользователя по Docker]:https://docs.docker.com/userguide/

[начало работы с Docker и составлять toodefine и запустите приложение контейнера несколькими на виртуальной машине Azure]:../docker-compose-quickstart.md
