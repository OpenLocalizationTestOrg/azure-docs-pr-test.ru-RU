## <a name="create-a-simulated-device-app"></a><span data-ttu-id="25f5a-101">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="25f5a-101">Create a simulated device app</span></span>
<span data-ttu-id="25f5a-102">В этом разделе выполняются следующие действия:</span><span class="sxs-lookup"><span data-stu-id="25f5a-102">In this section, you:</span></span>

* <span data-ttu-id="25f5a-103">Создайте консольное приложение Node.js, которое отвечает tooa прямой метод, вызываемый hello облака</span><span class="sxs-lookup"><span data-stu-id="25f5a-103">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="25f5a-104">активируете обновление имитации встроенного ПО;</span><span class="sxs-lookup"><span data-stu-id="25f5a-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="25f5a-105">Используйте hello выводятся свойства tooenable устройствами двойных запросы tooidentify устройства и их последнего завершения обновления встроенного по</span><span class="sxs-lookup"><span data-stu-id="25f5a-105">Use hello reported properties tooenable device twin queries tooidentify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="25f5a-106">Шаг 1. Создайте пустую папку с именем **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="25f5a-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="25f5a-107">В hello **manageddevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="25f5a-107">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="25f5a-108">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="25f5a-108">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="25f5a-109">Шаг 2: В командной строке в hello **manageddevice** папку, следующая команда tooinstall hello hello **azure iot устройства** и **azure iot устройства mqtt** устройства Пакеты SDK:</span><span class="sxs-lookup"><span data-stu-id="25f5a-109">Step 2: At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="25f5a-110">Шаг 3: С помощью текстового редактора создайте **dmpatterns_fwupdate_device.js** файла в hello **manageddevice** папки.</span><span class="sxs-lookup"><span data-stu-id="25f5a-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in hello **manageddevice** folder.</span></span>

<span data-ttu-id="25f5a-111">Шаг 4: Добавление следующих hello «требовать» операторы в начале hello hello **dmpatterns_fwupdate_device.js** файла:</span><span class="sxs-lookup"><span data-stu-id="25f5a-111">Step 4: Add hello following 'require' statements at hello start of hello **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="25f5a-112">Шаг 5: Добавление **connectionString** переменной и использовать его toocreate **клиента** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="25f5a-112">Step 5: Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="25f5a-113">Замените hello `{yourdeviceconnectionstring}` заполнитель строки подключения hello, сделанные ранее на заметку в разделе «Создание удостоверение устройства» hello ранее:</span><span class="sxs-lookup"><span data-stu-id="25f5a-113">Replace hello `{yourdeviceconnectionstring}` placeholder with hello connection string you previously made a note of in hello "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="25f5a-114">Шаг 6: Добавление hello следующую функцию, которая будет использоваться tooupdate сообщил свойства:</span><span class="sxs-lookup"><span data-stu-id="25f5a-114">Step 6: Add hello following function that is used tooupdate reported properties:</span></span>
   
    ```
    var reportFWUpdateThroughTwin = function(twin, firmwareUpdateValue) {
      var patch = {
          iothubDM : {
            firmwareUpdate : firmwareUpdateValue
          }
      };
   
      twin.properties.reported.update(patch, function(err) {
        if (err) throw err;
        console.log('twin state reported: ' + firmwareUpdateValue.status);
      });
    };
    ```

<span data-ttu-id="25f5a-115">Шаг 7: Добавление hello, следующие функции, которые имитируют загружать и устанавливать hello образ встроенного по:</span><span class="sxs-lookup"><span data-stu-id="25f5a-115">Step 7: Add hello following functions that simulate downloading and applying hello firmware image:</span></span>
   
    ```
    var simulateDownloadImage = function(imageUrl, callback) {
      var error = null;
      var image = "[fake image data]";
   
      console.log("Downloading image from " + imageUrl);
   
      callback(error, image);
    }
   
    var simulateApplyImage = function(imageData, callback) {
      var error = null;
   
      if (!imageData) {
        error = {message: 'Apply image failed because of missing image data.'};
      }
   
      callback(error);
    }
    ```

