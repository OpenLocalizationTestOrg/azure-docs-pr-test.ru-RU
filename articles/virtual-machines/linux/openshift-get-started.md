---
title: "Источник OpenShift tooAzure aaaDeploy | Документы Microsoft"
description: "Узнайте toodeploy OpenShift источника tooAzure виртуальных машин."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a><span data-ttu-id="51a4e-103">Развертывание источника OpenShift tooAzure виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="51a4e-103">Deploy OpenShift Origin tooAzure Virtual Machines</span></span> 

<span data-ttu-id="51a4e-104">[OpenShift Origin](https://www.openshift.org/) — это платформа контейнера с открытым исходным кодом, созданная на основе [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="51a4e-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="51a4e-105">Он упрощает процесс hello развертывания, масштабирование и эксплуатации приложения с несколькими клиентами.</span><span class="sxs-lookup"><span data-stu-id="51a4e-105">It simplifies hello process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="51a4e-106">В этом руководстве описывается, как hello toodeploy OpenShift источника на виртуальных машинах Azure с помощью Azure CLI и шаблоны Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="51a4e-106">This guide describes how toodeploy OpenShift Origin on Azure Virtual Machines using hello Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="51a4e-107">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="51a4e-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51a4e-108">Создание ключей SSH для кластера hello OpenShift KeyVault toomanage.</span><span class="sxs-lookup"><span data-stu-id="51a4e-108">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="51a4e-109">развернуть кластер OpenShift на виртуальных машинах Azure;</span><span class="sxs-lookup"><span data-stu-id="51a4e-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="51a4e-110">Установка и настройка hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello кластера.</span><span class="sxs-lookup"><span data-stu-id="51a4e-110">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>
> * <span data-ttu-id="51a4e-111">Настройка развертывания OpenShift hello.</span><span class="sxs-lookup"><span data-stu-id="51a4e-111">Customize hello OpenShift deployment.</span></span>

<span data-ttu-id="51a4e-112">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="51a4e-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="51a4e-113">В этом кратком руководстве требует hello Azure CLI версии 2.0.8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="51a4e-113">This quick start requires hello Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="51a4e-114">версия toofind hello, запустите `az --version`.</span><span class="sxs-lookup"><span data-stu-id="51a4e-114">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="51a4e-115">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="51a4e-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="51a4e-116">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="51a4e-116">Log in tooAzure</span></span> 
<span data-ttu-id="51a4e-117">Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкции или нажмите кнопку **опробовать** toouse оболочки облака.</span><span class="sxs-lookup"><span data-stu-id="51a4e-117">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions or click **Try it** toouse Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="51a4e-118">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="51a4e-118">Create a resource group</span></span>

<span data-ttu-id="51a4e-119">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="51a4e-119">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="51a4e-120">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="51a4e-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="51a4e-121">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.</span><span class="sxs-lookup"><span data-stu-id="51a4e-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="51a4e-122">создать хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="51a4e-122">Create a Key Vault</span></span>
<span data-ttu-id="51a4e-123">Создать ключи SSH для кластера hello hello toostore KeyVault hello [az keyvault создать](/cli/azure/keyvault#create) команды.</span><span class="sxs-lookup"><span data-stu-id="51a4e-123">Create a KeyVault toostore hello SSH keys for hello cluster with hello [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="51a4e-124">Создание ключа SSH</span><span class="sxs-lookup"><span data-stu-id="51a4e-124">Create an SSH key</span></span> 
<span data-ttu-id="51a4e-125">SSH-ключ является toohello доступа необходимые toosecure источника OpenShift кластера.</span><span class="sxs-lookup"><span data-stu-id="51a4e-125">An SSH key is needed toosecure access toohello OpenShift Origin cluster.</span></span> <span data-ttu-id="51a4e-126">Создать пару ключей SSH с помощью hello `ssh-keygen` команды.</span><span class="sxs-lookup"><span data-stu-id="51a4e-126">Create an SSH key-pair using hello `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="51a4e-127">Hello пару ключей SSH, создаваемые вами, не должны иметь парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="51a4e-127">hello SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="51a4e-128">Дополнительные сведения о ключах SSH в Windows [как ключи toocreate SSH в Windows](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="51a4e-128">For more information on SSH keys on Windows, [How toocreate SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="51a4e-129">Сохранение закрытого ключа SSH в Key Vault</span><span class="sxs-lookup"><span data-stu-id="51a4e-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="51a4e-130">Hello OpenShift развертывания использует hello SSH-ключ создан доступа toosecure toohello OpenShift master.</span><span class="sxs-lookup"><span data-stu-id="51a4e-130">hello OpenShift deployment uses hello SSH key you created toosecure access toohello OpenShift master.</span></span> <span data-ttu-id="51a4e-131">Развертывание toosecurely tooenable hello извлечь ключ SSH hello, hello ключ хранится в хранилище ключей с помощью hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="51a4e-131">tooenable hello deployment toosecurely retrieve hello SSH key, store hello key in Key Vault using hello following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="51a4e-132">Включение для развертывания шаблона</span><span class="sxs-lookup"><span data-stu-id="51a4e-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="51a4e-133">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="51a4e-133">Create a service principal</span></span> 
<span data-ttu-id="51a4e-134">OpenShift взаимодействует с Azure, используя имя пользователя и пароль или субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="51a4e-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="51a4e-135">Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и инструментами автоматизации, такими как OpenShift.</span><span class="sxs-lookup"><span data-stu-id="51a4e-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="51a4e-136">Управление и определить hello разрешения участника службы hello toowhat операции можно выполнять в Azure.</span><span class="sxs-lookup"><span data-stu-id="51a4e-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="51a4e-137">безопасность tooimprove просто задать имя пользователя и пароль, этот пример создает базовую службу участника.</span><span class="sxs-lookup"><span data-stu-id="51a4e-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="51a4e-138">Создание службы с основной [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) и hello учетные данные, которые требуется OpenShift выходные данные:</span><span class="sxs-lookup"><span data-stu-id="51a4e-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="51a4e-139">Запишите команда hello возвращать свойство appId hello.</span><span class="sxs-lookup"><span data-stu-id="51a4e-139">Take note of hello appId property returned from hello command.</span></span>
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > <span data-ttu-id="51a4e-140">Не используйте ненадежный пароль.</span><span class="sxs-lookup"><span data-stu-id="51a4e-140">Don't create an insecure password.</span></span>  <span data-ttu-id="51a4e-141">Следуйте руководству по [правилам и ограничениям для паролей Azure AD](/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="51a4e-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="51a4e-142">Дополнительные сведения о субъект-службе см. в статье [Создание субъекта-службы Azure с помощью Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="51a4e-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-hello-openshift-origin-template"></a><span data-ttu-id="51a4e-143">Развертывание hello OpenShift источника шаблона</span><span class="sxs-lookup"><span data-stu-id="51a4e-143">Deploy hello OpenShift Origin template</span></span>
<span data-ttu-id="51a4e-144">Далее развернем OpenShift Origin с помощью шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="51a4e-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="51a4e-145">Hello следующая команда требует az CLI 2.0.8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="51a4e-145">hello following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="51a4e-146">Вы можете проверить hello az CLI версии с hello `az --version` команды.</span><span class="sxs-lookup"><span data-stu-id="51a4e-146">You can verify hello az CLI version with hello `az --version` command.</span></span> <span data-ttu-id="51a4e-147">hello tooupdate версии CLI. в разделе [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="51a4e-147">tooupdate hello CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="51a4e-148">Используйте hello `appId` значение из hello участника службы, созданные ранее для hello `aadClientId` параметра.</span><span class="sxs-lookup"><span data-stu-id="51a4e-148">Use hello `appId` value from hello service principal you created earlier for hello `aadClientId` parameter.</span></span>

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
<span data-ttu-id="51a4e-149">Hello развертывания может занять до минуты toocomplete too20.</span><span class="sxs-lookup"><span data-stu-id="51a4e-149">hello deployment may take up too20 minutes toocomplete.</span></span> <span data-ttu-id="51a4e-150">Hello URL-адрес консоли OpenShift hello и DNS-имя hello OpenShift мастер находится на печать toohello терминалов после завершения развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="51a4e-150">hello URL of hello OpenShift console and DNS name of hello OpenShift master is printed toohello terminal when hello deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a><span data-ttu-id="51a4e-151">Подключите кластер OpenShift toohello</span><span class="sxs-lookup"><span data-stu-id="51a4e-151">Connect toohello OpenShift cluster</span></span>
<span data-ttu-id="51a4e-152">После завершения развертывания hello подключения консоли OpenShift toohello, с помощью браузера hello, с помощью hello `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="51a4e-152">When hello deployment completes, connect toohello OpenShift console using hello browser using hello `OpenShift Console Uri`.</span></span> <span data-ttu-id="51a4e-153">Кроме того можно подключаться toohello OpenShift master с помощью hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="51a4e-153">Alternatively, you can connect toohello OpenShift master using hello following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="51a4e-154">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="51a4e-154">Clean up resources</span></span>
<span data-ttu-id="51a4e-155">Если больше не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, OpenShift кластера и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="51a4e-155">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="51a4e-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="51a4e-156">Next steps</span></span>

<span data-ttu-id="51a4e-157">В рамках этого руководства вы узнали, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="51a4e-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="51a4e-158">Создание ключей SSH для кластера hello OpenShift KeyVault toomanage.</span><span class="sxs-lookup"><span data-stu-id="51a4e-158">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="51a4e-159">развернуть кластер OpenShift на виртуальных машинах Azure;</span><span class="sxs-lookup"><span data-stu-id="51a4e-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="51a4e-160">Установка и настройка hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello кластера.</span><span class="sxs-lookup"><span data-stu-id="51a4e-160">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>

<span data-ttu-id="51a4e-161">Теперь, когда вы развернули кластер OpenShift Origin,</span><span class="sxs-lookup"><span data-stu-id="51a4e-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="51a4e-162">Можно выполнить как toolearn OpenShift учебники toodeploy первого приложения и используйте hello OpenShift средства.</span><span class="sxs-lookup"><span data-stu-id="51a4e-162">You can follow OpenShift tutorials toolearn how toodeploy your first application and use hello OpenShift tools.</span></span> <span data-ttu-id="51a4e-163">В разделе [Приступая к работе с источником OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget работы.</span><span class="sxs-lookup"><span data-stu-id="51a4e-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) tooget started.</span></span> 
