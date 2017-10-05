---
title: "Настройка кластеров HDInsight с помощью действий скрипта — Azure | Документы Майкрософт"
description: "Добавление настраиваемых компонентов в кластеры HDInsight на основе Linux с помощью действий скриптов. Действия скриптов — это скрипты Bash, которые можно использовать для настройки конфигурации кластера или добавления дополнительных служб и служебных программ, таких как Hue, Solr или R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 0c5d00b6cb9f68a1a0e474f81c969eb1b5654c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="65037-104">Настройка кластеров HDInsight под управлением Linux с помощью действия сценария</span><span class="sxs-lookup"><span data-stu-id="65037-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="65037-105">В кластерах HDInsight есть параметр конфигурации **Действие скрипта** , вызывающий пользовательские скрипты, с помощью которых можно настроить кластер.</span><span class="sxs-lookup"><span data-stu-id="65037-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize the cluster.</span></span> <span data-ttu-id="65037-106">Эти скрипты используются для установки дополнительных компонентов и изменения параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="65037-106">These scripts are used to install additional components and change configuration settings.</span></span> <span data-ttu-id="65037-107">Действия скрипта можно использовать во время или после создания кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65037-108">Использовать действия скриптов в уже работающем кластере можно только в кластерах HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="65037-108">The ability to use script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="65037-109">Linux — единственная операционная система, используемая для работы с HDInsight 3.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="65037-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="65037-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="65037-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="65037-111">Действия сценариев можно опубликовать в Azure Marketplace как приложение HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-111">Script actions can also be published to the Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="65037-112">В некоторых примерах в этом документе показано, как можно установить приложение HDInsight с помощью команд действия сценария PowerShell и пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="65037-112">Some of the examples in this document show how you can install an HDInsight application using script action commands from PowerShell and the .NET SDK.</span></span> <span data-ttu-id="65037-113">Дополнительные сведения о приложениях HDInsight см. в статье [Публикация приложений HDInsight в Azure Marketplace](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="65037-113">For more information on HDInsight applications, see [Publish HDInsight applications into the Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="65037-114">Разрешения</span><span class="sxs-lookup"><span data-stu-id="65037-114">Permissions</span></span>

<span data-ttu-id="65037-115">При использовании присоединенного к домену кластера HDInsight для выполнения действий скрипта необходимо задать два следующих расширения Ambari:</span><span class="sxs-lookup"><span data-stu-id="65037-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with the cluster:</span></span>

* <span data-ttu-id="65037-116">**AMBARI.RUN\_CUSTOM\_COMMAND.** Это разрешение по умолчанию назначено для роли администратора Ambari.</span><span class="sxs-lookup"><span data-stu-id="65037-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: The Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="65037-117">**CLUSTER.RUN\_CUSTOM\_COMMAND.** Это разрешение по умолчанию назначено для администратора кластера HDInsight и администратора Ambari.</span><span class="sxs-lookup"><span data-stu-id="65037-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both the HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="65037-118">Дополнительные сведения о работе с разрешениями в присоединенном к домену кластере HDInsight см. в статье [Управление присоединенными к домену кластерами HDInsight (предварительная версия)](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="65037-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="65037-119">управление доступом;</span><span class="sxs-lookup"><span data-stu-id="65037-119">Access control</span></span>

<span data-ttu-id="65037-120">Если вы не администратор или владелец подписки Azure, ваша учетная запись должна иметь доступ к группе ресурсов, содержащий кластер HDInsight, по крайней мере с правами **участника**.</span><span class="sxs-lookup"><span data-stu-id="65037-120">If you are not the administrator/owner of your Azure subscription, your account must have at least **Contributor** access to the resource group that contains the HDInsight cluster.</span></span>

<span data-ttu-id="65037-121">Кроме того, при создании кластера HDInsight другой пользователь, которому назначена по крайней мере роль **участника** в рамках подписки Azure, должен заранее зарегистрировать поставщика ресурсов для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access to the Azure subscription must have previously registered the provider for HDInsight.</span></span> <span data-ttu-id="65037-122">Поставщик регистрируется тогда, когда пользователь с правами участника подписки впервые создает ресурс в подписке.</span><span class="sxs-lookup"><span data-stu-id="65037-122">Provider registration happens when a user with Contributor access to the subscription creates a resource for the first time on the subscription.</span></span> <span data-ttu-id="65037-123">Регистрацию также можно выполнить без создания ресурса [с помощью REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="65037-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="65037-124">Дополнительные сведения о работе с управлением доступом см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="65037-124">For more information on working with access management, see the following documents:</span></span>

* [<span data-ttu-id="65037-125">Начало работы с управлением доступом на портале Azure</span><span class="sxs-lookup"><span data-stu-id="65037-125">Get started with access management in the Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="65037-126">Использование назначений ролей для управления доступом к ресурсам в подписке Azure</span><span class="sxs-lookup"><span data-stu-id="65037-126">Use role assignments to manage access to your Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="65037-127">Что такое действия скриптов</span><span class="sxs-lookup"><span data-stu-id="65037-127">Understanding Script Actions</span></span>

<span data-ttu-id="65037-128">Действие скрипта — это просто скрипт Bash, в который вы вводите универсальный код ресурса (URI) и для которого вы указываете параметры.</span><span class="sxs-lookup"><span data-stu-id="65037-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="65037-129">Скрипт выполняется на узлах в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-129">The script runs on nodes in the HDInsight cluster.</span></span> <span data-ttu-id="65037-130">Ниже приведены характеристики и возможности действий скриптов.</span><span class="sxs-lookup"><span data-stu-id="65037-130">The following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="65037-131">Они должны храниться в URI, доступном из кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-131">Must be stored on a URI that is accessible from the HDInsight cluster.</span></span> <span data-ttu-id="65037-132">Возможные места хранения:</span><span class="sxs-lookup"><span data-stu-id="65037-132">The following are possible storage locations:</span></span>

    * <span data-ttu-id="65037-133">**учетная запись Azure Data Lake Store**, доступная из кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-133">An **Azure Data Lake Store** account that is accessible by the HDInsight cluster.</span></span> <span data-ttu-id="65037-134">Дополнительные сведения об использовании Azure Data Lake Store с HDInsight см. в статье [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="65037-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="65037-135">Если скрипт находится в Data Lake Store, универсальный код ресурса (URI) имеет следующий формат: `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="65037-135">When using a script stored in Data Lake Store, the URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="65037-136">Кластер HDInsight субъекта-службы с доступом к Data Lake Store должен иметь доступ на чтение к скрипту.</span><span class="sxs-lookup"><span data-stu-id="65037-136">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

    * <span data-ttu-id="65037-137">Большой двоичный объект в **учетной записи хранения Azure**, которая служит основной или дополнительной учетной записью хранения для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-137">A blob in an **Azure Storage account** that is either the primary or additional storage account for the HDInsight cluster.</span></span> <span data-ttu-id="65037-138">При создании кластера HDInsight получает доступ к обоим типам учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="65037-138">HDInsight is granted access to both of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="65037-139">Служба совместного доступа к файлам, например хранилище BLOB-объектов Azure, GitHub, OneDrive, Dropbox и т. д.</span><span class="sxs-lookup"><span data-stu-id="65037-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="65037-140">Примеры универсальных кодов ресурсов (URI) см. в разделе [Пример действий сценария](#example-script-action-scripts).</span><span class="sxs-lookup"><span data-stu-id="65037-140">For example URIs, see the [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="65037-141">HDInsight поддерживает только учетные записи хранения Azure __общего назначения__.</span><span class="sxs-lookup"><span data-stu-id="65037-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="65037-142">Учетные записи __хранилища BLOB-объектов__ сейчас не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="65037-142">It does not currently support the __Blob storage__ account type.</span></span>

* <span data-ttu-id="65037-143">Действия скрипта могут быть ограничены **запуском только на узлах определенного типа**, например головных или рабочих.</span><span class="sxs-lookup"><span data-stu-id="65037-143">Can be restricted to **run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="65037-144">При использовании HDInsight уровня "Премиум" можно указать использование сценария на граничном узле.</span><span class="sxs-lookup"><span data-stu-id="65037-144">When used with HDInsight Premium, you can specify that the script should be used on the edge node.</span></span>

* <span data-ttu-id="65037-145">Действия скрипта могут быть **сохраняемыми** или **специализированными**.</span><span class="sxs-lookup"><span data-stu-id="65037-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="65037-146">**Сохраняемые** — это скрипты, которые применяются на рабочих узлах, добавленных в кластер после выполнения скрипта,</span><span class="sxs-lookup"><span data-stu-id="65037-146">**Persisted** scripts are applied to worker nodes added to the cluster after the script runs.</span></span> <span data-ttu-id="65037-147">например при масштабировании кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-147">For example, when scaling up the cluster.</span></span>

    <span data-ttu-id="65037-148">Сохраняемый скрипт может также применять изменения к узлу другого типа, например головному.</span><span class="sxs-lookup"><span data-stu-id="65037-148">A persisted script might also apply changes to another node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="65037-149">Действия сохраняемых скриптов должны иметь уникальные имена.</span><span class="sxs-lookup"><span data-stu-id="65037-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="65037-150">**Специализированные** скрипты не сохраняются.</span><span class="sxs-lookup"><span data-stu-id="65037-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="65037-151">Они не применяются на рабочих узлах, добавленных в кластер после выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="65037-151">They are not applied to worker nodes added to the cluster after the script has ran.</span></span> <span data-ttu-id="65037-152">Специализированный скрипт можно впоследствии сделать сохраняемым (и наоборот).</span><span class="sxs-lookup"><span data-stu-id="65037-152">You can subsequently promote an ad hoc script to a persisted script, or demote a persisted script to an ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="65037-153">Действия скриптов, используемые при создании кластера, автоматически сохраняются.</span><span class="sxs-lookup"><span data-stu-id="65037-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="65037-154">Скрипты, в которых произошла ошибка, не сохраняются, даже если вы отдельно указали, что они должны быть сохранены.</span><span class="sxs-lookup"><span data-stu-id="65037-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="65037-155">Действия скрипта могут принимать **параметры**, используемые в процессе выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="65037-155">Can accept **parameters** that are used by the script during execution.</span></span>
* <span data-ttu-id="65037-156">Они выполняются с помощью **прав привилегированного пользователя** на узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-156">Run with **root level privileges** on the cluster nodes.</span></span>
* <span data-ttu-id="65037-157">Действия скрипта могут выполняться с помощью **портала Azure**, **Azure PowerShell**, **интерфейса командной строки Azure** или **пакета SDK HDInsight для .NET**.</span><span class="sxs-lookup"><span data-stu-id="65037-157">Can be used through the **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="65037-158">В кластере ведется журнал всех скриптов, которые в нем выполнялись.</span><span class="sxs-lookup"><span data-stu-id="65037-158">The cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="65037-159">Это позволяет определить идентификатор скрипта для операции изменения типа.</span><span class="sxs-lookup"><span data-stu-id="65037-159">The history is useful when you need to find the ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65037-160">Не существует способа автоматической отмены изменений, внесенных действием скрипта.</span><span class="sxs-lookup"><span data-stu-id="65037-160">There is no automatic way to undo the changes made by a script action.</span></span> <span data-ttu-id="65037-161">Отмените изменения вручную или предоставьте скрипт для их отмены.</span><span class="sxs-lookup"><span data-stu-id="65037-161">Either manually reverse the changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="65037-162">Действие сценария в процессе создания кластера</span><span class="sxs-lookup"><span data-stu-id="65037-162">Script Action in the cluster creation process</span></span>

<span data-ttu-id="65037-163">Действия скриптов, используемые в процессе создания кластера и выполняющиеся в существующем кластере, несколько отличаются:</span><span class="sxs-lookup"><span data-stu-id="65037-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="65037-164">Скрипт **сохраняется автоматически**.</span><span class="sxs-lookup"><span data-stu-id="65037-164">The script is **automatically persisted**.</span></span>
* <span data-ttu-id="65037-165">**Ошибка** в скрипте может вызвать сбой создания кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-165">A **failure** in the script can cause the cluster creation process to fail.</span></span>

<span data-ttu-id="65037-166">На следующей схеме показано, когда выполняется действие сценария в процессе создания.</span><span class="sxs-lookup"><span data-stu-id="65037-166">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="65037-167">![Настройка кластера HDInsight и этапы создания кластера][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="65037-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="65037-168">Скрипт выполняется во время настройки HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-168">The script runs while HDInsight is being configured.</span></span> <span data-ttu-id="65037-169">На этом этапе скрипт выполняется параллельно на всех указанных узлах кластера с правами привилегированного пользователя на узлах.</span><span class="sxs-lookup"><span data-stu-id="65037-169">At this stage, the script runs in parallel on all the specified nodes in the cluster, and runs with root privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="65037-170">Так как при выполнении скрипта у вас есть права привилегированного пользователя на узлах кластера, вы можете выполнять такие операции, как остановка и запуск служб, включая службы, связанные с Hadoop.</span><span class="sxs-lookup"><span data-stu-id="65037-170">Because the script runs with root level privilege on the cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="65037-171">Если вы останавливаете службы, перед завершением работы сценария необходимо запустить службу Ambari и другие службы, связанные с Hadoop.</span><span class="sxs-lookup"><span data-stu-id="65037-171">If you stop services, you must ensure that the Ambari service and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="65037-172">Эти службы нужны для определения работоспособности и состояния кластера при его создании.</span><span class="sxs-lookup"><span data-stu-id="65037-172">These services are required to successfully determine the health and state of the cluster while it is being created.</span></span>


<span data-ttu-id="65037-173">При создании кластера можно использовать несколько действий скриптов одновременно.</span><span class="sxs-lookup"><span data-stu-id="65037-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="65037-174">Они будут вызываться в том порядке, в котором были указаны.</span><span class="sxs-lookup"><span data-stu-id="65037-174">These scripts are invoked in the order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65037-175">Действия сценария должны быть завершены в течение 60 минут. В противном случае возникнет ошибка времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="65037-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="65037-176">В процессе подготовки кластера скрипт запускается одновременно с другими процессами установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="65037-176">During cluster provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="65037-177">Конкуренция за ресурсы, такие как ЦП или пропускная способность сети, может привести к затягиванию выполнения сценария по сравнению со временем его выполнения в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="65037-177">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>
>
> <span data-ttu-id="65037-178">Чтобы свести время выполнения сценария к минимуму, избегайте таких задач, как скачивание и компиляция приложений из исходного кода.</span><span class="sxs-lookup"><span data-stu-id="65037-178">To minimize the time it takes to run the script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="65037-179">Выполните предварительную компиляцию приложения и сохраните двоичный файл в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="65037-179">Pre-compile applications and store the binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="65037-180">Действие скрипта в работающем кластере</span><span class="sxs-lookup"><span data-stu-id="65037-180">Script action on a running cluster</span></span>

<span data-ttu-id="65037-181">В отличие от действий скриптов, используемых во время создания кластера, ошибка в выполняющемся скрипте в работающем кластере не приводит автоматически к сбою в работе кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause the cluster to change to a failed state.</span></span> <span data-ttu-id="65037-182">После завершения скрипта кластер должен вернуться в рабочее состояние.</span><span class="sxs-lookup"><span data-stu-id="65037-182">Once a script completes, the cluster should return to a "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65037-183">Даже если кластер запущен, ошибка скрипта может привести к проблемам.</span><span class="sxs-lookup"><span data-stu-id="65037-183">Even if the cluster has a 'running' state, the failed script may have broken things.</span></span> <span data-ttu-id="65037-184">К примеру, скрипт может удалить необходимые для работы кластера файлы.</span><span class="sxs-lookup"><span data-stu-id="65037-184">For example, a script could delete files needed by the cluster.</span></span>
>
> <span data-ttu-id="65037-185">Действия скриптов выполняются с использованием привилегий корневой учетной записи, поэтому вы должны понимать, что делает скрипт, прежде чем применять его в кластере.</span><span class="sxs-lookup"><span data-stu-id="65037-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it to your cluster.</span></span>

<span data-ttu-id="65037-186">Когда сценарий применяется в кластере, состояние кластера изменяется с **Работает** на **Принято**, затем на **Конфигурация HDInsight** и снова на **Работает**, если выполнение сценария завершается успешно.</span><span class="sxs-lookup"><span data-stu-id="65037-186">When applying a script to a cluster, the cluster state changes to from **Running** to **Accepted**, then **HDInsight configuration**, and finally back to **Running** for successful scripts.</span></span> <span data-ttu-id="65037-187">Так как состояние скрипта регистрируется в журнале действий скриптов, вы можете определить успешность его выполнения.</span><span class="sxs-lookup"><span data-stu-id="65037-187">The script status is logged in the script action history, and you can use this information to determine whether the script succeeded or failed.</span></span> <span data-ttu-id="65037-188">Например, командлет PowerShell `Get-AzureRmHDInsightScriptActionHistory` можно использовать для просмотра состояния сценария.</span><span class="sxs-lookup"><span data-stu-id="65037-188">For example, the `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used to view the status of a script.</span></span> <span data-ttu-id="65037-189">Эта команда возвращает следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="65037-189">It returns information similar to the following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="65037-190">Если вы изменили пароль пользователя (администратора) кластера после создания кластера, может происходить сбой при выполнении действий скриптов для этого кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-190">If you have changed the cluster user (admin) password after the cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="65037-191">Если у вас есть сохраненные действия скриптов, нацеленные на рабочие узлы, они могут завершиться ошибкой при масштабировании кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale the cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="65037-192">Пример действий сценария</span><span class="sxs-lookup"><span data-stu-id="65037-192">Example Script Action scripts</span></span>

<span data-ttu-id="65037-193">Действия скриптов можно использовать с помощью следующих служебных средств:</span><span class="sxs-lookup"><span data-stu-id="65037-193">Script Action scripts can be used through the following utilities:</span></span>

* <span data-ttu-id="65037-194">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="65037-194">Azure portal</span></span>
* <span data-ttu-id="65037-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="65037-195">Azure PowerShell</span></span>
* <span data-ttu-id="65037-196">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="65037-196">Azure CLI</span></span>
* <span data-ttu-id="65037-197">Пакет SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="65037-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="65037-198">В HDInsight доступны скрипты для установки следующих компонентов в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-198">HDInsight provides scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="65037-199">Имя</span><span class="sxs-lookup"><span data-stu-id="65037-199">Name</span></span> | <span data-ttu-id="65037-200">Скрипт</span><span class="sxs-lookup"><span data-stu-id="65037-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="65037-201">**Добавление учетной записи хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="65037-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="65037-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Ознакомьтесь со статьей [Добавление дополнительных учетных записей хранения Azure в HDInsight](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="65037-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="65037-203">**Установка Hue**</span><span class="sxs-lookup"><span data-stu-id="65037-203">**Install Hue**</span></span> |<span data-ttu-id="65037-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. См. статью [Установка и использование Hue на кластерах HDInsight Hadoop](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="65037-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="65037-205">**Установка Presto**</span><span class="sxs-lookup"><span data-stu-id="65037-205">**Install Presto**</span></span> |<span data-ttu-id="65037-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. См. статью [Установка и использование Presto в кластерах HDInsight](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="65037-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="65037-207">**Установка Solr**</span><span class="sxs-lookup"><span data-stu-id="65037-207">**Install Solr**</span></span> |<span data-ttu-id="65037-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Ознакомьтесь со статьей [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="65037-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="65037-209">**Установка Giraph**</span><span class="sxs-lookup"><span data-stu-id="65037-209">**Install Giraph**</span></span> |<span data-ttu-id="65037-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Ознакомьтесь со статьей [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="65037-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="65037-211">**Предварительная загрузка библиотек Hive**</span><span class="sxs-lookup"><span data-stu-id="65037-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="65037-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. См статью [Добавление библиотек Hive в кластеры HDInsight](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="65037-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="65037-213">**Установка или обновление Mono**</span><span class="sxs-lookup"><span data-stu-id="65037-213">**Install or update Mono**</span></span> | <span data-ttu-id="65037-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash</span><span class="sxs-lookup"><span data-stu-id="65037-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="65037-215">См. статью [Установка или обновление Mono в HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="65037-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="65037-216">Использование действия скрипта при создании кластера</span><span class="sxs-lookup"><span data-stu-id="65037-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="65037-217">В этом разделе приведены примеры различных способов использования действий скриптов при создании кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-217">This section provides examples on the different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-azure-portal"></a><span data-ttu-id="65037-218">Использование действия сценария при создании кластера с портала Azure</span><span class="sxs-lookup"><span data-stu-id="65037-218">Use a Script Action during cluster creation from the Azure portal</span></span>

1. <span data-ttu-id="65037-219">Начните создание кластера, как описано в разделе [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="65037-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="65037-220">Остановитесь, когда откроется колонка __Сводка по кластерам__.</span><span class="sxs-lookup"><span data-stu-id="65037-220">Stop when you reach the __Cluster summary__ section.</span></span>

2. <span data-ttu-id="65037-221">В колонке __Сводка по кластерам__ щелкните ссылку __Изменить__ для элемента __Дополнительные параметры__.</span><span class="sxs-lookup"><span data-stu-id="65037-221">From the __Cluster summary__ section, select the __edit__ link for __Advanced settings__.</span></span>

    ![Ссылка "Дополнительные параметры"](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="65037-223">В колонке __Дополнительные параметры__ выберите __Действия скрипта__.</span><span class="sxs-lookup"><span data-stu-id="65037-223">From the __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="65037-224">В колонке __Действия скрипта__ выберите __+Отправить новое__.</span><span class="sxs-lookup"><span data-stu-id="65037-224">From the __Script actions__ section, select __+ Submit new__</span></span>

    ![Отправка нового действия скрипта](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="65037-226">Используйте запись __Выберите скрипт__, чтобы выбрать готовый скрипт.</span><span class="sxs-lookup"><span data-stu-id="65037-226">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="65037-227">Чтобы использовать пользовательский скрипт, выберите запись __Пользовательский__, а затем укажите __имя__ и код __URI bash-скрипта__.</span><span class="sxs-lookup"><span data-stu-id="65037-227">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Добавление скрипта в форме выбора скрипта](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="65037-229">В приведенной ниже таблице описываются элементы формы.</span><span class="sxs-lookup"><span data-stu-id="65037-229">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="65037-230">Свойство</span><span class="sxs-lookup"><span data-stu-id="65037-230">Property</span></span> | <span data-ttu-id="65037-231">Значение</span><span class="sxs-lookup"><span data-stu-id="65037-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="65037-232">Выберите скрипт</span><span class="sxs-lookup"><span data-stu-id="65037-232">Select a script</span></span> | <span data-ttu-id="65037-233">Чтобы использовать собственный скрипт, выберите __Настраиваемый__.</span><span class="sxs-lookup"><span data-stu-id="65037-233">To use your own script, select __Custom__.</span></span> <span data-ttu-id="65037-234">В противном случае выберите один из предоставленных скриптов.</span><span class="sxs-lookup"><span data-stu-id="65037-234">Otherwise, select one of the provided scripts.</span></span> |
    | <span data-ttu-id="65037-235">Имя</span><span class="sxs-lookup"><span data-stu-id="65037-235">Name</span></span> |<span data-ttu-id="65037-236">Укажите имя для действия сценария.</span><span class="sxs-lookup"><span data-stu-id="65037-236">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="65037-237">URI bash-скрипта</span><span class="sxs-lookup"><span data-stu-id="65037-237">Bash script URI</span></span> |<span data-ttu-id="65037-238">Укажите URI для сценария, который вызывается для настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-238">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="65037-239">Головной, рабочий или Zookeeper</span><span class="sxs-lookup"><span data-stu-id="65037-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="65037-240">Укажите узлы (**головной**, **рабочий** или **ZooKeeper**), на которых выполняется скрипт настройки.</span><span class="sxs-lookup"><span data-stu-id="65037-240">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="65037-241">Параметры</span><span class="sxs-lookup"><span data-stu-id="65037-241">Parameters</span></span> |<span data-ttu-id="65037-242">Укажите параметры, если они требуются для сценария.</span><span class="sxs-lookup"><span data-stu-id="65037-242">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="65037-243">Используйте запись __Сохранить это действие скрипта__, чтобы скрипт применялся при масштабировании.</span><span class="sxs-lookup"><span data-stu-id="65037-243">Use the __Persist this script action__ entry to ensure that the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="65037-244">Чтобы сохранить скрипт, нажмите кнопку __Создать__.</span><span class="sxs-lookup"><span data-stu-id="65037-244">Select __Create__ to save the script.</span></span> <span data-ttu-id="65037-245">Чтобы добавить еще один скрипт, можно использовать элемент __+ Отправить новый__.</span><span class="sxs-lookup"><span data-stu-id="65037-245">You can then use __+ Submit new__ to add another script.</span></span>

    ![Несколько действий скриптов](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="65037-247">Завершив добавление скриптов, нажмите кнопку __Выбрать__, а затем — кнопку __Далее__, чтобы вернуться в раздел __Сводка по кластерам__.</span><span class="sxs-lookup"><span data-stu-id="65037-247">When you are done adding scripts, use the __Select__ button, and then the __Next__ button to return to the __Cluster summary__ section.</span></span>

3. <span data-ttu-id="65037-248">Чтобы создать кластер, в разделе __Сводка по кластерам__ нажмите __Создать__.</span><span class="sxs-lookup"><span data-stu-id="65037-248">To create the cluster, select __Create__ from the __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="65037-249">Использование действия сценария на основе шаблонов диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="65037-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="65037-250">Примеры в этом разделе демонстрируют использование действий скриптов с шаблонами Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65037-250">The examples in this section demonstrate how to use script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="65037-251">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="65037-251">Before you begin</span></span>

* <span data-ttu-id="65037-252">Сведения о настройке рабочей станции для запуска командлетов HDInsight PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65037-252">For information about configuring a workstation to run HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="65037-253">Инструкции по созданию шаблонов см. в статье [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) (Создание шаблонов Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="65037-253">For instructions on how to create templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="65037-254">Сведения об использовании Azure PowerShell с Resource Manager см. в [этой статье](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="65037-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="65037-255">Создание кластеров с помощью действия скрипта</span><span class="sxs-lookup"><span data-stu-id="65037-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="65037-256">Скопируйте следующий шаблон в папку на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="65037-256">Copy the following template to a location on your computer.</span></span> <span data-ttu-id="65037-257">Он устанавливает Giraph на головные и рабочие узлы в кластере.</span><span class="sxs-lookup"><span data-stu-id="65037-257">This template installs Giraph on the headnodes and worker nodes in the cluster.</span></span> <span data-ttu-id="65037-258">Чтобы убедиться, что шаблон JSON является допустимым,</span><span class="sxs-lookup"><span data-stu-id="65037-258">You can also verify if the JSON template is valid.</span></span> <span data-ttu-id="65037-259">Вставьте содержимое шаблона в [JSONLint](http://jsonlint.com/) — интерактивное средство проверки JSON.</span><span class="sxs-lookup"><span data-stu-id="65037-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="65037-260">Запустите Azure PowerShell и войдите в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="65037-260">Start Azure PowerShell and Log in to your Azure account.</span></span> <span data-ttu-id="65037-261">После предоставления учетных данных команда возвращает информацию о вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="65037-261">After providing your credentials, the command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="65037-262">Если у вас несколько подписок, укажите подписку, которую вы хотите использовать для развертывания.</span><span class="sxs-lookup"><span data-stu-id="65037-262">If you have multiple subscriptions, provide the subscription ID you wish to use for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="65037-263">Используйте `Get-AzureRmSubscription` для получения списка всех подписок, связанных с вашей учетной записью, в котором указан идентификатор каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="65037-263">You can use `Get-AzureRmSubscription` to get a list of all subscriptions associated with your account, which includes the subscription ID for each one.</span></span>

4. <span data-ttu-id="65037-264">Создайте группу ресурсов, если у вас нет существующей группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="65037-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="65037-265">Введите имя группы ресурсов и расположение, необходимое для решения.</span><span class="sxs-lookup"><span data-stu-id="65037-265">Provide the name of the resource group and location that you need for your solution.</span></span> <span data-ttu-id="65037-266">Появится сводка по новой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="65037-266">A summary of the new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="65037-267">Чтобы создать развертывание для группы ресурсов, выполните командлет **New-AzureRmResourceGroupDeployment** и укажите необходимые параметры.</span><span class="sxs-lookup"><span data-stu-id="65037-267">To create a deployment for your resource group, run the **New-AzureRmResourceGroupDeployment** command and provide the necessary parameters.</span></span> <span data-ttu-id="65037-268">Параметры включают следующие данные:</span><span class="sxs-lookup"><span data-stu-id="65037-268">The parameters include the following data:</span></span>

    * <span data-ttu-id="65037-269">имя развертывания;</span><span class="sxs-lookup"><span data-stu-id="65037-269">A name for your deployment</span></span>
    * <span data-ttu-id="65037-270">имя группы ресурсов;</span><span class="sxs-lookup"><span data-stu-id="65037-270">The name of your resource group</span></span>
    * <span data-ttu-id="65037-271">путь или URL-адрес к созданному шаблону.</span><span class="sxs-lookup"><span data-stu-id="65037-271">The path or URL to the template you created.</span></span>

  <span data-ttu-id="65037-272">Если для вашего шаблона требуются какие-либо параметры, необходимо также передать их.</span><span class="sxs-lookup"><span data-stu-id="65037-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="65037-273">В данном случае для действия сценария по установке R в кластере никакие параметры не требуются.</span><span class="sxs-lookup"><span data-stu-id="65037-273">In this case, the script action to install R on the cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="65037-274">Появится запрос на задание значений параметров, определенных в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="65037-274">You are prompted to provide values for the parameters defined in the template.</span></span>

1. <span data-ttu-id="65037-275">После развертывания группы ресурсов вы увидите сводку по развертыванию.</span><span class="sxs-lookup"><span data-stu-id="65037-275">When the resource group has been deployed, a summary of the deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="65037-276">Если развертывание завершается сбоем, вы можете использовать следующие командлеты для получения информации об ошибках.</span><span class="sxs-lookup"><span data-stu-id="65037-276">If your deployment fails, you can use the following cmdlets to get information about the failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="65037-277">Использование действия скрипта при создании кластера с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="65037-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="65037-278">В этом разделе мы используем командлет [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx), чтобы вызвать скрипты с помощью действия скрипта для настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-278">In this section, we use the [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet to invoke scripts by using Script Action to customize a cluster.</span></span> <span data-ttu-id="65037-279">Прежде чем продолжить, убедитесь, что вы установили и настроили Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65037-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="65037-280">Сведения о настройке рабочей станции для запуска командлетов HDInsight PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65037-280">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="65037-281">Следующий скрипт демонстрирует применение действия скрипта при создании кластера с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="65037-281">The following script demonstrates how to apply a script action when creating a cluster using PowerShell:</span></span>

<span data-ttu-id="65037-282">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span><span class="sxs-lookup"><span data-stu-id="65037-282">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span></span>

<span data-ttu-id="65037-283">Создание кластера может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="65037-283">It can take several minutes before the cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-hdinsight-net-sdk"></a><span data-ttu-id="65037-284">Использование действия скрипта при создании кластера с помощью пакета SDK HDInsight для .NET</span><span class="sxs-lookup"><span data-stu-id="65037-284">Use a Script Action during cluster creation from the HDInsight .NET SDK</span></span>

<span data-ttu-id="65037-285">Пакет SDK HDInsight для .NET предоставляет клиентские библиотеки, которые упрощают работу с кластерами HDInsight из приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="65037-285">The HDInsight .NET SDK provides client libraries that makes it easier to work with HDInsight from a .NET application.</span></span> <span data-ttu-id="65037-286">Пример кода см. в статье [Создание кластеров под управлением Linux в HDInsight с помощью пакета SDK для .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="65037-286">For a code sample, see [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-to-a-running-cluster"></a><span data-ttu-id="65037-287">Применение действия скрипта в работающем кластере</span><span class="sxs-lookup"><span data-stu-id="65037-287">Apply a Script Action to a running cluster</span></span>

<span data-ttu-id="65037-288">В этом разделе вы узнаете, как применять действия скриптов к работающему кластеру.</span><span class="sxs-lookup"><span data-stu-id="65037-288">In this section, learn how to apply script actions to a running cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-portal"></a><span data-ttu-id="65037-289">Применение действия сценария в работающем кластере с портала Azure</span><span class="sxs-lookup"><span data-stu-id="65037-289">Apply a Script Action to a running cluster from the Azure portal</span></span>

1. <span data-ttu-id="65037-290">На [портале Azure](https://portal.azure.com)выберите свой кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-290">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="65037-291">В представлении кластера HDInsight выберите плитку **Действия скрипта**.</span><span class="sxs-lookup"><span data-stu-id="65037-291">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Элемент "Действия сценариев"](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="65037-293">Кроме того, можно щелкнуть **Все параметры**, а затем выбрать **Действия скрипта** в разделе "Параметры".</span><span class="sxs-lookup"><span data-stu-id="65037-293">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

3. <span data-ttu-id="65037-294">В верхней части раздела "Действия скрипта" выберите **+Отправить новое**.</span><span class="sxs-lookup"><span data-stu-id="65037-294">From the top of the Script Actions section, select **Submit new**.</span></span>

    ![Добавление скрипта в работающий кластер](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="65037-296">Используйте запись __Выберите скрипт__, чтобы выбрать готовый скрипт.</span><span class="sxs-lookup"><span data-stu-id="65037-296">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="65037-297">Чтобы использовать пользовательский скрипт, выберите запись __Пользовательский__, а затем укажите __имя__ и код __URI bash-скрипта__.</span><span class="sxs-lookup"><span data-stu-id="65037-297">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Добавление скрипта в форме выбора скрипта](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="65037-299">В приведенной ниже таблице описываются элементы формы.</span><span class="sxs-lookup"><span data-stu-id="65037-299">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="65037-300">Свойство</span><span class="sxs-lookup"><span data-stu-id="65037-300">Property</span></span> | <span data-ttu-id="65037-301">Значение</span><span class="sxs-lookup"><span data-stu-id="65037-301">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="65037-302">Выберите скрипт</span><span class="sxs-lookup"><span data-stu-id="65037-302">Select a script</span></span> | <span data-ttu-id="65037-303">Чтобы использовать собственный скрипт, выберите __Настраиваемый__.</span><span class="sxs-lookup"><span data-stu-id="65037-303">To use your own script, select __custom__.</span></span> <span data-ttu-id="65037-304">В противном случае выберите предоставленный скрипт.</span><span class="sxs-lookup"><span data-stu-id="65037-304">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="65037-305">Имя</span><span class="sxs-lookup"><span data-stu-id="65037-305">Name</span></span> |<span data-ttu-id="65037-306">Укажите имя для действия сценария.</span><span class="sxs-lookup"><span data-stu-id="65037-306">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="65037-307">URI bash-скрипта</span><span class="sxs-lookup"><span data-stu-id="65037-307">Bash script URI</span></span> |<span data-ttu-id="65037-308">Укажите URI для сценария, который вызывается для настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-308">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="65037-309">Головной, рабочий или Zookeeper</span><span class="sxs-lookup"><span data-stu-id="65037-309">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="65037-310">Укажите узлы (**головной**, **рабочий** или **ZooKeeper**), на которых выполняется скрипт настройки.</span><span class="sxs-lookup"><span data-stu-id="65037-310">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="65037-311">Параметры</span><span class="sxs-lookup"><span data-stu-id="65037-311">Parameters</span></span> |<span data-ttu-id="65037-312">Укажите параметры, если они требуются для сценария.</span><span class="sxs-lookup"><span data-stu-id="65037-312">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="65037-313">Используйте запись __Сохранить это действие скрипта__, чтобы скрипт применялся при масштабировании.</span><span class="sxs-lookup"><span data-stu-id="65037-313">Use the __Persist this script action__ entry to make sure the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="65037-314">Наконец, нажмите кнопку **Создать**, чтобы применить скрипт к кластеру.</span><span class="sxs-lookup"><span data-stu-id="65037-314">Finally, use the **Create** button to apply the script to the cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-azure-powershell"></a><span data-ttu-id="65037-315">Применение действия скрипта в работающем кластере с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="65037-315">Apply a Script Action to a running cluster from Azure PowerShell</span></span>

<span data-ttu-id="65037-316">Прежде чем продолжить, убедитесь, что вы установили и настроили Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65037-316">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="65037-317">Сведения о настройке рабочей станции для запуска командлетов HDInsight PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65037-317">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="65037-318">Следующий пример демонстрирует применение действия скрипта к работающему кластеру:</span><span class="sxs-lookup"><span data-stu-id="65037-318">The following example demonstrates how to apply a script action to a running cluster:</span></span>

<span data-ttu-id="65037-319">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span><span class="sxs-lookup"><span data-stu-id="65037-319">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span></span>

<span data-ttu-id="65037-320">После завершения операции вы получите приблизительно такой текст:</span><span class="sxs-lookup"><span data-stu-id="65037-320">Once the operation completes, you receive information similar to the following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-cli"></a><span data-ttu-id="65037-321">Применение действия сценария в работающем кластере с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="65037-321">Apply a Script Action to a running cluster from the Azure CLI</span></span>

<span data-ttu-id="65037-322">Прежде чем продолжить, убедитесь, что вы установили и настроили Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="65037-322">Before proceeding, make sure you have installed and configured the Azure CLI.</span></span> <span data-ttu-id="65037-323">Дополнительные сведения см. в статье [Установка Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="65037-323">For more information, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="65037-324">Чтобы переключиться в режим Azure Resource Manager, выполните в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="65037-324">To switch to Azure Resource Manager mode, use the following command at the command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="65037-325">Выполните приведенную далее команду для аутентификации в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="65037-325">Use the following to authenticate to your Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="65037-326">Выполните приведенную далее команду, чтобы применить действие сценария к работающему кластеру.</span><span class="sxs-lookup"><span data-stu-id="65037-326">Use the following command to apply a script action to a running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="65037-327">Если параметры для этой команды не заданы, вам будет предложено сделать это.</span><span class="sxs-lookup"><span data-stu-id="65037-327">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="65037-328">Если сценарий, указанный с помощью `-u`, принимает параметры, их можно задать с помощью параметра `-p`.</span><span class="sxs-lookup"><span data-stu-id="65037-328">If the script you specify with `-u` accepts parameters, you can specify them using the `-p` parameter.</span></span>

    <span data-ttu-id="65037-329">Допустимые типы узлов: `headnode`, `workernode` и `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="65037-329">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="65037-330">Если сценарий должен быть применен к нескольким типам узлов, укажите типы, разделив их точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="65037-330">If the script should be applied to multiple node types, specify the types separated by a ';'.</span></span> <span data-ttu-id="65037-331">Например, `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="65037-331">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="65037-332">Чтобы сохранить сценарий, добавьте `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="65037-332">To persist the script, add the `--persistOnSuccess`.</span></span> <span data-ttu-id="65037-333">Чтобы сохранить скрипт позднее, используйте `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="65037-333">You can also persist the script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="65037-334">По завершении задания выходные данные будут иметь примерно следующий вид:</span><span class="sxs-lookup"><span data-stu-id="65037-334">Once the job completes, you receive output similar to the following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-to-a-running-cluster-using-rest-api"></a><span data-ttu-id="65037-335">Применение действия сценария в работающем кластере с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="65037-335">Apply a Script Action to a running cluster using REST API</span></span>

<span data-ttu-id="65037-336">См. статью [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx) (Выполнение действий скрипта в работающем кластере).</span><span class="sxs-lookup"><span data-stu-id="65037-336">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-hdinsight-net-sdk"></a><span data-ttu-id="65037-337">Применение действия скрипта в работающем кластере с помощью пакета SDK HDInsight для .NET</span><span class="sxs-lookup"><span data-stu-id="65037-337">Apply a Script Action to a running cluster from the HDInsight .NET SDK</span></span>

<span data-ttu-id="65037-338">Пример использования пакета SDK для .NET для применения скриптов к кластеру см. на странице [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="65037-338">For an example of using the .NET SDK to apply scripts to a cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="65037-339">Просмотр журнала и изменения типа действий скриптов</span><span class="sxs-lookup"><span data-stu-id="65037-339">View history, promote, and demote Script Actions</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="65037-340">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="65037-340">Using the Azure portal</span></span>

1. <span data-ttu-id="65037-341">На [портале Azure](https://portal.azure.com)выберите свой кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-341">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="65037-342">В представлении кластера HDInsight выберите плитку **Действия скрипта**.</span><span class="sxs-lookup"><span data-stu-id="65037-342">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Элемент "Действия сценариев"](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="65037-344">Кроме того, можно щелкнуть **Все параметры**, а затем выбрать **Действия скрипта** в разделе "Параметры".</span><span class="sxs-lookup"><span data-stu-id="65037-344">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

4. <span data-ttu-id="65037-345">Журнал скриптов для этого кластера отображается в разделе "Действия скрипта".</span><span class="sxs-lookup"><span data-stu-id="65037-345">A history of scripts for this cluster is displayed on the Script Actions section.</span></span> <span data-ttu-id="65037-346">Эти сведения включают в себя список сохраняемых скриптов.</span><span class="sxs-lookup"><span data-stu-id="65037-346">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="65037-347">Как показано на снимке экрана ниже, в этом кластере был выполнен скрипт Solr.</span><span class="sxs-lookup"><span data-stu-id="65037-347">In the screenshot below, you can see that the Solr script has been ran on this cluster.</span></span> <span data-ttu-id="65037-348">Сохраняемых скриптов на нем не видно.</span><span class="sxs-lookup"><span data-stu-id="65037-348">The screenshot does not show any persisted scripts.</span></span>

    ![Раздел "Действия скриптов"](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="65037-350">При выборе сценария в журнале отображается соответствующий раздел "Свойства".</span><span class="sxs-lookup"><span data-stu-id="65037-350">Selecting a script from the history displays the Properties section for this script.</span></span> <span data-ttu-id="65037-351">В верхней части экрана можно повторно запустить скрипт или изменить его тип.</span><span class="sxs-lookup"><span data-stu-id="65037-351">From the top of the screen, you can rerun the script or promote it.</span></span>

    ![Раздел "Свойства действий скрипта"](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="65037-353">Можно также использовать элемент **…** справа от записей в разделе "Действия скрипта" для выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="65037-353">You can also use the **...** to the right of entries on the Script Actions section to perform actions.</span></span>

    ![Использование действий скриптов](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="65037-355">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="65037-355">Using Azure PowerShell</span></span>

| <span data-ttu-id="65037-356">Командлет</span><span class="sxs-lookup"><span data-stu-id="65037-356">Use the following...</span></span> | <span data-ttu-id="65037-357">Действие</span><span class="sxs-lookup"><span data-stu-id="65037-357">To ...</span></span> |
| --- | --- |
| <span data-ttu-id="65037-358">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="65037-358">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="65037-359">Получение сведений о действиях сохраняемого скрипта</span><span class="sxs-lookup"><span data-stu-id="65037-359">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="65037-360">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="65037-360">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="65037-361">Получение журнала действий скриптов, применяемых в кластере, или сведений о конкретном скрипте</span><span class="sxs-lookup"><span data-stu-id="65037-361">Retrieve a history of script actions applied to the cluster, or details for a specific script</span></span> |
| <span data-ttu-id="65037-362">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="65037-362">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="65037-363">Изменение типа специального скрипта на сохраняемый скрипт</span><span class="sxs-lookup"><span data-stu-id="65037-363">Promotes an ad hoc script action to a persisted script action</span></span> |
| <span data-ttu-id="65037-364">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="65037-364">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="65037-365">Изменение типа сохраняемого скрипта на специальный скрипт</span><span class="sxs-lookup"><span data-stu-id="65037-365">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="65037-366">При использовании `Remove-AzureRmHDInsightPersistedScriptAction` действия, выполненные скриптом, не отменяются.</span><span class="sxs-lookup"><span data-stu-id="65037-366">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo the actions performed by a script.</span></span> <span data-ttu-id="65037-367">Этот командлет только удаляет флаг сохранения.</span><span class="sxs-lookup"><span data-stu-id="65037-367">This cmdlet only removes the persisted flag.</span></span>

<span data-ttu-id="65037-368">В приведенном ниже примере скрипта показано использование командлетов для изменения типа скрипта.</span><span class="sxs-lookup"><span data-stu-id="65037-368">The following example script demonstrates using the cmdlets to promote, then demote a script.</span></span>

<span data-ttu-id="65037-369">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span><span class="sxs-lookup"><span data-stu-id="65037-369">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span></span>

### <a name="using-the-azure-cli"></a><span data-ttu-id="65037-370">Использование Azure CLI</span><span class="sxs-lookup"><span data-stu-id="65037-370">Using the Azure CLI</span></span>

| <span data-ttu-id="65037-371">Командлет</span><span class="sxs-lookup"><span data-stu-id="65037-371">Use the following...</span></span> | <span data-ttu-id="65037-372">Действие</span><span class="sxs-lookup"><span data-stu-id="65037-372">To ...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="65037-373">Получение списка сохраняемых действий сценария</span><span class="sxs-lookup"><span data-stu-id="65037-373">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="65037-374">Получение сведений о конкретном сохраняемом действии сценария</span><span class="sxs-lookup"><span data-stu-id="65037-374">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="65037-375">Получение журнала действий сценария, применяемых в кластере</span><span class="sxs-lookup"><span data-stu-id="65037-375">Retrieve a history of script actions applied to the cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="65037-376">Получение сведений о конкретном действии сценария</span><span class="sxs-lookup"><span data-stu-id="65037-376">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="65037-377">Изменение типа специального скрипта на сохраняемый скрипт</span><span class="sxs-lookup"><span data-stu-id="65037-377">Promotes an ad hoc script action to a persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="65037-378">Изменение типа сохраняемого скрипта на специальный скрипт</span><span class="sxs-lookup"><span data-stu-id="65037-378">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="65037-379">При использовании `azure hdinsight script-action persisted delete` действия, выполненные скриптом, не отменяются.</span><span class="sxs-lookup"><span data-stu-id="65037-379">Using `azure hdinsight script-action persisted delete` does not undo the actions performed by a script.</span></span> <span data-ttu-id="65037-380">Этот командлет только удаляет флаг сохранения.</span><span class="sxs-lookup"><span data-stu-id="65037-380">This cmdlet only removes the persisted flag.</span></span>

### <a name="using-the-hdinsight-net-sdk"></a><span data-ttu-id="65037-381">Использование пакета SDK HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="65037-381">Using the HDInsight .NET SDK</span></span>

<span data-ttu-id="65037-382">Пример использования пакета SDK для .NET для получения журнала скриптов из кластера см. на странице [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="65037-382">For an example of using the .NET SDK to retrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="65037-383">В этом примере также показано, как установить приложение HDInsight с помощью пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="65037-383">This example also demonstrates how to install an HDInsight application using the .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="65037-384">Поддержка программного обеспечения с открытым исходным кодом, используемого в кластере HDInsight</span><span class="sxs-lookup"><span data-stu-id="65037-384">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="65037-385">Служба Microsoft Azure HDInsight использует сформированную вокруг Hadoop экосистему технологий с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="65037-385">The Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="65037-386">Microsoft Azure предоставляет общий уровень поддержки для технологий с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="65037-386">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="65037-387">Дополнительные сведения см. в разделе, посвященном **области действия поддержки**, на [веб-сайте с часто задаваемыми вопросами о поддержке Azure](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="65037-387">For more information, see the **Support Scope** section of the [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="65037-388">Служба HDInsight предоставляет дополнительный уровень поддержки для встроенных компонентов.</span><span class="sxs-lookup"><span data-stu-id="65037-388">The HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="65037-389">В службе HDInsight доступно два типа компонентов с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="65037-389">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="65037-390">**Встроенные компоненты.** Эти компоненты предварительно установлены в кластерах HDInsight и предоставляют его базовые функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="65037-390">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="65037-391">Например, к этой категории относится диспетчер ресурсов YARN, язык запросов Hive (HiveQL) и библиотека Mahout.</span><span class="sxs-lookup"><span data-stu-id="65037-391">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="65037-392">Полный список компонентов кластера доступен в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="65037-392">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="65037-393">**Настраиваемые компоненты.** Как пользователь кластера вы можете установить или использовать в рабочей нагрузке любой компонент, полученный из сообщества или созданный самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="65037-393">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="65037-394">Компоненты, поставляемые с кластером HDInsight, полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="65037-394">Components provided with the HDInsight cluster are fully supported.</span></span> <span data-ttu-id="65037-395">Служба поддержки Майкрософт помогает выявлять и устранять проблемы, связанные с этими компонентами.</span><span class="sxs-lookup"><span data-stu-id="65037-395">Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="65037-396">Настраиваемые компоненты получают ограниченную коммерчески оправданную поддержку, способствующую дальнейшей диагностике проблемы.</span><span class="sxs-lookup"><span data-stu-id="65037-396">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="65037-397">Служба поддержки Майкрософт может устранить проблему ИЛИ вас могут попросить обратиться к специалистам по технологиям с открытым исходным кодом, используя доступные каналы связи.</span><span class="sxs-lookup"><span data-stu-id="65037-397">Microsoft support may be able to resolve the issue OR they may ask you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="65037-398">Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).</span><span class="sxs-lookup"><span data-stu-id="65037-398">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="65037-399">Служба HDInsight позволяет использовать настраиваемые компоненты несколькими разными способами.</span><span class="sxs-lookup"><span data-stu-id="65037-399">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="65037-400">Уровень поддержки не зависит от того, как компонент используется или устанавливается в кластере.</span><span class="sxs-lookup"><span data-stu-id="65037-400">The same level of support applies, regardless of how a component is used or installed on the cluster.</span></span> <span data-ttu-id="65037-401">Ниже приведен список самых распространенных способов использования настраиваемых компонентов в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-401">The following list describes the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="65037-402">Отправка задания. В кластер можно отправлять задания Hadoop или другие типы заданий, выполняющие или использующие настраиваемые компоненты.</span><span class="sxs-lookup"><span data-stu-id="65037-402">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>

2. <span data-ttu-id="65037-403">Настройка кластера. Во время создания кластера можно указать дополнительные параметры и настраиваемые компоненты, устанавливаемые на узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-403">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on the cluster nodes.</span></span>

3. <span data-ttu-id="65037-404">Примеры. Для популярных настраиваемых компонентов корпорация Майкрософт и другие компании могут предоставлять примеры использования таких компонентов в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-404">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="65037-405">Эти примеры представляются без поддержки.</span><span class="sxs-lookup"><span data-stu-id="65037-405">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="65037-406">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="65037-406">Troubleshooting</span></span>

<span data-ttu-id="65037-407">Вы можете использовать веб-интерфейс Ambari для просмотра сведений, регистрируемых действиями скриптов.</span><span class="sxs-lookup"><span data-stu-id="65037-407">You can use Ambari web UI to view information logged by script actions.</span></span> <span data-ttu-id="65037-408">Если при создании кластера произошел сбой скрипта, вы можете просмотреть журналы в учетной записи хранения по умолчанию, связанной с кластером.</span><span class="sxs-lookup"><span data-stu-id="65037-408">If the script fails during cluster creation, the logs are also available in the default storage account associated with the cluster.</span></span> <span data-ttu-id="65037-409">Этот раздел содержит сведения о том, как получить журналы обоими этими способами.</span><span class="sxs-lookup"><span data-stu-id="65037-409">This section provides information on how to retrieve the logs using both these options.</span></span>

### <a name="using-the-ambari-web-ui"></a><span data-ttu-id="65037-410">Использование веб-интерфейса Ambari</span><span class="sxs-lookup"><span data-stu-id="65037-410">Using the Ambari Web UI</span></span>

1. <span data-ttu-id="65037-411">В браузере перейдите на сайт https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="65037-411">In your browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="65037-412">Параметр CLUSTERNAME нужно заменить именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-412">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="65037-413">При появлении запроса введите имя (admin) и пароль учетной записи администратора кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-413">When prompted, enter the admin account name (admin) and password for the cluster.</span></span> <span data-ttu-id="65037-414">Возможно, вам потребуется повторно ввести учетные данные администратора в веб-форме.</span><span class="sxs-lookup"><span data-stu-id="65037-414">You may have to reenter the admin credentials in a web form.</span></span>

2. <span data-ttu-id="65037-415">В панели вверху страницы выберите запись **ops**.</span><span class="sxs-lookup"><span data-stu-id="65037-415">From the bar at the top of the page, select the **ops** entry.</span></span> <span data-ttu-id="65037-416">Появится список текущих и предыдущих операций, выполняемых в кластере с помощью Ambari.</span><span class="sxs-lookup"><span data-stu-id="65037-416">A list of current and previous operations performed on the cluster through Ambari is displayed.</span></span>

    ![Веб-панель Ambari с выбранной записью ops](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="65037-418">Найдите записи, для которых в столбце **Операции** указано **run\_customscriptaction**.</span><span class="sxs-lookup"><span data-stu-id="65037-418">Find the entries that have **run\_customscriptaction** in the **Operations** column.</span></span> <span data-ttu-id="65037-419">Такие записи создаются при выполнении действий скриптов.</span><span class="sxs-lookup"><span data-stu-id="65037-419">These entries are created when the Script Actions run.</span></span>

    ![Снимок экрана операций](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="65037-421">Для просмотра выходных данных STDOUT и STDERR выберите запись run\customscriptaction и перейдите по ссылкам.</span><span class="sxs-lookup"><span data-stu-id="65037-421">To view the STDOUT and STDERR output, select the run\customscriptaction entry and drill down through the links.</span></span> <span data-ttu-id="65037-422">Эти выходные данные формируются при запуске сценария и могут содержать полезные сведения.</span><span class="sxs-lookup"><span data-stu-id="65037-422">This output is generated when the script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-the-default-storage-account"></a><span data-ttu-id="65037-423">Доступ к журналам из учетной записи хранения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="65037-423">Access logs from the default storage account</span></span>

<span data-ttu-id="65037-424">При сбое создания кластера из-за ошибки в действии скрипта журналы по-прежнему будут доступными в учетной записи хранения кластера.</span><span class="sxs-lookup"><span data-stu-id="65037-424">If the cluster creation fails due to a script action error, the logs can be accessed from the cluster storage account.</span></span>

* <span data-ttu-id="65037-425">Журналы хранилища находятся в `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="65037-425">The storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Снимок экрана операций](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="65037-427">В этом каталоге журналы упорядочены по узлам headnode, workernode и zookeeper.</span><span class="sxs-lookup"><span data-stu-id="65037-427">Under this directory, the logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="65037-428">Ниже приведены некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="65037-428">Some examples are:</span></span>

    * <span data-ttu-id="65037-429">**Головной узел:** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="65037-429">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="65037-430">**Рабочий узел** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="65037-430">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="65037-431">**Узел Zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="65037-431">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="65037-432">Все stdout и stderr соответствующего узла передаются в учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="65037-432">All stdout and stderr of the corresponding host is uploaded to the storage account.</span></span> <span data-ttu-id="65037-433">Для каждого действия скрипта создается файл **output-\*.txt** и файл **errors-\*.txt**.</span><span class="sxs-lookup"><span data-stu-id="65037-433">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="65037-434">Выходной TXT-файл содержит сведения об универсальном коде ресурса (URI) сценария, который был запущен на узле.</span><span class="sxs-lookup"><span data-stu-id="65037-434">The output-*.txt file contains information about the URI of the script that got run on the host.</span></span> <span data-ttu-id="65037-435">Например:</span><span class="sxs-lookup"><span data-stu-id="65037-435">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="65037-436">Возможно, повторно создан кластер действия сценария с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="65037-436">It's possible that you repeatedly create a script action cluster with the same name.</span></span> <span data-ttu-id="65037-437">В этом случае соответствующие журналы можно отличить по имени папки DATE.</span><span class="sxs-lookup"><span data-stu-id="65037-437">In such case, you can distinguish the relevant logs based on the DATE folder name.</span></span> <span data-ttu-id="65037-438">Например, структура папок для кластера (mycluster), созданного в другие дни, будет похожа на следующие записи журнала:</span><span class="sxs-lookup"><span data-stu-id="65037-438">For example, the folder structure for a cluster (mycluster) created on different dates appears similar to the following log entries:</span></span>

    <span data-ttu-id="65037-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="65037-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="65037-440">При создании кластера действие сценария с таким же именем в тот же день можно использовать уникальный префикс для идентификации соответствующих файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="65037-440">If you create a script action cluster with the same name on the same day, you can use the unique prefix to identify the relevant log files.</span></span>

* <span data-ttu-id="65037-441">При создании кластера около полуночи (00:00) файлы журналов могут включать сведения за два дня.</span><span class="sxs-lookup"><span data-stu-id="65037-441">If you create a cluster near 12:00AM (midnight), it's possible that the log files span across two days.</span></span> <span data-ttu-id="65037-442">В таких случаях для одного кластера будут отображаться две разные папки даты.</span><span class="sxs-lookup"><span data-stu-id="65037-442">In such cases, you see two different date folders for the same cluster.</span></span>

* <span data-ttu-id="65037-443">Передача файлов журнала в контейнер по умолчанию может занять до 5 минут, особенно для больших кластеров.</span><span class="sxs-lookup"><span data-stu-id="65037-443">Uploading log files to the default container can take up to 5 mins, especially for large clusters.</span></span> <span data-ttu-id="65037-444">Таким образом, если вы хотите получить доступ к журналам, не следует немедленно удалять кластер при сбое действия сценария.</span><span class="sxs-lookup"><span data-stu-id="65037-444">So, if you want to access the logs, you should not immediately delete the cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="65037-445">Модуль наблюдения Ambari</span><span class="sxs-lookup"><span data-stu-id="65037-445">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="65037-446">Не изменяйте пароль модуля наблюдения Ambari (hdinsightwatchdog) в кластере HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="65037-446">Do not change the password for the Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="65037-447">Это не позволит выполнять новые действия сценария в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-447">Changing the password for this account breaks the ability to run new script actions on the HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="65037-448">Не удается импортировать BlobService имени</span><span class="sxs-lookup"><span data-stu-id="65037-448">Can't import name BlobService</span></span>

<span data-ttu-id="65037-449">__Симптомы:__ сбой действия скрипта.</span><span class="sxs-lookup"><span data-stu-id="65037-449">__Symptoms__: The script action fails.</span></span> <span data-ttu-id="65037-450">При просмотре операции в Ambari выводится следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="65037-450">Text similar to the following error is displayed when you view the operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="65037-451">__Причина.__ Эта ошибка возникает при обновлении клиента Python службы хранилища Azure, который входит в состав кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65037-451">__Cause__: This error occurs if you upgrade the Python Azure Storage client that is included with the HDInsight cluster.</span></span> <span data-ttu-id="65037-452">HDInsight требуется клиент службы хранилища Azure версии 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="65037-452">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="65037-453">__Способ устранения.__ Чтобы устранить эту ошибку, подключитесь к каждому узлу кластера вручную, используя `ssh`, и выполните следующую команду, чтобы переустановить клиент службы хранилища требуемой версии:</span><span class="sxs-lookup"><span data-stu-id="65037-453">__Resolution__: To resolve this error, manually connect to each cluster node using `ssh` and use the following command to reinstall the correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="65037-454">Сведения о подключении к кластеру по протоколу SSH см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="65037-454">For information on connecting to the cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="65037-455">Журнал не отображает скрипты, используемые во время создания кластера</span><span class="sxs-lookup"><span data-stu-id="65037-455">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="65037-456">Если кластер создан до 15 марта 2016 г., в журнале действий скриптов могут отсутствовать записи.</span><span class="sxs-lookup"><span data-stu-id="65037-456">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="65037-457">Если размер кластера изменен после 15 марта 2016 г., скрипты, используемые при создании кластера, будут отображаться в журнале, так как они применялись на новых узлах кластера при изменении размера.</span><span class="sxs-lookup"><span data-stu-id="65037-457">If you resize the cluster after March 15, 2016, the scripts using during cluster creation appear in history as they are applied to new nodes in the cluster as part of the resize operation.</span></span>

<span data-ttu-id="65037-458">Есть два исключения.</span><span class="sxs-lookup"><span data-stu-id="65037-458">There are two exceptions:</span></span>

* <span data-ttu-id="65037-459">Если кластер создан до 1 сентября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="65037-459">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="65037-460">Это дата добавления действий скриптов.</span><span class="sxs-lookup"><span data-stu-id="65037-460">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="65037-461">Если кластер был создан раньше, действия скриптов не могли использоваться при его создании.</span><span class="sxs-lookup"><span data-stu-id="65037-461">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="65037-462">Если при создании кластера использовалось несколько действий скриптов, для которых использовалось одно имя, или же если для разных скриптов использовалось одно имя и один универсальный код ресурса (URI), но разные параметры.</span><span class="sxs-lookup"><span data-stu-id="65037-462">If you used multiple Script Actions during cluster creation, and used the same name for multiple scripts, or the same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="65037-463">В таких случаях происходит следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="65037-463">In these cases, you receive the following error:</span></span>

    <span data-ttu-id="65037-464">В таком кластере из-за конфликта имен скриптов в существующих скриптах новые действия скриптов выполняться не будут.</span><span class="sxs-lookup"><span data-stu-id="65037-464">No new script actions can be ran on this cluster due to conflicting script names in existing scripts.</span></span> <span data-ttu-id="65037-465">Имена скриптов, указанные при создании кластера, должны быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="65037-465">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="65037-466">Существующие скрипты выполняются при изменении размера.</span><span class="sxs-lookup"><span data-stu-id="65037-466">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65037-467">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65037-467">Next steps</span></span>

* [<span data-ttu-id="65037-468">Разработка скриптов действия сценария для HDInsight</span><span class="sxs-lookup"><span data-stu-id="65037-468">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="65037-469">Установка и использование Solr в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="65037-469">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="65037-470">Установка и использование Giraph в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="65037-470">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="65037-471">Добавление дополнительных учетных записей хранения Azure в HDInsight</span><span class="sxs-lookup"><span data-stu-id="65037-471">Add additional storage to an HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

<span data-ttu-id="65037-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Этапы создания кластера"</span><span class="sxs-lookup"><span data-stu-id="65037-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
