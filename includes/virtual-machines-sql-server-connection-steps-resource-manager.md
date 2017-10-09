### <a name="configure-a-dns-label-for-hello-public-ip-address"></a><span data-ttu-id="e49e0-101">Настроить метку для hello общедоступный IP-адрес DNS</span><span class="sxs-lookup"><span data-stu-id="e49e0-101">Configure a DNS Label for hello public IP address</span></span>

<span data-ttu-id="e49e0-102">toohello tooconnect SQL Server Database Engine из Интернета, hello рекомендуется создать метку DNS вашего общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="e49e0-102">tooconnect toohello SQL Server Database Engine from hello Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="e49e0-103">Можно подключиться по IP-адресу, но hello метка DNS создает записи, проще tooidentify и краткие описания hello базовой общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e49e0-103">You can connect by IP address, but hello DNS Label creates an A Record that is easier tooidentify and abstracts hello underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="e49e0-104">Метки DNS не требуются, если экземпляр плана tooonly подключения toohello SQL Server в рамках hello же виртуальной сети или только на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="e49e0-104">DNS Labels are not required if you plan tooonly connect toohello SQL Server instance within hello same Virtual Network or only locally.</span></span>

<span data-ttu-id="e49e0-105">toocreate метка DNS, сначала выберите **виртуальные машины** hello портала.</span><span class="sxs-lookup"><span data-stu-id="e49e0-105">toocreate a DNS Label, first select **Virtual machines** in hello portal.</span></span> <span data-ttu-id="e49e0-106">Установите на виртуальной Машине SQL Server toobring свойств.</span><span class="sxs-lookup"><span data-stu-id="e49e0-106">Select your SQL Server VM toobring up its properties.</span></span>

1. <span data-ttu-id="e49e0-107">В обзоре hello виртуальной машины, выберите ваш **общедоступный IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-107">In hello virtual machine overview, select your **Public IP address**.</span></span>

    ![общедоступный IP-адрес](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="e49e0-109">В свойствах hello на общедоступный IP-адрес, разверните **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-109">In hello properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="e49e0-110">Введите имя DNS.</span><span class="sxs-lookup"><span data-stu-id="e49e0-110">Enter a DNS Label name.</span></span> <span data-ttu-id="e49e0-111">Это имя является запись A, которая может быть напрямую используется tooconnect tooyour виртуальной Машине SQL Server по имени, а не по IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="e49e0-111">This name is an A Record that can be used tooconnect tooyour SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="e49e0-112">Нажмите кнопку hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e49e0-112">Click hello **Save** button.</span></span>

    ![имя DNS](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a><span data-ttu-id="e49e0-114">Подключения toohello компонент Database Engine с другого компьютера</span><span class="sxs-lookup"><span data-stu-id="e49e0-114">Connect toohello Database Engine from another computer</span></span>

1. <span data-ttu-id="e49e0-115">На компьютере подключен toohello Интернета, откройте SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="e49e0-115">On a computer connected toohello internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="e49e0-116">Если у вас нет SQL Server Management Studio, его можно скачать [здесь](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="e49e0-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="e49e0-117">В hello **подключения tooServer** или **подключения tooDatabase ядра** диалоговое окно, редактирование hello **имя сервера** значение.</span><span class="sxs-lookup"><span data-stu-id="e49e0-117">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, edit hello **Server name** value.</span></span> <span data-ttu-id="e49e0-118">Введите hello IP-адрес или полное DNS-имя виртуальной машины hello (определенный в предыдущей задаче hello).</span><span class="sxs-lookup"><span data-stu-id="e49e0-118">Enter hello IP address or full DNS name of hello virtual machine (determined in hello previous task).</span></span> <span data-ttu-id="e49e0-119">Кроме того, можно также после запятой указать TCP-порт SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e49e0-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="e49e0-120">Например, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="e49e0-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="e49e0-121">В hello **проверки подлинности** выберите **проверки подлинности SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-121">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="e49e0-122">В hello **входа** введите hello имя входа SQL.</span><span class="sxs-lookup"><span data-stu-id="e49e0-122">In hello **Login** box, type hello name of a valid SQL login.</span></span>

1. <span data-ttu-id="e49e0-123">В hello **пароль** поле, тип hello пароль входа hello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-123">In hello **Password** box, type hello password of hello login.</span></span>

1. <span data-ttu-id="e49e0-124">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-124">Click **Connect**.</span></span>

    ![подключение SSMS](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)