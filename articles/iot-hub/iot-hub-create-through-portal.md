---
title: "aaaUse hello Azure портала toocreate центра IoT | Документы Microsoft"
description: "Как toocreate, управление и удаление центры Azure IoT через портал Azure hello. Содержит сведения о ценовых категориях, масштабировании, безопасности, а также о настройке обмена сообщениями."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a><span data-ttu-id="aa49c-104">Создать центр IoT с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="aa49c-104">Create an IoT hub using hello Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="aa49c-105">Содержание статьи</span><span class="sxs-lookup"><span data-stu-id="aa49c-105">This article describes:</span></span>

* <span data-ttu-id="aa49c-106">Как toofind hello службы центр IoT в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="aa49c-106">How toofind hello IoT Hub service in hello Azure portal.</span></span>
* <span data-ttu-id="aa49c-107">Как toocreate IoT концентраторов и управление ими.</span><span class="sxs-lookup"><span data-stu-id="aa49c-107">How toocreate and manage IoT hubs.</span></span>

## <a name="where-toofind-hello-iot-hub-service"></a><span data-ttu-id="aa49c-108">Где toofind hello службы центра IoT</span><span class="sxs-lookup"><span data-stu-id="aa49c-108">Where toofind hello IoT Hub service</span></span>

<span data-ttu-id="aa49c-109">Hello службы центра IoT можно найти в следующих элементов на портале hello hello:</span><span class="sxs-lookup"><span data-stu-id="aa49c-109">You can find hello IoT Hub service in hello following locations in hello portal:</span></span>

* <span data-ttu-id="aa49c-110">Выберите **+Создать**, а затем — **Интернет вещей**.</span><span class="sxs-lookup"><span data-stu-id="aa49c-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="aa49c-111">В hello Marketplace, выберите **Интернета вещей**.</span><span class="sxs-lookup"><span data-stu-id="aa49c-111">In hello Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="aa49c-112">Создание центра IoT</span><span class="sxs-lookup"><span data-stu-id="aa49c-112">Create an IoT hub</span></span>

<span data-ttu-id="aa49c-113">Можно создать с помощью следующих методов hello центра IoT.</span><span class="sxs-lookup"><span data-stu-id="aa49c-113">You can create an IoT hub using hello following methods:</span></span>

* <span data-ttu-id="aa49c-114">Hello **+ создать** параметр открывает колонку hello, показанный на следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="aa49c-114">hello **+ New** option opens hello blade shown in hello following screen shot.</span></span> <span data-ttu-id="aa49c-115">Создание центра IoT hello через этот метод и hello marketplace этапы Hello идентичны.</span><span class="sxs-lookup"><span data-stu-id="aa49c-115">hello steps for creating hello IoT hub through this method and through hello marketplace are identical.</span></span>
* <span data-ttu-id="aa49c-116">В hello Marketplace, выберите **создать** tooopen hello колонки, показанный на следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="aa49c-116">In hello Marketplace, choose **Create** tooopen hello blade shown in hello following screen shot.</span></span>

<span data-ttu-id="aa49c-117">Hello следующих разделах описаны hello несколько шагов toocreate центра IoT:</span><span class="sxs-lookup"><span data-stu-id="aa49c-117">hello following sections describe hello several steps toocreate an IoT hub:</span></span>

### <a name="choose-hello-name-of-hello-iot-hub"></a><span data-ttu-id="aa49c-118">Выберите имя центра IoT hello hello</span><span class="sxs-lookup"><span data-stu-id="aa49c-118">Choose hello name of hello IoT hub</span></span>

<span data-ttu-id="aa49c-119">toocreate центра IoT, необходимо присвоить имя центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="aa49c-119">toocreate an IoT hub, you must name hello IoT hub.</span></span> <span data-ttu-id="aa49c-120">Это имя должно быть уникальным среди всех Центров Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="aa49c-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a><span data-ttu-id="aa49c-121">Выберите ценовую категорию hello</span><span class="sxs-lookup"><span data-stu-id="aa49c-121">Choose hello pricing tier</span></span>

