---
title: "Использование расширения виртуальных машин Docker для Linux | Документация Майкрософт"
description: "Описывает расширения виртуальных машин Azure и Docker, а также создание виртуальных машин Azure, являющихся узлами Docker, с помощью Azure CLI в классической модели развертывания."
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
ms.openlocfilehash: 932744208d9d53c87e31dcdf9e34539750be4bdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-docker-vm-extension-with-the-azure-classic-portal"></a><span data-ttu-id="d74a9-103">Использование расширения виртуальных машин Docker на классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="d74a9-103">Using the Docker VM Extension with the Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="d74a9-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d74a9-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d74a9-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="d74a9-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d74a9-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d74a9-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="d74a9-107">[Docker](https://www.docker.com/) — один из самых популярных подходов к виртуализации, использующий [контейнеры Linux](http://en.wikipedia.org/wiki/LXC) вместо виртуальных машин как способ изоляции данных и вычислений при использовании общих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d74a9-107">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="d74a9-108">Вы можете использовать расширение виртуальных машин Docker, управляемое [агентом Linux для Azure] , чтобы создать виртуальную машину Docker, в которой будет размещено любое количество контейнеров с приложениями в Azure.</span><span class="sxs-lookup"><span data-stu-id="d74a9-108">You can use the Docker VM extension managed by [Azure Linux Agent] to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="d74a9-109">В этом разделе описывается создание виртуальной машины Docker на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d74a9-109">This topic describes how to create a Docker VM from the Azure classic portal.</span></span> <span data-ttu-id="d74a9-110">Сведения о создании виртуальной машины Docker с помощью командной строки см. в статье [Использование расширения виртуальных машин Docker в интерфейсе командной строки Azure (CLI Azure)].</span><span class="sxs-lookup"><span data-stu-id="d74a9-110">To see how to create a Docker VM at the command line, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="d74a9-111">Обзорное обсуждение контейнеров и их преимуществ см. на [доске по Docker](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="d74a9-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-the-image-gallery"></a><span data-ttu-id="d74a9-112">Создание новой виртуальной машины в коллекции образов</span><span class="sxs-lookup"><span data-stu-id="d74a9-112">Create a new VM from the Image Gallery</span></span>
<span data-ttu-id="d74a9-113">На первом этапе необходима виртуальная машина Azure на основе образа Linux, который поддерживает расширение виртуальных машин Docker. Пример образа сервера из коллекции образов — Ubuntu 14.04 LTS, пример образа клиента — Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="d74a9-113">The first step requires an Azure VM from a Linux image that supports the Docker VM Extension, using an Ubuntu 14.04 LTS image from the Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="d74a9-114">На портале в нижнем левом углу нажмите кнопку **+ Создать**, чтобы создать экземпляр виртуальной машины, и выберите образ Ubuntu 14.04 LTS из доступных вариантов или из полной коллекции образов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d74a9-114">In the portal, click **+ New** in the bottom left corner to create a new VM instance and select an Ubuntu 14.04 LTS image from the selections available or from the complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="d74a9-115">В настоящее время расширение виртуальных машин Docker поддерживается только в образах Ubuntu 14.04 LTS, созданных позже июля 2014 г.</span><span class="sxs-lookup"><span data-stu-id="d74a9-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support the Docker VM Extension.</span></span>
> 
> 

