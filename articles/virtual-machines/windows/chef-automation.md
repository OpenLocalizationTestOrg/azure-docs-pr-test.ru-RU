---
title: "развертывание виртуальной машины aaaAzure с Chef | Документы Microsoft"
description: "Узнайте, как toouse Chef toodo автоматизировать развертывание виртуальной машины и конфигурации в Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="6d364-103">Автоматизация развертывания виртуальной машины Azure с помощью Chef</span><span class="sxs-lookup"><span data-stu-id="6d364-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="6d364-104">Chef — это отличное средство для автоматизации и для настройки требуемого состояния.</span><span class="sxs-lookup"><span data-stu-id="6d364-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="6d364-105">Наш последний выпуск api облака Chef обеспечивает прозрачную интеграцию с Azure, предоставляя возможность tooprovision hello и развертывание состояния конфигурации одной командой.</span><span class="sxs-lookup"><span data-stu-id="6d364-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you hello ability tooprovision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="6d364-106">В этой статье я покажу как tooset копирование вашей tooprovision среды Chef Azure виртуальных машин и пошаговыми руководствами по созданию политики или «Рецепты», а затем развернуть этот сборник рецептов tooan виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="6d364-106">In this article, I’ll show you how tooset up your Chef environment tooprovision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook tooan Azure virtual machine.</span></span>

<span data-ttu-id="6d364-107">Итак, начнем!</span><span class="sxs-lookup"><span data-stu-id="6d364-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="6d364-108">Основы использования Chef</span><span class="sxs-lookup"><span data-stu-id="6d364-108">Chef basics</span></span>
<span data-ttu-id="6d364-109">Прежде чем начать, я рекомендую просмотрите основные понятия hello Chef.</span><span class="sxs-lookup"><span data-stu-id="6d364-109">Before you begin, I suggest you review hello basic concepts of Chef.</span></span> <span data-ttu-id="6d364-110"><a href="http://www.chef.io/chef" target="_blank">Вот</a> великолепный материал. Я рекомендую быстро ознакомиться с ним, прежде чем начать работу с данным пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="6d364-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="6d364-111">Однако я будет повторим основы hello, прежде чем приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="6d364-111">I will however recap hello basics before we get started.</span></span>

<span data-ttu-id="6d364-112">Следующая схема Hello показана высокоуровневая архитектура Chef hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-112">hello following diagram depicts hello high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="6d364-113">Chef имеет три основных компонента архитектуры: сервер Chef, клиент (узел) Chef и рабочая станция Chef.</span><span class="sxs-lookup"><span data-stu-id="6d364-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="6d364-114">Hello сервера Chef является нашей точкой управления и есть два варианта для hello сервера Chef: ведущее решение или локальным решением.</span><span class="sxs-lookup"><span data-stu-id="6d364-114">hello Chef Server is our management point and there are two options for hello Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="6d364-115">Мы будем использовать размещенное решение.</span><span class="sxs-lookup"><span data-stu-id="6d364-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="6d364-116">Клиент Hello Chef (узел) — hello агент, который располагается на серверах hello, которыми вы управляете.</span><span class="sxs-lookup"><span data-stu-id="6d364-116">hello Chef Client (node) is hello agent that sits on hello servers you are managing.</span></span>

<span data-ttu-id="6d364-117">Hello рабочая станция Chef является нашей администраторские рабочие станции, где создать нашей политики и выполнять нашей команды управления.</span><span class="sxs-lookup"><span data-stu-id="6d364-117">hello Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="6d364-118">Запустим hello **knife** команду hello рабочей станции Chef toomanage инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="6d364-118">We run hello **knife** command from hello Chef Workstation toomanage our infrastructure.</span></span>

<span data-ttu-id="6d364-119">Имеется также hello понятие «Кулинарные книги» и «Рецепты».</span><span class="sxs-lookup"><span data-stu-id="6d364-119">There is also hello concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="6d364-120">Это эффективно политики hello мы определить и применить tooour серверов.</span><span class="sxs-lookup"><span data-stu-id="6d364-120">These are effectively hello policies we define and apply tooour servers.</span></span>

