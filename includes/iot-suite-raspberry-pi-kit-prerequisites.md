## <a name="prerequisites"></a><span data-ttu-id="d31be-101">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d31be-101">Prerequisites</span></span>

<span data-ttu-id="d31be-102">toocomplete этого учебника требуется Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="d31be-102">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d31be-103">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d31be-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d31be-104">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="d31be-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="d31be-105">Необходимое программное обеспечение</span><span class="sxs-lookup"><span data-stu-id="d31be-105">Required software</span></span>

<span data-ttu-id="d31be-106">Требуется клиент SSH на tooenable на настольном компьютере, вы tooremotely доступ hello командную строку на hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d31be-106">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="d31be-107">Windows не предоставляет клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="d31be-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="d31be-108">Мы советуем использовать [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="d31be-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="d31be-109">Большинство дистрибутивах Linux и Mac OS включают программу командной строки SSH hello.</span><span class="sxs-lookup"><span data-stu-id="d31be-109">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="d31be-110">Дополнительные сведения см. в статье [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (Подключение по протоколу SSH с помощью Linux или Mac OS).</span><span class="sxs-lookup"><span data-stu-id="d31be-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="d31be-111">Необходимое оборудование</span><span class="sxs-lookup"><span data-stu-id="d31be-111">Required hardware</span></span>

<span data-ttu-id="d31be-112">Tooenable настольного компьютера вы tooconnect удаленно toohello командную строку на hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d31be-112">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="d31be-113">[Начальный набор Microsoft IoT для Raspberry Pi 3][lnk-starter-kits] или эквивалентные компоненты.</span><span class="sxs-lookup"><span data-stu-id="d31be-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="d31be-114">В этом учебнике используется hello следующих элементов на основе набора hello:</span><span class="sxs-lookup"><span data-stu-id="d31be-114">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="d31be-115">Raspberry Pi 3;</span><span class="sxs-lookup"><span data-stu-id="d31be-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="d31be-116">карта MicroSD (с NOOBS);</span><span class="sxs-lookup"><span data-stu-id="d31be-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="d31be-117">кабель MiniUSB;</span><span class="sxs-lookup"><span data-stu-id="d31be-117">A USB Mini cable</span></span>
- <span data-ttu-id="d31be-118">кабель Ethernet;</span><span class="sxs-lookup"><span data-stu-id="d31be-118">An Ethernet cable</span></span>
- <span data-ttu-id="d31be-119">датчик BME280;</span><span class="sxs-lookup"><span data-stu-id="d31be-119">BME280 sensor</span></span>
- <span data-ttu-id="d31be-120">монтажная плата;</span><span class="sxs-lookup"><span data-stu-id="d31be-120">Breadboard</span></span>
- <span data-ttu-id="d31be-121">оптоволоконные кабеля с разъемами на обоих концах;</span><span class="sxs-lookup"><span data-stu-id="d31be-121">Jumper wires</span></span>
- <span data-ttu-id="d31be-122">резисторы;</span><span class="sxs-lookup"><span data-stu-id="d31be-122">Resistors</span></span>
- <span data-ttu-id="d31be-123">светодиодные индикаторы.</span><span class="sxs-lookup"><span data-stu-id="d31be-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/