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
ms.openlocfilehash: 9660a95b440c2e4311829979e270d9f10099f624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="be4ad-103">Создание базовой инфраструктуры в Azure с помощью Terraform</span><span class="sxs-lookup"><span data-stu-id="be4ad-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="be4ad-104">В этой статье описано, какие шаги необходимо выполнить для подготовки виртуальной машины вместе с базовой инфраструктурой в Azure.</span><span class="sxs-lookup"><span data-stu-id="be4ad-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="be4ad-105">Вы узнаете, как написать скрипты Terraform и визуализировать изменения перед их внесением в облачной инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="be4ad-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="be4ad-106">Вы также узнаете, как создать инфраструктуру в Azure с помощью Terraform.</span><span class="sxs-lookup"><span data-stu-id="be4ad-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="be4ad-107">Чтобы начать работу, в любом текстовом редакторе (Visual Studio Code, Sublime, Vim или др.) создайте файл с именем \terraform_azure101.tf.</span><span class="sxs-lookup"><span data-stu-id="be4ad-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="be4ad-108">Точное имя файла не имеет значения, так как Terraform принимает имя папки в качестве параметра — выполняются все скрипты в папке.</span><span class="sxs-lookup"><span data-stu-id="be4ad-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="be4ad-109">Скопируйте приведенный ниже код и вставьте его в новый файл:</span><span class="sxs-lookup"><span data-stu-id="be4ad-109">Paste the following code in the new file:</span></span>

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group 
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="be4ad-110">В разделе `provider` скрипта вы указываете Terraform использовать поставщик Azure для подготовки ресурсов в скрипте.</span><span class="sxs-lookup"><span data-stu-id="be4ad-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="be4ad-111">Воспользуйтесь руководством по [установке и настройке Terraform](terraform-install-configure.md), чтобы получить значения для параметров subscription_id, appId, password и tenant_id.</span><span class="sxs-lookup"><span data-stu-id="be4ad-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="be4ad-112">Если вы создали переменные среды для значений в этом блоке, то не следует его включать.</span><span class="sxs-lookup"><span data-stu-id="be4ad-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="be4ad-113">Ресурс `azurerm_resource_group` указывает Terraform создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="be4ad-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="be4ad-114">Ниже приведены другие типы ресурсов, которые также доступны в Terraform.</span><span class="sxs-lookup"><span data-stu-id="be4ad-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="be4ad-115">Выполнение скрипта</span><span class="sxs-lookup"><span data-stu-id="be4ad-115">Execute the script</span></span>
<span data-ttu-id="be4ad-116">Когда скрипт сохранен, перейдите в консоль или командную строку и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="be4ad-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
<span data-ttu-id="be4ad-117">для инициализации поставщика Terraform для Azure.</span><span class="sxs-lookup"><span data-stu-id="be4ad-117">to initialize Terraform provider for Azure.</span></span> <span data-ttu-id="be4ad-118">Затем введите следующее:</span><span class="sxs-lookup"><span data-stu-id="be4ad-118">Then type the following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="be4ad-119">В приведенной выше команде предполагается, что `terraformscripts` — это папка, в которую был сохранен скрипт.</span><span class="sxs-lookup"><span data-stu-id="be4ad-119">We assume that `terraformscripts` is the folder where the script was saved.</span></span> <span data-ttu-id="be4ad-120">Мы использовали команду Terraform `plan`, которая просматривает ресурсы, определенные в скрипте.</span><span class="sxs-lookup"><span data-stu-id="be4ad-120">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="be4ad-121">Она сравнивает их со сведениями о состоянии, сохраненными Terraform, а затем выводит запланированное выполнение _без_ фактического создания ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="be4ad-121">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="be4ad-122">После выполнения предыдущей команды вы должны увидеть что-то вроде этого:</span><span class="sxs-lookup"><span data-stu-id="be4ad-122">After you execute the previous command, you should see something like the following screen:</span></span>

