---
title: "aaaSet копирование приложений MPI toorun кластера Linux RDMA | Документы Microsoft"
description: "Создать кластер размер toouse H16r, H16mr, A8 или A9 виртуальных машин Linux hello Azure RDMA сетевых toorun MPI приложениях"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a>Настройка приложений MPI Linux RDMA toorun кластера
Узнайте, как кластер tooset копирование Linux RDMA в Azure с помощью [высокопроизводительных вычислений размеры виртуальных Машин](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun параллельных приложений интерфейса передачи сообщений (MPI). Эта статья содержит действия tooprepare toorun образа Linux HPC Intel MPI в кластере. После подготовки развернуть кластер виртуальных машин с помощью этого образа и одну hello размеров ВМ с поддержкой RDMA Azure (в настоящее время H16r, H16mr, A8 или A9). Используйте hello кластера toorun приложений MPI, эффективно взаимодействуют через низкой задержкой, высокой пропускной способностью сети на основе удаленного прямого доступа к памяти (RDMA) технологии.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager](../../../resource-manager-deployment-model.md) и классическая модель. В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

## <a name="cluster-deployment-options"></a>Варианты развертывания кластера
Ниже перечислены методы, независимо от планировщика заданий можно использовать toocreate кластеров Linux RDMA.

* **Скрипты Azure CLI**: как показано далее в этой статье, использовать hello [интерфейс командной строки Azure](../../../cli-install-nodejs.md) (CLI) tooscript hello развертывания кластера виртуальных машин, имеющих функцию RDMA. Hello CLI в режиме управления службой создает hello узлов кластера последовательно в hello классической модели развертывания, поэтому развертывание много вычислительных узлов может занять несколько минут. hello tooenable сетевое соединение RDMA при использовании hello классической модели развертывания, развертывания виртуальных машин hello в hello же облачной службе.
* **Шаблоны Azure Resource Manager**: также можно использовать модель развертывания toodeploy кластер виртуальных машин, имеющих функцию RDMA, который подключается toohello сети RDMA для hello диспетчера ресурсов. Вы можете [создать собственный шаблон](../../../resource-group-authoring-templates.md), или проверьте hello [шаблоны Azure краткое руководство](https://azure.microsoft.com/documentation/templates/) для шаблонов, представленные Microsoft или hello сообщества toodeploy hello решения, нужно. Шаблоны диспетчера ресурсов можно предоставить toodeploy быстрый и надежный способ кластеров Linux. hello tooenable сетевое соединение RDMA при использовании модели развертывания диспетчера ресурсов hello, развертывание виртуальных машин hello в hello одной группе доступности.
* **Пакет HPC**: создайте кластер из пакета Microsoft HPC в Azure и добавить поддержку функции RDMA вычислительных узлов под управлением поддерживаемых к сети RDMA tooaccess распространения Linux hello. Дополнительную информацию см. в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).

## <a name="sample-deployment-steps-in-hello-classic-model"></a>Пример развертывания шагов в классической модели hello
Hello следующие шаги показывают, как настроить toouse hello Azure CLI toodeploy виртуальную Машину HPC SP1 SUSE Linux Enterprise Server (SLES) 12 hello Azure Marketplace и создать образ виртуальной Машины. Затем можно использовать hello tooscript изображения hello развертывания кластера виртуальных машин, имеющих функцию RDMA.

> [!TIP]
> Используйте аналогичные действия toodeploy кластера функцией RDMA виртуальных машин на основании изображений на основе CentOS HPC в hello Azure Marketplace. Некоторые шаги незначительно отличаются (мы указываем на это). 
>
>

