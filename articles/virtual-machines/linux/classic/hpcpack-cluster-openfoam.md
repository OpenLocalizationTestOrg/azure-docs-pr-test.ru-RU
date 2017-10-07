---
title: "aaaRun OpenFOAM с пакетом HPC на виртуальных машинах Linux | Документы Microsoft"
description: "Развертывание кластера Microsoft HPC в Azure и запуск заданий OpenFOAM на нескольких вычислительных узлах Linux в сети RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Выполнение заданий OpenFoam в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC
В этой статье показывает один из способов toorun OpenFoam в виртуальных машинах Azure. Здесь мы развернем кластер пакета Microsoft HPC в Azure с использованием вычислительных узлов Linux и запустим задание [OpenFoam](http://openfoam.com/), используя библиотеку Intel MPI. Функцией RDMA виртуальных машинах Azure для hello вычислительных узлов, можно использовать, чтобы hello вычислительных узлов обмениваться данными по сети Azure RDMA hello. Другие параметры toorun, полностью включить OpenFoam в Azure настроен коммерческих образов, доступных в hello Marketplace, например UberCloud [OpenFoam 2.3 в CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)и запустив на [пакетной службы Azure](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/). 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

OpenFOAM (англ. Open Field Operation and Manipulation) — это пакет программного обеспечения с открытым исходным кодом для вычислительной гидродинамики (CFD). Он широко используется в технической и научной областях, а также в коммерческих и научных организациях. Пакет содержит средства для сеточного разбиения (например, snappyHexMesh), включает средство распараллеливания расчетов для сложных геометрических объектов, а также функции предварительной и последующей обработки. Почти все процессы выполняются параллельно, включение tootake потенциала пользователей оборудования компьютера в их распоряжении.  

Пакет Microsoft HPC предоставляет возможности toorun крупномасштабных HPC и параллельных приложений, включая приложения MPI, в кластерах из виртуальных машин Microsoft Azure. Пакет HPC также поддерживает приложения высокопроизводительных вычислений для Linux на виртуальных вычислительных узлах Linux, развернутых в кластере HPC. В разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md) для toousing введение Linux вычислительных узлов с помощью пакета HPC.

> [!NOTE]
> В этой статье показано, как toorun рабочей нагрузки Linux MPI с пакетом HPC. Здесь предполагается, что у вас есть опыт в администрировании Linux и выполнении рабочих нагрузок MPI на кластерах Linux. При использовании версии MPI и отличаются от тех, которые показаны в этой статье hello OpenFOAM возможно toomodify некоторые шаги установки и настройки. 
> 
> 

