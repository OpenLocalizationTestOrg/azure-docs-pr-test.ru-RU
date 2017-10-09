<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a><span data-ttu-id="ee6a7-101">tooconnect через последовательную консоль hello</span><span class="sxs-lookup"><span data-stu-id="ee6a7-101">tooconnect through hello serial console</span></span>
1. <span data-ttu-id="ee6a7-102">Подключения последовательный кабель toohello устройства (напрямую или через последовательный USB-адаптер).</span><span class="sxs-lookup"><span data-stu-id="ee6a7-102">Connect your serial cable toohello device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="ee6a7-103">Привет открыть **панели управления**, а затем откройте hello **диспетчер устройств**.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-103">Open hello **Control Panel**, and then open hello **Device Manager**.</span></span>
3. <span data-ttu-id="ee6a7-104">Определите hello COM-порта, как показано в hello после иллюстрации.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-104">Identify hello COM port as shown in hello following illustration.</span></span>
   
     ![Подключение через последовательную консоль](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="ee6a7-106">Запустите PuTTY.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="ee6a7-107">В правой области hello измените hello **тип подключения** слишком**последовательной**.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-107">In hello right pane, change hello **Connection type** too**Serial**.</span></span>
6. <span data-ttu-id="ee6a7-108">В правой области hello введите hello соответствующий COM-порт.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-108">In hello right pane, type hello appropriate COM port.</span></span> <span data-ttu-id="ee6a7-109">Убедитесь, что hello параметры последовательной конфигурации заданы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ee6a7-109">Make sure that hello serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="ee6a7-110">Скорость: 115200.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-110">Speed: 115,200</span></span>
   * <span data-ttu-id="ee6a7-111">Биты данных: 8.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-111">Data bits: 8</span></span>
   * <span data-ttu-id="ee6a7-112">Стоповые биты: 1.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-112">Stop bits: 1</span></span>
   * <span data-ttu-id="ee6a7-113">Четность: нет.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-113">Parity: None</span></span>
   * <span data-ttu-id="ee6a7-114">Управление потоком: нет.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-114">Flow control: None</span></span>
     
     <span data-ttu-id="ee6a7-115">Эти параметры показаны в следующих рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-115">These settings are shown in hello following illustration.</span></span>
     
     ![Параметры PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="ee6a7-117">Если параметр управления потоком по умолчанию hello не работает, попробуйте установить потока управления hello tooXON/XOFF.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-117">If hello default flow control setting does not work, try setting hello flow control tooXON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="ee6a7-118">Нажмите кнопку **откройте** toostart последовательный сеанс.</span><span class="sxs-lookup"><span data-stu-id="ee6a7-118">Click **Open** toostart a serial session.</span></span>

