---
title: "кластер aaaDeploy контейнер Docker в Azure | Документы Microsoft"
description: "Развертывание решения Kubernetes, DC/OS или с помощью Docker Swarm в контейнере службы Azure с помощью портала Azure hello или шаблона диспетчера ресурсов."
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
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a><span data-ttu-id="a1f36-104">Развертывания с помощью портала Azure hello решения по размещению контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="a1f36-104">Deploy a Docker container hosting solution using hello Azure portal</span></span>



<span data-ttu-id="a1f36-105">Служба контейнеров Azure предусматривает быстрое развертывание популярных решений с открытым кодом для кластеризации и оркестрации контейнеров.</span><span class="sxs-lookup"><span data-stu-id="a1f36-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="a1f36-106">В этом документе описывается развертывание кластера службы контейнера Azure с помощью портала Azure hello или шаблоном краткого руководства диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f36-106">This document walks you through deploying an Azure Container Service cluster by using hello Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="a1f36-107">Можно также развернуть кластер контейнера службы Azure с помощью hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) или hello API-интерфейсы службы контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f36-107">You can also deploy an Azure Container Service cluster by using hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="a1f36-108">Чтобы изучить общие положения, ознакомьтесь с разделом [Общие сведения о службе контейнеров Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="a1f36-108">For background, see [Azure Container Service introduction](../container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a1f36-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a1f36-109">Prerequisites</span></span>

