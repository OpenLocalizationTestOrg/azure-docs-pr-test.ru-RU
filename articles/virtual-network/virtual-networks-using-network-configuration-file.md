---
title: "Настройка (классической) виртуальной сети Azure с использованием файла конфигурации сети | Документация Майкрософт"
description: "Узнайте, как изменить и создать (классические) виртуальные сети путем экспорта, изменения и импорта файла конфигурации сети."
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
ms.openlocfilehash: f1e3ae26b6525f2235a6b0d53546b334dc027b94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="f2f3d-103">Настройка (классической) виртуальной сети с помощью файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="f2f3d-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f2f3d-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2f3d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="f2f3d-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="f2f3d-106">Для большинства новых развертываний корпорация Майкрософт рекомендует использовать модель развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-106">Microsoft recommends that most new deployments use the Resource Manager deployment model.</span></span>

<span data-ttu-id="f2f3d-107">Вы можете создать и настроить (классическую) виртуальную сеть с файлом конфигурации сети с помощью интерфейса командной строки Azure (CLI) 1.0 или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-107">You can create and configure a virtual network (classic) with a network configuration file using the Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="f2f3d-108">Вы не можете создавать или изменять виртуальную сеть с помощью модели развертывания Azure Resource Manager с использованием файла конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-108">You cannot create or modify a virtual network through the Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="f2f3d-109">Использовать портал Azure для создания или изменения (классической) виртуальной сети с помощью файла конфигурации сети нельзя. Однако портал Azure можно использовать для создания такой сети без использования файла конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-109">You cannot use the Azure portal to create or modify a virtual network (classic) using a network configuration file, however you can use the Azure portal to create a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="f2f3d-110">Для создания и настройки (классической) виртуальной сети с помощью файла конфигурации сети необходимо экспортировать, изменить и импортировать файл.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing the file.</span></span>

## <span data-ttu-id="f2f3d-111"><a name="export"></a>Экспорт файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="f2f3d-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="f2f3d-112">Чтобы экспортировать файл конфигурации сети, можно использовать PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-112">You can use PowerShell or the Azure CLI to export a network configuration file.</span></span> <span data-ttu-id="f2f3d-113">PowerShell экспортирует XML-файл, а Azure CLI — JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-113">PowerShell exports an XML file, while the Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="f2f3d-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2f3d-114">PowerShell</span></span>
 
