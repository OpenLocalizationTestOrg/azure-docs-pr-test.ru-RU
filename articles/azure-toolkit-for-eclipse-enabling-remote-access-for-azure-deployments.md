---
title: "aaaEnabling удаленного доступа для развертываний Azure в Eclipse"
description: "Узнайте, как tooenable доступ для развертываний Azure, с помощью hello набора средств Azure для Eclipse."
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
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="0b9af-103">Включение удаленного доступа для развертываний Azure в Eclipse</span><span class="sxs-lookup"><span data-stu-id="0b9af-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="0b9af-104">toohelp проблем развертывания, можно включить и использовать удаленный доступ toohello tooconnect виртуальная машина, содержащая развертывания.</span><span class="sxs-lookup"><span data-stu-id="0b9af-104">toohelp troubleshoot your deployments, you may enable and use Remote Access tooconnect toohello virtual machine hosting your deployment.</span></span> <span data-ttu-id="0b9af-105">Hello функциональные возможности удаленного доступа зависит от hello удаленного рабочего стола (RDP).</span><span class="sxs-lookup"><span data-stu-id="0b9af-105">hello Remote Access functionality relies on hello Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="0b9af-106">Можно настроить удаленный доступ для развертывания после его публикации tooAzure или если вы используете Eclipse с операционной системой Windows, можно настроить удаленный доступ перед публикацией tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0b9af-106">You can configure Remote Access for your deployment after you have published it tooAzure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish tooAzure.</span></span> <span data-ttu-id="0b9af-107">Обратите внимание, что вам потребуется клиент удаленного рабочего стола, совместимый с операционной системой на виртуальной машине порядок tooconnect tooyour развертывания в Azure.</span><span class="sxs-lookup"><span data-stu-id="0b9af-107">Note that you will need a remote desktop client that is compatible with your operating system in order tooconnect tooyour deployment's virtual machine in Azure.</span></span>

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a><span data-ttu-id="0b9af-108">Как tooenable удаленного доступа, прежде чем развертывать tooAzure</span><span class="sxs-lookup"><span data-stu-id="0b9af-108">How tooenable Remote Access before you deploy tooAzure</span></span>
> [!NOTE]
> <span data-ttu-id="0b9af-109">tooenable удаленного доступа перед развертыванием tooAzure вашего приложения, необходимо toobe выполнения Eclipse в Windows.</span><span class="sxs-lookup"><span data-stu-id="0b9af-109">tooenable Remote Access before you deploy your application tooAzure, you need toobe running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="0b9af-110">Hello на рисунке показаны hello **удаленного доступа** диалоговое окно свойств используется tooenable удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="0b9af-110">hello following image shows hello **Remote Access** properties dialog used tooenable remote access.</span></span>

![][ic719494]

<span data-ttu-id="0b9af-111">Существует два способа toodisplay hello **удаленного доступа** диалогового окна свойств:</span><span class="sxs-lookup"><span data-stu-id="0b9af-111">There are two ways toodisplay hello **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="0b9af-112">Нажмите кнопку hello **Дополнительно** ссылку в hello **удаленного доступа** раздел hello **публикации tooAzure** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0b9af-112">Click hello **Advanced** link in hello **Remote Access** section of hello **Publish tooAzure** dialog.</span></span>

* <span data-ttu-id="0b9af-113">Откройте hello **свойства** диалоговое окно проекта Azure.</span><span class="sxs-lookup"><span data-stu-id="0b9af-113">Open hello **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="0b9af-114">При создании нового проекта развертывания Azure hello проект не будет включен по умолчанию удаленный доступ.</span><span class="sxs-lookup"><span data-stu-id="0b9af-114">When you create a new Azure deployment project, hello project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="0b9af-115">Тем не менее, можно легко включить удаленный доступ, указав hello имя пользователя и пароль в hello **публикации tooAzure** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0b9af-115">However, you can easily enable remote access by specifying hello user name and password in hello **Publish tooAzure** dialog.</span></span> <span data-ttu-id="0b9af-116">пароль удаленного доступа Hello шифруется с использованием сертификатов X.509.</span><span class="sxs-lookup"><span data-stu-id="0b9af-116">hello Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="0b9af-117">Если вы не используете предоставить собственный сертификат hello шифрование использует самозаверяющий сертификат, поставляемых с hello подключаемый модуль Azure для Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0b9af-117">If you do not use provide your own certificate, hello encryption relies on a self-signed certificate shipped with hello Azure Plugin for Eclipse.</span></span> <span data-ttu-id="0b9af-118">Этот самозаверяющий сертификат находится в hello **cert** папку проекта Azure хранится как в виде файла открытого сертификата (SampleRemoteAccessPublic.cer) и файл сертификата как с обмена личной информацией (PFX) () SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="0b9af-118">This self-signed certificate is in hello **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="0b9af-119">последний Hello содержит закрытый ключ сертификата hello hello, и он имеет значение пароля по умолчанию **Password1**.</span><span class="sxs-lookup"><span data-stu-id="0b9af-119">hello latter contains hello private key for hello certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="0b9af-120">Тем не менее поскольку этот пароль разглашен, сертификат по умолчанию hello следует использовать только для изучения, но не для развертывания в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="0b9af-120">However, since this password is public knowledge, hello default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="0b9af-121">Поэтому за исключением в целях обучения, при необходимости tooenabled удаленные сеансы для своего развертывания, необходимо нажать кнопку hello **Дополнительно** ссылку в hello **публикации tooAzure** toospecify диалоговое окно собственные сертификат.</span><span class="sxs-lookup"><span data-stu-id="0b9af-121">So other than for learning purposes, when you want tooenabled remote sessions for your deployments, you should click hello **Advanced** link in hello **Publish tooAzure** dialog toospecify your own certificate.</span></span> <span data-ttu-id="0b9af-122">Обратите внимание, что вам требуется tooupload hello PFX-версию сертификата tooyour hello размещенной службы в пределах hello портала управления Azure, поэтому у Azure может расшифровать пароль пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="0b9af-122">Note that you'll need tooupload hello PFX version of hello certificate tooyour hosted service within hello Azure Management Portal, so that Azure can decrypt hello user password.</span></span>

