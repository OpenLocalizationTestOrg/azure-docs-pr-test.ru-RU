---
title: "Создание модуля Azure IoT Edge с помощью C# | Документация Майкрософт"
description: "В этом руководстве показано, как с помощью последних пакетов NuGet для Azure IoT Edge, Visual Studio Code и C# написать модуль преобразователя данных BLE."
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
ms.openlocfilehash: 7175ffc8de2c043593d61143b402484d33e4a8cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="0ce55-104">Создание модуля Azure IoT Edge с помощью C&#x23;</span><span class="sxs-lookup"><span data-stu-id="0ce55-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="0ce55-105">В этом руководстве показано, как создать модуль для `Azure IoT Edge` с помощью `Visual Studio Code` и `C#`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-105">This tutorial showcases how to create a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="0ce55-106">В этом руководстве приводятся пошаговые инструкции по настройке среды и написанию модуля преобразователя данных [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) с помощью последних пакетов `Azure IoT Edge NuGet`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-106">In this tutorial, we walk through environment set-up and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="0ce55-107">В этом руководстве используется пакет `.NET Core SDK`, который поддерживает кроссплатформенную совместимость.</span><span class="sxs-lookup"><span data-stu-id="0ce55-107">This tutorial is using the `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="0ce55-108">Приведенные ниже инструкции написаны на основе операционной системы `Windows 10`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-108">The following tutorial is written using the `Windows 10` operating system.</span></span> <span data-ttu-id="0ce55-109">Некоторые команды в этом руководстве могут отличаться в зависимости от используемой `development environment`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-109">Some of the commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0ce55-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0ce55-110">Prerequisites</span></span>

<span data-ttu-id="0ce55-111">В этом разделе настраивается среда для разработки модуля `Azure IoT Edge`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="0ce55-112">Данные настройки действительны для следующих операционных систем: **64-разрядная версия Windows** и **64-разрядная версия Linux (Ubuntu/Debian 8)**.</span><span class="sxs-lookup"><span data-stu-id="0ce55-112">It applies to both **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="0ce55-113">Требуется следующее ПО:</span><span class="sxs-lookup"><span data-stu-id="0ce55-113">The following software is required:</span></span>