## <a name="prerequisites"></a>Предварительные требования
* **Кластер пакета HPC с вычислительными узлами Linux с поддержкой RDMA**. Разверните кластер пакета HPC с вычислительными узлами размером A8, A9, H16r или H16rm под управлением Linux, используя [шаблон Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) или [сценарий Azure PowerShell](hpcpack-cluster-powershell-script.md). В разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md) hello предварительные условия и действия в любом случае. При выборе hello вариант развертывания сценария PowerShell см. Образец hello файла конфигурации в файлах образца hello в конце hello в этой статье. Используйте этот кластер HPC Pack toodeploy основе Azure конфигурации, состоящий из головного узла размера A8 Windows Server 2012 R2 и 2 размер A8 SUSE Linux Enterprise Server 12 вычислительных узлов. Вместо используемых в файле имен подписки и службы подставьте свои значения. 
  
  **Дополнительные важные tooknow**
  
  * Предварительные требования к использованию вычислительных узлов Linux RDMA в Azure см. в статье [Размеры виртуальных машин, оптимизированных для высокопроизводительных вычислений](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  * При использовании варианта развертывания сценария Powershell hello развертывания все hello Linux вычислительных узлов в рамках одной облачной службы toouse hello RDMA сетевое подключение.
  * После развертывания узлов hello Linux, подключаться с SSH tooperform любые дополнительные задачи администрирования. Сведения о подключении hello SSH для каждой виртуальной Машины Linux можно найти в hello портал Azure.  
* **Intel MPI** -toorun OpenFOAM на SLES 12 HPC вычислительные узлы в Azure, необходимо, чтобы среда выполнения hello 5 библиотеки Intel MPI tooinstall из hello [сайта Intel.com](https://software.intel.com/en-us/intel-mpi-library/). (Среда выполнения Intel MPI 5 предустановлена в образах на основе CentOS для HPC.)  Позже установите Intel MPI на вычислительные узлы Linux, если это будет необходимо. tooprepare для выполнения этого шага после регистрации с Intel, по ссылке hello hello подтверждение по электронной почте toohello связанных веб-странице. Затем копия hello Загрузите ссылку для файла .tgz hello для hello соответствующую версию Intel MPI. В этой статье используется Intel MPI версии 5.0.3.048.
* **Источник пакета OpenFOAM** -загрузки программного обеспечения hello OpenFOAM источника пакета для Linux с hello [OpenFOAM Foundation сайта](http://openfoam.org/download/2-3-1-source/). В этой статье используется пакет версии 2.3.1, доступный для загрузки в виде файла OpenFOAM-2.3.1.tgz. Следуйте инструкциям hello далее в этой статье toounpack и скомпилируйте OpenFOAM на вычислительных узлах hello Linux.
* **EnSight** (необязательно) — результаты hello toosee вашей модели OpenFOAM, загрузите и установите hello [EnSight](https://www.ceisoftware.com/download/) визуализации и анализа программы. Сведения о лицензировании и загрузки, на сайте EnSight hello.

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Настройка взаимного доверия между вычислительными узлами
Запуск задания межузловых на нескольких узлах Linux требует hello узлы tootrust друг с другом (с **rsh** или **ssh**). При создании кластера HPC Pack hello с hello скрипт развертывания IaaS пакета HPC Microsoft hello сценарий автоматически настраивает постоянное взаимного доверия для учетной записи администратора hello, указываемые. Для пользователей без прав администратора, созданные в домене hello кластера имеют tooset копирование временной взаимного доверия между узлами hello выделяется toothem, и задания уничтожить hello связь после завершения задания hello. tooestablish доверия для каждого пользователя предоставляют кластер toohello пару ключей RSA, пакет HPC для отношения доверия hello.

### <a name="generate-an-rsa-key-pair"></a>Создание пары ключей RSA
Легко toogenerate пару ключей RSA, который содержит открытый ключ и закрытый ключ, выполнив hello Linux **ssh-keygen** команды.

1. Войдите в систему tooa компьютера Linux.
2. Выполните следующую команду hello.
   
   ```
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
1. Сделать удаленного рабочего стола подключения tooyour головной узел с вашей учетной записью администратора HPC Pack (hello администратора учетной записи, настроенной при запуске скрипта развертывания hello).
2. Используйте стандартные toocreate процедуры Windows Server, учетную запись пользователя домена в домене Active Directory кластера hello. Например с помощью средства компьютеров и hello пользователя Active Directory на головном узле hello. Hello примеры в этой статье предполагается, что пользователь домена с именем hpclab\hpcuser.
3. Создайте файл с именем C:\cred.xml и скопируйте данные ключа hello RSA в него. Образец файла cred.xml-конец hello в этой статье.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. Откройте командную строку и введите следующую команду, tooset hello учетных данных данные для учетной записи hpclab\hpcuser hello hello. Использовать hello **extendeddata** toopass параметр hello имя C:\cred.xml файл, созданный для hello данных ключа.
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Эта команда успешно завершается без выходных данных. После установки hello учетные данные для учетных записей пользователей hello, необходимые toorun заданий, hello cred.xml файл хранится в безопасном месте или удалите его.
5. Если на одном из узлов Linux создан hello пару ключей RSA, помните ключи hello toodelete после завершения работы с ними. Пакет HPC не устанавливает взаимное доверие, если обнаруживает файл id_rsa или id_rsa.pub.

> [!IMPORTANT]
> Не рекомендуется запускать задания Linux как администратор кластера на общего кластера, поскольку задания, отправлен администратором выполняется под учетной записью root hello на узлах Linux hello. Тем не менее задания, отправленный пользователем без прав администратора выполняется под локальной учетной записью пользователя Linux с точно такое же имя, как пользователь задания hello hello. В этом случае пакет HPC устанавливает взаимного доверия для этого пользователя Linux по узлам hello выделенной toohello задания. Можно настроить пользователя Linux hello вручную на узлах Linux hello перед выполнением задания hello или автоматически создает hello пользователя при отправке задания hello пакета HPC. Если пакет HPC создает пользователя hello, HPC Pack удаляет его после завершения задания hello. угрозы безопасности tooreduce, пакет HPC удаляет ключи hello после завершения задания.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Настройка файлового ресурса для узлов Linux
Теперь Настройка стандартных ресурсу SMB на папку на головном узле hello. tooallow hello Linux узлы tooaccess файлы приложения с общий путь подключения hello общей папки на узлах Linux hello. Вы можете также использовать другие параметры общего доступа, например общие файлы Azure (рекомендуется для большинства сценариев) или общие папки NFS. Совместное использование информации и подробное описание действий в файле hello [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md).

1. Создайте папку на головном узле hello и предоставить к нему tooEveryone, задав права чтения и записи. Например, общий ресурс C:\OpenFOAM на hello головного узла в качестве \\ \\SUSE12RDMA HN\OpenFOAM. Здесь *SUSE12RDMA HN* — имя узла hello hello головного узла.
2. Откройте окно Windows PowerShell и выполните следующие команды hello:
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

Hello первая команда создает папку с именем /openfoam на всех узлах в группе LinuxNodes hello. Вторая команда Hello подключает //SUSE12RDMA-HN/OpenFOAM hello общие папки на узлах Linux hello с dir_mode и file_mode too777 набор битов. Hello *username* и *пароль* в hello команды должны быть учетные данные пользователя на головном узле hello hello.

> [!NOTE]
> Hello "\`" символа в hello вторая команда является escape-символа для PowerShell. «\`, «hello», означает» (запятая) является частью команды hello.
> 
> 

## <a name="install-mpi-and-openfoam"></a>Установка пакетов MPI и OpenFOAM
toorun OpenFOAM как задание MPI hello сети RDMA требуется toocompile OpenFOAM с библиотеками Intel MPI hello. 

Во-первых, выполнения нескольких **clusrun** команды tooinstall библиотеки Intel MPI (если она еще не установлена), а также OpenFOAM на узлах Linux. Используйте hello головной узел папка ранее настраивается tooshare hello установочные файлы по узлам Linux hello.

> [!IMPORTANT]
> Приведенные действия по установке и компиляции являются примерами. Требуется знание tooensure администрирования системы Linux, правильность установки зависимых компиляторы и библиотеки. Может потребоваться toomodify определенные переменные среды или другие параметры для версий Intel MPI и OpenFOAM. Дополнительные сведения см. в разделах [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) (Руководство по установке библиотеки Intel MPI для Linux) и [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) (Установка исходного пакета OpenFOAM) для своей среды.
> 
> 

### <a name="install-intel-mpi"></a>Установка пакета Intel MPI
Сохраните hello загруженного пакета установки для Intel MPI (l_mpi_p_5.0.3.048.tgz в этом примере) в C:\OpenFoam на головной узел hello и узлы Linux hello доступен этот файл с /openfoam. Затем запустите **clusrun** tooinstall библиотеки Intel MPI на всех узлах Linux hello.

1. Hello ниже команды копирования hello установочный пакет и извлеките его слишком/opt/intel на каждом узле.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. Библиотека MPI Intel tooinstall без вмешательства пользователя, используйте файл silent.cfg. Пример можно найти в hello файлы образцов в конце hello в этой статье. Поместить этот файл в hello общей папки /openfoam. Дополнительные сведения о файле silent.cfg hello см. в разделе [библиотека MPI Intel для Linux руководство по установке - автоматической установки](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).
   
   > [!TIP]
   > Сохраните файл silent.cfg как текстовый файл, в котором для завершения строк используется нотация Linux (только LF, а не CR LF). Это действие гарантирует, что он работает правильно на узлах Linux hello.
   > 
   > 
3. Установка библиотеки Intel MPI в автоматическом режиме.
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a>Настройка MPI
Для тестирования, следует добавить следующие строки toohello /etc/security/limits.conf на каждом узле Linux hello hello:

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


После обновления файла limits.conf hello, перезапустите hello узлах Linux. Например, используйте следующие hello **clusrun** команды:

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

После перезагрузки компьютера убедитесь, что в этой общей папке hello подключается как /openfoam.

### <a name="compile-and-install-openfoam"></a>Компиляция и установка OpenFOAM
Сохраните hello загруженного пакета установки для hello tooC:\OpenFoam OpenFOAM источника пакета (в этом примере OpenFOAM 2.3.1.tgz) на головной узел hello и узлы Linux hello доступен этот файл с /openfoam. Затем запустите **clusrun** команды Здравствуйте, toocompile OpenFOAM на всех узлах Linux.

1. Создайте /opt/OpenFOAM папки на каждом узле Linux, копирование hello источника пакета toothis папки и его извлечения.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. toocompile OpenFOAM с hello Intel MPI библиотеки, сначала настроить несколько переменных среды для Intel MPI и OpenFOAM. Используйте сценарий bash, называются переменными hello tooset settings.sh. Пример можно найти в hello файлы образцов в конце hello в этой статье. Поместить этот файл (с окончаниях Linux) в hello общей папки /openfoam. Этот файл также содержит параметры для сред MPI и OpenFOAM выполнения hello, используется более поздней версии toorun OpenFOAM задания.
3. Установите необходимые зависимые пакеты toocompile OpenFOAM. В зависимости от вашей дистрибутив Linux сначала необходимо tooadd репозитория. Запустите **clusrun** аналогичные toohello следующие команды:
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    При необходимости SSH tooeach Linux узел toorun hello команды tooconfirm правильного запуска.
4. Выполните следующие команды toocompile OpenFOAM hello. процесс компиляции Hello принимает toocomplete некоторое время и создает большой объем выходных данных toostandard сведения журнала, поэтому следует использовать hello **/ чередуются** параметр вывода hello toodisplay с чередованием.
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > Hello "\`" символ в команде hello является escape-символа для PowerShell. «\`&» является частью команды hello hello означает «&».
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a>Подготовка задания OpenFOAM toorun
Теперь get готов toorun задания MPI вызывается sloshingTank3D, которое является одним из примеров OpenFoam hello, на двух узлах Linux. 

### <a name="set-up-hello-runtime-environment"></a>Настройка среды выполнения hello
tooset hello среды выполнения для MPI и OpenFOAM на узлах Linux hello, запустите следующую команду в окне Windows PowerShell на головном узле hello hello. (Эта команда допустима только для SUSE Linux.)

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a>Подготовка примера данных
Используйте hello головном узле настроена общая папка вы ранее tooshare файлов между узлами Linux hello (Подключить как /openfoam).

1. Tooone SSH в ОС Linux вычислительных узлов.
2. Запустите hello, следующая команда tooset среды выполнения OpenFOAM hello, если это еще не сделано.
   
   ```
   $ source /openfoam/settings.sh
   ```
3. Скопируйте hello sloshingTank3D пример toohello общей папки и перейдите tooit.
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. При использовании параметров по умолчанию hello в этом примере может занять десятки toorun минут, поэтому вы можете toomodify toomake некоторых параметров, ее выполняться быстрее. Один простой вариант — toomodify hello время шаг переменные deltaT и writeInterval в файле system/controlDict hello. Этот файл хранит все входные данные, относящиеся управления toohello времени и чтения и записи данных в решении. Например можно изменить значение hello deltaT из 0,05 too0.5 и writeInterval из 0,05 too0.5 значение hello.
   
   ![Изменение переменных шага][step_variables]
5. Укажите нужные значения для переменных hello в файле system/decomposeParDict hello. В этом примере используются две Linux узлы каждого с 8 ядер, поэтому набора numberOfSubdomains too16 и n hierarchicalCoeffs too(1 1 16), означающее, что выполняется OpenFOAM параллельно с 16 процессов. Дополнительные сведения см. в статье [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4) (Руководство пользователя OpenFOAM. 3.4. Запуск приложений в параллельном режиме).
   
   ![Разделение процессов][decompose]
6. Выполните следующие команды из данных образца hello tooprepare каталога hello sloshingTank3D hello.
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. На головном узле hello вы увидите, что C:\OpenFoam\sloshingTank3D копируются файлы образцов данных hello. (C:\OpenFoam — hello общая папка на головном узле hello).
   
   ![Файлы данных на головном узле hello][data_files]

### <a name="host-file-for-mpirun"></a>Файл узлов для mpirun
На этом шаге создается узел файл (список вычислительных узлов) какие hello **mpirun** команда использует.

1. На одном из узлов Linux hello создайте файл с именем hostfile под /openfoam, поэтому этот файл может быть достигнута по /openfoam/hostfile на всех узлах Linux.
2. В этом файле укажите имена ваших узлов Linux. В этом примере файл hello содержит hello следующие имена:
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > Можно также создать этот файл в C:\OpenFoam\hostfile на головном узле hello. В таком случае сохраните его в виде текстового файла с нотацией Linux для завершения строк (только LF, а не CR LF). Это гарантирует, что он работает правильно на узлах Linux hello.
   > 
   > 
   
   **Оболочка сценария bash**
   
   При наличии большого числа узлов Linux и требуется, чтобы ваш toorun задания на лишь некоторые из них, это не рекомендуется toouse, файл основного узла, так как вы не знаете, какие узлы будут выделяться tooyour задания. В этом случае написать скрипт оболочку bash для **mpirun** toocreate hello файл узлов автоматически. Можно найти оболочку скрипт bash примере вызывается hpcimpirun.sh конце hello в этой статье и сохраните его как /openfoam/hpcimpirun.sh. В этом примере скрипта hello следующие:
   
   1. Настраивает hello переменные среды для **mpirun**и некоторые Добавление команды Параметры toorun hello задания MPI через сеть RDMA hello. В этом случае он устанавливает hello следующие переменные:
      
      * I_MPI_FABRICS=shm:dapl
      * I_MPI_DAPL_PROVIDER=ofa-v2-ib0
      * I_MPI_DYNAMIC_CONNECTION=0
   2. Создает файл узлов, в соответствии с toohello $ переменной среды CCP_NODES_CORES, задаваемый свойством головного узла HPC hello при активации задания hello.
      
      Формат Hello $CCP_NODES_CORES имеет следующую структуру:
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      где:
      
      * `<Number of nodes>`-hello количество узлов, выделенных toothis задания.  
      * `<Name of node_n_...>`— Задание toothis выделенной hello имя каждого узла.
      * `<Cores of node_n_...>`-hello количество ядер на задание toothis выделенный узел hello.
      
      Например если задание hello должен toorun двух узлов, $CCP_NODES_CORES аналогична
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. Hello вызовов **mpirun** команды и добавляет два параметры toohello командную строку.
      
      * `--hostfile <hostfilepath>: <hostfilepath>`-Создает hello путь файла hello hello узел сценария
      * `-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`— Задание toothis выделенной переменной среды, заданные hello головной узел пакета HPC, где хранятся номера hello общего количества ядер. В этом случае он указывает hello число процессов для **mpirun**.

## <a name="submit-an-openfoam-job"></a>Отправка задания OpenFOAM
Теперь вы можете отправить задание из диспетчера кластера HPC. Для некоторых задач задания hello должны hpcimpirun.sh сценария toopass hello в hello команд из командной строки.

1. Подключение tooyour головного узла кластера и запуск диспетчера кластеров HPC.
2. **В управлении ресурсами**, убедитесь, что hello Linux вычислительных узлов в hello **Online** состояния. Если это не так, выберите их и щелкните **Подключить**.
3. В разделе **Управление заданиями** щелкните **Новое задание**.
4. Введите имя задания, например *sloshingTank3D*.
   
   ![Сведения о задании][job_details]
5. В **задания ресурсы**выберите тип ресурса в виде «Узла» hello и установите too2 минимум hello. Эта конфигурация запускает задание hello на двух узлах Linux, каждый из которых имеет восемь ядер в этом примере.
   
   ![Ресурсы задания][job_resources]
6. Нажмите кнопку **изменение задач** в левой области навигации hello и нажмите кнопку **добавить** tooadd задание toohello задачи. Добавьте четыре задание toohello задачи с hello следующие команды и параметры.
   
   > [!NOTE]
   > Под управлением `source /openfoam/settings.sh` настраивает среды выполнения по hello OpenFOAM и MPI, поэтому каждый из следующих задач hello вызывает перед hello OpenFOAM команды.
   > 
   > 
   
   * **Задача 1**. Запустите **decomposePar** toogenerate файлы данных для выполнения **interDyMFoam** в параллельном режиме.
     
     * Назначить задачу toohello один узел
     * **Командная строка** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`
     * **Рабочий каталог** — /openfoam/sloshingTank3D.
     
     См. следующий рисунок hello. Аналогичным образом настроить hello оставшихся задач.
     
     ![Сведения о задаче 1][task_details1]
   * **Задача 2**. Запустите **interDyMFoam** в образце hello параллельных toocompute.
     
     * Назначить задачу toohello двух узлов
     * **Командная строка** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`
     * **Рабочий каталог** — /openfoam/sloshingTank3D.
   * **Задача 3**. Запустите **reconstructPar** toomerge hello задает время каталогов из каждого каталога processor_N_ в один набор.
     
     * Назначить задачу toohello один узел
     * **Командная строка** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`
     * **Рабочий каталог** — /openfoam/sloshingTank3D.
   * **Задача 4**. Запустите **foamToEnsight** в параллельных tooconvert hello OpenFOAM результирующие файлы в EnSight форматирования и поместить hello EnSight файлы в каталоге с именем Ensight в каталоге вариантов hello.
     
     * Назначить задачу toohello двух узлов
     * **Командная строка** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`
     * **Рабочий каталог** — /openfoam/sloshingTank3D.
7. Добавьте зависимости toothese задачи по возрастанию задачи.
   
   ![Зависимости задачи][task_dependencies]
8. Нажмите кнопку **отправить** toorun этого задания.
   
   По умолчанию пакет HPC отправляет задание hello в качестве учетной записи текущего вошедшего в систему пользователя. После нажатия кнопки **отправить**, может появиться диалоговое окно с приглашением tooenter hello имя и пароль пользователя.
   
   ![Учетные данные для задания][creds]
   
   При некоторых условиях HPC Pack запоминает сведения о пользователе hello входных данных до и не показывать это окно. toomake HPC Pack снова отобразить его, введите следующую команду в командной строке hello и затем отправить задание hello.
   
   ```
   hpccred delcreds
   ```
9. Задание Hello принимает от десятки минут tooseveral часов в соответствии с toohello параметров, заданных для образца hello. В карте температур hello вы видите hello задание, выполняющееся на узлах Linux hello. 
   
   ![Тепловая карта][heat_map]
   
   На каждом узле запускается 8 процессов.
   
   ![Процессы Linux][linux_processes]
10. По завершении задания hello найти результаты задания hello в папках C:\OpenFoam\sloshingTank3D и файлы журнала hello в C:\OpenFoam.

## <a name="view-results-in-ensight"></a>Просмотр результатов в EnSight
При необходимости использовать [EnSight](https://www.ceisoftware.com/) toovisualize и анализ результатов hello hello OpenFOAM задания. Дополнительные сведения о визуализации и анимации в EnSight см. в этом [видеоролике](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).

1. После установки EnSight на головном узле hello, запустите ее.
2. Откройте файл C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.
   
   Вы увидите бак в средстве просмотра hello.
   
   ![Резервуар в EnSight][tank]
3. Создание **Isosurface** из **internalMesh**, а затем выберите переменную hello **alpha_water**.
   
   ![Создание isosurface][isosurface]
4. Задайте цвет hello в **Isosurface_part** на предыдущем шаге hello. Например задайте его toowater синим.
   
   ![Изменение цвета isosurface][isosurface_color]
5. Создание **тома Iso** из **стен** , выбрав **стен** в hello **частей** панели и нажмите кнопку hello **Isosurfaces**  на инструментов hello.
6. В диалоговом окне приветствия выберите **тип** как **Isovolume** и задайте hello минимум **Isovolume диапазон** too0.5. toocreate Здравствуйте isovolume, нажмите кнопку **создать с помощью выделенных частей**.
7. Задайте цвет hello в **Iso_volume_part** на предыдущем шаге hello. Например задайте его toodeep воды синим.
8. Задайте цвет hello в **стен**. Например задайте его tootransparent белый.
9. Теперь щелкните **воспроизведение** toosee hello результаты моделирования hello.
   
    ![Результат для резервуара][tank_result]

## <a name="sample-files"></a>Файлы с примерами
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Пример XML-файла конфигурации для развертывания кластера с помощью скрипта PowerShell
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
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
### <a name="sample-silentcfg-file-tooinstall-mpi"></a>Образец silent.cfg файл tooinstall MPI
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a>Пример сценария settings.sh
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a>Пример сценария hpcimpirun.sh
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
