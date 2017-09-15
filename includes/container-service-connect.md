# <a name="make-a-remote-connection-to-a-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="a16b2-101">Создание удаленного подключения к кластеру Kubernetes, DC/OS или Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="a16b2-101">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="a16b2-102">После создания кластера службы контейнеров Azure необходимо подключиться к кластеру, чтобы развертывать рабочие нагрузки и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="a16b2-102">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span></span> <span data-ttu-id="a16b2-103">В этой статье описывается подключение к главной виртуальной машине кластера с удаленного компьютера.</span><span class="sxs-lookup"><span data-stu-id="a16b2-103">This article describes how to connect to the master VM of the cluster from a remote computer.</span></span> 

<span data-ttu-id="a16b2-104">Кластеры Kubernetes, DC/OS и Docker Swarm предоставляют конечные точки HTTP локально.</span><span class="sxs-lookup"><span data-stu-id="a16b2-104">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="a16b2-105">При использовании Kubernetes к этой конечной точке предоставляется безопасный доступ через Интернет, и к ней можно обратиться, выполнив команду `kubectl` в программе командной строки на любом компьютере, подключенном к Интернету.</span><span class="sxs-lookup"><span data-stu-id="a16b2-105">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="a16b2-106">Для DC/OS и Docker Swarm мы советуем создать туннель Secure Shell (SSH) от локального компьютера к системе управления кластером.</span><span class="sxs-lookup"><span data-stu-id="a16b2-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer to the cluster management system.</span></span> <span data-ttu-id="a16b2-107">После установления туннеля можно выполнять команды, которые используют конечные точки HTTP, и просматривать веб-интерфейс оркестратора (при наличии) из локальной системы.</span><span class="sxs-lookup"><span data-stu-id="a16b2-107">After the tunnel is established, you can run commands which use the HTTP endpoints and view the orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a16b2-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a16b2-108">Prerequisites</span></span>

