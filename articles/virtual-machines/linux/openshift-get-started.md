---
title: "Развертывание OpenShift Origin в Azure | Документация Майкрософт"
description: "Узнайте, как развернуть OpenShift Origin на виртуальных машинах Azure."
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
ms.openlocfilehash: e03da05625e440eab29ccc28a2343d3433fc7607
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-openshift-origin-to-azure-virtual-machines"></a><span data-ttu-id="ec398-103">Развертывание OpenShift Origin на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="ec398-103">Deploy OpenShift Origin to Azure Virtual Machines</span></span> 

<span data-ttu-id="ec398-104">[OpenShift Origin](https://www.openshift.org/) — это платформа контейнера с открытым исходным кодом, созданная на основе [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="ec398-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="ec398-105">Она упрощает развертывание, масштабирование и эксплуатацию приложений с несколькими клиентами.</span><span class="sxs-lookup"><span data-stu-id="ec398-105">It simplifies the process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="ec398-106">В этом руководстве описывается развертывание OpenShift Origin на виртуальных машинах Azure с помощью шаблонов Azure CLI и Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec398-106">This guide describes how to deploy OpenShift Origin on Azure Virtual Machines using the Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="ec398-107">Из этого руководства вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ec398-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ec398-108">создать хранилище ключей KeyVault, чтобы управлять ключами SSH для кластера OpenShift;</span><span class="sxs-lookup"><span data-stu-id="ec398-108">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="ec398-109">развернуть кластер OpenShift на виртуальных машинах Azure;</span><span class="sxs-lookup"><span data-stu-id="ec398-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="ec398-110">установить и настроить [интерфейс командной строки OpenShift](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) для управления кластером;</span><span class="sxs-lookup"><span data-stu-id="ec398-110">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>
> * <span data-ttu-id="ec398-111">настроить развертывание OpenShift.</span><span class="sxs-lookup"><span data-stu-id="ec398-111">Customize the OpenShift deployment.</span></span>

<span data-ttu-id="ec398-112">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) , прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="ec398-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="ec398-113">Для работы с этим кратким руководством требуется Azure CLI версии не ниже 2.0.8.</span><span class="sxs-lookup"><span data-stu-id="ec398-113">This quick start requires the Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="ec398-114">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="ec398-114">To find the version, run `az --version`.</span></span> <span data-ttu-id="ec398-115">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ec398-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="ec398-116">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="ec398-116">Log in to Azure</span></span> 
<span data-ttu-id="ec398-117">Войдите в подписку Azure с помощью команды [az login](/cli/azure/#login) и следуйте инструкциям на экране или щелкните **Попробовать**, чтобы использовать Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="ec398-117">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions or click **Try it** to use Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="ec398-118">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="ec398-118">Create a resource group</span></span>

<span data-ttu-id="ec398-119">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ec398-119">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ec398-120">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="ec398-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="ec398-121">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="ec398-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="ec398-122">создать хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="ec398-122">Create a Key Vault</span></span>
<span data-ttu-id="ec398-123">Создайте хранилище ключей KeyVault, где будут храниться ключи SSH для кластера, с помощью команды [az keyvault create](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="ec398-123">Create a KeyVault to store the SSH keys for the cluster with the [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="ec398-124">Создание ключа SSH</span><span class="sxs-lookup"><span data-stu-id="ec398-124">Create an SSH key</span></span> 
<span data-ttu-id="ec398-125">Ключ SSH необходим для обеспечения безопасного доступа к кластеру OpenShift Origin.</span><span class="sxs-lookup"><span data-stu-id="ec398-125">An SSH key is needed to secure access to the OpenShift Origin cluster.</span></span> <span data-ttu-id="ec398-126">Создайте пару ключей SSH с помощью команды `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="ec398-126">Create an SSH key-pair using the `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="ec398-127">Создаваемая пара ключей SSH не должна содержать парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="ec398-127">The SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="ec398-128">Дополнительные сведения о ключах SSH в Windows см. в статье [Использование ключей SSH с Windows в Azure](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="ec398-128">For more information on SSH keys on Windows, [How to create SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="ec398-129">Сохранение закрытого ключа SSH в Key Vault</span><span class="sxs-lookup"><span data-stu-id="ec398-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="ec398-130">Развертывание OpenShift использует созданный ключ SSH, чтобы защитить доступ к основному кластеру OpenShift.</span><span class="sxs-lookup"><span data-stu-id="ec398-130">The OpenShift deployment uses the SSH key you created to secure access to the OpenShift master.</span></span> <span data-ttu-id="ec398-131">Чтобы обеспечить для развертывания безопасное извлечение ключа SSH, сохраните ключ в Key Vault с помощью команды ниже:</span><span class="sxs-lookup"><span data-stu-id="ec398-131">To enable the deployment to securely retrieve the SSH key, store the key in Key Vault using the following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="ec398-132">Включение для развертывания шаблона</span><span class="sxs-lookup"><span data-stu-id="ec398-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="ec398-133">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="ec398-133">Create a service principal</span></span> 
<span data-ttu-id="ec398-134">OpenShift взаимодействует с Azure, используя имя пользователя и пароль или субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="ec398-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="ec398-135">Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и инструментами автоматизации, такими как OpenShift.</span><span class="sxs-lookup"><span data-stu-id="ec398-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="ec398-136">Вы можете управлять разрешениями на то, какие операции может выполнять субъект-служба в Azure, и определять их.</span><span class="sxs-lookup"><span data-stu-id="ec398-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="ec398-137">Для обеспечения более высокого уровня безопасности, чем при предоставлении имени пользователя и пароля, в этом примере создается базовая субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="ec398-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="ec398-138">Создайте субъект-службу с помощью команды [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) и выведите учетные данные, необходимые для OpenShift:</span><span class="sxs-lookup"><span data-stu-id="ec398-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="ec398-139">Запишите свойство appId, возвращенное из команды.</span><span class="sxs-lookup"><span data-stu-id="ec398-139">Take note of the appId property returned from the command.</span></span>
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
 > <span data-ttu-id="ec398-140">Не используйте ненадежный пароль.</span><span class="sxs-lookup"><span data-stu-id="ec398-140">Don't create an insecure password.</span></span>  <span data-ttu-id="ec398-141">Следуйте руководству по [правилам и ограничениям для паролей Azure AD](/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="ec398-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="ec398-142">Дополнительные сведения о субъект-службе см. в статье [Создание субъекта-службы Azure с помощью Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="ec398-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-the-openshift-origin-template"></a><span data-ttu-id="ec398-143">Развертывание шаблона OpenShift Origin</span><span class="sxs-lookup"><span data-stu-id="ec398-143">Deploy the OpenShift Origin template</span></span>
<span data-ttu-id="ec398-144">Далее развернем OpenShift Origin с помощью шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec398-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="ec398-145">Для выполнения следующей команды необходим интерфейс командной строки версии не ниже 2.0.8.</span><span class="sxs-lookup"><span data-stu-id="ec398-145">The following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="ec398-146">Узнать свою версию CLI вы можете с помощью команды `az --version`.</span><span class="sxs-lookup"><span data-stu-id="ec398-146">You can verify the az CLI version with the `az --version` command.</span></span> <span data-ttu-id="ec398-147">Чтобы обновить версию CLI, ознакомьтесь со статьей [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ec398-147">To update the CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="ec398-148">Используйте значение `appId` созданной ранее субъект-службы для параметра `aadClientId`.</span><span class="sxs-lookup"><span data-stu-id="ec398-148">Use the `appId` value from the service principal you created earlier for the `aadClientId` parameter.</span></span>

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
<span data-ttu-id="ec398-149">Развертывание может занять до 20 минут.</span><span class="sxs-lookup"><span data-stu-id="ec398-149">The deployment may take up to 20 minutes to complete.</span></span> <span data-ttu-id="ec398-150">После завершения развертывания в терминале появятся сведения об URL-адресе консоли OpenShift, а также DNS-имя основного кластера OpenShift.</span><span class="sxs-lookup"><span data-stu-id="ec398-150">The URL of the OpenShift console and DNS name of the OpenShift master is printed to the terminal when the deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-to-the-openshift-cluster"></a><span data-ttu-id="ec398-151">Подключение к кластеру OpenShift</span><span class="sxs-lookup"><span data-stu-id="ec398-151">Connect to the OpenShift cluster</span></span>
<span data-ttu-id="ec398-152">После завершения развертывания подключитесь к консоли OpenShift через браузер с помощью `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="ec398-152">When the deployment completes, connect to the OpenShift console using the browser using the `OpenShift Console Uri`.</span></span> <span data-ttu-id="ec398-153">Кроме того, вы можете подключиться к основному кластеру OpenShift, используя команду ниже:</span><span class="sxs-lookup"><span data-stu-id="ec398-153">Alternatively, you can connect to the OpenShift master using the following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="ec398-154">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="ec398-154">Clean up resources</span></span>
<span data-ttu-id="ec398-155">Вы можете удалить ставшие ненужными группу ресурсов, кластер OpenShift и все связанные с ним ресурсы, выполнив команду [az group delete](/cli/azure/group#delete).</span><span class="sxs-lookup"><span data-stu-id="ec398-155">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ec398-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec398-156">Next steps</span></span>

<span data-ttu-id="ec398-157">В рамках этого руководства вы узнали, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ec398-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="ec398-158">создать хранилище ключей KeyVault, чтобы управлять ключами SSH для кластера OpenShift;</span><span class="sxs-lookup"><span data-stu-id="ec398-158">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="ec398-159">развернуть кластер OpenShift на виртуальных машинах Azure;</span><span class="sxs-lookup"><span data-stu-id="ec398-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="ec398-160">установить и настроить [интерфейс командной строки OpenShift](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) для управления кластером.</span><span class="sxs-lookup"><span data-stu-id="ec398-160">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>

<span data-ttu-id="ec398-161">Теперь, когда вы развернули кластер OpenShift Origin,</span><span class="sxs-lookup"><span data-stu-id="ec398-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="ec398-162">можно ознакомиться со следующими руководствами, чтобы узнать, как развернуть свое первое приложение, а также как использовать инструменты OpenShift.</span><span class="sxs-lookup"><span data-stu-id="ec398-162">You can follow OpenShift tutorials to learn how to deploy your first application and use the OpenShift tools.</span></span> <span data-ttu-id="ec398-163">Ознакомьтесь с [обзором OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html).</span><span class="sxs-lookup"><span data-stu-id="ec398-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) to get started.</span></span> 
