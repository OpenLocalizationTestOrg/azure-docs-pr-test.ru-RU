---
title: "Создание Центра Интернета вещей на портале Azure | Документация Майкрософт"
description: "Сведения о том, как с помощью портала Azure создавать и удалять Центры Интернета вещей Azure, а также управлять ими. Содержит сведения о ценовых категориях, масштабировании, безопасности, а также о настройке обмена сообщениями."
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
ms.openlocfilehash: bca7eea5f44bbed3b784b56edaac235161b43e5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-portal"></a><span data-ttu-id="47a5d-104">Создание Центра Интернета вещей с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="47a5d-104">Create an IoT hub using the Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="47a5d-105">Содержание статьи</span><span class="sxs-lookup"><span data-stu-id="47a5d-105">This article describes:</span></span>

* <span data-ttu-id="47a5d-106">Как найти Центр Интернета вещей на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="47a5d-106">How to find the IoT Hub service in the Azure portal.</span></span>
* <span data-ttu-id="47a5d-107">Как создавать и администрировать Центры Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="47a5d-107">How to create and manage IoT hubs.</span></span>

## <a name="where-to-find-the-iot-hub-service"></a><span data-ttu-id="47a5d-108">Где найти службу Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="47a5d-108">Where to find the IoT Hub service</span></span>

<span data-ttu-id="47a5d-109">Службу Центра Интернета вещей на портале можно найти в следующих расположениях:</span><span class="sxs-lookup"><span data-stu-id="47a5d-109">You can find the IoT Hub service in the following locations in the portal:</span></span>

* <span data-ttu-id="47a5d-110">Выберите **+Создать**, а затем — **Интернет вещей**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="47a5d-111">В Microsoft Azure Marketplace выберите **Интернет вещей**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-111">In the Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="47a5d-112">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="47a5d-112">Create an IoT hub</span></span>

<span data-ttu-id="47a5d-113">Центр Интернета вещей можно создать с помощью следующих методов.</span><span class="sxs-lookup"><span data-stu-id="47a5d-113">You can create an IoT hub using the following methods:</span></span>

* <span data-ttu-id="47a5d-114">Действие **+Создать** открывает представленную ниже колонку.</span><span class="sxs-lookup"><span data-stu-id="47a5d-114">The **+ New** option opens the blade shown in the following screen shot.</span></span> <span data-ttu-id="47a5d-115">Шаги по созданию Центра Интернета вещей будут такими же, как и в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="47a5d-115">The steps for creating the IoT hub through this method and through the marketplace are identical.</span></span>
* <span data-ttu-id="47a5d-116">В Marketplace выберите **Создать**, чтобы открыть представленную ниже колонку.</span><span class="sxs-lookup"><span data-stu-id="47a5d-116">In the Marketplace, choose **Create** to open the blade shown in the following screen shot.</span></span>

<span data-ttu-id="47a5d-117">В следующих разделах поэтапно описано создание Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="47a5d-117">The following sections describe the several steps to create an IoT hub:</span></span>

### <a name="choose-the-name-of-the-iot-hub"></a><span data-ttu-id="47a5d-118">Выбор имени Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="47a5d-118">Choose the name of the IoT hub</span></span>

<span data-ttu-id="47a5d-119">Чтобы создать Центр Интернета вещей, следует указать его имя.</span><span class="sxs-lookup"><span data-stu-id="47a5d-119">To create an IoT hub, you must name the IoT hub.</span></span> <span data-ttu-id="47a5d-120">Это имя должно быть уникальным среди всех Центров Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="47a5d-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-the-pricing-tier"></a><span data-ttu-id="47a5d-121">Выбор ценового уровня</span><span class="sxs-lookup"><span data-stu-id="47a5d-121">Choose the pricing tier</span></span>

