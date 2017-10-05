---
title: "Разработка действий сценариев с помощью кластера HDInsight под управлением Linux (Azure) | Документация Майкрософт"
description: "Узнайте, как настраивать кластеры HDInsight под управлением Linux с помощью bash-сценариев. Действия сценариев в HDInsight позволяют выполнять сценарии во время или после создания кластера. С помощью сценария можно изменить параметры конфигурации кластера или установить дополнительное программное обеспечение."
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
ms.openlocfilehash: 7f1a0bd8c7e60770d376f10eaea136a55c632c5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="2fd7b-105">Разработка действий сценариев с помощью HDInsight</span><span class="sxs-lookup"><span data-stu-id="2fd7b-105">Script action development with HDInsight</span></span>

<span data-ttu-id="2fd7b-106">Узнайте, как настроить кластер HDInsight с помощью сценариев Bash.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-106">Learn how to customize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="2fd7b-107">Действия сценариев предназначены для настройки HDInsight во время или после создания кластера.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-107">Script actions are a way to customize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fd7b-108">Для выполнения действий, описанных в этом документе, необходим кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="2fd7b-109">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2fd7b-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="2fd7b-111">Что такое действия сценариев?</span><span class="sxs-lookup"><span data-stu-id="2fd7b-111">What are script actions</span></span>

<span data-ttu-id="2fd7b-112">Действия сценариев — это сценарии Bash, которые Azure выполняет на узлах кластера, чтобы вносить изменения в конфигурацию или устанавливать программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-112">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span></span> <span data-ttu-id="2fd7b-113">Действие сценария выполняется от имени привилегированного пользователя и предоставляет права полного доступа к узлам кластера.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-113">A script action is executed as root, and provides full access rights to the cluster nodes.</span></span>

<span data-ttu-id="2fd7b-114">Действия сценариев могут применяться следующими способами:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-114">Script actions can be applied through the following methods:</span></span>

| <span data-ttu-id="2fd7b-115">Этот метод используется для применения сценария…</span><span class="sxs-lookup"><span data-stu-id="2fd7b-115">Use this method to apply a script...</span></span> | <span data-ttu-id="2fd7b-116">При создании кластера…</span><span class="sxs-lookup"><span data-stu-id="2fd7b-116">During cluster creation...</span></span> | <span data-ttu-id="2fd7b-117">В работающем кластере…</span><span class="sxs-lookup"><span data-stu-id="2fd7b-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="2fd7b-118">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="2fd7b-118">Azure portal</span></span> |<span data-ttu-id="2fd7b-119">✓ </span><span class="sxs-lookup"><span data-stu-id="2fd7b-119">✓</span></span> |<span data-ttu-id="2fd7b-120">✓</span><span class="sxs-lookup"><span data-stu-id="2fd7b-120">✓</span></span> |
| <span data-ttu-id="2fd7b-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd7b-121">Azure PowerShell</span></span> |<span data-ttu-id="2fd7b-122">✓</span><span class="sxs-lookup"><span data-stu-id="2fd7b-122">✓</span></span> |<span data-ttu-id="2fd7b-123">✓</span><span class="sxs-lookup"><span data-stu-id="2fd7b-123">✓</span></span> |
| <span data-ttu-id="2fd7b-124">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="2fd7b-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="2fd7b-125">✓</span><span class="sxs-lookup"><span data-stu-id="2fd7b-125">✓</span></span> |
| <span data-ttu-id="2fd7b-126">Пакет SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="2fd7b-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="2fd7b-127">✓</span><span class="sxs-lookup"><span data-stu-id="2fd7b-127">✓</span></span> |<span data-ttu-id="2fd7b-128">✓</span><span class="sxs-lookup"><span data-stu-id="2fd7b-128">✓</span></span> |
| <span data-ttu-id="2fd7b-129">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2fd7b-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="2fd7b-130">✓</span><span class="sxs-lookup"><span data-stu-id="2fd7b-130">✓</span></span> |&nbsp; |

