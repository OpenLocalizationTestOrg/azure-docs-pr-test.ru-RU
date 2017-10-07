---
title: "aaaInstall адаптер StorSimple для SharePoint | Документы Microsoft"
description: "Описывает способ tooinstall и настроить или удалить hello адаптера StorSimple для SharePoint в ферме серверов SharePoint."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 9a7347232fb80156d93212e6382cdd4fab98a2d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-hello-storsimple-adapter-for-sharepoint"></a>Установка и настройка hello адаптера StorSimple для SharePoint
## <a name="overview"></a>Обзор
Hello адаптер StorSimple для SharePoint — это компонент, который позволяет предоставлять гибкий хранилища Microsoft Azure StorSimple и для ферм серверов tooSharePoint защиты данных. Можно использовать адаптер hello toomove содержимое больших двоичных объектов (BLOB) SQL Server hello баз данных контента toohello Microsoft Azure StorSimple гибридной облачной запоминающее устройство.

Hello адаптер StorSimple для SharePoint функционирует как поставщик удаленного хранилища больших Двоичных объектов и использует hello toostore функции удаленного хранилища больших двоичных ОБЪЕКТОВ SQL Server неструктурированное содержимое SharePoint (в виде hello больших двоичных объектов) на файловом сервере, поддерживаемый устройства StorSimple.

> [!NOTE]
> Hello адаптер StorSimple для SharePoint поддерживает SharePoint Server 2010 удаленного хранилища больших Двоичных объектов. Он не поддерживает внешнее хранилище больших двоичных объектов SharePoint Server 2010 (EBS).


* hello toodownload адаптер StorSimple для SharePoint, перейдите в слишком[адаптер StorSimple для SharePoint] [ 1] в hello центра загрузки Майкрософт.
* Сведения о планировании и RBS ограничения go слишком[Выбор toouse RBS в SharePoint 2013] [ 2] или [план для RBS (SharePoint Server 2010)] [3].

