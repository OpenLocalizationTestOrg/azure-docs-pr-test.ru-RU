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
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="95d1c-103">Пошаговое руководство. Использование записи концентраторов событий с Python</span><span class="sxs-lookup"><span data-stu-id="95d1c-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="95d1c-104">Записать концентраторы событий — функция концентраторов событий, который позволяет вам tooautomatically доставки hello потоковой передачи данных в вашей tooan концентратора событий учетной записи хранилища больших двоичных объектов Azure по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="95d1c-104">Event Hubs Capture is a feature of Event Hubs that enables you tooautomatically deliver hello streaming data in your event hub tooan Azure Blob storage account of your choice.</span></span> <span data-ttu-id="95d1c-105">Эта возможность позволяет легко tooperform пакетную обработку на потоковой передачи данных в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="95d1c-105">This capability makes it easy tooperform batch processing on real-time streaming data.</span></span> <span data-ttu-id="95d1c-106">В этой статье описывается как toouse концентраторов событий захвата с Python.</span><span class="sxs-lookup"><span data-stu-id="95d1c-106">This article describes how toouse Event Hubs Capture with Python.</span></span> <span data-ttu-id="95d1c-107">Дополнительные сведения о записи концентраторов событий см. в разделе hello [обзорную статью](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95d1c-107">For more information about Event Hubs Capture, see hello [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="95d1c-108">В этом образце используется hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) функция записи toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="95d1c-108">This sample uses hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate hello Capture feature.</span></span> <span data-ttu-id="95d1c-109">Программа Hello sender.py отправляет имитацию телеметрии среды tooEvent концентраторы в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="95d1c-109">hello sender.py program sends simulated environmental telemetry tooEvent Hubs in JSON format.</span></span> <span data-ttu-id="95d1c-110">Hello концентратора событий настроен toouse hello отслеживания компонентов toowrite это хранилище tooblob данных в пакетах.</span><span class="sxs-lookup"><span data-stu-id="95d1c-110">hello event hub is configured toouse hello Capture feature toowrite this data tooblob storage in batches.</span></span> <span data-ttu-id="95d1c-111">приложение Hello capturereader.py затем считывает эти большие двоичные объекты и создает файл append на устройство, а затем записывает данные hello в CSV-файлах.</span><span class="sxs-lookup"><span data-stu-id="95d1c-111">hello capturereader.py app then reads these blobs and creates an append file per device, then writes hello data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="95d1c-112">Что будет выполнено</span><span class="sxs-lookup"><span data-stu-id="95d1c-112">What will be accomplished</span></span>

1. <span data-ttu-id="95d1c-113">Создайте учетную запись хранилища больших двоичных объектов и контейнер больших двоичных объектов, с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="95d1c-113">Create an Azure Blob Storage account and a blob container within it, using hello Azure portal.</span></span>
2. <span data-ttu-id="95d1c-114">Создайте пространство имен концентратора событий с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="95d1c-114">Create an Event Hub namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="95d1c-115">Создание концентратора событий функция отслеживания hello, включена, с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="95d1c-115">Create an event hub with hello Capture feature enabled, using hello Azure portal.</span></span>
4. <span data-ttu-id="95d1c-116">Отправка данных концентратора событий toohello сценарий Python.</span><span class="sxs-lookup"><span data-stu-id="95d1c-116">Send data toohello event hub with a Python script.</span></span>
5. <span data-ttu-id="95d1c-117">Чтение файлов hello захвата hello и обрабатывать их с другой сценарий Python.</span><span class="sxs-lookup"><span data-stu-id="95d1c-117">Read hello files from hello capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95d1c-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="95d1c-118">Prerequisites</span></span>

