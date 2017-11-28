---
title: "Настройка Oracle ASM в виртуальной машине Linux в Azure | Документация Майкрософт"
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
ms.openlocfilehash: 117212a2e7e3da7c3e249798eec804a652e0ef58
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="36f37-103">Настройка Oracle ASM в виртуальной машине Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="36f37-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="36f37-104">Виртуальные машины Azure предоставляют полностью настраиваемую и гибкую вычислительную среду.</span><span class="sxs-lookup"><span data-stu-id="36f37-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="36f37-105">В этом руководстве описано развертывание базовой виртуальной машины Azure, а также установка и настройка Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="36f37-105">This tutorial covers basic Azure virtual machine deployment combined with the installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="36f37-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="36f37-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="36f37-107">Создание виртуальной машины базы данных Oracle и подключение к ней.</span><span class="sxs-lookup"><span data-stu-id="36f37-107">Create and connect to an Oracle Database VM</span></span>
> * <span data-ttu-id="36f37-108">Установка и настройка Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="36f37-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="36f37-109">Установка и настройка Oracle Grid Infrastructure.</span><span class="sxs-lookup"><span data-stu-id="36f37-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="36f37-110">Инициализация установки Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="36f37-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="36f37-111">Создание базы данных Oracle под управлением ASM.</span><span class="sxs-lookup"><span data-stu-id="36f37-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="36f37-112">Если вы решили установить и использовать интерфейс командной строки локально, то для работы с этим руководством вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="36f37-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="36f37-113">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="36f37-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="36f37-114">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="36f37-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-the-environment"></a><span data-ttu-id="36f37-115">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="36f37-115">Prepare the environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="36f37-116">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="36f37-116">Create a resource group</span></span>

