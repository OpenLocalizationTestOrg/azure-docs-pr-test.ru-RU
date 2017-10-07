---
title: "проблем с хранилищем файлов Azure aaaTroubleshoot в Windows | Документы Microsoft"
description: "Устранение неполадок в работе хранилища файлов Azure в Windows."
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
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: ba0315d1add76a27fec93a9aee3aa99ccb7fa164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a>Устранение неполадок хранилища файлов Azure в Windows

В этой статье перечислены обычные проблемы, связанные tooMicrosoft хранилища Azure File при подключении клиентов Windows. Кроме того, здесь представлены возможные причины этих проблем и способы их устранения. В дополнение к этому toohello Устранение неполадок шаги в этой статье, можно также использовать [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) чтобы убедиться, что Windows hello среды клиента имеет правильные предварительные условия. AzFileDiagnostics автоматизирует обнаружения большинства hello симптомы, упоминаемые в этой статье, а также помогает настроить оптимальной производительности tooget среды. Кроме того, эти сведения можно найти в hello [Azure общих ресурсов средство устранения неполадок](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) , предоставляющий tooassist действия вы с проблемами подключения или сопоставление/монтажного Azure общих ресурсов.


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a>Ошибка 53, 67 или 87 при попытке подключения или отключения файлового ресурса Azure

При попытке toomount файловый ресурс из локальной или другом центре обработки данных, может появиться hello следующие ошибки:

- "Произошла системная ошибка 53. Hello сетевой путь не найден.
- "Произошла системная ошибка 67. не удается найти имя сети Hello.
- "Произошла системная ошибка 87. Неверный параметр Hello.

### <a name="cause-1-unencrypted-communication-channel"></a>Причина 1: незашифрованный коммуникационный канал

По соображениям безопасности подключений tooAzure файловые ресурсы блокируются, если канал связи hello не зашифрованы и не предпринята попытка подключения hello из hello одного центра обработки данных, где находятся hello Azure общих папок. Шифрование канала связи предоставляется только в том случае, если пользователь hello клиентской ОС поддерживает шифрование SMB.

Windows 8, Windows Server 2012 или более поздние версии этих ОС отправляют запрос на согласование, который включает протокол в себя SMB 3.0, поддерживающий шифрование.

### <a name="solution-for-cause-1"></a>Решение для причины 1

Подключение от клиента, который выполняет одно из следующих hello:

- Соответствует требованиям hello Windows 8 и Windows Server 2012 или более поздней версии
- Соединяется с виртуальной машины в hello же центре обработки данных, как hello учетной записи хранилища Azure, которая используется для hello Azure общей папки

### <a name="cause-2-port-445-is-blocked"></a>Причина 2: порт 445 заблокирован

Системная ошибка 53 или системная ошибка 67 может произойти, если заблокирован порт 445 исходящей связи tooan файла Azure хранилище центра обработки данных. Сводка hello toosee поставщиков услуг Интернета, разрешить или запретить доступ к порту 445, go слишком[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).

toounderstand ли это причиной hello приветственное сообщение «Системная ошибка 53», можно использовать Portqry tooquery hello TCP:445 endpoint. Если конечная точка TCP:445 hello отображается как отфильтрованные, блокируется hello TCP-порт. Вот пример запроса:

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

Если TCP-порт 445 заблокировано правилом вдоль hello сетевой путь, можно увидеть hello следующие выходные данные:

  `TCP port 445 (microsoft-ds service): FILTERED`

