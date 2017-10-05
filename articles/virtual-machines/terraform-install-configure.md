---
title: "Установка и настройка Terraform для подготовки виртуальных машин и другой инфраструктуры в Azure | Документация Майкрософт"
description: "Узнайте, как установить и настроить Terraform для создания ресурсов Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 1f26bccf279ebb61fbf77767186d0435e4f4ba40
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-configure-terraform-to-provision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="050b2-103">Установка и настройка Terraform для подготовки виртуальных машин и другой инфраструктуры в Azure</span><span class="sxs-lookup"><span data-stu-id="050b2-103">Install and configure Terraform to provision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="050b2-104">В этой статье описано, как установить и настроить Terraform для подготовки ресурсов, таких как виртуальные машины, в Azure.</span><span class="sxs-lookup"><span data-stu-id="050b2-104">This article describes the necessary steps to install and configure Terraform to provision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="050b2-105">Вы узнаете, как создать и использовать учетные данные Azure, необходимые Terraform для подготовки облачных ресурсов в безопасном режиме.</span><span class="sxs-lookup"><span data-stu-id="050b2-105">You will learn how to create and use Azure credentials to enable Terraform to provision cloud resources in a secure manner.</span></span>

<span data-ttu-id="050b2-106">Terraform от компании HashiCorp предоставляет простой способ определить и развернуть облачную инфраструктуру, используя настраиваемый язык шаблонов HCL.</span><span class="sxs-lookup"><span data-stu-id="050b2-106">HashiCorp Terraform provides an easy way to define and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="050b2-107">Этот настраиваемый язык [удобен для написания и прост для понимания](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="050b2-107">This custom language is [easy to write and easy to understand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="050b2-108">Кроме того, с помощью команды `terraform plan` вы можете визуализировать изменения, внесенные в инфраструктуру, прежде чем они будут зафиксированы.</span><span class="sxs-lookup"><span data-stu-id="050b2-108">Additionally, by using the `terraform plan` command, you can visualize the changes to your infrastructure before you commit them.</span></span> <span data-ttu-id="050b2-109">Чтобы приступить к использованию Terraform с Azure, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="050b2-109">Follow these steps to start using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="050b2-110">Установка Terraform</span><span class="sxs-lookup"><span data-stu-id="050b2-110">Install Terraform</span></span>
<span data-ttu-id="050b2-111">Чтобы установить Terraform, [скачайте](https://www.terraform.io/downloads.html) пакет, соответствующий вашей операционной системе, в отдельный каталог установки.</span><span class="sxs-lookup"><span data-stu-id="050b2-111">To install Terraform, [download](https://www.terraform.io/downloads.html) the package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="050b2-112">Этот пакет содержит один исполняемый файл, для которого также необходимо задать глобальный путь.</span><span class="sxs-lookup"><span data-stu-id="050b2-112">The download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="050b2-113">Инструкции по настройке пути в операционных системах Linux и Mac можно найти на [этой веб-странице](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="050b2-113">For instructions on how to set the path on Linux and Mac, go to [this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="050b2-114">Инструкции по настройке пути в Windows можно найти на [этой веб-странице](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="050b2-114">For instructions on how to set the path on Windows, go to [this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="050b2-115">Проверьте правильность установки, выполнив команду `terraform`.</span><span class="sxs-lookup"><span data-stu-id="050b2-115">To verify your installation, run the `terraform` command.</span></span> <span data-ttu-id="050b2-116">В качестве выходных данных должен отобразиться список доступных параметров Terraform.</span><span class="sxs-lookup"><span data-stu-id="050b2-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="050b2-117">Затем необходимо разрешить Terraform доступ к вашей подписке Azure для выполнения подготовки инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="050b2-117">Next, you need to allow Terraform access to your Azure subscription to perform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-to-azure"></a><span data-ttu-id="050b2-118">Настройка доступа Terraform в Azure</span><span class="sxs-lookup"><span data-stu-id="050b2-118">Set up Terraform access to Azure</span></span>
<span data-ttu-id="050b2-119">Чтобы позволить Terraform предоставлять ресурсы в Azure, вам необходимо создать два объекта в Azure Active Directory (Azure AD): приложение Azure AD и субъект-службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="050b2-119">To enable Terraform to provision resources into Azure, you need to create two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="050b2-120">Затем идентификаторы этих сущностей используются в сценариях Terraform.</span><span class="sxs-lookup"><span data-stu-id="050b2-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="050b2-121">Субъект-служба — это локальный экземпляр глобального приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="050b2-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="050b2-122">Субъект-службы позволяет осуществлять детальный контроль локального доступа к глобальным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="050b2-122">A service principal allows granular local access control to global resources.</span></span>

<span data-ttu-id="050b2-123">Существует несколько способов создания приложения Azure AD и субъекта-службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="050b2-123">There are several ways to create an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="050b2-124">Самым простым и быстрым способом на сегодняшний день является установка с помощью интерфейса командной строки Azure CLI 2.0, который [можно скачать и установить на Windows, Mac или Linux](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="050b2-124">The easiest and fastest way today is to use Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="050b2-125">Для создания необходимой инфраструктуры безопасности можно также воспользоваться PowerShell или Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="050b2-125">You also can use PowerShell or Azure CLI 1.0 to create the necessary security infrastructure.</span></span> <span data-ttu-id="050b2-126">Ниже приведены инструкции по настройке Terraform для Azure с применением всех этих подходов.</span><span class="sxs-lookup"><span data-stu-id="050b2-126">The instructions that follow show you how to configure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="050b2-127">Использование Azure CLI 2.0 (для пользователей Windows, Mac и Linux)</span><span class="sxs-lookup"><span data-stu-id="050b2-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="050b2-128">После скачивания и установки [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) войдите в систему для администрирования своей подписки Azure, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="050b2-128">After you download and install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in to administer your Azure subscription by issuing the following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="050b2-129">Если вы используете облако Azure для Китая, Германии или государственных организаций, то сначала необходимо настроить Azure CLI для работы с соответствующим облаком.</span><span class="sxs-lookup"><span data-stu-id="050b2-129">If you use the China, Azure Germany, or Azure Government clouds, you need to first configure the Azure CLI to work with that cloud.</span></span> <span data-ttu-id="050b2-130">Для этого можно выполнить приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="050b2-130">You can do this by running the following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="050b2-131">Если у вас имеется несколько подписок Azure, то команда `az login` возвращает сведения о них.</span><span class="sxs-lookup"><span data-stu-id="050b2-131">If you have multiple Azure subscriptions, their details are returned by the `az login` command.</span></span> <span data-ttu-id="050b2-132">Настройте переменную среды `SUBSCRIPTION_ID`, чтобы она хранила значение возвращаемого поля `id` из подписки, которую необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="050b2-132">Set the `SUBSCRIPTION_ID` environment variable to hold the value of the returned `id` field from the subscription you want to use.</span></span> 

<span data-ttu-id="050b2-133">Укажите подписку, которую необходимо использовать для этого сеанса.</span><span class="sxs-lookup"><span data-stu-id="050b2-133">Set the subscription that you want to use for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="050b2-134">Опросите учетную запись, чтобы получить значения идентификатора подписки и идентификатора клиента.</span><span class="sxs-lookup"><span data-stu-id="050b2-134">Query the account to get the subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="050b2-135">Затем создайте отдельные учетные данные для Terraform.</span><span class="sxs-lookup"><span data-stu-id="050b2-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="050b2-136">Вы получите значения для параметров appId, password, sp_name и tenant.</span><span class="sxs-lookup"><span data-stu-id="050b2-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="050b2-137">Запишите значения параметров appId и password.</span><span class="sxs-lookup"><span data-stu-id="050b2-137">Make a note of the appId and password.</span></span>

<span data-ttu-id="050b2-138">Чтобы подтвердить свои учетные данные (субъект-службу), откройте новую оболочку и выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="050b2-138">To confirm your credentials (service principal), open a new shell and run the following commands.</span></span> <span data-ttu-id="050b2-139">Замените полученные значения для параметров sp_name, password и tenant:</span><span class="sxs-lookup"><span data-stu-id="050b2-139">Substitute the returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="050b2-140">Использование PowerShell (для пользователей Windows)</span><span class="sxs-lookup"><span data-stu-id="050b2-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="050b2-141">Если для записи и выполнения сценариев Terraform нужно использовать компьютер под управлением Windows и необходимо выполнять настройку с помощью PowerShell, настройте компьютер, используя соответствующие инструменты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="050b2-141">To use a Windows machine to write and execute your Terraform scripts and to use PowerShell for configuration tasks, configure your machine with the right PowerShell tools.</span></span> 

1. <span data-ttu-id="050b2-142">Установите инструменты PowerShell, выполнив шаги в статье [Установка и настройка Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="050b2-142">Install PowerShell tools by following the steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="050b2-143">Скачайте и выполните сценарий [azure-setup.ps1](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) из консоли PowerShell.</span><span class="sxs-lookup"><span data-stu-id="050b2-143">Download and execute the [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from the PowerShell console.</span></span>

3. <span data-ttu-id="050b2-144">Чтобы запустить сценарий azure-setup.ps1, скачайте его и выполните из консоли PowerShell команду `./azure-setup.ps1 setup`.</span><span class="sxs-lookup"><span data-stu-id="050b2-144">To run the azure-setup.ps1 script, download it and execute the `./azure-setup.ps1 setup` command from the PowerShell console.</span></span> <span data-ttu-id="050b2-145">Затем войдите в свою подписку Azure с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="050b2-145">Then sign in to your Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="050b2-146">При появлении запроса укажите имя приложения (произвольная строка, обязательно).</span><span class="sxs-lookup"><span data-stu-id="050b2-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="050b2-147">При необходимости при появлении запроса введите надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="050b2-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="050b2-148">Если не указать пароль, то надежный пароль будет создан автоматически с помощью библиотек безопасности .NET.</span><span class="sxs-lookup"><span data-stu-id="050b2-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="050b2-149">Использование Azure CLI 1.0 (для пользователей Linux или Mac)</span><span class="sxs-lookup"><span data-stu-id="050b2-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="050b2-150">Чтобы приступить к работе с Terraform на компьютерах Linux или Mac, используя Azure CLI 1.0, установите на компьютере соответствующие библиотеки.</span><span class="sxs-lookup"><span data-stu-id="050b2-150">To get started with Terraform on Linux machines or Macs with Azure CLI 1.0, install the proper libraries on your machine.</span></span>  

1. <span data-ttu-id="050b2-151">Для этого установите инструменты кроссплатформенного интерфейса командной строки Azure, выполнив действия в статье [Установка Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="050b2-151">Install Azure xPlat CLI tools by following the steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="050b2-152">Скачайте и установите процессор JSON, следуя инструкциям [здесь](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="050b2-152">Download and install a JSON processor by following the instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="050b2-153">Скачайте и выполните из консоли сценарий Bash [azure-setup.sh](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh).</span><span class="sxs-lookup"><span data-stu-id="050b2-153">Download and execute the [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from the console.</span></span>

4. <span data-ttu-id="050b2-154">Чтобы запустить сценарий azure-setup.sh, скачайте его и выполните команду `./azure-setup setup` из консоли.</span><span class="sxs-lookup"><span data-stu-id="050b2-154">To run the azure-setup.sh script, download it and execute the `./azure-setup setup` command from the console.</span></span> <span data-ttu-id="050b2-155">Затем войдите в свою подписку Azure с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="050b2-155">Then sign in to your Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="050b2-156">При появлении запроса укажите имя приложения (произвольная строка, обязательно).</span><span class="sxs-lookup"><span data-stu-id="050b2-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="050b2-157">При необходимости при появлении запроса введите надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="050b2-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="050b2-158">Если не указать пароль, то надежный пароль будет создан автоматически с помощью библиотек безопасности .NET.</span><span class="sxs-lookup"><span data-stu-id="050b2-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="050b2-159">Все приведенные выше сценарии создают приложение Azure AD и субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="050b2-159">All the previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="050b2-160">Субъект-служба получает доступ к подписке на уровне участника или владельца.</span><span class="sxs-lookup"><span data-stu-id="050b2-160">The service principal gets a contributor or owner-level access on the subscription.</span></span> <span data-ttu-id="050b2-161">Из-за высокого уровня предоставляемого доступа следует всегда защищать сведения о безопасности, которые создаются этими сценариями.</span><span class="sxs-lookup"><span data-stu-id="050b2-161">Because of the high level of access granted, you should always protect the security information generated by those scripts.</span></span> <span data-ttu-id="050b2-162">Запишите все четыре блока сведений о безопасности, предоставленные этими скриптами: appId, password, subscription_id и tenant_id.</span><span class="sxs-lookup"><span data-stu-id="050b2-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="050b2-163">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="050b2-163">Set environment variables</span></span>
<span data-ttu-id="050b2-164">После создания и настройки субъекта-службы Azure AD необходимо разрешить Terraform использовать значения кода клиента, идентификатора подписки, идентификатора клиента и секрета клиента.</span><span class="sxs-lookup"><span data-stu-id="050b2-164">After you create and configure an Azure AD service principal, you need to let Terraform know the tenant ID, subscription ID, client ID, and client secret to use.</span></span> <span data-ttu-id="050b2-165">Вы можете сделать это, вставив эти значения в сценарии Terraform, как описано в статье [Создание базовой инфраструктуры в Azure с помощью Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="050b2-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="050b2-166">Кроме того, можно задать следующие переменные среды (тем самым избежав случайной записи своих учетных данных или предоставления к ним общего доступа):</span><span class="sxs-lookup"><span data-stu-id="050b2-166">Alternately, you can set the following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="050b2-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="050b2-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="050b2-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="050b2-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="050b2-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="050b2-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="050b2-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="050b2-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="050b2-171">Вы можете использовать этот образец сценария оболочки для установки этих переменных:</span><span class="sxs-lookup"><span data-stu-id="050b2-171">You can use this sample shell script to set those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="050b2-172">Кроме того, при использовании Terraform с облаком Azure для Китая, Azure для государственных организаций или Azure для Германии необходимо правильно задать переменную среды.</span><span class="sxs-lookup"><span data-stu-id="050b2-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need to set the environment variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="050b2-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="050b2-173">Next steps</span></span>
<span data-ttu-id="050b2-174">Вы установили Terraform и настроили учетные данные Azure, так что вы можете начать развертывание инфраструктуры в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="050b2-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="050b2-175">Теперь вы можете перейти к [созданию инфраструктуры с помощью Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="050b2-175">Next, learn how to [create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