<span data-ttu-id="47a5d-122">Доступны четыре уровня: **Бесплатный**, **Стандартный 1**, **Стандартный 2** и **Стандартный S3**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="47a5d-123">Уровень "Бесплатный" позволяет подключить к Центру Интернета вещей только 500 устройств и отправлять до 8000 сообщений в день.</span><span class="sxs-lookup"><span data-stu-id="47a5d-123">The free tier allows only 500 devices to be connected to the IoT hub and up to 8,000 messages per day.</span></span>

<span data-ttu-id="47a5d-124">**Стандартный S1**: используйте выпуск S1 для решений Интернета вещей с большим числом устройств, каждое из которых генерирует небольшой объем данных.</span><span class="sxs-lookup"><span data-stu-id="47a5d-124">**Standard S1**: Use the S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="47a5d-125">Каждая единица выпуска S1 позволяет передавать не более 400 тыс. сообщений в день со всех устройств.</span><span class="sxs-lookup"><span data-stu-id="47a5d-125">Each unit of the S1 edition allows up to 400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="47a5d-126">**Стандартный S2**: выпуск S2 предназначен для решений Интернета вещей, в которых устройства генерируют большие объемы данных.</span><span class="sxs-lookup"><span data-stu-id="47a5d-126">**Standard S2**: Use the S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="47a5d-127">Каждая единица выпуска S2 позволяет передавать не более 6 млн сообщений в день со всех устройств.</span><span class="sxs-lookup"><span data-stu-id="47a5d-127">Each unit of the S2 edition allows up to 6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="47a5d-128">**Стандартный S3**: выпуск S3 предназначен для решений Интернета вещей с огромными объемами данных.</span><span class="sxs-lookup"><span data-stu-id="47a5d-128">**Standard S3**: Use the S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="47a5d-129">Каждая единица выпуска S3 позволяет передавать не более 300 млн сообщений в день со всех устройств.</span><span class="sxs-lookup"><span data-stu-id="47a5d-129">Each unit of the S3 edition allows up to 300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="47a5d-130">Центр Интернета вещей позволяет подключить только один центр уровня "Бесплатный" для каждой подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="47a5d-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="47a5d-131">Единицы Центров Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="47a5d-131">IoT hub units</span></span>

<span data-ttu-id="47a5d-132">Допустимое число сообщений за единицу в сутки зависит от ценовой категории концентратора.</span><span class="sxs-lookup"><span data-stu-id="47a5d-132">The number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="47a5d-133">Например, если требуется, чтобы Центр Интернета вещей поддерживал 700 000 входящих сообщений, то следует выбрать две единицы уровня S1.</span><span class="sxs-lookup"><span data-stu-id="47a5d-133">For example, if you want the IoT hub to support ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-to-cloud-partitions-and-resource-group"></a><span data-ttu-id="47a5d-134">Разделы «с устройства в облако» и группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="47a5d-134">Device to cloud partitions and resource group</span></span>

<span data-ttu-id="47a5d-135">Вы можете изменить количество разделов для Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="47a5d-135">You can change the number of partitions for an IoT hub.</span></span> <span data-ttu-id="47a5d-136">По умолчанию устанавливается четыре раздела, но вы можете изменить это число, используя раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="47a5d-136">The default number of partitions is 4, you can choose a different number from the drop-down list.</span></span>

<span data-ttu-id="47a5d-137">Отдельно создавать пустую группу ресурсов необязательно.</span><span class="sxs-lookup"><span data-stu-id="47a5d-137">You do not need to explicitly create an empty resource group.</span></span> <span data-ttu-id="47a5d-138">При создании ресурса вы можете выбрать существующую группу ресурсов или создать новую.</span><span class="sxs-lookup"><span data-stu-id="47a5d-138">When you create a resource, you can choose either to create a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="47a5d-139">Выбор подписки</span><span class="sxs-lookup"><span data-stu-id="47a5d-139">Choose subscription</span></span>

<span data-ttu-id="47a5d-140">Центр Интернета вещей Azure автоматически отображает все подписки, с которыми связана учетная запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="47a5d-140">Azure IoT Hub automatically lists the Azure subscriptions the user account is linked to.</span></span> <span data-ttu-id="47a5d-141">Здесь вы можете выбрать подписку Azure, с которой будет связан Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="47a5d-141">You can choose the Azure subscription to associate the IoT hub to.</span></span>

