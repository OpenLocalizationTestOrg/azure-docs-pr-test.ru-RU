## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="d1380-101">Добавочные и полные развертывания</span><span class="sxs-lookup"><span data-stu-id="d1380-101">Incremental and complete deployments</span></span>
<span data-ttu-id="d1380-102">При развертывании имеющихся ресурсов можно указать, что развертывание является добавочным или полным обновлением.</span><span class="sxs-lookup"><span data-stu-id="d1380-102">When deploying your resources, you specify that the deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="d1380-103">Основное различие между этими двумя режимами заключается в том, как Resource Manager обрабатывает имеющиеся ресурсы в группе ресурсов, которых нет в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="d1380-103">The primary difference between these two modes is how Resource Manager handles existing resources in the resource group that are not in the template:</span></span>

* <span data-ttu-id="d1380-104">При использовании полного режима Resource Manager **удаляет** ресурсы, которые существуют в группе ресурсов, но не указаны в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="d1380-104">In complete mode, Resource Manager **deletes** resources that exist in the resource group but are not specified in the template.</span></span> 
* <span data-ttu-id="d1380-105">В инкрементном режиме Resource Manager **оставляет без изменения** ресурсы, которые существуют в группе ресурсов, но не указаны в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="d1380-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in the resource group but are not specified in the template.</span></span>

<span data-ttu-id="d1380-106">Для обоих режимов Resource Manager пытается подготовить все ресурсы, указанные в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="d1380-106">For both modes, Resource Manager attempts to provision all resources specified in the template.</span></span> <span data-ttu-id="d1380-107">Если ресурс уже существует в группе ресурсов и его параметры не изменились, результаты операции останутся прежними.</span><span class="sxs-lookup"><span data-stu-id="d1380-107">If the resource already exists in the resource group and its settings are unchanged, the operation results in no change.</span></span> <span data-ttu-id="d1380-108">Если параметры ресурса были изменены, ресурс будет использовать новые параметры.</span><span class="sxs-lookup"><span data-stu-id="d1380-108">If you change the settings for a resource, the resource is provisioned with those new settings.</span></span> <span data-ttu-id="d1380-109">При попытке обновить расположение или тип имеющегося ресурса развертывание завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="d1380-109">If you attempt to update the location or type of an existing resource, the deployment fails with an error.</span></span> <span data-ttu-id="d1380-110">Вместо этого вы можете развернуть новый ресурс нужного вам типа с необходимым расположением.</span><span class="sxs-lookup"><span data-stu-id="d1380-110">Instead, deploy a new resource with the location or type that you need.</span></span>

<span data-ttu-id="d1380-111">По умолчанию Resource Manager использует инкрементный режим.</span><span class="sxs-lookup"><span data-stu-id="d1380-111">By default, Resource Manager uses the incremental mode.</span></span>

<span data-ttu-id="d1380-112">Чтобы понять различие между инкрементным и полным режимом, рассмотрим следующий сценарий.</span><span class="sxs-lookup"><span data-stu-id="d1380-112">To illustrate the difference between incremental and complete modes, consider the following scenario.</span></span>

<span data-ttu-id="d1380-113">**Имеющаяся группа ресурсов** содержит:</span><span class="sxs-lookup"><span data-stu-id="d1380-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="d1380-114">ресурс А;</span><span class="sxs-lookup"><span data-stu-id="d1380-114">Resource A</span></span>
* <span data-ttu-id="d1380-115">ресурс Б;</span><span class="sxs-lookup"><span data-stu-id="d1380-115">Resource B</span></span>
* <span data-ttu-id="d1380-116">ресурс В.</span><span class="sxs-lookup"><span data-stu-id="d1380-116">Resource C</span></span>

<span data-ttu-id="d1380-117">**Шаблон** определяет:</span><span class="sxs-lookup"><span data-stu-id="d1380-117">**Template** defines:</span></span>

* <span data-ttu-id="d1380-118">ресурс А;</span><span class="sxs-lookup"><span data-stu-id="d1380-118">Resource A</span></span>
* <span data-ttu-id="d1380-119">ресурс Б;</span><span class="sxs-lookup"><span data-stu-id="d1380-119">Resource B</span></span>
* <span data-ttu-id="d1380-120">ресурс Г.</span><span class="sxs-lookup"><span data-stu-id="d1380-120">Resource D</span></span>

<span data-ttu-id="d1380-121">При развертывании в **инкрементном** режиме группа ресурсов содержит:</span><span class="sxs-lookup"><span data-stu-id="d1380-121">When deployed in **incremental** mode, the resource group contains:</span></span>

* <span data-ttu-id="d1380-122">ресурс А;</span><span class="sxs-lookup"><span data-stu-id="d1380-122">Resource A</span></span>
* <span data-ttu-id="d1380-123">ресурс Б;</span><span class="sxs-lookup"><span data-stu-id="d1380-123">Resource B</span></span>
* <span data-ttu-id="d1380-124">ресурс В;</span><span class="sxs-lookup"><span data-stu-id="d1380-124">Resource C</span></span>
* <span data-ttu-id="d1380-125">ресурс Г.</span><span class="sxs-lookup"><span data-stu-id="d1380-125">Resource D</span></span>

<span data-ttu-id="d1380-126">При развертывании в **полном** режиме ресурс В будет удален.</span><span class="sxs-lookup"><span data-stu-id="d1380-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="d1380-127">Группа ресурсов содержит:</span><span class="sxs-lookup"><span data-stu-id="d1380-127">The resource group contains:</span></span>

* <span data-ttu-id="d1380-128">ресурс А;</span><span class="sxs-lookup"><span data-stu-id="d1380-128">Resource A</span></span>
* <span data-ttu-id="d1380-129">ресурс Б;</span><span class="sxs-lookup"><span data-stu-id="d1380-129">Resource B</span></span>
* <span data-ttu-id="d1380-130">ресурс Г.</span><span class="sxs-lookup"><span data-stu-id="d1380-130">Resource D</span></span>
