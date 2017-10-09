Hello [библиотека Configuration Manager Microsoft Azure для .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) предоставляет класс для обработки строки соединения из файла конфигурации. Hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) класс выполняет синтаксический анализ параметров конфигурации независимо от того, выполняется ли клиентское приложение hello на столе hello на мобильном устройстве, в виртуальной машине Azure или в облачной службе Azure.

tooreference Здравствуйте CloudConfigurationManager пакет, добавьте следующее hello `using` директиву:

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

Ниже приведен пример, в котором показано, как tooretrieve строка соединения из файла конфигурации:

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

С помощью hello Azure Configuration Manager является необязательным. Можно также использовать API-Интерфейс, как .NET Framework hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) класса.

