---
title: "Включение удаленного доступа для развертываний Azure в Eclipse"
description: "Узнайте, как включить удаленный доступ для развертываний Azure с помощью набора средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="a0c97-103">Включение удаленного доступа для развертываний Azure в Eclipse</span><span class="sxs-lookup"><span data-stu-id="a0c97-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="a0c97-104">Чтобы упростить устранение неполадок в развертываниях, вы можете включить и использовать удаленный доступ для подключения к виртуальной машине, на которой размещается ваше развертывание.</span><span class="sxs-lookup"><span data-stu-id="a0c97-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span></span> <span data-ttu-id="a0c97-105">Функциональность удаленного доступа основана на протоколе удаленного рабочего стола (RDP).</span><span class="sxs-lookup"><span data-stu-id="a0c97-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="a0c97-106">Вы можете настроить удаленный доступ для своего развертывания после его публикации в Azure, а при использовании Eclipse с операционной системой Windows вы можете настроить удаленный доступ перед публикацией в Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c97-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span></span> <span data-ttu-id="a0c97-107">Обратите внимание, что для подключения к виртуальной машине вашего развертывания в Azure потребуется клиент удаленного рабочего стола, совместимый с используемой операционной системой.</span><span class="sxs-lookup"><span data-stu-id="a0c97-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span></span>

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a><span data-ttu-id="a0c97-108">Включение удаленного доступа перед развертыванием в Azure</span><span class="sxs-lookup"><span data-stu-id="a0c97-108">How to enable Remote Access before you deploy to Azure</span></span>
> [!NOTE]
> <span data-ttu-id="a0c97-109">Чтобы включить удаленный доступ перед развертыванием приложения в Azure, необходимо использовать Eclipse в Windows.</span><span class="sxs-lookup"><span data-stu-id="a0c97-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="a0c97-110">На следующем рисунке показано диалоговое окно свойств **Удаленный доступ** , используемое для включения удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="a0c97-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span></span>

![][ic719494]

<span data-ttu-id="a0c97-111">Диалоговое окно свойств **Удаленный доступ** можно отобразить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="a0c97-111">There are two ways to display the **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="a0c97-112">Щелкните ссылку **Дополнительно** в разделе **Удаленный доступ** диалогового окна **Publish to Azure** (Публикация в Azure).</span><span class="sxs-lookup"><span data-stu-id="a0c97-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span></span>

* <span data-ttu-id="a0c97-113">Откройте диалоговое окно **Свойства** своего проекта Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c97-113">Open the **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="a0c97-114">При создании нового проекта развертывания Azure удаленный доступ в нем по умолчанию отключен.</span><span class="sxs-lookup"><span data-stu-id="a0c97-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="a0c97-115">Однако вы можете легко включить его, указав имя пользователя и пароль в диалоговом окне **Публикация в Azure** .</span><span class="sxs-lookup"><span data-stu-id="a0c97-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span></span> <span data-ttu-id="a0c97-116">Пароль удаленного доступа шифруется с использованием сертификатов X.509.</span><span class="sxs-lookup"><span data-stu-id="a0c97-116">The Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="a0c97-117">Если вы не предоставляете собственный сертификат, функция шифрования использует самозаверяющий сертификат, входящий в состав подключаемого модуля Azure для Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span></span> <span data-ttu-id="a0c97-118">Этот самозаверяющий сертификат находится в папке **cert** проекта Azure и сохранен в виде файла общедоступного сертификата (SampleRemoteAccessPublic.cer), а также в виде файла сертификата обмена личной информацией (PFX) (SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="a0c97-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="a0c97-119">Последний содержит закрытый ключ для сертификата, а также по умолчанию использует пароль **Password1**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="a0c97-120">Однако поскольку данный пароль общеизвестен, сертификат по умолчанию можно использовать в образовательных целях, но не для развертывания в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a0c97-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="a0c97-121">Поэтому если вы хотите включить удаленные сеансы для своих развертываний в любых целях, кроме образовательных, следует щелкнуть ссылку **Дополнительно** в диалоговом окне **Publish to Azure** (Публикация в Azure), чтобы указать собственный сертификат.</span><span class="sxs-lookup"><span data-stu-id="a0c97-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span></span> <span data-ttu-id="a0c97-122">Обратите внимание, что вам потребуется отправить PFX-версию сертификата в размещенную службу на портале управления Azure, чтобы служба Azure смогла расшифровать пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="a0c97-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span></span>

<span data-ttu-id="a0c97-123">В оставшейся части руководства показано, как включить удаленный доступ для проекта развертывания Azure, который изначально создавался с отключенным удаленным доступом.</span><span class="sxs-lookup"><span data-stu-id="a0c97-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="a0c97-124">В данном руководстве мы создадим новый самозаверяющий сертификат, PFX-файл которого будет иметь выбранный вами пароль.</span><span class="sxs-lookup"><span data-stu-id="a0c97-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="a0c97-125">Кроме того, вы можете использовать сертификат, выданный центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="a0c97-125">You also have the option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a><span data-ttu-id="a0c97-126">Включение удаленного доступа после развертывания в Azure</span><span class="sxs-lookup"><span data-stu-id="a0c97-126">How to enable Remote Access after you have deployed to Azure</span></span>
<span data-ttu-id="a0c97-127">Чтобы включить удаленный доступ после развертывания в Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a0c97-127">To enable remote access after you have deployed to Azure, use the following steps:</span></span>