<span data-ttu-id="2fd7b-131">Дополнительные сведения об использовании этих методов см. в статье [Настройка кластеров HDInsight с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-131">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="2fd7b-132"><a name="bestPracticeScripting"></a>Рекомендации по разработке сценариев</span><span class="sxs-lookup"><span data-stu-id="2fd7b-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="2fd7b-133">При разработке пользовательского сценария для кластера HDInsight следует иметь в виду некоторые рекомендации.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-133">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* [<span data-ttu-id="2fd7b-134">Выбор версии Hadoop</span><span class="sxs-lookup"><span data-stu-id="2fd7b-134">Target the Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="2fd7b-135">Выбор версии ОС</span><span class="sxs-lookup"><span data-stu-id="2fd7b-135">Target the OS Version</span></span>](#bps10)
* [<span data-ttu-id="2fd7b-136">Предоставление стабильных ссылок на ресурсы сценария</span><span class="sxs-lookup"><span data-stu-id="2fd7b-136">Provide stable links to script resources</span></span>](#bPS2)
* [<span data-ttu-id="2fd7b-137">Использование предварительно скомпилированных ресурсов</span><span class="sxs-lookup"><span data-stu-id="2fd7b-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="2fd7b-138">Обеспечение идемпотентности сценария настройки кластера</span><span class="sxs-lookup"><span data-stu-id="2fd7b-138">Ensure that the cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="2fd7b-139">Обеспечение высокого уровня доступности кластера</span><span class="sxs-lookup"><span data-stu-id="2fd7b-139">Ensure high availability of the cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="2fd7b-140">Настройка пользовательских компонентов для использования хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="2fd7b-140">Configure the custom components to use Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="2fd7b-141">Запись информации в STDOUT и STDERR</span><span class="sxs-lookup"><span data-stu-id="2fd7b-141">Write information to STDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="2fd7b-142">Сохранение файлов в формате ASCII с использованием LF в качестве символа завершения строки</span><span class="sxs-lookup"><span data-stu-id="2fd7b-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="2fd7b-143">Использование логики повтора для восстановления после временных ошибок</span><span class="sxs-lookup"><span data-stu-id="2fd7b-143">Use retry logic to recover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="2fd7b-144">Действия сценария должны завершиться в течение 60 минут. В противном случае процесс завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-144">Script actions must complete within 60 minutes or the process fails.</span></span> <span data-ttu-id="2fd7b-145">Во время подготовки узла данный сценарий выполняется одновременно с другими процессами установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-145">During node provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="2fd7b-146">Конкуренция за ресурсы, такие как ЦП или пропускная способность сети, может привести к затягиванию выполнения сценария по сравнению со временем его выполнения в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-146">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>

### <span data-ttu-id="2fd7b-147"><a name="bPS1"></a>Выбор целевой версии Hadoop</span><span class="sxs-lookup"><span data-stu-id="2fd7b-147"><a name="bPS1"></a>Target the Hadoop version</span></span>

<span data-ttu-id="2fd7b-148">В различных версиях HDInsight используются различные версии служб Hadoop и компонентов.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="2fd7b-149">Если сценарий предполагает наличие определенной версии службы или компонента, то такой сценарий следует использовать только с версией HDInsight, включающей необходимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-149">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span></span> <span data-ttu-id="2fd7b-150">Сведения о версиях компонентов, включенных в HDInsight, можно найти в документе [Версии компонентов HDInsight](hdinsight-component-versioning.md) .</span><span class="sxs-lookup"><span data-stu-id="2fd7b-150">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="2fd7b-151"><a name="bps10"></a> Выбор версии ОС</span><span class="sxs-lookup"><span data-stu-id="2fd7b-151"><a name="bps10"></a> Target the OS version</span></span>

<span data-ttu-id="2fd7b-152">HDInsight под управлением Linux основан на дистрибутиве Ubuntu под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-152">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span></span> <span data-ttu-id="2fd7b-153">Для разных версий HDInsight используются разные версии Ubuntu. Это может изменить поведение сценария.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="2fd7b-154">Например, HDInsight версии 3.4 и более ранних версий основан на версии Ubuntu, в которой используется Upstart.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="2fd7b-155">Версия 3.5 основана на Ubuntu версии 16.04, в которой используется Systemd.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="2fd7b-156">Systemd и Upstart используют разные команды, поэтому сценарий нужно написать таким образом, чтобы он был совместим и с тем, и с другим.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-156">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span></span>

<span data-ttu-id="2fd7b-157">Еще одно важное различие между HDInsight версии 3.4 и 3.5 заключается в том, что теперь `JAVA_HOME` указывает на Java 8.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span></span>

<span data-ttu-id="2fd7b-158">Чтобы проверить версию операционной системы, используйте `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-158">You can check the OS version by using `lsb_release`.</span></span> <span data-ttu-id="2fd7b-159">В следующем коде показано, как определить версию Ubuntu (14 или 16), в которой выполняется сценарий:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-159">The following code demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span></span>

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

<span data-ttu-id="2fd7b-160">Полный сценарий с этими фрагментами кода см. по адресу https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-160">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="2fd7b-161">Сведения о версии Ubuntu, используемой в HDInsight, см. в документе [HDInsight component version](hdinsight-component-versioning.md) (Версия компонента HDInsight).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-161">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="2fd7b-162">Сведения о различиях между Systemd и Upstart см. в статье [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers) (Systemd для пользователей Upstart).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-162">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="2fd7b-163"><a name="bPS2"></a>Предоставление стабильных ссылок на ресурсы сценария</span><span class="sxs-lookup"><span data-stu-id="2fd7b-163"><a name="bPS2"></a>Provide stable links to script resources</span></span>

<span data-ttu-id="2fd7b-164">Сценарии и связанные ресурсы должны оставаться доступными на протяжении жизненного цикла кластера.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-164">The script and associated resources must remain available throughout the lifetime of the cluster.</span></span> <span data-ttu-id="2fd7b-165">Эти ресурсы необходимы, если во время операций масштабирования в кластер добавляются новые узлы.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-165">These resources are required if new nodes are added to the cluster during scaling operations.</span></span>

<span data-ttu-id="2fd7b-166">Мы советуем скачивать и архивировать все данные в свою учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-166">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fd7b-167">Используемая учетная запись хранения должна быть учетной записью хранения по умолчанию для кластера или общедоступным и открытым только для чтения контейнером в другой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-167">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="2fd7b-168">К слову, примеры, предоставляемые корпорацией Майкрософт, хранятся в учетной записи хранения по адресу [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-168">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="2fd7b-169">Это открытый и доступный только для чтения контейнер, который поддерживает команда HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-169">This is a public, read-only container maintained by the HDInsight team.</span></span>

### <span data-ttu-id="2fd7b-170"><a name="bPS4"></a>Использование предварительно скомпилированных ресурсов</span><span class="sxs-lookup"><span data-stu-id="2fd7b-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="2fd7b-171">Чтобы сократить время выполнения сценария, избегайте операций, компилирующих ресурсы из исходного кода.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-171">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="2fd7b-172">Например, заранее скомпилируйте и сохраните ресурсы в BLOB-объекте учетной записи хранения Azure в том же центре обработки данных, что и кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-172">For example, pre-compile resources and store them in an Azure Storage account blob in the same data center as HDInsight.</span></span>

### <span data-ttu-id="2fd7b-173"><a name="bPS3"></a>Обеспечение идемпотентности сценария настройки кластера</span><span class="sxs-lookup"><span data-stu-id="2fd7b-173"><a name="bPS3"></a>Ensure that the cluster customization script is idempotent</span></span>

<span data-ttu-id="2fd7b-174">Сценарии должны быть идемпотентными.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-174">Scripts must be idempotent.</span></span> <span data-ttu-id="2fd7b-175">Имеется в виду, что при многократном выполнении в каждом случае сценарий должен обеспечивать возврат кластера к одному и тому же состоянию.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-175">If the script runs multiple times, it should return the cluster to the same state every time.</span></span>

<span data-ttu-id="2fd7b-176">Например, сценарий, который изменяет файлы конфигурации, не должен добавлять повторяющиеся записи в случае многократного выполнения.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="2fd7b-177"><a name="bPS5"></a>Обеспечение высокого уровня доступности кластера</span><span class="sxs-lookup"><span data-stu-id="2fd7b-177"><a name="bPS5"></a>Ensure high availability of the cluster architecture</span></span>

<span data-ttu-id="2fd7b-178">В кластерах HDInsight под управлением Linux есть два головных узла, активных в пределах кластера. Действия сценария выполняются на обоих узлах.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-178">Linux-based HDInsight clusters provide two head nodes that are active within the cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="2fd7b-179">Если устанавливаемым компонентам требуется только один головной узел, не устанавливайте компоненты не обоих головных узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-179">If the components you install expect only one head node, do not install the components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fd7b-180">Службы, устанавливаемые вместе с HDInsight, выполняют отработку отказа между двумя узлами.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-180">Services provided as part of HDInsight are designed to fail over between the two head nodes as needed.</span></span> <span data-ttu-id="2fd7b-181">Эта функциональность не распространяется на пользовательские компоненты, устанавливаемые при выполнении действий сценария.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-181">This functionality is not extended to custom components installed through script actions.</span></span> <span data-ttu-id="2fd7b-182">Если требуется высокий уровень доступности пользовательских компонентов, необходимо реализовать собственный механизм отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="2fd7b-183"><a name="bPS6"></a>Настройка пользовательских компонентов для использования хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="2fd7b-183"><a name="bPS6"></a>Configure the custom components to use Azure Blob storage</span></span>

<span data-ttu-id="2fd7b-184">Компоненты, устанавливаемые на кластере, могут по умолчанию использовать хранилище распределенной файловой системы Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-184">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="2fd7b-185">В качестве хранилища по умолчанию HDInsight использует хранилище Azure или Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-185">HDInsight uses either Azure Storage or Data Lake Store as the default storage.</span></span> <span data-ttu-id="2fd7b-186">Это обеспечивает совместимую с HDFS файловую систему, которая сохраняет данные даже после удаления кластера.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-186">Both provide an HDFS compatible file system that persists data even if the cluster is deleted.</span></span> <span data-ttu-id="2fd7b-187">Может потребоваться настроить устанавливаемые компоненты для использования WASB или ADL вместо HDFS.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-187">You may need to configure components you install to use WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="2fd7b-188">Для большинства операций не требуется указывать файловую систему.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-188">For most operations, you do not need to specify the file system.</span></span> <span data-ttu-id="2fd7b-189">Пример ниже копирует файл giraph-examples.jar из локальной файловой системы в хранилище кластера.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-189">For example, the following copies the giraph-examples.jar file from the local file system to cluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="2fd7b-190">В этом примере команда `hdfs` прозрачно использует хранилище кластера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-190">In this example, the `hdfs` command transparently uses the default cluster storage.</span></span> <span data-ttu-id="2fd7b-191">Для некоторых операций может потребоваться указать URI.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-191">For some operations, you may need to specify the URI.</span></span> <span data-ttu-id="2fd7b-192">Например, `adl:///example/jars` для Data Lake Store или `wasb:///example/jars` для хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="2fd7b-193"><a name="bPS7"></a>Запись информации в STDOUT и STDERR</span><span class="sxs-lookup"><span data-stu-id="2fd7b-193"><a name="bPS7"></a>Write information to STDOUT and STDERR</span></span>

<span data-ttu-id="2fd7b-194">HDInsight заносит в журнал выходные данные сценария, которые записываются в поток STDOUT и STDERR.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-194">HDInsight logs script output that is written to STDOUT and STDERR.</span></span> <span data-ttu-id="2fd7b-195">Эти данные можно просмотреть с помощью веб-интерфейса Ambari.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-195">You can view this information using the Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="2fd7b-196">Веб-интерфейс Ambari доступен только в том случае, если кластер успешно создан.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-196">Ambari is only available if the cluster is successfully created.</span></span> <span data-ttu-id="2fd7b-197">Если во время создания кластера используется действие сценария и создание завершается ошибкой, ознакомьтесь с другими способами доступа к данным журнала в разделе по устранению неполадок [Настройка кластеров HDInsight с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) .</span><span class="sxs-lookup"><span data-stu-id="2fd7b-197">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="2fd7b-198">Большинство программ и пакетов установки добавляют данные в STDOUT и STDERR по умолчанию, однако вам может потребоваться добавить дополнительные записи в журнал.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-198">Most utilities and installation packages already write information to STDOUT and STDERR, however you may want to add additional logging.</span></span> <span data-ttu-id="2fd7b-199">Для отправки текста в STDOUT используйте `echo`.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-199">To send text to STDOUT, use `echo`.</span></span> <span data-ttu-id="2fd7b-200">Например:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-200">For example:</span></span>

```bash
echo "Getting ready to install Foo"
```

<span data-ttu-id="2fd7b-201">По умолчанию ключевое слово `echo` отправляет строку в STDOUT.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-201">By default, `echo` sends the string to STDOUT.</span></span> <span data-ttu-id="2fd7b-202">Чтобы направить строку в STDERR, добавьте `>&2` перед `echo`.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-202">To direct it to STDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="2fd7b-203">Например:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="2fd7b-204">Информация, записываемая в STDOUT, перенаправляется STDERR (2).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-204">This redirects information written to STDOUT to STDERR (2) instead.</span></span> <span data-ttu-id="2fd7b-205">Дополнительные сведения о перенаправлении ввода-вывода см. на странице [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="2fd7b-206">Дополнительные сведения о просмотре журналов, созданных действиями сценариев, см. в статье [Настройка кластеров HDInsight с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="2fd7b-207"><a name="bps8"></a> Сохранение файлов в формате ASCII с использованием LF в качестве символа завершения строки</span><span class="sxs-lookup"><span data-stu-id="2fd7b-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="2fd7b-208">Сценарии Bash должны храниться в формате ASCII. Для завершения строк в этом файле используется символ LF.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="2fd7b-209">Если в файлах используется кодировка UTF-8 или используется CRLF в качестве конца строки, сценарий может завершиться следующей ошибкой:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-209">Files that are stored as UTF-8, or use CRLF as the line ending may fail with the following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="2fd7b-210"><a name="bps9"></a> Использование логики повтора для восстановления после временных ошибок</span><span class="sxs-lookup"><span data-stu-id="2fd7b-210"><a name="bps9"></a> Use retry logic to recover from transient errors</span></span>

<span data-ttu-id="2fd7b-211">При скачивании файлов, установке пакетов с помощью apt-get или других действиях, которые передают данные через Интернет, операция может завершиться ошибкой из-за временной ошибки сети.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-211">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span></span> <span data-ttu-id="2fd7b-212">Например, удаленный ресурс, с которым вы обмениваетесь данными, может находиться в процессе отработки отказа на резервный узел.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-212">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span></span>

<span data-ttu-id="2fd7b-213">Чтобы сделать свой сценарий устойчивым к временным ошибкам, можно реализовать логику повтора.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-213">To make your script resilient to transient errors, you can implement retry logic.</span></span> <span data-ttu-id="2fd7b-214">Приведенная ниже функция демонстрирует реализацию логику повтора.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-214">The following function demonstrates how to implement retry logic.</span></span> <span data-ttu-id="2fd7b-215">Она повторяет операцию три раза до сбоя.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-215">It retries the operation three times before failing.</span></span>

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

<span data-ttu-id="2fd7b-216">В следующих примерах показано, как использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-216">The following examples demonstrate how to use this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="2fd7b-217"><a name="helpermethods"></a>Вспомогательные методы для пользовательских сценариев</span><span class="sxs-lookup"><span data-stu-id="2fd7b-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="2fd7b-218">Вспомогательные методы действий сценариев — это служебные программы, которые можно использовать при создании пользовательских сценариев.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="2fd7b-219">Эти методы содержатся в сценарии [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="2fd7b-220">Чтобы скачать и использовать их как часть сценария, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-220">Use the following to download and use them as part of your script:</span></span>

```bash
# Import the helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="2fd7b-221">Эта команда открывает доступ к следующим вспомогательным приложениям, доступным для использования в сценарии:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-221">The following helpers available for use in your script:</span></span>

| <span data-ttu-id="2fd7b-222">Назначение вспомогательного приложения</span><span class="sxs-lookup"><span data-stu-id="2fd7b-222">Helper usage</span></span> | <span data-ttu-id="2fd7b-223">Описание</span><span class="sxs-lookup"><span data-stu-id="2fd7b-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="2fd7b-224">Скачивает файл из исходного универсального кода ресурса (URI) и сохраняет его в указанное расположение.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-224">Downloads a file from the source URI to the specified file path.</span></span> <span data-ttu-id="2fd7b-225">По умолчанию существующий файл не перезаписывается.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="2fd7b-226">Извлекает TAR-файл (с помощью `-xf`) в папку назначения.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-226">Extracts a tar file (using `-xf`) to the destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="2fd7b-227">При запуске на головном узле кластера возвращает значение 1, в противном случае — 0.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="2fd7b-228">Если текущий узел является узлом данных (рабочим узлом), то возвращается значение 1, в противном случае — 0.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-228">If the current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="2fd7b-229">Если текущий узел является первым узлом данных (рабочим узлом с именем workernode0), возвращается значение 1, в противном случае — 0.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-229">If the current node is the first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="2fd7b-230">Возвращает полное доменное имя головных узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-230">Return the fully qualified domain name of the headnodes in the cluster.</span></span> <span data-ttu-id="2fd7b-231">Имена содержат разделители-запятые.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-231">Names are comma delimited.</span></span> <span data-ttu-id="2fd7b-232">При возникновении ошибки возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="2fd7b-233">Возвращает полное доменное имя основного головного узла.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-233">Gets the fully qualified domain name of the primary headnode.</span></span> <span data-ttu-id="2fd7b-234">При возникновении ошибки возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="2fd7b-235">Возвращает полное доменное имя дополнительного головного узла.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-235">Gets the fully qualified domain name of the secondary headnode.</span></span> <span data-ttu-id="2fd7b-236">При возникновении ошибки возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="2fd7b-237">Возвращает числовой суффикс основного головного узла.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-237">Gets the numeric suffix of the primary headnode.</span></span> <span data-ttu-id="2fd7b-238">При возникновении ошибки возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="2fd7b-239">Возвращает числовой суффикс дополнительного головного узла.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-239">Gets the numeric suffix of the secondary headnode.</span></span> <span data-ttu-id="2fd7b-240">При возникновении ошибки возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="2fd7b-241"><a name="commonusage"></a>Общие варианты использования</span><span class="sxs-lookup"><span data-stu-id="2fd7b-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="2fd7b-242">В этом разделе содержится руководство по реализации некоторых общих вариантов использования, которые могут понадобиться при написании пользовательского сценария.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-242">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-to-a-script"></a><span data-ttu-id="2fd7b-243">Передача параметров в сценарий</span><span class="sxs-lookup"><span data-stu-id="2fd7b-243">Passing parameters to a script</span></span>

<span data-ttu-id="2fd7b-244">В некоторых случаях для сценария требуется указывать параметры.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="2fd7b-245">Например, при использовании интерфейса Ambari REST API может потребоваться пароль администратора кластера.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-245">For example, you may need the admin password for the cluster when using the Ambari REST API.</span></span>

<span data-ttu-id="2fd7b-246">Параметры, передаваемые в сценарий, называются *позиционными параметрами*, т. е. `$1` соответствует первому параметру, `$2` — второму и т.д.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-246">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span></span> <span data-ttu-id="2fd7b-247">Значение `$0` содержит имя самого сценария.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-247">`$0` contains the name of the script itself.</span></span>

<span data-ttu-id="2fd7b-248">Значения, передаваемые в сценарий в качестве параметров, должны быть заключены в одинарные кавычки (').</span><span class="sxs-lookup"><span data-stu-id="2fd7b-248">Values passed to the script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="2fd7b-249">В этом случае переданное значение рассматривается как литерал.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-249">Doing so ensures that the passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="2fd7b-250">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="2fd7b-250">Setting environment variables</span></span>

<span data-ttu-id="2fd7b-251">Настройка переменной среды выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-251">Setting an environment variable is performed by the following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="2fd7b-252">Где VARIABLENAME — имя переменной.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-252">Where VARIABLENAME is the name of the variable.</span></span> <span data-ttu-id="2fd7b-253">Для доступа к переменной используйте `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-253">To access the variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="2fd7b-254">Например, чтобы присвоить значение позиционного параметра переменной среды с именем PASSWORD, воспользуйтесь следующей инструкцией:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-254">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="2fd7b-255">Для последующего доступа к данным используйте `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-255">Subsequent access to the information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="2fd7b-256">Переменные среды, заданные в сценарии, существуют только в пределах области сценария.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-256">Environment variables set within the script only exist within the scope of the script.</span></span> <span data-ttu-id="2fd7b-257">В некоторых случаях может потребоваться добавить переменные среды, которые значимы на уровне системы и значение которых сохранится после выполнения сценария.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-257">In some cases, you may need to add system-wide environment variables that will persist after the script has finished.</span></span> <span data-ttu-id="2fd7b-258">Чтобы добавить переменные среды уровня системы, добавьте переменную в `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-258">To add system-wide environment variables, add the variable to `/etc/environment`.</span></span> <span data-ttu-id="2fd7b-259">Например, следующий оператор добавляет `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-259">For example, the following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="2fd7b-260">Доступ к расположениям, в которых хранятся пользовательские сценарии</span><span class="sxs-lookup"><span data-stu-id="2fd7b-260">Access to locations where the custom scripts are stored</span></span>

<span data-ttu-id="2fd7b-261">Сценарии, используемые для настройки кластера, должны храниться в одном из следующих расположений:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-261">Scripts used to customize a cluster needs to be stored in one of the following locations:</span></span>

* <span data-ttu-id="2fd7b-262">__учетной записи хранения Azure__, связанной с кластером;</span><span class="sxs-lookup"><span data-stu-id="2fd7b-262">An __Azure Storage account__ that is associated with the cluster.</span></span>

* <span data-ttu-id="2fd7b-263">__дополнительной учетной записи хранения__, связанной с кластером;</span><span class="sxs-lookup"><span data-stu-id="2fd7b-263">An __additional storage account__ associated with the cluster.</span></span>

* <span data-ttu-id="2fd7b-264">__ресурсе с общедоступным URI__.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-264">A __publicly readable URI__.</span></span> <span data-ttu-id="2fd7b-265">Например, URL-адрес к данным, хранящимся в OneDrive, Dropbox или других службах размещения файлов.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-265">For example, a URL to data stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="2fd7b-266">__учетной записи Azure Data Lake Store__, связанной с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-266">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span></span> <span data-ttu-id="2fd7b-267">Дополнительные сведения об использовании Azure Data Lake Store с HDInsight см. в статье [Создание кластера HDInsight с хранилищем озера данных с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="2fd7b-268">Кластер HDInsight субъекта-службы с доступом к Data Lake Store должен иметь доступ к сценарию с правами на чтение.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-268">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

<span data-ttu-id="2fd7b-269">Ресурсы, используемые сценарием, также должны быть общедоступными.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-269">Resources used by the script must also be publicly available.</span></span>

<span data-ttu-id="2fd7b-270">Сохранение файлов в учетной записи хранения Azure или Azure Data Lake Store поможет обеспечить быстрый доступ к файлам, так как оба хранилища находятся в сети Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-270">Storing the files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within the Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="2fd7b-271">Формат универсального кода ресурса (URI), используемый для ссылки на сценарий, отличается в зависимости от используемой службы.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-271">The URI format used to reference the script differs depending on the service being used.</span></span> <span data-ttu-id="2fd7b-272">Для учетной записи хранения, связанной с кластером HDInsight, используйте `wasb://` или `wasbs://`,</span><span class="sxs-lookup"><span data-stu-id="2fd7b-272">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="2fd7b-273">для общедоступного универсального кода ресурса (URI) — `http://` или `https://`,</span><span class="sxs-lookup"><span data-stu-id="2fd7b-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="2fd7b-274">а для Data Lake Store — `adl://`.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-the-operating-system-version"></a><span data-ttu-id="2fd7b-275">Проверка версии операционной системы</span><span class="sxs-lookup"><span data-stu-id="2fd7b-275">Checking the operating system version</span></span>

<span data-ttu-id="2fd7b-276">Для разных версий HDInsight используются конкретные версии Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="2fd7b-277">В сценарии следует проверить различия между версиями ОС.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="2fd7b-278">Например, может потребоваться установить двоичный файл, привязанный к версии Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-278">For example, you may need to install a binary that is tied to the version of Ubuntu.</span></span>

<span data-ttu-id="2fd7b-279">Чтобы проверить версию операционной системы, используйте `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-279">To check the OS version, use `lsb_release`.</span></span> <span data-ttu-id="2fd7b-280">Например, ниже показано, как создать ссылку на конкретный TAR-файл в зависимости от версии операционной системы:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-280">For example, the following script demonstrates how to reference a specific tar file depending on the OS version:</span></span>

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

## <span data-ttu-id="2fd7b-281"><a name="deployScript"></a>Контрольный список для развертывания действия сценария</span><span class="sxs-lookup"><span data-stu-id="2fd7b-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="2fd7b-282">Ниже приведены шаги, которые использовались при подготовке к развертыванию этих сценариев.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-282">Here are the steps we took when preparing to deploy these scripts:</span></span>

* <span data-ttu-id="2fd7b-283">Поместите файлы, содержащие пользовательские сценарии, в месте, доступном из узлов кластера во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-283">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="2fd7b-284">Например, в хранилище по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-284">For example, the default storage for the cluster.</span></span> <span data-ttu-id="2fd7b-285">Файлы также могут храниться в общедоступных службах размещения.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="2fd7b-286">Убедитесь, что сценарий является идемпотентным.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-286">Verify that the script is impotent.</span></span> <span data-ttu-id="2fd7b-287">Это обеспечит многократное выполнение сценария на одном узле.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-287">Doing so allows the script to be executed multiple times on the same node.</span></span>
* <span data-ttu-id="2fd7b-288">Используйте папку для временных файлов, например /tmp, чтобы хранить скачанные файлы, используемый сценариями. После выполнения сценариев очистите эту папку.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-288">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="2fd7b-289">В случае изменений параметров на уровне операционной системы или файлов конфигурации службы Hadoop может потребоваться перезапуск служб HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-289">If OS-level settings or Hadoop service configuration files are changed, you may want to restart HDInsight services.</span></span>

## <span data-ttu-id="2fd7b-290"><a name="runScriptAction"></a>Как запустить действие сценария</span><span class="sxs-lookup"><span data-stu-id="2fd7b-290"><a name="runScriptAction"></a>How to run a script action</span></span>

<span data-ttu-id="2fd7b-291">Действия сценариев можно использовать для настройки кластеров HDInsight с помощью следующих методов:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-291">You can use script actions to customize HDInsight clusters using the following methods:</span></span>

* <span data-ttu-id="2fd7b-292">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="2fd7b-292">Azure portal</span></span>
* <span data-ttu-id="2fd7b-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd7b-293">Azure PowerShell</span></span>
* <span data-ttu-id="2fd7b-294">Шаблоны диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="2fd7b-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="2fd7b-295">Пакет SDK для HDInsight .NET.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-295">The HDInsight .NET SDK.</span></span>

<span data-ttu-id="2fd7b-296">Дополнительные сведения об использовании каждого метода см. в разделе по [использованию действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-296">For more information on using each method, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="2fd7b-297"><a name="sampleScripts"></a>Примеры пользовательских сценариев</span><span class="sxs-lookup"><span data-stu-id="2fd7b-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="2fd7b-298">Корпорация Майкрософт предоставляет примеры сценариев для установки компонентов в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-298">Microsoft provides sample scripts to install components on an HDInsight cluster.</span></span> <span data-ttu-id="2fd7b-299">Дополнительные примеры действий сценариев доступны по приведенным ниже ссылкам.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-299">See the following links for more example script actions.</span></span>

* [<span data-ttu-id="2fd7b-300">Установка и использование Hue в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="2fd7b-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="2fd7b-301">Установка и использование Solr в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="2fd7b-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="2fd7b-302">Установка и использование Giraph в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="2fd7b-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="2fd7b-303">Установка и обновление Mono в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="2fd7b-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="2fd7b-304">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="2fd7b-304">Troubleshooting</span></span>

<span data-ttu-id="2fd7b-305">Ниже перечислены ошибки, которые могут возникнуть при использовании ваших сценариев.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-305">The following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="2fd7b-306">**Ошибка**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="2fd7b-307">Иногда дополняется фразой `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="2fd7b-308">*Причина.*Эта ошибка возникает, когда для завершения строк в сценарии используется символ CRLF.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-308">*Cause*: This error is caused when the lines in a script end with CRLF.</span></span> <span data-ttu-id="2fd7b-309">В системах UNIX для завершения строк допускается только символ LF.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-309">Unix systems expect only LF as the line ending.</span></span>

<span data-ttu-id="2fd7b-310">Зачастую эта проблема возникает при написании сценария в среде Windows, так как в текстовых редакторах для этой системы CRLF является стандартным символом завершения строки.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-310">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="2fd7b-311">*Решение.*Если в вашем текстовом редакторе имеется функция выбора формата Unix или использования символа LF для завершения строк, воспользуйтесь ею.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span></span> <span data-ttu-id="2fd7b-312">Кроме того, в системе Unix вы можете использовать следующие команды изменения CRLF на LF.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-312">You may also use the following commands on a Unix system to change the CRLF to an LF:</span></span>

> [!NOTE]
> <span data-ttu-id="2fd7b-313">Для замены символов CRLF на LF могут использоваться следующие аналогичные команды.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-313">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span></span> <span data-ttu-id="2fd7b-314">Выберите подходящий вариант в зависимости от наличия в системе соответствующих служебных программ.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-314">Select one based on the utilities available on your system.</span></span>

| <span data-ttu-id="2fd7b-315">Команда</span><span class="sxs-lookup"><span data-stu-id="2fd7b-315">Command</span></span> | <span data-ttu-id="2fd7b-316">Примечания</span><span class="sxs-lookup"><span data-stu-id="2fd7b-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="2fd7b-317">Для исходного файла будет создана резервная копия с расширением BAK.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-317">The original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="2fd7b-318">В файле OUTFILE для окончания строк будут использоваться только символы LF.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="2fd7b-319">Изменяет файл напрямую.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-319">Modifies the file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="2fd7b-320">В файле OUTFILE для окончания строк будут использоваться только символы LF.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="2fd7b-321">**Ошибка**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="2fd7b-322">*Причина.*Эта ошибка возникает, если сценарий сохранен в кодировке UTF-8 с меткой порядка байтов (BOM).</span><span class="sxs-lookup"><span data-stu-id="2fd7b-322">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="2fd7b-323">*Решение.*Сохраните файл в формате ASCII или UTF-8 без метки порядка байтов.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-323">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="2fd7b-324">Кроме того, для создания файла без метки порядка байтов в системе Linux или Unix вы можете использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2fd7b-324">You may also use the following command on a Linux or Unix system to create a file without the BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="2fd7b-325">Замените `INFILE` на файл с меткой порядка байтов.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-325">Replace `INFILE` with the file containing the BOM.</span></span> <span data-ttu-id="2fd7b-326">`OUTFILE` должно быть новым именем файла, который будет содержать сценарий без метки порядка байтов.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-326">`OUTFILE` should be a new file name, which contains the script without the BOM.</span></span>

## <span data-ttu-id="2fd7b-327"><a name="seeAlso"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2fd7b-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="2fd7b-328">Узнайте, как [Настройка кластеров HDInsight с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="2fd7b-328">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="2fd7b-329">Используйте [справочник по пакету SDK .NET для HDInsight](https://msdn.microsoft.com/library/mt271028.aspx) , чтобы узнать больше о создании приложений .NET, которые управляют HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-329">Use the [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) to learn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="2fd7b-330">Используйте [REST API HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) , чтобы узнать, как использовать REST для выполнения операций управления кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fd7b-330">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span></span>
