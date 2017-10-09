## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="453e9-101">Добавочные и полные развертывания</span><span class="sxs-lookup"><span data-stu-id="453e9-101">Incremental and complete deployments</span></span>
<span data-ttu-id="453e9-102">При развертывании ресурсов, указывается, что развертывания hello добавочное обновление или завершения обновления.</span><span class="sxs-lookup"><span data-stu-id="453e9-102">When deploying your resources, you specify that hello deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="453e9-103">Hello основное различие между этими двумя режимами — обработка существующие ресурсы в группе ресурсов hello, не входящие в шаблон hello диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="453e9-103">hello primary difference between these two modes is how Resource Manager handles existing resources in hello resource group that are not in hello template:</span></span>

* <span data-ttu-id="453e9-104">В полном режиме, диспетчер ресурсов **удаляет** ресурсы, которые существуют в группе ресурсов hello, но не указаны в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="453e9-104">In complete mode, Resource Manager **deletes** resources that exist in hello resource group but are not specified in hello template.</span></span> 
* <span data-ttu-id="453e9-105">В инкрементном режиме, диспетчер ресурсов **оставляет без изменений** ресурсы, которые существуют в группе ресурсов hello, но не указаны в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="453e9-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in hello resource group but are not specified in hello template.</span></span>

<span data-ttu-id="453e9-106">Для обоих режимов диспетчера ресурсов пытается tooprovision все ресурсы, указанные в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="453e9-106">For both modes, Resource Manager attempts tooprovision all resources specified in hello template.</span></span> <span data-ttu-id="453e9-107">Если ресурс hello уже существует в группе ресурсов hello и его параметры не изменяются, операция hello приводит без изменений.</span><span class="sxs-lookup"><span data-stu-id="453e9-107">If hello resource already exists in hello resource group and its settings are unchanged, hello operation results in no change.</span></span> <span data-ttu-id="453e9-108">Если в настройках hello для ресурса, ресурс hello предоставляется эти новые параметры.</span><span class="sxs-lookup"><span data-stu-id="453e9-108">If you change hello settings for a resource, hello resource is provisioned with those new settings.</span></span> <span data-ttu-id="453e9-109">При попытке tooupdate hello расположение или тип существующий ресурс, hello развертывания завершается с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="453e9-109">If you attempt tooupdate hello location or type of an existing resource, hello deployment fails with an error.</span></span> <span data-ttu-id="453e9-110">Вместо этого развернуть новый ресурс с расположением hello, или введите необходимость.</span><span class="sxs-lookup"><span data-stu-id="453e9-110">Instead, deploy a new resource with hello location or type that you need.</span></span>

<span data-ttu-id="453e9-111">По умолчанию диспетчер ресурсов использует hello инкрементном режиме.</span><span class="sxs-lookup"><span data-stu-id="453e9-111">By default, Resource Manager uses hello incremental mode.</span></span>

<span data-ttu-id="453e9-112">tooillustrate hello различие между режимами добавочное и полное, рассмотрите следующие сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="453e9-112">tooillustrate hello difference between incremental and complete modes, consider hello following scenario.</span></span>

<span data-ttu-id="453e9-113">**Имеющаяся группа ресурсов** содержит:</span><span class="sxs-lookup"><span data-stu-id="453e9-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="453e9-114">ресурс А;</span><span class="sxs-lookup"><span data-stu-id="453e9-114">Resource A</span></span>
* <span data-ttu-id="453e9-115">ресурс Б;</span><span class="sxs-lookup"><span data-stu-id="453e9-115">Resource B</span></span>
* <span data-ttu-id="453e9-116">ресурс В.</span><span class="sxs-lookup"><span data-stu-id="453e9-116">Resource C</span></span>

<span data-ttu-id="453e9-117">**Шаблон** определяет:</span><span class="sxs-lookup"><span data-stu-id="453e9-117">**Template** defines:</span></span>

* <span data-ttu-id="453e9-118">ресурс А;</span><span class="sxs-lookup"><span data-stu-id="453e9-118">Resource A</span></span>
* <span data-ttu-id="453e9-119">ресурс Б;</span><span class="sxs-lookup"><span data-stu-id="453e9-119">Resource B</span></span>
* <span data-ttu-id="453e9-120">ресурс Г.</span><span class="sxs-lookup"><span data-stu-id="453e9-120">Resource D</span></span>

<span data-ttu-id="453e9-121">При развертывании в **добавочное** режиме, группа ресурсов hello содержит:</span><span class="sxs-lookup"><span data-stu-id="453e9-121">When deployed in **incremental** mode, hello resource group contains:</span></span>

* <span data-ttu-id="453e9-122">ресурс А;</span><span class="sxs-lookup"><span data-stu-id="453e9-122">Resource A</span></span>
* <span data-ttu-id="453e9-123">ресурс Б;</span><span class="sxs-lookup"><span data-stu-id="453e9-123">Resource B</span></span>
* <span data-ttu-id="453e9-124">ресурс В;</span><span class="sxs-lookup"><span data-stu-id="453e9-124">Resource C</span></span>
* <span data-ttu-id="453e9-125">ресурс Г.</span><span class="sxs-lookup"><span data-stu-id="453e9-125">Resource D</span></span>

<span data-ttu-id="453e9-126">При развертывании в **полном** режиме ресурс В будет удален.</span><span class="sxs-lookup"><span data-stu-id="453e9-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="453e9-127">Группа ресурсов Hello содержит:</span><span class="sxs-lookup"><span data-stu-id="453e9-127">hello resource group contains:</span></span>

* <span data-ttu-id="453e9-128">ресурс А;</span><span class="sxs-lookup"><span data-stu-id="453e9-128">Resource A</span></span>
* <span data-ttu-id="453e9-129">ресурс Б;</span><span class="sxs-lookup"><span data-stu-id="453e9-129">Resource B</span></span>
* <span data-ttu-id="453e9-130">ресурс Г.</span><span class="sxs-lookup"><span data-stu-id="453e9-130">Resource D</span></span>
