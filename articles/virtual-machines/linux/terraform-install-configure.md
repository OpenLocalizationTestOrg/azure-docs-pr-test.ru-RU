---
title: "aaaInstall и настройки виртуальных машин tooprovision Terraform и другой инфраструктурой в Azure | Документы Microsoft"
description: "Узнайте, как tooinstall и настройте Terraform toocreate Azure ресурсы"
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
ms.openlocfilehash: b6706f53b21347442def05a592c30a2d22718984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="66cb1-103">Установка и настройка виртуальных машин tooprovision Terraform и другой инфраструктурой в Azure</span><span class="sxs-lookup"><span data-stu-id="66cb1-103">Install and configure Terraform tooprovision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="66cb1-104">В этой статье описываются необходимые шаги tooinstall hello и настройки Terraform tooprovision ресурсов, таких как виртуальные машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="66cb1-104">This article describes hello necessary steps tooinstall and configure Terraform tooprovision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="66cb1-105">Вы узнаете, как toocreate и использование Azure учетные данные tooenable Terraform tooprovision облачные ресурсы в безопасном режиме.</span><span class="sxs-lookup"><span data-stu-id="66cb1-105">You will learn how toocreate and use Azure credentials tooenable Terraform tooprovision cloud resources in a secure manner.</span></span>

