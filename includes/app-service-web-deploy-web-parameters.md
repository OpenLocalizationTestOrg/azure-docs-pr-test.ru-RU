<span data-ttu-id="2e4de-101">С помощью диспетчера ресурсов Azure можно определить параметры для значения требуется toospecify при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="2e4de-101">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="2e4de-102">шаблон Hello имеется раздел с именем параметров, содержащий все значения параметров hello.</span><span class="sxs-lookup"><span data-stu-id="2e4de-102">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="2e4de-103">Следует определить параметр для те значения, которые будут различаться на основе hello проекта, в которой выполняется развертывание или на основании hello среды, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="2e4de-103">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="2e4de-104">Определяет параметры для значения, которые всегда останутся hello таким же.</span><span class="sxs-lookup"><span data-stu-id="2e4de-104">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="2e4de-105">Каждое значение параметра используется в hello шаблона toodefine hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="2e4de-105">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

<span data-ttu-id="2e4de-106">При определении параметров следует использовать hello **allowedValues** toospecify поля, в которой значения пользователь может предоставить во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="2e4de-106">When defining parameters, use hello **allowedValues** field toospecify which values a user can provide during deployment.</span></span> <span data-ttu-id="2e4de-107">Используйте hello **defaultValue** tooassign поля toohello значение параметра, если значение не указано во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="2e4de-107">Use hello **defaultValue** field tooassign a value toohello parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="2e4de-108">Мы опишем каждого параметра в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="2e4de-108">We will describe each parameter in hello template.</span></span>

### <a name="sitename"></a><span data-ttu-id="2e4de-109">siteName</span><span class="sxs-lookup"><span data-stu-id="2e4de-109">siteName</span></span>
<span data-ttu-id="2e4de-110">Имя веб-приложения hello, что вы хотите toocreate Hello.</span><span class="sxs-lookup"><span data-stu-id="2e4de-110">hello name of hello web app that you wish toocreate.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="2e4de-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="2e4de-111">hostingPlanName</span></span>
<span data-ttu-id="2e4de-112">Имя Hello hello службы приложений плана toouse для размещения веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2e4de-112">hello name of hello App Service plan toouse for hosting hello web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="2e4de-113">sku</span><span class="sxs-lookup"><span data-stu-id="2e4de-113">sku</span></span>
<span data-ttu-id="2e4de-114">Здравствуйте, ценовую категорию для плана размещения hello.</span><span class="sxs-lookup"><span data-stu-id="2e4de-114">hello pricing tier for hello hosting plan.</span></span>

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

<span data-ttu-id="2e4de-115">шаблон Hello определяет hello значения, разрешенные для этого параметра и назначает значение по умолчанию (S1), если значение не указано.</span><span class="sxs-lookup"><span data-stu-id="2e4de-115">hello template defines hello values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="2e4de-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="2e4de-116">workerSize</span></span>
<span data-ttu-id="2e4de-117">размер экземпляра плана (небольшие, средние и большие) размещения hello Hello.</span><span class="sxs-lookup"><span data-stu-id="2e4de-117">hello instance size of hello hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="2e4de-118">шаблон Hello определяет hello значения, разрешенные для этого параметра (0, 1 или 2) и назначает значение по умолчанию (0), если значение не указано.</span><span class="sxs-lookup"><span data-stu-id="2e4de-118">hello template defines hello values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="2e4de-119">Hello значения соответствуют toosmall, средний и большой.</span><span class="sxs-lookup"><span data-stu-id="2e4de-119">hello values correspond toosmall, medium and large.</span></span>