<span data-ttu-id="0b9af-123">Остаток Hello hello учебника показано, как tooenable удаленный доступ к проект развертывания Azure, которая была создана с отключенным удаленным доступом.</span><span class="sxs-lookup"><span data-stu-id="0b9af-123">hello remainder of hello tutorial shows you how tooenable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="0b9af-124">В данном руководстве мы создадим новый самозаверяющий сертификат, PFX-файл которого будет иметь выбранный вами пароль.</span><span class="sxs-lookup"><span data-stu-id="0b9af-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="0b9af-125">Также имеется возможность использовать сертификат, выданный центром сертификации hello.</span><span class="sxs-lookup"><span data-stu-id="0b9af-125">You also have hello option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a><span data-ttu-id="0b9af-126">Как tooenable удаленного доступа после вы развернули tooAzure</span><span class="sxs-lookup"><span data-stu-id="0b9af-126">How tooenable Remote Access after you have deployed tooAzure</span></span>
<span data-ttu-id="0b9af-127">tooenable удаленного доступа после развертывания tooAzure hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="0b9af-127">tooenable remote access after you have deployed tooAzure, use hello following steps:</span></span>

1. <span data-ttu-id="0b9af-128">Войдите на портал управления Azure hello, с помощью учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="0b9af-128">Log into hello Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="0b9af-129">В списке **Облачные службы**выберите развернутую облачную службу.</span><span class="sxs-lookup"><span data-stu-id="0b9af-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="0b9af-130">Hello облака службы веб-странице щелкните hello **Настройка** ссылку</span><span class="sxs-lookup"><span data-stu-id="0b9af-130">In hello cloud service web page, click hello **Configure** link</span></span>

4. <span data-ttu-id="0b9af-131">Щелкните hello hello нижней части страницы конфигурации hello **удаленного** ссылку</span><span class="sxs-lookup"><span data-stu-id="0b9af-131">On hello bottom of hello configuration page, click hello **Remote** link</span></span>

5. <span data-ttu-id="0b9af-132">Когда появится всплывающее диалоговое окно «hello»:</span><span class="sxs-lookup"><span data-stu-id="0b9af-132">When hello pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="0b9af-133">Укажите hello роли вы, для которого требуется tooenable удаленного доступа</span><span class="sxs-lookup"><span data-stu-id="0b9af-133">Specify hello Role you for which you want tooenable remote access</span></span>

   * <span data-ttu-id="0b9af-134">Нажмите кнопку tooselect hello **включить удаленный рабочий стол** флажок</span><span class="sxs-lookup"><span data-stu-id="0b9af-134">Click tooselect hello **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="0b9af-135">Укажите имя пользователя и пароль для удаленного доступа требуется toouse</span><span class="sxs-lookup"><span data-stu-id="0b9af-135">Specify a user name and password you want toouse for remote access</span></span>
   
   * <span data-ttu-id="0b9af-136">Выберите сертификат toouse hello</span><span class="sxs-lookup"><span data-stu-id="0b9af-136">Select hello certificate toouse</span></span>

6. <span data-ttu-id="0b9af-137">Щелкните **ОК**</span><span class="sxs-lookup"><span data-stu-id="0b9af-137">Click **OK**</span></span> 

