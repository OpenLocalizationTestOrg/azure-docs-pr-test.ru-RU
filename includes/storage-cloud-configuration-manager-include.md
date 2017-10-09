<span data-ttu-id="8da93-101">Hello [библиотека Configuration Manager Microsoft Azure для .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) предоставляет класс для обработки строки соединения из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8da93-101">hello [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="8da93-102">Hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) класс выполняет синтаксический анализ параметров конфигурации независимо от того, выполняется ли клиентское приложение hello на столе hello на мобильном устройстве, в виртуальной машине Azure или в облачной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="8da93-102">hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether hello client application is running on hello desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="8da93-103">tooreference Здравствуйте CloudConfigurationManager пакет, добавьте следующее hello `using` директиву:</span><span class="sxs-lookup"><span data-stu-id="8da93-103">tooreference hello CloudConfigurationManager package, add hello following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="8da93-104">Ниже приведен пример, в котором показано, как tooretrieve строка соединения из файла конфигурации:</span><span class="sxs-lookup"><span data-stu-id="8da93-104">Here's an example that shows how tooretrieve a connection string from a configuration file:</span></span>

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="8da93-105">С помощью hello Azure Configuration Manager является необязательным.</span><span class="sxs-lookup"><span data-stu-id="8da93-105">Using hello Azure Configuration Manager is optional.</span></span> <span data-ttu-id="8da93-106">Можно также использовать API-Интерфейс, как .NET Framework hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) класса.</span><span class="sxs-lookup"><span data-stu-id="8da93-106">You can also use an API like hello .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

