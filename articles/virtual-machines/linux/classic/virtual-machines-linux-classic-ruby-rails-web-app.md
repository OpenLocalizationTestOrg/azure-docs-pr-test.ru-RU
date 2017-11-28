---
title: "aaaHost Ruby направляющие веб-сайта на виртуальной Машине Linux | Документы Microsoft"
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
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="2d6a3-103">Веб-приложение Ruby on Rails на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="2d6a3-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="2d6a3-104">В этом учебнике показано как toohost Ruby на веб-сайте направляющие на виртуальных машинах Linux.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-104">This tutorial shows how toohost a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="2d6a3-105">Данный учебник был проверен с использованием Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="2d6a3-106">Если вы используете другой дистрибутив Linux, может потребоваться toomodify hello шаги tooinstall направляющих.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-106">If you use a different Linux distribution, you might need toomodify hello steps tooinstall Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d6a3-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2d6a3-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="2d6a3-108">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="2d6a3-109">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="2d6a3-110">Создание виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="2d6a3-110">Create an Azure VM</span></span>
<span data-ttu-id="2d6a3-111">Начните с создания виртуальной машины Azure с помощью образа Linux.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="2d6a3-112">toocreate Здравствуйте виртуальной Машины, можно использовать портал Azure hello или hello Azure интерфейс командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="2d6a3-112">toocreate hello VM, you can use hello Azure portal or hello Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="2d6a3-113">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="2d6a3-113">Azure portal</span></span>
1. <span data-ttu-id="2d6a3-114">Вход в hello [портал Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="2d6a3-114">Sign into hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="2d6a3-115">Нажмите кнопку **New**, введите «Ubuntu Server 14.04» в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-115">Click **New**, then type "Ubuntu Server 14.04" in hello search box.</span></span> <span data-ttu-id="2d6a3-116">Щелкните запись hello, возвращенных hello поиска.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-116">Click hello entry returned by hello search.</span></span> <span data-ttu-id="2d6a3-117">Модель развертывания hello, выберите **классический**, затем нажмите кнопку «Создать».</span><span class="sxs-lookup"><span data-stu-id="2d6a3-117">For hello deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="2d6a3-118">В колонке основы hello, предоставить значения для hello необходимые поля: имя (для hello виртуальной Машины), имя пользователя, типа проверки подлинности и соответствующие учетные данные hello, подписки Azure, группу ресурсов и расположение.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-118">In hello Basics blade, supply values for hello required fields: Name (for hello VM), User name, Authentication type and hello corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Создание нового образа Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="2d6a3-120">После подготовки виртуальной Машины hello, щелкните имя виртуальной Машины hello и нажмите кнопку **конечные точки** в hello **параметры** категории.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-120">After hello VM is provisioned, click on hello VM name, and click **Endpoints** in hello **Settings** category.</span></span> <span data-ttu-id="2d6a3-121">Найти конечную точку SSH hello, перечисленных в разделе **автономный**.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-121">Find hello SSH endpoint, listed under **Standalone**.</span></span>

   ![Конечная точка по умолчанию](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="2d6a3-123">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="2d6a3-123">Azure CLI</span></span>
<span data-ttu-id="2d6a3-124">Следуйте указаниям hello [создать виртуальную машину под управлением Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="2d6a3-124">Follow hello steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="2d6a3-125">После подготовки виртуальной Машины hello конечную точку SSH hello можно получить, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="2d6a3-125">After hello VM is provisioned, you can get hello SSH endpoint by running hello following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="2d6a3-126">Установка Ruby on Rails</span><span class="sxs-lookup"><span data-stu-id="2d6a3-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="2d6a3-127">С помощью SSH tooconnect toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-127">Use SSH tooconnect toohello VM.</span></span>
2. <span data-ttu-id="2d6a3-128">Из сеанса SSH hello используйте hello после команды tooinstall Ruby на hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="2d6a3-128">From hello SSH session, use hello following commands tooinstall Ruby on hello VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    <span data-ttu-id="2d6a3-129">Hello установка может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-129">hello installation may take a few minutes.</span></span> <span data-ttu-id="2d6a3-130">После завершения использования hello следующая команда tooverify установку Ruby:</span><span class="sxs-lookup"><span data-stu-id="2d6a3-130">When it completes, use hello following command tooverify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="2d6a3-131">Используйте hello следующая команда Направляющие tooinstall:</span><span class="sxs-lookup"><span data-stu-id="2d6a3-131">Use hello following command tooinstall Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="2d6a3-132">Используйте hello--нет rdoc и--флаги нет ri tooskip Установка документации hello, скорость которого выше.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-132">Use hello --no-rdoc and --no-ri flags tooskip installing hello documentation, which is faster.</span></span>
    <span data-ttu-id="2d6a3-133">Эта команда будет скорее всего долго tooexecute, поэтому добавление hello -V будут отображаться сведения о ходе установки hello.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-133">This command will likely take a long time tooexecute, so adding hello -V will display information about hello installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="2d6a3-134">Создание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="2d6a3-134">Create and run an app</span></span>
<span data-ttu-id="2d6a3-135">Хотя по-прежнему вход через SSH, выполните следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="2d6a3-135">While still logged in via SSH, run hello following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="2d6a3-136">Hello [новый](http://guides.rubyonrails.org/command_line.html#rails-new) команда создает новое приложение направляющих.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-136">hello [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="2d6a3-137">Hello [сервера](http://guides.rubyonrails.org/command_line.html#rails-server) команда запускает hello WEBrick веб-сервер, входящий в состав направляющих.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-137">hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts hello WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="2d6a3-138">(Для использования в рабочей среде может потребоваться toouse другого сервера, например единорога или пассажира.)</span><span class="sxs-lookup"><span data-stu-id="2d6a3-138">(For production use, you would probably want toouse a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="2d6a3-139">Вы увидите примерно toohello следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-139">You should see output similar toohello following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="2d6a3-140">Добавление конечной точки</span><span class="sxs-lookup"><span data-stu-id="2d6a3-140">Add an endpoint</span></span>
1. <span data-ttu-id="2d6a3-141">Go toohello [портал Azure] [https://portal.azure.com] и выберите виртуальную Машину.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-141">Go toohello [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="2d6a3-142">Выберите **конечные ТОЧКИ** в hello **параметры** вдоль страницы приветствия hello левого края.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-142">Select **ENDPOINTS** in hello **Settings** along hello left edge hello page.</span></span>

3. <span data-ttu-id="2d6a3-143">Нажмите кнопку **добавить** вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-143">Click **ADD** at hello top of hello page.</span></span>

4. <span data-ttu-id="2d6a3-144">В hello **добавить конечную точку** диалогового окна введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="2d6a3-144">In hello **Add endpoint** dialog page, enter hello following information:</span></span>

   * <span data-ttu-id="2d6a3-145">**Имя**: HTTP.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="2d6a3-146">**Протокол**: TCP</span><span class="sxs-lookup"><span data-stu-id="2d6a3-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="2d6a3-147">**Общий порт**: 80.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-147">**Public port**: 80</span></span>
   * <span data-ttu-id="2d6a3-148">**Частный порт**: 3000.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="2d6a3-149">**Плавающий IP-адрес**: отключен.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="2d6a3-150">**Список управления доступом - порядок**: 1001 или другое значение, которое задает hello приоритет этого правила доступа.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-150">**Access control list - Order**: 1001, or another value that sets hello priority of this access rule.</span></span>
   * <span data-ttu-id="2d6a3-151">**Список управления доступом — имя**: allowHTTP.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="2d6a3-152">**Список управления доступом — действие**: разрешить.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="2d6a3-153">**Список управления доступом — удаленная подсеть**: 1.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="2d6a3-154">Эта конечная точка имеет общий порт 80, которая будет направлять трафик toohello частный порт 3000, где сервер направляющие hello прослушивается.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-154">This endpoint  has a public port of 80 that will route traffic toohello private port of 3000, where hello Rails server is listening.</span></span> <span data-ttu-id="2d6a3-155">правила списка управления доступом Hello позволяет общего трафика через порт 80.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-155">hello access control list rule allows public traffic on port 80.</span></span>

     ![Новая конечная точка](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="2d6a3-157">Нажмите кнопку ОК toosave hello endpoint.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-157">Click OK toosave hello endpoint.</span></span>

6. <span data-ttu-id="2d6a3-158">Должно появиться сообщение о **сохранении конечной точки виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="2d6a3-159">После этого сообщение исчезнет, конечная точка hello активен.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-159">Once this message disappears, hello endpoint is active.</span></span> <span data-ttu-id="2d6a3-160">Теперь может протестировать приложение, перейдя по toohello DNS-имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-160">You may now test your application by navigating toohello DNS name of your virtual machine.</span></span> <span data-ttu-id="2d6a3-161">Hello веб-сайт должен выглядеть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="2d6a3-161">hello website should appear similar toohello following:</span></span>

    ![страница Rails по умолчанию][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="2d6a3-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2d6a3-163">Next steps</span></span>
<span data-ttu-id="2d6a3-164">В этом учебнике вы сделали большинство hello действия вручную.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-164">In this tutorial, you did most of hello steps manually.</span></span> <span data-ttu-id="2d6a3-165">В рабочей среде может создавать приложения на компьютере для разработки и развернуть ее toohello виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-165">In a production environment, you would write your app on a development machine and deploy it toohello Azure VM.</span></span> <span data-ttu-id="2d6a3-166">Кроме того большинство рабочих средах размещения приложения направляющие hello в сочетании с другим процессом сервера, например Apache или NginX, который обрабатывает запрос маршрутизации toomultiple экземпляров приложения hello направляющие и обслуживает статические ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-166">Also, most production environments host hello Rails application in conjunction with another server process such as Apache or NginX, which handles request routing toomultiple instances of hello Rails application and serving static resources.</span></span> <span data-ttu-id="2d6a3-167">Дополнительные сведения см. на странице http://rubyonrails.org/deploy/.</span><span class="sxs-lookup"><span data-stu-id="2d6a3-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="2d6a3-168">toolearn Дополнительные сведения о Ruby на направляющие, посетите hello [Ruby направляющие руководствах по][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="2d6a3-168">toolearn more about Ruby on Rails, visit hello [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="2d6a3-169">toouse Ruby приложения службы Azure см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="2d6a3-169">toouse Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="2d6a3-170">[Хранение неструктурированных данных с использованием BLOB-объектов][blobs]</span><span class="sxs-lookup"><span data-stu-id="2d6a3-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="2d6a3-171">[Хранение пар "ключ-значение" с помощью таблиц][tables]</span><span class="sxs-lookup"><span data-stu-id="2d6a3-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="2d6a3-172">[Обработка содержимого высокой пропускной способностью с hello сеть доставки содержимого][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="2d6a3-172">[Serve high bandwidth content with hello Content Delivery Network][cdn-howto]</span></span>

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
