## <a name="overview"></a><span data-ttu-id="488d8-101">Обзор</span><span class="sxs-lookup"><span data-stu-id="488d8-101">Overview</span></span>

<span data-ttu-id="488d8-102">В этом учебнике необходимо выполнить следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="488d8-102">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="488d8-103">Разверните экземпляр hello удаленного мониторинга предварительно настроенных решений tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="488d8-103">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="488d8-104">На этом шаге автоматически разворачивается и настраивается несколько служб Azure.</span><span class="sxs-lookup"><span data-stu-id="488d8-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="488d8-105">Настройка toocommunicate вашего устройства с компьютера и решение для удаленного мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="488d8-105">Set up your device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="488d8-106">Обновите hello образец кода tooconnect toohello удаленного мониторинга устройствами и отправить смоделированные данные телеметрии, можно просмотреть на панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="488d8-106">Update hello sample device code tooconnect toohello remote monitoring solution, and send simulated telemetry that you can view on hello solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="488d8-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="488d8-107">Prerequisites</span></span>

<span data-ttu-id="488d8-108">toocomplete этого учебника требуется Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="488d8-108">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="488d8-109">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="488d8-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="488d8-110">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="488d8-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="488d8-111">Необходимое программное обеспечение</span><span class="sxs-lookup"><span data-stu-id="488d8-111">Required software</span></span>

<span data-ttu-id="488d8-112">Требуется клиент SSH на tooenable на настольном компьютере, вы tooremotely доступ hello командную строку на hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="488d8-112">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="488d8-113">Windows не предоставляет клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="488d8-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="488d8-114">Мы советуем использовать [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="488d8-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="488d8-115">Большинство дистрибутивах Linux и Mac OS включают программу командной строки SSH hello.</span><span class="sxs-lookup"><span data-stu-id="488d8-115">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="488d8-116">Дополнительные сведения см. в статье [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (Подключение по протоколу SSH с помощью Linux или Mac OS).</span><span class="sxs-lookup"><span data-stu-id="488d8-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="488d8-117">Необходимое оборудование</span><span class="sxs-lookup"><span data-stu-id="488d8-117">Required hardware</span></span>

<span data-ttu-id="488d8-118">Tooenable настольного компьютера вы tooconnect удаленно toohello командную строку на hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="488d8-118">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="488d8-119">[Начальный набор Microsoft IoT для Raspberry Pi 3][lnk-starter-kits] или эквивалентные компоненты.</span><span class="sxs-lookup"><span data-stu-id="488d8-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="488d8-120">В этом учебнике используется hello следующих элементов на основе набора hello:</span><span class="sxs-lookup"><span data-stu-id="488d8-120">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="488d8-121">Raspberry Pi 3;</span><span class="sxs-lookup"><span data-stu-id="488d8-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="488d8-122">карта MicroSD (с NOOBS);</span><span class="sxs-lookup"><span data-stu-id="488d8-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="488d8-123">кабель MiniUSB;</span><span class="sxs-lookup"><span data-stu-id="488d8-123">A USB Mini cable</span></span>
- <span data-ttu-id="488d8-124">кабель Ethernet.</span><span class="sxs-lookup"><span data-stu-id="488d8-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/