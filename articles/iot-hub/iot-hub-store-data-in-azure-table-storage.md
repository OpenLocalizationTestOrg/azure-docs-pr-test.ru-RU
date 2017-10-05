---
title: "Сохранение сообщений Центра Интернета вещей в хранилище данных Azure | Документация Майкрософт"
description: "Сохранение сообщений Центра Интернета вещей в хранилище таблиц Azure с помощью приложения-функции Azure. Сообщения Центра Интернета вещей содержат такие сведения, как данные датчиков, отправленные из устройства Интернета вещей."
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
ms.openlocfilehash: 06503f9564e00ef62587d02f2da4778974e246c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-to-your-azure-table-storage"></a><span data-ttu-id="b158d-105">Сохранение сообщений Центра Интернета вещей, которые содержат данные датчиков, в хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="b158d-105">Save IoT hub messages that contain sensor data to your Azure table storage</span></span>

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="b158d-107">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="b158d-107">What you learn</span></span>

<span data-ttu-id="b158d-108">Вы узнаете, как создать учетную запись хранения Azure и приложение-функцию Azure для сохранения сообщений Центра Интернета вещей в хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="b158d-108">You learn how to create an Azure storage account and an Azure function app to store IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="b158d-109">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="b158d-109">What you do</span></span>

- <span data-ttu-id="b158d-110">Создайте учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b158d-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="b158d-111">Выполните подготовку к подключению Центра Интернета вещей для чтения сообщений.</span><span class="sxs-lookup"><span data-stu-id="b158d-111">Prepare your IoT hub connection to read messages.</span></span>
- <span data-ttu-id="b158d-112">Создайте приложение-функцию Azure и разверните его.</span><span class="sxs-lookup"><span data-stu-id="b158d-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b158d-113">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="b158d-113">What you need</span></span>

