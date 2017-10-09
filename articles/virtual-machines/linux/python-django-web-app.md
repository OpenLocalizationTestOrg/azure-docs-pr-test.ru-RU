---
title: "aaaPython веб-приложения с Django на виртуальной Машине Linux Azure | Документы Microsoft"
description: "Узнайте, как toohost на основе Django веб-приложения в Azure с помощью виртуальной Машины Linux."
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="12ce1-103">Веб-приложение Hello World на Django на виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="12ce1-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12ce1-104">Windows</span><span class="sxs-lookup"><span data-stu-id="12ce1-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="12ce1-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="12ce1-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="12ce1-106">В этом учебнике показано как toohost веб-сайт на основе Django в Linux в виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="12ce1-106">This tutorial shows you how toohost a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="12ce1-107">В учебнике hello предполагается нет предыдущего опыта работы с Azure.</span><span class="sxs-lookup"><span data-stu-id="12ce1-107">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="12ce1-108">После завершения работы с учебником hello, может иметь приложении Django вверх и работающих в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="12ce1-108">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="12ce1-109">Ниже перечислено, что вы можете узнать.</span><span class="sxs-lookup"><span data-stu-id="12ce1-109">Learn how to:</span></span>

* <span data-ttu-id="12ce1-110">Настройка виртуальной машины Azure toohost Django.</span><span class="sxs-lookup"><span data-stu-id="12ce1-110">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="12ce1-111">Несмотря на то, что в этом учебнике описано как toodo для **Linux**, можно сделать hello одинаково для ВМ Windows Server, размещенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="12ce1-111">Although this tutorial explains how toodo this for **Linux**, you can do hello same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="12ce1-112">Создайте приложение Django в Linux.</span><span class="sxs-lookup"><span data-stu-id="12ce1-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="12ce1-113">Hello учебнике рассказывается о том, как toobuild basic Hello World веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="12ce1-113">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="12ce1-114">приложение Hello размещается на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="12ce1-114">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="12ce1-115">Следующий снимок экрана приветствия показано приложение hello завершена:</span><span class="sxs-lookup"><span data-stu-id="12ce1-115">hello following screenshot shows hello completed application:</span></span>