### <a name="choose-the-location"></a><span data-ttu-id="47a5d-142">Выберите расположение</span><span class="sxs-lookup"><span data-stu-id="47a5d-142">Choose the location</span></span>

<span data-ttu-id="47a5d-143">Параметр расположения содержит список регионов, в которых доступен Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="47a5d-143">The location option provides a list of the regions where IoT Hub is available.</span></span>

### <a name="create-the-iot-hub"></a><span data-ttu-id="47a5d-144">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="47a5d-144">Create the IoT hub</span></span>

<span data-ttu-id="47a5d-145">Когда вы выполните все описанные шаги, Центр Интернета вещей будет готов к созданию.</span><span class="sxs-lookup"><span data-stu-id="47a5d-145">When all previous steps are complete, you can create the IoT hub.</span></span> <span data-ttu-id="47a5d-146">Нажмите кнопку **Создать**, чтобы запустить фоновый процесс создания и развертывания Центра Интернета вещей с настроенными параметрами.</span><span class="sxs-lookup"><span data-stu-id="47a5d-146">Click **Create** to start the back-end process to create and deploy the IoT hub with the options you chose.</span></span>

<span data-ttu-id="47a5d-147">Процесс создания Центра Интернета вещей может занять несколько минут, так как развертывание для запуска на серверах в нужном расположении требует некоторого времени.</span><span class="sxs-lookup"><span data-stu-id="47a5d-147">It can take a few minutes to create the IoT hub as it takes time for the back-end deployment to run on the appropriate location servers.</span></span>

## <a name="change-the-settings-of-the-iot-hub"></a><span data-ttu-id="47a5d-148">Изменение параметров Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="47a5d-148">Change the settings of the IoT hub</span></span>

<span data-ttu-id="47a5d-149">Вы можете изменить параметры Центра Интернета вещей после его создания, используя колонку этого центра.</span><span class="sxs-lookup"><span data-stu-id="47a5d-149">You can change the settings of an existing IoT hub after it is created from the IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="47a5d-150">**Политики общего доступа:** эти политики определяют разрешения для подключения устройств и служб к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="47a5d-150">**Shared access policies**: These policies define the permissions for devices and services to connect to IoT Hub.</span></span> <span data-ttu-id="47a5d-151">Чтобы открыть эти политики, в разделе **Общие** щелкните пункт **Политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="47a5d-152">В этой колонке вы сможете изменить существующие политики или добавить новую.</span><span class="sxs-lookup"><span data-stu-id="47a5d-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="47a5d-153">Создание политики</span><span class="sxs-lookup"><span data-stu-id="47a5d-153">Create a policy</span></span>

* <span data-ttu-id="47a5d-154">Щелкните **Добавить**, чтобы открыть колонку.</span><span class="sxs-lookup"><span data-stu-id="47a5d-154">Click **Add** to open a blade.</span></span> <span data-ttu-id="47a5d-155">Здесь можно ввести новое имя политики и указать разрешения, которые нужно связать с ней. Эта колонка показана на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="47a5d-155">Here you can enter the new policy name and the permissions that you want to associate with this policy, as shown in the following figure:</span></span>

    <span data-ttu-id="47a5d-156">Для общих политик можно указать несколько разрешений.</span><span class="sxs-lookup"><span data-stu-id="47a5d-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="47a5d-157">Политики **Чтение реестра** и **Запись в реестр** предоставляют права на чтение и запись в реестре удостоверений.</span><span class="sxs-lookup"><span data-stu-id="47a5d-157">The **Registry read** and **Registry write** policies grant read and write access rights to the identity registry.</span></span> <span data-ttu-id="47a5d-158">Если вы выберете разрешение на запись, разрешение на чтение добавляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="47a5d-158">Choosing the write option automatically chooses the read option.</span></span>

    <span data-ttu-id="47a5d-159">Политика **Подключение службы** предоставляет разрешение на доступ к конечным точкам службы, например для **передачи данных от устройства в облако**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-159">The **Service connect** policy grants permission to access service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="47a5d-160">Политика **Подключение устройства** предоставляет разрешения на отправку и получение сообщений через конечные точки Центра Интернета вещей на стороне устройства.</span><span class="sxs-lookup"><span data-stu-id="47a5d-160">The **Device connect** policy grants permissions for sending and receiving messages using the IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="47a5d-161">Чтобы добавить новую политику к списку уже существующих, нажмите кнопку **Создать** .</span><span class="sxs-lookup"><span data-stu-id="47a5d-161">Click **Create** to add this newly created policy to the existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="47a5d-162">Endpoints</span><span class="sxs-lookup"><span data-stu-id="47a5d-162">Endpoints</span></span>