- <span data-ttu-id="b158d-114">[Настройте свое устройство](iot-hub-raspberry-pi-kit-node-get-started.md). У вас должны быть следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="b158d-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) to cover the following requirements:</span></span>
  - <span data-ttu-id="b158d-115">активная подписка Azure;</span><span class="sxs-lookup"><span data-stu-id="b158d-115">An active Azure subscription</span></span>
  - <span data-ttu-id="b158d-116">Центр Интернета вещей в подписке;</span><span class="sxs-lookup"><span data-stu-id="b158d-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="b158d-117">работающее приложение, отправляющее сообщения в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b158d-117">A running application that sends messages to your IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="b158d-118">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="b158d-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="b158d-119">На [портале Azure](https://portal.azure.com/) щелкните **Создать** > **Хранилище** > **Учетная запись хранения** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b158d-119">In the [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="b158d-120">Введите необходимые сведения для учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="b158d-120">Enter the necessary information for the storage account:</span></span>

   ![Создание учетной записи хранения на портале Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="b158d-122">**Имя**. Имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b158d-122">**Name**: The name of the storage account.</span></span> <span data-ttu-id="b158d-123">Оно должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="b158d-123">The name must be globally unique.</span></span>

   * <span data-ttu-id="b158d-124">**Группа ресурсов**. Выберите ту же группу ресурсов, которую использует Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b158d-124">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="b158d-125">**Закрепить на панели мониторинга.** Установите этот флажок, чтобы быстро открывать Центр Интернета вещей с помощью панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="b158d-125">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

3. <span data-ttu-id="b158d-126">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b158d-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-to-read-messages"></a><span data-ttu-id="b158d-127">Подготовка к подключению Центра Интернета вещей для чтения сообщений</span><span class="sxs-lookup"><span data-stu-id="b158d-127">Prepare your IoT hub connection to read messages</span></span>

<span data-ttu-id="b158d-128">Центр Интернета вещей предоставляет встроенную совместимую с концентратором событий конечную точку, с помощью которой приложения считывают сообщения Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b158d-128">IoT hub exposes a built-in event hub-compatible endpoint to enable applications to read IoT hub messages.</span></span> <span data-ttu-id="b158d-129">В то же время, чтобы считывать данные из Центра Интернета вещей, приложения используют группы получателей.</span><span class="sxs-lookup"><span data-stu-id="b158d-129">Meanwhile, applications use consumer groups to read data from your IoT hub.</span></span> <span data-ttu-id="b158d-130">Перед созданием приложения-функции Azure для считывания данных из Центра Интернета вещей, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b158d-130">Before you create an Azure function app to read data from your IoT hub, do the following:</span></span>

- <span data-ttu-id="b158d-131">получить строку подключения конечной точки Центра Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="b158d-131">Get the connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="b158d-132">создать группу потребителей для Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b158d-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-the-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="b158d-133">Получение строки подключения конечной точки Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="b158d-133">Get the connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="b158d-134">Откройте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b158d-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="b158d-135">В области **Центр Интернета вещей** в разделе **Сообщения** щелкните **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="b158d-135">On the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="b158d-136">В правой области в разделе **Встроенные конечные точки** выберите **События**.</span><span class="sxs-lookup"><span data-stu-id="b158d-136">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="b158d-137">В области **Свойства** обратите внимание на следующие значения:</span><span class="sxs-lookup"><span data-stu-id="b158d-137">In the **Properties** pane, note the following values:</span></span>
   - <span data-ttu-id="b158d-138">конечная точка, совместимая с концентратором событий;</span><span class="sxs-lookup"><span data-stu-id="b158d-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="b158d-139">имя, совместимое с концентратором событий.</span><span class="sxs-lookup"><span data-stu-id="b158d-139">Event hub-compatible name</span></span>

   ![Получение строки подключения конечной точки Центра Интернета вещей на портале Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="b158d-141">В области **Центр Интернета вещей** в разделе **Параметры** выберите **Политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="b158d-141">In the **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="b158d-142">Щелкните **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="b158d-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="b158d-143">Запишите значение **Первичный ключ**.</span><span class="sxs-lookup"><span data-stu-id="b158d-143">Note the **Primary key** value.</span></span>

8. <span data-ttu-id="b158d-144">Создайте строку подключения конечной точки Центра Интернета вещей в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="b158d-144">Create the connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="b158d-145">Замените `<Event Hub-compatible endpoint>` и `<Primary key>` значениями, записанными ранее.</span><span class="sxs-lookup"><span data-stu-id="b158d-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with the values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="b158d-146">Создание группы потребителей для Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="b158d-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="b158d-147">Откройте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b158d-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="b158d-148">В области **Центр Интернета вещей** в разделе **Сообщения** щелкните **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="b158d-148">In the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="b158d-149">В правой области в разделе **Встроенные конечные точки** выберите **События**.</span><span class="sxs-lookup"><span data-stu-id="b158d-149">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="b158d-150">В области **Свойства** в разделе **Группы потребителей** введите имя, а затем запишите его.</span><span class="sxs-lookup"><span data-stu-id="b158d-150">In the **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="b158d-151">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b158d-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="b158d-152">Создание и развертывание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="b158d-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="b158d-153">На [портале Azure](https://portal.azure.com/) щелкните **Создать** > **Вычисления** > **Приложение-функция** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b158d-153">In the [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="b158d-154">Введите необходимые сведения для приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="b158d-154">Enter the necessary information for the function app.</span></span>

   ![Создание приложения-функции на портале Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="b158d-156">**Имя приложения**. Имя приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="b158d-156">**App name**: The name of the function app.</span></span> <span data-ttu-id="b158d-157">Оно должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="b158d-157">The name must be globally unique.</span></span>

   * <span data-ttu-id="b158d-158">**Группа ресурсов**. Выберите ту же группу ресурсов, которую использует Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b158d-158">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="b158d-159">**Учетная запись хранения**. Созданная вами учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="b158d-159">**Storage Account**: The storage account that you created.</span></span>

   * <span data-ttu-id="b158d-160">**Закрепить на панели мониторинга**. Установите этот флажок, чтобы быстро открывать приложение-функцию с помощью панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="b158d-160">**Pin to dashboard**: Check this option for easy access to the function app from the dashboard.</span></span>

3. <span data-ttu-id="b158d-161">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b158d-161">Click **Create**.</span></span>

4. <span data-ttu-id="b158d-162">После создания приложения-функции откройте его.</span><span class="sxs-lookup"><span data-stu-id="b158d-162">After the function app has been created, open it.</span></span>

5. <span data-ttu-id="b158d-163">В приложении-функции создайте функцию, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b158d-163">In the function app, create a new function by doing the following:</span></span>

   <span data-ttu-id="b158d-164">а.</span><span class="sxs-lookup"><span data-stu-id="b158d-164">a.</span></span> <span data-ttu-id="b158d-165">Щелкните **Новая функция**.</span><span class="sxs-lookup"><span data-stu-id="b158d-165">Click **New Function**.</span></span>

   <span data-ttu-id="b158d-166">b.</span><span class="sxs-lookup"><span data-stu-id="b158d-166">b.</span></span> <span data-ttu-id="b158d-167">Для параметра **Язык** выберите **JavaScript**, а для **Сценарий** — **Обработка данных**.</span><span class="sxs-lookup"><span data-stu-id="b158d-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="b158d-168">c.</span><span class="sxs-lookup"><span data-stu-id="b158d-168">c.</span></span> <span data-ttu-id="b158d-169">Щелкните **Создайте эту функцию**, а затем — выберите **Новая функция**.</span><span class="sxs-lookup"><span data-stu-id="b158d-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="b158d-170">г)</span><span class="sxs-lookup"><span data-stu-id="b158d-170">d.</span></span> <span data-ttu-id="b158d-171">Выберите **JavaScript** в качестве языка и **Обработка данных** в качестве сценария.</span><span class="sxs-lookup"><span data-stu-id="b158d-171">Select **JavaScript** for the language, and **Data Processing** for the scenario.</span></span>

   <span data-ttu-id="b158d-172">д.</span><span class="sxs-lookup"><span data-stu-id="b158d-172">e.</span></span> <span data-ttu-id="b158d-173">Щелкните шаблон **EventHubTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="b158d-173">Click the **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="b158d-174">f.</span><span class="sxs-lookup"><span data-stu-id="b158d-174">f.</span></span> <span data-ttu-id="b158d-175">Введите необходимые сведения для шаблона.</span><span class="sxs-lookup"><span data-stu-id="b158d-175">Enter the necessary information for the template.</span></span>

      * <span data-ttu-id="b158d-176">**Присвойте имя функции**. Имя функции.</span><span class="sxs-lookup"><span data-stu-id="b158d-176">**Name your function**: The name of the function.</span></span>

      * <span data-ttu-id="b158d-177">**Имя концентратора событий**. Имя, совместимое с концентратором событий, которое вы записали ранее.</span><span class="sxs-lookup"><span data-stu-id="b158d-177">**Event Hub name**: The event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="b158d-178">**Подключение к концентратору событий**. Щелкните **Новые**, чтобы добавить строку подключения конечной точки Центра Интернета вещей, которую вы создали.</span><span class="sxs-lookup"><span data-stu-id="b158d-178">**Event Hub connection**: To add the connection string of the IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="b158d-179">g.</span><span class="sxs-lookup"><span data-stu-id="b158d-179">g.</span></span> <span data-ttu-id="b158d-180">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b158d-180">Click **Create**.</span></span>

6. <span data-ttu-id="b158d-181">Настройте выходные данные функции, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b158d-181">Configure an output of the function by doing the following:</span></span>

   <span data-ttu-id="b158d-182">а.</span><span class="sxs-lookup"><span data-stu-id="b158d-182">a.</span></span> <span data-ttu-id="b158d-183">Щелкните **Интегрировать** > **Новое выходное значение** > **Хранилище таблиц Azure** > **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b158d-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Добавление хранилища таблиц в приложение-функцию на портале Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="b158d-185">b.</span><span class="sxs-lookup"><span data-stu-id="b158d-185">b.</span></span> <span data-ttu-id="b158d-186">Введите необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="b158d-186">Enter the necessary information.</span></span>

      * <span data-ttu-id="b158d-187">**Имя параметра таблицы**. Используйте `outputTable`, которое будет использоваться в коде функции Azure.</span><span class="sxs-lookup"><span data-stu-id="b158d-187">**Table parameter name**: Use `outputTable`, which will be used in the Azure function's code.</span></span>
      
      * <span data-ttu-id="b158d-188">**Имя таблицы**. Используйте `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="b158d-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="b158d-189">**Подключение к учетной записи хранения**. Щелкните **Новые** и выберите или введите свою учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="b158d-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="b158d-190">Если учетная запись хранения не отображается, ознакомьтесь с разделом [Требования к учетной записи хранения](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="b158d-190">If the storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="b158d-191">c.</span><span class="sxs-lookup"><span data-stu-id="b158d-191">c.</span></span> <span data-ttu-id="b158d-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b158d-192">Click **Save**.</span></span>

7. <span data-ttu-id="b158d-193">В разделе **Триггеры** щелкните **Концентратор событий Azure (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="b158d-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="b158d-194">В разделе **Группа пользователей концентратора событий** введите имя созданной вами группы получателей, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b158d-194">Under **Event Hub consumer group**, enter the name of the consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="b158d-195">Щелкните созданную функцию в левой части экрана, а затем щелкните **Просмотреть файлы** справа.</span><span class="sxs-lookup"><span data-stu-id="b158d-195">Click the function you've created on the left and then click **View Files** on the right.</span></span>

10. <span data-ttu-id="b158d-196">Замените код в `index.js` приведенным ниже:</span><span class="sxs-lookup"><span data-stu-id="b158d-196">Replace the code in `index.js` with the following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in the IoT hub.
   // The message payload is persisted in an Azure storage table
 
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

11. <span data-ttu-id="b158d-197">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b158d-197">Click **Save**.</span></span>

<span data-ttu-id="b158d-198">Приложение-функция создано.</span><span class="sxs-lookup"><span data-stu-id="b158d-198">You have now created the function app.</span></span> <span data-ttu-id="b158d-199">Приложение-функция сохраняет сообщения, которые получает Центр Интернета вещей в хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="b158d-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="b158d-200">Используйте кнопку **Выполнить** для тестирования приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="b158d-200">You can use the **Run** button to test the function app.</span></span> <span data-ttu-id="b158d-201">Если вы нажмете кнопку **Выполнить**, в Центр Интернета вещей будет отправлено тестовое сообщение.</span><span class="sxs-lookup"><span data-stu-id="b158d-201">When you click **Run**, the test message is sent to your IoT hub.</span></span> <span data-ttu-id="b158d-202">Доставка сообщения должна активировать запуск приложения-функции, после чего сообщение сохранится в хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="b158d-202">The arrival of the message should trigger the function app to start and then save the message to your table storage.</span></span> <span data-ttu-id="b158d-203">В области **Журналы** записываются сведения о процессе.</span><span class="sxs-lookup"><span data-stu-id="b158d-203">The **Logs** pane records the details of the process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="b158d-204">Проверка сообщений в хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="b158d-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="b158d-205">Выполните пример приложения на устройстве, чтобы отправить сообщения в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b158d-205">Run the sample application on your device to send messages to your IoT hub.</span></span>

2. <span data-ttu-id="b158d-206">[Скачайте и установите обозреватель хранилищ Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="b158d-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="b158d-207">Откройте обозреватель хранилищ, щелкните **Add an Azure Account** (Добавление учетной записи Azure)  > **Вход**, а затем выполните вход в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b158d-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in to your Azure account.</span></span>

4. <span data-ttu-id="b158d-208">Щелкните подписку Azure > **Учетные записи хранения** > ваша учетная запись хранения > **Таблицы** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="b158d-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="b158d-209">Вы должны увидеть сообщения, отправленные с устройства в Центр Интернета вещей, в таблице `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="b158d-209">You should see messages sent from your device to your IoT hub logged in the `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b158d-210">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b158d-210">Next steps</span></span>

<span data-ttu-id="b158d-211">Вы успешно создали учетную запись хранения Azure и приложение-функцию Azure, которое сохраняет сообщения, поступающие в Центр Интернета вещей, в хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="b158d-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
