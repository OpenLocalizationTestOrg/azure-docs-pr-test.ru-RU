---
title: "aaaDeploy tooLinux приложений Node.js виртуальных машин в Azure"
description: "Узнайте, как toodeploy Node.js приложения tooLinux виртуальных машин в Azure."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a><span data-ttu-id="be8cc-103">Развертывание tooLinux приложений Node.js виртуальных машин в Azure</span><span class="sxs-lookup"><span data-stu-id="be8cc-103">Deploy a Node.js application tooLinux Virtual Machines in Azure</span></span>
<span data-ttu-id="be8cc-104">В этом учебнике показано как tootake приложений Node.js и разверните его tooLinux виртуальные машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="be8cc-104">This tutorial shows how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="be8cc-105">Hello инструкциям этого учебника можно выполнять в любой операционной системе, поддерживающий работу Node.js.</span><span class="sxs-lookup"><span data-stu-id="be8cc-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="be8cc-106">Вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="be8cc-106">You'll learn how to:</span></span>

* <span data-ttu-id="be8cc-107">разветвлять и клонировать репозиторий GitHub с простым приложением TODO;</span><span class="sxs-lookup"><span data-stu-id="be8cc-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="be8cc-108">Создать и настроить две виртуальные машины Linux в Azure toorun hello приложения;</span><span class="sxs-lookup"><span data-stu-id="be8cc-108">Create and configure two Linux virtual machines in Azure toorun hello application;</span></span>
* <span data-ttu-id="be8cc-109">Завершить цикл hello приложения с помощью принудительной отправки обновлений toohello web переднего плана для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="be8cc-109">Iterate on hello application by pushing updates toohello web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="be8cc-110">toocomplete этого учебника требуется учетная запись GitHub и учетной записи Microsoft Azure и hello возможности toouse Git с компьютера разработки.</span><span class="sxs-lookup"><span data-stu-id="be8cc-110">toocomplete this tutorial, you need a GitHub account and a Microsoft Azure account, and hello ability toouse Git from a development machine.</span></span>
> 
> <span data-ttu-id="be8cc-111">Если у вас нет учетной записи GitHub, вы можете зарегистрироваться [здесь](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="be8cc-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="be8cc-112">Если у вас нет учетной записи [Microsoft Azure](https://azure.microsoft.com/), вы можете зарегистрироваться [здесь](https://azure.microsoft.com/pricing/free-trial/) и получить бесплатную ознакомительную версию.</span><span class="sxs-lookup"><span data-stu-id="be8cc-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="be8cc-113">Это также поможет процедуры для регистрации hello [учетную запись Майкрософт](http://account.microsoft.com) Если вы не сделали этого.</span><span class="sxs-lookup"><span data-stu-id="be8cc-113">This will also lead you through hello sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="be8cc-114">Кроме того, если вы являетесь подписчиком Visual Studio, вы можете [активировать свои преимущества MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="be8cc-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="be8cc-115">Если на компьютере разработки не установлен Git и если вы используете компьютер Macintosh или Windows, установите Git с [этого ресурса](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="be8cc-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="be8cc-116">При использовании Linux Установка git с помощью механизма hello, наиболее подходящий для вас, например `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="be8cc-116">If you are using Linux, install git using hello mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a><span data-ttu-id="be8cc-117">Разветвление и клонирование hello приложения TODO</span><span class="sxs-lookup"><span data-stu-id="be8cc-117">Forking and Cloning hello TODO Application</span></span>
<span data-ttu-id="be8cc-118">Hello приложение TODO, используется в этом учебнике реализует простой веб-клиента через экземпляр MongoDB, который отслеживает TODO list.</span><span class="sxs-lookup"><span data-stu-id="be8cc-118">hello TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="be8cc-119">После входа в tooGitHub go [здесь](https://github.com/stepro/node-todo) toofind hello приложения и его с помощью ссылки hello в правом верхнем углу hello ветвления.</span><span class="sxs-lookup"><span data-stu-id="be8cc-119">After signing in tooGitHub, go [here](https://github.com/stepro/node-todo) toofind hello application and fork it using hello link in hello top right.</span></span> <span data-ttu-id="be8cc-120">Так вы создадите в своей учетной записи репозиторий с именем *имя_учетной_записи*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="be8cc-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="be8cc-121">Теперь клонируйте этот репозиторий на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="be8cc-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="be8cc-122">Мы будем использовать этот локальный клон репозитория hello немного позже при внесении изменений в исходный код toohello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-122">We'll use this local clone of hello repository a little later when making changes toohello source code.</span></span>

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a><span data-ttu-id="be8cc-123">Создание и настройка виртуальных машин Linux hello</span><span class="sxs-lookup"><span data-stu-id="be8cc-123">Creating and Configuring hello Linux Virtual Machines</span></span>
<span data-ttu-id="be8cc-124">Azure имеет хорошую поддержку вычислений с использованием виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="be8cc-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="be8cc-125">Эта часть hello учебника показано, как можно легко запустить две виртуальные машины Linux и развертывать toothem приложения hello TODO, выполнение веб-клиентом hello на одном и hello MongoDB экземпляра на другой hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-125">This part of hello tutorial shows how you can easily spin up two Linux virtual machines and deploy hello TODO application toothem, running hello web frontend on one and hello MongoDB instance on hello other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="be8cc-126">Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="be8cc-126">Creating Virtual Machines</span></span>
<span data-ttu-id="be8cc-127">Hello простым способом toocreate новую виртуальную машину в Azure — toouse hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="be8cc-127">hello easiest way toocreate a new virtual machine in Azure is toouse hello Azure Portal.</span></span> <span data-ttu-id="be8cc-128">Нажмите кнопку [здесь](https://portal.azure.com) toosign в и запустите hello портала Azure в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="be8cc-128">Click [here](https://portal.azure.com) toosign in and launch hello Azure Portal in your web browser.</span></span> <span data-ttu-id="be8cc-129">Сразу после загрузки hello портал Azure, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-129">Once hello Azure Portal has loaded, complete hello following steps:</span></span>

* <span data-ttu-id="be8cc-130">Нажмите кнопку hello «+ создать» связи;</span><span class="sxs-lookup"><span data-stu-id="be8cc-130">Click hello "+ New" link;</span></span>
* <span data-ttu-id="be8cc-131">Выберите категории «Вычисления» hello и выберите «Ubuntu Server 14.04 LTS»;</span><span class="sxs-lookup"><span data-stu-id="be8cc-131">Pick hello "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="be8cc-132">Выберите модель развертывания «диспетчер ресурсов» hello и нажмите кнопку «Создать»;</span><span class="sxs-lookup"><span data-stu-id="be8cc-132">Select hello "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="be8cc-133">Заполните основы hello следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="be8cc-133">Fill in hello basics following these guidelines:</span></span>
  * <span data-ttu-id="be8cc-134">Укажите имя, которое позже сможете легко узнать.</span><span class="sxs-lookup"><span data-stu-id="be8cc-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="be8cc-135">В целях этого руководства выберите проверку подлинности с использованием пароля.</span><span class="sxs-lookup"><span data-stu-id="be8cc-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="be8cc-136">Создайте новую группу ресурсов с узнаваемым именем.</span><span class="sxs-lookup"><span data-stu-id="be8cc-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="be8cc-137">Для hello размер виртуальной машины «Standard A1» является неплохим выбором для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="be8cc-137">For hello Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="be8cc-138">Для дополнительных параметров убедитесь, что тип диска hello «Standard» и принять Здравствуйте, все остальные значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="be8cc-138">For additional settings, ensure hello disk type is "Standard" and accept all hello remaining defaults.</span></span>
* <span data-ttu-id="be8cc-139">Начнем с создания приветствия на странице сводки hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-139">Kick off hello creation on hello summary page.</span></span>

<span data-ttu-id="be8cc-140">Выполнить hello выше обработки дважды toocreate двух виртуальных машин Linux: для веб-клиентом hello и для экземпляра MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-140">Perform hello above process twice toocreate two Linux virtual machines, one for hello web frontend and one for hello MongoDB instance.</span></span> <span data-ttu-id="be8cc-141">Создание виртуальных машин hello займет около 5 – 10 минут.</span><span class="sxs-lookup"><span data-stu-id="be8cc-141">Creation of hello virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="be8cc-142">Назначение DNS-записи для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="be8cc-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="be8cc-143">Виртуальные машины, созданные в Azure, по умолчанию доступны только по общедоступному IP-адресу, например 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="be8cc-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="be8cc-144">Сделаем hello машины более понятными, назначив их DNS-записей.</span><span class="sxs-lookup"><span data-stu-id="be8cc-144">Let's make hello machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="be8cc-145">После портала hello указывает, что hello виртуальных машин были созданы, щелкните ссылку «Виртуальные машины» hello в панель переходов слева hello и найдите компьютеры.</span><span class="sxs-lookup"><span data-stu-id="be8cc-145">Once hello portal indicates that hello virtual machines have been created, click on hello "Virtual machines" link in hello left navbar and locate your machines.</span></span> <span data-ttu-id="be8cc-146">Для каждой виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="be8cc-146">For each machine:</span></span>

* <span data-ttu-id="be8cc-147">Найдите вкладку hello Essentials и щелкните hello общедоступный IP-адрес;</span><span class="sxs-lookup"><span data-stu-id="be8cc-147">Locate hello Essentials tab and click on hello Public IP Address;</span></span>
* <span data-ttu-id="be8cc-148">В hello открытый IP-адрес назначьте метка DNS-имени и сохраните.</span><span class="sxs-lookup"><span data-stu-id="be8cc-148">In hello public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="be8cc-149">Hello портала будет убедитесь, что заданные hello имя доступно.</span><span class="sxs-lookup"><span data-stu-id="be8cc-149">hello portal will ensure that hello name you specify is available.</span></span> <span data-ttu-id="be8cc-150">После сохранения конфигурации hello, виртуальные машины будут иметь имена узлов аналогичные слишком`machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="be8cc-150">After saving hello configuration, your virtual machines will have host names similar too`machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-toohello-virtual-machines"></a><span data-ttu-id="be8cc-151">Подключение toohello виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="be8cc-151">Connecting toohello Virtual Machines</span></span>
<span data-ttu-id="be8cc-152">Если виртуальные машины были подготовлены, они были предварительно настроенных tooallow удаленные подключения через SSH.</span><span class="sxs-lookup"><span data-stu-id="be8cc-152">When your virtual machines were provisioned, they were pre-configured tooallow remote connections over SSH.</span></span> <span data-ttu-id="be8cc-153">Это механизм hello, мы будем использовать tooconfigure hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="be8cc-153">This is hello mechanism we will use tooconfigure hello virtual machines.</span></span> <span data-ttu-id="be8cc-154">Если вы используете Windows для разработки, если вы не сделали этого потребуется tooget клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="be8cc-154">If you are using Windows for your development, you will need tooget an SSH client if you do not already have one.</span></span> <span data-ttu-id="be8cc-155">Типичным вариантом является PuTTY, который можно загрузить с [этого ресурса](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="be8cc-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="be8cc-156">В операционных системах Linux и Macintosh уже есть встроенный клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="be8cc-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="be8cc-157">Настройка hello виртуальная машина Web переднего плана</span><span class="sxs-lookup"><span data-stu-id="be8cc-157">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="be8cc-158">SSH toohello web внешнего интерфейса компьютера, созданного с помощью PuTTY, ssh командной строки или другие избранный инструмент SSH.</span><span class="sxs-lookup"><span data-stu-id="be8cc-158">SSH toohello web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="be8cc-159">Отобразится приветствие и командная строка.</span><span class="sxs-lookup"><span data-stu-id="be8cc-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="be8cc-160">Сначала убедитесь, что Git и узел установлены.</span><span class="sxs-lookup"><span data-stu-id="be8cc-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="be8cc-161">Так как веб-приложения hello клиентом использует некоторые собственные модули Node.js, мы также должны tooinstall hello необходимый набор средств построения.</span><span class="sxs-lookup"><span data-stu-id="be8cc-161">Since hello application's web frontend relies on some native Node.js modules, we also need tooinstall hello essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="be8cc-162">Наконец, давайте установить приложение Node.js вызывается *навсегда*, которые помогают toorun Node.js серверные приложения:</span><span class="sxs-lookup"><span data-stu-id="be8cc-162">Finally, let's install a Node.js application called *forever*, which helps toorun Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="be8cc-163">Это все зависимости hello, необходимые на виртуальной машине toobe может toorun hello для этого приложения веб-клиентом, так что давайте работы.</span><span class="sxs-lookup"><span data-stu-id="be8cc-163">These are all hello dependencies needed on this virtual machine toobe able toorun hello application's web frontend, so let's get that running.</span></span> <span data-ttu-id="be8cc-164">toodo это, мы сначала создается исходного состояния системы клона репозитория GitHub hello ранее разделенными, можно легко опубликовать обновления toohello виртуальной машины (мы рассмотрим этот сценарий обновления более поздней версии) и затем клонировать tooprovide исходного состояния системы клон hello версии hello репозиторий, который фактически может выполняться.</span><span class="sxs-lookup"><span data-stu-id="be8cc-164">toodo this, we will first create a bare clone of hello GitHub repository you previously forked so that you can easily publish updates toohello virtual machine (we'll cover this update scenario later), and then clone hello bare clone tooprovide a version of hello repository that can actually be executed.</span></span>

<span data-ttu-id="be8cc-165">Начиная с hello домашнем каталоге (~), запустите hello, следующие команды (заменяя *accountname* с вашим именем учетной записи пользователя GitHub):</span><span class="sxs-lookup"><span data-stu-id="be8cc-165">Starting from hello home (~) directory, run hello following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="be8cc-166">Теперь введите каталог узла todo hello и выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="be8cc-166">Now enter hello node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="be8cc-167">Hello приложения веб-клиентом теперь работает, однако есть одно действие hello приложения для доступа к веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="be8cc-167">hello application's web frontend is now running, however there is one more step before you can access hello application from a web browser.</span></span> <span data-ttu-id="be8cc-168">Hello виртуальную машину, созданную защищен ресурс Azure, которая называется *сетевой группы безопасности*, который был создан для вас при подготовке hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="be8cc-168">hello virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned hello virtual machine.</span></span> <span data-ttu-id="be8cc-169">В настоящее время этот ресурс позволяет только внешние запросы tooport 22 toobe направлено toohello виртуальной машины, которое поддерживает связь SSH с машины hello, но ничего более.</span><span class="sxs-lookup"><span data-stu-id="be8cc-169">Currently, this resource only allows external requests tooport 22 toobe routed toohello virtual machine, which enables SSH communication with hello machine but nothing else.</span></span> <span data-ttu-id="be8cc-170">Поэтому в порядке tooview hello приложения TODO, которое служит toorun настроенный порт 8080, этот порт также должен toobe открыт.</span><span class="sxs-lookup"><span data-stu-id="be8cc-170">So in order tooview hello TODO application, which is configured toorun on port 8080, this port also needs toobe opened up.</span></span>

<span data-ttu-id="be8cc-171">Получите toohello портала Azure и выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-171">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="be8cc-172">Щелкните «Группы ресурсов» в левой hello панель переходов;</span><span class="sxs-lookup"><span data-stu-id="be8cc-172">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="be8cc-173">Выберите группу ресурсов hello, содержащий виртуальный компьютер;</span><span class="sxs-lookup"><span data-stu-id="be8cc-173">Select hello resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="be8cc-174">В hello полученный список ресурсов выберите группы безопасности сети hello (hello один щита на);</span><span class="sxs-lookup"><span data-stu-id="be8cc-174">In hello resulting list of resources, select hello network security group (hello one with a shield icon);</span></span>
* <span data-ttu-id="be8cc-175">В свойствах hello выберите «правила безопасности для входящего трафика»;</span><span class="sxs-lookup"><span data-stu-id="be8cc-175">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="be8cc-176">В панели инструментов hello нажмите кнопку «Добавить»;</span><span class="sxs-lookup"><span data-stu-id="be8cc-176">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="be8cc-177">Укажите имя, например default-allow-todo.</span><span class="sxs-lookup"><span data-stu-id="be8cc-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="be8cc-178">Задать протокол hello слишком «TCP»;</span><span class="sxs-lookup"><span data-stu-id="be8cc-178">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="be8cc-179">Задайте диапазон портов назначения hello слишком «8080»;</span><span class="sxs-lookup"><span data-stu-id="be8cc-179">Set hello destination port range too"8080";</span></span>
* <span data-ttu-id="be8cc-180">Нажмите кнопку ОК и дождитесь hello безопасности правило toobe создан.</span><span class="sxs-lookup"><span data-stu-id="be8cc-180">Click OK and wait for hello security rule toobe created.</span></span>

<span data-ttu-id="be8cc-181">После создания этого правила безопасности, hello приложения TODO общедоступен на hello Интернета и просмотром tooit, например с помощью URL-адреса, например:</span><span class="sxs-lookup"><span data-stu-id="be8cc-181">After creating this security rule, hello TODO application is publically visible on hello internet and you can browse tooit, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="be8cc-182">Можно заметить, несмотря на то, что мы еще не настроен hello MongoDB виртуальной машины, hello приложения TODO отображается toobe довольно работы.</span><span class="sxs-lookup"><span data-stu-id="be8cc-182">You will notice that even though we have not yet configured hello MongoDB virtual machine, hello TODO application appears toobe quite functional.</span></span> <span data-ttu-id="be8cc-183">Это, поскольку исходный репозиторий hello жестко toouse предварительно развернутого экземпляра MongoDB.</span><span class="sxs-lookup"><span data-stu-id="be8cc-183">This is because hello source repository is hardcoded toouse a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="be8cc-184">После настройки hello MongoDB виртуальной машины будет вернуться назад и изменить hello исходного кода tooutilize закрытого экземпляра MongoDB.</span><span class="sxs-lookup"><span data-stu-id="be8cc-184">Once we have configured hello MongoDB virtual machine, we will go back and change hello source code tooutilize our private MongoDB instance instead.</span></span>

### <a name="configuring-hello-mongodb-virtual-machine"></a><span data-ttu-id="be8cc-185">Настройка hello MongoDB виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="be8cc-185">Configuring hello MongoDB Virtual Machine</span></span>
<span data-ttu-id="be8cc-186">SSH toohello второй компьютер, созданного с помощью PuTTY, ssh командной строки или другие избранный инструмент SSH.</span><span class="sxs-lookup"><span data-stu-id="be8cc-186">SSH toohello second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="be8cc-187">После просмотра приветственное сообщение hello и из командной строки, установите MongoDB (эти инструкции были взяты из [здесь](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="be8cc-187">After seeing hello welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="be8cc-188">Стандартные настройки MongoDB предусматривают только локальный доступ.</span><span class="sxs-lookup"><span data-stu-id="be8cc-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="be8cc-189">В этом учебнике мы настраиваем MongoDB, доступных из приложения hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="be8cc-189">For this tutorial, we will configure MongoDB so it can be accessed from hello application's virtual machine.</span></span> <span data-ttu-id="be8cc-190">В контексте sudo, откройте файл /etc/mongod.conf hello и найдите hello `# network interfaces` раздела.</span><span class="sxs-lookup"><span data-stu-id="be8cc-190">In a sudo context, open hello /etc/mongod.conf file and locate hello `# network interfaces` section.</span></span> <span data-ttu-id="be8cc-191">Изменение hello `net.bindIp` конфигурации значение слишком`0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="be8cc-191">Change hello `net.bindIp` configuration value too`0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="be8cc-192">Эта конфигурация предназначена для целей hello только для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="be8cc-192">This configuration is for hello purposes of this tutorial only.</span></span> <span data-ttu-id="be8cc-193">Из соображений безопасности мы **НЕ** рекомендуем использовать этот прием в производственной среде.</span><span class="sxs-lookup"><span data-stu-id="be8cc-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="be8cc-194">Теперь убедитесь hello MongoDB служба была запущена.</span><span class="sxs-lookup"><span data-stu-id="be8cc-194">Now ensure hello MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="be8cc-195">По умолчанию MongoDB работает через порт 27017.</span><span class="sxs-lookup"><span data-stu-id="be8cc-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="be8cc-196">Поэтому в hello таким же образом, что нам нужен tooopen порт 8080 на виртуальной машине hello web переднего плана необходимо порт tooopen 27017 на виртуальной машине hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="be8cc-196">So, in hello same way that we needed tooopen port 8080 on hello web frontend virtual machine, we need tooopen port 27017 on hello MongoDB virtual machine.</span></span>

<span data-ttu-id="be8cc-197">Получите toohello портала Azure и выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-197">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="be8cc-198">Щелкните «Группы ресурсов» в левой hello панель переходов;</span><span class="sxs-lookup"><span data-stu-id="be8cc-198">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="be8cc-199">Выберите группу ресурсов hello, содержащий hello MongoDB виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="be8cc-199">Select hello resource group that contains hello MongoDB virtual machine;</span></span>
* <span data-ttu-id="be8cc-200">В hello полученный список ресурсов выберите группы безопасности сети hello (hello один щита на) с hello точно такое же имя, присвоенное toohello MongoDB виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="be8cc-200">In hello resulting list of resources, select hello network security group (hello one with a shield icon) with hello same name that you gave toohello MongoDB virtual machine;</span></span>
* <span data-ttu-id="be8cc-201">В свойствах hello выберите «правила безопасности для входящего трафика»;</span><span class="sxs-lookup"><span data-stu-id="be8cc-201">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="be8cc-202">В панели инструментов hello нажмите кнопку «Добавить»;</span><span class="sxs-lookup"><span data-stu-id="be8cc-202">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="be8cc-203">Укажите имя, например default-allow-mongo.</span><span class="sxs-lookup"><span data-stu-id="be8cc-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="be8cc-204">Задать протокол hello слишком «TCP»;</span><span class="sxs-lookup"><span data-stu-id="be8cc-204">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="be8cc-205">Задайте диапазон портов назначения hello слишком «27017»;</span><span class="sxs-lookup"><span data-stu-id="be8cc-205">Set hello destination port range too"27017";</span></span>
* <span data-ttu-id="be8cc-206">Нажмите кнопку ОК и дождитесь hello безопасности правило toobe создан.</span><span class="sxs-lookup"><span data-stu-id="be8cc-206">Click OK and wait for hello security rule toobe created.</span></span>

## <a name="iterating-on-hello-todo-application"></a><span data-ttu-id="be8cc-207">Итерации по hello приложения TODO</span><span class="sxs-lookup"><span data-stu-id="be8cc-207">Iterating on hello TODO application</span></span>
<span data-ttu-id="be8cc-208">Итак, мы подготовили две виртуальные машины Linux:, выполняется приложение hello веб-клиентом и один, на котором запущен экземпляр MongoDB.</span><span class="sxs-lookup"><span data-stu-id="be8cc-208">So far, we have provisioned two Linux virtual machines: one that is running hello application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="be8cc-209">Ошибка, но — веб-клиентом hello не использует фактически hello подготовить экземпляр MongoDB еще.</span><span class="sxs-lookup"><span data-stu-id="be8cc-209">But there is a problem - hello web frontend isn't actually using hello provisioned MongoDB instance yet.</span></span> <span data-ttu-id="be8cc-210">Исправим это путем обновления интерфейсных кода hello web toouse переменной среды, вместо жестко экземпляра.</span><span class="sxs-lookup"><span data-stu-id="be8cc-210">Let's fix that by updating hello web frontend code toouse an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-hello-todo-application"></a><span data-ttu-id="be8cc-211">Изменение приложения TODO hello</span><span class="sxs-lookup"><span data-stu-id="be8cc-211">Changing hello TODO application</span></span>
<span data-ttu-id="be8cc-212">На компьютере разработки, где сначала клонировать репозиторий hello todo узел, откройте hello `node-todo/config/database.js` файл в любом редакторе и измените значение hello URL-адреса с hello жестко запрограммированных значений, таких как `mongodb://...` слишком`process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="be8cc-212">On your development machine where you first cloned hello node-todo repository, open hello `node-todo/config/database.js` file in your favorite editor and change hello url value from hello hard-coded value like `mongodb://...` too`process.env.MONGODB`.</span></span>

<span data-ttu-id="be8cc-213">Фиксация изменений и отправить образец toohello GitHub:</span><span class="sxs-lookup"><span data-stu-id="be8cc-213">Commit your changes and push toohello GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="be8cc-214">К сожалению это не опубликует hello изменение toohello web переднего плана для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="be8cc-214">Unfortunately, this doesn't publish hello change toohello web frontend virtual machine.</span></span> <span data-ttu-id="be8cc-215">Сделаем несколько дополнительных tooenable изменения виртуальной машины toothat простой, но эффективный механизм для публикации обновлений, позволяющий быстро просматривать hello влияния изменений hello в реальной среде hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-215">Let's make a few more changes toothat virtual machine tooenable a simple but effective mechanism for publishing updates so you can quickly observe hello effect of hello changes in hello live environment.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="be8cc-216">Настройка hello виртуальная машина Web переднего плана</span><span class="sxs-lookup"><span data-stu-id="be8cc-216">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="be8cc-217">Помните, что мы созданного ранее исходного состояния системы клона репозитория hello todo узла на виртуальная машина hello web переднего плана.</span><span class="sxs-lookup"><span data-stu-id="be8cc-217">Recall that we previously created a bare clone of hello node-todo repository on hello web frontend virtual machine.</span></span> <span data-ttu-id="be8cc-218">Оказывается, что это действие создан новый Git удаленного toowhich изменения могут передаваться.</span><span class="sxs-lookup"><span data-stu-id="be8cc-218">It turns out that this action created a new Git remote toowhich changes can be pushed.</span></span> <span data-ttu-id="be8cc-219">Тем не менее просто помещает toothis удаленного совсем не дает модель быстрой итерации hello, ищете разработчики при работе в своем коде.</span><span class="sxs-lookup"><span data-stu-id="be8cc-219">However, simply pushing toothis remote doesn't quite give hello rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="be8cc-220">Что мы хотели бы могли toodo toobe убедитесь, что в случае принудительной toohello удаленный репозиторий на виртуальной машине hello hello запущенное приложение TODO автоматически обновлена.</span><span class="sxs-lookup"><span data-stu-id="be8cc-220">What we would like toobe able toodo is ensure that when a push toohello remote repository on hello virtual machine occurs, hello running TODO application is automatically updated.</span></span> <span data-ttu-id="be8cc-221">К счастью это легко tooachieve с git.</span><span class="sxs-lookup"><span data-stu-id="be8cc-221">Fortunately, this is easy tooachieve with git.</span></span>

<span data-ttu-id="be8cc-222">Git предоставляет ряд обработчиками, которые вызываются в tooactions tooreact определенные промежутки времени, затраченное на репозиторий hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-222">Git exposes a number of hooks that are called at particular times tooreact tooactions taken on hello repository.</span></span> <span data-ttu-id="be8cc-223">Они указываются с помощью сценариев оболочки в репозитории hello `hooks` папки.</span><span class="sxs-lookup"><span data-stu-id="be8cc-223">These are specified using shell scripts in hello repository's `hooks` folder.</span></span> <span data-ttu-id="be8cc-224">Hello обработчик, который лучше всего подходит для hello сценария автоматическое обновление — hello `post-update` событий.</span><span class="sxs-lookup"><span data-stu-id="be8cc-224">hello hook that is most applicable for hello auto-update scenario is hello `post-update` event.</span></span>

<span data-ttu-id="be8cc-225">В SSH сеанса toohello web переднего плана виртуальной машины, измените toohello `~/node-todo.git/hooks` каталога и добавьте следующие содержимого tooa файл с именем hello `post-update` (заменив `machinename` и `region` с указанием данных MongoDB виртуальной машины):</span><span class="sxs-lookup"><span data-stu-id="be8cc-225">In a SSH session toohello web frontend virtual machine, change toohello `~/node-todo.git/hooks` directory and add hello following content tooa file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="be8cc-226">Убедитесь, что этот файл является исполняемым, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-226">Ensure this file is executable by running hello following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="be8cc-227">Этот сценарий обеспечивает остановки текущего сервера приложения hello, кода hello в клонированного репозитория hello обновленные toohello последняя версия, все обновленные зависимостям, и перезапуска сервера hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-227">This script ensures that hello current server application is stopped, hello code in hello cloned repository is updated toohello latest, any updated dependencies are satisfied, and hello server is restarted.</span></span> <span data-ttu-id="be8cc-228">Это также гарантирует, что в этой среде hello был настроен в процессе подготовки для получения первого наш экземпляр MongoDB tooget обновления приложения hello из переменной среды.</span><span class="sxs-lookup"><span data-stu-id="be8cc-228">It also ensures that hello environment has been configured in preparation for receiving our first application update tooget hello MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="be8cc-229">Настройка компьютера разработки</span><span class="sxs-lookup"><span data-stu-id="be8cc-229">Configuring your Development Machine</span></span>
<span data-ttu-id="be8cc-230">Теперь давайте компьютере подключается виртуальная машина toohello web переднего плана.</span><span class="sxs-lookup"><span data-stu-id="be8cc-230">Now let's get your development machine hooked up toohello web frontend virtual machine.</span></span> <span data-ttu-id="be8cc-231">Это простым добавлением на виртуальной машине hello, что и удаленный репозиторий исходного состояния системы hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-231">This is as simple as adding hello bare repository on hello virtual machine as a remote.</span></span> <span data-ttu-id="be8cc-232">Выполните следующие команды toodo hello это (заменив *пользователя* с вашим именем входа виртуальной машины интерфейсных веб и *machinename* и *область* соответствующим образом):</span><span class="sxs-lookup"><span data-stu-id="be8cc-232">Run hello following command toodo this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="be8cc-233">Это все, что необходимые tooenable принудительной отправки, фактически публикации, или изменяет виртуальная машина toohello web переднего плана.</span><span class="sxs-lookup"><span data-stu-id="be8cc-233">This is all that is needed tooenable pushing, or in effect publishing, changes toohello web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="be8cc-234">Публикация обновлений</span><span class="sxs-lookup"><span data-stu-id="be8cc-234">Publishing Updates</span></span>
<span data-ttu-id="be8cc-235">Давайте публикация hello одно из изменений, сделанных к текущему моменту, чтобы приложение hello используется собственный экземпляр MongoDB.</span><span class="sxs-lookup"><span data-stu-id="be8cc-235">Let's publish hello one change that has been made so far so that hello application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="be8cc-236">Вы увидите примерно toothis выходные данные:</span><span class="sxs-lookup"><span data-stu-id="be8cc-236">You should see output similar toothis:</span></span>

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="be8cc-237">После выполнения этой команды, попробуйте обновить приложение hello в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="be8cc-237">After this command completes, try refreshing hello application in a web browser.</span></span> <span data-ttu-id="be8cc-238">Должно быть toosee возможности, представленные здесь список TODO hello пуст и больше не равноценных toohello общего развертывания MongoDB экземпляра.</span><span class="sxs-lookup"><span data-stu-id="be8cc-238">You should be able toosee that hello TODO list presented here is empty and no longer tied toohello shared deployed MongoDB instance.</span></span>

<span data-ttu-id="be8cc-239">Учебник hello toocomplete, давайте сделать другой, более видимым.</span><span class="sxs-lookup"><span data-stu-id="be8cc-239">toocomplete hello tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="be8cc-240">На компьютере разработки откройте файл node-todo/public/index.html hello, используя текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="be8cc-240">On your development machine, open hello node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="be8cc-241">Найдите заголовок jumbotron hello и измените заголовок hello из «Я Todo-aholic» слишком «я Todo-aholic в Azure!».</span><span class="sxs-lookup"><span data-stu-id="be8cc-241">Locate hello jumbotron header and change  hello title from "I'm a Todo-aholic" too"I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="be8cc-242">Зафиксируем это изменение.</span><span class="sxs-lookup"><span data-stu-id="be8cc-242">Now let's commit:</span></span>

    git commit -am "Azurify hello title"

<span data-ttu-id="be8cc-243">Это время, давайте публикации tooAzure изменение hello до отправки его в репозитории GitHub toohello tooback:</span><span class="sxs-lookup"><span data-stu-id="be8cc-243">This time, let's publish hello change tooAzure before pushing it tooback toohello GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="be8cc-244">После выполнения этой команды обновления hello веб-страницу, чтобы просмотреть изменения hello.</span><span class="sxs-lookup"><span data-stu-id="be8cc-244">Once this command completes, refresh hello web page and you will see hello changes.</span></span> <span data-ttu-id="be8cc-245">Так как они выглядят правильно, push удаленный источник назад toohello hello изменений:</span><span class="sxs-lookup"><span data-stu-id="be8cc-245">Since they look good, push hello change back toohello origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="be8cc-246">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be8cc-246">Next Steps</span></span>
<span data-ttu-id="be8cc-247">В этой статье показано, как tootake приложений Node.js и разверните его tooLinux виртуальные машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="be8cc-247">This article showed how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="be8cc-248">toolearn Дополнительные сведения о виртуальных машин Linux в Azure, в разделе [tooLinux введение в Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="be8cc-248">toolearn more about Linux virtual machines in Azure, see [Introduction tooLinux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="be8cc-249">Дополнительные сведения о том, как toodevelop приложений Node.js в Azure, в разделе hello [Центр разработчика Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="be8cc-249">For more information about how toodevelop Node.js applications on Azure, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

