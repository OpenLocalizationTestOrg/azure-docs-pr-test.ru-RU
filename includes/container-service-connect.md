# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="5ba40-101">Создания кластера, Kubernetes, DC/OS или с помощью Docker Swarm tooa удаленного подключения</span><span class="sxs-lookup"><span data-stu-id="5ba40-101">Make a remote connection tooa Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="5ba40-102">После создания кластера контейнера службы Azure, требуется toodeploy кластера toohello tooconnect и управление рабочими нагрузками.</span><span class="sxs-lookup"><span data-stu-id="5ba40-102">After creating an Azure Container Service cluster, you need tooconnect toohello cluster toodeploy and manage workloads.</span></span> <span data-ttu-id="5ba40-103">В этой статье описывается, как главный toohello tooconnect виртуальная машина hello кластера с удаленного компьютера.</span><span class="sxs-lookup"><span data-stu-id="5ba40-103">This article describes how tooconnect toohello master VM of hello cluster from a remote computer.</span></span> 

<span data-ttu-id="5ba40-104">Hello Kubernetes, DC/OS и с помощью Docker Swarm кластеры обеспечивают локально конечные точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="5ba40-104">hello Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="5ba40-105">Для Kubernetes, эта конечная точка безопасно предоставляется hello Интернет и доступ к нему, запустив hello `kubectl` средство командной строки с любого компьютера, подключенного к Интернету.</span><span class="sxs-lookup"><span data-stu-id="5ba40-105">For Kubernetes, this endpoint is securely exposed on hello internet, and you can access it by running hello `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="5ba40-106">Для контроллера домена/OS и помощью Docker Swarm рекомендуется создавать туннеля безопасного shell (SSH) из системы управления кластера toohello локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="5ba40-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer toohello cluster management system.</span></span> <span data-ttu-id="5ba40-107">После установления туннеля hello запуском команды, которые используют конечные точки HTTP hello и представление hello orchestrator веб-интерфейса (если он доступен) с локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="5ba40-107">After hello tunnel is established, you can run commands which use hello HTTP endpoints and view hello orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5ba40-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5ba40-108">Prerequisites</span></span>

* <span data-ttu-id="5ba40-109">Кластер Kubernetes, DC/OS или Docker Swarm, [развернутый в службе контейнеров Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5ba40-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="5ba40-110">SSH-RSA файла закрытого ключа, соответствующего открытого ключа добавлены toohello кластера toohello во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="5ba40-110">SSH RSA private key file, corresponding toohello public key added toohello cluster during deployment.</span></span> <span data-ttu-id="5ba40-111">Эти команды предполагают, что hello закрытого SSH-ключ находится в `$HOME/.ssh/id_rsa` на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ba40-111">These commands assume that hello private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="5ba40-112">Дополнительные сведения см. в статьях [Как создать и использовать пару из открытого и закрытого ключей SSH для виртуальных машин Linux в Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md) и [Использование ключей SSH с Windows в Azure](../articles/virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="5ba40-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="5ba40-113">Если hello SSH-подключение не работает, может потребоваться слишком [сброс ключей SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="5ba40-113">If hello SSH connection isn't working, you may need too [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-tooa-kubernetes-cluster"></a><span data-ttu-id="5ba40-114">Подключите кластер Kubernetes tooa</span><span class="sxs-lookup"><span data-stu-id="5ba40-114">Connect tooa Kubernetes cluster</span></span>

<span data-ttu-id="5ba40-115">Выполните эти шаги tooinstall и настройте `kubectl` на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ba40-115">Follow these steps tooinstall and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="5ba40-116">В Linux или macOS, может потребоваться toorun hello команды в этом разделе с помощью `sudo`.</span><span class="sxs-lookup"><span data-stu-id="5ba40-116">On Linux or macOS, you might need toorun hello commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="5ba40-117">Установка kubectl</span><span class="sxs-lookup"><span data-stu-id="5ba40-117">Install kubectl</span></span>
<span data-ttu-id="5ba40-118">Одним из способов tooinstall это средство — toouse hello `az acs kubernetes install-cli` команда Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="5ba40-118">One way tooinstall this tool is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="5ba40-119">toorun эту команду, убедитесь, что вы [установлен](/cli/azure/install-az-cli2) hello последнюю Azure CLI 2.0 и войти в учетную запись Azure tooan (`az login`).</span><span class="sxs-lookup"><span data-stu-id="5ba40-119">toorun this command, make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="5ba40-120">Кроме того, вы можете загрузить hello последней `kubectl` клиента непосредственно из hello [Kubernetes освобождает страницу](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="5ba40-120">Alternatively, you can download hello latest `kubectl` client directly from hello [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="5ba40-121">Дополнительные сведения см. в разделе [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Установка и настройка kubectl).</span><span class="sxs-lookup"><span data-stu-id="5ba40-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="5ba40-122">Скачивание учетных данных кластера</span><span class="sxs-lookup"><span data-stu-id="5ba40-122">Download cluster credentials</span></span>
<span data-ttu-id="5ba40-123">После получения `kubectl` установлен, нужна tooyour учетные данные машина, toocopy hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5ba40-123">Once you have `kubectl` installed, you need toocopy hello cluster credentials tooyour machine.</span></span> <span data-ttu-id="5ba40-124">Является одним из способов toodo get hello, учетные данные с hello `az acs kubernetes get-credentials` команды.</span><span class="sxs-lookup"><span data-stu-id="5ba40-124">One way toodo get hello credentials is with hello `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="5ba40-125">Передайте hello имя группы ресурсов hello и hello для ресурса службы hello контейнера:</span><span class="sxs-lookup"><span data-stu-id="5ba40-125">Pass hello name of hello resource group and hello name of hello container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="5ba40-126">Эта команда загружает учетные данные кластера hello слишком`$HOME/.kube/config`, где `kubectl` ожидает ее найти toobe.</span><span class="sxs-lookup"><span data-stu-id="5ba40-126">This command downloads hello cluster credentials too`$HOME/.kube/config`, where `kubectl` expects it toobe located.</span></span>