<span data-ttu-id="aa49c-122">Доступны четыре уровня: **Бесплатный**, **Стандартный 1**, **Стандартный 2** и **Стандартный S3**.</span><span class="sxs-lookup"><span data-stu-id="aa49c-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="aa49c-123">уровень free Hello позволяет только 500 toobe устройства подключены toohello центр IoT и копирование too8 000 сообщений в день.</span><span class="sxs-lookup"><span data-stu-id="aa49c-123">hello free tier allows only 500 devices toobe connected toohello IoT hub and up too8,000 messages per day.</span></span>

<span data-ttu-id="aa49c-124">**Стандартный S1**: используйте hello S1 edition для решения IoT с большим количеством устройств, генерируют небольших объемов данных.</span><span class="sxs-lookup"><span data-stu-id="aa49c-124">**Standard S1**: Use hello S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="aa49c-125">Каждая единица hello S1 edition позволяет вверх too400 000 сообщений в день на все подключенные устройства.</span><span class="sxs-lookup"><span data-stu-id="aa49c-125">Each unit of hello S1 edition allows up too400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="aa49c-126">**Стандартный S2**: используйте выпуск hello S2 для решения IoT, в которых устройства формировать большие объемы данных.</span><span class="sxs-lookup"><span data-stu-id="aa49c-126">**Standard S2**: Use hello S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="aa49c-127">Каждая единица hello S2 edition позволяет вверх too6 миллионов сообщений в день между все подключенные устройства.</span><span class="sxs-lookup"><span data-stu-id="aa49c-127">Each unit of hello S2 edition allows up too6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="aa49c-128">**Стандартный S3**: используйте выпуск hello S3 IoT решений, созданию больших объемов данных.</span><span class="sxs-lookup"><span data-stu-id="aa49c-128">**Standard S3**: Use hello S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="aa49c-129">Каждая единица hello S3 edition позволяет вверх too300 миллионов сообщений в день между все подключенные устройства.</span><span class="sxs-lookup"><span data-stu-id="aa49c-129">Each unit of hello S3 edition allows up too300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="aa49c-130">Центр Интернета вещей позволяет подключить только один центр уровня "Бесплатный" для каждой подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="aa49c-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="aa49c-131">Единицы Центров Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="aa49c-131">IoT hub units</span></span>

<span data-ttu-id="aa49c-132">Hello допустимое число сообщений за единицу в день, зависит от цен на концентратор.</span><span class="sxs-lookup"><span data-stu-id="aa49c-132">hello number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="aa49c-133">Например hello входящих toosupport концентратора IoT 700 000 сообщений следует выбрать два вида единиц уровня S1.</span><span class="sxs-lookup"><span data-stu-id="aa49c-133">For example, if you want hello IoT hub toosupport ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-toocloud-partitions-and-resource-group"></a><span data-ttu-id="aa49c-134">Устройство toocloud разделы и группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="aa49c-134">Device toocloud partitions and resource group</span></span>

<span data-ttu-id="aa49c-135">Можно изменить hello число разделов для центра IoT.</span><span class="sxs-lookup"><span data-stu-id="aa49c-135">You can change hello number of partitions for an IoT hub.</span></span> <span data-ttu-id="aa49c-136">количество секций по умолчанию Hello имеет значение 4, можно выбрать из раскрывающегося списка hello другой номер.</span><span class="sxs-lookup"><span data-stu-id="aa49c-136">hello default number of partitions is 4, you can choose a different number from hello drop-down list.</span></span>

<span data-ttu-id="aa49c-137">Нет необходимости tooexplicitly создания группы ресурсов пустым.</span><span class="sxs-lookup"><span data-stu-id="aa49c-137">You do not need tooexplicitly create an empty resource group.</span></span> <span data-ttu-id="aa49c-138">При создании ресурса можно выбрать либо toocreate новый или использовать существующую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="aa49c-138">When you create a resource, you can choose either toocreate a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="aa49c-139">Выбор подписки</span><span class="sxs-lookup"><span data-stu-id="aa49c-139">Choose subscription</span></span>

<span data-ttu-id="aa49c-140">Центр IoT Azure автоматически списки hello учетной записи пользователя hello подписки Azure связаны с.</span><span class="sxs-lookup"><span data-stu-id="aa49c-140">Azure IoT Hub automatically lists hello Azure subscriptions hello user account is linked to.</span></span> <span data-ttu-id="aa49c-141">Вы можете hello подписки Azure tooassociate hello в IoT hub.</span><span class="sxs-lookup"><span data-stu-id="aa49c-141">You can choose hello Azure subscription tooassociate hello IoT hub to.</span></span>

