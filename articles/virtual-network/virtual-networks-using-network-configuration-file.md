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
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="030ea-103">Настройка (классической) виртуальной сети с помощью файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="030ea-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="030ea-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="030ea-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="030ea-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="030ea-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="030ea-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="030ea-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="030ea-107">Можно создать и настроить виртуальную сеть (классические) с помощью файла конфигурации сети, с помощью hello Azure командной строки (CLI) 1.0 или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="030ea-107">You can create and configure a virtual network (classic) with a network configuration file using hello Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="030ea-108">Нельзя создавать или изменять виртуальной сети с помощью модели развертывания диспетчера ресурсов Azure hello, с помощью файла конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="030ea-108">You cannot create or modify a virtual network through hello Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="030ea-109">Невозможно использовать hello Azure портала toocreate или изменения виртуальной сети (классические), с помощью файла конфигурации сети, Здравствуйте Azure портала toocreate виртуальной сети (классической), без использования файла конфигурации сети, однако можно использовать.</span><span class="sxs-lookup"><span data-stu-id="030ea-109">You cannot use hello Azure portal toocreate or modify a virtual network (classic) using a network configuration file, however you can use hello Azure portal toocreate a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="030ea-110">Создание и настройка виртуальной сети (классические) с помощью файла конфигурации сети требуется экспорт, изменение и импорт файла hello.</span><span class="sxs-lookup"><span data-stu-id="030ea-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing hello file.</span></span>

## <span data-ttu-id="030ea-111"><a name="export"></a>Экспорт файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="030ea-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="030ea-112">Можно использовать PowerShell или hello Azure CLI tooexport файла конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="030ea-112">You can use PowerShell or hello Azure CLI tooexport a network configuration file.</span></span> <span data-ttu-id="030ea-113">PowerShell Экспортирует XML-файл, пока hello Azure CLI экспортирует json-файла.</span><span class="sxs-lookup"><span data-stu-id="030ea-113">PowerShell exports an XML file, while hello Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="030ea-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="030ea-114">PowerShell</span></span>
 