<span data-ttu-id="5ba40-127">Кроме того, можно использовать `scp` toosecurely Копировать файл hello из `$HOME/.kube/config` на hello основной виртуальной Машины tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="5ba40-127">Alternatively, you can use `scp` toosecurely copy hello file from `$HOME/.kube/config` on hello master VM tooyour local machine.</span></span> <span data-ttu-id="5ba40-128">Например:</span><span class="sxs-lookup"><span data-stu-id="5ba40-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="5ba40-129">При работе в Windows можно использовать Bash на Ubuntu на Windows, клиент копирования PuTTy защищенный файл hello или аналогичное средство.</span><span class="sxs-lookup"><span data-stu-id="5ba40-129">If you are on Windows, you can use Bash on Ubuntu on Windows, hello PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="5ba40-130">Использование kubectl</span><span class="sxs-lookup"><span data-stu-id="5ba40-130">Use kubectl</span></span>

<span data-ttu-id="5ba40-131">После получения `kubectl` настроен, проверка соединения hello, перечисляя hello узлов в кластере:</span><span class="sxs-lookup"><span data-stu-id="5ba40-131">Once you have `kubectl` configured, test hello connection by listing hello nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="5ba40-132">Можно использовать другие команды `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="5ba40-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="5ba40-133">Например можно просмотреть hello Kubernetes панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="5ba40-133">For example, you can view hello Kubernetes Dashboard.</span></span> <span data-ttu-id="5ba40-134">Сначала необходимо запустите учетную запись-посредник сервера API-интерфейса Kubernetes toohello:</span><span class="sxs-lookup"><span data-stu-id="5ba40-134">First, run a proxy toohello Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="5ba40-135">Hello Kubernetes пользовательского интерфейса теперь доступен на: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="5ba40-135">hello Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="5ba40-136">Дополнительные сведения см. в разделе hello [Kubernetes краткого](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="5ba40-136">For more information, see hello [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-tooa-dcos-or-swarm-cluster"></a><span data-ttu-id="5ba40-137">Подключите кластер tooa DC/OS или группу мелких объектов</span><span class="sxs-lookup"><span data-stu-id="5ba40-137">Connect tooa DC/OS or Swarm cluster</span></span>

<span data-ttu-id="5ba40-138">hello toouse DC/OS и кластеры с помощью Docker Swarm развернут контейнер службой Azure выполните эти инструкции toocreate туннель SSH из локальной системы Windows, Linux или macOS.</span><span class="sxs-lookup"><span data-stu-id="5ba40-138">toouse hello DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions toocreate a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="5ba40-139">В статье рассматриваются инструкции по туннелированию TCP-трафика по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="5ba40-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="5ba40-140">Можно также запустить интерактивный сеанс SSH с одной из систем управления hello внутри кластера, но это не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="5ba40-140">You can also start an interactive SSH session with one of hello internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="5ba40-141">Работа непосредственно во внутренней системе, вы рискуете случайно изменить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="5ba40-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="5ba40-142">Создание туннеля SSH в Linux или macOS</span><span class="sxs-lookup"><span data-stu-id="5ba40-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="5ba40-143">Hello первое, что при создании туннель SSH в Linux или macOS — toolocate hello открытому DNS-имени hello образцов балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5ba40-143">hello first thing that you do when you create an SSH tunnel on Linux or macOS is toolocate hello public DNS name of hello load-balanced masters.</span></span> <span data-ttu-id="5ba40-144">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5ba40-144">Follow these steps:</span></span>


1. <span data-ttu-id="5ba40-145">В hello [портал Azure](https://portal.azure.com), Обзор toohello группы ресурсов, содержащий контейнер службы кластера.</span><span class="sxs-lookup"><span data-stu-id="5ba40-145">In hello [Azure portal](https://portal.azure.com), browse toohello resource group containing your container service cluster.</span></span> <span data-ttu-id="5ba40-146">Разверните группу ресурсов hello, для отображения каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="5ba40-146">Expand hello resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="5ba40-147">Нажмите кнопку hello **контейнера службы** ресурс и нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="5ba40-147">Click hello **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="5ba40-148">Hello **полное доменное имя главного** из hello кластера отображается под **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="5ba40-148">hello **Master FQDN** of hello cluster appears under **Essentials**.</span></span> <span data-ttu-id="5ba40-149">Сохраните это имя для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="5ba40-149">Save this name for later use.</span></span> 

    ![Общедоступное DNS-имя](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="5ba40-151">Кроме того, запустите hello `az acs show` в контейнере службы.</span><span class="sxs-lookup"><span data-stu-id="5ba40-151">Alternatively, run hello `az acs show` command on your container service.</span></span> <span data-ttu-id="5ba40-152">Найдите hello **Master профиля: полное доменное имя** свойства в выходных данных команды hello.</span><span class="sxs-lookup"><span data-stu-id="5ba40-152">Look for hello **Master Profile:fqdn** property in hello command output.</span></span>

3. <span data-ttu-id="5ba40-153">Теперь откройте оболочку и запустите hello `ssh` команду, указав hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="5ba40-153">Now open a shell and run hello `ssh` command by specifying hello following values:</span></span> 

    <span data-ttu-id="5ba40-154">**LOCAL_PORT** используется TCP-порт hello на стороне службы hello hello tooconnect туннеля для.</span><span class="sxs-lookup"><span data-stu-id="5ba40-154">**LOCAL_PORT** is hello TCP port on hello service side of hello tunnel tooconnect to.</span></span> <span data-ttu-id="5ba40-155">Для группу мелких объектов значение этого too2375.</span><span class="sxs-lookup"><span data-stu-id="5ba40-155">For Swarm, set this too2375.</span></span> <span data-ttu-id="5ba40-156">Для контроллера домена/OS значение этого too80.</span><span class="sxs-lookup"><span data-stu-id="5ba40-156">For DC/OS, set this too80.</span></span> 
    <span data-ttu-id="5ba40-157">**REMOTE_PORT** — порт hello hello конечной точки, которые должны tooexpose.</span><span class="sxs-lookup"><span data-stu-id="5ba40-157">**REMOTE_PORT** is hello port of hello endpoint that you want tooexpose.</span></span> <span data-ttu-id="5ba40-158">Для Swarm используется порт 2375.</span><span class="sxs-lookup"><span data-stu-id="5ba40-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="5ba40-159">Для DC/OS используется порт 80.</span><span class="sxs-lookup"><span data-stu-id="5ba40-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="5ba40-160">**Имя пользователя** hello именем пользователя, предоставленный при развертывании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5ba40-160">**USERNAME** is hello user name that was provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="5ba40-161">**DNSPREFIX** — префикс DNS hello, указанный при развертывании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5ba40-161">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="5ba40-162">**ОБЛАСТЬ** — hello область, в которой находится в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5ba40-162">**REGION** is hello region in which your resource group is located.</span></span>  
    <span data-ttu-id="5ba40-163">**PATH_TO_PRIVATE_KEY** [необязательно] является hello путь toohello закрытый ключ, соответствующий toohello открытый ключ, указанный при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5ba40-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is hello path toohello private key that corresponds toohello public key you provided when you created hello cluster.</span></span> <span data-ttu-id="5ba40-164">Используйте этот параметр с hello `-i` флаг.</span><span class="sxs-lookup"><span data-stu-id="5ba40-164">Use this option with hello `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="5ba40-165">Hello порт SSH-подключения является 2200 и не hello стандартный порт 22.</span><span class="sxs-lookup"><span data-stu-id="5ba40-165">hello SSH connection port is 2200 and not hello standard port 22.</span></span> <span data-ttu-id="5ba40-166">В кластере с более чем один основной виртуальной Машины это hello подключения порт toohello первый образец виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5ba40-166">In a cluster with more than one master VM, this is hello connection port toohello first master VM.</span></span>
  > 

  <span data-ttu-id="5ba40-167">Команда Hello возвращает без выходных данных.</span><span class="sxs-lookup"><span data-stu-id="5ba40-167">hello command returns without output.</span></span>