![Создание нового образа Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="d74a9-117">Создание сертификатов Docker</span><span class="sxs-lookup"><span data-stu-id="d74a9-117">Create Docker Certificates</span></span>
<span data-ttu-id="d74a9-118">После создания виртуальной машины убедитесь, что Docker установлен на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="d74a9-118">After the VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="d74a9-119">(Подробные инструкции по установке Docker см. по [этой ссылке](https://docs.docker.com/installation/#installation)).</span><span class="sxs-lookup"><span data-stu-id="d74a9-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="d74a9-120">Создайте файлы сертификата и ключа для соединения Docker (сведения о запуске Docker с использованием https см. по [этой ссылке]) и поместите их в каталог **`~/.docker`** на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="d74a9-120">Create the certificate and key files for Docker communication according to [Running Docker with https] and place them in the **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="d74a9-121">В настоящее время для расширения виртуальных машин Docker на портале необходимы учетные данные с кодировкой base64.</span><span class="sxs-lookup"><span data-stu-id="d74a9-121">The Docker VM Extension in the portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="d74a9-122">В командной строке используйте **`base64`** или другой предпочитаемый инструмент кодирования для создания разделов с кодировкой base64.</span><span class="sxs-lookup"><span data-stu-id="d74a9-122">At the command line, use **`base64`** or another favorite encoding tool to create base64-encoded topics.</span></span> <span data-ttu-id="d74a9-123">Пример для простого набора файлов сертификатов и ключей:</span><span class="sxs-lookup"><span data-stu-id="d74a9-123">Doing this with a simple set of certificate and key files might look similar to this:</span></span>

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

## <a name="add-the-docker-vm-extension"></a><span data-ttu-id="d74a9-124">Добавление расширения виртуальных машин Docker</span><span class="sxs-lookup"><span data-stu-id="d74a9-124">Add the Docker VM Extension</span></span>
<span data-ttu-id="d74a9-125">Для добавления расширения виртуальных машин Docker найдите созданный экземпляр виртуальной машины и щелкните **Расширения**, чтобы открыть расширения виртуальных машин (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="d74a9-125">To add the Docker VM Extension, locate the VM instance you created and scroll down to **Extensions** and click it to bring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="d74a9-126">Эта функциональность поддерживается только на портале предварительной версии: https://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="d74a9-126">This functionality is supported in the preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="d74a9-127">Добавление расширения</span><span class="sxs-lookup"><span data-stu-id="d74a9-127">Add an Extension</span></span>
<span data-ttu-id="d74a9-128">Щелкните **+ Добавить** , чтобы просмотреть расширения, которые можно добавить к этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="d74a9-128">Click the **+ Add** to display the possible VM Extensions you can add to this VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-the-docker-vm-extension"></a><span data-ttu-id="d74a9-129">Выбор расширения виртуальных машин Docker</span><span class="sxs-lookup"><span data-stu-id="d74a9-129">Select the Docker VM Extension</span></span>
<span data-ttu-id="d74a9-130">Выберите расширение виртуальных машин Docker, которое обеспечит описание Docker и важные ссылки, и нажмите кнопку **Создать** внизу, чтобы начать процедуру установки.</span><span class="sxs-lookup"><span data-stu-id="d74a9-130">Choose the Docker VM Extension, which brings up the Docker description and important links, and then click **Create** at the bottom to begin the installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="d74a9-131">Добавление файлов сертификатов и ключей.</span><span class="sxs-lookup"><span data-stu-id="d74a9-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="d74a9-132">В полях формы введите версии сертификата ЦС, сертификата сервера и ключа сервера в кодировке base64, как показано на следующем графике.</span><span class="sxs-lookup"><span data-stu-id="d74a9-132">In the form fields, enter the base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in the following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="d74a9-133">Обратите внимание, что значение 2376 заполнено по умолчанию (как показано на предыдущем рисунке).</span><span class="sxs-lookup"><span data-stu-id="d74a9-133">Note that (as in the preceding image) the 2376 is filled in by default.</span></span> <span data-ttu-id="d74a9-134">Здесь можно указать любую конечную точку, однако на следующем этапе потребуется открыть соответствующую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="d74a9-134">You can enter any endpoint here, but the next step will be to open up the matching endpoint.</span></span> <span data-ttu-id="d74a9-135">Изменяя значение по умолчанию, на следующем этапе откройте соответствующую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="d74a9-135">If you change the default, make sure to open up the matching endpoint in the next step.</span></span>
> 
> 

## <a name="add-the-docker-communication-endpoint"></a><span data-ttu-id="d74a9-136">Добавление конечной точки соединения Docker</span><span class="sxs-lookup"><span data-stu-id="d74a9-136">Add the Docker Communication Endpoint</span></span>
<span data-ttu-id="d74a9-137">При просмотре созданной группы ресурсов выберите группу безопасности сети, связанную с вашей виртуальной машиной, и щелкните **Правила безопасности для входящего трафика** , чтобы просмотреть правила, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d74a9-137">When viewing the resource group you've created, select the Network Security Group associated with your VM, and click **Inbound Security Rules** to view the rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="d74a9-138">Щелкните **+ Добавить**, чтобы добавить еще одно правило, и, в случае по умолчанию, введите имя конечной точки (в этом примере — **Docker**) и значение 2376 в поле "Диапазон конечных портов".</span><span class="sxs-lookup"><span data-stu-id="d74a9-138">Click **+ Add** to add another rule, and in the default case, enter a name for the endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="d74a9-139">Укажите протокол **TCP** и нажмите кнопку **OK**, чтобы создать правило.</span><span class="sxs-lookup"><span data-stu-id="d74a9-139">Set the protocol value showing **TCP**, and Click **OK** to create the rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="d74a9-140">Тестирование клиента Docker и узла Docker в Azure</span><span class="sxs-lookup"><span data-stu-id="d74a9-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="d74a9-141">Найдите и скопируйте имя домена виртуальной машины, затем в командной строке клиентского компьютера введите `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (замените *dockerextension* поддоменом виртуальной машины).</span><span class="sxs-lookup"><span data-stu-id="d74a9-141">Locate and copy the name of your VM's domain, and at the command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by the subdomain for your VM).</span></span>

<span data-ttu-id="d74a9-142">Результат должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d74a9-142">The result should appear similar to this:</span></span>

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

<span data-ttu-id="d74a9-143">После завершения описанных выше действий вы получаете полнофункциональный узел Docker, выполняемый в виртуальной машине Azure и настроенный на удаленное подключение с других клиентов.</span><span class="sxs-lookup"><span data-stu-id="d74a9-143">Once you complete the above steps, you now have a fully functional Docker host running on an Azure VM, configured to be connected to remotely from other clients.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="d74a9-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d74a9-144">Next steps</span></span>
<span data-ttu-id="d74a9-145">Переходите к [руководству пользователя Docker] и использованию виртуальной машины Docker.</span><span class="sxs-lookup"><span data-stu-id="d74a9-145">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="d74a9-146">Если нужно автоматизировать создание узлов Docker на виртуальных машинах Azure через интерфейс командной строки, см. статью [Использование расширения виртуальных машин Docker в интерфейсе командной строки Azure (CLI Azure)].</span><span class="sxs-lookup"><span data-stu-id="d74a9-146">If you want to automate creating Docker hosts on Azure VMs through command line interface, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from the Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add the Docker VM Extension]:#adddockerextension
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
<span data-ttu-id="d74a9-147">[Использование расширения виртуальных машин Docker в интерфейсе командной строки Azure (CLI Azure)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/</span><span class="sxs-lookup"><span data-stu-id="d74a9-147">[How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/</span></span>
<span data-ttu-id="d74a9-148">[агентом Linux для Azure]:../agent-user-guide.md</span><span class="sxs-lookup"><span data-stu-id="d74a9-148">[Azure Linux Agent]:../agent-user-guide.md</span></span>
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md

<span data-ttu-id="d74a9-149">[этой ссылке]:http://docs.docker.com/articles/https/</span><span class="sxs-lookup"><span data-stu-id="d74a9-149">[Running Docker with https]:http://docs.docker.com/articles/https/</span></span>
<span data-ttu-id="d74a9-150">[руководству пользователя Docker]:https://docs.docker.com/userguide/</span><span class="sxs-lookup"><span data-stu-id="d74a9-150">[Docker User Guide]:https://docs.docker.com/userguide/</span></span>
