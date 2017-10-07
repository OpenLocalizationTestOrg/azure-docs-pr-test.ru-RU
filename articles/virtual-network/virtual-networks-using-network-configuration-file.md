---
title: "aaaConfigure виртуальной сети Azure (классические) - файл конфигурации сети | Документы Microsoft"
description: "Узнайте, как toocreate и изменять виртуальные сети (классические) путем экспорт, изменение и импорт файла конфигурации сети."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a>Настройка (классической) виртуальной сети с помощью файла конфигурации сети
> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели развертывания диспетчера ресурсов hello.

Можно создать и настроить виртуальную сеть (классические) с помощью файла конфигурации сети, с помощью hello Azure командной строки (CLI) 1.0 или Azure PowerShell. Нельзя создавать или изменять виртуальной сети с помощью модели развертывания диспетчера ресурсов Azure hello, с помощью файла конфигурации сети. Невозможно использовать hello Azure портала toocreate или изменения виртуальной сети (классические), с помощью файла конфигурации сети, Здравствуйте Azure портала toocreate виртуальной сети (классической), без использования файла конфигурации сети, однако можно использовать.

Создание и настройка виртуальной сети (классические) с помощью файла конфигурации сети требуется экспорт, изменение и импорт файла hello.

## <a name="export"></a>Экспорт файла конфигурации сети

Можно использовать PowerShell или hello Azure CLI tooexport файла конфигурации сети. PowerShell Экспортирует XML-файл, пока hello Azure CLI экспортирует json-файла.

### <a name="powershell"></a>PowerShell
 
1. [Установка Azure PowerShell и вход в tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Измените каталог hello (и убедитесь, он существует) и имя файла в hello следующие команды в качестве требуемой, а затем выполнения hello команда tooexport hello файла конфигурации сети:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [Установка hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Выполните оставшиеся шаги из командной строки Azure CLI 1.0 hello.
2. Войдите в tooAzure, указав hello `azure login` команды.
3. Убедитесь, вы находитесь в режиме ассемблерного кода, введя hello `azure config mode asm` команды.
4. Измените каталог hello (и убедитесь, он существует) и имя файла в hello следующие команды в качестве требуемой, а затем выполнения hello команда tooexport hello файла конфигурации сети:
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a>Создание и изменение файла конфигурации сети

Файл конфигурации сети является XML-файла (при использовании PowerShell) или json-файла (при использовании hello Azure CLI). Можно изменить файл hello в любой текст или редактор XML или json. Hello [параметрам схемы файла конфигурации сети](https://msdn.microsoft.com/library/azure/jj157100.aspx) статья содержит сведения для всех параметров. Дополнительное объяснение параметров hello. в разделе [просматривать виртуальные сети и параметры](virtual-network-manage-network.md#view-vnet). Hello изменения toohello файла:

- Должно соответствовать hello схемы или импорт hello сети файл конфигурации не выполняется.
- Перезапишут все имеющиеся параметры сети подписки. Поэтому соблюдайте предельную осторожность при внесении изменений. Например ссылка файлов конфигурации сети пример hello, следующие. Произнесите hello исходный файл содержит два **VirtualNetworkSite** экземпляров и изменить его, как показано в примерах hello. При импорте файла hello Azure удаляет hello виртуальной сети для hello **VirtualNetworkSite** экземпляра удаляемого в файле hello. Упрощенная предполагается ресурсы не были в hello виртуальной сети, как если бы, hello виртуальной сети не может быть удален, и не импорта hello.

> [!IMPORTANT]
> Azure считает, что подсети, которая содержит какие-то развернуты tooit как **используется**. Когда подсеть используется, она не может быть изменена. Прежде чем изменять сведения о подсети в файле конфигурации сети, переместите все, что вы развернули toohello подсети tooa другой подсети, не изменяется. В разделе [перемещения виртуальной Машины или экземпляра роли tooa другой подсети](virtual-networks-move-vm-role-to-subnet.md) подробные сведения.

### <a name="example-xml-for-use-with-powershell"></a>Пример кода XML для использования с PowerShell

Hello ниже пример файла конфигурации сети создает виртуальную сеть с именем *myVirtualNetwork* с адресным пространством *10.0.0.0/16* в hello *Восток США* Azure область. Hello виртуальная сеть содержит одну подсеть с именем *mySubnet* с префикс адреса *10.0.0.0/24*.

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

Файл конфигурации сети hello, который вы экспортировали содержит нет содержимого, можно скопировать hello XML в предыдущем примере hello и вставьте его в новый файл.

### <a name="example-json-for-use-with-hello-azure-cli-10"></a>Пример JSON для использования с hello Azure CLI 1.0

Hello ниже пример файла конфигурации сети создает виртуальную сеть с именем *myVirtualNetwork* с адресным пространством *10.0.0.0/16* в hello *Восток США* Azure область. Hello виртуальная сеть содержит одну подсеть с именем *mySubnet* с префикс адреса *10.0.0.0/24*.

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

Файл конфигурации сети hello, который вы экспортировали содержит нет содержимого, можно скопировать hello json в предыдущем примере hello и вставьте его в новый файл.

## <a name="import"></a>Импорт файла конфигурации сети

Можно использовать PowerShell или hello Azure CLI tooimport файла конфигурации сети. PowerShell импортирует XML-файл, пока hello Azure CLI импортирует файл json. Если импорт hello не удается, убедитесь, этот файл hello соответствует hello [схема конфигурации сети](https://msdn.microsoft.com/library/azure/jj157100.aspx). 

### <a name="powershell"></a>PowerShell
 
1. [Установка Azure PowerShell и вход в tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Измените hello каталог и имя файла в следующую команду, при необходимости hello, а затем запустите файл конфигурации сети hello tooimport hello команды:
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [Установка hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Выполните оставшиеся шаги из командной строки Azure CLI 1.0 hello.
2. Войдите в tooAzure, указав hello `azure login` команды.
3. Убедитесь, вы находитесь в режиме ассемблерного кода, введя hello `azure config mode asm` команды.
4. Измените hello каталог и имя файла в следующую команду, при необходимости hello, а затем запустите файл конфигурации сети hello tooimport hello команды:

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