<span data-ttu-id="66cb1-106">HashiCorp Terraform предоставляет простой способ toodefine и развертывание облачной инфраструктуры с помощью языка настраиваемых шаблонов, называемый языком конфигурации HashiCorp (HCL).</span><span class="sxs-lookup"><span data-stu-id="66cb1-106">HashiCorp Terraform provides an easy way toodefine and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="66cb1-107">Этот пользовательский язык [toowrite легко и просто toounderstand](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="66cb1-107">This custom language is [easy toowrite and easy toounderstand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="66cb1-108">Кроме того, с помощью hello `terraform plan` команды, прежде чем зафиксировать их можно визуализировать hello изменения tooyour инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="66cb1-108">Additionally, by using hello `terraform plan` command, you can visualize hello changes tooyour infrastructure before you commit them.</span></span> <span data-ttu-id="66cb1-109">Выполните эти шаги toostart, с помощью Terraform с Azure.</span><span class="sxs-lookup"><span data-stu-id="66cb1-109">Follow these steps toostart using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="66cb1-110">Установка Terraform</span><span class="sxs-lookup"><span data-stu-id="66cb1-110">Install Terraform</span></span>
<span data-ttu-id="66cb1-111">tooinstall Terraform, [загрузки](https://www.terraform.io/downloads.html) для вашей операционной системы в каталог установки отдельный пакет hello.</span><span class="sxs-lookup"><span data-stu-id="66cb1-111">tooinstall Terraform, [download](https://www.terraform.io/downloads.html) hello package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="66cb1-112">Hello загружаемый файл содержит один исполняемый файл, для которого следует задавать глобальный путь.</span><span class="sxs-lookup"><span data-stu-id="66cb1-112">hello download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="66cb1-113">Для инструкции о том, как tooset hello путь в Linux и Mac, посетите страницу слишком[веб-страницу](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="66cb1-113">For instructions on how tooset hello path on Linux and Mac, go too[this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="66cb1-114">Для инструкции как tooset hello пути в Windows, посетите страницу слишком[веб-страницу](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="66cb1-114">For instructions on how tooset hello path on Windows, go too[this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="66cb1-115">tooverify установку, запустите hello `terraform` команды.</span><span class="sxs-lookup"><span data-stu-id="66cb1-115">tooverify your installation, run hello `terraform` command.</span></span> <span data-ttu-id="66cb1-116">В качестве выходных данных должен отобразиться список доступных параметров Terraform.</span><span class="sxs-lookup"><span data-stu-id="66cb1-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="66cb1-117">Далее необходимо tooallow Terraform доступа tooyour подписки Azure tooperform подготовку инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="66cb1-117">Next, you need tooallow Terraform access tooyour Azure subscription tooperform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-tooazure"></a><span data-ttu-id="66cb1-118">Настройка доступа tooAzure Terraform</span><span class="sxs-lookup"><span data-stu-id="66cb1-118">Set up Terraform access tooAzure</span></span>
<span data-ttu-id="66cb1-119">tooenable Terraform tooprovision ресурсы в Azure, необходимо toocreate две сущности в Azure Active Directory (Azure AD): приложения Azure AD и субъект-служба Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66cb1-119">tooenable Terraform tooprovision resources into Azure, you need toocreate two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="66cb1-120">Затем идентификаторы этих сущностей используются в сценариях Terraform.</span><span class="sxs-lookup"><span data-stu-id="66cb1-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="66cb1-121">Субъект-служба — это локальный экземпляр глобального приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66cb1-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="66cb1-122">Субъекта-службы позволяет ресурсы tooglobal управления детальные локального доступа.</span><span class="sxs-lookup"><span data-stu-id="66cb1-122">A service principal allows granular local access control tooglobal resources.</span></span>

<span data-ttu-id="66cb1-123">Существует несколько способов toocreate приложения Azure AD и субъект-служба Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66cb1-123">There are several ways toocreate an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="66cb1-124">Hello простым и быстрым способом сегодняшний день является toouse Azure CLI 2.0, который [можно загрузить и установить на Windows, Linux или Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="66cb1-124">hello easiest and fastest way today is toouse Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="66cb1-125">Также можно использовать PowerShell или Azure CLI 1.0 toocreate hello инфраструктуры безопасности.</span><span class="sxs-lookup"><span data-stu-id="66cb1-125">You also can use PowerShell or Azure CLI 1.0 toocreate hello necessary security infrastructure.</span></span> <span data-ttu-id="66cb1-126">следующие инструкции Hello показывается, как tooconfigure Terraform для Azure с помощью всех этих подходов.</span><span class="sxs-lookup"><span data-stu-id="66cb1-126">hello instructions that follow show you how tooconfigure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="66cb1-127">Использование Azure CLI 2.0 (для пользователей Windows, Mac и Linux)</span><span class="sxs-lookup"><span data-stu-id="66cb1-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="66cb1-128">После загрузки и установки hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), войдите в tooadminister подписки Azure, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="66cb1-128">After you download and install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in tooadminister your Azure subscription by issuing hello following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="66cb1-129">При использовании hello Китай, Германия Azure или облаков Azure для государственных, необходимо toofirst Настройка toowork hello Azure CLI с помощью данного облака.</span><span class="sxs-lookup"><span data-stu-id="66cb1-129">If you use hello China, Azure Germany, or Azure Government clouds, you need toofirst configure hello Azure CLI toowork with that cloud.</span></span> <span data-ttu-id="66cb1-130">Это можно сделать, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="66cb1-130">You can do this by running hello following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="66cb1-131">Если у вас несколько подписок Azure, подробные сведения об их возвращаемые hello `az login` команды.</span><span class="sxs-lookup"><span data-stu-id="66cb1-131">If you have multiple Azure subscriptions, their details are returned by hello `az login` command.</span></span> <span data-ttu-id="66cb1-132">Набор hello `SUBSCRIPTION_ID` возвращено значение hello toohold переменной среды hello `id` из подписки hello требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="66cb1-132">Set hello `SUBSCRIPTION_ID` environment variable toohold hello value of hello returned `id` field from hello subscription you want toouse.</span></span> 

<span data-ttu-id="66cb1-133">Задать hello подписки требуется toouse для этого сеанса.</span><span class="sxs-lookup"><span data-stu-id="66cb1-133">Set hello subscription that you want toouse for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="66cb1-134">Запрос учетной записи tooget hello hello-идентификатор подписки и значения идентификатора клиента.</span><span class="sxs-lookup"><span data-stu-id="66cb1-134">Query hello account tooget hello subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="66cb1-135">Затем создайте отдельные учетные данные для Terraform.</span><span class="sxs-lookup"><span data-stu-id="66cb1-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="66cb1-136">Вы получите значения для параметров appId, password, sp_name и tenant.</span><span class="sxs-lookup"><span data-stu-id="66cb1-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="66cb1-137">Запишите hello appId и пароль.</span><span class="sxs-lookup"><span data-stu-id="66cb1-137">Make a note of hello appId and password.</span></span>

<span data-ttu-id="66cb1-138">tooconfirm учетные данные (субъекта-службы), откройте новой оболочки и выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="66cb1-138">tooconfirm your credentials (service principal), open a new shell and run hello following commands.</span></span> <span data-ttu-id="66cb1-139">Замена hello возвращаемые значения для sp_name и пароль клиента:</span><span class="sxs-lookup"><span data-stu-id="66cb1-139">Substitute hello returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="66cb1-140">Использование PowerShell (для пользователей Windows)</span><span class="sxs-lookup"><span data-stu-id="66cb1-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="66cb1-141">toouse Windows toowrite компьютер и выполнить вашей Terraform сценарии и toouse PowerShell для задач настройки настройки компьютера с помощью соответствующих средств PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="66cb1-141">toouse a Windows machine toowrite and execute your Terraform scripts and toouse PowerShell for configuration tasks, configure your machine with hello right PowerShell tools.</span></span> 

1. <span data-ttu-id="66cb1-142">Установка инструментов PowerShell с помощью инструкции hello в [Установка и настройка Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="66cb1-142">Install PowerShell tools by following hello steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="66cb1-143">Загрузка и выполнение hello [azure setup.ps1 скрипт](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) из консоли PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="66cb1-143">Download and execute hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from hello PowerShell console.</span></span>

3. <span data-ttu-id="66cb1-144">скрипт azure setup.ps1 toorun hello, загрузите и выполните hello `./azure-setup.ps1 setup` команду из консоли PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="66cb1-144">toorun hello azure-setup.ps1 script, download it and execute hello `./azure-setup.ps1 setup` command from hello PowerShell console.</span></span> <span data-ttu-id="66cb1-145">Затем войдите в tooyour подписки Azure с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="66cb1-145">Then sign in tooyour Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="66cb1-146">При появлении запроса укажите имя приложения (произвольная строка, обязательно).</span><span class="sxs-lookup"><span data-stu-id="66cb1-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="66cb1-147">При необходимости при появлении запроса введите надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="66cb1-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="66cb1-148">Если не указать пароль, то надежный пароль будет создан автоматически с помощью библиотек безопасности .NET.</span><span class="sxs-lookup"><span data-stu-id="66cb1-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="66cb1-149">Использование Azure CLI 1.0 (для пользователей Linux или Mac)</span><span class="sxs-lookup"><span data-stu-id="66cb1-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="66cb1-150">tooget работу с Terraform на компьютеры Linux и компьютерах Mac с помощью Azure CLI 1.0, соответствующие библиотеки hello установки на компьютере.</span><span class="sxs-lookup"><span data-stu-id="66cb1-150">tooget started with Terraform on Linux machines or Macs with Azure CLI 1.0, install hello proper libraries on your machine.</span></span>  

1. <span data-ttu-id="66cb1-151">Установка средств Azure xPlat CLI, следуя указаниям hello [установить CLI Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="66cb1-151">Install Azure xPlat CLI tools by following hello steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="66cb1-152">Загрузите и установите процессор JSON, следуя инструкциям hello [загрузки jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="66cb1-152">Download and install a JSON processor by following hello instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="66cb1-153">Загрузка и выполнение hello [azure setup.sh скрипт](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash скрипт из консоли hello.</span><span class="sxs-lookup"><span data-stu-id="66cb1-153">Download and execute hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from hello console.</span></span>

4. <span data-ttu-id="66cb1-154">скрипт azure setup.sh toorun hello, загрузите и выполните hello `./azure-setup setup` команду из консоли hello.</span><span class="sxs-lookup"><span data-stu-id="66cb1-154">toorun hello azure-setup.sh script, download it and execute hello `./azure-setup setup` command from hello console.</span></span> <span data-ttu-id="66cb1-155">Затем войдите в tooyour подписки Azure с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="66cb1-155">Then sign in tooyour Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="66cb1-156">При появлении запроса укажите имя приложения (произвольная строка, обязательно).</span><span class="sxs-lookup"><span data-stu-id="66cb1-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="66cb1-157">При необходимости при появлении запроса введите надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="66cb1-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="66cb1-158">Если не указать пароль, то надежный пароль будет создан автоматически с помощью библиотек безопасности .NET.</span><span class="sxs-lookup"><span data-stu-id="66cb1-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="66cb1-159">Все предыдущие сценарии hello создание основного приложения Azure AD и службы.</span><span class="sxs-lookup"><span data-stu-id="66cb1-159">All hello previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="66cb1-160">Участник службы Hello возвращает участника или доступ на уровне владельца на hello подписки.</span><span class="sxs-lookup"><span data-stu-id="66cb1-160">hello service principal gets a contributor or owner-level access on hello subscription.</span></span> <span data-ttu-id="66cb1-161">Из-за hello высокий уровень предоставлен доступ следует всегда защищать hello безопасности информации, создаваемой эти скрипты.</span><span class="sxs-lookup"><span data-stu-id="66cb1-161">Because of hello high level of access granted, you should always protect hello security information generated by those scripts.</span></span> <span data-ttu-id="66cb1-162">Запишите все четыре блока сведений о безопасности, предоставленные этими скриптами: appId, password, subscription_id и tenant_id.</span><span class="sxs-lookup"><span data-stu-id="66cb1-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="66cb1-163">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="66cb1-163">Set environment variables</span></span>
<span data-ttu-id="66cb1-164">После создания и настройки участника-службы Azure AD, необходимо toolet Terraform знать hello ИД клиента, идентификатор подписки, идентификатор клиента и секрета toouse клиента.</span><span class="sxs-lookup"><span data-stu-id="66cb1-164">After you create and configure an Azure AD service principal, you need toolet Terraform know hello tenant ID, subscription ID, client ID, and client secret toouse.</span></span> <span data-ttu-id="66cb1-165">Вы можете сделать это, вставив эти значения в сценарии Terraform, как описано в статье [Создание базовой инфраструктуры в Azure с помощью Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="66cb1-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="66cb1-166">Кроме того можно задать следующие переменные среды hello (и тем самым избежать случайно извлечение или учетные данные для управления доступом):</span><span class="sxs-lookup"><span data-stu-id="66cb1-166">Alternately, you can set hello following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="66cb1-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="66cb1-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="66cb1-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="66cb1-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="66cb1-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="66cb1-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="66cb1-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="66cb1-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="66cb1-171">Эти переменные могут использоваться tooset сценарий оболочки этот образец.</span><span class="sxs-lookup"><span data-stu-id="66cb1-171">You can use this sample shell script tooset those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="66cb1-172">Кроме того при использовании Terraform с Azure в Китае, или либо Azure для государственных или Германии Azure необходимо переменной СРЕДЫ tooset hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="66cb1-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need tooset hello ENVIRONMENT variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66cb1-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66cb1-173">Next steps</span></span>
<span data-ttu-id="66cb1-174">Вы установили Terraform и настроили учетные данные Azure, так что вы можете начать развертывание инфраструктуры в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="66cb1-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="66cb1-175">Далее, узнайте, как слишком[создания инфраструктуры с Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="66cb1-175">Next, learn how too[create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
