---
title: "Подключение tooAzure классических виртуальных сетей виртуальных сетей диспетчера ресурсов: PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate VPN-подключение между классических виртуальных сетей и виртуальных сетей диспетчера ресурсов с помощью VPN-шлюза и PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="ef695-103">Подключение виртуальных сетей из различных моделей развертывания с использованием PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef695-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="ef695-104">В этой статье показано, как tooconnect классических виртуальных сетей tooResource tooallow диспетчер виртуальных сетей hello ресурсам, расположенным в hello отдельное развертывание моделей toocommunicate друг с другом.</span><span class="sxs-lookup"><span data-stu-id="ef695-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="ef695-105">Hello действия, описанные в этой статье с помощью PowerShell, но можно также создать этой конфигурации с помощью портала Azure hello, выбрав статьи hello из этого списка.</span><span class="sxs-lookup"><span data-stu-id="ef695-105">hello steps in this article use PowerShell, but you can also create this configuration using hello Azure portal by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef695-106">Портал</span><span class="sxs-lookup"><span data-stu-id="ef695-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="ef695-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef695-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="ef695-108">Подключение классический tooa виртуальной сети VNet диспетчера ресурсов выполняется аналогично tooconnecting локального сайта виртуальной сети tooan расположения.</span><span class="sxs-lookup"><span data-stu-id="ef695-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="ef695-109">Оба типа подключения используйте tooprovide шлюза VPN защищенный туннель, с помощью IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="ef695-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="ef695-110">Подключение можно создать между виртуальными сетями, которые находятся в разных подписках и разных регионах.</span><span class="sxs-lookup"><span data-stu-id="ef695-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="ef695-111">Можно также подключиться, которые уже есть подключения tooon локальные сети, при условии, что шлюз hello, они были настроены: динамический или на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="ef695-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="ef695-112">Дополнительные сведения о подключениях к виртуальной сети для виртуальной сети см. в разделе hello [часто задаваемые вопросы о виртуальной сети для виртуальной сети](#faq) конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ef695-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="ef695-113">Если ваш виртуальных сетей в hello совпадают, вы можете tooinstead необходимо учитывать их с помощью Пиринг виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="ef695-114">При пиринговой связи между виртуальными сетями VPN-шлюз не используется.</span><span class="sxs-lookup"><span data-stu-id="ef695-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="ef695-115">Дополнительную информацию см. в статье [Пиринговая связь между виртуальными сетями](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef695-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="ef695-116">Подготовка</span><span class="sxs-lookup"><span data-stu-id="ef695-116">Before beginning</span></span>

<span data-ttu-id="ef695-117">Hello следующее пошаговыми руководствами tooconfigure необходимые параметры hello динамические или на основе маршрутов шлюза для каждой виртуальной сети и создания VPN-подключений между шлюзами hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-117">hello following steps walk you through hello settings necessary tooconfigure a dynamic or route-based gateway for each VNet and create a VPN connection between hello gateways.</span></span> <span data-ttu-id="ef695-118">Эта конфигурация не поддерживает статические шлюзы и шлюзы на основе политик.</span><span class="sxs-lookup"><span data-stu-id="ef695-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ef695-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ef695-119">Prerequisites</span></span>

* <span data-ttu-id="ef695-120">Обе виртуальные сети уже созданы.</span><span class="sxs-lookup"><span data-stu-id="ef695-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="ef695-121">Hello диапазоны адресов для hello виртуальных сетей не перекрываются друг с другом или перекрываться с любым hello диапазонов для других соединений, hello шлюзов могут быть подключены.</span><span class="sxs-lookup"><span data-stu-id="ef695-121">hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="ef695-122">Установлены новые командлеты PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-122">You have installed hello latest PowerShell cmdlets.</span></span> <span data-ttu-id="ef695-123">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="ef695-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="ef695-124">Убедитесь в том, что при установке службы управления (SM) hello и hello командлеты диспетчера ресурсов (RM).</span><span class="sxs-lookup"><span data-stu-id="ef695-124">Make sure you install both hello Service Management (SM) and hello Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="ef695-125"><a name="exampleref"></a>Примеры настроек</span><span class="sxs-lookup"><span data-stu-id="ef695-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="ef695-126">Можно использовать эти значения toocreate тестовой среде, или ссылаться toothem toobetter понять hello примеры в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ef695-126">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="ef695-127">**Параметры классической виртуальной сети**</span><span class="sxs-lookup"><span data-stu-id="ef695-127">**Classic VNet settings**</span></span>

<span data-ttu-id="ef695-128">Имя виртуальной сети = ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="ef695-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="ef695-129">Расположение: Западная часть США</span><span class="sxs-lookup"><span data-stu-id="ef695-129">Location = West US</span></span> <br>
<span data-ttu-id="ef695-130">Адресные пространства виртуальной сети = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="ef695-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="ef695-131">Подсеть-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="ef695-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="ef695-132">Шлюз подсети = 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="ef695-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="ef695-133">Имя локальной сети = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="ef695-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="ef695-134">Тип шлюза = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="ef695-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="ef695-135">**Параметры виртуальной сети Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="ef695-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="ef695-136">Имя виртуальной сети = RMVNet</span><span class="sxs-lookup"><span data-stu-id="ef695-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="ef695-137">Группа ресурсов = RG1</span><span class="sxs-lookup"><span data-stu-id="ef695-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="ef695-138">Адресные пространства виртуальной сети = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ef695-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="ef695-139">Подсеть-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="ef695-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="ef695-140">Шлюз подсети = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="ef695-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="ef695-141">Расположение = восточная часть США</span><span class="sxs-lookup"><span data-stu-id="ef695-141">Location = East US</span></span> <br>
<span data-ttu-id="ef695-142">Общедоступное IP-имя шлюза: gwpip</span><span class="sxs-lookup"><span data-stu-id="ef695-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="ef695-143">Шлюз локальной сети = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="ef695-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="ef695-144">Имя шлюза виртуальной сети = RMGateway</span><span class="sxs-lookup"><span data-stu-id="ef695-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="ef695-145">Конфигурация IP-адресации шлюза = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="ef695-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="ef695-146"><a name="createsmgw"></a>Раздел 1 — Настройка hello классической виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="ef695-146"><a name="createsmgw"></a>Section 1 - Configure hello classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="ef695-147">Часть 1. Скачивание файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="ef695-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="ef695-148">Войдите в tooyour учетной записи Azure в hello консоли PowerShell с повышенными правами.</span><span class="sxs-lookup"><span data-stu-id="ef695-148">Log in tooyour Azure account in hello PowerShell console with elevated rights.</span></span> <span data-ttu-id="ef695-149">Hello следующий командлет запросит hello учетные данные входа для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="ef695-149">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="ef695-150">После входа в систему, он загружает параметры учетной записи, чтобы они были доступны tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef695-150">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span> <span data-ttu-id="ef695-151">Используйте hello toocomplete командлеты SM PowerShell этой части конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-151">You use hello SM PowerShell cmdlets toocomplete this part of hello configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="ef695-152">Экспортируйте файл конфигурации сети Azure, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-152">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="ef695-153">Можно изменить расположение hello hello tooexport tooa различные расположения файла при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ef695-153">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="ef695-154">Привет открыть XML-файл, загруженный tooedit его.</span><span class="sxs-lookup"><span data-stu-id="ef695-154">Open hello .xml file that you downloaded tooedit it.</span></span> <span data-ttu-id="ef695-155">Пример файла конфигурации сети hello разделе hello [схема конфигурации сети](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef695-155">For an example of hello network configuration file, see hello [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-hello-gateway-subnet"></a><span data-ttu-id="ef695-156">Часть 2 - Проверьте hello подсеть шлюза</span><span class="sxs-lookup"><span data-stu-id="ef695-156">Part 2 -Verify hello gateway subnet</span></span>
<span data-ttu-id="ef695-157">В hello **VirtualNetworkSites** элемента, добавьте tooyour подсети шлюза виртуальной сети, если оно еще не создано.</span><span class="sxs-lookup"><span data-stu-id="ef695-157">In hello **VirtualNetworkSites** element, add a gateway subnet tooyour VNet if one has not already been created.</span></span> <span data-ttu-id="ef695-158">При работе с файлом конфигурации сети hello hello подсеть шлюза должен называться «GatewaySubnet» или Azure не удается распознать и использовать его как подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="ef695-158">When working with hello network configuration file, hello gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="ef695-159">**Пример**</span><span class="sxs-lookup"><span data-stu-id="ef695-159">**Example:**</span></span>

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a><span data-ttu-id="ef695-160">Часть 3 — Добавление hello сайта локальной сети</span><span class="sxs-lookup"><span data-stu-id="ef695-160">Part 3 - Add hello local network site</span></span>
<span data-ttu-id="ef695-161">Hello сайта локальной сети, добавляемые представляет hello требуется tooconnect toowhich RM виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-161">hello local network site you add represents hello RM VNet toowhich you want tooconnect.</span></span> <span data-ttu-id="ef695-162">Добавить **LocalNetworkSites** файл toohello элемента, если она еще не создана.</span><span class="sxs-lookup"><span data-stu-id="ef695-162">Add a **LocalNetworkSites** element toohello file if one doesn't already exist.</span></span> <span data-ttu-id="ef695-163">На этом этапе в конфигурации hello hello VPNGatewayAddress может быть любой допустимый общедоступный IP-адрес, так как мы еще не создали hello шлюз для hello диспетчера ресурсов виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-163">At this point in hello configuration, hello VPNGatewayAddress can be any valid public IP address because we haven't yet created hello gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="ef695-164">После создания шлюза hello, мы заменяем этот IP-адрес заполнителя hello открытый IP-адрес, которому назначен toohello RM шлюза.</span><span class="sxs-lookup"><span data-stu-id="ef695-164">Once we create hello gateway, we replace this placeholder IP address with hello correct public IP address that has been assigned toohello RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a><span data-ttu-id="ef695-165">Часть 4 - hello связывание виртуальной сети с сайта локальной сети hello</span><span class="sxs-lookup"><span data-stu-id="ef695-165">Part 4 - Associate hello VNet with hello local network site</span></span>
<span data-ttu-id="ef695-166">В этом разделе мы указываем hello сайта локальной сети, что требуется tooconnect виртуальной сети для hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-166">In this section, we specify hello local network site that you want tooconnect hello VNet to.</span></span> <span data-ttu-id="ef695-167">В этом случае это hello виртуальную сеть диспетчера ресурсов, ссылки на более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="ef695-167">In this case, it is hello Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="ef695-168">Убедитесь, что имена hello соответствует.</span><span class="sxs-lookup"><span data-stu-id="ef695-168">Make sure hello names match.</span></span> <span data-ttu-id="ef695-169">На этом этапе шлюз еще не создается.</span><span class="sxs-lookup"><span data-stu-id="ef695-169">This step does not create a gateway.</span></span> <span data-ttu-id="ef695-170">Он указывает, что hello локальной сети, hello шлюз будет подключаться к.</span><span class="sxs-lookup"><span data-stu-id="ef695-170">It specifies hello local network that hello gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a><span data-ttu-id="ef695-171">Часть 5 - сохранить файл hello и передачи</span><span class="sxs-lookup"><span data-stu-id="ef695-171">Part 5 - Save hello file and upload</span></span>
<span data-ttu-id="ef695-172">Сохраните файл hello, а затем импортировать его tooAzure, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-172">Save hello file, then import it tooAzure by running hello following command.</span></span> <span data-ttu-id="ef695-173">Убедитесь, что изменение пути файла hello, необходимые для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="ef695-173">Make sure you change hello file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="ef695-174">Вы увидите тот же результат, удовлетворены hello импорта.</span><span class="sxs-lookup"><span data-stu-id="ef695-174">You will see a similar result showing that hello import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a><span data-ttu-id="ef695-175">Часть 6 - Создание шлюза hello</span><span class="sxs-lookup"><span data-stu-id="ef695-175">Part 6 - Create hello gateway</span></span>

<span data-ttu-id="ef695-176">Перед запуском этого примера, см. toohello toosee ожидает, что файл конфигурации сети, загруженный для hello точные имена, которые платформа Azure.</span><span class="sxs-lookup"><span data-stu-id="ef695-176">Before running this example, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="ef695-177">файл конфигурации сети Hello содержит hello значения для классических виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="ef695-177">hello network configuration file contains hello values for your classic virtual networks.</span></span> <span data-ttu-id="ef695-178">Иногда hello имена для виртуальных сетей изменения в файле конфигурации сети hello при создании классического параметры виртуальной сети в классическом hello портал Azure, из-за различия toohello в модели развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-178">Sometimes hello names for classic VNets are changed in hello network configuration file when creating classic VNet settings in hello Azure portal due toohello differences in hello deployment models.</span></span> <span data-ttu-id="ef695-179">Например, при использовании Azure портала toocreate классической виртуальной сети с именем «Классической виртуальной сети» и он создан в группе ресурсов с именем «ClassicRG» hello, hello, содержащийся в файле конфигурации сети hello называется преобразованный too'Group ClassicRG классической виртуальной сети ".</span><span class="sxs-lookup"><span data-stu-id="ef695-179">For example, if you used hello Azure portal toocreate a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', hello name that is contained in hello network configuration file is converted too'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="ef695-180">При указании hello имя виртуальной сети, которая содержит пробелы, используйте кавычки вокруг значение hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-180">When specifying hello name of a VNet that contains spaces, use quotation marks around hello value.</span></span>


<span data-ttu-id="ef695-181">Используйте следующий пример toocreate шлюза с динамической маршрутизацией hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-181">Use hello following example toocreate a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="ef695-182">Можно проверить состояние hello hello шлюза с помощью hello **Get-AzureVNetGateway** командлета.</span><span class="sxs-lookup"><span data-stu-id="ef695-182">You can check hello status of hello gateway by using hello **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="ef695-183"><a name="creatermgw"></a>Раздел 2: Настройка шлюза виртуальной сети RM hello</span><span class="sxs-lookup"><span data-stu-id="ef695-183"><a name="creatermgw"></a>Section 2: Configure hello RM VNet gateway</span></span>
<span data-ttu-id="ef695-184">toocreate VPN-шлюз для hello RM виртуальной сети, следуйте инструкциям hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-184">toocreate a VPN gateway for hello RM VNet, follow hello following instructions.</span></span> <span data-ttu-id="ef695-185">Не начинайте hello действия до, после получения hello общедоступный IP-адрес для шлюза hello классической виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-185">Don't start hello steps until after you have retrieved hello public IP address for hello classic VNet's gateway.</span></span> 

1. <span data-ttu-id="ef695-186">Войдите в систему tooyour учетной записи Azure в консоли PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-186">Log in tooyour Azure account in hello PowerShell console.</span></span> <span data-ttu-id="ef695-187">Hello следующий командлет запросит hello учетные данные входа для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="ef695-187">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="ef695-188">После входа в систему, чтобы они были доступны tooAzure PowerShell, загружаются параметры учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ef695-188">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="ef695-189">Если у вас есть несколько подписок, запросите их список.</span><span class="sxs-lookup"><span data-stu-id="ef695-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="ef695-190">Укажите требуемый toouse подписки hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-190">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="ef695-191">Создайте локальный сетевой шлюз.</span><span class="sxs-lookup"><span data-stu-id="ef695-191">Create a local network gateway.</span></span> <span data-ttu-id="ef695-192">В виртуальной сети шлюз локальной сети hello обычно относится tooyour в локальном расположении.</span><span class="sxs-lookup"><span data-stu-id="ef695-192">In a virtual network, hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="ef695-193">В этом случае шлюз локальной сети hello указывает tooyour классической виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-193">In this case, hello local network gateway refers tooyour Classic VNet.</span></span> <span data-ttu-id="ef695-194">Присвойте ему имя, с помощью которого можно ссылаться tooit Azure, а также указать префикс пространства адресов hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-194">Give it a name by which Azure can refer tooit, and also specify hello address space prefix.</span></span> <span data-ttu-id="ef695-195">Azure использует префикс IP-адреса укажите tooidentify tooyour toosend какой трафик локального расположения hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-195">Azure uses hello IP address prefix you specify tooidentify which traffic toosend tooyour on-premises location.</span></span> <span data-ttu-id="ef695-196">Для получения tooadjust hello сведений здесь более поздней версии, перед созданием шлюза, можно изменить значения hello и образец hello выполнения снова.</span><span class="sxs-lookup"><span data-stu-id="ef695-196">If you need tooadjust hello information here later, before creating your gateway, you can modify hello values and run hello sample again.</span></span>
   
   <span data-ttu-id="ef695-197">**-Имя** является именем hello, требуется шлюз локальной сети toohello toorefer tooassign.</span><span class="sxs-lookup"><span data-stu-id="ef695-197">**-Name** is hello name you want tooassign toorefer toohello local network gateway.</span></span><br><span data-ttu-id="ef695-198">
   **-AddressPrefix** — hello адресное пространство для классической виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-198">
   **-AddressPrefix** is hello Address Space for your classic VNet.</span></span><br><span data-ttu-id="ef695-199">
**-GatewayIpAddress** — hello общедоступный IP-адрес шлюза hello классической виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-199">
**-GatewayIpAddress** is hello public IP address of hello classic VNet's gateway.</span></span> <span data-ttu-id="ef695-200">Убедитесь, что следующие hello toochange пример tooreflect hello правильный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="ef695-200">Be sure toochange hello following sample tooreflect hello correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="ef695-201">Запрос открытый IP адрес toobe toohello выделенный шлюз виртуальной сети для hello диспетчера ресурсов виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-201">Request a public IP address toobe allocated toohello virtual network gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="ef695-202">Нельзя указать hello IP-адреса, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="ef695-202">You can't specify hello IP address that you want toouse.</span></span> <span data-ttu-id="ef695-203">шлюз виртуальной сети toohello выделяется динамически Hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="ef695-203">hello IP address is dynamically allocated toohello virtual network gateway.</span></span> <span data-ttu-id="ef695-204">Однако это не означает hello изменения IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="ef695-204">However, this does not mean hello IP address changes.</span></span> <span data-ttu-id="ef695-205">Hello только время изменения IP-адреса шлюза виртуальной сети hello когда hello шлюза будет удалено и создано заново.</span><span class="sxs-lookup"><span data-stu-id="ef695-205">hello only time hello virtual network gateway IP address changes is when hello gateway is deleted and recreated.</span></span> <span data-ttu-id="ef695-206">Изменение размера, сброс или другие внутренние обслуживания или обновления шлюза hello не будет изменена.</span><span class="sxs-lookup"><span data-stu-id="ef695-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of hello gateway.</span></span>

  <span data-ttu-id="ef695-207">На этом этапе также задается переменная, которая будет использоваться позже.</span><span class="sxs-lookup"><span data-stu-id="ef695-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="ef695-208">Проверьте наличие подсети шлюза в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="ef695-209">Если подсети шлюза нет, добавьте ее.</span><span class="sxs-lookup"><span data-stu-id="ef695-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="ef695-210">Убедитесь, что подсеть шлюза hello называется *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="ef695-210">Make sure hello gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="ef695-211">Получить подсеть hello, используемая для шлюза hello, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-211">Retrieve hello subnet used for hello gateway by running hello following command.</span></span> <span data-ttu-id="ef695-212">На этом шаге мы также настроить переменной toobe используется в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-212">In this step, we also set a variable toobe used in hello next step.</span></span>
   
   <span data-ttu-id="ef695-213">**-Имя** hello имя виртуальной сети диспетчер ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ef695-213">**-Name** is hello name of your Resource Manager VNet.</span></span><br><span data-ttu-id="ef695-214">
   **-ResourceGroupName** является группой ресурсов hello, hello, связанный с виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-214">
**-ResourceGroupName** is hello resource group that hello VNet is associated with.</span></span> <span data-ttu-id="ef695-215">подсеть шлюза Hello уже должен существовать для этой виртуальной сети и должен называться *GatewaySubnet* toowork должным образом.</span><span class="sxs-lookup"><span data-stu-id="ef695-215">hello gateway subnet must already exist for this VNet and must be named *GatewaySubnet* toowork properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="ef695-216">Создайте адресации конфигурации IP-адрес шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-216">Create hello gateway IP addressing configuration.</span></span> <span data-ttu-id="ef695-217">Конфигурация шлюза Hello определяет подсеть hello и hello открытый IP адрес toouse.</span><span class="sxs-lookup"><span data-stu-id="ef695-217">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="ef695-218">Используйте следующие toocreate образец hello конфигурацию шлюза.</span><span class="sxs-lookup"><span data-stu-id="ef695-218">Use hello following sample toocreate your gateway configuration.</span></span>

  <span data-ttu-id="ef695-219">На этом шаге hello **- SubnetId** и **- PublicIpAddressId** параметры должны передаваться свойства id hello hello подсети и IP адрес объектов, соответственно.</span><span class="sxs-lookup"><span data-stu-id="ef695-219">In this step, hello **-SubnetId** and **-PublicIpAddressId** parameters must be passed hello id property from hello subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="ef695-220">Нельзя использовать простую строку.</span><span class="sxs-lookup"><span data-stu-id="ef695-220">You can't use a simple string.</span></span> <span data-ttu-id="ef695-221">Эти переменные задаются в toorequest шаг hello общедоступный IP-адрес и hello шаг tooretrieve hello подсети.</span><span class="sxs-lookup"><span data-stu-id="ef695-221">These variables are set in hello step toorequest a public IP and hello step tooretrieve hello subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="ef695-222">Создание шлюза виртуальной сети hello диспетчера ресурсов, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-222">Create hello Resource Manager virtual network gateway by running hello following command.</span></span> <span data-ttu-id="ef695-223">Hello `-VpnType` должно быть *routebased*.</span><span class="sxs-lookup"><span data-stu-id="ef695-223">hello `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="ef695-224">Может потребоваться 45 минут или больше toocreate hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="ef695-224">It can take 45 minutes or more for hello gateway toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="ef695-225">Скопируйте hello общедоступный IP-адрес после создания VPN-шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-225">Copy hello public IP address once hello VPN gateway has been created.</span></span> <span data-ttu-id="ef695-226">Используется при настройке параметров локальной сети hello для классической виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-226">You use it when you configure hello local network settings for your Classic VNet.</span></span> <span data-ttu-id="ef695-227">Можно использовать следующий командлет tooretrieve hello открытый IP-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-227">You can use hello following cmdlet tooretrieve hello public IP address.</span></span> <span data-ttu-id="ef695-228">Hello общедоступный IP-адрес указан в hello, возвращаемое как *IP-адрес*.</span><span class="sxs-lookup"><span data-stu-id="ef695-228">hello public IP address is listed in hello return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a><span data-ttu-id="ef695-229">Раздел 3: Изменение hello классический параметрами локального сайта виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="ef695-229">Section 3: Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="ef695-230">В этом разделе, работать с hello классической виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-230">In this section, you work with hello classic VNet.</span></span> <span data-ttu-id="ef695-231">Можно заменить hello заполнитель IP-адрес, который использовался при указании параметров hello локального сайта, которая будет toohello tooconnect используется шлюз виртуальной сети диспетчер ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ef695-231">You replace hello placeholder IP address that you used when specifying hello local site settings that will be used tooconnect toohello Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="ef695-232">Экспортируйте файл конфигурации сети hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-232">Export hello network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="ef695-233">В текстовом редакторе, измените значение hello для VPNGatewayAddress.</span><span class="sxs-lookup"><span data-stu-id="ef695-233">Using a text editor, modify hello value for VPNGatewayAddress.</span></span> <span data-ttu-id="ef695-234">Замените IP-адрес заполнителя hello hello общедоступный IP-адрес шлюза hello диспетчера ресурсов, а затем сохраните изменения hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-234">Replace hello placeholder IP address with hello public IP address of hello Resource Manager gateway and then save hello changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="ef695-235">Импорт hello изменить tooAzure файла конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="ef695-235">Import hello modified network configuration file tooAzure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="ef695-236"><a name="connect"></a>Раздел 4: Создайте подключение между шлюзами hello</span><span class="sxs-lookup"><span data-stu-id="ef695-236"><a name="connect"></a>Section 4: Create a connection between hello gateways</span></span>
<span data-ttu-id="ef695-237">Создание подключения между шлюзами hello требуется PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef695-237">Creating a connection between hello gateways requires PowerShell.</span></span> <span data-ttu-id="ef695-238">Может потребоваться tooadd вашей учетной записи Azure toouse hello классической версии hello командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef695-238">You may need tooadd your Azure Account toouse hello classic version of hello  PowerShell cmdlets.</span></span> <span data-ttu-id="ef695-239">Таким образом, используйте toodo **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="ef695-239">toodo so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="ef695-240">В консоли PowerShell hello задайте общий ключ.</span><span class="sxs-lookup"><span data-stu-id="ef695-240">In hello PowerShell console, set your shared key.</span></span> <span data-ttu-id="ef695-241">Перед выполнением командлетов hello, ссылаться toohello toosee ожидает, что файл конфигурации сети, загруженный для hello точные имена, которые платформа Azure.</span><span class="sxs-lookup"><span data-stu-id="ef695-241">Before running hello cmdlets, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="ef695-242">При указании hello имя виртуальной сети, которая содержит пробелы, используйте одинарные кавычки значение hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-242">When specifying hello name of a VNet that contains spaces, use single quotation marks around hello value.</span></span><br><br><span data-ttu-id="ef695-243">В следующем примере **- VNetName** — имя hello hello классической виртуальной сети и **- LocalNetworkSiteName** hello имя сайта локальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-243">In following example, **-VNetName** is hello name of hello classic VNet and **-LocalNetworkSiteName** is hello name you specified for hello local network site.</span></span> <span data-ttu-id="ef695-244">Hello **- SharedKey** создать и задать значение.</span><span class="sxs-lookup"><span data-stu-id="ef695-244">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="ef695-245">В примере hello мы использовали «abc123», но вы можете создавать и использовать более сложной.</span><span class="sxs-lookup"><span data-stu-id="ef695-245">In hello example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="ef695-246">Hello, важно, что очередь является то значение hello, здесь должно быть приветствия одинаковое значение указывается в hello следующий шаг при создании подключения.</span><span class="sxs-lookup"><span data-stu-id="ef695-246">hello important thing is that hello value you specify here must be hello same value that you specify in hello next step when you create your connection.</span></span> <span data-ttu-id="ef695-247">должно отображаться Hello возвращаемого **состояния: успешно**.</span><span class="sxs-lookup"><span data-stu-id="ef695-247">hello return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="ef695-248">Создайте hello VPN-подключение, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="ef695-248">Create hello VPN connection by running hello following commands:</span></span>
   
  <span data-ttu-id="ef695-249">Установка переменных hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-249">Set hello variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="ef695-250">Создание подключения hello.</span><span class="sxs-lookup"><span data-stu-id="ef695-250">Create hello connection.</span></span> <span data-ttu-id="ef695-251">Обратите внимание, что hello **- ConnectionType** — IPsec не Vnet2Vnet.</span><span class="sxs-lookup"><span data-stu-id="ef695-251">Notice that hello **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="ef695-252">Раздел 5. Проверка подключений</span><span class="sxs-lookup"><span data-stu-id="ef695-252">Section 5: Verify your connections</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="ef695-253">tooverify hello подключения из вашей классической виртуальной сети tooyour диспетчера ресурсов виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="ef695-253">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="ef695-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef695-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="ef695-255">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ef695-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="ef695-256">tooverify hello подключения из вашей виртуальной сети диспетчер ресурсов tooyour классической виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="ef695-256">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="ef695-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef695-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="ef695-258">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ef695-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="ef695-259"><a name="faq"></a>Часто задаваемые вопросы о подключениях типа "виртуальная сеть — виртуальная сеть"</span><span class="sxs-lookup"><span data-stu-id="ef695-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

