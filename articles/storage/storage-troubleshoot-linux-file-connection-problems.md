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
ms.openlocfilehash: 3dc537d714244451a5ff8e01f4a27f03873cf2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="647c5-103">Устранение неполадок в работе хранилища файлов Azure в Linux</span><span class="sxs-lookup"><span data-stu-id="647c5-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="647c5-104">В этой статье перечислены обычные проблемы, связанные tooMicrosoft хранилища Azure File при подключении из клиентов Linux.</span><span class="sxs-lookup"><span data-stu-id="647c5-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="647c5-105">Кроме того, здесь представлены возможные причины этих проблем и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="647c5-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a><span data-ttu-id="647c5-106">«[отказано в разрешении] Превышена дисковая квота» при попытке tooopen файла</span><span class="sxs-lookup"><span data-stu-id="647c5-106">"[permission denied] Disk quota exceeded" when you try tooopen a file</span></span>

<span data-ttu-id="647c5-107">В Linux появляется сообщение об ошибке, подобное hello ниже:</span><span class="sxs-lookup"><span data-stu-id="647c5-107">In Linux, you receive an error message that resembles hello following:</span></span>

<span data-ttu-id="647c5-108">**<filename> [permission denied] Disk quota exceeded**</span><span class="sxs-lookup"><span data-stu-id="647c5-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="647c5-109">Причина:</span><span class="sxs-lookup"><span data-stu-id="647c5-109">Cause</span></span>

<span data-ttu-id="647c5-110">Вы достигли hello верхний предел одновременных открытых дескрипторов, разрешенная для файла.</span><span class="sxs-lookup"><span data-stu-id="647c5-110">You have reached hello upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="647c5-111">Решение</span><span class="sxs-lookup"><span data-stu-id="647c5-111">Solution</span></span>