### <a name="choose-hello-location"></a><span data-ttu-id="aa49c-142">Выберите расположение hello</span><span class="sxs-lookup"><span data-stu-id="aa49c-142">Choose hello location</span></span>

<span data-ttu-id="aa49c-143">Параметр расположения Hello список hello регионов, где находится центр IoT.</span><span class="sxs-lookup"><span data-stu-id="aa49c-143">hello location option provides a list of hello regions where IoT Hub is available.</span></span>

### <a name="create-hello-iot-hub"></a><span data-ttu-id="aa49c-144">Создать центр IoT hello</span><span class="sxs-lookup"><span data-stu-id="aa49c-144">Create hello IoT hub</span></span>

<span data-ttu-id="aa49c-145">После выполнения всех предыдущих шагов можно создать центр IoT hello.</span><span class="sxs-lookup"><span data-stu-id="aa49c-145">When all previous steps are complete, you can create hello IoT hub.</span></span> <span data-ttu-id="aa49c-146">Нажмите кнопку **создать** toostart hello toocreate серверной части процесса и развертывание центра IoT hello с параметрами hello выбрано.</span><span class="sxs-lookup"><span data-stu-id="aa49c-146">Click **Create** toostart hello back-end process toocreate and deploy hello IoT hub with hello options you chose.</span></span>

<span data-ttu-id="aa49c-147">Может потребоваться центра IoT toocreate hello несколько минут, которое требуется время для hello toorun серверной части развертывания на серверах hello соответствующее расположение.</span><span class="sxs-lookup"><span data-stu-id="aa49c-147">It can take a few minutes toocreate hello IoT hub as it takes time for hello back-end deployment toorun on hello appropriate location servers.</span></span>

## <a name="change-hello-settings-of-hello-iot-hub"></a><span data-ttu-id="aa49c-148">Измените параметры центра IoT hello hello</span><span class="sxs-lookup"><span data-stu-id="aa49c-148">Change hello settings of hello IoT hub</span></span>

<span data-ttu-id="aa49c-149">Можно изменять параметры hello существующего центра IoT, созданный из hello колонке центр IoT.</span><span class="sxs-lookup"><span data-stu-id="aa49c-149">You can change hello settings of an existing IoT hub after it is created from hello IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="aa49c-150">**Политики общего доступа**: эти политики определяют hello разрешения для устройств и служб tooIoT tooconnect концентратора.</span><span class="sxs-lookup"><span data-stu-id="aa49c-150">**Shared access policies**: These policies define hello permissions for devices and services tooconnect tooIoT Hub.</span></span> <span data-ttu-id="aa49c-151">Чтобы открыть эти политики, в разделе **Общие** щелкните пункт **Политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="aa49c-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="aa49c-152">В этой колонке вы сможете изменить существующие политики или добавить новую.</span><span class="sxs-lookup"><span data-stu-id="aa49c-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="aa49c-153">Создание политики</span><span class="sxs-lookup"><span data-stu-id="aa49c-153">Create a policy</span></span>

