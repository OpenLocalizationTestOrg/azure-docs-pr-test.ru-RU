---
title: "базовая инфраструктура в Azure с помощью Terraform aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate Azure ресурсов с использованием Terraform"
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
ms.openlocfilehash: 52591009ee7cb906402b8bca2ce63794ac7afcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="80fd1-103">Создание базовой инфраструктуры в Azure с помощью Terraform</span><span class="sxs-lookup"><span data-stu-id="80fd1-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="80fd1-104">В этой статье описывается hello необходимо tootake tooprovision вместе с базовой инфраструктурой виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="80fd1-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="80fd1-105">Вы узнаете, как toowrite Terraform сценарии и изменение toovisualize hello прежде чем сделать их облачной инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="80fd1-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="80fd1-106">Вы также узнаете, как toocreate инфраструктуры в Azure с помощью Terraform.</span><span class="sxs-lookup"><span data-stu-id="80fd1-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="80fd1-107">tooget к работе, создайте файл с именем \terraform_azure101.tf в текстовом редакторе, по выбору (Visual Studio код и Sublime/Vim и т. д.).</span><span class="sxs-lookup"><span data-stu-id="80fd1-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="80fd1-108">Hello точное имя файла hello не важна, так как Terraform принимает имя папки hello в качестве параметра: все скрипты в папке hello была выполнена.</span><span class="sxs-lookup"><span data-stu-id="80fd1-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="80fd1-109">Вставьте следующий код в новый файл hello hello:</span><span class="sxs-lookup"><span data-stu-id="80fd1-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="80fd1-110">В hello `provider` раздел hello скрипта, вы указываете Terraform toouse tooprovision Azure поставщика ресурсов в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="80fd1-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="80fd1-111">значения tooget ИД_ПОДПИСКИ, appId, пароль и tenant_id, в разделе hello [установить и настроить Terraform](terraform-install-configure.md) руководства.</span><span class="sxs-lookup"><span data-stu-id="80fd1-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="80fd1-112">При создании переменных среды для hello значений в этом блоке, не требуется tooinclude его.</span><span class="sxs-lookup"><span data-stu-id="80fd1-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="80fd1-113">Hello `azurerm_resource_group` ресурсов предписывает Terraform toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="80fd1-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="80fd1-114">Ниже приведены другие типы ресурсов, которые также доступны в Terraform.</span><span class="sxs-lookup"><span data-stu-id="80fd1-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="80fd1-115">Выполнить сценарий hello</span><span class="sxs-lookup"><span data-stu-id="80fd1-115">Execute hello script</span></span>
<span data-ttu-id="80fd1-116">После сохранения скрипта hello, закройте toohello консоли или командной строки и введите hello ниже:</span><span class="sxs-lookup"><span data-stu-id="80fd1-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
 <span data-ttu-id="80fd1-117">Поставщик Terraform tooinitialize hello для Azure.</span><span class="sxs-lookup"><span data-stu-id="80fd1-117">tooinitialize hello Terraform provider for Azure.</span></span> <span data-ttu-id="80fd1-118">Измените каталог hello слишком**terraformscripts**, и проблема hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="80fd1-118">Then change hello directory too**terraformscripts**, and issue hello following command:</span></span>
```
terraform plan
```
<span data-ttu-id="80fd1-119">Мы использовали hello `plan` Terraform команду, которая просматривает hello ресурсы, определенные в скриптах hello.</span><span class="sxs-lookup"><span data-stu-id="80fd1-119">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="80fd1-120">Сравнивает их toohello сведения о состоянии сохранены по Terraform и затем выходы hello запланированного выполнения _без_ фактически создается ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="80fd1-120">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="80fd1-121">После выполнения предыдущей команды hello, вы увидите нечто похожее на следующий экран приветствия:</span><span class="sxs-lookup"><span data-stu-id="80fd1-121">After you execute hello previous command, you should see something like hello following screen:</span></span>

![План Terraform](./media/terraform/tf_plan2.png)

