---
title: "Создание - Azure кластера библиотек Hive aaaAdd во время HDInsight | Документы Microsoft"
description: "Узнайте, как tooadd библиотек Hive (jar-файлы), tooan HDInsight кластера во время создания кластера."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="aaf7d-103">Добавление пользовательских библиотек Hive при создании кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="aaf7d-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="aaf7d-104">Если у вас есть библиотек, которые часто используются с Hive в HDInsight, этот документ содержит сведения об использовании библиотеки hello действие сценария toopre нагрузки во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action toopre-load hello libraries during cluster creation.</span></span> <span data-ttu-id="aaf7d-105">Библиотеки, добавленные с помощью hello шаги в этом документе глобально доступны в кусте - у без необходимости toouse [Добавьте JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload их.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-105">Libraries added using hello steps in this document are globally available in Hive - there is no need toouse [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="aaf7d-106">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="aaf7d-106">How it works</span></span>

<span data-ttu-id="aaf7d-107">При создании кластера, можно также задать действие скрипта, который запускает сценарий на узлах кластера hello при их создании.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-107">When creating a cluster, you can optionally specify a Script Action that runs a script on hello cluster nodes while they are being created.</span></span> <span data-ttu-id="aaf7d-108">сценарий Hello в этом документе принимает один параметр, являющийся WASB расположение, которое содержит предварительно загружать toobe библиотеки (хранятся в виде файлов jar) hello.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-108">hello script in this document accepts a single parameter, which is a WASB location that contains hello libraries (stored as jar files) toobe pre-loaded.</span></span>

<span data-ttu-id="aaf7d-109">Во время создания кластера hello скрипт Перечисляет файлы hello, копирует их toohello `/usr/lib/customhivelibs/` каталог на головном и рабочих узлов, после чего они добавляются toohello `hive.aux.jars.path` свойство в hello `core-site.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-109">During cluster creation, hello script enumerates hello files, copies them toohello `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them toohello `hive.aux.jars.path` property in hello `core-site.xml` file.</span></span> <span data-ttu-id="aaf7d-110">Для кластеров под управлением Linux, он обновляет hello `hive-env.sh` файл с hello расположение файлов hello.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-110">On Linux-based clusters, it also updates hello `hive-env.sh` file with hello location of hello files.</span></span>

> [!NOTE]
> <span data-ttu-id="aaf7d-111">С помощью действий скрипта hello в этой статье обеспечивает библиотеки hello в hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="aaf7d-111">Using hello script actions in this article makes hello libraries available in hello following scenarios:</span></span>
>
> * <span data-ttu-id="aaf7d-112">**HDInsight под управлением Linux** — Если с помощью hello клиентом куст **WebHCat**, и **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-112">**Linux-based HDInsight** - when using hello a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="aaf7d-113">**HDInsight под управлением Windows** — при использовании клиента Hive hello и **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-113">**Windows-based HDInsight** - when using hello Hive client and **WebHCat**.</span></span>

## <a name="hello-script"></a><span data-ttu-id="aaf7d-114">сценарий Hello</span><span class="sxs-lookup"><span data-stu-id="aaf7d-114">hello script</span></span>

<span data-ttu-id="aaf7d-115">**Расположение скрипта**</span><span class="sxs-lookup"><span data-stu-id="aaf7d-115">**Script location**</span></span>

<span data-ttu-id="aaf7d-116">Для **кластеров под управлением Linux** — [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="aaf7d-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="aaf7d-117">Для **кластеров под управлением Windows** — [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="aaf7d-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aaf7d-118">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aaf7d-119">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="aaf7d-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="aaf7d-120">**Требования**</span><span class="sxs-lookup"><span data-stu-id="aaf7d-120">**Requirements**</span></span>

* <span data-ttu-id="aaf7d-121">Hello сценарии должны быть hello примененных tooboth **Head узлы** и **рабочих узлов**.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-121">hello scripts must be applied tooboth hello **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="aaf7d-122">Здравствуйте, JAR-файлов необходимо tooinstall должны храниться в хранилище больших двоичных объектов Azure в **один контейнер**.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-122">hello jars you wish tooinstall must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="aaf7d-123">Учетная запись хранения Hello hello библиотеку jar-файла, содержащего **должен** быть кластера HDInsight связанные toohello во время создания.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-123">hello storage account containing hello library of jar files **must** be linked toohello HDInsight cluster during creation.</span></span> <span data-ttu-id="aaf7d-124">Оно должно быть учетной записи хранения по умолчанию hello, или учетной записи добавляются через __необязательная конфигурация__.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-124">It must either be hello default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="aaf7d-125">путь toohello Hello WASB контейнер должен быть указан как параметр toohello действие сценария.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-125">hello WASB path toohello container must be specified as a parameter toohello Script Action.</span></span> <span data-ttu-id="aaf7d-126">Например, если hello JAR-файлов хранятся в контейнере с именем **библиотеки** в учетной записи хранения с именем **mystorage**, нужно указать параметр hello  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="aaf7d-126">For example, if hello jars are stored in a container named **libs** on a storage account named **mystorage**, hello parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="aaf7d-127">Данный документ предполагает уже создания учетной записи хранилища, контейнер больших двоичных объектов и tooit hello загруженные файлы.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-127">This document assumes that you have already create a storage account, blob container, and uploaded hello files tooit.</span></span>
  >
  > <span data-ttu-id="aaf7d-128">Если вы не создали учетную запись хранения, это можно сделать через hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aaf7d-128">If you have not created a storage account, you can do so through hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="aaf7d-129">Затем можно использовать программу например [обозреватель хранилищ Azure](http://storageexplorer.com/) toocreate контейнера в учетной записи hello и передача файлов tooit.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate a container in hello account and upload files tooit.</span></span>

## <a name="create-a-cluster-using-hello-script"></a><span data-ttu-id="aaf7d-130">Создание кластера с помощью скрипта hello</span><span class="sxs-lookup"><span data-stu-id="aaf7d-130">Create a cluster using hello script</span></span>

> [!NOTE]
> <span data-ttu-id="aaf7d-131">следующие шаги Hello создать кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-131">hello following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="aaf7d-132">Выберите toocreate кластера под управлением Windows, **Windows** как hello кластера ОС при создании кластера hello и используйте вместо hello bash script script приветствия Windows (PowerShell).</span><span class="sxs-lookup"><span data-stu-id="aaf7d-132">toocreate a Windows-based cluster, select **Windows** as hello cluster OS when creating hello cluster, and use hello Windows (PowerShell) script instead of hello bash script.</span></span>
>
> <span data-ttu-id="aaf7d-133">Можно также использовать Azure PowerShell или toocreate HDInsight .NET SDK hello в кластер, использующий этот сценарий.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-133">You can also use Azure PowerShell or hello HDInsight .NET SDK toocreate a cluster using this script.</span></span> <span data-ttu-id="aaf7d-134">Дополнительные сведения об использовании этих методов см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="aaf7d-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="aaf7d-135">Запуск подготовки кластера с помощью действия hello в [HDInsight подготовки кластеров в Linux](hdinsight-hadoop-provision-linux-clusters.md), но не завершайте подготовки.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-135">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="aaf7d-136">На hello **необязательная конфигурация** колонке выберите **действия скрипта**и укажите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="aaf7d-136">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="aaf7d-137">**ИМЯ**: Введите понятное имя для действия сценария hello.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-137">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="aaf7d-138">**Универсальный код ресурса скрипта** — https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh;</span><span class="sxs-lookup"><span data-stu-id="aaf7d-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="aaf7d-139">**Головной** — установите флажок.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="aaf7d-140">**Рабочая роль** — установите флажок;</span><span class="sxs-lookup"><span data-stu-id="aaf7d-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="aaf7d-141">**Zookeeper** — оставьте это поле пустым;</span><span class="sxs-lookup"><span data-stu-id="aaf7d-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="aaf7d-142">**Параметры**: Введите hello WASB адрес toohello контейнера и учетную запись хранилища, содержащий hello JAR-файлов.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-142">**PARAMETERS**: Enter hello WASB address toohello container and storage account that contains hello jars.</span></span> <span data-ttu-id="aaf7d-143">(например, **wasb://libs@mystorage.blob.core.windows.net/**).</span><span class="sxs-lookup"><span data-stu-id="aaf7d-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="aaf7d-144">Внизу hello hello **действия скрипта**, использовать hello **выберите** конфигурация hello toosave кнопок.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-144">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span>

4. <span data-ttu-id="aaf7d-145">На hello **необязательная конфигурация** колонке выберите **связанные учетные записи хранения** и выберите hello **добавить ключ хранилища** ссылку.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-145">On hello **Optional Configuration** blade, select **Linked Storage Accounts** and select hello **Add a storage key** link.</span></span> <span data-ttu-id="aaf7d-146">Выберите учетную запись хранения hello, содержащий hello JAR-файлов, а затем использовать hello **выберите** кнопки toosave параметров и возвращаемого hello **необязательная конфигурация** колонку.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-146">Select hello storage account that contains hello jars, and then use hello **select** buttons toosave settings and return hello **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="aaf7d-147">Используйте hello **выберите** кнопку внизу hello hello **необязательная конфигурация** колонке toosave hello необязательная конфигурация сведения.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-147">Use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

6. <span data-ttu-id="aaf7d-148">Продолжить подготовки кластера hello, как описано в [HDInsight подготовки кластеров в Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="aaf7d-148">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="aaf7d-149">После завершения выполнения создания кластера, вы, добавляемые с помощью этого скрипта из куста без необходимости toouse hello JAR-файлов hello может toouse `ADD JAR` инструкции.</span><span class="sxs-lookup"><span data-stu-id="aaf7d-149">Once cluster creation finishes, you are able toouse hello jars added through this script from Hive without having toouse hello `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaf7d-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aaf7d-150">Next steps</span></span>

<span data-ttu-id="aaf7d-151">Дополнительные сведения о работе с Hive см. в статье [Использование Hive и HiveQL с Hadoop в HDInsight для анализа примера файла Apache log4j](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="aaf7d-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
