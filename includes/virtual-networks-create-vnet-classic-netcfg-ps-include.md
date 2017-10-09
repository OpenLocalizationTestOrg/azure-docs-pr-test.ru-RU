## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a>Как toocreate виртуальной сети, используя файл конфигурации сети файла из PowerShell
Azure использует файл xml toodefine все подписки доступны tooa виртуальных сетей. Можно загрузить этот файл, изменить его toomodify или удалить существующие виртуальные сети и создания новых виртуальных сетей. В этом учебнике вы узнаете, как toodownload этот файл называется tooas сетевой файл конфигурации (или netcfg) и изменить его toocreate новую виртуальную сеть. toolearn Дополнительные сведения о hello файла конфигурации сети, в разделе hello [схема конфигурации виртуальной сети Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).

toocreate виртуальной сети с помощью файла netcfg, с помощью PowerShell, полные hello, следующие шаги:

1. Если ранее не пользовались Azure PowerShell, hello завершения шагов в hello [как tooInstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) статьи, а затем войдите в tooAzure и выберите свою подписку.
2. В консоли Azure PowerShell hello, используйте hello **Get AzureVnetConfig** командлет toodownload hello сетевой конфигурации файла tooa каталог на компьютере, выполнив следующую команду hello: 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   Ожидаемые выходные данные:
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. Откройте файл hello, сохраненный на шаге 2, с помощью любого приложения редактор текста или XML и найдите hello  **<VirtualNetworkSites>**  элемента. Если вы уже создавали сети, для каждой сети будет указан ее собственный элемент **<VirtualNetworkSite>**.
4. toocreate hello виртуальной сети в этом сценарии, добавьте следующий XML-код сразу под hello hello  **<VirtualNetworkSites>**  элемента:

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
   
5. Сохраните файл конфигурации сети hello.
6. В консоли Azure PowerShell hello, используйте hello **AzureVnetConfig набор** файла конфигурации сети hello tooupload командлета, выполнив следующую команду hello: 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   Возвращаемые выходные данные:
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   Если **OperationStatus** не *успешно* в hello возвращаемые выходные данные, проверьте hello XML-файла для ошибок и завершении шага 6 еще раз.

7. В консоли Azure PowerShell hello, используйте hello **Get AzureVnetSite** tooverify командлета, hello новую сеть была добавлена, выполнив следующую команду hello: 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   Hello возвращено (сокращенный) выходные данные содержат hello следующий текст:
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
