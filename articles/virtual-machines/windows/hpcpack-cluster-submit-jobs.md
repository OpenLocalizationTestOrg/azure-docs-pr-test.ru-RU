---
title: "кластер tooan aaaSubmit заданий HPC Pack в Azure | Документы Microsoft"
description: "Узнайте, как tooset копию на локальном компьютере toosubmit заданий tooan кластера HPC Pack в Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="cfe49-103">Отправка заданий HPC из кластера HPC Pack tooan компьютера в локальной среде, развернутой в Azure</span><span class="sxs-lookup"><span data-stu-id="cfe49-103">Submit HPC jobs from an on-premises computer tooan HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="cfe49-104">Настройка задания локального компьютера клиента toosubmit tooa [пакета Microsoft HPC](https://technet.microsoft.com/library/cc514029) кластера в Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe49-104">Configure an on-premises client computer toosubmit jobs tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="cfe49-105">В этой статье показано, как tooset настроить локальный компьютер с клиентом средств toosubmit задания через HTTPS toohello кластера в Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe49-105">This article shows you how tooset up a local computer with client tools toosubmit job over HTTPS toohello cluster in Azure.</span></span> <span data-ttu-id="cfe49-106">Таким образом, несколько пользователей кластера можно отправить задания tooa облачного пакета HPC кластера, но без непосредственное подключение к ВМ головного узла toohello или доступ к подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe49-106">In this way, several cluster users can submit jobs tooa cloud-based HPC Pack cluster, but without connecting directly toohello head node VM or accessing an Azure subscription.</span></span>

