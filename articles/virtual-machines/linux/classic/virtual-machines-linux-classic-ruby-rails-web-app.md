---
title: "Размещение веб-сайта Ruby on Rails в виртуальной машине Linux | Документация Майкрософт"
description: "Настройка и размещение веб-сайта на основе Ruby on Rails в Azure с помощью виртуальной машины Linux."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: 0518519da6c5e62a863a47d6743ab7b7c5923acf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="d56d4-103">Веб-приложение Ruby on Rails на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="d56d4-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="d56d4-104">В этом учебнике описано, как разместить веб-сайт Ruby on Rails в Azure с помощью виртуальной машины Linux.</span><span class="sxs-lookup"><span data-stu-id="d56d4-104">This tutorial shows how to host a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="d56d4-105">Данный учебник был проверен с использованием Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="d56d4-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="d56d4-106">Если вы используете другой дистрибутив Linux, могут потребоваться другие действия для установления Rails.</span><span class="sxs-lookup"><span data-stu-id="d56d4-106">If you use a different Linux distribution, you might need to modify the steps to install Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d56d4-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d56d4-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d56d4-108">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="d56d4-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="d56d4-109">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d56d4-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="d56d4-110">Создание виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="d56d4-110">Create an Azure VM</span></span>
<span data-ttu-id="d56d4-111">Начните с создания виртуальной машины Azure с помощью образа Linux.</span><span class="sxs-lookup"><span data-stu-id="d56d4-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="d56d4-112">Чтобы создать виртуальную машину, можно использовать портал Azure или интерфейс командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="d56d4-112">To create the VM, you can use the Azure portal or the Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="d56d4-113">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d56d4-113">Azure portal</span></span>
1. <span data-ttu-id="d56d4-114">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d56d4-114">Sign into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="d56d4-115">Щелкните **Создать**, затем в поле поиска введите "Ubuntu Server 14.04".</span><span class="sxs-lookup"><span data-stu-id="d56d4-115">Click **New**, then type "Ubuntu Server 14.04" in the search box.</span></span> <span data-ttu-id="d56d4-116">Щелкните запись, полученную в результате поиска.</span><span class="sxs-lookup"><span data-stu-id="d56d4-116">Click the entry returned by the search.</span></span> <span data-ttu-id="d56d4-117">Чтобы указать модель развертывания, выберите **Классическая**, и нажмите кнопку "Создать".</span><span class="sxs-lookup"><span data-stu-id="d56d4-117">For the deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="d56d4-118">В колонке "Основные" укажите следующие значения в обязательных полях: имя (для виртуальной машины), имя пользователя, тип аутентификации и соответствующие учетные данные, подписку Azure, группу ресурсов и расположение.</span><span class="sxs-lookup"><span data-stu-id="d56d4-118">In the Basics blade, supply values for the required fields: Name (for the VM), User name, Authentication type and the corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Создание нового образа Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="d56d4-120">После подготовки виртуальной машины выберите ее имя и щелкните **Конечные точки** в категории **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="d56d4-120">After the VM is provisioned, click on the VM name, and click **Endpoints** in the **Settings** category.</span></span> <span data-ttu-id="d56d4-121">Найдите конечную точку SSH в списке **Автономная**.</span><span class="sxs-lookup"><span data-stu-id="d56d4-121">Find the SSH endpoint, listed under **Standalone**.</span></span>

   ![Конечная точка по умолчанию](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="d56d4-123">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="d56d4-123">Azure CLI</span></span>
<span data-ttu-id="d56d4-124">Выполните действия в статье [Создание виртуальной машины под управлением Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="d56d4-124">Follow the steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="d56d4-125">После подготовки виртуальной машины можно получить конечную точку SSH, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d56d4-125">After the VM is provisioned, you can get the SSH endpoint by running the following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="d56d4-126">Установка Ruby on Rails</span><span class="sxs-lookup"><span data-stu-id="d56d4-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="d56d4-127">Используйте SSH, чтобы подключиться к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="d56d4-127">Use SSH to connect to the VM.</span></span>
2. <span data-ttu-id="d56d4-128">В сеансе SSH выполните следующие команды, чтобы установить Ruby на виртуальной машине:</span><span class="sxs-lookup"><span data-stu-id="d56d4-128">From the SSH session, use the following commands to install Ruby on the VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > The brightbox repository contains the current Ruby distribution.

    <span data-ttu-id="d56d4-129">Установка может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d56d4-129">The installation may take a few minutes.</span></span> <span data-ttu-id="d56d4-130">После завершения воспользуйтесь следующей командой, чтобы проверить установку Ruby:</span><span class="sxs-lookup"><span data-stu-id="d56d4-130">When it completes, use the following command to verify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="d56d4-131">Используйте следующую команду для установки Rails:</span><span class="sxs-lookup"><span data-stu-id="d56d4-131">Use the following command to install Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="d56d4-132">С помощью флагов --no-rdoc и --no-ri можно пропустить установку документации, что значительно ускорит процесс.</span><span class="sxs-lookup"><span data-stu-id="d56d4-132">Use the --no-rdoc and --no-ri flags to skip installing the documentation, which is faster.</span></span>
    <span data-ttu-id="d56d4-133">Вероятно, эта команда будет долго выполняться. Добавив параметр -V, вы сможете наблюдать за ходом установки.</span><span class="sxs-lookup"><span data-stu-id="d56d4-133">This command will likely take a long time to execute, so adding the -V will display information about the installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="d56d4-134">Создание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="d56d4-134">Create and run an app</span></span>
<span data-ttu-id="d56d4-135">Войдите в систему через SSH и выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="d56d4-135">While still logged in via SSH, run the following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="d56d4-136">Команда [new](http://guides.rubyonrails.org/command_line.html#rails-new) создает новое приложение Rails.</span><span class="sxs-lookup"><span data-stu-id="d56d4-136">The [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="d56d4-137">Команда [server](http://guides.rubyonrails.org/command_line.html#rails-server) запускает веб-сервер WEBrick, входящий в состав Rails.</span><span class="sxs-lookup"><span data-stu-id="d56d4-137">The [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts the WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="d56d4-138">(В рабочей среде вы, вероятно, будете использовать другой сервер, например Unicorn или Passenger).</span><span class="sxs-lookup"><span data-stu-id="d56d4-138">(For production use, you would probably want to use a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="d56d4-139">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="d56d4-139">You should see output similar to the following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C to shutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="d56d4-140">Добавление конечной точки</span><span class="sxs-lookup"><span data-stu-id="d56d4-140">Add an endpoint</span></span>
1. <span data-ttu-id="d56d4-141">Перейдите на [портал Azure][https://portal.azure.com] и выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d56d4-141">Go to the [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="d56d4-142">Выберите **Конечные точки** в категории **Параметры** у левого края страницы.</span><span class="sxs-lookup"><span data-stu-id="d56d4-142">Select **ENDPOINTS** in the **Settings** along the left edge the page.</span></span>

3. <span data-ttu-id="d56d4-143">В верхней части страницы щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d56d4-143">Click **ADD** at the top of the page.</span></span>

4. <span data-ttu-id="d56d4-144">На диалоговой странице **Добавление конечной точки** введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="d56d4-144">In the **Add endpoint** dialog page, enter the following information:</span></span>

   * <span data-ttu-id="d56d4-145">**Имя**: HTTP.</span><span class="sxs-lookup"><span data-stu-id="d56d4-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="d56d4-146">**Протокол**: TCP</span><span class="sxs-lookup"><span data-stu-id="d56d4-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="d56d4-147">**Общий порт**: 80.</span><span class="sxs-lookup"><span data-stu-id="d56d4-147">**Public port**: 80</span></span>
   * <span data-ttu-id="d56d4-148">**Частный порт**: 3000.</span><span class="sxs-lookup"><span data-stu-id="d56d4-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="d56d4-149">**Плавающий IP-адрес**: отключен.</span><span class="sxs-lookup"><span data-stu-id="d56d4-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="d56d4-150">**Список управления доступом — порядок**: 1001 или другое значение, которое задает приоритет этого правила доступа.</span><span class="sxs-lookup"><span data-stu-id="d56d4-150">**Access control list - Order**: 1001, or another value that sets the priority of this access rule.</span></span>
   * <span data-ttu-id="d56d4-151">**Список управления доступом — имя**: allowHTTP.</span><span class="sxs-lookup"><span data-stu-id="d56d4-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="d56d4-152">**Список управления доступом — действие**: разрешить.</span><span class="sxs-lookup"><span data-stu-id="d56d4-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="d56d4-153">**Список управления доступом — удаленная подсеть**: 1.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="d56d4-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="d56d4-154">У этой конечной точки есть общий порт 80, который будет применяться для маршрутизации трафика на частный порт 3000, на котором сервер Rails ожидает передачи данных.</span><span class="sxs-lookup"><span data-stu-id="d56d4-154">This endpoint  has a public port of 80 that will route traffic to the private port of 3000, where the Rails server is listening.</span></span> <span data-ttu-id="d56d4-155">Правило списка управления доступом разрешает передачу общего трафика через порт 80.</span><span class="sxs-lookup"><span data-stu-id="d56d4-155">The access control list rule allows public traffic on port 80.</span></span>

     ![Новая конечная точка](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="d56d4-157">Нажмите кнопку "ОК", чтобы сохранить конечную точку.</span><span class="sxs-lookup"><span data-stu-id="d56d4-157">Click OK to save the endpoint.</span></span>

6. <span data-ttu-id="d56d4-158">Должно появиться сообщение о **сохранении конечной точки виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="d56d4-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="d56d4-159">После того как сообщение исчезнет, конечная точка будет активирована.</span><span class="sxs-lookup"><span data-stu-id="d56d4-159">Once this message disappears, the endpoint is active.</span></span> <span data-ttu-id="d56d4-160">Теперь вы можете протестировать приложение, перейдя к имени DNS виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d56d4-160">You may now test your application by navigating to the DNS name of your virtual machine.</span></span> <span data-ttu-id="d56d4-161">Веб-сайт должен выглядеть аналогично следующему:</span><span class="sxs-lookup"><span data-stu-id="d56d4-161">The website should appear similar to the following:</span></span>

    ![страница Rails по умолчанию][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="d56d4-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d56d4-163">Next steps</span></span>
<span data-ttu-id="d56d4-164">В этом учебнике большинство действий вы выполняли вручную.</span><span class="sxs-lookup"><span data-stu-id="d56d4-164">In this tutorial, you did most of the steps manually.</span></span> <span data-ttu-id="d56d4-165">В рабочей среде вы напишете приложение на компьютере для разработки и развернете его на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="d56d4-165">In a production environment, you would write your app on a development machine and deploy it to the Azure VM.</span></span> <span data-ttu-id="d56d4-166">Кроме того, большинство рабочих сред размещают приложение Rails вместе с другим серверным процессом, например Apache или NginX, который обрабатывает маршрутизацию запросов к нескольким экземплярам приложения Rails и обслуживает статические ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d56d4-166">Also, most production environments host the Rails application in conjunction with another server process such as Apache or NginX, which handles request routing to multiple instances of the Rails application and serving static resources.</span></span> <span data-ttu-id="d56d4-167">Дополнительные сведения см. на странице http://rubyonrails.org/deploy/.</span><span class="sxs-lookup"><span data-stu-id="d56d4-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="d56d4-168">Дополнительные сведения о Ruby on Rails см. на веб-сайте [руководств по Ruby on Rails][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="d56d4-168">To learn more about Ruby on Rails, visit the [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="d56d4-169">Об использовании служб Azure из приложения Ruby можно узнать из следующих материалов:</span><span class="sxs-lookup"><span data-stu-id="d56d4-169">To use Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="d56d4-170">[Хранение неструктурированных данных с использованием BLOB-объектов][blobs]</span><span class="sxs-lookup"><span data-stu-id="d56d4-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="d56d4-171">[Хранение пар "ключ-значение" с помощью таблиц][tables]</span><span class="sxs-lookup"><span data-stu-id="d56d4-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="d56d4-172">[Передача контента с широкой полосой пропускания с помощью CDN][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="d56d4-172">[Serve high bandwidth content with the Content Delivery Network][cdn-howto]</span></span>

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
