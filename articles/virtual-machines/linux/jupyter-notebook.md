---
title: "Создание Jupyter/IPython Notebook | Документация Майкрософт"
description: "Узнайте, как развернуть Jupyter/IPython Notebook на виртуальной машине в Azure под управлением Linux или Windows, созданной с помощью модели развертывания с использованием менеджера ресурсов."
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
ms.openlocfilehash: b5940190822cd5c5b78ea0e8f5c8695608d351d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="c2567-103">Создание виртуальной машины Azure, установка Jupyter и запуск Jupyter Notebook в Azure</span><span class="sxs-lookup"><span data-stu-id="c2567-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="c2567-104">[Проект Jupyter](http://jupyter.org), ранее известный как [проект IPython](http://ipython.org), предоставляет собой набор средств для научных вычислений, который сочетает в себе выполнение кода с созданием документа вычислений в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="c2567-104">The [Jupyter project](http://jupyter.org), formerly the [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with the creation of a live computational document.</span></span> <span data-ttu-id="c2567-105">Эти файлы записной книжки могут содержать произвольный текст, математические формулы, код ввода, результаты, графику, видео и любые другие виды носителей, которые может отображать современный веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="c2567-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="c2567-106">Независимо от того, кем вы являетесь — новичком в Python, который хочет изучить этот язык в интересной интерактивной среде, или специалистом, которому требуется выполнить какие-то серьезные параллельные или технические вычисления, Jupyter Notebook станет великолепным выбором.</span><span class="sxs-lookup"><span data-stu-id="c2567-106">Whether you're absolutely new to Python and want to learn it in a fun, interactive environment or do some serious parallel/technical computing, the Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="c2567-107">![Снимок экрана](./media/jupyter-notebook/ipy-notebook-spectral.png) Применение пакетов SciPy и matplotlib для анализа структуры звукозаписи.</span><span class="sxs-lookup"><span data-stu-id="c2567-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages to analyze the structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="c2567-108">Два способа реализации Jupyter: Azure Notebook или пользовательское развертывание</span><span class="sxs-lookup"><span data-stu-id="c2567-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="c2567-109">В Azure есть служба, позволяющая [быстро начать работу с Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2567-109">Azure provides a service that you can use to [quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="c2567-110">С помощью службы Azure Notebook можно с легкостью получить доступ к веб-интерфейсу Jupyter для масштабируемых вычислительных ресурсов в сочетании со всеми возможностями Python и его многочисленных библиотек.</span><span class="sxs-lookup"><span data-stu-id="c2567-110">By using the Azure Notebook Service, you can easily gain access to Jupyter's web-accessible interface to scalable computational resources with all the power of Python and its many libraries.</span></span>  <span data-ttu-id="c2567-111">Поскольку установкой занимается служба, пользователи могут работать с этими ресурсами без всякого администрирования и настройки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c2567-111">Since the installation is handled by the service, users can access these resources without the need for administration and configuration by the user.</span></span>

<span data-ttu-id="c2567-112">Если служба Notebook не подходит для вашего сценария, далее в этой статье вы узнаете, как развернуть Jupyter Notebook в Microsoft Azure, используя виртуальные машины Linux.</span><span class="sxs-lookup"><span data-stu-id="c2567-112">If the notebook service does not work for your scenario please continue to read this article which will will show you how to deploy the Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="c2567-113">Создание и настройка виртуальной машины в Azure</span><span class="sxs-lookup"><span data-stu-id="c2567-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="c2567-114">Первым шагом является создание виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="c2567-114">The first step is to create a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="c2567-115">Эта виртуальная машина является полноценной операционной системой в облаке и будет использоваться для запуска Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="c2567-115">This VM is a complete operating system in the cloud and will be used to run the Jupyter Notebook.</span></span> <span data-ttu-id="c2567-116">В среде Azure можно размещать виртуальные машины Linux и Windows. Мы рассмотрим установку Jupyter на обоих типах виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c2567-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover the setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="c2567-117">Создание виртуальной Машины Linux и открытие порта для Jupyter</span><span class="sxs-lookup"><span data-stu-id="c2567-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="c2567-118">Следуя приведенным [здесь][portal-vm-linux] инструкциям, создайте виртуальную машину из дистрибутива *Ubuntu*.</span><span class="sxs-lookup"><span data-stu-id="c2567-118">Follow the instructions given [here][portal-vm-linux] to create a virtual machine of the *Ubuntu* distribution.</span></span> <span data-ttu-id="c2567-119">В этом учебнике используется Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="c2567-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="c2567-120">Предположим, что имя пользователя — *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="c2567-120">We'll assume the user name *azureuser*.</span></span>

<span data-ttu-id="c2567-121">После развертывания виртуальной машины необходимо открыть правило безопасности для группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="c2567-121">After the virtual machine deploys we need to open up a security rule on the network security group.</span></span>  <span data-ttu-id="c2567-122">На портале Azure откройте раздел **Сетевые группы безопасности** и перейдите на вкладку группы безопасности, соответствующей вашей виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c2567-122">From the Azure portal, go to **Network Security Groups** and open the tab for the Security Group corresponding to your VM.</span></span> <span data-ttu-id="c2567-123">Вам нужно добавить правило безопасности для входящего трафика со следующими параметрами: **TCP** в качестве протокола, **\*** в качестве исходного (открытого) порта и **9999** в качестве конечного (закрытого) порта.</span><span class="sxs-lookup"><span data-stu-id="c2567-123">You need to add an Inbound Security rule with the following settings: **TCP** for the protocol, **\*** for the source (public) port and **9999** for the destination (private) port.</span></span>

![Снимок экрана](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="c2567-125">В группе безопасности сети щелкните **Сетевые интерфейсы** и запишите **общедоступный IP-адрес** — он потребуется для подключения к виртуальной машине на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="c2567-125">While in your Network Security Group, click on **Network Interfaces** and note the **Public IP Address** as it will be needed to connect to your VM in the next step.</span></span>

## <a name="install-required-software-on-the-vm"></a><span data-ttu-id="c2567-126">Установка необходимого программного обеспечения в виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="c2567-126">Install required software on the VM</span></span>
<span data-ttu-id="c2567-127">Чтобы запустить Jupyter Notebook на своей виртуальной машине, необходимо предварительно установить Jupyter и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="c2567-127">To run the Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="c2567-128">Подключитесь к своей виртуальной машине Linux по протоколу SSH, указав имя пользователя и пароль, выбранные при ее создании.</span><span class="sxs-lookup"><span data-stu-id="c2567-128">Connect to your linux vm using ssh and the username/password pair you chose when you created the vm.</span></span> <span data-ttu-id="c2567-129">В этом учебнике используется PuTTY и подключение из Windows.</span><span class="sxs-lookup"><span data-stu-id="c2567-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="c2567-130">Установка Jupyter на Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c2567-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="c2567-131">Установите Anaconda, популярный дистрибутив Python для работы с научными данными, воспользовавшись одной из ссылок на сайте [Continuum Analytics](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="c2567-131">Install Anaconda, a popular data science python distribution, using one of the links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="c2567-132">На момент составления данного документа на последние версии вели указанные ниже ссылки.</span><span class="sxs-lookup"><span data-stu-id="c2567-132">As of the writing of this document, the below links are the most up to date versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="c2567-133">Дистрибутивы Anaconda для Linux</span><span class="sxs-lookup"><span data-stu-id="c2567-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="c2567-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="c2567-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="c2567-135">Python 2,7</span><span class="sxs-lookup"><span data-stu-id="c2567-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="c2567-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64-разрядная</href>
    </span><span class="sxs-lookup"><span data-stu-id="c2567-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="c2567-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64-разрядная</href>
    </span><span class="sxs-lookup"><span data-stu-id="c2567-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="c2567-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32-разрядная</href>
    </span><span class="sxs-lookup"><span data-stu-id="c2567-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="c2567-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32-разрядная</href>
    </span><span class="sxs-lookup"><span data-stu-id="c2567-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="c2567-140">Установка 64-разрядной версии Anaconda 3 2.3.0 на Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c2567-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="c2567-141">Приведем пример установки Anaconda на Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="c2567-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter to the latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Снимок экрана](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="c2567-143">Настройка Jupyter и использование протокола SSL</span><span class="sxs-lookup"><span data-stu-id="c2567-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="c2567-144">После установки необходимо настроить файлы конфигурации для Jupyter.</span><span class="sxs-lookup"><span data-stu-id="c2567-144">After installing we need to take a moment to setup the configuration files for Jupyter.</span></span> <span data-ttu-id="c2567-145">Если с настройкой Jupyter возникнут проблемы, обратитесь к [документации по Jupyter в части запуска сервера службы Notebook](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="c2567-145">If you experience troubles with configuring Jupyter it may be helpful to look at the [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="c2567-146">Далее мы выполним команду `cd` , чтобы перейти к папке профиля для создания своего SSL-сертификата и изменения файла конфигурации профилей.</span><span class="sxs-lookup"><span data-stu-id="c2567-146">Next we `cd` to the profile directory to create our SSL certificate and edit the profiles configuration file.</span></span>

<span data-ttu-id="c2567-147">В Linux используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c2567-147">On Linux use the following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="c2567-148">Используйте следующую команду, чтобы создать сертификат SSL (Linux и Windows).</span><span class="sxs-lookup"><span data-stu-id="c2567-148">Use the following command to create the SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="c2567-149">Обратите внимание — так как создается самозаверяющий SSL-сертификат, при подключении к записной книжке в браузере будет выведено предупреждение системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="c2567-149">Note that since we are creating a self-signed SSL certificate, when connecting to the notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="c2567-150">Для долгосрочного использования в рабочей среде потребуется должным образом подписанный сертификат, связанный с вашей организацией.</span><span class="sxs-lookup"><span data-stu-id="c2567-150">For long-term production use, you will want to use a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="c2567-151">Так как управление сертификатами выходит за рамки этой демонстрации, в данном случае мы ограничимся самозаверяющим сертификатом.</span><span class="sxs-lookup"><span data-stu-id="c2567-151">Since certificate management is beyond the scope of this demo, we will stick to a self-signed certificate for now.</span></span>

<span data-ttu-id="c2567-152">Помимо сертификата, необходимо также указать пароль для защиты записной книжки от несанкционированного использования.</span><span class="sxs-lookup"><span data-stu-id="c2567-152">In addition to using a certificate, you must also provide a password to protect your notebook from unauthorized use.</span></span>  <span data-ttu-id="c2567-153">Из соображений безопасности Jupyter использует зашифрованные пароли в своем файле конфигурации, поэтому сначала необходимо зашифровать пароль.</span><span class="sxs-lookup"><span data-stu-id="c2567-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need to encrypt your password first.</span></span>  <span data-ttu-id="c2567-154">IPython предоставляет для этого соответствующую утилиту; в командной строке выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2567-154">IPython provides a utility to do so; at a command prompt run the following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="c2567-155">Система запросит пароль и подтверждение, а затем выведет пароль на экран.</span><span class="sxs-lookup"><span data-stu-id="c2567-155">This will prompt you for a password and confirmation, and will then print the password.</span></span> <span data-ttu-id="c2567-156">Запишите его для следующего этапа.</span><span class="sxs-lookup"><span data-stu-id="c2567-156">Note this for the following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided the rest for security)

<span data-ttu-id="c2567-157">Далее предстоит отредактировать файл конфигурации профиля, т. е. файл `jupyter_notebook_config.py` в текущей папке профиля.</span><span class="sxs-lookup"><span data-stu-id="c2567-157">Next, we will edit the profile's configuration file, which is the `jupyter_notebook_config.py` file in the directory you are in.</span></span>  <span data-ttu-id="c2567-158">Если этот файл не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="c2567-158">Note that this file may not exist -- just create it if that is the case.</span></span>  <span data-ttu-id="c2567-159">Этот файл содержит несколько полей, которые по умолчанию закомментированы.</span><span class="sxs-lookup"><span data-stu-id="c2567-159">This file has a number of fields and by default all are commented out.</span></span>  <span data-ttu-id="c2567-160">Этот файл можно открыть в любом текстовом редакторе. Необходимо убедиться, что в нем есть по крайней мере следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="c2567-160">You can open this file with any text editor of your liking, and you should ensure that it has at least the following content.</span></span> <span data-ttu-id="c2567-161">**Не забудьте заменить c.NotebookApp.password в файле конфигурации паролем sha1 из предыдущего шага**.</span><span class="sxs-lookup"><span data-stu-id="c2567-161">**Be sure to replace the c.NotebookApp.password in the config with the sha1 from the previous step**.</span></span>

    c = get_config()

    # You must give the path to the certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-the-jupyter-notebook"></a><span data-ttu-id="c2567-162">Запустите Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="c2567-162">Run the Jupyter Notebook</span></span>