<span data-ttu-id="0b9af-138">Появится сообщение о том, что изменения конфигурации находится в состоянии выполнения, что может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0b9af-138">You will see a message stating that your configuration change is in progress, which may take a few minutes toocomplete.</span></span> <span data-ttu-id="0b9af-139">После завершения изменения конфигурации hello, выполните действия hello в hello **toolog в удаленном режиме** далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="0b9af-139">After hello configuration change has completed, follow hello steps in hello **toolog in remotely** section later in this article.</span></span>

## <a name="how-tooenable-remote-access-in-your-package"></a><span data-ttu-id="0b9af-140">Как tooenable удаленного доступа в пакете</span><span class="sxs-lookup"><span data-stu-id="0b9af-140">How tooenable Remote Access in your package</span></span>
1. <span data-ttu-id="0b9af-141">В области обозревателя проектов Eclipse щелкните правой кнопкой мыши свой проект Azure и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="0b9af-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="0b9af-142">В hello **свойства** диалогового окна разверните **Azure** hello левой панели и нажмите **удаленного доступа**.</span><span class="sxs-lookup"><span data-stu-id="0b9af-142">In hello **Properties** dialog, expand **Azure** in hello left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="0b9af-143">В hello **удаленного доступа** диалогового окна Убедитесь **включить все роли tooaccept дистанционного управления рабочим столом с этими учетными данными входа** проверяется.</span><span class="sxs-lookup"><span data-stu-id="0b9af-143">In hello **Remote Access** dialog, ensure **Enable all roles tooaccept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="0b9af-144">Укажите имя пользователя для подключения удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="0b9af-144">Specify a user name for hello Remote Desktop connection.</span></span>

5. <span data-ttu-id="0b9af-145">Укажите и подтвердите пароль hello hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="0b9af-145">Specify and confirm hello password for hello user.</span></span> <span data-ttu-id="0b9af-146">Hello пользователя имя и пароль, заданные в этом диалоговом окне будет использоваться при установке подключения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="0b9af-146">hello user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="0b9af-147">(Обратите внимание, что этот пароль отличается от пароля PFX.)</span><span class="sxs-lookup"><span data-stu-id="0b9af-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="0b9af-148">Укажите срок действия учетной записи пользователя hello hello.</span><span class="sxs-lookup"><span data-stu-id="0b9af-148">Specify hello expiration date for hello user account.</span></span>

