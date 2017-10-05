---
title: "Создание базовой инфраструктуры в Azure с помощью Terraform | Документация Майкрософт"
description: "Узнайте, как создать ресурсы Azure с помощью Terraform"
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
ms.openlocfilehash: aa0926de32dd85f4460bbfa84b7a6007e2199d51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="bf7cb-103">Создание базовой инфраструктуры в Azure с помощью Terraform</span><span class="sxs-lookup"><span data-stu-id="bf7cb-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="bf7cb-104">В этой статье описано, какие шаги необходимо выполнить для подготовки виртуальной машины вместе с базовой инфраструктурой в Azure.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="bf7cb-105">Вы узнаете, как написать скрипты Terraform и визуализировать изменения перед их внесением в облачной инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="bf7cb-106">Вы также узнаете, как создать инфраструктуру в Azure с помощью Terraform.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="bf7cb-107">Чтобы начать работу, в любом текстовом редакторе (Visual Studio Code, Sublime, Vim или др.) создайте файл с именем \terraform_azure101.tf.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="bf7cb-108">Точное имя файла не имеет значения, так как Terraform принимает имя папки в качестве параметра — выполняются все скрипты в папке.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="bf7cb-109">Скопируйте приведенный ниже код и вставьте его в новый файл:</span><span class="sxs-lookup"><span data-stu-id="bf7cb-109">Paste the following code in the new file:</span></span>

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
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
<span data-ttu-id="bf7cb-110">В разделе `provider` скрипта вы указываете Terraform использовать поставщик Azure для подготовки ресурсов в скрипте.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="bf7cb-111">Воспользуйтесь руководством по [установке и настройке Terraform](terraform-install-configure.md), чтобы получить значения для параметров subscription_id, appId, password и tenant_id.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="bf7cb-112">Если вы создали переменные среды для значений в этом блоке, то не следует его включать.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="bf7cb-113">Ресурс `azurerm_resource_group` указывает Terraform создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="bf7cb-114">Ниже приведены другие типы ресурсов, которые также доступны в Terraform.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="bf7cb-115">Выполнение скрипта</span><span class="sxs-lookup"><span data-stu-id="bf7cb-115">Execute the script</span></span>
<span data-ttu-id="bf7cb-116">Когда скрипт сохранен, перейдите в консоль или командную строку и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bf7cb-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
 <span data-ttu-id="bf7cb-117">для инициализации поставщика Terraform для Azure.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-117">to initialize the Terraform provider for Azure.</span></span> <span data-ttu-id="bf7cb-118">Затем перейдите в каталог **terraformscripts** и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bf7cb-118">Then change the directory to **terraformscripts**, and issue the following command:</span></span>
```
terraform plan
```
<span data-ttu-id="bf7cb-119">Мы использовали команду Terraform `plan`, которая просматривает ресурсы, определенные в скрипте.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-119">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="bf7cb-120">Она сравнивает их со сведениями о состоянии, сохраненными Terraform, а затем выводит запланированное выполнение _без_ фактического создания ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-120">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="bf7cb-121">После выполнения предыдущей команды вы должны увидеть что-то вроде этого:</span><span class="sxs-lookup"><span data-stu-id="bf7cb-121">After you execute the previous command, you should see something like the following screen:</span></span>

![План Terraform](./media/terraform/tf_plan2.png)

