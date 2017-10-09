## <a name="set-up-hello-development-environment"></a><span data-ttu-id="435d0-101">Настройка среды разработки hello</span><span class="sxs-lookup"><span data-stu-id="435d0-101">Set up hello development environment</span></span>

<span data-ttu-id="435d0-102">В этом подразделе содержатся Настройка среды разработки, включая создание приложения ASP.NET MVC, Добавление подключения подключенные службы, добавление контроллера, и указав hello необходимые директивы пространства имен.</span><span class="sxs-lookup"><span data-stu-id="435d0-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying hello required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="435d0-103">Создание проекта приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="435d0-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="435d0-104">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="435d0-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="435d0-105">Выберите **файл -> Создать -> проект** hello в главном меню</span><span class="sxs-lookup"><span data-stu-id="435d0-105">Select **File->New->Project** from hello main menu</span></span>

1. <span data-ttu-id="435d0-106">На hello **новый проект** диалогового окна, укажите параметры hello, как видно из hello следующий рисунок:</span><span class="sxs-lookup"><span data-stu-id="435d0-106">On hello **New Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![Создание проекта ASP.NET](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="435d0-108">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="435d0-108">Select **OK**.</span></span>

1. <span data-ttu-id="435d0-109">На hello **новый проект ASP.NET** диалогового окна, укажите параметры hello, как видно из hello следующий рисунок:</span><span class="sxs-lookup"><span data-stu-id="435d0-109">On hello **New ASP.NET Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![Указание параметров для проекта MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="435d0-111">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="435d0-111">Select **OK**.</span></span>

### <a name="use-connected-services-tooconnect-tooan-azure-storage-account"></a><span data-ttu-id="435d0-112">Использовать учетную запись хранилища Azure tooan tooconnect подключенные службы</span><span class="sxs-lookup"><span data-stu-id="435d0-112">Use Connected Services tooconnect tooan Azure storage account</span></span>

1. <span data-ttu-id="435d0-113">В hello **обозревателе решений**, щелкните правой кнопкой мыши проект hello и hello контекстном меню, выберите **Добавить -> подключенная служба**.</span><span class="sxs-lookup"><span data-stu-id="435d0-113">In hello **Solution Explorer**, right-click hello project, and from hello context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="435d0-114">На hello **добавление подключенной службы** диалогового окна выберите **хранилища Azure**, а затем выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="435d0-114">On hello **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![Диалоговое окно подключенной службы](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="435d0-116">На hello **хранилища Azure** диалогового окна выберите hello требуемой учетную запись хранения Azure с помощью которого toowork и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="435d0-116">On hello **Azure Storage** dialog, select hello desired Azure storage account with which you want toowork, and select **Add**.</span></span>
