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
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="d4c93-103">Устранение неполадок хранилища файлов Azure в Windows</span><span class="sxs-lookup"><span data-stu-id="d4c93-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="d4c93-104">В этой статье перечислены обычные проблемы, связанные tooMicrosoft хранилища Azure File при подключении клиентов Windows.</span><span class="sxs-lookup"><span data-stu-id="d4c93-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="d4c93-105">Кроме того, здесь представлены возможные причины этих проблем и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="d4c93-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="d4c93-106">В дополнение к этому toohello Устранение неполадок шаги в этой статье, можно также использовать [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) чтобы убедиться, что Windows hello среды клиента имеет правильные предварительные условия.</span><span class="sxs-lookup"><span data-stu-id="d4c93-106">In addition toohello troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that hello Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="d4c93-107">AzFileDiagnostics автоматизирует обнаружения большинства hello симптомы, упоминаемые в этой статье, а также помогает настроить оптимальной производительности tooget среды.</span><span class="sxs-lookup"><span data-stu-id="d4c93-107">AzFileDiagnostics automates detection of most of hello symptoms mentioned in this article and helps set up your environment tooget optimal performance.</span></span> <span data-ttu-id="d4c93-108">Кроме того, эти сведения можно найти в hello [Azure общих ресурсов средство устранения неполадок](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) , предоставляющий tooassist действия вы с проблемами подключения или сопоставление/монтажного Azure общих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4c93-108">You can also find this information in hello [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps tooassist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="d4c93-109">Ошибка 53, 67 или 87 при попытке подключения или отключения файлового ресурса Azure</span><span class="sxs-lookup"><span data-stu-id="d4c93-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="d4c93-110">При попытке toomount файловый ресурс из локальной или другом центре обработки данных, может появиться hello следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="d4c93-110">When you try toomount a file share from on-premises or from a different datacenter, you might receive hello following errors:</span></span>

- <span data-ttu-id="d4c93-111">"Произошла системная ошибка 53.</span><span class="sxs-lookup"><span data-stu-id="d4c93-111">System error 53 has occurred.</span></span> <span data-ttu-id="d4c93-112">Hello сетевой путь не найден.</span><span class="sxs-lookup"><span data-stu-id="d4c93-112">hello network path was not found.</span></span>
- <span data-ttu-id="d4c93-113">"Произошла системная ошибка 67.</span><span class="sxs-lookup"><span data-stu-id="d4c93-113">System error 67 has occurred.</span></span> <span data-ttu-id="d4c93-114">не удается найти имя сети Hello.</span><span class="sxs-lookup"><span data-stu-id="d4c93-114">hello network name cannot be found.</span></span>
- <span data-ttu-id="d4c93-115">"Произошла системная ошибка 87.</span><span class="sxs-lookup"><span data-stu-id="d4c93-115">System error 87 has occurred.</span></span> <span data-ttu-id="d4c93-116">Неверный параметр Hello.</span><span class="sxs-lookup"><span data-stu-id="d4c93-116">hello parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="d4c93-117">Причина 1: незашифрованный коммуникационный канал</span><span class="sxs-lookup"><span data-stu-id="d4c93-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="d4c93-118">По соображениям безопасности подключений tooAzure файловые ресурсы блокируются, если канал связи hello не зашифрованы и не предпринята попытка подключения hello из hello одного центра обработки данных, где находятся hello Azure общих папок.</span><span class="sxs-lookup"><span data-stu-id="d4c93-118">For security reasons, connections tooAzure file shares are blocked if hello communication channel isn’t encrypted and if hello connection attempt isn't made from hello same datacenter where hello Azure file shares reside.</span></span> <span data-ttu-id="d4c93-119">Шифрование канала связи предоставляется только в том случае, если пользователь hello клиентской ОС поддерживает шифрование SMB.</span><span class="sxs-lookup"><span data-stu-id="d4c93-119">Communication channel encryption is provided only if hello user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="d4c93-120">Windows 8, Windows Server 2012 или более поздние версии этих ОС отправляют запрос на согласование, который включает протокол в себя SMB 3.0, поддерживающий шифрование.</span><span class="sxs-lookup"><span data-stu-id="d4c93-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="d4c93-121">Решение для причины 1</span><span class="sxs-lookup"><span data-stu-id="d4c93-121">Solution for cause 1</span></span>

<span data-ttu-id="d4c93-122">Подключение от клиента, который выполняет одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="d4c93-122">Connect from a client that does one of hello following:</span></span>

- <span data-ttu-id="d4c93-123">Соответствует требованиям hello Windows 8 и Windows Server 2012 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="d4c93-123">Meets hello requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="d4c93-124">Соединяется с виртуальной машины в hello же центре обработки данных, как hello учетной записи хранилища Azure, которая используется для hello Azure общей папки</span><span class="sxs-lookup"><span data-stu-id="d4c93-124">Connects from a virtual machine in hello same datacenter as hello Azure storage account that is used for hello Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="d4c93-125">Причина 2: порт 445 заблокирован</span><span class="sxs-lookup"><span data-stu-id="d4c93-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="d4c93-126">Системная ошибка 53 или системная ошибка 67 может произойти, если заблокирован порт 445 исходящей связи tooan файла Azure хранилище центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="d4c93-126">System error 53 or system error 67 can occur if port 445 outbound communication tooan Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="d4c93-127">Сводка hello toosee поставщиков услуг Интернета, разрешить или запретить доступ к порту 445, go слишком[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4c93-127">toosee hello summary of ISPs that allow or disallow access from port 445, go too[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="d4c93-128">toounderstand ли это причиной hello приветственное сообщение «Системная ошибка 53», можно использовать Portqry tooquery hello TCP:445 endpoint.</span><span class="sxs-lookup"><span data-stu-id="d4c93-128">toounderstand whether this is hello reason behind hello "System error 53" message, you can use Portqry tooquery hello TCP:445 endpoint.</span></span> <span data-ttu-id="d4c93-129">Если конечная точка TCP:445 hello отображается как отфильтрованные, блокируется hello TCP-порт.</span><span class="sxs-lookup"><span data-stu-id="d4c93-129">If hello TCP:445 endpoint is displayed as filtered, hello TCP port is blocked.</span></span> <span data-ttu-id="d4c93-130">Вот пример запроса:</span><span class="sxs-lookup"><span data-stu-id="d4c93-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="d4c93-131">Если TCP-порт 445 заблокировано правилом вдоль hello сетевой путь, можно увидеть hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="d4c93-131">If TCP port 445 is blocked by a rule along hello network path, you will see hello following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="d4c93-132">Дополнительные сведения о разделе toouse Portqry, [описание программы командной строки Portqry.exe hello](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="d4c93-132">For more information about how toouse Portqry, see [Description of hello Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="d4c93-133">Решение для причины 2</span><span class="sxs-lookup"><span data-stu-id="d4c93-133">Solution for cause 2</span></span>

<span data-ttu-id="d4c93-134">Работать с портом tooopen отдел ИТ 445 исходящих слишком[Azure IP-диапазонов](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="d4c93-134">Work with your IT department tooopen port 445 outbound too[Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="d4c93-135">Причина 3: включена аутентификация NTLMv1</span><span class="sxs-lookup"><span data-stu-id="d4c93-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="d4c93-136">Системная ошибка 53 или системная ошибка 87 может произойти, если на клиенте hello включена связь NTLMv1.</span><span class="sxs-lookup"><span data-stu-id="d4c93-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on hello client.</span></span> <span data-ttu-id="d4c93-137">Хранилище файлов Azure поддерживает только аутентификацию NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="d4c93-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="d4c93-138">Протокол проверки подлинности NTLMv1 делает клиент менее безопасным,</span><span class="sxs-lookup"><span data-stu-id="d4c93-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="d4c93-139">в результате чего связь для хранилища файлов Azure блокируется.</span><span class="sxs-lookup"><span data-stu-id="d4c93-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="d4c93-140">toodetermine ли это причиной hello ошибки hello, убедитесь, что этой hello следующий подраздел реестра установлено значение tooa 3:</span><span class="sxs-lookup"><span data-stu-id="d4c93-140">toodetermine whether this is hello cause of hello error, verify that hello following registry subkey is set tooa value of 3:</span></span>

<span data-ttu-id="d4c93-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="d4c93-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="d4c93-142">Дополнительные сведения см. в разделе hello [параметра LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) на сайте TechNet.</span><span class="sxs-lookup"><span data-stu-id="d4c93-142">For more information, see hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="d4c93-143">Решение для причины 3</span><span class="sxs-lookup"><span data-stu-id="d4c93-143">Solution for cause 3</span></span>

<span data-ttu-id="d4c93-144">Вернуть hello **параметра LmCompatibilityLevel** значение toohello по умолчанию значение 3 в hello следующий подраздел реестра:</span><span class="sxs-lookup"><span data-stu-id="d4c93-144">Revert hello **LmCompatibilityLevel** value toohello default value of 3 in hello following registry subkey:</span></span>

  <span data-ttu-id="d4c93-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="d4c93-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a><span data-ttu-id="d4c93-146">Ошибка 1816 «недостаточно квоты имеет доступные tooprocess эта команда» при копировании tooan Azure общей папки</span><span class="sxs-lookup"><span data-stu-id="d4c93-146">Error 1816 “Not enough quota is available tooprocess this command” when you copy tooan Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="d4c93-147">Причина:</span><span class="sxs-lookup"><span data-stu-id="d4c93-147">Cause</span></span>

<span data-ttu-id="d4c93-148">Ошибка 1816 возникает, когда достигнут верхний предел hello параллельных открытых дескрипторов, разрешенные для файла на компьютере hello, где смонтирована hello общей папки.</span><span class="sxs-lookup"><span data-stu-id="d4c93-148">Error 1816 happens when you reach hello upper limit of concurrent open handles that are allowed for a file on hello computer where hello file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="d4c93-149">Решение</span><span class="sxs-lookup"><span data-stu-id="d4c93-149">Solution</span></span>

<span data-ttu-id="d4c93-150">Уменьшить hello число одновременных открытых дескрипторов, закрыв некоторые дескрипторы и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="d4c93-150">Reduce hello number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="d4c93-151">Дополнительные сведения см. в статье [Производительность хранилища Microsoft Azure и контрольный список масштабируемости](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="d4c93-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a><span data-ttu-id="d4c93-152">Файла низкая копирование tooand из хранилища Azure File в Windows</span><span class="sxs-lookup"><span data-stu-id="d4c93-152">Slow file copying tooand from Azure File storage in Windows</span></span>

<span data-ttu-id="d4c93-153">Может появиться снижения производительности при попытке toohello файлы tootransfer файловой службы Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c93-153">You might see slow performance when you try tootransfer files toohello Azure File service.</span></span>

- <span data-ttu-id="d4c93-154">Если у вас нет конкретные требования минимальный размер ввода-вывода, рекомендуется использовать 1 МБ, как hello размер ввода-вывода для достижения оптимальной производительности.</span><span class="sxs-lookup"><span data-stu-id="d4c93-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="d4c93-155">Если вы знаете hello окончательный размер файла, расширении с записывает и программного обеспечения имеет проблемы совместимости, если hello незаписанных заключительный фрагмент файла hello содержит нули, а затем набор hello размер файла заранее, а не выполняющего запись в расширенном режиме каждой операции записи.</span><span class="sxs-lookup"><span data-stu-id="d4c93-155">If you know hello final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when hello unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="d4c93-156">Используйте метод hello правой копирования:</span><span class="sxs-lookup"><span data-stu-id="d4c93-156">Use hello right copy method:</span></span>
    -   <span data-ttu-id="d4c93-157">Используйте [AZCopy](storage-use-azcopy.md#file-copy) для передачи данных между двумя файловыми ресурсами.</span><span class="sxs-lookup"><span data-stu-id="d4c93-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="d4c93-158">Используйте [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) для передачи данных между файловыми ресурсами и локальным компьютером.</span><span class="sxs-lookup"><span data-stu-id="d4c93-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="d4c93-159">Рекомендации для Windows 8.1 или Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d4c93-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="d4c93-160">Для клиентов, работающих под управлением Windows 8.1 или Windows Server 2012 R2, убедитесь, что hello [KB3114025](https://support.microsoft.com/help/3114025) установлено исправление.</span><span class="sxs-lookup"><span data-stu-id="d4c93-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that hello [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="d4c93-161">Это исправление повышает производительность hello инструкции create и закрытия дескрипторов.</span><span class="sxs-lookup"><span data-stu-id="d4c93-161">This hotfix improves hello performance of create and close handles.</span></span>

<span data-ttu-id="d4c93-162">Можно запустить следующий сценарий toocheck ли hello исправление установлено hello:</span><span class="sxs-lookup"><span data-stu-id="d4c93-162">You can run hello following script toocheck whether hello hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="d4c93-163">Если установлено исправление, hello выводятся следующие данные:</span><span class="sxs-lookup"><span data-stu-id="d4c93-163">If hotfix is installed, hello following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="d4c93-164">Начиная с декабря 2015 года в образах Windows Server 2012 R2, содержащихся в Azure Marketplace, исправление KB3114025 установлено по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d4c93-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="d4c93-165">В области **Мой компьютер** отсутствует папка с буквой диска</span><span class="sxs-lookup"><span data-stu-id="d4c93-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="d4c93-166">Если сопоставить Azure файловый ресурс от имени администратора с помощью команды net use, hello выступает toobe отсутствует.</span><span class="sxs-lookup"><span data-stu-id="d4c93-166">If you map an Azure file share as an administrator by using net use, hello share appears toobe missing.</span></span>

### <a name="cause"></a><span data-ttu-id="d4c93-167">Причина:</span><span class="sxs-lookup"><span data-stu-id="d4c93-167">Cause</span></span>

<span data-ttu-id="d4c93-168">По умолчанию проводник не запускается от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="d4c93-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="d4c93-169">При запуске команды net use из командной строки с правами администратора, можно подключить сетевой диск hello с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="d4c93-169">If you run net use from an administrative command prompt, you map hello network drive as an administrator.</span></span> <span data-ttu-id="d4c93-170">Так как подключенные сетевые диски ориентированное на пользователей, hello учетной записи пользователя, зарегистрированного в не отображает hello диски при подключении под другой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="d4c93-170">Because mapped drives are user-centric, hello user account that is logged in does not display hello drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="d4c93-171">Решение</span><span class="sxs-lookup"><span data-stu-id="d4c93-171">Solution</span></span>
<span data-ttu-id="d4c93-172">Общая папка hello подключения из командной строки без прав администратора.</span><span class="sxs-lookup"><span data-stu-id="d4c93-172">Mount hello share from a non-administrator command line.</span></span> <span data-ttu-id="d4c93-173">Кроме того, можно выполнить [в этом разделе TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** значение реестра.</span><span class="sxs-lookup"><span data-stu-id="d4c93-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a><span data-ttu-id="d4c93-174">Команды net use завершается сбоем, если учетная запись хранения hello содержит косой черты</span><span class="sxs-lookup"><span data-stu-id="d4c93-174">Net use command fails if hello storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="d4c93-175">Причина:</span><span class="sxs-lookup"><span data-stu-id="d4c93-175">Cause</span></span>

<span data-ttu-id="d4c93-176">команды net use Hello интерпретирует косой черты (/), как параметр командной строки.</span><span class="sxs-lookup"><span data-stu-id="d4c93-176">hello net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="d4c93-177">Если имя пользователя учетной записи начинается с косой черты, сопоставление дисков hello завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="d4c93-177">If your user account name starts with a forward slash, hello drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="d4c93-178">Решение</span><span class="sxs-lookup"><span data-stu-id="d4c93-178">Solution</span></span>

<span data-ttu-id="d4c93-179">Можно использовать любой из следующих шагов toowork проблемы hello hello:</span><span class="sxs-lookup"><span data-stu-id="d4c93-179">You can use either of hello following steps toowork around hello problem:</span></span>

- <span data-ttu-id="d4c93-180">Выполните следующую команду PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="d4c93-180">Run hello following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="d4c93-181">Из пакетного файла можно выполнить команду hello таким образом:</span><span class="sxs-lookup"><span data-stu-id="d4c93-181">From a batch file, you can run hello command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="d4c93-182">Поместите двойных кавычек вокруг hello ключа toowork этой проблемы — Если hello первый символ косой черты hello.</span><span class="sxs-lookup"><span data-stu-id="d4c93-182">Put double quotation marks around hello key toowork around this problem--unless hello forward slash is hello first character.</span></span> <span data-ttu-id="d4c93-183">Если это так, используйте hello интерактивный режим и отдельно введите пароль или повторно создать ваш ключи tooget ключ, который не начинается с косой черты.</span><span class="sxs-lookup"><span data-stu-id="d4c93-183">If it is, either use hello interactive mode and enter your password separately or regenerate your keys tooget a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="d4c93-184">Приложение или служба не может получить доступ к подключенному диску хранилища файлов Azure</span><span class="sxs-lookup"><span data-stu-id="d4c93-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="d4c93-185">Причина:</span><span class="sxs-lookup"><span data-stu-id="d4c93-185">Cause</span></span>

<span data-ttu-id="d4c93-186">Диски подключаются для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="d4c93-186">Drives are mounted per user.</span></span> <span data-ttu-id="d4c93-187">Если приложение или служба выполняется под другой учетной записью чем hello, присоединенного диска hello, приложение hello не будут видеть hello диска.</span><span class="sxs-lookup"><span data-stu-id="d4c93-187">If your application or service is running under a different user account than hello one that mounted hello drive, hello application will not see hello drive.</span></span>

### <a name="solution"></a><span data-ttu-id="d4c93-188">Решение</span><span class="sxs-lookup"><span data-stu-id="d4c93-188">Solution</span></span>

<span data-ttu-id="d4c93-189">Используйте один из hello следующие решения:</span><span class="sxs-lookup"><span data-stu-id="d4c93-189">Use one of hello following solutions:</span></span>

-   <span data-ttu-id="d4c93-190">Подключить диск hello из hello же учетной записью пользователя, содержащего приложение hello.</span><span class="sxs-lookup"><span data-stu-id="d4c93-190">Mount hello drive from hello same user account that contains hello application.</span></span> <span data-ttu-id="d4c93-191">Можно использовать такой инструмент, как PsExec.</span><span class="sxs-lookup"><span data-stu-id="d4c93-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="d4c93-192">Передайте hello имя учетной записи хранения и ключ hello пользователя имя и пароль параметры команды net use hello.</span><span class="sxs-lookup"><span data-stu-id="d4c93-192">Pass hello storage account name and key in hello user name and password parameters of hello net use command.</span></span>

<span data-ttu-id="d4c93-193">После выполнения этих инструкций может появиться hello, при запуске команды net use для учетной записи службы системы или сети hello следующие сообщение об ошибке: «Произошла системная ошибка 1312.</span><span class="sxs-lookup"><span data-stu-id="d4c93-193">After you follow these instructions, you might receive hello following error message when you run net use for hello system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="d4c93-194">A specified logon session does not exist.</span><span class="sxs-lookup"><span data-stu-id="d4c93-194">A specified logon session does not exist.</span></span> <span data-ttu-id="d4c93-195">Возможно, он уже завершен".</span><span class="sxs-lookup"><span data-stu-id="d4c93-195">It may already have been terminated."</span></span> <span data-ttu-id="d4c93-196">В этом случае убедитесь, что username hello, передаваемое используйте toonet включает сведения о домене (например: «[имя учетной записи хранилища]. file.core.windows .net»).</span><span class="sxs-lookup"><span data-stu-id="d4c93-196">If this occurs, make sure that hello username that is passed toonet use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a><span data-ttu-id="d4c93-197">Ошибка «Копировании назначения tooa файл, который не поддерживает шифрование»</span><span class="sxs-lookup"><span data-stu-id="d4c93-197">Error "You are copying a file tooa destination that does not support encryption"</span></span>

<span data-ttu-id="d4c93-198">При копировании файла по сети hello hello файла расшифровывается на исходном компьютере hello, передается в виде обычного текста и повторно зашифрованы в месте назначения hello.</span><span class="sxs-lookup"><span data-stu-id="d4c93-198">When a file is copied over hello network, hello file is decrypted on hello source computer, transmitted in plaintext, and re-encrypted at hello destination.</span></span> <span data-ttu-id="d4c93-199">Тем не менее, может появиться следующая ошибка, если вы пытаетесь toocopy зашифрованный файл hello: «Выполняется копирование hello файл tooa назначения, который не поддерживает шифрование».</span><span class="sxs-lookup"><span data-stu-id="d4c93-199">However, you might see hello following error when you're trying toocopy an encrypted file: "You are copying hello file tooa destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="d4c93-200">Причина:</span><span class="sxs-lookup"><span data-stu-id="d4c93-200">Cause</span></span>
<span data-ttu-id="d4c93-201">Эта проблема может возникнуть при использовании шифрованной файловой системы (EFS).</span><span class="sxs-lookup"><span data-stu-id="d4c93-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="d4c93-202">Файлы, зашифрованные BitLocker может быть tooAzure скопированный файл хранилища.</span><span class="sxs-lookup"><span data-stu-id="d4c93-202">BitLocker-encrypted files can be copied tooAzure File storage.</span></span> <span data-ttu-id="d4c93-203">Однако хранилище файлов Azure не поддерживает шифрованную файловую систему (EFS) NTFS.</span><span class="sxs-lookup"><span data-stu-id="d4c93-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="d4c93-204">Возможное решение</span><span class="sxs-lookup"><span data-stu-id="d4c93-204">Workaround</span></span>
<span data-ttu-id="d4c93-205">toocopy файл hello сети, необходимо сначала расшифровать его.</span><span class="sxs-lookup"><span data-stu-id="d4c93-205">toocopy a file over hello network, you must first decrypt it.</span></span> <span data-ttu-id="d4c93-206">Используйте один из следующих методов hello.</span><span class="sxs-lookup"><span data-stu-id="d4c93-206">Use one of hello following methods:</span></span>

- <span data-ttu-id="d4c93-207">Используйте hello **скопируйте /d** команды.</span><span class="sxs-lookup"><span data-stu-id="d4c93-207">Use hello **copy /d** command.</span></span> <span data-ttu-id="d4c93-208">Он позволяет hello зашифрованные файлы toobe как расшифрованных в месте назначения hello.</span><span class="sxs-lookup"><span data-stu-id="d4c93-208">It allows hello encrypted files toobe saved as decrypted files at hello destination.</span></span>
- <span data-ttu-id="d4c93-209">Набор hello следующий раздел реестра:</span><span class="sxs-lookup"><span data-stu-id="d4c93-209">Set hello following registry key:</span></span>
  - <span data-ttu-id="d4c93-210">путь: HKLM\Software\Policies\Microsoft\Windows\System;</span><span class="sxs-lookup"><span data-stu-id="d4c93-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="d4c93-211">тип значения: DWORD;</span><span class="sxs-lookup"><span data-stu-id="d4c93-211">Value type = DWORD</span></span>
  - <span data-ttu-id="d4c93-212">Name = CopyFileAllowDecryptedRemoteDestination;</span><span class="sxs-lookup"><span data-stu-id="d4c93-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="d4c93-213">Value = 1.</span><span class="sxs-lookup"><span data-stu-id="d4c93-213">Value = 1</span></span>

<span data-ttu-id="d4c93-214">Имейте в виду, что разделу реестра hello параметр влияет на все операции копирования, сделанных toonetwork общих папок.</span><span class="sxs-lookup"><span data-stu-id="d4c93-214">Be aware that setting hello registry key affects all copy operations that are made toonetwork shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="d4c93-215">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="d4c93-215">Need help?</span></span> <span data-ttu-id="d4c93-216">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="d4c93-216">Contact support.</span></span>
<span data-ttu-id="d4c93-217">Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="d4c93-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
