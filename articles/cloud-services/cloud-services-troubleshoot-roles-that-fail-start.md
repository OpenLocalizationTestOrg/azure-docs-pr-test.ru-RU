---
title: "aaaTroubleshoot ролей, которые не toostart | Документы Microsoft"
description: "Ниже приведены наиболее распространенные причины, почему роли облачной службы может завершиться ошибкой toostart. Также предоставляются toothese решения проблемы."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a><span data-ttu-id="5cd30-104">Устранение неполадок ролей облачной службы, которые не toostart</span><span class="sxs-lookup"><span data-stu-id="5cd30-104">Troubleshoot Cloud Service roles that fail toostart</span></span>
<span data-ttu-id="5cd30-105">Ниже приведены некоторые распространенные проблемы и решения связанных tooAzure облачные службы ролей, которые не toostart.</span><span class="sxs-lookup"><span data-stu-id="5cd30-105">Here are some common problems and solutions related tooAzure Cloud Services roles that fail toostart.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="5cd30-106">Отсутствующие DLL-библиотеки и зависимости</span><span class="sxs-lookup"><span data-stu-id="5cd30-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="5cd30-107">Если роли не отвечают или циклически переключаются между состояниями **Инициализация**, **Занято** и **Остановка**, это может быть вызвано отсутствием сборок или библиотек DLL.</span><span class="sxs-lookup"><span data-stu-id="5cd30-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="5cd30-108">Симптомы отсутствия сборок и библиотек DLL могут быть такими:</span><span class="sxs-lookup"><span data-stu-id="5cd30-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="5cd30-109">Экземпляр роли циклически переключается между состояниями **Инициализация**, **Занято** и **Остановка**.</span><span class="sxs-lookup"><span data-stu-id="5cd30-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="5cd30-110">Экземпляр роли перемещено слишком**готовности** , но при переходе tooyour веб-приложение hello страница не отображается.</span><span class="sxs-lookup"><span data-stu-id="5cd30-110">Your role instance has moved too**Ready** but if you navigate tooyour web application, hello page does not appear.</span></span>

<span data-ttu-id="5cd30-111">Эти проблемы можно решить несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="5cd30-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="5cd30-112">Диагностика неполадок в связи с отсутствующими библиотеками DLL в веб-роли</span><span class="sxs-lookup"><span data-stu-id="5cd30-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="5cd30-113">Когда перейдите tooa веб-сайт, который развертывается на веб-роли и hello браузер отображает сервера ошибка аналогичные toohello ниже, это может указывать, что библиотека DLL отсутствует.</span><span class="sxs-lookup"><span data-stu-id="5cd30-113">When you navigate tooa website that is deployed in a web role, and hello browser displays a server error similar toohello following, it may indicate that a DLL is missing.</span></span>

