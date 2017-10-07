---
title: "агент резервного копирования aaaAzure часто задаваемые вопросы | Документы Microsoft"
description: "Содержит ответы на вопросы toocommon о: как hello ограничения агента резервного копирования Azure работает, резервного копирования и хранения."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "резервное копирование и аварийное восстановление; служба архивации"
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: bdefb4efb39301f38cdf692bdc93c841a2bbb441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-agent"></a>Вопросы о hello Azure Backup agent
Данная статья содержит ответы toocommon вопросы toohelp быстро оценить hello компоненты агента Azure Backup. В некоторые ответы hello существуют ссылки toohello статей, имеющих исчерпывающую информацию. Вы также можете публиковать вопросы о hello службы архивации Azure в hello [дискуссионный форум](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Настройка резервного копирования
### <a name="where-can-i-download-hello-latest-azure-backup-agent-br"></a>Где можно загрузить последнюю версию агента резервного копирования Azure hello <br/>
Можно загрузить последнюю версию агента hello для резервного копирования Windows Server, System Center DPM или клиента Windows с [здесь](http://aka.ms/azurebackup_agent). Tooback виртуальную машину, воспользуйтесь hello агент виртуальной Машины (который автоматически установит соответствующие расширения hello). Hello агент виртуальной Машины уже присутствует на виртуальные машины, созданные из коллекции Azure hello.

### <a name="when-configuring-hello-azure-backup-agent-i-am-prompted-tooenter-hello-vault-credentials-do-vault-credentials-expire"></a>При настройке агента Azure Backup hello, я tooenter запрашиваемые учетные данные хранилища hello. Ограничен ли срок действия этих учетных данных?
Да, учетные данные хранилища hello истекает через 48 часов. После истечения срока действия файла hello, в toohello Azure портал и загрузки hello хранилище учетных данных в файлах журнала из вашего хранилища.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>С каких типов дисков можно создавать резервные копии файлов и папок? <br/>
Не удается архивировать hello следующие диски и тома:

* Съемные носители. Все источники для резервного копирования должны быть фиксированными.
* Только для чтения томов: hello том должен быть доступен для hello тома теневого копирования (томов VSS) службы toofunction записи.
* Автономные тома: hello тома должен быть подключен к сети VSS toofunction.
* Общий сетевой ресурс: hello тома должен составлять toobe toohello локального сервера, резервное копирование с использованием оперативной архивации.
* Защищенные BitLocker тома: hello том необходимо разблокировать hello резервное копирование может выполняться.
* Идентификация системных файла: NTFS является единственной файловой системы hello поддерживается.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>Для каких типов файлов и папок можно создавать резервные копии с моего сервера?<br/>
поддерживаются следующие типы Hello:

* зашифрованные;
* сжатые;
* разреженные;
* сжатые и разреженные;
* жесткие связи (не поддерживаются, пропускаются);
* точки повторного анализа (не поддерживаются, пропускаются);
* зашифрованные и разреженные (не поддерживаются, пропускаются);
* сжатые потоки (не поддерживаются, пропускаются);
* разреженные потоки (не поддерживаются, пропускаются).

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-already-backed-by-hello-azure-backup-service-using-hello-vm-extension-br"></a>Можно установить hello Azure Backup agent на Виртуальной машине Azure, уже выполнено резервное копирование Azure службой hello hello расширения виртуальной Машины <br/>
Конечно. Резервное копирование Azure служит резервное копирование на уровне виртуальной Машины для виртуальных машин Azure с помощью расширения ВМ hello. tooprotect файлов и папок на hello гостевой ОС Windows, установите агент Azure Backup hello на hello гостевой ОС Windows.

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-tooback-up-files-and-folders-present-on-temporary-storage-provided-by-hello-azure-vm-br"></a>Можно установить hello Azure Backup agent на виртуальной Машине Azure tooback копирования файлов и папок на временное хранилище, предоставляемые hello виртуальной Машине Azure? <br/>
Да. Установите агент Azure Backup hello на hello гостевой ОС Windows, а резервное копирование файлов и папок tootemporary хранилища. Удаление данных из временного хранилища приведет к сбою заданий резервного копирования. Кроме того Если был удален hello временного хранилища данных, можно восстановить только toonon ПЗУ.

### <a name="whats-hello-minimum-size-requirement-for-hello-cache-folder-br"></a>Что такое hello минимальному требованию к размеру для папки кэша hello <br/>
Hello размер папки кэша hello определяет hello объем данных, резервное копирование выполняется. Папки кэша должно быть 5% hello пространство, необходимое для хранения данных.

### <a name="how-do-i-register-my-server-tooanother-datacenterbr"></a>Как зарегистрировать my server tooanother datacenter?<br/>
Резервные данные отправляются в центр обработки данных toohello toowhich hello хранилища, которую он зарегистрирован. Hello простым способом toochange hello центра обработки данных toouninstall hello агент и повторно установите агент hello и зарегистрировать tooa новое хранилище, к которому относится toodesired центра обработки данных.

### <a name="does-hello-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>Поддерживает hello Azure Backup, агент работает на сервере, где используется дедупликация Windows Server 2012? <br/>
Да. Служба агента Hello преобразует данные toonormal hello дедупликации данных, при подготовке операции резервного копирования hello. Он затем оптимизирует hello данные для резервного копирования, шифрует данные hello, а затем отправляет hello зашифрованные данные toohello службы резервного копирования.

## <a name="backup"></a>Резервное копирование
### <a name="how-do-i-change-hello-cache-location-specified-for-hello-azure-backup-agentbr"></a>Как изменить расположение кэша hello, указанными для агента Azure Backup hello?<br/>
Используйте следующие расположение кэша hello toochange списка hello.

1. Остановите обработчик hello резервной копии, выполнив следующую команду в командную строку hello:

    ```PS C:\> Net stop obengine``` 
  
2. Не перемещайте файлы hello. Вместо этого скопируйте hello кэша пространство папки tooa другой диск с достаточно места. Hello исходного места в кэше могут быть удалены после подтверждения hello резервных копий с которыми работает hello нового места в кэше.
3. Обновление hello следующих параметров реестра с hello путь toohello новое пространство папки кэша.<br/>

    | Путь к элементу реестра | Ключ реестра | Значение |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*Новое расположение папки кэша* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*Новое расположение папки кэша* |

4. Перезапустите engine hello резервной копии, выполнив следующую команду в командную строку hello:

    ```PS C:\> Net start obengine```

После успешного завершения создания резервной копии hello в новое расположение кэша hello, можно удалить исходную папку кэша hello.


### <a name="where-can-i-put-hello-cache-folder-for-hello-azure-backup-agent-toowork-as-expectedbr"></a>Где можно поместить папку кэша hello для hello Azure Backup Agent toowork должным образом<br/>
Hello следующие расположения папки кэша hello не рекомендуется.

* Сетевой общий ресурс или съемные носители: hello папки кэша должно быть toohello на локальном сервере, которому требуется, резервное копирование с использованием оперативной архивации. Сетевые расположения и съемные носители (например, USB-накопители) не поддерживаются.
* Автономные тома: hello папки кэша должно быть доступно для ожидаемого резервного копирования с помощью агента резервного копирования Azure.

### <a name="are-there-any-attributes-of-hello-cache-folder-that-are-not-supportedbr"></a>Существуют ли какие-либо атрибуты папки кэша hello, которые не поддерживаются?<br/>
Hello следующие атрибуты или их сочетаний не поддерживаются для папки кэша hello:

* зашифрованные;
* дедупликация;
* сжатые;
* разреженные;
* точка повторного анализа.

папка кэша Hello и метаданные hello виртуального жесткого диска нет hello необходимые атрибуты для hello Azure Backup agent.

### <a name="is-there-a-way-tooadjust-hello-amount-of-bandwidth-used-by-hello-backup-servicebr"></a>Есть ли способ tooadjust hello объем пропускной способности, используемой службой hello резервного копирования?<br/>
  Да, использовать hello **изменить свойства** параметр пропускной способности tooadjust агента резервного копирования hello. Вы можете настроить hello объем пропускной способности и hello раз при использовании пропускную способность. Пошаговые инструкции см. в разделе **[Включение регулирования сети](backup-configure-vault.md#enable-network-throttling)**.

## <a name="manage-backups"></a>Управление резервными копиями
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-tooazurebr"></a>Что произойдет, если я переименую сервер Windows, резервное копирование данных tooAzure?<br/>
Если переименовать сервер, остановятся все настроенные процессы резервного копирования.
Зарегистрируйте новое имя сервера hello hello hello резервное хранилище. При регистрации нового имени hello хранилище hello, — первая операция резервного копирования hello *полного* резервного копирования. Если требуются данные toorecover резервное хранилище toohello с hello старого имени сервера, используйте hello [ **другой сервер** ](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) параметр в hello **восстановить данные** мастера.

### <a name="what-is-hello-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>Что такое hello Максимальная длина пути, могут быть указаны в политику резервного копирования с помощью агента архивации Azure? <br/>
Агент службы архивации Azure использует NTFS. Hello [Указание длины filepath ограничивается Windows API hello](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths). Если длина пути к файлу, больше допустимых hello интерфейса Windows API, создайте резервную копию hello родительской папки или дисковый накопитель, hello hello файлы tooprotect.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>Какие символы можно использовать в пути к файлу, определяемом в политике резервного копирования Azure с помощью агента службы архивации Azure? <br>
 Агент службы архивации Azure использует NTFS. Поэтому, указывая файлы, можно использовать [символы, которые поддерживаются в NTFS](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) . 
 
### <a name="i-receive-hello-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>Получено предупреждение, hello, «Операций резервного копирования Azure не были настроены для этого сервера», несмотря на то, что я настроил политику резервного копирования <br/>
Это предупреждение возникает, когда параметры расписания резервного копирования hello, хранящиеся на локальном сервере hello не hello таким же, как hello настроек, хранимых в хранилище архивации hello. Когда сервер hello или параметры hello стали восстановленные tooa известное хорошее состояние, hello расписания резервного копирования могут потерять синхронизацию. Если это предупреждение появляется [перенастройте политику резервного копирования hello](backup-azure-manage-windows-server.md) и затем **запустить архивацию сейчас** tooresynchronize hello локального сервера с помощью Azure.
