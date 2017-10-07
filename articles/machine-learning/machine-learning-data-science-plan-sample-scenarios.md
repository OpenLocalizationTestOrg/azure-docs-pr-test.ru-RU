---
title: "Дополнительные сценарии анализа для машинного обучения Azure aaaIdentify | Документы Microsoft"
description: "Выберите подходящие сценарии hello это расширенный прогнозной аналитики с hello командного процесса обработки и анализа данных."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a>Сценарии для расширенной аналитики в Машинном обучении Azure
В этой статье рассматриваются различные hello образцы источников данных и целевые сценарии, которые могут быть обработаны hello [процесса обработки и анализа данных Team (TDSP)](data-science-process-overview.md). Hello TDSP предоставляет систематический подход для toocollaborate команды на создание интеллектуальных приложений. представленные сценарии Hello показаны параметры, доступные в рабочем процессе hello обработки данных, зависящих от целевой репозиториев в Azure, расположений и характеристики данных hello.

Hello **дерева принятия решений** для выбора hello примеры сценариев, подходящий для данных и цель представлены в последнем разделе hello.

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

Каждого hello в следующих разделах представлен пример сценария. Для каждого сценария перечислены возможные последовательности операций процесса обработки и анализа или расширенного анализа данных, а также вспомогательные ресурсы Azure.

> [!NOTE]
> **Все следующие сценарии hello необходимо:**
> <br/>
> 
> * [создать учетную запись хранения](../storage/common/storage-create-storage-account.md)
>   ;<br/>
> * [Создание рабочей области машинного обучения Azure](machine-learning-create-workspace.md)
> 
> 

## <a name="smalllocal"></a>Сценарий \#1: небольшой toomedium набор табличных данных в локальных файлах
![Небольшие toomedium локальные файлы][1]

#### <a name="additional-azure-resources-none"></a>Дополнительные ресурсы Azure: отсутствуют
1. Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).
2. Отправьте набор данных.
3. Создайте последовательность операций эксперимента Машинного обучения Azure, начиная с отправленных наборов данных.

## <a name="smalllocalprocess"></a>Сценарий \#2: набор данных небольшой toomedium локальных файлов, которые требуют обработки
![Небольшие toomedium локальных файлов с обработкой][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Дополнительные ресурсы Azure: виртуальная машина Azure (сервер IPython Notebook)
1. Создайте виртуальную машину Azure с IPython Notebook.
2. Передача данных контейнер хранилища Azure tooan.
3. Предварительно обработайте и очистите данные в IPython Notebook из контейнера хранилища Azure.
4. Преобразование данных toocleaned, табличной форме.
5. Сохраните преобразованные данные в большие двоичные объекты Azure.
6. Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).
7. Чтение данных hello из больших двоичных объектов Azure с помощью hello [импорта данных] [ import-data] модуля.
8. Создайте последовательность операций эксперимента Машинного обучения Azure, начиная с принятых наборов данных.

## <a name="largelocal"></a>Сценарий\# №3. Большой набор данных в локальных файлах, загружаемый в большие двоичные объекты Azure
![Локальные файлы большого размера][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Дополнительные ресурсы Azure: виртуальная машина Azure (сервер IPython Notebook)
1. Создайте виртуальную машину Azure с IPython Notebook.
2. Передача данных контейнер хранилища Azure tooan.
3. Предварительно обработайте и очистите данные в IPython Notebook из больших двоичных объектов Azure.
4. При необходимости, преобразовывать toocleaned данных, в табличной форме.
5. Просмотрите данные и при необходимости создайте компоненты.
6. Извлеките пример данных небольшого или среднего размера.
7. Сохраните данные выборки hello в больших двоичных объектов Azure.
8. Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).
9. Чтение данных hello из больших двоичных объектов Azure с помощью hello [импорта данных] [ import-data] модуля.
10. Создайте последовательность операций эксперимента Машинного обучения Azure, начиная с принятых наборов данных.

