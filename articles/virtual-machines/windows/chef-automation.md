---
title: "Развертывание виртуальной машины Azure с помощью Chef | Документация Майкрософт"
description: "Узнайте, как использовать Chef для автоматизированного развертывания и настройки виртуальных машин в Microsoft Azure."
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
ms.openlocfilehash: b6db0fbb4e0de896994954974ddcc39daad9c125
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="a69e0-103">Автоматизация развертывания виртуальной машины Azure с помощью Chef</span><span class="sxs-lookup"><span data-stu-id="a69e0-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="a69e0-104">Chef — это отличное средство для автоматизации и для настройки требуемого состояния.</span><span class="sxs-lookup"><span data-stu-id="a69e0-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="a69e0-105">После нашего последнего выпуска облачного API средство Chef обеспечивает прозрачную интеграцию с Azure, позволяя подготовить и развернуть состояния конфигурации одной командой.</span><span class="sxs-lookup"><span data-stu-id="a69e0-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you the ability to provision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="a69e0-106">В этой статье показано, как настроить среду Chef для подготовки виртуальных машин Azure, а также рассматривается пошаговая процедура создания политики или "подробной инструкции", после чего данная инструкция применяется на практике к виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e0-106">In this article, I’ll show you how to set up your Chef environment to provision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook to an Azure virtual machine.</span></span>

<span data-ttu-id="a69e0-107">Итак, начнем!</span><span class="sxs-lookup"><span data-stu-id="a69e0-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="a69e0-108">Основы использования Chef</span><span class="sxs-lookup"><span data-stu-id="a69e0-108">Chef basics</span></span>
<span data-ttu-id="a69e0-109">Прежде чем начать, рекомендую вам изучить основные принципы работы со средой Chef.</span><span class="sxs-lookup"><span data-stu-id="a69e0-109">Before you begin, I suggest you review the basic concepts of Chef.</span></span> <span data-ttu-id="a69e0-110"><a href="http://www.chef.io/chef" target="_blank">Вот</a> великолепный материал. Я рекомендую быстро ознакомиться с ним, прежде чем начать работу с данным пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="a69e0-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="a69e0-111">Однако перед началом работы мы все равно повторим основы.</span><span class="sxs-lookup"><span data-stu-id="a69e0-111">I will however recap the basics before we get started.</span></span>

<span data-ttu-id="a69e0-112">На приведенной ниже схеме показана высокоуровневая архитектура Chef.</span><span class="sxs-lookup"><span data-stu-id="a69e0-112">The following diagram depicts the high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="a69e0-113">Chef имеет три основных компонента архитектуры: сервер Chef, клиент (узел) Chef и рабочая станция Chef.</span><span class="sxs-lookup"><span data-stu-id="a69e0-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="a69e0-114">Сервер Chef является управляющим компонентом и доступен в двух вариантах: размещенное решение или локальное решение.</span><span class="sxs-lookup"><span data-stu-id="a69e0-114">The Chef Server is our management point and there are two options for the Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="a69e0-115">Мы будем использовать размещенное решение.</span><span class="sxs-lookup"><span data-stu-id="a69e0-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="a69e0-116">Клиент Chef (узел) — это агент, который находится на управляемых серверах.</span><span class="sxs-lookup"><span data-stu-id="a69e0-116">The Chef Client (node) is the agent that sits on the servers you are managing.</span></span>

<span data-ttu-id="a69e0-117">Рабочая станция Chef является нашей рабочей станцией администрирования, где мы создаем политики и выполняем команды управления.</span><span class="sxs-lookup"><span data-stu-id="a69e0-117">The Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="a69e0-118">Для управления инфраструктурой мы выполняем команду **knife** на рабочей станции Chef.</span><span class="sxs-lookup"><span data-stu-id="a69e0-118">We run the **knife** command from the Chef Workstation to manage our infrastructure.</span></span>

<span data-ttu-id="a69e0-119">Кроме того, существует понятие "детальных инструкций" и "рецептов".</span><span class="sxs-lookup"><span data-stu-id="a69e0-119">There is also the concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="a69e0-120">Фактически, это те политики, которые мы определяем и применяем к своим серверам.</span><span class="sxs-lookup"><span data-stu-id="a69e0-120">These are effectively the policies we define and apply to our servers.</span></span>