1. <span data-ttu-id="f2f3d-115">[Установите Azure PowerShell и войдите в Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2f3d-115">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="f2f3d-116">При необходимости измените каталог (убедитесь, что он существует) и имя файла в указанной ниже команде. Затем выполните команду, чтобы экспортировать файл конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-116">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="f2f3d-117">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f2f3d-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="f2f3d-118">[Установите Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2f3d-118">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="f2f3d-119">Выполните оставшиеся шаги в командной строке Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-119">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="f2f3d-120">Войдите в Azure, выполнив команду `azure login`.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-120">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="f2f3d-121">Выполните команду `azure config mode asm`, чтобы убедиться, что используется режим ASM.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-121">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="f2f3d-122">При необходимости измените каталог (убедитесь, что он существует) и имя файла в указанной ниже команде. Затем выполните команду, чтобы экспортировать файл конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-122">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="f2f3d-123">Создание и изменение файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="f2f3d-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="f2f3d-124">Файл конфигурации сети имеет формат XML (при использовании PowerShell) или JSON (при использовании Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="f2f3d-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using the Azure CLI).</span></span> <span data-ttu-id="f2f3d-125">Файл можно изменить в любом текстовом редакторе и в редакторе XML или JSON.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-125">You can edit the file in any text, or XML/json editor.</span></span> <span data-ttu-id="f2f3d-126">Сведения о параметрах схемы файла конфигурации сети см. в [этой статье](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2f3d-126">The [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="f2f3d-127">Дополнительные сведения о параметрах см. в разделе [Просмотр виртуальных сетей и параметров](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="f2f3d-127">For additional explanation of the settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="f2f3d-128">Изменения, внесенные в файл:</span><span class="sxs-lookup"><span data-stu-id="f2f3d-128">The changes you make to the file:</span></span>

- <span data-ttu-id="f2f3d-129">Должны соответствовать схеме. В противном случае импорт файла конфигурации сети завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-129">Must comply with the schema, or importing the network configuration file will fail.</span></span>
- <span data-ttu-id="f2f3d-130">Перезапишут все имеющиеся параметры сети подписки. Поэтому соблюдайте предельную осторожность при внесении изменений.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="f2f3d-131">Например, просмотрите указанные ниже примеры файла конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-131">For example, reference the example network configuration files that follow.</span></span> <span data-ttu-id="f2f3d-132">Предположим, что исходный файл содержит два экземпляра **VirtualNetworkSite** и вы его изменили, как показано в примерах.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-132">Say the original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in the examples.</span></span> <span data-ttu-id="f2f3d-133">При импорте файла Azure удаляет виртуальную сеть для экземпляра **VirtualNetworkSite**, удаленного в файле.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-133">When you import the file, Azure deletes the virtual network for the **VirtualNetworkSite** instance you removed in the file.</span></span> <span data-ttu-id="f2f3d-134">Этот упрощенный сценарий предполагает, что в виртуальной сети отсутствуют ресурсы. В противном случае виртуальную сеть не удастся удалить, а импорт завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-134">This simplified scenario assumes no resources were in the virtual network, as if there were, the virtual network could not be deleted, and the import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2f3d-135">Azure рассматривает подсеть с имеющимся развертыванием как **используемую**.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-135">Azure considers a subnet that has something deployed to it as **in use**.</span></span> <span data-ttu-id="f2f3d-136">Когда подсеть используется, она не может быть изменена.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="f2f3d-137">Перед изменением информации о подсети в файле конфигурации сети переместите все, что было развернуто в подсети, в другую подсеть, которая не изменяется.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-137">Before modifying subnet information in a network configuration file, move anything that you have deployed to the subnet to a different subnet that isn't being modified.</span></span> <span data-ttu-id="f2f3d-138">Дополнительные сведения см. в статье [Перемещение (классической) виртуальной машины или экземпляра роли облачных служб в другую подсеть с помощью PowerShell](virtual-networks-move-vm-role-to-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="f2f3d-138">See [Move a VM or Role Instance to a Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="f2f3d-139">Пример кода XML для использования с PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2f3d-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="f2f3d-140">В следующем примере файла конфигурации сети создается виртуальная сеть с именем *myVirtualNetwork* и адресным пространством *10.0.0.0/16* в регионе Azure — *восточная часть США*.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-140">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="f2f3d-141">Виртуальная сеть содержит одну подсеть с именем *mySubnet* и префиксом адреса *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-141">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="f2f3d-142">Если экспортированный файл конфигурации сети пуст, можно скопировать код XML из предыдущего примера и вставить его в новый файл.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-142">If the network configuration file you exported contains no contents, you can copy the XML in the previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-the-azure-cli-10"></a><span data-ttu-id="f2f3d-143">Пример кода JSON для использования с Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f2f3d-143">Example JSON for use with the Azure CLI 1.0</span></span>

<span data-ttu-id="f2f3d-144">В следующем примере файла конфигурации сети создается виртуальная сеть с именем *myVirtualNetwork* и адресным пространством *10.0.0.0/16* в регионе Azure — *восточная часть США*.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-144">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="f2f3d-145">Виртуальная сеть содержит одну подсеть с именем *mySubnet* и префиксом адреса *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-145">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="f2f3d-146">Если экспортируемый файл конфигурации сети пуст, можно скопировать код JSON из предыдущего примера и вставить его в новый файл.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-146">If the network configuration file you exported contains no contents, you can copy the json in the previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="f2f3d-147"><a name="import"></a>Импорт файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="f2f3d-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="f2f3d-148">Чтобы импортировать файл конфигурации сети, можно использовать PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-148">You can use PowerShell or the Azure CLI to import a network configuration file.</span></span> <span data-ttu-id="f2f3d-149">PowerShell импортирует XML-файл, а Azure CLI — JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-149">PowerShell imports an XML file, while the Azure CLI imports a json file.</span></span> <span data-ttu-id="f2f3d-150">При сбое импорта убедитесь, что файл соответствует [схеме конфигурации сети](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2f3d-150">If the import fails, confirm that the file complies with the [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="f2f3d-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2f3d-151">PowerShell</span></span>
 
1. <span data-ttu-id="f2f3d-152">[Установите Azure PowerShell и войдите в Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2f3d-152">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="f2f3d-153">При необходимости измените каталог и имя файла в указанной ниже команде. Затем выполните команду, чтобы импортировать файл конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-153">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="f2f3d-154">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f2f3d-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="f2f3d-155">[Установите Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2f3d-155">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="f2f3d-156">Выполните оставшиеся шаги в командной строке Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-156">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="f2f3d-157">Войдите в Azure, выполнив команду `azure login`.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-157">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="f2f3d-158">Выполните команду `azure config mode asm`, чтобы убедиться, что используется режим ASM.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-158">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="f2f3d-159">При необходимости измените каталог и имя файла в указанной ниже команде. Затем выполните команду, чтобы импортировать файл конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="f2f3d-159">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
