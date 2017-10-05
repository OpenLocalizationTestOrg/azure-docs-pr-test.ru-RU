---
title: "Создание пакета поддержки StorSimple | Документация Майкрософт"
description: "Узнайте, как создавать, расшифровывать и изменять содержимое пакетов поддержки для устройства StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 32d20e7a8adcfc646c592213fe7395b87a93c985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="62dd5-103">Создание пакетов поддержки StorSimple и управление ими</span><span class="sxs-lookup"><span data-stu-id="62dd5-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="62dd5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="62dd5-104">Overview</span></span>
<span data-ttu-id="62dd5-105">Пакет поддержки StorSimple — это простой в использовании механизм, который собирает все соответствующие журналы, помогая службе технической поддержки Майкрософт устранять неполадки в работе устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="62dd5-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="62dd5-106">Собранные журналы шифруются и сжимаются.</span><span class="sxs-lookup"><span data-stu-id="62dd5-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="62dd5-107">В этом руководстве содержатся пошаговые инструкции по созданию пакета поддержки и управлению им.</span><span class="sxs-lookup"><span data-stu-id="62dd5-107">This tutorial includes step-by-step instructions to create and manage the support package.</span></span>

## <a name="create-and-upload-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="62dd5-108">Создание и отправка пакета поддержки на классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="62dd5-108">Create and upload a support package in the Azure classic portal</span></span>
<span data-ttu-id="62dd5-109">Можно создать и отправить пакет поддержки на сайт службы поддержки Майкрософт с помощью страницы **Обслуживание** для службы на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="62dd5-109">You can create and upload a support package to the Microsoft Support site through the **Maintenance** page of the service in the Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="62dd5-110">Для отправки требуется ключ доступа к поддержке.</span><span class="sxs-lookup"><span data-stu-id="62dd5-110">The upload requires a support passkey.</span></span> <span data-ttu-id="62dd5-111">Он должен быть предоставлен вам сотрудником службы поддержки по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="62dd5-111">Your support engineer should provide this to you in an email.</span></span>
> 
> 

<span data-ttu-id="62dd5-112">Зашифрованный и сжатый пакет поддержки (CAB-файл) создается и отправляется на сайт службы поддержки.</span><span class="sxs-lookup"><span data-stu-id="62dd5-112">An encrypted and compressed support package (.cab file) is created and uploaded to the Support site.</span></span> <span data-ttu-id="62dd5-113">Затем сотрудник службы поддержки может получить этот пакет с сайта технической поддержки для устранения неполадки.</span><span class="sxs-lookup"><span data-stu-id="62dd5-113">The support engineer can then retrieve this package from the Support site for troubleshooting the issue.</span></span>

<span data-ttu-id="62dd5-114">Чтобы создать пакет поддержки, выполните указанные ниже действия на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="62dd5-114">Perform the following steps in the classic portal to create a support package.</span></span>