7. <span data-ttu-id="0b9af-149">Нажмите кнопку **New** toocreate новый самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="0b9af-149">Click **New** toocreate a new self-signed certificate.</span></span> <span data-ttu-id="0b9af-150">(Кроме того, можно выбрать сертификат из рабочей области или файловой системы, используя hello **рабочей** или **FileSystem** кнопок, соответственно, но для целей этого учебника мы создадим новый сертификат).</span><span class="sxs-lookup"><span data-stu-id="0b9af-150">(Alternatively, you could select a certificate from your workspace or file system through hello **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="0b9af-151">В hello **новый сертификат** диалогового окна, укажите и подтвердите пароль hello, которое будет использоваться для PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="0b9af-151">In hello **New Certificate** dialog, specify and confirm hello password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="0b9af-152">Примите значение hello для **имя (CN)**, или используйте имя файла.</span><span class="sxs-lookup"><span data-stu-id="0b9af-152">Accept hello value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="0b9af-153">Укажите hello путь и имя файла для сохранения нового сертификата hello в виде CER-файл.</span><span class="sxs-lookup"><span data-stu-id="0b9af-153">Specify hello path and file name where hello new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="0b9af-154">Для этого шага и hello следующий шаг можно использовать hello **cert** папки проекта Azure, но вы являетесь toochoose бесплатной другое расположение.</span><span class="sxs-lookup"><span data-stu-id="0b9af-154">For this step and hello next step, you could use hello **cert** folder of your Azure project, but you're free toochoose another location.</span></span> <span data-ttu-id="0b9af-155">В рамках данного руководства мы будем использовать **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="0b9af-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="0b9af-156">(Создать hello **c:\mycert** tooproceeding предыдущего папки или используйте существующую папку при желании.)</span><span class="sxs-lookup"><span data-stu-id="0b9af-156">(Create hello **c:\mycert** folder prior tooproceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="0b9af-157">Укажите hello путь и имя файла сохранения hello новый сертификат и его закрытый ключ в виде PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="0b9af-157">Specify hello path and file name where hello new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="0b9af-158">В рамках этого руководства мы будем использовать **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="0b9af-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="0b9af-159">Ваш **новый сертификат** диалоговое окно должно выглядеть примерно следующее toohello (обновление hello пути к папкам, если вы не использовали **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="0b9af-159">Your **New Certificate** dialog should look similar toohello following (update hello folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="0b9af-160">Нажмите кнопку **ОК** tooclose hello **новый сертификат** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0b9af-160">Click **OK** tooclose hello **New Certificate** dialog.</span></span>

8. <span data-ttu-id="0b9af-161">Ваш **удаленного доступа** диалоговое окно должно выглядеть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="0b9af-161">Your **Remote Access** dialog should look similar toohello following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="0b9af-162">Нажмите кнопку **ОК** tooclose hello **удаленного доступа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0b9af-162">Click **OK** tooclose hello **Remote Access** dialog.</span></span>

<span data-ttu-id="0b9af-163">Перестройте приложение, с помощью hello создать набор для развертывания toocloud.</span><span class="sxs-lookup"><span data-stu-id="0b9af-163">Rebuild your application, with hello build set for deployment toocloud.</span></span>

## <a name="toolog-in-remotely"></a><span data-ttu-id="0b9af-164">toolog в удаленном режиме</span><span class="sxs-lookup"><span data-stu-id="0b9af-164">toolog in remotely</span></span>
<span data-ttu-id="0b9af-165">После подготовки экземпляра роли можно удаленно войти toohello виртуальной машины, на котором размещается приложение.</span><span class="sxs-lookup"><span data-stu-id="0b9af-165">Once your role instance is ready, you can remotely log in toohello virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="0b9af-166">Если вы используете Eclipse в Windows и выбранного hello **запуск удаленного рабочего стола на развертывание** параметр во время вашей tooAzure развертывания вы откроется экран входа в систему удаленного рабочего стола при запуске развертывания.</span><span class="sxs-lookup"><span data-stu-id="0b9af-166">If are using Eclipse on Windows and you selected hello **Start remote desktop on deploy** option during your deployment tooAzure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="0b9af-167">При появлении запроса hello имени пользователя и пароля введите hello значения, заданные для удаленного пользователя hello и будет может toolog в.</span><span class="sxs-lookup"><span data-stu-id="0b9af-167">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

* <span data-ttu-id="0b9af-168">Другой способ toolog в — удаленно с помощью hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">портала управления Azure</a>:</span><span class="sxs-lookup"><span data-stu-id="0b9af-168">Another way toolog in remotely is through hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="0b9af-169">В рамках hello **облачные службы** представление hello портал управления Azure щелкните свою облачную службу, нажмите кнопку **экземпляров**, выберите конкретный экземпляр и нажмите кнопку hello **Connect**кнопки.</span><span class="sxs-lookup"><span data-stu-id="0b9af-169">Within hello **Cloud Services** view of hello Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click hello **Connect** button.</span></span> <span data-ttu-id="0b9af-170">Hello **Connect** кнопка отображается в виде hello следующее в командной строке hello:</span><span class="sxs-lookup"><span data-stu-id="0b9af-170">hello **Connect** button appears as hello following in hello command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="0b9af-171">После нажатия кнопки hello **Connect** кнопку, появится запрос tooopen RDP-файл.</span><span class="sxs-lookup"><span data-stu-id="0b9af-171">After clicking hello **Connect** button, you will be prompted tooopen an RDP file.</span></span> <span data-ttu-id="0b9af-172">Откройте файл hello и следуйте появляющимся на hello.</span><span class="sxs-lookup"><span data-stu-id="0b9af-172">Open hello file and follow hello prompts.</span></span> <span data-ttu-id="0b9af-173">(Можно также сохранить этот файл tooyour локального компьютера и затем запустите файл hello, дважды щелкнув его журнала tooremote в tooyour виртуальной машины без необходимости toofirst go hello портала управления.)</span><span class="sxs-lookup"><span data-stu-id="0b9af-173">(You could also save this file tooyour local computer, and then run hello file by double-clicking it tooremote log in tooyour virtual machine without needing toofirst go hello management portal.)</span></span>

  * <span data-ttu-id="0b9af-174">При появлении запроса hello имени пользователя и пароля введите hello значения, заданные для удаленного пользователя hello и будет может toolog в.</span><span class="sxs-lookup"><span data-stu-id="0b9af-174">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

> [!NOTE]
> <span data-ttu-id="0b9af-175">Если в операционной системе не на базе Windows требуется toouse клиент удаленного рабочего стола, совместимый с операционной системой и выполните шаги tooconfigure hello клиента с помощью параметров hello в hello RDP-файл, загруженный.</span><span class="sxs-lookup"><span data-stu-id="0b9af-175">If you are on a non-Windows operating system, you need toouse a Remote Desktop client that is compatible with your operating system and follow hello steps tooconfigure that client with hello settings in hello RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="0b9af-176">См. также</span><span class="sxs-lookup"><span data-stu-id="0b9af-176">See Also</span></span>
<span data-ttu-id="0b9af-177">[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0b9af-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="0b9af-178">[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0b9af-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="0b9af-179">[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0b9af-179">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="0b9af-180">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="0b9af-180">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
