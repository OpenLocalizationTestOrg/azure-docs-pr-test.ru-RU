---
title: "aaaIntroduction tooAzure хранения файлов | Документы Microsoft"
description: "Обзор хранилища Azure File, служба, которая позволяет вам toocreate и использование файла сети Общие папки на hello облака Майкрософт, с помощью стандартного hello."
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
ms.openlocfilehash: a0a6a80a2ccd9742aa470bdd02ff375387a1629b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Введение tooAzure хранения файлов
Хранилище файлов Azure предлагает сети файловыми ресурсами общего доступа в облаке hello, с использованием hello отраслевого стандарта [протокола Server Message Block (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) и [общие файловая система Интернета (CIFS)](https://technet.microsoft.com/library/cc939973.aspx). Файловые ресурсы Azure могут параллельно подключаться такими клиентами, как локальные развертывания Windows, macOS, Linux или службы "Виртуальные машины Azure". Предоставляет учетной записи хранилища общего назначения, доступ tooAzure хранения файлов и других служб, таких как большие двоичные объекты, диски виртуальной машины Azure, очереди от одной учетной записи.



## <a name="videos"></a>Видеоролики
| Введение в хранилище файлов Azure (27 мин) | Руководство по файловому хранилищу Azure (5 мин)  |
|-|-|
| [![ScreenCap hello Представляем Azure файла хранилища видео - щелкните tooplay!](media/storage-file-storage/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![ScreenCap из хранилища Azure File hello учебника - щелкните tooplay!](media/storage-file-storage/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Почему нужно использовать хранилище файлов Azure
Хранилище файлов Azure позволяет tooreplace Windows Server, Linux, или NAS файловых серверах размещается локально или в облаке hello с файлом освободить ОС облачной совместного использования. Это дает следующие преимущества hello:

* **Совместный доступ.** Azure общие файлы поддержки hello отрасли стандартного протокола SMB, то есть можно легко заменить на локальных файловых ресурсов общих ресурсов Azure, не беспокоясь о совместимости приложений. Между несколькими компьютерами, что может tooshare файловой системы, приложений и экземпляров становится большим преимуществом с хранилищем файлов Azure для приложений, требующих возможность общего доступа.. 
* **Полная управляемость.** Azure общих папок можно создать без hello необходимость toomanage оборудования и ОС. Это означает, что у вас нет toodeal с исправлений ОС на сервере hello критические обновления или замены неисправного жестких дисков.
* **Сценарии и средства.** Командлеты PowerShell Azure CLI можно и используется toocreate подключения и управления общими папками хранилища в рамках hello администрирование приложений Azure. Можно создавать и управлять ресурсами Azure с помощью портала Azure и хранилищем Azure обозревателя. 
* **Устойчивость.** Хранилища Azure файл был создан из hello основание, toobe доступна всегда. Замена локальных файловых ресурсах Azure хранилища означает, что у вас больше нет toowake копирование toodeal с локальной энергоснабжения или проблемы с сетью. 
* **Знакомое программирование.** Приложения, работающие в Azure может обращаться к данным в папке hello посредством файла [API ввода-вывода системы](https://msdn.microsoft.com/library/system.io.file.aspx). Таким образом, разработчики могут использовать свои существующий код и навыки toomigrate существующих приложений. В дополнение к этому tooSystem API ввода-ВЫВОДА, можно использовать [клиентских библиотек хранилища Azure](https://msdn.microsoft.com/library/azure/dn261237.aspx) или hello [API REST хранилища Azure](/rest/api/storageservices/file-service-rest-api).

Файловые ресурсы Azure можно использовать следующим образом:

* **Для замены локальных файловых серверов.**  
    Хранилище Azure файл может быть используется toocompletely замены общих папок на файловых серверах в локальном или устройства NAS. Распространенных операционных систем Windows, Linux и macOS легко можно подключить Azure файловый ресурс, независимо от их в Здравствуй, мир.

* **Для приложений Lift-and-Shift.**  
    Хранилище файлов Azure позволяет легко слишком «точности прогнозов и сдвиг» облачных приложений toohello, используйте файл в локальной среде делится данными tooshare между частями приложения hello. Это происходит, toomake каждой виртуальной Машины подключается toohello общей папки и затем мог считывать и записывать файлы так же, как он локального файла используют.

* **Для упрощения разработки в облаке.**  
    Хранилище Azure файл может использоваться несколькими различными способами toosimplify новых облачных проектов разработки.
    * **Общие параметры приложения.**  
        Распространенный подход для распределенных приложений является toohave файлы конфигурации в центральном расположении, где они могли быть доступны из много различных виртуальных машин. Эти файлы конфигурации можно хранить в общем ресурсе файлов Azure, и его могут читать все экземпляры приложений. Эти параметры также можно управлять с помощью интерфейса REST hello, позволяющий получить доступ по всему миру toohello файлы конфигурации.

    * **Общий ресурс диагностики.**  
        Azure файловый ресурс также может быть файлы диагностики используется toosave как журналы, метрики и аварийных дампов. Наличие этих доступны через интерфейс REST и hello SMB позволяет toobuild приложения или использовать разнообразные средства анализа для обработки и анализа диагностических данных hello.

    * **Разработка, тестирование и отладка.**  
        Если разработчики и администраторы работают на виртуальных машинах в облаке hello, они часто требуется набор средств и служебных программ. Установка и распространение этих служебных программ на каждой виртуальной машине, где они требуются, занимает много времени. Благодаря хранилища Azure File разработчик или администратор может хранить своих любимых средств на файловом ресурсе, который может быть легко подключенных toofrom любой виртуальной машине.
        
## <a name="how-does-it-work"></a>Как это работает?
Управление файловыми ресурсами Azure гораздо проще, чем управление локальными файловыми ресурсами. Привет, следующая схема иллюстрирует конструкции управления хранилище файлов Azure hello:

![Структура файла](../../includes/media/storage-file-concepts-include/files-concepts.png)

* **Учетная запись хранения**: обращаться к tooAzure хранилища осуществляется через учетную запись хранилища. Сведения о емкости учетной записи хранения см. в статье о целевых показателях масштабируемости и производительности службы хранилища Azure.
* **Общая папка.** Общая папка хранилища файлов представляет собой общую папку с файлами в Azure, использующую протокол SMB. Все каталоги и файлы должны быть созданы в родительской общей папке. Учетная запись может содержать неограниченное количество общих ресурсов и общую папку можно сохранить неограниченное количество файлов копии общей емкости toohello 5 ТБ hello файлового ресурса общего доступа.
* **Каталог.** Необязательная иерархия каталогов.
* **Файл**: файл в общей папке hello. Файл может являться вверх too1 ТБ.
* **Формат URL-адреса**: файлы, можно с помощью hello следующий формат URL-адреса:  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```
## <a name="next-steps"></a>Дальнейшие действия
* [Create a File Share in Azure File storage](storage-file-how-to-create-file-share.md) (Создание файлового ресурса в хранилище файлов Azure)
* [Mount an Azure File share and access the share in Windows](storage-file-how-to-use-files-windows.md) (Подключение файлового ресурса Azure и доступ к нему в Windows)
* [Использование хранилища файлов Azure в Linux](storage-how-to-use-files-linux.md)
* [Mount Azure File share over SMB with macOS](storage-file-how-to-use-files-mac.md) (Использование хранилища файлов Azure с помощью протокола SMB в macOS)
* [Часто задаваемые вопросы](storage-files-faq.md)
* [Устранение неполадок](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Тематические статьи и видео
* [Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Хранилище файлов Azure: удобная облачная файловая система SMB для Windows и Linux)

### <a name="tooling-support-for-azure-file-storage"></a>Поддержка средств для работы с хранилищем файлов Azure
* [Использование Azure PowerShell со службой хранилища Azure](storage-powershell-guide-full.md)
* [Как toouse AzCopy с хранилищем Microsoft Azure](storage-use-azcopy.md)
* [С помощью hello Azure CLI со службой хранилища Azure](storage-azure-cli.md#create-and-manage-file-shares)

### <a name="blog-posts"></a>Записи блога
* [Хранилище файлов Azure стало общедоступным](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Хранилище файлов Azure: взгляд изнутри)
* [Введение в службы файлов Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Миграция данных tooAzure файла](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Справочные материалы
* [Клиент хранилища .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Справочник по REST API службы файлов](http://msdn.microsoft.com/library/azure/dn167006.aspx)
