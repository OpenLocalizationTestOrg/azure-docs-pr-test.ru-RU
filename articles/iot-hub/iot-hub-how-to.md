---
title: "Использование Центра Интернета вещей в Azure | Документация Майкрософт"
description: "Как разработчик может использовать разные возможности Центра Интернета вещей?"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 786121ae249d69376b4be4c74000868cbb208989
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-iot-hub"></a><span data-ttu-id="ea21c-103">Использование Центра Интернета вещей в Azure</span><span class="sxs-lookup"><span data-stu-id="ea21c-103">How to use Azure IoT Hub</span></span>

<span data-ttu-id="ea21c-104">Вы можете обучиться разработке для служб Центра Интернета вещей разными способами:</span><span class="sxs-lookup"><span data-stu-id="ea21c-104">You have various options to learn how to develop for the IoT Hub service:</span></span>

* <span data-ttu-id="ea21c-105">прочтите статьи с подробным описанием основных понятий и возможностей Центра Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="ea21c-105">Read the conceptual articles that describe the features of IoT Hub in detail.</span></span>
* <span data-ttu-id="ea21c-106">выполните задачи в одном из руководств, посвященных различным возможностям Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ea21c-106">Follow one of the tutorials that cover the various features of IoT Hub.</span></span>

## <a name="developer-guide"></a><span data-ttu-id="ea21c-107">Руководство разработчика по центру Azure IoT (IoT — Интернет вещей)</span><span class="sxs-lookup"><span data-stu-id="ea21c-107">Developer guide</span></span>

<span data-ttu-id="ea21c-108">Разработчики могут ознакомиться с подробной документацией о Центре Интернета вещей из [руководства разработчика][lnk-devguide].</span><span class="sxs-lookup"><span data-stu-id="ea21c-108">As a developer, you can read detailed conceptual guidance about IoT Hub in the [Developer Guide][lnk-devguide].</span></span> <span data-ttu-id="ea21c-109">Это руководство содержит:</span><span class="sxs-lookup"><span data-stu-id="ea21c-109">This guide includes:</span></span>

* <span data-ttu-id="ea21c-110">подробное описание всех возможностей Центра Интернета вещей и способов их использования;</span><span class="sxs-lookup"><span data-stu-id="ea21c-110">Detailed descriptions of all IoT Hub features that help you to learn how to use them.</span></span>
* <span data-ttu-id="ea21c-111">рекомендации по выбору, если доступно несколько вариантов.</span><span class="sxs-lookup"><span data-stu-id="ea21c-111">Guidance on how to choose when multiple options are available.</span></span>

## <a name="tutorials"></a><span data-ttu-id="ea21c-112">Учебники</span><span class="sxs-lookup"><span data-stu-id="ea21c-112">Tutorials</span></span>

<span data-ttu-id="ea21c-113">Если вы предпочитаете изучать определенные функции Центра Интернета вещей с помощью практических упражнений, доступно несколько руководств.</span><span class="sxs-lookup"><span data-stu-id="ea21c-113">If you prefer to learn about specific IoT Hub features by working through hands-on exercises, there are several tutorials to choose from.</span></span> <span data-ttu-id="ea21c-114">Некоторые руководства описывают работу с разными языками программирования.</span><span class="sxs-lookup"><span data-stu-id="ea21c-114">Many of these tutorials are available in multiple programming languages.</span></span> <span data-ttu-id="ea21c-115">Ниже представлен список таких руководств.</span><span class="sxs-lookup"><span data-stu-id="ea21c-115">These tutorials include:</span></span>

