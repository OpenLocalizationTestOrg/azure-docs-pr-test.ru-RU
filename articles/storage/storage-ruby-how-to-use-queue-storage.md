---
title: "aaaHow toouse хранилища очередей из Ruby | Документы Microsoft"
description: "Узнайте, как toocreate службы очередей Azure hello toouse и очереди delete и insert, получение и удаление сообщений. Примеры кода написаны на Ruby."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a><span data-ttu-id="040c1-104">Как toouse хранилища очередей из Ruby</span><span class="sxs-lookup"><span data-stu-id="040c1-104">How toouse Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="040c1-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="040c1-105">Overview</span></span>
<span data-ttu-id="040c1-106">В этом руководстве показано, как tooperform распространенных сценариев использования hello службы хранилища очередей Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="040c1-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="040c1-107">образцы Hello записываются с помощью API-интерфейса Azure Ruby hello.</span><span class="sxs-lookup"><span data-stu-id="040c1-107">hello samples are written using hello Ruby Azure API.</span></span>
<span data-ttu-id="040c1-108">Hello сценарии включают **Вставка**, **Просмотр**, **начало**, и **удаление** очередь сообщений, а также  **Создание и удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="040c1-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="040c1-109">Создание приложения Ruby</span><span class="sxs-lookup"><span data-stu-id="040c1-109">Create a Ruby Application</span></span>
<span data-ttu-id="040c1-110">Создайте приложение Ruby.</span><span class="sxs-lookup"><span data-stu-id="040c1-110">Create a Ruby application.</span></span> <span data-ttu-id="040c1-111">Инструкции см. в разделе [Веб-приложение Ruby on Rails на виртуальной машине Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="040c1-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="040c1-112">Настройка приложения tooAccess хранилища</span><span class="sxs-lookup"><span data-stu-id="040c1-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="040c1-113">toouse хранилища Azure, понадобится toodownload и используйте hello Ruby azure пакет, который включает в себя набор библиотек удобства, взаимодействующих со службами REST hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="040c1-113">toouse Azure storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="040c1-114">Используйте RubyGems tooobtain hello пакет</span><span class="sxs-lookup"><span data-stu-id="040c1-114">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="040c1-115">Используйте интерфейс командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="040c1-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="040c1-116">Введите команду «gem Установка azure» в hello команда окна tooinstall hello gem и зависимости.</span><span class="sxs-lookup"><span data-stu-id="040c1-116">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="040c1-117">Импорт пакета hello</span><span class="sxs-lookup"><span data-stu-id="040c1-117">Import hello package</span></span>
<span data-ttu-id="040c1-118">Используйте текстовый редактор, добавить следующие toohello вверху hello Ruby файл, куда будет toouse хранилища hello:</span><span class="sxs-lookup"><span data-stu-id="040c1-118">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="040c1-119">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="040c1-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="040c1-120">модуль Hello azure будет считывать переменные среды hello **AZURE\_ХРАНЕНИЯ\_учетной записи** и **AZURE\_ХРАНЕНИЯ\_ключ_доступа** для сведения, необходимые учетной записи хранилища Azure tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="040c1-120">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="040c1-121">Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello перед использованием **Azure::QueueService** с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="040c1-121">If these environment variables are not set, you must specify hello account information before using **Azure::QueueService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="040c1-122">tooobtain эти значения из классические или диспетчер ресурсов хранилища учетной записи в hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="040c1-122">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="040c1-123">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="040c1-123">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="040c1-124">Перейдите toohello необходимом toouse учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="040c1-124">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="040c1-125">В колонке параметров hello на hello вправо, щелкните **клавиши доступа**.</span><span class="sxs-lookup"><span data-stu-id="040c1-125">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="040c1-126">В колонке ключи hello доступа, отображается вы увидите ключ доступа hello 1 и ключ доступа 2.</span><span class="sxs-lookup"><span data-stu-id="040c1-126">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="040c1-127">Можно использовать любой из них.</span><span class="sxs-lookup"><span data-stu-id="040c1-127">You can use either of these.</span></span> 
5. <span data-ttu-id="040c1-128">Щелкните hello скопировать значок toocopy hello ключа toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="040c1-128">Click hello copy icon toocopy hello key toohello clipboard.</span></span> 

<span data-ttu-id="040c1-129">Эти значения из классической хранилища учетной записи в классический портал Azure hello tooobtain:</span><span class="sxs-lookup"><span data-stu-id="040c1-129">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="040c1-130">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="040c1-130">Log in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="040c1-131">Перейдите toohello необходимом toouse учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="040c1-131">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="040c1-132">Нажмите кнопку **УПРАВЛЕНИЕ КЛЮЧАМИ доступа** hello нижней части панели навигации hello.</span><span class="sxs-lookup"><span data-stu-id="040c1-132">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="040c1-133">В hello всплывающее диалоговое окно вы увидите имя учетной записи хранения hello, первичный ключ доступа и вторичный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="040c1-133">In hello pop up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="040c1-134">Клавиша доступа можно использовать hello первичной или вторичной hello.</span><span class="sxs-lookup"><span data-stu-id="040c1-134">For access key, you can use either hello primary one or hello secondary one.</span></span> 
5. <span data-ttu-id="040c1-135">Щелкните hello скопировать значок toocopy hello ключа toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="040c1-135">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="040c1-136">Практическое руководство. Создание очереди</span><span class="sxs-lookup"><span data-stu-id="040c1-136">How To: Create a Queue</span></span>
<span data-ttu-id="040c1-137">Hello следующий код создает **Azure::QueueService** объекта, который позволяет toowork с очередями.</span><span class="sxs-lookup"><span data-stu-id="040c1-137">hello following code creates a **Azure::QueueService** object, which enables you toowork with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="040c1-138">Используйте hello **create_queue()** toocreate метод очередь с hello заданное имя.</span><span class="sxs-lookup"><span data-stu-id="040c1-138">Use hello **create_queue()** method toocreate a queue with hello specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="040c1-139">Практическое руководство. Вставка сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="040c1-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="040c1-140">tooinsert сообщения в очереди, используйте hello **create_message()** toocreate метод новое сообщение и добавьте его toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="040c1-140">tooinsert a message into a queue, use hello **create_message()** method toocreate a new message and add it toohello queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="040c1-141">Практическое руководство: Просмотр следующего сообщения hello</span><span class="sxs-lookup"><span data-stu-id="040c1-141">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="040c1-142">Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **peek\_messages()** метод.</span><span class="sxs-lookup"><span data-stu-id="040c1-142">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages()** method.</span></span> <span data-ttu-id="040c1-143">По умолчанию метод **peek\_messages()** просматривает одно сообщение.</span><span class="sxs-lookup"><span data-stu-id="040c1-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="040c1-144">Можно также указать, сколько сообщений требуется toopeek.</span><span class="sxs-lookup"><span data-stu-id="040c1-144">You can also specify how many messages you want toopeek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="040c1-145">Практическое руководство: Следующее сообщение hello вывода из очереди</span><span class="sxs-lookup"><span data-stu-id="040c1-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="040c1-146">Вы можете удалить сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="040c1-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="040c1-147">При вызове **списка\_messages()**, получить следующее сообщение hello в очередь по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="040c1-147">When you call **list\_messages()**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="040c1-148">Можно также указать, сколько сообщений требуется tooget.</span><span class="sxs-lookup"><span data-stu-id="040c1-148">You can also specify how many messages you want tooget.</span></span> <span data-ttu-id="040c1-149">Здравствуйте, сообщения, возвращаемые из **списка\_messages()** становится невидимой tooany другой код, чтение сообщений из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="040c1-149">hello messages returned from **list\_messages()** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="040c1-150">Передать hello видимость тайм-аута в секундах в виде параметра.</span><span class="sxs-lookup"><span data-stu-id="040c1-150">You pass in hello visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="040c1-151">toofinish удаление приветственное сообщение из очереди hello, необходимо также вызвать **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="040c1-151">toofinish removing hello message from hello queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="040c1-152">Это двухэтапный процесс удаления сообщения гарантирует, что при tooprocess завершается с ошибкой вашего кода, получит сообщение из-за toohardware или ошибок программного обеспечения, другой экземпляр кода hello же сообщение и повторите.</span><span class="sxs-lookup"><span data-stu-id="040c1-152">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="040c1-153">Вызовы кода **удаление\_message()** сразу после обработки сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="040c1-153">Your code calls **delete\_message()** right after hello message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="040c1-154">Практическое руководство: Изменение содержимого hello сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="040c1-154">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="040c1-155">Вы можете изменить содержимое сообщений на месте в очереди hello hello.</span><span class="sxs-lookup"><span data-stu-id="040c1-155">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="040c1-156">Приведенный ниже код Hello использует hello **update_message()** tooupdate метод сообщение.</span><span class="sxs-lookup"><span data-stu-id="040c1-156">hello code below uses hello **update_message()** method tooupdate a message.</span></span> <span data-ttu-id="040c1-157">метод Hello возвращает кортеж, содержащий hello подтверждение сообщения в очереди hello и UTC значения даты-времени, представляющая hello сообщение будет видимо в очереди hello.</span><span class="sxs-lookup"><span data-stu-id="040c1-157">hello method will return a tuple which contains hello pop receipt of hello queue message and a UTC date time value that represents when hello message will be visible on hello queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="040c1-158">Практическое руководство. Использование дополнительных параметров для удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="040c1-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="040c1-159">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="040c1-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="040c1-160">Можно получить пакет сообщения.</span><span class="sxs-lookup"><span data-stu-id="040c1-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="040c1-161">Можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="040c1-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="040c1-162">Hello следующий пример кода использует hello **списка\_messages()** метод tooget 15 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="040c1-162">hello following code example uses hello **list\_messages()** method tooget 15 messages in one call.</span></span> <span data-ttu-id="040c1-163">Затем код выводит и удаляет все сообщения.</span><span class="sxs-lookup"><span data-stu-id="040c1-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="040c1-164">Он также устанавливает минут toofive hello невидимости время ожидания для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="040c1-164">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="040c1-165">Практическое руководство: Получение hello длина очереди</span><span class="sxs-lookup"><span data-stu-id="040c1-165">How To: Get hello Queue Length</span></span>
<span data-ttu-id="040c1-166">Можно получить оценки hello количество сообщений в очереди hello.</span><span class="sxs-lookup"><span data-stu-id="040c1-166">You can get an estimation of hello number of messages in hello queue.</span></span> <span data-ttu-id="040c1-167">Hello **получить\_очереди\_metadata()** метод запрашивает hello очереди службы tooreturn hello приблизительное количество сообщений и метаданные о hello очереди.</span><span class="sxs-lookup"><span data-stu-id="040c1-167">hello **get\_queue\_metadata()** method asks hello queue service tooreturn hello approximate message count and metadata about hello queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="040c1-168">Практическое руководство. Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="040c1-168">How To: Delete a Queue</span></span>
<span data-ttu-id="040c1-169">toodelete все сообщения hello и очереди содержащиеся в нем, вызов hello **удаление\_queue()** метод hello объекта очереди.</span><span class="sxs-lookup"><span data-stu-id="040c1-169">toodelete a queue and all hello messages contained in it, call hello **delete\_queue()** method on hello queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="040c1-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="040c1-170">Next Steps</span></span>
<span data-ttu-id="040c1-171">Теперь, когда вы узнали основы hello хранилища очередей, выполните эти ссылки toolearn о более сложных задач хранилища.</span><span class="sxs-lookup"><span data-stu-id="040c1-171">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="040c1-172">Посетите hello [блог группы разработчиков хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="040c1-172">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="040c1-173">Посетите hello [пакет Azure SDK для Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) репозитория в GitHub</span><span class="sxs-lookup"><span data-stu-id="040c1-173">Visit hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="040c1-174">Сравнение между hello службы очередей Azure, рассматриваемые в данной статье, рассматриваемые в hello очереди шины обслуживания Azure [как toouse очереди Service Bus](/develop/ruby/how-to-guides/service-bus-queues/) статьи см. в разделе [очереди Azure и очереди шины обслуживания — сравнение и Отличия](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="040c1-174">For a comparison between hello Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in hello [How toouse Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>