* <span data-ttu-id="a1f36-110">**Подписка Azure.** Если у вас ее нет, зарегистрируйтесь, чтобы [воспользоваться бесплатной пробной версией](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="a1f36-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="a1f36-111">Для более крупных кластеров можно использовать подписку с оплатой по мере использования или другие варианты приобретения.</span><span class="sxs-lookup"><span data-stu-id="a1f36-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a1f36-112">Использование вашей подписки Azure и [квоты ресурсов](../../azure-subscription-service-limits.md), такие как квоты ядер, можно ограничить размер hello развертывания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-112">Your Azure subscription usage and [resource quotas](../../azure-subscription-service-limits.md), such as cores quotas, can limit hello size of hello cluster you deploy.</span></span> <span data-ttu-id="a1f36-113">Увеличение квоты, откройте toorequest [запрос на получение поддержки сети клиента](../../azure-supportability/how-to-create-azure-support-request.md) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="a1f36-113">toorequest a quota increase, open an [online customer support request](../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="a1f36-114">**Открытый ключ SSH-RSA**: требуется при развертывании через портал hello или один из шаблонов hello Azure краткое руководство, tooprovide hello открытый ключ для проверки подлинности Azure контейнера службы виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a1f36-114">**SSH RSA public key**: When deploying through hello portal or one of hello Azure quickstart templates, you need tooprovide hello public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="a1f36-115">ключи RSA Secure Shell (SSH) toocreate, в разделе hello [OS X и Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) или [Windows](../../virtual-machines/linux/ssh-from-windows.md) рекомендации.</span><span class="sxs-lookup"><span data-stu-id="a1f36-115">toocreate Secure Shell (SSH) RSA keys, see hello [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="a1f36-116">**Идентификатор участника клиента и секрет службы** (Kubernetes): Дополнительные сведения и рекомендации toocreate участника-службы Azure Active Directory, см. [о hello участника-службы для кластера Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="a1f36-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance toocreate an Azure Active Directory service principal, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-hello-azure-portal"></a><span data-ttu-id="a1f36-117">Создание кластера с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="a1f36-117">Create a cluster by using hello Azure portal</span></span>
1. <span data-ttu-id="a1f36-118">Выберите вход toohello портал Azure **New**и hello Azure Marketplace для поиска **контейнера службы Azure**.</span><span class="sxs-lookup"><span data-stu-id="a1f36-118">Sign in toohello Azure portal, select **New**, and search hello Azure Marketplace for **Azure Container Service**.</span></span>

    ![Служба контейнеров Azure в Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="a1f36-120">Выберите **Служба контейнеров Azure** и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a1f36-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="a1f36-121">На hello **основы** колонке введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="a1f36-121">On hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="a1f36-122">**Orchestrator**: выберите один из toodeploy orchestrators контейнера hello в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-122">**Orchestrator**: Select one of hello container orchestrators toodeploy on hello cluster.</span></span>
        * <span data-ttu-id="a1f36-123">**DC/OS** — развертывает кластер DC/OS.</span><span class="sxs-lookup"><span data-stu-id="a1f36-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="a1f36-124">**Swarm** — развертывает кластер Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="a1f36-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="a1f36-125">**Kubernetes** — развертывает кластер Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a1f36-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="a1f36-126">**Подписка**— выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f36-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="a1f36-127">**Группа ресурсов**: Введите hello имя группы ресурсов для развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-127">**Resource group**: Enter hello name of a new resource group for hello deployment.</span></span>
    * <span data-ttu-id="a1f36-128">**Расположение**: Выберите регион Azure для развертывания службы Azure контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-128">**Location**: Select an Azure region for hello Azure Container Service deployment.</span></span> <span data-ttu-id="a1f36-129">Проверьте [доступность продуктов по регионам](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="a1f36-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![Основные параметры](./media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="a1f36-131">Нажмите кнопку **ОК** когда вы будете готовы tooproceed.</span><span class="sxs-lookup"><span data-stu-id="a1f36-131">Click **OK** when you're ready tooproceed.</span></span>

4. <span data-ttu-id="a1f36-132">На hello **главный конфигурации** колонки, введите следующие параметры для hello Linux главный узел или узлы в кластере hello (некоторые параметры, определенные tooeach orchestrator) hello:</span><span class="sxs-lookup"><span data-stu-id="a1f36-132">On hello **Master configuration** blade, enter hello following settings for hello Linux master node or nodes in hello cluster (some settings are specific tooeach orchestrator):</span></span>

    * <span data-ttu-id="a1f36-133">**Основной DNS-имя**: hello префикс, используемый toocreate уникальное полное доменное имя (FQDN) для базы данных master hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-133">**Master DNS name**: hello prefix used toocreate a unique fully qualified domain name (FQDN) for hello master.</span></span> <span data-ttu-id="a1f36-134">Hello master полное доменное имя имеет вид hello *префикс*управления*расположение*. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="a1f36-134">hello master FQDN is of hello form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="a1f36-135">**Имя пользователя**: hello имя пользователя для учетной записи для всех виртуальных машин Linux hello в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-135">**User name**: hello user name for an account on each of hello Linux virtual machines in hello cluster.</span></span>
    * <span data-ttu-id="a1f36-136">**Открытый ключ SSH-RSA**: добавление ключа toobe с общей hello используемых для проверки подлинности виртуальных машин Linux hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-136">**SSH RSA public key**: Add hello public key toobe used for authentication against hello Linux virtual machines.</span></span> <span data-ttu-id="a1f36-137">Очень важно, что этот раздел содержит без разрывов строки, а также hello `ssh-rsa` префикс.</span><span class="sxs-lookup"><span data-stu-id="a1f36-137">It is important that this key contains no line breaks, and it includes hello `ssh-rsa` prefix.</span></span> <span data-ttu-id="a1f36-138">Hello `username@domain` постфиксная является необязательным.</span><span class="sxs-lookup"><span data-stu-id="a1f36-138">hello `username@domain` postfix is optional.</span></span> <span data-ttu-id="a1f36-139">Hello ключ должен выглядеть примерно hello следующим образом: **AAAAB3Nz ssh-rsa... <>...... UcyupgH azureuser@linuxvm** .</span><span class="sxs-lookup"><span data-stu-id="a1f36-139">hello key should look something like hello following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="a1f36-140">**Участника-службы**: Если вы выбрали hello Kubernetes orchestrator, введите Azure Active Directory **идентификатор участника клиент службы** (также называемые hello appId) и **основной секретный службы** (пароль).</span><span class="sxs-lookup"><span data-stu-id="a1f36-140">**Service principal**: If you selected hello Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called hello appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="a1f36-141">Дополнительные сведения см. в разделе [о hello участника-службы для кластера Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="a1f36-141">For more information, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="a1f36-142">**Главный счетчик**: hello число образцов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-142">**Master count**: hello number of masters in hello cluster.</span></span>
    * <span data-ttu-id="a1f36-143">**Диагностика виртуальных Машин**: для некоторых orchestrators можно включить диагностику виртуальных Машин в hello образцов.</span><span class="sxs-lookup"><span data-stu-id="a1f36-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on hello masters.</span></span>

    ![Конфигурация главных узлов](./media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="a1f36-145">Нажмите кнопку **ОК** когда вы будете готовы tooproceed.</span><span class="sxs-lookup"><span data-stu-id="a1f36-145">Click **OK** when you're ready tooproceed.</span></span>

5. <span data-ttu-id="a1f36-146">На hello **конфигурация агента** колонке введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="a1f36-146">On hello **Agent configuration** blade, enter hello following information:</span></span>

    * <span data-ttu-id="a1f36-147">**Количество агентов**: для Docker группу мелких объектов и Kubernetes, это значение равно hello начальное количество агентов в наборе масштабирования агент hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-147">**Agent count**: For Docker Swarm and Kubernetes, this value is hello initial number of agents in hello agent scale set.</span></span> <span data-ttu-id="a1f36-148">Для контроллера домена/OS это hello начальное количество агентов в наборе масштабирования закрытый.</span><span class="sxs-lookup"><span data-stu-id="a1f36-148">For DC/OS, it is hello initial number of agents in a private scale set.</span></span> <span data-ttu-id="a1f36-149">Кроме того, для DC/OS создается общедоступный масштабируемый набор с заранее определенным количеством агентов.</span><span class="sxs-lookup"><span data-stu-id="a1f36-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="a1f36-150">Hello количество агентов в этот набор общих шкалы определяется hello число образцов в кластере hello: один открытый агент для одной базы данных master и два общих агентов для три или пять образцов.</span><span class="sxs-lookup"><span data-stu-id="a1f36-150">hello number of agents in this public scale set is determined by hello number of masters in hello cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="a1f36-151">**Размер виртуальной машины агента**: hello размер hello агент виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a1f36-151">**Agent virtual machine size**: hello size of hello agent virtual machines.</span></span>
    * <span data-ttu-id="a1f36-152">**Операционная система**: этот параметр в настоящее время доступен только в том случае, если вы выбрали hello Kubernetes orchestrator.</span><span class="sxs-lookup"><span data-stu-id="a1f36-152">**Operating system**: This setting is currently available only if you selected hello Kubernetes orchestrator.</span></span> <span data-ttu-id="a1f36-153">Выберите ОС Linux или toorun операционной системы Windows Server на агентах hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-153">Choose either a Linux distribution or a Windows Server operating system toorun on hello agents.</span></span> <span data-ttu-id="a1f36-154">Этот параметр определяет, может ли кластер запускать приложения-контейнеры Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="a1f36-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="a1f36-155">Поддержка контейнера Windows для кластеров Kubernetes находится на этапе предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="a1f36-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="a1f36-156">Для кластеров DC/OS и Swarm в настоящее время поддерживаются только агенты Linux в Службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f36-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="a1f36-157">**Учетные данные агента**: Если вы выбрали операционной системы Windows hello, введите администратор **имя пользователя** и **пароль** hello агента ВМ.</span><span class="sxs-lookup"><span data-stu-id="a1f36-157">**Agent credentials**: If you selected hello Windows operating system, enter an administrator **User name** and **Password** for hello agent VMs.</span></span> 

    ![Конфигурация агента](./media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="a1f36-159">Нажмите кнопку **ОК** когда вы будете готовы tooproceed.</span><span class="sxs-lookup"><span data-stu-id="a1f36-159">Click **OK** when you're ready tooproceed.</span></span>

6. <span data-ttu-id="a1f36-160">Когда проверка службы завершится, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a1f36-160">After service validation finishes, click **OK**.</span></span>

    ![Проверка](./media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="a1f36-162">Просмотреть условия hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-162">Review hello terms.</span></span> <span data-ttu-id="a1f36-163">процесс развертывания toostart hello, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="a1f36-163">toostart hello deployment process, click **Create**.</span></span>

    <span data-ttu-id="a1f36-164">Если выбрана toopin hello развертывания toohello портал Azure, можно просмотреть состояние развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-164">If you've elected toopin hello deployment toohello Azure portal, you can see hello deployment status.</span></span>

    ![Состояния развертывания](./media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="a1f36-166">Hello развертывания занимает несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a1f36-166">hello deployment takes several minutes toocomplete.</span></span> <span data-ttu-id="a1f36-167">Затем кластер hello Azure контейнера службы будет готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="a1f36-167">Then, hello Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="a1f36-168">Создание кластера с помощью шаблона быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="a1f36-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="a1f36-169">Быстрый запуск Azure шаблоны, доступные toodeploy кластера в службе контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f36-169">Azure quickstart templates are available toodeploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="a1f36-170">Hello при условии, что примеры использования шаблоны могут быть измененный tooinclude дополнительные или расширенные конфигурации Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f36-170">hello provided quickstart templates can be modified tooinclude additional or advanced Azure configuration.</span></span> <span data-ttu-id="a1f36-171">toocreate кластер контейнера службы Azure с помощью шаблона Azure краткое руководство, требуется подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f36-171">toocreate an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="a1f36-172">Если у вас ее нет, зарегистрируйтесь, чтобы [воспользоваться бесплатной пробной версией](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="a1f36-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="a1f36-173">Выполните эти шаги toodeploy кластера, с помощью шаблона и hello Azure CLI 2.0 (в разделе [инструкции по установке и настройке](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="a1f36-173">Follow these steps toodeploy a cluster using a template and hello Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="a1f36-174">Если вы в системе Windows, можно использовать аналогичные действия toodeploy шаблона с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1f36-174">If you're on a Windows system, you can use similar steps toodeploy a template using Azure PowerShell.</span></span> <span data-ttu-id="a1f36-175">Инструкции см. далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="a1f36-175">See steps later in this section.</span></span> <span data-ttu-id="a1f36-176">Можно также развернуть шаблон через hello [портала](../../azure-resource-manager/resource-group-template-deploy-portal.md) или других методов.</span><span class="sxs-lookup"><span data-stu-id="a1f36-176">You can also deploy a template through hello [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="a1f36-177">toodeploy DC/OS помощью Docker Swarm и Kubernetes кластера, выберите один из шаблонов доступные примеры использования hello из GitHub.</span><span class="sxs-lookup"><span data-stu-id="a1f36-177">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="a1f36-178">Ниже приведен неполный список шаблонов.</span><span class="sxs-lookup"><span data-stu-id="a1f36-178">A partial list follows.</span></span> <span data-ttu-id="a1f36-179">Hello DC/OS и шаблонов группу мелких объектов являются hello же, за исключением выбора orchestrator по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-179">hello DC/OS and Swarm templates are hello same, except for hello default orchestrator selection.</span></span>

    * <span data-ttu-id="a1f36-180">[Шаблон DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos).</span><span class="sxs-lookup"><span data-stu-id="a1f36-180">[DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)</span></span>
    * <span data-ttu-id="a1f36-181">[шаблон Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm);</span><span class="sxs-lookup"><span data-stu-id="a1f36-181">[Swarm template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)</span></span>
    * <span data-ttu-id="a1f36-182">[Шаблон Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="a1f36-182">[Kubernetes template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)</span></span>

2. <span data-ttu-id="a1f36-183">Войдите в учетную запись Azure tooyour (`az login`) и убедитесь, что hello Azure CLI tooyour подключенных подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f36-183">Log in tooyour Azure account (`az login`), and make sure that hello Azure CLI is connected tooyour Azure subscription.</span></span> <span data-ttu-id="a1f36-184">Подписка по умолчанию hello можно просмотреть с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a1f36-184">You can see hello default subscription by using hello following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="a1f36-185">При наличии более одной подписки и необходимость tooset подписки по умолчанию выполнить `az account set --subscription` и укажите идентификатор подписки hello или имя.</span><span class="sxs-lookup"><span data-stu-id="a1f36-185">If you have more than one subscription and need tooset a different default subscription, run `az account set --subscription` and specify hello subscription ID or name.</span></span>

3. <span data-ttu-id="a1f36-186">Рекомендуется используйте новую группу ресурсов для развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-186">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="a1f36-187">использовать toocreate группу ресурсов hello `az group create` команда указывает имя группы ресурсов и расположение:</span><span class="sxs-lookup"><span data-stu-id="a1f36-187">toocreate a resource group, use hello `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="a1f36-188">Шаблон JSON файла содержащего hello необходимые параметры.</span><span class="sxs-lookup"><span data-stu-id="a1f36-188">Create a JSON file containing hello required template parameters.</span></span> <span data-ttu-id="a1f36-189">Загрузите hello параметры файл с именем `azuredeploy.parameters.json` , сопровождающее шаблона службы контейнера Azure hello `azuredeploy.json` в GitHub.</span><span class="sxs-lookup"><span data-stu-id="a1f36-189">Download hello parameters file named `azuredeploy.parameters.json` that accompanies hello Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="a1f36-190">Введите необходимые значения параметров кластера.</span><span class="sxs-lookup"><span data-stu-id="a1f36-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="a1f36-191">Например, hello toouse [шаблона DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), укажите значения параметров для `dnsNamePrefix` и `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="a1f36-191">For example, toouse hello [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="a1f36-192">В разделе описания hello в `azuredeploy.json` и параметры для других параметров.</span><span class="sxs-lookup"><span data-stu-id="a1f36-192">See hello descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="a1f36-193">Создание контейнера службы кластера, передав файл параметров развертывания hello с hello следующую команду, где:</span><span class="sxs-lookup"><span data-stu-id="a1f36-193">Create a Container Service cluster by passing hello deployment parameters file with hello following command, where:</span></span>

    * <span data-ttu-id="a1f36-194">**RESOURCE_GROUP** — имя группы ресурсов hello, созданную в предыдущем шаге hello hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-194">**RESOURCE_GROUP** is hello name of hello resource group that you created in hello previous step.</span></span>
    * <span data-ttu-id="a1f36-195">**DEPLOYMENT_NAME** (необязательно) — это имя, вы предоставляете toohello развертывания.</span><span class="sxs-lookup"><span data-stu-id="a1f36-195">**DEPLOYMENT_NAME** (optional) is a name you give toohello deployment.</span></span>
    * <span data-ttu-id="a1f36-196">**TEMPLATE_URI** hello расположения файла развертывания hello `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="a1f36-196">**TEMPLATE_URI** is hello location of hello deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="a1f36-197">Этот URI должен быть Необработанный файл hello, указатель toohello GitHub пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a1f36-197">This URI must be hello Raw file, not a pointer toohello GitHub UI.</span></span> <span data-ttu-id="a1f36-198">toofind этот URI выберите hello `azuredeploy.json` на GitHub и нажмите кнопку hello **Raw** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a1f36-198">toofind this URI, select hello `azuredeploy.json` file in GitHub, and click hello **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="a1f36-199">Можно также предоставляют параметры, как строку формата JSON в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-199">You can also provide parameters as a JSON-formatted string on hello command line.</span></span> <span data-ttu-id="a1f36-200">Используйте следующие команды аналогичные toohello:</span><span class="sxs-lookup"><span data-stu-id="a1f36-200">Use a command similar toohello following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="a1f36-201">Hello развертывания занимает несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a1f36-201">hello deployment takes several minutes toocomplete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="a1f36-202">Аналогичные команды PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1f36-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="a1f36-203">Шаблон кластера Службы контейнеров Azure также можно развернуть с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1f36-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="a1f36-204">В этом документе основана на hello версии 1.0 [модуля Azure PowerShell](https://azure.microsoft.com/blog/azps-1-0/).</span><span class="sxs-lookup"><span data-stu-id="a1f36-204">This document is based on hello version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="a1f36-205">toodeploy DC/OS помощью Docker Swarm и Kubernetes кластера, выберите один из шаблонов доступные примеры использования hello из GitHub.</span><span class="sxs-lookup"><span data-stu-id="a1f36-205">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="a1f36-206">Ниже приведен неполный список шаблонов.</span><span class="sxs-lookup"><span data-stu-id="a1f36-206">A partial list follows.</span></span> <span data-ttu-id="a1f36-207">Обратите внимание, что hello DC/OS и шаблонов группу мелких объектов являются hello таким же, за исключением hello выбора orchestrator по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-207">Note that hello DC/OS and Swarm templates are hello same, with hello exception of hello default orchestrator selection.</span></span>

    * <span data-ttu-id="a1f36-208">[Шаблон DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos).</span><span class="sxs-lookup"><span data-stu-id="a1f36-208">[DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)</span></span>
    * <span data-ttu-id="a1f36-209">[шаблон Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm);</span><span class="sxs-lookup"><span data-stu-id="a1f36-209">[Swarm template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)</span></span>
    * <span data-ttu-id="a1f36-210">[Шаблон Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="a1f36-210">[Kubernetes template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)</span></span>

2. <span data-ttu-id="a1f36-211">Перед созданием кластера в вашей подписке Azure, убедитесь, что сеанс PowerShell подписанный в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a1f36-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in tooAzure.</span></span> <span data-ttu-id="a1f36-212">Это можно сделать с помощью hello `Get-AzureRMSubscription` команды:</span><span class="sxs-lookup"><span data-stu-id="a1f36-212">You can do this with hello `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="a1f36-213">Если требуется toosign в tooAzure использовать hello `Login-AzureRMAccount` команды:</span><span class="sxs-lookup"><span data-stu-id="a1f36-213">If you need toosign in tooAzure, use hello `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="a1f36-214">Рекомендуется используйте новую группу ресурсов для развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-214">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="a1f36-215">использовать toocreate группу ресурсов hello `New-AzureRmResourceGroup` команду и укажите регион имени и места назначения группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="a1f36-215">toocreate a resource group, use hello `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="a1f36-216">После создания группы ресурсов, можно создать кластер с hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="a1f36-216">After you create a resource group, you can create your cluster with hello following command.</span></span> <span data-ttu-id="a1f36-217">Hello URI hello требуемого указан шаблон с hello `-TemplateUri` параметра.</span><span class="sxs-lookup"><span data-stu-id="a1f36-217">hello URI of hello desired template is specified with hello `-TemplateUri` parameter.</span></span> <span data-ttu-id="a1f36-218">При выполнении этой команды в PowerShell отобразится запрос на ввод значений параметров развертывания.</span><span class="sxs-lookup"><span data-stu-id="a1f36-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="a1f36-219">Выбор параметров шаблона</span><span class="sxs-lookup"><span data-stu-id="a1f36-219">Provide template parameters</span></span>
<span data-ttu-id="a1f36-220">Если вы знакомы с помощью PowerShell, вы знаете, что циклического перемещения между hello доступные параметры командлета, введите знак минус (-) и нажав клавишу TAB hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-220">If you're familiar with PowerShell, you know that you can cycle through hello available parameters for a cmdlet by typing a minus sign (-) and then pressing hello TAB key.</span></span> <span data-ttu-id="a1f36-221">Точно так же это работает с параметрами, которые вы определили в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="a1f36-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="a1f36-222">Сразу после ввода имени шаблона hello hello командлет выбирает шаблон hello, выполняет синтаксический анализ параметров hello и динамически добавляет команды toohello параметры шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-222">As soon as you type hello template name, hello cmdlet fetches hello template, parses hello parameters, and adds hello template parameters toohello command dynamically.</span></span> <span data-ttu-id="a1f36-223">Это делает значения параметров шаблона легко toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-223">This makes it easy toospecify hello template parameter values.</span></span> <span data-ttu-id="a1f36-224">И, если вы забыли требуемое значение параметра, PowerShell запрашивает значение hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-224">And, if you forget a required parameter value, PowerShell prompts you for hello value.</span></span>

<span data-ttu-id="a1f36-225">Ниже приведен полный команда hello с параметрами, которые включены.</span><span class="sxs-lookup"><span data-stu-id="a1f36-225">Here is hello full command, with parameters included.</span></span> <span data-ttu-id="a1f36-226">Укажите собственные значения для hello имена ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="a1f36-226">Provide your own values for hello names of hello resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="a1f36-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1f36-227">Next steps</span></span>
<span data-ttu-id="a1f36-228">Теперь, когда у вас есть работающий кластер, выберите ссылки ниже, чтобы узнать о возможностях подключения и управления.</span><span class="sxs-lookup"><span data-stu-id="a1f36-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="a1f36-229">Подключите кластер tooan контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="a1f36-229">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="a1f36-230">Работа со службой контейнеров Azure и DC/OS</span><span class="sxs-lookup"><span data-stu-id="a1f36-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="a1f36-231">Работа со службой контейнеров Azure и Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="a1f36-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="a1f36-232">Работа со службой контейнеров Azure и Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a1f36-232">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)
