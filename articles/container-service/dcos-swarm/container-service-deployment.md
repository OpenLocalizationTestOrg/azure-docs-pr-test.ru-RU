---
title: "Развертывание кластера контейнера Docker в Azure | Документация Майкрософт"
description: "Развертывание решений Kubernetes, DC/OS или Docker Swarm в службе контейнеров Azure с помощью портала Azure или шаблона Resource Manager."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure, dcos, swarm, kubernetes, служба контейнеров azure, acs"
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 0ef256537bf095e2a5d582bd345a9c8dcede2095
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-the-azure-portal"></a><span data-ttu-id="5f30d-104">Развертывание решения для размещения контейнера Docker с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="5f30d-104">Deploy a Docker container hosting solution using the Azure portal</span></span>



<span data-ttu-id="5f30d-105">Служба контейнеров Azure предусматривает быстрое развертывание популярных решений с открытым кодом для кластеризации и оркестрации контейнеров.</span><span class="sxs-lookup"><span data-stu-id="5f30d-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="5f30d-106">В этом документе описано развертывание кластера Службы контейнеров Azure с использованием портала Azure или шаблона быстрого запуска Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f30d-106">This document walks you through deploying an Azure Container Service cluster by using the Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="5f30d-107">Вы также можете развернуть кластер Службы контейнеров Azure с помощью [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) или с помощью интерфейсов API Службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5f30d-107">You can also deploy an Azure Container Service cluster by using the [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or the Azure Container Service APIs.</span></span>

