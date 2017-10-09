---
title: "aaaSave концентратор IoT сообщений хранения данных tooAzure | Документы Microsoft"
description: "Используйте приложение Azure функция toosave вашей tooyour сообщений концентратора IoT табличного хранилища Azure. Hello IoT hub сообщения содержат сведения, такие как данные датчика, отправленные с вашего устройства IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "хранилище данных Центра Интернета вещей, хранилище для данных датчиков Центра Интернета вещей"
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a><span data-ttu-id="49476-105">Сохранить сообщения концентратора IoT, содержащие датчиков данных tooyour табличного хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="49476-105">Save IoT hub messages that contain sensor data tooyour Azure table storage</span></span>

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="49476-107">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="49476-107">What you learn</span></span>

<span data-ttu-id="49476-108">Вы узнаете, как toocreate учетную запись хранилища Azure и Azure функцию сообщения концентратора IoT toostore приложения в хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="49476-108">You learn how toocreate an Azure storage account and an Azure function app toostore IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="49476-109">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="49476-109">What you do</span></span>

- <span data-ttu-id="49476-110">Создайте учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="49476-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="49476-111">Подготовьте ваш центр IoT сообщений tooread подключения.</span><span class="sxs-lookup"><span data-stu-id="49476-111">Prepare your IoT hub connection tooread messages.</span></span>
- <span data-ttu-id="49476-112">Создайте приложение-функцию Azure и разверните его.</span><span class="sxs-lookup"><span data-stu-id="49476-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="49476-113">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="49476-113">What you need</span></span>

