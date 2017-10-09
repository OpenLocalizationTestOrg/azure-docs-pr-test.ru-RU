
* [<span data-ttu-id="c238b-101">Быстрое создание виртуальной машины в Azure</span><span class="sxs-lookup"><span data-stu-id="c238b-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="c238b-102">Развертывание виртуальной машины в Azure из шаблона</span><span class="sxs-lookup"><span data-stu-id="c238b-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="c238b-103">Создание виртуальной машины из настраиваемого образа</span><span class="sxs-lookup"><span data-stu-id="c238b-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="c238b-104">Развертывание виртуальной машины, которая использует виртуальную сеть и балансировщик нагрузки</span><span class="sxs-lookup"><span data-stu-id="c238b-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="c238b-105">Удаление группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="c238b-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="c238b-106">Показать журнал hello для развертывания группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="c238b-106">Show hello log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="c238b-107">Отображение информации о виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="c238b-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="c238b-108">Подключения на основе Linux tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c238b-108">Connect tooa Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="c238b-109">Останов виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c238b-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="c238b-110">Запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c238b-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="c238b-111">Подключение диска с данными</span><span class="sxs-lookup"><span data-stu-id="c238b-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="c238b-112">Подготовка</span><span class="sxs-lookup"><span data-stu-id="c238b-112">Getting ready</span></span>
<span data-ttu-id="c238b-113">Перед использованием hello Azure CLI с группами ресурсов Azure, понадобится подходящую версию Azure CLI toohave hello и учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="c238b-113">Before you can use hello Azure CLI with Azure resource groups, you need toohave hello right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="c238b-114">Если у вас нет hello Azure CLI [установить его](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c238b-114">If you don't have hello Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-too090-or-later"></a><span data-ttu-id="c238b-115">Обновите ваш too0.9.0 Azure CLI версии или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="c238b-115">Update your Azure CLI version too0.9.0 or later</span></span>
<span data-ttu-id="c238b-116">Тип `azure --version` toosee ли вы уже установили версию 0.9.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c238b-116">Type `azure --version` toosee whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="c238b-117">Если ваша версия 0.9.0 или более поздней версии, необходимо tooupdate его с помощью одного из hello собственного установщики или через **npm** , введя `npm update -g azure-cli`.</span><span class="sxs-lookup"><span data-stu-id="c238b-117">If your version is not 0.9.0 or later, you need tooupdate it by using one of hello native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="c238b-118">Можно также запустить Azure CLI как контейнер Docker с помощью следующих hello [образа Docker](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="c238b-118">You can also run Azure CLI as a Docker container by using hello following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="c238b-119">В узел Docker выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="c238b-119">From a Docker host, run hello following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="c238b-120">Настройка учетной записи и подписки Azure</span><span class="sxs-lookup"><span data-stu-id="c238b-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="c238b-121">Если у вас нет подписки Azure, но есть подписка MSDN, то вы можете [активировать преимущества подписчика MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="c238b-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="c238b-122">или подписаться на [бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c238b-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="c238b-123">Теперь [интерактивного входа в учетную запись Azure tooyour](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) , введя `azure login` и следуя hello запрашивает tooyour возможности интерактивного входа в систему учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="c238b-123">Now [log in tooyour Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following hello prompts for an interactive login experience tooyour Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="c238b-124">Если вас есть рабочая идентификатор и известно, что у вас двухфакторная проверка подлинности включена, вы можете **также** использовать `azure login -u` вместе с hello работы или учебы toolog идентификатор в *без* интерактивного сеанса.</span><span class="sxs-lookup"><span data-stu-id="c238b-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with hello work or school ID toolog in *without* an interactive session.</span></span> <span data-ttu-id="c238b-125">Если вы не рабочий или учебный идентификатор, вы можете [создать рабочую или учебную идентификатор из личную учетную запись Майкрософт](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog в hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="c238b-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello same way.</span></span>
>
>

<span data-ttu-id="c238b-126">У вашей учетной записи может быть несколько подписок.</span><span class="sxs-lookup"><span data-stu-id="c238b-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="c238b-127">Их можно указать, введя `azure account list`. Результат может выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c238b-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="c238b-128">Можно задать текущую подписку Azure hello, введя следующее hello.</span><span class="sxs-lookup"><span data-stu-id="c238b-128">You can set hello current Azure subscription by typing hello following.</span></span> <span data-ttu-id="c238b-129">Используйте hello имя или hello идентификатор подписки, имеющего требуется toomanage ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="c238b-129">Use hello subscription name or hello ID that has hello resources you want toomanage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a><span data-ttu-id="c238b-130">Переключить режим группы ресурсов Azure CLI toohello</span><span class="sxs-lookup"><span data-stu-id="c238b-130">Switch toohello Azure CLI resource group mode</span></span>
<span data-ttu-id="c238b-131">По умолчанию hello Azure CLI запускается в режиме управления службы hello (**asm** режиме).</span><span class="sxs-lookup"><span data-stu-id="c238b-131">By default, hello Azure CLI starts in hello service management mode (**asm** mode).</span></span> <span data-ttu-id="c238b-132">Введите следующий режим группы tooresource tooswitch hello.</span><span class="sxs-lookup"><span data-stu-id="c238b-132">Type hello following tooswitch tooresource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="c238b-133">Общая информация о шаблонах ресурсов Azure и группах ресурсов</span><span class="sxs-lookup"><span data-stu-id="c238b-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="c238b-134">Большинство приложений создаются с использованием различных ресурсов. Это может быть комбинация из одной или нескольких виртуальных машин и учетных записей хранения, базы данных SQL, виртуальной сети или сети доставки содержимого.</span><span class="sxs-lookup"><span data-stu-id="c238b-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="c238b-135">Здравствуйте, API управления службы Azure по умолчанию и hello классический портал Azure представлены эти элементы, используя подход по службами.</span><span class="sxs-lookup"><span data-stu-id="c238b-135">hello default Azure service management API and hello Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="c238b-136">Этот подход требует toodeploy и управлять hello отдельных служб по отдельности (или найти другие средства, сделать это), а не как одна Логическая единица развертывания.</span><span class="sxs-lookup"><span data-stu-id="c238b-136">This approach requires you toodeploy and manage hello individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="c238b-137">*Шаблоны Azure Resource Manager*, однако позволяют вам toodeploy эти ресурсы и управлять различных как единое логическое развертывание в декларативной форме.</span><span class="sxs-lookup"><span data-stu-id="c238b-137">*Azure Resource Manager templates*, however, make it possible for you toodeploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="c238b-138">Вместо принудительно указывает, Azure команду toodeploy один за другим, описывающие всего развертывания в файле JSON — все ресурсы hello и связанной конфигурации и параметры развертывания — и сообщить Azure toodeploy эти ресурсы как один Группа.</span><span class="sxs-lookup"><span data-stu-id="c238b-138">Instead of imperatively telling Azure what toodeploy one command after another, you describe your entire deployment in a JSON file -- all of hello resources and associated configuration and deployment parameters -- and tell Azure toodeploy those resources as one group.</span></span>

<span data-ttu-id="c238b-139">Затем можно будет управлять hello всего жизненного цикла hello группы ресурсов с помощью команды управления ресурса Azure CLI для:</span><span class="sxs-lookup"><span data-stu-id="c238b-139">You can then manage hello overall life cycle of hello group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="c238b-140">Остановить, запустить или удалить все ресурсы hello в пределах группы hello сразу.</span><span class="sxs-lookup"><span data-stu-id="c238b-140">Stop, start, or delete all of hello resources within hello group at once.</span></span>
* <span data-ttu-id="c238b-141">Примените toolock правила управления доступом на основе ролей (RBAC) распространение разрешений безопасности на них.</span><span class="sxs-lookup"><span data-stu-id="c238b-141">Apply Role-Based Access Control (RBAC) rules toolock down security permissions on them.</span></span>
* <span data-ttu-id="c238b-142">вести аудит операций;</span><span class="sxs-lookup"><span data-stu-id="c238b-142">Audit operations.</span></span>
* <span data-ttu-id="c238b-143">отмечать ресурсы с помощью дополнительных метаданных для более точного отслеживания.</span><span class="sxs-lookup"><span data-stu-id="c238b-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="c238b-144">Можно узнать многое другое, о группах ресурсов Azure и что можно делать для вас в hello [Обзор диспетчера ресурсов Azure](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c238b-144">You can learn lots more about Azure resource groups and what they can do for you in hello [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="c238b-145">Если вас интересует разработка шаблонов, ознакомьтесь со статьей [Создание шаблонов Azure Resource Manager](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c238b-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="c238b-146"><a id="quick-create-a-vm-in-azure"></a>Задача: быстрое создание виртуальной машины в Azure</span><span class="sxs-lookup"><span data-stu-id="c238b-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="c238b-147">Иногда известно, какой образ, необходимо, и из этого образа виртуальной Машины необходимо в данный момент вас не интересует слишком сильно hello инфраструктуры — возможно tootest что-нибудь на чистой виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="c238b-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about hello infrastructure -- maybe you have tootest something on a clean VM.</span></span> <span data-ttu-id="c238b-148">То есть необходимо toouse hello `azure vm quick-create` команды и передать toocreate необходимые аргументы hello виртуальной Машины и ее инфраструктура.</span><span class="sxs-lookup"><span data-stu-id="c238b-148">That's when you want toouse hello `azure vm quick-create` command, and pass hello arguments necessary toocreate a VM and its infrastructure.</span></span>

<span data-ttu-id="c238b-149">Сначала создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c238b-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="c238b-150">Затем вам понадобится образ.</span><span class="sxs-lookup"><span data-stu-id="c238b-150">Second, you'll need an image.</span></span> <span data-ttu-id="c238b-151">toofind образа с hello Azure CLI см. в разделе [навигация и выбрав образов виртуальных машин Azure с помощью PowerShell и hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c238b-151">toofind an image with hello Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c238b-152">В данной же статье ниже приведен краткий список часто используемых образов.</span><span class="sxs-lookup"><span data-stu-id="c238b-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="c238b-153">В этой задаче по быстрому созданию мы используем образ с номером SKU Stable и издателем CoreOS.</span><span class="sxs-lookup"><span data-stu-id="c238b-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="c238b-154">Для ComputeImageVersion можно просто указать «последние» как параметр в обоих язык шаблона hello и hello Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="c238b-154">For ComputeImageVersion, you can also simply supply 'latest' as hello parameter in both hello template language and in hello Azure CLI.</span></span> <span data-ttu-id="c238b-155">Это позволит tooalways использовать hello последние и обновленной версии образа hello без необходимости toomodify скриптов или шаблонов.</span><span class="sxs-lookup"><span data-stu-id="c238b-155">This will allow you tooalways use hello latest and patched version of hello image without having toomodify your scripts or templates.</span></span> <span data-ttu-id="c238b-156">Такой способ показан ниже.</span><span class="sxs-lookup"><span data-stu-id="c238b-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="c238b-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="c238b-157">PublisherName</span></span> | <span data-ttu-id="c238b-158">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="c238b-158">Offer</span></span> | <span data-ttu-id="c238b-159">Sku</span><span class="sxs-lookup"><span data-stu-id="c238b-159">Sku</span></span> | <span data-ttu-id="c238b-160">Версия</span><span class="sxs-lookup"><span data-stu-id="c238b-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c238b-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="c238b-161">OpenLogic</span></span> |<span data-ttu-id="c238b-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="c238b-162">CentOS</span></span> |<span data-ttu-id="c238b-163">7</span><span class="sxs-lookup"><span data-stu-id="c238b-163">7</span></span> |<span data-ttu-id="c238b-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="c238b-164">7.0.201503</span></span> |
| <span data-ttu-id="c238b-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="c238b-165">OpenLogic</span></span> |<span data-ttu-id="c238b-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="c238b-166">CentOS</span></span> |<span data-ttu-id="c238b-167">7.1.</span><span class="sxs-lookup"><span data-stu-id="c238b-167">7.1</span></span> |<span data-ttu-id="c238b-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="c238b-168">7.1.201504</span></span> |
| <span data-ttu-id="c238b-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c238b-169">CoreOS</span></span> |<span data-ttu-id="c238b-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c238b-170">CoreOS</span></span> |<span data-ttu-id="c238b-171">Beta</span><span class="sxs-lookup"><span data-stu-id="c238b-171">Beta</span></span> |<span data-ttu-id="c238b-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="c238b-172">647.0.0</span></span> |
| <span data-ttu-id="c238b-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c238b-173">CoreOS</span></span> |<span data-ttu-id="c238b-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c238b-174">CoreOS</span></span> |<span data-ttu-id="c238b-175">Stable</span><span class="sxs-lookup"><span data-stu-id="c238b-175">Stable</span></span> |<span data-ttu-id="c238b-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="c238b-176">633.1.0</span></span> |
| <span data-ttu-id="c238b-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="c238b-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="c238b-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="c238b-178">DynamicsNAV</span></span> |<span data-ttu-id="c238b-179">2015</span><span class="sxs-lookup"><span data-stu-id="c238b-179">2015</span></span> |<span data-ttu-id="c238b-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="c238b-180">8.0.40459</span></span> |
| <span data-ttu-id="c238b-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="c238b-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="c238b-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="c238b-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="c238b-183">2013</span><span class="sxs-lookup"><span data-stu-id="c238b-183">2013</span></span> |<span data-ttu-id="c238b-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c238b-184">1.0.0</span></span> |
| <span data-ttu-id="c238b-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="c238b-185">msopentech</span></span> |<span data-ttu-id="c238b-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="c238b-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="c238b-187">Стандартная</span><span class="sxs-lookup"><span data-stu-id="c238b-187">Standard</span></span> |<span data-ttu-id="c238b-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c238b-188">1.0.0</span></span> |
| <span data-ttu-id="c238b-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="c238b-189">msopentech</span></span> |<span data-ttu-id="c238b-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="c238b-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="c238b-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="c238b-191">Enterprise</span></span> |<span data-ttu-id="c238b-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c238b-192">1.0.0</span></span> |
| <span data-ttu-id="c238b-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="c238b-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="c238b-194">SQL2014 WS2012R2</span><span class="sxs-lookup"><span data-stu-id="c238b-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="c238b-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="c238b-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="c238b-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="c238b-196">12.0.2430</span></span> |
| <span data-ttu-id="c238b-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="c238b-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="c238b-198">SQL2014 WS2012R2</span><span class="sxs-lookup"><span data-stu-id="c238b-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="c238b-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="c238b-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="c238b-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="c238b-200">12.0.2430</span></span> |
| <span data-ttu-id="c238b-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="c238b-201">Canonical</span></span> |<span data-ttu-id="c238b-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c238b-202">UbuntuServer</span></span> |<span data-ttu-id="c238b-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="c238b-203">12.04.5-LTS</span></span> |<span data-ttu-id="c238b-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="c238b-204">12.04.201504230</span></span> |
| <span data-ttu-id="c238b-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="c238b-205">Canonical</span></span> |<span data-ttu-id="c238b-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c238b-206">UbuntuServer</span></span> |<span data-ttu-id="c238b-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="c238b-207">14.04.2-LTS</span></span> |<span data-ttu-id="c238b-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="c238b-208">14.04.201503090</span></span> |
| <span data-ttu-id="c238b-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c238b-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="c238b-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c238b-210">WindowsServer</span></span> |<span data-ttu-id="c238b-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="c238b-211">2012-Datacenter</span></span> |<span data-ttu-id="c238b-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="c238b-212">3.0.201503</span></span> |
| <span data-ttu-id="c238b-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c238b-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="c238b-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c238b-214">WindowsServer</span></span> |<span data-ttu-id="c238b-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="c238b-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="c238b-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="c238b-216">4.0.201503</span></span> |
| <span data-ttu-id="c238b-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c238b-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="c238b-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c238b-218">WindowsServer</span></span> |<span data-ttu-id="c238b-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="c238b-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="c238b-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="c238b-220">5.0.201504</span></span> |
| <span data-ttu-id="c238b-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="c238b-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="c238b-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="c238b-222">WindowsServerEssentials</span></span> |<span data-ttu-id="c238b-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="c238b-223">WindowsServerEssentials</span></span> |<span data-ttu-id="c238b-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="c238b-224">1.0.141204</span></span> |
| <span data-ttu-id="c238b-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="c238b-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="c238b-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="c238b-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="c238b-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="c238b-227">2012R2</span></span> |<span data-ttu-id="c238b-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="c238b-228">4.3.4665</span></span> |

<span data-ttu-id="c238b-229">Просто создайте ВМ, введя hello `azure vm quick-create` команда и готовый к hello приглашения.</span><span class="sxs-lookup"><span data-stu-id="c238b-229">Just create your VM by entering hello `azure vm quick-create` command and being ready for hello prompts.</span></span> <span data-ttu-id="c238b-230">Должно отобразиться примерно следующее:</span><span class="sxs-lookup"><span data-stu-id="c238b-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="c238b-231">Теперь вы можете работать в своей новой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c238b-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="c238b-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Задача: развертывание виртуальной машины в Azure из шаблона</span><span class="sxs-lookup"><span data-stu-id="c238b-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="c238b-233">Используйте инструкции hello в этих разделах toodeploy новой виртуальной Машины Azure с помощью шаблона с hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c238b-233">Use hello instructions in these sections toodeploy a new Azure VM by using a template with hello Azure CLI.</span></span> <span data-ttu-id="c238b-234">Этот шаблон создает одну виртуальную машину в новую виртуальную сеть с одной подсетью и в отличие от `azure vm quick-create`, позволяет вам toodescribe выберите точно и повторить его без ошибок.</span><span class="sxs-lookup"><span data-stu-id="c238b-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you toodescribe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="c238b-235">Вот что создает этот шаблон:</span><span class="sxs-lookup"><span data-stu-id="c238b-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a><span data-ttu-id="c238b-236">Шаг 1: Проверьте файл JSON hello для параметров шаблона hello</span><span class="sxs-lookup"><span data-stu-id="c238b-236">Step 1: Examine hello JSON file for hello template parameters</span></span>
<span data-ttu-id="c238b-237">Вот содержимое hello hello JSON-файл для шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="c238b-237">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="c238b-238">(шаблон hello также находится в [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="c238b-238">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="c238b-239">Шаблоны являются гибкими и, поэтому конструктор hello возможно выбрана toogive множество параметров, или выбранный toooffer лишь небольшое путем создания шаблона, более фиксированный.</span><span class="sxs-lookup"><span data-stu-id="c238b-239">Templates are flexible, so hello designer may have chosen toogive you lots of parameters or chosen toooffer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="c238b-240">В порядке toocollect hello информацию, если шаблон hello toopass как параметры, откройте файл шаблона hello (этот раздел содержит встроенный шаблон ниже) и изучите hello **параметры** значения.</span><span class="sxs-lookup"><span data-stu-id="c238b-240">In order toocollect hello information you need toopass hello template as parameters, open hello template file (this topic has a template inline, below) and examine hello **parameters** values.</span></span>

<span data-ttu-id="c238b-241">В этом случае запросит приведенный ниже шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="c238b-241">In this case, hello template below will ask for:</span></span>

* <span data-ttu-id="c238b-242">уникальное имя учетной записи хранения;</span><span class="sxs-lookup"><span data-stu-id="c238b-242">A unique storage account name.</span></span>
* <span data-ttu-id="c238b-243">Имя пользователя администратора для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c238b-243">An admin user name for hello VM.</span></span>
* <span data-ttu-id="c238b-244">пароль;</span><span class="sxs-lookup"><span data-stu-id="c238b-244">A password.</span></span>
* <span data-ttu-id="c238b-245">Имя домена для hello за пределами toouse мира.</span><span class="sxs-lookup"><span data-stu-id="c238b-245">A domain name for hello outside world toouse.</span></span>
* <span data-ttu-id="c238b-246">номер версии Ubuntu Server, который содержится в списке.</span><span class="sxs-lookup"><span data-stu-id="c238b-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="c238b-247">См. дополнительные сведения о [требованиях к имени пользователя и паролю](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="c238b-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="c238b-248">После принятия решения на эти значения, вы будете готовы toocreate группы для и развернуть этот шаблон в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="c238b-248">Once you decide on these values, you're ready toocreate a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="c238b-249">Шаг 2: Создание hello виртуальной машины с помощью шаблона hello</span><span class="sxs-lookup"><span data-stu-id="c238b-249">Step 2: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="c238b-250">После значения параметра готова, необходимо создать группу ресурсов для шаблона-развертывания и затем разверните шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="c238b-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy hello template.</span></span>

<span data-ttu-id="c238b-251">Группа ресурсов hello toocreate, тип `azure group create <group name> <location>` с именем hello группу hello и hello расположение центра обработки данных, в которую будут toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c238b-251">toocreate hello resource group, type `azure group create <group name> <location>` with hello name of hello group you want and hello datacenter location into which you want toodeploy.</span></span> <span data-ttu-id="c238b-252">Затем немедленно отобразится следующее:</span><span class="sxs-lookup"><span data-stu-id="c238b-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="c238b-253">Теперь toocreate hello развертывания, вызовите `azure group deployment create` и передать:</span><span class="sxs-lookup"><span data-stu-id="c238b-253">Now toocreate hello deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="c238b-254">файл шаблона Hello (Если вы сохранили hello выше JSON шаблона tooa локального файла).</span><span class="sxs-lookup"><span data-stu-id="c238b-254">hello template file (if you saved hello above JSON template tooa local file).</span></span>
* <span data-ttu-id="c238b-255">Шаблон URI (если toopoint в файл hello в GitHub или другие веб-адрес).</span><span class="sxs-lookup"><span data-stu-id="c238b-255">A template URI (if you want toopoint at hello file in GitHub or some other web address).</span></span>
* <span data-ttu-id="c238b-256">Группа ресурсов Hello, в которую будут toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c238b-256">hello resource group into which you want toodeploy.</span></span>
* <span data-ttu-id="c238b-257">имя развертывания (необязательно).</span><span class="sxs-lookup"><span data-stu-id="c238b-257">An optional deployment name.</span></span>

<span data-ttu-id="c238b-258">Появится запрос toosupply hello значения параметров в разделе «Параметры» hello hello JSON-файла.</span><span class="sxs-lookup"><span data-stu-id="c238b-258">You will be prompted toosupply hello values of parameters in hello "parameters" section of hello JSON file.</span></span> <span data-ttu-id="c238b-259">При указании значения всех параметров hello развертывание начнет.</span><span class="sxs-lookup"><span data-stu-id="c238b-259">When you have specified all hello parameter values, your deployment will begin.</span></span>

<span data-ttu-id="c238b-260">Пример:</span><span class="sxs-lookup"><span data-stu-id="c238b-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="c238b-261">Вы получите hello следующий тип данных:</span><span class="sxs-lookup"><span data-stu-id="c238b-261">You will receive hello following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <span data-ttu-id="c238b-262"><a id="create-a-custom-vm-image"></a>Задача: создание настраиваемого образа виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c238b-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="c238b-263">Вы уже видели hello базовое использование шаблонов выше, поэтому теперь можно использовать аналогичные инструкции toocreate пользовательских виртуальных Машин из конкретный VHD-файл в Azure с помощью шаблона через hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c238b-263">You've seen hello basic usage of templates above, so now we can use similar instructions toocreate a custom VM from a specific .vhd file in Azure by using a template via hello Azure CLI.</span></span> <span data-ttu-id="c238b-264">Hello различие состоит в том, что этот шаблон создает одну виртуальную машину из указанного виртуального жесткого диска (VHD).</span><span class="sxs-lookup"><span data-stu-id="c238b-264">hello difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="c238b-265">Шаг 1: Проверьте файл JSON hello hello шаблона</span><span class="sxs-lookup"><span data-stu-id="c238b-265">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="c238b-266">Вот содержимое hello hello JSON-файл для шаблона hello, в этом разделе используется в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c238b-266">Here are hello contents of hello JSON file for hello template that this section uses as an example.</span></span> <span data-ttu-id="c238b-267">(шаблон hello также находится в [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="c238b-267">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="c238b-268">Опять же необходимо будет toofind hello значениями, tooenter для параметров hello, у которых нет значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c238b-268">Again, you will need toofind hello values you want tooenter for hello parameters that do not have default values.</span></span> <span data-ttu-id="c238b-269">При запуске hello `azure group deployment create` команды hello Azure CLI предложит вам tooenter эти значения.</span><span class="sxs-lookup"><span data-stu-id="c238b-269">When you run hello `azure group deployment create` command, hello Azure CLI will prompt you tooenter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a><span data-ttu-id="c238b-270">Шаг 2: Получение hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="c238b-270">Step 2: Obtain hello VHD</span></span>
<span data-ttu-id="c238b-271">Очевидно, что для этого вам понадобится VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="c238b-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="c238b-272">Можно использовать один из уже имеющихся в Azure файлов или передать новый.</span><span class="sxs-lookup"><span data-stu-id="c238b-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="c238b-273">Для виртуальной машины под управлением Windows, в разделе [Создание и отправка Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c238b-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="c238b-274">Для виртуальной машины под управлением Linux, в разделе [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c238b-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains hello Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="c238b-275">Шаг 3: Создание hello виртуальной машины с помощью шаблона hello</span><span class="sxs-lookup"><span data-stu-id="c238b-275">Step 3: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="c238b-276">Теперь вы готовы toocreate на hello .vhd основе новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c238b-276">Now you're ready toocreate a new virtual machine based on hello .vhd.</span></span> <span data-ttu-id="c238b-277">Создание группы toodeploy, с помощью `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="c238b-277">Create a group toodeploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="c238b-278">Затем создайте hello развертывания с помощью hello `--template-uri` toocall параметр в шаблоне hello напрямую (или использовать hello `--template-file` параметр toouse файл, который вы сохранили локально).</span><span class="sxs-lookup"><span data-stu-id="c238b-278">Then create hello deployment by using hello `--template-uri` option toocall in hello template directly (or you can use hello `--template-file` option toouse a file that you have saved locally).</span></span> <span data-ttu-id="c238b-279">Обратите внимание, что так как шаблон hello указанного значения по умолчанию, запрашивается только несколько вещей.</span><span class="sxs-lookup"><span data-stu-id="c238b-279">Note that because hello template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="c238b-280">При развертывании шаблона hello в разных местах, возможно возникновение некоторых конфликтами именования со значениями по умолчанию hello (особенно hello DNS-имя, создаваемых).</span><span class="sxs-lookup"><span data-stu-id="c238b-280">If you deploy hello template in different places, you may find that some naming collisions occur with hello default values (particularly hello DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="c238b-281">Выходные данные выглядят примерно hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c238b-281">Output looks something like hello following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <span data-ttu-id="c238b-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Задача: развертывание приложения для нескольких виртуальных машин, которое использует виртуальную сеть и внешний балансировщик нагрузки</span><span class="sxs-lookup"><span data-stu-id="c238b-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="c238b-283">Этот шаблон позволяет toocreate две виртуальные машины в группе балансировки нагрузки и настроить правило балансировки нагрузки на порт 80.</span><span class="sxs-lookup"><span data-stu-id="c238b-283">This template allows you toocreate two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="c238b-284">Кроме того, этот шаблон позволяет развернуть учетную запись хранения, виртуальную сеть, общедоступный IP-адрес, группу доступности и сетевые интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="c238b-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="c238b-285">Выполните эти шаги toodeploy нескольких виртуальных Машин приложение, которое использует виртуальную сеть и Подсистема балансировки нагрузки с помощью шаблона диспетчера ресурсов в репозитории GitHub шаблона hello, посредством команд Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c238b-285">Follow these steps toodeploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in hello GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="c238b-286">Шаг 1: Проверьте файл JSON hello hello шаблона</span><span class="sxs-lookup"><span data-stu-id="c238b-286">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="c238b-287">Вот содержимое hello hello JSON-файл для шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="c238b-287">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="c238b-288">Если требуется hello самую последнюю версию, он был обнаружен [в репозитории GitHub hello для шаблонов](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="c238b-288">If you want hello most recent version, it's located [at hello GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="c238b-289">В этом разделе используется hello `--template-uri` toocall коммутатора в шаблон hello, но можно также использовать hello `--template-file` переключения toopass локальной версии.</span><span class="sxs-lookup"><span data-stu-id="c238b-289">This topic uses hello `--template-uri` switch toocall in hello template, but you can also use hello `--template-file` switch toopass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a><span data-ttu-id="c238b-290">Шаг 2: Создание hello развертывания с помощью шаблона hello</span><span class="sxs-lookup"><span data-stu-id="c238b-290">Step 2: Create hello deployment by using hello template</span></span>
<span data-ttu-id="c238b-291">Создание группы ресурсов для hello шаблона с помощью `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="c238b-291">Create a resource group for hello template by using `azure group create <location>`.</span></span> <span data-ttu-id="c238b-292">Затем создайте развертывание в этой группе ресурсов с помощью `azure group deployment create` и передачи hello группы ресурсов, передав имя развертывания и ответы на экране приветствия для параметров в шаблоне hello, который не имеет значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c238b-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing hello resource group, passing a deployment name, and answering hello prompts for parameters in hello template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="c238b-293">Теперь использовать hello `azure group deployment create` команда и hello `--template-uri` параметр toodeploy hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="c238b-293">Now use hello `azure group deployment create` command and hello `--template-uri` option toodeploy hello template.</span></span> <span data-ttu-id="c238b-294">При появлении запроса введите значения параметров, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c238b-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="c238b-295">Обратите внимание, что этот шаблон развертывает образ Windows Server. При этом он также с легкостью может развернуть любой образ Linux.</span><span class="sxs-lookup"><span data-stu-id="c238b-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="c238b-296">Требуется toocreate Docker кластера с несколькими диспетчерами группу мелких объектов?</span><span class="sxs-lookup"><span data-stu-id="c238b-296">Want toocreate a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="c238b-297">[Вы можете это сделать.](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/)</span><span class="sxs-lookup"><span data-stu-id="c238b-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="c238b-298"><a id="remove-a-resource-group"></a>Задача: удаление группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="c238b-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="c238b-299">Помните, что можно повторно развернуть tooa группы ресурсов, но после этого с помощью одного, его можно удалить с помощью `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="c238b-299">Remember that you can redeploy tooa resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="c238b-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Задача: Показать журнал hello для развертывания группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="c238b-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show hello log for a resource group deployment</span></span>
<span data-ttu-id="c238b-301">Это одно из действий, которое довольно часто используется при создании или использовании шаблонов.</span><span class="sxs-lookup"><span data-stu-id="c238b-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="c238b-302">Hello вызовов toodisplay hello журналы развертывания для группы является `azure group log show <groupname>`, отображающий бит сведения, полезные для понимания того, почему что-то произошло--или не был.</span><span class="sxs-lookup"><span data-stu-id="c238b-302">hello call toodisplay hello deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="c238b-303">(Дополнительные сведения об устранении неполадок развертывания и о возможных проблемах см. в статье об [устранении распространенных ошибок при развертывании Azure с помощью Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md)).</span><span class="sxs-lookup"><span data-stu-id="c238b-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="c238b-304">tootarget конкретных ошибок, например, можно использовать такие средства, как **jq** tooquery вещи, более точно, например какие отдельных ошибок нужно toocorrect.</span><span class="sxs-lookup"><span data-stu-id="c238b-304">tootarget specific failures, for example, you might use tools like **jq** tooquery things a bit more precisely, such as which individual failures you need toocorrect.</span></span> <span data-ttu-id="c238b-305">Hello следующий пример использует **jq** tooparse развертывания в журнале **lbgroup**, которым нужен сбоев.</span><span class="sxs-lookup"><span data-stu-id="c238b-305">hello following example uses **jq** tooparse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="c238b-306">Вы можете быстро обнаружить ошибку, исправить ее и повторить попытку.</span><span class="sxs-lookup"><span data-stu-id="c238b-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="c238b-307">В следующих варианта hello, шаблон hello Создание две виртуальные машины во hello одновременно, создавшего блокировку на hello .vhd.</span><span class="sxs-lookup"><span data-stu-id="c238b-307">In hello following case, hello template had been creating two VMs at hello same time, which created a lock on hello .vhd.</span></span> <span data-ttu-id="c238b-308">(После изменения шаблона hello мы hello успешное развертывание быстро.)</span><span class="sxs-lookup"><span data-stu-id="c238b-308">(After we modified hello template, hello deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="c238b-309"><a id="display-information-about-a-virtual-machine"></a>Задача: отображение информации о виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="c238b-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="c238b-310">Можно просмотреть сведения о конкретных виртуальных машин в группе ресурсов, с помощью hello `azure vm show <groupname> <vmname>` команды.</span><span class="sxs-lookup"><span data-stu-id="c238b-310">You can see information about specific VMs in your resource group by using hello `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="c238b-311">При наличии нескольких виртуальных Машин в группе, сначала может потребоваться hello toolist виртуальных машин в группе с помощью `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="c238b-311">If you have more than one VM in your group, you might first need toolist hello VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="c238b-312">Затем вы можете просмотреть сведения о виртуальной машине myVM1:</span><span class="sxs-lookup"><span data-stu-id="c238b-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="c238b-313">Если tooprogrammatically хранилище и управлять hello выходные данные команды консоли, можно toouse JSON синтаксического анализа средство, например  **[jq](https://github.com/stedolan/jq)**  или  **[jsawk](https://github.com/micha/jsawk)** , или языка библиотеки, которые подходят для задачи «hello».</span><span class="sxs-lookup"><span data-stu-id="c238b-313">If you want tooprogrammatically store and manipulate hello output of your console commands, you may want toouse a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for hello task.</span></span>
>
>

## <span data-ttu-id="c238b-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Задача: Войдите под управлением Linux tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c238b-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on tooa Linux-based virtual machine</span></span>
<span data-ttu-id="c238b-315">Обычно компьютеры Linux являются подключенных toothrough SSH.</span><span class="sxs-lookup"><span data-stu-id="c238b-315">Typically Linux machines are connected toothrough SSH.</span></span> <span data-ttu-id="c238b-316">Дополнительные сведения см. в разделе [как toouse SSH с Linux в Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c238b-316">For more information, see [How toouse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="c238b-317"><a id="stop-a-virtual-machine"></a>Задача: остановка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c238b-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="c238b-318">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c238b-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="c238b-319">Используйте этот параметр tookeep hello виртуальный IP-адрес (VIP) hello виртуальной сети в случае hello последняя виртуальная машина в этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c238b-319">Use this parameter tookeep hello virtual IP (VIP) of hello vnet in case it's hello last VM in that vnet.</span></span> <br><br> <span data-ttu-id="c238b-320">Если вы используете hello `StayProvisioned` параметр, вы будете по-прежнему выставлен счет за hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c238b-320">If you use hello `StayProvisioned` parameter, you'll still be billed for hello VM.</span></span>
>
>

## <span data-ttu-id="c238b-321"><a id="start-a-virtual-machine"></a>Задача: запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c238b-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="c238b-322">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c238b-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="c238b-323"><a id="attach-a-data-disk"></a>Задача: подключение диска данных</span><span class="sxs-lookup"><span data-stu-id="c238b-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="c238b-324">Кроме того, потребуется toodecide tooattach новый диск или один, содержит ли данные.</span><span class="sxs-lookup"><span data-stu-id="c238b-324">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="c238b-325">Для нового диска hello команда создает hello VHD-файл и привязывает его в hello одной команде.</span><span class="sxs-lookup"><span data-stu-id="c238b-325">For a new disk, hello command creates hello .vhd file and attaches it in hello same command.</span></span>

<span data-ttu-id="c238b-326">tooattach новый диск, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c238b-326">tooattach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="c238b-327">tooattach существующий диск данных, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c238b-327">tooattach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="c238b-328">Затем вам потребуется диск toomount hello, как обычно в Linux.</span><span class="sxs-lookup"><span data-stu-id="c238b-328">Then you'll need toomount hello disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c238b-329">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c238b-329">Next steps</span></span>
<span data-ttu-id="c238b-330">Гораздо более примеры использования Azure CLI с hello **arm** режим, в разделе [использование hello Azure CLI для Mac, Linux и Windows с помощью диспетчера ресурсов Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c238b-330">For far more examples of Azure CLI usage with hello **arm** mode, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="c238b-331">toolearn Дополнительные сведения о ресурсах Azure и их основные понятия в разделе [Обзор диспетчера ресурсов Azure](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c238b-331">toolearn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="c238b-332">Дополнительные шаблоны см. на странице [Шаблоны быстрого запуска Azure](https://azure.microsoft.com/documentation/templates/) и в статье [Развертывание популярных платформ приложений с помощью шаблонов Azure Resource Manager](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c238b-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
