---
title: "Удаленный мониторинг и отправка уведомлений в Центре Интернета вещей с помощью Azure Logic Apps | Документация Майкрософт"
description: "Azure Logic Apps можно использовать для мониторинга температуры в Центре Интернета вещей и автоматической отправки уведомлений на электронную почту в случае обнаружения аномалий."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "мониторинг Центра Интернета вещей, уведомления Центра Интернета вещей, мониторинг температуры в Центре Интернета вещей"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 7a611912ae55eb22103539dbba9f1a06aaa543b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="39624-104">Удаленный мониторинг и отправка уведомлений в Центре Интернета вещей с помощью службы Azure Logic Apps, обеспечивающей подключение между Центром Интернета вещей и почтовым ящиком</span><span class="sxs-lookup"><span data-stu-id="39624-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Комплексная схема](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="39624-106">Azure Logic Apps позволяет автоматизировать процессы в виде последовательности действий.</span><span class="sxs-lookup"><span data-stu-id="39624-106">Azure Logic Apps provides a way to automate processes as a series of steps.</span></span> <span data-ttu-id="39624-107">Приложение логики поддерживает подключение к различным службам по различным протоколам.</span><span class="sxs-lookup"><span data-stu-id="39624-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="39624-108">Сначала в нем срабатывает триггер, например "При добавлении учетной записи", а затем выполняется набор действий, например "отправка push-уведомления".</span><span class="sxs-lookup"><span data-stu-id="39624-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="39624-109">Благодаря этой функции Logic Apps, помимо прочего, идеально подходит для мониторинга Центра Интернета вещей, например оповещения об аномалиях.</span><span class="sxs-lookup"><span data-stu-id="39624-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="39624-110">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="39624-110">What you learn</span></span>

<span data-ttu-id="39624-111">Вы научитесь создавать приложение логики, обеспечивающее подключение между Центром Интернета вещей и почтовым ящиком для мониторинга температуры и отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="39624-111">You learn how to create a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="39624-112">Когда температура превышает 30 °C, клиентское приложение добавляет отметку `temperatureAlert = "true"` в сообщение, которое оно отправляет в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="39624-112">When the temperature is above 30 C, the client application marks `temperatureAlert = "true"` in the message it sends to your IoT hub.</span></span> <span data-ttu-id="39624-113">Сообщение активирует отправку приложением логики уведомления по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="39624-113">The message triggers the logic app to send you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="39624-114">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="39624-114">What you do</span></span>

* <span data-ttu-id="39624-115">Создадим пространство имен служебной шины и добавим в него очередь.</span><span class="sxs-lookup"><span data-stu-id="39624-115">Create a service bus namespace and add a queue to it.</span></span>
* <span data-ttu-id="39624-116">Добавим конечную точку и правило маршрутизации в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="39624-116">Add an endpoint and a routing rule to your IoT hub.</span></span>
* <span data-ttu-id="39624-117">Создадим, настроим и протестируем приложение логики.</span><span class="sxs-lookup"><span data-stu-id="39624-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="39624-118">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="39624-118">What you need</span></span>

