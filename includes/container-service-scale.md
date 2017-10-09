# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="cf33e-101">Масштабирование узлов агента в кластере службы контейнеров</span><span class="sxs-lookup"><span data-stu-id="cf33e-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="cf33e-102">После [развертывание кластера службы контейнера Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), может потребоваться toochange hello числу узлов, агент.</span><span class="sxs-lookup"><span data-stu-id="cf33e-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need toochange hello number of agent nodes.</span></span> <span data-ttu-id="cf33e-103">Например, будут нужны дополнительные узлы агентов для запуска большего количества контейнеров или экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="cf33e-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="cf33e-104">Можно изменить с помощью портала Azure hello hello количество узлов агента в кластере DC/OS помощью Docker Swarm и Kubernetes или hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="cf33e-104">You can change hello number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using hello Azure portal or hello Azure CLI 2.0.</span></span> 

## <a name="scale-with-hello-azure-portal"></a><span data-ttu-id="cf33e-105">Масштабирование с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="cf33e-105">Scale with hello Azure portal</span></span>

1. <span data-ttu-id="cf33e-106">В hello [портал Azure](https://portal.azure.com), поиск **служб контейнеров**, а затем нажмите кнопку hello контейнер службы, которые должны toomodify.</span><span class="sxs-lookup"><span data-stu-id="cf33e-106">In hello [Azure portal](https://portal.azure.com), browse for **Container services**, and then click hello container service that you want toomodify.</span></span>
2. <span data-ttu-id="cf33e-107">В hello **контейнера службы** колонка, щелкните **агенты**.</span><span class="sxs-lookup"><span data-stu-id="cf33e-107">In hello **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="cf33e-108">В **число виртуальных Машин**, введите номер требуемого hello агентов узлов.</span><span class="sxs-lookup"><span data-stu-id="cf33e-108">In **VM Count**, enter hello desired number of agents nodes.</span></span>

    ![Масштабирование пула hello портала](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="cf33e-110">Конфигурация toosave hello, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cf33e-110">toosave hello configuration, click **Save**.</span></span>

## <a name="scale-with-hello-azure-cli-20"></a><span data-ttu-id="cf33e-111">Масштабирование с hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cf33e-111">Scale with hello Azure CLI 2.0</span></span>

<span data-ttu-id="cf33e-112">Убедитесь, что вы [установлен](/cli/azure/install-az-cli2) hello последнюю Azure CLI 2.0 и вход tooan учетная запись azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="cf33e-112">Make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan azure account (`az login`).</span></span>

### <a name="see-hello-current-agent-count"></a><span data-ttu-id="cf33e-113">В разделе hello текущее количество агентов</span><span class="sxs-lookup"><span data-stu-id="cf33e-113">See hello current agent count</span></span>
<span data-ttu-id="cf33e-114">количество агентов в настоящее время hello toosee в кластере hello запуска hello `az acs show` команды.</span><span class="sxs-lookup"><span data-stu-id="cf33e-114">toosee hello number of agents currently in hello cluster, run hello `az acs show` command.</span></span> <span data-ttu-id="cf33e-115">Это показано hello конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="cf33e-115">This shows hello cluster configuration.</span></span> <span data-ttu-id="cf33e-116">Здравствуйте, например, следующая команда отображает hello конфигурации hello контейнер службы с именем `containerservice-myACSName` в группе ресурсов hello `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="cf33e-116">For example, hello following command shows hello configuration of hello container service named `containerservice-myACSName` in hello resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="cf33e-117">Команда Hello возвращает hello количество агентов в hello `Count` в разделе `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="cf33e-117">hello command returns hello number of agents in hello `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-hello-az-acs-scale-command"></a><span data-ttu-id="cf33e-118">Используйте hello az команды масштаб acs</span><span class="sxs-lookup"><span data-stu-id="cf33e-118">Use hello az acs scale command</span></span>
<span data-ttu-id="cf33e-119">количество узлов агента выполните hello hello toochange `az acs scale` команды и указывайте hello **группы ресурсов**, **имя контейнера службы**и требуемого hello **количество новых агента**.</span><span class="sxs-lookup"><span data-stu-id="cf33e-119">toochange hello number of agent nodes, run hello `az acs scale` command and supply hello **resource group**, **container service name**, and hello desired **new agent count**.</span></span> <span data-ttu-id="cf33e-120">Используя меньшее или большее количество агентов, можно уменьшать или увеличивать масштаб соответственно.</span><span class="sxs-lookup"><span data-stu-id="cf33e-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="cf33e-121">Например количество агентов в предыдущих hello hello toochange кластеров too10 типа hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cf33e-121">For example, toochange hello number of agents in hello previous cluster too10, type hello following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="cf33e-122">Hello Azure CLI 2.0 возвращает строку JSON, представляющую hello новую конфигурацию службы hello контейнера, включая количество новых агента hello.</span><span class="sxs-lookup"><span data-stu-id="cf33e-122">hello Azure CLI 2.0 returns a JSON string representing hello new configuration of hello container service, including hello new agent count.</span></span>

<span data-ttu-id="cf33e-123">Чтобы увидеть дополнительные параметры команды, запустите `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="cf33e-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="cf33e-124">Рекомендации по масштабированию</span><span class="sxs-lookup"><span data-stu-id="cf33e-124">Scaling considerations</span></span>

* <span data-ttu-id="cf33e-125">Номер Hello узлов агент должен быть от 1 до 100 включительно.</span><span class="sxs-lookup"><span data-stu-id="cf33e-125">hello number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="cf33e-126">Свою квоту ядер можно ограничить число hello агента узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="cf33e-126">Your cores quota can limit hello number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="cf33e-127">Операции масштабирования узла агента задаются примененных tooan виртуальной машины Azure шкалы, содержащий пул агентов hello.</span><span class="sxs-lookup"><span data-stu-id="cf33e-127">Agent node scaling operations are applied tooan Azure virtual machine scale set that contains hello agent pool.</span></span> <span data-ttu-id="cf33e-128">В кластере DC/OS только узлы агентов в пуле закрытый hello масштабируются операциями hello, приведенными в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cf33e-128">In a DC/OS cluster, only agent nodes in hello private pool are scaled by hello operations shown in this article.</span></span>

* <span data-ttu-id="cf33e-129">В зависимости от того, orchestrator hello, развертываемым в кластере можно отдельно масштабировать hello число экземпляров контейнера, запущенного в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="cf33e-129">Depending on hello orchestrator you deploy in your cluster, you can separately scale hello number of instances of a container running on hello cluster.</span></span> <span data-ttu-id="cf33e-130">Например, в кластере DC/OS использовать hello [пользовательского интерфейса Marathon](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello число экземпляров приложения-контейнера.</span><span class="sxs-lookup"><span data-stu-id="cf33e-130">For example, in a DC/OS cluster, use hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello number of instances of a container application.</span></span>

* <span data-ttu-id="cf33e-131">В настоящее время не поддерживается автоматическое масштабирование узлов агентов в кластере службы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="cf33e-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf33e-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cf33e-132">Next steps</span></span>
* <span data-ttu-id="cf33e-133">Изучите [дополнительные примеры](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) использования команд Azure CLI 2.0 для работы со службой контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="cf33e-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="cf33e-134">См. дополнительные сведения о [пулах агентов DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="cf33e-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

