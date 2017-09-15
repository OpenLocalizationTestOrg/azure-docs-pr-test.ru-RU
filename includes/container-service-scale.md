# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="e013c-101">Масштабирование узлов агента в кластере службы контейнеров</span><span class="sxs-lookup"><span data-stu-id="e013c-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="e013c-102">После того как вы [развернете кластер службы контейнера Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), может потребоваться изменить число узлов агента.</span><span class="sxs-lookup"><span data-stu-id="e013c-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need to change the number of agent nodes.</span></span> <span data-ttu-id="e013c-103">Например, будут нужны дополнительные узлы агентов для запуска большего количества контейнеров или экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="e013c-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="e013c-104">Количество узлов агентов в кластере DC/OS, Docker Swarm или Kubernetes можно изменить с помощью портала Azure или Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="e013c-104">You can change the number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using the Azure portal or the Azure CLI 2.0.</span></span> 

## <a name="scale-with-the-azure-portal"></a><span data-ttu-id="e013c-105">Масштабирование с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="e013c-105">Scale with the Azure portal</span></span>

1. <span data-ttu-id="e013c-106">На [портале Azure](https://portal.azure.com) найдите **Службы контейнеров** и выберите службу контейнера, которую хотите изменить.</span><span class="sxs-lookup"><span data-stu-id="e013c-106">In the [Azure portal](https://portal.azure.com), browse for **Container services**, and then click the container service that you want to modify.</span></span>
2. <span data-ttu-id="e013c-107">В колонке **службы контейнеров** щелкните **Агенты**.</span><span class="sxs-lookup"><span data-stu-id="e013c-107">In the **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="e013c-108">В поле **Число виртуальных машин** введите нужное число узлов агентов.</span><span class="sxs-lookup"><span data-stu-id="e013c-108">In **VM Count**, enter the desired number of agents nodes.</span></span>

    ![Масштабирование кластера на портале](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="e013c-110">Чтобы сохранить конфигурацию, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e013c-110">To save the configuration, click **Save**.</span></span>

## <a name="scale-with-the-azure-cli-20"></a><span data-ttu-id="e013c-111">Масштабирование с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e013c-111">Scale with the Azure CLI 2.0</span></span>

<span data-ttu-id="e013c-112">Убедитесь, что у вас [установлена](/cli/azure/install-az-cli2) последняя версия Azure CLI 2.0, и войдите в учетную запись Azure с помощью команды `az login`.</span><span class="sxs-lookup"><span data-stu-id="e013c-112">Make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an azure account (`az login`).</span></span>

### <a name="see-the-current-agent-count"></a><span data-ttu-id="e013c-113">Просмотр текущего числа агентов</span><span class="sxs-lookup"><span data-stu-id="e013c-113">See the current agent count</span></span>
<span data-ttu-id="e013c-114">Чтобы просмотреть количество агентов, входящих в кластер на текущий момент, запустите команду `az acs show`.</span><span class="sxs-lookup"><span data-stu-id="e013c-114">To see the number of agents currently in the cluster, run the `az acs show` command.</span></span> <span data-ttu-id="e013c-115">Эта команда показывает конфигурацию кластера.</span><span class="sxs-lookup"><span data-stu-id="e013c-115">This shows the cluster configuration.</span></span> <span data-ttu-id="e013c-116">Например, следующая команда отображает конфигурацию службы контейнеров с именем `containerservice-myACSName` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e013c-116">For example, the following command shows the configuration of the container service named `containerservice-myACSName` in the resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="e013c-117">Количество агентов содержится в параметре `Count` в разделе `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="e013c-117">The command returns the number of agents in the `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-the-az-acs-scale-command"></a><span data-ttu-id="e013c-118">Использование команды az acs scale</span><span class="sxs-lookup"><span data-stu-id="e013c-118">Use the az acs scale command</span></span>
<span data-ttu-id="e013c-119">Чтобы изменить число узлов агента, запустите команду `az acs scale`, указав для нее **группу ресурсов**, **имя службы контейнеров** и требуемое **новое число агентов**.</span><span class="sxs-lookup"><span data-stu-id="e013c-119">To change the number of agent nodes, run the `az acs scale` command and supply the **resource group**, **container service name**, and the desired **new agent count**.</span></span> <span data-ttu-id="e013c-120">Используя меньшее или большее количество агентов, можно уменьшать или увеличивать масштаб соответственно.</span><span class="sxs-lookup"><span data-stu-id="e013c-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="e013c-121">Например, чтобы для кластера из предыдущего примера установить значение 10 в качестве количества агентов, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e013c-121">For example, to change the number of agents in the previous cluster to 10, type the following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="e013c-122">Azure CLI 2.0 возвращает строку JSON, представляющую новую конфигурацию службы контейнеров, включая измененное количество агентов.</span><span class="sxs-lookup"><span data-stu-id="e013c-122">The Azure CLI 2.0 returns a JSON string representing the new configuration of the container service, including the new agent count.</span></span>

<span data-ttu-id="e013c-123">Чтобы увидеть дополнительные параметры команды, запустите `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="e013c-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="e013c-124">Рекомендации по масштабированию</span><span class="sxs-lookup"><span data-stu-id="e013c-124">Scaling considerations</span></span>

* <span data-ttu-id="e013c-125">Количество узлов агентов должно находиться в диапазоне от 1 до 100 включительно.</span><span class="sxs-lookup"><span data-stu-id="e013c-125">The number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="e013c-126">Квота на использование ядер может налагать ограничения на количество узлов агентов в кластере.</span><span class="sxs-lookup"><span data-stu-id="e013c-126">Your cores quota can limit the number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="e013c-127">Операции масштабирования узлов агентов применяются к масштабируемому набору виртуальных машин Azure, который содержит пул агентов.</span><span class="sxs-lookup"><span data-stu-id="e013c-127">Agent node scaling operations are applied to an Azure virtual machine scale set that contains the agent pool.</span></span> <span data-ttu-id="e013c-128">В кластере DC/OS операции масштабирования, описанные в этой статье, влияют только на число узлов агентов в закрытом пуле.</span><span class="sxs-lookup"><span data-stu-id="e013c-128">In a DC/OS cluster, only agent nodes in the private pool are scaled by the operations shown in this article.</span></span>

* <span data-ttu-id="e013c-129">В зависимости от того, какой оркестратор развернут в кластере, можно отдельно масштабировать число экземпляров контейнера, работающих в кластере.</span><span class="sxs-lookup"><span data-stu-id="e013c-129">Depending on the orchestrator you deploy in your cluster, you can separately scale the number of instances of a container running on the cluster.</span></span> <span data-ttu-id="e013c-130">Например, в кластере DC/OS [пользовательский интерфейс Marathon](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) позволяет изменять число экземпляров для приложения контейнера.</span><span class="sxs-lookup"><span data-stu-id="e013c-130">For example, in a DC/OS cluster, use the [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) to change the number of instances of a container application.</span></span>

* <span data-ttu-id="e013c-131">В настоящее время не поддерживается автоматическое масштабирование узлов агентов в кластере службы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="e013c-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e013c-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e013c-132">Next steps</span></span>
* <span data-ttu-id="e013c-133">Изучите [дополнительные примеры](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) использования команд Azure CLI 2.0 для работы со службой контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="e013c-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="e013c-134">См. дополнительные сведения о [пулах агентов DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="e013c-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