<span data-ttu-id="647c5-112">Уменьшить hello число одновременных открытых дескрипторов, закрыв некоторые дескрипторы, а затем повторите операцию hello.</span><span class="sxs-lookup"><span data-stu-id="647c5-112">Reduce hello number of concurrent open handles by closing some handles, and then retry hello operation.</span></span> <span data-ttu-id="647c5-113">Дополнительные сведения см. в статье [Производительность хранилища Microsoft Azure и контрольный список масштабируемости](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="647c5-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a><span data-ttu-id="647c5-114">Копирование из хранилища Azure File в Linux tooand файла низкая</span><span class="sxs-lookup"><span data-stu-id="647c5-114">Slow file copying tooand from Azure File storage in Linux</span></span>

-   <span data-ttu-id="647c5-115">Если у вас нет конкретные требования минимальный размер ввода-вывода, рекомендуется использовать 1 МБ, как hello размер ввода-вывода для достижения оптимальной производительности.</span><span class="sxs-lookup"><span data-stu-id="647c5-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="647c5-116">Если вы знаете hello окончательный размер файла, расширение с помощью записи и программное обеспечение не проблем совместимости с незаписанных заключительного hello файл содержит нули, задайте размер файла hello заранее, вместо выполнения каждой операции записи, в расширение запись.</span><span class="sxs-lookup"><span data-stu-id="647c5-116">If you know hello final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="647c5-117">Используйте метод hello правой копирования:</span><span class="sxs-lookup"><span data-stu-id="647c5-117">Use hello right copy method:</span></span>
    -   <span data-ttu-id="647c5-118">Используйте [AZCopy](storage-use-azcopy.md#file-copy) для передачи данных между двумя файловыми ресурсами.</span><span class="sxs-lookup"><span data-stu-id="647c5-118">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="647c5-119">Используйте [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) для передачи данных между файловыми ресурсами и локальным компьютером.</span><span class="sxs-lookup"><span data-stu-id="647c5-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="647c5-120">Отображается сообщение "Mount error(112): Host is down" (Ошибка подключения (112). Узел не работает) из-за истечения времени ожидания повторного подключения</span><span class="sxs-lookup"><span data-stu-id="647c5-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="647c5-121">Ошибка «112» монтирования происходит на клиента Linux hello, когда клиент hello бездействует в течение долгого времени.</span><span class="sxs-lookup"><span data-stu-id="647c5-121">A "112" mount error occurs on hello Linux client when hello client has been idle for a long time.</span></span> <span data-ttu-id="647c5-122">После расширенной время простоя отключении клиента hello и время ожидания соединения hello.</span><span class="sxs-lookup"><span data-stu-id="647c5-122">After extended idle time, hello client disconnects and hello connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="647c5-123">Причина:</span><span class="sxs-lookup"><span data-stu-id="647c5-123">Cause</span></span>

<span data-ttu-id="647c5-124">Hello подключение может простаивать для hello следующих причин:</span><span class="sxs-lookup"><span data-stu-id="647c5-124">hello connection can be idle for hello following reasons:</span></span>

-   <span data-ttu-id="647c5-125">Сбои подключения сети, препятствующие восстановив серверу toohello подключения TCP, при использовании параметра «soft» подключения по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="647c5-125">Network communication failures that prevent re-establishing a TCP connection toohello server when hello default “soft” mount option is used</span></span>
-   <span data-ttu-id="647c5-126">последние исправления повторного подключения, отсутствующие в ядрах предыдущих версий.</span><span class="sxs-lookup"><span data-stu-id="647c5-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="647c5-127">Решение</span><span class="sxs-lookup"><span data-stu-id="647c5-127">Solution</span></span>

<span data-ttu-id="647c5-128">Эта проблема повторного подключения в ядре Linux hello теперь исправлена как часть hello следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="647c5-128">This reconnection problem in hello Linux kernel is now fixed as part of hello following changes:</span></span>

- [<span data-ttu-id="647c5-129">Исправление переподключение toonot отложить smb3 сеанса повторное подключение длинная после повторного подключения сокета</span><span class="sxs-lookup"><span data-stu-id="647c5-129">Fix reconnect toonot defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="647c5-130">Вызов службы echo сразу же после повторного подключения сокета</span><span class="sxs-lookup"><span data-stu-id="647c5-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="647c5-131">CIFS: устранение возможного повреждения содержимого памяти во время повторного подключения</span><span class="sxs-lookup"><span data-stu-id="647c5-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [<span data-ttu-id="647c5-132">CIFS: устранение возможной двойной блокировки мьютекса во время повторного подключения — для ядра v4.9 и более поздних версий</span><span class="sxs-lookup"><span data-stu-id="647c5-132">CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

<span data-ttu-id="647c5-133">Тем не менее эти изменения не может быть перенесена, еще tooall hello дистрибутивов Linux.</span><span class="sxs-lookup"><span data-stu-id="647c5-133">However, these changes might not be ported yet tooall hello Linux distributions.</span></span> <span data-ttu-id="647c5-134">Это исправление и исправления других повторное подключение вносятся в следующие популярных ядер Linux hello: 4.4.40, 4.8.16 и 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="647c5-134">This fix and other reconnection fixes are made in hello following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="647c5-135">Это исправление можно получить, tooone из этих версий ядра рекомендуемые обновления.</span><span class="sxs-lookup"><span data-stu-id="647c5-135">You can get this fix by upgrading tooone of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="647c5-136">Возможное решение</span><span class="sxs-lookup"><span data-stu-id="647c5-136">Workaround</span></span>

<span data-ttu-id="647c5-137">Можно обойти эту проблему, указав жесткое подключение.</span><span class="sxs-lookup"><span data-stu-id="647c5-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="647c5-138">Это заставляет клиента toowait hello до установления соединения или его явно прерывается и может быть используется tooprevent ошибки из-за тайм-ауты сети.</span><span class="sxs-lookup"><span data-stu-id="647c5-138">This forces hello client toowait until a connection is established or until it’s explicitly interrupted and can be used tooprevent errors because of network time-outs.</span></span> <span data-ttu-id="647c5-139">Тем не менее этот способ может породить неопределенное время ожидания.</span><span class="sxs-lookup"><span data-stu-id="647c5-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="647c5-140">Быть подготовленного toostop соединения при необходимости.</span><span class="sxs-lookup"><span data-stu-id="647c5-140">Be prepared toostop connections as necessary.</span></span>

<span data-ttu-id="647c5-141">Если нельзя обновить toohello последние версии ядра, эту проблему можно обойти за счет файла в папке файлов Azure hello записи tooevery 30 секунд или менее.</span><span class="sxs-lookup"><span data-stu-id="647c5-141">If you cannot upgrade toohello latest kernel versions, you can work around this problem by keeping a file in hello Azure file share that you write tooevery 30 seconds or less.</span></span> <span data-ttu-id="647c5-142">Это должен быть операции записи, такие как перезаписи hello создания или изменения файла hello даты.</span><span class="sxs-lookup"><span data-stu-id="647c5-142">This must be a write operation, such as rewriting hello created or modified date on hello file.</span></span> <span data-ttu-id="647c5-143">В противном случае может появиться кэшированные результаты и операция не может привести к запуску переподключения hello.</span><span class="sxs-lookup"><span data-stu-id="647c5-143">Otherwise, you might get cached results, and your operation might not trigger hello reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="647c5-144">Отображается ошибка "Mount error(115): Operation now in progress" (Ошибка подключения (115). Идет выполнение операции) при подключении хранилища файлов Azure с помощью SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="647c5-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="647c5-145">Причина:</span><span class="sxs-lookup"><span data-stu-id="647c5-145">Cause</span></span>

<span data-ttu-id="647c5-146">Некоторые дистрибутивы Linux еще не поддерживает возможности шифрования в SMB 3.0, и пользователи могут получать сообщение об ошибке «115», если они пытаются выполнить toomount хранилища Azure File с помощью SMB 3.0 из-за отсутствующих компонентов.</span><span class="sxs-lookup"><span data-stu-id="647c5-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try toomount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="647c5-147">Решение</span><span class="sxs-lookup"><span data-stu-id="647c5-147">Solution</span></span>

<span data-ttu-id="647c5-148">Функция шифрования протокола SMB 3.0 для Linux появилась в ядре версии 4.11.</span><span class="sxs-lookup"><span data-stu-id="647c5-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="647c5-149">Эта функция позволяет подключать общую папку файлов Azure из локальной среды или другого региона Azure.</span><span class="sxs-lookup"><span data-stu-id="647c5-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="647c5-150">Во время публикации hello эта функциональность была backported tooUbuntu 17.04 и Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="647c5-150">At hello time of publishing, this functionality has been backported tooUbuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="647c5-151">Если клиент Linux SMB не поддерживает шифрование, с помощью SMB 2.1 из в виртуальной Машине Linux Azure Подключите хранилища Azure File hello одного центра обработки данных, как hello учетной записи хранения файла.</span><span class="sxs-lookup"><span data-stu-id="647c5-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in hello same datacenter as hello File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="647c5-152">Низкая производительность файлового ресурса Azure, подключенного к виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="647c5-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="647c5-153">Причина:</span><span class="sxs-lookup"><span data-stu-id="647c5-153">Cause</span></span>

<span data-ttu-id="647c5-154">Одной из возможных причин снижения производительности может быть отключенное кэширование.</span><span class="sxs-lookup"><span data-stu-id="647c5-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="647c5-155">Решение</span><span class="sxs-lookup"><span data-stu-id="647c5-155">Solution</span></span>

<span data-ttu-id="647c5-156">toocheck ли кэширование отключено, найдите hello **кэша =** входа.</span><span class="sxs-lookup"><span data-stu-id="647c5-156">toocheck whether caching is disabled, look for hello **cache=** entry.</span></span> 

<span data-ttu-id="647c5-157">Запись **cache=none** означает, что кэширование отключено.</span><span class="sxs-lookup"><span data-stu-id="647c5-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="647c5-158">Общий ресурс hello повторного подключения с помощью команды mount по умолчанию hello или путем явного добавления hello **кэша = strict** включен параметр подключения toohello команды tooensure, кэширования или «strict» режим кэширования по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="647c5-158">Remount hello share by using hello default mount command or by explicitly adding hello **cache=strict** option toohello mount command tooensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="647c5-159">В некоторых сценариях hello **serverino** подключения может привести к hello **ls** stat toorun команду для каждой записи каталога.</span><span class="sxs-lookup"><span data-stu-id="647c5-159">In some scenarios, hello **serverino** mount option can cause hello **ls** command toorun stat against every directory entry.</span></span> <span data-ttu-id="647c5-160">Это приводит к снижению производительности при выводе содержимого больших каталогов.</span><span class="sxs-lookup"><span data-stu-id="647c5-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="647c5-161">Проверьте параметры подключения hello в вашей **/etc/fstab** входа:</span><span class="sxs-lookup"><span data-stu-id="647c5-161">You can check hello mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="647c5-162">Можно также проверить, используются ли hello правильные параметры, выполнив hello **подключения sudo | grep cifs** команда и проверка его выходные данные, например hello следующий пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="647c5-162">You can also check whether hello correct options are being used by running hello  **sudo mount | grep cifs** command and checking its output, such as hello following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="647c5-163">Если hello **кэша = strict** или **serverino** может не представлять, отключите и снова подключить хранилище файлов Azure, выполнив команду подключения hello из hello [документации](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="647c5-163">If hello **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running hello mount command from hello [documentation](storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="647c5-164">Затем, повторно проверьте что hello **/etc/fstab** запись имеет правильные параметры hello.</span><span class="sxs-lookup"><span data-stu-id="647c5-164">Then, recheck that hello **/etc/fstab** entry has hello correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a><span data-ttu-id="647c5-165">Отметки времени были потеряны при копировании файлов из Windows tooLinux</span><span class="sxs-lookup"><span data-stu-id="647c5-165">Time stamps were lost in copying files from Windows tooLinux</span></span>

<span data-ttu-id="647c5-166">На платформах, Linux и Unix, hello **cp -p** команда завершается ошибкой, если файл 1 и 2 принадлежат разным пользователям.</span><span class="sxs-lookup"><span data-stu-id="647c5-166">On Linux/Unix platforms, hello **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="647c5-167">Причина:</span><span class="sxs-lookup"><span data-stu-id="647c5-167">Cause</span></span>

<span data-ttu-id="647c5-168">Здравствуйте, флаг force **f** в COPYFILE результатов при выполнении **cp -p -f** в Unix.</span><span class="sxs-lookup"><span data-stu-id="647c5-168">hello force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="647c5-169">Эта команда также завершается неудачей, отметка времени toopreserve hello hello файла, который вы не владеете.</span><span class="sxs-lookup"><span data-stu-id="647c5-169">This command also fails toopreserve hello time stamp of hello file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="647c5-170">Возможное решение</span><span class="sxs-lookup"><span data-stu-id="647c5-170">Workaround</span></span>

<span data-ttu-id="647c5-171">Использовать hello пользователя учетной записи хранилища для копирования файлов hello:</span><span class="sxs-lookup"><span data-stu-id="647c5-171">Use hello storage account user for copying hello files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="647c5-172">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="647c5-172">Need help?</span></span> <span data-ttu-id="647c5-173">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="647c5-173">Contact support.</span></span>

<span data-ttu-id="647c5-174">Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="647c5-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
