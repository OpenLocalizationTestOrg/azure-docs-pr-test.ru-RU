---
title: "aaaSet копирование Oracle ASM на виртуальной машине Azure Linux | Документы Microsoft"
description: "Быстрая подготовка и запуск Oracle ASM в среде Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="523c6-103">Настройка Oracle ASM в виртуальной машине Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="523c6-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="523c6-104">Виртуальные машины Azure предоставляют полностью настраиваемую и гибкую вычислительную среду.</span><span class="sxs-lookup"><span data-stu-id="523c6-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="523c6-105">В этом учебнике описано развертывание основных Azure виртуальной машины, в сочетании с hello установки и настройки из Oracle автоматического хранения данных управления (ASM).</span><span class="sxs-lookup"><span data-stu-id="523c6-105">This tutorial covers basic Azure virtual machine deployment combined with hello installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="523c6-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="523c6-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="523c6-107">Создать и присоединить tooan виртуальной Машины базы данных Oracle</span><span class="sxs-lookup"><span data-stu-id="523c6-107">Create and connect tooan Oracle Database VM</span></span>
> * <span data-ttu-id="523c6-108">Установка и настройка Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="523c6-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="523c6-109">Установка и настройка Oracle Grid Infrastructure.</span><span class="sxs-lookup"><span data-stu-id="523c6-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="523c6-110">Инициализация установки Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="523c6-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="523c6-111">Создание базы данных Oracle под управлением ASM.</span><span class="sxs-lookup"><span data-stu-id="523c6-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="523c6-112">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="523c6-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="523c6-113">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="523c6-114">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="523c6-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-hello-environment"></a><span data-ttu-id="523c6-115">Подготовка среды hello</span><span class="sxs-lookup"><span data-stu-id="523c6-115">Prepare hello environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="523c6-116">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="523c6-116">Create a resource group</span></span>

<span data-ttu-id="523c6-117">использовать toocreate группу ресурсов hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="523c6-117">toocreate a resource group, use hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="523c6-118">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="523c6-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="523c6-119">В этом примере имя группы ресурсов *myResourceGroup* в hello *eastus* области.</span><span class="sxs-lookup"><span data-stu-id="523c6-119">In this example, a resource group named *myResourceGroup* in hello *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="523c6-120">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="523c6-120">Create a VM</span></span>