### <a name="prerequisites"></a>Предварительные требования
* **Клиентский компьютер**: требуется toocommunicate компьютера Mac, Linux или Windows клиента с помощью Azure. Далее предполагается, что вы используете клиент Linux.
* **Подписка Azure**. Если у вас ее нет, можно за пару минут создать [бесплатную учетную запись](https://azure.microsoft.com/free/). Для больших кластеров можно использовать подписку с оплатой по мере использования или другие варианты приобретения.
* **Доступность размер виртуальной Машины**: hello следующие размеры экземпляра являются поддержкой RDMA: H16r, H16mr, A8 и A9. Проверьте [доступность продуктов по регионам](https://azure.microsoft.com/regions/services/) , чтобы узнать, в каких регионах Azure их можно использовать.
* **Квота ядер**: может потребоваться Квота hello tooincrease toodeploy ядра кластера виртуальных машин с большим объемом вычислений. Например менее 128 ядрами требуется, если требуется, чтобы ВМ A9 toodeploy 8, как показано в этой статье. Подписки также может ограничить hello количество ядер, развертываемого в определенных семейств размер виртуальной Машины, включая hello H-series. toorequest увеличить квоту, [откройте запрос поддержки сети клиента](../../../azure-supportability/how-to-create-azure-support-request.md) бесплатно.
* **Azure CLI**: [установить](../../../cli-install-nodejs.md) hello Azure CLI и [подключения tooyour подписки Azure](../../../xplat-cli-connect.md) hello клиентского компьютера.

### <a name="provision-an-sles-12-sp1-hpc-vm"></a>Подготовка виртуальной машины SLES 12 SP1 HPC
После входа в tooAzure с hello Azure CLI, запустите `azure config list` tooconfirm, hello выходных данных показан режим службы управления. Если нет, установите режим hello, запустив следующую команду:

    azure config mode asm


Введите следующие toolist hello все подписки hello вы являетесь авторизованным toouse:

    azure account list

Hello текущей активной подписки обозначена `Current` значение слишком`true`. Если эта подписка не hello тот, который toouse toocreate hello кластера, назначить идентификатор hello соответствующие подписки hello активной подписки:

    azure account set <subscription-Id>

общедоступные образы SLES 12 SP1 HPC в Azure, выполните такую команду hello следующие, при условии, что среда поддерживает ваш оболочки hello toosee **grep**:

    azure vm image list | grep "suse.*hpc"

Подготовить функцией RDMA ВМ с помощью образа SLES 12 SP1 HPC, выполнив команду hello следующим образом:

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

Описание

* Здравствуйте, размер (в данном примере — A9) является одним из размеров виртуальных Машин hello функцией RDMA.
* номер порта внешних SSH для Hello (22 в этом примере — hello SSH по умолчанию) — любой допустимый номер порта. Hello внутренний номер порта SSH устанавливается too22.
* Новой облачной службы создается в hello Azure область, задаваемую расположение hello. Укажите расположение, в какие hello виртуальной Машины доступен выбранного размера.
* Для поддержки назначения приоритета SUSE (что влечет за собой дополнительной оплаты) имя образа hello SLES 12 SP1 в настоящее время может принимать одно из этих двух вариантов: 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a>Настройка hello виртуальной Машины
По завершении подготовки виртуальной Машины hello toohello SSH виртуальной Машины с помощью hello внешний IP-адрес Виртуальной машины (или DNS-имя) и hello внешний порт настроен и настроить его. Дополнительные сведения о подключении, в разделе [как toolog на tooa виртуальной машине под управлением Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Выполните команды имени пользователя hello, настроенные на hello виртуальной Машины, если доступ к корню не требуется toocomplete шаг.

> [!IMPORTANT]
> Microsoft Azure не предоставляет доступ к корню tooLinux виртуальных машин. toogain административный доступ при подключении в качестве пользователя toohello виртуальной Машины, выполните команды с помощью `sudo`.
>
>

* **Обновления**. Установите обновления с помощью zypper. Можно использовать программы tooinstall NFS.

  > [!IMPORTANT]
  > В SP1 HPC SLES 12 ВМ рекомендуется не применять обновления ядра, которые могут вызвать проблемы с hello Linux RDMA драйверы.
  >
  >
* **Intel MPI**: завершить установку hello Intel MPI на hello SLES 12 SP1 HPC ВМ, выполнив следующую команду hello:

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* **Блокировать память**: для MPI коды toolock hello доступной памяти для RDMA, добавить или изменить следующие параметры в файле /etc/security/limits.conf hello hello. Требуется корневой доступ tooedit этот файл.

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > В целях тестирования можно также задать memlock toounlimited. Например, `<User or group name>    hard    memlock unlimited`. Дополнительные сведения см. в статье [Best Known Methods for Setting Locked Memory Size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size) (Рекомендуемые методы определения размера заблокированной памяти).
  >
  >
* **Ключи SSH для виртуальных машин SLES**: создание SSH ключи tooestablish доверия для вашей учетной записи пользователя между hello вычислительных узлов в кластере SLES hello, при выполнении заданий MPI. Если развернута виртуальная машина HPC на основе CentOS, не выполняйте этот шаг. См. инструкции далее в этой статье tooset passwordless доверительные SSH узлам кластера hello после записи образа hello и развертывания кластера hello.

    toocreate ключи SSH, запустите следующую команду hello. При появлении запроса для ввода выберите **ввод** ключей toogenerate hello в расположение по умолчанию hello без указания пароля.

        ssh-keygen

    Добавьте файл authorized_keys hello toohello открытого ключа для известных открытых ключей.

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    В каталоге ~/.ssh hello изменить или создать файл конфигурации hello. Укажите диапазон IP-адресов hello hello частной сети планировать toouse в Azure (10.32.0.0/16 в этом примере):

        host 10.32.0.*
        StrictHostKeyChecking no

    Кроме того список hello частной сети IP-адрес каждой виртуальной Машины в кластере следующим образом:

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > Настройка `StrictHostKeyChecking no` может создать потенциальную угрозу безопасности, если определенный IP-адрес или диапазон не задан.
  >
  >
* **Приложения**: установки приложений необходимо или выполнить другие пользовательские настройки до того как образ hello.

### <a name="capture-hello-image"></a>Записать образ hello
hello изображение toocapture, сначала необходимо запустить следующую команду на виртуальной Машине Linux hello hello. Эта команда deprovisions hello виртуальной Машины, но поддерживает учетные записи пользователей и ключи SSH, которые можно настроить.

```
sudo waagent -deprovision
```

С клиентского компьютера выполните следующие toocapture hello Azure CLI команды изображения hello. Дополнительные сведения см. в разделе [как toocapture классической виртуальной машины Linux как изображение](capture-image.md).  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

После выполнения этих команд образа виртуальной Машины hello для использования, а удаляется hello виртуальной Машины. Теперь у вас ваш пользовательский образ готов toodeploy кластера.

### <a name="deploy-a-cluster-with-hello-image"></a>Развертывание кластера с изображением hello
Измените следующий сценарий Bash с соответствующими значениями для вашей среды hello и запустите его с клиентского компьютера. Поскольку Azure развертывает ВМ hello последовательно в hello классической модели развертывания, он занимает несколько минут, toodeploy hello восемь ВМ A9, предлагаемые в этот сценарий.

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a>Рекомендации для кластера CentOS HPC
Tooset кластера на основе одного из изображений на основе CentOS HPC hello в hello Azure Marketplace вместо SLES 12 для HPC, выполните общие шаги hello в предшествующих раздел hello. Обратите внимание, hello при инициализации и настройки виртуальной Машины hello следующие различия:

- На виртуальной машине, подготовленной из образа на основе CentOS HPC, уже установлен интерфейс Intel MPI.
- Параметры памяти блокировки уже добавлены в файл /etc/security/limits.conf hello виртуальной Машины.
- Не создавайте ключи SSH на hello Подготовка виртуальной Машины для отслеживания. Вместо этого рекомендуется настроить проверку подлинности на основе пользователя после развертывания кластера hello. Дополнительные сведения см. в разделе hello в следующем разделе.  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a>Настройка passwordless доверия SSH в кластере hello
В кластере HPC на основе CentOS существует два метода для установления отношений доверия между вычислительными узлами hello: проверка подлинности на основе узла и проверку подлинности. Проверка подлинности на основе узла находится вне области hello данной статьи и обычно должны осуществляться через сценарий расширения во время развертывания. Проверку подлинности удобен для установления отношений доверия после развертывания и требует создания hello и совместное использование ключей SSH среди hello вычислительных узлов в кластере hello. Такой метод, называемый входом через SSH без пароля, необходим для выполнения заданий MPI.

Пример сценария, были получены из hello сообщества можно найти в [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) проверки подлинности пользователя легко tooenable в кластере HPC на основе CentOS. Загрузите и используйте этот скрипт с помощью hello следующие шаги. Кроме того, можно изменить этот скрипт или использовать любой другой метод tooestablish passwordless SSH проверки подлинности между hello кластерных вычислительных узлов.

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

сценарий toorun hello, необходима tooknow hello префикс подсети IP-адреса. Получите префикс hello, выполнив следующую команду на одном из узлов кластера hello hello. Ваш результат должен выглядеть примерно так 10.1.3.5 и часть hello 10.1.3 используется префикс hello.

    ifconfig eth0 | grep -w inet | awk '{print $2}'

Теперь запустите скрипт hello, используя три параметра: hello общее имя пользователя на hello вычислительных узлов, hello общий пароль для этого пользователя на hello вычислительных узлов и префикса подсети hello, который был возвращен из предыдущей команды hello.

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

Этот сценарий hello следующие:

* Создает каталог на hello узла с именем .ssh, который необходим для passwordless входа.
* Создает файл конфигурации в каталоге .ssh hello, который указывает, что имя входа tooallow passwordless входа из любого узла в кластере hello.
* Создает файлы, содержащие имена узлов hello и узла IP-адреса для всех узлов кластера hello hello. Эти файлы остаются после выполнения скрипта hello для дальнейшего использования.
* Создает пару закрытого и открытого ключа для каждого узла кластера (включая hello главного узла) и записи в файл authorized_keys hello.

> [!WARNING]
> Выполнение этого сценария может создать угрозу безопасности. Убедитесь, что hello сведения об открытом ключе в ~/.ssh не распространяется.
>
>

## <a name="configure-intel-mpi"></a>Настройка Intel MPI
toorun приложений MPI в Azure Linux RDMA, требуется tooconfigure конкретных tooIntel каталога переменные определенные среды MPI. Ниже приведен пример Bash сценария tooconfigure hello переменные, необходимые toorun приложения. Измените путь toompivars.sh hello для установки Intel MPI.

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

Hello hello узла файла имеет следующий формат. Добавьте одну строку для каждого узла в кластере. Укажите частные IP-адреса из виртуальной сети hello определенные ранее, не DNS-имена. Например для двух узлов с IP-адресами 10.32.0.1 и 10.32.0.2 hello файл содержит hello следующее:

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a>Запуск интерфейса MPI на базовом кластере с двумя узлами
Если это еще не сделано, настройте hello среды для Intel MPI.

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a>Выполнение команды MPI
Выполните команду MPI на одном из hello вычислительных узлов tooshow, MPI правильно установлен и может обмениваться данными между по крайней мере два вычислительных узлов. следующие Hello **mpirun** команда выполняет hello **hostname** команду на двух узлах.

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
Выходные данные должны быть перечислены hello имена всех узлов hello, переданные как входные данные для `-hosts`. Например **mpirun** команды с двумя узлами возвращает выходные данные hello следующим образом:

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a>Запуск теста производительности MPI
Следующая команда Intel MPI Hello выполняется pingpong тест tooverify hello конфигурации и подключения toohello RDMA сети кластера.

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

В работе кластера с двумя узлами вы увидите выходные данные hello следующим образом. В сети Azure RDMA hello ожидать задержки на уровне или ниже 3 микросекундах размеры сообщений вверх too512 байт.

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a>Дальнейшие действия
* Разверните и запустите приложения MPI в кластере Linux.
* В разделе hello [документация по библиотеке MPI Intel](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) рекомендации по Intel MPI.
* Повторите [шаблоном краткого руководства](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate Lustre Intel кластера с помощью образа на основе CentOS HPC. Дополнительные сведения см. в статье [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/) (Развертывание Intel Cloud Edition для Lustre в Microsoft Azure).
