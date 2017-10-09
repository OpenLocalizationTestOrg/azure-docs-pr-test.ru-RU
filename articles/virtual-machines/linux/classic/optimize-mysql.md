---
title: "aaaOptimize MySQL производительности в Linux | Документы Microsoft"
description: "Узнайте, как toooptimize MySQL на виртуальной машине Azure (ВМ) под управлением Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a>Оптимизация производительности MySQL на виртуальных машинах Linux в Azure
Существует множество факторов, влияющих на производительность MySQL в Azure, которые зависят и от выбора виртуального оборудования, и от конфигурации программного обеспечения. Эта статья посвящена оптимизации производительности с помощью конфигураций хранилища, системы и базы данных.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager](../../../resource-manager-deployment-model.md) и классическая модель. В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Сведения об оптимизации виртуальных Машин Linux с моделью hello диспетчера ресурсов см. в разделе [оптимизировать ВМ Linux в Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="utilize-raid-on-an-azure-virtual-machine"></a>Использование RAID на виртуальной машине Azure
Хранилище — hello ключевым фактором, влияющим на производительность базы данных в облачных средах. Сравниваемые tooa одного диска, RAID обеспечивается более быстрый доступ посредством параллелизма. Дополнительные сведения см. в описании [стандартных уровней RAID](http://en.wikipedia.org/wiki/Standard_RAID_levels).   

С помощью RAID в Azure можно существенно увеличить пропускную способность и время ответа для операций ввода-вывода. Наши тесты лаборатории Показать, что можно удвоить пропускной способности дискового ввода-вывода и времени ответа ввода-вывода уменьшается вдвое в среднем при hello количество дисков RAID в два раза (из двух toofour, четыре tooeight, и т. д.). Дополнительные сведения см. в [приложении А](#AppendixA).  

В дополнение к этому toodisk ввода-вывода, MySQL производительность повышается при увеличении hello уровень RAID.  Дополнительные сведения см. в [приложении Б](#AppendixB).  

Можно также настроить размер блока tooconsider hello. Обычно чем больше размер блока, тем ниже нагрузка, особенно для объемных операций записи. Однако когда hello размер фрагмента данных слишком велик, может добавить дополнительную нагрузку, которая не позволяет воспользоваться преимуществом RAID. Hello текущий размер по умолчанию — 512 КБ, что подтверждается toobe оптимальным для большинства рабочих сред. Дополнительные сведения см. в [приложении В](#AppendixC).   

Для виртуальных машин разных типов существуют ограничения на количество дисков, которые можно добавить. Эти ограничения описаны в статье [Размеры для облачных служб](http://msdn.microsoft.com/library/azure/dn197896.aspx). Несмотря на то, что вы можете tooset копирование RAID с меньшим числом дисков, потребуется четыре присоединенные диски toofollow hello RAID пример данных в этой статье.  

В этой статье предполагается, что вы уже создали виртуальную машину Linux, а также установили и настроили MySQL. Дополнительные сведения о начале работы см. в разделе как tooinstall MySQL в Azure.  

### <a name="set-up-raid-on-azure"></a>Настройка RAID в Azure
Hello следующие шаги показывают, как toocreate RAID-КОНТРОЛЛЕР на Azure с помощью портала Azure hello. RAID также можно настроить с помощью сценариев Windows PowerShell.
В этом примере мы настроим RAID 0 с 4 дисками.  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a>Добавить виртуальную машину tooyour диска данных
В hello портал Azure перейдите toohello панели мониторинга и выберите toowhich hello виртуальной машины, нужно tooadd диск данных. В этом примере hello виртуальной машины — mysqlnode1.  

<!--![Virtual machines][1]-->

Щелкните **Диски** и выберите **Подключить новый**.

![Добавление дисков в виртуальную машину](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

Создайте новый диск объемом 500 ГБ. Убедитесь, что **настройки кэша узла** задано слишком**нет**.  Закончив, нажмите кнопку **ОК**.

![Присоединить пустой диск](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


Теперь вы добавили один пустой диск в виртуальную машину. Повторите этот шаг еще три раза, чтобы настроить четыре диска данных для RAID.  

Вы увидите hello добавлены дисков на виртуальной машине hello, просмотрев журнал сообщений hello ядра. Например, toosee это на Ubuntu hello используйте следующую команду:  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a>Создайте RAID с hello дополнительные диски.
Hello следующие шаги описывают как слишком[Настройка программного RAID на платформе Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> При использовании hello XFS файловой системы, выполните следующие шаги после создания RAID hello.
>
>

tooinstall XFS на Linux Mint, Debian и Ubuntu hello используйте следующую команду:  

    apt-get -y install xfsprogs  

tooinstall XFS на Fedora, CentOS или RHEL, hello используйте следующую команду:  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a>Настройка нового пути к хранилищу
Используйте hello следующая команда tooset новый путь хранения:  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a>Скопируйте hello исходные данные toohello новый путь к хранилищу
Используйте следующие команды toocopy данных toohello новый путь к хранилищу hello.  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a>Изменить разрешения, поэтому можно получить доступ к MySQL (чтение и запись) диска данных hello
Используйте следующие команды toomodify разрешения hello.  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a>Настройка hello дискового ввода-вывода, алгоритм планирования
В Linux реализовано четыре типа алгоритмов планирования операций ввода-вывода:  

* алгоритм NOOP (без операции);
* алгоритм крайнего срока (крайний срок);
* алгоритм организации полностью равноправных очередей (CFQ);
* алгоритм бюджетного периода (прогнозирование).  

Можно выбрать различные планировщики ввода-вывода в различных сценариях toooptimize производительности. В среде полностью произвольного доступа не значительные различия между hello CFQ и алгоритмы крайний срок для повышения производительности. Мы рекомендуем задавать tooDeadline среды базы данных MySQL hello для стабильности. Если выполняется много последовательных операций ввода-вывода, метод равноправных очередей может снизить производительность дисковых операций ввода-вывода.   

SSD и другом оборудовании NOOP или крайний срок можно улучшить производительность, чем планировщик по умолчанию hello.   

Предыдущий toohello ядра 2.5 hello ввода-вывода по умолчанию алгоритм планирования — крайнего срока. Начиная с hello ядра 2.6.18 CFQ стала Алгоритм планирования операций ввода-вывода по умолчанию hello.  Можно указать этот параметр во время загрузки ядра или динамически изменять этот параметр, при запуске системы hello.  

Hello в следующем примере показано, как toocheck и набор hello алгоритм NOOP toohello планировщик по умолчанию hello Debian распространения семейства.  

### <a name="view-hello-current-io-scheduler"></a>Представление hello текущего планировщика ввода-вывода
Запустите планировщик hello tooview hello следующую команду:  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

Вы увидите следующие выходных данных, который указывает hello текущего планировщика.  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a>Изменить текущее устройство hello (/ dev/sda) Алгоритм планирования hello ввода-вывода
Выполните следующие команды toochange hello текущего устройства hello.  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> Настраивать алгоритм только для устройства /dev/sda бесполезно. Его необходимо задавать на все диски с данными, где находится база данных hello.  
>
>

Вы должны увидеть hello следующие выходные данные, об grub.cfg был перестроен успешно, и этот планировщик по умолчанию hello был обновленные tooNOOP.  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

Для hello семейства распространения Red Hat требуются только hello следующую команду:

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a>Настройка параметров операций системного файла
Один рекомендуется toodisable hello *atime* функции ведения журнала в файловой системе hello. Atime — hello времени последнего открытия файла. При каждом обращении к файлу, записей hello hello timestamp в журнале hello. Однако эта информация используется редко. При необходимости эту функцию можно отключить, что позволит уменьшить общее время доступа к диску.  

toodisable atime ведения журнала, toomodify hello файла система конфигурации файл/etc / fstab и добавьте hello **noatime** параметр.  

Например измените файл/etc/fstab vim hello, добавления hello noatime, как показано в следующих образец hello.  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

Затем подключите hello файловой системы с hello следующую команду:  

    mount -o remount /RAID0

Тест hello изменить результат. При изменении файла теста hello, время доступа hello не обновляется. Hello в следующих примерах показано, какая часть кода hello выглядит до и после изменения.

До:        

![Код до внесения изменений][5]

После:

![Код после внесения изменений][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a>Увеличьте максимальное число системных дескрипторов для высокого уровня параллелизма hello
MySQL — база данных с высокой степенью параллелизма. количество параллельных дескрипторы по умолчанию Hello — 1024 для Linux, что не всегда достаточно. Используйте следующие шаги tooincrease hello Максимальная одновременных дескрипторы hello системы toosupport высокого уровня параллелизма MySQL hello.

### <a name="modify-hello-limitsconf-file"></a>Измените файл limits.conf hello
hello tooincrease максимальное допустимое параллельных дескрипторов, добавьте следующие четыре строки в файле /etc/security/limits.conf hello hello. Обратите внимание, что 65536 hello максимального количества, которое может поддерживаться системой hello.   

    * soft nofile 65536
    * hard nofile 65536
    * soft nproc 65536
    * hard nproc 65536

### <a name="update-hello-system-for-hello-new-limits"></a>Обновление системы hello hello новых ограничений
tooupdate система hello, запустите hello, следующие команды:  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a>Убедитесь, что ограничения hello обновляются во время загрузки
Поместите hello, после запуска команды в файле /etc/rc.local hello, вступают в силу во время загрузки.  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a>Оптимизация базы данных MySQL
tooconfigure MySQL в Azure, можно использовать hello же стратегия настройки производительности, используйте на локальном компьютере.  

Hello основных операций ввода-вывода оптимизации правила таковы:   

* Увеличивайте размер кэша hello.
* уменьшите время ответа при выполнении операций ввода-вывода.  

Параметры сервера MySQL toooptimize, можно обновить файл my.cnf hello, хранящийся в файле конфигурации по умолчанию hello для сервера и клиентских компьютеров.  

Hello следующие элементы конфигурации являются hello основные факторы, влияющие на производительность MySQL.  

* **innodb_buffer_pool_size**: hello буферный пул содержит буферизованные данные и индекс hello. Этот параметр обычно задается too70% физической памяти.
* **innodb_log_file_size**: размер журнала hello повтора. Используется tooensure журналы повтора операции записи, быстрый, надежный и возможностью восстановления после сбоя. Этот параметр задается too512 МБ, что обеспечит Вам достаточно места для ведения журнала операций записи.
* **max_connections**. Иногда приложения не закрывают подключения должным образом. Увеличьте значение даст hello server toorecycle привело к бездействию подключений больше времени. Максимальное число подключений Hello 10 000, но рекомендуется hello, максимальное — 5000.
* **Innodb_file_per_table**: этот параметр включает или отключает возможность hello InnoDB toostore таблиц в отдельных файлах. Включите параметр tooensure hello, что несколько операций расширенного администрирования может применяться эффективно. С точки зрения производительности его ускорения передачи пространство таблицы hello и оптимизировать производительность управления hello мусор. Hello рекомендуемые для этого параметра имеет значение ON.</br></br>
Из MySQL 5.6 hello по умолчанию равно ON, поэтому никаких действий не требуется. В более ранних версиях hello по умолчанию — OFF. параметр Hello должны изменяться до загрузки данных, так как она затронет только вновь созданных таблицах.
* **innodb_flush_log_at_trx_commit**: hello значение по умолчанию равно 1, с hello область значение too0 ~ 2. значение по умолчанию Hello — hello наиболее подходящий вариант для автономной базы данных MySQL. Hello, равное 2 — разрешает hello большинство целостность данных и подходит для базы данных Master в кластере MySQL. параметр Hello 0 позволяет потерь данных, который может повлиять на надежность (в некоторых случаях с точки зрения производительности) и подходит для ведомый экземпляр в кластер MySQL.
* **Innodb_log_buffer_size**: hello буфера журнала позволяет toorun транзакций без необходимости toodisk журнала hello tooflush до фиксации транзакции hello. Если большой двоичный объект или текстовое поле, hello кэша будет быстро израсходовано и часто дискового ввода-вывода будет запущено. Это лучше увеличить размер буфера hello, если переменной состояния Innodb_log_waits не 0.
* **query_cache_size**: hello наилучшим вариантом является toodisable с самого начала hello. Too0 query_cache_size (это параметр по умолчанию hello в MySQL 5.6) и выбрать другие методы toospeed запросов.  

В разделе [приложение D](#AppendixD) Сравнение производительности до и после оптимизации hello.

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a>Включите журнал медленных запросов hello MySQL для анализа узким местом производительности hello
Журнал медленных запросов в MySQL Hello может помочь в идентификации медленных запросов hello для MySQL. После включения журнал медленных запросов в MySQL hello, вы можете использовать инструменты MySQL как **mysqldumpslow** tooidentify узким местом производительности hello.  

По умолчанию он отключен. Включение hello журнал медленных запросов может использовать некоторые ресурсы ЦП. Мы рекомендуем включать его ненадолго, только для устранения узких мест производительности. tooturn на журнал медленных запросов hello:

1. Измените файл my.cnf hello, добавив после окончания строк toohello hello:

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. Перезапустите сервер MySQL hello.

        service  mysql  restart

3. Проверьте, занимает ли приветствия эффект с помощью hello **Показать** команды.

![Включение Slow-query-log][7]   

![Результаты Slow-query-log][8]

В этом примере вы увидите, включите эту функцию hello медленных запросов. Затем можно использовать hello **mysqldumpslow** средства toodetermine узкие места по производительности и оптимизации производительности, например, добавлением индексов.

## <a name="appendices"></a>Приложения
Здесь представлены Hello образец производительности тестовых данных, полученных в целевой среде. Они предоставляют общие для данных тренда hello производительности различных подходов быстродействия. Hello результаты могут отличаться в различных версиях среды или продукта.

### <a name="AppendixA"></a>Приложение А  
**Производительность диска (количество операций ввода-вывода в секунду) с разными уровнями RAID**

![Количество операций ввода-вывода в секунду с разными уровнями RAID][9]

**Команды тестирования**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> Рабочая нагрузка Hello этого теста использует 64 потока, попытки tooreach hello верхний предел RAID.
>
>

### <a name="AppendixB"></a>Приложение Б  
**Сравнение производительности (пропускной способности) MySQL с разными уровнями RAID**   
(Файловая система XFS)

![Сравнение производительности MySQL с разными уровнями RAID][10]  
![Сравнение производительности MySQL с разными уровнями RAID][11]

**Команды тестирования**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

**Сравнение производительности (OLTP) MySQL с разными уровнями RAID**  
![Сравнение производительности (OLTP) MySQL с разными уровнями RAID][12]

**Команды тестирования**

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <a name="AppendixC"></a>Приложение В   
**Сравнение производительности диска (количества операций ввода-вывода в секунду) для разного размера блоков**  
(Файловая система XFS)

![][13]

**Команды тестирования**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

размеры файлов Hello, используемые для тестирования 30 ГБ и 1 ГБ, соответственно, с помощью RAID 0 (4 диска) XFS файловой системы.

### <a name="AppendixD"></a>Приложение Г  
**Сравнение производительности (пропускной способности) MySQL до и после оптимизации**  
(Файловая система XFS)

![Сравнение производительности (пропускной способности) MySQL до и после оптимизации][14]

**Команды тестирования**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

**параметр конфигурации Hello для оптимизации и по умолчанию будет следующим:**

| Параметры | значение по умолчанию | Оптимизация |
| --- | --- | --- |
| **innodb_buffer_pool_size** |None |7 ГБ |
| **innodb_log_file_size** |5 МБ |512 МБ |
| **max_connections** |100 |5000 |
| **innodb_file_per_table** |0 |1 |
| **innodb_flush_log_at_trx_commit** |1 |2 |
| **innodb_log_buffer_size** |8 МБ |128 МБ |
| **query_cache_size** |16 МБ |0 |

Более подробные [параметров конфигурации оптимизации](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), см. toohello [MySQL официальный инструкции](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).  

  **Тестовая среда**  

| Оборудование | Сведения |
| --- | --- |
| ЦП |AMD Opteron(tm), процессор 4171 HE, 4 ядра |
| Память |14 ГБ |
| Диск |10 ГБ на диск |
| ОС |Ubuntu 14.04.1 LTS |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

