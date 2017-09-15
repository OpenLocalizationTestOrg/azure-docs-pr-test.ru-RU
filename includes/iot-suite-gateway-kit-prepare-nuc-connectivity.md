## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="27d75-101">Подготовка Intel NUC</span><span class="sxs-lookup"><span data-stu-id="27d75-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="27d75-102">Чтобы завершить настройку оборудования, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="27d75-102">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="27d75-103">Подключите Intel NUC к источнику питания, входящему в состав набора.</span><span class="sxs-lookup"><span data-stu-id="27d75-103">Connect your Intel NUC to the power supply included in the kit.</span></span>
- <span data-ttu-id="27d75-104">Подключите Intel NUC к сети, используя кабель Ethernet.</span><span class="sxs-lookup"><span data-stu-id="27d75-104">Connect your Intel NUC to your network using an Ethernet cable.</span></span>

<span data-ttu-id="27d75-105">Установка оборудования для устройства шлюза Intel NUC завершена.</span><span class="sxs-lookup"><span data-stu-id="27d75-105">You have now completed the hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="27d75-106">Вход и доступ к терминалу</span><span class="sxs-lookup"><span data-stu-id="27d75-106">Sign in and access the terminal</span></span>

<span data-ttu-id="27d75-107">Существует два варианта получения доступа к среде терминала на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="27d75-107">You have two options to access a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="27d75-108">Если клавиатура и монитор подключены к Intel NUC, вы можете получить доступ к оболочке напрямую.</span><span class="sxs-lookup"><span data-stu-id="27d75-108">If you have a keyboard and monitor connected to your Intel NUC, you can access the shell directly.</span></span> <span data-ttu-id="27d75-109">Как учетные данные по умолчанию используется имя пользователя **root** и пароль **root**.</span><span class="sxs-lookup"><span data-stu-id="27d75-109">The default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="27d75-110">Получите доступ к оболочке на Intel NUC с настольного компьютера через SSH.</span><span class="sxs-lookup"><span data-stu-id="27d75-110">Access the shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="27d75-111">Вход с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="27d75-111">Sign in with SSH</span></span>

<span data-ttu-id="27d75-112">Чтобы выполнить вход с помощью SSH, вам потребуется IP-адрес Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="27d75-112">To sign in with SSH, you need the IP address of your Intel NUC.</span></span> <span data-ttu-id="27d75-113">Если клавиатура и монитор подключены к Intel NUC, выполните команду `ifconfig`, чтобы найти IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="27d75-113">If you have a keyboard and monitor connected to your Intel NUC, use the `ifconfig` command to find the IP address.</span></span> <span data-ttu-id="27d75-114">Вы также можете подключиться к маршрутизатору, чтобы получить список адресов устройств вашей сети.</span><span class="sxs-lookup"><span data-stu-id="27d75-114">Alternatively, connect to your router to list the addresses of devices on your network.</span></span>

<span data-ttu-id="27d75-115">Войдите, используя имя пользователя **root** и пароль **root**.</span><span class="sxs-lookup"><span data-stu-id="27d75-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="27d75-116">Совместный доступ к папке на устройстве Intel NUC (необязательно)</span><span class="sxs-lookup"><span data-stu-id="27d75-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="27d75-117">При необходимости вы можете предоставить общий доступ к папке на устройстве Intel NUC для среды рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="27d75-117">Optionally, you may want to share a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="27d75-118">Предоставив общий доступ к папке, вы сможете использовать предпочитаемый классический текстовый редактор (например, [Visual Studio Code](https://code.visualstudio.com/) или [Sublime Text](http://www.sublimetext.com/)), чтобы редактировать файлы на устройстве Intel NUC вместо использования `nano` или `vi`.</span><span class="sxs-lookup"><span data-stu-id="27d75-118">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="27d75-119">Чтобы предоставить общий доступ к папке в Windows, необходимо настроить сервер Samba на устройстве Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="27d75-119">To share a folder with Windows, configure a Samba server on the Intel NUC.</span></span> <span data-ttu-id="27d75-120">Вы также можете использовать сервер SFTP на Intel NUC с клиентом SFTP на настольном компьютере.</span><span class="sxs-lookup"><span data-stu-id="27d75-120">Alternatively, use the SFTP server on the Intel NUC with an SFTP client on your desktop machine.</span></span>
