---
title: "контроллер StorSimple 8600 EBOD aaaReplace | Документы Microsoft"
description: "Объясняет, как tooremove и заменить один или оба контроллера EBOD на устройстве StorSimple 8600."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 8343ed6f48ae97fc9204452f85e1936bfb1d6919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="fdecc-103">Замена контроллера EBOD на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="fdecc-103">Replace an EBOD controller on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="fdecc-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="fdecc-104">Overview</span></span>
<span data-ttu-id="fdecc-105">В этом учебнике описано как tooreplace неисправный модуль контроллера EBOD на устройстве Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="fdecc-105">This tutorial explains how tooreplace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="fdecc-106">tooreplace модуль контроллера EBOD, необходимо:</span><span class="sxs-lookup"><span data-stu-id="fdecc-106">tooreplace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="fdecc-107">Удалить неисправный контроллер EBOD hello</span><span class="sxs-lookup"><span data-stu-id="fdecc-107">Remove hello faulty EBOD controller</span></span>
* <span data-ttu-id="fdecc-108">установить новый контроллер EBOD</span><span class="sxs-lookup"><span data-stu-id="fdecc-108">Install a new EBOD controller</span></span>

<span data-ttu-id="fdecc-109">Рассмотрим следующую информацию, прежде чем начать hello.</span><span class="sxs-lookup"><span data-stu-id="fdecc-109">Consider hello following information before you begin:</span></span>

* <span data-ttu-id="fdecc-110">Во все неиспользуемые отсеки должны быть установлены пустые модули EBOD.</span><span class="sxs-lookup"><span data-stu-id="fdecc-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="fdecc-111">Hello охлаждение корпуса не будет правильно Если слот остается открытым.</span><span class="sxs-lookup"><span data-stu-id="fdecc-111">hello enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="fdecc-112">с поддержкой горячей замены контроллера EBOD Hello и могут удаляться или заменяться.</span><span class="sxs-lookup"><span data-stu-id="fdecc-112">hello EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="fdecc-113">Не снимайте неисправный модуль, если у вас нет модуля на замену.</span><span class="sxs-lookup"><span data-stu-id="fdecc-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="fdecc-114">При запуске процесса hello замены необходимо завершить в течение 10 минут.</span><span class="sxs-lookup"><span data-stu-id="fdecc-114">When you initiate hello replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdecc-115">Прежде чем tooremove или заменить любой компонент StorSimple, обязательно изучите hello [условные обозначения значков безопасности](storsimple-safety.md#safety-icon-conventions) и других [меры предосторожности](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="fdecc-115">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="fdecc-116">Снятие контроллера EBOD</span><span class="sxs-lookup"><span data-stu-id="fdecc-116">Remove an EBOD controller</span></span>
<span data-ttu-id="fdecc-117">Перед замена hello сбой модуля контроллера EBOD в вашем устройстве StorSimple, убедитесь, что hello другой модуль контроллера EBOD включен и запущен.</span><span class="sxs-lookup"><span data-stu-id="fdecc-117">Before replacing hello failed EBOD controller module in your StorSimple device, make sure that hello other EBOD controller module is active and running.</span></span> <span data-ttu-id="fdecc-118">Hello следующей процедуре и таблице объясняется, как tooremove hello модуль контроллера EBOD.</span><span class="sxs-lookup"><span data-stu-id="fdecc-118">hello following procedure and table explain how tooremove hello EBOD controller module.</span></span>

