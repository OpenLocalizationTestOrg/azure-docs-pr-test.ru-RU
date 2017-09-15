### <a name="configure-a-dns-label-for-the-public-ip-address"></a><span data-ttu-id="8fb95-101">Настройка имени DNS для общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="8fb95-101">Configure a DNS Label for the public IP address</span></span>

<span data-ttu-id="8fb95-102">Для подключения к СУБД SQL Server через Интернет рекомендуем создать имя DNS для вашего общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="8fb95-102">To connect to the SQL Server Database Engine from the Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="8fb95-103">Вы можете подключиться по IP-адресу, но метка DNS создает запись А, которую легче идентифицировать, и абстрагирует базовый общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="8fb95-103">You can connect by IP address, but the DNS Label creates an A Record that is easier to identify and abstracts the underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="8fb95-104">DNS-метки не обязательны, если вы подключаетесь к экземпляру SQL Server в той же виртуальной сети или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="8fb95-104">DNS Labels are not required if you plan to only connect to the SQL Server instance within the same Virtual Network or only locally.</span></span>

<span data-ttu-id="8fb95-105">Чтобы создать DNS-метку, сначала выберите **Виртуальные машины** на портале.</span><span class="sxs-lookup"><span data-stu-id="8fb95-105">To create a DNS Label, first select **Virtual machines** in the portal.</span></span> <span data-ttu-id="8fb95-106">Выберите виртуальную машину SQL Server, чтобы открыть ее свойства.</span><span class="sxs-lookup"><span data-stu-id="8fb95-106">Select your SQL Server VM to bring up its properties.</span></span>

1. <span data-ttu-id="8fb95-107">В обозревателе виртуальной машины выберите **общедоступный IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="8fb95-107">In the virtual machine overview, select your **Public IP address**.</span></span>

    ![общедоступный IP-адрес](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="8fb95-109">В свойствах общедоступного IP-адреса разверните раздел **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="8fb95-109">In the properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="8fb95-110">Введите имя DNS.</span><span class="sxs-lookup"><span data-stu-id="8fb95-110">Enter a DNS Label name.</span></span> <span data-ttu-id="8fb95-111">Это имя, которое можно использовать для подключения к виртуальной машине SQL Server по имени, а не по IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="8fb95-111">This name is an A Record that can be used to connect to your SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="8fb95-112">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8fb95-112">Click the **Save** button.</span></span>

    ![имя DNS](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-to-the-database-engine-from-another-computer"></a><span data-ttu-id="8fb95-114">Подключение к ядру СУБД с другого компьютера</span><span class="sxs-lookup"><span data-stu-id="8fb95-114">Connect to the Database Engine from another computer</span></span>

1. <span data-ttu-id="8fb95-115">На компьютере, подключенном к сети Интернет, откройте SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="8fb95-115">On a computer connected to the internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="8fb95-116">Если у вас нет SQL Server Management Studio, его можно скачать [здесь](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="8fb95-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="8fb95-117">В диалоговом окне **Подключение к серверу** или **Подключение к ядру СУБД** измените значение **Имя сервера**.</span><span class="sxs-lookup"><span data-stu-id="8fb95-117">In the **Connect to Server** or **Connect to Database Engine** dialog box, edit the **Server name** value.</span></span> <span data-ttu-id="8fb95-118">Введите IP-адрес или полное DNS-имя виртуальной машины (определено в предыдущей задаче).</span><span class="sxs-lookup"><span data-stu-id="8fb95-118">Enter the IP address or full DNS name of the virtual machine (determined in the previous task).</span></span> <span data-ttu-id="8fb95-119">Кроме того, можно также после запятой указать TCP-порт SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8fb95-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="8fb95-120">Например, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="8fb95-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="8fb95-121">В поле **Проверка подлинности** выберите **Проверка подлинности SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="8fb95-121">In the **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="8fb95-122">В поле **Имя пользователя** введите допустимое имя пользователя SQL.</span><span class="sxs-lookup"><span data-stu-id="8fb95-122">In the **Login** box, type the name of a valid SQL login.</span></span>

1. <span data-ttu-id="8fb95-123">В поле **Пароль** введите пароль для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="8fb95-123">In the **Password** box, type the password of the login.</span></span>

1. <span data-ttu-id="8fb95-124">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="8fb95-124">Click **Connect**.</span></span>

    ![подключение SSMS](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)