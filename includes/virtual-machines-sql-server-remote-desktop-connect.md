1. <span data-ttu-id="e6974-101">После создания и запуска виртуальной машины Azure щелкните значок "Виртуальные машины" на портале Azure для просмотра виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e6974-101">After the Azure virtual machine is created and running, click the Virtual Machines icon in the Azure portal to view your VMs.</span></span>

1. <span data-ttu-id="e6974-102">Нажмите кнопку с многоточием **…** для новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e6974-102">Click the ellipsis, **...**, for your new VM.</span></span>

1. <span data-ttu-id="e6974-103">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="e6974-103">Click **Connect**.</span></span>

   ![Подключение к виртуальной машине на портале](./media/virtual-machines-sql-server-remote-desktop-connect/azure-virtual-machine-connect.png)

1. <span data-ttu-id="e6974-105">Откройте **RDP**-файл, скачанный для виртуальной машины через браузер.</span><span class="sxs-lookup"><span data-stu-id="e6974-105">Open the **RDP** file that your browser downloads for the VM.</span></span>

1. <span data-ttu-id="e6974-106">В ходе подключения к удаленному рабочему столу может появиться предупреждение о том, что издателя этого удаленного подключения невозможно определить.</span><span class="sxs-lookup"><span data-stu-id="e6974-106">The Remote Desktop Connection notifies you that the publisher of this remote connection cannot be identified.</span></span> <span data-ttu-id="e6974-107">Чтобы продолжить, щелкните **Подключить** .</span><span class="sxs-lookup"><span data-stu-id="e6974-107">Click **Connect** to continue.</span></span>

1. <span data-ttu-id="e6974-108">В диалоговом окне **Безопасность Windows** выберите **Использовать другую учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="e6974-108">In the **Windows Security** dialog, click **Use a different account**.</span></span> <span data-ttu-id="e6974-109">Для отображения этой команды может потребоваться щелкнуть элемент **Больше вариантов**.</span><span class="sxs-lookup"><span data-stu-id="e6974-109">You might have to click **More choices** to see this.</span></span> <span data-ttu-id="e6974-110">Укажите имя пользователя и пароль, которые были настроены при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e6974-110">Specify the user name and password that you configured when you created the VM.</span></span> <span data-ttu-id="e6974-111">Перед именем пользователя необходимо добавить обратную косую черту.</span><span class="sxs-lookup"><span data-stu-id="e6974-111">You must add a backslash before the user name.</span></span>

   ![Проверка подлинности при подключении к удаленному рабочему столу](./media/virtual-machines-sql-server-remote-desktop-connect/remote-desktop-connect.png)

1. <span data-ttu-id="e6974-113">Нажмите кнопку **ОК** для подключения.</span><span class="sxs-lookup"><span data-stu-id="e6974-113">Click **OK** to connect.</span></span>