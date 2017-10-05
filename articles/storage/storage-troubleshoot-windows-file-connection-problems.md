---
title: "Устранение неполадок хранилища файлов Azure в Windows | Документация Майкрософт"
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
ms.openlocfilehash: 71a8f4edf7776556b383f446e5aad007748ef090
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="407a7-103">Устранение неполадок хранилища файлов Azure в Windows</span><span class="sxs-lookup"><span data-stu-id="407a7-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="407a7-104">В этой статье приведен список распространенных проблем, возникающих в хранилище файлов Microsoft Azure при подключении с клиентов Windows.</span><span class="sxs-lookup"><span data-stu-id="407a7-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="407a7-105">Кроме того, здесь представлены возможные причины этих проблем и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="407a7-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="407a7-106">Помимо действий по устранению неполадок, описываемых в этой статье, можно также использовать [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5), чтобы обеспечить выполнение необходимых условий для среды клиента Windows.</span><span class="sxs-lookup"><span data-stu-id="407a7-106">In addition to the troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that the Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="407a7-107">AzFileDiagnostics автоматизирует обнаружение большинства симптомов, упомянутых в этой статье, и помогает настроить среду для достижения оптимальной производительности.</span><span class="sxs-lookup"><span data-stu-id="407a7-107">AzFileDiagnostics automates detection of most of the symptoms mentioned in this article and helps set up your environment to get optimal performance.</span></span> <span data-ttu-id="407a7-108">Эту информацию можно найти также на странице [устранения неполадок с общими ресурсами Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares), где приведены пошаговые инструкции по устранению проблем с подключением и сопоставлением общих ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="407a7-108">You can also find this information in the [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps to assist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="407a7-109">Ошибка 53, 67 или 87 при попытке подключения или отключения файлового ресурса Azure</span><span class="sxs-lookup"><span data-stu-id="407a7-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="407a7-110">При попытке подключить файловый ресурс из локальной среды или другого центра обработки данных могут возникнуть следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="407a7-110">When you try to mount a file share from on-premises or from a different datacenter, you might receive the following errors:</span></span>

- <span data-ttu-id="407a7-111">"Произошла системная ошибка 53.</span><span class="sxs-lookup"><span data-stu-id="407a7-111">System error 53 has occurred.</span></span> <span data-ttu-id="407a7-112">Сетевой путь не найден".</span><span class="sxs-lookup"><span data-stu-id="407a7-112">The network path was not found.</span></span>
- <span data-ttu-id="407a7-113">"Произошла системная ошибка 67.</span><span class="sxs-lookup"><span data-stu-id="407a7-113">System error 67 has occurred.</span></span> <span data-ttu-id="407a7-114">Не найдено сетевое имя".</span><span class="sxs-lookup"><span data-stu-id="407a7-114">The network name cannot be found.</span></span>
- <span data-ttu-id="407a7-115">"Произошла системная ошибка 87.</span><span class="sxs-lookup"><span data-stu-id="407a7-115">System error 87 has occurred.</span></span> <span data-ttu-id="407a7-116">Неправильный параметр".</span><span class="sxs-lookup"><span data-stu-id="407a7-116">The parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="407a7-117">Причина 1: незашифрованный коммуникационный канал</span><span class="sxs-lookup"><span data-stu-id="407a7-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="407a7-118">По соображениям безопасности, если коммуникационный канал не зашифрован, а попытка подключения осуществляется не из того же центра обработки данных, в котором находятся файловые ресурсы Azure, то подключение к ним Azure будет заблокировано.</span><span class="sxs-lookup"><span data-stu-id="407a7-118">For security reasons, connections to Azure file shares are blocked if the communication channel isn’t encrypted and if the connection attempt isn't made from the same datacenter where the Azure file shares reside.</span></span> <span data-ttu-id="407a7-119">Шифрование коммуникационного канала выполняется, только если ОС клиента пользователя поддерживает шифрование SMB.</span><span class="sxs-lookup"><span data-stu-id="407a7-119">Communication channel encryption is provided only if the user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="407a7-120">Windows 8, Windows Server 2012 или более поздние версии этих ОС отправляют запрос на согласование, который включает протокол в себя SMB 3.0, поддерживающий шифрование.</span><span class="sxs-lookup"><span data-stu-id="407a7-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="407a7-121">Решение для причины 1</span><span class="sxs-lookup"><span data-stu-id="407a7-121">Solution for cause 1</span></span>

<span data-ttu-id="407a7-122">Подключитесь посредством клиента, который соответствует одному из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="407a7-122">Connect from a client that does one of the following:</span></span>

- <span data-ttu-id="407a7-123">соответствует требованиям для Windows 8 и Windows Server 2012 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="407a7-123">Meets the requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="407a7-124">подключается из виртуальной машины, размещенной в том же центре обработки данных, что и учетная запись хранения Azure, используемая для файлового ресурса Azure.</span><span class="sxs-lookup"><span data-stu-id="407a7-124">Connects from a virtual machine in the same datacenter as the Azure storage account that is used for the Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="407a7-125">Причина 2: порт 445 заблокирован</span><span class="sxs-lookup"><span data-stu-id="407a7-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="407a7-126">Системная ошибка 53 или системная ошибка 67 может произойти, если исходящие подключения через порт 445 к центру обработки данных хранилища файлов Azure заблокированы.</span><span class="sxs-lookup"><span data-stu-id="407a7-126">System error 53 or system error 67 can occur if port 445 outbound communication to an Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="407a7-127">Чтобы просмотреть сведения о поставщиках услуг Интернета, поддерживающих (или не поддерживающих) подключение через порт 445, перейдите на сайт [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="407a7-127">To see the summary of ISPs that allow or disallow access from port 445, go to [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="407a7-128">Чтобы определить, вызвана ли системная ошибка 53 этой причиной, отправьте запрос к конечной точке TCP:445 с помощью Portqry.</span><span class="sxs-lookup"><span data-stu-id="407a7-128">To understand whether this is the reason behind the "System error 53" message, you can use Portqry to query the TCP:445 endpoint.</span></span> <span data-ttu-id="407a7-129">Если конечная точка TCP:445 отображается как отфильтрованная, значит TCP-порт заблокирован.</span><span class="sxs-lookup"><span data-stu-id="407a7-129">If the TCP:445 endpoint is displayed as filtered, the TCP port is blocked.</span></span> <span data-ttu-id="407a7-130">Вот пример запроса:</span><span class="sxs-lookup"><span data-stu-id="407a7-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="407a7-131">Если TCP-порт 445 заблокирован правилом для сетевого пути, вы увидите такой результат:</span><span class="sxs-lookup"><span data-stu-id="407a7-131">If TCP port 445 is blocked by a rule along the network path, you will see the following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="407a7-132">Дополнительные сведения об использовании Portqry см. в статье [Описание запускаемого из командной строки средства Portqry.exe](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="407a7-132">For more information about how to use Portqry, see [Description of the Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="407a7-133">Решение для причины 2</span><span class="sxs-lookup"><span data-stu-id="407a7-133">Solution for cause 2</span></span>

<span data-ttu-id="407a7-134">Обратитесь в отдел ИТ, чтобы разрешить исходящий трафик через порт 445 для [диапазонов IP-адресов Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="407a7-134">Work with your IT department to open port 445 outbound to [Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="407a7-135">Причина 3: включена аутентификация NTLMv1</span><span class="sxs-lookup"><span data-stu-id="407a7-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="407a7-136">Системная ошибка 53 или 87 может произойти, если в клиенте включена аутентификация NTLMv1.</span><span class="sxs-lookup"><span data-stu-id="407a7-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on the client.</span></span> <span data-ttu-id="407a7-137">Хранилище файлов Azure поддерживает только аутентификацию NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="407a7-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="407a7-138">Протокол проверки подлинности NTLMv1 делает клиент менее безопасным,</span><span class="sxs-lookup"><span data-stu-id="407a7-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="407a7-139">в результате чего связь для хранилища файлов Azure блокируется.</span><span class="sxs-lookup"><span data-stu-id="407a7-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="407a7-140">Чтобы определить, заключается ли причина ошибки в этом, убедитесь, что для следующего подраздела реестра задано значение 3:</span><span class="sxs-lookup"><span data-stu-id="407a7-140">To determine whether this is the cause of the error, verify that the following registry subkey is set to a value of 3:</span></span>

<span data-ttu-id="407a7-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="407a7-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="407a7-142">Дополнительные сведения см. в статье [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) на сайте TechNet.</span><span class="sxs-lookup"><span data-stu-id="407a7-142">For more information, see the [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="407a7-143">Решение для причины 3</span><span class="sxs-lookup"><span data-stu-id="407a7-143">Solution for cause 3</span></span>

<span data-ttu-id="407a7-144">Верните параметру **LmCompatibilityLevel** значение по умолчанию (3) в следующем подразделе реестра:</span><span class="sxs-lookup"><span data-stu-id="407a7-144">Revert the **LmCompatibilityLevel** value to the default value of 3 in the following registry subkey:</span></span>

  <span data-ttu-id="407a7-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="407a7-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-to-process-this-command-when-you-copy-to-an-azure-file-share"></a><span data-ttu-id="407a7-146">Ошибка 1816 "Недостаточно квот для обработки команды" при копировании в файловый ресурс Azure</span><span class="sxs-lookup"><span data-stu-id="407a7-146">Error 1816 “Not enough quota is available to process this command” when you copy to an Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="407a7-147">Причина:</span><span class="sxs-lookup"><span data-stu-id="407a7-147">Cause</span></span>

<span data-ttu-id="407a7-148">Ошибка 1816 возникает, когда достигнуто максимальное количество одновременно открытых дескрипторов для файла на компьютере, к которому подключается файловый ресурс.</span><span class="sxs-lookup"><span data-stu-id="407a7-148">Error 1816 happens when you reach the upper limit of concurrent open handles that are allowed for a file on the computer where the file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="407a7-149">Решение</span><span class="sxs-lookup"><span data-stu-id="407a7-149">Solution</span></span>

<span data-ttu-id="407a7-150">Сократите количество одновременно открытых дескрипторов, закрыв некоторые из них, и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="407a7-150">Reduce the number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="407a7-151">Дополнительные сведения см. в статье [Производительность хранилища Microsoft Azure и контрольный список масштабируемости](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="407a7-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-windows"></a><span data-ttu-id="407a7-152">Медленное копирование файлов в хранилище файлов Azure и из него в Windows</span><span class="sxs-lookup"><span data-stu-id="407a7-152">Slow file copying to and from Azure File storage in Windows</span></span>

<span data-ttu-id="407a7-153">При попытке передать файлы в службу файлов Azure можно наблюдать низкую производительность.</span><span class="sxs-lookup"><span data-stu-id="407a7-153">You might see slow performance when you try to transfer files to the Azure File service.</span></span>

- <span data-ttu-id="407a7-154">Если определенные требования к минимальному размеру операций ввода-вывода отсутствуют, для оптимальной производительности мы рекомендуем использовать 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="407a7-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="407a7-155">Если окончательный размер файла, в который выполняются операции записи, известен, а у программного обеспечения нет проблем совместимости, и если еще не записанный заключительный фрагмент файла содержит нули, то укажите размер файла заранее вместо того, чтобы расширять его для каждой операции записи.</span><span class="sxs-lookup"><span data-stu-id="407a7-155">If you know the final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when the unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="407a7-156">Используйте правильный метод копирования:</span><span class="sxs-lookup"><span data-stu-id="407a7-156">Use the right copy method:</span></span>
    -   <span data-ttu-id="407a7-157">Используйте [AZCopy](storage-use-azcopy.md#file-copy) для передачи данных между двумя файловыми ресурсами.</span><span class="sxs-lookup"><span data-stu-id="407a7-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="407a7-158">Используйте [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) для передачи данных между файловыми ресурсами и локальным компьютером.</span><span class="sxs-lookup"><span data-stu-id="407a7-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="407a7-159">Рекомендации для Windows 8.1 или Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="407a7-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="407a7-160">Для клиентов, использующих Windows 8.1 или Windows Server 2012 R2, следует установить исправление [KB3114025](https://support.microsoft.com/help/3114025).</span><span class="sxs-lookup"><span data-stu-id="407a7-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that the [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="407a7-161">Это исправление повышает производительность операций создания и закрытия дескрипторов.</span><span class="sxs-lookup"><span data-stu-id="407a7-161">This hotfix improves the performance of create and close handles.</span></span>

<span data-ttu-id="407a7-162">Выполните следующий сценарий, чтобы проверить, установлено ли это исправление.</span><span class="sxs-lookup"><span data-stu-id="407a7-162">You can run the following script to check whether the hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="407a7-163">Если это так, выводятся следующие данные:</span><span class="sxs-lookup"><span data-stu-id="407a7-163">If hotfix is installed, the following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="407a7-164">Начиная с декабря 2015 года в образах Windows Server 2012 R2, содержащихся в Azure Marketplace, исправление KB3114025 установлено по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="407a7-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="407a7-165">В области **Мой компьютер** отсутствует папка с буквой диска</span><span class="sxs-lookup"><span data-stu-id="407a7-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="407a7-166">Если вы сопоставили файловый ресурс Azure от имени администратора с помощью команды net use, то может показаться, что он отсутствует.</span><span class="sxs-lookup"><span data-stu-id="407a7-166">If you map an Azure file share as an administrator by using net use, the share appears to be missing.</span></span>

### <a name="cause"></a><span data-ttu-id="407a7-167">Причина:</span><span class="sxs-lookup"><span data-stu-id="407a7-167">Cause</span></span>

<span data-ttu-id="407a7-168">По умолчанию проводник не запускается от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="407a7-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="407a7-169">При выполнении команды net use из командной строки администрирования пользователь подключает сетевой диск от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="407a7-169">If you run net use from an administrative command prompt, you map the network drive as an administrator.</span></span> <span data-ttu-id="407a7-170">Подключенные диски ориентированы на пользователя. Если для их подключения использовалась одна учетная запись, а пользователь вошел в систему с помощью другой, то диски отображаться не будут.</span><span class="sxs-lookup"><span data-stu-id="407a7-170">Because mapped drives are user-centric, the user account that is logged in does not display the drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="407a7-171">Решение</span><span class="sxs-lookup"><span data-stu-id="407a7-171">Solution</span></span>
<span data-ttu-id="407a7-172">Подключите общую папку из командной строки без прав администратора.</span><span class="sxs-lookup"><span data-stu-id="407a7-172">Mount the share from a non-administrator command line.</span></span> <span data-ttu-id="407a7-173">Кроме того, настройте значение регистра **EnableLinkedConnections**, следуя указаниям в [этой статье TechNet](https://technet.microsoft.com/library/ee844140.aspx).</span><span class="sxs-lookup"><span data-stu-id="407a7-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) to configure the **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-the-storage-account-contains-a-forward-slash"></a><span data-ttu-id="407a7-174">Если учетная запись хранения содержит косую черту (/), то выполнение команды net use завершается сбоем</span><span class="sxs-lookup"><span data-stu-id="407a7-174">Net use command fails if the storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="407a7-175">Причина:</span><span class="sxs-lookup"><span data-stu-id="407a7-175">Cause</span></span>

<span data-ttu-id="407a7-176">Команда net use интерпретирует косую черту (/) как параметр командной строки.</span><span class="sxs-lookup"><span data-stu-id="407a7-176">The net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="407a7-177">Если имя учетной записи пользователя начинается с косой черты, то сопоставление диска завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="407a7-177">If your user account name starts with a forward slash, the drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="407a7-178">Решение</span><span class="sxs-lookup"><span data-stu-id="407a7-178">Solution</span></span>

<span data-ttu-id="407a7-179">Чтобы обойти эту проблему, выполните одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="407a7-179">You can use either of the following steps to work around the problem:</span></span>

- <span data-ttu-id="407a7-180">Выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="407a7-180">Run the following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="407a7-181">Из пакетного файла выполнить команду можно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="407a7-181">From a batch file, you can run the command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="407a7-182">Заключите значение ключа в двойные прямые кавычки (если первый знак не является косой чертой).</span><span class="sxs-lookup"><span data-stu-id="407a7-182">Put double quotation marks around the key to work around this problem--unless the forward slash is the first character.</span></span> <span data-ttu-id="407a7-183">Если значение ключа начинается с косой черты (/), используйте интерактивный режим и введите пароль отдельно или повторно создайте ключи, которые не начинаются с этого знака.</span><span class="sxs-lookup"><span data-stu-id="407a7-183">If it is, either use the interactive mode and enter your password separately or regenerate your keys to get a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="407a7-184">Приложение или служба не может получить доступ к подключенному диску хранилища файлов Azure</span><span class="sxs-lookup"><span data-stu-id="407a7-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="407a7-185">Причина:</span><span class="sxs-lookup"><span data-stu-id="407a7-185">Cause</span></span>

<span data-ttu-id="407a7-186">Диски подключаются для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="407a7-186">Drives are mounted per user.</span></span> <span data-ttu-id="407a7-187">Если приложение или служба выполняется не под той учетной записью, к которой относится подключенный диск, то приложение не увидит этот диск.</span><span class="sxs-lookup"><span data-stu-id="407a7-187">If your application or service is running under a different user account than the one that mounted the drive, the application will not see the drive.</span></span>

### <a name="solution"></a><span data-ttu-id="407a7-188">Решение</span><span class="sxs-lookup"><span data-stu-id="407a7-188">Solution</span></span>

<span data-ttu-id="407a7-189">Используйте одно из следующих решений.</span><span class="sxs-lookup"><span data-stu-id="407a7-189">Use one of the following solutions:</span></span>

-   <span data-ttu-id="407a7-190">Используйте для подключения дисков учетную запись пользователя, содержащую это приложение.</span><span class="sxs-lookup"><span data-stu-id="407a7-190">Mount the drive from the same user account that contains the application.</span></span> <span data-ttu-id="407a7-191">Можно использовать такой инструмент, как PsExec.</span><span class="sxs-lookup"><span data-stu-id="407a7-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="407a7-192">Передайте имя и ключ учетной записи хранения в параметры имени пользователя и пароля команды net use.</span><span class="sxs-lookup"><span data-stu-id="407a7-192">Pass the storage account name and key in the user name and password parameters of the net use command.</span></span>

<span data-ttu-id="407a7-193">После выполнения этих инструкций при выполнении команды net use для учетной записи системы или сети может появиться следующее сообщение об ошибке: "Произошла системная ошибка 1312.</span><span class="sxs-lookup"><span data-stu-id="407a7-193">After you follow these instructions, you might receive the following error message when you run net use for the system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="407a7-194">A specified logon session does not exist.</span><span class="sxs-lookup"><span data-stu-id="407a7-194">A specified logon session does not exist.</span></span> <span data-ttu-id="407a7-195">Возможно, он уже завершен".</span><span class="sxs-lookup"><span data-stu-id="407a7-195">It may already have been terminated."</span></span> <span data-ttu-id="407a7-196">В этом случае убедитесь, что имя пользователя, переданное в net use, содержит сведения о домене (например, [имя_учетной_записи_хранения].file.core.windows.net).</span><span class="sxs-lookup"><span data-stu-id="407a7-196">If this occurs, make sure that the username that is passed to net use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-to-a-destination-that-does-not-support-encryption"></a><span data-ttu-id="407a7-197">Ошибка "Вы копируете файл в место, которое не поддерживает шифрование"</span><span class="sxs-lookup"><span data-stu-id="407a7-197">Error "You are copying a file to a destination that does not support encryption"</span></span>

<span data-ttu-id="407a7-198">Когда файл копируется по сети, он расшифровывается на исходном компьютере, передается в виде обычного текста и повторно шифруется в месте назначения.</span><span class="sxs-lookup"><span data-stu-id="407a7-198">When a file is copied over the network, the file is decrypted on the source computer, transmitted in plaintext, and re-encrypted at the destination.</span></span> <span data-ttu-id="407a7-199">Тем не менее при попытке скопировать зашифрованный файл может появиться следующее сообщение об ошибке: "Вы копируете файл в место, которое не поддерживает шифрование".</span><span class="sxs-lookup"><span data-stu-id="407a7-199">However, you might see the following error when you're trying to copy an encrypted file: "You are copying the file to a destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="407a7-200">Причина:</span><span class="sxs-lookup"><span data-stu-id="407a7-200">Cause</span></span>
<span data-ttu-id="407a7-201">Эта проблема может возникнуть при использовании шифрованной файловой системы (EFS).</span><span class="sxs-lookup"><span data-stu-id="407a7-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="407a7-202">Файлы с шифрованием BitLocker можно копировать в хранилище файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="407a7-202">BitLocker-encrypted files can be copied to Azure File storage.</span></span> <span data-ttu-id="407a7-203">Однако хранилище файлов Azure не поддерживает шифрованную файловую систему (EFS) NTFS.</span><span class="sxs-lookup"><span data-stu-id="407a7-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="407a7-204">Возможное решение</span><span class="sxs-lookup"><span data-stu-id="407a7-204">Workaround</span></span>
<span data-ttu-id="407a7-205">Чтобы скопировать файл по сети, его сначала необходимо расшифровать.</span><span class="sxs-lookup"><span data-stu-id="407a7-205">To copy a file over the network, you must first decrypt it.</span></span> <span data-ttu-id="407a7-206">Используйте один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="407a7-206">Use one of the following methods:</span></span>

- <span data-ttu-id="407a7-207">Используйте команду **copy /d**.</span><span class="sxs-lookup"><span data-stu-id="407a7-207">Use the **copy /d** command.</span></span> <span data-ttu-id="407a7-208">Она позволяет сохранить зашифрованные файлы как расшифрованные файлы в месте назначения.</span><span class="sxs-lookup"><span data-stu-id="407a7-208">It allows the encrypted files to be saved as decrypted files at the destination.</span></span>
- <span data-ttu-id="407a7-209">Настройте следующий раздел реестра:</span><span class="sxs-lookup"><span data-stu-id="407a7-209">Set the following registry key:</span></span>
  - <span data-ttu-id="407a7-210">путь: HKLM\Software\Policies\Microsoft\Windows\System;</span><span class="sxs-lookup"><span data-stu-id="407a7-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="407a7-211">тип значения: DWORD;</span><span class="sxs-lookup"><span data-stu-id="407a7-211">Value type = DWORD</span></span>
  - <span data-ttu-id="407a7-212">Name = CopyFileAllowDecryptedRemoteDestination;</span><span class="sxs-lookup"><span data-stu-id="407a7-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="407a7-213">Value = 1.</span><span class="sxs-lookup"><span data-stu-id="407a7-213">Value = 1</span></span>

<span data-ttu-id="407a7-214">Помните, что настройка раздела реестра влияет на все операции копирования в сетевые общие папки.</span><span class="sxs-lookup"><span data-stu-id="407a7-214">Be aware that setting the registry key affects all copy operations that are made to network shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="407a7-215">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="407a7-215">Need help?</span></span> <span data-ttu-id="407a7-216">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="407a7-216">Contact support.</span></span>
<span data-ttu-id="407a7-217">Если вам все еще нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), которая поможет быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="407a7-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
