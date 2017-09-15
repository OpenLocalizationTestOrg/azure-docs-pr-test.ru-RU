


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="d424e-101">Пометка виртуальной машины с помощью шаблонов</span><span class="sxs-lookup"><span data-stu-id="d424e-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="d424e-102">Для начала рассмотрим пометку с помощью шаблонов.</span><span class="sxs-lookup"><span data-stu-id="d424e-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="d424e-103">[Этот шаблон](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) добавляет теги к следующим ресурсам: Compute (виртуальная машина), Storage (учетная запись хранения) и Network (общедоступный IP-адрес, виртуальная сеть и сетевой интерфейс).</span><span class="sxs-lookup"><span data-stu-id="d424e-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on the following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="d424e-104">(Это шаблон для виртуальной машины Windows, но его можно приспособить для виртуальных машин Linux.)</span><span class="sxs-lookup"><span data-stu-id="d424e-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="d424e-105">Нажмите кнопку **Развернуть в Azure** , после того как перейдете по [ссылке на шаблон](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="d424e-105">Click the **Deploy to Azure** button from the [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="d424e-106">Откроется [портал Azure](https://portal.azure.com/) , где можно развернуть этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="d424e-106">This will navigate to the [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Простое развертывание с тегами](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="d424e-108">Этот шаблон включает следующие теги: *Отдел*, *Приложение* и *Создано*.</span><span class="sxs-lookup"><span data-stu-id="d424e-108">This template includes the following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="d424e-109">Вы можете добавлять и редактировать эти теги непосредственно в шаблоне, если вам нужно изменить их имена.</span><span class="sxs-lookup"><span data-stu-id="d424e-109">You can add/edit these tags directly in the template if you would like different tag names.</span></span>

![Теги Azure в шаблоне](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="d424e-111">Как видите, теги определяются как пары "ключ-значение", разделенные двоеточием (:).</span><span class="sxs-lookup"><span data-stu-id="d424e-111">As you can see, the tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="d424e-112">Теги должны быть определены в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="d424e-112">The tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="d424e-113">Завершив добавление нужных тегов в файл шаблона, сохраните его.</span><span class="sxs-lookup"><span data-stu-id="d424e-113">Save the template file after you finish editing it with the tags of your choice.</span></span>

<span data-ttu-id="d424e-114">Затем вы можете указать значения для тегов в разделе **Редактирование параметров** .</span><span class="sxs-lookup"><span data-stu-id="d424e-114">Next, in the **Edit Parameters** section, you can fill out the values for your tags.</span></span>

![Редактирование тегов на портале Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="d424e-116">Нажмите **Создать** , чтобы развернуть шаблон со значениями тегов.</span><span class="sxs-lookup"><span data-stu-id="d424e-116">Click **Create** to deploy this template with your tag values.</span></span>

## <a name="tagging-through-the-portal"></a><span data-ttu-id="d424e-117">Пометка с помощью портала</span><span class="sxs-lookup"><span data-stu-id="d424e-117">Tagging through the Portal</span></span>
<span data-ttu-id="d424e-118">После создания ресурсов с тегами вы можете просматривать, добавлять и удалять теги на портале.</span><span class="sxs-lookup"><span data-stu-id="d424e-118">After creating your resources with tags, you can view, add, and delete tags in the portal.</span></span>

<span data-ttu-id="d424e-119">Выберите значок тегов, чтобы просмотреть свои теги:</span><span class="sxs-lookup"><span data-stu-id="d424e-119">Select the tags icon to view your tags:</span></span>

![Значок тегов на портале Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="d424e-121">Добавьте новый тег с помощью портала, определив собственную пару "ключ-значение", и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="d424e-121">Add a new tag through the portal by defining your own Key/Value pair, and save it.</span></span>

![Добавление тега на портале Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="d424e-123">Новый тег должен появиться в списке тегов для ресурса.</span><span class="sxs-lookup"><span data-stu-id="d424e-123">Your new tag should now appear in the list of tags for your resource.</span></span>

![Новый тег, сохраненный на портале Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