* <span data-ttu-id="aa49c-154">Нажмите кнопку **добавить** tooopen стоечный модуль.</span><span class="sxs-lookup"><span data-stu-id="aa49c-154">Click **Add** tooopen a blade.</span></span> <span data-ttu-id="aa49c-155">Здесь можно ввести новое имя политики hello и рисунок hello разрешения, как показано в следующих hello должны tooassociate с этой политикой:</span><span class="sxs-lookup"><span data-stu-id="aa49c-155">Here you can enter hello new policy name and hello permissions that you want tooassociate with this policy, as shown in hello following figure:</span></span>

    <span data-ttu-id="aa49c-156">Для общих политик можно указать несколько разрешений.</span><span class="sxs-lookup"><span data-stu-id="aa49c-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="aa49c-157">Hello **чтение реестра** и **записи реестра** политики предоставить чтения и реестру удостоверений toohello права доступа на запись.</span><span class="sxs-lookup"><span data-stu-id="aa49c-157">hello **Registry read** and **Registry write** policies grant read and write access rights toohello identity registry.</span></span> <span data-ttu-id="aa49c-158">При выборе параметра записи hello автоматически выберет hello чтение параметра.</span><span class="sxs-lookup"><span data-stu-id="aa49c-158">Choosing hello write option automatically chooses hello read option.</span></span>

    <span data-ttu-id="aa49c-159">Hello **подключения службы** политика например предоставляет разрешение tooaccess для конечных точек службы **получать устройства в облако**.</span><span class="sxs-lookup"><span data-stu-id="aa49c-159">hello **Service connect** policy grants permission tooaccess service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="aa49c-160">Hello **подключить устройство** политика предоставляет разрешения для отправки и получения сообщений через конечные точки hello IoT Hub на стороне устройства.</span><span class="sxs-lookup"><span data-stu-id="aa49c-160">hello **Device connect** policy grants permissions for sending and receiving messages using hello IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="aa49c-161">Нажмите кнопку **создать** tooadd этом вновь созданные политики toohello существующего списка.</span><span class="sxs-lookup"><span data-stu-id="aa49c-161">Click **Create** tooadd this newly created policy toohello existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="aa49c-162">Endpoints</span><span class="sxs-lookup"><span data-stu-id="aa49c-162">Endpoints</span></span>

<span data-ttu-id="aa49c-163">Нажмите кнопку **конечные точки** toodisplay список конечных точек для центра IoT hello, которые изменяются.</span><span class="sxs-lookup"><span data-stu-id="aa49c-163">Click **Endpoints** toodisplay a list of endpoints for hello IoT hub that you are modifying.</span></span> <span data-ttu-id="aa49c-164">Существует два типа конечных точек: конечные точки, которые встроены в центр IoT hello и конечные точки, добавьте центра IoT toohello после ее создания.</span><span class="sxs-lookup"><span data-stu-id="aa49c-164">There are two types of endpoints: endpoints that are built into hello IoT hub, and endpoints that you add toohello IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="aa49c-165">Встроенные конечные точки</span><span class="sxs-lookup"><span data-stu-id="aa49c-165">Built-in endpoints</span></span>

<span data-ttu-id="aa49c-166">Существуют две встроенные конечные точки: **облако отзыв toodevice** и **события**.</span><span class="sxs-lookup"><span data-stu-id="aa49c-166">There are two built-in endpoints: **Cloud toodevice feedback** and **Events**.</span></span>

