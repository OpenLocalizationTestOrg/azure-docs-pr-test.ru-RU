---
title: "aaaCreate и передачи Виртуальной машине OpenBSD изображений tooAzure | Документы Microsoft"
description: "Узнайте, как toocreate и передача виртуального жесткого диска (VHD), содержащий hello toocreate OpenBSD операционной системы виртуальной машины Azure через Azure CLI"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a><span data-ttu-id="89bc8-103">Создание и отправка tooAzure образ диска OpenBSD</span><span class="sxs-lookup"><span data-stu-id="89bc8-103">Create and Upload an OpenBSD disk image tooAzure</span></span>
<span data-ttu-id="89bc8-104">В этой статье показано, как toocreate и передача виртуального жесткого диска (VHD), содержащий hello OpenBSD операционной системы.</span><span class="sxs-lookup"><span data-stu-id="89bc8-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello OpenBSD operating system.</span></span> <span data-ttu-id="89bc8-105">После загрузки, она может служить toocreate собственный образ виртуальной машины (VM) в Azure через Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="89bc8-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="89bc8-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="89bc8-106">Prerequisites</span></span>
<span data-ttu-id="89bc8-107">В этой статье предполагается, что hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="89bc8-107">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="89bc8-108">**Подписка Azure.** Если у вас нет учетной записи, то ее можно создать, что займет всего лишь несколько минут.</span><span class="sxs-lookup"><span data-stu-id="89bc8-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="89bc8-109">Если у вас есть подписка MSDN, см. страницу [Ежемесячная сумма денег на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="89bc8-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="89bc8-110">В противном случае — Узнайте, каким образом слишком[создать бесплатную пробную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89bc8-110">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="89bc8-111">**Azure CLI 2.0** -убедитесь, что у вас есть hello последней [Azure CLI 2.0](/cli/azure/install-azure-cli) установлен и вход tooyour учетная запись Azure с [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="89bc8-111">**Azure CLI 2.0** - Make sure you have hello latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in tooyour Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="89bc8-112">**OpenBSD операционной системы, установленной в VHD-файл** -поддерживаемой операционной системы OpenBSD (версии 6.1) должен быть tooa установленного виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="89bc8-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="89bc8-113">Существуют несколько средства toocreate VHD-файлы.</span><span class="sxs-lookup"><span data-stu-id="89bc8-113">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="89bc8-114">Например можно использовать решение виртуализации, таких как Hyper-V toocreate hello VHD-файл и установить hello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="89bc8-114">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="89bc8-115">Инструкции о том, как tooinstall и использование Hyper-V, на экране [Установка Hyper-V и создание виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="89bc8-115">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="89bc8-116">Подготовка образа OpenBSD для Azure</span><span class="sxs-lookup"><span data-stu-id="89bc8-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="89bc8-117">На hello виртуальной Машины, где установлен hello OpenBSD операционную систему 6.1, которая добавлена поддержка Hyper-V, выполните hello следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="89bc8-117">On hello VM where you installed hello OpenBSD operating system 6.1, which added Hyper-V support, complete hello following procedures:</span></span>

1. <span data-ttu-id="89bc8-118">Если DHCP не включен во время установки, включите службу hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89bc8-118">If DHCP is not enabled during installation, enable hello service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="89bc8-119">Настройте последовательную консоль.</span><span class="sxs-lookup"><span data-stu-id="89bc8-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="89bc8-120">Настройте пакет установки следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89bc8-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="89bc8-121">По умолчанию hello `root` пользователь отключен на виртуальных машинах в Azure.</span><span class="sxs-lookup"><span data-stu-id="89bc8-121">By default, hello `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="89bc8-122">Пользователи могут запускать команды с повышенными привилегиями, используя hello `doas` на OpenBSD виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="89bc8-122">Users can run commands with elevated privileges by using hello `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="89bc8-123">Doas включен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="89bc8-123">Doas is enabled by default.</span></span> <span data-ttu-id="89bc8-124">Дополнительные сведения см. на веб-сайте [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="89bc8-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="89bc8-125">Установка и настройка необходимых компонентов для hello агент Azure следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89bc8-125">Install and configure prerequisites for hello Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="89bc8-126">всегда Hello последний выпуск hello Azure агента можно найти на [Github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="89bc8-126">hello latest release of hello Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="89bc8-127">Установка агента hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89bc8-127">Install hello agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="89bc8-128">После установки агента Azure очень хорошее представление tooverify, на котором выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89bc8-128">After you install Azure Agent, it's a good idea tooverify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="89bc8-129">Отзыв hello системы tooclean его и внести он подходит для инициализацию.</span><span class="sxs-lookup"><span data-stu-id="89bc8-129">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="89bc8-130">Hello следующая команда также удаляет hello последнего подготовленных учетную запись и hello связанных данных:</span><span class="sxs-lookup"><span data-stu-id="89bc8-130">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="89bc8-131">Теперь вы можете завершить работу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="89bc8-131">Now you can shut down your VM.</span></span>


## <a name="prepare-hello-vhd"></a><span data-ttu-id="89bc8-132">Подготовка hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="89bc8-132">Prepare hello VHD</span></span>
<span data-ttu-id="89bc8-133">Hello формат VHDX не поддерживается только в Azure, **фиксированный VHD**.</span><span class="sxs-lookup"><span data-stu-id="89bc8-133">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="89bc8-134">Можно преобразовать с помощью диспетчера Hyper-V VHD формат hello диск toofixed или hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) командлета.</span><span class="sxs-lookup"><span data-stu-id="89bc8-134">You can convert hello disk toofixed VHD format using Hyper-V Manager or hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="89bc8-135">Например.</span><span class="sxs-lookup"><span data-stu-id="89bc8-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="89bc8-136">Создание и передача ресурсов хранилища</span><span class="sxs-lookup"><span data-stu-id="89bc8-136">Create storage resources and upload</span></span>
<span data-ttu-id="89bc8-137">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="89bc8-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="89bc8-138">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="89bc8-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="89bc8-139">tooupload виртуальный жесткий ДИСК, создайте учетную запись хранения с [создания учетной записи хранилища az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="89bc8-139">tooupload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="89bc8-140">Имя учетной записи хранения должно быть уникальным, поэтому введите собственное имя.</span><span class="sxs-lookup"><span data-stu-id="89bc8-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="89bc8-141">Hello следующий пример создает учетную запись хранения с именем *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="89bc8-141">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="89bc8-142">toocontrol доступ к учетной записи хранилища toohello, получите ключ хранилища hello с [список ключей учетной записи хранилища az](/cli/azure/storage/account/keys#list) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89bc8-142">toocontrol access toohello storage account, obtain hello storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="89bc8-143">отдельные hello toologically виртуальные жесткие диски, вы отправляете, создать контейнер в учетной записи хранилища hello с [создать контейнер хранилища az](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="89bc8-143">toologically separate hello VHDs you upload, create a container within hello storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="89bc8-144">Наконец, отправьте ваш VHD с помощью команды [az storage blob upload](/cli/azure/storage/blob#upload) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89bc8-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="89bc8-145">Создание виртуальной машины из VHD</span><span class="sxs-lookup"><span data-stu-id="89bc8-145">Create VM from your VHD</span></span>
<span data-ttu-id="89bc8-146">Можно создать виртуальную машину с помощью [примера скрипта](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) или напрямую с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="89bc8-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="89bc8-147">toospecify hello OpenBSD виртуального жесткого диска вы отправили hello используйте `--image` параметр следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89bc8-147">toospecify hello OpenBSD VHD you uploaded, use hello `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="89bc8-148">Получить hello IP-адрес для виртуальной Машины с OpenBSD [ВМ az список ip адреса](/cli/azure/vm#list-ip-addresses) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89bc8-148">Obtain hello IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="89bc8-149">Теперь вы можете SSH tooyour OpenBSD ВМ в обычном режиме:</span><span class="sxs-lookup"><span data-stu-id="89bc8-149">Now you can SSH tooyour OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="89bc8-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89bc8-150">Next steps</span></span>
<span data-ttu-id="89bc8-151">Дополнительные сведения о Hyper-V поддерживает на OpenBSD6.1 tooknow прочитать [OpenBSD 6.1](https://www.openbsd.org/61.html) и [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="89bc8-151">If you want tooknow more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="89bc8-152">Toocreate ВМ из управляемого диска следует прочитать [диска az](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="89bc8-152">If you want toocreate a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 
