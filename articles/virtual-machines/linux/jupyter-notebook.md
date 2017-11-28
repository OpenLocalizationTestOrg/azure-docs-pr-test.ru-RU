---
title: "aaaCreate книжки Jupyter и IPython | Документы Microsoft"
description: "Дополнительные сведения, способ создания toodeploy hello записной книжки Jupyter и IPython на виртуальной машине Linux с помощью модели развертывания диспетчера ресурсов hello в Azure."
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="e97d5-103">Создание виртуальной машины Azure, установка Jupyter и запуск Jupyter Notebook в Azure</span><span class="sxs-lookup"><span data-stu-id="e97d5-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="e97d5-104">Hello [проекта Jupyter](http://jupyter.org), ранее hello [IPython проекта](http://ipython.org), предоставляет набор средств для научных вычислений с помощью мощных интерактивный оболочек, объединяющие выполнения кода с помощью создания hello Динамическая вычислительных документа.</span><span class="sxs-lookup"><span data-stu-id="e97d5-104">hello [Jupyter project](http://jupyter.org), formerly hello [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with hello creation of a live computational document.</span></span> <span data-ttu-id="e97d5-105">Эти файлы записной книжки могут содержать произвольный текст, математические формулы, код ввода, результаты, графику, видео и любые другие виды носителей, которые может отображать современный веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="e97d5-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="e97d5-106">Вы будете абсолютно новый tooPython и требуется toolearn его в fun, интерактивную среду или выполните некоторые серьезные параллельного или технической вычислений, hello книжке Jupyter очень удобно.</span><span class="sxs-lookup"><span data-stu-id="e97d5-106">Whether you're absolutely new tooPython and want toolearn it in a fun, interactive environment or do some serious parallel/technical computing, hello Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="e97d5-107">![Снимок экрана](./media/jupyter-notebook/ipy-notebook-spectral.png) с помощью SciPy и Matplotlib пакетов tooanalyze hello структуры запись звука.</span><span class="sxs-lookup"><span data-stu-id="e97d5-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages tooanalyze hello structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="e97d5-108">Два способа реализации Jupyter: Azure Notebook или пользовательское развертывание</span><span class="sxs-lookup"><span data-stu-id="e97d5-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="e97d5-109">Azure предоставляет службу, можно использовать слишком[быстро начать использовать Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="e97d5-109">Azure provides a service that you can use too[quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="e97d5-110">С помощью hello записной книжки службы Azure, можно легко получить tooJupyter доступ веб-интерфейса для масштабируемый вычислительные ресурсы со всех hello возможности Python и его многие библиотеки.</span><span class="sxs-lookup"><span data-stu-id="e97d5-110">By using hello Azure Notebook Service, you can easily gain access tooJupyter's web-accessible interface to scalable computational resources with all hello power of Python and its many libraries.</span></span>  <span data-ttu-id="e97d5-111">С момента установки hello обрабатывается службой hello, пользователи могут доступа к этим ресурсам без необходимости hello администрирования и настройки пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="e97d5-111">Since hello installation is handled by hello service, users can access these resources without hello need for administration and configuration by hello user.</span></span>

<span data-ttu-id="e97d5-112">Если служба записной книжки hello не работает для вашего сценария продолжайте tooread в этой статье, который будет будет показано, как toodeploy hello книжке Jupyter на базе Microsoft Azure с помощью Linux виртуальных машин (ВМ).</span><span class="sxs-lookup"><span data-stu-id="e97d5-112">If hello notebook service does not work for your scenario please continue tooread this article which will will show you how toodeploy hello Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="e97d5-113">Создание и настройка виртуальной машины в Azure</span><span class="sxs-lookup"><span data-stu-id="e97d5-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="e97d5-114">Hello первым шагом является toocreate виртуальной машины (VM), работающей в Azure.</span><span class="sxs-lookup"><span data-stu-id="e97d5-114">hello first step is toocreate a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="e97d5-115">Эта виртуальная машина является всей операционной системы в облаке hello и будет использоваться для запуска hello книжке Jupyter.</span><span class="sxs-lookup"><span data-stu-id="e97d5-115">This VM is a complete operating system in hello cloud and will be used to run hello Jupyter Notebook.</span></span> <span data-ttu-id="e97d5-116">Способен работающих виртуальных машин Linux и Windows Azure, и мы рассмотрим hello установки Jupyter и другие виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e97d5-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover hello setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="e97d5-117">Создание виртуальной Машины Linux и открытие порта для Jupyter</span><span class="sxs-lookup"><span data-stu-id="e97d5-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="e97d5-118">Следуйте инструкциям hello [здесь] [ portal-vm-linux] toocreate виртуальной машины из hello *Ubuntu* распространения.</span><span class="sxs-lookup"><span data-stu-id="e97d5-118">Follow hello instructions given [here][portal-vm-linux] toocreate a virtual machine of hello *Ubuntu* distribution.</span></span> <span data-ttu-id="e97d5-119">В этом учебнике используется Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="e97d5-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="e97d5-120">Предположим, имя пользователя hello *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="e97d5-120">We'll assume hello user name *azureuser*.</span></span>