## <a name="preparing-hello-workstation"></a><span data-ttu-id="6d364-121">Подготовка рабочей станции hello</span><span class="sxs-lookup"><span data-stu-id="6d364-121">Preparing hello workstation</span></span>
<span data-ttu-id="6d364-122">Во-первых позволяет рабочей станции с подготовки hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-122">First, lets prep hello workstation.</span></span> <span data-ttu-id="6d364-123">В данном случае используется стандартная рабочая станция Windows.</span><span class="sxs-lookup"><span data-stu-id="6d364-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="6d364-124">Мы должны toocreate directory toostore наших файлов конфигурации и справочники.</span><span class="sxs-lookup"><span data-stu-id="6d364-124">We need toocreate a directory toostore our config files and cookbooks.</span></span>

<span data-ttu-id="6d364-125">Сначала создайте каталог с именем C:\chef.</span><span class="sxs-lookup"><span data-stu-id="6d364-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="6d364-126">Затем создайте каталог C:\chef\cookbooks.</span><span class="sxs-lookup"><span data-stu-id="6d364-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="6d364-127">Теперь нужно toodownload наш файл настроек Azure чтобы Chef можно взаимодействовать с нашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="6d364-127">We now need toodownload our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="6d364-128">Загрузите вашей hello PowerShell Azure с помощью параметров публикации [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) команды.</span><span class="sxs-lookup"><span data-stu-id="6d364-128">Download your publish settings using hello PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="6d364-129">Сохраните hello файл параметров публикации в C:\chef.</span><span class="sxs-lookup"><span data-stu-id="6d364-129">Save hello publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="6d364-130">Создание управляемой учетной записи Chef</span><span class="sxs-lookup"><span data-stu-id="6d364-130">Creating a managed Chef account</span></span>
<span data-ttu-id="6d364-131">Зарегистрируйте размещенную учетную запись Chef [здесь](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="6d364-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="6d364-132">Во время процесса регистрации hello, появится запрос toocreate новой организации.</span><span class="sxs-lookup"><span data-stu-id="6d364-132">During hello signup process, you will be asked toocreate a new organization.</span></span>

![][3]

<span data-ttu-id="6d364-133">После создания вашей организации, загрузите начальный набор hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-133">Once your organization is created, download hello starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="6d364-134">Если появится предупреждение, что ключи будут сброшены, это будет ОК tooproceed, поскольку у нас есть без существующей инфраструктуры, как еще не настроены.</span><span class="sxs-lookup"><span data-stu-id="6d364-134">If you receive a prompt warning you that your keys will be reset, it’s ok tooproceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="6d364-135">Этот ZIP-файл начального набора содержит ключи и файлы конфигурации вашей организации.</span><span class="sxs-lookup"><span data-stu-id="6d364-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-hello-chef-workstation"></a><span data-ttu-id="6d364-136">Настройка рабочей станции Chef hello</span><span class="sxs-lookup"><span data-stu-id="6d364-136">Configuring hello Chef workstation</span></span>
<span data-ttu-id="6d364-137">Извлеките содержимое hello tooC:\chef chef starter.zip hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-137">Extract hello content of hello chef-starter.zip tooC:\chef.</span></span>

<span data-ttu-id="6d364-138">Скопируйте все файлы в starter\chef-chef-repo\.chef tooyour c:\chef каталога.</span><span class="sxs-lookup"><span data-stu-id="6d364-138">Copy all files under chef-starter\chef-repo\.chef tooyour c:\chef directory.</span></span>

<span data-ttu-id="6d364-139">Каталог должен выглядеть примерно следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-139">Your directory should now look something like hello following example.</span></span>

![][5]

<span data-ttu-id="6d364-140">Должны появиться четыре файлы, включая hello Azure файла публикации в корне c:\chef hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-140">You should now have four files including hello Azure publishing file in hello root of c:\chef.</span></span>

<span data-ttu-id="6d364-141">PEM-файлы Hello содержаться вашей организации и закрытый ключи администратора для обмена данными, а файл knife.rb hello содержит конфигурацию инструментом.</span><span class="sxs-lookup"><span data-stu-id="6d364-141">hello PEM files contain your organization and admin private keys for communication while hello knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="6d364-142">Нам понадобится файл knife.rb tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-142">We will need tooedit hello knife.rb file.</span></span>

<span data-ttu-id="6d364-143">Откройте файл hello в редакторе по выбору и изменить cookbook_path «hello», удалив hello /... из пути hello выводится так, как показано далее.</span><span class="sxs-lookup"><span data-stu-id="6d364-143">Open hello file in your editor of choice and modify hello “cookbook_path” by removing hello /../ from hello path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="6d364-144">Также добавьте hello следующей строке, отражающей имя hello Azure файл параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="6d364-144">Also add hello following line reflecting hello name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="6d364-145">Файл knife.rb должен выглядеть примерно toohello следующий пример.</span><span class="sxs-lookup"><span data-stu-id="6d364-145">Your knife.rb file should now look similar toohello following example.</span></span>

![][6]

<span data-ttu-id="6d364-146">Эти строки будут убедитесь, что Knife ссылается на каталог справочники hello в c:\chef\cookbooks и также использует наш файл настроек публикации Azure во время операций Azure.</span><span class="sxs-lookup"><span data-stu-id="6d364-146">These lines will ensure that Knife references hello cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-hello-chef-development-kit"></a><span data-ttu-id="6d364-147">Установка пакета средств разработки Chef hello</span><span class="sxs-lookup"><span data-stu-id="6d364-147">Installing hello Chef Development Kit</span></span>
<span data-ttu-id="6d364-148">Далее [загрузить и установить](http://downloads.getchef.com/chef-dk/windows) hello tooset ChefDK (Chef Development Kit) вверх рабочей станции Chef.</span><span class="sxs-lookup"><span data-stu-id="6d364-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) hello ChefDK (Chef Development Kit) tooset up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="6d364-149">Установите в расположение по умолчанию hello c:\opscode.</span><span class="sxs-lookup"><span data-stu-id="6d364-149">Install in hello default location of c:\opscode.</span></span> <span data-ttu-id="6d364-150">Эта установка займет около 10 минут.</span><span class="sxs-lookup"><span data-stu-id="6d364-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="6d364-151">Убедитесь, что переменная PATH содержит записи для путей C:\opscode\chefdk\bin, C:\opscode\chefdk\embedded\bin и C:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin.</span><span class="sxs-lookup"><span data-stu-id="6d364-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="6d364-152">Если они отсутствуют, обязательно добавьте эти пути!</span><span class="sxs-lookup"><span data-stu-id="6d364-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="6d364-153">*Примечание hello ЗАКАЗА из hello путь — важно!*</span><span class="sxs-lookup"><span data-stu-id="6d364-153">*NOTE hello ORDER OF hello PATH IS IMPORTANT!*</span></span> <span data-ttu-id="6d364-154">Если ваш opscode пути не в правильном порядке hello связаны проблемы.</span><span class="sxs-lookup"><span data-stu-id="6d364-154">If your opscode paths are not in hello correct order you will have issues.</span></span>

<span data-ttu-id="6d364-155">Прежде чем продолжить, перезагрузите рабочую станцию.</span><span class="sxs-lookup"><span data-stu-id="6d364-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="6d364-156">После этого будет установлен модуль Knife для Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-156">Next, we will install hello Knife Azure extension.</span></span> <span data-ttu-id="6d364-157">Это предоставляет Knife hello «Подключаемый модуль Azure».</span><span class="sxs-lookup"><span data-stu-id="6d364-157">This provides Knife with hello “Azure Plugin”.</span></span>

<span data-ttu-id="6d364-158">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-158">Run hello following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="6d364-159">Аргумент – pre Hello гарантирует, что вы получили hello последнюю версию-КАНДИДАТ hello подключаемый модуль Azure инструментом, который предоставляет доступ toohello последний набор API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="6d364-159">hello –pre argument ensures you are receiving hello latest RC version of hello Knife Azure Plugin which provides access toohello latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="6d364-160">Вполне вероятно, что число зависимостей, также будут установлены в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="6d364-160">It’s likely that a number of dependencies will also be installed at hello same time.</span></span>

![][8]

<span data-ttu-id="6d364-161">tooensure — все компоненты настроены неправильно, выполнения hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6d364-161">tooensure everything is configured correctly, run hello following command.</span></span>

    knife azure image list

<span data-ttu-id="6d364-162">Если все настроено правильно, появится прокручиваемый список доступных образов Azure.</span><span class="sxs-lookup"><span data-stu-id="6d364-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="6d364-163">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="6d364-163">Congratulations.</span></span> <span data-ttu-id="6d364-164">Настройка рабочей станции Hello!</span><span class="sxs-lookup"><span data-stu-id="6d364-164">hello workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="6d364-165">Создание подробной инструкции</span><span class="sxs-lookup"><span data-stu-id="6d364-165">Creating a Cookbook</span></span>
<span data-ttu-id="6d364-166">Рецепты используется Chef toodefine набор команд, которые нужно tooexecute на управляемый клиент.</span><span class="sxs-lookup"><span data-stu-id="6d364-166">A Cookbook is used by Chef toodefine a set of commands that you wish tooexecute on your managed client.</span></span> <span data-ttu-id="6d364-167">Создание кулинарной книги довольно просто, и мы используем hello **chef создания рецепты** команды toogenerate нашей рецепты шаблона.</span><span class="sxs-lookup"><span data-stu-id="6d364-167">Creating a Cookbook is straightforward and we use hello **chef generate cookbook** command toogenerate our Cookbook template.</span></span> <span data-ttu-id="6d364-168">Мы назовем свою подробную инструкцию именем webserver, так как нам нужна политика, которая автоматически развертывает службы IIS.</span><span class="sxs-lookup"><span data-stu-id="6d364-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="6d364-169">В каталоге C:\Chef выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-169">Under your C:\Chef directory run hello following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="6d364-170">Будет создан набор файлов в каталоге C:\Chef\cookbooks\webserver hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-170">This will generate a set of files under hello directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="6d364-171">Теперь мы должны toodefine hello набор команд, что мы предлагаем наши tooexecute клиент Chef на нашем управляемую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="6d364-171">We now need toodefine hello set of commands we would like our Chef client tooexecute on our managed virtual machine.</span></span>

<span data-ttu-id="6d364-172">Hello команды сохраняются в файле default.rb hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-172">hello commands are stored in hello file default.rb.</span></span> <span data-ttu-id="6d364-173">В этом файле я будет определяться набор команд, установка служб IIS, запускающий IIS и копирует папку wwwroot toohello файла шаблона.</span><span class="sxs-lookup"><span data-stu-id="6d364-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file toohello wwwroot folder.</span></span>

<span data-ttu-id="6d364-174">Измените файл C:\chef\cookbooks\webserver\recipes\default.rb hello и добавьте следующие строки hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-174">Modify hello C:\chef\cookbooks\webserver\recipes\default.rb file and add hello following lines.</span></span>

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

<span data-ttu-id="6d364-175">Сохраните файл hello, после завершения работы.</span><span class="sxs-lookup"><span data-stu-id="6d364-175">Save hello file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="6d364-176">Создание шаблона</span><span class="sxs-lookup"><span data-stu-id="6d364-176">Creating a template</span></span>
<span data-ttu-id="6d364-177">Как упоминалось ранее, мы должны toogenerate файл шаблона, который будет использоваться в качестве нашу страницу default.html.</span><span class="sxs-lookup"><span data-stu-id="6d364-177">As we mentioned previously, we need toogenerate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="6d364-178">Запустите следующий шаблон hello toogenerate команды hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-178">Run hello following command toogenerate hello template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="6d364-179">Теперь перейдите toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb файл.</span><span class="sxs-lookup"><span data-stu-id="6d364-179">Now navigate toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="6d364-180">Измените файл hello, добавление простого кода HTML «Hello World», а затем сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-180">Edit hello file by adding some simple “Hello World” HTML code, and then save hello file.</span></span>

## <a name="upload-hello-cookbook-toohello-chef-server"></a><span data-ttu-id="6d364-181">Отправка toohello рецепты hello сервера Chef</span><span class="sxs-lookup"><span data-stu-id="6d364-181">Upload hello Cookbook toohello Chef Server</span></span>
<span data-ttu-id="6d364-182">На этом шаге мы создавая копию hello рецепты, созданную на локальном компьютере и передачи их toohello размещенного сервера Chef.</span><span class="sxs-lookup"><span data-stu-id="6d364-182">In this step, we are taking a copy of hello Cookbook that we have created on our local machine and uploading it toohello Chef Hosted Server.</span></span> <span data-ttu-id="6d364-183">После отправки hello рецепты будут отображаться в узле hello **политики** вкладки.</span><span class="sxs-lookup"><span data-stu-id="6d364-183">Once uploaded, hello Cookbook will appear under hello **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="6d364-184">Развертывание виртуальной машины с помощью Knife Azure</span><span class="sxs-lookup"><span data-stu-id="6d364-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="6d364-185">Мы развертывание виртуальной машины Azure и применить hello «Веб-сервер» рецепты, который будет установлен в нашей IIS web service и по умолчанию веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="6d364-185">We will now deploy an Azure virtual machine and apply hello “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="6d364-186">В заказ toodo это, используйте hello **knife azure server создать** команды.</span><span class="sxs-lookup"><span data-stu-id="6d364-186">In order toodo this, use hello **knife azure server create** command.</span></span>

<span data-ttu-id="6d364-187">Уверен, что пример hello команды появится рядом.</span><span class="sxs-lookup"><span data-stu-id="6d364-187">Am example of hello command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="6d364-188">Hello параметров говорят сами за себя.</span><span class="sxs-lookup"><span data-stu-id="6d364-188">hello parameters are self-explanatory.</span></span> <span data-ttu-id="6d364-189">Подставьте свои переменные и запустите команду.</span><span class="sxs-lookup"><span data-stu-id="6d364-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="6d364-190">Через командную строку hello hello я также автоматизация правила фильтра конечной точки сети с помощью параметра hello конечные точки — tcp.</span><span class="sxs-lookup"><span data-stu-id="6d364-190">Through hello hello command line, I’m also automating my endpoint network filter rules by using hello –tcp-endpoints parameter.</span></span> <span data-ttu-id="6d364-191">Открыли порты 80 и 3389 tooprovide доступа toomy веб-страницы и сеансу удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="6d364-191">I’ve opened up ports 80 and 3389 tooprovide access toomy web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="6d364-192">После выполнения команды hello перехода toohello Azure портал, чтобы просмотреть начать tooprovision компьютере.</span><span class="sxs-lookup"><span data-stu-id="6d364-192">Once you run hello command, go toohello Azure portal and you will see your machine begin tooprovision.</span></span>

![][13]

<span data-ttu-id="6d364-193">Далее появится Hello Командная строка.</span><span class="sxs-lookup"><span data-stu-id="6d364-193">hello command prompt appears next.</span></span>

![][10]

<span data-ttu-id="6d364-194">После завершения развертывания hello, мы должен быть веб-службы может tooconnect toohello через порт 80, как мы открыт порт hello, когда мы провизионировали hello виртуальную машину с hello команд Knife для Azure.</span><span class="sxs-lookup"><span data-stu-id="6d364-194">Once hello deployment is complete, we should be able tooconnect toohello web service over port 80 as we had opened hello port when we provisioned hello virtual machine with hello Knife Azure command.</span></span> <span data-ttu-id="6d364-195">Как эта виртуальная машина hello только виртуальной машины в облачной службе, он будет подключен с URL-адрес hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="6d364-195">As this virtual machine is hello only virtual machine in my cloud service, I’ll connect it with hello cloud service url.</span></span>

![][11]

<span data-ttu-id="6d364-196">Здесь вы могли наблюдать пример творческого подхода к написанию кода.</span><span class="sxs-lookup"><span data-stu-id="6d364-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="6d364-197">Не забывайте, что можно также подключиться через сеанс RDP с портала Azure через порт 3389 hello.</span><span class="sxs-lookup"><span data-stu-id="6d364-197">Don’t forget we can also connect through an RDP session from hello Azure portal via port 3389.</span></span>

<span data-ttu-id="6d364-198">Надеюсь, что эта информация была для вас полезной!</span><span class="sxs-lookup"><span data-stu-id="6d364-198">I hope this has been helpful!</span></span> <span data-ttu-id="6d364-199">Начинайте использовать подход "инфраструктура как код" прямо сейчас с помощью Azure!</span><span class="sxs-lookup"><span data-stu-id="6d364-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