<span data-ttu-id="bf7cb-123">Если все выглядит правильно, подготовьте эту новую группу ресурсов в Azure, выполнив следующее:</span><span class="sxs-lookup"><span data-stu-id="bf7cb-123">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply
```
<span data-ttu-id="bf7cb-124">На портале Azure вы должны увидеть новую пустую группу ресурсов с именем `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-124">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="bf7cb-125">В следующем разделе показано, как добавить виртуальную машину и всю поддерживающую инфраструктуру для этой виртуальной машины в группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-125">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="bf7cb-126">Подготовка виртуальной машины Ubuntu с помощью Terraform</span><span class="sxs-lookup"><span data-stu-id="bf7cb-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="bf7cb-127">Давайте расширим скрипт Terraform, который мы создали выше, добавив в него сведения, необходимые для подготовки виртуальной машины под управлением Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-127">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="bf7cb-128">В следующих разделах вы подготовите такие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="bf7cb-128">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="bf7cb-129">сеть с одной подсетью;</span><span class="sxs-lookup"><span data-stu-id="bf7cb-129">A network with a single subnet</span></span>
* <span data-ttu-id="bf7cb-130">сетевая карта;</span><span class="sxs-lookup"><span data-stu-id="bf7cb-130">A network interface card</span></span> 
* <span data-ttu-id="bf7cb-131">учетная запись хранения для диагностических данных виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="bf7cb-131">A storage account for the virtual machine diagnostics</span></span>
* <span data-ttu-id="bf7cb-132">общедоступный IP-адрес;</span><span class="sxs-lookup"><span data-stu-id="bf7cb-132">A public IP</span></span>
* <span data-ttu-id="bf7cb-133">виртуальная машина, использующая все перечисленные выше ресурсы.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-133">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="bf7cb-134">Подробную документацию по каждому из ресурсов Azure Terraform см. в разделе [документация Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="bf7cb-134">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="bf7cb-135">Для удобства также предоставляется полная версия [сценария подготовки](#complete-terraform-script).</span><span class="sxs-lookup"><span data-stu-id="bf7cb-135">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="bf7cb-136">Расширение скрипта Terraform</span><span class="sxs-lookup"><span data-stu-id="bf7cb-136">Extend the Terraform script</span></span>
<span data-ttu-id="bf7cb-137">Вы можете расширить ранее созданный скрипт, используя следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="bf7cb-137">Extend the script that was created with the following resources:</span></span> 
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
<span data-ttu-id="bf7cb-138">Предыдущий скрипт создает виртуальную сеть и подсеть внутри этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-138">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="bf7cb-139">Обратите внимание на ссылку на уже созданную группу ресурсов ("${azurerm_resource_group.helloterraform.name}"), которая есть в определениях виртуальной сети и подсети.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-139">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

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
<span data-ttu-id="bf7cb-140">Предыдущие фрагменты скрипта создают общедоступный IP-адрес и сетевой интерфейс, который использует созданный публичный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-140">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="bf7cb-141">Обратите внимание на ссылки на subnet_id и public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-141">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="bf7cb-142">Terraform обладает встроенной системой аналитики, позволяющей понять, что сетевой интерфейс имеет зависимость от ресурсов, которые должны быть созданы раньше него.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-142">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

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
<span data-ttu-id="bf7cb-143">Вы создали учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-143">Here, you created a storage account.</span></span> <span data-ttu-id="bf7cb-144">В этой учетной записи хранения виртуальная машина будет хранить свои сведения о диагностике.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-144">This storage account is where the virtual machine will store its diagnostics details.</span></span>

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
<span data-ttu-id="bf7cb-145">Наконец, предыдущий фрагмент создает виртуальную машину, которая использует все подготовленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-145">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="bf7cb-146">Это учетная запись хранения для диагностических данных виртуальной машины, сетевой интерфейс с указанными общедоступным IP-адресом и подсетью и группа ресурсов, которую вы уже создали.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-146">They are a storage account for the virtual machine diagnostics, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="bf7cb-147">Обратите внимание на свойство vm_size, в котором сценарий указывает номер SKU Azure Standard (DS1v2).</span><span class="sxs-lookup"><span data-stu-id="bf7cb-147">Note the vm_size property, where the script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="bf7cb-148">Необходимо предоставить открытый ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-148">You are required to supply an SSH public key.</span></span> <span data-ttu-id="bf7cb-149">Вставьте значение открытого ключа в приведенный выше раздел **... INSERT OPENSSH PUBLIC KEY HERE ...** (Вставьте сюда значение открытого ключа OpenSSH).</span><span class="sxs-lookup"><span data-stu-id="bf7cb-149">Place the public key value into the section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="bf7cb-150">Можно использовать существующую пару ключей SSH или следовать инструкциям в документации для [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) или [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys), чтобы создать пару ключей.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-150">You can use an existing ssh key pair or follow the [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation to generate the key pair.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="bf7cb-151">Выполнение скрипта</span><span class="sxs-lookup"><span data-stu-id="bf7cb-151">Execute the script</span></span>
<span data-ttu-id="bf7cb-152">Когда скрипт будет сохранен, перейдите в консоль или командную строку и введите следующее:</span><span class="sxs-lookup"><span data-stu-id="bf7cb-152">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply
```
<span data-ttu-id="bf7cb-153">Через некоторое время ресурсы, включая виртуальную машину, появятся в группе ресурсов `terraformtest` на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-153">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="bf7cb-154">Полный скрипт Terraform</span><span class="sxs-lookup"><span data-stu-id="bf7cb-154">Complete Terraform script</span></span>

<span data-ttu-id="bf7cb-155">Для удобства ниже приведен полный скрипт Terraform, который подготавливает всю инфраструктуру, рассмотренную в этой статье.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-155">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

```
# Configure the Microsoft Azure Provider
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

## <a name="next-steps"></a><span data-ttu-id="bf7cb-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf7cb-156">Next steps</span></span>
<span data-ttu-id="bf7cb-157">Вы создали базовую инфраструктуру в Azure с помощью Terraform.</span><span class="sxs-lookup"><span data-stu-id="bf7cb-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="bf7cb-158">Для более сложных сценариев, включая примеры с использованием подсистемы балансировки нагрузки и масштабируемых наборов виртуальных машин, см. многочисленные [примеры Terraform для Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="bf7cb-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="bf7cb-159">Обновленный список поддерживаемых поставщиков Azure см. в [документации Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="bf7cb-159">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