#### <a name="tooremove-an-ebod-module"></a><span data-ttu-id="fdecc-119">tooremove модуля EBOD</span><span class="sxs-lookup"><span data-stu-id="fdecc-119">tooremove an EBOD module</span></span>
1. <span data-ttu-id="fdecc-120">Здравствуйте, откройте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fdecc-120">Open hello Azure portal.</span></span>
2. <span data-ttu-id="fdecc-121">Go tooyour устройства и перейдите слишком**параметры** > **работоспособности оборудования**и проверьте состояние hello hello Индикатор для hello действующего модуля контроллера EBOD — зеленый и hello Индикатор для hello не удалось Модуль контроллера EBOD — красным.</span><span class="sxs-lookup"><span data-stu-id="fdecc-121">Go tooyour device and navigate too**Settings** > **Hardware health**, and verify that hello status of hello LED for hello active EBOD controller module is green and hello LED for hello failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="fdecc-122">Найдите модуль контроллера EBOD сбой hello в hello задняя сторона устройства hello.</span><span class="sxs-lookup"><span data-stu-id="fdecc-122">Locate hello failed EBOD controller module at hello back of hello device.</span></span>
4. <span data-ttu-id="fdecc-123">Отсоедините кабели hello, подключения контроллера toohello модуль контроллера EBOD hello перед извлечением модуля EBOD hello из системы hello.</span><span class="sxs-lookup"><span data-stu-id="fdecc-123">Remove hello cables that connect hello EBOD controller module toohello controller before taking hello EBOD module out of hello system.</span></span>
5. <span data-ttu-id="fdecc-124">Запишите hello точный номер порта SAS модуля контроллера EBOD hello, подключенных toohello контроллера.</span><span class="sxs-lookup"><span data-stu-id="fdecc-124">Make a note of hello exact SAS port of hello EBOD controller module that was connected toohello controller.</span></span> <span data-ttu-id="fdecc-125">Конфигурация toothis необходимые toorestore hello системы будет после замены модуля EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="fdecc-125">You will be required toorestore hello system toothis configuration after you replace hello EBOD module.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fdecc-126">Как правило, это будет порт A, который обозначается как **размещения в** в hello следующие схемы.</span><span class="sxs-lookup"><span data-stu-id="fdecc-126">Typically, this will be Port A, which is labeled as **Host in** in hello following diagram.</span></span>
   
    ![Задняя панель контроллера EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="fdecc-128">**Рис. 1.** Задняя поверхность модуля EBOD</span><span class="sxs-lookup"><span data-stu-id="fdecc-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="fdecc-129">Метка</span><span class="sxs-lookup"><span data-stu-id="fdecc-129">Label</span></span> | <span data-ttu-id="fdecc-130">Описание</span><span class="sxs-lookup"><span data-stu-id="fdecc-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="fdecc-131">1</span><span class="sxs-lookup"><span data-stu-id="fdecc-131">1</span></span> |<span data-ttu-id="fdecc-132">Индикатор сбоя</span><span class="sxs-lookup"><span data-stu-id="fdecc-132">Fault LED</span></span> |
   | <span data-ttu-id="fdecc-133">2</span><span class="sxs-lookup"><span data-stu-id="fdecc-133">2</span></span> |<span data-ttu-id="fdecc-134">Индикатор питания</span><span class="sxs-lookup"><span data-stu-id="fdecc-134">Power LED</span></span> |
   | <span data-ttu-id="fdecc-135">3</span><span class="sxs-lookup"><span data-stu-id="fdecc-135">3</span></span> |<span data-ttu-id="fdecc-136">Соединители SAS</span><span class="sxs-lookup"><span data-stu-id="fdecc-136">SAS connectors</span></span> |
   | <span data-ttu-id="fdecc-137">4</span><span class="sxs-lookup"><span data-stu-id="fdecc-137">4</span></span> |<span data-ttu-id="fdecc-138">Индикаторы SAS</span><span class="sxs-lookup"><span data-stu-id="fdecc-138">SAS LEDs</span></span> |
   | <span data-ttu-id="fdecc-139">5</span><span class="sxs-lookup"><span data-stu-id="fdecc-139">5</span></span> |<span data-ttu-id="fdecc-140">Последовательные порты только для служебного использования</span><span class="sxs-lookup"><span data-stu-id="fdecc-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="fdecc-141">6</span><span class="sxs-lookup"><span data-stu-id="fdecc-141">6</span></span> |<span data-ttu-id="fdecc-142">Порт A (Входной порт узла)</span><span class="sxs-lookup"><span data-stu-id="fdecc-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="fdecc-143">7</span><span class="sxs-lookup"><span data-stu-id="fdecc-143">7</span></span> |<span data-ttu-id="fdecc-144">Порт B (Выходной порт узла)</span><span class="sxs-lookup"><span data-stu-id="fdecc-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="fdecc-145">8</span><span class="sxs-lookup"><span data-stu-id="fdecc-145">8</span></span> |<span data-ttu-id="fdecc-146">Порт C (только для служебного использования)</span><span class="sxs-lookup"><span data-stu-id="fdecc-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="fdecc-147">установить новый контроллер EBOD</span><span class="sxs-lookup"><span data-stu-id="fdecc-147">Install a new EBOD controller</span></span>
<span data-ttu-id="fdecc-148">Hello следующей процедуре и таблице поясняется, как tooinstall модуль контроллера EBOD в вашем устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="fdecc-148">hello following procedure and table explain how tooinstall an EBOD controller module in your StorSimple device.</span></span>

#### <a name="tooinstall-an-ebod-controller"></a><span data-ttu-id="fdecc-149">tooinstall контроллера EBOD</span><span class="sxs-lookup"><span data-stu-id="fdecc-149">tooinstall an EBOD controller</span></span>
1. <span data-ttu-id="fdecc-150">Проверьте устройство EBOD hello наличие повреждений, особенно toohello разъем для подключения.</span><span class="sxs-lookup"><span data-stu-id="fdecc-150">Check hello EBOD device for damage, especially toohello interface connector.</span></span> <span data-ttu-id="fdecc-151">Если какие-либо выводы погнуты, не устанавливайте hello нового контроллера EBOD.</span><span class="sxs-lookup"><span data-stu-id="fdecc-151">Do not install hello new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="fdecc-152">Откройте позиции модуля hello слайд в корпус hello пока hello защелки hello кратковременных блокировок в hello.</span><span class="sxs-lookup"><span data-stu-id="fdecc-152">With hello latches in hello open position, slide hello module into hello enclosure until hello latches engage.</span></span>
   
    ![Установка контроллера EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="fdecc-154">**На рисунке 2** модуль контроллера EBOD Установка hello</span><span class="sxs-lookup"><span data-stu-id="fdecc-154">**Figure 2**  Installing hello EBOD controller module</span></span>
3. <span data-ttu-id="fdecc-155">Закрыть hello кратковременной блокировки.</span><span class="sxs-lookup"><span data-stu-id="fdecc-155">Close hello latch.</span></span> <span data-ttu-id="fdecc-156">При фиксации защелки hello должны услышать щелчок.</span><span class="sxs-lookup"><span data-stu-id="fdecc-156">You should hear a click as hello latch engages.</span></span>
   
    ![Освобождение защелки EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="fdecc-158">**Рис. 3** закрытие защелки модуля EBOD hello</span><span class="sxs-lookup"><span data-stu-id="fdecc-158">**Figure 3**  Closing hello EBOD module latch</span></span>
4. <span data-ttu-id="fdecc-159">Подключите кабели hello.</span><span class="sxs-lookup"><span data-stu-id="fdecc-159">Reconnect hello cables.</span></span> <span data-ttu-id="fdecc-160">Используйте hello точной конфигурации, который существовал до замены hello.</span><span class="sxs-lookup"><span data-stu-id="fdecc-160">Use hello exact configuration that was present before hello replacement.</span></span> <span data-ttu-id="fdecc-161">Просмотреть hello, следующая диаграмма и таблица, Дополнительные сведения о том, как tooconnect hello кабели.</span><span class="sxs-lookup"><span data-stu-id="fdecc-161">See hello following diagram and table for details about how tooconnect hello cables.</span></span>
   
    ![Подключите питание к устройству 4U](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="fdecc-163">**Рис. 4**.</span><span class="sxs-lookup"><span data-stu-id="fdecc-163">**Figure 4**.</span></span> <span data-ttu-id="fdecc-164">Повторное подключение кабелей</span><span class="sxs-lookup"><span data-stu-id="fdecc-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="fdecc-165">Метка</span><span class="sxs-lookup"><span data-stu-id="fdecc-165">Label</span></span> | <span data-ttu-id="fdecc-166">Описание</span><span class="sxs-lookup"><span data-stu-id="fdecc-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="fdecc-167">1</span><span class="sxs-lookup"><span data-stu-id="fdecc-167">1</span></span> |<span data-ttu-id="fdecc-168">Основной корпус</span><span class="sxs-lookup"><span data-stu-id="fdecc-168">Primary enclosure</span></span> |
   | <span data-ttu-id="fdecc-169">2</span><span class="sxs-lookup"><span data-stu-id="fdecc-169">2</span></span> |<span data-ttu-id="fdecc-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="fdecc-170">PCM 0</span></span> |
   | <span data-ttu-id="fdecc-171">3</span><span class="sxs-lookup"><span data-stu-id="fdecc-171">3</span></span> |<span data-ttu-id="fdecc-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="fdecc-172">PCM 1</span></span> |
   | <span data-ttu-id="fdecc-173">4</span><span class="sxs-lookup"><span data-stu-id="fdecc-173">4</span></span> |<span data-ttu-id="fdecc-174">Контроллер 0</span><span class="sxs-lookup"><span data-stu-id="fdecc-174">Controller 0</span></span> |
   | <span data-ttu-id="fdecc-175">5</span><span class="sxs-lookup"><span data-stu-id="fdecc-175">5</span></span> |<span data-ttu-id="fdecc-176">Контроллер 1</span><span class="sxs-lookup"><span data-stu-id="fdecc-176">Controller 1</span></span> |
   | <span data-ttu-id="fdecc-177">6</span><span class="sxs-lookup"><span data-stu-id="fdecc-177">6</span></span> |<span data-ttu-id="fdecc-178">Контроллер EBOD 0</span><span class="sxs-lookup"><span data-stu-id="fdecc-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="fdecc-179">7</span><span class="sxs-lookup"><span data-stu-id="fdecc-179">7</span></span> |<span data-ttu-id="fdecc-180">Контроллер EBOD 1</span><span class="sxs-lookup"><span data-stu-id="fdecc-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="fdecc-181">8</span><span class="sxs-lookup"><span data-stu-id="fdecc-181">8</span></span> |<span data-ttu-id="fdecc-182">Корпус EBOD</span><span class="sxs-lookup"><span data-stu-id="fdecc-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="fdecc-183">9</span><span class="sxs-lookup"><span data-stu-id="fdecc-183">9</span></span> |<span data-ttu-id="fdecc-184">Блоки распределения питания</span><span class="sxs-lookup"><span data-stu-id="fdecc-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fdecc-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fdecc-185">Next steps</span></span>
<span data-ttu-id="fdecc-186">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="fdecc-186">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