<span data-ttu-id="80fd1-123">Если все выглядит правильно, подготовьте этой новой группы ресурсов в Azure, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="80fd1-123">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply
```
<span data-ttu-id="80fd1-124">В hello портал Azure, вы увидите hello новой пустой ресурсов группы с именем `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="80fd1-124">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="80fd1-125">В следующем разделе hello добавьте виртуальную машину, а все hello инфраструктуру поддержки для данной группы ресурсов toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="80fd1-125">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="80fd1-126">Подготовка виртуальной машины Ubuntu с помощью Terraform</span><span class="sxs-lookup"><span data-stu-id="80fd1-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="80fd1-127">Давайте расширение виртуальной машины, работающей Ubuntu hello Terraform сценария, который мы создали с hello сведения, необходимые tooprovision.</span><span class="sxs-lookup"><span data-stu-id="80fd1-127">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="80fd1-128">Hello ресурсы, которые подготовки в следующих разделах hello:</span><span class="sxs-lookup"><span data-stu-id="80fd1-128">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="80fd1-129">сеть с одной подсетью;</span><span class="sxs-lookup"><span data-stu-id="80fd1-129">A network with a single subnet</span></span>
* <span data-ttu-id="80fd1-130">сетевая карта;</span><span class="sxs-lookup"><span data-stu-id="80fd1-130">A network interface card</span></span> 
* <span data-ttu-id="80fd1-131">Учетную запись хранения диагностики hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="80fd1-131">A storage account for hello virtual machine diagnostics</span></span>
* <span data-ttu-id="80fd1-132">общедоступный IP-адрес;</span><span class="sxs-lookup"><span data-stu-id="80fd1-132">A public IP</span></span>
* <span data-ttu-id="80fd1-133">Виртуальной машине, которая использует все ресурсы в предыдущем hello</span><span class="sxs-lookup"><span data-stu-id="80fd1-133">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="80fd1-134">Тщательное документацию для каждого ресурса hello Azure Terraform см. hello [Terraform документации](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="80fd1-134">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="80fd1-135">Полная версия Hello hello [сценариев установки](#complete-terraform-script) также предоставляется для удобства.</span><span class="sxs-lookup"><span data-stu-id="80fd1-135">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="80fd1-136">Расширение сценария Terraform hello</span><span class="sxs-lookup"><span data-stu-id="80fd1-136">Extend hello Terraform script</span></span>
<span data-ttu-id="80fd1-137">Расширить hello скрипт, который был создан с hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="80fd1-137">Extend hello script that was created with hello following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="80fd1-138">Hello предыдущий сценарий создает виртуальную сеть и подсети в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="80fd1-138">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="80fd1-139">Обратите внимание, группа ресурсов toohello ссылка hello, уже созданных через «${azurerm_resource_group.helloterraform.name}» в виртуальной сети hello и определения подсетей hello.</span><span class="sxs-lookup"><span data-stu-id="80fd1-139">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="80fd1-140">Hello предыдущего сценария фрагментов создание общедоступного IP-адреса и сетевого интерфейса, который использует hello общедоступный IP-адрес создан.</span><span class="sxs-lookup"><span data-stu-id="80fd1-140">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="80fd1-141">Обратите внимание toosubnet_id ссылки hello и public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="80fd1-141">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="80fd1-142">Terraform имеет встроенный toounderstand, hello сетевой интерфейс имеет зависимость ресурсов hello, toobe необходимость создания до создания hello hello сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="80fd1-142">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="80fd1-143">Вы создали учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="80fd1-143">Here, you created a storage account.</span></span> <span data-ttu-id="80fd1-144">Эта учетная запись хранения является хранения сведений о нем диагностики hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="80fd1-144">This storage account is where hello virtual machine will store its diagnostics details.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="80fd1-145">Наконец предыдущий код hello создает виртуальной машины, которая использует все ресурсы hello уже подготовлены.</span><span class="sxs-lookup"><span data-stu-id="80fd1-145">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="80fd1-146">Они являются учетную запись хранения диагностики hello виртуальной машины, сетевой интерфейс открытый IP-адрес и подсеть указана, а hello группы ресурсов уже были созданы.</span><span class="sxs-lookup"><span data-stu-id="80fd1-146">They are a storage account for hello virtual machine diagnostics, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="80fd1-147">Обратите внимание, свойство vm_size hello, где скрипт hello указывает номер SKU Azure Standard DS1v2.</span><span class="sxs-lookup"><span data-stu-id="80fd1-147">Note hello vm_size property, where hello script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="80fd1-148">Все необходимые toosupply открытый ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="80fd1-148">You are required toosupply an SSH public key.</span></span> <span data-ttu-id="80fd1-149">Поместите hello значение открытого ключа в разделе hello **... INSERT OPENSSH PUBLIC KEY HERE ...** (Вставьте сюда значение открытого ключа OpenSSH).</span><span class="sxs-lookup"><span data-stu-id="80fd1-149">Place hello public key value into hello section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="80fd1-150">Вы можете использовать существующий ssh пару ключей или выполните hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) или [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) пары ключей hello toogenerate документации.</span><span class="sxs-lookup"><span data-stu-id="80fd1-150">You can use an existing ssh key pair or follow hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation toogenerate hello key pair.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="80fd1-151">Выполнить сценарий hello</span><span class="sxs-lookup"><span data-stu-id="80fd1-151">Execute hello script</span></span>
<span data-ttu-id="80fd1-152">Сохранить полный скрипт hello выйти из toohello консоли или командной строки и введите ниже hello:</span><span class="sxs-lookup"><span data-stu-id="80fd1-152">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply
```
<span data-ttu-id="80fd1-153">Через некоторое время hello ресурсы, включая виртуальной машины, отображаются в hello `terraformtest` группы ресурсов в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="80fd1-153">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="80fd1-154">Полный скрипт Terraform</span><span class="sxs-lookup"><span data-stu-id="80fd1-154">Complete Terraform script</span></span>

<span data-ttu-id="80fd1-155">Для удобства ниже приведен полный сценарий Terraform hello которая подготавливает все hello инфраструктуры, описанные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="80fd1-155">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
# Configure hello Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}

# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }

    tags {
        environment = "Terraform Demo"
    }
}

# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="80fd1-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80fd1-156">Next steps</span></span>
<span data-ttu-id="80fd1-157">Вы создали базовую инфраструктуру в Azure с помощью Terraform.</span><span class="sxs-lookup"><span data-stu-id="80fd1-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="80fd1-158">Для более сложных сценариев, включая примеры с использованием подсистемы балансировки нагрузки и масштабируемых наборов виртуальных машин, см. многочисленные [примеры Terraform для Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="80fd1-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="80fd1-159">Текущий список поддерживаемых поставщиков Azure, в разделе hello [Terraform документации](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="80fd1-159">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
