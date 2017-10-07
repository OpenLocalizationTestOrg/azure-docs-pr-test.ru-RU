---
title: "Пошаговое руководство захвата концентраторов событий aaaAzure | Документы Microsoft"
description: "Пример, использующий toodemonstrate hello Azure Python SDK, с помощью функции записи концентраторов событий hello."
services: event-hubs
documentationcenter: 
author: djrosanova
manager: timlt
editor: 
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: darosa;sethm
ms.openlocfilehash: 1737dcca283711d863aa970db0e80ae71814e666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a>Пошаговое руководство. Использование записи концентраторов событий с Python

Записать концентраторы событий — функция концентраторов событий, который позволяет вам tooautomatically доставки hello потоковой передачи данных в вашей tooan концентратора событий учетной записи хранилища больших двоичных объектов Azure по своему усмотрению. Эта возможность позволяет легко tooperform пакетную обработку на потоковой передачи данных в реальном времени. В этой статье описывается как toouse концентраторов событий захвата с Python. Дополнительные сведения о записи концентраторов событий см. в разделе hello [обзорную статью](event-hubs-archive-overview.md).

В этом образце используется hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) функция записи toodemonstrate hello. Программа Hello sender.py отправляет имитацию телеметрии среды tooEvent концентраторы в формате JSON. Hello концентратора событий настроен toouse hello отслеживания компонентов toowrite это хранилище tooblob данных в пакетах. приложение Hello capturereader.py затем считывает эти большие двоичные объекты и создает файл append на устройство, а затем записывает данные hello в CSV-файлах.

## <a name="what-will-be-accomplished"></a>Что будет выполнено

1. Создайте учетную запись хранилища больших двоичных объектов и контейнер больших двоичных объектов, с помощью портала Azure hello.
2. Создайте пространство имен концентратора событий с помощью портала Azure hello.
3. Создание концентратора событий функция отслеживания hello, включена, с помощью портала Azure hello.
4. Отправка данных концентратора событий toohello сценарий Python.
5. Чтение файлов hello захвата hello и обрабатывать их с другой сценарий Python.

## <a name="prerequisites"></a>Предварительные требования

- Python 2.7.x.
- Подписка Azure
- Активные [пространство имен концентраторов событий и концентратор событий](event-hubs-create.md).

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a>Создание учетной записи хранения Azure
1. Войдите на toohello [портал Azure][Azure portal].
2. В области навигации слева hello hello портала щелкните **New**, нажмите кнопку **хранилища**и нажмите кнопку **учетной записи хранилища**.
3. Заполните поля hello в колонке учетной записи хранилища hello и нажмите кнопку **создать**.
   
   ![][1]
4. После появления hello **развертывания успешно** сообщений, щелкните имя hello hello новой учетной записи хранения и в hello **Essentials** колонке нажмите кнопку **большие двоичные объекты**. Здравствуйте, когда **службе BLOB-объектов** открывается колонка, щелкните **+ контейнер** вверху hello. Имя контейнера hello **захвата**, затем закройте окно hello **службе BLOB-объектов** колонку.
5. Нажмите кнопку **ключи доступа** в hello левой колонке и скопируйте hello имя учетной записи хранилища hello и значение hello **key1**. Сохраните эти значения tooNotepad или других временное расположение.

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a>Создать концентратор событий tooyour Python сценария toosend события
1. Откройте предпочитаемый редактор Python, например [Visual Studio Code][Visual Studio Code].
2. Создайте сценарий с именем **sender.py**. Этот скрипт отправляет концентратора событий tooyour 200 событий. События представляют собой простые данные показаний среды, пересылаемые в формате JSON.
3. Вставьте следующий код в sender.py hello:
   
  ```python
  import uuid
  import datetime
  import random
  import json
  from azure.servicebus import ServiceBusService
   
  sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
  devices = []
  for x in range(0, 10):
      devices.append(str(uuid.uuid4()))
   
  for y in range(0,20):
      for dev in devices:
          reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
          s = json.dumps(reading)
          sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
      print y
  ```
4. Обновите hello, предшествующий код toouse вашего пространства имен, значение ключа и имени концентратора событий, полученный при создании имен hello концентраторов событий.

## <a name="create-a-python-script-tooread-your-capture-files"></a>Создать сценарий Python tooread записи файлов

1. Заполните колонке hello и нажмите кнопку **создать**.
2. Создайте скрипт с именем **capturereader.py**. Этот скрипт читает hello собранных файлов и создает файл на устройстве toowrite hello данных только для этого устройства.
3. Вставьте следующий код в capturereader.py hello:
   
  ```python
  import os
  import string
  import json
  import avro.schema
  from avro.datafile import DataFileReader, DataFileWriter
  from avro.io import DatumReader, DatumWriter
  from azure.storage.blob import BlockBlobService
   
  def processBlob(filename):
      reader = DataFileReader(open(filename, 'rb'), DatumReader())
      dict = {}
      for reading in reader:
          parsed_json = json.loads(reading["Body"])
          if not 'id' in parsed_json:
              return
          if not dict.has_key(parsed_json['id']):
              list = []
              dict[parsed_json['id']] = list
          else:
              list = dict[parsed_json['id']]
              list.append(parsed_json)
      reader.close()
      for device in dict.keys():
          deviceFile = open(device + '.csv', "a")
          for r in dict[device]:
              deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
  def startProcessing(accountName, key, container):
      print 'Processor started using path: ' + os.getcwd()
      block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
      generator = block_blob_service.list_blobs(container)
      for blob in generator:
          if blob.properties.content_length != 0:
              print('Downloaded a non empty blob: ' + blob.name)
              cleanName = string.replace(blob.name, '/', '_')
              block_blob_service.get_blob_to_path(container, blob.name, cleanName)
              processBlob(cleanName)
              os.remove(cleanName)
          block_blob_service.delete_blob(container, blob.name)
  startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
  ```
4. Быть убедиться, что toopaste hello соответствующие значения для имени учетной записи хранения и ключ в hello вызовов слишком`startProcessing`.

## <a name="run-hello-scripts"></a>Выполнять сценарии hello
1. Откройте командную строку с Python в пути и выполните необходимые пакеты Python tooinstall эти команды:
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  Если у вас есть более ранней версии хранилища azure или azure, может потребоваться toouse hello **--обновление** параметр
   
  Вы также могут потребоваться следующие hello toorun (не обязательно, в большинстве систем):
   
  ```
  pip install cryptography
  ```
2. Перейдите к toowherever directory сохранены sender.py и capturereader.py и выполните следующую команду:
   
  ```
  start python sender.py
  ```
   
  Эта команда запускает новый процесс отправителя hello toorun Python.
3. Теперь, подождите несколько минут для отслеживания toorun hello. Введите следующую команду в вашей исходной командное окно приветствия:
   
   ```
   python capturereader.py
   ```

   Этот процессор отслеживания использует локальный каталог toodownload hello все большие двоичные объекты hello из учетной записи хранилища hello или контейнера. Обрабатывает имена, которые не являются пустыми и hello результаты записываются в файлы CSV в локальном каталоге hello.

## <a name="next-steps"></a>Дальнейшие действия

На сайте ссылкам hello, изучите более подробную концентраторов событий:

* [Запись концентраторов событий Azure][Overview of Event Hubs Capture]
* полный [пример приложения, использующего концентраторы событий][sample application that uses Event Hubs];
* Hello [масштабирования с концентраторами событий обработки событий] [ Scale out Event Processing with Event Hubs] образца.
* [Обзор концентраторов событий Azure][Event Hubs overview].

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
