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
ms.openlocfilehash: 916a838c118f28b3fbd373188e0acb2afc655081
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="e091a-103">Создание базовой инфраструктуры в Azure с помощью Terraform</span><span class="sxs-lookup"><span data-stu-id="e091a-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="e091a-104">В этой статье описывается hello необходимо tootake tooprovision вместе с базовой инфраструктурой виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="e091a-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="e091a-105">Вы узнаете, как toowrite Terraform сценарии и изменение toovisualize hello прежде чем сделать их облачной инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="e091a-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="e091a-106">Вы также узнаете, как toocreate инфраструктуры в Azure с помощью Terraform.</span><span class="sxs-lookup"><span data-stu-id="e091a-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="e091a-107">tooget к работе, создайте файл с именем \terraform_azure101.tf в текстовом редакторе, по выбору (Visual Studio код и Sublime/Vim и т. д.).</span><span class="sxs-lookup"><span data-stu-id="e091a-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="e091a-108">Hello точное имя файла hello не важна, так как Terraform принимает имя папки hello в качестве параметра: все скрипты в папке hello была выполнена.</span><span class="sxs-lookup"><span data-stu-id="e091a-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="e091a-109">Вставьте следующий код в новый файл hello hello:</span><span class="sxs-lookup"><span data-stu-id="e091a-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
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
<span data-ttu-id="e091a-110">В hello `provider` раздел hello скрипта, вы указываете Terraform toouse tooprovision Azure поставщика ресурсов в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="e091a-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="e091a-111">значения tooget ИД_ПОДПИСКИ, appId, пароль и tenant_id, в разделе hello [установить и настроить Terraform](terraform-install-configure.md) руководства.</span><span class="sxs-lookup"><span data-stu-id="e091a-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="e091a-112">При создании переменных среды для hello значений в этом блоке, не требуется tooinclude его.</span><span class="sxs-lookup"><span data-stu-id="e091a-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="e091a-113">Hello `azurerm_resource_group` ресурсов предписывает Terraform toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e091a-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="e091a-114">Ниже приведены другие типы ресурсов, которые также доступны в Terraform.</span><span class="sxs-lookup"><span data-stu-id="e091a-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="e091a-115">Выполнить сценарий hello</span><span class="sxs-lookup"><span data-stu-id="e091a-115">Execute hello script</span></span>
<span data-ttu-id="e091a-116">После сохранения скрипта hello, закройте toohello консоли или командной строки и введите hello ниже:</span><span class="sxs-lookup"><span data-stu-id="e091a-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
<span data-ttu-id="e091a-117">Поставщик Terraform tooinitialize для Azure.</span><span class="sxs-lookup"><span data-stu-id="e091a-117">tooinitialize Terraform provider for Azure.</span></span> <span data-ttu-id="e091a-118">Затем введите hello следующее:</span><span class="sxs-lookup"><span data-stu-id="e091a-118">Then type hello following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="e091a-119">Мы предполагаем, что `terraformscripts` является папку hello для сохранения скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="e091a-119">We assume that `terraformscripts` is hello folder where hello script was saved.</span></span> <span data-ttu-id="e091a-120">Мы использовали hello `plan` Terraform команду, которая просматривает hello ресурсы, определенные в скриптах hello.</span><span class="sxs-lookup"><span data-stu-id="e091a-120">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="e091a-121">Сравнивает их toohello сведения о состоянии сохранены по Terraform и затем выходы hello запланированного выполнения _без_ фактически создается ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="e091a-121">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="e091a-122">После выполнения предыдущей команды hello, вы увидите нечто похожее на следующий экран приветствия:</span><span class="sxs-lookup"><span data-stu-id="e091a-122">After you execute hello previous command, you should see something like hello following screen:</span></span>