![Ошибка сервера в приложении «/».](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="5cd30-115">Диагностика проблем с помощью отключения режима настраиваемых ошибок</span><span class="sxs-lookup"><span data-stu-id="5cd30-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="5cd30-116">Более полные сведения об ошибке можно просмотреть, настроив файл web.config hello для hello tooset роли web hello tooOff режим пользовательских ошибок и повторного развертывания службы hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-116">More complete error information can be viewed by configuring hello web.config for hello web role tooset hello custom error mode tooOff and redeploying hello service.</span></span>

<span data-ttu-id="5cd30-117">tooview более выполните ошибки без использования удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="5cd30-117">tooview more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="5cd30-118">Откройте решение hello в Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5cd30-118">Open hello solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="5cd30-119">В hello **обозревателе решений**hello файл web.config и откройте его.</span><span class="sxs-lookup"><span data-stu-id="5cd30-119">In hello **Solution Explorer**, locate hello web.config file and open it.</span></span>
3. <span data-ttu-id="5cd30-120">В файле web.config hello найдите раздел system.web hello и добавьте hello, следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="5cd30-120">In hello web.config file, locate hello system.web section and add hello following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="5cd30-121">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-121">Save hello file.</span></span>
5. <span data-ttu-id="5cd30-122">Упакуйте и повторно разверните службу hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-122">Repackage and redeploy hello service.</span></span>

<span data-ttu-id="5cd30-123">После развертывания службы hello, вы увидите сообщение об ошибке с именем hello hello отсутствующих сборок или библиотек DLL.</span><span class="sxs-lookup"><span data-stu-id="5cd30-123">Once hello service is redeployed, you will see an error message with hello name of hello missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a><span data-ttu-id="5cd30-124">Диагностировать проблемы, просмотрев ошибки hello удаленно</span><span class="sxs-lookup"><span data-stu-id="5cd30-124">Diagnose issues by viewing hello error remotely</span></span>
<span data-ttu-id="5cd30-125">Можно использовать удаленный рабочий стол tooaccess hello роли и удаленно просматривать более полные сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5cd30-125">You can use Remote Desktop tooaccess hello role and view more complete error information remotely.</span></span> <span data-ttu-id="5cd30-126">Используйте следующие шаги tooview hello ошибки с помощью удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-126">Use hello following steps tooview hello errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="5cd30-127">Убедитесь, что установлен пакет SDK для Azure версии 1.3 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="5cd30-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="5cd30-128">Слишком во время развертывания hello hello решения с помощью Visual Studio, выберите «Настроить удаленный рабочий стол подключений...».</span><span class="sxs-lookup"><span data-stu-id="5cd30-128">During hello deployment of hello solution by using Visual Studio, choose too“Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="5cd30-129">Дополнительные сведения о настройке подключения удаленного рабочего стола hello см. в разделе [использование удаленного рабочего стола с ролями Azure](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5cd30-129">For more information on configuring hello Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="5cd30-130">Hello Microsoft Azure классическом портале, как только состояние экземпляра hello **готовности**, выберите один из экземпляров роли hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-130">In hello Microsoft Azure classic portal, once hello instance shows a status of **Ready**, click one of hello role instances.</span></span>
4. <span data-ttu-id="5cd30-131">Нажмите кнопку hello **Connect** значок в hello **удаленного доступа** ленте hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-131">Click hello **Connect** icon in hello **Remote Access** area of hello ribbon.</span></span>
5. <span data-ttu-id="5cd30-132">Войдите в toohello виртуальной машины с помощью hello учетные данные, которые были указаны во время настройки удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-132">Sign in toohello virtual machine by using hello credentials that were specified during hello Remote Desktop configuration.</span></span>
6. <span data-ttu-id="5cd30-133">Откройте командное окно.</span><span class="sxs-lookup"><span data-stu-id="5cd30-133">Open a command window.</span></span>
7. <span data-ttu-id="5cd30-134">Введите `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="5cd30-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="5cd30-135">Запомните значение IPV4-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-135">Note hello IPV4 Address value.</span></span>
9. <span data-ttu-id="5cd30-136">Откройте браузер Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="5cd30-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="5cd30-137">Введите адрес hello и имя hello hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5cd30-137">Type hello address and hello name of hello web application.</span></span> <span data-ttu-id="5cd30-138">Например, `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="5cd30-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="5cd30-139">Навигация по toohello веб-сайта теперь возвращают более подробные сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5cd30-139">Navigating toohello website will now return more explicit error messages:</span></span>

* <span data-ttu-id="5cd30-140">Ошибка сервера в приложении «/».</span><span class="sxs-lookup"><span data-stu-id="5cd30-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="5cd30-141">Описание: Необработанное исключение произошло во время выполнения hello hello текущего веб-запроса.</span><span class="sxs-lookup"><span data-stu-id="5cd30-141">Description: An unhandled exception occurred during hello execution of hello current web request.</span></span> <span data-ttu-id="5cd30-142">Просмотрите трассировку стека hello Дополнительные сведения об ошибке hello и где он находится в коде hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-142">Please review hello stack trace for more information about hello error and where it originated in hello code.</span></span>
* <span data-ttu-id="5cd30-143">Сведения об исключении: System.IO.FIleNotFoundException: не удалось загрузить файл, сборку Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35 или какую-то их зависимость.</span><span class="sxs-lookup"><span data-stu-id="5cd30-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="5cd30-144">Hello системе не удается найти указанный файл hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-144">hello system cannot find hello file specified.</span></span>

<span data-ttu-id="5cd30-145">Например:</span><span class="sxs-lookup"><span data-stu-id="5cd30-145">For example:</span></span>

![Явная ошибка сервера в приложении «/».](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a><span data-ttu-id="5cd30-147">Диагностика проблем с помощью эмулятора вычислений hello</span><span class="sxs-lookup"><span data-stu-id="5cd30-147">Diagnose issues by using hello compute emulator</span></span>
<span data-ttu-id="5cd30-148">Можно использовать toodiagnose эмулятор вычислений Microsoft Azure hello и устранения проблем с отсутствующими зависимостями и ошибок в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="5cd30-148">You can use hello Microsoft Azure compute emulator toodiagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="5cd30-149">Чтобы улучшить результаты использования этого метода диагностики, следует использовать компьютер или виртуальную машину, на которой выполнена чистая установка Windows.</span><span class="sxs-lookup"><span data-stu-id="5cd30-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="5cd30-150">toobest имитировать hello среды Azure, используйте Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="5cd30-150">toobest simulate hello Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="5cd30-151">Установите автономную версию hello hello [пакета Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5cd30-151">Install hello standalone version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="5cd30-152">На компьютере для разработки hello построение проекта облачной службы hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-152">On hello development machine, build hello cloud service project.</span></span>
3. <span data-ttu-id="5cd30-153">В проводнике Windows перейдите toohello папку bin\debug проекта облачной службы hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-153">In Windows Explorer, navigate toohello bin\debug folder of hello cloud service project.</span></span>
4. <span data-ttu-id="5cd30-154">Скопируйте папку .csx hello и .cscfg файл toohello компьютер, что вы используете toodebug hello проблемы.</span><span class="sxs-lookup"><span data-stu-id="5cd30-154">Copy hello .csx folder and .cscfg file toohello computer that you are using toodebug hello issues.</span></span>
5. <span data-ttu-id="5cd30-155">На hello очистки компьютера, откройте окно командной строки Azure SDK и введите `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="5cd30-155">On hello clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="5cd30-156">Введите в командной строке hello `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="5cd30-156">At hello command prompt, type `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="5cd30-157">При запуске роли hello, вы увидите подробные сведения об ошибке в Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="5cd30-157">When hello role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="5cd30-158">Можно также использовать стандартные средства устранения неполадок Windows toofurther диагностировать проблему hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-158">You can also use standard Windows troubleshooting tools toofurther diagnose hello problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="5cd30-159">Диагностика неполадок с помощью IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="5cd30-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="5cd30-160">Для рабочих ролей и веб-ролей, которые используют платформу .NET Framework 4, можно использовать функцию [EnterpriseIntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), доступную в Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5cd30-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="5cd30-161">Выполните эти шаги toodeploy hello службы с включенным компонентом IntelliTrace.</span><span class="sxs-lookup"><span data-stu-id="5cd30-161">Follow these steps toodeploy hello service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="5cd30-162">Убедитесь, что установлен пакет SDK для Azure версии 1.3 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="5cd30-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="5cd30-163">Развертывание решения hello с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5cd30-163">Deploy hello solution by using Visual Studio.</span></span> <span data-ttu-id="5cd30-164">Во время развертывания, проверьте hello **включить IntelliTrace для ролей .NET 4** флажок.</span><span class="sxs-lookup"><span data-stu-id="5cd30-164">During deployment, check hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="5cd30-165">После запуска экземпляра hello, откройте hello **обозревателя серверов**.</span><span class="sxs-lookup"><span data-stu-id="5cd30-165">Once hello instance starts, open hello **Server Explorer**.</span></span>
4. <span data-ttu-id="5cd30-166">Разверните hello **Azure\\облачные службы** узла и найдите развертывание hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-166">Expand hello **Azure\\Cloud Services** node and locate hello deployment.</span></span>
5. <span data-ttu-id="5cd30-167">Расширяйте развертывание hello, пока не увидите hello экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="5cd30-167">Expand hello deployment until you see hello role instances.</span></span> <span data-ttu-id="5cd30-168">Щелкните правой кнопкой мыши один из экземпляров hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-168">Right-click on one of hello instances.</span></span>
6. <span data-ttu-id="5cd30-169">Выберите элемент **Просмотр журналов IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="5cd30-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="5cd30-170">Hello **Сводка IntelliTrace** будет открыт.</span><span class="sxs-lookup"><span data-stu-id="5cd30-170">hello **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="5cd30-171">Найдите раздел исключений hello hello сводки.</span><span class="sxs-lookup"><span data-stu-id="5cd30-171">Locate hello exceptions section of hello summary.</span></span> <span data-ttu-id="5cd30-172">Если существуют исключения, будет называться hello раздел **данные исключения**.</span><span class="sxs-lookup"><span data-stu-id="5cd30-172">If there are exceptions, hello section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="5cd30-173">Разверните hello **данные исключения** и выполните поиск **System.IO.FileNotFoundException** аналогичные toohello следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="5cd30-173">Expand hello **Exception Data** and look for **System.IO.FileNotFoundException** errors similar toohello following:</span></span>

![Данные исключения, отсутствующий файл или сборка](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="5cd30-175">Устранение ошибок из-за отсутствующих библиотек DLL и сборок</span><span class="sxs-lookup"><span data-stu-id="5cd30-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="5cd30-176">tooaddress отсутствует DLL и сборок ошибки, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5cd30-176">tooaddress missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="5cd30-177">Откройте решение hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5cd30-177">Open hello solution in Visual Studio.</span></span>
2. <span data-ttu-id="5cd30-178">В **обозревателе решений**откройте hello **ссылки** папки.</span><span class="sxs-lookup"><span data-stu-id="5cd30-178">In **Solution Explorer**, open hello **References** folder.</span></span>
3. <span data-ttu-id="5cd30-179">Щелкните сборку hello, указанную в ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="5cd30-179">Click hello assembly identified in hello error.</span></span>
4. <span data-ttu-id="5cd30-180">В hello **свойства** панели найдите **свойства Copy Local** и задайте значение hello слишком**True**.</span><span class="sxs-lookup"><span data-stu-id="5cd30-180">In hello **Properties** pane, locate **Copy Local property** and set hello value too**True**.</span></span>
5. <span data-ttu-id="5cd30-181">Повторное развертывание hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5cd30-181">Redeploy hello cloud service.</span></span>

<span data-ttu-id="5cd30-182">После проверки того, что все ошибки исправлены, вы можете развернуть службу hello без проверки hello **включить IntelliTrace для ролей .NET 4** флажок.</span><span class="sxs-lookup"><span data-stu-id="5cd30-182">Once you have verified that all errors have been corrected, you can deploy hello service without checking hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cd30-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5cd30-183">Next steps</span></span>
<span data-ttu-id="5cd30-184">Просмотрите дополнительные [статьи об устранении неполадок](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) в облачных службах.</span><span class="sxs-lookup"><span data-stu-id="5cd30-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="5cd30-185">toolearn как проблемы tootroubleshoot роль облачной службы с помощью диагностические данные Azure PaaS компьютера, в разделе [серии публикаций в блоге Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="5cd30-185">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