<span data-ttu-id="e97d5-121">После развертывает hello виртуальной машины необходимо tooopen правило безопасности для групп безопасности сети hello.</span><span class="sxs-lookup"><span data-stu-id="e97d5-121">After hello virtual machine deploys we need tooopen up a security rule on hello network security group.</span></span>  <span data-ttu-id="e97d5-122">С hello портал Azure, откройте слишком**сетевых групп безопасности** и Привет открыть вкладку tooyour соответствующей группы безопасности hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e97d5-122">From hello Azure portal, go too**Network Security Groups** and open hello tab for hello Security Group corresponding tooyour VM.</span></span> <span data-ttu-id="e97d5-123">Требуется tooadd правило безопасности для входящего трафика с hello следующие параметры: **TCP** для протокола hello  **\***  для hello порт источника (public) и **9999** для порт назначения (private) Hello.</span><span class="sxs-lookup"><span data-stu-id="e97d5-123">You need tooadd an Inbound Security rule with hello following settings: **TCP** for hello protocol, **\*** for hello source (public) port and **9999** for hello destination (private) port.</span></span>

![Снимок экрана](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="e97d5-125">В группе безопасности сети, нажмите кнопку **сетевых интерфейсов** и Примечание hello **общедоступный IP-адрес** как необходимые tooconnect tooyour ВМ будет находиться в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="e97d5-125">While in your Network Security Group, click on **Network Interfaces** and note hello **Public IP Address** as it will be needed tooconnect tooyour VM in hello next step.</span></span>

## <a name="install-required-software-on-hello-vm"></a><span data-ttu-id="e97d5-126">Установите необходимое программное обеспечение на hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="e97d5-126">Install required software on hello VM</span></span>
<span data-ttu-id="e97d5-127">toorun Здравствуйте записной книжки Jupyter на нашем виртуальной Машины, нам необходимо сначала установить Jupyter и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="e97d5-127">toorun hello Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="e97d5-128">Подключите tooyour виртуальных машин linux с помощью ssh и hello пары имя пользователя и пароль, выбранный при создании hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e97d5-128">Connect tooyour linux vm using ssh and hello username/password pair you chose when you created hello vm.</span></span> <span data-ttu-id="e97d5-129">В этом учебнике используется PuTTY и подключение из Windows.</span><span class="sxs-lookup"><span data-stu-id="e97d5-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="e97d5-130">Установка Jupyter на Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e97d5-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="e97d5-131">Установите распространения python обработки и анализа данных популярных, Anaconda, с помощью одного из hello ссылки из [компания Continuum Analytics](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="e97d5-131">Install Anaconda, a popular data science python distribution, using one of hello links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="e97d5-132">На момент написания данного документа hello, hello следующие ссылки являются hello наиболее вверх toodate версии.</span><span class="sxs-lookup"><span data-stu-id="e97d5-132">As of hello writing of this document, hello below links are hello most up toodate versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="e97d5-133">Дистрибутивы Anaconda для Linux</span><span class="sxs-lookup"><span data-stu-id="e97d5-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="e97d5-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="e97d5-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="e97d5-135">Python 2,7</span><span class="sxs-lookup"><span data-stu-id="e97d5-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="e97d5-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64-разрядная</href>
    </span><span class="sxs-lookup"><span data-stu-id="e97d5-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="e97d5-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64-разрядная</href>
    </span><span class="sxs-lookup"><span data-stu-id="e97d5-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e97d5-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32-разрядная</href>
    </span><span class="sxs-lookup"><span data-stu-id="e97d5-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="e97d5-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32-разрядная</href>
    </span><span class="sxs-lookup"><span data-stu-id="e97d5-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="e97d5-140">Установка 64-разрядной версии Anaconda 3 2.3.0 на Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e97d5-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="e97d5-141">Приведем пример установки Anaconda на Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="e97d5-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Снимок экрана](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="e97d5-143">Настройка Jupyter и использование протокола SSL</span><span class="sxs-lookup"><span data-stu-id="e97d5-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="e97d5-144">После установки нужно tootake файлы конфигурации момент hello toosetup для Jupyter.</span><span class="sxs-lookup"><span data-stu-id="e97d5-144">After installing we need tootake a moment toosetup hello configuration files for Jupyter.</span></span> <span data-ttu-id="e97d5-145">Если возникают проблемы с настройкой Jupyter часто бывает полезно toolook на hello [сервер записной книжки Jupyter документации](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="e97d5-145">If you experience troubles with configuring Jupyter it may be helpful toolook at hello [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="e97d5-146">Далее мы `cd` toohello профиль directory toocreate нашей SSL-сертификат и изменить файл конфигурации профилей hello.</span><span class="sxs-lookup"><span data-stu-id="e97d5-146">Next we `cd` toohello profile directory toocreate our SSL certificate and edit hello profiles configuration file.</span></span>

<span data-ttu-id="e97d5-147">В Linux используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="e97d5-147">On Linux use hello following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="e97d5-148">Используйте hello, следующая команда toocreate hello SSL-сертификат (Linux и Windows).</span><span class="sxs-lookup"><span data-stu-id="e97d5-148">Use hello following command toocreate hello SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="e97d5-149">Обратите внимание, что создания самозаверяющего сертификата SSL, при подключении записной книжки toohello браузере выдаст предупреждение системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="e97d5-149">Note that since we are creating a self-signed SSL certificate, when connecting toohello notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="e97d5-150">Для долгосрочного применения в рабочей среде может потребоваться toouse должным образом подписанный сертификат, связанный с вашей организацией.</span><span class="sxs-lookup"><span data-stu-id="e97d5-150">For long-term production use, you will want toouse a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="e97d5-151">Так как сертификат управления выходит за область действия этой демонстрации hello, мы будем придерживаться tooa самозаверяющий сертификат сейчас.</span><span class="sxs-lookup"><span data-stu-id="e97d5-151">Since certificate management is beyond hello scope of this demo, we will stick tooa self-signed certificate for now.</span></span>

<span data-ttu-id="e97d5-152">В дополнение к этому toousing сертификат, необходимо также указать tooprotect пароль портативного компьютера от несанкционированного использования.</span><span class="sxs-lookup"><span data-stu-id="e97d5-152">In addition toousing a certificate, you must also provide a password tooprotect your notebook from unauthorized use.</span></span>  <span data-ttu-id="e97d5-153">По соображениям безопасности Jupyter используется зашифрованные пароли в файле конфигурации, поэтому вам понадобится tooencrypt пароль сначала.</span><span class="sxs-lookup"><span data-stu-id="e97d5-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need tooencrypt your password first.</span></span>  <span data-ttu-id="e97d5-154">IPython предоставляет toodo программы. в командной строке выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="e97d5-154">IPython provides a utility toodo so; at a command prompt run hello following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="e97d5-155">Это предложит ввести пароль и подтверждение, а затем будет напечатать пароль hello.</span><span class="sxs-lookup"><span data-stu-id="e97d5-155">This will prompt you for a password and confirmation, and will then print hello password.</span></span> <span data-ttu-id="e97d5-156">Запомнить, что даст hello.</span><span class="sxs-lookup"><span data-stu-id="e97d5-156">Note this for hello following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

<span data-ttu-id="e97d5-157">Далее мы внесем изменения файла конфигурации hello профиля, который имеет `jupyter_notebook_config.py` в каталоге hello в файл.</span><span class="sxs-lookup"><span data-stu-id="e97d5-157">Next, we will edit hello profile's configuration file, which is the `jupyter_notebook_config.py` file in hello directory you are in.</span></span>  <span data-ttu-id="e97d5-158">Обратите внимание, что этот файл не существует — просто создать противном случае hello.</span><span class="sxs-lookup"><span data-stu-id="e97d5-158">Note that this file may not exist -- just create it if that is hello case.</span></span>  <span data-ttu-id="e97d5-159">Этот файл содержит несколько полей, которые по умолчанию закомментированы.  Этот файл можно открыть в любом текстовом редакторе из желанию и следует убедиться, что он имеет по крайней мере Здравствуйте, после содержимого.</span><span class="sxs-lookup"><span data-stu-id="e97d5-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least hello following content.</span></span> <span data-ttu-id="e97d5-160">**Быть убедиться, что c.NotebookApp.password tooreplace hello в hello конфигурации с помощью sha1 hello из предыдущего шага hello**.</span><span class="sxs-lookup"><span data-stu-id="e97d5-160">**Be sure tooreplace hello c.NotebookApp.password in hello config with hello sha1 from hello previous step**.</span></span>

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a><span data-ttu-id="e97d5-161">Запустите hello книжке Jupyter</span><span class="sxs-lookup"><span data-stu-id="e97d5-161">Run hello Jupyter Notebook</span></span>
<span data-ttu-id="e97d5-162">На этом этапе не готов toostart hello книжке Jupyter.</span><span class="sxs-lookup"><span data-stu-id="e97d5-162">At this point we are ready toostart hello Jupyter Notebook.</span></span> <span data-ttu-id="e97d5-163">toodo это, перейдите в каталог toohello toostore записных книжек и начать hello server книжке Jupyter с hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e97d5-163">toodo this, navigate toohello directory you want toostore notebooks in and start hello Jupyter Notebook server with hello following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="e97d5-164">Теперь должна быть блокнота Jupyter по адресу hello может tooaccess `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="e97d5-164">You should now be able tooaccess your Jupyter Notebook at hello address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="e97d5-165">При первом обращении к записной страницы входа hello запрашивает пароль.</span><span class="sxs-lookup"><span data-stu-id="e97d5-165">When you first access your notebook, hello login page asks for your password.</span></span> <span data-ttu-id="e97d5-166">И после входа, вы увидите «Мониторинга записной книжки Jupyter,» hello которого является центр непечатаемые для всех операций в записной книжке.</span><span class="sxs-lookup"><span data-stu-id="e97d5-166">And once you log in, you will see hello "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="e97d5-167">На этой странице можно создать новые записные книжки и открывать существующие:</span><span class="sxs-lookup"><span data-stu-id="e97d5-167">From this page you can create new notebooks and open existing ones.</span></span>

![Снимок экрана](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a><span data-ttu-id="e97d5-169">С помощью hello книжке Jupyter</span><span class="sxs-lookup"><span data-stu-id="e97d5-169">Using hello Jupyter Notebook</span></span>
<span data-ttu-id="e97d5-170">Если щелкнуть hello **New** кнопки, вы увидите после открытия страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="e97d5-170">If you click hello **New** button, you will see hello following opening page.</span></span>

![Снимок экрана](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="e97d5-172">область Hello, отмеченные `In []:` является область ввода hello и здесь можно ввести любой допустимый код Python, и он будет выполняться при достижении `Shift-Enter` или щелкните значок «Play» hello (hello указывающий направо треугольник в hello инструментов).</span><span class="sxs-lookup"><span data-stu-id="e97d5-172">hello area marked with an `In []:` prompt is hello input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on hello "Play" icon (hello right-pointing triangle in hello toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="e97d5-173">Мощная парадигма: документы с вычислениями в режиме реального времени и богатыми возможностями мультимедиа</span><span class="sxs-lookup"><span data-stu-id="e97d5-173">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="e97d5-174">ноутбук Hello сам должно быть очень естественный tooanyone, который использовал Python и текстовые редакторы, так как он находится в некотором смысле их комбинацию: могут выполняться блоков кода Python, но могут также содержать заметки и другой текст, изменив слишком стиль hello в ячейке «Code» «Ma rkdown» с помощью hello раскрывающееся меню в панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="e97d5-174">hello notebook itself should feel very natural tooanyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing hello style of a cell from "Code" too"Markdown" using hello drop-down menu in the toolbar.</span></span>

<span data-ttu-id="e97d5-175">Но это гораздо больше, чем текстовый процессор, так как Jupyter позволяет совмещать вычисления и широкие возможности мультимедиа (текст, графику, видео и практически любые данные, которые способен отображать современный браузер).</span><span class="sxs-lookup"><span data-stu-id="e97d5-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="e97d5-176">Вы можете комбинировать текст, код, видео и многое другое!</span><span class="sxs-lookup"><span data-stu-id="e97d5-176">You can mix, text, code, videos and more!</span></span>

![Снимок экрана](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="e97d5-178">И мощность hello многие отлично библиотеки Python для научных и технических вычислений, в следующий снимок экрана, hello простых вычислений могут быть выполнены с hello облегчают же, как анализ сложную сеть, все в одной среде.</span><span class="sxs-lookup"><span data-stu-id="e97d5-178">And with hello power of Python's many excellent libraries for scientific and technical computing, in hello following screenshot, a simple calculation can be performed with hello same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="e97d5-179">Это парадигма совпадением power hello современных веб-hello и динамической вычисление предлагает множество возможностей и идеально подходит для облака hello. можно использовать Hello записной книжки:</span><span class="sxs-lookup"><span data-stu-id="e97d5-179">This paradigm of mixing hello power of hello modern web with live computation offers many possibilities, and is ideally suited for hello cloud; hello Notebook can be used:</span></span>

* <span data-ttu-id="e97d5-180">Вычислительные пометок toorecord произвольного вместе на неполадки.</span><span class="sxs-lookup"><span data-stu-id="e97d5-180">As a computational scratchpad toorecord exploratory work on a problem.</span></span>
* <span data-ttu-id="e97d5-181">tooshare результаты с коллегами в форме «live» вычислений или Бумажная копия форматов (HTML, PDF).</span><span class="sxs-lookup"><span data-stu-id="e97d5-181">tooshare results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="e97d5-182">toodistribute и присутствует динамической преподавателя материалов, которые включать в себя вычисления, поэтому учащихся немедленно можно поэкспериментировать с кодом реальных hello, измените его и повторно выполните ее интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="e97d5-182">toodistribute and present live teaching materials that involve computation, so students can immediately experiment with hello real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="e97d5-183">tooprovide «исполняемый документы», предоставляющие hello результаты запроса в виде, можно немедленно воспроизвести, проверки и расширены за счет других.</span><span class="sxs-lookup"><span data-stu-id="e97d5-183">tooprovide "executable papers" that present hello results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="e97d5-184">Как платформу для совместной работы: несколько пользователи могут входить в toothe же записной книжки server tooshare динамической вычислительных сеанс.</span><span class="sxs-lookup"><span data-stu-id="e97d5-184">As a platform for collaborative computing: multiple users can log in toothe same notebook server tooshare a live computational session.</span></span>

<span data-ttu-id="e97d5-185">При переходе в исходном коде toohello IPython [репозитория][repository], вы найдете весь каталог с примерами ноутбук, которых можно загрузить и затем поэкспериментировать с на виртуальной Машине Jupyter собственные Azure.</span><span class="sxs-lookup"><span data-stu-id="e97d5-185">If you go toohello IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="e97d5-186">Просто загрузите hello `.ipynb` файлы из hello сайта и передать их в панель мониторинга hello записной виртуальной Машины Azure (или загрузить их непосредственно в hello виртуальной Машины).</span><span class="sxs-lookup"><span data-stu-id="e97d5-186">Simply download hello `.ipynb` files from hello site and upload them onto hello dashboard of your notebook Azure VM (or download them directly into hello VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="e97d5-187">Заключение</span><span class="sxs-lookup"><span data-stu-id="e97d5-187">Conclusion</span></span>
<span data-ttu-id="e97d5-188">Hello книжке Jupyter предоставляет мощный интерфейс для доступа к интерактивно power hello hello экосистемы Python в Azure.</span><span class="sxs-lookup"><span data-stu-id="e97d5-188">hello Jupyter Notebook provides a powerful interface for accessing interactively hello power of hello Python ecosystem on Azure.</span></span>  <span data-ttu-id="e97d5-189">Он охватывает широкий диапазон вариантов использования, включая простой просмотр и изучения Python, анализ данных и визуализацию, моделирование и параллельные вычисления.</span><span class="sxs-lookup"><span data-stu-id="e97d5-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="e97d5-190">Hello итоговые записной книжки документы содержат полную запись hello вычислений, которые выполняются, а также можно использовать совместно с другими пользователями Jupyter.</span><span class="sxs-lookup"><span data-stu-id="e97d5-190">hello resulting Notebook documents contain a complete record of hello computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="e97d5-191">Hello книжке Jupyter можно использовать в качестве локального приложения, но идеально подходит для развертывания в облаке в Azure</span><span class="sxs-lookup"><span data-stu-id="e97d5-191">hello Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="e97d5-192">Основные функции Hello Jupyter также доступны в Visual Studio через [средства Python для Visual Studio] [ Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="e97d5-192">hello core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="e97d5-193">PTVS является бесплатным подключаемым модулем с открытым кодом от корпорации Майкрософт, который превращает Visual Studio в среду разработки Python с расширенными возможностями, включающую редактор с интеграцией IntelliSense, средств отладки, профилирования и параллельных вычислений.</span><span class="sxs-lookup"><span data-stu-id="e97d5-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e97d5-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e97d5-194">Next steps</span></span>
<span data-ttu-id="e97d5-195">Дополнительные сведения см. в разделе hello [центре разработчиков Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="e97d5-195">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
