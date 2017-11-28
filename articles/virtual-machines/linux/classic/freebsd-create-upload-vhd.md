---
title: "Создание и передача образа виртуальной машины FreeBSD | Документация Майкрософт"
description: "Узнайте, как создать и передать виртуальный жесткий диск (VHD-файл), содержащий операционную систему FreeBSD, для создания виртуальной машины Azure."
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
ms.openlocfilehash: 918f454784a9676297077c2e94c3e49ab2872d2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-freebsd-vhd-to-azure"></a><span data-ttu-id="060bd-103">Создание и отправка виртуального жесткого диска FreeBSD в Azure</span><span class="sxs-lookup"><span data-stu-id="060bd-103">Create and upload a FreeBSD VHD to Azure</span></span>
<span data-ttu-id="060bd-104">В этой статье описывается, как создать и передать виртуальный жесткий диск, содержащий операционную систему FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="060bd-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the FreeBSD operating system.</span></span> <span data-ttu-id="060bd-105">После передачи его можно использовать как свой собственный образ для создания виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="060bd-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="060bd-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="060bd-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="060bd-107">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="060bd-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="060bd-108">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="060bd-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="060bd-109">Дополнительные сведения о передаче виртуального жесткого диска с помощью модели Resource Manager см. [здесь](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="060bd-109">For information about uploading a VHD using the Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="060bd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="060bd-110">Prerequisites</span></span>
<span data-ttu-id="060bd-111">В данной статье предполагается, что у вас есть следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="060bd-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="060bd-112">**Подписка Azure**. Если у вас нет учетной записи, то ее можно создать, что займет всего лишь несколько минут.</span><span class="sxs-lookup"><span data-stu-id="060bd-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="060bd-113">Если у вас есть подписка MSDN, см. страницу [Ежемесячная сумма денег на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="060bd-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="060bd-114">В противном случае узнайте, как [создать бесплатную пробную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="060bd-114">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="060bd-115">**Инструменты Azure PowerShell**. Модуль Azure PowerShell необходимо установить и настроить на использование вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="060bd-115">**Azure PowerShell tools**--The Azure PowerShell module must be installed and configured to use your Azure subscription.</span></span> <span data-ttu-id="060bd-116">Сведения о скачивании модуля см. в разделе [загрузок Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="060bd-116">To download the module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="060bd-117">Руководство по установке и настройке этого модуля см. здесь.</span><span class="sxs-lookup"><span data-stu-id="060bd-117">A tutorial that describes how to install and configure the module is available here.</span></span> <span data-ttu-id="060bd-118">Для передачи VHD-файла используйте командлет из раздела [загрузок Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="060bd-118">Use the [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet to upload the VHD.</span></span>
* <span data-ttu-id="060bd-119">**Операционная система FreeBSD, установленная в VHD-файл**. На виртуальный жесткий диск необходимо установить поддерживаемую операционную систему FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="060bd-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed to a virtual hard disk.</span></span> <span data-ttu-id="060bd-120">Существует несколько средств для создания VHD-файлов.</span><span class="sxs-lookup"><span data-stu-id="060bd-120">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="060bd-121">Например, для создания VHD-файла и установки операционной системы можно использовать решение для виртуализации, например Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="060bd-121">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="060bd-122">Инструкции по установке и использованию Hyper-V см. в статье [Установка Hyper-V и создание виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="060bd-122">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="060bd-123">Более новый формат VHDX не поддерживается в Azure.</span><span class="sxs-lookup"><span data-stu-id="060bd-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="060bd-124">Вы можете преобразовать диск в формат VHD с помощью диспетчера Hyper-V или командлета [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="060bd-124">You can convert the disk to VHD format by using Hyper-V Manager or the cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="060bd-125">Кроме того, [на сайте MSDN доступно руководство по использованию FreeBSD с Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="060bd-125">In addition, there is a [tutorial on MSDN about how to use FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="060bd-126">Эта задача включает в себя следующие пять шагов:</span><span class="sxs-lookup"><span data-stu-id="060bd-126">This task includes the following five steps:</span></span>

## <a name="step-1-prepare-the-image-for-upload"></a><span data-ttu-id="060bd-127">Шаг 1. Подготовка образа для передачи</span><span class="sxs-lookup"><span data-stu-id="060bd-127">Step 1: Prepare the image for upload</span></span>
<span data-ttu-id="060bd-128">Из виртуальной машины, где была установлена операционная система FreeBSD, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="060bd-128">On the virtual machine where you installed the FreeBSD operating system, complete the following procedures:</span></span>

1. <span data-ttu-id="060bd-129">Включите DHCP.</span><span class="sxs-lookup"><span data-stu-id="060bd-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="060bd-130">Включите SSH.</span><span class="sxs-lookup"><span data-stu-id="060bd-130">Enable SSH.</span></span>

    <span data-ttu-id="060bd-131">Убедитесь, что SSH-сервер установлен и настроен для включения во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="060bd-131">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="060bd-132">Он включается по умолчанию после установки с диска FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="060bd-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="060bd-133">Настройте последовательную консоль.</span><span class="sxs-lookup"><span data-stu-id="060bd-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="060bd-134">Установите sudo.</span><span class="sxs-lookup"><span data-stu-id="060bd-134">Install sudo.</span></span>

    <span data-ttu-id="060bd-135">Учетная запись root в Azure отключена.</span><span class="sxs-lookup"><span data-stu-id="060bd-135">The root account is disabled in Azure.</span></span> <span data-ttu-id="060bd-136">Поэтому вам необходимо использовать sudo от лица непривилегированного пользователя для запуска команд с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="060bd-136">This means you need to utilize sudo from an unprivileged user to run commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="060bd-137">Необходимые условия для агента Azure.</span><span class="sxs-lookup"><span data-stu-id="060bd-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="060bd-138">Установите агент Azure.</span><span class="sxs-lookup"><span data-stu-id="060bd-138">Install Azure Agent.</span></span>

    <span data-ttu-id="060bd-139">Последний выпуск агента Azure всегда можно найти на сайте [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="060bd-139">The latest release of the Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="060bd-140">Версия 2.0.10 и более поздние версии официально поддерживают FreeBSD 10 и 10.1, а версия 2.1.4 и более поздние (включая 2.2.x) официально поддерживает FreeBSD 10.2 и более поздние версии.</span><span class="sxs-lookup"><span data-stu-id="060bd-140">The version 2.0.10 + officially supports FreeBSD 10 & 10.1, and the version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="060bd-141">В качестве примера версии 2.0 будем использовать версию 2.0.16.</span><span class="sxs-lookup"><span data-stu-id="060bd-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="060bd-142">В качестве примера версии 2.1 будем использовать версию 2.1.4.</span><span class="sxs-lookup"><span data-stu-id="060bd-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="060bd-143">После установки агента Azure рекомендуется проверить его работу.</span><span class="sxs-lookup"><span data-stu-id="060bd-143">After you install Azure Agent, it's a good idea to verify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="060bd-144">Отзовите систему.</span><span class="sxs-lookup"><span data-stu-id="060bd-144">Deprovision the system.</span></span>

    <span data-ttu-id="060bd-145">Отзовите систему, чтобы очистить ее и сделать пригодной для повторной подготовки.</span><span class="sxs-lookup"><span data-stu-id="060bd-145">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="060bd-146">Приведенная ниже команда также удаляет последнюю подготовленную учетную запись пользователя и связанные с ней данные.</span><span class="sxs-lookup"><span data-stu-id="060bd-146">The following command also deletes the last provisioned user account and the associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="060bd-147">Теперь вы можете завершить работу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="060bd-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="060bd-148">Шаг 2. Создание учетной записи хранения в Azure</span><span class="sxs-lookup"><span data-stu-id="060bd-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="060bd-149">Чтобы передать VHD-файл, который можно использовать в Azure для создания виртуальной машины, потребуется учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="060bd-149">You need a storage account in Azure to upload a .vhd file so it can be used to create a virtual machine.</span></span> <span data-ttu-id="060bd-150">Для создания учетной записи хранения можно использовать классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="060bd-150">You can use the Azure classic portal to create a storage account.</span></span>

1. <span data-ttu-id="060bd-151">Войдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="060bd-151">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="060bd-152">На панели команд нажмите **New**(Создать).</span><span class="sxs-lookup"><span data-stu-id="060bd-152">On the command bar, select **New**.</span></span>
3. <span data-ttu-id="060bd-153">Последовательно выберите **Службы данных** > **Хранилище** > **Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="060bd-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Быстрое создание учетной записи хранения](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="060bd-155">Заполните поля, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="060bd-155">Fill out the fields as follows:</span></span>

   * <span data-ttu-id="060bd-156">В поле **URL-адрес** введите имя поддомена, которое нужно использовать в URL-адресе для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="060bd-156">In the **URL** field, type a subdomain name to use in the storage account URL.</span></span> <span data-ttu-id="060bd-157">Записи могут содержать от 3 до 24 строчных букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="060bd-157">The entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="060bd-158">Это имя становится именем узла в URL-адресе, используемом для адресации ресурсов хранилища BLOB-объектов, хранилища очередей или хранилища таблиц Azure для подписки.</span><span class="sxs-lookup"><span data-stu-id="060bd-158">This name becomes the host name within the URL that is used to address Azure Blob storage, Azure Queue storage, or Azure Table storage resources for the subscription.</span></span>
   * <span data-ttu-id="060bd-159">В раскрывающемся меню **Расположение или территориальная группа** выберите **расположение или территориальную группу** для этой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="060bd-159">In the **Location/Affinity Group** drop-down menu, choose the **location or affinity group** for the storage account.</span></span> <span data-ttu-id="060bd-160">Указав территориальную группу, можно разместить облачные службы и хранилища в одном центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="060bd-160">An affinity group lets you put your cloud services and storage in the same data center.</span></span>
   * <span data-ttu-id="060bd-161">В поле **Репликация** укажите, следует ли использовать **геоизбыточную** репликацию для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="060bd-161">In the **Replication** field, decide whether to use **Geo-Redundant** replication for the storage account.</span></span> <span data-ttu-id="060bd-162">По умолчанию георепликация включена.</span><span class="sxs-lookup"><span data-stu-id="060bd-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="060bd-163">Этот параметр позволяет бесплатно выполнять репликацию данных в дополнительное расположение. Таким образом хранилище переключится на это расположение в случае аварийного отказа основного расположения.</span><span class="sxs-lookup"><span data-stu-id="060bd-163">This option replicates your data to a secondary location, at no cost to you, so that your storage fails over to that location if a major failure occurs at the primary location.</span></span> <span data-ttu-id="060bd-164">Дополнительное местоположение назначается автоматически и не может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="060bd-164">The secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="060bd-165">Если в соответствии с законодательными требованиями или организационной политикой требуется более жесткий контроль расположения облачного хранилища, георепликацию можно отключить.</span><span class="sxs-lookup"><span data-stu-id="060bd-165">If you need more control over the location of your cloud-based storage due to legal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="060bd-166">Однако следует помнить, что если вы опять включите георепликацию, с вас будет взята однократная плата за репликацию существующих данных в дополнительное местоположение.</span><span class="sxs-lookup"><span data-stu-id="060bd-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee to replicate your existing data to the secondary location.</span></span> <span data-ttu-id="060bd-167">Службы хранения без георепликации предлагаются со скидкой.</span><span class="sxs-lookup"><span data-stu-id="060bd-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="060bd-168">Дополнительные сведения об управлении георепликацией учетных записей хранения см. в статье [Репликация службы хранилища Azure](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="060bd-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Введите сведения об учетной записи хранения](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="060bd-170">Щелкните **Создать учетную запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="060bd-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="060bd-171">Учетная запись появится в списке раздела **Хранилище**.</span><span class="sxs-lookup"><span data-stu-id="060bd-171">The account now appears under **storage**.</span></span>

    ![Учетная запись хранения успешно создана](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="060bd-173">Теперь создайте контейнер для переданных VHD-файлов.</span><span class="sxs-lookup"><span data-stu-id="060bd-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="060bd-174">Введите имя учетной записи хранения и выберите **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="060bd-174">Select the storage account name, and then select **Containers**.</span></span>

    ![Информация об учетной записи хранения](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="060bd-176">Щелкните **Создать контейнер**.</span><span class="sxs-lookup"><span data-stu-id="060bd-176">Select **Create a Container**.</span></span>

    ![Информация об учетной записи хранения](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="060bd-178">В поле **Имя** введите имя своего контейнера.</span><span class="sxs-lookup"><span data-stu-id="060bd-178">In the **Name** field, type a name for your container.</span></span> <span data-ttu-id="060bd-179">Затем в раскрывающемся меню **Доступ** выберите требуемый тип политики доступа.</span><span class="sxs-lookup"><span data-stu-id="060bd-179">Then, in the **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Имя контейнера](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="060bd-181">По умолчанию доступ к контейнеру предоставляется только владельцу учетной записи.</span><span class="sxs-lookup"><span data-stu-id="060bd-181">By default, the container is private and can only be accessed by the account owner.</span></span> <span data-ttu-id="060bd-182">Чтобы разрешить общий доступ на чтение для больших двоичных объектов в контейнере, но не к свойствам и метаданным контейнера, используйте параметр **Общедоступный BLOB-объект** .</span><span class="sxs-lookup"><span data-stu-id="060bd-182">To allow public read access to the blobs in the container, but not to the container properties and metadata, use the **Public Blob** option.</span></span> <span data-ttu-id="060bd-183">Чтобы разрешить полный общий доступ на чтение для контейнера и больших двоичных объектов, используйте параметр **Общедоступный контейнер** .</span><span class="sxs-lookup"><span data-stu-id="060bd-183">To allow full public read access for the container and blobs, use the **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-the-connection-to-azure"></a><span data-ttu-id="060bd-184">Шаг 3. Подготовка подключения к Azure</span><span class="sxs-lookup"><span data-stu-id="060bd-184">Step 3: Prepare the connection to Azure</span></span>
<span data-ttu-id="060bd-185">Перед передачей VHD-файла необходимо установить безопасное соединение между компьютером и вашей подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="060bd-185">Before you can upload a .vhd file, you need to establish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="060bd-186">Это можно сделать, используя метод Azure Active Directory (Azure AD) или метод сертификатов.</span><span class="sxs-lookup"><span data-stu-id="060bd-186">You can use the Azure Active Directory (Azure AD) method or the certificate method to do it.</span></span>

### <a name="use-the-azure-ad-method-to-upload-a-vhd-file"></a><span data-ttu-id="060bd-187">Использование метода Azure AD для передачи VHD-файла</span><span class="sxs-lookup"><span data-stu-id="060bd-187">Use the Azure AD method to upload a .vhd file</span></span>
1. <span data-ttu-id="060bd-188">Откройте консоль Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="060bd-188">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="060bd-189">Введите следующую команду: </span><span class="sxs-lookup"><span data-stu-id="060bd-189">Type the following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="060bd-190">После выполнения команды откроется окно входа и вы сможете войти, используя свою рабочую или учебную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="060bd-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![Окно PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="060bd-192">Azure выполняет проверку подлинности и сохраняет учетные данные,</span><span class="sxs-lookup"><span data-stu-id="060bd-192">Azure authenticates and saves the credential information.</span></span> <span data-ttu-id="060bd-193">а затем закрывает окно.</span><span class="sxs-lookup"><span data-stu-id="060bd-193">Then it closes the window.</span></span>

### <a name="use-the-certificate-method-to-upload-a-vhd-file"></a><span data-ttu-id="060bd-194">Использование метода сертификата для передачи VHD-файла</span><span class="sxs-lookup"><span data-stu-id="060bd-194">Use the certificate method to upload a .vhd file</span></span>
1. <span data-ttu-id="060bd-195">Откройте консоль Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="060bd-195">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="060bd-196">Введите `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="060bd-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="060bd-197">В открывшемся окне браузера появится запрос на скачивание PUBLISHSETTINGS-файла.</span><span class="sxs-lookup"><span data-stu-id="060bd-197">A browser window opens and prompts you to download the .publishsettings file.</span></span> <span data-ttu-id="060bd-198">Этот файл содержит сведения и сертификат для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="060bd-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Страница скачивания браузера](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="060bd-200">Сохраните файл .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="060bd-200">Save the .publishsettings file.</span></span>
5. <span data-ttu-id="060bd-201">Введите `Import-AzurePublishSettingsFile <PathToFile>`, где `<PathToFile>` — это полный путь к файлу PUBLISHSETTINGS.</span><span class="sxs-lookup"><span data-stu-id="060bd-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is the full path to the .publishsettings file.</span></span>

   <span data-ttu-id="060bd-202">Дополнительные сведения см. в статье [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx) (Начало работы с командлетами Azure).</span><span class="sxs-lookup"><span data-stu-id="060bd-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="060bd-203">Дополнительные сведения об установке и настройке PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="060bd-203">For more information about installing and configuring PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-the-vhd-file"></a><span data-ttu-id="060bd-204">Шаг 4. Загрузка файла VHD</span><span class="sxs-lookup"><span data-stu-id="060bd-204">Step 4: Upload the .vhd file</span></span>
<span data-ttu-id="060bd-205">При передаче VHD-файла его можно поместить в любом месте внутри хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="060bd-205">When you upload the .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="060bd-206">Ниже приведены некоторые термины, которые будут использоваться при отправке файла.</span><span class="sxs-lookup"><span data-stu-id="060bd-206">Following are some terms you will use when you upload the file:</span></span>

* <span data-ttu-id="060bd-207">**BlobStorageURL** — URL-адрес для учетной записи хранения, созданной на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="060bd-207">**BlobStorageURL** is the URL for the storage account that you created in Step 2.</span></span>
* <span data-ttu-id="060bd-208">**YourImagesFolder** — контейнер внутри хранилища BLOB-объектов, где будут храниться образы.</span><span class="sxs-lookup"><span data-stu-id="060bd-208">**YourImagesFolder** is the container within Blob storage where you want to store your images.</span></span>
* <span data-ttu-id="060bd-209">**VHDName** — это метка, которая отображается на классическом портале Azure для идентификации виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="060bd-209">**VHDName** is the label that appears in the Azure classic portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="060bd-210">**PathToVHDFile** — это полный путь и имя файла .vhd.</span><span class="sxs-lookup"><span data-stu-id="060bd-210">**PathToVHDFile** is the full path and name of the .vhd file.</span></span>

<span data-ttu-id="060bd-211">В окне Azure PowerShell, использованном при выполнении предыдущего шага, введите:</span><span class="sxs-lookup"><span data-stu-id="060bd-211">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-the-uploaded-vhd-file"></a><span data-ttu-id="060bd-212">Шаг 5. Создание виртуальной машины с использованием переданного VHD-файла</span><span class="sxs-lookup"><span data-stu-id="060bd-212">Step 5: Create a VM with the uploaded .vhd file</span></span>
<span data-ttu-id="060bd-213">После передачи VHD-файл можно добавить в качестве образа в список пользовательских образов, связанных с вашей подпиской, и создать виртуальную машину с помощью этого пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="060bd-213">After you upload the .vhd file, you can add it as an image to the list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="060bd-214">В окне Azure PowerShell, использованном при выполнении предыдущего шага, введите:</span><span class="sxs-lookup"><span data-stu-id="060bd-214">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of the VHD> -OS <Type of the OS on the VHD>

   > [!NOTE]
   > <span data-ttu-id="060bd-215">В качестве типа ОС используйте Linux.</span><span class="sxs-lookup"><span data-stu-id="060bd-215">Use Linux as the OS type.</span></span> <span data-ttu-id="060bd-216">Текущая версия Azure PowerShell принимает в качестве значения параметра только Linux или Windows.</span><span class="sxs-lookup"><span data-stu-id="060bd-216">The current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="060bd-217">После выполнения предыдущих шагов новый образ отображается при выборе вкладки **Образы** на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="060bd-217">After you complete the previous steps, the new image is listed when you choose the **Images** tab on the Azure classic portal.</span></span>  

    ![Выбор образа](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="060bd-219">Создайте виртуальную машину из коллекции.</span><span class="sxs-lookup"><span data-stu-id="060bd-219">Create a virtual machine from the gallery.</span></span> <span data-ttu-id="060bd-220">Этот новый образ теперь доступен в разделе **Мои образы**.</span><span class="sxs-lookup"><span data-stu-id="060bd-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="060bd-221">Выберите новый образ.</span><span class="sxs-lookup"><span data-stu-id="060bd-221">Select the new image.</span></span> <span data-ttu-id="060bd-222">Затем выполните указания для настройки имени узла, пароля, SSH-ключа и т. п.</span><span class="sxs-lookup"><span data-stu-id="060bd-222">Next, go through the prompts to set up a host name, password, SSH key, and so on.</span></span>

    ![Пользовательский образ](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="060bd-224">После завершения подготовки вы увидите в Azure запущенную виртуальную машину FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="060bd-224">After you complete the provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Образ FreeBSD в Azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
