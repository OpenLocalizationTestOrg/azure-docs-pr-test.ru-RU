---
title: "aaaDeploy вашего первого приложения tooCloud Foundry в Microsoft Azure | Документы Microsoft"
description: "Развертывание приложения tooCloud Foundry в Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a><span data-ttu-id="b9081-103">Развертывание вашего первого приложения tooCloud Foundry в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b9081-103">Deploy your first app tooCloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="b9081-104">[Cloud Foundry](http://cloudfoundry.org) — это популярная платформа приложений с открытым кодом в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b9081-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="b9081-105">В этой статье показано, как toodeploy и управлять ими на Foundry облачные приложения в среду Azure.</span><span class="sxs-lookup"><span data-stu-id="b9081-105">In this article, we show how toodeploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="b9081-106">Создание среды Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="b9081-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="b9081-107">Существует несколько способов создания среды Cloud Foundry в Azure.</span><span class="sxs-lookup"><span data-stu-id="b9081-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="b9081-108">Используйте hello [предложение жизненно важную Foundry облака] [ pcf-azuremarketplace] в Azure Marketplace hello toocreate стандартной среды, которые включают диспетчер Ops PCF и hello Azure Service Broker.</span><span class="sxs-lookup"><span data-stu-id="b9081-108">Use hello [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in hello Azure Marketplace toocreate a standard environment that includes PCF Ops Manager and hello Azure Service Broker.</span></span> <span data-ttu-id="b9081-109">Можно найти [завершения инструкции] [ pcf-azuremarketplace-pivotaldocs] развертывания hello marketplace предложить в hello жизненно важную документацию.</span><span class="sxs-lookup"><span data-stu-id="b9081-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying hello marketplace offer in hello Pivotal documentation.</span></span>
- <span data-ttu-id="b9081-110">Создайте пользовательскую среду, [развернув Pivotal Cloud Foundry вручную][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="b9081-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="b9081-111">[Развертывание пакетов Foundry облака открытая hello непосредственно] [ oss-cf-bosh] , настроив [BOSH](http://bosh.io) директора виртуальной Машины, которая координирует развертывания hello hello Foundry облачной среды.</span><span class="sxs-lookup"><span data-stu-id="b9081-111">[Deploy hello open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates hello deployment of hello Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b9081-112">При развертывании PCF из hello Azure Marketplace, запишите hello SYSTEMDOMAINURL и требуемые учетные данные администратора hello tooaccess hello жизненно важную Диспетчер приложений, которые описаны в руководстве по развертыванию marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="b9081-112">If you are deploying PCF from hello Azure Marketplace, make a note of hello SYSTEMDOMAINURL and hello admin credentials required tooaccess hello Pivotal Apps Manager, both of which are described in hello marketplace deployment guide.</span></span> <span data-ttu-id="b9081-113">Они имеют необходимые toocomplete этого учебника.</span><span class="sxs-lookup"><span data-stu-id="b9081-113">They are needed toocomplete this tutorial.</span></span> <span data-ttu-id="b9081-114">Для развертываний marketplace hello SYSTEMDOMAINURL находится в форме https://system hello. *IP-адрес*. cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="b9081-114">For marketplace deployments, hello SYSTEMDOMAINURL is in hello form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-toohello-cloud-controller"></a><span data-ttu-id="b9081-115">Подключение toohello контроллера облака</span><span class="sxs-lookup"><span data-stu-id="b9081-115">Connect toohello Cloud Controller</span></span>

<span data-ttu-id="b9081-116">Hello контроллера облака — hello первичная запись точки tooa Foundry облачной среды для развертывания и управления приложениями.</span><span class="sxs-lookup"><span data-stu-id="b9081-116">hello Cloud Controller is hello primary entry point tooa Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="b9081-117">Hello core API контроллера облака (CCAPI) представляет собой API REST, однако он доступен с помощью различных средств.</span><span class="sxs-lookup"><span data-stu-id="b9081-117">hello core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="b9081-118">В этом случае мы взаимодействуют с его помощью hello [CLI Foundry облака][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="b9081-118">In this case, we interact with it through hello [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="b9081-119">Можно установить на Windows, Linux, MacOS или hello CLI, но если вы предпочитаете не tooinstall, он будет доступен предварительно установленных в hello [оболочки облако Azure][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="b9081-119">You can install hello CLI on Linux, MacOS, or Windows, but if you'd prefer not tooinstall it at all, it is available pre-installed in hello [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="b9081-120">toolog в начале `api` toohello SYSTEMDOMAINURL, полученный из развертывания marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="b9081-120">toolog in, prepend `api` toohello SYSTEMDOMAINURL that you obtained from hello marketplace deployment.</span></span> <span data-ttu-id="b9081-121">Поскольку развертывание по умолчанию hello использует самозаверяющий сертификат, следует также добавить hello `skip-ssl-validation` переключения.</span><span class="sxs-lookup"><span data-stu-id="b9081-121">Since hello default deployment uses a self-signed certificate, you should also include hello `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="b9081-122">Все запрашиваемые toolog в toohello контроллера облака.</span><span class="sxs-lookup"><span data-stu-id="b9081-122">You are prompted toolog in toohello Cloud Controller.</span></span> <span data-ttu-id="b9081-123">Используйте hello учетных данных администратора, полученные из шагов развертывания marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="b9081-123">Use hello admin account credentials that you acquired from hello marketplace deployment steps.</span></span>

<span data-ttu-id="b9081-124">Предоставляет облачные Foundry *организаций* и *пробелы* как пространства имен tooisolate hello групп и сред в рамках общего развертывания.</span><span class="sxs-lookup"><span data-stu-id="b9081-124">Cloud Foundry provides *orgs* and *spaces* as namespaces tooisolate hello teams and environments within a shared deployment.</span></span> <span data-ttu-id="b9081-125">Hello PCF marketplace развертывания включает по умолчанию hello *системы* организации и набор областей создания toocontain hello базовые компоненты, как автоматическое масштабирование службы hello и hello Azure service broker.</span><span class="sxs-lookup"><span data-stu-id="b9081-125">hello PCF marketplace deployment includes hello default *system* org and a set of spaces created toocontain hello base components, like hello autoscaling service and hello Azure service broker.</span></span> <span data-ttu-id="b9081-126">Теперь нажмите кнопку hello *системы* пространства.</span><span class="sxs-lookup"><span data-stu-id="b9081-126">For now, choose hello *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="b9081-127">Создание организации и пространства</span><span class="sxs-lookup"><span data-stu-id="b9081-127">Create an org and space</span></span>

<span data-ttu-id="b9081-128">Если ввести `cf apps`, вы видите набор приложений системы, которые были развернуты в пространстве системы hello в системе org. hello</span><span class="sxs-lookup"><span data-stu-id="b9081-128">If you type `cf apps`, you see a set of system applications that have been deployed in hello system space within hello system org.</span></span> 

<span data-ttu-id="b9081-129">Необходимо хранить hello *системы* организации, зарезервированных для приложений системы, таким образом создать toohouse организации и пространство приложении образца.</span><span class="sxs-lookup"><span data-stu-id="b9081-129">You should keep hello *system* org reserved for system applications, so create an org and space toohouse our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="b9081-130">Используйте hello целевой команда tooswitch toohello новой организации и пространства:</span><span class="sxs-lookup"><span data-stu-id="b9081-130">Use hello target command tooswitch toohello new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="b9081-131">Теперь при развертывании приложения, он автоматически создается в новой организации hello и пространства.</span><span class="sxs-lookup"><span data-stu-id="b9081-131">Now, when you deploy an application, it is automatically created in hello new org and space.</span></span> <span data-ttu-id="b9081-132">Введите tooconfirm, который в настоящее время нет приложений в новой организации hello дискового пространства, `cf apps` еще раз.</span><span class="sxs-lookup"><span data-stu-id="b9081-132">tooconfirm that there are currently no apps in hello new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="b9081-133">Дополнительные сведения о организаций и пробелы и как они могут использоваться для управления доступом на основе ролей (RBAC) см. в разделе hello [документации Foundry облака][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="b9081-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see hello [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="b9081-134">Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="b9081-134">Deploy an application</span></span>

<span data-ttu-id="b9081-135">Используем образец приложения Foundry облака, вызывается Hello Spring облака, который написан на языке Java и основании hello [Spring Framework](http://spring.io) и [Spring загрузки](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="b9081-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on hello [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-hello-hello-spring-cloud-repository"></a><span data-ttu-id="b9081-136">Клонирование репозитория облака Spring Hello hello</span><span class="sxs-lookup"><span data-stu-id="b9081-136">Clone hello Hello Spring Cloud repository</span></span>

<span data-ttu-id="b9081-137">Образец Hello Spring облачные приложения Hello можно найти в GitHub.</span><span class="sxs-lookup"><span data-stu-id="b9081-137">hello Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="b9081-138">Клонирует его tooyour среды и преобразовать в новый каталог hello:</span><span class="sxs-lookup"><span data-stu-id="b9081-138">Clone it tooyour environment and change into hello new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a><span data-ttu-id="b9081-139">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="b9081-139">Build hello application</span></span>

<span data-ttu-id="b9081-140">С помощью приложения hello построения [Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="b9081-140">Build hello app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a><span data-ttu-id="b9081-141">Развертывание приложения hello с принудительной отправкой cf</span><span class="sxs-lookup"><span data-stu-id="b9081-141">Deploy hello application with cf push</span></span>

<span data-ttu-id="b9081-142">Большинство приложений tooCloud Foundry можно развернуть с помощью hello `push` команды:</span><span class="sxs-lookup"><span data-stu-id="b9081-142">You can deploy most applications tooCloud Foundry using hello `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="b9081-143">Когда вы *принудительной* Foundry облачные приложения, определяет тип hello приложения (в данном случае приложение Java) и определяет его зависимости (в это случае framework Spring hello).</span><span class="sxs-lookup"><span data-stu-id="b9081-143">When you *push* an application, Cloud Foundry detects hello type of application (in this case, a Java app) and identifies its dependencies (in this case, hello Spring framework).</span></span> <span data-ttu-id="b9081-144">Затем он упаковывает все необходимые toorun кода в автономный образ контейнера, известный как *дроплета*.</span><span class="sxs-lookup"><span data-stu-id="b9081-144">It then packages everything required toorun your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="b9081-145">Наконец расписания Foundry облака hello приложения на одном hello доступных компьютеров в вашей среде и создает URL-адрес, где можно получить доступ, который доступен в hello выходные данные команды hello.</span><span class="sxs-lookup"><span data-stu-id="b9081-145">Finally, Cloud Foundry schedules hello application on one of hello available machines in your environment and creates a URL where you can reach it, which is available in hello output of hello command.</span></span>

![Выходные данные команды cf push][cf-push-output]

<span data-ttu-id="b9081-147">приложение hello spring облако hello toosee, откройте hello предоставленный URL-адрес в браузере:</span><span class="sxs-lookup"><span data-stu-id="b9081-147">toosee hello hello-spring-cloud application, open hello provided URL in your browser:</span></span>

![Пользовательский интерфейс по умолчанию для приложения Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="b9081-149">toolearn Дополнительные сведения о том, что происходит во время `cf push`, в разделе [как поэтапно приложений] [ cf-push-docs] в hello документации Foundry облака.</span><span class="sxs-lookup"><span data-stu-id="b9081-149">toolearn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in hello Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="b9081-150">Просмотр журналов приложения</span><span class="sxs-lookup"><span data-stu-id="b9081-150">View application logs</span></span>

<span data-ttu-id="b9081-151">Можно использовать журналы tooview hello облака Foundry CLI для приложения по имени:</span><span class="sxs-lookup"><span data-stu-id="b9081-151">You can use hello Cloud Foundry CLI tooview logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="b9081-152">По умолчанию hello журналы команда с помощью *заключительного*, который демонстрирует новые журналы, записываемые.</span><span class="sxs-lookup"><span data-stu-id="b9081-152">By default, hello logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="b9081-153">отображается toosee новые журналы, обновите приложение hello spring облако hello в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="b9081-153">toosee new logs appear, refresh hello hello-spring-cloud app in hello browser.</span></span>

<span data-ttu-id="b9081-154">tooview журналы, которые уже были записаны, добавить hello `recent` переключения:</span><span class="sxs-lookup"><span data-stu-id="b9081-154">tooview logs that have already been written, add hello `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a><span data-ttu-id="b9081-155">Масштабирование приложения hello</span><span class="sxs-lookup"><span data-stu-id="b9081-155">Scale hello application</span></span>

<span data-ttu-id="b9081-156">По умолчанию команда `cf push` создает только один экземпляр приложения.</span><span class="sxs-lookup"><span data-stu-id="b9081-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="b9081-157">tooensure высокого уровня доступности и масштабирования включить более высокую пропускную способность, обычно требуется toorun более одного экземпляра приложения.</span><span class="sxs-lookup"><span data-stu-id="b9081-157">tooensure high availability and enable scale out for higher throughput, you generally want toorun more than one instance of your applications.</span></span> <span data-ttu-id="b9081-158">Можно легко масштабировать уже развернутых приложений с помощью hello `scale` команды:</span><span class="sxs-lookup"><span data-stu-id="b9081-158">You can easily scale out already deployed applications using hello `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="b9081-159">Выполнение hello `cf app` команда приложения hello показывает, что облачные Foundry создает другой экземпляр приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b9081-159">Running hello `cf app` command on hello application shows that Cloud Foundry is creating another instance of hello application.</span></span> <span data-ttu-id="b9081-160">После запуска приложения hello Foundry облака автоматически запускает tooit трафика балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b9081-160">Once hello application has started, Cloud Foundry automatically starts load balancing traffic tooit.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b9081-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9081-161">Next steps</span></span>

- <span data-ttu-id="b9081-162">[Hello чтения документации Foundry облака][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="b9081-162">[Read hello Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="b9081-163">[Настройка подключаемого модуля Visual Studio Team Services hello для облака Foundry][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="b9081-163">[Set up hello Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="b9081-164">[Настройка hello сопел аналитика журналов Microsoft для облака Foundry][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="b9081-164">[Configure hello Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png