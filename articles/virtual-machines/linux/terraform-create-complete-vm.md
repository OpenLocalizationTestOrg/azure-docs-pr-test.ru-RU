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

# create a resource group if it doesn't exist
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
 Поставщик Terraform tooinitialize hello для Azure. Измените каталог hello слишком**terraformscripts**, и проблема hello следующую команду:
```
terraform plan
```
Мы использовали hello `plan` Terraform команду, которая просматривает hello ресурсы, определенные в скриптах hello. Сравнивает их toohello сведения о состоянии сохранены по Terraform и затем выходы hello запланированного выполнения _без_ фактически создается ресурсы в Azure. 

После выполнения предыдущей команды hello, вы увидите нечто похожее на следующий экран приветствия:

![План Terraform](./media/terraform/tf_plan2.png)

Если все выглядит правильно, подготовьте этой новой группы ресурсов в Azure, выполнив следующие hello: 
```
terraform apply
```
В hello портал Azure, вы увидите hello новой пустой ресурсов группы с именем `terraformtest`. В следующем разделе hello добавьте виртуальную машину, а все hello инфраструктуру поддержки для данной группы ресурсов toohello виртуальной машины.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Подготовка виртуальной машины Ubuntu с помощью Terraform
Давайте расширение виртуальной машины, работающей Ubuntu hello Terraform сценария, который мы создали с hello сведения, необходимые tooprovision. Hello ресурсы, которые подготовки в следующих разделах hello:

* сеть с одной подсетью;
* сетевая карта; 
* Учетную запись хранения диагностики hello виртуальной машины
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
Hello предыдущий сценарий создает виртуальную сеть и подсети в виртуальной сети. Обратите внимание, группа ресурсов toohello ссылка hello, уже созданных через «${azurerm_resource_group.helloterraform.name}» в виртуальной сети hello и определения подсетей hello.

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
Hello предыдущего сценария фрагментов создание общедоступного IP-адреса и сетевого интерфейса, который использует hello общедоступный IP-адрес создан. Обратите внимание toosubnet_id ссылки hello и public_ip_address_id. Terraform имеет встроенный toounderstand, hello сетевой интерфейс имеет зависимость ресурсов hello, toobe необходимость создания до создания hello hello сетевого интерфейса.

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
Вы создали учетную запись хранения. Эта учетная запись хранения является хранения сведений о нем диагностики hello виртуальной машины.

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
Наконец предыдущий код hello создает виртуальной машины, которая использует все ресурсы hello уже подготовлены. Они являются учетную запись хранения диагностики hello виртуальной машины, сетевой интерфейс открытый IP-адрес и подсеть указана, а hello группы ресурсов уже были созданы. Обратите внимание, свойство vm_size hello, где скрипт hello указывает номер SKU Azure Standard DS1v2.

Все необходимые toosupply открытый ключ SSH. Поместите hello значение открытого ключа в разделе hello **... INSERT OPENSSH PUBLIC KEY HERE ...** (Вставьте сюда значение открытого ключа OpenSSH). Вы можете использовать существующий ssh пару ключей или выполните hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) или [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) пары ключей hello toogenerate документации.

### <a name="execute-hello-script"></a>Выполнить сценарий hello
Сохранить полный скрипт hello выйти из toohello консоли или командной строки и введите ниже hello:
```
terraform apply
```
Через некоторое время hello ресурсы, включая виртуальной машины, отображаются в hello `terraformtest` группы ресурсов в hello портал Azure.

## <a name="complete-terraform-script"></a>Полный скрипт Terraform

Для удобства ниже приведен полный сценарий Terraform hello которая подготавливает все hello инфраструктуры, описанные в этой статье.

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

## <a name="next-steps"></a>Дальнейшие действия
Вы создали базовую инфраструктуру в Azure с помощью Terraform. Для более сложных сценариев, включая примеры с использованием подсистемы балансировки нагрузки и масштабируемых наборов виртуальных машин, см. многочисленные [примеры Terraform для Azure](https://github.com/hashicorp/terraform/tree/master/examples). Текущий список поддерживаемых поставщиков Azure, в разделе hello [Terraform документации](https://www.terraform.io/docs/providers/azurerm/index.html).