<span data-ttu-id="36f37-117">Чтобы создать группу ресурсов, используйте команду [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="36f37-117">To create a resource group, use the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="36f37-118">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="36f37-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="36f37-119">В этом примере создается группа ресурсов с именем *myResourceGroup* в регионе *eastus*.</span><span class="sxs-lookup"><span data-stu-id="36f37-119">In this example, a resource group named *myResourceGroup* in the *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="36f37-120">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="36f37-120">Create a VM</span></span>

<span data-ttu-id="36f37-121">Чтобы создать виртуальную машину на основе образа базы данных Oracle и настроить ее для использования Oracle ASM, выполните команду [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="36f37-121">To create a virtual machine based on the Oracle Database image and configure it to use Oracle ASM, use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="36f37-122">В следующем примере создается виртуальная машина с именем myVM размера Standard_DS2_v2, к которой подключено четыре диска данных по 50 ГБ каждый.</span><span class="sxs-lookup"><span data-stu-id="36f37-122">The following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="36f37-123">Кроме того, создаются ключи SSH, если они не существуют в расположении ключей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="36f37-123">If they do not already exist in the default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="36f37-124">Чтобы использовать определенный набор ключей, используйте параметр `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="36f37-124">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="36f37-125">После создания виртуальной машины в Azure CLI отображается информация следующего вида.</span><span class="sxs-lookup"><span data-stu-id="36f37-125">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="36f37-126">Обратите внимание на значение `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="36f37-126">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="36f37-127">Этот адрес используется для доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="36f37-127">You use this address to access the VM.</span></span>

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

### <a name="connect-to-the-vm"></a><span data-ttu-id="36f37-128">Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="36f37-128">Connect to the VM</span></span>

<span data-ttu-id="36f37-129">Чтобы создать сеанс SSH с виртуальной машиной и настроить дополнительные параметры, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="36f37-129">To create an SSH session with the VM and configure additional settings, use the following command.</span></span> <span data-ttu-id="36f37-130">Замените IP-адрес общедоступным IP-адресом виртуальной машины (значение `publicIpAddress`).</span><span class="sxs-lookup"><span data-stu-id="36f37-130">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="36f37-131">Установка Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="36f37-131">Install Oracle ASM</span></span>

<span data-ttu-id="36f37-132">Чтобы установить ASM, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="36f37-132">To install Oracle ASM, complete the following steps.</span></span> 

<span data-ttu-id="36f37-133">Дополнительные сведения об установке Oracle ASM см. в статье [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html) (Скачиваемые компоненты Oracle ASMLib для Oracle Linux 6).</span><span class="sxs-lookup"><span data-stu-id="36f37-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="36f37-134">Необходимо войти в систему как привилегированный пользователь, чтобы продолжить установку ASM:</span><span class="sxs-lookup"><span data-stu-id="36f37-134">You need to login as root in order to continue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="36f37-135">Выполните эти дополнительные команды для установки компонентов Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="36f37-135">Run these additional commands to install Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="36f37-136">Убедитесь, что служба Oracle ASM установлена:</span><span class="sxs-lookup"><span data-stu-id="36f37-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="36f37-137">Выходные данные этой команды должны содержать следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="36f37-137">The output of this command should list the following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="36f37-138">Для правильной работы ASM требуется конкретный пользователь и роли.</span><span class="sxs-lookup"><span data-stu-id="36f37-138">ASM requires specific users and roles in order to function correctly.</span></span> <span data-ttu-id="36f37-139">Следующие команды создают необходимые учетные записи пользователей и группы:</span><span class="sxs-lookup"><span data-stu-id="36f37-139">The following commands create the pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="36f37-140">Убедитесь, что пользователи и группы созданы правильно:</span><span class="sxs-lookup"><span data-stu-id="36f37-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="36f37-141">Выходные данные этой команды должны содержать следующих пользователей и группы:</span><span class="sxs-lookup"><span data-stu-id="36f37-141">The output of this command should list the following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="36f37-142">Создайте папку для пользователя *grid* и смените владельца:</span><span class="sxs-lookup"><span data-stu-id="36f37-142">Create a folder for user *grid* and change the owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="36f37-143">Настройка Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="36f37-143">Set up Oracle ASM</span></span>

<span data-ttu-id="36f37-144">В этом руководстве пользователем по умолчанию является *grid*, а группой по умолчанию — *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="36f37-144">For this tutorial, the default user is *grid* and the default group is *asmadmin*.</span></span> <span data-ttu-id="36f37-145">Убедитесь, что пользователь *oracle* входит в группу asmadmin.</span><span class="sxs-lookup"><span data-stu-id="36f37-145">Ensure that the *oracle* user is part of the asmadmin group.</span></span> <span data-ttu-id="36f37-146">Чтобы настроить установку Oracle ASM, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="36f37-146">To set up your Oracle ASM installation, complete the following steps:</span></span>

1. <span data-ttu-id="36f37-147">При настройке драйвера библиотеки Oracle ASM нужно определить пользователя (grid) и группу по умолчанию (asmadmin), настроить запуск и сканирование дисков во время запуска (выберите y).</span><span class="sxs-lookup"><span data-stu-id="36f37-147">Setting up the Oracle ASM library driver involves defining the default user (grid) and default group (asmadmin) as well as configuring the drive to start on boot (choose y) and to scan for disks on boot (choose y).</span></span> <span data-ttu-id="36f37-148">Необходимо указать сведения в ответ на запросы, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="36f37-148">You need to answer the prompts from the following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="36f37-149">Выходные данные этой команды должны выглядеть следующим образом (указывать сведения в ответ на запросы больше не потребуется).</span><span class="sxs-lookup"><span data-stu-id="36f37-149">The output of this command should look similar to the following, stopping with prompts to be answered.</span></span>

    ```bash
   Configuring the Oracle ASM library driver.

   This will configure the on-boot properties of the Oracle ASM library
   driver. The following questions will determine whether the driver is
   loaded on boot and what permissions it will have. The current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user to own the driver interface []: grid
   Default group to own the driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="36f37-150">Просмотрите конфигурацию диска:</span><span class="sxs-lookup"><span data-stu-id="36f37-150">View the disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="36f37-151">Результат этой команды должен выглядеть примерно как перечисление доступных дисков:</span><span class="sxs-lookup"><span data-stu-id="36f37-151">The output of this command should look similar to the following listing of available disks</span></span>

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

3. <span data-ttu-id="36f37-152">Отформатируйте диск */dev/sdc*, выполнив следующую команду и указав следующие сведения в ответ на запрос:</span><span class="sxs-lookup"><span data-stu-id="36f37-152">Format disk */dev/sdc* by running the following command and answering the prompts with:</span></span>
   - <span data-ttu-id="36f37-153">*n* — новый раздел;</span><span class="sxs-lookup"><span data-stu-id="36f37-153">*n* for new partition</span></span>
   - <span data-ttu-id="36f37-154">*p* — основной раздел;</span><span class="sxs-lookup"><span data-stu-id="36f37-154">*p* for primary partition</span></span>
   - <span data-ttu-id="36f37-155">*1*— выбор первого раздела;</span><span class="sxs-lookup"><span data-stu-id="36f37-155">*1* to select the first partition</span></span>
   - <span data-ttu-id="36f37-156">нажмите клавишу `enter` для выбора первого цилиндра по умолчанию;</span><span class="sxs-lookup"><span data-stu-id="36f37-156">press `enter` for the default first cylinder</span></span>
   - <span data-ttu-id="36f37-157">нажмите клавишу `enter` для выбора последнего цилиндра по умолчанию;</span><span class="sxs-lookup"><span data-stu-id="36f37-157">press `enter` for the default last cylinder</span></span>
   - <span data-ttu-id="36f37-158">нажмите клавишу *w* для записи изменений в таблицу разделов.</span><span class="sxs-lookup"><span data-stu-id="36f37-158">press *w* to write the changes to the partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="36f37-159">В соответствии с указанными выше сведениями выходные данные команды fdisk должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36f37-159">Using the answers provided above, the output for the fdisk command should look like the following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide to write them.
   After that, of course, the previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   The device presents a logical sector size that is smaller than
   the physical sector size. Aligning to a physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off the mode (command 'c') and change display units to
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
   The partition table has been altered!

   Calling ioctl() to re-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="36f37-160">Повторите предыдущую команду fdisk для `/dev/sdd`, `/dev/sde` и `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="36f37-160">Repeat the preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="36f37-161">Проверьте конфигурацию диска:</span><span class="sxs-lookup"><span data-stu-id="36f37-161">Check the disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="36f37-162">Выходные данные команды должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36f37-162">The output of the command should look like the following:</span></span>

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

6. <span data-ttu-id="36f37-163">Проверьте состояние службы Oracle ASM и запустите ее:</span><span class="sxs-lookup"><span data-stu-id="36f37-163">Check the Oracle ASM service status and start the Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="36f37-164">Выходные данные команды должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36f37-164">The output of the command should look like the following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing the Oracle ASMLib driver:                     [  OK  ]
   Scanning the system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="36f37-165">Создайте диски Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="36f37-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="36f37-166">Выходные данные команды должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36f37-166">The output of the command should look like the following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="36f37-167">Выведите список дисков Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="36f37-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="36f37-168">Выходные данные команды должны содержать следующие диски Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="36f37-168">The output of the command should list off the following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="36f37-169">Измените пароли для пользователей root, oracle и grid.</span><span class="sxs-lookup"><span data-stu-id="36f37-169">Change the passwords for the root, oracle, and grid users.</span></span> <span data-ttu-id="36f37-170">**Запишите эти новые пароли**, так как они пригодятся во время установки позже.</span><span class="sxs-lookup"><span data-stu-id="36f37-170">**Make note of these new passwords** as you are using them later during the installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="36f37-171">Измените разрешение папки:</span><span class="sxs-lookup"><span data-stu-id="36f37-171">Change the folder permission:</span></span>

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

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="36f37-172">Скачивание и подготовка Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="36f37-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="36f37-173">Чтобы скачать и подготовить программное обеспечение Oracle Grid Infrastructure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="36f37-173">To download and prepare the Oracle Grid Infrastructure software, complete the following steps:</span></span>

1. <span data-ttu-id="36f37-174">Скачайте Oracle Grid Infrastructure со [страницы скачивания Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="36f37-174">Download Oracle Grid Infrastructure from the [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="36f37-175">Под заголовком **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) для Linux x86–64** должно быть два ZIP-файла для скачивания.</span><span class="sxs-lookup"><span data-stu-id="36f37-175">Under the download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download the two .zip files.</span></span>

2. <span data-ttu-id="36f37-176">Скачав ZIP-файлы на клиентском компьютере, вы можете скопировать файлы на виртуальную машину по протоколу SCP:</span><span class="sxs-lookup"><span data-stu-id="36f37-176">After you download the .zip files to your client computer, you can use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="36f37-177">Подключитесь к виртуальной машине Oracle в Azure по протоколу SSH, чтобы переместить ZIP-файлы в папку /opt.</span><span class="sxs-lookup"><span data-stu-id="36f37-177">SSH back into your Oracle VM in Azure in order to move the .zip files into the /opt folder.</span></span> <span data-ttu-id="36f37-178">Затем измените владельца файлов:</span><span class="sxs-lookup"><span data-stu-id="36f37-178">Then, change the owner of the files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="36f37-179">Распакуйте файлы.</span><span class="sxs-lookup"><span data-stu-id="36f37-179">Unzip the files.</span></span> <span data-ttu-id="36f37-180">(Установите инструмент Linux для распаковки, если он еще не установлен.)</span><span class="sxs-lookup"><span data-stu-id="36f37-180">(Install the Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="36f37-181">Измените разрешение:</span><span class="sxs-lookup"><span data-stu-id="36f37-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="36f37-182">Обновите настроенную область буфера.</span><span class="sxs-lookup"><span data-stu-id="36f37-182">Update configured swap space.</span></span> <span data-ttu-id="36f37-183">Для установки компонентов Oracle Grid требуется по крайней мере 6,8 ГБ области буфера.</span><span class="sxs-lookup"><span data-stu-id="36f37-183">Oracle Grid components need at least 6.8 GB of swap space to install Grid.</span></span> <span data-ttu-id="36f37-184">Размер файла подкачки по умолчанию для образов Oracle Linux в Azure всего 2048 МБ.</span><span class="sxs-lookup"><span data-stu-id="36f37-184">The default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="36f37-185">Вам нужно увеличить значение `ResourceDisk.SwapSizeMB` в файле `/etc/waagent.conf` и перезапустить службу WALinuxAgent, чтобы изменения вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="36f37-185">You need to increase `ResourceDisk.SwapSizeMB` in the `/etc/waagent.conf` file and restart the WALinuxAgent service in order for the updated settings to take effect.</span></span> <span data-ttu-id="36f37-186">Так как это файл только для чтения, необходимо изменить разрешения, чтобы включить доступ для записи.</span><span class="sxs-lookup"><span data-stu-id="36f37-186">Because it is a read-only file, you need to change file permissions to enable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="36f37-187">Найдите параметр `ResourceDisk.SwapSizeMB` и измените его значение на **8192**.</span><span class="sxs-lookup"><span data-stu-id="36f37-187">Search for `ResourceDisk.SwapSizeMB` and change the value to **8192**.</span></span> <span data-ttu-id="36f37-188">Необходимо будет нажать `insert`, чтобы перейти в режим вставки, ввести значение **8192** и нажать клавишу `esc` для возврата в режим команд.</span><span class="sxs-lookup"><span data-stu-id="36f37-188">You will need to press `insert` to enter insert mode, type in the value of **8192** and then press `esc` to return to command mode.</span></span> <span data-ttu-id="36f37-189">Чтобы записать изменения и закрыть файл, введите `:wq` и нажмите клавишу `enter`.</span><span class="sxs-lookup"><span data-stu-id="36f37-189">To write the changes and quit the file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="36f37-190">Для достижения оптимальной производительности и настройки области буфера мы настоятельно рекомендуем использовать `WALinuxAgent`, чтобы он всегда создавался на локальном временном диске.</span><span class="sxs-lookup"><span data-stu-id="36f37-190">We highly recommend that you always use `WALinuxAgent` to configure swap space so that it's always created on the local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="36f37-191">Дополнительные сведения см. в статье [How to add a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines) (Как добавить файл подкачки на виртуальной машине Linux Azure).</span><span class="sxs-lookup"><span data-stu-id="36f37-191">For more information on, see [How to add a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-to-run-x11"></a><span data-ttu-id="36f37-192">Подготовка локального клиента и виртуальной машины для запуска x11</span><span class="sxs-lookup"><span data-stu-id="36f37-192">Prepare your local client and VM to run x11</span></span>
<span data-ttu-id="36f37-193">Для установки и настройки Oracle ASM требуется графический интерфейс.</span><span class="sxs-lookup"><span data-stu-id="36f37-193">Configuring Oracle ASM requires a graphical interface to complete the install and configuration.</span></span> <span data-ttu-id="36f37-194">Для упрощения установки мы используем протокол x11.</span><span class="sxs-lookup"><span data-stu-id="36f37-194">We are using the x11 protocol to facilitate this installation.</span></span> <span data-ttu-id="36f37-195">Если вы используете клиентскую систему (Mac или Linux) с возможностями X11, вы можете пропустить эту установку и настройку, предназначенную для компьютеров с Windows.</span><span class="sxs-lookup"><span data-stu-id="36f37-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive to Windows machines.</span></span> 

1. <span data-ttu-id="36f37-196">Скачайте [PuTTY](http://www.putty.org/) и [Xming](https://xming.en.softonic.com/) на компьютер с Windows.</span><span class="sxs-lookup"><span data-stu-id="36f37-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) to your Windows computer.</span></span> <span data-ttu-id="36f37-197">Прежде чем продолжить, необходимо будет установить оба приложения со значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="36f37-197">You will need to complete the installation of both of these applications with the default values before proceeding.</span></span>

2. <span data-ttu-id="36f37-198">После установки PuTTY откройте командную строку, перейдите в папку PuTTY (например, C:\Program Files\PuTTY) и запустите файл `puttygen.exe` для создания ключа.</span><span class="sxs-lookup"><span data-stu-id="36f37-198">After you install PuTTY, open a command prompt, change into the PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order to generate a key.</span></span>

3. <span data-ttu-id="36f37-199">В генераторе ключей PuTTY сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="36f37-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="36f37-200">Чтобы создать ключ, нажмите кнопку `Generate`.</span><span class="sxs-lookup"><span data-stu-id="36f37-200">Generate a key by selecting the `Generate` button.</span></span>
   2. <span data-ttu-id="36f37-201">Скопируйте содержимое ключа (CTRL+C).</span><span class="sxs-lookup"><span data-stu-id="36f37-201">Copy the contents of the key (Ctrl+C).</span></span>
   3. <span data-ttu-id="36f37-202">Нажмите кнопку `Save private key`.</span><span class="sxs-lookup"><span data-stu-id="36f37-202">Select the `Save private key` button.</span></span>
   4. <span data-ttu-id="36f37-203">Пропустите предупреждение о защите ключа с помощью парольной фразы, а затем нажмите кнопку `OK`.</span><span class="sxs-lookup"><span data-stu-id="36f37-203">Ignore the warning about securing the key with a passphrase, and then select `OK`.</span></span>

   ![Снимок экрана генератора ключей PuTTY](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="36f37-205">В виртуальной машине выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="36f37-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="36f37-206">Создайте файл с именем `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="36f37-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="36f37-207">Вставьте содержимое ключа в этот файл и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="36f37-207">Paste the contents of the key in this file, and then save the file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="36f37-208">Ключ должен содержать строку `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="36f37-208">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="36f37-209">Кроме того, содержимое ключа должно быть одной строкой текста.</span><span class="sxs-lookup"><span data-stu-id="36f37-209">Also, the contents of the key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="36f37-210">В клиентской системе запустите PuTTY.</span><span class="sxs-lookup"><span data-stu-id="36f37-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="36f37-211">В области **Категория** выберите **Подключение** > **SSH** > **Проверка подлинности**.</span><span class="sxs-lookup"><span data-stu-id="36f37-211">In the **Category** pane, go to **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="36f37-212">В поле **Private key file for authentication** (Файл закрытого ключа для проверки подлинности) выберите созданный ранее ключ.</span><span class="sxs-lookup"><span data-stu-id="36f37-212">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

   ![Снимок экрана параметров аутентификации SSH](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="36f37-214">В области **Категория** выберите **Подключение** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="36f37-214">In the **Category** pane, go to **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="36f37-215">Установите флажок **Enable X11 forwarding** (Включить перенаправление X11).</span><span class="sxs-lookup"><span data-stu-id="36f37-215">Select the **Enable X11 forwarding** check box.</span></span>

   ![Снимок экрана параметров перенаправления X11 SSH](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="36f37-217">В области **Категория** выберите **Сеанс**.</span><span class="sxs-lookup"><span data-stu-id="36f37-217">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="36f37-218">Введите значение `<publicIPaddress>` виртуальной машины Oracle ASM в диалоговом окне имени узла, укажите новое имя `Saved Session` и нажмите кнопку `Save`.</span><span class="sxs-lookup"><span data-stu-id="36f37-218">Enter your Oracle ASM VM `<publicIPaddress>` in the host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="36f37-219">После сохранения щелкните `open` для подключения к виртуальной машине Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="36f37-219">Once saved, click on `open` to connect to your Oracle ASM virtual machine.</span></span>  <span data-ttu-id="36f37-220">При первом подключении выводится предупреждение о том, что удаленная система не кэшируется в реестре.</span><span class="sxs-lookup"><span data-stu-id="36f37-220">The first time you connect you are warned  the remote system is not cached in your registry.</span></span> <span data-ttu-id="36f37-221">Щелкните `yes`, чтобы добавить ее и продолжить.</span><span class="sxs-lookup"><span data-stu-id="36f37-221">Click on `yes` to add it and continue.</span></span>

   ![Снимок экрана параметров сеанса PuTTY](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="36f37-223">Установка Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="36f37-223">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="36f37-224">Чтобы установить Oracle Grid Infrastructure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="36f37-224">To install Oracle Grid Infrastructure, complete the following steps:</span></span>

1. <span data-ttu-id="36f37-225">Выполните вход в качестве пользователя **grid**.</span><span class="sxs-lookup"><span data-stu-id="36f37-225">Sign in as **grid**.</span></span> <span data-ttu-id="36f37-226">Вы сможете войти, не вводя пароль.</span><span class="sxs-lookup"><span data-stu-id="36f37-226">(You should be able to sign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="36f37-227">Если вы используете Windows, перед установкой запустите Xming.</span><span class="sxs-lookup"><span data-stu-id="36f37-227">If you are running Windows, make sure you have started Xming before you begin the installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="36f37-228">Откроется установщик Oracle Grid Infrastructure 12c Release 1.</span><span class="sxs-lookup"><span data-stu-id="36f37-228">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="36f37-229">Запуск установщика может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="36f37-229">(It might take a few minutes for the  installer to start.)</span></span>

2. <span data-ttu-id="36f37-230">На странице **выбора варианта установки** выберите **Install and Configure Oracle Grid Infrastructure for a Standalone Server** (Установить и настроить Oracle Grid Infrastructure для автономного сервера).</span><span class="sxs-lookup"><span data-stu-id="36f37-230">On the **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Снимок экрана со страницей выбора варианта установки в установщике](./media/oracle-asm/install01.png)

3. <span data-ttu-id="36f37-232">На странице **выбора языка продукта** выберите **английский** или другой нужный язык.</span><span class="sxs-lookup"><span data-stu-id="36f37-232">On the **Select Product Languages** page, ensure **English** or the language that you want is selected.</span></span>  <span data-ttu-id="36f37-233">Щелкните `next`.</span><span class="sxs-lookup"><span data-stu-id="36f37-233">Click `next`.</span></span>

4. <span data-ttu-id="36f37-234">На странице **Create ASM Disk Group** (Создание группы дисков ASM) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="36f37-234">On the **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="36f37-235">Введите имя группы дисков.</span><span class="sxs-lookup"><span data-stu-id="36f37-235">Enter a name for the disk group.</span></span>
   - <span data-ttu-id="36f37-236">В разделе **Redundancy** (Избыточность) выберите **External** (Внешняя).</span><span class="sxs-lookup"><span data-stu-id="36f37-236">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="36f37-237">В списке **Allocation Unit Size** (Размер единицы распределения) выберите значение **4**.</span><span class="sxs-lookup"><span data-stu-id="36f37-237">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="36f37-238">В разделе **Add Disks** (Добавление дисков) выберите **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="36f37-238">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="36f37-239">Щелкните `next`.</span><span class="sxs-lookup"><span data-stu-id="36f37-239">Click `next`.</span></span>

5. <span data-ttu-id="36f37-240">На странице **указания пароля ASM** установите переключатель **Use same passwords for these accounts** (Использовать одинаковые пароли для этих учетных записей) и введите пароль.</span><span class="sxs-lookup"><span data-stu-id="36f37-240">On the **Specify ASM Password** page, select the **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Снимок экрана со страницей указания пароля ASM в установщике](./media/oracle-asm/install04.png)

6. <span data-ttu-id="36f37-242">На странице **указания параметров управления** предусмотрен параметр настройки EM Cloud Control.</span><span class="sxs-lookup"><span data-stu-id="36f37-242">On the **Specify Management Options** page, you have the option to configure EM Cloud Control.</span></span> <span data-ttu-id="36f37-243">Мы пропустим его. Щелкните `next`, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="36f37-243">We are skipping this option - click `next` to continue.</span></span> 

7. <span data-ttu-id="36f37-244">На странице **привилегированных групп ОС** используйте параметры по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="36f37-244">On the **Privileged Operating System Groups** page, use the default settings.</span></span> <span data-ttu-id="36f37-245">Щелкните `next`, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="36f37-245">Click `next` to continue.</span></span>

8. <span data-ttu-id="36f37-246">На странице **указания расположения установки** используйте параметры по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="36f37-246">On the **Specify Installation Location** page, use the default settings.</span></span> <span data-ttu-id="36f37-247">Щелкните `next`, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="36f37-247">Click `next` to continue.</span></span>

9. <span data-ttu-id="36f37-248">На странице **создания инвентаризации** смените каталог инвентаризации на `/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="36f37-248">On the **Create Inventory** page, change the Inventory Directory to `/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="36f37-249">Щелкните `next`, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="36f37-249">Click `next` to continue.</span></span>

   ![Снимок экрана со страницей создания инвентаризации в установщике](./media/oracle-asm/install08.png)

10. <span data-ttu-id="36f37-251">На странице **Root script execution configurationRoot script execution configuration** (Конфигурация выполнения корневого сценария) установите флажок **Automatically run configuration scripts** (Запускать сценарии настройки автоматически).</span><span class="sxs-lookup"><span data-stu-id="36f37-251">On the **Root script execution configuration** page, select the **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="36f37-252">Затем установите флажок **Use "root" user credential** (Использовать учетные данные привилегированного пользователя) и введите пароль привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="36f37-252">Then, select the **Use "root" user credential** option, and enter the root user password.</span></span>

    ![Снимок экрана со страницей настройки выполнения корневого сценария в установщике](./media/oracle-asm/install09.png)

11. <span data-ttu-id="36f37-254">На странице **выполнения предварительных проверок** установка завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="36f37-254">On the **Perform Prerequisite Checks** page, the current setup will fail with errors.</span></span> <span data-ttu-id="36f37-255">Это ожидаемое поведение.</span><span class="sxs-lookup"><span data-stu-id="36f37-255">This is an expected behavior.</span></span> <span data-ttu-id="36f37-256">Выберите `Fix & Check Again`.</span><span class="sxs-lookup"><span data-stu-id="36f37-256">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="36f37-257">В диалоговом окне **Fixup Script** (Сценарий исправления) нажмите кнопку `OK`.</span><span class="sxs-lookup"><span data-stu-id="36f37-257">In the **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="36f37-258">На странице **Сводка** просмотрите выбранные параметры и нажмите кнопку `Install`.</span><span class="sxs-lookup"><span data-stu-id="36f37-258">On the **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Снимок экрана со страницей сводки в установщике](./media/oracle-asm/install12.png)

14. <span data-ttu-id="36f37-260">Появится диалоговое окно с предупреждением о том, что сценарии настройки может выполнять только привилегированный пользователь.</span><span class="sxs-lookup"><span data-stu-id="36f37-260">A warning dialog box appears informing you configuration scripts need to be run as a privileged user.</span></span> <span data-ttu-id="36f37-261">Щелкните `Yes`, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="36f37-261">Click `Yes` to continue.</span></span>

15. <span data-ttu-id="36f37-262">На странице **завершения** нажмите кнопку `Close` для завершения установки.</span><span class="sxs-lookup"><span data-stu-id="36f37-262">On the **Finish** page, click `Close` to finish the installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="36f37-263">Настройка установки Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="36f37-263">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="36f37-264">Чтобы настроить установку Oracle ASM, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="36f37-264">To set up your Oracle ASM installation, complete the following steps:</span></span>

1. <span data-ttu-id="36f37-265">Убедитесь, что в сеансе X11 по-прежнему используется пользователь **grid**.</span><span class="sxs-lookup"><span data-stu-id="36f37-265">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="36f37-266">Может потребоваться нажать кнопку `enter`, чтобы восстановить работу терминала.</span><span class="sxs-lookup"><span data-stu-id="36f37-266">You might need to hit `enter` to revive the terminal.</span></span> <span data-ttu-id="36f37-267">Затем запустите помощник по настройке Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="36f37-267">Then launch the Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="36f37-268">Откроется Oracle ASM Configuration Assistant.</span><span class="sxs-lookup"><span data-stu-id="36f37-268">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="36f37-269">В диалоговом окне **Configure ASM: Disk Groups** (Настройка ASM: группы дисков) нажмите кнопку `Create` и `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="36f37-269">In the **Configure ASM: Disk Groups** dialog box, click the `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="36f37-270">В диалоговом окне **Create Disk Group** (Создание группы дисков) выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="36f37-270">In the **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="36f37-271">Введите имя группы дисков **DATA**.</span><span class="sxs-lookup"><span data-stu-id="36f37-271">Enter the disk group name **DATA**.</span></span>
   - <span data-ttu-id="36f37-272">В разделе **Select Member Disks** (Выбор дисков-участников) выберите **ORCL_DATA** и **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="36f37-272">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="36f37-273">В списке **Allocation Unit Size** (Размер единицы распределения) выберите значение **4**.</span><span class="sxs-lookup"><span data-stu-id="36f37-273">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="36f37-274">Щелкните `ok` для создания группы дисков.</span><span class="sxs-lookup"><span data-stu-id="36f37-274">Click `ok` to create the disk group.</span></span>
   - <span data-ttu-id="36f37-275">Щелкните `ok`, чтобы закрыть окно подтверждения.</span><span class="sxs-lookup"><span data-stu-id="36f37-275">Click `ok` to close the confirmation window.</span></span>

   ![Снимок экрана с диалоговым окном "Create Disk Group" (Создание группы дисков)](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="36f37-277">В диалоговом окне **Configure ASM: Disk Groups** (Настройка ASM: группы дисков) нажмите кнопку `Create` и `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="36f37-277">In the **Configure ASM: Disk Groups** dialog box, click the `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="36f37-278">В диалоговом окне **Create Disk Group** (Создание группы дисков) выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="36f37-278">In the **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="36f37-279">Введите имя группы дисков **FRA**.</span><span class="sxs-lookup"><span data-stu-id="36f37-279">Enter the disk group name **FRA**.</span></span>
   - <span data-ttu-id="36f37-280">В разделе **Redundancy** (Избыточность) выберите **External (none)** (Внешняя(нет)).</span><span class="sxs-lookup"><span data-stu-id="36f37-280">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="36f37-281">В разделе **Select Member Disks** (Выбор дисков-участников) выберите **ORCL_FRA**.</span><span class="sxs-lookup"><span data-stu-id="36f37-281">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="36f37-282">В списке **Allocation Unit Size** (Размер единицы распределения) выберите значение **4**.</span><span class="sxs-lookup"><span data-stu-id="36f37-282">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="36f37-283">Щелкните `ok` для создания группы дисков.</span><span class="sxs-lookup"><span data-stu-id="36f37-283">Click `ok` to create the disk group.</span></span>
   - <span data-ttu-id="36f37-284">Щелкните `ok`, чтобы закрыть окно подтверждения.</span><span class="sxs-lookup"><span data-stu-id="36f37-284">Click `ok` to close the confirmation window.</span></span>

   ![Снимок экрана с диалоговым окном "Create Disk Group" (Создание группы дисков)](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="36f37-286">Нажмите кнопку **Выйти**, чтобы закрыть ASM Configuration Assistant.</span><span class="sxs-lookup"><span data-stu-id="36f37-286">Select **Exit** to close ASM Configuration Assistant.</span></span>

   ![Снимок экрана с диалоговым окном "Configure ASM: Disk Groups" (Настройка ASM: группы дисков) с кнопкой "Выйти"](./media/oracle-asm/asm05.png)

## <a name="create-the-database"></a><span data-ttu-id="36f37-288">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="36f37-288">Create the database</span></span>

<span data-ttu-id="36f37-289">Программное обеспечение базы данных Oracle уже установлено в образе Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="36f37-289">The Oracle database software is already installed on the Azure Marketplace image.</span></span> <span data-ttu-id="36f37-290">Чтобы создать базу данных, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="36f37-290">To create a database, complete the following steps:</span></span>

1. <span data-ttu-id="36f37-291">Переключитесь на суперпользователя Oracle и инициализируйте прослушиватель для ведения журнала:</span><span class="sxs-lookup"><span data-stu-id="36f37-291">Switch users to the Oracle superuser, and then initialize the listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="36f37-292">Откроется Database Configuration Assistant.</span><span class="sxs-lookup"><span data-stu-id="36f37-292">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="36f37-293">На странице **операций с базой данных** щелкните `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="36f37-293">On the **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="36f37-294">На странице **Creation Mode** (Режим создания) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="36f37-294">On the **Creation Mode** page:</span></span>

   - <span data-ttu-id="36f37-295">Введите имя для базы данных.</span><span class="sxs-lookup"><span data-stu-id="36f37-295">Enter a name for the database.</span></span>
   - <span data-ttu-id="36f37-296">Выберите **Automatic Storage Management (ASM)** в качестве **типа хранилища**.</span><span class="sxs-lookup"><span data-stu-id="36f37-296">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="36f37-297">В качестве **расположения файлов базы данных** используйте расположение ASM по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="36f37-297">For **Database Files Location**, use the default ASM suggested location.</span></span>
   - <span data-ttu-id="36f37-298">В качестве **области быстрого восстановления** используйте расположение ASM по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="36f37-298">For **Fast Recovery Area**, use the default ASM suggested location.</span></span>
   - <span data-ttu-id="36f37-299">Введите **пароль администратора** и **подтвердите его**.</span><span class="sxs-lookup"><span data-stu-id="36f37-299">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="36f37-300">Убедитесь, что выбран параметр `create as container database`.</span><span class="sxs-lookup"><span data-stu-id="36f37-300">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="36f37-301">Введите значение `pluggable database name`.</span><span class="sxs-lookup"><span data-stu-id="36f37-301">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="36f37-302">На странице **Сводка** просмотрите выбранные параметры и нажмите кнопку `Finish`, чтобы создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="36f37-302">On the **Summary** page, review your selected settings, and then click `Finish` to create the database.</span></span>

   ![Снимок экрана со страницей сводки](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="36f37-304">База данных создана.</span><span class="sxs-lookup"><span data-stu-id="36f37-304">The Database has been created.</span></span> <span data-ttu-id="36f37-305">На странице **завершения** вы можете разблокировать дополнительные учетные записи для использования этой базы данных и изменить пароли.</span><span class="sxs-lookup"><span data-stu-id="36f37-305">On the **Finish** page, you have the option to unlock additional accounts to use this database and change the passwords.</span></span> <span data-ttu-id="36f37-306">Для этого выберите параметр **управления паролями**. В противном случае щелкните `close`.</span><span class="sxs-lookup"><span data-stu-id="36f37-306">If you wish to do so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-the-vm"></a><span data-ttu-id="36f37-307">Удаление виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="36f37-307">Delete the VM</span></span>

<span data-ttu-id="36f37-308">Вы успешно настроили Oracle ASM на основе образа база данных Oracle из Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="36f37-308">You have successfully configured Oracle Automated Storage Management on the Oracle DB image from the Azure Marketplace.</span></span>  <span data-ttu-id="36f37-309">Вы можете удалить ставшие ненужными группу ресурсов, виртуальную машину и все связанные с ней ресурсы, использовав следующую команду:</span><span class="sxs-lookup"><span data-stu-id="36f37-309">When you no longer need this VM, you can use the following command to remove the resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="36f37-310">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36f37-310">Next steps</span></span>

[<span data-ttu-id="36f37-311">Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="36f37-311">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="36f37-312">Реализация Oracle Golden Gate на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="36f37-312">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="36f37-313">Ознакомьтесь со статьей [Разработка базы данных Oracle и ее внедрение в Azure](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="36f37-313">Review [Architect an Oracle DB](oracle-design.md)</span></span>