#### <a name="to-create-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="62dd5-115">Создание пакета поддержки на классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="62dd5-115">To create a support package in the Azure classic portal</span></span>
1. <span data-ttu-id="62dd5-116">Выберите **Устройства** > **Обслуживание**.</span><span class="sxs-lookup"><span data-stu-id="62dd5-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="62dd5-117">В разделе **Пакет поддержки** щелкните **Создание и отправка пакета поддержки**.</span><span class="sxs-lookup"><span data-stu-id="62dd5-117">In the **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="62dd5-118">В окне **Создание и загрузка пакета поддержки** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62dd5-118">In the **Create and upload support package** dialog box, do the following:</span></span>
   
    ![Создание пакета поддержки](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="62dd5-120">В текстовое поле **Ключ доступа к поддержке** введите ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="62dd5-120">In the **Support Passkey** text box, enter the passkey.</span></span> <span data-ttu-id="62dd5-121">Этот ключ должен быть отправлен вам сотрудником службы поддержки Майкрософт в сообщении электронной почты.</span><span class="sxs-lookup"><span data-stu-id="62dd5-121">Your Microsoft support engineer should send this passkey to you in email.</span></span>
   * <span data-ttu-id="62dd5-122">Установите флажок, чтобы дать согласие на автоматическую отправку пакета поддержки на сайт службы поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="62dd5-122">Select the check box to provide consent to automatically upload the support package to the Microsoft Support site.</span></span>
   * <span data-ttu-id="62dd5-123">Щелкните значок галочки </span><span class="sxs-lookup"><span data-stu-id="62dd5-123">Click the check icon</span></span> ![значок с изображением флажка](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="62dd5-125">.</span><span class="sxs-lookup"><span data-stu-id="62dd5-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="62dd5-126">Создание пакета поддержки вручную</span><span class="sxs-lookup"><span data-stu-id="62dd5-126">Manually create a support package</span></span>
<span data-ttu-id="62dd5-127">В некоторых случаях необходимо вручную создать пакет поддержки с помощью Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="62dd5-127">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="62dd5-128">Например:</span><span class="sxs-lookup"><span data-stu-id="62dd5-128">For example:</span></span>

* <span data-ttu-id="62dd5-129">Если необходимо удалить конфиденциальную информацию из файлов журнала до их предоставления службе технической поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="62dd5-129">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="62dd5-130">Если возникают сложности с отправкой пакета из-за проблем с подключением.</span><span class="sxs-lookup"><span data-stu-id="62dd5-130">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="62dd5-131">Созданный вручную пакет поддержки можно предоставить службе технической поддержки Майкрософт по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="62dd5-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="62dd5-132">Для создания пакета поддержки в Windows PowerShell для StorSimple выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62dd5-132">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="62dd5-133">Создание пакета поддержки в Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="62dd5-133">To create a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="62dd5-134">Для запуска сеанса Windows PowerShell с правами администратора на удаленном компьютере, используемом для подключения к устройству StorSimple, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="62dd5-134">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="62dd5-135">В сеансе Windows PowerShell подключитесь к консоли SSAdmin устройства:</span><span class="sxs-lookup"><span data-stu-id="62dd5-135">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="62dd5-136">В командной строке введите:</span><span class="sxs-lookup"><span data-stu-id="62dd5-136">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="62dd5-137">В открывшемся диалоговом окне введите пароль администратора устройства.</span><span class="sxs-lookup"><span data-stu-id="62dd5-137">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="62dd5-138">Пароль по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="62dd5-138">The default password is:</span></span>
     
      `Password1`
     
      ![Диалоговое окно с учетными данными PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="62dd5-140">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="62dd5-140">Select **OK**.</span></span>
   * <span data-ttu-id="62dd5-141">В командной строке введите:</span><span class="sxs-lookup"><span data-stu-id="62dd5-141">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="62dd5-142">В открывшемся сеансе введите соответствующую команду.</span><span class="sxs-lookup"><span data-stu-id="62dd5-142">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="62dd5-143">Для сетевых ресурсов, которые защищены паролем, введите:</span><span class="sxs-lookup"><span data-stu-id="62dd5-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="62dd5-144">Будет предложено ввести пароль, путь к общей сетевой папке и парольную фразу для шифрования (поскольку пакет поддержки зашифрован).</span><span class="sxs-lookup"><span data-stu-id="62dd5-144">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="62dd5-145">Затем будет создан пакет поддержки в указанной папке.</span><span class="sxs-lookup"><span data-stu-id="62dd5-145">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="62dd5-146">Для общих папок, не защищенных паролем, указывать параметр `-Credential` не требуется.</span><span class="sxs-lookup"><span data-stu-id="62dd5-146">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="62dd5-147">Заполните следующие поля:</span><span class="sxs-lookup"><span data-stu-id="62dd5-147">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="62dd5-148">Пакет поддержки создается для обоих контроллеров в указанной общей сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="62dd5-148">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="62dd5-149">Это зашифрованный сжатый файл, который можно отправить в службу поддержки Майкрософт для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="62dd5-149">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="62dd5-150">Дополнительные сведения см. в статье [Обращение в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="62dd5-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="62dd5-151">Параметры командлета Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="62dd5-151">The Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="62dd5-152">С командлетом Export-HcsSupportPackage можно использовать следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="62dd5-152">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="62dd5-153">Параметр</span><span class="sxs-lookup"><span data-stu-id="62dd5-153">Parameter</span></span> | <span data-ttu-id="62dd5-154">Обязательный/необязательный</span><span class="sxs-lookup"><span data-stu-id="62dd5-154">Required/Optional</span></span> | <span data-ttu-id="62dd5-155">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="62dd5-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="62dd5-156">Обязательно</span><span class="sxs-lookup"><span data-stu-id="62dd5-156">Required</span></span> |<span data-ttu-id="62dd5-157">Позволяет указать расположение общей сетевой папки, в которой будет расположен пакет поддержки.</span><span class="sxs-lookup"><span data-stu-id="62dd5-157">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="62dd5-158">Обязательно</span><span class="sxs-lookup"><span data-stu-id="62dd5-158">Required</span></span> |<span data-ttu-id="62dd5-159">Позволяет указать парольную фразу для шифрования пакета поддержки.</span><span class="sxs-lookup"><span data-stu-id="62dd5-159">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="62dd5-160">Необязательно</span><span class="sxs-lookup"><span data-stu-id="62dd5-160">Optional</span></span> |<span data-ttu-id="62dd5-161">Позволяет передать учетные данные для доступа к общей сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="62dd5-161">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="62dd5-162">Необязательно</span><span class="sxs-lookup"><span data-stu-id="62dd5-162">Optional</span></span> |<span data-ttu-id="62dd5-163">Используется, чтобы пропустить шаг подтверждения парольной фразы шифрования.</span><span class="sxs-lookup"><span data-stu-id="62dd5-163">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="62dd5-164">Необязательно</span><span class="sxs-lookup"><span data-stu-id="62dd5-164">Optional</span></span> |<span data-ttu-id="62dd5-165">Позволяет указать в поле *Путь* каталог, в котором будет размещен пакет поддержки.</span><span class="sxs-lookup"><span data-stu-id="62dd5-165">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="62dd5-166">Значение по умолчанию — [имя устройства]-[текущая дата и время:гггг-ММ-дд-ЧЧ-мм-сс].</span><span class="sxs-lookup"><span data-stu-id="62dd5-166">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="62dd5-167">Необязательно</span><span class="sxs-lookup"><span data-stu-id="62dd5-167">Optional</span></span> |<span data-ttu-id="62dd5-168">Укажите в качестве значения **Cluster** (по умолчанию), чтобы создать пакет поддержки для обоих контроллеров.</span><span class="sxs-lookup"><span data-stu-id="62dd5-168">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="62dd5-169">Если требуется создать пакет только для текущего контроллера, укажите значение **Controller**.</span><span class="sxs-lookup"><span data-stu-id="62dd5-169">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="62dd5-170">Изменение пакета поддержки</span><span class="sxs-lookup"><span data-stu-id="62dd5-170">Edit a support package</span></span>
<span data-ttu-id="62dd5-171">Созданный пакет поддержки при необходимости можно изменить для удаления конфиденциальных сведений.</span><span class="sxs-lookup"><span data-stu-id="62dd5-171">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="62dd5-172">К таким сведениям относится имена томов, IP-адреса устройств и имена резервных копий из файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="62dd5-172">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62dd5-173">Изменить можно только пакет поддержки, который был создан через Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="62dd5-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="62dd5-174">Пакет, созданный на классическом портале Azure в службе диспетчера StorSimple, изменить нельзя.</span><span class="sxs-lookup"><span data-stu-id="62dd5-174">You can't edit a package created in the Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="62dd5-175">Чтобы изменить пакет поддержки перед отправкой на сайт технической поддержки корпорации Майкрософт, сначала расшифруйте пакет поддержки, внесите изменения в файлы, а затем снова зашифруйте пакет.</span><span class="sxs-lookup"><span data-stu-id="62dd5-175">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="62dd5-176">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62dd5-176">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="62dd5-177">Изменение пакета поддержки в Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="62dd5-177">To edit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="62dd5-178">Создайте пакет поддержки в соответствии с инструкциями в приведенном выше разделе [Создание пакета поддержки в Windows PowerShell для StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="62dd5-178">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="62dd5-179">[Загрузите скрипт](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) в локальную систему на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="62dd5-179">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="62dd5-180">Импортируйте модуль Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62dd5-180">Import the Windows PowerShell module.</span></span> <span data-ttu-id="62dd5-181">Укажите путь к локальной папке, в которую вы скачали скрипт.</span><span class="sxs-lookup"><span data-stu-id="62dd5-181">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="62dd5-182">Для импорта модуля введите команду:</span><span class="sxs-lookup"><span data-stu-id="62dd5-182">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="62dd5-183">Все файлы имеют расширение *AES*. Они сжаты и зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="62dd5-183">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="62dd5-184">Для распаковки и расшифровки файлов введите:</span><span class="sxs-lookup"><span data-stu-id="62dd5-184">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="62dd5-185">Обратите внимание, что теперь у всех файлов отображаются настоящие расширения.</span><span class="sxs-lookup"><span data-stu-id="62dd5-185">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Изменение пакета поддержки](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="62dd5-187">При появлении запроса введите парольную фразу, которая использовалась при создании пакета поддержки.</span><span class="sxs-lookup"><span data-stu-id="62dd5-187">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="62dd5-188">Перейдите в папку с файлами журналов.</span><span class="sxs-lookup"><span data-stu-id="62dd5-188">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="62dd5-189">Так как файлы журналов теперь распакованы и расшифрованы, у них будут исходные расширения.</span><span class="sxs-lookup"><span data-stu-id="62dd5-189">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="62dd5-190">Измените эти файлы, удалив информацию о пользователе (например, имена томов и IP-адреса устройств), и сохраните файлы.</span><span class="sxs-lookup"><span data-stu-id="62dd5-190">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="62dd5-191">Закройте файлы, чтобы сжать их с помощью средства gzip и зашифровать алгоритмом AES-256.</span><span class="sxs-lookup"><span data-stu-id="62dd5-191">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="62dd5-192">Это выполняется из соображений безопасности, а также для ускорения передачи пакета поддержки по сети.</span><span class="sxs-lookup"><span data-stu-id="62dd5-192">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="62dd5-193">Для сжатия и шифрования файлов введите следующее:</span><span class="sxs-lookup"><span data-stu-id="62dd5-193">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Изменение пакета поддержки](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="62dd5-195">По запросу введите парольную фразу для шифрования для измененного пакета поддержки.</span><span class="sxs-lookup"><span data-stu-id="62dd5-195">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="62dd5-196">Запишите новую парольную фразу, чтобы сообщить ее специалистам службы технической поддержки Майкрософт по запросу.</span><span class="sxs-lookup"><span data-stu-id="62dd5-196">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="62dd5-197">Пример: изменение файлов в пакете поддержки на ресурсе, защищенном паролем</span><span class="sxs-lookup"><span data-stu-id="62dd5-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="62dd5-198">Ниже приведен пример, демонстрирующий расшифровку, изменение и повторное шифрование пакета поддержки.</span><span class="sxs-lookup"><span data-stu-id="62dd5-198">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="62dd5-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62dd5-199">Next steps</span></span>
* <span data-ttu-id="62dd5-200">Узнайте об [использовании пакетов поддержки и журналов устройства для устранения неполадок при его развертывании](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="62dd5-200">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="62dd5-201">Узнайте об [использовании службы диспетчера StorSimple для администрирования устройства StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="62dd5-201">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