## <a name="smalllocaltodb"></a>Сценарий \#4: небольшой toomedium набора данных из локальных файлов, предназначенных для SQL Server в виртуальных машинах Azure
![Небольшие toomedium tooSQL локальные файлы базы данных в Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Дополнительные ресурсы Azure: виртуальная машина Azure (сервер SQL Server и IPython Notebook)
1. Создайте виртуальную машину Azure с SQL Server и IPython Notebook.
2. Передача данных контейнер хранилища Azure tooan.
3. Предварительно обработайте и очистите данные в контейнере хранилища Azure с помощью IPython Notebook.
4. При необходимости, преобразовывать toocleaned данных, в табличной форме.
5. Сохранить tooVM локальных файлов данных (ноутбук IPython работает на виртуальной Машине см. в локальные диски tooVM дисков).
6. Загрузите данные tooSQL сервера базы данных, на Виртуальной машине Azure.
   
   Вариант \# №1. Использование SQL Server Management Studio.
   
   * TooSQL входа в систему сервера виртуальных Машин
   * Запустите среду SQL Server Management Studio.
   * Создайте базу данных и целевые таблицы.
   * Используйте одну из массового hello импортировать методы tooload hello данные из файлов локальной виртуальной Машины.
   
   Вариант \# №2. Использование IPython Notebook (не рекомендуется использовать этот вариант для средних и больших наборов данных).
   
   <!-- -->    
   * Используйте tooaccess строку соединения ODBC SQL Server на виртуальной Машине.
   * Создайте базу данных и целевые таблицы.
   * Используйте одну из массового hello импортировать методы tooload hello данные из файлов локальной виртуальной Машины.
7. Просмотрите данные и при необходимости создайте компоненты. Обратите внимание, что функции hello не toobe материализуются в таблицах базы данных hello. Только Примечание hello необходимый запрос toocreate их.
8. При необходимости выберите размер примера данных.
9. Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).
10. Hello чтения данных непосредственно из hello SQL Server с помощью hello [импорта данных] [ import-data] модуля. Необходимый запрос hello вставки, которая извлекает поля, создает компоненты и образцы данных, при необходимости непосредственно в hello [импорта данных] [ import-data] запроса.
11. Создайте последовательность операций эксперимента Машинного обучения Azure, начиная с принятых наборов данных.

## <a name="largelocaltodb"></a>Сценарий \#№5. Большой набор данных в локальных файлах, загружаемый на сервер SQL Server в виртуальной машине Azure
![TooSQL большие файлы локальной базы данных в Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Дополнительные ресурсы Azure: виртуальная машина Azure (сервер SQL Server и IPython Notebook)
1. Создайте виртуальную машину Azure с SQL Server и IPython Notebook.
2. Передача данных контейнер хранилища Azure tooan.
3. Предварительно обработайте и очистите данные (необязательно).
   
   а.  Предварительно обработайте и очистите данные в IPython Notebook из Azure.
   
       blobs.
   
   b.  При необходимости, преобразовывать toocleaned данных, в табличной форме.
   
   c.  Сохранить tooVM локальных файлов данных (ноутбук IPython работает на виртуальной Машине см. в локальные диски tooVM дисков).
4. Загрузите данные tooSQL сервера базы данных, на Виртуальной машине Azure.
   
   а.  TooSQL входа сервера виртуальной Машины.
   
   b.  Если данные еще не сохранены, скачайте файлы данных из Azure.
   
       storage container toolocal-VM folder.
   
   В.  Запустите среду SQL Server Management Studio.
   
   г)  Создайте базу данных и целевые таблицы.
   
   д.  Используйте одну из hello массового импорта данных hello tooload методы.
   
   f.  Если требуется соединение таблиц, создайте индексы tooexpedite соединения.
   
   > [!NOTE]
   > Быстрее загружать из размеров больших объемов данных, рекомендуется создавать секционированные таблицы и выполнить массовый импорт данных hello в параллельном режиме. Дополнительные сведения см. в разделе [параллельный импорт данных tooSQL секционированных таблиц](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Просмотрите данные и при необходимости создайте компоненты. Обратите внимание, что функции hello не toobe материализуются в таблицах базы данных hello. Только Примечание hello необходимый запрос toocreate их.
6. При необходимости выберите размер примера данных.
7. Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).
8. Hello чтения данных непосредственно из hello SQL Server с помощью hello [импорта данных] [ import-data] модуля. Необходимый запрос hello вставки, которая извлекает поля, создает компоненты и образцы данных, при необходимости непосредственно в hello [импорта данных] [ import-data] запроса.
9. Создайте простую последовательность операций эксперимента Машинного обучения Azure, начиная с отправленного набора данных.

