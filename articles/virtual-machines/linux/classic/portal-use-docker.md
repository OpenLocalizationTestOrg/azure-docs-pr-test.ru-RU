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
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a><span data-ttu-id="4959e-103">Использование hello расширение ВМ Docker с hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="4959e-103">Using hello Docker VM Extension with hello Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="4959e-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4959e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4959e-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="4959e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4959e-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4959e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="4959e-107">[Docker](https://www.docker.com/) является одним из hello наиболее популярных виртуализации подходов, которые использует [контейнеров Linux](http://en.wikipedia.org/wiki/LXC) вместо виртуальных машин как способ разделения данных и вычисления на общих ресурсах.</span><span class="sxs-lookup"><span data-stu-id="4959e-107">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="4959e-108">Можно использовать расширение ВМ Docker hello управляется [агент Azure Linux] toocreate виртуальной Машины Docker, на котором размещена любое число контейнеров для приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="4959e-108">You can use hello Docker VM extension managed by [Azure Linux Agent] toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="4959e-109">В этом разделе описывается, как toocreate a виртуальной Машины Docker из hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4959e-109">This topic describes how toocreate a Docker VM from hello Azure classic portal.</span></span> <span data-ttu-id="4959e-110">toocreate виртуальной Машины Docker hello командной строки, в статье toosee [как toouse hello расширение ВМ Docker из hello Azure командной строки (CLI Azure)].</span><span class="sxs-lookup"><span data-stu-id="4959e-110">toosee how toocreate a Docker VM at hello command line, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="4959e-111">toosee общие обсуждения контейнеров и их преимущества, в разделе hello [Docker высокий уровень доски](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="4959e-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a><span data-ttu-id="4959e-112">Создание новой виртуальной Машины из коллекции образов hello</span><span class="sxs-lookup"><span data-stu-id="4959e-112">Create a new VM from hello Image Gallery</span></span>
<span data-ttu-id="4959e-113">Первым шагом Hello требуется Виртуальной машине Azure из образа Linux, который поддерживает расширение ВМ Docker, используя Ubuntu 14.04 LTS образ из коллекции образов hello в качестве образа сервера пример и Ubuntu 14.04 Desktop как клиент hello.</span><span class="sxs-lookup"><span data-stu-id="4959e-113">hello first step requires an Azure VM from a Linux image that supports hello Docker VM Extension, using an Ubuntu 14.04 LTS image from hello Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="4959e-114">На портале hello щелкните **+ создать** в hello левый нижний угол toocreate новый экземпляр виртуальной Машины и выберите изображение Ubuntu 14.04 LTS из доступные варианты hello или hello завершения коллекция изображений, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4959e-114">In hello portal, click **+ New** in hello bottom left corner toocreate a new VM instance and select an Ubuntu 14.04 LTS image from hello selections available or from hello complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="4959e-115">В настоящее время только изображения Ubuntu 14.04 LTS, более свежие, чем июль 2014 г. поддерживает hello расширение ВМ Docker.</span><span class="sxs-lookup"><span data-stu-id="4959e-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support hello Docker VM Extension.</span></span>
> 
> 

![Создание нового образа Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="4959e-117">Создание сертификатов Docker</span><span class="sxs-lookup"><span data-stu-id="4959e-117">Create Docker Certificates</span></span>
<span data-ttu-id="4959e-118">После hello будет создана виртуальная машина, убедитесь, что Docker установлен на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="4959e-118">After hello VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="4959e-119">(Подробные инструкции по установке Docker см. по [этой ссылке](https://docs.docker.com/installation/#installation)).</span><span class="sxs-lookup"><span data-stu-id="4959e-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="4959e-120">Создать сертификат и ключ файлов для обмена данными Docker слишком в соответствии с hello[под управлением Docker с помощью протокола https] и помещать их в hello  **`~/.docker`**  каталог на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="4959e-120">Create hello certificate and key files for Docker communication according too[Running Docker with https] and place them in hello **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="4959e-121">в настоящее время Hello расширение ВМ Docker на портале hello требует учетные данные, закодированные методом base64.</span><span class="sxs-lookup"><span data-stu-id="4959e-121">hello Docker VM Extension in hello portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="4959e-122">В командной строке hello с помощью  **`base64`**  или другой избранного кодирования средство toocreate кодировке base64 разделы.</span><span class="sxs-lookup"><span data-stu-id="4959e-122">At hello command line, use **`base64`** or another favorite encoding tool toocreate base64-encoded topics.</span></span> <span data-ttu-id="4959e-123">Таким образом с простым набором файлов сертификатов и ключей может выглядеть примерно toothis:</span><span class="sxs-lookup"><span data-stu-id="4959e-123">Doing this with a simple set of certificate and key files might look similar toothis:</span></span>

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

## <a name="add-hello-docker-vm-extension"></a><span data-ttu-id="4959e-124">Добавить расширение ВМ Docker hello</span><span class="sxs-lookup"><span data-stu-id="4959e-124">Add hello Docker VM Extension</span></span>
<span data-ttu-id="4959e-125">tooadd hello расширение ВМ Docker найдите созданный экземпляр виртуальной Машины hello и прокрутите вниз слишком**расширения** и щелкните его toobring копирование расширений ВМ, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4959e-125">tooadd hello Docker VM Extension, locate hello VM instance you created and scroll down too**Extensions** and click it toobring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="4959e-126">Эта функция поддерживается в hello предварительной версии портала: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="4959e-126">This functionality is supported in hello preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="4959e-127">Добавление расширения</span><span class="sxs-lookup"><span data-stu-id="4959e-127">Add an Extension</span></span>
<span data-ttu-id="4959e-128">Нажмите кнопку hello **+ добавить** toodisplay hello возможных расширений виртуальной Машины, можно добавить toothis виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4959e-128">Click hello **+ Add** toodisplay hello possible VM Extensions you can add toothis VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a><span data-ttu-id="4959e-129">Выберите расширение ВМ Docker hello</span><span class="sxs-lookup"><span data-stu-id="4959e-129">Select hello Docker VM Extension</span></span>
<span data-ttu-id="4959e-130">Выберите hello расширение ВМ Docker, которая вызывает описание Docker hello и важных ссылок, а затем нажмите кнопку **создать** в процедуре установки hello toobegin нижней hello.</span><span class="sxs-lookup"><span data-stu-id="4959e-130">Choose hello Docker VM Extension, which brings up hello Docker description and important links, and then click **Create** at hello bottom toobegin hello installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="4959e-131">Добавление файлов сертификатов и ключей.</span><span class="sxs-lookup"><span data-stu-id="4959e-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="4959e-132">В полях формы hello введите hello кодировке base64 версии вашего сертификата ЦС, сертификат сервера и ключа сервера, как показано в следующих график hello.</span><span class="sxs-lookup"><span data-stu-id="4959e-132">In hello form fields, enter hello base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in hello following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="4959e-133">Обратите внимание, что (как hello предшествующий изображения) hello 2376 заполняется по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4959e-133">Note that (as in hello preceding image) hello 2376 is filled in by default.</span></span> <span data-ttu-id="4959e-134">Можно ввести любой конечной точки, но hello следующим шагом будет tooopen копирование hello совпадения конечной точки.</span><span class="sxs-lookup"><span data-stu-id="4959e-134">You can enter any endpoint here, but hello next step will be tooopen up hello matching endpoint.</span></span> <span data-ttu-id="4959e-135">При изменении по умолчанию hello, убедитесь, что tooopen копирование hello совпадения конечной точки в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="4959e-135">If you change hello default, make sure tooopen up hello matching endpoint in hello next step.</span></span>
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a><span data-ttu-id="4959e-136">Добавить hello Docker для взаимодействия</span><span class="sxs-lookup"><span data-stu-id="4959e-136">Add hello Docker Communication Endpoint</span></span>
<span data-ttu-id="4959e-137">При просмотре hello группы ресурсов, вы создали, выберите hello связанные группы безопасности сети с ВМ и нажмите кнопку **правила для входящих подключений безопасности** tooview hello правила, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4959e-137">When viewing hello resource group you've created, select hello Network Security Group associated with your VM, and click **Inbound Security Rules** tooview hello rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="4959e-138">Нажмите кнопку **+ добавить** tooadd другого правила, а в случае по умолчанию hello, введите имя для конечной точки hello (в этом примере **Docker**) и диапазон портов, 2376 «назначения».</span><span class="sxs-lookup"><span data-stu-id="4959e-138">Click **+ Add** tooadd another rule, and in hello default case, enter a name for hello endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="4959e-139">Задайте значение отображение hello протокола **TCP**и нажмите кнопку **ОК** toocreate hello правило.</span><span class="sxs-lookup"><span data-stu-id="4959e-139">Set hello protocol value showing **TCP**, and Click **OK** toocreate hello rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="4959e-140">Тестирование клиента Docker и узла Docker в Azure</span><span class="sxs-lookup"><span data-stu-id="4959e-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="4959e-141">Найдите и скопируйте hello имя домена Виртуальной машины, а hello командной строки для клиентского компьютера, тип `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (где *dockerextension* заменяется hello дочерний домен для виртуальной Машины).</span><span class="sxs-lookup"><span data-stu-id="4959e-141">Locate and copy hello name of your VM's domain, and at hello command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by hello subdomain for your VM).</span></span>

<span data-ttu-id="4959e-142">Hello результат должен выглядеть примерно toothis:</span><span class="sxs-lookup"><span data-stu-id="4959e-142">hello result should appear similar toothis:</span></span>

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

<span data-ttu-id="4959e-143">После завершения hello выше шаги, теперь у вас есть полнофункциональный узел Docker, работающих на Виртуальной машине Azure, настроить toobe подключен tooremotely с других клиентов.</span><span class="sxs-lookup"><span data-stu-id="4959e-143">Once you complete hello above steps, you now have a fully functional Docker host running on an Azure VM, configured toobe connected tooremotely from other clients.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="4959e-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4959e-144">Next steps</span></span>
<span data-ttu-id="4959e-145">Будут готовы toogo toohello [руководство пользователя по Docker] и использовать ВМ Docker.</span><span class="sxs-lookup"><span data-stu-id="4959e-145">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="4959e-146">Tooautomate создании узлах Docker на виртуальных машинах Azure через интерфейс командной строки см [как toouse hello расширение ВМ Docker из hello Azure командной строки (CLI Azure)]</span><span class="sxs-lookup"><span data-stu-id="4959e-146">If you want tooautomate creating Docker hosts on Azure VMs through command line interface, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)]</span></span>

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