* <span data-ttu-id="a16b2-109">Кластер Kubernetes, DC/OS или Docker Swarm, [развернутый в службе контейнеров Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a16b2-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="a16b2-110">Файл закрытого ключа RSA (SSH), соответствующий открытому ключу, добавленному в кластер во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="a16b2-110">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span></span> <span data-ttu-id="a16b2-111">В этих командах предполагается, что закрытый ключ SSH хранится на вашем компьютере в папке `$HOME/.ssh/id_rsa`.</span><span class="sxs-lookup"><span data-stu-id="a16b2-111">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="a16b2-112">Дополнительные сведения см. в статьях [Как создать и использовать пару из открытого и закрытого ключей SSH для виртуальных машин Linux в Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md) и [Использование ключей SSH с Windows в Azure](../articles/virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="a16b2-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="a16b2-113">Если SSH-подключение не работает, может потребоваться [сбросить ключи SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="a16b2-113">If the SSH connection isn't working, you may need to [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-to-a-kubernetes-cluster"></a><span data-ttu-id="a16b2-114">Подключение к кластеру Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a16b2-114">Connect to a Kubernetes cluster</span></span>

<span data-ttu-id="a16b2-115">Выполните следующие действия, чтобы установить и настроить `kubectl` на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a16b2-115">Follow these steps to install and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="a16b2-116">В Linux или macOS может потребоваться выполнить команды из этого раздела с помощью `sudo`.</span><span class="sxs-lookup"><span data-stu-id="a16b2-116">On Linux or macOS, you might need to run the commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="a16b2-117">Установка kubectl</span><span class="sxs-lookup"><span data-stu-id="a16b2-117">Install kubectl</span></span>
<span data-ttu-id="a16b2-118">Один из способов установки этого инструмента — с помощью команды `az acs kubernetes install-cli` в Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a16b2-118">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="a16b2-119">Чтобы выполнить эту команду, обязательно [установите](/cli/azure/install-az-cli2) последнюю версию Azure CLI 2.0 и войдите в учетную запись Azure с помощью команды `az login`.</span><span class="sxs-lookup"><span data-stu-id="a16b2-119">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="a16b2-120">Последнюю версию клиента `kubectl` можно также скачать со страницы [списка выпусков Kubernetes](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="a16b2-120">Alternatively, you can download the latest `kubectl` client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="a16b2-121">Дополнительные сведения см. в разделе [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Установка и настройка kubectl).</span><span class="sxs-lookup"><span data-stu-id="a16b2-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="a16b2-122">Скачивание учетных данных кластера</span><span class="sxs-lookup"><span data-stu-id="a16b2-122">Download cluster credentials</span></span>
<span data-ttu-id="a16b2-123">Когда средство `kubectl` будет установлено, скопируйте на локальный компьютер учетные данные кластера.</span><span class="sxs-lookup"><span data-stu-id="a16b2-123">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span></span> <span data-ttu-id="a16b2-124">Чтобы получить учетные данные, выполните команду `az acs kubernetes get-credentials`.</span><span class="sxs-lookup"><span data-stu-id="a16b2-124">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="a16b2-125">Передайте имя группы ресурсов и имя ресурса службы контейнеров:</span><span class="sxs-lookup"><span data-stu-id="a16b2-125">Pass the name of the resource group and the name of the container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="a16b2-126">Эта команда загрузит учетные данные кластера в папку `$HOME/.kube/config`, где средство `kubectl` будет их искать.</span><span class="sxs-lookup"><span data-stu-id="a16b2-126">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span></span>

<span data-ttu-id="a16b2-127">Вы также можете с помощью `scp` безопасно скопировать файл на локальный компьютер из папки `$HOME/.kube/config` на главной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a16b2-127">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span></span> <span data-ttu-id="a16b2-128">Например:</span><span class="sxs-lookup"><span data-stu-id="a16b2-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="a16b2-129">При работе в Windows можно использовать Bash на Ubuntu в Windows, клиент безопасного копирования файлов PuTTy или аналогичное средство.</span><span class="sxs-lookup"><span data-stu-id="a16b2-129">If you are on Windows, you can use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="a16b2-130">Использование kubectl</span><span class="sxs-lookup"><span data-stu-id="a16b2-130">Use kubectl</span></span>

<span data-ttu-id="a16b2-131">После того как вы настроите `kubectl`, проверьте подключение, просмотрев список узлов в кластере:</span><span class="sxs-lookup"><span data-stu-id="a16b2-131">Once you have `kubectl` configured, test the connection by listing the nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="a16b2-132">Можно использовать другие команды `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="a16b2-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="a16b2-133">Например, вы можете просмотреть панель мониторинга Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a16b2-133">For example, you can view the Kubernetes Dashboard.</span></span> <span data-ttu-id="a16b2-134">Сначала запустите прокси для сервера Kubernetes API:</span><span class="sxs-lookup"><span data-stu-id="a16b2-134">First, run a proxy to the Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="a16b2-135">Теперь пользовательский интерфейс Kubernetes доступен по адресу `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="a16b2-135">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="a16b2-136">Дополнительные сведения см. в статье о [быстром запуске Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="a16b2-136">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-to-a-dcos-or-swarm-cluster"></a><span data-ttu-id="a16b2-137">Подключение к кластеру DC/OS или Swarm</span><span class="sxs-lookup"><span data-stu-id="a16b2-137">Connect to a DC/OS or Swarm cluster</span></span>

<span data-ttu-id="a16b2-138">Чтобы использовать кластеры DC/OS и Docker Swarm, развернутые в службе контейнеров Azure, создайте туннель SSH из локальной системы Linux, macOS или Windows.</span><span class="sxs-lookup"><span data-stu-id="a16b2-138">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="a16b2-139">В статье рассматриваются инструкции по туннелированию TCP-трафика по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="a16b2-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="a16b2-140">Кроме того, можно запустить интерактивный сеанс SSH с одной из внутренних систем управления кластером, но мы не рекомендуем это делать.</span><span class="sxs-lookup"><span data-stu-id="a16b2-140">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="a16b2-141">Работа непосредственно во внутренней системе, вы рискуете случайно изменить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="a16b2-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="a16b2-142">Создание туннеля SSH в Linux или macOS</span><span class="sxs-lookup"><span data-stu-id="a16b2-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="a16b2-143">Во-первых, чтобы создать туннель SSH в любой из этих операционных систем, вам нужно узнать общедоступное DNS-имя главного сервера с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a16b2-143">The first thing that you do when you create an SSH tunnel on Linux or macOS is to locate the public DNS name of the load-balanced masters.</span></span> <span data-ttu-id="a16b2-144">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a16b2-144">Follow these steps:</span></span>


1. <span data-ttu-id="a16b2-145">На [портале Azure](https://portal.azure.com) перейдите в группу ресурсов, содержащую кластер службы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="a16b2-145">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span></span> <span data-ttu-id="a16b2-146">Разверните группу ресурсов, чтобы отображались все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a16b2-146">Expand the resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="a16b2-147">Щелкните ресурс **службы контейнеров** и нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="a16b2-147">Click the **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="a16b2-148">В разделе **Основное** отобразится **полное доменное имя главного кластера**.</span><span class="sxs-lookup"><span data-stu-id="a16b2-148">The **Master FQDN** of the cluster appears under **Essentials**.</span></span> <span data-ttu-id="a16b2-149">Сохраните это имя для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="a16b2-149">Save this name for later use.</span></span> 

    ![Общедоступное DNS-имя](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="a16b2-151">Кроме того, в службе контейнеров можно выполнить команду `az acs show`</span><span class="sxs-lookup"><span data-stu-id="a16b2-151">Alternatively, run the `az acs show` command on your container service.</span></span> <span data-ttu-id="a16b2-152">и в выходных данных найти свойство **Master Profile:fqdn**.</span><span class="sxs-lookup"><span data-stu-id="a16b2-152">Look for the **Master Profile:fqdn** property in the command output.</span></span>

3. <span data-ttu-id="a16b2-153">Теперь откройте оболочку и выполните команду `ssh`, указав следующие значения:</span><span class="sxs-lookup"><span data-stu-id="a16b2-153">Now open a shell and run the `ssh` command by specifying the following values:</span></span> 

    <span data-ttu-id="a16b2-154">**LOCAL_PORT** — TCP-порт на стороне службы, к которому подключается туннель.</span><span class="sxs-lookup"><span data-stu-id="a16b2-154">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span></span> <span data-ttu-id="a16b2-155">Для Swarm задайте порт 2375,</span><span class="sxs-lookup"><span data-stu-id="a16b2-155">For Swarm, set this to 2375.</span></span> <span data-ttu-id="a16b2-156">а для DC/OS — 80.</span><span class="sxs-lookup"><span data-stu-id="a16b2-156">For DC/OS, set this to 80.</span></span> 
    <span data-ttu-id="a16b2-157">**REMOTE_PORT** — порт конечной точки, к которой требуется предоставить доступ.</span><span class="sxs-lookup"><span data-stu-id="a16b2-157">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span></span> <span data-ttu-id="a16b2-158">Для Swarm используется порт 2375.</span><span class="sxs-lookup"><span data-stu-id="a16b2-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="a16b2-159">Для DC/OS используется порт 80.</span><span class="sxs-lookup"><span data-stu-id="a16b2-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="a16b2-160">**USERNAME** — имя пользователя, указанное при развертывании кластера.</span><span class="sxs-lookup"><span data-stu-id="a16b2-160">**USERNAME** is the user name that was provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="a16b2-161">**DNSPREFIX** — префикс DNS, указанный при развертывании кластера.</span><span class="sxs-lookup"><span data-stu-id="a16b2-161">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="a16b2-162">**REGION** — регион, в котором расположена ваша группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a16b2-162">**REGION** is the region in which your resource group is located.</span></span>  
    <span data-ttu-id="a16b2-163">**PATH_TO_PRIVATE_KEY** (необязательно) — это путь к закрытому ключу, который соответствует открытому ключу, указанному во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="a16b2-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span></span> <span data-ttu-id="a16b2-164">Используйте этот параметр с флагом `-i`.</span><span class="sxs-lookup"><span data-stu-id="a16b2-164">Use this option with the `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="a16b2-165">Для SSH-подключения используется порт 2200, а не стандартный 22.</span><span class="sxs-lookup"><span data-stu-id="a16b2-165">The SSH connection port is 2200 and not the standard port 22.</span></span> <span data-ttu-id="a16b2-166">В кластере с несколькими главными виртуальными машинами этот порт используется для подключения к первой главной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a16b2-166">In a cluster with more than one master VM, this is the connection port to the first master VM.</span></span>
  > 

  <span data-ttu-id="a16b2-167">Команда завершится без выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a16b2-167">The command returns without output.</span></span>

<span data-ttu-id="a16b2-168">Примеры для кластеров DC/OS и Swarm приведены в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="a16b2-168">See the examples for DC/OS and Swarm in the following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="a16b2-169">Туннель DC/OS</span><span class="sxs-lookup"><span data-stu-id="a16b2-169">DC/OS tunnel</span></span>
<span data-ttu-id="a16b2-170">Чтобы открыть туннель для конечных точек DC/ОС, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a16b2-170">To open a tunnel for DC/OS endpoints, run a command like the following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="a16b2-171">Убедитесь, что у вас нет другого локального процесса, привязанного к порту 80.</span><span class="sxs-lookup"><span data-stu-id="a16b2-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="a16b2-172">При необходимости в качестве локального порта вместо 80 можно указать, например, 8080,</span><span class="sxs-lookup"><span data-stu-id="a16b2-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="a16b2-173">но в этом случае некоторые ссылки в пользовательском веб-интерфейсе могут не работать.</span><span class="sxs-lookup"><span data-stu-id="a16b2-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="a16b2-174">Теперь вы можете подключаться к конечным точкам DC/OS из локальной системы, используя следующие URL-адреса (при условии, что в качестве локального порта используется 80):</span><span class="sxs-lookup"><span data-stu-id="a16b2-174">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="a16b2-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="a16b2-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="a16b2-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="a16b2-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="a16b2-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="a16b2-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="a16b2-178">Аналогичным образом через этот туннель можно подключаться к интерфейсам REST API каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="a16b2-178">Similarly, you can reach the rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="a16b2-179">Туннель Swarm</span><span class="sxs-lookup"><span data-stu-id="a16b2-179">Swarm tunnel</span></span>
<span data-ttu-id="a16b2-180">Чтобы открыть туннель для конечной точки Swarm, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a16b2-180">To open a tunnel to the Swarm endpoint, run a command like the following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="a16b2-181">Убедитесь, что у вас нет другого локального процесса, привязанного к порту 2375.</span><span class="sxs-lookup"><span data-stu-id="a16b2-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="a16b2-182">Например, если управляющая программа Docker выполняется локально, по умолчанию используется порт 2375.</span><span class="sxs-lookup"><span data-stu-id="a16b2-182">For example, if you are running the Docker daemon locally, it's set by default to use port 2375.</span></span> <span data-ttu-id="a16b2-183">При необходимости вместо 2375 можно указать локальный порт.</span><span class="sxs-lookup"><span data-stu-id="a16b2-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="a16b2-184">Теперь доступ к кластеру Docker Swarm можно получить с помощью интерфейса командной строки Docker (Docker CLI) в локальной системе.</span><span class="sxs-lookup"><span data-stu-id="a16b2-184">Now you can access the Docker Swarm cluster using the Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="a16b2-185">Инструкции по установке Docker см. в [этом руководстве](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="a16b2-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="a16b2-186">Задайте для переменной среды DOCKER_HOST значение локального порта, настроенное для туннеля.</span><span class="sxs-lookup"><span data-stu-id="a16b2-186">Set your DOCKER_HOST environment variable to the local port you configured for the tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="a16b2-187">Выполните команды Docker, открывающие туннель к кластеру Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="a16b2-187">Run Docker commands that tunnel to the Docker Swarm cluster.</span></span> <span data-ttu-id="a16b2-188">Например:</span><span class="sxs-lookup"><span data-stu-id="a16b2-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="a16b2-189">Создание туннеля SSH в Windows</span><span class="sxs-lookup"><span data-stu-id="a16b2-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="a16b2-190">Создавать туннели SSH в Windows можно несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="a16b2-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="a16b2-191">Если вы используете Bash на Ubuntu в Windows или аналогичное средство, для macOS и Linux необходимо выполнить инструкции по туннелированию SSH, приведенные ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a16b2-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow the SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="a16b2-192">В качестве альтернативы для Windows в этом разделе описывается, как создать туннель с помощью PuTTY.</span><span class="sxs-lookup"><span data-stu-id="a16b2-192">As an alternative on Windows, this section describes how to use PuTTY to create the tunnel.</span></span>

1. <span data-ttu-id="a16b2-193">[Скачайте PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) в операционную систему Windows.</span><span class="sxs-lookup"><span data-stu-id="a16b2-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span></span>

2. <span data-ttu-id="a16b2-194">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="a16b2-194">Run the application.</span></span>

3. <span data-ttu-id="a16b2-195">Введите имя узла, которое состоит из имени администратора кластера и общедоступного DNS-имени первого главного сервера в кластере.</span><span class="sxs-lookup"><span data-stu-id="a16b2-195">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span></span> <span data-ttu-id="a16b2-196">**Имя узла** будет указано в этом формате: `azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="a16b2-196">The **Host Name** looks similar to `azureuser@PublicDNSName`.</span></span> <span data-ttu-id="a16b2-197">В поле **Порт**введите значение 2200.</span><span class="sxs-lookup"><span data-stu-id="a16b2-197">Enter 2200 for the **Port**.</span></span>

    ![Конфигурация PuTTY 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="a16b2-199">Выберите **SSH > Проверка подлинности**.</span><span class="sxs-lookup"><span data-stu-id="a16b2-199">Select **SSH > Auth**.</span></span> <span data-ttu-id="a16b2-200">Добавьте путь к файлу закрытого ключа (в формате PPK) для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="a16b2-200">Add a path to your private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="a16b2-201">Чтобы создать этот файл из SSH-ключа, используемого для создания кластера, можно использовать средство [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="a16b2-201">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span></span>

    ![Конфигурация PuTTY 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="a16b2-203">Выберите **SSH > Туннели** и настройте следующие порты для перенаправления:</span><span class="sxs-lookup"><span data-stu-id="a16b2-203">Select **SSH > Tunnels** and configure the following forwarded ports:</span></span>

    * <span data-ttu-id="a16b2-204">**исходный порт** — используйте порт 80 для DC/OS или 2375 для Swarm;</span><span class="sxs-lookup"><span data-stu-id="a16b2-204">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="a16b2-205">**конечный порт** — используйте localhost:80 для DC/OS или localhost:2375 для Swarm.</span><span class="sxs-lookup"><span data-stu-id="a16b2-205">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="a16b2-206">В следующем примере выполняется настройка для DC/OS. Для Docker Swarm эта процедура аналогична.</span><span class="sxs-lookup"><span data-stu-id="a16b2-206">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a16b2-207">При создании этого туннеля нужно, чтобы порт 80 больше нигде не использовался.</span><span class="sxs-lookup"><span data-stu-id="a16b2-207">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Конфигурация PuTTY 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="a16b2-209">По завершении выберите **Сеанс > Сохранить**, чтобы сохранить конфигурацию подключения.</span><span class="sxs-lookup"><span data-stu-id="a16b2-209">When you're finished, click **Session > Save** to save the connection configuration.</span></span>

7. <span data-ttu-id="a16b2-210">Чтобы подключиться к сеансу PuTTY, нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="a16b2-210">To connect to the PuTTY session, click **Open**.</span></span> <span data-ttu-id="a16b2-211">После подключения конфигурацию порта можно просмотреть в журнале событий PuTTY.</span><span class="sxs-lookup"><span data-stu-id="a16b2-211">When you connect, you can see the port configuration in the PuTTY event log.</span></span>

    ![Журнал событий PuTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="a16b2-213">После настройки туннеля для DC/OS связанные конечные точки будут доступны по такому адресу:</span><span class="sxs-lookup"><span data-stu-id="a16b2-213">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span></span>

* <span data-ttu-id="a16b2-214">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="a16b2-214">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="a16b2-215">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="a16b2-215">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="a16b2-216">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="a16b2-216">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="a16b2-217">После настройки туннеля для Docker Swarm откройте параметры Windows, чтобы указать значение `:2375` для системной переменной среды `DOCKER_HOST`.</span><span class="sxs-lookup"><span data-stu-id="a16b2-217">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="a16b2-218">Теперь вы можете обращаться к кластеру Swarm из интерфейса командной строки Docker.</span><span class="sxs-lookup"><span data-stu-id="a16b2-218">Then, you can access the Swarm cluster through the Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a16b2-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a16b2-219">Next steps</span></span>
<span data-ttu-id="a16b2-220">Развертывание контейнеров в кластере и управление ими.</span><span class="sxs-lookup"><span data-stu-id="a16b2-220">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="a16b2-221">Работа со службой контейнеров Azure и Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a16b2-221">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="a16b2-222">Работа со службой контейнеров Azure и DC/OS</span><span class="sxs-lookup"><span data-stu-id="a16b2-222">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="a16b2-223">Работа со службой контейнеров Azure и Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="a16b2-223">Work with the Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

