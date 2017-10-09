## <a name="create-a-simulated-device-app"></a>Создание приложения виртуального устройства
В этом разделе выполняются следующие действия:

* Создайте консольное приложение Node.js, которое отвечает tooa прямой метод, вызываемый hello облака
* активируете обновление имитации встроенного ПО;
* Используйте hello выводятся свойства tooenable устройствами двойных запросы tooidentify устройства и их последнего завершения обновления встроенного по

Шаг 1. Создайте пустую папку с именем **manageddevice**.  В hello **manageddevice** папки, создайте файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```

Шаг 2: В командной строке в hello **manageddevice** папку, следующая команда tooinstall hello hello **azure iot устройства** и **azure iot устройства mqtt** устройства Пакеты SDK:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

Шаг 3: С помощью текстового редактора создайте **dmpatterns_fwupdate_device.js** файла в hello **manageddevice** папки.

Шаг 4: Добавление следующих hello «требовать» операторы в начале hello hello **dmpatterns_fwupdate_device.js** файла:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
Шаг 5: Добавление **connectionString** переменной и использовать его toocreate **клиента** экземпляра. Замените hello `{yourdeviceconnectionstring}` заполнитель строки подключения hello, сделанные ранее на заметку в разделе «Создание удостоверение устройства» hello ранее:
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

Шаг 6: Добавление hello следующую функцию, которая будет использоваться tooupdate сообщил свойства:
   
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

Шаг 7: Добавление hello, следующие функции, которые имитируют загружать и устанавливать hello образ встроенного по:
   
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

Шаг 8: Добавление hello после функции, что состояние обновления встроенного по hello обновлений через hello также выводятся свойства**ожидания**. Как правило устройств сообщается о доступных обновлений, заданной администратором политики вызывает hello устройства toostart загружать и устанавливать обновления hello. Эта функция является где hello tooenable логику выполнения политики. Для простоты образец hello ожидает четырех секунд перед продолжением toodownload hello встроенное:
   
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

Шаг 9: Добавление hello после функции, что состояние обновления встроенного по hello обновлений через hello также выводятся свойства**Загрузка**. Hello функция затем имитирует загрузка встроенного по, и наконец обновлений hello tooeither состояние обновления встроенного по **downloadFailed** или **downloadComplete**:
   
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

Шаг 10: Добавление hello после функции, что состояние обновления встроенного по hello обновлений через hello также выводятся свойства**применения**. Hello функция затем имитирует применение образ встроенного по hello и наконец обновлений hello tooeither состояние обновления встроенного по **applyFailed** или **applyComplete**:
    
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

Шаг 11: Добавление hello следующие функции, дескрипторы hello **firmwareUpdate** прямой метод и инициирует hello многоэтапным обновление встроенного по процессу:
    
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

Шаг 12: Наконец, добавьте следующий код, который соединяет центр IoT tooyour hello:
    
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
> простые действия tookeep, этот учебник не реализует никакую политику повтора. В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 