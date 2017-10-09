


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="63d10-101">Пометка виртуальной машины с помощью шаблонов</span><span class="sxs-lookup"><span data-stu-id="63d10-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="63d10-102">Для начала рассмотрим пометку с помощью шаблонов.</span><span class="sxs-lookup"><span data-stu-id="63d10-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="63d10-103">[Этот шаблон](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) помещает теги hello следующие ресурсы: вычислительные (виртуальная машина), (учетной записи хранилища) хранилища и сети (общедоступный IP-адрес виртуальной сети и сетевой интерфейс).</span><span class="sxs-lookup"><span data-stu-id="63d10-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on hello following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="63d10-104">(Это шаблон для виртуальной машины Windows, но его можно приспособить для виртуальных машин Linux.)</span><span class="sxs-lookup"><span data-stu-id="63d10-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="63d10-105">Нажмите кнопку hello **развертывание tooAzure** кнопку hello [ссылка на шаблон](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="63d10-105">Click hello **Deploy tooAzure** button from hello [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="63d10-106">Это произойдет переход toohello [портал Azure](https://portal.azure.com/) которого можно развернуть этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="63d10-106">This will navigate toohello [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Простое развертывание с тегами](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="63d10-108">Этот шаблон включает в себя следующие теги hello: *отдел*, *приложения*, и *автор*.</span><span class="sxs-lookup"><span data-stu-id="63d10-108">This template includes hello following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="63d10-109">Вы можно добавить или изменить эти теги непосредственно в шаблоне hello при желании имена другой тег.</span><span class="sxs-lookup"><span data-stu-id="63d10-109">You can add/edit these tags directly in hello template if you would like different tag names.</span></span>

![Теги Azure в шаблоне](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="63d10-111">Как видите, теги hello определяются как пар ключей и значений, разделенных двоеточием (:).</span><span class="sxs-lookup"><span data-stu-id="63d10-111">As you can see, hello tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="63d10-112">Hello теги должны быть определены в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="63d10-112">hello tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="63d10-113">Сохраните файл шаблона hello после завершения изменения его с тегами hello по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="63d10-113">Save hello template file after you finish editing it with hello tags of your choice.</span></span>

<span data-ttu-id="63d10-114">Затем в hello **изменение параметров** раздел, вы сами можете заполнить hello значения тегов.</span><span class="sxs-lookup"><span data-stu-id="63d10-114">Next, in hello **Edit Parameters** section, you can fill out hello values for your tags.</span></span>

![Редактирование тегов на портале Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="63d10-116">Нажмите кнопку **создать** toodeploy этот шаблон нужные значения тега.</span><span class="sxs-lookup"><span data-stu-id="63d10-116">Click **Create** toodeploy this template with your tag values.</span></span>

## <a name="tagging-through-hello-portal"></a><span data-ttu-id="63d10-117">Добавление тегов через портал hello</span><span class="sxs-lookup"><span data-stu-id="63d10-117">Tagging through hello Portal</span></span>
<span data-ttu-id="63d10-118">После создания ресурсов с тегами, можно просматривать, добавлять и удалять теги в портале hello.</span><span class="sxs-lookup"><span data-stu-id="63d10-118">After creating your resources with tags, you can view, add, and delete tags in hello portal.</span></span>

<span data-ttu-id="63d10-119">Выберите hello теги tooview значок тегов:</span><span class="sxs-lookup"><span data-stu-id="63d10-119">Select hello tags icon tooview your tags:</span></span>

![Значок тегов на портале Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="63d10-121">Добавить новый тег через портал hello, определив собственные пара ключ-значение и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="63d10-121">Add a new tag through hello portal by defining your own Key/Value pair, and save it.</span></span>

![Добавление тега на портале Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="63d10-123">Ваш новый тег должен появиться в списке hello тегов для ресурса.</span><span class="sxs-lookup"><span data-stu-id="63d10-123">Your new tag should now appear in hello list of tags for your resource.</span></span>

![Новый тег, сохраненный на портале Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