* <span data-ttu-id="aa49c-167">**Облако отзыв toodevice** параметры: этот параметр имеет два subsettings: **облако tooDevice TTL** (time-to-live) и **время хранения** (в часах) для сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="aa49c-167">**Cloud toodevice feedback** settings: This setting has two subsettings: **Cloud tooDevice TTL** (time-to-live) and **Retention time** (in hours) for hello messages.</span></span> <span data-ttu-id="aa49c-168">При первом создать центр IoT, оба эти параметра имеет значения по умолчанию hello один час.</span><span class="sxs-lookup"><span data-stu-id="aa49c-168">When your first create an IoT hub, both these settings have hello default value of one hour.</span></span> <span data-ttu-id="aa49c-169">tooadjust эти параметры с помощью ползунков hello, или введите значения hello.</span><span class="sxs-lookup"><span data-stu-id="aa49c-169">tooadjust these settings, use hello sliders or type hello values.</span></span>
* <span data-ttu-id="aa49c-170">**События** имеют несколько вложенных параметров, и некоторые из них доступны только для чтения.</span><span class="sxs-lookup"><span data-stu-id="aa49c-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="aa49c-171">После списка Hello описаны эти параметры:</span><span class="sxs-lookup"><span data-stu-id="aa49c-171">hello following list describes these settings:</span></span>

  * <span data-ttu-id="aa49c-172">**Секции**: значение по умолчанию устанавливается при создании центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="aa49c-172">**Partitions**: A default value is set when hello IoT hub is created.</span></span> <span data-ttu-id="aa49c-173">Hello количество секций через этот параметр можно изменить.</span><span class="sxs-lookup"><span data-stu-id="aa49c-173">You can change hello number of partitions through this setting.</span></span>

  * <span data-ttu-id="aa49c-174">**Имя совместимое концентратора событий и конечной точки**: при создании центра IoT hello концентратор событий создается внутренне, требуется доступ к toounder определенных обстоятельствах.</span><span class="sxs-lookup"><span data-stu-id="aa49c-174">**Event Hub-compatible name and endpoint**: When hello IoT hub is created, an Event Hub is created internally that you may need access toounder certain circumstances.</span></span> <span data-ttu-id="aa49c-175">Нельзя настроить hello совместимое концентратора событий значения имени и конечной точки, но их можно скопировать, щелкнув **копирования**.</span><span class="sxs-lookup"><span data-stu-id="aa49c-175">You cannot customize hello Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="aa49c-176">**Время хранения**: по умолчанию значение tooone день, но его можно изменить с помощью раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="aa49c-176">**Retention Time**: Set tooone day by default but you can change it using hello drop-down list.</span></span> <span data-ttu-id="aa49c-177">Это значение является в днях для приветствия устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="aa49c-177">This value is in days for hello device-to-cloud setting.</span></span>

  * <span data-ttu-id="aa49c-178">**Группы потребителей**: групп потребителей включить несколько сообщений tooread читатели независимо от центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="aa49c-178">**Consumer Groups**: Consumer groups enable multiple readers tooread messages independently from hello IoT hub.</span></span> <span data-ttu-id="aa49c-179">Каждый Центр Интернета вещей создается с одной группой потребителей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="aa49c-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="aa49c-180">Тем не менее можно добавить или удалить потребителя tooyour группы IoT концентраторы, с помощью этого параметра.</span><span class="sxs-lookup"><span data-stu-id="aa49c-180">However, you can add or delete consumer groups tooyour IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="aa49c-181">Нельзя изменить или удалить группу потребителей по умолчанию Hello.</span><span class="sxs-lookup"><span data-stu-id="aa49c-181">hello default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="aa49c-182">Пользовательские конечные точки</span><span class="sxs-lookup"><span data-stu-id="aa49c-182">Custom endpoints</span></span>

