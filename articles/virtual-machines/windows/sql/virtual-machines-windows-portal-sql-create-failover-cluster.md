---
title: "aaaSQL Server FCI - виртуальных машинах Azure | Документы Microsoft"
description: "В этой статье объясняется, каким образом toocreate отказоустойчивого кластера SQL Server экземпляра на виртуальных машинах Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a>Настройка экземпляра отказоустойчивого кластера SQL Server на виртуальных машинах Azure

В этой статье объясняется, как toocreate SQL Server отказоустойчивого кластера экземпляра (FCI) на виртуальных машинах Azure в модель диспетчера ресурсов. Это решение использует [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) как программный виртуальную сеть SAN, синхронизирующего hello хранения (диски с данными) между узлами hello (виртуальные машины Azure) в Кластер Windows. S2D — это новшество в Windows Server 2016.

Hello следующей схеме показано законченное решение hello на виртуальных машинах Azure.

![Группа доступности](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

Hello предшествующий диаграмме показано:

- Две виртуальные машины Azure в отказоустойчивом кластере Windows. Когда виртуальная машина находится в отказоустойчивом кластере, она также называется *узлом кластера* или просто *узлом*.
- В каждой виртуальной машине есть два или больше дисков данных.
- S2D синхронизирует hello данные на диске данных hello и представляется hello синхронизации хранилища в качестве пула носителей.
- пул носителей Hello представляется toohello отказоустойчивого кластера общего тома (CSV) кластера.
- роли кластера Hello отказоустойчивого Кластера SQL Server использует hello CSV для дисков с данными hello.
- Нагрузки Azure балансировки toohold hello IP-адрес для hello отказоустойчивого Кластера SQL Server.
- Группы доступности Azure хранит все ресурсы hello.

   >[!NOTE]
   >Все ресурсы Azure, в диаграмме hello в hello одну группу ресурсов.

[Дополнительные сведения о \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) см. в статье Локальные дисковые пространства в Windows Server 2016.

S2D поддерживает два типа архитектуры — конвергентную и гиперконвергентную. Архитектура Hello в этом документе гиперконвергентных. Хранилища hello местах инфраструктуры гиперконвергентных на hello серверы, ведущее приложение hello кластеризованным. В этой архитектуре hello хранятся на каждом узле отказоустойчивого Кластера SQL Server.

### <a name="example-azure-template"></a>Пример шаблона Azure

Всего решения hello в Azure можно создать на основе шаблона. Пример шаблона доступен в hello GitHub [шаблоны быстрый запуск Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad). Этот пример не предназначен или протестирован для какой-либо конкретной рабочей нагрузки. Можно запустить toocreate шаблона hello отказоустойчивого Кластера SQL Server с доменом подключенных tooyour S2D хранилища. Можно оценить hello шаблон и измените его при необходимости.

## <a name="before-you-begin"></a>Перед началом работы

Существует несколько моментов, которые необходимо tooknow и несколько факторов, которые необходимы в месте перед продолжением работы.

### <a name="what-tooknow"></a>Какие tooknow
Должно быть оперативной понимание hello следующие технологии:

- [технологии кластера под управлением Windows](http://technet.microsoft.com/library/hh831579.aspx);
-  [экземпляры отказоустойчивого кластера SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).

Кроме того должен иметь общее представление о hello следующие технологии:

- [гиперконвергентное решение, использующее локальные дисковые пространства в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct);
- [группы ресурсов Azure](../../../azure-resource-manager/resource-group-portal.md).

### <a name="what-toohave"></a>Какие toohave

Перед выполнением инструкции hello в этой статье, необходимо иметь:

- подписка Microsoft Azure;
- домен Windows на виртуальных машинах Azure;
- Учетная запись с объектами toocreate разрешений в hello виртуальной машины Azure.
- Виртуальная сеть Azure и подсеть с достаточно пространство IP-адресов для hello следующие компоненты:
   - обе виртуальные машины;
   - IP-адрес кластера отработки отказа Hello.
   - IP-адрес для каждого экземпляра отказоустойчивого кластера;
- Служба DNS настроена на hello сети Azure, указывающий toohello контроллеров домена.

После выполнения этих предварительных требований можно продолжить создание отказоустойчивого кластера. Hello первым шагом является toocreate hello виртуальных машин.

## <a name="step-1-create-virtual-machines"></a>Шаг 1. Создание виртуальных машин

1. Войдите в toohello [портал Azure](http://portal.azure.com) с вашей подпиской.

1. [Создайте группу доступности Azure](../tutorial-availability-sets.md).

   доступность Hello задать группы виртуальных машин в доменах сбоя и домены обновления. набор доступности Hello гарантирует, что ваше приложение не повлияют единственных точек отказа, таких как hello сетевой коммутатор или блок питания стойки серверов hello.

   Если вы не создали hello группы ресурсов для виртуальных машин, только при создании группы доступности Azure. Если вы используете группы доступности hello Azure портала toocreate hello, hello следующие действия:

   - В hello портал Azure, щелкните  **+**  tooopen hello Azure Marketplace. Найдите **Группа доступности**.
   - Выберите **Группа доступности**.
   - Щелкните **Создать**.
   - На hello **создать набор доступности** колонке hello набор следующие значения:
      - **Имя**: имя набора доступности hello.
      - **Подписка.** Ваша подписка Azure.
      - **Группа ресурсов**: toouse существующую группу, нажмите кнопку **использовать существующие** и hello выберите группу из раскрывающегося списка hello. В противном случае выберите **создать новый** и введите имя для группы hello.
      - **Расположение**: задать hello расположение, где toocreate виртуальных машин.
      - **Домены отказоустойчивости**: использовать значение по умолчанию hello (3).
      - **Домены обновления**: использовать значение по умолчанию hello (5).
   - Нажмите кнопку **создать** набор доступности toocreate hello.

1. Создание виртуальных машин hello в набор доступности hello.

   Подготовить два виртуальных машин SQL Server в наборе доступности Azure hello. Инструкции см. в разделе [подготовки виртуальной машины SQL Server в Azure portal hello](virtual-machines-windows-portal-sql-server-provision.md).

   Разместите обе виртуальные машины:

   - В hello одной группе ресурсов Azure, задайте доступности находится в.
   - На hello сетевых как контроллер домена.
   - в подсети с достаточным пространством IP-адресов для обеих виртуальных машин и всех экземпляров отказоустойчивого кластера, которые со временем могут использоваться в этом кластере;
   - В наборе доступности Azure hello.   

      >[!IMPORTANT]
      >После создания виртуальной машины установить или изменить группу доступности невозможно.

   Выбор изображения из hello Azure Marketplace. Можно использовать Marketplace включает образ с, Windows Server и SQL Server или просто hello Windows Server. Дополнительные сведения см. в статье [Приступая к работе с SQL Server в виртуальных машинах Azure](../../virtual-machines-windows-sql-server-iaas-overview.md).

   Hello официальный образов SQL Server в коллекции Azure hello включают установленного экземпляра SQL Server, а также программное обеспечение для установки SQL Server hello и требуемый раздел hello.

   Выберите правом изображении hello в соответствии с нужным toohow toopay hello лицензии SQL Server:

   - **Оплата за использование лицензирования**: hello / мин стоимость этих образов включает hello лицензирования SQL Server:
      - **SQL Server 2016 Enterprise на базе Windows Server Datacenter 2016**;
      - **SQL Server 2016 Standard на базе Windows Server Datacenter 2016**;
      - **SQL Server 2016 Developer на базе Windows Server Datacenter 2016**.

   - **BYOL (с использованием собственной лицензии)**:

      - **{BYOL} SQL Server 2016 Enterprise на базе Windows Server Datacenter 2016**;
      - **{BYOL} SQL Server 2016 Standard на базе Windows Server Datacenter 2016**.

   >[!IMPORTANT]
   >После создания виртуальной машины hello, удалите hello предустановленных автономным экземпляром SQL Server. После настройки hello отказоустойчивого кластера и S2D будет использоваться hello предварительно установить SQL Server носителя toocreate hello отказоустойчивого Кластера SQL Server.

   Кроме того можно использовать образы Azure Marketplace просто hello операционную систему. Выберите **Windows Server 2016 Datacenter** и образов установки hello отказоустойчивого Кластера SQL Server после настройки hello отказоустойчивого кластера и S2D. Этот образ не содержит установочный носитель SQL Server. Поместите hello установочного носителя в расположении, где выполняется установка SQL Server hello для каждого сервера.

1. После Azure создает виртуальные машины, подключите tooeach виртуальную машину с помощью протокола удаленного рабочего СТОЛА.

   При первом подключении tooa виртуальной машины с помощью протокола удаленного рабочего СТОЛА, компьютер hello запросом tooallow этот ПК toobe обнаружения сети hello. Щелкните **Да**.

1. При использовании одного из образов hello виртуальной машины под управлением SQL Server, удалите hello экземпляр SQL Server.

   - В разделе **Программы и компоненты** правой кнопкой мыши щелкните **Microsoft SQL Server 2016 (64-разрядная версия)** и выберите **Удалить/Изменить**.
   - Нажмите кнопку **Удалить**.
   - Выберите экземпляр по умолчанию hello.
   - Удалите все компоненты в разделе **Службы ядра СУБД**. Не удаляйте компоненты в разделе **Общие компоненты**. См. следующий рисунок hello.

      ![Удаление компонентов](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - Нажмите кнопку **Далее**, а затем — кнопку **Удалить**.

1. <a name="ports"></a>Открыть порты брандмауэра hello.

   На каждой виртуальной машине откройте следующие порты в брандмауэре Windows hello hello.

   | Назначение | TCP-порт | Примечания
   | ------ | ------ | ------
   | SQL Server | 1433 | Обычный порт для экземпляров SQL Server по умолчанию. Если использовать образ из коллекции hello, этот порт будет автоматически открыт.
   | Проверка работоспособности | 59999 | Любой открытый TCP-порт. На более позднем этапе настройки балансировки нагрузки hello [проверки работоспособности](#probe) и hello кластера toouse этот порт.  

1. Добавление хранилища toohello виртуальной машины. Дополнительные сведения см. в статье [Хранилище класса "Премиум": высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../../../storage/common/storage-premium-storage.md).

   Для обеих виртуальных машин необходимо по крайней мере два диска данных.

   Присоедините диски в формате RAW — диски, не отформатированные в NTFS.
      >[!NOTE]
      >Если присоединить диски, отформатированные в NTFS, S2D можно включить только без проверки допустимости диска.  

   Присоедините как минимум два tooeach хранилище Premium (SSD-дисков) виртуальной Машины. Мы рекомендуем по крайней мере диски P30 (1 ТБ).

   Набор узлов, кэширование слишком**только для чтения**.

   Hello емкость хранилища, используемого в рабочей среде зависит от рабочей нагрузки. Hello значений, описанных в этой статье предназначены для демонстрации и тестирования.

1. [Добавить существующий домен hello виртуальные машины tooyour](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

После создания и настройки hello виртуальных машин можно настроить hello отказоустойчивого кластера.

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a>Шаг 2: Настройка отказоустойчивого кластера Windows hello с S2D

Hello следующим шагом является tooconfigure hello отказоустойчивый кластер с S2D. На этом шаге будет выполнять hello следующие шаги:

1. Добавление компонента отказоустойчивой кластеризации Windows.
1. Проверка кластера hello
1. Создание отказоустойчивого кластера hello
1. Создание следящий сервер облака hello
1. Добавление хранилища.

### <a name="add-windows-failover-clustering-feature"></a>Добавление компонента отказоустойчивой кластеризации Windows.

1. toobegin, подключение toohello первую виртуальную машину с помощью протокола удаленного рабочего СТОЛА, используя учетную запись домена, которая является членом локальной группы администраторов и не имеет разрешения toocreate объектов в Active Directory. Используйте эту учетную запись для hello остальной конфигурацией hello.

1. [Добавить виртуальную машину отказоустойчивой кластеризации для компонентов tooeach](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

   Средство отказоустойчивости кластеров tooinstall из пользовательского интерфейса, hello hello инструкциям на обеих виртуальных машин.
   - В **диспетчере серверов** выберите **Управление**, а затем — **Добавить роли и компоненты**.
   - В **мастера добавления ролей и компонентов**, нажмите кнопку **Далее** пока не будет получен слишком**Выбор компонентов**.
   - В разделе **Выбор компонентов** выберите **Отказоустойчивая кластеризация**. Включить все необходимые компоненты и средства управления hello. Щелкните **Добавить компоненты**.
   - Нажмите кнопку **Далее** и нажмите кнопку **Готово** tooinstall функции hello.

   tooinstall hello отказоустойчивой кластеризации с помощью PowerShell, запустите следующий скрипт из сеанса PowerShell администратора на одной из виртуальных машин hello hello.

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

Справочник, дальнейшие действия hello следовать инструкциям hello в шаге 3 [схождения Hyper решения, с помощью дисковых пространств в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).

### <a name="validate-hello-cluster"></a>Проверка кластера hello

В этом руководстве tooinstructions под [проверки кластера](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).

Проверка кластера hello hello пользовательского интерфейса или с помощью PowerShell.

toovalidate hello кластера с помощью пользовательского интерфейса, hello hello, выполнив действия из одной из виртуальных машин hello.

1. В **диспетчере серверов** выберите **Сервис**, а затем — **Диспетчер отказоустойчивости кластеров**.
1. В **диспетчере отказоустойчивости кластеров** выберите **Действие**, а затем щелкните **Проверить конфигурацию...**.
1. Щелкните **Далее**.
1. На **Выбор серверов или кластера**, имя типа hello обе виртуальные машины.
1. На вкладке **Параметры тестирования** выберите **Выполнять только выбранные тесты**. Щелкните **Далее**.
1. На вкладке **Выбор тестов** выберите все тесты, кроме **Хранилище**. См. следующий рисунок hello.

   ![Проверка тестов](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. Щелкните **Далее**.
1. На вкладке **Подтверждение** нажмите кнопку **Далее**.

Hello **мастер проверки конфигурации** запусков hello проверочные тесты.

toovalidate hello кластера с помощью PowerShell, запустите следующий скрипт из сеанса PowerShell администратора на одной из виртуальных машин hello hello.

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

После проверки кластера hello, создайте отказоустойчивый кластер hello.

### <a name="create-hello-failover-cluster"></a>Создание отказоустойчивого кластера hello

В этом руководстве, слишком[создать hello отказоустойчивого кластера](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).

toocreate hello отказоустойчивый кластер, необходимо:
- имена Hello hello виртуальных машин, которые становятся hello узлов кластера.
- Имя для hello отказоустойчивого кластера
- IP-адрес для hello отказоустойчивого кластера. Можно использовать IP-адрес, который не используется на hello одной виртуальной сети Azure и подсеть, как hello узлов кластера.

Привет, следуя PowerShell создается отказоустойчивый кластер. Обновление hello скрипт с hello имена узлов hello (приветствия имен виртуальных машин) и доступные IP-адрес из hello виртуальной сети Azure:

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a>Создание облака-свидетеля

Облако-свидетель является новым типом свидетеля кворума кластера, хранящегося в Azure Storage Blob. Эта функция удаляет необходимость hello отдельной виртуальной машины, размещение общей папке следящего сервера.

1. [Создание облачных следящего сервера для hello отказоустойчивого кластера](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).

1. Создайте контейнер больших двоичных объектов.

1. Сохраните ключи доступа hello и URL-адрес контейнера hello.

1. Настройка следящего сервера кворума кластера hello отказоустойчивого кластера. В разделе, [Настройка свидетеля кворума hello в пользовательском интерфейсе hello]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) в hello пользовательского интерфейса.

### <a name="add-storage"></a>Добавление хранилища.

Hello дисков для S2D должны toobe пустой и без секций или других данных. Выполните дисков tooclean [hello шаги данного руководства](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).

1. [Включите локальные дисковые пространства \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).

   Привет, следуя PowerShell позволяет дисковые пространства прямого подключения.  

   ```PowerShell
   Enable-ClusterS2D
   ```

   В **Диспетчер отказоустойчивости кластеров**, теперь можно увидеть hello пула носителей.

1. [Создайте том](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).

   Одной из функций hello S2D является, он автоматически создается пул носителей при его включении. Теперь вы находитесь готов toocreate тома. Здравствуйте, командлет PowerShell `New-Volume` автоматизирует процесс создания тома hello, включая форматирование, добавление toohello кластера и создание общий том кластера (CSV). Следующий пример Hello создает 800 ГБ CSV.

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   После выполнения этой команды том емкостью 800 ГБ подключается как ресурс кластера. том Hello в `C:\ClusterStorage\Volume1\`.

   Привет, следующая схема показывает общий том кластера с S2D:

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a>Шаг 3. Тестирование отработки отказа отказоустойчивого кластера

В диспетчере отказоустойчивости кластеров, убедитесь, что можно переместить toohello ресурсов хранилища hello другой узел кластера. Если вы можете подключиться toohello отказоустойчивый кластер с **Диспетчер отказоустойчивости кластеров** и переместить хранилище hello из одного узла toohello других, вы готовы tooconfigure hello отказоустойчивого Кластера.

## <a name="step-4-create-sql-server-fci"></a>Шаг 4. Создание экземпляра отказоустойчивого кластера SQL Server

После настройки hello отказоустойчивого кластера и все компоненты кластера, включая хранилище можно создать hello отказоустойчивого Кластера SQL Server.

1. Первая виртуальная машина toohello подключитесь с помощью протокола удаленного рабочего СТОЛА.

1. В **Диспетчер отказоустойчивости кластеров**, убедитесь, что все основные ресурсы кластера на первой виртуальной машине hello. При необходимости переместите все ресурсы toothis виртуальную машину.

1. Найдите hello установочного носителя. Если виртуальная машина hello использует одно из изображений hello Azure Marketplace, hello мультимедиа находится в `C:\SQLServer_<version number>_Full`. Щелкните **Настройка**.

1. В hello **центр установки SQL Server**, нажмите кнопку **установки**.

1. Щелкните **Новая установка отказоустойчивого кластера SQL Server**. Следуйте инструкциям hello приветствия мастера tooinstall hello отказоустойчивого Кластера SQL Server.

   каталоги данных Hello отказоустойчивого Кластера должны toobe на кластерных хранилищ. С S2D он не общий диск, но tooa точки подключения тома на каждом сервере. S2D синхронизирует тома hello между обоих узлов. Hello тома выводится toohello кластера как общий том кластера. Используйте точку подключения CSV hello каталогов данных hello.

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. После завершения мастера hello, программа установки установит отказоустойчивого Кластера SQL Server на первом узле hello.

1. После успешного Установка hello отказоустойчивого Кластера на первом узле hello, подключиться toohello второго узла с помощью протокола удаленного рабочего СТОЛА.

1. Откройте hello **центр установки SQL Server**. Щелкните **Установка**.

1. Нажмите кнопку **отказоустойчивого кластера SQL Server tooa добавить узел**. Следуйте инструкциям hello приветствия мастера tooinstall SQL server и добавьте этот сервер toohello отказоустойчивого Кластера.

   >[!NOTE]
   >При использовании образа коллекции Azure Marketplace с SQL Server средств SQL Server были включены с помощью образа hello. Если вы не использовали этот образ, установите средства SQL Server hello отдельно. См. сведения в статье [Скачивание SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="step-5-create-azure-load-balancer"></a>Шаг 5.Создание Azure Load Balancer

На виртуальных машинах Azure кластеров с помощью toohold подсистемы балансировки нагрузки IP-адрес, который должен toobe на одном узле кластера одновременно. В этом решении балансировки нагрузки hello содержит hello IP-адрес для hello отказоустойчивого Кластера SQL Server.

[Создайте и настройте балансировщик нагрузки Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a>Создание hello балансировки нагрузки в hello портал Azure

Подсистема балансировки нагрузки hello toocreate:

1. В hello портал Azure перейдите toohello группы ресурсов с виртуальными машинами hello.

1. Щелкните **+ Добавить**. Поиск hello Marketplace для **балансировки нагрузки**. Щелкните **Балансировщик нагрузки**.

1. Щелкните **Создать**.

1. Настройка балансировки нагрузки hello с:

   - **Имя**: имя, идентифицирующее hello подсистемы балансировки нагрузки.
   - **Тип**: hello балансировки нагрузки может быть открытой или закрытой. Балансировщик нагрузки закрытый может осуществляться в hello одной виртуальной сети. Большинство приложений Azure могут использовать закрытый балансировщик нагрузки. Если приложению доступа tooSQL сервер непосредственно через Интернет hello используется внешняя Подсистема балансировки нагрузки.
   - **Виртуальная сеть**: hello сетевых как hello виртуальные машины.
   - **Подсети**: hello подсети hello виртуальных машин.
   - **Частный IP-адрес**: hello же IP-адрес, назначенный ресурсу сетевого кластера toohello отказоустойчивого Кластера SQL Server.
   - **Подписка.** Ваша подписка Azure.
   - **Группа ресурсов**: используйте hello же группе ресурсов, что виртуальные машины.
   - **Расположение**: используйте hello же расположению Azure, виртуальные машины.
   См. следующий рисунок hello.

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a>Настройка внутреннего пула подсистемы балансировки нагрузки hello

1. Возвращает toohello группы ресурсов Azure с виртуальными машинами hello и найдите hello новую подсистему балансировки нагрузки. Может иметь вид hello toorefresh на hello группы ресурсов. Выберите hello подсистему балансировки нагрузки.

1. В колонке подсистемы балансировки нагрузки hello, нажмите кнопку **внутренние пулы**.

1. Нажмите кнопку **+ добавить** tooadd внутренний пул.

1. Введите имя для hello внутренний пул.

1. Щелкните **Добавить виртуальную машину**.

1. На hello **выберите виртуальные машины** колонка, щелкните **выберите группу доступности**.

1. Выберите группу доступности hello помещен hello виртуальных машин SQL Server в.

1. На hello **выберите виртуальные машины** колонка, щелкните **выберите виртуальные машины hello**.

   Портал Azure должно иметь вид hello следующий рисунок:

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. Нажмите кнопку **выберите** на hello **выберите виртуальные машины** колонку.

1. Нажмите **ОК** дважды.

### <a name="configure-a-load-balancer-health-probe"></a>Настройка пробы работоспособности балансировщика нагрузки

1. В колонке подсистемы балансировки нагрузки hello, нажмите кнопку **зонды работоспособности**.

1. Щелкните **+ Добавить**.

1. На hello **проверки работоспособности добавить** колонке <a name="probe"> </a>задать параметры проверки работоспособности hello:

   - **Имя**: имя для проверки работоспособности hello.
   - **Протокол.** TCP.
   - **Порт**: задать tooan доступный TCP-порт. Для этого порта требуется открытый порт брандмауэра. Используйте hello [тот же порт](#ports) , задаваемое для проверки работоспособности hello на брандмауэре hello.
   - **Интервал.** 5 секунд.
   - **Порог состояния неработоспособности.** 2 последовательных сбоя.

1. Нажмите кнопку ОК.

### <a name="set-load-balancing-rules"></a>Задание правил балансировки нагрузки

1. В колонке подсистемы балансировки нагрузки hello, нажмите кнопку **правила подсистемы балансировки нагрузки**.

1. Щелкните **+ Добавить**.

1. Задайте параметры правила балансировки нагрузки hello:

   - **Имя**: имя для правила подсистемы балансировки нагрузки hello.
   - **Интерфейсный IP-адрес**: использовать hello IP-адрес для hello ресурса сети кластера для отказоустойчивого Кластера SQL Server.
   - **Порт**: задать для hello порт TCP отказоустойчивого Кластера SQL Server. порт экземпляра по умолчанию Hello: 1433.
   - **Внутренний порт**: hello же порт использует это значение в качестве hello **порт** значение при включении **плавающий IP-адрес (прямой возврат сервера)**.
   - **Внутренний пул**: имя пула внутренних hello использование ранее.
   - **Проверка работоспособности**: проверка работоспособности hello использование ранее.
   - **Сохранение сеанса.** Нет.
   - **Время ожидания простоя (в минутах)**: 4.
   - **Плавающий IP-адрес (direct server return).** Включено.

1. Нажмите кнопку **ОК**.

## <a name="step-6-configure-cluster-for-probe"></a>Шаг 6. Настройка кластера для проверки

Параметр hello кластера пробы порт в PowerShell.

tooset Здравствуйте параметр port проверки кластера, обновить переменные в hello следующий скрипт из среды.

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a>Шаг 7. Проверка отработки отказа экземпляра отказоустойчивого кластера

Тестовая отработка отказа FCI toovalidate кластера функции hello. Здравствуйте, следующие действия:

1. Подключитесь tooone узлов кластера hello отказоустойчивого Кластера SQL Server с помощью протокола удаленного рабочего СТОЛА.

1. Откройте **диспетчер отказоустойчивости кластеров**. Щелкните **Роли**. Обратите внимание, какой из узлов является владельцем роли hello отказоустойчивого Кластера SQL Server.

1. Щелкните правой кнопкой мыши роль hello отказоустойчивого Кластера SQL Server.

1. Щелкните **Переместить** и выберите **Лучший из возможных узлов**.

**Диспетчер отказоустойчивости кластеров** показано hello роли и его ресурсы переходят в автономный режим. Hello ресурсы затем переместите и переходит в оперативный режим Здравствуйте, на другой узел.

### <a name="test-connectivity"></a>Проверка подключения

возможность подключения tootest журнала tooanother виртуальной машине в hello одной виртуальной сети. Откройте **SQL Server Management Studio** и подключите toohello имя отказоустойчивого Кластера SQL Server.

>[!NOTE]
>При необходимости можно [скачать SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="limitations"></a>Ограничения
На виртуальных машинах Azure координатора распределенных транзакций (DTC) не поддерживается на отказоустойчивые кластеры, поскольку hello порта RPC не поддерживается подсистемой балансировки нагрузки hello.

## <a name="see-also"></a>См. также

[Deploy a two-node S2D SOFS for UPD storage in Azure](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment) (Развертывание S2D SOFS с двумя узлами для хранилища UPD в Azure).

[Гиперконвергентное решение с использованием локальных дисковых пространств в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).

[Локальные дисковые пространства в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

[SQL Server 2016 now supports Windows Server 2016 Storage Spaces Direct](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/) (SQL Server 2016 теперь поддерживает локальные дисковые пространства Windows Server 2016).
