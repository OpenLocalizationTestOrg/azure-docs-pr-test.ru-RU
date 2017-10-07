---
title: "проблем с хранилищем файлов Azure aaaTroubleshoot в Linux | Документы Microsoft"
description: "Устранение неполадок, возникающих в работе хранилища файлов Azure в Linux."
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 4bdc3c6ed2e48f245060a03632fca9bd14d33545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Устранение неполадок в работе хранилища файлов Azure в Linux

В этой статье перечислены обычные проблемы, связанные tooMicrosoft хранилища Azure File при подключении из клиентов Linux. Кроме того, здесь представлены возможные причины этих проблем и способы их устранения.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a>«[отказано в разрешении] Превышена дисковая квота» при попытке tooopen файла

В Linux появляется сообщение об ошибке, подобное hello ниже:

**<filename> [permission denied] Disk quota exceeded**

### <a name="cause"></a>Причина:

Вы достигли hello верхний предел одновременных открытых дескрипторов, разрешенная для файла.

### <a name="solution"></a>Решение

Уменьшить hello число одновременных открытых дескрипторов, закрыв некоторые дескрипторы, а затем повторите операцию hello. Дополнительные сведения см. в статье [Производительность хранилища Microsoft Azure и контрольный список масштабируемости](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a>Копирование из хранилища Azure File в Linux tooand файла низкая

-   Если у вас нет конкретные требования минимальный размер ввода-вывода, рекомендуется использовать 1 МБ, как hello размер ввода-вывода для достижения оптимальной производительности.
-   Если вы знаете hello окончательный размер файла, расширение с помощью записи и программное обеспечение не проблем совместимости с незаписанных заключительного hello файл содержит нули, задайте размер файла hello заранее, вместо выполнения каждой операции записи, в расширение запись.
-   Используйте метод hello правой копирования:
    -   Используйте [AZCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) для передачи данных между двумя файловыми ресурсами.
    -   Используйте [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) для передачи данных между файловыми ресурсами и локальным компьютером.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>Отображается сообщение "Mount error(112): Host is down" (Ошибка подключения (112). Узел не работает) из-за истечения времени ожидания повторного подключения

Ошибка «112» монтирования происходит на клиента Linux hello, когда клиент hello бездействует в течение долгого времени. После расширенной время простоя отключении клиента hello и время ожидания соединения hello.  

### <a name="cause"></a>Причина:

Hello подключение может простаивать для hello следующих причин:

-   Сбои подключения сети, препятствующие восстановив серверу toohello подключения TCP, при использовании параметра «soft» подключения по умолчанию hello
-   последние исправления повторного подключения, отсутствующие в ядрах предыдущих версий.

### <a name="solution"></a>Решение

Эта проблема повторного подключения в ядре Linux hello теперь исправлена как часть hello следующие изменения:

- [Исправление переподключение toonot отложить smb3 сеанса повторное подключение длинная после повторного подключения сокета](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Вызов службы echo сразу же после повторного подключения сокета](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [CIFS: устранение возможного повреждения содержимого памяти во время повторного подключения](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [CIFS: устранение возможной двойной блокировки мьютекса во время повторного подключения — для ядра v4.9 и более поздних версий](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

Тем не менее эти изменения не может быть перенесена, еще tooall hello дистрибутивов Linux. Это исправление и исправления других повторное подключение вносятся в следующие популярных ядер Linux hello: 4.4.40, 4.8.16 и 4.9.1. Это исправление можно получить, tooone из этих версий ядра рекомендуемые обновления.

### <a name="workaround"></a>Возможное решение

Можно обойти эту проблему, указав жесткое подключение. Это заставляет клиента toowait hello до установления соединения или его явно прерывается и может быть используется tooprevent ошибки из-за тайм-ауты сети. Тем не менее этот способ может породить неопределенное время ожидания. Быть подготовленного toostop соединения при необходимости.

Если нельзя обновить toohello последние версии ядра, эту проблему можно обойти за счет файла в папке файлов Azure hello записи tooevery 30 секунд или менее. Это должен быть операции записи, такие как перезаписи hello создания или изменения файла hello даты. В противном случае может появиться кэшированные результаты и операция не может привести к запуску переподключения hello.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>Отображается ошибка "Mount error(115): Operation now in progress" (Ошибка подключения (115). Идет выполнение операции) при подключении хранилища файлов Azure с помощью SMB 3.0

### <a name="cause"></a>Причина:

Некоторые дистрибутивы Linux еще не поддерживает возможности шифрования в SMB 3.0, и пользователи могут получать сообщение об ошибке «115», если они пытаются выполнить toomount хранилища Azure File с помощью SMB 3.0 из-за отсутствующих компонентов.

### <a name="solution"></a>Решение

Функция шифрования протокола SMB 3.0 для Linux появилась в ядре версии 4.11. Эта функция позволяет подключать общую папку файлов Azure из локальной среды или другого региона Azure. Во время публикации hello эта функциональность была backported tooUbuntu 17.04 и Ubuntu 16.10. Если клиент Linux SMB не поддерживает шифрование, с помощью SMB 2.1 из в виртуальной Машине Linux Azure Подключите хранилища Azure File hello одного центра обработки данных, как hello учетной записи хранения файла.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Низкая производительность файлового ресурса Azure, подключенного к виртуальной машине Linux

### <a name="cause"></a>Причина:

Одной из возможных причин снижения производительности может быть отключенное кэширование.

### <a name="solution"></a>Решение

toocheck ли кэширование отключено, найдите hello **кэша =** входа. 

Запись **cache=none** означает, что кэширование отключено.  Общий ресурс hello повторного подключения с помощью команды mount по умолчанию hello или путем явного добавления hello **кэша = strict** включен параметр подключения toohello команды tooensure, кэширования или «strict» режим кэширования по умолчанию.

В некоторых сценариях hello **serverino** подключения может привести к hello **ls** stat toorun команду для каждой записи каталога. Это приводит к снижению производительности при выводе содержимого больших каталогов. Проверьте параметры подключения hello в вашей **/etc/fstab** входа:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

Можно также проверить, используются ли hello правильные параметры, выполнив hello **подключения sudo | grep cifs** команда и проверка его выходные данные, например hello следующий пример выходных данных:

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Если hello **кэша = strict** или **serverino** может не представлять, отключите и снова подключить хранилище файлов Azure, выполнив команду подключения hello из hello [документации](../storage-how-to-use-files-linux.md). Затем, повторно проверьте что hello **/etc/fstab** запись имеет правильные параметры hello.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a>Отметки времени были потеряны при копировании файлов из Windows tooLinux

На платформах, Linux и Unix, hello **cp -p** команда завершается ошибкой, если файл 1 и 2 принадлежат разным пользователям.

### <a name="cause"></a>Причина:

Здравствуйте, флаг force **f** в COPYFILE результатов при выполнении **cp -p -f** в Unix. Эта команда также завершается неудачей, отметка времени toopreserve hello hello файла, который вы не владеете.

### <a name="workaround"></a>Возможное решение

Использовать hello пользователя учетной записи хранилища для копирования файлов hello:

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.

Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.