1. <span data-ttu-id="a0c97-128">Выполните вход на портал управления, используя свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c97-128">Log into the Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="a0c97-129">В списке **Облачные службы**выберите развернутую облачную службу.</span><span class="sxs-lookup"><span data-stu-id="a0c97-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="a0c97-130">На веб-странице облачной службы щелкните ссылку **Настроить** .</span><span class="sxs-lookup"><span data-stu-id="a0c97-130">In the cloud service web page, click the **Configure** link</span></span>

4. <span data-ttu-id="a0c97-131">В нижней части страницы конфигурации щелкните ссылку **Удаленный** .</span><span class="sxs-lookup"><span data-stu-id="a0c97-131">On the bottom of the configuration page, click the **Remote** link</span></span>

5. <span data-ttu-id="a0c97-132">При отображении всплывающего диалогового окна:</span><span class="sxs-lookup"><span data-stu-id="a0c97-132">When the pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="a0c97-133">Укажите роль, для которой требуется разрешить удаленный доступ.</span><span class="sxs-lookup"><span data-stu-id="a0c97-133">Specify the Role you for which you want to enable remote access</span></span>

   * <span data-ttu-id="a0c97-134">Установите флажок **Включить удаленный рабочий стол** .</span><span class="sxs-lookup"><span data-stu-id="a0c97-134">Click to select the **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="a0c97-135">Укажите имя пользователя и пароль, которые вы хотите использовать для удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="a0c97-135">Specify a user name and password you want to use for remote access</span></span>
   
   * <span data-ttu-id="a0c97-136">Выберите используемый сертификат.</span><span class="sxs-lookup"><span data-stu-id="a0c97-136">Select the certificate to use</span></span>

6. <span data-ttu-id="a0c97-137">Нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="a0c97-137">Click **OK**</span></span> 

<span data-ttu-id="a0c97-138">Появится сообщение о внесении изменений в конфигурацию, которое может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a0c97-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span></span> <span data-ttu-id="a0c97-139">После завершения изменения конфигурации выполните действия, описанные в разделе **Удаленный вход в систему** ниже.</span><span class="sxs-lookup"><span data-stu-id="a0c97-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span></span>

## <a name="how-to-enable-remote-access-in-your-package"></a><span data-ttu-id="a0c97-140">Включение удаленного доступа в пакете</span><span class="sxs-lookup"><span data-stu-id="a0c97-140">How to enable Remote Access in your package</span></span>
1. <span data-ttu-id="a0c97-141">В области обозревателя проектов Eclipse щелкните правой кнопкой мыши свой проект Azure и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="a0c97-142">В диалоговом окне **Свойства** разверните узел **Azure** на левой панели и щелкните **Удаленный доступ**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="a0c97-143">В диалоговом окне **Удаленный доступ** установите флажок **Enable all roles to accept Remote Desktop Connections with these login credentials** (Разрешить всем ролям принимать подключения удаленного рабочего стола с этими учетными данными входа).</span><span class="sxs-lookup"><span data-stu-id="a0c97-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="a0c97-144">Укажите имя пользователя для подключения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="a0c97-144">Specify a user name for the Remote Desktop connection.</span></span>

5. <span data-ttu-id="a0c97-145">Укажите и подтвердите пароль для пользователя.</span><span class="sxs-lookup"><span data-stu-id="a0c97-145">Specify and confirm the password for the user.</span></span> <span data-ttu-id="a0c97-146">Значения имени пользователя и пароля в этом диалоговом окне будут использоваться при установке подключения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="a0c97-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="a0c97-147">(Обратите внимание, что этот пароль отличается от пароля PFX.)</span><span class="sxs-lookup"><span data-stu-id="a0c97-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="a0c97-148">Укажите дату истечения срока действия для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="a0c97-148">Specify the expiration date for the user account.</span></span>