Дополнительные сведения о разделе toouse Portqry, [описание программы командной строки Portqry.exe hello](https://support.microsoft.com/help/310099).

### <a name="solution-for-cause-2"></a>Решение для причины 2

Работать с портом tooopen отдел ИТ 445 исходящих слишком[Azure IP-диапазонов](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="cause-3-ntlmv1-is-enabled"></a>Причина 3: включена аутентификация NTLMv1

Системная ошибка 53 или системная ошибка 87 может произойти, если на клиенте hello включена связь NTLMv1. Хранилище файлов Azure поддерживает только аутентификацию NTLMv2. Протокол проверки подлинности NTLMv1 делает клиент менее безопасным, в результате чего связь для хранилища файлов Azure блокируется. 

toodetermine ли это причиной hello ошибки hello, убедитесь, что этой hello следующий подраздел реестра установлено значение tooa 3:

**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**

Дополнительные сведения см. в разделе hello [параметра LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) на сайте TechNet.

### <a name="solution-for-cause-3"></a>Решение для причины 3

Вернуть hello **параметра LmCompatibilityLevel** значение toohello по умолчанию значение 3 в hello следующий подраздел реестра:

  **HKLM\SYSTEM\CurrentControlSet\Control\Lsa**

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a>Ошибка 1816 «недостаточно квоты имеет доступные tooprocess эта команда» при копировании tooan Azure общей папки

### <a name="cause"></a>Причина:

Ошибка 1816 возникает, когда достигнут верхний предел hello параллельных открытых дескрипторов, разрешенные для файла на компьютере hello, где смонтирована hello общей папки.

### <a name="solution"></a>Решение

Уменьшить hello число одновременных открытых дескрипторов, закрыв некоторые дескрипторы и повторите попытку. Дополнительные сведения см. в статье [Производительность хранилища Microsoft Azure и контрольный список масштабируемости](storage-performance-checklist.md).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a>Файла низкая копирование tooand из хранилища Azure File в Windows

Может появиться снижения производительности при попытке toohello файлы tootransfer файловой службы Azure.

- Если у вас нет конкретные требования минимальный размер ввода-вывода, рекомендуется использовать 1 МБ, как hello размер ввода-вывода для достижения оптимальной производительности.
-   Если вы знаете hello окончательный размер файла, расширении с записывает и программного обеспечения имеет проблемы совместимости, если hello незаписанных заключительный фрагмент файла hello содержит нули, а затем набор hello размер файла заранее, а не выполняющего запись в расширенном режиме каждой операции записи.
-   Используйте метод hello правой копирования:
    -   Используйте [AZCopy](storage-use-azcopy.md#file-copy) для передачи данных между двумя файловыми ресурсами.
    -   Используйте [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) для передачи данных между файловыми ресурсами и локальным компьютером.

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a>Рекомендации для Windows 8.1 или Windows Server 2012 R2

Для клиентов, работающих под управлением Windows 8.1 или Windows Server 2012 R2, убедитесь, что hello [KB3114025](https://support.microsoft.com/help/3114025) установлено исправление. Это исправление повышает производительность hello инструкции create и закрытия дескрипторов.

Можно запустить следующий сценарий toocheck ли hello исправление установлено hello:

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

Если установлено исправление, hello выводятся следующие данные:

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> Начиная с декабря 2015 года в образах Windows Server 2012 R2, содержащихся в Azure Marketplace, исправление KB3114025 установлено по умолчанию.

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a>В области **Мой компьютер** отсутствует папка с буквой диска

Если сопоставить Azure файловый ресурс от имени администратора с помощью команды net use, hello выступает toobe отсутствует.

### <a name="cause"></a>Причина:

По умолчанию проводник не запускается от имени администратора. При запуске команды net use из командной строки с правами администратора, можно подключить сетевой диск hello с правами администратора. Так как подключенные сетевые диски ориентированное на пользователей, hello учетной записи пользователя, зарегистрированного в не отображает hello диски при подключении под другой учетной записью.

### <a name="solution"></a>Решение
Общая папка hello подключения из командной строки без прав администратора. Кроме того, можно выполнить [в этом разделе TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** значение реестра.

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a>Команды net use завершается сбоем, если учетная запись хранения hello содержит косой черты

### <a name="cause"></a>Причина:

команды net use Hello интерпретирует косой черты (/), как параметр командной строки. Если имя пользователя учетной записи начинается с косой черты, сопоставление дисков hello завершается ошибкой.

### <a name="solution"></a>Решение

Можно использовать любой из следующих шагов toowork проблемы hello hello:

- Выполните следующую команду PowerShell hello.

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  Из пакетного файла можно выполнить команду hello таким образом:

  `Echo new-smbMapping ... | powershell -command –`

- Поместите двойных кавычек вокруг hello ключа toowork этой проблемы — Если hello первый символ косой черты hello. Если это так, используйте hello интерактивный режим и отдельно введите пароль или повторно создать ваш ключи tooget ключ, который не начинается с косой черты.

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a>Приложение или служба не может получить доступ к подключенному диску хранилища файлов Azure

### <a name="cause"></a>Причина:

Диски подключаются для каждого пользователя. Если приложение или служба выполняется под другой учетной записью чем hello, присоединенного диска hello, приложение hello не будут видеть hello диска.

### <a name="solution"></a>Решение

Используйте один из hello следующие решения:

-   Подключить диск hello из hello же учетной записью пользователя, содержащего приложение hello. Можно использовать такой инструмент, как PsExec.
- Передайте hello имя учетной записи хранения и ключ hello пользователя имя и пароль параметры команды net use hello.

После выполнения этих инструкций может появиться hello, при запуске команды net use для учетной записи службы системы или сети hello следующие сообщение об ошибке: «Произошла системная ошибка 1312. A specified logon session does not exist. Возможно, он уже завершен". В этом случае убедитесь, что username hello, передаваемое используйте toonet включает сведения о домене (например: «[имя учетной записи хранилища]. file.core.windows .net»).

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a>Ошибка «Копировании назначения tooa файл, который не поддерживает шифрование»

При копировании файла по сети hello hello файла расшифровывается на исходном компьютере hello, передается в виде обычного текста и повторно зашифрованы в месте назначения hello. Тем не менее, может появиться следующая ошибка, если вы пытаетесь toocopy зашифрованный файл hello: «Выполняется копирование hello файл tooa назначения, который не поддерживает шифрование».

### <a name="cause"></a>Причина:
Эта проблема может возникнуть при использовании шифрованной файловой системы (EFS). Файлы, зашифрованные BitLocker может быть tooAzure скопированный файл хранилища. Однако хранилище файлов Azure не поддерживает шифрованную файловую систему (EFS) NTFS.

### <a name="workaround"></a>Возможное решение
toocopy файл hello сети, необходимо сначала расшифровать его. Используйте один из следующих методов hello.

- Используйте hello **скопируйте /d** команды. Он позволяет hello зашифрованные файлы toobe как расшифрованных в месте назначения hello.
- Набор hello следующий раздел реестра:
  - путь: HKLM\Software\Policies\Microsoft\Windows\System;
  - тип значения: DWORD;
  - Name = CopyFileAllowDecryptedRemoteDestination;
  - Value = 1.

Имейте в виду, что разделу реестра hello параметр влияет на все операции копирования, сделанных toonetwork общих папок.

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.