<span data-ttu-id="47a5d-163">Щелкните **Конечные точки**, чтобы отобразить список конечных точек для редактируемого Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="47a5d-163">Click **Endpoints** to display a list of endpoints for the IoT hub that you are modifying.</span></span> <span data-ttu-id="47a5d-164">Существует два типа конечных точек: конечные точки, встроенные в Центр Интернета вещей, и конечные точки, добавляемые в Центр Интернета вещей после его создания.</span><span class="sxs-lookup"><span data-stu-id="47a5d-164">There are two types of endpoints: endpoints that are built into the IoT hub, and endpoints that you add to the IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="47a5d-165">Встроенные конечные точки</span><span class="sxs-lookup"><span data-stu-id="47a5d-165">Built-in endpoints</span></span>

<span data-ttu-id="47a5d-166">Встроенные конечные точки делятся на два типа: **Cloud to device feedback** (Ответ, отправляемый из облака на устройство) и **События**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-166">There are two built-in endpoints: **Cloud to device feedback** and **Events**.</span></span>

* <span data-ttu-id="47a5d-167">**Cloud to device feedback** (Ответ, отправляемый из облака на устройство) имеет два вложенных параметра: **Cloud to Device TTL** (Срок жизни) и **Время хранения** (в часах) для сообщений.</span><span class="sxs-lookup"><span data-stu-id="47a5d-167">**Cloud to device feedback** settings: This setting has two subsettings: **Cloud to Device TTL** (time-to-live) and **Retention time** (in hours) for the messages.</span></span> <span data-ttu-id="47a5d-168">При создании Центра Интернета вещей оба этих параметра имеют значение по умолчанию "один час".</span><span class="sxs-lookup"><span data-stu-id="47a5d-168">When your first create an IoT hub, both these settings have the default value of one hour.</span></span> <span data-ttu-id="47a5d-169">Чтобы изменить эти параметры, используйте ползунки или введите значения вручную.</span><span class="sxs-lookup"><span data-stu-id="47a5d-169">To adjust these settings, use the sliders or type the values.</span></span>
* <span data-ttu-id="47a5d-170">**События** имеют несколько вложенных параметров, и некоторые из них доступны только для чтения.</span><span class="sxs-lookup"><span data-stu-id="47a5d-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="47a5d-171">Эти параметры приведены в следующем списке:</span><span class="sxs-lookup"><span data-stu-id="47a5d-171">The following list describes these settings:</span></span>

  * <span data-ttu-id="47a5d-172">**Секции**: значение по умолчанию задается при создании Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="47a5d-172">**Partitions**: A default value is set when the IoT hub is created.</span></span> <span data-ttu-id="47a5d-173">Вы можете изменить количество секций, используя этот параметр.</span><span class="sxs-lookup"><span data-stu-id="47a5d-173">You can change the number of partitions through this setting.</span></span>

  * <span data-ttu-id="47a5d-174">**Имя и конечная точка, совместимые с концентратором событий.** При создании Центра Интернета вещей автоматически создается концентратор событий, к которому при некоторых обстоятельствах может потребоваться доступ.</span><span class="sxs-lookup"><span data-stu-id="47a5d-174">**Event Hub-compatible name and endpoint**: When the IoT hub is created, an Event Hub is created internally that you may need access to under certain circumstances.</span></span> <span data-ttu-id="47a5d-175">Значения имени и конечной точки, совместимых с концентраторами событий, невозможно изменить, но их можно скопировать, щелкнув **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-175">You cannot customize the Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="47a5d-176">**Время хранения**: по умолчанию устанавливается значение "один день", но его можно изменить с помощью раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="47a5d-176">**Retention Time**: Set to one day by default but you can change it using the drop-down list.</span></span> <span data-ttu-id="47a5d-177">Это значение задается в днях и относится к событиям, передаваемым с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="47a5d-177">This value is in days for the device-to-cloud setting.</span></span>

  * <span data-ttu-id="47a5d-178">**Группы потребителей** позволяют сгруппировать модули чтения, которые будут независимо друг от друга получать сообщения от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="47a5d-178">**Consumer Groups**: Consumer groups enable multiple readers to read messages independently from the IoT hub.</span></span> <span data-ttu-id="47a5d-179">Каждый Центр Интернета вещей создается с одной группой потребителей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="47a5d-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="47a5d-180">С помощью этого параметра можно добавлять и удалять группы потребителей для Центров Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="47a5d-180">However, you can add or delete consumer groups to your IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="47a5d-181">Группа потребителей по умолчанию не может быть удалена или изменена.</span><span class="sxs-lookup"><span data-stu-id="47a5d-181">The default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="47a5d-182">Пользовательские конечные точки</span><span class="sxs-lookup"><span data-stu-id="47a5d-182">Custom endpoints</span></span>

