---
title: "удаленный мониторинг aaaIoT и уведомлений с приложениями логики Azure | Документы Microsoft"
description: "Использование приложения логики Azure IoT температуры отслеживания на ваш центр IoT и автоматически отправлять почтовому ящику tooyour уведомления для любых аномалий обнаружил."
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
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="212ac-104">Удаленный мониторинг и отправка уведомлений в Центре Интернета вещей с помощью службы Azure Logic Apps, обеспечивающей подключение между Центром Интернета вещей и почтовым ящиком</span><span class="sxs-lookup"><span data-stu-id="212ac-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="212ac-106">Приложения логики Azure предоставляет способ tooautomate процессы, так как последовательность шагов.</span><span class="sxs-lookup"><span data-stu-id="212ac-106">Azure Logic Apps provides a way tooautomate processes as a series of steps.</span></span> <span data-ttu-id="212ac-107">Приложение логики поддерживает подключение к различным службам по различным протоколам.</span><span class="sxs-lookup"><span data-stu-id="212ac-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="212ac-108">Сначала в нем срабатывает триггер, например "При добавлении учетной записи", а затем выполняется набор действий, например "отправка push-уведомления".</span><span class="sxs-lookup"><span data-stu-id="212ac-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="212ac-109">Благодаря этой функции Logic Apps, помимо прочего, идеально подходит для мониторинга Центра Интернета вещей, например оповещения об аномалиях.</span><span class="sxs-lookup"><span data-stu-id="212ac-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="212ac-110">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="212ac-110">What you learn</span></span>

<span data-ttu-id="212ac-111">Вы узнаете, как toocreate приложения логики, который подключается ваш центр IoT и почтового ящика для мониторинга температуры и уведомлений.</span><span class="sxs-lookup"><span data-stu-id="212ac-111">You learn how toocreate a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="212ac-112">При hello температуры выше 30 C hello метки приложение клиента `temperatureAlert = "true"` в приветственное сообщение, он отправляет tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="212ac-112">When hello temperature is above 30 C, hello client application marks `temperatureAlert = "true"` in hello message it sends tooyour IoT hub.</span></span> <span data-ttu-id="212ac-113">приветственное сообщение, триггеры hello toosend логику приложения вам уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="212ac-113">hello message triggers hello logic app toosend you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="212ac-114">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="212ac-114">What you do</span></span>

* <span data-ttu-id="212ac-115">Создайте пространство имен служебной шины и добавьте tooit очереди.</span><span class="sxs-lookup"><span data-stu-id="212ac-115">Create a service bus namespace and add a queue tooit.</span></span>
* <span data-ttu-id="212ac-116">Добавьте конечную точку и маршрутизации центра IoT tooyour правила.</span><span class="sxs-lookup"><span data-stu-id="212ac-116">Add an endpoint and a routing rule tooyour IoT hub.</span></span>
* <span data-ttu-id="212ac-117">Создадим, настроим и протестируем приложение логики.</span><span class="sxs-lookup"><span data-stu-id="212ac-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="212ac-118">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="212ac-118">What you need</span></span>

