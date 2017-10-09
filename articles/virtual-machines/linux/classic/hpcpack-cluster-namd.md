---
title: "aaaNAMD с пакетом Microsoft HPC на виртуальных машинах Linux | Документы Microsoft"
description: "Развертывание кластера пакета Microsoft HPC в Azure и запуск моделирования NAMD с использованием charmrun на нескольких вычислительных узлах Linux."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a>Запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure
В этой статье показано одним из способов toorun Linux высокопроизводительных вычислительных систем (HPC) рабочей нагрузки на виртуальных машинах Azure. Здесь, настроить [пакета Microsoft HPC](https://technet.microsoft.com/library/cc514029) кластер в Azure с Linux вычислительных узлов и запустите [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate моделирование и визуализировать структуру hello больших biomolecular системы.  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* **NAMD** (для программы Nanoscale молекулярные Dynamics) — параллельных молекулярные dynamics пакет, предназначенный для высокопроизводительных моделирования больших biomolecular систем, содержащий копии toomillions из атомами. К этим системам относятся вирусы, клеточные структуры и большие белки. NAMD масштабирует toohundreds ядер для типичных моделирования и toomore более 500 000 ядер для имитации наибольшее hello.
* **Пакет Microsoft HPC** предоставляет возможности toorun крупномасштабных HPC и параллельных приложений в кластерах с локальных компьютеров или виртуальных машинах Azure. Изначально предназначенный для рабочих нагрузок HPC, пакет HPC теперь поддерживает приложения HPC для Linux на виртуальных машинах вычислительного узла Linux, развернутых в кластере пакета HPC. Общие сведения см. в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).

Для других параметров toorun Linux HPC рабочих нагрузок в Azure, в разделе [технические ресурсы для пакета и высокопроизводительных вычислительных систем](../../../batch/batch-hpc-solutions.md).

## <a name="prerequisites"></a>Предварительные требования
* **Кластер пакета HPC с вычислительными узлами Linux.** Разверните кластер пакета HPC с вычислительными узлами Linux в Azure, используя [шаблон Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) или [скрипт Azure PowerShell](hpcpack-cluster-powershell-script.md). В разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md) hello предварительные условия и действия в любом случае. При выборе hello вариант развертывания сценария PowerShell см. Образец hello файла конфигурации в файлах образца hello в конце hello в этой статье. Этот файл позволяет настроить кластер пакета HPC на основе Azure, который состоит из головного узла Windows Server 2012 R2 и четырех вычислительных узлов большого размера под управлением CentOS 6.6. Измените этот файл в соответствии со своей средой.
* **Файлы программного обеспечения и учебник NAMD** -NAMD загрузить программное обеспечение для Linux из hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) сайта (требуется регистрация). В этой статье на основании NAMD версии 2.10 и использует hello [Linux-x86_64 (64-разрядных Intel и AMD с Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) архива. Кроме того, загрузить hello [файлы учебника NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd). Hello загружаемые файлы — это файлы в формате TAR, и требуется tooextract средство Windows hello файлов на головном узле кластера hello. файлы tooextract hello, следуйте инструкциям hello далее в этой статье. 
* **VMD** (необязательно) — toosee hello результаты задания NAMD, загрузите и установите программу молекулярные визуализации hello [VMD](http://www.ks.uiuc.edu/Research/vmd/) на компьютере по своему усмотрению. Текущая версия Hello — 1.9.2. В разделе hello VMD загрузки tooget сайт к работе.  

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Настройка взаимного доверия между вычислительными узлами
Запуск задания межузловых на нескольких узлах Linux требует hello узлы tootrust друг с другом (с **rsh** или **ssh**). При создании кластера HPC Pack hello с hello скрипт развертывания IaaS пакета HPC Microsoft hello сценарий автоматически настраивает постоянное взаимного доверия для учетной записи администратора hello, указываемые. Для пользователей без прав администратора, созданные в домене hello кластера имеют tooset копирование временной взаимного доверия между узлами hello при выделении toothem задания. Затем удалите связь hello после завершения задания hello. toodo это действие для каждого пользователя, укажите кластер toohello пару ключей RSA какие HPC пакет использует tooestablish hello доверительные отношения. Следуйте инструкциям ниже.

### <a name="generate-an-rsa-key-pair"></a>Создание пары ключей RSA
Легко toogenerate пару ключей RSA, который содержит открытый ключ и закрытый ключ, выполнив hello Linux **ssh-keygen** команды.

1. Войдите в систему tooa компьютера Linux.
2. Выполните следующую команду hello.
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > Нажмите клавишу **ввод** toouse параметры по умолчанию hello до завершения команды hello. Не вводите парольную фразу. При запросе пароля просто нажмите клавишу **ВВОД**.
   > 
   > 
   
   ![Создание пары ключей RSA][keygen]
3. Изменить каталог toohello ~/.ssh каталог. Hello закрытый ключ хранится в id_rsa и hello открытый ключ в id_rsa.pub.
   
   ![Открытые и закрытые ключи][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a>Добавление кластера HPC Pack toohello пары ключей hello
1. [Подключитесь с удаленного рабочего стола](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello головного узла виртуальной Машины с помощью учетных данных домена, указанный при развертывании кластера hello (например, hpc\clusteradmin) "hello". Управление hello кластера из головного узла hello.
2. Используйте стандартные toocreate процедуры Windows Server, учетную запись пользователя домена в домене Active Directory кластера hello. Например с помощью средства компьютеров и hello пользователя Active Directory на головном узле hello. Hello примеры в этой статье предполагается, что пользователь домена с именем hpcuser в домене hpclab hello (hpclab\hpcuser).
3. Добавление домена пользователя hello toohello-кластера HPC Pack в качестве пользователя кластера. Инструкции см. в статье [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx) (Добавление и удаление пользователей кластера).
4. Создайте файл с именем C:\cred.xml и скопируйте данные ключа hello RSA в него. Пример можно найти в hello файлы образцов в конце hello в этой статье.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. Откройте командную строку и введите следующую команду, tooset hello учетных данных данные для учетной записи hpclab\hpcuser hello hello. Использовать hello **extendeddata** toopass параметр hello имя hello C:\cred.xml файл, созданный для hello данных ключа.
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Эта команда успешно завершается без выходных данных. После установки hello учетные данные для учетных записей пользователей hello, необходимые toorun заданий, hello cred.xml файл хранится в безопасном месте или удалите его.
6. Если на одном из узлов Linux создан hello пару ключей RSA, помните ключи hello toodelete после завершения работы с ними. Пакет HPC не устанавливает взаимное доверие, если обнаруживает существующий файл id_rsa или id_rsa.pub.

> [!IMPORTANT]
> Не рекомендуется запускать задания Linux как администратор кластера на общего кластера, поскольку задания, отправлен администратором выполняется под учетной записью root hello на узлах Linux hello. Задания, отправленный пользователем без прав администратора выполняется под локальной учетной записью пользователя Linux с точно такое же имя, как пользователь задания hello hello. В этом случае пакет HPC устанавливает взаимного доверия для этого пользователя Linux на всех узлах hello выделенной toohello задания. Можно настроить пользователя Linux hello вручную на узлах Linux hello перед выполнением задания hello или автоматически создает hello пользователя при отправке задания hello пакета HPC. Если пакет HPC создает пользователя hello, HPC Pack удаляет его после завершения задания hello. tooreduce угрозу безопасности, ключи, удаляются после завершения задания hello на узлах hello hello.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Настройка файлового ресурса для узлов Linux
Теперь настроить файловый ресурс SMB и подключить hello общей папки на все Linux узлы tooallow hello Linux узлы tooaccess NAMD файлы с общий путь. Ниже приведены шаги toomount общей папки на головном узле hello. Например CentOS 6.6 распределения, которые в настоящее время не поддерживают hello файловая служба Azure рекомендуется общую папку. Если на узлах Linux поддерживает Azure файловый ресурс, в разделе [как toouse хранилища Azure File с Linux](../../../storage/files/storage-how-to-use-files-linux.md). Дополнительные параметры использования файловых ресурсов с помощью пакета HPC описаны в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).

1. Создайте папку на головном узле hello и предоставить к нему tooEveryone, задав права чтения и записи. В этом примере \\ \\CentOS66HN\Namd — имя hello hello папки, где CentOS66HN — имя узла hello hello головного узла.
2. Создайте вложенную папку с именем namd2 в общей папке hello. В namd2 создайте вложенную папку namdsample.
3. Для извлечения файлов NAMD hello в папке hello используется версия Windows **tar** или другой программы Windows, работающая в формате TAR архивы. 
   
   * Извлеките архив tar NAMD hello слишком\\\\CentOS66HN\Namd\namd2.
   * Извлеките файлы учебника hello под \\ \\CentOS66HN\Namd\namd2\namdsample.
4. Откройте окно Windows PowerShell и выполните следующие команды toomount hello общую папку на узлах Linux hello hello.
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Hello первая команда создает папку с именем /namd2 на всех узлах в группе LinuxNodes hello. Вторая команда Hello подключает //CentOS66HN/Namd/namd2 hello общие папки на папку hello с dir_mode и file_mode too777 набор битов. Hello *username* и *пароль* в hello команды должны быть учетные данные пользователя на головном узле hello hello.

> [!NOTE]
> Hello "\`" символа в hello вторая команда является escape-символа для PowerShell. «\`, «hello», означает» (запятая) является частью команды hello.
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a>Создание скрипта Bash toorun NAMD задания
Задание NAMD должен *nodelist* в файле **charmrun** toodetermine hello количество узлов toouse при запуске NAMD процессов. С помощью Bash скрипта, создающий файл nodelist hello и запускает **charmrun** с этим файлом набору узлов. Затем отправьте задание NAMD в диспетчер кластера HPC, вызывающий этот сценарий.

В текстовом редакторе, по своему усмотрению, создайте сценарий Bash папки /namd2 hello hello NAMD программные файлы и назовите его hpccharmrun.sh. Для быстрого пробной версии, скопируйте сценарий hpccharmrun.sh пример hello, приведенный в конце hello в этой статье и перейти слишком[отправить задание NAMD](#submit-a-namd-job).

> [!TIP]
> Сохраните сценарий как текстовый файл, в котором для завершения строк используется нотация Linux (только LF, а не CR LF). Это гарантирует, что он работает правильно на узлах Linux hello.
> 
> 

Ниже приведены сведения о том, что делает этот сценарий Bash. 

1. Определите несколько переменных.
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. Получите сведения об узле из переменных среды hello. В переменной $NODESCORES хранится список разбиения слов из $CCP_NODES_CORES. $COUNT — размер hello $NODESCORES.
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   Hello для переменной CCP_NODES_CORES hello $ имеет следующий формат:
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   Эта переменная перечисляет hello общее число узлов, имена узлов и количество ядер на каждом узле, выделенных toohello задания. Например если задание hello должен 10 toorun ядер, значение hello $CCP_NODES_CORES похожа на:
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. Если переменная CCP_NODES_CORES $ hello не задано, запустите **charmrun** напрямую. (это должно происходить, только если сценарий запускается непосредственно на узлах Linux).
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. Или создайте файл nodelist для **charmrun**.
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. Запустите **charmrun** файлом nodelist hello, получить его состояние возврата и удалите файл nodelist hello в конце hello.
   
   ${CCP_NUMCPUS} является другой переменной среды, заданные головной узел пакета HPC hello. Он хранит номер hello общего количества ядер, выделенных toothis задания. Мы используем его toospecify hello число процессов для charmrun.
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. Выход с hello **charmrun** код возврата.
   
   ```
   exit ${RTNSTS}
   ```

Ниже приведен hello данные в файле nodelist hello, какой сценарий hello приводит к возникновению ошибки.

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

Например:

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a>Отправка задания NAMD
Теперь все готово toosubmit NAMD задания в диспетчере кластера HPC.

1. Подключение tooyour головного узла кластера и запуск диспетчера кластеров HPC.
2. В **управление ресурсами**, убедитесь, что hello Linux вычислительных узлов в hello **Online** состояния. Если это не так, выберите их и щелкните **Подключить**.
3. В разделе **Управление заданиями** щелкните **Новое задание**.
4. Введите для задания имя, например *hpccharmrun*.
   
   ![Новое задание HPC][namd_job]
5. На hello **сведений о задании** в разделе **ресурсы задания**, выберите тип ресурса в качестве hello **узел** и набор hello **минимум** too3. , запустим hello задания на трех узлах Linux, и каждый узел имеет четыре ядра.
   
   ![Ресурсы задания][job_resources]
6. Нажмите кнопку **изменение задач** в левой области навигации hello и нажмите кнопку **добавить** tooadd задание toohello задачи.    
7. На hello **сведения о задаче и перенаправление ввода-вывода** страница hello набор следующие значения:
   
   * **Командная строка** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`
     
     > [!TIP]
     > Hello предыдущей командной строке является единственной командой, без разрывов. Создает оболочку tooappear на несколько строк в группе **командной строки**.
     > 
     > 
   * **Рабочий каталог** — /namd2.
   * **Минимум** — 3.
     
     ![Сведения о задаче][task_details]
     
     > [!NOTE]
     > Заданные hello рабочий каталог из-за **charmrun** пытается toonavigate toohello же рабочий каталог на каждом узле. Если hello рабочий каталог не настроен, пакет HPC запускается команда hello в произвольным именем папки, созданной на одном из узлов Linux hello. В результате следующая ошибка на hello hello других узлов: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid эту проблему, укажите путь к папке, доступный на всех узлах как hello рабочий каталог.
     > 
     > 
8. Нажмите кнопку **ОК** и нажмите кнопку **отправить** toorun этого задания.
   
   По умолчанию пакет HPC отправляет задание hello в качестве учетной записи текущего вошедшего в систему пользователя. Диалоговое окно может попросить tooenter hello имя и пароль пользователя после нажатия кнопки **отправить**.
   
   ![Учетные данные для задания][creds]
   
   При некоторых условиях HPC Pack запоминает сведения о пользователе hello входных данных до и не показывать это окно. toomake HPC Pack снова отобразить его, введите следующую команду в командной строке hello и затем отправить задание hello.
   
   ```command
   hpccred delcreds
   ```
9. Задание Hello занимает несколько минут toofinish.
10. Поиск журнала задания hello в \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log и hello выходные файлы в \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.
11. При необходимости запустите VMD tooview результаты задания. Hello действия для визуализации hello NAMD выходных файлов (в данном случае молекула белок ubiquitin в сфере воды) выходят за рамки данной статьи hello. Дополнительные сведения см. в [руководстве по NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf).
    
    ![Результаты задания][vmd_view]

## <a name="sample-files"></a>Файлы с примерами
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Пример XML-файла конфигурации для развертывания кластера с помощью скрипта PowerShell
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a>Пример файла cred.xml
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```

### <a name="sample-hpccharmrunsh-script"></a>Пример сценария hpccharmrun.sh
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
