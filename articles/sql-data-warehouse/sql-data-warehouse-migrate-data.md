---
title: "aaaMigrate вашей tooSQL данных хранилища данных | Документы Microsoft"
description: "Советы по переносу вашей tooAzure данных хранилища данных SQL для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a>Перенос данных
Данные из различных источников можно переместить в хранилище данных SQL с помощью различных инструментов.  Копировать ADF, SSIS и bcp можно все используемые tooachieve этой цели. Однако с увеличением hello объем данных следует подумать о Дробление hello процесса миграции данных в действия. Это предоставляет hello toooptimize возможности каждого шага для производительности и устойчивости tooensure переноса smooth данных.

Сценарии переноса простой hello Копировать ADF, SSIS и bcp сначала описаны в этой статье. Он затем изучить более детально как можно оптимизировать hello миграции.

## <a name="azure-data-factory-adf-copy"></a>Копирование с помощью фабрики данных Azure (ADF)
[ADF Copy][ADF Copy] входит в [фабрику данных Azure][Azure Data Factory]. Можно использовать копию ADF tooexport tooflat файлы данных, находящиеся в локальном хранилище tooremote неструктурированных файлов, хранящихся в хранилище больших двоичных объектов или непосредственно в хранилище данных SQL.

Если запускается данные в неструктурированные файлы, то необходимо сначала tootransfer его BLOB-объекта хранилища tooAzure перед запуском нагрузочного его в хранилище данных SQL. После hello данные передаются в хранилище больших двоичных объектов можно выбрать toouse [ADF копирования] [ ADF Copy] снова toopush hello данных в хранилище данных SQL.

PolyBase также позволяет высокой производительности загрузки данных hello. Однако в этом случае придется использовать два средства вместо одного. Если требуется hello наилучшей производительности с помощью PolyBase. Если требуется один интерфейс (и не больших объемов данных hello) ADF представляет решение этой задачи.


> 
> 

Головной по следующей статьей некоторые превосходная toohello [образцы ADF][ADF samples].

## <a name="integration-services"></a>Службы интеграции
Службы Integration Services (SSIS) — это мощное и гибкое средство загрузки данных, которое поддерживает сложные рабочие потоки, преобразование данных и разные параметры загрузки. Используйте перенос данных служб SSIS toosimply tooAzure или как часть более широкой миграции.

> [!NOTE]
> Службы SSIS можно экспортировать tooUTF-8 без отметки порядка байтов hello в файле hello. tooconfigure, это необходимо, с помощью hello производный столбец компонента tooconvert hello символьные данные в hello данных потока toouse hello 65001 UTF-8 кодовую страницу. После преобразования hello столбцы записи hello данных toohello неструктурированный файл назначения адаптера обеспечение 65001 также был выбран как hello кодовой страницы для файла hello.
> 
> 

Службы SSIS подключается tooSQL хранилища данных, так же, как он должен быть подключен tooa развертывания сервера SQL Server. Тем не менее подключениями потребуется toobe, используя диспетчер соединений ADO.NET. Следует также обратить внимание hello tooconfigure «Использование инструкции bulk insert при наличии» пропускная способность toomaximize параметр. См. toohello [адаптер назначения ADO.NET] [ ADO.NET destination adapter] toolearn статье Дополнительные об этом свойстве

> [!NOTE]
> Подключение tooAzure хранилище данных SQL с помощью OLE DB не поддерживается.
> 
> 

Кроме того, всегда есть возможность hello, что пакет может завершиться ошибкой из-за проблем с toothrottling или сети. Конструктор пакетов, их можно было возобновить в точке сбоя hello без возврат работы, выполненной до сбоя hello.

Дополнительные сведения можно найти hello [документации служб SSIS][SSIS documentation].

## <a name="bcp"></a>bcp
Программа bcp — средство командной строки, предназначенное для импорта и экспорта данных неструктурированных файлов. Во время экспорта можно выполнять преобразование. простой преобразования tooperform использовать tooselect запроса и преобразования данных hello. После экспорта hello неструктурированные файлы затем можно загрузить непосредственно в hello хранилище данных SQL hello целевой базы данных.

