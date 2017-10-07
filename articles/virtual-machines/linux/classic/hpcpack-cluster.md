---
title: "aaaLinux вычислений виртуальных машин в кластере HPC Pack | Документы Microsoft"
description: "Узнайте, как toocreate используйте HPC Pack кластер в Azure для Linux высокопроизводительных вычислительных систем (HPC) рабочих нагрузок"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure
В этой статье описывается, как настроить в Azure [кластер пакета Microsoft HPC](https://technet.microsoft.com/library/cc514029.aspx), содержащий головной узел под управлением Windows Server и несколько вычислительных узлов под управлением поддерживаемого дистрибутива Linux. Просмотр данных toomove параметры среди узлов hello Linux и Windows hello головного узла кластера hello. Узнайте, как toosubmit Linux HPC заданий toohello кластера.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

На высоком уровне hello следующей диаграмме показан кластер HPC Pack hello создания и работы с.

![Кластер пакета HPC с узлами Linux][scenario]

Для других параметров toorun Linux HPC рабочих нагрузок в Azure, в разделе [технические ресурсы для пакета и высокопроизводительных вычислительных систем](../../../batch/big-compute-resources.md).

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a>Развертывание кластера пакета HPC с вычислительными узлами Linux
В этой статье показано два варианта toodeploy кластере HPC Pack в Azure с Linux вычислительных узлов. Оба метода используют образа Marketplace из Windows Server и головного узла HPC Pack toocreate hello. 

* **Шаблон диспетчера ресурсов Azure** -использовать шаблон из hello Azure Marketplace или шаблон начало работы от сообщества hello, создания tooautomate hello кластера в модели развертывания диспетчера ресурсов hello. Здравствуйте, например, [кластера HPC Pack для рабочих нагрузок Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) шаблона в hello Azure Marketplace создается полная инфраструктура кластера HPC Pack для Linux HPC рабочих нагрузок.
* **Сценарий PowerShell** -hello используйте [скрипт развертывания IaaS пакета Microsoft HPC](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate развертывания для завершения создания кластера в hello классической модели развертывания. Этот скрипт Azure PowerShell использует образ виртуальной Машины HPC Pack в hello Azure Marketplace для быстрого развертывания и предоставляет широкий набор параметров toodeploy конфигурации вычислительные узлы Linux.

Дополнительные сведения о вариантах развертывания кластера HPC Pack в Azure см. в разделе [параметры toocreate и управлять кластером высокопроизводительных вычислительных систем (HPC) в Azure с пакетом Microsoft HPC](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="prerequisites"></a>Предварительные требования
* **Подписка Azure** -подписки можно использовать в любом hello Azure Global или Azure China. Если ее нет, можно создать [бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.
* **Квота ядер** -может потребоваться tooincrease hello квоту ядер, особенно в том случае, если выбрать toodeploy несколько узлов кластера с несколькими ядрами размеры виртуальных Машин. tooincrease квоту, откройте запрос поддержки сети клиента бесплатно.
* **Дистрибутивы Linux** -в настоящее время HPC Pack поддерживает hello следующие дистрибутивы Linux для вычислительных узлов. Можно использовать версии этих дистрибутивов, доступные в Marketplace, или создать собственные.
  
  * **Выпуски на основе CentOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC
  * **Red Hat Enterprise Linux**: 6.7, 6.8, 7.2
  * **SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 для HPC, SLES 12 для HPC (Premium)
  * **Ubuntu Server**: 14.04 LTS, 16.04 LTS
    
    > [!TIP]
    > сети Azure RDMA hello toouse с помощью одного из размеров виртуальных Машин hello функцией RDMA, укажите образ SUSE Linux Enterprise Server 12 HPC или на основе CentOS HPC из hello Azure Marketplace. Дополнительные сведения см. в статье [Размеры виртуальных машин Linux, оптимизированных для HPC](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

Предварительные условия toodeploy hello кластера с помощью скрипта развертывания IaaS пакета HPC hello:

* **Клиентский компьютер** -необходим сценарий развертывания клиента на основе Windows компьютера toorun hello кластера.
* **Azure PowerShell** - [установите и настройте Azure PowerShell](/powershell/azure/overview) (версии 0.8.10 или более поздней) на клиентском компьютере.
* **Скрипт развертывания IaaS пакета HPC** — Загрузите и распакуйте hello последнюю версию скрипта hello из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=44949). Проверьте версию hello hello сценария, введя `.\New-HPCIaaSCluster.ps1 –Version`. Эта статья основана на версии 4.4.1 или более поздней hello сценария.

### <a name="deployment-option-1-use-a-resource-manager-template"></a>Вариант развертывания 1. Использование шаблона Resource Manager
1. Go toohello [кластера HPC Pack для рабочих нагрузок Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) шаблона в hello Azure Marketplace и нажмите кнопку **развернуть**.
2. В hello портал Azure просмотрите hello данные, а затем нажмите кнопку **создать**.
   
    ![Создание на портале][portal]
3. На hello **основы** колонки, введите имя кластера hello, который также имена hello ВМ головного узла. Можно выбрать существующую группу ресурсов или создать группу для развертывания hello в расположении, которое является доступной tooyou. Hello расположение влияет на доступность hello некоторые размеры виртуальной Машины и другим службам Azure (см. [продукты, доступные по регионам](https://azure.microsoft.com/regions/services/)).
4. На hello **головной узел параметры** колонке первого развертывания можно принять параметры по умолчанию hello. 
   
   > [!NOTE]
   > Hello **URL-адрес сценария после конфигурации** — необязательный параметр toospecify общедоступным сценарий Windows PowerShell, вы хотите toorun на ВМ головного узла hello после ее запуска. 
   > 
   > 
5. На hello **вычислить параметры узла** колонке выберите шаблон именования для узлов hello, hello число и размер узлов hello и hello toodeploy распространения Linux.
6. На hello **параметры инфраструктуры** колонки, введите имена для hello виртуальной сети и Active Directory домена, домена и учетные данные администратора виртуальной Машины и шаблон именования для учетных записей хранения hello.
   
   > [!NOTE]
   > Пакет HPC использует пользователей кластера tooauthenticate домена Active Directory hello. 
   > 
   > 
7. После запуска hello проверочные тесты и просмотрите hello условия использования, нажмите кнопку **покупки**.

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a>Вариант развертывания 2. Использование скрипта развертывания IaaS hello
Ниже перечислены предварительные условия toodeploy hello кластера с помощью скрипта развертывания IaaS пакета HPC hello:

* **Клиентский компьютер** -необходим сценарий развертывания клиента на основе Windows компьютера toorun hello кластера.
* **Azure PowerShell** - [установите и настройте Azure PowerShell](/powershell/azure/overview) (версии 0.8.10 или более поздней) на клиентском компьютере.
* **Скрипт развертывания IaaS пакета HPC** — Загрузите и распакуйте hello последнюю версию скрипта hello из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=44949). Проверьте версию hello hello сценария, введя `.\New-HPCIaaSCluster.ps1 –Version`. Эта статья основана на версии 4.4.1 или более поздней hello сценария.

**XML-файл конфигурации**

Hello скрипт развертывания IaaS пакета HPC использует в качестве кластера HPC hello toodescribe входного XML-файла конфигурации. Hello следующий образец файла конфигурации указывает небольшой кластере, состоящем из головного узла HPC Pack и два размер A7 CentOS 7.0 Linux вычислительных узлов. 

При необходимости для вашей среды и конфигурации кластера требуемой, измените файл hello и сохраните его с именем, например HPCDemoConfig.xml. Например необходимо toosupply имя своей подписки и имя учетной записи хранилища с уникальным и имя облачной службы. Кроме того может потребоваться, поддерживаемый toochoose другого образа Linux для hello вычислительных узлов. Дополнительные сведения об элементах hello в файле конфигурации hello см. в разделе файла Manual.rtf hello в папке скрипта hello и [создание кластера HPC с помощью скрипта развертывания IaaS пакета HPC hello](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

**hello toorun скрипт развертывания IaaS пакета HPC**

1. Откройте Windows PowerShell на клиентском компьютере hello с правами администратора.
2. Изменение каталога toohello папку, где hello сценария установки (E:\IaaSClusterScript в этом примере).
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. Запустите следующие кластера HPC Pack hello toodeploy команда hello. В этом примере предполагается, что этот файл конфигурации hello находится в E:\HPCDemoConfig.xml
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    а. Поскольку hello **AdminPassword** не указан в hello предшествующий команды, не запрошенные tooenter hello пароль для пользователя *MyAdminName*.
   
    b. затем скрипт Hello запускает файл конфигурации toovalidate hello. Он может занять tooseveral минут в зависимости от сетевого подключения hello.
   
    ![Проверка][validate]
   
    c. После проверки передачи, скрипт hello перечисляет toocreate ресурсы кластера hello. Введите *Y* toocontinue.
   
    ![Ресурсы][resources]
   
    d. Hello сценарий запускает кластера HPC Pack toodeploy hello и завершения конфигурации hello без дальнейшего действия вручную. Hello скрипт может занять несколько минут.
   
    ![Развернуть][deploy]
   
   > [!NOTE]
   > В этом примере hello скрипт создает файл журнала автоматически с момента hello **- файл журнала** параметр не указан. журналы Hello не записываются в режиме реального времени, но будут собраны в конце hello hello проверки и развертывания hello. При остановке процесса PowerShell hello во время выполнения скрипта hello некоторые журналы будут потеряны.
   > 
   > 

## <a name="connect-toohello-head-node"></a>Подключение toohello головного узла
После развертывания кластера HPC Pack hello в Azure, [подключитесь с удаленного рабочего стола](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello головного узла виртуальной Машины с помощью учетных данных домена, указанный при развертывании кластера hello "hello" (например, *hpc\\ clusteradmin*). Управление hello кластера из головного узла hello.

На головном узле hello запустите диспетчер кластеров HPC toocheck hello состояние кластера HPC Pack hello. Можно управлять и отслеживать Linux вычислительные узлы hello так же, как работать с Windows вычислительных узлов. Например, отобразятся узлы Linux hello, перечисленных в **управление ресурсами** (эти узлы развертываются с hello **LinuxNode** шаблона).

![Управление узлами][management]

Также отобразятся узлы Linux hello в hello **тепловой карты** представления.

![Тепловая карта][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a>Как toomove данных в кластере с узлами Linux
У вас есть несколько вариантов toomove данных узлах Linux, а Windows hello головного узла кластера hello. Ниже приведены три распространенных методов, более подробно в следующих разделах hello.

* **Файл Azure** -предоставляет файлы управляемых toostore данных общей папки SMB файла в хранилище Azure. Windows узлы и узлы Linux можно подключить Azure файловый ресурс как к диску или папке на hello же время, даже если они развернуты в разных виртуальных сетей.
* **Головной узел SMB совместно использовать** -подключение стандартных общую папку Windows hello головного узла на узлах Linux.
* **Сервер NFS головного узла** — предоставляет решение для обмена файлами для смешанной среды Windows и Linux.

### <a name="azure-file-storage"></a>Хранилище файлов Azure
Hello [файла Azure](https://azure.microsoft.com/services/storage/files/) служба предоставляет общие файловые ресурсы с помощью стандартного протокола SMB 2.1 hello. Виртуальные машины Azure и облачных служб можно совместно использовать данные файлов между компонентами приложения с помощью монтируемых хранилищ и локальных приложений можно обращаться из файла данных в общей папке hello API-Интерфейс хранилища файлов. 

Подробное описание шагов toocreate совместного использования файлов Azure, а затем подключите его на головном узле hello, см. [приступить к работе с хранилищем Windows Azure файл](../../../storage/files/storage-how-to-use-files-windows.md). в разделе toomount hello Azure общей папки на узлах Linux hello, [как toouse хранилища Azure File с Linux](../../../storage/files/storage-how-to-use-files-linux.md). tooset сохранение подключения в разделе [tooMicrosoft Persisting соединений файлов Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).

В следующем примере hello создайте Azure файловый ресурс в учетной записи хранения. toomount hello делиться на hello головного узла, откройте командную строку и введите следующие команды hello:

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

В этом примере allvhdsje — это имя учетной записи хранилища, storageaccountkey является ключ учетной записи хранилища и rdma — hello Azure имя общей папки. Hello Azure общей папки на головном узле hello подключается как Z:.

toomount hello Azure общей папки на узлах Linux, запустите **clusrun** на головном узле hello. **[ClusRun](https://technet.microsoft.com/library/cc947685.aspx)**  является полезным toocarry средство HPC Pack административные задачи на нескольких узлах. (См. также раздел [Clusrun для узлов Linux](#Clusrun-for-Linux-nodes) в этой статье.)

Откройте окно Windows PowerShell и введите следующие команды hello:

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

Hello первая команда создает папку с именем /rdma на всех узлах в группе LinuxNodes hello. Вторая команда Hello подключает hello allvhdsjw.file.core.windows.net/rdma общую папку файлов Azure на папку /rdma hello с dir и файл too777 набор битов режима. Вторая команда hello allvhdsje — это имя учетной записи хранилища и storageaccountkey является ключ учетной записи хранилища.

> [!NOTE]
> Hello "\`" символа в hello вторая команда является escape-символа для PowerShell. «\`, «означает, что hello»,» (запятая) является частью команды hello.
> 
> 

### <a name="head-node-share"></a>Общая папка головного узла
Кроме того подключите общей папки hello головного узла на узлах Linux. Hello простейший способ tooshare файлов предоставляет общую папку, но hello головного узла и всех узлах Linux должны быть развернуты в hello одной виртуальной сети. Ниже приведены шаги, hello.

1. Создайте папку на головном узле hello и предоставить к нему tooEveryone с разрешениями чтения и записи. Например, общий ресурс D:\OpenFOAM на hello головного узла в качестве \\CentOS7RDMA HN\OpenFOAM. Здесь CentOS7RDMA HN — имя узла hello hello головного узла.
   
    ![Разрешения общих папок][fileshareperms]
   
    ![Общий доступ к файлам][filesharing]
2. Откройте окно Windows PowerShell и выполните следующие команды hello:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Hello первая команда создает папку с именем /openfoam на всех узлах в группе LinuxNodes hello. Вторая команда Hello подключает //CentOS7RDMA-HN/OpenFOAM hello общие папки на папку hello с dir и файл too777 набор битов режима. Hello имя пользователя и пароль в команде hello должно быть hello пользователя и пароль для пользователя кластера на головном узле hello. (См. раздел [Добавление и удаление пользователей кластера](https://technet.microsoft.com/library/ff919330.aspx).)

> [!NOTE]
> Hello "\`" символа в hello вторая команда является escape-символа для PowerShell. «\`, «означает, что hello»,» (запятая) является частью команды hello.
> 
> 

### <a name="nfs-server"></a>Сервер NFS
Hello службы для NFS позволяет tooshare и перенос файлов между компьютерами под управлением операционной системы Windows Server 2012 hello, с помощью протокола SMB hello и компьютеров под управлением Linux, с помощью протокола NFS hello. Hello NFS-сервер и все остальные узлы имеют toobe, развернутых в hello одной виртуальной сети. Он обеспечивает большую совместимость с узлами Linux, чем общая папка SMB. Например, он поддерживает ссылки на файлы.

1. tooinstall и настройке NFS-сервер, следуйте указаниям hello [сервера для системы сетевой общей папке первый-законченный](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).
   
    Например можно создайте с именем nfs и hello следующие свойства общего ресурса NFS:
   
    ![Авторизация NFS][nfsauth]
   
    ![Разрешения общих папок NFS][nfsshare]
   
    ![Разрешения NTFS NFS][nfsperm]
   
    ![Свойства управления NFS][nfsmanage]
2. Откройте окно Windows PowerShell и выполните следующие команды hello:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   Hello первая команда создает папку с именем /nfsshared на всех узлах в группе LinuxNodes hello. Hello вторая команда подключение hello NFS совместно использовать CentOS7RDMA HN: / nfs на hello папки. Здесь CentOS7RDMA HN: / nfs — hello удаленный путь общего ресурса NFS.

## <a name="how-toosubmit-jobs"></a>Как toosubmit заданий
Существует несколько способов кластера HPC Pack toohello toosubmit заданий:

* Пользовательский интерфейс диспетчера кластеров HPC или диспетчера заданий HPC
* Веб-портал HPC
* Интерфейс REST API

Задание отправки toohello кластера в Azure с помощью средства графического интерфейса пользователя пакета HPC и веб-портал HPC hello hello таким же как и для вычислительных узлов Windows. В разделе [диспетчера заданий HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) и [как toosubmit заданий на локальном компьютере клиента](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

задания toosubmit через REST API hello ссылаться слишком[Создание и отправка заданий с помощью hello REST API в пакете Microsoft HPC](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx). toosubmit задания из клиента Linux, также см. Образец hello Python toohello [пакет SDK HPC](https://www.microsoft.com/download/details.aspx?id=47756).

## <a name="clusrun-for-linux-nodes"></a>Clusrun для узлов Linux
Hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) средство может стать команд используется tooexecute на узлах Linux через командную строку или в диспетчере кластера HPC. Ниже приводится несколько простых примеров.

* Показать текущие имена пользователей на всех узлах в кластере hello.
  
    ```command
    clusrun whoami
    ```
* Установка hello **gdb** средства отладки с **yum** на всех узлах hello linuxnodes группировать и затем перезапустить узлы hello через 10 минут.
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* Создать сценарий оболочки, отображение каждого числа от 1 до 10 в течение одной секунды на каждом узле Linux в кластере hello, запустите его и Показать выходные данные от узлов hello немедленно.
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> Может потребоваться toouse некоторые escape-символы в **clusrun** команд. Как показано в следующем примере используется ^ в командной строке tooescape hello» > «символ.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* Попробуйте вертикальное масштабирование hello кластера tooa большим числом узлов, или под управлением Linux рабочей нагрузки в кластере hello. Пример см. в статье [Запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure](hpcpack-cluster-namd.md).
* Повторите кластер с [ВМ с поддержкой RDMA, большим объемом вычислений](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun рабочих нагрузок MPI. С примером можно ознакомиться в статье [Выполнение заданий OpenFoam в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC](hpcpack-cluster-openfoam.md).
* Если вы заинтересованы в работе с Linux узлов в кластере HPC Pack в локальной среде, см. раздел hello [TechNet рекомендации](https://technet.microsoft.com/library/mt595803.aspx).

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
