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
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="5b557-104">Создание модуля Azure IoT Edge с помощью C&#x23;</span><span class="sxs-lookup"><span data-stu-id="5b557-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="5b557-105">Этот учебник демонстрирует способ toocreate какой-либо модуль для `Azure IoT Edge` с помощью `Visual Studio Code` и `C#`.</span><span class="sxs-lookup"><span data-stu-id="5b557-105">This tutorial showcases how toocreate a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="5b557-106">В этом учебнике мы будем рассматривать настройки среды и как toowrite [ЛЮЧИТЬ](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) модуля преобразователя данных с помощью последней hello `Azure IoT Edge NuGet` пакетов.</span><span class="sxs-lookup"><span data-stu-id="5b557-106">In this tutorial, we walk through environment set-up and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="5b557-107">Этот учебник использует hello `.NET Core SDK`, который поддерживает кросс платформенной совместимости.</span><span class="sxs-lookup"><span data-stu-id="5b557-107">This tutorial is using hello `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="5b557-108">Hello следующий учебник записывается с помощью hello `Windows 10` операционной системы.</span><span class="sxs-lookup"><span data-stu-id="5b557-108">hello following tutorial is written using hello `Windows 10` operating system.</span></span> <span data-ttu-id="5b557-109">Некоторые команды hello в этом учебнике может отличаться в зависимости от вашей `development environment`.</span><span class="sxs-lookup"><span data-stu-id="5b557-109">Some of hello commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5b557-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5b557-110">Prerequisites</span></span>

<span data-ttu-id="5b557-111">В этом разделе настраивается среда для разработки модуля `Azure IoT Edge`.</span><span class="sxs-lookup"><span data-stu-id="5b557-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="5b557-112">Оно применяется tooboth **64-разрядной версии Windows** и **64-разрядных Linux (8 Ubuntu/Debian)** операционных систем.</span><span class="sxs-lookup"><span data-stu-id="5b557-112">It applies tooboth **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="5b557-113">Привет, следуя программного обеспечения не требуется:</span><span class="sxs-lookup"><span data-stu-id="5b557-113">hello following software is required:</span></span>