![Окно браузера отображается страница Hello World hello в Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="12ce1-117">Создание и настройка виртуальной машины Azure toohost Django</span><span class="sxs-lookup"><span data-stu-id="12ce1-117">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="12ce1-118">виртуальной машине Azure с hello распространения Ubuntu Server 14.04 LTS toocreate см [Создание виртуальной машины Linux в hello портал Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="12ce1-118">toocreate an Azure virtual machine with hello Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in hello Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="12ce1-119">Кроме того, можно выбрать проверку пароля вместо открытого ключа SSH.</span><span class="sxs-lookup"><span data-stu-id="12ce1-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="12ce1-120">tooedit hello сетевой безопасности группы tooallow входящих HTTP трафика tooport 80, в разделе [создавать группы безопасности сети в hello портал Azure](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="12ce1-120">tooedit hello network security group tooallow incoming HTTP traffic tooport 80, see [Create network security groups in hello Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="12ce1-121">(Необязательно.) По умолчанию у новой виртуальной машины нет полного доменного имени (FQDN).</span><span class="sxs-lookup"><span data-stu-id="12ce1-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="12ce1-122">toocreate ВМ с полным доменным ИМЕНЕМ в разделе [Создание полного доменного ИМЕНИ в hello портал Azure для виртуальной Машины Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="12ce1-122">toocreate a VM with an FQDN, see [Create an FQDN in hello Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="12ce1-123">Этот шаг не требуется для изучения этого руководства.</span><span class="sxs-lookup"><span data-stu-id="12ce1-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="12ce1-124"><a id="setup"></a>Настроить среду разработки hello</span><span class="sxs-lookup"><span data-stu-id="12ce1-124"><a id="setup"> </a>Set up hello development environment</span></span>
> [!NOTE]
> <span data-ttu-id="12ce1-125">Если нужна tooinstall Python ли toouse hello клиентские библиотеки, см. раздел hello [руководство по установке Python](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="12ce1-125">If you need tooinstall Python or want toouse hello client libraries, see hello [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="12ce1-126">Hello виртуальной Машине Ubuntu Linux имеет предустановлен Python 2.7, но она не поставляется с Apache или Django.</span><span class="sxs-lookup"><span data-stu-id="12ce1-126">hello Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="12ce1-127">Выполните следующие шаги tooconnect tooyour ВМ hello и установите Apache и Django:</span><span class="sxs-lookup"><span data-stu-id="12ce1-127">Complete hello following steps tooconnect tooyour VM and install Apache and Django:</span></span>

1. <span data-ttu-id="12ce1-128">Откройте новое окно терминала.</span><span class="sxs-lookup"><span data-stu-id="12ce1-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="12ce1-129">tooconnect toohello ВМ Azure, введите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="12ce1-129">tooconnect toohello Azure VM, enter hello following command.</span></span> <span data-ttu-id="12ce1-130">Если не удалось создать полное доменное имя, можно подключиться с помощью hello общедоступный IP-адрес, отображаемый в виртуальной машине hello сводки в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="12ce1-130">If you didn't create an FQDN, you can connect by using hello public IP address that's displayed in hello virtual machine summary in hello Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="12ce1-131">tooinstall Django, введите следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="12ce1-131">tooinstall Django, enter hello following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="12ce1-132">tooinstall Apache с остаток от деления wsgi, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="12ce1-132">tooinstall Apache with mod-wsgi, enter hello following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="12ce1-133">Создание приложения Django</span><span class="sxs-lookup"><span data-stu-id="12ce1-133">Create a new Django app</span></span>
1. <span data-ttu-id="12ce1-134">tooaccess SSH toouse виртуальная машина, hello откройте окно терминала, который использовался в предшествующих раздел hello.</span><span class="sxs-lookup"><span data-stu-id="12ce1-134">toouse SSH tooaccess your VM, open hello Terminal window you used in hello preceding section.</span></span>
2. <span data-ttu-id="12ce1-135">toocreate новый проект Django, введите следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="12ce1-135">toocreate a new Django project, enter hello following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="12ce1-136">Hello `django-admin.py` сценарий создает базовую структуру для веб-сайтов на основе Django:</span><span class="sxs-lookup"><span data-stu-id="12ce1-136">hello `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="12ce1-137">`helloworld/manage.py` поможет вам начать и остановить размещение веб-сайта на основе Django.</span><span class="sxs-lookup"><span data-stu-id="12ce1-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="12ce1-138">`helloworld/helloworld/settings.py` содержит настройки Django для приложения.</span><span class="sxs-lookup"><span data-stu-id="12ce1-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="12ce1-139">`helloworld/helloworld/urls.py`имеет кода hello сопоставления между каждого URL-адреса и его представление.</span><span class="sxs-lookup"><span data-stu-id="12ce1-139">`helloworld/helloworld/urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="12ce1-140">В каталоге /var/www/helloworld/helloworld hello создайте новый файл с именем views.py.</span><span class="sxs-lookup"><span data-stu-id="12ce1-140">In hello /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="12ce1-141">Этот файл имеет hello представление, которое отображает hello страницы «hello world».</span><span class="sxs-lookup"><span data-stu-id="12ce1-141">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="12ce1-142">В редакторе кода введите следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="12ce1-142">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="12ce1-143">Замените содержимое файла urls.py hello hello hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="12ce1-143">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="12ce1-144">Настройка Apache</span><span class="sxs-lookup"><span data-stu-id="12ce1-144">Set up Apache</span></span>
1. <span data-ttu-id="12ce1-145">В папке /etc/apache2/sites-available/helloworld.conf hello создайте файл конфигурации виртуальный узел Apache.</span><span class="sxs-lookup"><span data-stu-id="12ce1-145">In hello /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="12ce1-146">Задайте следующие значения toohello содержимое hello.</span><span class="sxs-lookup"><span data-stu-id="12ce1-146">Set hello contents toohello following values.</span></span> <span data-ttu-id="12ce1-147">Замените *yourVmName* hello фактическое имя машины hello используется (например, *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="12ce1-147">Replace *yourVmName* with hello actual name of hello machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="12ce1-148">узел tooactivate hello hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="12ce1-148">tooactivate hello site, use hello following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="12ce1-149">toorestart Apache hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="12ce1-149">toorestart Apache, use hello following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="12ce1-150">Загрузка hello веб-страницу в браузере.</span><span class="sxs-lookup"><span data-stu-id="12ce1-150">Load hello webpage in your browser:</span></span>
   
   ![Окно обозревателя отображает hello hello world страницу в Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="12ce1-152">Завершение работы виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="12ce1-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="12ce1-153">После завершения работы с учебником, рекомендуется завершить работу или удаление виртуальной Машины Azure, созданную для учебника hello hello.</span><span class="sxs-lookup"><span data-stu-id="12ce1-153">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="12ce1-154">Это позволит освободить ресурсы для работы с другими руководствами, а также избежать расходов за использование Azure.</span><span class="sxs-lookup"><span data-stu-id="12ce1-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