## <a name="preparing-the-workstation"></a><span data-ttu-id="a69e0-121">Подготовка рабочей станции</span><span class="sxs-lookup"><span data-stu-id="a69e0-121">Preparing the workstation</span></span>
<span data-ttu-id="a69e0-122">Сначала давайте подготовим рабочую станцию.</span><span class="sxs-lookup"><span data-stu-id="a69e0-122">First, lets prep the workstation.</span></span> <span data-ttu-id="a69e0-123">В данном случае используется стандартная рабочая станция Windows.</span><span class="sxs-lookup"><span data-stu-id="a69e0-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="a69e0-124">Необходимо создать каталог для хранения файлов конфигурации и детальных инструкций.</span><span class="sxs-lookup"><span data-stu-id="a69e0-124">We need to create a directory to store our config files and cookbooks.</span></span>

<span data-ttu-id="a69e0-125">Сначала создайте каталог с именем C:\chef.</span><span class="sxs-lookup"><span data-stu-id="a69e0-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="a69e0-126">Затем создайте каталог C:\chef\cookbooks.</span><span class="sxs-lookup"><span data-stu-id="a69e0-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="a69e0-127">Теперь нам нужно скачать наш файл параметров Azure, чтобы средство Chef могло взаимодействовать с нашей подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e0-127">We now need to download our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="a69e0-128">Скачайте свои параметры публикации с помощью команды PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="a69e0-128">Download your publish settings using the PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="a69e0-129">Сохраните файл параметров публикации в каталоге C:\chef.</span><span class="sxs-lookup"><span data-stu-id="a69e0-129">Save the publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="a69e0-130">Создание управляемой учетной записи Chef</span><span class="sxs-lookup"><span data-stu-id="a69e0-130">Creating a managed Chef account</span></span>
<span data-ttu-id="a69e0-131">Зарегистрируйте размещенную учетную запись Chef [здесь](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="a69e0-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="a69e0-132">В процессе регистрации вам будет предложено создать новую организацию.</span><span class="sxs-lookup"><span data-stu-id="a69e0-132">During the signup process, you will be asked to create a new organization.</span></span>

![][3]

<span data-ttu-id="a69e0-133">После создания организации скачайте начальный набор.</span><span class="sxs-lookup"><span data-stu-id="a69e0-133">Once your organization is created, download the starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="a69e0-134">Если появится предупреждение о том, что ваши ключи будут сброшены, вы можете спокойно продолжить процедуру, так как у вас пока нет никакой настроенной инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="a69e0-134">If you receive a prompt warning you that your keys will be reset, it’s ok to proceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="a69e0-135">Этот ZIP-файл начального набора содержит ключи и файлы конфигурации вашей организации.</span><span class="sxs-lookup"><span data-stu-id="a69e0-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-the-chef-workstation"></a><span data-ttu-id="a69e0-136">Настройка рабочей станции Chef</span><span class="sxs-lookup"><span data-stu-id="a69e0-136">Configuring the Chef workstation</span></span>
<span data-ttu-id="a69e0-137">Извлеките содержимое файла chef-starter.zip в каталог C:\chef.</span><span class="sxs-lookup"><span data-stu-id="a69e0-137">Extract the content of the chef-starter.zip to C:\chef.</span></span>

<span data-ttu-id="a69e0-138">Скопируйте все файлы из расположения chef-starter\chef-repo\.chef в каталог C:\chef.</span><span class="sxs-lookup"><span data-stu-id="a69e0-138">Copy all files under chef-starter\chef-repo\.chef to your c:\chef directory.</span></span>

<span data-ttu-id="a69e0-139">Теперь ваш каталог должен выглядеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a69e0-139">Your directory should now look something like the following example.</span></span>

![][5]

<span data-ttu-id="a69e0-140">У вас должно быть четыре файла, включая файл публикации Azure в корне каталога C:\chef.</span><span class="sxs-lookup"><span data-stu-id="a69e0-140">You should now have four files including the Azure publishing file in the root of c:\chef.</span></span>

<span data-ttu-id="a69e0-141">PEM-файлы содержат закрытые ключи администратора и организации для обеспечения связи, а файл knife.rb содержит конфигурацию knife.</span><span class="sxs-lookup"><span data-stu-id="a69e0-141">The PEM files contain your organization and admin private keys for communication while the knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="a69e0-142">Нам потребуется изменить файл knife.rb.</span><span class="sxs-lookup"><span data-stu-id="a69e0-142">We will need to edit the knife.rb file.</span></span>

<span data-ttu-id="a69e0-143">Откройте файл в предпочитаемом вами редакторе и измените путь cookbook_path, удалив из него "/../" и получив следующий вид:</span><span class="sxs-lookup"><span data-stu-id="a69e0-143">Open the file in your editor of choice and modify the “cookbook_path” by removing the /../ from the path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="a69e0-144">Кроме того, добавьте следующие строки с учетом имени своего файла параметров публикации Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e0-144">Also add the following line reflecting the name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="a69e0-145">Теперь файл knife.rb должен выглядеть как в показанном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="a69e0-145">Your knife.rb file should now look similar to the following example.</span></span>

![][6]

<span data-ttu-id="a69e0-146">Благодаря этим строкам Knife ссылается на каталог подробных инструкций C:\chef\cookbooks, а также использует наш файл параметров публикации Azure во время выполнения операций Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e0-146">These lines will ensure that Knife references the cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-the-chef-development-kit"></a><span data-ttu-id="a69e0-147">Установка пакета средств разработки Chef</span><span class="sxs-lookup"><span data-stu-id="a69e0-147">Installing the Chef Development Kit</span></span>
<span data-ttu-id="a69e0-148">Затем [скачайте и установите](http://downloads.getchef.com/chef-dk/windows) ChefDK (пакет средств разработки Chef) для настройки рабочей станции Chef.</span><span class="sxs-lookup"><span data-stu-id="a69e0-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) the ChefDK (Chef Development Kit) to set up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="a69e0-149">Установите пакет в расположение по умолчанию — C:\opscode.</span><span class="sxs-lookup"><span data-stu-id="a69e0-149">Install in the default location of c:\opscode.</span></span> <span data-ttu-id="a69e0-150">Эта установка займет около 10 минут.</span><span class="sxs-lookup"><span data-stu-id="a69e0-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="a69e0-151">Убедитесь, что переменная PATH содержит записи для путей C:\opscode\chefdk\bin, C:\opscode\chefdk\embedded\bin и C:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin.</span><span class="sxs-lookup"><span data-stu-id="a69e0-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="a69e0-152">Если они отсутствуют, обязательно добавьте эти пути!</span><span class="sxs-lookup"><span data-stu-id="a69e0-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="a69e0-153">*ОБРАТИТЕ ВНИМАНИЕ, ЧТО ВАЖЕН ПОРЯДОК ПУТЕЙ!*</span><span class="sxs-lookup"><span data-stu-id="a69e0-153">*NOTE THE ORDER OF THE PATH IS IMPORTANT!*</span></span> <span data-ttu-id="a69e0-154">Если пути opscode указаны в неправильном порядке, возникнут проблемы.</span><span class="sxs-lookup"><span data-stu-id="a69e0-154">If your opscode paths are not in the correct order you will have issues.</span></span>

<span data-ttu-id="a69e0-155">Прежде чем продолжить, перезагрузите рабочую станцию.</span><span class="sxs-lookup"><span data-stu-id="a69e0-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="a69e0-156">Далее мы установим расширение для Knife Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e0-156">Next, we will install the Knife Azure extension.</span></span> <span data-ttu-id="a69e0-157">Это предоставляет Knife "подключаемый модуль Azure".</span><span class="sxs-lookup"><span data-stu-id="a69e0-157">This provides Knife with the “Azure Plugin”.</span></span>

<span data-ttu-id="a69e0-158">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a69e0-158">Run the following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="a69e0-159">Благодаря аргументу –pre вы получите последнюю версию-кандидат подключаемого модуля Knife для Azure, предоставляющего доступ к актуальному набору API.</span><span class="sxs-lookup"><span data-stu-id="a69e0-159">The –pre argument ensures you are receiving the latest RC version of the Knife Azure Plugin which provides access to the latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="a69e0-160">Вполне вероятно, что в это же время будет установлен набор зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a69e0-160">It’s likely that a number of dependencies will also be installed at the same time.</span></span>

![][8]

<span data-ttu-id="a69e0-161">Чтобы проверить правильность настройки, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="a69e0-161">To ensure everything is configured correctly, run the following command.</span></span>

    knife azure image list

<span data-ttu-id="a69e0-162">Если все настроено правильно, появится прокручиваемый список доступных образов Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e0-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="a69e0-163">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="a69e0-163">Congratulations.</span></span> <span data-ttu-id="a69e0-164">Рабочая станция настроена.</span><span class="sxs-lookup"><span data-stu-id="a69e0-164">The workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="a69e0-165">Создание подробной инструкции</span><span class="sxs-lookup"><span data-stu-id="a69e0-165">Creating a Cookbook</span></span>
<span data-ttu-id="a69e0-166">Подробная инструкция Chef используется для определения набора команд, которые необходимо выполнить на управляемом клиенте.</span><span class="sxs-lookup"><span data-stu-id="a69e0-166">A Cookbook is used by Chef to define a set of commands that you wish to execute on your managed client.</span></span> <span data-ttu-id="a69e0-167">Создание подробной инструкции не вызывает проблем, поэтому для создания шаблона подробной инструкции мы используем команду **chef generate cookbook** .</span><span class="sxs-lookup"><span data-stu-id="a69e0-167">Creating a Cookbook is straightforward and we use the **chef generate cookbook** command to generate our Cookbook template.</span></span> <span data-ttu-id="a69e0-168">Мы назовем свою подробную инструкцию именем webserver, так как нам нужна политика, которая автоматически развертывает службы IIS.</span><span class="sxs-lookup"><span data-stu-id="a69e0-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="a69e0-169">В каталоге C:\Chef выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a69e0-169">Under your C:\Chef directory run the following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="a69e0-170">Будет создан набор файлов в каталоге C:\Chef\cookbooks\webserver.</span><span class="sxs-lookup"><span data-stu-id="a69e0-170">This will generate a set of files under the directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="a69e0-171">Теперь необходимо определить набор команд, который наш клиент Chef должен будет выполнять на управляемой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a69e0-171">We now need to define the set of commands we would like our Chef client to execute on our managed virtual machine.</span></span>

<span data-ttu-id="a69e0-172">Команды хранятся в файле default.rb.</span><span class="sxs-lookup"><span data-stu-id="a69e0-172">The commands are stored in the file default.rb.</span></span> <span data-ttu-id="a69e0-173">В этом файле мы определим набор команд, который устанавливает службы IIS, запускает их и копирует файл шаблона в папку wwwroot.</span><span class="sxs-lookup"><span data-stu-id="a69e0-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file to the wwwroot folder.</span></span>

<span data-ttu-id="a69e0-174">Измените файл C:\chef\cookbooks\webserver\recipes\default.rb и добавьте в него указанные ниже строки.</span><span class="sxs-lookup"><span data-stu-id="a69e0-174">Modify the C:\chef\cookbooks\webserver\recipes\default.rb file and add the following lines.</span></span>

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

<span data-ttu-id="a69e0-175">После завершения работы сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="a69e0-175">Save the file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="a69e0-176">Создание шаблона</span><span class="sxs-lookup"><span data-stu-id="a69e0-176">Creating a template</span></span>
<span data-ttu-id="a69e0-177">Как упоминалось ранее, необходимо создать файл шаблона, который будет использоваться в качестве нашей страницы default.html.</span><span class="sxs-lookup"><span data-stu-id="a69e0-177">As we mentioned previously, we need to generate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="a69e0-178">Выполните следующую команду, чтобы создать шаблон:</span><span class="sxs-lookup"><span data-stu-id="a69e0-178">Run the following command to generate the template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="a69e0-179">Перейдите к файлу C:\chef\cookbooks\webserver\templates\default\Default.htm.erb.</span><span class="sxs-lookup"><span data-stu-id="a69e0-179">Now navigate to the C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="a69e0-180">Добавьте в него простой HTML-код Hello World и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="a69e0-180">Edit the file by adding some simple “Hello World” HTML code, and then save the file.</span></span>

## <a name="upload-the-cookbook-to-the-chef-server"></a><span data-ttu-id="a69e0-181">Передача подробной инструкции на сервер Chef</span><span class="sxs-lookup"><span data-stu-id="a69e0-181">Upload the Cookbook to the Chef Server</span></span>
<span data-ttu-id="a69e0-182">В этом шаге мы отправляем копию подробной инструкции, созданной на локальном компьютере, на размещенный сервер Chef.</span><span class="sxs-lookup"><span data-stu-id="a69e0-182">In this step, we are taking a copy of the Cookbook that we have created on our local machine and uploading it to the Chef Hosted Server.</span></span> <span data-ttu-id="a69e0-183">После передачи подробная инструкция появится на вкладке **Политика** .</span><span class="sxs-lookup"><span data-stu-id="a69e0-183">Once uploaded, the Cookbook will appear under the **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="a69e0-184">Развертывание виртуальной машины с помощью Knife Azure</span><span class="sxs-lookup"><span data-stu-id="a69e0-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="a69e0-185">Теперь мы развернем виртуальную машину Azure и применим подробную инструкцию Webserver, которая установит нашу веб-службу IIS и веб-страницу по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a69e0-185">We will now deploy an Azure virtual machine and apply the “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="a69e0-186">Чтобы сделать это, используйте команду **knife azure server create** .</span><span class="sxs-lookup"><span data-stu-id="a69e0-186">In order to do this, use the **knife azure server create** command.</span></span>

<span data-ttu-id="a69e0-187">Пример этой команды приводится ниже.</span><span class="sxs-lookup"><span data-stu-id="a69e0-187">Am example of the command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="a69e0-188">Названия параметров говорят сами за себя.</span><span class="sxs-lookup"><span data-stu-id="a69e0-188">The parameters are self-explanatory.</span></span> <span data-ttu-id="a69e0-189">Подставьте свои переменные и запустите команду.</span><span class="sxs-lookup"><span data-stu-id="a69e0-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="a69e0-190">Мы автоматизируем работу правил сетевых фильтров конечной точки, используя параметр –tcp-endpoints в командной строке.</span><span class="sxs-lookup"><span data-stu-id="a69e0-190">Through the the command line, I’m also automating my endpoint network filter rules by using the –tcp-endpoints parameter.</span></span> <span data-ttu-id="a69e0-191">Здесь открыты порты 80 и 3389, чтобы обеспечить доступ к веб-странице и сеансу протокола удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="a69e0-191">I’ve opened up ports 80 and 3389 to provide access to my web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="a69e0-192">После выполнения команды перейдите на портал Azure, где можно наблюдать за началом подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a69e0-192">Once you run the command, go to the Azure portal and you will see your machine begin to provision.</span></span>

![][13]

<span data-ttu-id="a69e0-193">Откроется командная строка.</span><span class="sxs-lookup"><span data-stu-id="a69e0-193">The command prompt appears next.</span></span>

![][10]

<span data-ttu-id="a69e0-194">После завершения развертывания мы должны получить возможность подключения к веб-службе через порт 80, так как мы открыли этот порт, когда подготавливали виртуальную машину с помощью команды Knife Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e0-194">Once the deployment is complete, we should be able to connect to the web service over port 80 as we had opened the port when we provisioned the virtual machine with the Knife Azure command.</span></span> <span data-ttu-id="a69e0-195">Поскольку эта виртуальная машина — единственная в моей облачной службе, я подключусь к ней по URL-адресу облачной службы.</span><span class="sxs-lookup"><span data-stu-id="a69e0-195">As this virtual machine is the only virtual machine in my cloud service, I’ll connect it with the cloud service url.</span></span>

![][11]

<span data-ttu-id="a69e0-196">Здесь вы могли наблюдать пример творческого подхода к написанию кода.</span><span class="sxs-lookup"><span data-stu-id="a69e0-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="a69e0-197">Не забывайте, что можно также подключиться через сеанс протокола удаленного рабочего стола с портала Azure через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="a69e0-197">Don’t forget we can also connect through an RDP session from the Azure portal via port 3389.</span></span>

<span data-ttu-id="a69e0-198">Надеюсь, что эта информация была для вас полезной!</span><span class="sxs-lookup"><span data-stu-id="a69e0-198">I hope this has been helpful!</span></span> <span data-ttu-id="a69e0-199">Начинайте использовать подход "инфраструктура как код" прямо сейчас с помощью Azure!</span><span class="sxs-lookup"><span data-stu-id="a69e0-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

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
