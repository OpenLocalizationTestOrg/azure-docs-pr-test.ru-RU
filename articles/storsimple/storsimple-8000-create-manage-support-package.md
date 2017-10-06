---
title: "пакет поддержки серии StorSimple 8000 aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate, расшифровки и изменить пакет поддержки для вашего устройства серии StorSimple 8000."
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
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="b8fe4-103">Создание пакета поддержки StorSimple для устройства StorSimple серии 8000 и управление им</span><span class="sxs-lookup"><span data-stu-id="b8fe4-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="b8fe4-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b8fe4-104">Overview</span></span>

<span data-ttu-id="b8fe4-105">Пакет поддержки StorSimple — это простой в использовании механизм, который собирает все журналы tooassist технической поддержки Майкрософт с устранить любые проблемы устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="b8fe4-106">Hello собирать журналы зашифрованные и сжатые.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="b8fe4-107">Этот учебник включает toocreate пошаговые инструкции и управление ими hello пакет поддержки для вашего устройства серии StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-107">This tutorial includes step-by-step instructions toocreate and manage hello support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="b8fe4-108">При работе с StorSimple Virtual Array go слишком[создания пакета журналов](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="b8fe4-108">If you are working with a StorSimple Virtual Array, go too[generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="b8fe4-109">Создать пакет поддержки.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-109">Create a support package</span></span>

<span data-ttu-id="b8fe4-110">В некоторых случаях вам потребуется toomanually создать пакет поддержки hello через Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-110">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b8fe4-111">Например:</span><span class="sxs-lookup"><span data-stu-id="b8fe4-111">For example:</span></span>