<span data-ttu-id="5ba40-168">В следующих разделах hello см. Примеры hello для контроллера домена/OS и группу мелких объектов.</span><span class="sxs-lookup"><span data-stu-id="5ba40-168">See hello examples for DC/OS and Swarm in hello following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="5ba40-169">Туннель DC/OS</span><span class="sxs-lookup"><span data-stu-id="5ba40-169">DC/OS tunnel</span></span>
<span data-ttu-id="5ba40-170">tooopen туннеля для контроллера домена/OS конечные точки, выполните команду hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5ba40-170">tooopen a tunnel for DC/OS endpoints, run a command like hello following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="5ba40-171">Убедитесь, что у вас нет другого локального процесса, привязанного к порту 80.</span><span class="sxs-lookup"><span data-stu-id="5ba40-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="5ba40-172">При необходимости в качестве локального порта вместо 80 можно указать, например, 8080,</span><span class="sxs-lookup"><span data-stu-id="5ba40-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="5ba40-173">но в этом случае некоторые ссылки в пользовательском веб-интерфейсе могут не работать.</span><span class="sxs-lookup"><span data-stu-id="5ba40-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="5ba40-174">Теперь вы можете использовать конечные точки контроллера домена/OS hello из локальной системы, используя hello следующие URL-адреса (при условии, что локальный порт 80):</span><span class="sxs-lookup"><span data-stu-id="5ba40-174">You can now access hello DC/OS endpoints from your local system through hello following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="5ba40-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="5ba40-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="5ba40-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="5ba40-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="5ba40-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="5ba40-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="5ba40-178">Аналогичным образом может достигать hello API rest для каждого приложения через этот туннель.</span><span class="sxs-lookup"><span data-stu-id="5ba40-178">Similarly, you can reach hello rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="5ba40-179">Туннель Swarm</span><span class="sxs-lookup"><span data-stu-id="5ba40-179">Swarm tunnel</span></span>
<span data-ttu-id="5ba40-180">tooopen конечной точки группу мелких объектов toohello туннеля, выполните команду hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5ba40-180">tooopen a tunnel toohello Swarm endpoint, run a command like hello following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="5ba40-181">Убедитесь, что у вас нет другого локального процесса, привязанного к порту 2375.</span><span class="sxs-lookup"><span data-stu-id="5ba40-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="5ba40-182">Например управляющая программа Docker hello выполняются локально, устанавливается по умолчанию toouse порт 2375.</span><span class="sxs-lookup"><span data-stu-id="5ba40-182">For example, if you are running hello Docker daemon locally, it's set by default toouse port 2375.</span></span> <span data-ttu-id="5ba40-183">При необходимости вместо 2375 можно указать локальный порт.</span><span class="sxs-lookup"><span data-stu-id="5ba40-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="5ba40-184">Теперь можно получить доступ к hello помощью Docker Swarm кластера, с помощью интерфейса командной строки Docker hello (Docker CLI) в локальной системе.</span><span class="sxs-lookup"><span data-stu-id="5ba40-184">Now you can access hello Docker Swarm cluster using hello Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="5ba40-185">Инструкции по установке Docker см. в [этом руководстве](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="5ba40-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="5ba40-186">Задайте ваш toohello переменную среды DOCKER_HOST локального порта, настроенного для hello туннеля.</span><span class="sxs-lookup"><span data-stu-id="5ba40-186">Set your DOCKER_HOST environment variable toohello local port you configured for hello tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="5ba40-187">Выполните команды Docker, туннеля toohello помощью Docker Swarm кластера.</span><span class="sxs-lookup"><span data-stu-id="5ba40-187">Run Docker commands that tunnel toohello Docker Swarm cluster.</span></span> <span data-ttu-id="5ba40-188">Например:</span><span class="sxs-lookup"><span data-stu-id="5ba40-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="5ba40-189">Создание туннеля SSH в Windows</span><span class="sxs-lookup"><span data-stu-id="5ba40-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="5ba40-190">Создавать туннели SSH в Windows можно несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="5ba40-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="5ba40-191">При выполнении Bash на Ubuntu в Windows или аналогичное средство, вы можете использовать hello SSH туннелирования инструкции, приведенные ранее в этой статье macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="5ba40-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow hello SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="5ba40-192">В качестве альтернативы для Windows в этом разделе описываются как toouse PuTTY toocreate hello туннеля.</span><span class="sxs-lookup"><span data-stu-id="5ba40-192">As an alternative on Windows, this section describes how toouse PuTTY toocreate hello tunnel.</span></span>