<span data-ttu-id="5f30d-108">Чтобы изучить общие положения, ознакомьтесь с разделом [Общие сведения о службе контейнеров Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5f30d-108">For background, see [Azure Container Service introduction](../container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5f30d-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5f30d-109">Prerequisites</span></span>

* <span data-ttu-id="5f30d-110">**Подписка Azure.** Если у вас ее нет, зарегистрируйтесь, чтобы [воспользоваться бесплатной пробной версией](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="5f30d-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="5f30d-111">Для более крупных кластеров можно использовать подписку с оплатой по мере использования или другие варианты приобретения.</span><span class="sxs-lookup"><span data-stu-id="5f30d-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f30d-112">Объем использования подписки Azure и [квоты на ресурсы](../../azure-subscription-service-limits.md), включая квоты на ядра, могут ограничивать размер развертываемого кластера.</span><span class="sxs-lookup"><span data-stu-id="5f30d-112">Your Azure subscription usage and [resource quotas](../../azure-subscription-service-limits.md), such as cores quotas, can limit the size of the cluster you deploy.</span></span> <span data-ttu-id="5f30d-113">Чтобы увеличить квоту, [отправьте запрос в службу поддержки](../../azure-supportability/how-to-create-azure-support-request.md). Это бесплатная услуга.</span><span class="sxs-lookup"><span data-stu-id="5f30d-113">To request a quota increase, open an [online customer support request](../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="5f30d-114">**Открытый ключ RSA (SSH).** При развертывании на портале или с помощью одного из шаблонов быстрого запуска Azure необходимо предоставить открытый ключ, используемый для аутентификации в виртуальных машинах Службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5f30d-114">**SSH RSA public key**: When deploying through the portal or one of the Azure quickstart templates, you need to provide the public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="5f30d-115">Инструкции по созданию ключей RSA (SSH) см. в соответствующих статьях для [OS X, Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) или [Windows](../../virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="5f30d-115">To create Secure Shell (SSH) RSA keys, see the [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="5f30d-116">**Секрет и идентификатор клиента субъекта-службы (только для Kubernetes).** Дополнительные сведения и рекомендации по созданию субъекта-службы Azure Active Directory см. в разделе [Сведения о субъекте-службе Azure Active Directory для кластера Kubernetes в службе контейнеров Azure](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="5f30d-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance to create an Azure Active Directory service principal, see [About the service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-the-azure-portal"></a><span data-ttu-id="5f30d-117">Создание кластера с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="5f30d-117">Create a cluster by using the Azure portal</span></span>
1. <span data-ttu-id="5f30d-118">Войдите на портал Azure, выберите **Создать** и найдите **службу контейнеров Azure** в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5f30d-118">Sign in to the Azure portal, select **New**, and search the Azure Marketplace for **Azure Container Service**.</span></span>

    ![Служба контейнеров Azure в Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="5f30d-120">Выберите **Служба контейнеров Azure** и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5f30d-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="5f30d-121">В колонке **Основные сведения** задайте следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="5f30d-121">On the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="5f30d-122">**Orchestrator** — выберите один из оркестраторов контейнера для развертывания в кластере.</span><span class="sxs-lookup"><span data-stu-id="5f30d-122">**Orchestrator**: Select one of the container orchestrators to deploy on the cluster.</span></span>
        * <span data-ttu-id="5f30d-123">**DC/OS** — развертывает кластер DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5f30d-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="5f30d-124">**Swarm** — развертывает кластер Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="5f30d-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="5f30d-125">**Kubernetes** — развертывает кластер Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5f30d-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="5f30d-126">**Подписка**— выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="5f30d-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="5f30d-127">**Группа ресурсов** — введите имя новой группы ресурсов для развертывания.</span><span class="sxs-lookup"><span data-stu-id="5f30d-127">**Resource group**: Enter the name of a new resource group for the deployment.</span></span>
    * <span data-ttu-id="5f30d-128">**Расположение**— выберите регион Azure для развертывания службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5f30d-128">**Location**: Select an Azure region for the Azure Container Service deployment.</span></span> <span data-ttu-id="5f30d-129">Проверьте [доступность продуктов по регионам](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="5f30d-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![Основные параметры](./media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="5f30d-131">Когда будете готовы продолжить, нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="5f30d-131">Click **OK** when you're ready to proceed.</span></span>

4. <span data-ttu-id="5f30d-132">В колонке **Master configuration** (Конфигурация главных узлов) введите указанные ниже параметры для главных узлов Linux в кластере (некоторые параметры относятся к каждому оркестратору).</span><span class="sxs-lookup"><span data-stu-id="5f30d-132">On the **Master configuration** blade, enter the following settings for the Linux master node or nodes in the cluster (some settings are specific to each orchestrator):</span></span>

    * <span data-ttu-id="5f30d-133">**Master DNS name** (DNS-имя главного узла) — префикс, используемый для создания уникального полного доменного имени главного узла.</span><span class="sxs-lookup"><span data-stu-id="5f30d-133">**Master DNS name**: The prefix used to create a unique fully qualified domain name (FQDN) for the master.</span></span> <span data-ttu-id="5f30d-134">Полное доменное имя главного узла имеет вид *префикс*mgmt.*расположение*.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="5f30d-134">The master FQDN is of the form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="5f30d-135">**Имя пользователя** — имя пользователя для учетной записи на каждой виртуальной машине Linux в кластере.</span><span class="sxs-lookup"><span data-stu-id="5f30d-135">**User name**: The user name for an account on each of the Linux virtual machines in the cluster.</span></span>
    * <span data-ttu-id="5f30d-136">**Открытый ключ RSA (SSH)** — добавьте открытый ключ, который будет использоваться для аутентификации в виртуальных машинах Linux.</span><span class="sxs-lookup"><span data-stu-id="5f30d-136">**SSH RSA public key**: Add the public key to be used for authentication against the Linux virtual machines.</span></span> <span data-ttu-id="5f30d-137">Важно, чтобы ключ не был разбит разрывами строки, но содержал префикс `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="5f30d-137">It is important that this key contains no line breaks, and it includes the `ssh-rsa` prefix.</span></span> <span data-ttu-id="5f30d-138">Постфикс `username@domain` добавлять необязательно.</span><span class="sxs-lookup"><span data-stu-id="5f30d-138">The `username@domain` postfix is optional.</span></span> <span data-ttu-id="5f30d-139">Ключ должен выглядеть так: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span><span class="sxs-lookup"><span data-stu-id="5f30d-139">The key should look something like the following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="5f30d-140">**Субъект-служба** — если вы выбрали оркестратор Kubernetes, введите **идентификатор клиента субъекта-службы** (также называемый appId) Azure Active Directory и **секрет клиента субъекта-службы** (пароль).</span><span class="sxs-lookup"><span data-stu-id="5f30d-140">**Service principal**: If you selected the Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called the appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="5f30d-141">Дополнительные сведения см. в статье [о субъекте-службе для кластера Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="5f30d-141">For more information, see [About the service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="5f30d-142">**Количество главных серверов** — количество главных серверов в кластере.</span><span class="sxs-lookup"><span data-stu-id="5f30d-142">**Master count**: The number of masters in the cluster.</span></span>
    * <span data-ttu-id="5f30d-143">**VM diagnostics** (Диагностика виртуальных машин) — для некоторых оркестраторов на главных узлах можно включить диагностику виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5f30d-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on the masters.</span></span>

    ![Конфигурация главных узлов](./media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="5f30d-145">Когда будете готовы продолжить, нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="5f30d-145">Click **OK** when you're ready to proceed.</span></span>

5. <span data-ttu-id="5f30d-146">В колонке **Конфигурация агента** введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="5f30d-146">On the **Agent configuration** blade, enter the following information:</span></span>

    * <span data-ttu-id="5f30d-147">**Agent count** (Количество агентов) — начальное количество агентов в масштабируемом наборе агента для Docker Swarm и Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5f30d-147">**Agent count**: For Docker Swarm and Kubernetes, this value is the initial number of agents in the agent scale set.</span></span> <span data-ttu-id="5f30d-148">Для DC/OS этот параметр указывает на начальное количество агентов в частном масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="5f30d-148">For DC/OS, it is the initial number of agents in a private scale set.</span></span> <span data-ttu-id="5f30d-149">Кроме того, для DC/OS создается общедоступный масштабируемый набор с заранее определенным количеством агентов.</span><span class="sxs-lookup"><span data-stu-id="5f30d-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="5f30d-150">Количество агентов в этом общедоступном масштабируемом наборе определяется с учетом количества главных узлов в кластере: один общедоступный агент для одного главного узла и два общедоступных агента для трех или пяти главных узлов.</span><span class="sxs-lookup"><span data-stu-id="5f30d-150">The number of agents in this public scale set is determined by the number of masters in the cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="5f30d-151">**Размер виртуальной машины агента**— размер виртуальных машин агентов.</span><span class="sxs-lookup"><span data-stu-id="5f30d-151">**Agent virtual machine size**: The size of the agent virtual machines.</span></span>
    * <span data-ttu-id="5f30d-152">**Операционная система** — в настоящее время этот параметр доступен только в том случае, если вы выбрали оркестратор Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5f30d-152">**Operating system**: This setting is currently available only if you selected the Kubernetes orchestrator.</span></span> <span data-ttu-id="5f30d-153">Выберите дистрибутив Linux или операционную систему Windows Server для агентов.</span><span class="sxs-lookup"><span data-stu-id="5f30d-153">Choose either a Linux distribution or a Windows Server operating system to run on the agents.</span></span> <span data-ttu-id="5f30d-154">Этот параметр определяет, может ли кластер запускать приложения-контейнеры Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="5f30d-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="5f30d-155">Поддержка контейнера Windows для кластеров Kubernetes находится на этапе предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="5f30d-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="5f30d-156">Для кластеров DC/OS и Swarm в настоящее время поддерживаются только агенты Linux в Службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5f30d-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="5f30d-157">**Учетные данные агента** — если вы выбрали операционную систему Windows, введите **имя пользователя** и **пароль** администратора для виртуальных машин агента.</span><span class="sxs-lookup"><span data-stu-id="5f30d-157">**Agent credentials**: If you selected the Windows operating system, enter an administrator **User name** and **Password** for the agent VMs.</span></span> 

    ![Конфигурация агента](./media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="5f30d-159">Когда будете готовы продолжить, нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="5f30d-159">Click **OK** when you're ready to proceed.</span></span>

6. <span data-ttu-id="5f30d-160">Когда проверка службы завершится, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5f30d-160">After service validation finishes, click **OK**.</span></span>

    ![Проверка](./media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="5f30d-162">Просмотрите условия.</span><span class="sxs-lookup"><span data-stu-id="5f30d-162">Review the terms.</span></span> <span data-ttu-id="5f30d-163">Нажмите кнопку **Создать**, чтобы начать развертывание.</span><span class="sxs-lookup"><span data-stu-id="5f30d-163">To start the deployment process, click **Create**.</span></span>

    <span data-ttu-id="5f30d-164">Если вы решили выполнить развертывание на портале Azure, вы сможете просматривать состояние развертывания.</span><span class="sxs-lookup"><span data-stu-id="5f30d-164">If you've elected to pin the deployment to the Azure portal, you can see the deployment status.</span></span>

    ![Состояния развертывания](./media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="5f30d-166">Развертывание занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="5f30d-166">The deployment takes several minutes to complete.</span></span> <span data-ttu-id="5f30d-167">Затем кластер Службы контейнеров Azure можно использовать.</span><span class="sxs-lookup"><span data-stu-id="5f30d-167">Then, the Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="5f30d-168">Создание кластера с помощью шаблона быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="5f30d-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="5f30d-169">Для развертывания кластера в Службе контейнеров Azure можно использовать шаблоны быстрого запуска Azure.</span><span class="sxs-lookup"><span data-stu-id="5f30d-169">Azure quickstart templates are available to deploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="5f30d-170">Предоставляемые шаблоны быстрого запуска можно изменять, включив дополнительную или расширенную конфигурацию Azure.</span><span class="sxs-lookup"><span data-stu-id="5f30d-170">The provided quickstart templates can be modified to include additional or advanced Azure configuration.</span></span> <span data-ttu-id="5f30d-171">Чтобы создать кластер Службы контейнеров Azure с помощью шаблона быстрого запуска Azure, вам потребуется подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="5f30d-171">To create an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="5f30d-172">Если у вас ее нет, зарегистрируйтесь, чтобы [воспользоваться бесплатной пробной версией](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="5f30d-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="5f30d-173">Чтобы развернуть кластер с помощью шаблона или Azure CLI 2.0, выполните приведенные ниже действия (см. [инструкции по установке и настройке](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="5f30d-173">Follow these steps to deploy a cluster using a template and the Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="5f30d-174">В системе Windows эти же действия можно выполнить с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f30d-174">If you're on a Windows system, you can use similar steps to deploy a template using Azure PowerShell.</span></span> <span data-ttu-id="5f30d-175">Инструкции см. далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="5f30d-175">See steps later in this section.</span></span> <span data-ttu-id="5f30d-176">Кроме того, шаблон можно развернуть на [портале](../../azure-resource-manager/resource-group-template-deploy-portal.md) или с помощью других методов.</span><span class="sxs-lookup"><span data-stu-id="5f30d-176">You can also deploy a template through the [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="5f30d-177">Чтобы развернуть кластер DC/OS, Docker Swarm или Kubernetes, выберите на GitHub один из следующих шаблонов быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="5f30d-177">To deploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of the available quickstart templates from GitHub.</span></span> <span data-ttu-id="5f30d-178">Ниже приведен неполный список шаблонов.</span><span class="sxs-lookup"><span data-stu-id="5f30d-178">A partial list follows.</span></span> <span data-ttu-id="5f30d-179">Шаблоны DC/OS и Swarm отличаются только выбором оркестратора по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5f30d-179">The DC/OS and Swarm templates are the same, except for the default orchestrator selection.</span></span>

    * <span data-ttu-id="5f30d-180">[Шаблон DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos).</span><span class="sxs-lookup"><span data-stu-id="5f30d-180">[DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)</span></span>
    * <span data-ttu-id="5f30d-181">[шаблон Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm);</span><span class="sxs-lookup"><span data-stu-id="5f30d-181">[Swarm template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)</span></span>
    * <span data-ttu-id="5f30d-182">[Шаблон Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="5f30d-182">[Kubernetes template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)</span></span>

2. <span data-ttu-id="5f30d-183">Войдите в учетную запись Azure (`az login`) и подключите Azure CLI к подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="5f30d-183">Log in to your Azure account (`az login`), and make sure that the Azure CLI is connected to your Azure subscription.</span></span> <span data-ttu-id="5f30d-184">Чтобы просмотреть подписку Azure по умолчанию, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="5f30d-184">You can see the default subscription by using the following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="5f30d-185">Если у вас есть несколько подписок и вы хотите выбрать другую подписку по умолчанию, выполните командлет `az account set --subscription`, указав идентификатор или имя этой подписки.</span><span class="sxs-lookup"><span data-stu-id="5f30d-185">If you have more than one subscription and need to set a different default subscription, run `az account set --subscription` and specify the subscription ID or name.</span></span>

3. <span data-ttu-id="5f30d-186">Мы советуем использовать для развертывания новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5f30d-186">As a best practice, use a new resource group for the deployment.</span></span> <span data-ttu-id="5f30d-187">Чтобы создать группу ресурсов, выполните команду `az group create`, указав ее имя и расположение.</span><span class="sxs-lookup"><span data-stu-id="5f30d-187">To create a resource group, use the `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="5f30d-188">Создайте файл JSON, содержащий необходимые параметры шаблона.</span><span class="sxs-lookup"><span data-stu-id="5f30d-188">Create a JSON file containing the required template parameters.</span></span> <span data-ttu-id="5f30d-189">Скачайте файл параметров `azuredeploy.parameters.json`, доступный с шаблоном `azuredeploy.json` Службы контейнеров Azure в GitHub.</span><span class="sxs-lookup"><span data-stu-id="5f30d-189">Download the parameters file named `azuredeploy.parameters.json` that accompanies the Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="5f30d-190">Введите необходимые значения параметров кластера.</span><span class="sxs-lookup"><span data-stu-id="5f30d-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="5f30d-191">Например, чтобы использовать [шаблон DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), укажите значения параметров `dnsNamePrefix` и `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="5f30d-191">For example, to use the [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="5f30d-192">Описания и значения других параметров см. в файле `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="5f30d-192">See the descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="5f30d-193">Создайте кластер Службы контейнеров, передав файл параметров развертывания с помощью следующей команды, где:</span><span class="sxs-lookup"><span data-stu-id="5f30d-193">Create a Container Service cluster by passing the deployment parameters file with the following command, where:</span></span>

    * <span data-ttu-id="5f30d-194">**RESOURCE_GROUP** — имя группы ресурсов, созданной на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="5f30d-194">**RESOURCE_GROUP** is the name of the resource group that you created in the previous step.</span></span>
    * <span data-ttu-id="5f30d-195">**DEPLOYMENT_NAME** (необязательный) — имя развертывания.</span><span class="sxs-lookup"><span data-stu-id="5f30d-195">**DEPLOYMENT_NAME** (optional) is a name you give to the deployment.</span></span>
    * <span data-ttu-id="5f30d-196">**TEMPLATE_URI** — расположение файла развертывания `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="5f30d-196">**TEMPLATE_URI** is the location of the deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="5f30d-197">Этот URI должен быть необработанным файлом (RAW), а не указателем на пользовательский интерфейс GitHub.</span><span class="sxs-lookup"><span data-stu-id="5f30d-197">This URI must be the Raw file, not a pointer to the GitHub UI.</span></span> <span data-ttu-id="5f30d-198">Чтобы найти этот URI, выберите в GitHub файл `azuredeploy.json` и нажмите кнопку **RAW**.</span><span class="sxs-lookup"><span data-stu-id="5f30d-198">To find this URI, select the `azuredeploy.json` file in GitHub, and click the **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="5f30d-199">Параметры также можно указать как строку в формате JSON в командной строке.</span><span class="sxs-lookup"><span data-stu-id="5f30d-199">You can also provide parameters as a JSON-formatted string on the command line.</span></span> <span data-ttu-id="5f30d-200">Используйте команду, аналогичную приведенной ниже.</span><span class="sxs-lookup"><span data-stu-id="5f30d-200">Use a command similar to the following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="5f30d-201">Развертывание занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="5f30d-201">The deployment takes several minutes to complete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="5f30d-202">Аналогичные команды PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f30d-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="5f30d-203">Шаблон кластера Службы контейнеров Azure также можно развернуть с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f30d-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="5f30d-204">В этом документе используется [модуль Azure PowerShell](https://azure.microsoft.com/blog/azps-1-0/)версии 1.0.</span><span class="sxs-lookup"><span data-stu-id="5f30d-204">This document is based on the version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="5f30d-205">Чтобы развернуть кластер DC/OS, Docker Swarm или Kubernetes, выберите на GitHub один из следующих шаблонов быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="5f30d-205">To deploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of the available quickstart templates from GitHub.</span></span> <span data-ttu-id="5f30d-206">Ниже приведен неполный список шаблонов.</span><span class="sxs-lookup"><span data-stu-id="5f30d-206">A partial list follows.</span></span> <span data-ttu-id="5f30d-207">Обратите внимание, что шаблоны DC/OS и Swarm отличаются только выбором оркестратора по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5f30d-207">Note that the DC/OS and Swarm templates are the same, with the exception of the default orchestrator selection.</span></span>

    * <span data-ttu-id="5f30d-208">[Шаблон DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos).</span><span class="sxs-lookup"><span data-stu-id="5f30d-208">[DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)</span></span>
    * <span data-ttu-id="5f30d-209">[шаблон Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm);</span><span class="sxs-lookup"><span data-stu-id="5f30d-209">[Swarm template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)</span></span>
    * <span data-ttu-id="5f30d-210">[Шаблон Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="5f30d-210">[Kubernetes template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)</span></span>

2. <span data-ttu-id="5f30d-211">Прежде чем создать кластер в подписке Azure, убедитесь, что для сеанса PowerShell выполнен вход в Azure.</span><span class="sxs-lookup"><span data-stu-id="5f30d-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in to Azure.</span></span> <span data-ttu-id="5f30d-212">Это можно сделать с помощью команды `Get-AzureRMSubscription` .</span><span class="sxs-lookup"><span data-stu-id="5f30d-212">You can do this with the `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="5f30d-213">Войти в Azure можно с помощью команды `Login-AzureRMAccount` .</span><span class="sxs-lookup"><span data-stu-id="5f30d-213">If you need to sign in to Azure, use the `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="5f30d-214">Мы советуем использовать для развертывания новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5f30d-214">As a best practice, use a new resource group for the deployment.</span></span> <span data-ttu-id="5f30d-215">Чтобы создать группу ресурсов, используйте команду `New-AzureRmResourceGroup`, указав имя группы ресурсов и регион назначения.</span><span class="sxs-lookup"><span data-stu-id="5f30d-215">To create a resource group, use the `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="5f30d-216">После создания группы ресурсов можно создать кластер, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f30d-216">After you create a resource group, you can create your cluster with the following command.</span></span> <span data-ttu-id="5f30d-217">Универсальный код ресурса (URI) нужного шаблона указывается в параметре `-TemplateUri`.</span><span class="sxs-lookup"><span data-stu-id="5f30d-217">The URI of the desired template is specified with the `-TemplateUri` parameter.</span></span> <span data-ttu-id="5f30d-218">При выполнении этой команды в PowerShell отобразится запрос на ввод значений параметров развертывания.</span><span class="sxs-lookup"><span data-stu-id="5f30d-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="5f30d-219">Выбор параметров шаблона</span><span class="sxs-lookup"><span data-stu-id="5f30d-219">Provide template parameters</span></span>
<span data-ttu-id="5f30d-220">Если вы знакомы с PowerShell, вы знаете, что можете проходить по кругу все доступные параметры для командлета. Для этого введите знак минус (-) и нажмите клавишу TAB.</span><span class="sxs-lookup"><span data-stu-id="5f30d-220">If you're familiar with PowerShell, you know that you can cycle through the available parameters for a cmdlet by typing a minus sign (-) and then pressing the TAB key.</span></span> <span data-ttu-id="5f30d-221">Точно так же это работает с параметрами, которые вы определили в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="5f30d-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="5f30d-222">Сразу после ввода имени шаблона командлет выбирает шаблон, анализирует его параметры и динамически добавляет параметры шаблона в команду.</span><span class="sxs-lookup"><span data-stu-id="5f30d-222">As soon as you type the template name, the cmdlet fetches the template, parses the parameters, and adds the template parameters to the command dynamically.</span></span> <span data-ttu-id="5f30d-223">Таким образом можно легко указать значения параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="5f30d-223">This makes it easy to specify the template parameter values.</span></span> <span data-ttu-id="5f30d-224">Если вы забыли значение обязательного параметра, PowerShell подскажет его вам.</span><span class="sxs-lookup"><span data-stu-id="5f30d-224">And, if you forget a required parameter value, PowerShell prompts you for the value.</span></span>

<span data-ttu-id="5f30d-225">Вот полная версия команды, в которой указаны параметры.</span><span class="sxs-lookup"><span data-stu-id="5f30d-225">Here is the full command, with parameters included.</span></span> <span data-ttu-id="5f30d-226">Укажите собственные значения для имен ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5f30d-226">Provide your own values for the names of the resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="5f30d-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f30d-227">Next steps</span></span>
<span data-ttu-id="5f30d-228">Теперь, когда у вас есть работающий кластер, выберите ссылки ниже, чтобы узнать о возможностях подключения и управления.</span><span class="sxs-lookup"><span data-stu-id="5f30d-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="5f30d-229">Подключение к кластеру службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="5f30d-229">Connect to an Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="5f30d-230">Работа со службой контейнеров Azure и DC/OS</span><span class="sxs-lookup"><span data-stu-id="5f30d-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="5f30d-231">Работа со службой контейнеров Azure и Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="5f30d-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="5f30d-232">Работа со службой контейнеров Azure и Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5f30d-232">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)