- <span data-ttu-id="0ce55-114">[клиент Git](https://git-scm.com/downloads);</span><span class="sxs-lookup"><span data-stu-id="0ce55-114">[Git Client](https://git-scm.com/downloads)</span></span>
- [<span data-ttu-id="0ce55-115">Базовый пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="0ce55-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="0ce55-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0ce55-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="0ce55-117">Для данного примера не требуется клонирование репозитория, хотя все рассматриваемые в этом руководстве примеры кода находятся в следующем репозитории:</span><span class="sxs-lookup"><span data-stu-id="0ce55-117">You do not need to clone the repo for this sample, however all of the sample code discussed in this tutorial is located in the following repository:</span></span>

- <span data-ttu-id="0ce55-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="0ce55-119">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="0ce55-119">Getting started</span></span>

1. <span data-ttu-id="0ce55-120">Установите `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="0ce55-121">Установите `Visual Studio Code`и `C# extension` из Marketplace для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0ce55-121">Install `Visual Studio Code` and the `C# extension` from the Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="0ce55-122">Просмотрите это [краткое видеоруководство](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) о том, как приступить к работе с `Visual Studio Code` и `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how to get started using `Visual Studio Code` and the `.NET Core SDK`.</span></span>

## <a name="creating-the-azure-iot-edge-converter-module"></a><span data-ttu-id="0ce55-123">Создание модуля преобразователя Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="0ce55-123">Creating the Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="0ce55-124">Инициализируйте новый проект C# библиотеки классов `.NET Core`:</span><span class="sxs-lookup"><span data-stu-id="0ce55-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="0ce55-125">Откройте командную строку (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="0ce55-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="0ce55-126">Перейдите к папке, в которой хотите создать проект `C#`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-126">Navigate to the folder where you'd like to create the `C#` project.</span></span>
    - <span data-ttu-id="0ce55-127">Введите **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="0ce55-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="0ce55-128">Эта команда создает в каталоге проектов пустой класс с именем `Class1.cs`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="0ce55-129">Перейдите к папке, в которой мы только что создали проект библиотеки классов. Для этого введите команду **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="0ce55-129">Navigate to the folder where we just created the class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="0ce55-130">Откройте проект в `Visual Studio Code`, введя команду **code .**.</span><span class="sxs-lookup"><span data-stu-id="0ce55-130">Open the project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="0ce55-131">После открытия проекта в `Visual Studio Code` щелкните **IoTEdgeConverterModule.csproj**, чтобы открыть файл, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="0ce55-131">Once the project is opened in `Visual Studio Code`, click on the **IoTEdgeConverterModule.csproj** to open the file as shown in the following image:</span></span>

    ![Окно редактирования Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="0ce55-133">Вставьте большой двоичный объект `XML` из приведенного ниже фрагмента кода между закрывающими тегами `PropertyGroup` и `Project` (шестая строка на предыдущем изображении) и сохраните файл, нажав сочетание клавиш `Ctrl` + `S`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-133">Insert the `XML` blob shown in the following code snippet between the closing `PropertyGroup` tag and the closing `Project` tag; line six in the preceding image and save the file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="0ce55-134">После сохранения файла `.csproj` в `Visual Studio Code` должен отобразиться запрос в виде диалогового окна `unresolved dependencies`, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="0ce55-134">Once you save the `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in the following image:</span></span> 

    ![Диалоговое окно восстановления зависимостей Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="0ce55-136">a) Нажмите кнопку `Restore`, чтобы восстановить все ссылки в файле `.csproj` проекта, включая добавленные нами `PackageReferences`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-136">a) Click `Restore` to restore all of the references in the projects `.csproj` file including the `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="0ce55-137">b) `Visual Studio Code` автоматически создает файл `project.assets.json` в папке `obj` проекта.</span><span class="sxs-lookup"><span data-stu-id="0ce55-137">b) `Visual Studio Code` automatically creates the `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="0ce55-138">Этот файл содержит сведения о зависимостях проекта, которые позволяют ускорить последующие операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="0ce55-138">This file contains information about your project's dependencies to make subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="0ce55-139">`.NET Core Tools` теперь основаны на MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0ce55-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="0ce55-140">Это означает, что вместо файла `project.json` создается файл `.csproj` проекта.</span><span class="sxs-lookup"><span data-stu-id="0ce55-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="0ce55-141">Если `Visual Studio Code` не отображает запрос, то это не проблема, так как эти действия можно выполнить вручную.</span><span class="sxs-lookup"><span data-stu-id="0ce55-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="0ce55-142">Откройте окно интегрированного терминала `Visual Studio Code`, нажав сочетание клавиш `Ctrl` + `backtick`. Либо воспользуйтесь меню `View` -> `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-142">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="0ce55-143">В окне `Integrated Terminal` введите команду **dotnet restore**.</span><span class="sxs-lookup"><span data-stu-id="0ce55-143">In the `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="0ce55-144">Переименуйте файл `Class1.cs` в `BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-144">Rename the `Class1.cs` file to `BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="0ce55-145">a) Чтобы переименовать файл, сначала щелкните файл, а затем нажмите клавишу `F2`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-145">a) To rename the file first click on the file then press the `F2` key.</span></span>
    
    <span data-ttu-id="0ce55-146">b) Введите новое имя **BleConverterModule**, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="0ce55-146">b) Type in the new name **BleConverterModule**, as seen in the following image:</span></span>

    ![Переименование класса в Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="0ce55-148">Замените существующий код в файле `BleConverterModule.cs`, скопировав и вставив следующий фрагмент кода в файл `BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-148">Replace the existing code in the `BleConverterModule.cs` file by copying and pasting the following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="0ce55-149">Сохраните файл, нажав сочетание клавиш `Ctrl` + `S`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-149">Save the file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="0ce55-150">Создайте файл с именем `Untitled-1`, нажав сочетание клавиш `Ctrl` + `N`, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="0ce55-150">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys as seen in the following image:</span></span>

    ![Новый файл Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="0ce55-152">Чтобы десериализировать объект `JSON`, который мы получаем с имитации устройства `BLE`, скопируйте следующий код в окно редактора кода файла `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-152">To deserialize the `JSON` object that we receive from the simulated `BLE` device, copy the following code into the `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="0ce55-153">Сохраните файл как `BleData.cs`, нажав сочетание клавиш `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-153">Save the file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="0ce55-154">В диалоговом окне "Сохранить как" в раскрывающемся меню `Save as Type` выберите `C# (*.cs;*.csx)`, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="0ce55-154">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in the following image:</span></span>

    ![Диалоговое окно "Сохранить как" Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="0ce55-156">Создайте файл с именем `Untitled-1`, нажав сочетание клавиш `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-156">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="0ce55-157">Скопируйте следующий фрагмент кода и вставьте его в файл `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-157">Copy and paste the following code snippet into the `Untitled-1` file.</span></span> <span data-ttu-id="0ce55-158">Этот класс является модулем `Azure IoT Edge`, который мы используем для вывода данных, получаемых от модуля `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-158">This class is a `Azure IoT Edge` module, which we use to output the data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="0ce55-159">Сохраните файл как `DotNetPrinterModule.cs`, нажав сочетание клавиш `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-159">Save the file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="0ce55-160">В диалоговом окне "Сохранить как" в раскрывающемся меню `Save as Type` выберите `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-160">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="0ce55-161">Создайте файл с именем `Untitled-1`, нажав сочетание клавиш `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-161">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="0ce55-162">Чтобы десериализировать объект `JSON`, который мы получаем от модуля `BleConverterModule`, скопируйте следующий фрагмент кода и вставьте его в файл `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-162">To deserialize the `JSON` object that we receive from the `BleConverterModule`, Copy and paste the following code snippet into the `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="0ce55-163">Сохраните файл как `BleConverterData.cs`, нажав сочетание клавиш `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-163">Save the file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="0ce55-164">В диалоговом окне "Сохранить как" в раскрывающемся меню `Save as Type` выберите `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-164">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="0ce55-165">Создайте файл с именем `Untitled-1`, нажав сочетание клавиш `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-165">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="0ce55-166">Скопируйте следующий фрагмент кода и вставьте его в файл `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-166">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="0ce55-167">Сохраните файл как `gw-config.json`, нажав сочетание клавиш `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-167">Save the file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="0ce55-168">В диалоговом окне "Сохранить как" в раскрывающемся меню `Save as Type` выберите `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-168">On the save as dialog box, in the `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="0ce55-169">Чтобы файл конфигурации можно было скопировать в выходной каталог, обновите файл `IoTEdgeConverterModule.csproj`, вставив в него следующий большой двоичный объект XML:</span><span class="sxs-lookup"><span data-stu-id="0ce55-169">To enable copying of the configuration file to the output directory, update the `IoTEdgeConverterModule.csproj` with the following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="0ce55-170">Обновленный файл `IoTEdgeConverterModule.csproj` должен выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="0ce55-170">The updated `IoTEdgeConverterModule.csproj` should look like the following image:</span></span>

    ![Обновленный CSPROJ-файл Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="0ce55-172">Создайте файл с именем `Untitled-1`, нажав сочетание клавиш `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-172">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="0ce55-173">Скопируйте следующий фрагмент кода и вставьте его в файл `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-173">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="0ce55-174">Сохраните файл как `binplace.ps1`, нажав сочетание клавиш `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-174">Save the file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="0ce55-175">В диалоговом окне "Сохранить как" в раскрывающемся меню `Save as Type` выберите `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-175">On the save as dialog box, in the `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="0ce55-176">Выполните сборку проекта, нажав сочетание клавиш `Ctrl` + `Shift` + `B`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-176">Build the project by pressing the `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="0ce55-177">При первом выполнении сборки проекта в `Visual Studio Code` отобразится запрос в виде диалогового окна `No build task defined.`, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="0ce55-177">When you build the project for the first time, `Visual Studio Code` prompts you with the `No build task defined.` dialog as seen in the following image:</span></span>

    ![Диалоговое окно задачи сборки Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="0ce55-179">a) Нажмите кнопку `Configure Build Task`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-179">a) Click the `Configure Build Task` button.</span></span>

    <span data-ttu-id="0ce55-180">b) В раскрывающегося меню `Select a Task Runner` диалогового окна</span><span class="sxs-lookup"><span data-stu-id="0ce55-180">b) In the `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="0ce55-181">выберите `.NET Core`, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="0ce55-181">Select `.NET Core` as seen in the following image:</span></span> 

    ![Диалоговое окно выбора задачи Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="0ce55-183">c) Если щелкнуть элемент `.NET Core`, то в каталоге `.vscode` будет создан файл `tasks.json`, который затем откроется в окне `code editor`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-183">c) Clicking the `.NET Core` item creates the `tasks.json` file in your `.vscode` directory and opens the file in the `code editor` window.</span></span> <span data-ttu-id="0ce55-184">Нет необходимости изменять этот файл. Просто закройте вкладку.</span><span class="sxs-lookup"><span data-stu-id="0ce55-184">There is no need to modify this file, close the tab.</span></span>

27.  <span data-ttu-id="0ce55-185">Откройте окно интегрированного терминала `Visual Studio Code`, нажав сочетание клавиш `Ctrl` + `backtick` или с помощью меню `View` -> `Integrated Terminal`, и введите в командной строке `PowerShell` команду **.\binplace.ps1**.</span><span class="sxs-lookup"><span data-stu-id="0ce55-185">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into the `PowerShell` command prompt.</span></span> <span data-ttu-id="0ce55-186">Эта команда копирует все зависимости в выходной каталог.</span><span class="sxs-lookup"><span data-stu-id="0ce55-186">This command copies all our dependencies to the output directory.</span></span>

28. <span data-ttu-id="0ce55-187">Перейдите в выходной каталог проекта в окне `Integrated Terminal`, введя команду **cd .\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="0ce55-187">Navigate to the projects output directory in the `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="0ce55-188">Запустите пример проекта, введя команду **.\gw.exe gw-config.json** в окно командной строки `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-188">Run the sample project by typing **.\gw.exe gw-config.json** into the `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="0ce55-189">Если вы четко следовали инструкциям, приведенным в этом руководстве, то у вас должен запуститься пример проекта `Azure IoT Edge BLE Data Converter Module`, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="0ce55-189">If you have followed the steps in this tutorial closely, you should now be running the `Azure IoT Edge BLE Data Converter Module` sample project as seen in the following image:</span></span>
    
        ![Пример имитации устройства, запущенный в Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="0ce55-191">Чтобы завершить работу приложения, нажмите клавишу `<Enter>`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-191">If you want to terminate the application, press the `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="0ce55-192">Не рекомендуется использовать сочетание клавиш `Ctrl` + `C` для завершения работы приложения шлюза `IoT Edge` (то есть **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="0ce55-192">It is not recommended to use `Ctrl` + `C` to terminate the `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="0ce55-193">Это действие может вызвать аварийное завершение процесса.</span><span class="sxs-lookup"><span data-stu-id="0ce55-193">As this action may cause the process to terminate abnormally.</span></span>