1. <span data-ttu-id="5ba40-193">[Загрузить PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour системы Windows.</span><span class="sxs-lookup"><span data-stu-id="5ba40-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows system.</span></span>

2. <span data-ttu-id="5ba40-194">Запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5ba40-194">Run hello application.</span></span>

3. <span data-ttu-id="5ba40-195">Введите имя узла, который состоит из имени пользователя администратора кластера hello и hello открытому DNS-имени первый образец hello в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="5ba40-195">Enter a host name that is comprised of hello cluster admin user name and hello public DNS name of hello first master in hello cluster.</span></span> <span data-ttu-id="5ba40-196">Hello **имя узла** выглядит примерно`azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="5ba40-196">hello **Host Name** looks similar too`azureuser@PublicDNSName`.</span></span> <span data-ttu-id="5ba40-197">Введите 2200 hello **порт**.</span><span class="sxs-lookup"><span data-stu-id="5ba40-197">Enter 2200 for hello **Port**.</span></span>

    ![Конфигурация PuTTY 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="5ba40-199">Выберите **SSH > Проверка подлинности**. Добавьте путь tooyour файл закрытого ключа (формат .ppk) для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5ba40-199">Select **SSH > Auth**. Add a path tooyour private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="5ba40-200">Можно использовать это средство, например [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate, этот файл из hello SSH ключа используется toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5ba40-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate this file from hello SSH key used toocreate hello cluster.</span></span>

    ![Конфигурация PuTTY 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="5ba40-202">Выберите **SSH > туннели** и настройте ниже hello пересылаться порты:</span><span class="sxs-lookup"><span data-stu-id="5ba40-202">Select **SSH > Tunnels** and configure hello following forwarded ports:</span></span>

    * <span data-ttu-id="5ba40-203">**исходный порт** — используйте порт 80 для DC/OS или 2375 для Swarm;</span><span class="sxs-lookup"><span data-stu-id="5ba40-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="5ba40-204">**конечный порт** — используйте localhost:80 для DC/OS или localhost:2375 для Swarm.</span><span class="sxs-lookup"><span data-stu-id="5ba40-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="5ba40-205">Следующий пример Hello настроен для контроллера домена/OS, но будет выглядеть для помощью Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="5ba40-205">hello following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ba40-206">При создании этого туннеля нужно, чтобы порт 80 больше нигде не использовался.</span><span class="sxs-lookup"><span data-stu-id="5ba40-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Конфигурация PuTTY 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="5ba40-208">Закончив, нажмите кнопку **сеанса > Сохранить** конфигурация подключения toosave hello.</span><span class="sxs-lookup"><span data-stu-id="5ba40-208">When you're finished, click **Session > Save** toosave hello connection configuration.</span></span>

7. <span data-ttu-id="5ba40-209">tooconnect toohello PuTTY сеанс, нажмите кнопку **откройте**.</span><span class="sxs-lookup"><span data-stu-id="5ba40-209">tooconnect toohello PuTTY session, click **Open**.</span></span> <span data-ttu-id="5ba40-210">При подключении, вы увидите, что конфигурация порта hello в журнале событий PuTTY hello.</span><span class="sxs-lookup"><span data-stu-id="5ba40-210">When you connect, you can see hello port configuration in hello PuTTY event log.</span></span>

    ![Журнал событий PuTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="5ba40-212">После настройки туннеля hello для контроллера домена/OS, доступ к hello связанных конечных точек по адресу:</span><span class="sxs-lookup"><span data-stu-id="5ba40-212">After you've configured hello tunnel for DC/OS, you can access hello related endpoints at:</span></span>

* <span data-ttu-id="5ba40-213">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="5ba40-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="5ba40-214">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="5ba40-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="5ba40-215">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="5ba40-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="5ba40-216">После настройки туннеля hello для помощью Docker Swarm Откройте ваш tooconfigure параметры Windows системную переменную среды с именем `DOCKER_HOST` со значением `:2375`.</span><span class="sxs-lookup"><span data-stu-id="5ba40-216">After you've configured hello tunnel for Docker Swarm, open your Windows settings tooconfigure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="5ba40-217">Затем можно обращаться из кластера группу мелких объектов hello hello Docker CLI.</span><span class="sxs-lookup"><span data-stu-id="5ba40-217">Then, you can access hello Swarm cluster through hello Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ba40-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ba40-218">Next steps</span></span>
<span data-ttu-id="5ba40-219">Развертывание контейнеров в кластере и управление ими.</span><span class="sxs-lookup"><span data-stu-id="5ba40-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="5ba40-220">Работа со службой контейнеров Azure и Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5ba40-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="5ba40-221">Работа со службой контейнеров Azure и DC/OS</span><span class="sxs-lookup"><span data-stu-id="5ba40-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="5ba40-222">Работа с hello контейнера службы Azure и помощью Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="5ba40-222">Work with hello Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