<span data-ttu-id="aa49c-183">Можно добавить пользовательские конечные точки на портале hello концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="aa49c-183">You can add custom endpoints on your IoT hub using hello portal.</span></span> <span data-ttu-id="aa49c-184">Из hello **конечные точки** колонке нажмите кнопку **добавить** в верхнем tooopen hello hello **добавить конечную точку** колонку.</span><span class="sxs-lookup"><span data-stu-id="aa49c-184">From hello **Endpoints** blade, click **Add** at hello top tooopen hello **Add endpoint** blade.</span></span> <span data-ttu-id="aa49c-185">Введите hello необходимые сведения, затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="aa49c-185">Enter hello required information, then click **OK**.</span></span> <span data-ttu-id="aa49c-186">Вашей пользовательской конечной точки теперь отображается в главном hello **конечные точки** колонку.</span><span class="sxs-lookup"><span data-stu-id="aa49c-186">Your custom endpoint is now listed in hello main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="aa49c-187">Дополнительные сведения о пользовательских конечных точках см. в статье [Руководство. Конечные точки Центра Интернета вещей][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="aa49c-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="aa49c-188">Маршруты</span><span class="sxs-lookup"><span data-stu-id="aa49c-188">Routes</span></span>

<span data-ttu-id="aa49c-189">Нажмите кнопку **маршруты** toomanage как центр IoT отправляет сообщения устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="aa49c-189">Click **Routes** toomanage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="aa49c-190">Центр IoT tooyour маршруты можно добавить, щелкнув **добавить** вверху hello hello **маршруты*** колонки, введя hello необходимые данные и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="aa49c-190">You can add routes tooyour IoT hub by clicking **Add** at hello top of hello **Routes*** blade, entering hello required information, and clicking **OK**.</span></span> <span data-ttu-id="aa49c-191">Маршрута затем перечисляются в главном hello **маршруты** колонку.</span><span class="sxs-lookup"><span data-stu-id="aa49c-191">Your route is then listed in hello main **Routes** blade.</span></span> <span data-ttu-id="aa49c-192">Маршрут можно изменить, щелкнув его в списке hello маршрутов.</span><span class="sxs-lookup"><span data-stu-id="aa49c-192">You can edit a route by clicking it in hello list of routes.</span></span> <span data-ttu-id="aa49c-193">tooenable маршрут, щелкните его в списке hello маршрутов и задайте hello **включено** переключения слишком**Off**.</span><span class="sxs-lookup"><span data-stu-id="aa49c-193">tooenable a route, click it in hello list of routes and set hello **Enabled** toggle too**Off**.</span></span> <span data-ttu-id="aa49c-194">Изменение toosave hello, нажмите кнопку **ОК** hello нижней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="aa49c-194">toosave hello change, click **OK** at hello bottom of hello blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="aa49c-195">Цены и масштабирование</span><span class="sxs-lookup"><span data-stu-id="aa49c-195">Pricing and scale</span></span>

<span data-ttu-id="aa49c-196">Hello стоимости существующего центра IoT можно изменить с помощью hello **цены** параметры с hello следующие исключения:</span><span class="sxs-lookup"><span data-stu-id="aa49c-196">hello pricing of an existing IoT hub can be changed through hello **Pricing** settings, with hello following exceptions:</span></span>

* <span data-ttu-id="aa49c-197">В текущей реализации hello центр IoT с произвольным SKU нельзя изменить уровни tooone из hello платных SKU, или наоборот.</span><span class="sxs-lookup"><span data-stu-id="aa49c-197">In hello current implementation, an IoT hub with a free SKU cannot change tiers tooone of hello paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="aa49c-198">Может существовать только один центр IoT бесплатный уровень в hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="aa49c-198">There can only be one free tier IoT hub in hello Azure subscription.</span></span>

![][12]

<span data-ttu-id="aa49c-199">Можно перемещать из более высокого уровня toolower только в том случае, когда hello количество сообщений, отправленных в этот день превышена квота hello для hello низкий уровень.</span><span class="sxs-lookup"><span data-stu-id="aa49c-199">You can move from a higher toolower tier only when hello number of messages sent that day do exceed hello quota for hello lower tier.</span></span> <span data-ttu-id="aa49c-200">Например если количество сообщений в день в hello превышает 400 000, hello уровень для hello IoT hub можно изменить.</span><span class="sxs-lookup"><span data-stu-id="aa49c-200">For example, if hello number of messages per day exceeds 400,000, then hello tier for hello IoT hub can be changed.</span></span> <span data-ttu-id="aa49c-201">Однако при изменении уровня S1 toohello центр IoT hello регулируется в тот же день.</span><span class="sxs-lookup"><span data-stu-id="aa49c-201">However, if you change toohello S1 tier then hello IoT hub is throttled for that day.</span></span>

## <a name="delete-hello-iot-hub"></a><span data-ttu-id="aa49c-202">Удаление концентратора IoT hello</span><span class="sxs-lookup"><span data-stu-id="aa49c-202">Delete hello IoT hub</span></span>

<span data-ttu-id="aa49c-203">Можно просматривать центр IoT toohello, выбрав toodelete **Обзор**, и выбрав соответствующий центр toodelete "hello".</span><span class="sxs-lookup"><span data-stu-id="aa49c-203">You can browse toohello IoT hub you want toodelete by clicking **Browse**, and then choosing hello appropriate hub toodelete.</span></span> <span data-ttu-id="aa49c-204">toodelete Здравствуйте центра IoT, нажмите кнопку hello **удалить** кнопку под названием концентратора IoT hello.</span><span class="sxs-lookup"><span data-stu-id="aa49c-204">toodelete hello IoT hub, click hello **Delete** button below hello IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa49c-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aa49c-205">Next steps</span></span>

<span data-ttu-id="aa49c-206">Выполните эти дополнительные сведения об управлении центр IoT Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="aa49c-206">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="aa49c-207">[Массовое управление удостоверениями устройств Центра Интернета вещей][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="aa49c-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="aa49c-208">[Метрики Центра Интернета вещей][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="aa49c-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="aa49c-209">[Мониторинг операций][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="aa49c-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="aa49c-210">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="aa49c-210">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="aa49c-211">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="aa49c-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="aa49c-212">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="aa49c-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="aa49c-213">[Защита вашего решения IoT из hello основание,][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="aa49c-213">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
