## <a name="set-up-the-development-environment"></a><span data-ttu-id="74ec2-101">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="74ec2-101">Set up the development environment</span></span>

<span data-ttu-id="74ec2-102">В этом разделе описаны шаги по настройке среды разработки, включая создание приложения ASP.NET MVC, добавление подключения к подключенным службам, добавление контроллера и указание требуемых директив пространства имен.</span><span class="sxs-lookup"><span data-stu-id="74ec2-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying the required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="74ec2-103">Создание проекта приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="74ec2-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="74ec2-104">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74ec2-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="74ec2-105">В главном меню последовательно выберите **Файл -> Создать -> Проект**.</span><span class="sxs-lookup"><span data-stu-id="74ec2-105">Select **File->New->Project** from the main menu</span></span>

1. <span data-ttu-id="74ec2-106">В диалоговом окне **Создание проекта** задайте параметры, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="74ec2-106">On the **New Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![Создание проекта ASP.NET](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="74ec2-108">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="74ec2-108">Select **OK**.</span></span>

1. <span data-ttu-id="74ec2-109">В диалоговом окне **Новый проект ASP.NET** задайте параметры, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="74ec2-109">On the **New ASP.NET Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![Указание параметров для проекта MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="74ec2-111">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="74ec2-111">Select **OK**.</span></span>

### <a name="use-connected-services-to-connect-to-an-azure-storage-account"></a><span data-ttu-id="74ec2-112">Подключение к учетной записи хранения Azure с помощью подключенных служб</span><span class="sxs-lookup"><span data-stu-id="74ec2-112">Use Connected Services to connect to an Azure storage account</span></span>

1. <span data-ttu-id="74ec2-113">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите в контекстном меню **Добавить > Подключенная служба**.</span><span class="sxs-lookup"><span data-stu-id="74ec2-113">In the **Solution Explorer**, right-click the project, and from the context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="74ec2-114">В диалоговом окне **Добавить подключенную службу** выберите **Хранилище Azure** и нажмите кнопку **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="74ec2-114">On the **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![Диалоговое окно подключенной службы](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="74ec2-116">В диалоговом окне **Хранилище Azure** выберите нужную учетную запись хранения Azure и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="74ec2-116">On the **Azure Storage** dialog, select the desired Azure storage account with which you want to work, and select **Add**.</span></span>