- <span data-ttu-id="ea21c-116">[Обработка сообщений Центра Интернета вещей, отправляемых с устройства в облако, с использованием маршрутов (.NET)][lnk-routes-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ea21c-116">[Process IoT Hub device-to-cloud messages using routes][lnk-routes-tutorial].</span></span> <span data-ttu-id="ea21c-117">Из этого руководства вы узнаете, как через настройки системы можно использовать правила маршрутизации Центра Интернета вещей для перенаправления сообщений, отправляемых с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="ea21c-117">This tutorial shows you how to use IoT Hub routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>

- <span data-ttu-id="ea21c-118">[Отправка сообщений из облака на устройство с помощью Центра Интернета вещей (.NET)][lnk-c2d-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ea21c-118">[Send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial].</span></span> <span data-ttu-id="ea21c-119">В этом руководстве описано, как отправлять сообщения из облака на устройства с помощью Центра Интернета вещей и получать сообщения, передаваемые из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="ea21c-119">This tutorial shows you how to send cloud-to-device messages through IoT Hub and receive cloud-to-device messages on a device.</span></span>

- <span data-ttu-id="ea21c-120">[Передача файлов из устройств в облако в Центре Интернета вещей][lnk-upload-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ea21c-120">[Upload files from devices to the cloud with IoT Hub][lnk-upload-tutorial].</span></span> <span data-ttu-id="ea21c-121">В этом руководстве описано, как использовать возможности передачи файлов Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ea21c-121">This tutorial shows you how to use the file upload capabilities of IoT Hub.</span></span>

- <span data-ttu-id="ea21c-122">[Начало работы с двойниками устройств (Node)][lnk-twin-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ea21c-122">[Get started with device twins][lnk-twin-tutorial].</span></span> <span data-ttu-id="ea21c-123">В этом руководстве описываются двойники устройств, сообщаемые свойства, требуемые свойства и теги.</span><span class="sxs-lookup"><span data-stu-id="ea21c-123">This tutorial introduces you to device twins, reported properties, desired properties, and tags.</span></span> <span data-ttu-id="ea21c-124">Двойники устройств позволяют синхронизировать значения с устройствами.</span><span class="sxs-lookup"><span data-stu-id="ea21c-124">You use device twins to synchronize values with your devices.</span></span>

- <span data-ttu-id="ea21c-125">[Использование прямых методов (Node)][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ea21c-125">[Use direct methods][lnk-methods-tutorial].</span></span> <span data-ttu-id="ea21c-126">В этом руководстве описано использование прямых методов.</span><span class="sxs-lookup"><span data-stu-id="ea21c-126">This tutorial shows you how to use direct methods.</span></span> <span data-ttu-id="ea21c-127">Вы добавляете обработчик для прямого метода на виртуальном устройстве и вызываете прямой метод из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ea21c-127">You add a handler for a direct method in your simulated device and invoke the direct method from IoT Hub.</span></span>

- <span data-ttu-id="ea21c-128">[Начало работы с управлением устройствами (Node)][lnk-dm-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ea21c-128">[Get started with device management][lnk-dm-tutorial].</span></span> <span data-ttu-id="ea21c-129">В этом руководстве описано, как использовать ключевые функции управления устройствами (например, функции двойника устройства или прямого метода).</span><span class="sxs-lookup"><span data-stu-id="ea21c-129">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="ea21c-130">Эти функции используются для удаленной перезагрузки виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="ea21c-130">You use these features to remotely reboot your simulated device.</span></span>

- <span data-ttu-id="ea21c-131">[Настройка устройств с помощью требуемых свойств][lnk-properties-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ea21c-131">[Use desired properties to configure devices][lnk-properties-tutorial].</span></span> <span data-ttu-id="ea21c-132">В этом руководстве представлены сведения об удаленной настройке устройства с помощью сообщаемых свойств двойника устройства.</span><span class="sxs-lookup"><span data-stu-id="ea21c-132">This tutorial shows you how to use the device twin's desired and reported properties, to remotely configure your device.</span></span>

- <span data-ttu-id="ea21c-133">[Используйте управление устройствами, чтобы запустить обновление встроенного ПО устройства (Node/Node)][lnk-jobs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ea21c-133">[Use device jobs to initiate a device firmware update][lnk-jobs-tutorial].</span></span> <span data-ttu-id="ea21c-134">В этом руководстве описано, как использовать ключевые функции управления устройствами (например, функции двойника устройства или прямого метода).</span><span class="sxs-lookup"><span data-stu-id="ea21c-134">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="ea21c-135">Вы узнаете, как применять эти функции для удаленного обновления встроенного ПО на устройстве.</span><span class="sxs-lookup"><span data-stu-id="ea21c-135">You learn how to use these features to remotely update your device's firmware.</span></span>

- <span data-ttu-id="ea21c-136">[Учебник. Планирование и трансляция заданий][lnk-schedule-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ea21c-136">[Schedule and broadcast jobs][lnk-schedule-tutorial].</span></span> <span data-ttu-id="ea21c-137">В этом руководстве показано, как использовать требуемые свойства и прямые методы для взаимодействия с несколькими устройствами в запланированное время.</span><span class="sxs-lookup"><span data-stu-id="ea21c-137">This tutorial shows you how to use desired properties and direct methods to interact with multiple devices at a scheduled time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea21c-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ea21c-138">Next steps</span></span>

<span data-ttu-id="ea21c-139">Дополнительные сведения о службе Центра Интернета вещей см. в [руководстве для разработчика][lnk-devguide].</span><span class="sxs-lookup"><span data-stu-id="ea21c-139">To learn more about the IoT Hub service, see the [Developer Guide][lnk-devguide].</span></span>

[lnk-devguide]: ./iot-hub-devguide.md
[lnk-routes-tutorial]: ./iot-hub-csharp-csharp-process-d2c.md
[lnk-c2d-tutorial]: ./iot-hub-csharp-csharp-c2d.md
[lnk-upload-tutorial]: ./iot-hub-csharp-csharp-file-upload.md
[lnk-twin-tutorial]: ./iot-hub-node-node-twin-getstarted.md
[lnk-methods-tutorial]: ./iot-hub-node-node-direct-methods.md
[lnk-dm-tutorial]: ./iot-hub-node-node-device-management-get-started.md
[lnk-properties-tutorial]: ./iot-hub-node-node-twin-how-to-configure.md
[lnk-jobs-tutorial]: ./iot-hub-node-node-firmware-update.md
[lnk-schedule-tutorial]: ./iot-hub-node-node-schedule-jobs.md