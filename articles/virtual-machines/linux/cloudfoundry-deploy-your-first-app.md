---
title: "Развертывание первого приложения в Cloud Foundry в Microsoft Azure | Документация Майкрософт"
description: "Сведения о развертывании приложения в Cloud Foundry в Azure"
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
ms.openlocfilehash: b617127fc0a3f8dcae293e356ea669edcfa5deff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-your-first-app-to-cloud-foundry-on-microsoft-azure"></a><span data-ttu-id="b34bc-103">Развертывание первого приложения в Cloud Foundry в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b34bc-103">Deploy your first app to Cloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="b34bc-104">[Cloud Foundry](http://cloudfoundry.org) — это популярная платформа приложений с открытым кодом в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b34bc-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="b34bc-105">В этой статье рассматривается развертывание приложения в Cloud Foundry в среде Azure и управление им.</span><span class="sxs-lookup"><span data-stu-id="b34bc-105">In this article, we show how to deploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="b34bc-106">Создание среды Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="b34bc-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="b34bc-107">Существует несколько способов создания среды Cloud Foundry в Azure.</span><span class="sxs-lookup"><span data-stu-id="b34bc-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="b34bc-108">Используйте [предложение Pivotal Cloud Foundry][pcf-azuremarketplace] в Azure Marketplace для создания стандартной среды, содержащей диспетчер операций PCF и компонент Azure Service Broker.</span><span class="sxs-lookup"><span data-stu-id="b34bc-108">Use the [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in the Azure Marketplace to create a standard environment that includes PCF Ops Manager and the Azure Service Broker.</span></span> <span data-ttu-id="b34bc-109">[Полные инструкции][pcf-azuremarketplace-pivotaldocs] по развертыванию предложения Marketplace представлены в документации по Pivotal.</span><span class="sxs-lookup"><span data-stu-id="b34bc-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying the marketplace offer in the Pivotal documentation.</span></span>
- <span data-ttu-id="b34bc-110">Создайте пользовательскую среду, [развернув Pivotal Cloud Foundry вручную][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="b34bc-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="b34bc-111">[Разверните пакеты Cloud Foundry напрямую][oss-cf-bosh], настроив директор [BOSH](http://bosh.io), виртуальную машину, координирующую развертывание среды Cloud Foundry.</span><span class="sxs-lookup"><span data-stu-id="b34bc-111">[Deploy the open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates the deployment of the Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b34bc-112">Если вы развертываете PCF из Azure Marketplace, запишите SYSTEMDOMAINURL и учетные данные администратора, необходимые для доступа к Pivotal Apps Manager (описано в руководстве по развертыванию Marketplace).</span><span class="sxs-lookup"><span data-stu-id="b34bc-112">If you are deploying PCF from the Azure Marketplace, make a note of the SYSTEMDOMAINURL and the admin credentials required to access the Pivotal Apps Manager, both of which are described in the marketplace deployment guide.</span></span> <span data-ttu-id="b34bc-113">Эти значения необходимы для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="b34bc-113">They are needed to complete this tutorial.</span></span> <span data-ttu-id="b34bc-114">Для развертываний Marketplace значение SYSTEMDOMAINURL представлено в форме https://system.*IP-адрес*.cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="b34bc-114">For marketplace deployments, the SYSTEMDOMAINURL is in the form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-to-the-cloud-controller"></a><span data-ttu-id="b34bc-115">Подключение к Cloud Controller</span><span class="sxs-lookup"><span data-stu-id="b34bc-115">Connect to the Cloud Controller</span></span>

<span data-ttu-id="b34bc-116">Cloud Controller — основная точка входа в среду Cloud Foundry для развертывания приложений и управления ими.</span><span class="sxs-lookup"><span data-stu-id="b34bc-116">The Cloud Controller is the primary entry point to a Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="b34bc-117">Основной API Cloud Controller — это REST API. Доступ к нему можно получить с помощью различных средств.</span><span class="sxs-lookup"><span data-stu-id="b34bc-117">The core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="b34bc-118">В этом случае взаимодействие с ним осуществляется с помощью [интерфейса командной строки Cloud Foundry][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="b34bc-118">In this case, we interact with it through the [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="b34bc-119">Его можно установить в Windows, Linux или MacOS. Если вы не хотите его устанавливать, он уже предварительно установлен в [Azure Cloud Shell][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="b34bc-119">You can install the CLI on Linux, MacOS, or Windows, but if you'd prefer not to install it at all, it is available pre-installed in the [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="b34bc-120">Для входа добавьте `api` перед SYSTEMDOMAINURL, полученным из развертывания Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b34bc-120">To log in, prepend `api` to the SYSTEMDOMAINURL that you obtained from the marketplace deployment.</span></span> <span data-ttu-id="b34bc-121">Так как развертывание по умолчанию использует самозаверяющий сертификат, следует также добавить параметр `skip-ssl-validation`.</span><span class="sxs-lookup"><span data-stu-id="b34bc-121">Since the default deployment uses a self-signed certificate, you should also include the `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="b34bc-122">Вам будет предложено войти в Cloud Controller.</span><span class="sxs-lookup"><span data-stu-id="b34bc-122">You are prompted to log in to the Cloud Controller.</span></span> <span data-ttu-id="b34bc-123">Используйте учетные данные учетной записи администратора, полученные при развертывании из Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b34bc-123">Use the admin account credentials that you acquired from the marketplace deployment steps.</span></span>

<span data-ttu-id="b34bc-124">Для изоляции команд и сред в общей среде Cloud Foundry предоставляет *организации* и *пространства*, используемые в качестве пространств имен.</span><span class="sxs-lookup"><span data-stu-id="b34bc-124">Cloud Foundry provides *orgs* and *spaces* as namespaces to isolate the teams and environments within a shared deployment.</span></span> <span data-ttu-id="b34bc-125">Развертывание PCF Marketplace содержит *системную* организацию по умолчанию и несколько пространств, созданных для хранения основных компонентов, таких как служба автомасштабирования и Azure Service Broker.</span><span class="sxs-lookup"><span data-stu-id="b34bc-125">The PCF marketplace deployment includes the default *system* org and a set of spaces created to contain the base components, like the autoscaling service and the Azure service broker.</span></span> <span data-ttu-id="b34bc-126">Сейчас выберите *системное* пространство.</span><span class="sxs-lookup"><span data-stu-id="b34bc-126">For now, choose the *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="b34bc-127">Создание организации и пространства</span><span class="sxs-lookup"><span data-stu-id="b34bc-127">Create an org and space</span></span>

<span data-ttu-id="b34bc-128">Если ввести `cf apps`, отобразится набор системных приложений, развернутых в системном пространстве в системной организации.</span><span class="sxs-lookup"><span data-stu-id="b34bc-128">If you type `cf apps`, you see a set of system applications that have been deployed in the system space within the system org.</span></span> 

<span data-ttu-id="b34bc-129">*Системную* организацию необходимо зарезервировать для системных приложений. Создайте организацию и пространство для размещения примера приложения.</span><span class="sxs-lookup"><span data-stu-id="b34bc-129">You should keep the *system* org reserved for system applications, so create an org and space to house our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="b34bc-130">Используйте команду target для перехода к новой организации и пространству:</span><span class="sxs-lookup"><span data-stu-id="b34bc-130">Use the target command to switch to the new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="b34bc-131">Теперь при развертывании приложения оно автоматически создается в новой организации и пространстве.</span><span class="sxs-lookup"><span data-stu-id="b34bc-131">Now, when you deploy an application, it is automatically created in the new org and space.</span></span> <span data-ttu-id="b34bc-132">Чтобы убедиться, что в новой организации или пространстве нет приложений, введите `cf apps` еще раз.</span><span class="sxs-lookup"><span data-stu-id="b34bc-132">To confirm that there are currently no apps in the new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="b34bc-133">Дополнительные сведения об организациях и пространствах, а также о том, как их можно использовать для управления доступом на основе ролей (RBAC), см. в [документации по Cloud Foundry][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="b34bc-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see the [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="b34bc-134">Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="b34bc-134">Deploy an application</span></span>

<span data-ttu-id="b34bc-135">Воспользуемся примером приложения Cloud Foundry (Hello Spring Cloud), написанным на языке Java и созданным на основе [Spring Framework](http://spring.io) и [Spring Boot](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="b34bc-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on the [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-the-hello-spring-cloud-repository"></a><span data-ttu-id="b34bc-136">Клонирование репозитория Hello Spring Cloud</span><span class="sxs-lookup"><span data-stu-id="b34bc-136">Clone the Hello Spring Cloud repository</span></span>

<span data-ttu-id="b34bc-137">Пример приложения Hello Spring Cloud доступен на GitHub.</span><span class="sxs-lookup"><span data-stu-id="b34bc-137">The Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="b34bc-138">Клонируйте его в свою среду и измените расположение на новый каталог:</span><span class="sxs-lookup"><span data-stu-id="b34bc-138">Clone it to your environment and change into the new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-the-application"></a><span data-ttu-id="b34bc-139">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="b34bc-139">Build the application</span></span>

<span data-ttu-id="b34bc-140">Создайте приложение с помощью [Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="b34bc-140">Build the app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-the-application-with-cf-push"></a><span data-ttu-id="b34bc-141">Развертывание приложения с помощью команды cf push</span><span class="sxs-lookup"><span data-stu-id="b34bc-141">Deploy the application with cf push</span></span>

<span data-ttu-id="b34bc-142">Большинство приложений можно развернуть в Cloud Foundry с помощью команды `push`:</span><span class="sxs-lookup"><span data-stu-id="b34bc-142">You can deploy most applications to Cloud Foundry using the `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="b34bc-143">При *принудительной передаче* приложения Cloud Foundry определяет его тип (в данном случае — приложение Java) и зависимости (в данном случае — Spring Framework).</span><span class="sxs-lookup"><span data-stu-id="b34bc-143">When you *push* an application, Cloud Foundry detects the type of application (in this case, a Java app) and identifies its dependencies (in this case, the Spring framework).</span></span> <span data-ttu-id="b34bc-144">Затем это решение упаковывает все необходимые для выполнения кода компоненты в автономный образ контейнера, известный как *дроплет*.</span><span class="sxs-lookup"><span data-stu-id="b34bc-144">It then packages everything required to run your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="b34bc-145">Наконец, Cloud Foundry планирует приложение на одном из компьютеров, доступных в среде, и создает URL-адрес, по которому к нему можно получить доступ. Этот URL-адрес доступен в выходных данных команды.</span><span class="sxs-lookup"><span data-stu-id="b34bc-145">Finally, Cloud Foundry schedules the application on one of the available machines in your environment and creates a URL where you can reach it, which is available in the output of the command.</span></span>

![Выходные данные команды cf push][cf-push-output]

<span data-ttu-id="b34bc-147">Чтобы просмотреть приложение Hello Spring Cloud, откройте указанный URL-адрес в браузере:</span><span class="sxs-lookup"><span data-stu-id="b34bc-147">To see the hello-spring-cloud application, open the provided URL in your browser:</span></span>

![Пользовательский интерфейс по умолчанию для приложения Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="b34bc-149">Дополнительные сведения о том, что происходит при выполнении команды `cf push`, см. в разделе [How Applications Are Staged][cf-push-docs] (Поэтапное развертывание приложений) в документации по Cloud Foundry.</span><span class="sxs-lookup"><span data-stu-id="b34bc-149">To learn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in the Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="b34bc-150">Просмотр журналов приложения</span><span class="sxs-lookup"><span data-stu-id="b34bc-150">View application logs</span></span>

<span data-ttu-id="b34bc-151">С помощью интерфейса командной строки Cloud Foundry можно просмотреть журналы приложения по имени:</span><span class="sxs-lookup"><span data-stu-id="b34bc-151">You can use the Cloud Foundry CLI to view logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="b34bc-152">По умолчанию команда logs использует *заключительный фрагмент*, который позволяет просмотреть новые записываемые журналы.</span><span class="sxs-lookup"><span data-stu-id="b34bc-152">By default, the logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="b34bc-153">Чтобы просмотреть новые отображаемые журналы, обновите приложение Hello Spring Cloud в браузере.</span><span class="sxs-lookup"><span data-stu-id="b34bc-153">To see new logs appear, refresh the hello-spring-cloud app in the browser.</span></span>

<span data-ttu-id="b34bc-154">Чтобы просмотреть записанные журналы, добавьте параметр `recent`:</span><span class="sxs-lookup"><span data-stu-id="b34bc-154">To view logs that have already been written, add the `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-the-application"></a><span data-ttu-id="b34bc-155">Масштабирование приложения</span><span class="sxs-lookup"><span data-stu-id="b34bc-155">Scale the application</span></span>

<span data-ttu-id="b34bc-156">По умолчанию команда `cf push` создает только один экземпляр приложения.</span><span class="sxs-lookup"><span data-stu-id="b34bc-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="b34bc-157">Чтобы обеспечить высокий уровень доступности и развертывания для поддержки более высокой пропускной способности, обычно требуется запустить несколько экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="b34bc-157">To ensure high availability and enable scale out for higher throughput, you generally want to run more than one instance of your applications.</span></span> <span data-ttu-id="b34bc-158">Развернутые приложения можно легко масштабировать с помощью команды `scale`:</span><span class="sxs-lookup"><span data-stu-id="b34bc-158">You can easily scale out already deployed applications using the `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="b34bc-159">Если выполнить команду `cf app` в приложении, мы увидим, что Cloud Foundry создает другой экземпляр приложения.</span><span class="sxs-lookup"><span data-stu-id="b34bc-159">Running the `cf app` command on the application shows that Cloud Foundry is creating another instance of the application.</span></span> <span data-ttu-id="b34bc-160">После запуска приложения Cloud Foundry автоматически запускает балансировку нагрузки по трафику к нему.</span><span class="sxs-lookup"><span data-stu-id="b34bc-160">Once the application has started, Cloud Foundry automatically starts load balancing traffic to it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b34bc-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b34bc-161">Next steps</span></span>

- <span data-ttu-id="b34bc-162">[Ознакомьтесь с документацией по Cloud Foundry][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="b34bc-162">[Read the Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="b34bc-163">[Настройте подключаемый модуль Visual Studio Team Services для Cloud Foundry][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="b34bc-163">[Set up the Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="b34bc-164">[Настройте Microsoft Log Analytics Nozzle для Cloud Foundry][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="b34bc-164">[Configure the Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

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