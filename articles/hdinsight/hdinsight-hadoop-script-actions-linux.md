---
title: "Разработка действий aaaScript с HDInsight под управлением Linux — в Azure | Документы Microsoft"
description: "Узнайте, как toouse Bash сценарии toocustomize кластеры HDInsight под управлением Linux. Hello скрипт действие hdinsight, позволяет toorun скриптов во время или после создания кластера. Скрипты можно использовать toochange параметры конфигурации кластера или установить дополнительное программное обеспечение."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="d9db1-105">Разработка действий сценариев с помощью HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9db1-105">Script action development with HDInsight</span></span>

<span data-ttu-id="d9db1-106">Узнайте, как Bash toocustomize кластера HDInsight с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="d9db1-106">Learn how toocustomize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="d9db1-107">Действия сценариев являются способом toocustomize HDInsight во время или после создания кластера.</span><span class="sxs-lookup"><span data-stu-id="d9db1-107">Script actions are a way toocustomize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9db1-108">Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux.</span><span class="sxs-lookup"><span data-stu-id="d9db1-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="d9db1-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="d9db1-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d9db1-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d9db1-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="d9db1-111">Что такое действия сценариев?</span><span class="sxs-lookup"><span data-stu-id="d9db1-111">What are script actions</span></span>

<span data-ttu-id="d9db1-112">Действия сценариев Bash скрипты, которые Azure работает на изменения конфигурации toomake узлы кластера hello и устанавливать программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="d9db1-112">Script actions are Bash scripts that Azure runs on hello cluster nodes toomake configuration changes or install software.</span></span> <span data-ttu-id="d9db1-113">Действие сценария выполняется как корневой и обеспечивает полный доступ узлов кластера toohello права.</span><span class="sxs-lookup"><span data-stu-id="d9db1-113">A script action is executed as root, and provides full access rights toohello cluster nodes.</span></span>

<span data-ttu-id="d9db1-114">Действия сценариев могут применяться через hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="d9db1-114">Script actions can be applied through hello following methods:</span></span>

| <span data-ttu-id="d9db1-115">Используйте этот метод tooapply сценария:</span><span class="sxs-lookup"><span data-stu-id="d9db1-115">Use this method tooapply a script...</span></span> | <span data-ttu-id="d9db1-116">При создании кластера…</span><span class="sxs-lookup"><span data-stu-id="d9db1-116">During cluster creation...</span></span> | <span data-ttu-id="d9db1-117">В работающем кластере…</span><span class="sxs-lookup"><span data-stu-id="d9db1-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="d9db1-118">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d9db1-118">Azure portal</span></span> |<span data-ttu-id="d9db1-119">✓ </span><span class="sxs-lookup"><span data-stu-id="d9db1-119">✓</span></span> |<span data-ttu-id="d9db1-120">✓</span><span class="sxs-lookup"><span data-stu-id="d9db1-120">✓</span></span> |
| <span data-ttu-id="d9db1-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9db1-121">Azure PowerShell</span></span> |<span data-ttu-id="d9db1-122">✓</span><span class="sxs-lookup"><span data-stu-id="d9db1-122">✓</span></span> |<span data-ttu-id="d9db1-123">✓</span><span class="sxs-lookup"><span data-stu-id="d9db1-123">✓</span></span> |
| <span data-ttu-id="d9db1-124">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="d9db1-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="d9db1-125">✓</span><span class="sxs-lookup"><span data-stu-id="d9db1-125">✓</span></span> |
| <span data-ttu-id="d9db1-126">Пакет SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="d9db1-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="d9db1-127">✓</span><span class="sxs-lookup"><span data-stu-id="d9db1-127">✓</span></span> |<span data-ttu-id="d9db1-128">✓</span><span class="sxs-lookup"><span data-stu-id="d9db1-128">✓</span></span> |
| <span data-ttu-id="d9db1-129">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d9db1-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="d9db1-130">✓ </span><span class="sxs-lookup"><span data-stu-id="d9db1-130">✓</span></span> |&nbsp; |

