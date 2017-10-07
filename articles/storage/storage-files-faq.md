---
title: "вопросы и ответы о хранилища Azure File aaaFrequently | Документы Microsoft"
description: "Найдите ответы на вопросы и ответы о хранилища Azure File toofrequently."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: ecd685b3094f51e998bbf5dd0567a20732757015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Часто задаваемые вопросы о хранилище файлов Azure

## <a name="general"></a>Общие сведения
* **В. Что такое хранилище файлов Azure?**  
   
    Хранилище файлов Azure — распределенная файловая система в Azure. Он предоставляет интерфейс протокола SMB, который позволяет пользователям toomount hello хранилища native общей поддерживает виртуальные машины Azure или на локальном компьютере.

* **В. В чем заключается удобство хранилища файлов Azure?**  
   
    Хранилище файлов Azure предоставляет доступ к общим данным между несколькими виртуальными машинами и платформами. См. слишком[хранилище почему файлов Azure может оказаться полезным](storage-files-introduction.md#why-azure-file-storage-is-useful).

* **В. Когда следует использовать файлы Azure, BLOB-объекты Azure и диски Azure?**  
   
    Microsoft Azure предоставляет несколько способов toostore и просматривать данные в облако hello.  
   
    Хранилище Azure файла — предоставляет интерфейс SMB, клиентские библиотеки и интерфейс REST, который позволяет легко доступ из любого места toostored файлы.  
   
    Azure BLOB-объектов — предоставляет клиентские библиотеки и интерфейс REST, который позволяет toobe неструктурированные данные сохраняются и становятся доступными при массовом масштабировании в блочных больших двоичных объектов.  
   
    Данных Azure диски — предоставляет клиентские библиотеки и интерфейс REST, который позволяет toobe данных постоянно сохраняются и становятся доступными из подключенный виртуальный жесткий диск.  
   
    Дополнительные сведения о [Deciding при toouse больших двоичных объектов Azure, файлов Azure и дисков данных Azure](storage-decide-blobs-files-disks.md)

* **В. Как начать работу с хранилищем файлов Azure?**  
   
    Для начала создайте общую папку Azure. Можно создать общих ресурсов Azure с помощью портала Azure, командлеты PowerShell хранилища Azure hello, клиентских библиотек хранилища Azure hello или hello API REST хранилища Azure. В этом учебнике вы узнаете:

    * [Узнайте, как предоставить доступ toocreate файлов Azure с помощью портала hello](storage-file-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Узнайте, как предоставить доступ toocreate файлов Azure с помощью Powershell](storage-file-how-to-create-file-share.md#create-file-share-through-powershell)
    * [Узнайте, как предоставить доступ toocreate файлов Azure с использованием интерфейса CLI](storage-file-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **В. Какие репликации поддерживаются хранилищем файлов Azure?**  
   
    Сейчас хранилище файлов Azure поддерживает только локально избыточное хранилище и геоизбыточное хранилище. Мы планируем toosupport RA-GRS, но существует еще не tooshare временной шкалы.

## <a name="security-authentication-and-access-control"></a>Безопасность, проверка подлинности и управление доступом

* **В. Что такое файлы tooaccess различными способами, в хранилище файлов Azure?**
    
    Можно подключить hello общую папку на локальном компьютере с использованием протокола SMB 3.0 или использовать средства, такие как [обозреватель хранилищ](http://storageexplorer.com/) tooaccess файлы в папке файла. Из своего приложения можно использовать клиентских библиотек хранилища, API-интерфейс REST или Powershell tooaccess файлов в файле Azure общей папки.

* **В. Как предоставить доступ tooa конкретный файл в редакторе веб-браузер**
    
    SAS позволяет создавать маркеры с определенными разрешениями, действующими в течение указанного периода. Например можно создать токен с определенного файла tooa доступ только для чтения за определенный период времени. Любой пользователь, обладающий этот URL-адрес можно получить доступ к hello файлу напрямую из любого браузера, поскольку он является допустимым. Ключи SAS можно легко создать с помощью пользовательского интерфейса, например обозревателя хранилищ.

* **В. Это возможно toospecify только для чтения или только для записи разрешения для папок в общей папке hello?**
    
    Этот уровень контроля над разрешениями нет, если подключить hello общую папку через SMB. Тем не менее этого можно добиться путем создания подписи общего доступа (SAS) через hello REST API или клиентские библиотеки.  

* **В. Как включить шифрование на стороне сервера для хранилища файлов Azure?**

    [Шифрование на стороне сервера](storage-service-encryption.md) для хранилища файлов Azure общедоступно во всех регионах и общедоступных и национальных облаках. Вы можете включить шифрование на стороне сервера для хранилища файлов Azure с помощью [портала Azure](https://portal.azure.com/), [API поставщика ресурсов службы хранилища Microsoft Azure](/rest/api/storagerp/storageaccounts), [Azure PowerShell](https://msdn.microsoft.com/library/azure/mt607151.aspx) или [интерфейса командной строки Azure](storage-azure-cli.md).
    
    После включения SSE на хранилища Azure File, все новые данные, записанные toohello хранения файлов в этой учетной записи хранения будут автоматически шифруются. Эта функция доступна для всех новых данных записаны tooexisting или новые общие папки в существующую или новую учетную запись хранилища. Включение этой функции не требует дополнительной оплаты. Дополнительные сведения о [как tooenable SSE на хранилища Azure File](storage-service-encryption.md).

* **В. Поддерживает ли хранилище файлов Azure проверку подлинности на основе Active Directory?**
   
    Сейчас мы не поддерживаем проверку подлинности на основе AD и списки управления доступом, но запросы на добавление этих функций включены в наш список. На данном этапе hello ключи учетной записи хранилища Azure, используется tooprovide проверки подлинности toohello общей папки. Мы предлагаем обходной путь, с помощью подписи коллективного доступа (SAS) через hello API-интерфейса REST или hello клиентских библиотек. SAS позволяет создавать маркеры с определенными разрешениями, действующими в течение указанного периода. Например можно создать токен с доступом только для чтения tooa данного файла и срока действия 10 минут. Любой пользователь, обладающий этот маркер, поскольку он является допустимым имеет доступ только для чтения файл toothat эти 10 минут.
   
    SAS поддерживается только через API-интерфейса REST или клиент библиотеки hello. При подключении hello общую папку через протокол SMB hello нельзя использовать SAS toodelegate доступа tooits содержимое. 
    
* **В. Что такое поддерживается для хранилища Azure File политики соответствия требованиям данных hello**

   Хранилище файлов Azure работает на hello архитектуру хранилища, как другие хранилища службы в хранилище Azure и применяет hello же политики соответствия требованиям данных. Дополнительные сведения о соответствии данных хранилища Azure можно загрузить и ссылаться слишком[защиты данных Microsoft Azure документа](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).

## <a name="on-premises-access"></a>Локальный доступ

* **У меня есть toouse хранилища Azure ExpressRoute tooconnect tooAzure файла от локальной виртуальной Машины Q.Do?**
   
    Нет. Если у вас нет ExpressRoute, по-прежнему доступны hello общей папки из локальной, пока у вас есть порт 445 (TCP-исходящий) открыт для доступа к Интернету. Но при желании вы можете работать с хранилищем файлов Azure через ExpressRoute.

* **В. Как подключить общую папку Azure на локальном компьютере?** 
    
    Можно подключить hello общую папку через протокол SMB hello, при условии, что открыт порт 445 (TCP-исходящий) и поддерживает протокол SMB 3.0 hello клиент (например, вы используете Windows 10 или Windows Server 2012). Обратитесь с портом hello поставщика toounblock локального поставщика услуг Интернета. В промежуточном hello, можно просматривать файлы с помощью [обозреватель хранилищ](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).


## <a name="billing-and-pricing"></a>Выставление счетов и цены
* **В. Hello сетевой трафик между Виртуальной машине Azure и число файлов общего ресурса как внешнюю полосу пропускания, которая зачисляется toohello подписки?**
   
    Если общая папка hello и виртуальной Машины находятся в hello же регионе Azure hello трафик между ними не взимается. Если они находятся в разных регионах, hello трафик между ними будет взиматься как внешнюю полосу пропускания.

## <a name="backup"></a>Резервное копирование

* **В. Как создать резервную копию общей папки, расположенной в хранилище файлов Azure?**
    
    Вы можете воспользоваться AzCopy, RoboCopy или сторонним средством архивации, с помощью которого можно создать резервную копию подключенной общей папки. Ожидается, что toohave моментальные снимки tootake hello возможности файловых ресурсов в hello ближайшее будущее; будет toouse могут совместно использовать файл Azure toobackup этой функции.

## <a name="performance"></a>Производительность

* **В. Каковы ограничения масштабирования hello хранилища файлов Azure?**
    Дополнительные сведения о целевых показателях масштабируемости и производительности хранилища файлов Azure см. в статье [Целевые показатели масштабируемости и производительности службы хранилища Azure](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).

* **В. Мои производительности замедлялось при попытке toounzip файлы в хранилище файлов Azure. Что делать?**
    
    tootransfer большого числа файлов в хранилище файлов Azure, мы рекомендуем использовать AzCopy (Windows, предварительный просмотр для Linux и Unix) или Azure Powershell, как эти средства оптимизированы для переноса по сети.

* **В. Том, что было исправлений выпущены toofix проблемой привести к снижению производительности хранилища Azure File?**
    
    группа Windows Hello недавно выпустила исправление toofix проблему снижения производительности при hello клиент обращается к хранилища Azure File с Windows 8.1 или Windows Server 2012 R2. Для получения дополнительной информации обратитесь извлечение hello связанные статья БАЗЫ знаний [снижение производительности при доступе к хранилища Azure File с Windows 8.1 или Server 2012 R2](https://support.microsoft.com/kb/3114025).

## <a name="features-and-interoperability-with-other-services"></a>Функции и взаимодействие с другими службами
* **В. — «Файловый ресурс-свидетель» для отказоустойчивого кластера, один из hello варианты использования для хранения файлов Azure?**
   
    Сейчас такая возможность не поддерживается.

* **В. Есть ли операция переименования в hello API-интерфейса REST?**
   
    На данный момент нет.

* **В. Можно ли использовать вложенные общие папки, то есть создавать общую папку в другой общей папке?**
    
    Нет. Hello общая папка является hello виртуальный драйвер, который можно подключить, поэтому вложенные общих папок, не поддерживаются.

* **В. Использование хранилища файлов Azure с IBM MQ**
    
    IBM выпустила документа tooguide IBM MQ клиентов, при настройке хранилища Azure File с их службы. Дополнительные сведения можно найти [как toosetup IBM MQ Multi экземпляр диспетчера очереди с помощью службы Microsoft Azure файл](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).


## <a name="troubleshooting"></a>Устранение неполадок
* **В. Как устранить ошибки в хранилище файлов Azure?**
    
    Можно ссылаться слишком[хранилища Azure File статьи по устранению неполадок](storage-troubleshoot-file-connection-problems.md) для начала до конца рекомендации по устранению неполадок. 


## <a name="see-also"></a>См. также
Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.

### <a name="conceptual-articles-and-videos"></a>Тематические статьи и видео
* [Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Хранилище файлов Azure: удобная облачная файловая система SMB для Windows и Linux)
* [Как toouse хранилища Azure File с Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Средства для работы с хранилищем файлов
* [Использование Azure PowerShell со службой хранилища Azure](storage-powershell-guide-full.md)
* [Как toouse AzCopy с хранилищем Microsoft Azure](storage-use-azcopy.md)
* [С помощью hello Azure CLI со службой хранилища Azure](storage-azure-cli.md)
* [Устранение неполадок хранилища файлов Azure](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a>Записи блога
* [Хранилище файлов Azure стало общедоступным](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Хранилище файлов Azure: взгляд изнутри)
* [Введение в службы файлов Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Миграция данных tooAzure хранения файлов](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Справочные материалы
* [Справочник по клиентской библиотеке хранилища для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Справочник по REST API службы файлов](http://msdn.microsoft.com/library/azure/dn167006.aspx)
