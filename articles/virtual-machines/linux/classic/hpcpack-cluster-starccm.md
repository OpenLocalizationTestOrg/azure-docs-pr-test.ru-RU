---
title: "aaaRun ЗВЕЗДА-CCM + с пакетом HPC на виртуальных машинах Linux | Документы Microsoft"
description: "Развертывание кластера Microsoft HPC в Azure и запуск задания STAR-CCM+ на нескольких вычислительных узлах Linux в сети RDMA."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Выполнение заданий STAR-CCM+ в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC
В этой статье показано, как кластера toodeploy пакета Microsoft HPC в Azure и выполнения [ЗВЕЗДА приложения adapco CD-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) задания на нескольких вычислительных узлов Linux, которые связаны между собой с InfiniBand.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Пакет Microsoft HPC предоставляет возможности toorun разнообразные крупномасштабных HPC и параллельных приложений, включая приложения MPI, в кластерах из виртуальных машин Microsoft Azure. Пакет HPC также поддерживает приложения высокопроизводительных вычислений для Linux на виртуальных вычислительных узлах Linux, развернутых в кластере HPC. Введение toousing Linux вычислительных узлов с помощью пакета HPC, см. в разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md).

## <a name="set-up-an-hpc-pack-cluster"></a>Настройка кластера пакета HPC
Загрузите скрипты развертывания IaaS пакета HPC hello из hello [центра загрузки](https://www.microsoft.com/en-us/download/details.aspx?id=44949) и извлеките их локально.

В системе должен быть установлен компонент Azure PowerShell. Если PowerShell на локальном компьютере не настроен, прочтите статью hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

На момент написания этой статьи hello образы Linux hello из hello Azure Marketplace (который содержит драйверы hello InfiniBand в Azure) — для SLES 12, CentOS версии 6.5 и CentOS 7.1. Эта статья основана на использовании hello SLES 12. Имя hello tooretrieve все образы Linux, которые поддерживают HPC в hello Marketplace, выполните следующую команду PowerShell hello:

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

Результатом Hello список hello расположение, в котором эти изображения доступны и hello имя образа (**ImageName**) toobe, используемый в шаблон развертывания hello позже.

Перед развертыванием кластера hello toobuild имеется файл шаблона развертывания пакета HPC. Так как мы целевой кластер небольшой, hello головной узел будет hello контроллера домена и размещения локальной базы данных SQL.

Hello следующий шаблон будет развертывания головного узла, создайте XML-файл с именем **MyCluster.xml**и замените значения hello **SubscriptionId**, **StorageAccount**,  **Расположение**, **VMName**, и **ServiceName** с вашими.

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

Запустите Создание hello головной узел, выполнив команду PowerShell hello в командную строку с повышенными привилегиями:

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

Через 20 минут too30 hello головной узел должен быть готов. Tooit можно подключиться из hello портал Azure, щелкнув hello **Connect** значок hello виртуальной машины.

В конечном итоге возможно toofix hello DNS-сервер пересылки. toodo таким образом, запустите диспетчер DNS.

1. Имя сервера правой кнопкой мыши hello в диспетчере DNS, выберите **свойства**, а затем нажмите кнопку hello **серверов пересылки** вкладку.
2. Нажмите кнопку hello **изменить** tooremove серверы пересылки, а затем нажмите **ОК**.
3. Убедитесь в том, что hello **использовать корневые ссылки, если нет серверов пересылки доступны** флажок установлен и нажмите кнопку **ОК**.

## <a name="set-up-linux-compute-nodes"></a>Настройка вычислительных узлов Linux
Развертывание вычислительных узлов hello Linux с помощью hello того же шаблона развертывания, вы использовали toocreate hello головного узла.

Копирование файла hello **MyCluster.xml** из головного узла toohello локального компьютера, а также обновление hello **NodeCount** тег с hello число узлов, которое следует toodeploy (< = 20). Быть внимательны toohave достаточное количество доступных ядер Azure квоты, так как каждого экземпляра A9 будет занимать 16 ядер в подписке. Экземпляры A8 (8 ядер) можно использовать вместо A9, если требуется больше виртуальных машин в hello toouse же бюджет.

На головном узле hello скопируйте скрипты развертывания IaaS пакета HPC hello.

Выполните следующие команды Azure PowerShell в командную строку hello.

1. Запустите **Add-AzureAccount** tooconnect tooyour подписки Azure.
2. Если у вас несколько подписок, запустите **Get-AzureSubscription** toolist их.
3. Задать подписку по умолчанию, выполнив hello **xxxx Select-AzureSubscription - SubscriptionName-по умолчанию** команды.
4. Запустите **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart развертывание Linux вычислительных узлов.
   
   ![Развертывание головного узла][hndeploy]

Откройте средство диспетчера кластеров HPC Pack hello. Через несколько минут вычислительные узлы Linux станут периодически появляться в списке вычислительных узлов кластера. Режимом hello классического развертывания ВМ IaaS создаются последовательно. Поэтому если важно hello количество узлов, получение все развертывания может занять значительное время.

![Узлы Linux в диспетчере кластера пакета HPC][clustermanager]

Теперь, когда все узлы в кластере hello доступны и запущены, существуют параметры toomake дополнительную инфраструктуру.

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a>Настройка общей папки Azure для узлов Windows и Linux
Можно использовать скрипты toostore службы файлов Azure hello, пакеты приложений и файлов данных. Служба файлов Azure предоставляет возможности CIFS на базе хранилища BLOB-объектов Azure как постоянного хранилища. Имейте в виду, это не самым эффективным решением hello, но он hello один простой и не требует выделенных виртуальных машин.

Создать общий ресурс файла Azure в соответствии с инструкциями hello в статье hello [приступить к работе с хранилищем Windows Azure файл](../../../storage/files/storage-dotnet-how-to-use-files.md).

Оставьте hello имя вашей учетной записи хранилища, как **saname**, имя общей папки hello как **sharename**и ключ учетной записи хранения hello как **sakey**.

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a>Подключите hello Azure общей папки на головном узле hello
Откройте окно командной строки с повышенными привилегиями и выполните следующие команды toostore hello и учетные данные в хранилище локального компьютера hello hello:

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

Затем toomount hello Azure общую папку, запустите:

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a>Подключите hello Azure общей папки на вычислительных узлах Linux
Один полезным инструментом, который поставляется с пакетом HPC — средство clusrun hello. Это средство командной строки toorun hello, же команды можно использовать одновременно на нескольких вычислительных узлов. В нашем случае он использовал toomount hello Azure общую папку и ее сохранения toosurvive после перезагрузки.
В командную строку на головном узле hello выполните следующие команды hello.

каталог подключения hello toocreate:

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

toomount hello Azure общей папки:

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

общий ресурс подключения hello toopersist:

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a>Установка STAR-CCM+
Экземпляры виртуальной машины Azure A8 и A9 обеспечивают поддержку InfiniBand и возможности RDMA. драйверы ядра Hello, обеспечивающие эти возможности доступны для Windows Server 2012 R2, SUSE 12, CentOS версии 6.5 и CentOS 7.1 изображений в hello Azure Marketplace. Microsoft MPI и Intel MPI (выпуск 5.x) — это два MPI библиотеки hello, поддерживающие драйверы в Azure.

В состав пакета STAR-CCM+ CD-adapco (11.x и более поздней версии) входит библиотека Intel MPI версии 5.x, что обеспечивает поддержку InfiniBand для Azure.

Получить hello Linux64 ЗВЕЗДА-CCM + пакета из hello [приложения adapco компакт-диска портал](https://steve.cd-adapco.com). В нашем случае мы использовали версию 11.02.010 в режиме смешанной точности.

На головном узле hello в hello **/hpcdata** файла Azure совместного использования, создайте сценарий с именем **setupstarccm.sh** с hello после содержимого. Этот сценарий будет выполняться каждый tooset узел вычислений копирование ЗВЕЗДА-CCM + локально.

#### <a name="sample-setupstarcmsh-script"></a>Пример сценария setupstarcm.sh
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
Теперь tooset копирование ЗВЕЗДА-CCM + в вашей системе Linux вычислительных узлов, откройте командную строку с повышенными привилегиями и выполните hello следующую команду:

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

Пока выполняется команда hello, hello ЦП можно отслеживать с помощью hello тепловой карты диспетчера кластеров служб. Через несколько минут все узлы будут настроены должным образом.

## <a name="run-star-ccm-jobs"></a>Запуск заданий STAR-CCM+
Пакет HPC используется для его возможности планировщика заданий в порядке toorun ЗВЕЗДА-CCM + заданий. toodo таким образом, требуется hello поддержки несколько скриптов, используемых toostart hello задания и выполняемые ЗВЕЗДА-CCM +. Hello входных данных хранится на hello Azure общей папки, первый для простоты.

Следующий сценарий PowerShell Hello — используется tooqueue ЗВЕЗДЫ-CCM + задания. Он принимает три аргумента:

* Имя модели Hello
* число Hello используется toobe узлов
* Hello количество ядер на каждый узел, toobe используется

Поскольку ЗВЕЗДА-CCM + можно заполнить hello пропускной способности памяти, это обычно лучше toouse меньше ядра на вычислительные узлы и добавить новые узлы. Hello точное число ядер на узел будет зависеть от семейство процессоров hello и скорость взаимосвязь hello.

узлы Hello выделяются исключительно для задания hello и не может совместно использоваться другими заданиями. Hello задание не запускается как задание MPI напрямую. Hello **runstarccm.sh** запускает сценарий запуска MPI hello.

Hello входных данных модели и hello **runstarccm.sh** сценарий хранятся в hello **/hpcdata** общего ресурса, который был подключен ранее.

Файлы журналов именуются с ИД задания hello и хранятся в hello **/hpcdata папки**, вместе с hello ЗВЕЗДА-CCM + выходные файлы.

#### <a name="sample-submitstarccmjobps1-script"></a>Пример сценария SubmitStarccmJob.ps1
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
Замените **runner.java** предпочтительным средством запуска моделей Java и кодом ведения журнала STAR-CCM+.

#### <a name="sample-runstarccmsh-script"></a>Пример сценария runstarccm.sh
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

В рамках теста мы использовали маркер лицензии увеличения мощности по требованию. Для этого токена у вас есть tooset hello **$CDLMD_LICENSE_FILE** переменной среды слишком **1999@flex.cd-adapco.com**  и ключ hello в hello **- podkey** параметр hello командной строки .

После некоторых инициализации hello сценарий извлекает--из hello **$CCP_NODES_CORES** переменные среды, HPC Pack — hello список узлов toobuild использует hostfile, который hello запуска MPI. Этот hostfile будет содержать список имен узлов вычислений, используемые для задания hello, по одному имени на строку hello.

Формат Hello **$CCP_NODES_CORES** имеет следующую структуру:

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

Описание

* `<Number of nodes>`— количество узлов, выделенных toothis задания hello.
* `<Name of node_n_...>`— Имя каждого узла, выделенное задание toothis hello.
* `<Cores of node_n_...>`— hello количество ядер на узле hello выделенной toothis задания.

Здравствуйте, количество ядер (**$NBCORES**) — это также вычисляемый на основе hello количество узлов (**$NBNODES**) и hello количество ядер на узел (передается в качестве параметра **$NBCORESPERNODE**).

Для доступа к параметрам MPI hello, hello, которые используются с Intel MPI в Azure:

* `-mpi intel`toospecify Intel MPI.
* `-fabric UDAPL`команды toouse InfiniBand в Azure.
* `-cpubind bandwidth,v`пропускная способность toooptimize для MPI с ЗВЕЗДА-CCM +.
* `-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI работы с Azure InfiniBand и tooset hello необходимое количество ядер на узел.
* `-batch`toostart ЗВЕЗДА-CCM + в пакетном режиме без пользовательского интерфейса.

И, наконец toostart задания, убедитесь, что узлы доступны и запущены и находятся в оперативном режиме в диспетчере кластеров. В командной строке PowerShell выполните следующую команду:

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a>Остановка узлов
Позднее после завершения тестов, можно использовать следующие toostop команд HPC Pack PowerShell hello и запуска узлов:

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a>Дальнейшие действия
Попробуйте запустить другие рабочие нагрузки Linux. Например, ознакомьтесь со следующими статьями:

* [Запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure](hpcpack-cluster-namd.md)
* [Выполнение заданий OpenFoam в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