7. <span data-ttu-id="a0c97-149">Щелкните элемент **Создать** для создания нового самозаверяющего сертификата.</span><span class="sxs-lookup"><span data-stu-id="a0c97-149">Click **New** to create a new self-signed certificate.</span></span> <span data-ttu-id="a0c97-150">(Кроме того, можно выбрать сертификат из рабочей области или файловой системы с помощью кнопки **Рабочая область** или **Файловая система** соответственно, но в этом руководстве мы создадим сертификат.)</span><span class="sxs-lookup"><span data-stu-id="a0c97-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="a0c97-151">В диалоговом окне **Новый сертификат** укажите и подтвердите пароль, который будет использоваться для PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="a0c97-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="a0c97-152">Примите предложенное значение **Имя (общее)**или используйте пользовательское имя.</span><span class="sxs-lookup"><span data-stu-id="a0c97-152">Accept the value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="a0c97-153">Укажите путь и имя файла для сохранения нового сертификата в виде CER-файла.</span><span class="sxs-lookup"><span data-stu-id="a0c97-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="a0c97-154">На этом и следующем шаге вы можете использовать папку **cert** проекта Azure, однако вы можете выбрать и другое расположение.</span><span class="sxs-lookup"><span data-stu-id="a0c97-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span></span> <span data-ttu-id="a0c97-155">В рамках данного руководства мы будем использовать **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="a0c97-156">(Перед тем, как продолжить, создайте папку **c:\mycert** или используйте имеющуюся.)</span><span class="sxs-lookup"><span data-stu-id="a0c97-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="a0c97-157">Укажите путь и имя файла для сохранения нового сертификата и его закрытого ключа в виде PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="a0c97-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="a0c97-158">В рамках этого руководства мы будем использовать **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="a0c97-159">Диалоговое окно **Новый сертификат** должно выглядеть следующим образом (обновите пути к папкам, если вы не использовали **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="a0c97-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="a0c97-160">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Новый сертификат**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-160">Click **OK** to close the **New Certificate** dialog.</span></span>

8. <span data-ttu-id="a0c97-161">Диалоговое окно **Удаленный доступ** должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="a0c97-161">Your **Remote Access** dialog should look similar to the following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="a0c97-162">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Удаленный доступ**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-162">Click **OK** to close the **Remote Access** dialog.</span></span>

<span data-ttu-id="a0c97-163">Перестройте свое приложение для развертывания в облаке.</span><span class="sxs-lookup"><span data-stu-id="a0c97-163">Rebuild your application, with the build set for deployment to cloud.</span></span>

## <a name="to-log-in-remotely"></a><span data-ttu-id="a0c97-164">Удаленный вход в систему</span><span class="sxs-lookup"><span data-stu-id="a0c97-164">To log in remotely</span></span>
<span data-ttu-id="a0c97-165">Когда экземпляр роли готов, вы можете удаленно войти на виртуальную машину, где размещается ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="a0c97-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="a0c97-166">Если вы используете Eclipse в Windows и вы выбрали параметр **Start remote desktop on deploy** (Запуск удаленного рабочего стола при развертывании) во время развертывания в Azure, отображается экран входа в подключение к удаленному рабочему столу при запуске развертывания.</span><span class="sxs-lookup"><span data-stu-id="a0c97-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="a0c97-167">При появлении запроса на ввод имени пользователя и пароля введите значения, указанные для удаленного пользователя, чтобы выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="a0c97-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

* <span data-ttu-id="a0c97-168">Другой способ удаленного вход заключается в использовании <a href="http://go.microsoft.com/fwlink/?LinkID=512959">портала управления Azure</a>:</span><span class="sxs-lookup"><span data-stu-id="a0c97-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="a0c97-169">В представлении **Облачные службы** на портале управления Azure выберите облачную службу, щелкните элемент **Экземпляры**, выберите определенный экземпляр и нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span></span> <span data-ttu-id="a0c97-170">Кнопка **Подключить** на панели команд выглядит так:</span><span class="sxs-lookup"><span data-stu-id="a0c97-170">The **Connect** button appears as the following in the command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="a0c97-171">После нажатия кнопки **Подключить** вам будет предложено открыть RDP-файл.</span><span class="sxs-lookup"><span data-stu-id="a0c97-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span></span> <span data-ttu-id="a0c97-172">Откройте файл и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="a0c97-172">Open the file and follow the prompts.</span></span> <span data-ttu-id="a0c97-173">(Кроме того, вы можете сохранить этот файл на локальном компьютере и затем дважды щелкнуть его для выполнения удаленного входа на виртуальную машину без перехода на портал управления.)</span><span class="sxs-lookup"><span data-stu-id="a0c97-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span></span>

  * <span data-ttu-id="a0c97-174">При появлении запроса на ввод имени пользователя и пароля введите значения, указанные для удаленного пользователя, чтобы выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="a0c97-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

> [!NOTE]
> <span data-ttu-id="a0c97-175">Если вы работаете с операционной системой, отличной от Windows, необходимо использовать клиент удаленного рабочего стола, совместимый с вашей операционной системой, настроив его с помощью параметров из скачанного RDP-файла в соответствии с приведенными ниже инструкциями.</span><span class="sxs-lookup"><span data-stu-id="a0c97-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="a0c97-176">См. также</span><span class="sxs-lookup"><span data-stu-id="a0c97-176">See Also</span></span>
<span data-ttu-id="a0c97-177">[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a0c97-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="a0c97-178">[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a0c97-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="a0c97-179">[Установка набора средств Azure для Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a0c97-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="a0c97-180">Дополнительные сведения об использовании Azure с Java можно найти в [Центре разработчиков Java для Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="a0c97-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