![План Terraform](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="e091a-124">Если все выглядит правильно, подготовьте этой новой группы ресурсов в Azure, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="e091a-124">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="e091a-125">В hello портал Azure, вы увидите hello новой пустой ресурсов группы с именем `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="e091a-125">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="e091a-126">В следующем разделе hello добавьте виртуальную машину, а все hello инфраструктуру поддержки для данной группы ресурсов toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e091a-126">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="e091a-127">Подготовка виртуальной машины Ubuntu с помощью Terraform</span><span class="sxs-lookup"><span data-stu-id="e091a-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="e091a-128">Давайте расширение виртуальной машины, работающей Ubuntu hello Terraform сценария, который мы создали с hello сведения, необходимые tooprovision.</span><span class="sxs-lookup"><span data-stu-id="e091a-128">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="e091a-129">Hello ресурсы, которые подготовки в следующих разделах hello:</span><span class="sxs-lookup"><span data-stu-id="e091a-129">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="e091a-130">сеть с одной подсетью;</span><span class="sxs-lookup"><span data-stu-id="e091a-130">A network with a single subnet</span></span>
* <span data-ttu-id="e091a-131">сетевая карта;</span><span class="sxs-lookup"><span data-stu-id="e091a-131">A network interface card</span></span> 
* <span data-ttu-id="e091a-132">учетная запись хранения с контейнером хранилища;</span><span class="sxs-lookup"><span data-stu-id="e091a-132">A storage account with a storage container</span></span>
* <span data-ttu-id="e091a-133">общедоступный IP-адрес;</span><span class="sxs-lookup"><span data-stu-id="e091a-133">A public IP</span></span>
* <span data-ttu-id="e091a-134">Виртуальной машине, которая использует все ресурсы в предыдущем hello</span><span class="sxs-lookup"><span data-stu-id="e091a-134">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="e091a-135">Тщательное документацию для каждого ресурса hello Azure Terraform см. hello [Terraform документации](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="e091a-135">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="e091a-136">Полная версия Hello hello [сценариев установки](#complete-terraform-script) также предоставляется для удобства.</span><span class="sxs-lookup"><span data-stu-id="e091a-136">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="e091a-137">Расширение сценария Terraform hello</span><span class="sxs-lookup"><span data-stu-id="e091a-137">Extend hello Terraform script</span></span>
<span data-ttu-id="e091a-138">Расширить hello скрипт, который был создан с hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="e091a-138">Extend hello script that was created with hello following resources:</span></span> 
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
<span data-ttu-id="e091a-139">Hello предыдущий сценарий создает виртуальную сеть и подсети в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e091a-139">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="e091a-140">Обратите внимание, группа ресурсов toohello ссылка hello, уже созданных через «${azurerm_resource_group.helloterraform.name}» в виртуальной сети hello и определения подсетей hello.</span><span class="sxs-lookup"><span data-stu-id="e091a-140">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

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
<span data-ttu-id="e091a-141">Hello предыдущего сценария фрагментов создание общедоступного IP-адреса и сетевого интерфейса, который использует hello общедоступный IP-адрес создан.</span><span class="sxs-lookup"><span data-stu-id="e091a-141">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="e091a-142">Обратите внимание toosubnet_id ссылки hello и public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="e091a-142">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="e091a-143">Terraform имеет встроенный toounderstand, hello сетевой интерфейс имеет зависимость ресурсов hello, toobe необходимость создания до создания hello hello сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e091a-143">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

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
<span data-ttu-id="e091a-144">Здесь вы создали учетную запись хранения и определили в ней контейнер хранилища.</span><span class="sxs-lookup"><span data-stu-id="e091a-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="e091a-145">Эта учетная запись хранения — где хранить виртуальные жесткие диски (VHD) для виртуальной машины hello о toobe создан.</span><span class="sxs-lookup"><span data-stu-id="e091a-145">This storage account is where you store virtual hard disks (VHDs) for hello virtual machine about toobe created.</span></span>

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
<span data-ttu-id="e091a-146">Наконец предыдущий код hello создает виртуальной машины, которая использует все ресурсы hello уже подготовлены.</span><span class="sxs-lookup"><span data-stu-id="e091a-146">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="e091a-147">Это учетная запись хранения и контейнер для виртуального жесткого диска, сетевого интерфейса открытый IP-адрес и подсеть указана, так и hello группы ресурсов уже были созданы.</span><span class="sxs-lookup"><span data-stu-id="e091a-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="e091a-148">Обратите внимание, свойство vm_size hello, где скрипт hello указывает A0 номер SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="e091a-148">Note hello vm_size property, where hello script specifies an Azure A0 SKU.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="e091a-149">Выполнить сценарий hello</span><span class="sxs-lookup"><span data-stu-id="e091a-149">Execute hello script</span></span>
<span data-ttu-id="e091a-150">Сохранить полный скрипт hello выйти из toohello консоли или командной строки и введите ниже hello:</span><span class="sxs-lookup"><span data-stu-id="e091a-150">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="e091a-151">Через некоторое время hello ресурсы, включая виртуальной машины, отображаются в hello `terraformtest` группы ресурсов в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e091a-151">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="e091a-152">Полный скрипт Terraform</span><span class="sxs-lookup"><span data-stu-id="e091a-152">Complete Terraform script</span></span>

<span data-ttu-id="e091a-153">Для удобства ниже приведен полный сценарий Terraform hello которая подготавливает все hello инфраструктуры, описанные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="e091a-153">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

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

## <a name="next-steps"></a><span data-ttu-id="e091a-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e091a-154">Next steps</span></span>
<span data-ttu-id="e091a-155">Вы создали базовую инфраструктуру в Azure с помощью Terraform.</span><span class="sxs-lookup"><span data-stu-id="e091a-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="e091a-156">Для более сложных сценариев, включая примеры с использованием подсистемы балансировки нагрузки и масштабируемых наборов виртуальных машин, см. многочисленные [примеры Terraform для Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="e091a-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="e091a-157">Текущий список поддерживаемых поставщиков Azure, в разделе hello [Terraform документации](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="e091a-157">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
