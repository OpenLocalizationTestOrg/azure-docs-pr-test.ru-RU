---
title: "aaaIntroduction tooAzure хранения файлов | Документы Microsoft"
description: "Введение tooAzure хранилища файлов, который предоставляет файл сети в общие папки на hello облака Майкрософт"
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
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: fe6826e79c364a6956831d2e273c4342a5fd47f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Введение tooAzure хранения файлов

Хранилище файлов Azure предлагает сети файловыми ресурсами общего доступа в облаке hello, с использованием hello отраслевого стандарта [протокола Server Message Block (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) и [общие файловая система Интернета (CIFS)](https://technet.microsoft.com/library/cc939973.aspx). Файловые ресурсы Azure могут параллельно подключаться службами "Виртуальные машины Azure" и клиентами локального развертывания под управлением Windows, macOS или Linux. Предоставляет учетной записи хранилища общего назначения, доступ tooAzure хранения файлов, хранилище больших двоичных объектов Azure и хранилища очередей Azure.

## <a name="videos"></a>Видеоролики
| Введение в хранилище файлов Azure (27 мин) | Руководство по файловому хранилищу Azure (5 мин)  |
|-|-|
| [![Демонстрация hello Представляем Azure файла хранилища видео - щелкните tooplay!](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![Демонстрация из хранилища Azure File hello учебника - щелкните tooplay!](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Почему нужно использовать хранилище файлов Azure

Хранилище файлов Azure позволяет tooreplace Windows Server, Linux, или NAS файловых серверах размещается локально или в облаке hello с файлом освободить ОС облачной совместного использования. Хранилище Azure файл имеет hello следующие преимущества:

* **Общий доступ к** Azure общие файлы поддержки hello отрасли стандартного протокола SMB, то есть можно легко заменить на локальных файловых ресурсов общих ресурсов Azure, не беспокоясь о совместимости приложений. Выполняется доступ tooaccess общую папку из нескольких машин и приложений и экземпляров становится большим преимуществом с хранилищем файлов Azure.

* **Управляемые** без hello необходимость toomanage оборудования и ОС, это значит, не будут toodeal с исправлений ОС на сервере hello критические обновления или замены неисправного жесткие диски могут создаваться общих ресурсов Azure.

* **Сценарии и средства** и командлеты PowerShell Azure CLI можно использовать toocreate подключения и управление общими папками Azure как часть hello администрирование приложений Azure. Можно создавать и управлять Azure файловые ресурсы с использованием hello [портал Azure](https://portal.azure.com) и hello [обозреватель хранилищ Azure](https://storageexplorer.com). 

* **Устойчивость** хранилища Azure File построенной hello основание, toobe доступна всегда. Замена локальных файловых ресурсах Azure хранилища означает, что у вас больше нет toowake копирование toodeal с локальной энергоснабжения или проблемы с сетью. 

* **Знакомые программные** приложений, работающих в Azure может обращаться к данным в общей папке hello через [файловая система API-интерфейсов ввода-вывода](https://msdn.microsoft.com/library/system.io.file.aspx). Таким образом, разработчики могут использовать свои существующий код и навыки toomigrate существующих приложений. В дополнение к этому tooSystem API ввода-ВЫВОДА, можно использовать любой из хранилища Azure hello клиента библиотеки, например hello, один для [.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet), или hello [API REST хранилища Azure](/rest/api/storageservices/file-service-rest-api).

Файловые ресурсы Azure можно использовать следующим образом:

* **Замена локальных файловых серверах** хранилища Azure File может быть используется toocompletely замены общих папок на файловых серверах в локальном или устройства NAS. Распространенных операционных систем Windows, Linux и macOS легко можно подключить Azure файловый ресурс, независимо от их в Здравствуй, мир.

* **Для переноса приложений по методике lift-and-shift.**

    Хранилище файлов Azure позволяет легко слишком «точности прогнозов и сдвиг» облачных приложений toohello, используйте файл в локальной среде делится данными tooshare между частями приложения hello. tooimplement, каждая виртуальная машина подключается toohello общей папки, а затем мог считывать и записывать файлы так же, как он локального файла используют.

* **Для упрощения разработки в облаке.**
    
    Хранилище Azure файл может использоваться несколькими различными способами toosimplify новых облачных проектов разработки.
    
    * **Общие параметры приложения**
    
        Распространенный подход для распределенных приложений является toohave файлы конфигурации в центральном расположении, где они могли быть доступны из много различных виртуальных машин. Эти файлы конфигурации можно хранить в общем ресурсе файлов Azure, и его могут читать все экземпляры приложений. Эти параметры также можно управлять с помощью интерфейса REST hello, позволяющий получить доступ по всему миру toohello файлы конфигурации.

    * **Общий ресурс диагностики**
    
        Azure файловый ресурс также может быть файлы диагностики используется toosave как журналы, метрики и аварийных дампов. Наличие общих папок, доступных через hello SMB и интерфейс REST позволяет toobuild приложения или использовать разнообразные средства анализа для обработки и анализа диагностических данных hello.

    * **Разработка, тестирование и отладка**

        Если разработчики и администраторы работают на виртуальных машинах в облаке hello, они часто требуется набор средств и служебных программ. Установка и распространение этих служебных программ на каждой виртуальной машине, где они требуются, занимает много времени. Благодаря хранилища Azure File разработчик или администратор может хранить своих любимых средств на файловом ресурсе, который может быть легко подключенных toofrom любой виртуальной машине.
        
## <a name="how-does-it-work"></a>Как это работает?

Управление файловыми ресурсами Azure гораздо проще, чем управление локальными файловыми ресурсами. Привет, следующая схема иллюстрирует конструкции управления хранилище файлов Azure hello:

![Структура файла](./media/storage-files-introduction/files-concepts.png)

* **Учетная запись хранения** обращаться к tooAzure хранилища осуществляется через учетную запись хранилища. Сведения о емкости учетной записи хранения см. в статье [о целевых показателях масштабируемости и производительности службы хранилища Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

* **Общая папка.** Общая папка хранилища файлов представляет собой общую папку с файлами в Azure, использующую протокол SMB. Все каталоги и файлы должны быть созданы в родительской общей папке. Учетная запись может содержать неограниченное количество общих ресурсов и общую папку можно сохранить неограниченное количество файлов копии общей емкости toohello 5 ТБ hello файлового ресурса общего доступа.

* **Каталог.** Необязательная иерархия каталогов.

* **Файл** файл в общей папке hello. Файл может являться вверх too1 ТБ.

* **Формат URL-адреса** файлы, можно с помощью hello следующий формат URL-адреса:  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```

## <a name="next-steps"></a>Дальнейшие действия

* [Create a File Share in Azure File storage](storage-how-to-create-file-share.md) (Создание файлового ресурса в хранилище файлов Azure)
* [Mount an Azure File share and access the share in Windows](storage-how-to-use-files-windows.md) (Подключение файлового ресурса Azure и доступ к нему в Windows)
* [Использование хранилища файлов Azure в Linux](storage-how-to-use-files-linux.md)
* [Mount Azure File share over SMB with macOS](storage-how-to-use-files-mac.md) (Использование хранилища файлов Azure с помощью протокола SMB в macOS)
* [Часто задаваемые вопросы](../storage-files-faq.md)
* [Troubleshoot Azure File storage problems in Windows](storage-troubleshoot-windows-file-connection-problems.md) (Устранение неполадок хранилища файлов Azure в Windows)   
* [Troubleshoot Azure File storage problems in Linux](storage-troubleshoot-linux-file-connection-problems.md) (Устранение неполадок хранилища файлов Azure в Linux)   

<!-- Rena I would remove any articles from here that are more than a year old. - Robin-->
### <a name="conceptual-articles-and-videos"></a>Тематические статьи и видео
* [Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Хранилище файлов Azure: удобная облачная файловая система SMB для Windows и Linux)

### <a name="tooling-support-for-azure-file-storage"></a>Поддержка средств для работы с хранилищем файлов Azure
* [Как toouse AzCopy с хранилищем Microsoft Azure](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [С помощью hello Azure CLI со службой хранилища Azure](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)

### <a name="blog-posts"></a>Записи блога
* [Хранилище файлов Azure стало общедоступным](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Хранилище файлов Azure: взгляд изнутри)
* [Введение в службы файлов Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Миграция данных tooAzure файла](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Справочные материалы
* [Справочник по клиентской библиотеке хранилища для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Справочник по REST API службы файлов](http://msdn.microsoft.com/library/azure/dn167006.aspx)