<span data-ttu-id="c2567-163">Теперь можно запустить Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="c2567-163">At this point we are ready to start the Jupyter Notebook.</span></span> <span data-ttu-id="c2567-164">Для этого перейдите в каталог, в котором предполагается хранить записные книжки, и запустите сервер Jupyter Notebook с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="c2567-164">To do this, navigate to the directory you want to store notebooks in and start the Jupyter Notebook server with the following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="c2567-165">Теперь можно получить доступ к Jupyter Notebook по адресу `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="c2567-165">You should now be able to access your Jupyter Notebook at the address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="c2567-166">При первом обращении к записной книжке, на странице входа будет запрошен пароль:</span><span class="sxs-lookup"><span data-stu-id="c2567-166">When you first access your notebook, the login page asks for your password.</span></span> <span data-ttu-id="c2567-167">После входа в систему вы увидите "Панель мониторинга Jupyter Notebook", которая является центром управления для всех операций с записными книжками.</span><span class="sxs-lookup"><span data-stu-id="c2567-167">And once you log in, you will see the "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="c2567-168">На этой странице можно создать новые записные книжки и открывать существующие:</span><span class="sxs-lookup"><span data-stu-id="c2567-168">From this page you can create new notebooks and open existing ones.</span></span>

![Снимок экрана](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-the-jupyter-notebook"></a><span data-ttu-id="c2567-170">Использование Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="c2567-170">Using the Jupyter Notebook</span></span>
<span data-ttu-id="c2567-171">Нажав кнопку **Создать** , вы увидите следующую начальную страницу.</span><span class="sxs-lookup"><span data-stu-id="c2567-171">If you click the **New** button, you will see the following opening page.</span></span>

![Снимок экрана](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="c2567-173">Область, отмеченная запросом `In []:`, является областью ввода: здесь можно ввести любой допустимый код Python и он будет исполнен, если нажать `Shift-Enter` или щелкнуть значок «Воспроизведение» (направленный вправо треугольник на панели инструментов).</span><span class="sxs-lookup"><span data-stu-id="c2567-173">The area marked with an `In []:` prompt is the input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on the "Play" icon (the right-pointing triangle in the toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="c2567-174">Мощная парадигма: документы с вычислениями в режиме реального времени и богатыми возможностями мультимедиа</span><span class="sxs-lookup"><span data-stu-id="c2567-174">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="c2567-175">Сама работа с записной книжкой должна быть интуитивно понятна для любого, кто использовал Python и текстовый процессор, так как это является в некотором смысле сочетанием обоих вариантов: здесь можно выполнять блоки кода Python, но можно также сохранять заметки и другой текст, изменив стиль в ячейки с «Код» на «Разметка» в раскрывающемся меню на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="c2567-175">The notebook itself should feel very natural to anyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing the style of a cell from "Code" to "Markdown" using the drop-down menu in the toolbar.</span></span>

<span data-ttu-id="c2567-176">Но это гораздо больше, чем текстовый процессор, так как Jupyter позволяет совмещать вычисления и широкие возможности мультимедиа (текст, графику, видео и практически любые данные, которые способен отображать современный браузер).</span><span class="sxs-lookup"><span data-stu-id="c2567-176">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="c2567-177">Вы можете комбинировать текст, код, видео и многое другое!</span><span class="sxs-lookup"><span data-stu-id="c2567-177">You can mix, text, code, videos and more!</span></span>

![Снимок экрана](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="c2567-179">И с помощью множества великолепных библиотек Python, предназначенных для научных и технических вычислений, как показано на следующем снимке экрана, можно с легкостью выполнять и простые вычисления, и анализ сложных сетей в единой среде.</span><span class="sxs-lookup"><span data-stu-id="c2567-179">And with the power of Python's many excellent libraries for scientific and technical computing, in the following screenshot, a simple calculation can be performed with the same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="c2567-180">Эта парадигма сочетания мощи современных веб-технологий с вычислениями в режиме реального времени предоставляет множество возможностей и идеально подходит для облака. Notebook можно использовать для следующих целей:</span><span class="sxs-lookup"><span data-stu-id="c2567-180">This paradigm of mixing the power of the modern web with live computation offers many possibilities, and is ideally suited for the cloud; the Notebook can be used:</span></span>

* <span data-ttu-id="c2567-181">Как вычислительный электронный блокнот для регистрации исследовательской работы над проблемой.</span><span class="sxs-lookup"><span data-stu-id="c2567-181">As a computational scratchpad to record exploratory work on a problem.</span></span>
* <span data-ttu-id="c2567-182">Для совместного использования результатов с коллегами либо в форме вычислений в режиме реального времени, либо в формате печатной копии (HTML, PDF).</span><span class="sxs-lookup"><span data-stu-id="c2567-182">To share results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="c2567-183">Для распространения и представления материалов интерактивного обучения,включающих вычисления, что позволит слушателям сразу же приступить к экспериментам с реальным кодом, изменять его и повторно выполнять в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="c2567-183">To distribute and present live teaching materials that involve computation, so students can immediately experiment with the real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="c2567-184">Для предоставления «исполняемых документов», в которых представлены результаты исследования таким образом,что оно может быть немедленно воспроизведено, проверено и дополнено другими.</span><span class="sxs-lookup"><span data-stu-id="c2567-184">To provide "executable papers" that present the results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="c2567-185">Как платформа для совместной работы: несколько пользователей могут войти на один сервер записной книжки для совместной работы в интерактивном сеансе вычислений.</span><span class="sxs-lookup"><span data-stu-id="c2567-185">As a platform for collaborative computing: multiple users can log in to the same notebook server to share a live computational session.</span></span>

<span data-ttu-id="c2567-186">В [репозитории][repository] исходного кода IPython доступен весь каталог с примерами Notebook, которые можно скачать и использовать в виртуальной машине Jupyter для Azure для экспериментов.</span><span class="sxs-lookup"><span data-stu-id="c2567-186">If you go to the IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="c2567-187">Просто загрузите файлы `.ipynb` с сайта и отправьте их на панель мониторинга виртуальной машины Azure для записной книжки (или загрузите их прямо в виртуальную машину).</span><span class="sxs-lookup"><span data-stu-id="c2567-187">Simply download the `.ipynb` files from the site and upload them onto the dashboard of your notebook Azure VM (or download them directly into the VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="c2567-188">Заключение</span><span class="sxs-lookup"><span data-stu-id="c2567-188">Conclusion</span></span>
<span data-ttu-id="c2567-189">Jupyter Notebook предоставляет богатый возможностями интерфейс для интерактивной работы с мощной экосистемой Python в Azure.</span><span class="sxs-lookup"><span data-stu-id="c2567-189">The Jupyter Notebook provides a powerful interface for accessing interactively the power of the Python ecosystem on Azure.</span></span>  <span data-ttu-id="c2567-190">Он охватывает широкий диапазон вариантов использования, включая простой просмотр и изучения Python, анализ данных и визуализацию, моделирование и параллельные вычисления.</span><span class="sxs-lookup"><span data-stu-id="c2567-190">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="c2567-191">Итоговые документы Notebook содержат полную запись выполненных вычислений и могут использоваться совместно с другими пользователями Jupyter.</span><span class="sxs-lookup"><span data-stu-id="c2567-191">The resulting Notebook documents contain a complete record of the computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="c2567-192">Приложение Jupyter Notebook можно использовать в качестве локального приложения, однако оно идеально подходит для развертываний в облаке Azure.</span><span class="sxs-lookup"><span data-stu-id="c2567-192">The Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="c2567-193">Основные функции Jupyter также доступны в Visual Studio в [средствах Python для Visual Studio][Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="c2567-193">The core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="c2567-194">PTVS является бесплатным подключаемым модулем с открытым кодом от корпорации Майкрософт, который превращает Visual Studio в среду разработки Python с расширенными возможностями, включающую редактор с интеграцией IntelliSense, средств отладки, профилирования и параллельных вычислений.</span><span class="sxs-lookup"><span data-stu-id="c2567-194">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2567-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c2567-195">Next steps</span></span>
<span data-ttu-id="c2567-196">Дополнительную информацию можно найти в [Центре разработчика Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="c2567-196">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
