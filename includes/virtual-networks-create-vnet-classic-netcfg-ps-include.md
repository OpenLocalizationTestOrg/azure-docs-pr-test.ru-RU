## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="be99a-101">Как toocreate виртуальной сети, используя файл конфигурации сети файла из PowerShell</span><span class="sxs-lookup"><span data-stu-id="be99a-101">How toocreate a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="be99a-102">Azure использует файл xml toodefine все подписки доступны tooa виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="be99a-102">Azure uses an xml file toodefine all virtual networks available tooa subscription.</span></span> <span data-ttu-id="be99a-103">Можно загрузить этот файл, изменить его toomodify или удалить существующие виртуальные сети и создания новых виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="be99a-103">You can download this file, edit it toomodify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="be99a-104">В этом учебнике вы узнаете, как toodownload этот файл называется tooas сетевой файл конфигурации (или netcfg) и изменить его toocreate новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="be99a-104">In this tutorial, you learn how toodownload this file, referred tooas network configuration (or netcfg) file, and edit it toocreate a new virtual network.</span></span> <span data-ttu-id="be99a-105">toolearn Дополнительные сведения о hello файла конфигурации сети, в разделе hello [схема конфигурации виртуальной сети Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="be99a-105">toolearn more about hello network configuration file, see hello [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="be99a-106">toocreate виртуальной сети с помощью файла netcfg, с помощью PowerShell, полные hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="be99a-106">toocreate a virtual network with a netcfg file using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="be99a-107">Если ранее не пользовались Azure PowerShell, hello завершения шагов в hello [как tooInstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) статьи, а затем войдите в tooAzure и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="be99a-107">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in tooAzure and select your subscription.</span></span>
2. <span data-ttu-id="be99a-108">В консоли Azure PowerShell hello, используйте hello **Get AzureVnetConfig** командлет toodownload hello сетевой конфигурации файла tooa каталог на компьютере, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="be99a-108">From hello Azure PowerShell console, use hello **Get-AzureVnetConfig** cmdlet toodownload hello network configuration file tooa directory on your computer by running hello following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="be99a-109">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="be99a-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="be99a-110">Откройте файл hello, сохраненный на шаге 2, с помощью любого приложения редактор текста или XML и найдите hello  **<VirtualNetworkSites>**  элемента.</span><span class="sxs-lookup"><span data-stu-id="be99a-110">Open hello file you saved in step 2 using any XML or text editor application, and look for hello **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="be99a-111">Если вы уже создавали сети, для каждой сети будет указан ее собственный элемент **<VirtualNetworkSite>**.</span><span class="sxs-lookup"><span data-stu-id="be99a-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="be99a-112">toocreate hello виртуальной сети в этом сценарии, добавьте следующий XML-код сразу под hello hello  **<VirtualNetworkSites>**  элемента:</span><span class="sxs-lookup"><span data-stu-id="be99a-112">toocreate hello virtual network described in this scenario, add hello following XML just under hello **<VirtualNetworkSites>** element:</span></span>

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. <span data-ttu-id="be99a-113">Сохраните файл конфигурации сети hello.</span><span class="sxs-lookup"><span data-stu-id="be99a-113">Save hello network configuration file.</span></span>
6. <span data-ttu-id="be99a-114">В консоли Azure PowerShell hello, используйте hello **AzureVnetConfig набор** файла конфигурации сети hello tooupload командлета, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="be99a-114">From hello Azure PowerShell console, use hello **Set-AzureVnetConfig** cmdlet tooupload hello network configuration file by running hello following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="be99a-115">Возвращаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="be99a-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="be99a-116">Если **OperationStatus** не *успешно* в hello возвращаемые выходные данные, проверьте hello XML-файла для ошибок и завершении шага 6 еще раз.</span><span class="sxs-lookup"><span data-stu-id="be99a-116">If **OperationStatus** is not *Succeeded* in hello returned output, check hello xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="be99a-117">В консоли Azure PowerShell hello, используйте hello **Get AzureVnetSite** tooverify командлета, hello новую сеть была добавлена, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="be99a-117">From hello Azure PowerShell console, use hello **Get-AzureVnetSite** cmdlet tooverify that hello new network was added by running hello following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="be99a-118">Hello возвращено (сокращенный) выходные данные содержат hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="be99a-118">hello returned (abbreviated) output includes hello following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
