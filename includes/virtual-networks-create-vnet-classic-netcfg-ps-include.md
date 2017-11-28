## <a name="how-to-create-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="c2181-101">Как создать виртуальную сеть с помощью файла конфигурации сети в PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2181-101">How to create a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="c2181-102">В Azure для определения всех виртуальных сетей, доступных для подписки, используется XML-файл.</span><span class="sxs-lookup"><span data-stu-id="c2181-102">Azure uses an xml file to define all virtual networks available to a subscription.</span></span> <span data-ttu-id="c2181-103">Вы можете скачать этот файл и внести в него изменения, чтобы изменить или удалить существующие виртуальные сети и создать новые.</span><span class="sxs-lookup"><span data-stu-id="c2181-103">You can download this file, edit it to modify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="c2181-104">Из этого руководства вы узнаете, как скачать этот файл, который называется файлом конфигурации сети (или NETCGF), и внести в него изменения для создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c2181-104">In this tutorial, you learn how to download this file, referred to as network configuration (or netcfg) file, and edit it to create a new virtual network.</span></span> <span data-ttu-id="c2181-105">Дополнительные сведения о файле конфигурации сети см. в статье [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx) (Схема конфигурации виртуальной сети Azure).</span><span class="sxs-lookup"><span data-stu-id="c2181-105">To learn more about the network configuration file, see the [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="c2181-106">Чтобы создать виртуальную сеть в PowerShell, используя файл NETCGF, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c2181-106">To create a virtual network with a netcfg file using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="c2181-107">Если вы ранее не использовали Azure PowerShell, выполните действия по [установке и настройке Azure PowerShell](/powershell/azureps-cmdlets-docs). Затем войдите в учетную запись Azure и выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="c2181-107">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in to Azure and select your subscription.</span></span>
2. <span data-ttu-id="c2181-108">В консоли Azure PowerShell воспользуйтесь командлетом **Get-AzureVnetConfig**, чтобы скачать файл конфигурации сети в каталог на компьютере, выполнив указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c2181-108">From the Azure PowerShell console, use the **Get-AzureVnetConfig** cmdlet to download the network configuration file to a directory on your computer by running the following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="c2181-109">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c2181-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="c2181-110">Откройте файл, сохраненный при выполнении шага 2, в любом XML- или текстовом редакторе и найдите элемент **<VirtualNetworkSites>**.</span><span class="sxs-lookup"><span data-stu-id="c2181-110">Open the file you saved in step 2 using any XML or text editor application, and look for the **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="c2181-111">Если вы уже создавали сети, для каждой сети будет указан ее собственный элемент **<VirtualNetworkSite>**.</span><span class="sxs-lookup"><span data-stu-id="c2181-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="c2181-112">Для создания виртуальной сети, описанной в этом сценарии, добавьте следующий XML-код сразу после элемента **<VirtualNetworkSites>** :</span><span class="sxs-lookup"><span data-stu-id="c2181-112">To create the virtual network described in this scenario, add the following XML just under the **<VirtualNetworkSites>** element:</span></span>

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
   
5. <span data-ttu-id="c2181-113">Сохраните файл конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="c2181-113">Save the network configuration file.</span></span>
6. <span data-ttu-id="c2181-114">В консоли Azure PowerShell воспользуйтесь командлетом **Set-AzureVnetConfig**, чтобы отправить файл конфигурации сети, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2181-114">From the Azure PowerShell console, use the **Set-AzureVnetConfig** cmdlet to upload the network configuration file by running the following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="c2181-115">Возвращаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c2181-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="c2181-116">Если в возвращаемых выходных данных значение параметра **OperationStatus** отлично от *Succeeded*, проверьте XML-файл на наличие ошибок и повторите шаг 6.</span><span class="sxs-lookup"><span data-stu-id="c2181-116">If **OperationStatus** is not *Succeeded* in the returned output, check the xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="c2181-117">В консоли Azure PowerShell воспользуйтесь командлетом **Get AzureVnetSite**, чтобы убедиться в том, что новая сеть добавлена, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2181-117">From the Azure PowerShell console, use the **Get-AzureVnetSite** cmdlet to verify that the new network was added by running the following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="c2181-118">Возвращаемые выходные данные (сокращенные) содержат следующий текст:</span><span class="sxs-lookup"><span data-stu-id="c2181-118">The returned (abbreviated) output includes the following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