- <span data-ttu-id="49476-114">[Настройка устройства](iot-hub-raspberry-pi-kit-node-get-started.md) hello toocover следующие требования:</span><span class="sxs-lookup"><span data-stu-id="49476-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello following requirements:</span></span>
  - <span data-ttu-id="49476-115">активная подписка Azure;</span><span class="sxs-lookup"><span data-stu-id="49476-115">An active Azure subscription</span></span>
  - <span data-ttu-id="49476-116">Центр Интернета вещей в подписке;</span><span class="sxs-lookup"><span data-stu-id="49476-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="49476-117">Приложения, отправляющего сообщения tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="49476-117">A running application that sends messages tooyour IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="49476-118">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="49476-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="49476-119">В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **New** > **хранения** > **учетной записи хранилища**  >   **Создание**.</span><span class="sxs-lookup"><span data-stu-id="49476-119">In hello [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="49476-120">Введите hello необходимые сведения для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="49476-120">Enter hello necessary information for hello storage account:</span></span>

   ![Создать учетную запись хранилища в hello портал Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="49476-122">**Имя**: hello имя учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="49476-122">**Name**: hello name of hello storage account.</span></span> <span data-ttu-id="49476-123">Hello имя должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="49476-123">hello name must be globally unique.</span></span>

   * <span data-ttu-id="49476-124">**Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="49476-124">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="49476-125">**ПИН-код toodashboard**: выберите этот параметр для облегчения доступа центра IoT tooyour из панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="49476-125">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

3. <span data-ttu-id="49476-126">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="49476-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a><span data-ttu-id="49476-127">Подготовка концентратор IoT сообщений tooread подключения</span><span class="sxs-lookup"><span data-stu-id="49476-127">Prepare your IoT hub connection tooread messages</span></span>

<span data-ttu-id="49476-128">Центр IoT представлено встроенные события концентратора совместимой конечной точки tooenable приложений tooread IoT hub сообщений.</span><span class="sxs-lookup"><span data-stu-id="49476-128">IoT hub exposes a built-in event hub-compatible endpoint tooenable applications tooread IoT hub messages.</span></span> <span data-ttu-id="49476-129">В то же время приложения используют потребителя данных tooread групп из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="49476-129">Meanwhile, applications use consumer groups tooread data from your IoT hub.</span></span> <span data-ttu-id="49476-130">Перед созданием Azure функций приложения tooread данных-концентратор IoT hello следующие:</span><span class="sxs-lookup"><span data-stu-id="49476-130">Before you create an Azure function app tooread data from your IoT hub, do hello following:</span></span>

- <span data-ttu-id="49476-131">Получите строку hello подключения из вашей конечной точки центра IoT.</span><span class="sxs-lookup"><span data-stu-id="49476-131">Get hello connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="49476-132">создать группу потребителей для Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="49476-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="49476-133">Получить строку hello подключения из вашей конечной точки центра IoT</span><span class="sxs-lookup"><span data-stu-id="49476-133">Get hello connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="49476-134">Откройте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="49476-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="49476-135">На hello **центр IoT** панели в разделе **обмен сообщениями**, нажмите кнопку **конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="49476-135">On hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="49476-136">В hello правой панели в разделе **встроенных конечных точек**, нажмите кнопку **события**.</span><span class="sxs-lookup"><span data-stu-id="49476-136">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="49476-137">В hello **свойства** области, Примечание hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="49476-137">In hello **Properties** pane, note hello following values:</span></span>
   - <span data-ttu-id="49476-138">конечная точка, совместимая с концентратором событий;</span><span class="sxs-lookup"><span data-stu-id="49476-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="49476-139">имя, совместимое с концентратором событий.</span><span class="sxs-lookup"><span data-stu-id="49476-139">Event hub-compatible name</span></span>

   ![Получить строку подключения к конечной точки центра IoT hello в hello портал Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="49476-141">В hello **центр IoT** панели в разделе **параметры**, нажмите кнопку **политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="49476-141">In hello **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="49476-142">Щелкните **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="49476-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="49476-143">Примечание hello **первичного ключа** значение.</span><span class="sxs-lookup"><span data-stu-id="49476-143">Note hello **Primary key** value.</span></span>

8. <span data-ttu-id="49476-144">Создайте hello строка подключения к конечной точки центра IoT следующим образом:</span><span class="sxs-lookup"><span data-stu-id="49476-144">Create hello connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="49476-145">Замените `<Event Hub-compatible endpoint>` и `<Primary key>` со значениями hello, записанные ранее.</span><span class="sxs-lookup"><span data-stu-id="49476-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with hello values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="49476-146">Создание группы потребителей для Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="49476-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="49476-147">Откройте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="49476-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="49476-148">В hello **центр IoT** панели в разделе **обмен сообщениями**, нажмите кнопку **конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="49476-148">In hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="49476-149">В hello правой панели в разделе **встроенных конечных точек**, нажмите кнопку **события**.</span><span class="sxs-lookup"><span data-stu-id="49476-149">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="49476-150">В hello **свойства** панели в разделе **групп потребителей**, введите имя, а затем запишите его.</span><span class="sxs-lookup"><span data-stu-id="49476-150">In hello **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="49476-151">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="49476-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="49476-152">Создание и развертывание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="49476-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="49476-153">В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **New** > **вычислений** > **функции приложения**  >   **Создание**.</span><span class="sxs-lookup"><span data-stu-id="49476-153">In hello [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="49476-154">Введите необходимые сведения hello для функции приложение hello.</span><span class="sxs-lookup"><span data-stu-id="49476-154">Enter hello necessary information for hello function app.</span></span>

   ![Создание приложения функции в hello портал Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="49476-156">**Имя приложения**: hello имя функции приложение hello.</span><span class="sxs-lookup"><span data-stu-id="49476-156">**App name**: hello name of hello function app.</span></span> <span data-ttu-id="49476-157">Hello имя должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="49476-157">hello name must be globally unique.</span></span>

   * <span data-ttu-id="49476-158">**Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="49476-158">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="49476-159">**Учетная запись хранения**: hello созданной учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="49476-159">**Storage Account**: hello storage account that you created.</span></span>

   * <span data-ttu-id="49476-160">**ПИН-код toodashboard**: выберите этот параметр для приложения функции toohello простой доступ из панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="49476-160">**Pin toodashboard**: Check this option for easy access toohello function app from hello dashboard.</span></span>

3. <span data-ttu-id="49476-161">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="49476-161">Click **Create**.</span></span>

4. <span data-ttu-id="49476-162">После создания функции приложение hello, откройте его.</span><span class="sxs-lookup"><span data-stu-id="49476-162">After hello function app has been created, open it.</span></span>

5. <span data-ttu-id="49476-163">В приложении функции hello создайте новую функцию, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="49476-163">In hello function app, create a new function by doing hello following:</span></span>

   <span data-ttu-id="49476-164">а.</span><span class="sxs-lookup"><span data-stu-id="49476-164">a.</span></span> <span data-ttu-id="49476-165">Щелкните **Новая функция**.</span><span class="sxs-lookup"><span data-stu-id="49476-165">Click **New Function**.</span></span>

   <span data-ttu-id="49476-166">b.</span><span class="sxs-lookup"><span data-stu-id="49476-166">b.</span></span> <span data-ttu-id="49476-167">Для параметра **Язык** выберите **JavaScript**, а для **Сценарий** — **Обработка данных**.</span><span class="sxs-lookup"><span data-stu-id="49476-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="49476-168">c.</span><span class="sxs-lookup"><span data-stu-id="49476-168">c.</span></span> <span data-ttu-id="49476-169">Щелкните **Создайте эту функцию**, а затем — выберите **Новая функция**.</span><span class="sxs-lookup"><span data-stu-id="49476-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="49476-170">d.</span><span class="sxs-lookup"><span data-stu-id="49476-170">d.</span></span> <span data-ttu-id="49476-171">Выберите **JavaScript** для языка hello и **обработки данных** для сценария hello.</span><span class="sxs-lookup"><span data-stu-id="49476-171">Select **JavaScript** for hello language, and **Data Processing** for hello scenario.</span></span>

   <span data-ttu-id="49476-172">д.</span><span class="sxs-lookup"><span data-stu-id="49476-172">e.</span></span> <span data-ttu-id="49476-173">Нажмите кнопку hello **EventHubTrigger JavaScript** шаблона.</span><span class="sxs-lookup"><span data-stu-id="49476-173">Click hello **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="49476-174">f.</span><span class="sxs-lookup"><span data-stu-id="49476-174">f.</span></span> <span data-ttu-id="49476-175">Введите необходимые сведения hello для шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="49476-175">Enter hello necessary information for hello template.</span></span>

      * <span data-ttu-id="49476-176">**Имя функции**: hello имя функции hello.</span><span class="sxs-lookup"><span data-stu-id="49476-176">**Name your function**: hello name of hello function.</span></span>

      * <span data-ttu-id="49476-177">**Имя концентратора событий**: hello события концентратора совместимое имя, записанное ранее.</span><span class="sxs-lookup"><span data-stu-id="49476-177">**Event Hub name**: hello event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="49476-178">**Подключение концентратора событий**: щелкните строку подключения hello tooadd hello IoT hub созданной конечной точке, **New**.</span><span class="sxs-lookup"><span data-stu-id="49476-178">**Event Hub connection**: tooadd hello connection string of hello IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="49476-179">ж.</span><span class="sxs-lookup"><span data-stu-id="49476-179">g.</span></span> <span data-ttu-id="49476-180">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="49476-180">Click **Create**.</span></span>

6. <span data-ttu-id="49476-181">Настройка выхода функции hello, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="49476-181">Configure an output of hello function by doing hello following:</span></span>

   <span data-ttu-id="49476-182">а.</span><span class="sxs-lookup"><span data-stu-id="49476-182">a.</span></span> <span data-ttu-id="49476-183">Щелкните **Интегрировать** > **Новое выходное значение** > **Хранилище таблиц Azure** > **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="49476-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Добавление таблицы хранилища tooyour функции приложения в hello портал Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="49476-185">b.</span><span class="sxs-lookup"><span data-stu-id="49476-185">b.</span></span> <span data-ttu-id="49476-186">Введите необходимые сведения hello.</span><span class="sxs-lookup"><span data-stu-id="49476-186">Enter hello necessary information.</span></span>

      * <span data-ttu-id="49476-187">**Имя параметра таблицы**: использование `outputTable`, который будет использоваться в hello Azure кода функции.</span><span class="sxs-lookup"><span data-stu-id="49476-187">**Table parameter name**: Use `outputTable`, which will be used in hello Azure function's code.</span></span>
      
      * <span data-ttu-id="49476-188">**Имя таблицы**. Используйте `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="49476-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="49476-189">**Подключение к учетной записи хранения**. Щелкните **Новые** и выберите или введите свою учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="49476-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="49476-190">Если учетная запись хранения hello не отображается, см. раздел [требования к учетной записи хранилища](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="49476-190">If hello storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="49476-191">c.</span><span class="sxs-lookup"><span data-stu-id="49476-191">c.</span></span> <span data-ttu-id="49476-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="49476-192">Click **Save**.</span></span>

7. <span data-ttu-id="49476-193">В разделе **Триггеры** щелкните **Концентратор событий Azure (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="49476-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="49476-194">В разделе **группы потребителей концентратора событий**, введите имя группы потребителей hello, который был создан и нажмите кнопку hello **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="49476-194">Under **Event Hub consumer group**, enter hello name of hello consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="49476-195">Нажмите кнопку функции hello, созданный для hello слева, а затем нажмите кнопку **Просмотр файлов** на hello вправо.</span><span class="sxs-lookup"><span data-stu-id="49476-195">Click hello function you've created on hello left and then click **View Files** on hello right.</span></span>

10. <span data-ttu-id="49476-196">Замените код hello в `index.js` hello следующее:</span><span class="sxs-lookup"><span data-stu-id="49476-196">Replace hello code in `index.js` with hello following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. <span data-ttu-id="49476-197">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="49476-197">Click **Save**.</span></span>

<span data-ttu-id="49476-198">Вы создали приложение функции hello.</span><span class="sxs-lookup"><span data-stu-id="49476-198">You have now created hello function app.</span></span> <span data-ttu-id="49476-199">Приложение-функция сохраняет сообщения, которые получает Центр Интернета вещей в хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="49476-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="49476-200">Можно использовать hello **запуска** приложение функции hello tootest кнопки.</span><span class="sxs-lookup"><span data-stu-id="49476-200">You can use hello **Run** button tootest hello function app.</span></span> <span data-ttu-id="49476-201">При нажатии кнопки **запуска**, отправлено тестовое сообщение hello tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="49476-201">When you click **Run**, hello test message is sent tooyour IoT hub.</span></span> <span data-ttu-id="49476-202">Hello прибытия сообщения hello следует активировать toostart приложения hello функции, а затем сохраните хранилище таблиц tooyour сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="49476-202">hello arrival of hello message should trigger hello function app toostart and then save hello message tooyour table storage.</span></span> <span data-ttu-id="49476-203">Hello **журналы** области Подробности hello hello процесса.</span><span class="sxs-lookup"><span data-stu-id="49476-203">hello **Logs** pane records hello details of hello process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="49476-204">Проверка сообщений в хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="49476-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="49476-205">Запустите образец приложения hello на концентратор IoT tooyour устройства toosend сообщений.</span><span class="sxs-lookup"><span data-stu-id="49476-205">Run hello sample application on your device toosend messages tooyour IoT hub.</span></span>

2. <span data-ttu-id="49476-206">[Скачайте и установите обозреватель хранилищ Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="49476-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="49476-207">Откройте обозреватель хранилищ, щелкните **добавьте учетную запись Azure** > **вход**и выполните вход в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="49476-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in tooyour Azure account.</span></span>

4. <span data-ttu-id="49476-208">Щелкните подписку Azure > **Учетные записи хранения** > ваша учетная запись хранения > **Таблицы** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="49476-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="49476-209">Вы увидите сообщений, отправленных из вашего центра IoT tooyour устройства вход hello `deviceData` таблицы.</span><span class="sxs-lookup"><span data-stu-id="49476-209">You should see messages sent from your device tooyour IoT hub logged in hello `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49476-210">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="49476-210">Next steps</span></span>

<span data-ttu-id="49476-211">Вы успешно создали учетную запись хранения Azure и приложение-функцию Azure, которое сохраняет сообщения, поступающие в Центр Интернета вещей, в хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="49476-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
