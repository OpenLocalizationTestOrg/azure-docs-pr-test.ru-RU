---
title: "Замена контроллера EBOD на устройстве StorSimple | Документация Майкрософт"
description: "Объясняется процесс снятия или замены одного или обоих контроллеров EBOD на устройстве StorSimple 8600."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 23d819ddc3bbcbaf2847cdcc9191407ead0ff43d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="c8e9e-103">Замена контроллера EBOD на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="c8e9e-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="c8e9e-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c8e9e-104">Overview</span></span>
<span data-ttu-id="c8e9e-105">В этом учебнике объясняется, как заменить неисправный модуль контроллера EBOD на устройстве Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-105">This tutorial explains how to replace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="c8e9e-106">Чтобы заменить модуль контроллера EBOD, необходимо:</span><span class="sxs-lookup"><span data-stu-id="c8e9e-106">To replace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="c8e9e-107">снять неисправный контроллер EBOD</span><span class="sxs-lookup"><span data-stu-id="c8e9e-107">Remove the faulty EBOD controller</span></span>
* <span data-ttu-id="c8e9e-108">установить новый контроллер EBOD</span><span class="sxs-lookup"><span data-stu-id="c8e9e-108">Install a new EBOD controller</span></span>

<span data-ttu-id="c8e9e-109">Прежде чем начать, ознакомьтесь с приведенной ниже информацией.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-109">Consider the following information before you begin:</span></span>

