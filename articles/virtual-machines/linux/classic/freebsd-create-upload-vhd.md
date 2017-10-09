---
title: "изображений aaaCreate и отправки ВМ FreeBSD | Документы Microsoft"
description: "Узнайте, toocreate и отправка виртуального жесткого диска (VHD), содержащий toocreate операционной системе FreeBSD hello виртуальной машине Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a><span data-ttu-id="722c9-103">Создание и отправка tooAzure FreeBSD виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="722c9-103">Create and upload a FreeBSD VHD tooAzure</span></span>
<span data-ttu-id="722c9-104">В этой статье показано, как toocreate и передача виртуального жесткого диска (VHD), содержащий hello FreeBSD операционной системы.</span><span class="sxs-lookup"><span data-stu-id="722c9-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello FreeBSD operating system.</span></span> <span data-ttu-id="722c9-105">После загрузки, его можно использовать как toocreate собственный образ виртуальной машины (VM) в Azure.</span><span class="sxs-lookup"><span data-stu-id="722c9-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="722c9-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="722c9-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="722c9-107">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="722c9-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="722c9-108">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="722c9-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="722c9-109">Сведения о загрузке VHD с помощью модели hello диспетчера ресурсов см. в разделе [здесь](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="722c9-109">For information about uploading a VHD using hello Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="722c9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="722c9-110">Prerequisites</span></span>
<span data-ttu-id="722c9-111">В этой статье предполагается, что hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="722c9-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="722c9-112">**Подписка Azure**. Если у вас нет учетной записи, то ее можно создать, что займет всего лишь несколько минут.</span><span class="sxs-lookup"><span data-stu-id="722c9-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="722c9-113">Если у вас есть подписка MSDN, см. страницу [Ежемесячная сумма денег на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="722c9-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="722c9-114">В противном случае — Узнайте, каким образом слишком[создать бесплатную пробную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="722c9-114">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="722c9-115">**Средства Azure PowerShell**--hello Azure PowerShell модуль должен быть установлен и настроен toouse подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="722c9-115">**Azure PowerShell tools**--hello Azure PowerShell module must be installed and configured toouse your Azure subscription.</span></span> <span data-ttu-id="722c9-116">модуль toodownload hello, в разделе [загрузки Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="722c9-116">toodownload hello module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="722c9-117">Учебник, в котором описывается как tooinstall и настроить модуль hello доступен здесь.</span><span class="sxs-lookup"><span data-stu-id="722c9-117">A tutorial that describes how tooinstall and configure hello module is available here.</span></span> <span data-ttu-id="722c9-118">Используйте hello [загрузки Azure](https://azure.microsoft.com/downloads/) hello tooupload командлет виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="722c9-118">Use hello [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.</span></span>
* <span data-ttu-id="722c9-119">**FreeBSD операционной системы, установленной в VHD-файл**--поддерживаемой операционной системе FreeBSD должен быть установлен tooa виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="722c9-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="722c9-120">Существуют несколько средства toocreate VHD-файлы.</span><span class="sxs-lookup"><span data-stu-id="722c9-120">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="722c9-121">Например можно использовать решение виртуализации, таких как Hyper-V toocreate hello VHD-файл и установить hello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="722c9-121">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="722c9-122">Инструкции о том, как tooinstall и использование Hyper-V, на экране [Установка Hyper-V и создание виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="722c9-122">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="722c9-123">Hello более новый формат VHDX не поддерживается в Azure.</span><span class="sxs-lookup"><span data-stu-id="722c9-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="722c9-124">Вы можете преобразования формата tooVHD hello диска с помощью диспетчера Hyper-V или командлета hello [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="722c9-124">You can convert hello disk tooVHD format by using Hyper-V Manager or hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="722c9-125">Кроме того, [учебник на MSDN о том, как toouse FreeBSD в Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="722c9-125">In addition, there is a [tutorial on MSDN about how toouse FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="722c9-126">Эта задача включает hello следующие пять шагов:</span><span class="sxs-lookup"><span data-stu-id="722c9-126">This task includes hello following five steps:</span></span>

## <a name="step-1-prepare-hello-image-for-upload"></a><span data-ttu-id="722c9-127">Шаг 1: Подготовка образа hello для передачи</span><span class="sxs-lookup"><span data-stu-id="722c9-127">Step 1: Prepare hello image for upload</span></span>
<span data-ttu-id="722c9-128">На виртуальной машине hello установленным hello FreeBSD операционной системы выполните hello следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="722c9-128">On hello virtual machine where you installed hello FreeBSD operating system, complete hello following procedures:</span></span>

1. <span data-ttu-id="722c9-129">Включите DHCP.</span><span class="sxs-lookup"><span data-stu-id="722c9-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="722c9-130">Включите SSH.</span><span class="sxs-lookup"><span data-stu-id="722c9-130">Enable SSH.</span></span>

    <span data-ttu-id="722c9-131">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="722c9-131">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="722c9-132">Он включается по умолчанию после установки с диска FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="722c9-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="722c9-133">Настройте последовательную консоль.</span><span class="sxs-lookup"><span data-stu-id="722c9-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="722c9-134">Установите sudo.</span><span class="sxs-lookup"><span data-stu-id="722c9-134">Install sudo.</span></span>

    <span data-ttu-id="722c9-135">Учетная запись root Hello отключен в Azure.</span><span class="sxs-lookup"><span data-stu-id="722c9-135">hello root account is disabled in Azure.</span></span> <span data-ttu-id="722c9-136">Это означает, что необходимо tooutilize sudo с помощью команд toorun непривилегированного пользователя с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="722c9-136">This means you need tooutilize sudo from an unprivileged user toorun commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="722c9-137">Необходимые условия для агента Azure.</span><span class="sxs-lookup"><span data-stu-id="722c9-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="722c9-138">Установите агент Azure.</span><span class="sxs-lookup"><span data-stu-id="722c9-138">Install Azure Agent.</span></span>

    <span data-ttu-id="722c9-139">Hello последний выпуск hello агент Azure всегда находятся на [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="722c9-139">hello latest release of hello Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="722c9-140">Здравствуйте, версия 2.0.10 + официально поддерживающей FreeBSD 10 & 10.1 и версии hello 2.1.4 Установка + (включая 2.2.x) официально поддерживающей FreeBSD 10.2 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="722c9-140">hello version 2.0.10 + officially supports FreeBSD 10 & 10.1, and hello version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="722c9-141">В качестве примера версии 2.0 будем использовать версию 2.0.16.</span><span class="sxs-lookup"><span data-stu-id="722c9-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="722c9-142">В качестве примера версии 2.1 будем использовать версию 2.1.4.</span><span class="sxs-lookup"><span data-stu-id="722c9-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="722c9-143">После установки агента Azure очень хорошее представление tooverify, на котором он выполняется:</span><span class="sxs-lookup"><span data-stu-id="722c9-143">After you install Azure Agent, it's a good idea tooverify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="722c9-144">Сделать hello системы.</span><span class="sxs-lookup"><span data-stu-id="722c9-144">Deprovision hello system.</span></span>

    <span data-ttu-id="722c9-145">Отзыв hello системы tooclean его и внести он подходит для инициализацию.</span><span class="sxs-lookup"><span data-stu-id="722c9-145">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="722c9-146">Hello следующая команда также удаляет hello последнего подготовленных учетную запись и hello связанных данных:</span><span class="sxs-lookup"><span data-stu-id="722c9-146">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="722c9-147">Теперь вы можете завершить работу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="722c9-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="722c9-148">Шаг 2. Создание учетной записи хранения в Azure</span><span class="sxs-lookup"><span data-stu-id="722c9-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="722c9-149">Необходимо учетной записи хранилища в Azure tooupload VHD-файл, чтобы его можно использовать toocreate виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="722c9-149">You need a storage account in Azure tooupload a .vhd file so it can be used toocreate a virtual machine.</span></span> <span data-ttu-id="722c9-150">Можно использовать hello Azure классического портала toocreate учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="722c9-150">You can use hello Azure classic portal toocreate a storage account.</span></span>

1. <span data-ttu-id="722c9-151">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="722c9-151">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="722c9-152">Выберите на панели команд hello, **New**.</span><span class="sxs-lookup"><span data-stu-id="722c9-152">On hello command bar, select **New**.</span></span>
3. <span data-ttu-id="722c9-153">Последовательно выберите **Службы данных** > **Хранилище** > **Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="722c9-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Быстрое создание учетной записи хранения](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="722c9-155">Заполните поля hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="722c9-155">Fill out hello fields as follows:</span></span>

   * <span data-ttu-id="722c9-156">В hello **URL-адрес** введите имя дочернего домена toouse в URL-адрес учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="722c9-156">In hello **URL** field, type a subdomain name toouse in hello storage account URL.</span></span> <span data-ttu-id="722c9-157">запись Hello могут содержать от 3 до 24 цифры и буквы в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="722c9-157">hello entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="722c9-158">Это имя становится именем узла hello в hello URL-адреса, используемые tooaddress хранилища больших двоичных объектов Azure, хранилища очередей Azure или ресурсами хранилища таблиц Azure для подписки hello.</span><span class="sxs-lookup"><span data-stu-id="722c9-158">This name becomes hello host name within hello URL that is used tooaddress Azure Blob storage, Azure Queue storage, or Azure Table storage resources for hello subscription.</span></span>
   * <span data-ttu-id="722c9-159">В hello **расположение или территориальная группа** раскрывающееся меню, выберите hello **расположение или территориальная группа** для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="722c9-159">In hello **Location/Affinity Group** drop-down menu, choose hello **location or affinity group** for hello storage account.</span></span> <span data-ttu-id="722c9-160">Территориальная группа позволяет поместить облачных служб и хранилища в hello одного центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="722c9-160">An affinity group lets you put your cloud services and storage in hello same data center.</span></span>
   * <span data-ttu-id="722c9-161">В hello **репликации** определите ли toouse **Геоизбыточное** репликации для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="722c9-161">In hello **Replication** field, decide whether toouse **Geo-Redundant** replication for hello storage account.</span></span> <span data-ttu-id="722c9-162">По умолчанию георепликация включена.</span><span class="sxs-lookup"><span data-stu-id="722c9-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="722c9-163">Этот параметр реплицируется на данных tooa вторичного расположения, в tooyou без затрат, чтобы хранилища при сбое toothat расположении при крупном сбое происходит hello основного расположения.</span><span class="sxs-lookup"><span data-stu-id="722c9-163">This option replicates your data tooa secondary location, at no cost tooyou, so that your storage fails over toothat location if a major failure occurs at hello primary location.</span></span> <span data-ttu-id="722c9-164">вторичное расположение Hello присваивается автоматически и не может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="722c9-164">hello secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="722c9-165">Если требуется больший контроль над расположение hello облачного хранилища из-за требований toolegal или политика организации географическую репликацию можно отключить.</span><span class="sxs-lookup"><span data-stu-id="722c9-165">If you need more control over hello location of your cloud-based storage due toolegal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="722c9-166">Однако имейте в виду, что если позже включить географическую репликацию данных будет взиматься однократного входящий трафик передачи данных tooreplicate плата имеющееся местоположение вторичного toohello данных.</span><span class="sxs-lookup"><span data-stu-id="722c9-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee tooreplicate your existing data toohello secondary location.</span></span> <span data-ttu-id="722c9-167">Службы хранения без георепликации предлагаются со скидкой.</span><span class="sxs-lookup"><span data-stu-id="722c9-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="722c9-168">Дополнительные сведения об управлении георепликацией учетных записей хранения см. в статье [Репликация службы хранилища Azure](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="722c9-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Введите сведения об учетной записи хранения](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="722c9-170">Щелкните **Создать учетную запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="722c9-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="722c9-171">Hello учетной записи теперь отображается в списке **хранения**.</span><span class="sxs-lookup"><span data-stu-id="722c9-171">hello account now appears under **storage**.</span></span>

    ![Учетная запись хранения успешно создана](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="722c9-173">Теперь создайте контейнер для переданных VHD-файлов.</span><span class="sxs-lookup"><span data-stu-id="722c9-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="722c9-174">Выберите имя учетной записи хранения hello, а затем выберите **контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="722c9-174">Select hello storage account name, and then select **Containers**.</span></span>

    ![Информация об учетной записи хранения](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="722c9-176">Щелкните **Создать контейнер**.</span><span class="sxs-lookup"><span data-stu-id="722c9-176">Select **Create a Container**.</span></span>

    ![Информация об учетной записи хранения](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="722c9-178">В hello **имя** введите имя для контейнера.</span><span class="sxs-lookup"><span data-stu-id="722c9-178">In hello **Name** field, type a name for your container.</span></span> <span data-ttu-id="722c9-179">Затем в hello **доступа** раскрывающееся меню, выберите тип политики доступа, требуется.</span><span class="sxs-lookup"><span data-stu-id="722c9-179">Then, in hello **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Имя контейнера](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="722c9-181">По умолчанию hello контейнер является закрытым и может осуществляться только владельцем учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="722c9-181">By default, hello container is private and can only be accessed by hello account owner.</span></span> <span data-ttu-id="722c9-182">tooallow общего доступа на чтение toohello BLOB-объектов в контейнере hello, но toohello свойства контейнера и метаданные, использовать hello **большой двоичный объект открытого** параметр.</span><span class="sxs-lookup"><span data-stu-id="722c9-182">tooallow public read access toohello blobs in hello container, but not toohello container properties and metadata, use hello **Public Blob** option.</span></span> <span data-ttu-id="722c9-183">tooallow полный открытый доступ чтения для hello контейнера и больших двоичных объектов, используйте hello **открытый контейнер** параметр.</span><span class="sxs-lookup"><span data-stu-id="722c9-183">tooallow full public read access for hello container and blobs, use hello **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a><span data-ttu-id="722c9-184">Шаг 3: Подготовка tooAzure подключения hello</span><span class="sxs-lookup"><span data-stu-id="722c9-184">Step 3: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="722c9-185">Перед отправкой VHD-файл, необходимо tooestablish безопасное подключение между компьютером и вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="722c9-185">Before you can upload a .vhd file, you need tooestablish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="722c9-186">Можно использовать метод hello Azure Active Directory (Azure AD) или hello toodo метод сертификата его.</span><span class="sxs-lookup"><span data-stu-id="722c9-186">You can use hello Azure Active Directory (Azure AD) method or hello certificate method toodo it.</span></span>

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a><span data-ttu-id="722c9-187">Используйте метод hello Azure AD tooupload VHD-файл</span><span class="sxs-lookup"><span data-stu-id="722c9-187">Use hello Azure AD method tooupload a .vhd file</span></span>
1. <span data-ttu-id="722c9-188">Откройте hello консоли Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="722c9-188">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="722c9-189">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="722c9-189">Type hello following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="722c9-190">После выполнения команды откроется окно входа и вы сможете войти, используя свою рабочую или учебную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="722c9-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![Окно PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="722c9-192">Azure выполняет проверку подлинности и сохраняет hello учетные данные.</span><span class="sxs-lookup"><span data-stu-id="722c9-192">Azure authenticates and saves hello credential information.</span></span> <span data-ttu-id="722c9-193">Затем он закрывает окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="722c9-193">Then it closes hello window.</span></span>

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a><span data-ttu-id="722c9-194">Используйте tooupload метод сертификат hello VHD-файл</span><span class="sxs-lookup"><span data-stu-id="722c9-194">Use hello certificate method tooupload a .vhd file</span></span>
1. <span data-ttu-id="722c9-195">Откройте hello консоли Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="722c9-195">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="722c9-196">Введите `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="722c9-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="722c9-197">Окно браузера откроется и предлагает вам toodownload hello файл PUBLISHSETTINGS.</span><span class="sxs-lookup"><span data-stu-id="722c9-197">A browser window opens and prompts you toodownload hello .publishsettings file.</span></span> <span data-ttu-id="722c9-198">Этот файл содержит сведения и сертификат для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="722c9-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Страница скачивания браузера](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="722c9-200">Сохраните файл PUBLISHSETTINGS hello.</span><span class="sxs-lookup"><span data-stu-id="722c9-200">Save hello .publishsettings file.</span></span>
5. <span data-ttu-id="722c9-201">Тип: `Import-AzurePublishSettingsFile <PathToFile>`, где `<PathToFile>` — файл PUBLISHSETTINGS toohello hello полный путь.</span><span class="sxs-lookup"><span data-stu-id="722c9-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is hello full path toohello .publishsettings file.</span></span>

   <span data-ttu-id="722c9-202">Дополнительные сведения см. в статье [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx) (Начало работы с командлетами Azure).</span><span class="sxs-lookup"><span data-stu-id="722c9-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="722c9-203">Дополнительные сведения об установке и настройке PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="722c9-203">For more information about installing and configuring PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-hello-vhd-file"></a><span data-ttu-id="722c9-204">Шаг 4: Отправка hello VHD-файл</span><span class="sxs-lookup"><span data-stu-id="722c9-204">Step 4: Upload hello .vhd file</span></span>
<span data-ttu-id="722c9-205">При передаче hello VHD-файл, его можно поместить в любом месте в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="722c9-205">When you upload hello .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="722c9-206">Ниже приведены некоторые термины, которые будут использоваться при отправке файла hello.</span><span class="sxs-lookup"><span data-stu-id="722c9-206">Following are some terms you will use when you upload hello file:</span></span>

* <span data-ttu-id="722c9-207">**BlobStorageURL** hello URL-адрес для учетной записи хранения hello, созданный на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="722c9-207">**BlobStorageURL** is hello URL for hello storage account that you created in Step 2.</span></span>
* <span data-ttu-id="722c9-208">**YourImagesFolder** — контейнер hello в хранилище больших двоичных объектов, место toostore изображений.</span><span class="sxs-lookup"><span data-stu-id="722c9-208">**YourImagesFolder** is hello container within Blob storage where you want toostore your images.</span></span>
* <span data-ttu-id="722c9-209">**VHDName** — hello метка, которая отображается в hello Azure классического портала tooidentify hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="722c9-209">**VHDName** is hello label that appears in hello Azure classic portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="722c9-210">**PathToVHDFile** hello полный путь и имя hello VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="722c9-210">**PathToVHDFile** is hello full path and name of hello .vhd file.</span></span>

<span data-ttu-id="722c9-211">Из окна Azure PowerShell hello, использованные в предыдущем шаге hello введите:</span><span class="sxs-lookup"><span data-stu-id="722c9-211">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a><span data-ttu-id="722c9-212">Шаг 5: Создайте виртуальную Машину с hello загруженный VHD-файл</span><span class="sxs-lookup"><span data-stu-id="722c9-212">Step 5: Create a VM with hello uploaded .vhd file</span></span>
<span data-ttu-id="722c9-213">После загрузки hello VHD-файл можно добавить его как изображение toohello список пользовательских образов, связанных с подпиской и создать виртуальную машину с этого пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="722c9-213">After you upload hello .vhd file, you can add it as an image toohello list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="722c9-214">Из окна Azure PowerShell hello, использованные в предыдущем шаге hello введите:</span><span class="sxs-lookup"><span data-stu-id="722c9-214">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > <span data-ttu-id="722c9-215">Используйте в качестве типа hello операционной системы Linux.</span><span class="sxs-lookup"><span data-stu-id="722c9-215">Use Linux as hello OS type.</span></span> <span data-ttu-id="722c9-216">Текущая версия Azure PowerShell Hello принимает в качестве параметра только «Linux» или «Windows».</span><span class="sxs-lookup"><span data-stu-id="722c9-216">hello current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="722c9-217">После выполнения предыдущих шагов hello hello новое изображение отображается при выборе hello **изображения** вкладку на hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="722c9-217">After you complete hello previous steps, hello new image is listed when you choose hello **Images** tab on hello Azure classic portal.</span></span>  

    ![Выбор образа](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="722c9-219">Создание виртуальной машины из коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="722c9-219">Create a virtual machine from hello gallery.</span></span> <span data-ttu-id="722c9-220">Этот новый образ теперь доступен в разделе **Мои образы**.</span><span class="sxs-lookup"><span data-stu-id="722c9-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="722c9-221">Выбор нового образа hello.</span><span class="sxs-lookup"><span data-stu-id="722c9-221">Select hello new image.</span></span> <span data-ttu-id="722c9-222">Далее выполните tooset приглашения hello имя узла, пароль, ключа SSH и т. д.</span><span class="sxs-lookup"><span data-stu-id="722c9-222">Next, go through hello prompts tooset up a host name, password, SSH key, and so on.</span></span>

    ![Пользовательский образ](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="722c9-224">После завершения подготовки hello, вы увидите FreeBSD ВМ в Azure.</span><span class="sxs-lookup"><span data-stu-id="722c9-224">After you complete hello provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Образ FreeBSD в Azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