* <span data-ttu-id="212ac-119">Учебник по [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md) завершения, который охватывает hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="212ac-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  * <span data-ttu-id="212ac-120">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="212ac-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="212ac-121">Центр Интернета вещей Azure в подписке;</span><span class="sxs-lookup"><span data-stu-id="212ac-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="212ac-122">Клиентское приложение, которое отправляет центр Azure IoT tooyour сообщений.</span><span class="sxs-lookup"><span data-stu-id="212ac-122">A client application that sends messages tooyour Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a><span data-ttu-id="212ac-123">Создайте пространство имен шины обслуживания и добавьте tooit очереди</span><span class="sxs-lookup"><span data-stu-id="212ac-123">Create service bus namespace and add a queue tooit</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="212ac-124">Создание пространства имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="212ac-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="212ac-125">На hello [портал Azure](https://portal.azure.com/), нажмите кнопку **New** > **интеграцию** > **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="212ac-125">On hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="212ac-126">Укажите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="212ac-126">Provide hello following information:</span></span>

   <span data-ttu-id="212ac-127">**Имя**: hello имя hello служебной шины.</span><span class="sxs-lookup"><span data-stu-id="212ac-127">**Name**: hello name of hello service bus.</span></span>

   <span data-ttu-id="212ac-128">**Ценовая категория**. Щелкните **Базовая** > **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="212ac-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="212ac-129">для этого учебника, достаточно Hello базового уровня.</span><span class="sxs-lookup"><span data-stu-id="212ac-129">hello Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="212ac-130">**Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="212ac-130">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="212ac-131">**Расположение**: используйте hello же местоположения, которое использует ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="212ac-131">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="212ac-132">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="212ac-132">Click **Create**.</span></span>

   ![Создать пространство имен служебной шины в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="212ac-134">Добавление очереди служебной шины</span><span class="sxs-lookup"><span data-stu-id="212ac-134">Add a service bus queue</span></span>

1. <span data-ttu-id="212ac-135">Откройте hello пространства имен шины обслуживания и нажмите кнопку **+ очередь**.</span><span class="sxs-lookup"><span data-stu-id="212ac-135">Open hello service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="212ac-136">Введите имя для очереди hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="212ac-136">Enter a name for hello queue and then click **Create**.</span></span>
1. <span data-ttu-id="212ac-137">Откройте очередь service bus hello и нажмите кнопку **политики общего доступа** > **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="212ac-137">Open hello service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="212ac-138">Введите имя для политики hello, проверка **управление**, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="212ac-138">Enter a name for hello policy, check **Manage**, and then click **Create**.</span></span>

   ![Добавить очередь служебной шины в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a><span data-ttu-id="212ac-140">Добавить конечную точку и маршрутизации центра IoT tooyour правило</span><span class="sxs-lookup"><span data-stu-id="212ac-140">Add an endpoint and a routing rule tooyour IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="212ac-141">Добавление конечной точки</span><span class="sxs-lookup"><span data-stu-id="212ac-141">Add an endpoint</span></span>

1. <span data-ttu-id="212ac-142">Откройте Центр Интернета вещей и щелкните "Конечные точки > + Добавить".</span><span class="sxs-lookup"><span data-stu-id="212ac-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="212ac-143">Введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="212ac-143">Enter hello following information:</span></span>

   <span data-ttu-id="212ac-144">**Имя**: hello имя конечной точки hello.</span><span class="sxs-lookup"><span data-stu-id="212ac-144">**Name**: hello name of hello endpoint.</span></span>

   <span data-ttu-id="212ac-145">**Тип конечной точки**. Выберите **Очередь служебной шины**.</span><span class="sxs-lookup"><span data-stu-id="212ac-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="212ac-146">**Пространство имен служебной шины**: выберите созданную имен hello.</span><span class="sxs-lookup"><span data-stu-id="212ac-146">**Service Bus namespace**: Select hello namespace you created.</span></span>

   <span data-ttu-id="212ac-147">**Очередь Service Bus**: hello выберите очереди, вы создали.</span><span class="sxs-lookup"><span data-stu-id="212ac-147">**Service Bus queue**: Select hello queue you created.</span></span>
1. <span data-ttu-id="212ac-148">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="212ac-148">Click **OK**.</span></span>

   ![Добавление конечной точки центра IoT tooyour в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="212ac-150">Добавление правила маршрутизации</span><span class="sxs-lookup"><span data-stu-id="212ac-150">Add a routing rule</span></span>

1. <span data-ttu-id="212ac-151">В Центре Интернета вещей щелкните **Маршруты** > **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="212ac-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="212ac-152">Введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="212ac-152">Enter hello following information:</span></span>

   <span data-ttu-id="212ac-153">**Имя**: hello имя правила маршрутизации hello.</span><span class="sxs-lookup"><span data-stu-id="212ac-153">**Name**: hello name of hello routing rule.</span></span>

   <span data-ttu-id="212ac-154">**Источник данных**. Выберите **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="212ac-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="212ac-155">**Конечная точка**: выберите созданную конечную точку hello.</span><span class="sxs-lookup"><span data-stu-id="212ac-155">**Endpoint**: Select hello endpoint you created.</span></span>

   <span data-ttu-id="212ac-156">**Строка запроса**. Введите `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="212ac-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="212ac-157">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="212ac-157">Click **Save**.</span></span>

   ![Добавление правила маршрутизации в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="212ac-159">Создание и настройка приложения логики</span><span class="sxs-lookup"><span data-stu-id="212ac-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="212ac-160">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="212ac-160">Create a logic app</span></span>

1. <span data-ttu-id="212ac-161">В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **New** > **интеграцию** > **приложения логики**.</span><span class="sxs-lookup"><span data-stu-id="212ac-161">In hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="212ac-162">Введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="212ac-162">Enter hello following information:</span></span>

   <span data-ttu-id="212ac-163">**Имя**: hello имя hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="212ac-163">**Name**: hello name of hello logic app.</span></span>

   <span data-ttu-id="212ac-164">**Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="212ac-164">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="212ac-165">**Расположение**: используйте hello же местоположения, которое использует ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="212ac-165">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="212ac-166">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="212ac-166">Click **Create**.</span></span>

### <a name="configure-hello-logic-app"></a><span data-ttu-id="212ac-167">Настройка логики приложения hello</span><span class="sxs-lookup"><span data-stu-id="212ac-167">Configure hello logic app</span></span>

1. <span data-ttu-id="212ac-168">Откройте приложение hello логику, которая открывается в конструкторе логики приложения hello.</span><span class="sxs-lookup"><span data-stu-id="212ac-168">Open hello logic app that opens into hello Logic Apps Designer.</span></span>
1. <span data-ttu-id="212ac-169">В hello конструктора логики приложения, щелкните **пустое приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="212ac-169">In hello Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Начать с пустой логику приложения в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="212ac-171">Щелкните **Служебная шина**.</span><span class="sxs-lookup"><span data-stu-id="212ac-171">Click **Service Bus**.</span></span>

   ![Выберите Создание логику приложения в hello портал Azure toostart Service Bus](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="212ac-173">Щелкните **Служебная шина — Когда одно или несколько сообщений поступает в очередь (автозавершение)**.</span><span class="sxs-lookup"><span data-stu-id="212ac-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="212ac-174">Создайте подключение к служебной шине.</span><span class="sxs-lookup"><span data-stu-id="212ac-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="212ac-175">Введите имя подключения.</span><span class="sxs-lookup"><span data-stu-id="212ac-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="212ac-176">Выберите пространство имен шины обслуживания hello > Здравствуйте service bus политики > **создать**.</span><span class="sxs-lookup"><span data-stu-id="212ac-176">Click hello service bus namespace > hello service bus policy > **Create**.</span></span>

      ![Создание подключения service bus логику приложения в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="212ac-178">Нажмите кнопку **Продолжить** после создания подключения service bus hello.</span><span class="sxs-lookup"><span data-stu-id="212ac-178">Click **Continue** after hello service bus connection is created.</span></span>
   1. <span data-ttu-id="212ac-179">Выберите очередь hello, созданный и введите `175` для **максимальное количество сообщений**</span><span class="sxs-lookup"><span data-stu-id="212ac-179">Select hello queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Укажите число максимальное сообщение hello для подключения service bus hello в приложении логики](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="212ac-181">Нажмите кнопку «Сохранить» hello toosave кнопке изменится.</span><span class="sxs-lookup"><span data-stu-id="212ac-181">Click "Save" button toosave hello changes.</span></span>

1. <span data-ttu-id="212ac-182">Создайте подключение к службе SMTP.</span><span class="sxs-lookup"><span data-stu-id="212ac-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="212ac-183">Выберите **Новый шаг** > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="212ac-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="212ac-184">Тип `SMTP`, нажмите кнопку hello **SMTP** службы в результате поиска hello и нажмите кнопку **SMTP - Отправка сообщения**.</span><span class="sxs-lookup"><span data-stu-id="212ac-184">Type `SMTP`, click hello **SMTP** service in hello search result, and then click **SMTP - Send Email**.</span></span>

      ![Создание соединения SMTP в приложении логику в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="212ac-186">Введите сведения hello SMTP почтового ящика и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="212ac-186">Enter hello SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Введите сведения о подключении к SMTP в приложении логику в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="212ac-188">Получить сведения о hello SMTP для [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), и [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="212ac-188">Get hello SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="212ac-189">Введите адрес электронной почты в полях **От** и **Кому** и укажите `High temperature detected` в **теме** и **тексте сообщения**.</span><span class="sxs-lookup"><span data-stu-id="212ac-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="212ac-190">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="212ac-190">Click **Save**.</span></span>

<span data-ttu-id="212ac-191">приложение Hello логика находится в рабочем состоянии, при его сохранении.</span><span class="sxs-lookup"><span data-stu-id="212ac-191">hello logic app is in working order when you save it.</span></span>

## <a name="test-hello-logic-app"></a><span data-ttu-id="212ac-192">Приложения логики теста hello</span><span class="sxs-lookup"><span data-stu-id="212ac-192">Test hello logic app</span></span>

1. <span data-ttu-id="212ac-193">Запустите клиентское приложение hello развертываемой tooyour устройство в [tooAzure ESP8266 подключения центр IoT](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="212ac-193">Start hello client application that you deploy tooyour device in [Connect ESP8266 tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="212ac-194">Увеличить температуры среды hello вокруг toobe SensorTag hello выше 30 C. Например легкий свечи вокруг вашего SensorTag.</span><span class="sxs-lookup"><span data-stu-id="212ac-194">Increase hello environment temperature around hello SensorTag toobe above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="212ac-195">Вы получите уведомление по электронной почте, отправленных hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="212ac-195">You should receive an email notification sent by hello logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="212ac-196">Поставщик услуг электронной почты может потребоваться tooverify hello отправителя удостоверения toomake том, что кто отправляет электронное сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="212ac-196">Your email service provider may need tooverify hello sender identity toomake sure it is you who sends hello email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="212ac-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="212ac-197">Next steps</span></span>

<span data-ttu-id="212ac-198">Вы успешно создали приложение логики, обеспечивающее подключение между Центром Интернета вещей и почтовым ящиком для мониторинга температуры и отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="212ac-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
