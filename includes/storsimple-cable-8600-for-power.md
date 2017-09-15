<!--author=alkohli last changed: 9/16/15-->


#### <a name="to-cable-your-device-for-power"></a><span data-ttu-id="f5760-101">Подключение питания к устройству</span><span class="sxs-lookup"><span data-stu-id="f5760-101">To cable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="f5760-102">Оба корпусах устройстве StorSimple имеют резервные блоки PCM.</span><span class="sxs-lookup"><span data-stu-id="f5760-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="f5760-103">Их необходимо установить и подключить к разным источникам питания, чтобы обеспечить высокий уровень доступности.</span><span class="sxs-lookup"><span data-stu-id="f5760-103">For each enclosure, the PCMs must be installed and connected to different power sources to ensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="f5760-104">Убедитесь, что переключатели питания на всех блоках питания и охлаждения PCM установлены в положение OFF.</span><span class="sxs-lookup"><span data-stu-id="f5760-104">Make sure that the power switches on all the PCMs are in the OFF position.</span></span>
2. <span data-ttu-id="f5760-105">На основном корпусе подключите кабели питания к обоим блокам PCM.</span><span class="sxs-lookup"><span data-stu-id="f5760-105">On the primary enclosure, connect the power cords to both PCMs.</span></span> <span data-ttu-id="f5760-106">На схеме подключения ниже кабели питания обозначены красным цветом.</span><span class="sxs-lookup"><span data-stu-id="f5760-106">The power cords are identified in red in the power cabling diagram, below.</span></span>
3. <span data-ttu-id="f5760-107">Убедитесь, что для двух блоков PCM на основном корпусе используются разные источники питания.</span><span class="sxs-lookup"><span data-stu-id="f5760-107">Make sure that the two PCMs on the primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="f5760-108">Присоедините кабели питания к сети на распределительных блоках стойки, как показано на схеме подключения.</span><span class="sxs-lookup"><span data-stu-id="f5760-108">Attach the power cords to the power on the rack distribution units as shown in the power cabling diagram.</span></span>
5. <span data-ttu-id="f5760-109">Повторите шаги со 2 по 4 для корпуса EBOD.</span><span class="sxs-lookup"><span data-stu-id="f5760-109">Repeat steps 2 through 4 for the EBOD enclosure.</span></span>
6. <span data-ttu-id="f5760-110">Включите питание корпуса EBOD, установив переключатели питания на каждом блоке PCM в положение ON.</span><span class="sxs-lookup"><span data-stu-id="f5760-110">Turn on the EBOD enclosure by flipping the power switch on each PCM to the ON position.</span></span>
7. <span data-ttu-id="f5760-111">Проверьте питание корпуса EBOD: зеленые индикаторы на задней панели контроллера EBOD должны светиться.</span><span class="sxs-lookup"><span data-stu-id="f5760-111">Verify that the EBOD enclosure is turned on by checking that the green LEDs on the back of the EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="f5760-112">Включите питание основного корпуса, установив переключатели каждого блока PCM в положение ON.</span><span class="sxs-lookup"><span data-stu-id="f5760-112">Turn on the primary enclosure by flipping each PCM switch to the ON position.</span></span>
9. <span data-ttu-id="f5760-113">Проверьте питание системы: индикаторы контроллера устройства должны светиться.</span><span class="sxs-lookup"><span data-stu-id="f5760-113">Verify that the system is on by ensuring the device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="f5760-114">Проверьте активность соединения между контроллером EBOD и контроллером устройства: четыре индикатора рядом с портом SAS на контроллере EBOD должны светиться зеленым.</span><span class="sxs-lookup"><span data-stu-id="f5760-114">Make sure that the connection between the EBOD controller and the device controller is active by verifying that the four LEDs next to the SAS port on the EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="f5760-115">Чтобы обеспечить высокий уровень доступности системы, рекомендуем строго придерживаться схемы подключения кабелей питания, показанной на следующей диаграмме.</span><span class="sxs-lookup"><span data-stu-id="f5760-115">To ensure high availability for your system, we recommend that you strictly adhere to the power cabling scheme shown in the following diagram.</span></span>
    > 
    > 
    
    ![Подключите питание к устройству 4U](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="f5760-117">**кабели питания.**</span><span class="sxs-lookup"><span data-stu-id="f5760-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="f5760-118">Метка</span><span class="sxs-lookup"><span data-stu-id="f5760-118">Label</span></span> | <span data-ttu-id="f5760-119">Описание</span><span class="sxs-lookup"><span data-stu-id="f5760-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="f5760-120">1</span><span class="sxs-lookup"><span data-stu-id="f5760-120">1</span></span> |<span data-ttu-id="f5760-121">Основной корпус</span><span class="sxs-lookup"><span data-stu-id="f5760-121">Primary enclosure</span></span> |
    | <span data-ttu-id="f5760-122">2</span><span class="sxs-lookup"><span data-stu-id="f5760-122">2</span></span> |<span data-ttu-id="f5760-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="f5760-123">PCM 0</span></span> |
    | <span data-ttu-id="f5760-124">3</span><span class="sxs-lookup"><span data-stu-id="f5760-124">3</span></span> |<span data-ttu-id="f5760-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="f5760-125">PCM 1</span></span> |
    | <span data-ttu-id="f5760-126">4</span><span class="sxs-lookup"><span data-stu-id="f5760-126">4</span></span> |<span data-ttu-id="f5760-127">Контроллер 0</span><span class="sxs-lookup"><span data-stu-id="f5760-127">Controller 0</span></span> |
    | <span data-ttu-id="f5760-128">5</span><span class="sxs-lookup"><span data-stu-id="f5760-128">5</span></span> |<span data-ttu-id="f5760-129">Контроллер 1</span><span class="sxs-lookup"><span data-stu-id="f5760-129">Controller 1</span></span> |
    | <span data-ttu-id="f5760-130">6</span><span class="sxs-lookup"><span data-stu-id="f5760-130">6</span></span> |<span data-ttu-id="f5760-131">Контроллер EBOD 0</span><span class="sxs-lookup"><span data-stu-id="f5760-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="f5760-132">7</span><span class="sxs-lookup"><span data-stu-id="f5760-132">7</span></span> |<span data-ttu-id="f5760-133">Контроллер EBOD 1</span><span class="sxs-lookup"><span data-stu-id="f5760-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="f5760-134">8</span><span class="sxs-lookup"><span data-stu-id="f5760-134">8</span></span> |<span data-ttu-id="f5760-135">Корпус EBOD</span><span class="sxs-lookup"><span data-stu-id="f5760-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="f5760-136">9</span><span class="sxs-lookup"><span data-stu-id="f5760-136">9</span></span> |<span data-ttu-id="f5760-137">Блоки распределения питания</span><span class="sxs-lookup"><span data-stu-id="f5760-137">PDUs</span></span> |