* <span data-ttu-id="b8fe4-112">Если необходимо tooremove конфиденциальные сведения из журналов файлы предыдущих toosharing со службой поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-112">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="b8fe4-113">Если вам трудно Отправка hello пакета из-за проблем с tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-113">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="b8fe4-114">Созданный вручную пакет поддержки можно предоставить службе технической поддержки Майкрософт по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="b8fe4-115">Выполните следующие шаги toocreate пакета поддержки в Windows PowerShell для StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-115">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="b8fe4-116">toocreate пакета поддержки в Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="b8fe4-116">toocreate a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="b8fe4-117">toostart сеанс Windows PowerShell с правами администратора на удаленном компьютере hello, который использовал устройства StorSimple tooyour tooconnect, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="b8fe4-117">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="b8fe4-118">В сеансе Windows PowerShell hello подключение toohello консоли SSAdmin на устройстве:</span><span class="sxs-lookup"><span data-stu-id="b8fe4-118">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="b8fe4-119">Hello командной строки введите:</span><span class="sxs-lookup"><span data-stu-id="b8fe4-119">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="b8fe4-120">В hello открывшемся диалоговом окне введите пароль администратора устройства.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-120">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="b8fe4-121">пароль по умолчанию Hello — _Password1_.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-121">hello default password is _Password1_.</span></span>
     
      ![Диалоговое окно с учетными данными PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="b8fe4-123">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-123">Select **OK**.</span></span>
   4. <span data-ttu-id="b8fe4-124">Hello командной строки введите:</span><span class="sxs-lookup"><span data-stu-id="b8fe4-124">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="b8fe4-125">В открывшемся сеансе hello введите соответствующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-125">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="b8fe4-126">Для сетевых ресурсов, которые защищены паролем, введите:</span><span class="sxs-lookup"><span data-stu-id="b8fe4-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="b8fe4-127">Вам будет выведен на пароль, путь toohello общую сетевую папку и парольную фразу для шифрования (поскольку hello пакет поддержки зашифрован).</span><span class="sxs-lookup"><span data-stu-id="b8fe4-127">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="b8fe4-128">Затем создается пакет поддержки в указанную папку hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-128">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="b8fe4-129">Для общих папок, которые не защищен паролем, нет необходимости hello `-Credential` параметра.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-129">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="b8fe4-130">Введите hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="b8fe4-130">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="b8fe4-131">для обоих контроллеров в hello указанной общей сетевой папке создается пакет поддержки Hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-131">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="b8fe4-132">Это зашифрованный, сжатый файл, который может быть отправлен tooMicrosoft поддержки для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-132">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="b8fe4-133">Дополнительные сведения см. в статье [Обращение в службу поддержки Майкрософт](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b8fe4-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="b8fe4-134">параметры командлета Export-HcsSupportPackage Hello</span><span class="sxs-lookup"><span data-stu-id="b8fe4-134">hello Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="b8fe4-135">Можно использовать следующие параметры с помощью командлета Export-HcsSupportPackage hello hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-135">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="b8fe4-136">Параметр</span><span class="sxs-lookup"><span data-stu-id="b8fe4-136">Parameter</span></span> | <span data-ttu-id="b8fe4-137">Обязательный/необязательный</span><span class="sxs-lookup"><span data-stu-id="b8fe4-137">Required/Optional</span></span> | <span data-ttu-id="b8fe4-138">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="b8fe4-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="b8fe4-139">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b8fe4-139">Required</span></span> |<span data-ttu-id="b8fe4-140">Используйте расположение hello tooprovide hello общей сетевой папке в какой hello помещен пакет поддержки.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-140">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="b8fe4-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b8fe4-141">Required</span></span> |<span data-ttu-id="b8fe4-142">Используйте tooprovide toohelp парольной фразы шифрования пакета поддержки hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-142">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="b8fe4-143">Необязательно</span><span class="sxs-lookup"><span data-stu-id="b8fe4-143">Optional</span></span> |<span data-ttu-id="b8fe4-144">Использование учетных данных доступа toosupply для hello общей сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-144">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="b8fe4-145">Необязательно</span><span class="sxs-lookup"><span data-stu-id="b8fe4-145">Optional</span></span> |<span data-ttu-id="b8fe4-146">Используйте шага подтверждения парольной фразы шифрования tooskip hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-146">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="b8fe4-147">Необязательно</span><span class="sxs-lookup"><span data-stu-id="b8fe4-147">Optional</span></span> |<span data-ttu-id="b8fe4-148">Используйте в каталоге toospecify *путь* помещают пакет поддержки какие hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-148">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="b8fe4-149">по умолчанию Hello — [имя устройства]-[Текущая дата и время:ГГГГ-MM-дд-чч-мм-сс].</span><span class="sxs-lookup"><span data-stu-id="b8fe4-149">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="b8fe4-150">Необязательно</span><span class="sxs-lookup"><span data-stu-id="b8fe4-150">Optional</span></span> |<span data-ttu-id="b8fe4-151">Укажите в качестве **кластера** toocreate (по умолчанию) пакет поддержки для обоих контроллеров.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-151">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="b8fe4-152">Toocreate пакета только для текущего контроллера hello, укажите **контроллера**.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-152">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="b8fe4-153">Изменение пакета поддержки</span><span class="sxs-lookup"><span data-stu-id="b8fe4-153">Edit a support package</span></span>

<span data-ttu-id="b8fe4-154">После создания пакета поддержки может понадобиться tooedit hello tooremove конфиденциальных сведений о пакете.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-154">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="b8fe4-155">Это может включать имена томов, IP-адреса устройств и имена резервных копий из файлов журнала hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-155">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8fe4-156">Изменить можно только пакет поддержки, который был создан через Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b8fe4-157">Невозможно изменить пакет, созданный на портал Azure в службе диспетчера StorSimple устройство hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-157">You can't edit a package created in hello Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="b8fe4-158">tooedit пакет поддержки до отправки на сайт технической поддержки Microsoft hello, сначала расшифровать пакет поддержки hello, изменять файлы hello и повторно зашифровать.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-158">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="b8fe4-159">Выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-159">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="b8fe4-160">tooedit пакета поддержки в Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="b8fe4-160">tooedit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="b8fe4-161">Создать пакет поддержки, как описано ранее в [toocreate пакет поддержки в Windows PowerShell для StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="b8fe4-161">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="b8fe4-162">[Загрузка скрипта hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) локально на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-162">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="b8fe4-163">Импортируйте модуль Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-163">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="b8fe4-164">Укажите hello путь toohello локальной папке в которой был загружен скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-164">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="b8fe4-165">модуль hello tooimport, введите:</span><span class="sxs-lookup"><span data-stu-id="b8fe4-165">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="b8fe4-166">Все файлы hello, *.aes* файлы, которые сжаты и зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-166">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="b8fe4-167">toodecompress и расшифровки файлов, введите:</span><span class="sxs-lookup"><span data-stu-id="b8fe4-167">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="b8fe4-168">Обратите внимание, для всех файлов hello теперь отображаются фактические расширения hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-168">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Изменение пакета поддержки](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="b8fe4-170">Когда появится для hello парольную фразу для шифрования, введите hello парольную фразу, которая использовалась при создании пакета поддержки hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-170">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="b8fe4-171">Обзор toohello папки, содержащей файлы журналов hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-171">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="b8fe4-172">Поскольку файлы журнала hello распакованы и расшифрованы, это будет иметь исходное расширение файла.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-172">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="b8fe4-173">Изменять эти файлы tooremove сведений о конкретных клиентов, такие как имена томов и IP-адреса устройств и сохранять файлы hello.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-173">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="b8fe4-174">Закрыть hello файлы toocompress их с помощью gzip и их шифрования с помощью AES-256.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-174">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="b8fe4-175">Это необходимо для скорости и безопасности при передаче пакета поддержки hello по сети.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-175">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="b8fe4-176">toocompress и шифрование файлов, введите ниже hello:</span><span class="sxs-lookup"><span data-stu-id="b8fe4-176">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Изменение пакета поддержки](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="b8fe4-178">При появлении запроса введите парольную фразу для hello измененного пакета поддержки.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-178">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="b8fe4-179">Запишите hello новую парольную фразу, чтобы совместно использовать его службе технической поддержки Майкрософт по запросу.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-179">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="b8fe4-180">Пример: изменение файлов в пакете поддержки на ресурсе, защищенном паролем</span><span class="sxs-lookup"><span data-stu-id="b8fe4-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="b8fe4-181">Привет, в следующем примере показано, как toodecrypt, изменения и повторного шифрования пакета поддержки.</span><span class="sxs-lookup"><span data-stu-id="b8fe4-181">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="b8fe4-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b8fe4-182">Next steps</span></span>

* <span data-ttu-id="b8fe4-183">Дополнительные сведения о hello [данные, полученные из пакета поддержки hello](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="b8fe4-183">Learn about hello [information collected in hello Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="b8fe4-184">Узнайте, каким образом слишком[пакеты поддержки использования и устройства в журналах tootroubleshoot развертывания устройства](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="b8fe4-184">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="b8fe4-185">Узнайте, каким образом слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="b8fe4-185">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

