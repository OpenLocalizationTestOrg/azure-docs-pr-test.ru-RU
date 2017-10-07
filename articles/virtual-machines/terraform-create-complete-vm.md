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
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Создание базовой инфраструктуры в Azure с помощью Terraform
В этой статье описывается hello необходимо tootake tooprovision вместе с базовой инфраструктурой виртуальной машины в Azure. Вы узнаете, как toowrite Terraform сценарии и изменение toovisualize hello прежде чем сделать их облачной инфраструктуры. Вы также узнаете, как toocreate инфраструктуры в Azure с помощью Terraform.

tooget к работе, создайте файл с именем \terraform_azure101.tf в текстовом редакторе, по выбору (Visual Studio код и Sublime/Vim и т. д.). Hello точное имя файла hello не важна, так как Terraform принимает имя папки hello в качестве параметра: все скрипты в папке hello была выполнена. Вставьте следующий код в новый файл hello hello:

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
В hello `provider` раздел hello скрипта, вы указываете Terraform toouse tooprovision Azure поставщика ресурсов в скрипте hello. значения tooget ИД_ПОДПИСКИ, appId, пароль и tenant_id, в разделе hello [установить и настроить Terraform](terraform-install-configure.md) руководства. При создании переменных среды для hello значений в этом блоке, не требуется tooinclude его. 

Hello `azurerm_resource_group` ресурсов предписывает Terraform toocreate новую группу ресурсов. Ниже приведены другие типы ресурсов, которые также доступны в Terraform.

## <a name="execute-hello-script"></a>Выполнить сценарий hello
После сохранения скрипта hello, закройте toohello консоли или командной строки и введите hello ниже:
```
terraform init
```
Поставщик Terraform tooinitialize для Azure. Затем введите hello следующее:
```
terraform plan terraformscripts
```
Мы предполагаем, что `terraformscripts` является папку hello для сохранения скрипта hello. Мы использовали hello `plan` Terraform команду, которая просматривает hello ресурсы, определенные в скриптах hello. Сравнивает их toohello сведения о состоянии сохранены по Terraform и затем выходы hello запланированного выполнения _без_ фактически создается ресурсы в Azure. 

После выполнения предыдущей команды hello, вы увидите нечто похожее на следующий экран приветствия:

![План Terraform](linux/media/terraform/tf_plan2.png)

Если все выглядит правильно, подготовьте этой новой группы ресурсов в Azure, выполнив следующие hello: 
```
terraform apply terraformscripts
```
В hello портал Azure, вы увидите hello новой пустой ресурсов группы с именем `terraformtest`. В следующем разделе hello добавьте виртуальную машину, а все hello инфраструктуру поддержки для данной группы ресурсов toohello виртуальной машины.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Подготовка виртуальной машины Ubuntu с помощью Terraform
Давайте расширение виртуальной машины, работающей Ubuntu hello Terraform сценария, который мы создали с hello сведения, необходимые tooprovision. Hello ресурсы, которые подготовки в следующих разделах hello:

* сеть с одной подсетью;
* сетевая карта; 
* учетная запись хранения с контейнером хранилища;
* общедоступный IP-адрес;
* Виртуальной машине, которая использует все ресурсы в предыдущем hello 

Тщательное документацию для каждого ресурса hello Azure Terraform см. hello [Terraform документации](https://www.terraform.io/docs/providers/azurerm/index.html).

Полная версия Hello hello [сценариев установки](#complete-terraform-script) также предоставляется для удобства.

### <a name="extend-hello-terraform-script"></a>Расширение сценария Terraform hello
Расширить hello скрипт, который был создан с hello следующие ресурсы: 
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
Hello предыдущий сценарий создает виртуальную сеть и подсети в виртуальной сети. Обратите внимание, группа ресурсов toohello ссылка hello, уже созданных через «${azurerm_resource_group.helloterraform.name}» в виртуальной сети hello и определения подсетей hello.

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
Hello предыдущего сценария фрагментов создание общедоступного IP-адреса и сетевого интерфейса, который использует hello общедоступный IP-адрес создан. Обратите внимание toosubnet_id ссылки hello и public_ip_address_id. Terraform имеет встроенный toounderstand, hello сетевой интерфейс имеет зависимость ресурсов hello, toobe необходимость создания до создания hello hello сетевого интерфейса.

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
Здесь вы создали учетную запись хранения и определили в ней контейнер хранилища. Эта учетная запись хранения — где хранить виртуальные жесткие диски (VHD) для виртуальной машины hello о toobe создан.

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
Наконец предыдущий код hello создает виртуальной машины, которая использует все ресурсы hello уже подготовлены. Это учетная запись хранения и контейнер для виртуального жесткого диска, сетевого интерфейса открытый IP-адрес и подсеть указана, так и hello группы ресурсов уже были созданы. Обратите внимание, свойство vm_size hello, где скрипт hello указывает A0 номер SKU Azure.

### <a name="execute-hello-script"></a>Выполнить сценарий hello
Сохранить полный скрипт hello выйти из toohello консоли или командной строки и введите ниже hello:
```
terraform apply terraformscripts
```
Через некоторое время hello ресурсы, включая виртуальной машины, отображаются в hello `terraformtest` группы ресурсов в hello портал Azure.

## <a name="complete-terraform-script"></a>Полный скрипт Terraform

Для удобства ниже приведен полный сценарий Terraform hello которая подготавливает все hello инфраструктуры, описанные в этой статье.

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

## <a name="next-steps"></a>Дальнейшие действия
Вы создали базовую инфраструктуру в Azure с помощью Terraform. Для более сложных сценариев, включая примеры с использованием подсистемы балансировки нагрузки и масштабируемых наборов виртуальных машин, см. многочисленные [примеры Terraform для Azure](https://github.com/hashicorp/terraform/tree/master/examples). Текущий список поддерживаемых поставщиков Azure, в разделе hello [Terraform документации](https://www.terraform.io/docs/providers/azurerm/index.html).