<span data-ttu-id="47a5d-183">Пользовательские конечные точки можно добавить в Центр Интернета вещей с помощью портала.</span><span class="sxs-lookup"><span data-stu-id="47a5d-183">You can add custom endpoints on your IoT hub using the portal.</span></span> <span data-ttu-id="47a5d-184">В верхней части колонки **Конечные точки** щелкните **Добавить**, чтобы открыть колонку **Добавить конечную точку**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-184">From the **Endpoints** blade, click **Add** at the top to open the **Add endpoint** blade.</span></span> <span data-ttu-id="47a5d-185">Введите необходимые сведения и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-185">Enter the required information, then click **OK**.</span></span> <span data-ttu-id="47a5d-186">После этого пользовательская конечная точка появится в основной колонке **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-186">Your custom endpoint is now listed in the main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="47a5d-187">Дополнительные сведения о пользовательских конечных точках см. в статье [Руководство. Конечные точки Центра Интернета вещей][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="47a5d-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="47a5d-188">Маршруты</span><span class="sxs-lookup"><span data-stu-id="47a5d-188">Routes</span></span>

<span data-ttu-id="47a5d-189">Щелкните **Маршруты**, чтобы управлять тем, как Центр Интернета вещей отправляет сообщения из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="47a5d-189">Click **Routes** to manage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="47a5d-190">Вы можете добавить маршруты для Центра Интернета вещей. Для этого в верхней части колонки **Маршруты*** щелкните **Добавить** , введите необходимые сведения и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-190">You can add routes to your IoT hub by clicking **Add** at the top of the **Routes*** blade, entering the required information, and clicking **OK**.</span></span> <span data-ttu-id="47a5d-191">После этого ваш маршрут появится в основной колонке **Маршруты**.</span><span class="sxs-lookup"><span data-stu-id="47a5d-191">Your route is then listed in the main **Routes** blade.</span></span> <span data-ttu-id="47a5d-192">Маршрут можно изменить, щелкнув его в списке маршрутов.</span><span class="sxs-lookup"><span data-stu-id="47a5d-192">You can edit a route by clicking it in the list of routes.</span></span> <span data-ttu-id="47a5d-193">Чтобы включить маршрут, щелкните его в списке маршрутов и установите переключатель **включения и отключения** в положение **Выкл**</span><span class="sxs-lookup"><span data-stu-id="47a5d-193">To enable a route, click it in the list of routes and set the **Enabled** toggle to **Off**.</span></span> <span data-ttu-id="47a5d-194">Нажмите кнопку **ОК** в нижней части колонки, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="47a5d-194">To save the change, click **OK** at the bottom of the blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="47a5d-195">Цены и масштабирование</span><span class="sxs-lookup"><span data-stu-id="47a5d-195">Pricing and scale</span></span>