<span data-ttu-id="25f5a-116">Шаг 8: Добавление hello после функции, что состояние обновления встроенного по hello обновлений через hello также выводятся свойства**ожидания**.</span><span class="sxs-lookup"><span data-stu-id="25f5a-116">Step 8: Add hello following function that updates hello firmware update status through hello reported properties too**waiting**.</span></span> <span data-ttu-id="25f5a-117">Как правило устройств сообщается о доступных обновлений, заданной администратором политики вызывает hello устройства toostart загружать и устанавливать обновления hello.</span><span class="sxs-lookup"><span data-stu-id="25f5a-117">Typically, devices are informed of an available update and an administrator defined policy causes hello device toostart downloading and applying hello update.</span></span> <span data-ttu-id="25f5a-118">Эта функция является где hello tooenable логику выполнения политики.</span><span class="sxs-lookup"><span data-stu-id="25f5a-118">This function is where hello logic tooenable that policy should run.</span></span> <span data-ttu-id="25f5a-119">Для простоты образец hello ожидает четырех секунд перед продолжением toodownload hello встроенное:</span><span class="sxs-lookup"><span data-stu-id="25f5a-119">For simplicity, hello sample waits for four seconds before proceeding toodownload hello firmware image:</span></span>
   
    ```
    var waitToDownload = function(twin, fwPackageUriVal, callback) {
      var now = new Date();
   
      reportFWUpdateThroughTwin(twin, {
        fwPackageUri: fwPackageUriVal,
        status: 'waiting',
        error : null,
        startedWaitingTime : now.toISOString()
      });
      setTimeout(callback, 4000);
    };
    ```

<span data-ttu-id="25f5a-120">Шаг 9: Добавление hello после функции, что состояние обновления встроенного по hello обновлений через hello также выводятся свойства**Загрузка**.</span><span class="sxs-lookup"><span data-stu-id="25f5a-120">Step 9: Add hello following function that updates hello firmware update status through hello reported properties too**downloading**.</span></span> <span data-ttu-id="25f5a-121">Hello функция затем имитирует загрузка встроенного по, и наконец обновлений hello tooeither состояние обновления встроенного по **downloadFailed** или **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="25f5a-121">hello function then simulates a firmware download and finally updates hello firmware update status tooeither **downloadFailed** or **downloadComplete**:</span></span>
   
    ```
    var downloadImage = function(twin, fwPackageUriVal, callback) {
      var now = new Date();   
   
      reportFWUpdateThroughTwin(twin, {
        status: 'downloading',
      });
   
      setTimeout(function() {
        // Simulate download
        simulateDownloadImage(fwPackageUriVal, function(err, image) {
   
          if (err)
          {
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadfailed',
              error: {
                code: error_code,
                message: error_message,
              }
            });
          }
          else {        
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadComplete',
              downloadCompleteTime: now.toISOString(),
            });
   
            setTimeout(function() { callback(image); }, 4000);   
          }
        });
   
      }, 4000);
    }
    ```

<span data-ttu-id="25f5a-122">Шаг 10: Добавление hello после функции, что состояние обновления встроенного по hello обновлений через hello также выводятся свойства**применения**.</span><span class="sxs-lookup"><span data-stu-id="25f5a-122">Step 10: Add hello following function that updates hello firmware update status through hello reported properties too**applying**.</span></span> <span data-ttu-id="25f5a-123">Hello функция затем имитирует применение образ встроенного по hello и наконец обновлений hello tooeither состояние обновления встроенного по **applyFailed** или **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="25f5a-123">hello function then simulates applying hello firmware image and finally updates hello firmware update status tooeither **applyFailed** or **applyComplete**:</span></span>
    
    ```
    var applyImage = function(twin, imageData, callback) {
      var now = new Date();   
    
      reportFWUpdateThroughTwin(twin, {
        status: 'applying',
        startedApplyingImage : now.toISOString()
      });
    
      setTimeout(function() {
    
        // Simulate apply firmware image
        simulateApplyImage(imageData, function(err) {
          if (err) {
            reportFWUpdateThroughTwin(twin, {
              status: 'applyFailed',
              error: {
                code: err.error_code,
                message: err.error_message,
              }
            });
          } else { 
            reportFWUpdateThroughTwin(twin, {
              status: 'applyComplete',
              lastFirmwareUpdate: now.toISOString()
            });    
    
          }
        });
    
        setTimeout(callback, 4000);
    
      }, 4000);
    }
    ```

<span data-ttu-id="25f5a-124">Шаг 11: Добавление hello следующие функции, дескрипторы hello **firmwareUpdate** прямой метод и инициирует hello многоэтапным обновление встроенного по процессу:</span><span class="sxs-lookup"><span data-stu-id="25f5a-124">Step 11: Add hello following function that handles hello **firmwareUpdate** direct method and initiates hello multi-stage firmware update process:</span></span>
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond hello cloud app for hello direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get hello parameter from hello body of hello method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain hello device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start hello multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

<span data-ttu-id="25f5a-125">Шаг 12: Наконец, добавьте следующий код, который соединяет центр IoT tooyour hello:</span><span class="sxs-lookup"><span data-stu-id="25f5a-125">Step 12: Finally, add hello following code that connects tooyour IoT hub:</span></span>
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect tooIotHub client');
      }  else {
        console.log('Client connected tooIoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> <span data-ttu-id="25f5a-126">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="25f5a-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="25f5a-127">В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="25f5a-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 