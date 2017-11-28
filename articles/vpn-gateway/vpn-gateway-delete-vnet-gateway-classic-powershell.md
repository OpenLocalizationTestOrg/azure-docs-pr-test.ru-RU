---
title: "Удаление шлюза виртуальной сети с помощью PowerShell (классическая модель Azure) | Документация Майкрософт"
description: "Удаление шлюза виртуальной сети с помощью PowerShell в классической модели развертывания."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cherylmc
ms.openlocfilehash: b1bc18307227a728e2bc8fd95e30fdc1cbdb8c59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a><span data-ttu-id="96b06-103">Удаление шлюза виртуальной сети с помощью PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="96b06-103">Delete a virtual network gateway using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96b06-104">Resource Manager — портал Azure</span><span class="sxs-lookup"><span data-stu-id="96b06-104">Resource Manager - Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="96b06-105">Resource Manager — PowerShell</span><span class="sxs-lookup"><span data-stu-id="96b06-105">Resource Manager - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="96b06-106">Классическая модель: PowerShell</span><span class="sxs-lookup"><span data-stu-id="96b06-106">Classic - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="96b06-107">В этой статье описано, как удалить VPN-шлюз в классической модели развертывания с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96b06-107">This article helps you delete a VPN gateway in the classic deployment model by using PowerShell.</span></span> <span data-ttu-id="96b06-108">После удаления шлюза виртуальной сети измените файл конфигурации сети, чтобы удалить элементы, которые больше не используются.</span><span class="sxs-lookup"><span data-stu-id="96b06-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span></span>

##<span data-ttu-id="96b06-109"><a name="connect"></a>Шаг 1. Подключение к Azure</span><span class="sxs-lookup"><span data-stu-id="96b06-109"><a name="connect"></a>Step 1: Connect to Azure</span></span>

### <a name="1-install-the-latest-powershell-cmdlets"></a><span data-ttu-id="96b06-110">1. Установите последнюю версию командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96b06-110">1. Install the latest PowerShell cmdlets.</span></span>

<span data-ttu-id="96b06-111">Скачайте и установите последнюю версию командлетов PowerShell для управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="96b06-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="96b06-112">Дополнительные сведения см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96b06-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="96b06-113">2. Подключитесь к своей учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="96b06-113">2. Connect to your Azure account.</span></span> 

<span data-ttu-id="96b06-114">Откройте консоль PowerShell с повышенными правами и подключитесь к своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="96b06-114">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="96b06-115">Для подключения используйте следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="96b06-115">Use the following example to help you connect:</span></span>

```powershell
Add-AzureAccount
```

## <span data-ttu-id="96b06-116"><a name="export"></a>Шаг 2. Экспорт и просмотр файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="96b06-116"><a name="export"></a>Step 2: Export and view the network configuration file</span></span>

<span data-ttu-id="96b06-117">Создайте каталог на компьютере, а затем экспортируйте в него файл конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="96b06-117">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="96b06-118">С помощью этого файла можно просмотреть сведения о текущей конфигурации, а также изменить конфигурацию сети.</span><span class="sxs-lookup"><span data-stu-id="96b06-118">You use this file to both view the current configuration information, and also to modify the network configuration.</span></span>

<span data-ttu-id="96b06-119">В этом примере файл конфигурации сети экспортируется в каталог C:\AzureNet.</span><span class="sxs-lookup"><span data-stu-id="96b06-119">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="96b06-120">Откройте файл в текстовом редакторе и просмотрите имя для классической виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="96b06-120">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="96b06-121">При создании виртуальной сети на портале Azure полное имя, которое используется Azure, не отображается на портале.</span><span class="sxs-lookup"><span data-stu-id="96b06-121">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span></span> <span data-ttu-id="96b06-122">Например, если виртуальной сеть отображается на портале Azure с именем ClassicVNet1, то в файле конфигурации сети она может иметь гораздо более длинное имя.</span><span class="sxs-lookup"><span data-stu-id="96b06-122">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="96b06-123">Это имя может выглядеть примерно следующим образом: Group ClassicRG1 ClassicVNet1.</span><span class="sxs-lookup"><span data-stu-id="96b06-123">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span></span> <span data-ttu-id="96b06-124">Имена виртуальных сетей перечислены как **VirtualNetworkSite name =**.</span><span class="sxs-lookup"><span data-stu-id="96b06-124">Virtual network names are listed as **'VirtualNetworkSite name ='**.</span></span> <span data-ttu-id="96b06-125">При выполнении командлетов PowerShell используйте имена из файла конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="96b06-125">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

## <span data-ttu-id="96b06-126"><a name="delete"></a>Шаг 3. Удаление шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="96b06-126"><a name="delete"></a>Step 3: Delete the virtual network gateway</span></span>

<span data-ttu-id="96b06-127">При удалении шлюза виртуальной сети все подключения к виртуальной сети через шлюз будут отключены.</span><span class="sxs-lookup"><span data-stu-id="96b06-127">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span></span> <span data-ttu-id="96b06-128">Если к виртуальной сети подключены клиенты P2S, то они будут отключены без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="96b06-128">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span></span>

<span data-ttu-id="96b06-129">В этом примере удаляется шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="96b06-129">This example deletes the virtual network gateway.</span></span> <span data-ttu-id="96b06-130">Обязательно используйте полное имя виртуальной сети из файла конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="96b06-130">Make sure to use the full name of the virtual network from the network configuration file.</span></span>

```powershell
Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"
```

<span data-ttu-id="96b06-131">При успешном выполнении возвращается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="96b06-131">If successful, the return shows:</span></span>