1. <span data-ttu-id="030ea-115">[Установка Azure PowerShell и вход в tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="030ea-115">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="030ea-116">Измените каталог hello (и убедитесь, он существует) и имя файла в hello следующие команды в качестве требуемой, а затем выполнения hello команда tooexport hello файла конфигурации сети:</span><span class="sxs-lookup"><span data-stu-id="030ea-116">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="030ea-117">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="030ea-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="030ea-118">[Установка hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="030ea-118">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="030ea-119">Выполните оставшиеся шаги из командной строки Azure CLI 1.0 hello.</span><span class="sxs-lookup"><span data-stu-id="030ea-119">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="030ea-120">Войдите в tooAzure, указав hello `azure login` команды.</span><span class="sxs-lookup"><span data-stu-id="030ea-120">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="030ea-121">Убедитесь, вы находитесь в режиме ассемблерного кода, введя hello `azure config mode asm` команды.</span><span class="sxs-lookup"><span data-stu-id="030ea-121">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="030ea-122">Измените каталог hello (и убедитесь, он существует) и имя файла в hello следующие команды в качестве требуемой, а затем выполнения hello команда tooexport hello файла конфигурации сети:</span><span class="sxs-lookup"><span data-stu-id="030ea-122">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="030ea-123">Создание и изменение файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="030ea-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="030ea-124">Файл конфигурации сети является XML-файла (при использовании PowerShell) или json-файла (при использовании hello Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="030ea-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using hello Azure CLI).</span></span> <span data-ttu-id="030ea-125">Можно изменить файл hello в любой текст или редактор XML или json.</span><span class="sxs-lookup"><span data-stu-id="030ea-125">You can edit hello file in any text, or XML/json editor.</span></span> <span data-ttu-id="030ea-126">Hello [параметрам схемы файла конфигурации сети](https://msdn.microsoft.com/library/azure/jj157100.aspx) статья содержит сведения для всех параметров.</span><span class="sxs-lookup"><span data-stu-id="030ea-126">hello [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="030ea-127">Дополнительное объяснение параметров hello. в разделе [просматривать виртуальные сети и параметры](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="030ea-127">For additional explanation of hello settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="030ea-128">Hello изменения toohello файла:</span><span class="sxs-lookup"><span data-stu-id="030ea-128">hello changes you make toohello file:</span></span>

- <span data-ttu-id="030ea-129">Должно соответствовать hello схемы или импорт hello сети файл конфигурации не выполняется.</span><span class="sxs-lookup"><span data-stu-id="030ea-129">Must comply with hello schema, or importing hello network configuration file will fail.</span></span>
- <span data-ttu-id="030ea-130">Перезапишут все имеющиеся параметры сети подписки. Поэтому соблюдайте предельную осторожность при внесении изменений.</span><span class="sxs-lookup"><span data-stu-id="030ea-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="030ea-131">Например ссылка файлов конфигурации сети пример hello, следующие.</span><span class="sxs-lookup"><span data-stu-id="030ea-131">For example, reference hello example network configuration files that follow.</span></span> <span data-ttu-id="030ea-132">Произнесите hello исходный файл содержит два **VirtualNetworkSite** экземпляров и изменить его, как показано в примерах hello.</span><span class="sxs-lookup"><span data-stu-id="030ea-132">Say hello original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in hello examples.</span></span> <span data-ttu-id="030ea-133">При импорте файла hello Azure удаляет hello виртуальной сети для hello **VirtualNetworkSite** экземпляра удаляемого в файле hello.</span><span class="sxs-lookup"><span data-stu-id="030ea-133">When you import hello file, Azure deletes hello virtual network for hello **VirtualNetworkSite** instance you removed in hello file.</span></span> <span data-ttu-id="030ea-134">Упрощенная предполагается ресурсы не были в hello виртуальной сети, как если бы, hello виртуальной сети не может быть удален, и не импорта hello.</span><span class="sxs-lookup"><span data-stu-id="030ea-134">This simplified scenario assumes no resources were in hello virtual network, as if there were, hello virtual network could not be deleted, and hello import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="030ea-135">Azure считает, что подсети, которая содержит какие-то развернуты tooit как **используется**.</span><span class="sxs-lookup"><span data-stu-id="030ea-135">Azure considers a subnet that has something deployed tooit as **in use**.</span></span> <span data-ttu-id="030ea-136">Когда подсеть используется, она не может быть изменена.</span><span class="sxs-lookup"><span data-stu-id="030ea-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="030ea-137">Прежде чем изменять сведения о подсети в файле конфигурации сети, переместите все, что вы развернули toohello подсети tooa другой подсети, не изменяется.</span><span class="sxs-lookup"><span data-stu-id="030ea-137">Before modifying subnet information in a network configuration file, move anything that you have deployed toohello subnet tooa different subnet that isn't being modified.</span></span> <span data-ttu-id="030ea-138">В разделе [перемещения виртуальной Машины или экземпляра роли tooa другой подсети](virtual-networks-move-vm-role-to-subnet.md) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="030ea-138">See [Move a VM or Role Instance tooa Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="030ea-139">Пример кода XML для использования с PowerShell</span><span class="sxs-lookup"><span data-stu-id="030ea-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="030ea-140">Hello ниже пример файла конфигурации сети создает виртуальную сеть с именем *myVirtualNetwork* с адресным пространством *10.0.0.0/16* в hello *Восток США* Azure область.</span><span class="sxs-lookup"><span data-stu-id="030ea-140">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="030ea-141">Hello виртуальная сеть содержит одну подсеть с именем *mySubnet* с префикс адреса *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="030ea-141">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="030ea-142">Файл конфигурации сети hello, который вы экспортировали содержит нет содержимого, можно скопировать hello XML в предыдущем примере hello и вставьте его в новый файл.</span><span class="sxs-lookup"><span data-stu-id="030ea-142">If hello network configuration file you exported contains no contents, you can copy hello XML in hello previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-hello-azure-cli-10"></a><span data-ttu-id="030ea-143">Пример JSON для использования с hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="030ea-143">Example JSON for use with hello Azure CLI 1.0</span></span>

<span data-ttu-id="030ea-144">Hello ниже пример файла конфигурации сети создает виртуальную сеть с именем *myVirtualNetwork* с адресным пространством *10.0.0.0/16* в hello *Восток США* Azure область.</span><span class="sxs-lookup"><span data-stu-id="030ea-144">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="030ea-145">Hello виртуальная сеть содержит одну подсеть с именем *mySubnet* с префикс адреса *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="030ea-145">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="030ea-146">Файл конфигурации сети hello, который вы экспортировали содержит нет содержимого, можно скопировать hello json в предыдущем примере hello и вставьте его в новый файл.</span><span class="sxs-lookup"><span data-stu-id="030ea-146">If hello network configuration file you exported contains no contents, you can copy hello json in hello previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="030ea-147"><a name="import"></a>Импорт файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="030ea-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="030ea-148">Можно использовать PowerShell или hello Azure CLI tooimport файла конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="030ea-148">You can use PowerShell or hello Azure CLI tooimport a network configuration file.</span></span> <span data-ttu-id="030ea-149">PowerShell импортирует XML-файл, пока hello Azure CLI импортирует файл json.</span><span class="sxs-lookup"><span data-stu-id="030ea-149">PowerShell imports an XML file, while hello Azure CLI imports a json file.</span></span> <span data-ttu-id="030ea-150">Если импорт hello не удается, убедитесь, этот файл hello соответствует hello [схема конфигурации сети](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="030ea-150">If hello import fails, confirm that hello file complies with hello [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="030ea-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="030ea-151">PowerShell</span></span>
 
1. <span data-ttu-id="030ea-152">[Установка Azure PowerShell и вход в tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="030ea-152">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="030ea-153">Измените hello каталог и имя файла в следующую команду, при необходимости hello, а затем запустите файл конфигурации сети hello tooimport hello команды:</span><span class="sxs-lookup"><span data-stu-id="030ea-153">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="030ea-154">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="030ea-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="030ea-155">[Установка hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="030ea-155">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="030ea-156">Выполните оставшиеся шаги из командной строки Azure CLI 1.0 hello.</span><span class="sxs-lookup"><span data-stu-id="030ea-156">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="030ea-157">Войдите в tooAzure, указав hello `azure login` команды.</span><span class="sxs-lookup"><span data-stu-id="030ea-157">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="030ea-158">Убедитесь, вы находитесь в режиме ассемблерного кода, введя hello `azure config mode asm` команды.</span><span class="sxs-lookup"><span data-stu-id="030ea-158">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="030ea-159">Измените hello каталог и имя файла в следующую команду, при необходимости hello, а затем запустите файл конфигурации сети hello tooimport hello команды:</span><span class="sxs-lookup"><span data-stu-id="030ea-159">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