* <span data-ttu-id="39624-119">Изучите руководство [Настройка вашего устройства](iot-hub-raspberry-pi-kit-node-get-started.md), где описаны следующие требования.</span><span class="sxs-lookup"><span data-stu-id="39624-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  * <span data-ttu-id="39624-120">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="39624-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="39624-121">Центр Интернета вещей Azure в подписке;</span><span class="sxs-lookup"><span data-stu-id="39624-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="39624-122">клиентское приложение, которое отправляет сообщения в Центр Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="39624-122">A client application that sends messages to your Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-to-it"></a><span data-ttu-id="39624-123">Создание пространства имен служебной шины и добавление в него очереди</span><span class="sxs-lookup"><span data-stu-id="39624-123">Create service bus namespace and add a queue to it</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="39624-124">Создание пространства имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="39624-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="39624-125">На [портале Azure](https://portal.azure.com/) последовательно выберите **Создать** > **Enterprise Integration** (Корпоративная интеграция) > **Service Bus** (Служебная шина).</span><span class="sxs-lookup"><span data-stu-id="39624-125">On the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="39624-126">Введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="39624-126">Provide the following information:</span></span>

   <span data-ttu-id="39624-127">**Имя**. Имя служебной шины.</span><span class="sxs-lookup"><span data-stu-id="39624-127">**Name**: The name of the service bus.</span></span>

   <span data-ttu-id="39624-128">**Ценовая категория**. Щелкните **Базовая** > **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="39624-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="39624-129">Базового уровня для данного учебника достаточно.</span><span class="sxs-lookup"><span data-stu-id="39624-129">The Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="39624-130">**Группа ресурсов**. Выберите ту же группу ресурсов, которую использует Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="39624-130">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="39624-131">**Расположение**. Выберите то же расположение, которое используется для Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="39624-131">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="39624-132">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="39624-132">Click **Create**.</span></span>

   ![Создание пространства имен служебной шины с помощью портала Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="39624-134">Добавление очереди служебной шины</span><span class="sxs-lookup"><span data-stu-id="39624-134">Add a service bus queue</span></span>

1. <span data-ttu-id="39624-135">Откройте пространство имен служебной шины и щелкните **+ Очередь**.</span><span class="sxs-lookup"><span data-stu-id="39624-135">Open the service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="39624-136">Введите имя очереди и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="39624-136">Enter a name for the queue and then click **Create**.</span></span>
1. <span data-ttu-id="39624-137">Откройте очередь служебной шины и щелкните **Политики общего доступа** > **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="39624-137">Open the service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="39624-138">Введите имя политики, установите флажок **Управление**, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="39624-138">Enter a name for the policy, check **Manage**, and then click **Create**.</span></span>

   ![Добавление очереди служебной шины на портале Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-to-your-iot-hub"></a><span data-ttu-id="39624-140">Добавление конечной точки и правила маршрутизации в Центр Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="39624-140">Add an endpoint and a routing rule to your IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="39624-141">Добавление конечной точки</span><span class="sxs-lookup"><span data-stu-id="39624-141">Add an endpoint</span></span>

1. <span data-ttu-id="39624-142">Откройте Центр Интернета вещей и щелкните "Конечные точки > + Добавить".</span><span class="sxs-lookup"><span data-stu-id="39624-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="39624-143">Введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="39624-143">Enter the following information:</span></span>

   <span data-ttu-id="39624-144">**Имя**. Имя конечной точки.</span><span class="sxs-lookup"><span data-stu-id="39624-144">**Name**: The name of the endpoint.</span></span>

   <span data-ttu-id="39624-145">**Тип конечной точки**. Выберите **Очередь служебной шины**.</span><span class="sxs-lookup"><span data-stu-id="39624-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="39624-146">**Пространство имен служебной шины**. Выберите созданное пространство имен.</span><span class="sxs-lookup"><span data-stu-id="39624-146">**Service Bus namespace**: Select the namespace you created.</span></span>

   <span data-ttu-id="39624-147">**Очередь служебной шины**. Выберите созданную очередь.</span><span class="sxs-lookup"><span data-stu-id="39624-147">**Service Bus queue**: Select the queue you created.</span></span>
1. <span data-ttu-id="39624-148">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="39624-148">Click **OK**.</span></span>

   ![Добавление конечной точки в Центр Интернета вещей на портале Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="39624-150">Добавление правила маршрутизации</span><span class="sxs-lookup"><span data-stu-id="39624-150">Add a routing rule</span></span>

1. <span data-ttu-id="39624-151">В Центре Интернета вещей щелкните **Маршруты** > **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="39624-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="39624-152">Введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="39624-152">Enter the following information:</span></span>

   <span data-ttu-id="39624-153">**Имя**. Имя правила маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="39624-153">**Name**: The name of the routing rule.</span></span>

   <span data-ttu-id="39624-154">**Источник данных**. Выберите **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="39624-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="39624-155">**Конечная точка**. Выберите созданную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="39624-155">**Endpoint**: Select the endpoint you created.</span></span>

   <span data-ttu-id="39624-156">**Строка запроса**. Введите `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="39624-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="39624-157">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="39624-157">Click **Save**.</span></span>

   ![Добавление правила маршрутизации на портале Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="39624-159">Создание и настройка приложения логики</span><span class="sxs-lookup"><span data-stu-id="39624-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="39624-160">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="39624-160">Create a logic app</span></span>

1. <span data-ttu-id="39624-161">На [портале Azure](https://portal.azure.com/) последовательно выберите **Создать** > **Enterprise Integration** (Корпоративная интеграция) > **Приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="39624-161">In the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="39624-162">Введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="39624-162">Enter the following information:</span></span>

   <span data-ttu-id="39624-163">**Имя**. Имя приложения логики.</span><span class="sxs-lookup"><span data-stu-id="39624-163">**Name**: The name of the logic app.</span></span>

   <span data-ttu-id="39624-164">**Группа ресурсов**. Выберите ту же группу ресурсов, которую использует Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="39624-164">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="39624-165">**Расположение**. Выберите то же расположение, которое используется для Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="39624-165">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="39624-166">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="39624-166">Click **Create**.</span></span>

### <a name="configure-the-logic-app"></a><span data-ttu-id="39624-167">Настройка приложения логики</span><span class="sxs-lookup"><span data-stu-id="39624-167">Configure the logic app</span></span>

1. <span data-ttu-id="39624-168">Откройте приложение логики в конструкторе Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="39624-168">Open the logic app that opens into the Logic Apps Designer.</span></span>
1. <span data-ttu-id="39624-169">Щелкните в нем **Пустое приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="39624-169">In the Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Начало работы с пустым приложением логики на портале Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="39624-171">Щелкните **Служебная шина**.</span><span class="sxs-lookup"><span data-stu-id="39624-171">Click **Service Bus**.</span></span>

   ![Выбор служебной шины для начала создания приложения логики на портале Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="39624-173">Щелкните **Служебная шина — Когда одно или несколько сообщений поступает в очередь (автозавершение)**.</span><span class="sxs-lookup"><span data-stu-id="39624-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="39624-174">Создайте подключение к служебной шине.</span><span class="sxs-lookup"><span data-stu-id="39624-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="39624-175">Введите имя подключения.</span><span class="sxs-lookup"><span data-stu-id="39624-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="39624-176">Выберите пространство имен и политику служебной шины, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="39624-176">Click the service bus namespace > the service bus policy > **Create**.</span></span>

      ![Создание подключения к служебной шине для приложения логики на портале Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="39624-178">После создания подключения к служебной шине щелкните **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="39624-178">Click **Continue** after the service bus connection is created.</span></span>
   1. <span data-ttu-id="39624-179">Выберите созданную очередь и введите значение `175` для параметра **Максимальное число сообщений**.</span><span class="sxs-lookup"><span data-stu-id="39624-179">Select the queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Установка максимального числа сообщений для подключения к служебной шине в приложении логики](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="39624-181">Щелкните "Сохранить" , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="39624-181">Click "Save" button to save the changes.</span></span>

1. <span data-ttu-id="39624-182">Создайте подключение к службе SMTP.</span><span class="sxs-lookup"><span data-stu-id="39624-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="39624-183">Выберите **Новый шаг** > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="39624-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="39624-184">Введите `SMTP`, щелкните службу **SMTP** в результатах поиска, а затем выберите **SMTP — отправка электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="39624-184">Type `SMTP`, click the **SMTP** service in the search result, and then click **SMTP - Send Email**.</span></span>

      ![Создание подключения к службе SMTP в приложении логики на портале Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="39624-186">Введите сведения о службе SMTP почтового ящика и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="39624-186">Enter the SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Ввод сведений о подключении к службе SMTP в приложении логики на портале Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="39624-188">Получение сведений об SMTP для [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en) и [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="39624-188">Get the SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="39624-189">Введите адрес электронной почты в полях **От** и **Кому** и укажите `High temperature detected` в **теме** и **тексте сообщения**.</span><span class="sxs-lookup"><span data-stu-id="39624-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="39624-190">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="39624-190">Click **Save**.</span></span>

<span data-ttu-id="39624-191">При сохранении приложения логика находится в рабочем состоянии.</span><span class="sxs-lookup"><span data-stu-id="39624-191">The logic app is in working order when you save it.</span></span>

## <a name="test-the-logic-app"></a><span data-ttu-id="39624-192">Тестирование приложения логики</span><span class="sxs-lookup"><span data-stu-id="39624-192">Test the logic app</span></span>

1. <span data-ttu-id="39624-193">Запустите клиентское приложение, развертываемое на устройстве, как описано в статье [Подключение Adafruit Feather HUZZAH ESP8266 к Центру Интернета вещей Azure в облаке](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="39624-193">Start the client application that you deploy to your device in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="39624-194">Увеличьте температуру среды вокруг устройства SensorTag до отметки свыше 30 °C, например зажгите рядом с ним свечу.</span><span class="sxs-lookup"><span data-stu-id="39624-194">Increase the environment temperature around the SensorTag to be above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="39624-195">Вы должны получить уведомление по электронной почте, отправленное приложением логики.</span><span class="sxs-lookup"><span data-stu-id="39624-195">You should receive an email notification sent by the logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="39624-196">Возможно, поставщику услуг электронной почты потребуется проверить подлинность отправителя и убедиться, что именно вы отправили это сообщение.</span><span class="sxs-lookup"><span data-stu-id="39624-196">Your email service provider may need to verify the sender identity to make sure it is you who sends the email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39624-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="39624-197">Next steps</span></span>

<span data-ttu-id="39624-198">Вы успешно создали приложение логики, обеспечивающее подключение между Центром Интернета вещей и почтовым ящиком для мониторинга температуры и отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="39624-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