> [!NOTE]
> Часто бывает hello tooencapsulate смысл, экспортировать преобразований, использованной для данных в представлении в исходной системе hello. Это гарантирует, что логика hello сохраняется и hello процесса необходимо повторять.
> 
> 

Программа bcp обладает следующими преимуществами.

* Простота. команды bcp простой toobuild и выполнение
* Процесс загрузки можно повторять. Один раз экспортированного hello загрузки может оказаться выполняться любое количество раз

Программа bcp имеет следующие ограничения.

* Программа bcp работает только с табличными неструктурированными файлами. Программа bcp не работает с такими файлами, как XML или JSON.
* Возможности по преобразованию данных являются только ограниченный toohello этапе экспорта и просты по своей природе
* bcp не был адаптирован toobe надежным при загрузке данных через hello internet. Любой сетевой сбой приводит к ошибке загрузки.
* bcp зависит от схемы hello их присутствия в загрузки предыдущих toohello hello целевой базы данных

Дополнительные сведения см. в разделе [использовать bcp tooload данные в хранилище данных SQL][Use bcp tooload data into SQL Data Warehouse].

## <a name="optimizing-data-migration"></a>Оптимизация переноса данных
Процесс переноса данных с помощью SQLDW можно эффективно разделить на три этапа:

1. Экспорт исходных данных
2. Передача данных tooAzure
3. Загрузить в базу данных SQLDW целевой hello

Каждый шаг можно по отдельности оптимизированного toocreate процесса миграции надежной, повторно запустить и гибкой, позволяет повысить производительность на каждом шаге.

## <a name="optimizing-data-load"></a>Оптимизация загрузки данных
Просматривая их в обратном порядке для некоторое время; Hello самый быстрый способ tooload данных осуществляется через PolyBase. Оптимизация для загрузки процесса PolyBase помещает необходимые компоненты на предыдущих шагах, поэтому наиболее toounderstand это hello переднего плана. К ним относятся:

1. Кодирование файлов данных
2. Форматирование файлов данных
3. Размещение файлов данных

### <a name="encoding"></a>Кодирование
PolyBase требуется toobe файлы данных UTF-8 или UTF-16FE. 



### <a name="format-of-data-files"></a>Форматирование файлов данных
PolyBase требует наличия признака конца строки \n или новой строки. Файлы данных должны соответствовать toothis standard. Нет ограничений для признаков конца строки или столбца.

Вы получите toodefine каждый столбец в файле hello как часть в PolyBase внешней таблицы. Убедитесь, что все экспортированные столбцы являются обязательными и соответствия стандартам toohello необходимые типы hello.

Можно найти toohello [миграция схемы] статьи, сведения о поддерживаемых типах данных.

### <a name="location-of-data-files"></a>Размещение файлов данных
Хранилище данных SQL используются только данные tooload PolyBase из хранилища больших двоичных объектов. Следовательно hello данных необходимо сначала перенесены в хранилище больших двоичных объектов.

## <a name="optimizing-data-transfer"></a>Оптимизация переноса данных
Одна из самых медленных частей hello переноса данных — перенос hello tooAzure данных hello. Проблемой может стать не только пропускная способность сети, но и ее стабильная работа. По умолчанию tooAzure перенос данных превышает hello Интернет так hello возможность передачи ошибок могут быть достаточно. Однако этих ошибок может потребоваться повторно отправлять целиком или частично toobe данных.

К счастью, имеется несколько параметров tooimprove hello скорость и отказоустойчивость этого процесса:

### <a name="expressrouteexpressroute"></a>[ExpressRoute][ExpressRoute]
Вы можете с помощью tooconsider [ExpressRoute] [ ExpressRoute] toospeed копирование hello передачи. [ExpressRoute] [ ExpressRoute] предоставляет вам tooAzure частного подключения, подключения hello не передается по hello общедоступный Интернет. Это отнюдь не является обязательным этапом. Тем не менее, он будет повысить пропускную способность, при принудительной установке tooAzure данных из локальной или совместно используемой.

Здравствуйте, преимущества использования [ExpressRoute] [ ExpressRoute] являются:

1. Повышенная надежность
2. Более высокая скорость сети
3. Низкая задержка сети
4. Более высокая степень сетевой безопасности