* <span data-ttu-id="c8e9e-110">Во все неиспользуемые отсеки должны быть установлены пустые модули EBOD.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="c8e9e-111">Если хотя бы один отсек останется открытым, корпус не сможет правильно охлаждаться.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-111">The enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="c8e9e-112">Контроллер EBOD поддерживает горячую замену, и его можно снять или заменить.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-112">The EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="c8e9e-113">Не снимайте неисправный модуль, если у вас нет модуля на замену.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="c8e9e-114">После начала процесса замены его необходимо завершить в течение 10 минут.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-114">When you initiate the replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8e9e-115">Перед снятием или заменой любого компонента StorSimple обязательно ознакомьтесь с [условными обозначениями сведений о безопасности](storsimple-safety.md#safety-icon-conventions) и другими [мерами предосторожности](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="c8e9e-115">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="c8e9e-116">Снятие контроллера EBOD</span><span class="sxs-lookup"><span data-stu-id="c8e9e-116">Remove an EBOD controller</span></span>
<span data-ttu-id="c8e9e-117">Перед заменой неисправного модуля контроллера EBOD в устройстве StorSimple убедитесь, что модуль другого контроллера EBOD включен и работает.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-117">Before replacing the failed EBOD controller module in your StorSimple device, make sure that the other EBOD controller module is active and running.</span></span> <span data-ttu-id="c8e9e-118">Снятие модуля контроллера EBOD описано в следующей процедуре и таблице.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-118">The following procedure and table explain how to remove the EBOD controller module.</span></span>

#### <a name="to-remove-an-ebod-module"></a><span data-ttu-id="c8e9e-119">Снятие модуля EBOD</span><span class="sxs-lookup"><span data-stu-id="c8e9e-119">To remove an EBOD module</span></span>
1. <span data-ttu-id="c8e9e-120">Откройте классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-120">Open the Azure classic portal.</span></span>
2. <span data-ttu-id="c8e9e-121">Откройте **Устройства** > **Обслуживание** > **Состояние оборудования** и убедитесь, что светодиодный индикатор для действующего модуля контроллера EBOD имеет зеленый цвет, а для неисправного — красный.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-121">Navigate to **Devices** > **Maintenance** > **Hardware Status**, and verify that the status of the LED for the active EBOD controller module is green and the LED for the failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="c8e9e-122">Найдите неисправный модуль контроллера EBOD на задней стороне устройства.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-122">Locate the failed EBOD controller module at the back of the device.</span></span>
4. <span data-ttu-id="c8e9e-123">Отключите кабели, подключающие модуль контроллера EBOD к контроллеру, затем извлеките модуль EBOD из системы.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-123">Remove the cables that connect the EBOD controller module to the controller before taking the EBOD module out of the system.</span></span>
5. <span data-ttu-id="c8e9e-124">Запишите точный номер порта SAS модуля контроллера EBOD, который был подключен к контроллеру.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-124">Make a note of the exact SAS port of the EBOD controller module that was connected to the controller.</span></span> <span data-ttu-id="c8e9e-125">После замены модуля EBOD система должна вернуться к прежней конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-125">You will be required to restore the system to this configuration after you replace the EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c8e9e-126">Как правило, это порт A, обозначенный как **Входной порт узла** на приведенной ниже схеме.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-126">Typically, this will be Port A, which is labeled as **Host in** in the following diagram.</span></span>
   > 
   > 
   
    ![Задняя панель контроллера EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="c8e9e-128">**Рис. 1.** Задняя поверхность модуля EBOD</span><span class="sxs-lookup"><span data-stu-id="c8e9e-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="c8e9e-129">Метка</span><span class="sxs-lookup"><span data-stu-id="c8e9e-129">Label</span></span> | <span data-ttu-id="c8e9e-130">Описание</span><span class="sxs-lookup"><span data-stu-id="c8e9e-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c8e9e-131">1</span><span class="sxs-lookup"><span data-stu-id="c8e9e-131">1</span></span> |<span data-ttu-id="c8e9e-132">Индикатор сбоя</span><span class="sxs-lookup"><span data-stu-id="c8e9e-132">Fault LED</span></span> |
   | <span data-ttu-id="c8e9e-133">2</span><span class="sxs-lookup"><span data-stu-id="c8e9e-133">2</span></span> |<span data-ttu-id="c8e9e-134">Индикатор питания</span><span class="sxs-lookup"><span data-stu-id="c8e9e-134">Power LED</span></span> |
   | <span data-ttu-id="c8e9e-135">3</span><span class="sxs-lookup"><span data-stu-id="c8e9e-135">3</span></span> |<span data-ttu-id="c8e9e-136">Соединители SAS</span><span class="sxs-lookup"><span data-stu-id="c8e9e-136">SAS connectors</span></span> |
   | <span data-ttu-id="c8e9e-137">4</span><span class="sxs-lookup"><span data-stu-id="c8e9e-137">4</span></span> |<span data-ttu-id="c8e9e-138">Индикаторы SAS</span><span class="sxs-lookup"><span data-stu-id="c8e9e-138">SAS LEDs</span></span> |
   | <span data-ttu-id="c8e9e-139">5</span><span class="sxs-lookup"><span data-stu-id="c8e9e-139">5</span></span> |<span data-ttu-id="c8e9e-140">Последовательные порты только для служебного использования</span><span class="sxs-lookup"><span data-stu-id="c8e9e-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="c8e9e-141">6</span><span class="sxs-lookup"><span data-stu-id="c8e9e-141">6</span></span> |<span data-ttu-id="c8e9e-142">Порт A (Входной порт узла)</span><span class="sxs-lookup"><span data-stu-id="c8e9e-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="c8e9e-143">7</span><span class="sxs-lookup"><span data-stu-id="c8e9e-143">7</span></span> |<span data-ttu-id="c8e9e-144">Порт B (Выходной порт узла)</span><span class="sxs-lookup"><span data-stu-id="c8e9e-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="c8e9e-145">8</span><span class="sxs-lookup"><span data-stu-id="c8e9e-145">8</span></span> |<span data-ttu-id="c8e9e-146">Порт C (только для служебного использования)</span><span class="sxs-lookup"><span data-stu-id="c8e9e-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="c8e9e-147">установить новый контроллер EBOD</span><span class="sxs-lookup"><span data-stu-id="c8e9e-147">Install a new EBOD controller</span></span>
<span data-ttu-id="c8e9e-148">Установка модуля контроллера EBOD для устройства StorSimple описана в следующей процедуре и таблице.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-148">The following procedure and table explain how to install an EBOD controller module in your StorSimple device.</span></span>

#### <a name="to-install-an-ebod-controller"></a><span data-ttu-id="c8e9e-149">Для установки контроллера EBOD</span><span class="sxs-lookup"><span data-stu-id="c8e9e-149">To install an EBOD controller</span></span>
1. <span data-ttu-id="c8e9e-150">Проверьте контроллер EBOD, особенно соединительный разъем на отсутствие повреждений.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-150">Check the EBOD device for damage, especially to the interface connector.</span></span> <span data-ttu-id="c8e9e-151">Если контакты разъема изогнуты, не устанавливайте новый контроллер EBOD.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-151">Do not install the new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="c8e9e-152">С защелками в открытом положении установите модуль в корпус и продвигайте его до срабатывания защелок.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-152">With the latches in the open position, slide the module into the enclosure until the latches engage.</span></span>
   
    ![Установка контроллера EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="c8e9e-154">**Рис. 2.** Установка модуля контроллера EBOD</span><span class="sxs-lookup"><span data-stu-id="c8e9e-154">**Figure 2**  Installing the EBOD controller module</span></span>
3. <span data-ttu-id="c8e9e-155">Закройте защелку.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-155">Close the latch.</span></span> <span data-ttu-id="c8e9e-156">При срабатывании защелки вы должны услышать щелчок.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-156">You should hear a click as the latch engages.</span></span>
   
    ![Освобождение защелки EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="c8e9e-158">**Рис. 3.** Закрытие защелки модуля EBOD</span><span class="sxs-lookup"><span data-stu-id="c8e9e-158">**Figure 3**  Closing the EBOD module latch</span></span>
4. <span data-ttu-id="c8e9e-159">Подключите кабели.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-159">Reconnect the cables.</span></span> <span data-ttu-id="c8e9e-160">Конфигурация должна остаться той же, которая была до замены модуля.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-160">Use the exact configuration that was present before the replacement.</span></span> <span data-ttu-id="c8e9e-161">Подробные сведения о подключении кабелей приведены на следующей схеме и в таблице.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-161">See the following diagram and table for details about how to connect the cables.</span></span>
   
    ![Подключите питание к устройству 4U](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="c8e9e-163">**Рис. 4**.</span><span class="sxs-lookup"><span data-stu-id="c8e9e-163">**Figure 4**.</span></span> <span data-ttu-id="c8e9e-164">Повторное подключение кабелей</span><span class="sxs-lookup"><span data-stu-id="c8e9e-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="c8e9e-165">Метка</span><span class="sxs-lookup"><span data-stu-id="c8e9e-165">Label</span></span> | <span data-ttu-id="c8e9e-166">Описание</span><span class="sxs-lookup"><span data-stu-id="c8e9e-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c8e9e-167">1</span><span class="sxs-lookup"><span data-stu-id="c8e9e-167">1</span></span> |<span data-ttu-id="c8e9e-168">Основной корпус</span><span class="sxs-lookup"><span data-stu-id="c8e9e-168">Primary enclosure</span></span> |
   | <span data-ttu-id="c8e9e-169">2</span><span class="sxs-lookup"><span data-stu-id="c8e9e-169">2</span></span> |<span data-ttu-id="c8e9e-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="c8e9e-170">PCM 0</span></span> |
   | <span data-ttu-id="c8e9e-171">3</span><span class="sxs-lookup"><span data-stu-id="c8e9e-171">3</span></span> |<span data-ttu-id="c8e9e-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="c8e9e-172">PCM 1</span></span> |
   | <span data-ttu-id="c8e9e-173">4</span><span class="sxs-lookup"><span data-stu-id="c8e9e-173">4</span></span> |<span data-ttu-id="c8e9e-174">Контроллер 0</span><span class="sxs-lookup"><span data-stu-id="c8e9e-174">Controller 0</span></span> |
   | <span data-ttu-id="c8e9e-175">5</span><span class="sxs-lookup"><span data-stu-id="c8e9e-175">5</span></span> |<span data-ttu-id="c8e9e-176">Контроллер 1</span><span class="sxs-lookup"><span data-stu-id="c8e9e-176">Controller 1</span></span> |
   | <span data-ttu-id="c8e9e-177">6</span><span class="sxs-lookup"><span data-stu-id="c8e9e-177">6</span></span> |<span data-ttu-id="c8e9e-178">Контроллер EBOD 0</span><span class="sxs-lookup"><span data-stu-id="c8e9e-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="c8e9e-179">7</span><span class="sxs-lookup"><span data-stu-id="c8e9e-179">7</span></span> |<span data-ttu-id="c8e9e-180">Контроллер EBOD 1</span><span class="sxs-lookup"><span data-stu-id="c8e9e-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="c8e9e-181">8</span><span class="sxs-lookup"><span data-stu-id="c8e9e-181">8</span></span> |<span data-ttu-id="c8e9e-182">Корпус EBOD</span><span class="sxs-lookup"><span data-stu-id="c8e9e-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="c8e9e-183">9</span><span class="sxs-lookup"><span data-stu-id="c8e9e-183">9</span></span> |<span data-ttu-id="c8e9e-184">Блоки распределения питания</span><span class="sxs-lookup"><span data-stu-id="c8e9e-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c8e9e-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8e9e-185">Next steps</span></span>
<span data-ttu-id="c8e9e-186">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="c8e9e-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