![План Terraform](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="be4ad-124">Если все выглядит правильно, подготовьте эту новую группу ресурсов в Azure, выполнив следующее:</span><span class="sxs-lookup"><span data-stu-id="be4ad-124">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="be4ad-125">На портале Azure вы должны увидеть новую пустую группу ресурсов с именем `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="be4ad-125">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="be4ad-126">В следующем разделе показано, как добавить виртуальную машину и всю поддерживающую инфраструктуру для этой виртуальной машины в группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="be4ad-126">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="be4ad-127">Подготовка виртуальной машины Ubuntu с помощью Terraform</span><span class="sxs-lookup"><span data-stu-id="be4ad-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="be4ad-128">Давайте расширим скрипт Terraform, который мы создали выше, добавив в него сведения, необходимые для подготовки виртуальной машины под управлением Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="be4ad-128">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="be4ad-129">В следующих разделах вы подготовите такие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="be4ad-129">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="be4ad-130">сеть с одной подсетью;</span><span class="sxs-lookup"><span data-stu-id="be4ad-130">A network with a single subnet</span></span>
* <span data-ttu-id="be4ad-131">сетевая карта;</span><span class="sxs-lookup"><span data-stu-id="be4ad-131">A network interface card</span></span> 
* <span data-ttu-id="be4ad-132">учетная запись хранения с контейнером хранилища;</span><span class="sxs-lookup"><span data-stu-id="be4ad-132">A storage account with a storage container</span></span>
* <span data-ttu-id="be4ad-133">общедоступный IP-адрес;</span><span class="sxs-lookup"><span data-stu-id="be4ad-133">A public IP</span></span>
* <span data-ttu-id="be4ad-134">виртуальная машина, использующая все перечисленные выше ресурсы.</span><span class="sxs-lookup"><span data-stu-id="be4ad-134">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="be4ad-135">Подробную документацию по каждому из ресурсов Azure Terraform см. в разделе [документация Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="be4ad-135">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="be4ad-136">Для удобства также предоставляется полная версия [сценария подготовки](#complete-terraform-script).</span><span class="sxs-lookup"><span data-stu-id="be4ad-136">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="be4ad-137">Расширение скрипта Terraform</span><span class="sxs-lookup"><span data-stu-id="be4ad-137">Extend the Terraform script</span></span>
<span data-ttu-id="be4ad-138">Вы можете расширить ранее созданный скрипт, используя следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="be4ad-138">Extend the script that was created with the following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="be4ad-139">Предыдущий скрипт создает виртуальную сеть и подсеть внутри этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="be4ad-139">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="be4ad-140">Обратите внимание на ссылку на уже созданную группу ресурсов ("${azurerm_resource_group.helloterraform.name}"), которая есть в определениях виртуальной сети и подсети.</span><span class="sxs-lookup"><span data-stu-id="be4ad-140">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
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
}
~~~~
<span data-ttu-id="be4ad-141">Предыдущие фрагменты скрипта создают общедоступный IP-адрес и сетевой интерфейс, который использует созданный публичный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="be4ad-141">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="be4ad-142">Обратите внимание на ссылки на subnet_id и public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="be4ad-142">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="be4ad-143">Terraform обладает встроенной системой аналитики, позволяющей понять, что сетевой интерфейс имеет зависимость от ресурсов, которые должны быть созданы раньше него.</span><span class="sxs-lookup"><span data-stu-id="be4ad-143">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}
~~~~
<span data-ttu-id="be4ad-144">Здесь вы создали учетную запись хранения и определили в ней контейнер хранилища.</span><span class="sxs-lookup"><span data-stu-id="be4ad-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="be4ad-145">В этой учетной записи хранения хранятся виртуальные жесткие диски (VHD) для создаваемой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="be4ad-145">This storage account is where you store virtual hard disks (VHDs) for the virtual machine about to be created.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
~~~~
<span data-ttu-id="be4ad-146">Наконец, предыдущий фрагмент создает виртуальную машину, которая использует все подготовленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="be4ad-146">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="be4ad-147">Это учетная запись хранения и контейнер для VHD, сетевой интерфейс с указанным общедоступным IP-адресом и подсетью и группа ресурсов, которую вы уже создали.</span><span class="sxs-lookup"><span data-stu-id="be4ad-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="be4ad-148">Обратите внимание на свойство vm_size, в котором сценарий указывает номер SKU Azure (A0).</span><span class="sxs-lookup"><span data-stu-id="be4ad-148">Note the vm_size property, where the script specifies an Azure A0 SKU.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="be4ad-149">Выполнение скрипта</span><span class="sxs-lookup"><span data-stu-id="be4ad-149">Execute the script</span></span>
<span data-ttu-id="be4ad-150">Когда скрипт будет сохранен, перейдите в консоль или командную строку и введите следующее:</span><span class="sxs-lookup"><span data-stu-id="be4ad-150">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="be4ad-151">Через некоторое время ресурсы, включая виртуальную машину, появятся в группе ресурсов `terraformtest` на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="be4ad-151">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="be4ad-152">Полный скрипт Terraform</span><span class="sxs-lookup"><span data-stu-id="be4ad-152">Complete Terraform script</span></span>

<span data-ttu-id="be4ad-153">Для удобства ниже приведен полный скрипт Terraform, который подготавливает всю инфраструктуру, рассмотренную в этой статье.</span><span class="sxs-lookup"><span data-stu-id="be4ad-153">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

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

# create virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "tfvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "tfsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}


# create public IPs
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
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
}

# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="be4ad-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be4ad-154">Next steps</span></span>
<span data-ttu-id="be4ad-155">Вы создали базовую инфраструктуру в Azure с помощью Terraform.</span><span class="sxs-lookup"><span data-stu-id="be4ad-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="be4ad-156">Для более сложных сценариев, включая примеры с использованием подсистемы балансировки нагрузки и масштабируемых наборов виртуальных машин, см. многочисленные [примеры Terraform для Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="be4ad-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="be4ad-157">Обновленный список поддерживаемых поставщиков Azure см. в [документации Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="be4ad-157">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