<span data-ttu-id="47a5d-196">Вы можете изменить цену существующего Центра Интернета вещей с помощью параметров **Цены**, но есть определенные исключения.</span><span class="sxs-lookup"><span data-stu-id="47a5d-196">The pricing of an existing IoT hub can be changed through the **Pricing** settings, with the following exceptions:</span></span>

* <span data-ttu-id="47a5d-197">В текущей версии нельзя перенести Центр Интернета вещей с бесплатного уровня на один из платных, и наоборот.</span><span class="sxs-lookup"><span data-stu-id="47a5d-197">In the current implementation, an IoT hub with a free SKU cannot change tiers to one of the paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="47a5d-198">Для каждой подписки Azure можно использовать только один Центр Интернета вещей уровня "Бесплатный".</span><span class="sxs-lookup"><span data-stu-id="47a5d-198">There can only be one free tier IoT hub in the Azure subscription.</span></span>

![][12]

<span data-ttu-id="47a5d-199">Вы можете перейти с высокого уровня на более низкий, только если число сообщений за текущий день еще не превысило квоту, установленную для более низкого уровня.</span><span class="sxs-lookup"><span data-stu-id="47a5d-199">You can move from a higher to lower tier only when the number of messages sent that day do exceed the quota for the lower tier.</span></span> <span data-ttu-id="47a5d-200">Например, если количество сообщений за день превышает 400 000, уровень Центра Интернета вещей может измениться.</span><span class="sxs-lookup"><span data-stu-id="47a5d-200">For example, if the number of messages per day exceeds 400,000, then the tier for the IoT hub can be changed.</span></span> <span data-ttu-id="47a5d-201">Однако если изменить уровень на S1, Центр Интернета вещей регулируется в зависимости от количества сообщений, полученных на протяжении этого дня.</span><span class="sxs-lookup"><span data-stu-id="47a5d-201">However, if you change to the S1 tier then the IoT hub is throttled for that day.</span></span>

## <a name="delete-the-iot-hub"></a><span data-ttu-id="47a5d-202">Удаление Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="47a5d-202">Delete the IoT hub</span></span>

<span data-ttu-id="47a5d-203">Вы можете найти Центр Интернета вещей с помощью кнопки **Обзор** и выбрать его для удаления.</span><span class="sxs-lookup"><span data-stu-id="47a5d-203">You can browse to the IoT hub you want to delete by clicking **Browse**, and then choosing the appropriate hub to delete.</span></span> <span data-ttu-id="47a5d-204">Чтобы удалить Центр Интернета вещей, нажмите кнопку **Удалить** под соответствующим именем.</span><span class="sxs-lookup"><span data-stu-id="47a5d-204">To delete the IoT hub, click the **Delete** button below the IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47a5d-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47a5d-205">Next steps</span></span>

<span data-ttu-id="47a5d-206">Дополнительные сведения об управлении центром Интернета вещей в Azure см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="47a5d-206">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="47a5d-207">[Массовое управление удостоверениями устройств Центра Интернета вещей][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="47a5d-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="47a5d-208">[Метрики Центра Интернета вещей][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="47a5d-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="47a5d-209">[Мониторинг операций][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="47a5d-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="47a5d-210">Для дальнейшего изучения возможностей Центра Интернета вещей см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="47a5d-210">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="47a5d-211">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="47a5d-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="47a5d-212">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="47a5d-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="47a5d-213">[Все аспекты безопасности решения Центра Интернета вещей][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="47a5d-213">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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