```
Status : Successful
```

## <span data-ttu-id="96b06-132"><a name="modify"></a>Шаг 4. Изменение файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="96b06-132"><a name="modify"></a>Step 4: Modify the network configuration file</span></span>

<span data-ttu-id="96b06-133">При удалении шлюза виртуальной сети командлет не изменяет файл конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="96b06-133">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span></span> <span data-ttu-id="96b06-134">Необходимо изменить файл, чтобы удалить элементы, которые больше не используются.</span><span class="sxs-lookup"><span data-stu-id="96b06-134">You need to modify the file to remove the elements that are no longer being used.</span></span> <span data-ttu-id="96b06-135">В следующих разделах описывается, как изменить скачанный файл конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="96b06-135">The following sections help you modify the network configuration file that you downloaded.</span></span>

### <span data-ttu-id="96b06-136"><a name="lnsref"></a>Ссылки на сайты локальной сети</span><span class="sxs-lookup"><span data-stu-id="96b06-136"><a name="lnsref"></a>Local Network Site References</span></span>

<span data-ttu-id="96b06-137">Чтобы удалить данные ссылок на сайты, внесите изменения в элемент **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span><span class="sxs-lookup"><span data-stu-id="96b06-137">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span></span> <span data-ttu-id="96b06-138">Удаление ссылки на локальный сайт Azure инициирует удаление туннеля.</span><span class="sxs-lookup"><span data-stu-id="96b06-138">Removing a local site reference triggers Azure to delete a tunnel.</span></span> <span data-ttu-id="96b06-139">В зависимости от созданной конфигурации элемент **LocalNetworkSiteRef** может отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="96b06-139">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
     <LocalNetworkSiteRef name="D1BFC9CB_Site2">
       <Connection type="IPsec" />
     </LocalNetworkSiteRef>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

<span data-ttu-id="96b06-140">Пример:</span><span class="sxs-lookup"><span data-stu-id="96b06-140">Example:</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

###<span data-ttu-id="96b06-141"><a name="lns"></a>Сайты локальной сети</span><span class="sxs-lookup"><span data-stu-id="96b06-141"><a name="lns"></a>Local Network Sites</span></span>

<span data-ttu-id="96b06-142">Удалите все локальные сайты, которые больше не используются.</span><span class="sxs-lookup"><span data-stu-id="96b06-142">Remove any local sites that you are no longer using.</span></span> <span data-ttu-id="96b06-143">В зависимости от созданной конфигурации элемент **LocalNetworkSite** может отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="96b06-143">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
  <LocalNetworkSite name="Site3">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

<span data-ttu-id="96b06-144">В этом примере мы удалили только Site3.</span><span class="sxs-lookup"><span data-stu-id="96b06-144">In this example, we removed only Site3.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

### <span data-ttu-id="96b06-145"><a name="clientaddresss"></a>Пул адресов клиента</span><span class="sxs-lookup"><span data-stu-id="96b06-145"><a name="clientaddresss"></a>Client AddressPool</span></span>

<span data-ttu-id="96b06-146">Если к виртуальной сети установлено подключение типа "точка — сеть", то должен быть элемент **VPNClientAddressPool**.</span><span class="sxs-lookup"><span data-stu-id="96b06-146">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span></span> <span data-ttu-id="96b06-147">Удалите пулы адресов клиента, которые соответствуют удаленному шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="96b06-147">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span></span>

```
<Gateway>
    <VPNClientAddressPool>
      <AddressPrefix>10.1.0.0/24</AddressPrefix>
    </VPNClientAddressPool>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

<span data-ttu-id="96b06-148">Пример:</span><span class="sxs-lookup"><span data-stu-id="96b06-148">Example:</span></span>

```
<Gateway>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

### <span data-ttu-id="96b06-149"><a name="gwsub"></a>Подсеть шлюза</span><span class="sxs-lookup"><span data-stu-id="96b06-149"><a name="gwsub"></a>GatewaySubnet</span></span>

<span data-ttu-id="96b06-150">Удалите подсеть шлюза (элемент **GatewaySubnet**), которая соответствует виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="96b06-150">Delete the **GatewaySubnet** that corresponds to the VNet.</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
   <Subnet name="GatewaySubnet">
     <AddressPrefix>10.11.1.0/29</AddressPrefix>
   </Subnet>
 </Subnets>
```

<span data-ttu-id="96b06-151">Пример:</span><span class="sxs-lookup"><span data-stu-id="96b06-151">Example:</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
 </Subnets>
```

## <span data-ttu-id="96b06-152"><a name="upload"></a>Шаг 5. Передача файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="96b06-152"><a name="upload"></a>Step 5: Upload the network configuration file</span></span>

<span data-ttu-id="96b06-153">Сохраните изменения и передайте файл конфигурации сети в Azure.</span><span class="sxs-lookup"><span data-stu-id="96b06-153">Save your changes and upload the network configuration file to Azure.</span></span> <span data-ttu-id="96b06-154">Обязательно измените путь к файлу в соответствии с вашей средой.</span><span class="sxs-lookup"><span data-stu-id="96b06-154">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="96b06-155">При успешном выполнении возвращается примерно следующий результат:</span><span class="sxs-lookup"><span data-stu-id="96b06-155">If successful, the return shows something similar to this example:</span></span>

```
OperationDescription        OperationId                      OperationStatus                                                
--------------------        -----------                      ---------------                                           
Set-AzureVNetConfig         e0ee6e66-9167-cfa7-a746-7casb9   Succeeded