![Отправить задание tooa кластера в Azure][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="cfe49-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cfe49-108">Prerequisites</span></span>
* <span data-ttu-id="cfe49-109">**Головной узел пакета HPC, развернутых в Виртуальной машине Azure** -мы рекомендуем использовать такие как автоматические средства [шаблона Azure краткое руководство](https://azure.microsoft.com/documentation/templates/) или [скрипт Azure PowerShell](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello головного узла и кластер.</span><span class="sxs-lookup"><span data-stu-id="cfe49-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello head node and cluster.</span></span> <span data-ttu-id="cfe49-110">Требуется DNS-имя головного узла hello hello и hello учетные данные администратора кластера для выполнения шагов hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cfe49-110">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>
* <span data-ttu-id="cfe49-111">**Клиентский компьютер**. Требуется клиентский компьютер под управлением Windows или Windows Server, который поддерживает запуск клиентских служебных программ для пакета HPC (ознакомьтесь с [требованиями к системе](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="cfe49-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="cfe49-112">Если требуется только toouse hello HPC Pack веб-портала или API-интерфейса REST toosubmit задания, можно использовать любой клиентский компьютер по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="cfe49-112">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="cfe49-113">**Установочный носитель пакета HPC** -tooinstall hello клиентских служебных программ пакета HPC, hello бесплатный установочный пакет для последней версии пакета HPC (HPC Pack 2012 R2) доступен в [центра загрузки Майкрософт](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="cfe49-113">**HPC Pack installation media** - tooinstall hello HPC Pack client utilities, hello free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="cfe49-114">Убедитесь, что при загрузке hello же версии пакета HPC, установленной на ВМ головного узла hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-114">Make sure that you download hello same version of HPC Pack that is installed on hello head node VM.</span></span>

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a><span data-ttu-id="cfe49-115">Шаг 1: Установка и настройка hello веб-компонентов на головном узле hello</span><span class="sxs-lookup"><span data-stu-id="cfe49-115">Step 1: Install and configure hello web components on hello head node</span></span>
<span data-ttu-id="cfe49-116">tooenable toohello заданий REST интерфейс toosubmit кластера по протоколу HTTPS, убедитесь, что веб-компонентов пакета HPC hello, настроены на головной узел пакета HPC hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-116">tooenable a REST interface toosubmit jobs toohello cluster over HTTPS, ensure that hello HPC Pack web components are configured on hello HPC Pack head node.</span></span> <span data-ttu-id="cfe49-117">Если они не установлены, сначала установите hello веб-компоненты, запустив файл установки HpcWebComponents.msi hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-117">If they aren't already installed, first install hello web components by running hello HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="cfe49-118">Затем настройте компоненты hello, запустив скрипт HPC PowerShell hello **Set-HPCWebComponents.ps1**.</span><span class="sxs-lookup"><span data-stu-id="cfe49-118">Then, configure hello components by running hello HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="cfe49-119">Подробные инструкции см. в разделе [установить веб-компоненты hello Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfe49-119">For detailed procedures, see [Install hello Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="cfe49-120">Некоторые шаблоны Azure краткое руководство для пакета HPC установки и автоматической настройки веб-компоненты hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-120">Certain Azure quickstart templates for HPC Pack install and configure hello web components automatically.</span></span> <span data-ttu-id="cfe49-121">Если вы используете hello [скрипт развертывания IaaS пакета HPC](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello кластера, при необходимости можно установить и настроить hello веб-компоненты как часть развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-121">If you use hello [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello cluster, you can optionally install and configure hello web components as part of hello deployment.</span></span>
> 
> 

<span data-ttu-id="cfe49-122">**веб-компоненты tooinstall hello**</span><span class="sxs-lookup"><span data-stu-id="cfe49-122">**tooinstall hello web components**</span></span>

1. <span data-ttu-id="cfe49-123">Подключение toohello ВМ головного узла с помощью hello учетные данные администратора кластера.</span><span class="sxs-lookup"><span data-stu-id="cfe49-123">Connect toohello head node VM by using hello credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="cfe49-124">Из папки установки пакета HPC hello запустите файл HpcWebComponents.msi на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-124">From hello HPC Pack Setup folder, run HpcWebComponents.msi on hello head node.</span></span>
3. <span data-ttu-id="cfe49-125">Выполните действия hello приветствия мастера tooinstall hello веб-компонентов</span><span class="sxs-lookup"><span data-stu-id="cfe49-125">Follow hello steps in hello wizard tooinstall hello web components</span></span>

<span data-ttu-id="cfe49-126">**веб-компоненты tooconfigure hello**</span><span class="sxs-lookup"><span data-stu-id="cfe49-126">**tooconfigure hello web components**</span></span>

1. <span data-ttu-id="cfe49-127">На головном узле hello запустите HPC PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="cfe49-127">On hello head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="cfe49-128">toochange toohello каталоге сценария настройки hello, тип hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cfe49-128">toochange directory toohello location of hello configuration script, type hello following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="cfe49-129">tooconfigure hello интерфейс REST и запуска hello веб-службы HPC типа hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cfe49-129">tooconfigure hello REST interface and start hello HPC Web Service, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="cfe49-130">Когда запрашиваемые tooselect сертификат, выберите сертификат hello, соответствующий открытому DNS-имени toohello hello головного узла.</span><span class="sxs-lookup"><span data-stu-id="cfe49-130">When prompted tooselect a certificate, choose hello certificate that corresponds toohello public DNS name of hello head node.</span></span> <span data-ttu-id="cfe49-131">Например, при развертывании головного узла hello виртуальную Машину с помощью hello классической модели развертывания, имя сертификата hello выглядит CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="cfe49-131">For example, if you deploy hello head node VM using hello classic deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="cfe49-132">При использовании модели развертывания диспетчера ресурсов hello, имя сертификата hello выглядит CN =&lt;*HeadNodeDnsName*&gt;.&lt; *область*&gt;. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="cfe49-132">If you use hello Resource Manager deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cfe49-133">Этот сертификат выбрать позднее при отправке задания toohello головного узла на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="cfe49-133">You select this certificate later when you submit jobs toohello head node from an on-premises computer.</span></span> <span data-ttu-id="cfe49-134">Не выбирайте и не настраивайте сертификат, который соответствует имени компьютера toohello hello головного узла в домене Active Directory hello (например, CN =*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="cfe49-134">Don't select or configure a certificate that corresponds toohello computer name of hello head node in hello Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="cfe49-135">tooconfigure hello веб-портал для отправки заданий, типа hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cfe49-135">tooconfigure hello web portal for job submission, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="cfe49-136">После завершения скрипта hello, остановите и перезапустите hello служба планировщика заданий HPC, введя hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="cfe49-136">After hello script completes, stop and restart hello HPC Job Scheduler Service by typing hello following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="cfe49-137">Шаг 2: Установка клиентских служебных программ пакета HPC hello на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="cfe49-137">Step 2: Install hello HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="cfe49-138">Если вы хотите tooinstall hello HPC Pack клиентские служебные программы на компьютере, загрузить файлы установки пакета HPC (полная установка) из hello [центра загрузки Майкрософт](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="cfe49-138">If you want tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="cfe49-139">При установке hello, выберите вариант установки hello для hello **клиентских служебных программ пакета HPC**.</span><span class="sxs-lookup"><span data-stu-id="cfe49-139">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="cfe49-140">toouse hello HPC Pack клиентские средства toosubmit заданий toohello ВМ головного узла, также требуется tooexport сертификат из головного узла hello и установить его на клиентском компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-140">toouse hello HPC Pack client tools toosubmit jobs toohello head node VM, you also need tooexport a certificate from hello head node and install it on hello client computer.</span></span> <span data-ttu-id="cfe49-141">Hello сертификат должен находиться в. Формат CER.</span><span class="sxs-lookup"><span data-stu-id="cfe49-141">hello certificate must be in .CER format.</span></span>

<span data-ttu-id="cfe49-142">**tooexport hello сертификат из головного узла hello**</span><span class="sxs-lookup"><span data-stu-id="cfe49-142">**tooexport hello certificate from hello head node**</span></span>

1. <span data-ttu-id="cfe49-143">На головном узле hello добавьте hello сертификатов оснастки tooa консоли управления для hello учетной записи локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="cfe49-143">On hello head node, add hello Certificates snap-in tooa Microsoft Management Console for hello Local Computer account.</span></span> <span data-ttu-id="cfe49-144">Оснастка tooadd hello, содержится [добавьте hello оснастку сертификатов tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfe49-144">For steps tooadd hello snap-in, see [Add hello Certificates Snap-in tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="cfe49-145">В дереве консоли hello, разверните **сертификаты — локальный компьютер** > **личных**, а затем нажмите кнопку **сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="cfe49-145">In hello console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="cfe49-146">Найдите hello сертификат, настроенный для hello HPC Pack веб-компонентов в [шаг 1: Установка и настройка hello веб-компонентов на головном узле hello](#step-1:-install-and-configure-the-web-components-on-the-head-node) (например, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="cfe49-146">Locate hello certificate that you configured for hello HPC Pack web components in [Step 1: Install and configure hello web components on hello head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="cfe49-147">Щелкните правой кнопкой мыши сертификат hello и нажмите кнопку **все задачи** > **Экспорт**.</span><span class="sxs-lookup"><span data-stu-id="cfe49-147">Right-click hello certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="cfe49-148">В окне приветствия мастера экспорта сертификатов нажмите кнопку **Далее**и убедитесь, что **нет, не экспортировать закрытый ключ hello** выбран.</span><span class="sxs-lookup"><span data-stu-id="cfe49-148">In hello Certificate Export Wizard, click **Next**, and ensure that **No, do not export hello private key** is selected.</span></span>
6. <span data-ttu-id="cfe49-149">Hello выполните оставшиеся действия мастера hello tooexport сертификата hello DER-кодировке X.509 (. Формат CER).</span><span class="sxs-lookup"><span data-stu-id="cfe49-149">Follow hello remaining steps of hello wizard tooexport hello certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="cfe49-150">**tooimport hello сертификатов на клиентском компьютере hello**</span><span class="sxs-lookup"><span data-stu-id="cfe49-150">**tooimport hello certificate on hello client computer**</span></span>

1. <span data-ttu-id="cfe49-151">Скопируйте экспортированный из папки tooa hello головного узла на клиентском компьютере hello hello сертификат.</span><span class="sxs-lookup"><span data-stu-id="cfe49-151">Copy hello certificate that you exported from hello head node tooa folder on hello client computer.</span></span>
2. <span data-ttu-id="cfe49-152">На клиентском компьютере hello запустите certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="cfe49-152">On hello client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="cfe49-153">В диспетчере сертификатов разверните **Сертификаты — текущий пользователь** > **Доверенные корневые центры сертификации**, щелкните правой кнопкой мыши **Сертификаты** и щелкните **Все задачи** > **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="cfe49-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="cfe49-154">В окне приветствия мастера импорта сертификатов нажмите кнопку **Далее** и выполните hello действия tooimport hello сертификат, экспортированный из головного узла toohello hello, хранилище доверенных корневых центров сертификации.</span><span class="sxs-lookup"><span data-stu-id="cfe49-154">In hello Certificate Import Wizard, click **Next** and follow hello steps tooimport hello certificate that you exported from hello head node toohello Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="cfe49-155">Может появиться предупреждение о безопасности, поскольку hello центр сертификации на головном узле hello не распознаются hello клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="cfe49-155">You might see a security warning, because hello certification authority on hello head node isn't recognized by hello client computer.</span></span> <span data-ttu-id="cfe49-156">В целях тестирования можно игнорировать это предупреждения и завершения импорта сертификатов hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-156">For testing purposes, you can ignore this warning and complete hello certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a><span data-ttu-id="cfe49-157">Шаг 3: Запуск тестовые задания в кластере hello</span><span class="sxs-lookup"><span data-stu-id="cfe49-157">Step 3: Run test jobs on hello cluster</span></span>
<span data-ttu-id="cfe49-158">tooverify конфигурацию, повторите выполнение задания на hello кластера в Azure из hello локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="cfe49-158">tooverify your configuration, try running jobs on hello cluster in Azure from hello on-premises computer.</span></span> <span data-ttu-id="cfe49-159">Например можно использовать средства графического интерфейса пользователя HPC Pack или командной строки toosubmit заданий toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="cfe49-159">For example, you can use HPC Pack GUI tools or command-line commands toosubmit jobs toohello cluster.</span></span> <span data-ttu-id="cfe49-160">Также можно использовать веб-портала toosubmit заданий.</span><span class="sxs-lookup"><span data-stu-id="cfe49-160">You can also use a web-based portal toosubmit jobs.</span></span>

<span data-ttu-id="cfe49-161">**toorun команд отправки заданий на клиентском компьютере hello**</span><span class="sxs-lookup"><span data-stu-id="cfe49-161">**toorun job submission commands on hello client computer**</span></span>

1. <span data-ttu-id="cfe49-162">На клиентском компьютере, где установлены клиентских служебных программ пакета HPC hello откройте командную строку.</span><span class="sxs-lookup"><span data-stu-id="cfe49-162">On a client computer where hello HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="cfe49-163">Введите тестовую команду.</span><span class="sxs-lookup"><span data-stu-id="cfe49-163">Type a sample command.</span></span> <span data-ttu-id="cfe49-164">Например toolist все задания в кластере hello введите tooone аналогичные команды из hello следующие, в зависимости от hello полное DNS-имя головного узла hello:</span><span class="sxs-lookup"><span data-stu-id="cfe49-164">For example, toolist all jobs on hello cluster, type a command similar tooone of hello following, depending on hello full DNS name of hello head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="cfe49-165">или</span><span class="sxs-lookup"><span data-stu-id="cfe49-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="cfe49-166">Используйте hello полное DNS-имя головного узла hello, не hello IP-адрес, в URL-адрес планировщика hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-166">Use hello full DNS name of hello head node, not hello IP address, in hello scheduler URL.</span></span> <span data-ttu-id="cfe49-167">При указании hello IP-адрес, отображается сообщение об ошибке примерно слишком "сертификат сервера hello должен tooeither имеет цепочку доверия или помещен в хранилище доверенных корневых hello toobe.»</span><span class="sxs-lookup"><span data-stu-id="cfe49-167">If you specify hello IP address, an error appears similar too"hello server certificate needs tooeither have a valid chain of trust or toobe placed in hello trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="cfe49-168">При появлении запроса введите имя пользователя hello (в форме hello &lt;DomainName&gt;\\&lt;UserName&gt;) и пароль администратора кластера HPC hello или другого пользователя кластера, который вы настроили.</span><span class="sxs-lookup"><span data-stu-id="cfe49-168">When prompted, type hello user name (in hello form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="cfe49-169">Вы можете toostore hello учетные данные локально для других операций.</span><span class="sxs-lookup"><span data-stu-id="cfe49-169">You can choose toostore hello credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="cfe49-170">Появится список заданий.</span><span class="sxs-lookup"><span data-stu-id="cfe49-170">A list of jobs appears.</span></span>

<span data-ttu-id="cfe49-171">**toouse диспетчер заданий HPC на клиентском компьютере hello**</span><span class="sxs-lookup"><span data-stu-id="cfe49-171">**toouse HPC Job Manager on hello client computer**</span></span>

1. <span data-ttu-id="cfe49-172">Если при отправке задания не ранее хранить учетные данные домена для пользователя кластера, можно добавить учетные данные hello в диспетчере учетных данных.</span><span class="sxs-lookup"><span data-stu-id="cfe49-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add hello credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="cfe49-173">а.</span><span class="sxs-lookup"><span data-stu-id="cfe49-173">a.</span></span> <span data-ttu-id="cfe49-174">На панели управления на клиентском компьютере hello запустите диспетчер учетных данных.</span><span class="sxs-lookup"><span data-stu-id="cfe49-174">In Control Panel on hello client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="cfe49-175">b.</span><span class="sxs-lookup"><span data-stu-id="cfe49-175">b.</span></span> <span data-ttu-id="cfe49-176">Щелкните **Учетные данные Windows** > **Добавить общие учетные данные**.</span><span class="sxs-lookup"><span data-stu-id="cfe49-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="cfe49-177">c.</span><span class="sxs-lookup"><span data-stu-id="cfe49-177">c.</span></span> <span data-ttu-id="cfe49-178">Укажите адрес в Интернете hello (например, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler "или" https://&lt;HeadNodeDnsName&gt;.&lt; область&gt;.cloudapp.azure.com/HpcScheduler) и имя пользователя hello (&lt;DomainName&gt;\\&lt;UserName&gt;) и пароль администратора кластера hello или другой пользователь кластера, вы настроили.</span><span class="sxs-lookup"><span data-stu-id="cfe49-178">Specify hello Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and hello user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="cfe49-179">На клиентском компьютере hello запустите диспетчер заданий HPC.</span><span class="sxs-lookup"><span data-stu-id="cfe49-179">On hello client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="cfe49-180">В hello **Выбор головного узла** диалоговое окно, тип hello URL-адрес toohello головного узла в Azure (например, https://&lt;HeadNodeDnsName&gt;. cloudapp.net "или" https://&lt;HeadNodeDnsName&gt;. &lt;область&gt;. cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cfe49-180">In hello **Select Head Node** dialog box, type hello URL toohello head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="cfe49-181">Диспетчер заданий HPC открывается и отображается список заданий на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-181">HPC Job Manager opens and shows a list of jobs on hello head node.</span></span>

<span data-ttu-id="cfe49-182">**веб-портал toouse hello, работающих на головном узле hello**</span><span class="sxs-lookup"><span data-stu-id="cfe49-182">**toouse hello web portal running on hello head node**</span></span>

1. <span data-ttu-id="cfe49-183">Запуск веб-браузер на клиентском компьютере hello и введите одну из hello следующие адреса в зависимости от hello полное DNS-имя головного узла hello:</span><span class="sxs-lookup"><span data-stu-id="cfe49-183">Start a web browser on hello client computer, and enter one of hello following addresses, depending on hello full DNS name of hello head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="cfe49-184">или</span><span class="sxs-lookup"><span data-stu-id="cfe49-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="cfe49-185">В hello безопасности появившемся введите учетные данные администратора кластера HPC hello hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-185">In hello security dialog box that appears, type hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="cfe49-186">(Вы также можете добавить пользователей кластера в разных ролях.</span><span class="sxs-lookup"><span data-stu-id="cfe49-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="cfe49-187">Ознакомьтесь со статьей [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx)(Управление пользователями кластера.)</span><span class="sxs-lookup"><span data-stu-id="cfe49-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="cfe49-188">веб-портал Hello откроется представление списка заданий toohello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-188">hello web portal opens toohello job list view.</span></span>
3. <span data-ttu-id="cfe49-189">Щелкните toosubmit образец задания, возвращает строку hello «Hello World» из кластера hello **новое задание** hello левой навигационной панели.</span><span class="sxs-lookup"><span data-stu-id="cfe49-189">toosubmit a sample job that returns hello string “Hello World” from hello cluster, click **New job** in hello left-hand navigation.</span></span>
4. <span data-ttu-id="cfe49-190">На hello **новое задание** в разделе **со страниц отправки**, нажмите кнопку **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="cfe49-190">On hello **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="cfe49-191">Откроется страница отправки задания Hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-191">hello job submission page appears.</span></span>
5. <span data-ttu-id="cfe49-192">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="cfe49-192">Click **Submit**.</span></span> <span data-ttu-id="cfe49-193">При запросе введите учетные данные администратора кластера HPC hello hello.</span><span class="sxs-lookup"><span data-stu-id="cfe49-193">If prompted, provide hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="cfe49-194">отправке задания Hello и hello идентификатор задания появится на hello **Мои задания** страницы.</span><span class="sxs-lookup"><span data-stu-id="cfe49-194">hello job is submitted, and hello job ID appears on hello **My Jobs** page.</span></span>
6. <span data-ttu-id="cfe49-195">Щелкните идентификатор задания hello результаты hello tooview hello отправленного задания и нажмите кнопку **Просмотр задач** tooview выходные данные команды hello (в разделе **выходные данные**).</span><span class="sxs-lookup"><span data-stu-id="cfe49-195">tooview hello results of hello job that you submitted, click hello job ID, and then click **View Tasks** tooview hello command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfe49-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cfe49-196">Next steps</span></span>
* <span data-ttu-id="cfe49-197">Также можно отправлять задания toohello Azure кластер с hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfe49-197">You can also submit jobs toohello Azure cluster with hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="cfe49-198">Toosubmit кластерных заданий из клиента Linux, см hello Python в hello [HPC Pack 2012 R2 SDK и образцы кода](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="cfe49-198">If you want toosubmit cluster jobs from a Linux client, see hello Python sample in hello [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