## <a name="largedbtodb"></a>Сценарий\# №6. Большой набор данных в локальной базе данных SQL Server, загружаемый на сервер SQL Server в виртуальной машине Azure
![В локальной среде tooSQL больших баз данных SQL Server DB в Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Дополнительные ресурсы Azure: виртуальная машина Azure (сервер SQL Server и IPython Notebook)
1. Создайте виртуальную машину Azure с SQL Server и IPython Notebook.
2. Используйте одну из данных hello Экспорт данных hello tooexport методы toodump файлов SQL Server.
   
   > [!NOTE]
   > Если вы решите toomove все данные из базы данных в локальной среде hello, альтернативный (быстрее) метод toomove hello полный экземпляр базы данных toothe SQL Server в Azure. Пропустите hello действия tooexport данных, создание базы данных и загрузки и импорта данных toohello целевую базу данных и выполните hello альтернативный метод.
   > 
   > 
3. Отправьте контейнер хранилища tooAzure файлов дампа.
4. Загрузить hello данных tooa базы данных SQL Server на виртуальной машине Azure.
   
   а.  Toohello входа в систему виртуальной Машины SQL Server.
   
   b.  Загрузите файлы данных из папки локальной ВМ toohello контейнер хранилища Azure.
   
   c.  Запустите среду SQL Server Management Studio.
   
   г)  Создайте базу данных и целевые таблицы.
   
   д.  Используйте одну из hello массового импорта данных hello tooload методы.
   
   f.  Если требуется соединение таблиц, создайте индексы tooexpedite соединения.
   
   > [!NOTE]
   > Быстрее загружать большие объемы данных размеров параллельного создания секционированных таблиц и данных hello toobulk импорта. Дополнительные сведения см. в разделе [параллельный импорт данных tooSQL секционированных таблиц](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Просмотрите данные и при необходимости создайте компоненты. Обратите внимание, что функции hello не toobe материализуются в таблицах базы данных hello. Только Примечание hello необходимый запрос toocreate их.
6. При необходимости выберите размер примера данных.
7. Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).
8. Hello чтения данных непосредственно из hello SQL Server с помощью hello [импорта данных] [ import-data] модуля. Необходимый запрос hello вставки, которая извлекает поля, создает компоненты и образцы данных, при необходимости непосредственно в hello [импорта данных] [ import-data] запроса.
9. Создайте простую последовательность операций эксперимента Машинного обучения Azure, начиная с отправленного набора данных.

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a>Альтернативный способ toocopy всей базы данных из tooAzure SQL Server в локальной базе данных SQL
![Присоединение и отсоединение базы данных local DB tooSQL DB в Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Дополнительные ресурсы Azure: виртуальная машина Azure (сервер SQL Server и IPython Notebook)
tooreplicate hello всей базы данных SQL Server на виртуальной машине SQL Server, следует скопировать базу данных из одного tooanother расположения и сервера, при условии, что hello базы данных можно было временно отключить. Для этого в обозревателе объектов SQL Server Management Studio hello, или с помощью hello эквивалентные команды Transact-SQL.

1. Отсоединение базы данных hello в исходных папках hello. Дополнительные сведения см. в статье [Отсоединение базы данных](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).
2. В окне проводника Windows или командной строки Windows hello копирования отсоединенного файла базы данных или файлов и файла журнала или файлы toohello целевое расположение на виртуальной Машине SQL Server в Azure hello.
3. Присоедините hello копируются файлы toohello целевого экземпляра SQL Server. Дополнительные сведения см. в статье [Присоединение базы данных](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).

[Перенос базы данных путем отсоединения и присоединения (язык Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)

## <a name="largedbtohive"></a>Сценарий \# №7. Данные большого размера в локальных файлах, загружаемые в базу данных Hive в кластерах Azure HDInsight Hadoop
![Данные большого размера в локальных файлах для базы данных Hive][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a>Дополнительные ресурсы Azure: кластер Azure HDInsight Hadoop и виртуальная машина Azure (сервер IPython Notebook)
1. Создайте виртуальную машину Azure с сервером IPython Notebook.
2. Создайте кластер Azure HDInsight Hadoop.
3. Предварительно обработайте и очистите данные (необязательно).
   
   а.  Предварительно обработайте и очистите данные в IPython Notebook из Azure.
   
       blobs.
   
   b.  При необходимости, преобразовывать toocleaned данных, в табличной форме.
   
   c.  Сохранить tooVM локальных файлов данных (ноутбук IPython работает на виртуальной Машине см. в локальные диски tooVM дисков).
4. Передача данных контейнер по умолчанию toohello hello кластера Hadoop, выбранного в шаге hello 2.
5. Загрузить tooHive база данных в кластере Azure HDInsight Hadoop.
   
   а.  Войдите в toohello головного узла кластера Hadoop hello
   
   b.  Откройте hello командной строки Hadoop.
   
   c.  Введите каталог корневого куста hello командой `cd %hive_home%\bin` в Hadoop командной строки.
   
   d.  Выполнение hello запросы Hive toocreate к базе данных и таблиц и загрузки данных из таблиц tooHive хранилища больших двоичных объектов.
   
   > [!NOTE]
   > Если данные hello больших, пользователи могут создавать таблицу Hive hello с секциями. После этого пользователи могут использовать `for` цикл в hello командной строки Hadoop на hello головного узла tooload данных в таблицу Hive hello секционированы по секциям.
   > 
   > 
6. Просмотрите данные и при необходимости создайте компоненты в командной строке Hadoop. Обратите внимание, что функции hello не toobe материализуются в таблицах базы данных hello. Только Примечание hello необходимый запрос toocreate их.
   
   а.  Войдите в toohello головного узла кластера Hadoop hello
   
   b.  Откройте hello командной строки Hadoop.
   
   c.  Введите каталог корневого куста hello командой `cd %hive_home%\bin` в Hadoop командной строки.
   
   d.  Выполнять запросы Hive hello в Hadoop командной строки на головном узле данных hello tooexplore кластера Hadoop hello hello и создавать компоненты при необходимости.
7. При необходимости или требуемого, образец hello toofit данных в студии машинного обучения Azure.
8. Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).
9. Чтение данных hello непосредственно из hello `Hive Queries` с помощью hello [импорта данных] [ import-data] модуля. Необходимый запрос hello вставки, которая извлекает поля, создает компоненты и образцы данных, при необходимости непосредственно в hello [импорта данных] [ import-data] запроса.
10. Создайте простую последовательность операций эксперимента Машинного обучения Azure, начиная с отправленного набора данных.

## <a name="decisiontree"></a>Дерево принятия решений для выбора сценариев
- - -
Hello следующей диаграмме показаны описанных выше сценариях hello и hello Advanced Analytics процесса и технологии выборов, сделанных использующие tooeach hello перечислено сценариев. Обратите внимание, что может занять обработки данных, просмотра, конструируются и выборки поместите в одной или нескольких метод/среды--hello источника промежуточных данных, или целевых средах — и может выполняться последовательно по мере необходимости. Схема Hello только служит в качестве иллюстрации того, некоторые из возможных потоков и не предоставляет полное перечисление.

![Примеры сценариев с пошаговыми действиями процесса обработки и анализа данных][8]

### <a name="advanced-analytics-in-action-examples"></a>Практические примеры расширенного анализа
Пошаговые руководства машинного обучения Azure начала до конца, в которых используются hello Advanced Analytics процесса и технологии использования общих наборов данных см. в разделе:

* [Процесс обработки и анализа данных группы на практике: использование SQL Server](machine-learning-data-science-process-sql-walkthrough.md).
* [Процесс обработки и анализа данных группы на практике: использование кластеров HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md).

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