[ExpressRoute] [ ExpressRoute] является полезным для некоторых сценариев; не только hello миграции.

Заинтересовались? Дополнительные сведения и ценах обратитесь по адресу hello [документации по ExpressRoute][ExpressRoute documentation].

### <a name="azure-import-and-export-service"></a>Служба импорта и экспорта Azure
Hello службы Azure импорта и экспорта является процесса передачи данных, предназначенных для больших (ГБ ++) toomassive (ТБ ++) передач данных в Azure. Он включает в себя записи вашей toodisks данных и доставку их tooan центр обработки данных Azure. Затем содержимое диска Hello будут загружены в хранилище BLOB-объектов Azure от вашего имени.

Высокоуровневый обзор процесса экспорта импорта hello выглядит следующим образом:

1. Настройка данных hello tooreceive контейнер хранилища больших двоичных объектов
2. Экспорт toolocal хранилище данных
3. Скопируйте hello данных too3.5 дюйма SATA II или III жестких дисков с помощью hello [средство импорта и экспорта Azure]
4. Создание задания импорта с помощью hello Azure импорта и экспорта службы, предоставляющей hello файлы журнала, созданные hello [средство импорта и экспорта Azure]
5. Переслать диски hello назначенный ЦОД Azure
6. Данные не переносятся tooyour контейнер хранилища больших двоичных объектов
7. Загрузка данных с помощью PolyBase SQLDW hello

### <a name="azcopyazcopy-utility"></a>Служебная программа [AZCopy][AZCopy]
Hello [AZCopy][AZCopy] программа — это мощный инструмент для получения данных передано в BLOB-объектов хранилища Azure. Она предназначена для небольших (МБ ++) toovery больших (ГБ ++) передачи данных. [AZCopy] был спроектированный tooprovide устойчивым повышению производительности при передаче данных tooAzure и поэтому отлично подходит для шага передачи данных hello. Один раз переносятся можно загрузить данные hello, используя PolyBase в хранилище данных SQL. Средство AZCopy можно также добавить в пакеты служб SSIS с помощью задания "Выполнить процесс".

toouse AZCopy, то сначала необходимо toodownload и установить его. Существует [рабочая версия][production version] и [пробная версия][preview version].

tooupload файл из файловой системы достаточно команды, аналогичной hello один ниже:

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

В целом процесс может выглядеть следующим образом.

1. Настройка хранилища Azure данные большого двоичного объекта контейнера tooreceive hello
2. Экспорт toolocal хранилище данных
3. AZCopy данных в контейнер хранилища больших двоичных объектов hello
4. Hello данные загружаются в хранилище данных SQL с помощью PolyBase

См. полную документацию по [AZCopy][AZCopy].

## <a name="optimizing-data-export"></a>Оптимизация экспорта данных
В дополнение к этому tooensuring соответствие требованиям toohello располагаются с PolyBase вы hello экспорта можно выполнять поиск экспорта hello toooptimize процесса hello данных tooimprove hello дальнейшей.



### <a name="data-compression"></a>Сжатие данных
PolyBase может читать данные, сжатые с помощью gzip. Если вы не можете toocompress toogzip файлов данных, то можно будет свести к минимуму hello объем данных, отправленных по сети hello.

### <a name="multiple-files"></a>Разделение на несколько файлов
Разбиение большой таблицы на несколько файлов не только tooimprove Экспорт скорости, также позволяет передавать re-startability и hello общей управляемости hello данных один раз в хранилище больших двоичных объектов hello. Одно из hello множество удобных функций PolyBase является будет читать все hello файлы в папку и рассматривать его как одна таблица. Именно поэтому файлов hello tooisolate хорошей идеей для каждой таблицы в отдельную папку.

PolyBase также поддерживает так называемую функцию рекурсивного перебора папок. Эту функцию можно использовать toofurther улучшения организации hello вашей tooimprove экспортированных данных на управление данными.

в разделе toolearn Дополнительные сведения о загрузке данных с помощью PolyBase, [PolyBase используйте tooload данных в хранилище данных SQL][Use PolyBase tooload data into SQL Data Warehouse].

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о миграции см. в разделе [перенести tooSQL вашего решения хранилища данных][Migrate your solution tooSQL Data Warehouse].
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