- <span data-ttu-id="95d1c-119">Python 2.7.x.</span><span class="sxs-lookup"><span data-stu-id="95d1c-119">Python 2.7.x</span></span>
- <span data-ttu-id="95d1c-120">Подписка Azure</span><span class="sxs-lookup"><span data-stu-id="95d1c-120">An Azure subscription</span></span>
- <span data-ttu-id="95d1c-121">Активные [пространство имен концентраторов событий и концентратор событий](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="95d1c-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="95d1c-122">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="95d1c-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="95d1c-123">Войдите на toohello [портал Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="95d1c-123">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="95d1c-124">В области навигации слева hello hello портала щелкните **New**, нажмите кнопку **хранилища**и нажмите кнопку **учетной записи хранилища**.</span><span class="sxs-lookup"><span data-stu-id="95d1c-124">In hello left navigation pane of hello portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="95d1c-125">Заполните поля hello в колонке учетной записи хранилища hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="95d1c-125">Complete hello fields in hello storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="95d1c-126">После появления hello **развертывания успешно** сообщений, щелкните имя hello hello новой учетной записи хранения и в hello **Essentials** колонке нажмите кнопку **большие двоичные объекты**.</span><span class="sxs-lookup"><span data-stu-id="95d1c-126">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account and in hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="95d1c-127">Здравствуйте, когда **службе BLOB-объектов** открывается колонка, щелкните **+ контейнер** вверху hello.</span><span class="sxs-lookup"><span data-stu-id="95d1c-127">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="95d1c-128">Имя контейнера hello **захвата**, затем закройте окно hello **службе BLOB-объектов** колонку.</span><span class="sxs-lookup"><span data-stu-id="95d1c-128">Name hello container **capture**, then close hello **Blob service** blade.</span></span>
5. <span data-ttu-id="95d1c-129">Нажмите кнопку **ключи доступа** в hello левой колонке и скопируйте hello имя учетной записи хранилища hello и значение hello **key1**.</span><span class="sxs-lookup"><span data-stu-id="95d1c-129">Click **Access keys** in hello left blade and copy hello name of hello storage account and hello value of **key1**.</span></span> <span data-ttu-id="95d1c-130">Сохраните эти значения tooNotepad или других временное расположение.</span><span class="sxs-lookup"><span data-stu-id="95d1c-130">Save these values tooNotepad or some other temporary location.</span></span>

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a><span data-ttu-id="95d1c-131">Создать концентратор событий tooyour Python сценария toosend события</span><span class="sxs-lookup"><span data-stu-id="95d1c-131">Create a Python script toosend events tooyour event hub</span></span>
1. <span data-ttu-id="95d1c-132">Откройте предпочитаемый редактор Python, например [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="95d1c-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="95d1c-133">Создайте сценарий с именем **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="95d1c-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="95d1c-134">Этот скрипт отправляет концентратора событий tooyour 200 событий.</span><span class="sxs-lookup"><span data-stu-id="95d1c-134">This script sends 200 events tooyour event hub.</span></span> <span data-ttu-id="95d1c-135">События представляют собой простые данные показаний среды, пересылаемые в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="95d1c-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="95d1c-136">Вставьте следующий код в sender.py hello:</span><span class="sxs-lookup"><span data-stu-id="95d1c-136">Paste hello following code into sender.py:</span></span>
   
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
4. <span data-ttu-id="95d1c-137">Обновите hello, предшествующий код toouse вашего пространства имен, значение ключа и имени концентратора событий, полученный при создании имен hello концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="95d1c-137">Update hello preceding code toouse your namespace name, key value, and event hub name that you obtained when you created hello Event Hubs namespace.</span></span>

## <a name="create-a-python-script-tooread-your-capture-files"></a><span data-ttu-id="95d1c-138">Создать сценарий Python tooread записи файлов</span><span class="sxs-lookup"><span data-stu-id="95d1c-138">Create a Python script tooread your Capture files</span></span>

1. <span data-ttu-id="95d1c-139">Заполните колонке hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="95d1c-139">Fill out hello blade and click **Create**.</span></span>
2. <span data-ttu-id="95d1c-140">Создайте скрипт с именем **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="95d1c-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="95d1c-141">Этот скрипт читает hello собранных файлов и создает файл на устройстве toowrite hello данных только для этого устройства.</span><span class="sxs-lookup"><span data-stu-id="95d1c-141">This script reads hello captured files and creates a file per device toowrite hello data only for that device.</span></span>
3. <span data-ttu-id="95d1c-142">Вставьте следующий код в capturereader.py hello:</span><span class="sxs-lookup"><span data-stu-id="95d1c-142">Paste hello following code into capturereader.py:</span></span>
   
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
4. <span data-ttu-id="95d1c-143">Быть убедиться, что toopaste hello соответствующие значения для имени учетной записи хранения и ключ в hello вызовов слишком`startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="95d1c-143">Be sure toopaste hello appropriate values for your storage account name and key in hello call too`startProcessing`.</span></span>

## <a name="run-hello-scripts"></a><span data-ttu-id="95d1c-144">Выполнять сценарии hello</span><span class="sxs-lookup"><span data-stu-id="95d1c-144">Run hello scripts</span></span>
1. <span data-ttu-id="95d1c-145">Откройте командную строку с Python в пути и выполните необходимые пакеты Python tooinstall эти команды:</span><span class="sxs-lookup"><span data-stu-id="95d1c-145">Open a command prompt that has Python in its path, and then run these commands tooinstall Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="95d1c-146">Если у вас есть более ранней версии хранилища azure или azure, может потребоваться toouse hello **--обновление** параметр</span><span class="sxs-lookup"><span data-stu-id="95d1c-146">If you have an earlier version of either azure-storage or azure, you may need toouse hello **--upgrade** option</span></span>
   
  <span data-ttu-id="95d1c-147">Вы также могут потребоваться следующие hello toorun (не обязательно, в большинстве систем):</span><span class="sxs-lookup"><span data-stu-id="95d1c-147">You might also need toorun hello following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="95d1c-148">Перейдите к toowherever directory сохранены sender.py и capturereader.py и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="95d1c-148">Change your directory toowherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="95d1c-149">Эта команда запускает новый процесс отправителя hello toorun Python.</span><span class="sxs-lookup"><span data-stu-id="95d1c-149">This command starts a new Python process toorun hello sender.</span></span>
3. <span data-ttu-id="95d1c-150">Теперь, подождите несколько минут для отслеживания toorun hello.</span><span class="sxs-lookup"><span data-stu-id="95d1c-150">Now wait a few minutes for hello capture toorun.</span></span> <span data-ttu-id="95d1c-151">Введите следующую команду в вашей исходной командное окно приветствия:</span><span class="sxs-lookup"><span data-stu-id="95d1c-151">Then type hello following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="95d1c-152">Этот процессор отслеживания использует локальный каталог toodownload hello все большие двоичные объекты hello из учетной записи хранилища hello или контейнера.</span><span class="sxs-lookup"><span data-stu-id="95d1c-152">This capture processor uses hello local directory toodownload all hello blobs from hello storage account/container.</span></span> <span data-ttu-id="95d1c-153">Обрабатывает имена, которые не являются пустыми и hello результаты записываются в файлы CSV в локальном каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="95d1c-153">It processes any that are not empty, and writes hello results as .csv files into hello local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95d1c-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="95d1c-154">Next steps</span></span>

<span data-ttu-id="95d1c-155">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="95d1c-155">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="95d1c-156">[Запись концентраторов событий Azure][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="95d1c-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="95d1c-157">полный [пример приложения, использующего концентраторы событий][sample application that uses Event Hubs];</span><span class="sxs-lookup"><span data-stu-id="95d1c-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="95d1c-158">Hello [масштабирования с концентраторами событий обработки событий] [ Scale out Event Processing with Event Hubs] образца.</span><span class="sxs-lookup"><span data-stu-id="95d1c-158">hello [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="95d1c-159">[Обзор концентраторов событий Azure][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="95d1c-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
