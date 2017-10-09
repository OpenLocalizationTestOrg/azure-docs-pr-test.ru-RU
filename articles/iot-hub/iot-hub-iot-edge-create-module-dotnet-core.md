---
title: "aaaCreate модуль Edge IoT Azure с помощью C# | Документы Microsoft"
description: "Этот учебник демонстрирует, как отключить данных преобразователь модуля с помощью toowrite hello последние пакеты Azure IoT Edge NuGet кода Visual Studio и C#."
services: iot-hub
author: jeffreyCline
manager: timlt
keywords: "azure, iot, руководство, модуль, nuget, vscode, csharp, edge"
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: jcline
ms.openlocfilehash: b104609c05d1613e21acc7d7bed547f311179151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a>Создание модуля Azure IoT Edge с помощью C&#x23;

Этот учебник демонстрирует способ toocreate какой-либо модуль для `Azure IoT Edge` с помощью `Visual Studio Code` и `C#`.

В этом учебнике мы будем рассматривать настройки среды и как toowrite [ЛЮЧИТЬ](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) модуля преобразователя данных с помощью последней hello `Azure IoT Edge NuGet` пакетов. 

>[!NOTE]
Этот учебник использует hello `.NET Core SDK`, который поддерживает кросс платформенной совместимости. Hello следующий учебник записывается с помощью hello `Windows 10` операционной системы. Некоторые команды hello в этом учебнике может отличаться в зависимости от вашей `development environment`. 

## <a name="prerequisites"></a>Предварительные требования

В этом разделе настраивается среда для разработки модуля `Azure IoT Edge`. Оно применяется tooboth **64-разрядной версии Windows** и **64-разрядных Linux (8 Ubuntu/Debian)** операционных систем.

Привет, следуя программного обеспечения не требуется:

- [клиент Git](https://git-scm.com/downloads);
- [Базовый пакет SDK для .NET](https://www.microsoft.com/net/core#windowscmd)
- [Visual Studio Code](https://code.visualstudio.com/)

Tooclone hello репозитория для данного образца не требуется, однако все hello пример кода, рассматриваемые в этом учебнике расположен в следующих репозитория hello:

- `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a>Приступая к работе

1. Установите `.NET Core SDK`.
2. Установка `Visual Studio Code` и hello `C# extension` из Visual Studio Marketplace кода hello.

Просмотр этой [краткий учебник видео](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) о том, как tooget приступить к работе с помощью `Visual Studio Code` и hello `.NET Core SDK`.

## <a name="creating-hello-azure-iot-edge-converter-module"></a>Создание модуля преобразователя hello Azure IoT Edge

1. Инициализируйте новый проект C# библиотеки классов `.NET Core`:
    - Откройте командную строку (`Windows + R` -> `cmd` -> `enter`).
    - Перейдите в папку toohello, куда toocreate hello `C#` проекта.
    - Введите **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**. 
    - Эта команда создает в каталоге проектов пустой класс с именем `Class1.cs`.
2. Перейдите в папку toohello, где только что созданный проект библиотеки классов hello, введя **cd IoTEdgeConverterModule**.
3. Привет открыть проект в `Visual Studio Code` , введя **кода.**.
4. После открытия проекта hello в `Visual Studio Code`, щелкните hello **IoTEdgeConverterModule.csproj** tooopen hello файла, как показано в hello после изображения:

    ![Окно редактирования Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. Вставка hello `XML` большого двоичного объекта в следующий фрагмент кода между закрывающей hello hello `PropertyGroup` теги и hello закрытие `Project` тега; строка шесть hello предшествующий изображение и сохраните файл hello, нажав клавишу `Ctrl`  +  `S`.

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. После сохранения hello `.csproj` файл `Visual Studio Code` должна вывести запрос с `unresolved dependencies` диалогового окна, как показано в hello после изображения: 

    ![Диалоговое окно восстановления зависимостей Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    ) нажмите кнопку `Restore` toorestore все hello ссылок в проектах hello `.csproj` файла, включая hello `PackageReferences` добавлена. 

    (б) `Visual Studio Code` автоматически создает hello `project.assets.json` файла в проектах `obj` папки. Этот файл содержит сведения о проекте зависимости toomake последующие операции восстановления быстрее.
 
    >[!NOTE]
    `.NET Core Tools` теперь основаны на MSBuild. Это означает, что вместо файла `project.json` создается файл `.csproj` проекта.

    - Если `Visual Studio Code` не отображает запрос, то это не проблема, так как эти действия можно выполнить вручную. Откройте hello `Visual Studio Code` интеграции окно терминала, нажав клавишу hello `Ctrl`  +  `backtick` ключей или с помощью меню hello `View`  ->  `Integrated Terminal`.
    - В hello `Integrated Terminal` тип окна **восстановления dotnet**.
    
7. Переименование hello `Class1.cs` файла слишком`BleConverterModule.cs`. 

    ) файл hello toorename сначала щелкните на файле hello нажмите клавишу hello `F2` ключа.
    
    b) введите новое имя hello **BleConverterModule**, как показано в hello после изображения:

    ![Переименование класса в Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. Замените существующий код hello в hello `BleConverterModule.cs` файл путем копирования и вставки hello, следующий фрагмент кода в ваш `BleConverterModule.cs` файла.

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Globalization;
   using System.Linq;
   using System.Text;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace IoTEdgeConverterModule
   {
       public class BleConverterModule : IGatewayModule, IGatewayModuleStart
       {
           private Broker broker;
           private string configuration;
           private int messageCount;

           public void Create(Broker broker, byte[] configuration)
           {
               this.broker = broker;
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Start()
           {
           }

           public void Destroy()
           {
           }

           public void Receive(Message received_message)
           {
               string recMsg = Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               BleData receivedData = JsonConvert.DeserializeObject<BleData>(recMsg);

               float temperature = float.Parse(receivedData.Temperature, CultureInfo.InvariantCulture.NumberFormat); 
               Dictionary<string, string> receivedProperties = received_message.Properties;
            
               Dictionary<string, string> properties = new Dictionary<string, string>();
               properties.Add("source", receivedProperties["source"]);
               properties.Add("macAddress", receivedProperties["macAddress"]);
               properties.Add("temperatureAlert", temperature > 30 ? "true" : "false");
   
               String content = String.Format("{0} \"deviceId\": \"Intel NUC Gateway\", \"messageId\": {1}, \"temperature\": {2} {3}", "{", ++this.messageCount, temperature, "}");
               Message messageToPublish = new Message(content, properties);
   
               this.broker.Publish(messageToPublish);
           }
       }
   }
   ```

9. Сохраните файл hello, нажав клавишу `Ctrl`  +  `S`.

10. Создайте новый файл с именем `Untitled-1` , нажав клавишу hello `Ctrl`  +  `N` ключи, как показано в hello после изображения:

    ![Новый файл Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. toodeserialize hello `JSON` объекта, которые мы получаем от hello имитировать `BLE` устройства, следующий код в hello hello копирования `Untitled-1` окне редактора кода в файл. 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace IoTEdgeConverterModule
   {
       public class BleData
       {
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

12. Сохраните файл как файл hello `BleData.cs` , нажав клавишу `Ctrl`  +  `Shift`  +  `S` ключей.
    - На hello Сохранить как диалоговое окно, в hello `Save as Type` раскрывающееся меню, выберите `C# (*.cs;*.csx)` в hello после изображения:

    ![Диалоговое окно "Сохранить как" Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. Создайте новый файл с именем `Untitled-1` , нажав клавишу hello `Ctrl`  +  `N` ключей.

14. Скопируйте и вставьте следующий фрагмент кода в hello hello `Untitled-1` файла. Этот класс является `Azure IoT Edge` модуль, который мы используем данные toooutput hello, полученных от наших `BleConverterModule`.

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace PrinterModule
   {
       public class DotNetPrinterModule : IGatewayModule
       {
           private string configuration;
           public void Create(Broker broker, byte[] configuration)
           {
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Destroy()
           {
           }
   
           public void Receive(Message received_message)
           {
               string recMsg = System.Text.Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               Dictionary<string, string> receivedProperties = received_message.Properties;
               
               BleConverterData receivedData = JsonConvert.DeserializeObject<BleConverterData>(recMsg);
   
               Console.WriteLine();
               Console.WriteLine("Module           : [DotNetPrinterModule]");
               Console.WriteLine("received_message : {0}", recMsg);
   
               if(received_message.Properties["source"] == "bleTelemetry")
               {
                   Console.WriteLine("Source           : {0}", receivedProperties["source"]);
                   Console.WriteLine("MAC address      : {0}", receivedProperties["macAddress"]);
                   Console.WriteLine("Temperature Alert: {0}", receivedProperties["temperatureAlert"]);
                   Console.WriteLine("Deserialized Obj : [BleConverterData]");
                   Console.WriteLine("  DeviceId       : {0}", receivedData.DeviceId);
                   Console.WriteLine("  MessageId      : {0}", receivedData.MessageId);
                   Console.WriteLine("  Temperature    : {0}", receivedData.Temperature);
               }
   
               Console.WriteLine();
           }
       }
   }
   ```

15. Сохраните файл как файл hello `DotNetPrinterModule.cs` , нажав клавишу `Ctrl`  +  `Shift`  +  `S`.
    - На hello Сохранить как диалоговое окно, в hello `Save as Type` раскрывающееся меню, выберите `C# (*.cs;*.csx)`.

16. Создайте новый файл с именем `Untitled-1` , нажав клавишу hello `Ctrl`  +  `N` ключей.

17. toodeserialize hello `JSON` объектов, которые мы получаем от hello `BleConverterModule`, копировать и вставить hello следующий фрагмент кода hello `Untitled-1` файла. 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace PrinterModule
   {
       public class BleConverterData
       {
           [JsonProperty(PropertyName = "deviceId")]
           public string DeviceId { get; set; }
   
           [JsonProperty(PropertyName = "messageId")]
           public string MessageId { get; set; }
   
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

18. Сохраните файл как файл hello `BleConverterData.cs` , нажав клавишу `Ctrl`  +  `Shift`  +  `S`.
    - На hello Сохранить как диалоговое окно, в hello `Save as Type` раскрывающееся меню, выберите `C# (*.cs;*.csx)`.

19. Создайте новый файл с именем `Untitled-1` , нажав клавишу hello `Ctrl`  +  `N` ключей.

20. Скопируйте и вставьте следующий фрагмент кода в hello hello `Untitled-1` файла.

   ```json
   {
       "loaders": [
           {
               "type": "dotnetcore",
               "name": "dotnetcore",
               "configuration": {
                   "binding.path": "dotnetcore.dll",
                   "binding.coreclrpath": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\coreclr.dll",
                   "binding.trustedplatformassemblieslocation": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\"
               }
           }
       ],
          "modules": [
           {
               "name": "simulated_device",
               "loader": {
                   "name": "native",
                   "entrypoint": {
                       "module.path": "simulated_device.dll"
                   }
               },
               "args": {
                   "macAddress": "01:02:03:03:02:01",
                   "messagePeriod": 500
               }
           },
           {
               "name": "ble_converter_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "IoTEdgeConverterModule.BleConverterModule"
                   }
               },
               "args": ""
           },
           {
               "name": "printer_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "PrinterModule.DotNetPrinterModule"
                   }
               },
               "args": ""
           }
       ],
       "links": [
           {
               "source": "simulated_device", "sink": "ble_converter_module"
           },
           {
               "source": "ble_converter_module", "sink": "printer_module"
           }
   ]
   }
   ```

21. Сохраните файл как файл hello `gw-config.json` , нажав клавишу `Ctrl`  +  `Shift`  +  `S`.
    - На hello Сохранить как диалоговое окно, в hello `Save as Type` раскрывающееся меню, выберите `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.

22. копирование tooenable toohello файл конфигурации hello выходного каталога, обновления hello `IoTEdgeConverterModule.csproj` с hello после двоичных данных XML:

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - Обновить Hello `IoTEdgeConverterModule.csproj` следует выглядят hello следующие изображения:

    ![Обновленный CSPROJ-файл Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. Создайте новый файл с именем `Untitled-1` , нажав клавишу hello `Ctrl`  +  `N` ключей.

24. Скопируйте и вставьте следующий фрагмент кода в hello hello `Untitled-1` файла.

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. Сохраните файл как файл hello `binplace.ps1` , нажав клавишу `Ctrl`  +  `Shift`  +  `S`.
    - На hello Сохранить как диалоговое окно, в hello `Save as Type` раскрывающееся меню, выберите `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.

26. Выполните построение проекта hello, нажав клавишу hello `Ctrl`  +  `Shift`  +  `B` ключей. При построении проекта hello для hello первый раз `Visual Studio Code` , предлагающее hello `No build task defined.` диалогового окна, как показано в hello после изображения:

    ![Диалоговое окно задачи сборки Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    ) щелкните hello `Configure Build Task` кнопки.

    (б) в hello `Select a Task Runner` раскрывающегося меню диалогового окна. Выберите `.NET Core` как видно в hello после изображения: 

    ![Диалоговое окно выбора задачи Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    по щелчку c) hello `.NET Core` hello создает элемент `tasks.json` файла в вашей `.vscode` каталога и открывает файл в hello Здравствуйте, `code editor` окна. Нет этого файла hello закрыть вкладку toomodify нет необходимости.

27.  Откройте hello `Visual Studio Code` интеграции окно терминала, нажав клавишу hello `Ctrl`  +  `backtick` ключей или с помощью меню hello `View`  ->  `Integrated Terminal` и тип **.\binplace.ps1**в hello `PowerShell` командной строки. Эта команда копирует все наши зависимости toohello выходной каталог.

28. Перейдите в выходной каталог проекты toohello hello `Integrated Terminal` окна, введя **cd.\bin\Debug\netstandard1.3**.

29. Запустите проект образец hello, введя **. \gw.exe gw-config.json** в hello `Integrated Terminal` строке окна. 
    - Если вы следовали hello шаги в этом учебнике точно, вы должны выполняться hello `Azure IoT Edge BLE Data Converter Module` образец проекта, как показано в hello после изображения:
    
        ![Пример имитации устройства, запущенный в Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - Приложение hello tooterminate, нажмите клавишу hello `<Enter>` ключа.

>[!IMPORTANT]
Не рекомендуется toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` шлюза приложений (то есть **gw.exe**). Это действие может привести к тому, tooterminate hello процесса аварийно.