<span data-ttu-id="523c6-121">toocreate виртуальной машины на основе образа hello базы данных Oracle и настройте его toouse Oracle ASM, использовать hello [создания виртуальной машины az](/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="523c6-121">toocreate a virtual machine based on hello Oracle Database image and configure it toouse Oracle ASM, use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="523c6-122">Hello следующий пример создает виртуальную Машину с именем myVM, имеет размер Standard_DS2_v2 с четырьмя подключенными дисками данных 50 ГБ.</span><span class="sxs-lookup"><span data-stu-id="523c6-122">hello following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="523c6-123">Если они еще не существуют в ключевое расположение по умолчанию hello, он также создает ключи SSH.</span><span class="sxs-lookup"><span data-stu-id="523c6-123">If they do not already exist in hello default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="523c6-124">toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.</span><span class="sxs-lookup"><span data-stu-id="523c6-124">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="523c6-125">После создания виртуальной Машины hello Azure CLI отображает toohello аналогичные сведения, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="523c6-125">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="523c6-126">Запомните значение hello для `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="523c6-126">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="523c6-127">Используется этот адрес tooaccess hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="523c6-127">You use this address tooaccess hello VM.</span></span>

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a><span data-ttu-id="523c6-128">Подключение toohello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="523c6-128">Connect toohello VM</span></span>

<span data-ttu-id="523c6-129">toocreate сеанс SSH с hello виртуальной Машины и настроить дополнительные параметры, используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-129">toocreate an SSH session with hello VM and configure additional settings, use hello following command.</span></span> <span data-ttu-id="523c6-130">Замените hello hello IP-адрес `publicIpAddress` значение для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="523c6-130">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="523c6-131">Установка Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="523c6-131">Install Oracle ASM</span></span>

<span data-ttu-id="523c6-132">tooinstall ASM Oracle, полный hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="523c6-132">tooinstall Oracle ASM, complete hello following steps.</span></span> 

<span data-ttu-id="523c6-133">Дополнительные сведения об установке Oracle ASM см. в статье [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html) (Скачиваемые компоненты Oracle ASMLib для Oracle Linux 6).</span><span class="sxs-lookup"><span data-stu-id="523c6-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="523c6-134">Требуется toologin как корневой элемент в порядке toocontinue с установкой ассемблерного кода:</span><span class="sxs-lookup"><span data-stu-id="523c6-134">You need toologin as root in order toocontinue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="523c6-135">Выполните эти дополнительные команды tooinstall Oracle ASM компоненты:</span><span class="sxs-lookup"><span data-stu-id="523c6-135">Run these additional commands tooinstall Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="523c6-136">Убедитесь, что служба Oracle ASM установлена:</span><span class="sxs-lookup"><span data-stu-id="523c6-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="523c6-137">Hello выходные данные этой команды должен содержать hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="523c6-137">hello output of this command should list hello following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="523c6-138">ASM требует определенных пользователей и ролей в порядке toofunction правильно.</span><span class="sxs-lookup"><span data-stu-id="523c6-138">ASM requires specific users and roles in order toofunction correctly.</span></span> <span data-ttu-id="523c6-139">hello необходимых учетных записей и групп, создайте Hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="523c6-139">hello following commands create hello pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="523c6-140">Убедитесь, что пользователи и группы созданы правильно:</span><span class="sxs-lookup"><span data-stu-id="523c6-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="523c6-141">Hello выходные данные этой команды должны содержать следующие hello пользователей и групп:</span><span class="sxs-lookup"><span data-stu-id="523c6-141">hello output of this command should list hello following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="523c6-142">Создайте папку для пользователя *сетки* и сменить владельца hello:</span><span class="sxs-lookup"><span data-stu-id="523c6-142">Create a folder for user *grid* and change hello owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="523c6-143">Настройка Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="523c6-143">Set up Oracle ASM</span></span>

<span data-ttu-id="523c6-144">В этом учебнике — пользователя по умолчанию hello *сетки* и группа по умолчанию hello *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="523c6-144">For this tutorial, hello default user is *grid* and hello default group is *asmadmin*.</span></span> <span data-ttu-id="523c6-145">Убедитесь, что hello *oracle* пользователь является членом группы asmadmin hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-145">Ensure that hello *oracle* user is part of hello asmadmin group.</span></span> <span data-ttu-id="523c6-146">tooset копирование установку Oracle ASM завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="523c6-146">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="523c6-147">Настройка библиотеки драйвера hello Oracle ASM заключается в определении пользователя по умолчанию hello (сетка) и группа по умолчанию (asmadmin) и настройка toostart hello диска во время загрузки (выберите y) и tooscan для дисков во время загрузки (выберите y).</span><span class="sxs-lookup"><span data-stu-id="523c6-147">Setting up hello Oracle ASM library driver involves defining hello default user (grid) and default group (asmadmin) as well as configuring hello drive toostart on boot (choose y) and tooscan for disks on boot (choose y).</span></span> <span data-ttu-id="523c6-148">Требуется tooanswer запросы hello hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="523c6-148">You need tooanswer hello prompts from hello following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="523c6-149">Hello выходные данные этой команды должен выглядеть примерно toohello следующие, остановка с toobe приглашения ответов на.</span><span class="sxs-lookup"><span data-stu-id="523c6-149">hello output of this command should look similar toohello following, stopping with prompts toobe answered.</span></span>

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="523c6-150">Просмотр конфигурации диска hello:</span><span class="sxs-lookup"><span data-stu-id="523c6-150">View hello disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="523c6-151">Hello выходные данные этой команды должен выглядеть примерно toohello следующий список доступных дисков</span><span class="sxs-lookup"><span data-stu-id="523c6-151">hello output of this command should look similar toohello following listing of available disks</span></span>

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. <span data-ttu-id="523c6-152">Отформатировать диск *иметь идентификатор/dev/sdc* , выполнив hello следующую команду и ответы на hello приглашения с:</span><span class="sxs-lookup"><span data-stu-id="523c6-152">Format disk */dev/sdc* by running hello following command and answering hello prompts with:</span></span>
   - <span data-ttu-id="523c6-153">*n* — новый раздел;</span><span class="sxs-lookup"><span data-stu-id="523c6-153">*n* for new partition</span></span>
   - <span data-ttu-id="523c6-154">*p* — основной раздел;</span><span class="sxs-lookup"><span data-stu-id="523c6-154">*p* for primary partition</span></span>
   - <span data-ttu-id="523c6-155">*1* tooselect hello первую секцию</span><span class="sxs-lookup"><span data-stu-id="523c6-155">*1* tooselect hello first partition</span></span>
   - <span data-ttu-id="523c6-156">Нажмите клавишу `enter` для первого цилиндра по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="523c6-156">press `enter` for hello default first cylinder</span></span>
   - <span data-ttu-id="523c6-157">Нажмите клавишу `enter` для последнего цилиндра по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="523c6-157">press `enter` for hello default last cylinder</span></span>
   - <span data-ttu-id="523c6-158">Нажмите клавишу *w* toowrite hello изменения toohello секции таблицы</span><span class="sxs-lookup"><span data-stu-id="523c6-158">press *w* toowrite hello changes toohello partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="523c6-159">Используя приведенные выше ответы hello, должен выглядеть hello выходные данные команды fdisk hello hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="523c6-159">Using hello answers provided above, hello output for hello fdisk command should look like hello following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="523c6-160">Повторите hello предшествующий команды fdisk для `/dev/sdd`, `/dev/sde`, и `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="523c6-160">Repeat hello preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="523c6-161">Проверьте конфигурацию диска hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-161">Check hello disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="523c6-162">Hello выходные данные команды hello должен выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="523c6-162">hello output of hello command should look like hello following:</span></span>

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. <span data-ttu-id="523c6-163">Проверьте состояние службы Oracle ассемблерного кода hello и запустить службу hello Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="523c6-163">Check hello Oracle ASM service status and start hello Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="523c6-164">Hello выходные данные команды hello должен выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="523c6-164">hello output of hello command should look like hello following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="523c6-165">Создайте диски Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="523c6-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="523c6-166">Hello выходные данные команды hello должен выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="523c6-166">hello output of hello command should look like hello following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="523c6-167">Выведите список дисков Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="523c6-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="523c6-168">выходные данные Hello hello команды должны содержать off hello следующие диски Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="523c6-168">hello output of hello command should list off hello following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="523c6-169">Измените пароли hello для пользователей hello корневой сервер, oracle и сетки.</span><span class="sxs-lookup"><span data-stu-id="523c6-169">Change hello passwords for hello root, oracle, and grid users.</span></span> <span data-ttu-id="523c6-170">**Запишите эти новые пароли** как с помощью их позднее, во время установки hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-170">**Make note of these new passwords** as you are using them later during hello installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="523c6-171">Измените разрешения папки hello:</span><span class="sxs-lookup"><span data-stu-id="523c6-171">Change hello folder permission:</span></span>

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="523c6-172">Скачивание и подготовка Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="523c6-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="523c6-173">toodownload и подготовки программного обеспечения Oracle сетки инфраструктуры hello, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="523c6-173">toodownload and prepare hello Oracle Grid Infrastructure software, complete hello following steps:</span></span>

1. <span data-ttu-id="523c6-174">Загрузить hello инфраструктуры сетки Oracle [страницы загрузки Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="523c6-174">Download Oracle Grid Infrastructure from hello [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="523c6-175">В разделе загрузок hello под названием **Oracle Database 12c выпуск 1 сетки инфраструктуры (12.1.0.2.0) для Linux x86-64**, загрузите hello два ZIP-файлов.</span><span class="sxs-lookup"><span data-stu-id="523c6-175">Under hello download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download hello two .zip files.</span></span>

2. <span data-ttu-id="523c6-176">После загрузки hello .zip файлы tooyour клиентского компьютера, можно использовать протокол Secure копии (SCP) toocopy hello файлы tooyour виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="523c6-176">After you download hello .zip files tooyour client computer, you can use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="523c6-177">SSH обратно в Oracle ВМ в Azure в порядке toomove hello ZIP-файлы в hello / opt папки.</span><span class="sxs-lookup"><span data-stu-id="523c6-177">SSH back into your Oracle VM in Azure in order toomove hello .zip files into hello /opt folder.</span></span> <span data-ttu-id="523c6-178">Затем измените владельца hello hello файлов:</span><span class="sxs-lookup"><span data-stu-id="523c6-178">Then, change hello owner of hello files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="523c6-179">Распакуйте файлы hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-179">Unzip hello files.</span></span> <span data-ttu-id="523c6-180">(Hello установки Linux Распакуйте средство, если он еще не установлен.)</span><span class="sxs-lookup"><span data-stu-id="523c6-180">(Install hello Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="523c6-181">Измените разрешение:</span><span class="sxs-lookup"><span data-stu-id="523c6-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="523c6-182">Обновите настроенную область буфера.</span><span class="sxs-lookup"><span data-stu-id="523c6-182">Update configured swap space.</span></span> <span data-ttu-id="523c6-183">Компоненты Oracle сетки требуется по крайней мере 6,8 ГБ пространства подкачки tooinstall сетки.</span><span class="sxs-lookup"><span data-stu-id="523c6-183">Oracle Grid components need at least 6.8 GB of swap space tooinstall Grid.</span></span> <span data-ttu-id="523c6-184">размер файла подкачки по умолчанию Hello для изображений Oracle Linux в Azure — 2048 МБ памяти.</span><span class="sxs-lookup"><span data-stu-id="523c6-184">hello default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="523c6-185">Требуется tooincrease `ResourceDisk.SwapSizeMB` в hello `/etc/waagent.conf` файл и перезапустите службу WALinuxAgent hello в порядке для hello обновлены параметры tootake эффекта.</span><span class="sxs-lookup"><span data-stu-id="523c6-185">You need tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` file and restart hello WALinuxAgent service in order for hello updated settings tootake effect.</span></span> <span data-ttu-id="523c6-186">Так как он является файлом только для чтения, необходимо разрешение на запись tooenable разрешения toochange файла.</span><span class="sxs-lookup"><span data-stu-id="523c6-186">Because it is a read-only file, you need toochange file permissions tooenable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="523c6-187">Поиск `ResourceDisk.SwapSizeMB` и измените значение hello слишком**8192**.</span><span class="sxs-lookup"><span data-stu-id="523c6-187">Search for `ResourceDisk.SwapSizeMB` and change hello value too**8192**.</span></span> <span data-ttu-id="523c6-188">Вам потребуется toopress `insert` режим вставки tooenter, введите значение hello **8192** и нажмите клавишу `esc` tooreturn toocommand режим.</span><span class="sxs-lookup"><span data-stu-id="523c6-188">You will need toopress `insert` tooenter insert mode, type in hello value of **8192** and then press `esc` tooreturn toocommand mode.</span></span> <span data-ttu-id="523c6-189">toowrite hello изменения и закройте hello, тип файла `:wq` и нажмите клавишу `enter`.</span><span class="sxs-lookup"><span data-stu-id="523c6-189">toowrite hello changes and quit hello file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="523c6-190">Настоятельно рекомендуется всегда использовать `WALinuxAgent` tooconfigure пространство подкачки, чтобы он всегда создается hello локальных временных диска (временный диск) для достижения оптимальной производительности.</span><span class="sxs-lookup"><span data-stu-id="523c6-190">We highly recommend that you always use `WALinuxAgent` tooconfigure swap space so that it's always created on hello local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="523c6-191">Дополнительные сведения о разделе [как файл tooadd переключения на виртуальных машинах Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="523c6-191">For more information on, see [How tooadd a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a><span data-ttu-id="523c6-192">Подготовить локального клиента и виртуальной Машины toorun x11</span><span class="sxs-lookup"><span data-stu-id="523c6-192">Prepare your local client and VM toorun x11</span></span>
<span data-ttu-id="523c6-193">Настройка Oracle ASM требуется графический интерфейс toocomplete hello установки и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="523c6-193">Configuring Oracle ASM requires a graphical interface toocomplete hello install and configuration.</span></span> <span data-ttu-id="523c6-194">Мы используем toofacilitate протокола hello x11 этой установки.</span><span class="sxs-lookup"><span data-stu-id="523c6-194">We are using hello x11 protocol toofacilitate this installation.</span></span> <span data-ttu-id="523c6-195">Если вы используете клиентскую систему (Mac или Linux), которая уже имеет X11 возможности включена и настроена — можно пропустить эту конфигурацию и настройки машин монопольного tooWindows.</span><span class="sxs-lookup"><span data-stu-id="523c6-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive tooWindows machines.</span></span> 

1. <span data-ttu-id="523c6-196">[Загрузить PuTTY](http://www.putty.org/) и [загрузки Xming](https://xming.en.softonic.com/) tooyour компьютер Windows.</span><span class="sxs-lookup"><span data-stu-id="523c6-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) tooyour Windows computer.</span></span> <span data-ttu-id="523c6-197">Вам необходима установка toocomplete hello оба приложения со значениями по умолчанию hello, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="523c6-197">You will need toocomplete hello installation of both of these applications with hello default values before proceeding.</span></span>

2. <span data-ttu-id="523c6-198">После установки PuTTY, откройте командную строку, перейдите в hello PuTTY папки (например, C:\Program Files\PuTTY) и запустите `puttygen.exe` чтобы toogenerate ключа.</span><span class="sxs-lookup"><span data-stu-id="523c6-198">After you install PuTTY, open a command prompt, change into hello PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order toogenerate a key.</span></span>

3. <span data-ttu-id="523c6-199">В генераторе ключей PuTTY сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="523c6-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="523c6-200">Создать ключ, выбрав hello `Generate` кнопки.</span><span class="sxs-lookup"><span data-stu-id="523c6-200">Generate a key by selecting hello `Generate` button.</span></span>
   2. <span data-ttu-id="523c6-201">Скопируйте содержимое hello hello ключ (сочетание клавиш Ctrl + C).</span><span class="sxs-lookup"><span data-stu-id="523c6-201">Copy hello contents of hello key (Ctrl+C).</span></span>
   3. <span data-ttu-id="523c6-202">Выберите hello `Save private key` кнопки.</span><span class="sxs-lookup"><span data-stu-id="523c6-202">Select hello `Save private key` button.</span></span>
   4. <span data-ttu-id="523c6-203">Пропустить hello предупреждение о защите hello ключ с помощью парольной фразы, а затем выберите `OK`.</span><span class="sxs-lookup"><span data-stu-id="523c6-203">Ignore hello warning about securing hello key with a passphrase, and then select `OK`.</span></span>

   ![Снимок экрана генератора ключей PuTTY](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="523c6-205">В виртуальной машине выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="523c6-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="523c6-206">Создайте файл с именем `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="523c6-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="523c6-207">Вставьте содержимое hello hello ключ в этом файле, а затем сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-207">Paste hello contents of hello key in this file, and then save hello file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="523c6-208">Hello ключ должен содержать строку hello `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="523c6-208">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="523c6-209">Кроме того содержимое hello hello ключа должно быть одну строку текста.</span><span class="sxs-lookup"><span data-stu-id="523c6-209">Also, hello contents of hello key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="523c6-210">В клиентской системе запустите PuTTY.</span><span class="sxs-lookup"><span data-stu-id="523c6-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="523c6-211">В hello **категории** панели перейдите слишком**подключения** > **SSH** > **Auth**. В hello **файла закрытого ключа для проверки подлинности** поле, найдите toohello ключ, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="523c6-211">In hello **Category** pane, go too**Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

   ![Снимок экрана параметров проверки подлинности SSH hello](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="523c6-213">В hello **категории** панели перейдите слишком**подключения** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="523c6-213">In hello **Category** pane, go too**Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="523c6-214">Выберите hello **включить X11 пересылку** флажок.</span><span class="sxs-lookup"><span data-stu-id="523c6-214">Select hello **Enable X11 forwarding** check box.</span></span>

   ![Снимок экрана: hello SSH X11 параметры пересылки](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="523c6-216">В hello **категории** панели перейдите слишком**сеанса**.</span><span class="sxs-lookup"><span data-stu-id="523c6-216">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="523c6-217">Введите ВМ ASM Oracle `<publicIPaddress>` hello имя диалоговом окне узла, заполните в новый `Saved Session` имя и нажмите кнопку на `Save`.</span><span class="sxs-lookup"><span data-stu-id="523c6-217">Enter your Oracle ASM VM `<publicIPaddress>` in hello host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="523c6-218">После сохранения щелкните `open` tooconnect tooyour Oracle ASM виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="523c6-218">Once saved, click on `open` tooconnect tooyour Oracle ASM virtual machine.</span></span>  <span data-ttu-id="523c6-219">Hello первом подключении вам предупреждение указывает на то что hello удаленной системе не кэшируются в реестре.</span><span class="sxs-lookup"><span data-stu-id="523c6-219">hello first time you connect you are warned  hello remote system is not cached in your registry.</span></span> <span data-ttu-id="523c6-220">Щелкните `yes` tooadd его и продолжить.</span><span class="sxs-lookup"><span data-stu-id="523c6-220">Click on `yes` tooadd it and continue.</span></span>

   ![Снимок экрана параметров сеанса PuTTY hello](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="523c6-222">Установка Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="523c6-222">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="523c6-223">tooinstall инфраструктуры сетки Oracle, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="523c6-223">tooinstall Oracle Grid Infrastructure, complete hello following steps:</span></span>

1. <span data-ttu-id="523c6-224">Выполните вход в качестве пользователя **grid**.</span><span class="sxs-lookup"><span data-stu-id="523c6-224">Sign in as **grid**.</span></span> <span data-ttu-id="523c6-225">(Вы должны иметь доступ toosign в без необходимости вводить пароль.)</span><span class="sxs-lookup"><span data-stu-id="523c6-225">(You should be able toosign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="523c6-226">Если вы используете Windows, убедитесь, что вы запустили Xming перед началом установки hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-226">If you are running Windows, make sure you have started Xming before you begin hello installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="523c6-227">Откроется установщик Oracle Grid Infrastructure 12c Release 1.</span><span class="sxs-lookup"><span data-stu-id="523c6-227">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="523c6-228">(Может занять несколько минут для hello установщика toostart.)</span><span class="sxs-lookup"><span data-stu-id="523c6-228">(It might take a few minutes for hello  installer toostart.)</span></span>

2. <span data-ttu-id="523c6-229">На hello **выберите вариант установки** выберите **Установка и Настройка инфраструктуры сетки Oracle для автономного сервера**.</span><span class="sxs-lookup"><span data-stu-id="523c6-229">On hello **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Снимок экрана со страницей выберите вариант установки установщика hello](./media/oracle-asm/install01.png)

3. <span data-ttu-id="523c6-231">На hello **выберите языки продукта** Убедитесь **английского** или выбран нужный язык hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-231">On hello **Select Product Languages** page, ensure **English** or hello language that you want is selected.</span></span>  <span data-ttu-id="523c6-232">Щелкните `next`.</span><span class="sxs-lookup"><span data-stu-id="523c6-232">Click `next`.</span></span>

4. <span data-ttu-id="523c6-233">На hello **создать группу дисков ASM** страницы:</span><span class="sxs-lookup"><span data-stu-id="523c6-233">On hello **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="523c6-234">Введите имя для группы дисков hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-234">Enter a name for hello disk group.</span></span>
   - <span data-ttu-id="523c6-235">В разделе **Redundancy** (Избыточность) выберите **External** (Внешняя).</span><span class="sxs-lookup"><span data-stu-id="523c6-235">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="523c6-236">В списке **Allocation Unit Size** (Размер единицы распределения) выберите значение **4**.</span><span class="sxs-lookup"><span data-stu-id="523c6-236">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="523c6-237">В разделе **Add Disks** (Добавление дисков) выберите **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="523c6-237">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="523c6-238">Щелкните `next`.</span><span class="sxs-lookup"><span data-stu-id="523c6-238">Click `next`.</span></span>

5. <span data-ttu-id="523c6-239">На hello **укажите пароль ASM** страницу, выберите hello **использовать одинаковые пароли для этих учетных записей** и введите пароль.</span><span class="sxs-lookup"><span data-stu-id="523c6-239">On hello **Specify ASM Password** page, select hello **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Снимок экрана со страницей укажите пароль ассемблерного кода hello установщика](./media/oracle-asm/install04.png)

6. <span data-ttu-id="523c6-241">На hello **Указание параметров управления** страницы, у вас есть tooconfigure hello параметр EM облака управления.</span><span class="sxs-lookup"><span data-stu-id="523c6-241">On hello **Specify Management Options** page, you have hello option tooconfigure EM Cloud Control.</span></span> <span data-ttu-id="523c6-242">Этот параметр будет пропущено - щелкните `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="523c6-242">We are skipping this option - click `next` toocontinue.</span></span> 

7. <span data-ttu-id="523c6-243">На hello **привилегированных групп ОС** , используйте параметры по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-243">On hello **Privileged Operating System Groups** page, use hello default settings.</span></span> <span data-ttu-id="523c6-244">Нажмите кнопку `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="523c6-244">Click `next` toocontinue.</span></span>

8. <span data-ttu-id="523c6-245">На hello **укажите место установки** , используйте параметры по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-245">On hello **Specify Installation Location** page, use hello default settings.</span></span> <span data-ttu-id="523c6-246">Нажмите кнопку `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="523c6-246">Click `next` toocontinue.</span></span>

9. <span data-ttu-id="523c6-247">На hello **создать инвентаризации** измените hello инвентаризации каталога слишком`/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="523c6-247">On hello **Create Inventory** page, change hello Inventory Directory too`/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="523c6-248">Нажмите кнопку `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="523c6-248">Click `next` toocontinue.</span></span>

   ![Снимок экрана со страницей создать инвентаризации hello установщика](./media/oracle-asm/install08.png)

10. <span data-ttu-id="523c6-250">На hello **конфигурация выполнения сценария корневого** страницу, выберите hello **автоматически запускать скрипты настройки** флажок.</span><span class="sxs-lookup"><span data-stu-id="523c6-250">On hello **Root script execution configuration** page, select hello **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="523c6-251">Выберите hello **использовать учетные данные пользователя «root»** и введите пароль пользователя root hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-251">Then, select hello **Use "root" user credential** option, and enter hello root user password.</span></span>

    ![Снимок экрана установщика hello корневой сценария выполнения страницы "Конфигурация"](./media/oracle-asm/install09.png)

11. <span data-ttu-id="523c6-253">На hello **выполнения проверки готовности к установке** странице hello текущей настройки будут завершаться с ошибками.</span><span class="sxs-lookup"><span data-stu-id="523c6-253">On hello **Perform Prerequisite Checks** page, hello current setup will fail with errors.</span></span> <span data-ttu-id="523c6-254">Это ожидаемое поведение.</span><span class="sxs-lookup"><span data-stu-id="523c6-254">This is an expected behavior.</span></span> <span data-ttu-id="523c6-255">Выберите `Fix & Check Again`.</span><span class="sxs-lookup"><span data-stu-id="523c6-255">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="523c6-256">В hello **адресная привязка скрипта** диалоговое окно, нажмите кнопку `OK`.</span><span class="sxs-lookup"><span data-stu-id="523c6-256">In hello **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="523c6-257">На hello **Сводка** страницы, просмотрите выбранные параметры и нажмите кнопку `Install`.</span><span class="sxs-lookup"><span data-stu-id="523c6-257">On hello **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Снимок экрана: hello установщика страница «Сводка»](./media/oracle-asm/install12.png)

14. <span data-ttu-id="523c6-259">Диалоговое окно предупреждения отображается информирования сценариев настройки требуется toobe запуска от имени привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="523c6-259">A warning dialog box appears informing you configuration scripts need toobe run as a privileged user.</span></span> <span data-ttu-id="523c6-260">Нажмите кнопку `Yes` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="523c6-260">Click `Yes` toocontinue.</span></span>

15. <span data-ttu-id="523c6-261">На hello **Готово** щелкните `Close` toofinish hello установки.</span><span class="sxs-lookup"><span data-stu-id="523c6-261">On hello **Finish** page, click `Close` toofinish hello installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="523c6-262">Настройка установки Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="523c6-262">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="523c6-263">tooset копирование установку Oracle ASM завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="523c6-263">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="523c6-264">Убедитесь, что в сеансе X11 по-прежнему используется пользователь **grid**.</span><span class="sxs-lookup"><span data-stu-id="523c6-264">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="523c6-265">Может потребоваться toohit `enter` toorevive hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="523c6-265">You might need toohit `enter` toorevive hello terminal.</span></span> <span data-ttu-id="523c6-266">Затем запустите hello Oracle автоматическое хранилище управления помощник по настройке:</span><span class="sxs-lookup"><span data-stu-id="523c6-266">Then launch hello Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="523c6-267">Откроется Oracle ASM Configuration Assistant.</span><span class="sxs-lookup"><span data-stu-id="523c6-267">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="523c6-268">В hello **Настройка ASM: группы дисков** диалогового окна выберите hello `Create` , а затем нажмите `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="523c6-268">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="523c6-269">В hello **создать группу дисков** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="523c6-269">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="523c6-270">Введите имя группы диска hello **данные**.</span><span class="sxs-lookup"><span data-stu-id="523c6-270">Enter hello disk group name **DATA**.</span></span>
   - <span data-ttu-id="523c6-271">В разделе **Select Member Disks** (Выбор дисков-участников) выберите **ORCL_DATA** и **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="523c6-271">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="523c6-272">В списке **Allocation Unit Size** (Размер единицы распределения) выберите значение **4**.</span><span class="sxs-lookup"><span data-stu-id="523c6-272">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="523c6-273">Нажмите кнопку `ok` группы дисков toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-273">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="523c6-274">Нажмите кнопку `ok` окно подтверждения tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-274">Click `ok` tooclose hello confirmation window.</span></span>

   ![Снимок экрана диалогового окна создания группы дисков hello](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="523c6-276">В hello **Настройка ASM: группы дисков** диалогового окна выберите hello `Create` , а затем нажмите `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="523c6-276">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="523c6-277">В hello **создать группу дисков** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="523c6-277">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="523c6-278">Введите имя группы диска hello **FRA**.</span><span class="sxs-lookup"><span data-stu-id="523c6-278">Enter hello disk group name **FRA**.</span></span>
   - <span data-ttu-id="523c6-279">В разделе **Redundancy** (Избыточность) выберите **External (none)** (Внешняя(нет)).</span><span class="sxs-lookup"><span data-stu-id="523c6-279">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="523c6-280">В разделе **Select Member Disks** (Выбор дисков-участников) выберите **ORCL_FRA**.</span><span class="sxs-lookup"><span data-stu-id="523c6-280">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="523c6-281">В списке **Allocation Unit Size** (Размер единицы распределения) выберите значение **4**.</span><span class="sxs-lookup"><span data-stu-id="523c6-281">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="523c6-282">Нажмите кнопку `ok` группы дисков toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-282">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="523c6-283">Нажмите кнопку `ok` окно подтверждения tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-283">Click `ok` tooclose hello confirmation window.</span></span>

   ![Снимок экрана диалогового окна создания группы дисков hello](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="523c6-285">Выберите **выхода** tooclose ASM Configuration Assistant.</span><span class="sxs-lookup"><span data-stu-id="523c6-285">Select **Exit** tooclose ASM Configuration Assistant.</span></span>

   ![Снимок экрана: hello, настройте ASM: диалоговое окно группы дисков с кнопки выхода](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a><span data-ttu-id="523c6-287">Создание базы данных hello</span><span class="sxs-lookup"><span data-stu-id="523c6-287">Create hello database</span></span>

<span data-ttu-id="523c6-288">Hello программное обеспечение базы данных Oracle уже установлены на изображении hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="523c6-288">hello Oracle database software is already installed on hello Azure Marketplace image.</span></span> <span data-ttu-id="523c6-289">toocreate базы данных полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="523c6-289">toocreate a database, complete hello following steps:</span></span>

1. <span data-ttu-id="523c6-290">Переключение пользователей toohello Oracle суперпользователя, а затем инициализируйте hello прослушивателя для ведения журнала:</span><span class="sxs-lookup"><span data-stu-id="523c6-290">Switch users toohello Oracle superuser, and then initialize hello listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="523c6-291">Откроется Database Configuration Assistant.</span><span class="sxs-lookup"><span data-stu-id="523c6-291">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="523c6-292">На hello **операции базы данных** щелкните `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="523c6-292">On hello **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="523c6-293">На hello **режимом создания** страницы:</span><span class="sxs-lookup"><span data-stu-id="523c6-293">On hello **Creation Mode** page:</span></span>

   - <span data-ttu-id="523c6-294">Введите имя для базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-294">Enter a name for hello database.</span></span>
   - <span data-ttu-id="523c6-295">Выберите **Automatic Storage Management (ASM)** в качестве **типа хранилища**.</span><span class="sxs-lookup"><span data-stu-id="523c6-295">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="523c6-296">Для **расположение файлов базы данных**, использовать значение по умолчанию hello ASM предложенные расположения.</span><span class="sxs-lookup"><span data-stu-id="523c6-296">For **Database Files Location**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="523c6-297">Для **быстрого восстановления области**, использовать значение по умолчанию hello ASM предложенные расположения.</span><span class="sxs-lookup"><span data-stu-id="523c6-297">For **Fast Recovery Area**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="523c6-298">Введите **пароль администратора** и **подтвердите его**.</span><span class="sxs-lookup"><span data-stu-id="523c6-298">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="523c6-299">Убедитесь, что выбран параметр `create as container database`.</span><span class="sxs-lookup"><span data-stu-id="523c6-299">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="523c6-300">Введите значение `pluggable database name`.</span><span class="sxs-lookup"><span data-stu-id="523c6-300">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="523c6-301">На hello **Сводка** страницы, просмотрите выбранные параметры и нажмите кнопку `Finish` базы данных toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-301">On hello **Summary** page, review your selected settings, and then click `Finish` toocreate hello database.</span></span>

   ![Снимок экрана: hello страница «Сводка»](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="523c6-303">Hello базы данных был создан.</span><span class="sxs-lookup"><span data-stu-id="523c6-303">hello Database has been created.</span></span> <span data-ttu-id="523c6-304">На hello **Готово** предусмотрена hello параметр toouse toounlock дополнительные учетные записи этой базы данных и изменения паролей hello.</span><span class="sxs-lookup"><span data-stu-id="523c6-304">On hello **Finish** page, you have hello option toounlock additional accounts toouse this database and change hello passwords.</span></span> <span data-ttu-id="523c6-305">Toodo так, выберите **управления паролями** -в противном случае щелкните `close`.</span><span class="sxs-lookup"><span data-stu-id="523c6-305">If you wish toodo so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="523c6-306">Удалить hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="523c6-306">Delete hello VM</span></span>

<span data-ttu-id="523c6-307">Автоматическое управление хранилищем для Oracle успешно настроена на изображении hello база данных Oracle из hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="523c6-307">You have successfully configured Oracle Automated Storage Management on hello Oracle DB image from hello Azure Marketplace.</span></span>  <span data-ttu-id="523c6-308">Если вам больше не требуется этой виртуальной Машины, можно использовать hello следующая команда tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="523c6-308">When you no longer need this VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="523c6-309">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="523c6-309">Next steps</span></span>

[<span data-ttu-id="523c6-310">Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="523c6-310">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="523c6-311">Реализация Oracle Golden Gate на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="523c6-311">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="523c6-312">Ознакомьтесь со статьей [Разработка базы данных Oracle и ее внедрение в Azure](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="523c6-312">Review [Architect an Oracle DB](oracle-design.md)</span></span>