Hello остальная часть в этом обзоре кратко описывается роль hello hello адаптер StorSimple для SharePoint и емкости SharePoint hello и ограничения производительности, что следует учитывать перед установкой и настройкой адаптера hello. После просмотра этих сведений перейдите слишком[адаптера StorSimple для SharePoint](#storsimple-adapter-for-sharepoint-installation) toobegin Настройка адаптера hello.

### <a name="storsimple-adapter-for-sharepoint-benefits"></a>Преимущества адаптера StorSimple для SharePoint
На сайте SharePoint содержимое хранится в виде неструктурированных данных больших двоичных объектов в одной или нескольких базах данных содержимого. По умолчанию эти базы данных размещаются на компьютерах, на которых работает SQL Server и расположены в ферме серверов SharePoint hello. Большие двоичные объекты могут быстро увеличиваться в размерах, занимая огромный объем пространства в локальном хранилище. По этой причине может потребоваться toofind хранилища на другой, менее затратное решение. SQL Server предоставляет технологию удаленного хранилища больших Двоичных объектов, позволяет хранить содержимое больших двоичных ОБЪЕКТОВ в hello файловой системы за пределами базы данных SQL Server hello. Благодаря RBS большие двоичные объекты могут находиться в hello файловой системы на компьютере hello, на котором выполняется SQL Server или могут храниться в файловой системе hello на другой компьютер.

RBS необходимо использовать поставщик RBS, например hello адаптер StorSimple для SharePoint, tooenable RBS в SharePoint. Hello адаптер StorSimple для SharePoint работает с поставщиком RBS, позволяя перемещения сервера tooa большие двоичные объекты включаются в резервную копию hello система Microsoft Azure StorSimple. Microsoft Azure StorSimple сохраняет данные больших двоичных ОБЪЕКТОВ hello локально или в облаке hello в зависимости от использования. Большие двоичные объекты, которые очень активны локально находятся (который обычно ссылается tooas уровня 1 или горячим данным). Менее активных данных и архивные данные находятся в облаке hello. После включения RBS в базе данных контента, любое новое содержимое больших двоичных ОБЪЕКТОВ, созданное в SharePoint хранится на устройстве StorSimple hello и не в базе данных содержимого hello.

Реализация Microsoft Azure StorSimple Hello RBS предоставляет следующие преимущества hello:

* Путем перемещения больших двоичных ОБЪЕКТОВ содержимого tooa отдельный сервер можно сократить время загрузки запроса hello на SQL Server, что может повысить скорость реагирования SQL Server. 
* Azure StorSimple использует дедупликацию и сжатие размер tooreduce данных.
* Azure StorSimple предоставляет защиту данных в форме hello локальных и облачных моментальных снимков. Кроме того Если поместить саму базу данных hello на устройстве StorSimple hello, можно выполнять архивацию hello базы данных контента и больших двоичных объектов совместно сбоям способом. (Перемещение устройства toohello hello содержимого базы данных поддерживается только для устройства серии StorSimple 8000 hello. Эта функция не поддерживается для ряда hello 5000 или 7000.)
* Azure StorSimple включает функции аварийного восстановления, включая отработку отказа, восстановление файлов и томов (включая тестовое восстановление) и быстрое восстановление данных.
* Программное обеспечение восстановления данных, таких как Kroll Ontrack PowerControls, можно использовать с моментальными снимками StorSimple восстановления на уровне элементов tooperform большого двоичного ОБЪЕКТА данных содержимого SharePoint. (Это программное обеспечение восстановления данных приобретается отдельно.)
* Hello адаптер StorSimple для SharePoint подключается портал hello центра администрирования SharePoint, позволяя toomanage всего решения SharePoint из центрального расположения.

Перемещение больших двоичных ОБЪЕКТОВ содержимого toohello файловая система может предоставить дополнительную экономию расходов и преимущества. Например использование RBS может уменьшить hello потребность в дорогих хранилищах уровня 1 и за счет уменьшения hello содержимого базы данных, RBS может снизить hello количество баз данных, необходимых в ферме серверов SharePoint hello. Тем не менее других факторов, таких как максимальный размер базы данных и hello объем содержимого, без поддержки RBS, могут также влиять на требования к хранилищу. Дополнительные сведения о затратах hello и преимущества использования RBS см. в разделе [план для RBS (SharePoint Foundation 2010)] [ 4] и [Выбор toouse RBS в SharePoint 2013] [ 5].

### <a name="capacity-and-performance-limits"></a>Ограничения емкости и производительности
Прежде чем рассматривать использование RBS в решении SharePoint, должны учитывать hello тестирование производительности и ограничения емкости SharePoint Server 2010 и SharePoint Server 2013 и как эти ограничения связаны tooacceptable производительности. Дополнительные сведения см. в статье [Ограничения, связанные с программным обеспечением, в SharePoint 2013](https://technet.microsoft.com/library/cc262787.aspx).

Просмотрите следующие hello перед настройкой RBS:

* Убедитесь, что общий размер содержимого (hello размер базы данных содержимого) плюс размер hello любой связанный во внешних хранилищах больших двоичных объектов не превышает предельный размер hello RBS, поддерживаемого SharePoint hello, hello. Он составляет 200 Гб. 
  
    **toomeasure базы данных содержимого и размер большого двоичного ОБЪЕКТА**
  
  1. Выполните этот запрос на hello WFE центра администрирования. Запустите консоль управления SharePoint hello, а затем введите следующие команды Windows PowerShell tooget размер hello баз данных содержимого hello hello:
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      Этот шаг возвращает размер hello hello базы данных содержимого на диске hello.
  2. Выполните одну из hello, следующие запросы SQL в SQL Management Studio полю hello SQL server, все базы данных содержимого и добавить номер toohello hello результат, полученный на шаге 1.
     
     Для баз данных содержимого SharePoint 2013 введите:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     Для баз данных содержимого SharePoint 2010 введите:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     Этот шаг получает hello размер больших двоичных объектов, которые были внешне выводятся hello.
* Рекомендуется хранить все BLOB-ОБЪЕКТОВ и базы данных содержимого локально на устройстве StorSimple hello. устройство StorSimple Hello является двухузлового кластера для обеспечения высокой доступности. Размещение баз данных содержимого hello и больших двоичных объектов на устройстве StorSimple hello обеспечивает высокий уровень доступности.
  
    Используйте традиционные SQL Server миграции лучшие методики toomove hello базы данных содержимого toohello устройства StorSimple. Перемещение базы данных hello, только после содержимого больших двоичных ОБЪЕКТОВ из базы данных hello перемещенный toohello общую папку через RBS. При выборе устройства toomove hello базы данных контента toohello StorSimple рекомендуется настроить хранилище hello базы данных контента на устройстве hello как первичный том.
* В Microsoft Azure StorSimple, если с помощью многоуровневых томов нет возможности tooguarantee, содержимое хранится локально на устройстве StorSimple hello будут многоуровневого tooMicrosoft Облачное хранилище Azure. Следовательно, мы рекомендуем использовать локально закрепленные тома StorSimple в сочетании с SharePoint RBS. Это позволит гарантировать остается локально на устройстве StorSimple hello содержимого больших двоичных ОБЪЕКТОВ и не перемещать tooMicrosoft Azure.
* Если hello баз данных контента не сохраняются на устройстве StorSimple hello, используйте традиционные SQL Server высокой доступности передовые методы, которые поддерживают RBS. Кластеризация SQL Server поддерживает RBS, а зеркальное отображение SQL Server не поддерживает. 

> [!WARNING]
> Если RBS не включен, не рекомендуется перемещение устройства StorSimple toohello hello базы данных содержимого. Эта конфигурация не тестировалась.

## <a name="storsimple-adapter-for-sharepoint-installation"></a>Адаптер StorSimple для SharePoint
Перед установкой hello адаптера StorSimple для SharePoint, необходимо настроить устройство StorSimple hello и убедитесь, что hello ферма серверов SharePoint и создание экземпляров SQL Server выполнении всех предварительных условий. Этот учебник описывает требования к конфигурации, а также процедуры установки и обновления hello адаптера StorSimple для SharePoint.

## <a name="configure-prerequisites"></a>Настройка необходимых компонентов
Перед установкой hello адаптера StorSimple для SharePoint, убедитесь, что устройство StorSimple hello, ферма серверов SharePoint и создание экземпляров SQL Server соответствуют hello следующие необходимые условия.

### <a name="system-requirements"></a>Требования к системе
Hello адаптер StorSimple для SharePoint работает с hello оборудования и программного обеспечения:

* Поддерживаемые операционные системы — Windows Server 2008 R2 с пакетом обновления 1, Windows Server 2012 и Windows Server 2012 R2.
* Поддерживаемые версии SharePoint — SharePoint Server 2010 и SharePoint Server 2013.
* Поддерживаемые версии SQL Server — SQL Server 2008 Enterprise Edition, SQL Server 2008 R2 Enterprise Edition и SQL Server 2012 Enterprise Edition.
* Поддерживаемые устройства StorSimple — устройства StorSimple серий 8000, 7000 и 5000.

### <a name="storsimple-device-configuration-prerequisites"></a>Предварительные требования для настройки устройства StorSimple
устройство StorSimple Hello является блочным устройством, для которого требуется файловый сервер, на котором могут размещаться данные hello. Мы рекомендуем использовать отдельный сервер, а не существующий сервер из фермы SharePoint hello. Этот файловый сервер должен быть на hello же локальной сети (LAN) как hello компьютер SQL Server, размещены hello содержимого базы данных.

> [!TIP]
> * При настройке фермы SharePoint для обеспечения высокой доступности, следует также развернуть hello файлового сервера для обеспечения высокой доступности.
> * Если hello базы данных контента не сохраняются на устройстве StorSimple hello, используйте традиционные высокого уровня доступности рекомендации, которые поддерживают RBS. Кластеризация SQL Server поддерживает RBS, а зеркальное отображение SQL Server не поддерживает. 


Убедитесь, что, устройства StorSimple настроена правильно и что соответствующие тома toosupport развертывания SharePoint настроены и доступны с компьютера с SQL Server. Go слишком[развертывание локального устройства StorSimple](storsimple-8000-deployment-walkthrough-u2.md) Если вы еще не развертывания и настройки устройства StorSimple. Обратите внимание, hello IP-адрес устройства StorSimple hello; они потребуются во время адаптера StorSimple для SharePoint.

Кроме того убедитесь, что toobe тома, hello, используемые для перемещения больших двоичных ОБЪЕКТОВ отвечает hello следующие требования:

* Hello том должен быть отформатирован размер кластера 64 КБ.
* Веб-интерфейса (WFE) и серверов приложений должен быть томом hello tooaccess доступ по пути соглашения об универсальных именах (UNC).
* Ферма серверов SharePoint Hello должен быть томом настроенных toowrite toohello.

> [!NOTE]
> После установки и настройки адаптера hello перемещения всех больших двоичных ОБЪЕКТОВ должен проходить через устройство StorSimple hello (hello устройства будут представлять tooSQL hello томов сервера и управлять ими hello уровней хранилища). Другие целевые устройства для перемещения больших двоичных объектов не поддерживаются.


Если план toouse диспетчера моментальных снимков StorSimple tootake моментальные снимки hello больших двоичных ОБЪЕКТОВ и данных, базы данных будет убедиться, что tooinstall диспетчера моментальных снимков StorSimple на сервере базы данных hello, чтобы можно было использовать hello tooimplement служба модуля записи SQL hello теневого копирования томов Windows Служба (томов VSS).

> [!IMPORTANT]
> Диспетчер моментальных снимков StorSimple не поддерживает hello модуля записи VSS SharePoint и не может делать моментальные снимки приложений данных SharePoint. В сценарии SharePoint диспетчер моментальных снимков StorSimple предоставляет только отказоустойчивые резервные копии.


## <a name="sharepoint-farm-configuration-prerequisites"></a>Предварительные требования для настройки фермы SharePoint
Убедитесь, что ферма серверов SharePoint настроена правильно, как описано ниже.

* Убедитесь, что ферма серверов SharePoint в рабочем состоянии и проверьте hello ниже:
* Все SharePoint WFE и серверов приложений, зарегистрированные в ферме hello выполняются и можно установить связь с hello сервера, на котором будет устанавливаться hello адаптера StorSimple для SharePoint.
* Hello служба таймера SharePoint (SPTimerV3 или SPTimerV4) запущена на каждом веб-сервере и сервере приложений.
* Hello служба таймера SharePoint и пул приложений IIS hello которых hello сайт работает центр администрирования SharePoint права администратора.
* Убедитесь, что конфигурация усиленной безопасности Internet Explorer (IE ESC) отключена. Выполните эти шаги toodisable IE ESC.
  
  1. Закройте все экземпляры Internet Explorer.
  2. Запустите диспетчер сервера hello.
  3. Hello левой панели щелкните **локального сервера**.
  4. На hello правой панели рядом слишком**конфигурация усиленной безопасности Internet Explorer**, нажмите кнопку **на**.
  5. В разделе **Администраторы** нажмите **Выкл.**
  6. Нажмите кнопку **ОК**.

## <a name="remote-blob-storage-rbs-prerequisites"></a>Необходимые компоненты удаленного хранилища больших двоичных объектов (RBS)
Убедитесь, что используется поддерживаемая версия SQL Server. Только hello поддерживаются следующие версии поддерживаются toouse RBS:

* SQL Server 2008 Enterprise Edition
* SQL Server 2008 R2 Enterprise Edition
* SQL Server 2012 Enterprise Edition

Большие двоичные объекты можно переместить только те тома, которые hello устройство StorSimple предоставляет tooSQL сервера. Другие целевые устройства для перемещения больших двоичных объектов не поддерживаются.

После завершения всех необходимых шагов go слишком[hello Установка адаптера StorSimple для SharePoint](#install-the-storsimple-adapter-for-sharepoint).

## <a name="install-hello-storsimple-adapter-for-sharepoint"></a>Установка hello адаптера StorSimple для SharePoint
Используйте следующие шаги tooinstall hello адаптера StorSimple для SharePoint hello. При переустановке программного обеспечения hello. в разделе [обновить или переустановить hello адаптера StorSimple для SharePoint](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint). Hello время, необходимое для установки hello зависит от hello общее число баз данных SharePoint в ферме серверов SharePoint.

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a>Настройка RBS
После установки hello адаптера StorSimple для SharePoint, настройте RBS, как описано в hello после процедуры.

> [!TIP]
> Адаптер StorSimple для SharePoint Hello подключается к странице центра администрирования SharePoint hello, чтобы разрешить toobe RBS включены или отключены в каждой базе данных контента в ферме SharePoint hello. Тем не менее Включение или отключение RBS в базе данных контента hello вызывает сброс IIS, что в зависимости от конфигурации фермы, может ненадолго прервать доступность hello hello SharePoint веб-интерфейса (WFE). (Факторы, такие как использование hello подсистемы балансировки нагрузки для интерфейсного веб, текущая рабочая нагрузка сервера hello и т. д., могут ограничить или устранить это прерывание). tooprotect пользователей от прерывания, корпорация Майкрософт рекомендует включать или отключать RBS только во время запланированного обслуживания.


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a>Настройка сбора мусора
При удалении объектов с сайта SharePoint, они не удаляются автоматически из тома хранилища RBS hello. Вместо этого асинхронный, фоновая программа обслуживания удаляет потерянные большие двоичные объекты из хранилища файлов hello. Системные администраторы могут запланировать toorun этот процесс, периодически или они могут запускать его при необходимости.

Программа обслуживания (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) автоматически устанавливается на всех интерфейсных веб-серверах SharePoint и серверах приложений при включении RBS. Программа Hello установлена в следующие расположения hello: *загрузочный диск*: 10.50\Maintainer\ \Program Files\Microsoft удаленного хранилища BLOB-данных SQL

Сведения о настройке и использовании программы обслуживания hello см. в разделе [обслуживание RBS в SharePoint Server 2013][8].

> [!IMPORTANT]
> Hello программа обслуживания RBS является ресурсоемкой. Следует планировать ее toorun только во время периодов низкий уровень активности на ферме SharePoint hello.


### <a name="delete-orphaned-blobs-immediately"></a>Немедленное удаление потерянных больших двоичных объектов
Если необходимо немедленно toodelete потерянные большие двоичные объекты можно использовать hello, следуйте инструкциям. Обратите внимание, что эти инструкции являются примером как это можно сделать в среде SharePoint 2013 с hello следующие компоненты:

* Имя базы данных содержимого Hello — WSS_Content.
* имя SQL Server Hello — SHRPT13 SQL12\SHRPT13.
* Имя веб-приложения Hello — SharePoint — 80.

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-hello-storsimple-adapter-for-sharepoint"></a>Обновление или переустановка hello адаптера StorSimple для SharePoint
Используйте следующие процедуры tooupgrade SharePoint server hello и переустановка адаптера StorSimple для SharePoint или toosimply обновления или переустановки адаптера hello в существующую ферму серверов SharePoint.

> [!IMPORTANT]
> Просмотрите следующие сведения, прежде чем tooupgrade hello программного обеспечения SharePoint и/или обновление или переустановка hello адаптера StorSimple для SharePoint:
> 
> * Все файлы, перемещенные ранее хранилища tooexternal СДРес будут не будут доступны, пока закончится переустановка hello и hello функция RBS не будет включена снова. пользователь toolimit влияние, выполните обновление или переустановку во время запланированного обслуживания.
> * Hello время, необходимое для hello обновления/переустановки, зависит от hello общее число баз данных SharePoint в ферме серверов SharePoint hello.
> * После завершения обновления hello/переустановки необходимо tooenable RBS для баз данных контента hello. Дополнительные сведения см. в разделе [Настройка RBS](#configure-rbs).
> * Если RBS настраивается для фермы SharePoint с очень большим числом баз данных (более 200), hello **центра администрирования SharePoint** страницы может истечь. В этом случае обновите страницу приветствия. Это не влияет на процесс настройки hello.


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a>Удаление адаптера StorSimple для SharePoint
Hello следующие процедуры описывают, как toomove hello большие двоичные объекты обратно toohello баз данных содержимого SQL Server, а затем удалите hello адаптера StorSimple для SharePoint. 

> [!IMPORTANT]
> У вас есть toomove hello большие двоичные объекты задней toohello баз данных содержимого перед удалением программное обеспечение адаптера hello.


### <a name="before-you-begin"></a>Перед началом работы
Соберите следующую информацию, прежде чем перемещать данные hello резервное toohello баз данных содержимого SQL Server и начать процесс удаления адаптера hello hello.

* имена всех баз данных hello, для которых включен RBS Hello
* UNC-путь Hello hello настроить хранилище больших двоичных ОБЪЕКТОВ

### <a name="move-hello-blobs-back-toohello-content-databases"></a>Перемещение баз данных содержимого задней toohello hello больших двоичных объектов
Перед удалением hello адаптера StorSimple для SharePoint, необходимо перенести все hello больших двоичных объектов, которые были во внешних хранилищах задней toohello баз данных содержимого SQL Server. При попытке hello toouninstall адаптера StorSimple для SharePoint до перемещения всех hello большие двоичные объекты задней toohello баз данных содержимого вы увидите следующие предупреждающее сообщение hello.

![Предупреждение](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="toomove-hello-blobs-back-toohello-content-databases"></a>toomove hello большие двоичные объекты задней toohello баз данных содержимого
1. Загрузите каждый из объектов внешне выводятся hello.
2. Откройте hello **центра администрирования SharePoint** и перейдите в слишком**параметры системы**.
3. В разделе **Azure StorSimple** щелкните **Configure StorSimple Adapter** (Настроить адаптер StorSimple).
4. На hello **настроить адаптер StorSimple** щелкните hello **отключить** расположенную под каждой из баз данных содержимого hello, что требуется tooremove из внешнего хранилища BLOB-ОБЪЕКТОВ. 
5. Удалите объекты hello из SharePoint и затем снова отправьте их.

Кроме того, можно использовать hello Microsoft` RBS Migrate()` командлет PowerShell, включенный в SharePoint. Дополнительные сведения см. в статье о [переносе содержимого в RBS и из RBS](https://technet.microsoft.com/library/ff628255.aspx).

После перемещения базы данных контента задней toohello hello большие двоичные объекты go toohello следующий шаг: [удаления адаптера hello](#uninstall-the-adapter).

### <a name="uninstall-hello-adapter"></a>Удаление адаптера hello
После перемещения hello большие двоичные объекты задней toohello содержимого баз данных SQL Server, используйте одну из hello следующие параметры toouninstall hello адаптера StorSimple для SharePoint.

#### <a name="toouse-hello-installation-program-toouninstall-hello-adapter"></a>hello toouse hello установки программы toouninstall адаптера
1. Используйте учетную запись с toolog права администратора на сервера toohello веб-интерфейса (WFE).
2. Дважды щелкните hello адаптера StorSimple для SharePoint установщика. запускает приветствия мастера установки.
   
    ![Мастер установки](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. Щелкните **Далее**. Появится следующая страница приветствия.
   
    ![Мастер установки: страница удаления](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. Нажмите кнопку **удалить** процесс удаления tooselect hello. Появится следующая страница приветствия.
   
    ![Мастер установки: страница подтверждения](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. Нажмите кнопку **удалить** tooconfirm hello удаления. Появится следующая страница хода выполнения Hello.
   
    ![Мастер установки: страница хода выполнения](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. По завершении удаления hello появится последняя страница приветствия. Нажмите кнопку **Готово** tooclose приветствия мастера установки.

#### <a name="toouse-hello-control-panel-toouninstall-hello-adapter"></a>toouse hello панели управления toouninstall hello адаптера
1. Откройте панель управления hello и нажмите кнопку **программы и компоненты**.
2. Выберите **Адаптер StorSimple для SharePoint** и щелкните **Удалить**.

## <a name="next-steps"></a>Дальнейшие действия
[Узнайте больше о StorSimple](storsimple-overview.md).

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx
