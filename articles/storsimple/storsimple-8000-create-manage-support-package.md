---
title: "Создание пакета поддержки StorSimple серии 8000 | Документация Майкрософт"
description: "Узнайте, как создавать, расшифровывать и изменять содержимое пакетов поддержки для устройства StorSimple серии 8000."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 92abbb96b2117e10800de61b5c405a784453265b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="ab6fb-103">Создание пакета поддержки StorSimple для устройства StorSimple серии 8000 и управление им</span><span class="sxs-lookup"><span data-stu-id="ab6fb-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="ab6fb-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="ab6fb-104">Overview</span></span>

<span data-ttu-id="ab6fb-105">Пакет поддержки StorSimple — это простой в использовании механизм, который собирает все соответствующие журналы, помогая службе технической поддержки Майкрософт устранять неполадки в работе устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="ab6fb-106">Собранные журналы шифруются и сжимаются.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="ab6fb-107">Это руководство содержит пошаговые инструкции по созданию пакета поддержки для устройства StorSimple серии 8000 и управлению им.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-107">This tutorial includes step-by-step instructions to create and manage the support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="ab6fb-108">Если вы работаете с виртуальным массивом StorSimple, перейдите к [созданию пакета журналов](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="ab6fb-108">If you are working with a StorSimple Virtual Array, go to [generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="ab6fb-109">Создать пакет поддержки.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-109">Create a support package</span></span>

<span data-ttu-id="ab6fb-110">В некоторых случаях необходимо вручную создать пакет поддержки с помощью Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-110">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="ab6fb-111">Например:</span><span class="sxs-lookup"><span data-stu-id="ab6fb-111">For example:</span></span>

* <span data-ttu-id="ab6fb-112">Если необходимо удалить конфиденциальную информацию из файлов журнала до их предоставления службе технической поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-112">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="ab6fb-113">Если возникают сложности с отправкой пакета из-за проблем с подключением.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-113">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="ab6fb-114">Созданный вручную пакет поддержки можно предоставить службе технической поддержки Майкрософт по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="ab6fb-115">Для создания пакета поддержки в Windows PowerShell для StorSimple выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-115">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="ab6fb-116">Создание пакета поддержки в Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="ab6fb-116">To create a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="ab6fb-117">Для запуска сеанса Windows PowerShell с правами администратора на удаленном компьютере, используемом для подключения к устройству StorSimple, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ab6fb-117">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="ab6fb-118">В сеансе Windows PowerShell подключитесь к консоли SSAdmin устройства:</span><span class="sxs-lookup"><span data-stu-id="ab6fb-118">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="ab6fb-119">В командной строке введите:</span><span class="sxs-lookup"><span data-stu-id="ab6fb-119">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="ab6fb-120">В открывшемся диалоговом окне введите пароль администратора устройства.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-120">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="ab6fb-121">Пароль по умолчанию — _Password1_.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-121">The default password is _Password1_.</span></span>
     
      ![Диалоговое окно с учетными данными PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="ab6fb-123">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-123">Select **OK**.</span></span>
   4. <span data-ttu-id="ab6fb-124">В командной строке введите:</span><span class="sxs-lookup"><span data-stu-id="ab6fb-124">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="ab6fb-125">В открывшемся сеансе введите соответствующую команду.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-125">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="ab6fb-126">Для сетевых ресурсов, которые защищены паролем, введите:</span><span class="sxs-lookup"><span data-stu-id="ab6fb-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="ab6fb-127">Будет предложено ввести пароль, путь к общей сетевой папке и парольную фразу для шифрования (поскольку пакет поддержки зашифрован).</span><span class="sxs-lookup"><span data-stu-id="ab6fb-127">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="ab6fb-128">Затем будет создан пакет поддержки в указанной папке.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-128">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="ab6fb-129">Для общих папок, не защищенных паролем, указывать параметр `-Credential` не требуется.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-129">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="ab6fb-130">Заполните следующие поля:</span><span class="sxs-lookup"><span data-stu-id="ab6fb-130">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="ab6fb-131">Пакет поддержки создается для обоих контроллеров в указанной общей сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-131">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="ab6fb-132">Это зашифрованный сжатый файл, который можно отправить в службу поддержки Майкрософт для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-132">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="ab6fb-133">Дополнительные сведения см. в статье [Обращение в службу поддержки Майкрософт](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="ab6fb-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="ab6fb-134">Параметры командлета Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="ab6fb-134">The Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="ab6fb-135">С командлетом Export-HcsSupportPackage можно использовать следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-135">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="ab6fb-136">Параметр</span><span class="sxs-lookup"><span data-stu-id="ab6fb-136">Parameter</span></span> | <span data-ttu-id="ab6fb-137">Обязательный/необязательный</span><span class="sxs-lookup"><span data-stu-id="ab6fb-137">Required/Optional</span></span> | <span data-ttu-id="ab6fb-138">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="ab6fb-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="ab6fb-139">Обязательно</span><span class="sxs-lookup"><span data-stu-id="ab6fb-139">Required</span></span> |<span data-ttu-id="ab6fb-140">Позволяет указать расположение общей сетевой папки, в которой будет расположен пакет поддержки.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-140">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="ab6fb-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="ab6fb-141">Required</span></span> |<span data-ttu-id="ab6fb-142">Позволяет указать парольную фразу для шифрования пакета поддержки.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-142">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="ab6fb-143">Необязательно</span><span class="sxs-lookup"><span data-stu-id="ab6fb-143">Optional</span></span> |<span data-ttu-id="ab6fb-144">Позволяет передать учетные данные для доступа к общей сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-144">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="ab6fb-145">Необязательно</span><span class="sxs-lookup"><span data-stu-id="ab6fb-145">Optional</span></span> |<span data-ttu-id="ab6fb-146">Используется, чтобы пропустить шаг подтверждения парольной фразы шифрования.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-146">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="ab6fb-147">Необязательно</span><span class="sxs-lookup"><span data-stu-id="ab6fb-147">Optional</span></span> |<span data-ttu-id="ab6fb-148">Позволяет указать в поле *Путь* каталог, в котором будет размещен пакет поддержки.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-148">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="ab6fb-149">Значение по умолчанию — [имя устройства]-[текущая дата и время:гггг-ММ-дд-ЧЧ-мм-сс].</span><span class="sxs-lookup"><span data-stu-id="ab6fb-149">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="ab6fb-150">Необязательно</span><span class="sxs-lookup"><span data-stu-id="ab6fb-150">Optional</span></span> |<span data-ttu-id="ab6fb-151">Укажите в качестве значения **Cluster** (по умолчанию), чтобы создать пакет поддержки для обоих контроллеров.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-151">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="ab6fb-152">Если требуется создать пакет только для текущего контроллера, укажите значение **Controller**.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-152">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="ab6fb-153">Изменение пакета поддержки</span><span class="sxs-lookup"><span data-stu-id="ab6fb-153">Edit a support package</span></span>

<span data-ttu-id="ab6fb-154">Созданный пакет поддержки при необходимости можно изменить для удаления конфиденциальных сведений.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-154">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="ab6fb-155">К таким сведениям относится имена томов, IP-адреса устройств и имена резервных копий из файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-155">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab6fb-156">Изменить можно только пакет поддержки, который был создан через Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="ab6fb-157">Пакет, созданный на портале Azure в службе диспетчера устройств StorSimple, изменить нельзя.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-157">You can't edit a package created in the Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="ab6fb-158">Чтобы изменить пакет поддержки перед отправкой на сайт технической поддержки корпорации Майкрософт, сначала расшифруйте пакет поддержки, внесите изменения в файлы, а затем снова зашифруйте пакет.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-158">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="ab6fb-159">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-159">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="ab6fb-160">Изменение пакета поддержки в Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="ab6fb-160">To edit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="ab6fb-161">Создайте пакет поддержки в соответствии с инструкциями в приведенном выше разделе [Создание пакета поддержки в Windows PowerShell для StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="ab6fb-161">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="ab6fb-162">[Загрузите скрипт](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) в локальную систему на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-162">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="ab6fb-163">Импортируйте модуль Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-163">Import the Windows PowerShell module.</span></span> <span data-ttu-id="ab6fb-164">Укажите путь к локальной папке, в которую вы скачали скрипт.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-164">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="ab6fb-165">Для импорта модуля введите команду:</span><span class="sxs-lookup"><span data-stu-id="ab6fb-165">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="ab6fb-166">Все файлы имеют расширение *AES*. Они сжаты и зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-166">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="ab6fb-167">Для распаковки и расшифровки файлов введите:</span><span class="sxs-lookup"><span data-stu-id="ab6fb-167">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="ab6fb-168">Обратите внимание, что теперь у всех файлов отображаются настоящие расширения.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-168">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Изменение пакета поддержки](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="ab6fb-170">При появлении запроса введите парольную фразу, которая использовалась при создании пакета поддержки.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-170">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="ab6fb-171">Перейдите в папку с файлами журналов.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-171">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="ab6fb-172">Так как файлы журналов теперь распакованы и расшифрованы, у них будут исходные расширения.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-172">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="ab6fb-173">Измените эти файлы, удалив информацию о пользователе (например, имена томов и IP-адреса устройств), и сохраните файлы.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-173">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="ab6fb-174">Закройте файлы, чтобы сжать их с помощью средства gzip и зашифровать алгоритмом AES-256.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-174">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="ab6fb-175">Это выполняется из соображений безопасности, а также для ускорения передачи пакета поддержки по сети.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-175">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="ab6fb-176">Для сжатия и шифрования файлов введите следующее:</span><span class="sxs-lookup"><span data-stu-id="ab6fb-176">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Изменение пакета поддержки](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="ab6fb-178">По запросу введите парольную фразу для шифрования для измененного пакета поддержки.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-178">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="ab6fb-179">Запишите новую парольную фразу, чтобы сообщить ее специалистам службы технической поддержки Майкрософт по запросу.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-179">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="ab6fb-180">Пример: изменение файлов в пакете поддержки на ресурсе, защищенном паролем</span><span class="sxs-lookup"><span data-stu-id="ab6fb-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="ab6fb-181">Ниже приведен пример, демонстрирующий расшифровку, изменение и повторное шифрование пакета поддержки.</span><span class="sxs-lookup"><span data-stu-id="ab6fb-181">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="ab6fb-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ab6fb-182">Next steps</span></span>

* <span data-ttu-id="ab6fb-183">Дополнительные сведения о [данных, собираемых в пакете поддержки](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs).</span><span class="sxs-lookup"><span data-stu-id="ab6fb-183">Learn about the [information collected in the Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="ab6fb-184">Узнайте об [использовании пакетов поддержки и журналов устройства для устранения неполадок при его развертывании](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ab6fb-184">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="ab6fb-185">Узнайте, как [использовать службу диспетчера устройств StorSimple для администрирования устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ab6fb-185">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