<span data-ttu-id="d9db1-131">Дополнительные сведения об использовании этих действий скрипта tooapply методов см. в разделе [HDInsight настроить кластеры, использующие действия скрипта](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d9db1-131">For more information on using these methods tooapply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="d9db1-132"><a name="bestPracticeScripting"></a>Рекомендации по разработке сценариев</span><span class="sxs-lookup"><span data-stu-id="d9db1-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="d9db1-133">При разработке пользовательского скрипта для кластера HDInsight, существует несколько лучшие методики tookeep помнить:</span><span class="sxs-lookup"><span data-stu-id="d9db1-133">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* [<span data-ttu-id="d9db1-134">Целевая версия Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="d9db1-134">Target hello Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="d9db1-135">Hello целевой версии ОС</span><span class="sxs-lookup"><span data-stu-id="d9db1-135">Target hello OS Version</span></span>](#bps10)
* [<span data-ttu-id="d9db1-136">Обеспечить стабильность связывает tooscript ресурсы</span><span class="sxs-lookup"><span data-stu-id="d9db1-136">Provide stable links tooscript resources</span></span>](#bPS2)
* [<span data-ttu-id="d9db1-137">Использование предварительно скомпилированных ресурсов</span><span class="sxs-lookup"><span data-stu-id="d9db1-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="d9db1-138">Убедитесь, что скрипт настройки кластера hello идемпотентными</span><span class="sxs-lookup"><span data-stu-id="d9db1-138">Ensure that hello cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="d9db1-139">Обеспечить высокий уровень доступности кластера архитектура hello</span><span class="sxs-lookup"><span data-stu-id="d9db1-139">Ensure high availability of hello cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="d9db1-140">Настройка хранилища больших двоичных объектов Azure toouse пользовательские компоненты hello</span><span class="sxs-lookup"><span data-stu-id="d9db1-140">Configure hello custom components toouse Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="d9db1-141">TooSTDOUT сведения о записи и STDERR</span><span class="sxs-lookup"><span data-stu-id="d9db1-141">Write information tooSTDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="d9db1-142">Сохранение файлов в формате ASCII с использованием LF в качестве символа завершения строки</span><span class="sxs-lookup"><span data-stu-id="d9db1-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="d9db1-143">Использовать toorecover логику повторных попыток от временных ошибок</span><span class="sxs-lookup"><span data-stu-id="d9db1-143">Use retry logic toorecover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="d9db1-144">Действия скриптов должна быть завершена в течение 60 минут или hello процесс завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="d9db1-144">Script actions must complete within 60 minutes or hello process fails.</span></span> <span data-ttu-id="d9db1-145">Во время инициализации узла, hello скрипт выполняется параллельно с другими процессами, установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="d9db1-145">During node provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="d9db1-146">Соперничество за ресурсы, такие как ЦП или в сети может вызвать скрипт hello tootake больше toofinish не так, как в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="d9db1-146">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>

### <span data-ttu-id="d9db1-147"><a name="bPS1"></a>Целевая версия Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="d9db1-147"><a name="bPS1"></a>Target hello Hadoop version</span></span>

<span data-ttu-id="d9db1-148">В различных версиях HDInsight используются различные версии служб Hadoop и компонентов.</span><span class="sxs-lookup"><span data-stu-id="d9db1-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="d9db1-149">Если сценарий требует определенной версии службы или компонента, hello скрипт следует использовать только с версией hello HDInsight, которая включает hello необходимых компонентов.</span><span class="sxs-lookup"><span data-stu-id="d9db1-149">If your script expects a specific version of a service or component, you should only use hello script with hello version of HDInsight that includes hello required components.</span></span> <span data-ttu-id="d9db1-150">Можно найти сведения о версии компонентов, включенных в HDInsight с помощью hello [управление версиями компонента HDInsight](hdinsight-component-versioning.md) документа.</span><span class="sxs-lookup"><span data-stu-id="d9db1-150">You can find information on component versions included with HDInsight using hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="d9db1-151"><a name="bps10"></a>Целевая версия ОС hello</span><span class="sxs-lookup"><span data-stu-id="d9db1-151"><a name="bps10"></a> Target hello OS version</span></span>

<span data-ttu-id="d9db1-152">HDInsight под управлением Linux основан на hello распространения Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="d9db1-152">Linux-based HDInsight is based on hello Ubuntu Linux distribution.</span></span> <span data-ttu-id="d9db1-153">Для разных версий HDInsight используются разные версии Ubuntu. Это может изменить поведение сценария.</span><span class="sxs-lookup"><span data-stu-id="d9db1-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="d9db1-154">Например, HDInsight версии 3.4 и более ранних версий основан на версии Ubuntu, в которой используется Upstart.</span><span class="sxs-lookup"><span data-stu-id="d9db1-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="d9db1-155">Версия 3.5 основана на Ubuntu версии 16.04, в которой используется Systemd.</span><span class="sxs-lookup"><span data-stu-id="d9db1-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="d9db1-156">Systemd и Upstart используют различные команды, скрипт должен быть записан toowork с обоими.</span><span class="sxs-lookup"><span data-stu-id="d9db1-156">Systemd and Upstart rely on different commands, so your script should be written toowork with both.</span></span>

<span data-ttu-id="d9db1-157">Является еще одним важным различием между HDInsight 3.4 и 3.5, `JAVA_HOME` теперь указывает tooJava 8.</span><span class="sxs-lookup"><span data-stu-id="d9db1-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points tooJava 8.</span></span>

<span data-ttu-id="d9db1-158">Версия ОС hello можно проверить с помощью `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-158">You can check hello OS version by using `lsb_release`.</span></span> <span data-ttu-id="d9db1-159">Hello следующий код демонстрирует, как toodetermine Если hello скрипт выполняется на Ubuntu 14 или 16:</span><span class="sxs-lookup"><span data-stu-id="d9db1-159">hello following code demonstrates how toodetermine if hello script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="d9db1-160">Можно найти hello полный скрипт, содержащий эти фрагменты кода в https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="d9db1-160">You can find hello full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="d9db1-161">Версию hello Ubuntu, используемый HDInsight см. в разделе hello [версия компонента HDInsight](hdinsight-component-versioning.md) документа.</span><span class="sxs-lookup"><span data-stu-id="d9db1-161">For hello version of Ubuntu that is used by HDInsight, see hello [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="d9db1-162">. в разделе toounderstand hello различия между Systemd и Upstart, [Systemd для пользователей Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="d9db1-162">toounderstand hello differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="d9db1-163"><a name="bPS2"></a>Обеспечить стабильность связывает tooscript ресурсы</span><span class="sxs-lookup"><span data-stu-id="d9db1-163"><a name="bPS2"></a>Provide stable links tooscript resources</span></span>

<span data-ttu-id="d9db1-164">Hello скрипта и связанных ресурсов должен оставаться доступными во время существования hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="d9db1-164">hello script and associated resources must remain available throughout hello lifetime of hello cluster.</span></span> <span data-ttu-id="d9db1-165">Эти ресурсы являются обязательными при добавлении новых узлов кластера toohello во время операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d9db1-165">These resources are required if new nodes are added toohello cluster during scaling operations.</span></span>

<span data-ttu-id="d9db1-166">Рекомендуется Hello является toodownload и архивировать все данные в учетной записи хранилища Azure для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="d9db1-166">hello best practice is toodownload and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9db1-167">Hello хранилища учетная запись должна быть hello по умолчанию учетной записи хранилища для кластера hello или открытые, только для чтения контейнера на любой другой учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d9db1-167">hello storage account used must be hello default storage account for hello cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="d9db1-168">Например, hello образцы, поставляемые корпорацией Майкрософт, хранятся в hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d9db1-168">For example, hello samples provided by Microsoft are stored in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="d9db1-169">Это поддерживается командой HDInsight hello контейнер открытым и доступным только для чтения.</span><span class="sxs-lookup"><span data-stu-id="d9db1-169">This is a public, read-only container maintained by hello HDInsight team.</span></span>

### <span data-ttu-id="d9db1-170"><a name="bPS4"></a>Использование предварительно скомпилированных ресурсов</span><span class="sxs-lookup"><span data-stu-id="d9db1-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="d9db1-171">tooreduce hello время принимает toorun hello скрипт, избежать операций, которые компиляции ресурсов из исходного кода.</span><span class="sxs-lookup"><span data-stu-id="d9db1-171">tooreduce hello time it takes toorun hello script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="d9db1-172">Например, предварительной компиляции ресурсов и сохранять их в большом двоичном объекте учетной записи хранилища Azure в hello же центре обработки данных с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d9db1-172">For example, pre-compile resources and store them in an Azure Storage account blob in hello same data center as HDInsight.</span></span>

### <span data-ttu-id="d9db1-173"><a name="bPS3"></a>Убедитесь, что скрипт настройки кластера hello идемпотентными</span><span class="sxs-lookup"><span data-stu-id="d9db1-173"><a name="bPS3"></a>Ensure that hello cluster customization script is idempotent</span></span>

<span data-ttu-id="d9db1-174">Сценарии должны быть идемпотентными.</span><span class="sxs-lookup"><span data-stu-id="d9db1-174">Scripts must be idempotent.</span></span> <span data-ttu-id="d9db1-175">Если сценарий hello запускается несколько раз, он должен возвращать hello же состояния при каждом toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="d9db1-175">If hello script runs multiple times, it should return hello cluster toohello same state every time.</span></span>

<span data-ttu-id="d9db1-176">Например, сценарий, который изменяет файлы конфигурации, не должен добавлять повторяющиеся записи в случае многократного выполнения.</span><span class="sxs-lookup"><span data-stu-id="d9db1-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="d9db1-177"><a name="bPS5"></a>Обеспечить высокий уровень доступности кластера архитектура hello</span><span class="sxs-lookup"><span data-stu-id="d9db1-177"><a name="bPS5"></a>Ensure high availability of hello cluster architecture</span></span>

<span data-ttu-id="d9db1-178">Кластеры HDInsight под управлением Linux предоставляют два головного узла, которые активны в кластере hello и скрипт действия выполняются на обоих узлах.</span><span class="sxs-lookup"><span data-stu-id="d9db1-178">Linux-based HDInsight clusters provide two head nodes that are active within hello cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="d9db1-179">Если hello компоненты, которые можно установить только один головной узел, не устанавливайте компоненты hello на оба головного узла.</span><span class="sxs-lookup"><span data-stu-id="d9db1-179">If hello components you install expect only one head node, do not install hello components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9db1-180">Службы, предоставляемые в рамках HDInsight превышают спроектированный toofail между двумя узлами головного hello при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d9db1-180">Services provided as part of HDInsight are designed toofail over between hello two head nodes as needed.</span></span> <span data-ttu-id="d9db1-181">Эта функция не будет продлен toocustom компоненты устанавливаются с помощью действий скрипта.</span><span class="sxs-lookup"><span data-stu-id="d9db1-181">This functionality is not extended toocustom components installed through script actions.</span></span> <span data-ttu-id="d9db1-182">Если требуется высокий уровень доступности пользовательских компонентов, необходимо реализовать собственный механизм отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="d9db1-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="d9db1-183"><a name="bPS6"></a>Настройка хранилища больших двоичных объектов Azure toouse пользовательские компоненты hello</span><span class="sxs-lookup"><span data-stu-id="d9db1-183"><a name="bPS6"></a>Configure hello custom components toouse Azure Blob storage</span></span>

<span data-ttu-id="d9db1-184">Возможно, компонентов, установленных на кластер hello конфигурацию по умолчанию, который использует хранилище системы распределенных файла Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="d9db1-184">Components that you install on hello cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="d9db1-185">HDInsight использует хранилище Azure или хранилища Озера данных в качестве хранилища по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-185">HDInsight uses either Azure Storage or Data Lake Store as hello default storage.</span></span> <span data-ttu-id="d9db1-186">Они обеспечивают системой совместимый файл HDFS, которая сохраняет данные, даже если удалить кластер hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-186">Both provide an HDFS compatible file system that persists data even if hello cluster is deleted.</span></span> <span data-ttu-id="d9db1-187">Может потребоваться установить toouse WASB или ADL вместо HDFS компонентов tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="d9db1-187">You may need tooconfigure components you install toouse WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="d9db1-188">Для большинства операций не обязательно toospecify hello файловой системы.</span><span class="sxs-lookup"><span data-stu-id="d9db1-188">For most operations, you do not need toospecify hello file system.</span></span> <span data-ttu-id="d9db1-189">Например следующие hello копирует файл giraph-examples.jar hello из хранилища toocluster hello локальной файловой системы:</span><span class="sxs-lookup"><span data-stu-id="d9db1-189">For example, hello following copies hello giraph-examples.jar file from hello local file system toocluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="d9db1-190">В этом примере hello `hdfs` команда прозрачно использует хранилище кластера по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-190">In this example, hello `hdfs` command transparently uses hello default cluster storage.</span></span> <span data-ttu-id="d9db1-191">Для некоторых операций может потребоваться toospecify hello URI.</span><span class="sxs-lookup"><span data-stu-id="d9db1-191">For some operations, you may need toospecify hello URI.</span></span> <span data-ttu-id="d9db1-192">Например, `adl:///example/jars` для Data Lake Store или `wasb:///example/jars` для хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d9db1-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="d9db1-193"><a name="bPS7"></a>TooSTDOUT сведения о записи и STDERR</span><span class="sxs-lookup"><span data-stu-id="d9db1-193"><a name="bPS7"></a>Write information tooSTDOUT and STDERR</span></span>

<span data-ttu-id="d9db1-194">HDInsight заносит в журнал выходные данные скрипт, написанный tooSTDOUT и STDERR.</span><span class="sxs-lookup"><span data-stu-id="d9db1-194">HDInsight logs script output that is written tooSTDOUT and STDERR.</span></span> <span data-ttu-id="d9db1-195">Можно просмотреть эти сведения, с помощью Ambari web hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d9db1-195">You can view this information using hello Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="d9db1-196">Ambari доступна только в том случае, если hello кластер успешно создан.</span><span class="sxs-lookup"><span data-stu-id="d9db1-196">Ambari is only available if hello cluster is successfully created.</span></span> <span data-ttu-id="d9db1-197">Hello, устранении неполадок см. Если вы используете действие сценария во время создания кластера и создание завершается с ошибкой, [HDInsight настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) другие способы доступа к записываемых данных.</span><span class="sxs-lookup"><span data-stu-id="d9db1-197">If you use a script action during cluster creation, and creation fails, see hello troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="d9db1-198">Большинство программ и пакеты установки уже записи tooSTDOUT сведения и STDERR, однако вы можете tooadd более подробное ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="d9db1-198">Most utilities and installation packages already write information tooSTDOUT and STDERR, however you may want tooadd additional logging.</span></span> <span data-ttu-id="d9db1-199">tooSTDOUT toosend текста, используйте `echo`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-199">toosend text tooSTDOUT, use `echo`.</span></span> <span data-ttu-id="d9db1-200">Например:</span><span class="sxs-lookup"><span data-stu-id="d9db1-200">For example:</span></span>

```bash
echo "Getting ready tooinstall Foo"
```

<span data-ttu-id="d9db1-201">По умолчанию `echo` отправляет hello tooSTDOUT строки.</span><span class="sxs-lookup"><span data-stu-id="d9db1-201">By default, `echo` sends hello string tooSTDOUT.</span></span> <span data-ttu-id="d9db1-202">toodirect его tooSTDERR, добавьте `>&2` перед `echo`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-202">toodirect it tooSTDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="d9db1-203">Например:</span><span class="sxs-lookup"><span data-stu-id="d9db1-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="d9db1-204">Это перенаправляет данные, которые записываются вместо tooSTDOUT tooSTDERR (2).</span><span class="sxs-lookup"><span data-stu-id="d9db1-204">This redirects information written tooSTDOUT tooSTDERR (2) instead.</span></span> <span data-ttu-id="d9db1-205">Дополнительные сведения о перенаправлении ввода-вывода см. на странице [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="d9db1-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="d9db1-206">Дополнительные сведения о просмотре журналов, созданных действиями сценариев, см. в статье [Настройка кластеров HDInsight с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="d9db1-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="d9db1-207"><a name="bps8"></a> Сохранение файлов в формате ASCII с использованием LF в качестве символа завершения строки</span><span class="sxs-lookup"><span data-stu-id="d9db1-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="d9db1-208">Сценарии Bash должны храниться в формате ASCII. Для завершения строк в этом файле используется символ LF.</span><span class="sxs-lookup"><span data-stu-id="d9db1-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="d9db1-209">Файлы, которые хранятся в кодировке UTF-8 или использовать в качестве завершения строк hello CRLF могут завершаться со hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="d9db1-209">Files that are stored as UTF-8, or use CRLF as hello line ending may fail with hello following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="d9db1-210"><a name="bps9"></a>Использовать toorecover логику повторных попыток от временных ошибок</span><span class="sxs-lookup"><span data-stu-id="d9db1-210"><a name="bps9"></a> Use retry logic toorecover from transient errors</span></span>

<span data-ttu-id="d9db1-211">При загрузке файлов, установки пакетов с помощью apt get или других действий, которые передачи данных через Здравствуйте Интернета, действие hello может завершиться ошибкой из-за ошибки сети tootransient.</span><span class="sxs-lookup"><span data-stu-id="d9db1-211">When downloading files, installing packages using apt-get, or other actions that transmit data over hello internet, hello action may fail due tootransient networking errors.</span></span> <span data-ttu-id="d9db1-212">Например удаленный ресурс hello, которые обмениваются данными с может быть в процессе hello переключения tooa узел резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="d9db1-212">For example, hello remote resource you are communicating with may be in hello process of failing over tooa backup node.</span></span>

<span data-ttu-id="d9db1-213">toomake устойчивым tootransient ошибки скрипта, можно реализовать логику повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="d9db1-213">toomake your script resilient tootransient errors, you can implement retry logic.</span></span> <span data-ttu-id="d9db1-214">следующие функции Hello показано, как tooimplement логику повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="d9db1-214">hello following function demonstrates how tooimplement retry logic.</span></span> <span data-ttu-id="d9db1-215">Он пытается выполнить сбойные операции hello трижды до сбоя.</span><span class="sxs-lookup"><span data-stu-id="d9db1-215">It retries hello operation three times before failing.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="d9db1-216">Hello следующие примеры демонстрируют, как toouse эту функцию.</span><span class="sxs-lookup"><span data-stu-id="d9db1-216">hello following examples demonstrate how toouse this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="d9db1-217"><a name="helpermethods"></a>Вспомогательные методы для пользовательских сценариев</span><span class="sxs-lookup"><span data-stu-id="d9db1-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="d9db1-218">Вспомогательные методы действий сценариев — это служебные программы, которые можно использовать при создании пользовательских сценариев.</span><span class="sxs-lookup"><span data-stu-id="d9db1-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="d9db1-219">Эти методы содержатся в сценарии [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="d9db1-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="d9db1-220">Используйте следующие toodownload hello и использовать их как часть сценария:</span><span class="sxs-lookup"><span data-stu-id="d9db1-220">Use hello following toodownload and use them as part of your script:</span></span>

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="d9db1-221">Hello следующие вспомогательные классы, доступные для использования в скрипте:</span><span class="sxs-lookup"><span data-stu-id="d9db1-221">hello following helpers available for use in your script:</span></span>

| <span data-ttu-id="d9db1-222">Назначение вспомогательного приложения</span><span class="sxs-lookup"><span data-stu-id="d9db1-222">Helper usage</span></span> | <span data-ttu-id="d9db1-223">Описание</span><span class="sxs-lookup"><span data-stu-id="d9db1-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="d9db1-224">Загружает файл из hello исходный URI toohello указанный путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="d9db1-224">Downloads a file from hello source URI toohello specified file path.</span></span> <span data-ttu-id="d9db1-225">По умолчанию существующий файл не перезаписывается.</span><span class="sxs-lookup"><span data-stu-id="d9db1-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="d9db1-226">Извлекает tar-файл (с помощью `-xf`) toohello целевой каталог.</span><span class="sxs-lookup"><span data-stu-id="d9db1-226">Extracts a tar file (using `-xf`) toohello destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="d9db1-227">При запуске на головном узле кластера возвращает значение 1, в противном случае — 0.</span><span class="sxs-lookup"><span data-stu-id="d9db1-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="d9db1-228">Если hello текущий узел является узлом данных (рабочая), возвращают значение 1; в противном случае — 0.</span><span class="sxs-lookup"><span data-stu-id="d9db1-228">If hello current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="d9db1-229">Если hello текущий узел сначала данные hello (рабочая) узла (именованные workernode0) возвращает 1; в противном случае — 0.</span><span class="sxs-lookup"><span data-stu-id="d9db1-229">If hello current node is hello first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="d9db1-230">Полное доменное имя возвращаемого hello headnodes hello в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-230">Return hello fully qualified domain name of hello headnodes in hello cluster.</span></span> <span data-ttu-id="d9db1-231">Имена содержат разделители-запятые.</span><span class="sxs-lookup"><span data-stu-id="d9db1-231">Names are comma delimited.</span></span> <span data-ttu-id="d9db1-232">При возникновении ошибки возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="d9db1-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="d9db1-233">Возвращает полное доменное имя hello головному узлу первичной hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-233">Gets hello fully qualified domain name of hello primary headnode.</span></span> <span data-ttu-id="d9db1-234">При возникновении ошибки возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="d9db1-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="d9db1-235">Возвращает hello полное доменное имя получателя головному узлу hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-235">Gets hello fully qualified domain name of hello secondary headnode.</span></span> <span data-ttu-id="d9db1-236">При возникновении ошибки возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="d9db1-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="d9db1-237">Возвращает числовой суффикс hello головному узлу первичной hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-237">Gets hello numeric suffix of hello primary headnode.</span></span> <span data-ttu-id="d9db1-238">При возникновении ошибки возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="d9db1-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="d9db1-239">Возвращает числовой суффикс hello объекта получателя головному узлу hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-239">Gets hello numeric suffix of hello secondary headnode.</span></span> <span data-ttu-id="d9db1-240">При возникновении ошибки возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="d9db1-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="d9db1-241"><a name="commonusage"></a>Общие варианты использования</span><span class="sxs-lookup"><span data-stu-id="d9db1-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="d9db1-242">В этом разделе приводятся рекомендации по реализации некоторых hello распространенных шаблонов использования, вы можете столкнуться при написании пользовательского скрипта.</span><span class="sxs-lookup"><span data-stu-id="d9db1-242">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-tooa-script"></a><span data-ttu-id="d9db1-243">Передача параметров сценария tooa</span><span class="sxs-lookup"><span data-stu-id="d9db1-243">Passing parameters tooa script</span></span>

<span data-ttu-id="d9db1-244">В некоторых случаях для сценария требуется указывать параметры.</span><span class="sxs-lookup"><span data-stu-id="d9db1-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="d9db1-245">Например может потребоваться пароль администратора hello для hello кластера при использовании Ambari REST API hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-245">For example, you may need hello admin password for hello cluster when using hello Ambari REST API.</span></span>

<span data-ttu-id="d9db1-246">Параметры, передаваемые toohello сценария известны как *позиционные параметры*и им назначается слишком`$1` для первого параметра hello, `$2` для hello второй и поэтому на.</span><span class="sxs-lookup"><span data-stu-id="d9db1-246">Parameters passed toohello script are known as *positional parameters*, and are assigned too`$1` for hello first parameter, `$2` for hello second, and so-on.</span></span> <span data-ttu-id="d9db1-247">`$0`содержит имя самого сценария hello hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-247">`$0` contains hello name of hello script itself.</span></span>

<span data-ttu-id="d9db1-248">Значения, передаваемые toohello сценария в качестве параметров должны быть заключены в одинарные кавычки (').</span><span class="sxs-lookup"><span data-stu-id="d9db1-248">Values passed toohello script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="d9db1-249">Это гарантирует, что hello передано значение рассматривается как литерал.</span><span class="sxs-lookup"><span data-stu-id="d9db1-249">Doing so ensures that hello passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="d9db1-250">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="d9db1-250">Setting environment variables</span></span>

<span data-ttu-id="d9db1-251">Установив переменную среды осуществляется hello следующей инструкцией:</span><span class="sxs-lookup"><span data-stu-id="d9db1-251">Setting an environment variable is performed by hello following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="d9db1-252">Где VARIABLENAME — hello имя переменной hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-252">Where VARIABLENAME is hello name of hello variable.</span></span> <span data-ttu-id="d9db1-253">Использование переменной, hello tooaccess `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-253">tooaccess hello variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="d9db1-254">Например tooassign значение, предоставляемые позиционного параметра переменной среды с именем пароль, следует использовать hello, следующем за инструкцией:</span><span class="sxs-lookup"><span data-stu-id="d9db1-254">For example, tooassign a value provided by a positional parameter as an environment variable named PASSWORD, you would use hello following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="d9db1-255">Затем можно использовать сведения toohello последующий доступ к нему `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-255">Subsequent access toohello information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="d9db1-256">Переменные среды, заданные в скриптах hello существуют только в области hello hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="d9db1-256">Environment variables set within hello script only exist within hello scope of hello script.</span></span> <span data-ttu-id="d9db1-257">В некоторых случаях может потребоваться tooadd системные переменные, которые будет сохраняться после hello сценария.</span><span class="sxs-lookup"><span data-stu-id="d9db1-257">In some cases, you may need tooadd system-wide environment variables that will persist after hello script has finished.</span></span> <span data-ttu-id="d9db1-258">переменные среды уровня системы tooadd, добавьте переменную hello слишком`/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-258">tooadd system-wide environment variables, add hello variable too`/etc/environment`.</span></span> <span data-ttu-id="d9db1-259">Например, добавляет hello, следующем за инструкцией `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="d9db1-259">For example, hello following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="d9db1-260">Доступ к toolocations, где хранятся пользовательские сценарии hello</span><span class="sxs-lookup"><span data-stu-id="d9db1-260">Access toolocations where hello custom scripts are stored</span></span>

<span data-ttu-id="d9db1-261">Скрипты, используемые toocustomize кластер должен toobe хранятся в одном из следующих элементов hello:</span><span class="sxs-lookup"><span data-stu-id="d9db1-261">Scripts used toocustomize a cluster needs toobe stored in one of hello following locations:</span></span>

* <span data-ttu-id="d9db1-262">__Учетной записи хранилища Azure__ связанное с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-262">An __Azure Storage account__ that is associated with hello cluster.</span></span>

* <span data-ttu-id="d9db1-263">__Дополнительная учетная запись хранения__ связанные с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-263">An __additional storage account__ associated with hello cluster.</span></span>

* <span data-ttu-id="d9db1-264">__ресурсе с общедоступным URI__.</span><span class="sxs-lookup"><span data-stu-id="d9db1-264">A __publicly readable URI__.</span></span> <span data-ttu-id="d9db1-265">Например URL-адрес toodata хранятся в OneDrive, Dropbox или другой файл размещения службы.</span><span class="sxs-lookup"><span data-stu-id="d9db1-265">For example, a URL toodata stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="d9db1-266">__Хранилища Озера данных Azure__ связанное с кластером HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-266">An __Azure Data Lake Store account__ that is associated with hello HDInsight cluster.</span></span> <span data-ttu-id="d9db1-267">Дополнительные сведения об использовании Azure Data Lake Store с HDInsight см. в статье [Создание кластера HDInsight с хранилищем озера данных с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d9db1-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9db1-268">tooaccess Hello службы основной HDInsight использует хранилище Озера данных должен иметь доступ на чтение toohello сценария.</span><span class="sxs-lookup"><span data-stu-id="d9db1-268">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

<span data-ttu-id="d9db1-269">Ресурсы, используемые сценарием hello также необходимо быть общедоступным.</span><span class="sxs-lookup"><span data-stu-id="d9db1-269">Resources used by hello script must also be publicly available.</span></span>

<span data-ttu-id="d9db1-270">Хранение файлов hello в учетной записи хранилища Azure или хранилища Озера данных Azure предоставляет быстрый доступ, как в пределах hello сети Azure.</span><span class="sxs-lookup"><span data-stu-id="d9db1-270">Storing hello files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within hello Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="d9db1-271">Hello URI формат, используемый tooreference hello сценария зависит от того, использование службы hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-271">hello URI format used tooreference hello script differs depending on hello service being used.</span></span> <span data-ttu-id="d9db1-272">Учетные записи хранения, связанные с кластером HDInsight hello, используйте `wasb://` или `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-272">For storage accounts associated with hello HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="d9db1-273">для общедоступного универсального кода ресурса (URI) — `http://` или `https://`,</span><span class="sxs-lookup"><span data-stu-id="d9db1-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="d9db1-274">а для Data Lake Store — `adl://`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-hello-operating-system-version"></a><span data-ttu-id="d9db1-275">Проверка версии операционной системы hello</span><span class="sxs-lookup"><span data-stu-id="d9db1-275">Checking hello operating system version</span></span>

<span data-ttu-id="d9db1-276">Для разных версий HDInsight используются конкретные версии Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d9db1-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="d9db1-277">В сценарии следует проверить различия между версиями ОС.</span><span class="sxs-lookup"><span data-stu-id="d9db1-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="d9db1-278">Например может потребоваться tooinstall связанные toohello версия Ubuntu двоичный файл.</span><span class="sxs-lookup"><span data-stu-id="d9db1-278">For example, you may need tooinstall a binary that is tied toohello version of Ubuntu.</span></span>

<span data-ttu-id="d9db1-279">toocheck hello ОС версии, используйте `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-279">toocheck hello OS version, use `lsb_release`.</span></span> <span data-ttu-id="d9db1-280">Например hello следующий сценарий демонстрирует, как файл tooreference конкретных tar-файл в зависимости от версии ОС hello:</span><span class="sxs-lookup"><span data-stu-id="d9db1-280">For example, hello following script demonstrates how tooreference a specific tar file depending on hello OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <span data-ttu-id="d9db1-281"><a name="deployScript"></a>Контрольный список для развертывания действия сценария</span><span class="sxs-lookup"><span data-stu-id="d9db1-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="d9db1-282">Ниже приведены шаги hello, который мы воспользовались при подготовке toodeploy эти скрипты.</span><span class="sxs-lookup"><span data-stu-id="d9db1-282">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

* <span data-ttu-id="d9db1-283">Поместите файлы hello, содержащие пользовательские скрипты hello в месте, доступном из узлов кластера hello во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="d9db1-283">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="d9db1-284">Например hello хранилища по умолчанию для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-284">For example, hello default storage for hello cluster.</span></span> <span data-ttu-id="d9db1-285">Файлы также могут храниться в общедоступных службах размещения.</span><span class="sxs-lookup"><span data-stu-id="d9db1-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="d9db1-286">Убедитесь, что скрипт hello impotent.</span><span class="sxs-lookup"><span data-stu-id="d9db1-286">Verify that hello script is impotent.</span></span> <span data-ttu-id="d9db1-287">Это позволит toobe hello сценарий выполняться несколько раз на hello же узла.</span><span class="sxs-lookup"><span data-stu-id="d9db1-287">Doing so allows hello script toobe executed multiple times on hello same node.</span></span>
* <span data-ttu-id="d9db1-288">Использование типа hello tookeep временный файл/TMP directory загруженные файлы, используемые сценарии hello и затем очистить их после выполнения скриптов.</span><span class="sxs-lookup"><span data-stu-id="d9db1-288">Use a temporary file directory /tmp tookeep hello downloaded files used by hello scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="d9db1-289">Если изменяются параметры на уровне операционной системы или файлы конфигурации службы Hadoop, вы можете toorestart службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d9db1-289">If OS-level settings or Hadoop service configuration files are changed, you may want toorestart HDInsight services.</span></span>

## <span data-ttu-id="d9db1-290"><a name="runScriptAction"></a>Как toorun действие сценария</span><span class="sxs-lookup"><span data-stu-id="d9db1-290"><a name="runScriptAction"></a>How toorun a script action</span></span>

<span data-ttu-id="d9db1-291">Можно использовать сценарий toocustomize действия HDInsight кластеры, использующие hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="d9db1-291">You can use script actions toocustomize HDInsight clusters using hello following methods:</span></span>

* <span data-ttu-id="d9db1-292">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d9db1-292">Azure portal</span></span>
* <span data-ttu-id="d9db1-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9db1-293">Azure PowerShell</span></span>
* <span data-ttu-id="d9db1-294">Шаблоны диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="d9db1-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="d9db1-295">Здравствуйте, HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d9db1-295">hello HDInsight .NET SDK.</span></span>

<span data-ttu-id="d9db1-296">Дополнительные сведения об использовании каждого метода см. в разделе [как toouse записать действие в скрипт](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d9db1-296">For more information on using each method, see [How toouse script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="d9db1-297"><a name="sampleScripts"></a>Примеры пользовательских сценариев</span><span class="sxs-lookup"><span data-stu-id="d9db1-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="d9db1-298">Корпорация Майкрософт предоставляет примеры сценариев tooinstall компонентов в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d9db1-298">Microsoft provides sample scripts tooinstall components on an HDInsight cluster.</span></span> <span data-ttu-id="d9db1-299">См. следующие ссылки для выполнения сценариев дополнительные пример hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-299">See hello following links for more example script actions.</span></span>

* [<span data-ttu-id="d9db1-300">Установка и использование Hue в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9db1-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="d9db1-301">Установка и использование Solr в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9db1-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="d9db1-302">Установка и использование Giraph в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9db1-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="d9db1-303">Установка и обновление Mono в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9db1-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="d9db1-304">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="d9db1-304">Troubleshooting</span></span>

<span data-ttu-id="d9db1-305">Здесь представлены Hello ошибок, которые могут возникнуть при использовании скриптов, разработанным:</span><span class="sxs-lookup"><span data-stu-id="d9db1-305">hello following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="d9db1-306">**Ошибка**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="d9db1-307">Иногда дополняется фразой `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="d9db1-308">*Причина*: Эта ошибка возникает, когда hello строки в скрипте заканчиваться CRLF.</span><span class="sxs-lookup"><span data-stu-id="d9db1-308">*Cause*: This error is caused when hello lines in a script end with CRLF.</span></span> <span data-ttu-id="d9db1-309">В системах UNIX ожидать только LF как hello завершения строк.</span><span class="sxs-lookup"><span data-stu-id="d9db1-309">Unix systems expect only LF as hello line ending.</span></span>

<span data-ttu-id="d9db1-310">Эта проблема чаще всего происходит, когда hello скрипт создается в среде Windows, CRLF является общей оси конца для многих текстовых редакторах, в Windows.</span><span class="sxs-lookup"><span data-stu-id="d9db1-310">This problem most often occurs when hello script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="d9db1-311">*Разрешение*: Если этот вариант в текстовом редакторе, выберите формат Unix или LF hello завершения строк.</span><span class="sxs-lookup"><span data-stu-id="d9db1-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for hello line ending.</span></span> <span data-ttu-id="d9db1-312">Можно также использовать следующие команды на tooan CRLF hello toochange системы Unix LF hello:</span><span class="sxs-lookup"><span data-stu-id="d9db1-312">You may also use hello following commands on a Unix system toochange hello CRLF tooan LF:</span></span>

> [!NOTE]
> <span data-ttu-id="d9db1-313">Hello следующие команды представляют собой примерно соответствует тем, что им следует менять tooLF символ конца строки CRLF hello.</span><span class="sxs-lookup"><span data-stu-id="d9db1-313">hello following commands are roughly equivalent in that they should change hello CRLF line endings tooLF.</span></span> <span data-ttu-id="d9db1-314">Выберите его в соответствии с hello служебных программ, доступных в системе.</span><span class="sxs-lookup"><span data-stu-id="d9db1-314">Select one based on hello utilities available on your system.</span></span>

| <span data-ttu-id="d9db1-315">Команда</span><span class="sxs-lookup"><span data-stu-id="d9db1-315">Command</span></span> | <span data-ttu-id="d9db1-316">Примечания</span><span class="sxs-lookup"><span data-stu-id="d9db1-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="d9db1-317">исходный файл Hello резервного копирования с. Расширение BAK</span><span class="sxs-lookup"><span data-stu-id="d9db1-317">hello original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="d9db1-318">В файле OUTFILE для окончания строк будут использоваться только символы LF.</span><span class="sxs-lookup"><span data-stu-id="d9db1-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="d9db1-319">Изменяет файл hello напрямую</span><span class="sxs-lookup"><span data-stu-id="d9db1-319">Modifies hello file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="d9db1-320">В файле OUTFILE для окончания строк будут использоваться только символы LF.</span><span class="sxs-lookup"><span data-stu-id="d9db1-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="d9db1-321">**Ошибка**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="d9db1-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="d9db1-322">*Причина*: Эта ошибка возникает при hello скрипт был сохранен как с метки порядка байтов (BOM) UTF-8.</span><span class="sxs-lookup"><span data-stu-id="d9db1-322">*Cause*: This error occurs when hello script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="d9db1-323">*Разрешение*: hello файл в формате ASCII или UTF-8 без метки порядка БАЙТОВ.</span><span class="sxs-lookup"><span data-stu-id="d9db1-323">*Resolution*: Save hello file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="d9db1-324">Можно также использовать следующую команду на Linux или Unix системы toocreate файл без hello Спецификации hello:</span><span class="sxs-lookup"><span data-stu-id="d9db1-324">You may also use hello following command on a Linux or Unix system toocreate a file without hello BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="d9db1-325">Замените `INFILE` с файлом hello содержащий hello Спецификации.</span><span class="sxs-lookup"><span data-stu-id="d9db1-325">Replace `INFILE` with hello file containing hello BOM.</span></span> <span data-ttu-id="d9db1-326">`OUTFILE`должно быть новое имя файла, содержащего сценарий hello без hello Спецификации.</span><span class="sxs-lookup"><span data-stu-id="d9db1-326">`OUTFILE` should be a new file name, which contains hello script without hello BOM.</span></span>

## <span data-ttu-id="d9db1-327"><a name="seeAlso"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9db1-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="d9db1-328">Узнайте, каким образом слишком[HDInsight настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="d9db1-328">Learn how too[Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="d9db1-329">Используйте hello [HDInsight .NET SDK ссылка](https://msdn.microsoft.com/library/mt271028.aspx) toolearn Дополнительные сведения о создании приложений .NET, которые управляют HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9db1-329">Use hello [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) toolearn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="d9db1-330">Используйте hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn как действия по управлению tooperform toouse REST на HDInsight кластеров.</span><span class="sxs-lookup"><span data-stu-id="d9db1-330">Use hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn how toouse REST tooperform management actions on HDInsight clusters.</span></span>