- <span data-ttu-id="5b557-114">[клиент Git](https://git-scm.com/downloads);</span><span class="sxs-lookup"><span data-stu-id="5b557-114">[Git Client](https://git-scm.com/downloads)</span></span>
- [<span data-ttu-id="5b557-115">Базовый пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="5b557-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="5b557-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5b557-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="5b557-117">Tooclone hello репозитория для данного образца не требуется, однако все hello пример кода, рассматриваемые в этом учебнике расположен в следующих репозитория hello:</span><span class="sxs-lookup"><span data-stu-id="5b557-117">You do not need tooclone hello repo for this sample, however all of hello sample code discussed in this tutorial is located in hello following repository:</span></span>

- <span data-ttu-id="5b557-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="5b557-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="5b557-119">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="5b557-119">Getting started</span></span>

1. <span data-ttu-id="5b557-120">Установите `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="5b557-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="5b557-121">Установка `Visual Studio Code` и hello `C# extension` из Visual Studio Marketplace кода hello.</span><span class="sxs-lookup"><span data-stu-id="5b557-121">Install `Visual Studio Code` and hello `C# extension` from hello Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="5b557-122">Просмотр этой [краткий учебник видео](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) о том, как tooget приступить к работе с помощью `Visual Studio Code` и hello `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="5b557-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how tooget started using `Visual Studio Code` and hello `.NET Core SDK`.</span></span>

## <a name="creating-hello-azure-iot-edge-converter-module"></a><span data-ttu-id="5b557-123">Создание модуля преобразователя hello Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="5b557-123">Creating hello Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="5b557-124">Инициализируйте новый проект C# библиотеки классов `.NET Core`:</span><span class="sxs-lookup"><span data-stu-id="5b557-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="5b557-125">Откройте командную строку (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="5b557-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="5b557-126">Перейдите в папку toohello, куда toocreate hello `C#` проекта.</span><span class="sxs-lookup"><span data-stu-id="5b557-126">Navigate toohello folder where you'd like toocreate hello `C#` project.</span></span>
    - <span data-ttu-id="5b557-127">Введите **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="5b557-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="5b557-128">Эта команда создает в каталоге проектов пустой класс с именем `Class1.cs`.</span><span class="sxs-lookup"><span data-stu-id="5b557-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="5b557-129">Перейдите в папку toohello, где только что созданный проект библиотеки классов hello, введя **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="5b557-129">Navigate toohello folder where we just created hello class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="5b557-130">Привет открыть проект в `Visual Studio Code` , введя **кода.**.</span><span class="sxs-lookup"><span data-stu-id="5b557-130">Open hello project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="5b557-131">После открытия проекта hello в `Visual Studio Code`, щелкните hello **IoTEdgeConverterModule.csproj** tooopen hello файла, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="5b557-131">Once hello project is opened in `Visual Studio Code`, click on hello **IoTEdgeConverterModule.csproj** tooopen hello file as shown in hello following image:</span></span>

    ![Окно редактирования Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="5b557-133">Вставка hello `XML` большого двоичного объекта в следующий фрагмент кода между закрывающей hello hello `PropertyGroup` теги и hello закрытие `Project` тега; строка шесть hello предшествующий изображение и сохраните файл hello, нажав клавишу `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="5b557-133">Insert hello `XML` blob shown in hello following code snippet between hello closing `PropertyGroup` tag and hello closing `Project` tag; line six in hello preceding image and save hello file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="5b557-134">После сохранения hello `.csproj` файл `Visual Studio Code` должна вывести запрос с `unresolved dependencies` диалогового окна, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="5b557-134">Once you save hello `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in hello following image:</span></span> 

    ![Диалоговое окно восстановления зависимостей Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="5b557-136">) нажмите кнопку `Restore` toorestore все hello ссылок в проектах hello `.csproj` файла, включая hello `PackageReferences` добавлена.</span><span class="sxs-lookup"><span data-stu-id="5b557-136">a) Click `Restore` toorestore all of hello references in hello projects `.csproj` file including hello `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="5b557-137">(б) `Visual Studio Code` автоматически создает hello `project.assets.json` файла в проектах `obj` папки.</span><span class="sxs-lookup"><span data-stu-id="5b557-137">b) `Visual Studio Code` automatically creates hello `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="5b557-138">Этот файл содержит сведения о проекте зависимости toomake последующие операции восстановления быстрее.</span><span class="sxs-lookup"><span data-stu-id="5b557-138">This file contains information about your project's dependencies toomake subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="5b557-139">`.NET Core Tools` теперь основаны на MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5b557-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="5b557-140">Это означает, что вместо файла `project.json` создается файл `.csproj` проекта.</span><span class="sxs-lookup"><span data-stu-id="5b557-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="5b557-141">Если `Visual Studio Code` не отображает запрос, то это не проблема, так как эти действия можно выполнить вручную.</span><span class="sxs-lookup"><span data-stu-id="5b557-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="5b557-142">Откройте hello `Visual Studio Code` интеграции окно терминала, нажав клавишу hello `Ctrl`  +  `backtick` ключей или с помощью меню hello `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="5b557-142">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="5b557-143">В hello `Integrated Terminal` тип окна **восстановления dotnet**.</span><span class="sxs-lookup"><span data-stu-id="5b557-143">In hello `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="5b557-144">Переименование hello `Class1.cs` файла слишком`BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="5b557-144">Rename hello `Class1.cs` file too`BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="5b557-145">) файл hello toorename сначала щелкните на файле hello нажмите клавишу hello `F2` ключа.</span><span class="sxs-lookup"><span data-stu-id="5b557-145">a) toorename hello file first click on hello file then press hello `F2` key.</span></span>
    
    <span data-ttu-id="5b557-146">b) введите новое имя hello **BleConverterModule**, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="5b557-146">b) Type in hello new name **BleConverterModule**, as seen in hello following image:</span></span>

    ![Переименование класса в Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="5b557-148">Замените существующий код hello в hello `BleConverterModule.cs` файл путем копирования и вставки hello, следующий фрагмент кода в ваш `BleConverterModule.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="5b557-148">Replace hello existing code in hello `BleConverterModule.cs` file by copying and pasting hello following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="5b557-149">Сохраните файл hello, нажав клавишу `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="5b557-149">Save hello file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="5b557-150">Создайте новый файл с именем `Untitled-1` , нажав клавишу hello `Ctrl`  +  `N` ключи, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="5b557-150">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys as seen in hello following image:</span></span>

    ![Новый файл Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="5b557-152">toodeserialize hello `JSON` объекта, которые мы получаем от hello имитировать `BLE` устройства, следующий код в hello hello копирования `Untitled-1` окне редактора кода в файл.</span><span class="sxs-lookup"><span data-stu-id="5b557-152">toodeserialize hello `JSON` object that we receive from hello simulated `BLE` device, copy hello following code into hello `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="5b557-153">Сохраните файл как файл hello `BleData.cs` , нажав клавишу `Ctrl`  +  `Shift`  +  `S` ключей.</span><span class="sxs-lookup"><span data-stu-id="5b557-153">Save hello file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="5b557-154">На hello Сохранить как диалоговое окно, в hello `Save as Type` раскрывающееся меню, выберите `C# (*.cs;*.csx)` в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="5b557-154">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in hello following image:</span></span>

    ![Диалоговое окно "Сохранить как" Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="5b557-156">Создайте новый файл с именем `Untitled-1` , нажав клавишу hello `Ctrl`  +  `N` ключей.</span><span class="sxs-lookup"><span data-stu-id="5b557-156">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="5b557-157">Скопируйте и вставьте следующий фрагмент кода в hello hello `Untitled-1` файла.</span><span class="sxs-lookup"><span data-stu-id="5b557-157">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> <span data-ttu-id="5b557-158">Этот класс является `Azure IoT Edge` модуль, который мы используем данные toooutput hello, полученных от наших `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="5b557-158">This class is a `Azure IoT Edge` module, which we use toooutput hello data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="5b557-159">Сохраните файл как файл hello `DotNetPrinterModule.cs` , нажав клавишу `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="5b557-159">Save hello file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="5b557-160">На hello Сохранить как диалоговое окно, в hello `Save as Type` раскрывающееся меню, выберите `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="5b557-160">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="5b557-161">Создайте новый файл с именем `Untitled-1` , нажав клавишу hello `Ctrl`  +  `N` ключей.</span><span class="sxs-lookup"><span data-stu-id="5b557-161">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="5b557-162">toodeserialize hello `JSON` объектов, которые мы получаем от hello `BleConverterModule`, копировать и вставить hello следующий фрагмент кода hello `Untitled-1` файла.</span><span class="sxs-lookup"><span data-stu-id="5b557-162">toodeserialize hello `JSON` object that we receive from hello `BleConverterModule`, Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="5b557-163">Сохраните файл как файл hello `BleConverterData.cs` , нажав клавишу `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="5b557-163">Save hello file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="5b557-164">На hello Сохранить как диалоговое окно, в hello `Save as Type` раскрывающееся меню, выберите `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="5b557-164">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="5b557-165">Создайте новый файл с именем `Untitled-1` , нажав клавишу hello `Ctrl`  +  `N` ключей.</span><span class="sxs-lookup"><span data-stu-id="5b557-165">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="5b557-166">Скопируйте и вставьте следующий фрагмент кода в hello hello `Untitled-1` файла.</span><span class="sxs-lookup"><span data-stu-id="5b557-166">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="5b557-167">Сохраните файл как файл hello `gw-config.json` , нажав клавишу `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="5b557-167">Save hello file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="5b557-168">На hello Сохранить как диалоговое окно, в hello `Save as Type` раскрывающееся меню, выберите `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="5b557-168">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="5b557-169">копирование tooenable toohello файл конфигурации hello выходного каталога, обновления hello `IoTEdgeConverterModule.csproj` с hello после двоичных данных XML:</span><span class="sxs-lookup"><span data-stu-id="5b557-169">tooenable copying of hello configuration file toohello output directory, update hello `IoTEdgeConverterModule.csproj` with hello following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="5b557-170">Обновить Hello `IoTEdgeConverterModule.csproj` следует выглядят hello следующие изображения:</span><span class="sxs-lookup"><span data-stu-id="5b557-170">hello updated `IoTEdgeConverterModule.csproj` should look like hello following image:</span></span>

    ![Обновленный CSPROJ-файл Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="5b557-172">Создайте новый файл с именем `Untitled-1` , нажав клавишу hello `Ctrl`  +  `N` ключей.</span><span class="sxs-lookup"><span data-stu-id="5b557-172">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="5b557-173">Скопируйте и вставьте следующий фрагмент кода в hello hello `Untitled-1` файла.</span><span class="sxs-lookup"><span data-stu-id="5b557-173">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="5b557-174">Сохраните файл как файл hello `binplace.ps1` , нажав клавишу `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="5b557-174">Save hello file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="5b557-175">На hello Сохранить как диалоговое окно, в hello `Save as Type` раскрывающееся меню, выберите `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="5b557-175">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="5b557-176">Выполните построение проекта hello, нажав клавишу hello `Ctrl`  +  `Shift`  +  `B` ключей.</span><span class="sxs-lookup"><span data-stu-id="5b557-176">Build hello project by pressing hello `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="5b557-177">При построении проекта hello для hello первый раз `Visual Studio Code` , предлагающее hello `No build task defined.` диалогового окна, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="5b557-177">When you build hello project for hello first time, `Visual Studio Code` prompts you with hello `No build task defined.` dialog as seen in hello following image:</span></span>

    ![Диалоговое окно задачи сборки Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="5b557-179">) щелкните hello `Configure Build Task` кнопки.</span><span class="sxs-lookup"><span data-stu-id="5b557-179">a) Click hello `Configure Build Task` button.</span></span>

    <span data-ttu-id="5b557-180">(б) в hello `Select a Task Runner` раскрывающегося меню диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5b557-180">b) In hello `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="5b557-181">Выберите `.NET Core` как видно в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="5b557-181">Select `.NET Core` as seen in hello following image:</span></span> 

    ![Диалоговое окно выбора задачи Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="5b557-183">по щелчку c) hello `.NET Core` hello создает элемент `tasks.json` файла в вашей `.vscode` каталога и открывает файл в hello Здравствуйте, `code editor` окна.</span><span class="sxs-lookup"><span data-stu-id="5b557-183">c) Clicking hello `.NET Core` item creates hello `tasks.json` file in your `.vscode` directory and opens hello file in hello `code editor` window.</span></span> <span data-ttu-id="5b557-184">Нет этого файла hello закрыть вкладку toomodify нет необходимости.</span><span class="sxs-lookup"><span data-stu-id="5b557-184">There is no need toomodify this file, close hello tab.</span></span>

27.  <span data-ttu-id="5b557-185">Откройте hello `Visual Studio Code` интеграции окно терминала, нажав клавишу hello `Ctrl`  +  `backtick` ключей или с помощью меню hello `View`  ->  `Integrated Terminal` и тип **.\binplace.ps1**в hello `PowerShell` командной строки.</span><span class="sxs-lookup"><span data-stu-id="5b557-185">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into hello `PowerShell` command prompt.</span></span> <span data-ttu-id="5b557-186">Эта команда копирует все наши зависимости toohello выходной каталог.</span><span class="sxs-lookup"><span data-stu-id="5b557-186">This command copies all our dependencies toohello output directory.</span></span>

28. <span data-ttu-id="5b557-187">Перейдите в выходной каталог проекты toohello hello `Integrated Terminal` окна, введя **cd.\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="5b557-187">Navigate toohello projects output directory in hello `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="5b557-188">Запустите проект образец hello, введя **. \gw.exe gw-config.json** в hello `Integrated Terminal` строке окна.</span><span class="sxs-lookup"><span data-stu-id="5b557-188">Run hello sample project by typing **.\gw.exe gw-config.json** into hello `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="5b557-189">Если вы следовали hello шаги в этом учебнике точно, вы должны выполняться hello `Azure IoT Edge BLE Data Converter Module` образец проекта, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="5b557-189">If you have followed hello steps in this tutorial closely, you should now be running hello `Azure IoT Edge BLE Data Converter Module` sample project as seen in hello following image:</span></span>
    
        ![Пример имитации устройства, запущенный в Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="5b557-191">Приложение hello tooterminate, нажмите клавишу hello `<Enter>` ключа.</span><span class="sxs-lookup"><span data-stu-id="5b557-191">If you want tooterminate hello application, press hello `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="5b557-192">Не рекомендуется toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` шлюза приложений (то есть **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="5b557-192">It is not recommended toouse `Ctrl` + `C` tooterminate hello `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="5b557-193">Это действие может привести к тому, tooterminate hello процесса аварийно.</span><span class="sxs-lookup"><span data-stu-id="5b557-193">As this action may cause hello process tooterminate abnormally.</span></span>

