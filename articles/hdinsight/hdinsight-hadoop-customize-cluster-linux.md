---
title: "кластеры HDInsight aaaCustomize с помощью действий скрипта - Azure | Документы Microsoft"
description: "Добавьте пользовательские компоненты кластеров на основе tooLinux HDInsight с помощью действий скрипта. Действия сценариев, Bash-скриптов, которые могут быть конфигурации кластера используется toocustomize hello или добавить дополнительные службы и служебные программы, например цветового тона, Solr или R."
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
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="5e064-104">Настройка кластеров HDInsight под управлением Linux с помощью действия сценария</span><span class="sxs-lookup"><span data-stu-id="5e064-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="5e064-105">HDInsight предоставляет параметр конфигурации **действие сценария** , вызывающий пользовательские скрипты, настроить кластер hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize hello cluster.</span></span> <span data-ttu-id="5e064-106">Эти сценарии, используемые tooinstall дополнительные компоненты и изменения параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5e064-106">These scripts are used tooinstall additional components and change configuration settings.</span></span> <span data-ttu-id="5e064-107">Действия скрипта можно использовать во время или после создания кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e064-108">действия сценариев toouse возможность Hello в кластере уже запущенному доступна только для кластеров HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="5e064-108">hello ability toouse script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="5e064-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="5e064-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5e064-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5e064-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="5e064-111">Действия скриптов также может быть опубликованным toohello Azure Marketplace как приложение HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e064-111">Script actions can also be published toohello Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="5e064-112">Некоторые примеры hello в этом документе показывают, как можно установить приложения HDInsight с помощью команд-действий сценарий PowerShell и hello пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="5e064-112">Some of hello examples in this document show how you can install an HDInsight application using script action commands from PowerShell and hello .NET SDK.</span></span> <span data-ttu-id="5e064-113">Дополнительные сведения о приложениях HDInsight см. в разделе [HDInsight публикации приложения в Azure Marketplace hello](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-113">For more information on HDInsight applications, see [Publish HDInsight applications into hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="5e064-114">Разрешения</span><span class="sxs-lookup"><span data-stu-id="5e064-114">Permissions</span></span>

<span data-ttu-id="5e064-115">При использовании кластера HDInsight, присоединенных к домену, существует два Ambari разрешения, необходимые при использовании действия скриптов с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with hello cluster:</span></span>

* <span data-ttu-id="5e064-116">**AMBARI. ЗАПУСТИТЕ\_НАСТРАИВАЕМЫЙ\_команда**: роль администратора Ambari hello имеет это разрешение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5e064-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: hello Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="5e064-117">**КЛАСТЕР. ЗАПУСТИТЕ\_НАСТРАИВАЕМЫЙ\_команда**: оба Здравствуйте, администратор кластера HDInsight и администратор Ambari иметь это разрешение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5e064-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both hello HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="5e064-118">Дополнительные сведения о работе с разрешениями в присоединенном к домену кластере HDInsight см. в статье [Управление присоединенными к домену кластерами HDInsight (предварительная версия)](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="5e064-119">управление доступом;</span><span class="sxs-lookup"><span data-stu-id="5e064-119">Access control</span></span>

<span data-ttu-id="5e064-120">Если вы не hello администратором или владельцем подписки Azure, ваша учетная запись должна быть хотя бы **участника** доступа toohello ресурсов группы, содержащей hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e064-120">If you are not hello administrator/owner of your Azure subscription, your account must have at least **Contributor** access toohello resource group that contains hello HDInsight cluster.</span></span>

<span data-ttu-id="5e064-121">Кроме того при создании кластера HDInsight, имеющим по крайней мере **участника** toohello доступа к подписке Azure необходимо уже зарегистрированы hello поставщика для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e064-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access toohello Azure subscription must have previously registered hello provider for HDInsight.</span></span> <span data-ttu-id="5e064-122">Регистрация поставщика происходит, когда пользователь с подпиской toohello доступа участника создает ресурс для hello первый раз на hello подписки.</span><span class="sxs-lookup"><span data-stu-id="5e064-122">Provider registration happens when a user with Contributor access toohello subscription creates a resource for hello first time on hello subscription.</span></span> <span data-ttu-id="5e064-123">Регистрацию также можно выполнить без создания ресурса [с помощью REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="5e064-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="5e064-124">Дополнительные сведения о работе с помощью управления доступом см. в разделе hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="5e064-124">For more information on working with access management, see hello following documents:</span></span>

* [<span data-ttu-id="5e064-125">Приступая к управлению доступом в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5e064-125">Get started with access management in hello Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="5e064-126">Использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure</span><span class="sxs-lookup"><span data-stu-id="5e064-126">Use role assignments toomanage access tooyour Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="5e064-127">Что такое действия скриптов</span><span class="sxs-lookup"><span data-stu-id="5e064-127">Understanding Script Actions</span></span>

<span data-ttu-id="5e064-128">Действие скрипта — это просто скрипт Bash, в который вы вводите универсальный код ресурса (URI) и для которого вы указываете параметры.</span><span class="sxs-lookup"><span data-stu-id="5e064-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="5e064-129">Hello скрипт выполняется на узлах в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-129">hello script runs on nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="5e064-130">Hello ниже приведены характеристики и возможности выполнения сценариев.</span><span class="sxs-lookup"><span data-stu-id="5e064-130">hello following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="5e064-131">Должен быть сохранен в URI, который доступен с кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-131">Must be stored on a URI that is accessible from hello HDInsight cluster.</span></span> <span data-ttu-id="5e064-132">Hello ниже приведены возможные хранилищах.</span><span class="sxs-lookup"><span data-stu-id="5e064-132">hello following are possible storage locations:</span></span>

    * <span data-ttu-id="5e064-133">**Хранилища Озера данных Azure** учетной записи, доступном из кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-133">An **Azure Data Lake Store** account that is accessible by hello HDInsight cluster.</span></span> <span data-ttu-id="5e064-134">Дополнительные сведения об использовании Azure Data Lake Store с HDInsight см. в статье [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="5e064-135">При использовании сценария, сохраненного в хранилище Озера данных, является формат URI hello `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="5e064-135">When using a script stored in Data Lake Store, hello URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="5e064-136">tooaccess Hello службы основной HDInsight использует хранилище Озера данных должен иметь доступ на чтение toohello сценария.</span><span class="sxs-lookup"><span data-stu-id="5e064-136">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

    * <span data-ttu-id="5e064-137">Большой двоичный объект в **учетной записи хранилища Azure** , является либо учетной записи хранения основной или дополнительный hello для кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-137">A blob in an **Azure Storage account** that is either hello primary or additional storage account for hello HDInsight cluster.</span></span> <span data-ttu-id="5e064-138">Во время создания кластера HDInsight предоставляется доступ tooboth из этих типов учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="5e064-138">HDInsight is granted access tooboth of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="5e064-139">Служба совместного доступа к файлам, например хранилище BLOB-объектов Azure, GitHub, OneDrive, Dropbox и т. д.</span><span class="sxs-lookup"><span data-stu-id="5e064-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="5e064-140">Примеры URI, в разделе hello [скрипты действий примера сценария](#example-script-action-scripts) раздела.</span><span class="sxs-lookup"><span data-stu-id="5e064-140">For example URIs, see hello [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="5e064-141">HDInsight поддерживает только учетные записи хранения Azure __общего назначения__.</span><span class="sxs-lookup"><span data-stu-id="5e064-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="5e064-142">Он не поддерживает hello __хранилище больших двоичных объектов__ тип учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5e064-142">It does not currently support hello __Blob storage__ account type.</span></span>

* <span data-ttu-id="5e064-143">Можно ограничить слишком**проведение только определенные типы узлов**, пример головного узла или узлов рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="5e064-143">Can be restricted too**run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5e064-144">При использовании с HDInsight Premium, можно задать, использование hello сценария на узле edge hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-144">When used with HDInsight Premium, you can specify that hello script should be used on hello edge node.</span></span>

* <span data-ttu-id="5e064-145">Действия скрипта могут быть **сохраняемыми** или **специализированными**.</span><span class="sxs-lookup"><span data-stu-id="5e064-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="5e064-146">**Сохранить** сценарии, примененные tooworker узлы добавлены toohello кластера после запуска сценария hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-146">**Persisted** scripts are applied tooworker nodes added toohello cluster after hello script runs.</span></span> <span data-ttu-id="5e064-147">Например, при масштабировании hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-147">For example, when scaling up hello cluster.</span></span>

    <span data-ttu-id="5e064-148">Сохраненный скрипт также может применять изменения tooanother узел типа, например головного узла.</span><span class="sxs-lookup"><span data-stu-id="5e064-148">A persisted script might also apply changes tooanother node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5e064-149">Действия сохраняемых скриптов должны иметь уникальные имена.</span><span class="sxs-lookup"><span data-stu-id="5e064-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="5e064-150">**Специализированные** скрипты не сохраняются.</span><span class="sxs-lookup"><span data-stu-id="5e064-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="5e064-151">Они не применяются tooworker узлы добавлены toohello кластера после hello сценарий был выполнен.</span><span class="sxs-lookup"><span data-stu-id="5e064-151">They are not applied tooworker nodes added toohello cluster after hello script has ran.</span></span> <span data-ttu-id="5e064-152">Впоследствии можно распространить нерегламентированных сценариев tooa сохранить скрипт или понизить уровень скрипта нерегламентированных tooan сохраненный скрипт.</span><span class="sxs-lookup"><span data-stu-id="5e064-152">You can subsequently promote an ad hoc script tooa persisted script, or demote a persisted script tooan ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5e064-153">Действия скриптов, используемые при создании кластера, автоматически сохраняются.</span><span class="sxs-lookup"><span data-stu-id="5e064-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="5e064-154">Скрипты, в которых произошла ошибка, не сохраняются, даже если вы отдельно указали, что они должны быть сохранены.</span><span class="sxs-lookup"><span data-stu-id="5e064-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="5e064-155">Может принимать **параметров** , используемых скриптом hello во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="5e064-155">Can accept **parameters** that are used by hello script during execution.</span></span>
* <span data-ttu-id="5e064-156">Запустите с **корневой права доступа уровня** на узлах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-156">Run with **root level privileges** on hello cluster nodes.</span></span>
* <span data-ttu-id="5e064-157">Можно использовать через hello **портал Azure**, **Azure PowerShell**, **Azure CLI**, или **HDInsight .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="5e064-157">Can be used through hello **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="5e064-158">кластер Hello ведет журнал всех сценариев, которые уже были выполнены.</span><span class="sxs-lookup"><span data-stu-id="5e064-158">hello cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="5e064-159">Журнал Hello полезно при необходимости идентификатор hello toofind скрипта для операции повышения или понижения роли.</span><span class="sxs-lookup"><span data-stu-id="5e064-159">hello history is useful when you need toofind hello ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e064-160">Нет не tooundo автоматическим способом hello изменений, внесенных в действие сценария.</span><span class="sxs-lookup"><span data-stu-id="5e064-160">There is no automatic way tooundo hello changes made by a script action.</span></span> <span data-ttu-id="5e064-161">Либо вручную отменить изменения hello, или укажите скрипт, который изменяет их.</span><span class="sxs-lookup"><span data-stu-id="5e064-161">Either manually reverse hello changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="5e064-162">Действие сценария в процессе создания кластера hello</span><span class="sxs-lookup"><span data-stu-id="5e064-162">Script Action in hello cluster creation process</span></span>

<span data-ttu-id="5e064-163">Действия скриптов, используемые в процессе создания кластера и выполняющиеся в существующем кластере, несколько отличаются:</span><span class="sxs-lookup"><span data-stu-id="5e064-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="5e064-164">скрипт Hello **автоматически сохраненные**.</span><span class="sxs-lookup"><span data-stu-id="5e064-164">hello script is **automatically persisted**.</span></span>
* <span data-ttu-id="5e064-165">Объект **сбоя** в hello сценарий может привести к toofail процесса создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-165">A **failure** in hello script can cause hello cluster creation process toofail.</span></span>

<span data-ttu-id="5e064-166">Hello следующей схеме показана при выполнении сценария действия во время создания hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-166">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="5e064-167">![Настройка кластера HDInsight и этапы создания кластера][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="5e064-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="5e064-168">Hello скрипт выполняется при HDInsight настроена.</span><span class="sxs-lookup"><span data-stu-id="5e064-168">hello script runs while HDInsight is being configured.</span></span> <span data-ttu-id="5e064-169">На этом этапе hello сценарий выполняется параллельно на всех hello указанные узлы в кластере hello и запускается с правами корневой на узлах hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-169">At this stage, hello script runs in parallel on all hello specified nodes in hello cluster, and runs with root privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="5e064-170">Поскольку hello скрипт выполняется на узлах кластера hello корневой уровень прав доступа, можно выполнять такие операции, как остановка и запуск служб, включая службы, связанные с Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5e064-170">Because hello script runs with root level privilege on hello cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="5e064-171">При остановке службы, необходимо убедиться, что служба Ambari hello и других служб, связанных с Hadoop доступны и запущены перед hello сценарий завершает работу.</span><span class="sxs-lookup"><span data-stu-id="5e064-171">If you stop services, you must ensure that hello Ambari service and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="5e064-172">Эти службы необходимы toosuccessfully определить работоспособность hello и состояние кластера hello во время создания.</span><span class="sxs-lookup"><span data-stu-id="5e064-172">These services are required toosuccessfully determine hello health and state of hello cluster while it is being created.</span></span>


<span data-ttu-id="5e064-173">При создании кластера можно использовать несколько действий скриптов одновременно.</span><span class="sxs-lookup"><span data-stu-id="5e064-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="5e064-174">Эти сценарии вызываются в порядке hello, в котором они указаны.</span><span class="sxs-lookup"><span data-stu-id="5e064-174">These scripts are invoked in hello order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e064-175">Действия сценария должны быть завершены в течение 60 минут. В противном случае возникнет ошибка времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="5e064-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="5e064-176">Во время подготовки кластеров, hello скрипт выполняется параллельно с другими процессами, установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="5e064-176">During cluster provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="5e064-177">Соперничество за ресурсы, такие как ЦП или в сети может вызвать скрипт hello tootake больше toofinish не так, как в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="5e064-177">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>
>
> <span data-ttu-id="5e064-178">toominimize hello время принимает toorun hello скрипт, избежать задач, таких как загрузка и компиляция приложения из источника.</span><span class="sxs-lookup"><span data-stu-id="5e064-178">toominimize hello time it takes toorun hello script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="5e064-179">Предварительная компиляция приложения и хранения hello двоичного файла в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="5e064-179">Pre-compile applications and store hello binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="5e064-180">Действие скрипта в работающем кластере</span><span class="sxs-lookup"><span data-stu-id="5e064-180">Script action on a running cluster</span></span>

<span data-ttu-id="5e064-181">В отличие от сценария, который используется во время создания кластера, ошибка в скрипте действия были выполнены на уже запущенному кластеру не вызывает автоматического состояние tooa сбой toochange hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause hello cluster toochange tooa failed state.</span></span> <span data-ttu-id="5e064-182">По завершении сценария hello кластера должна возвращать tooa состояние «запущен».</span><span class="sxs-lookup"><span data-stu-id="5e064-182">Once a script completes, hello cluster should return tooa "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e064-183">Даже если hello кластер находится в состоянии «работает», hello невыполненного сценария может нарушили вещей.</span><span class="sxs-lookup"><span data-stu-id="5e064-183">Even if hello cluster has a 'running' state, hello failed script may have broken things.</span></span> <span data-ttu-id="5e064-184">Например сценарий удалось удалить файлы, необходимый hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-184">For example, a script could delete files needed by hello cluster.</span></span>
>
> <span data-ttu-id="5e064-185">Действия сценариев выполняются с правами корневой, поэтому необходимо понять назначение сценарий перед ее применением tooyour кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it tooyour cluster.</span></span>

<span data-ttu-id="5e064-186">При применении кластера tooa сценария, состояние кластера hello изменяется toofrom **под управлением** слишком**принято**, затем **конфигурацию HDInsight**опять слишком**Под управлением** для успешного скриптов.</span><span class="sxs-lookup"><span data-stu-id="5e064-186">When applying a script tooa cluster, hello cluster state changes toofrom **Running** too**Accepted**, then **HDInsight configuration**, and finally back too**Running** for successful scripts.</span></span> <span data-ttu-id="5e064-187">состояние скрипта Hello заносится в журнал действий скриптов hello и toodetermine этой информации можно использовать ли скрипт hello успешно или неудачно.</span><span class="sxs-lookup"><span data-stu-id="5e064-187">hello script status is logged in hello script action history, and you can use this information toodetermine whether hello script succeeded or failed.</span></span> <span data-ttu-id="5e064-188">Например, hello `Get-AzureRmHDInsightScriptActionHistory` командлет PowerShell может быть состояние hello используется tooview сценария.</span><span class="sxs-lookup"><span data-stu-id="5e064-188">For example, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used tooview hello status of a script.</span></span> <span data-ttu-id="5e064-189">Она возвращает сведения аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="5e064-189">It returns information similar toohello following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="5e064-190">Если вы изменили пароль пользователя (администратор) hello кластера после создания кластера hello, сценарий, который выполняли действия для этого кластера может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="5e064-190">If you have changed hello cluster user (admin) password after hello cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="5e064-191">При наличии каких-либо действий сохраненный скрипт рабочих узлов, целевой этих скриптов может возникать, если масштабирование hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale hello cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="5e064-192">Пример действий сценария</span><span class="sxs-lookup"><span data-stu-id="5e064-192">Example Script Action scripts</span></span>

<span data-ttu-id="5e064-193">Сценарий, сценарии, действие применяется с помощью hello следующие программы:</span><span class="sxs-lookup"><span data-stu-id="5e064-193">Script Action scripts can be used through hello following utilities:</span></span>

* <span data-ttu-id="5e064-194">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5e064-194">Azure portal</span></span>
* <span data-ttu-id="5e064-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e064-195">Azure PowerShell</span></span>
* <span data-ttu-id="5e064-196">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="5e064-196">Azure CLI</span></span>
* <span data-ttu-id="5e064-197">Пакет SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="5e064-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="5e064-198">HDInsight предоставляет следующие компоненты в кластерах HDInsight hello tooinstall сценариев:</span><span class="sxs-lookup"><span data-stu-id="5e064-198">HDInsight provides scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="5e064-199">Имя</span><span class="sxs-lookup"><span data-stu-id="5e064-199">Name</span></span> | <span data-ttu-id="5e064-200">Скрипт</span><span class="sxs-lookup"><span data-stu-id="5e064-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="5e064-201">**Добавление учетной записи хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="5e064-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="5e064-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. В разделе [tooan HDInsight добавить дополнительное хранилище кластера](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="5e064-203">**Установка Hue**</span><span class="sxs-lookup"><span data-stu-id="5e064-203">**Install Hue**</span></span> |<span data-ttu-id="5e064-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. См. статью [Установка и использование Hue на кластерах HDInsight Hadoop](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="5e064-205">**Установка Presto**</span><span class="sxs-lookup"><span data-stu-id="5e064-205">**Install Presto**</span></span> |<span data-ttu-id="5e064-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. См. статью [Установка и использование Presto в кластерах HDInsight](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="5e064-207">**Установка Solr**</span><span class="sxs-lookup"><span data-stu-id="5e064-207">**Install Solr**</span></span> |<span data-ttu-id="5e064-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Ознакомьтесь со статьей [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="5e064-209">**Установка Giraph**</span><span class="sxs-lookup"><span data-stu-id="5e064-209">**Install Giraph**</span></span> |<span data-ttu-id="5e064-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Ознакомьтесь со статьей [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="5e064-211">**Предварительная загрузка библиотек Hive**</span><span class="sxs-lookup"><span data-stu-id="5e064-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="5e064-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. См статью [Добавление библиотек Hive в кластеры HDInsight](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="5e064-213">**Установка или обновление Mono**</span><span class="sxs-lookup"><span data-stu-id="5e064-213">**Install or update Mono**</span></span> | <span data-ttu-id="5e064-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash</span><span class="sxs-lookup"><span data-stu-id="5e064-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="5e064-215">См. статью [Установка или обновление Mono в HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="5e064-216">Использование действия скрипта при создании кластера</span><span class="sxs-lookup"><span data-stu-id="5e064-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="5e064-217">В этом разделе приведены примеры о различных способах hello действия скриптов можно использовать при создании кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e064-217">This section provides examples on hello different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a><span data-ttu-id="5e064-218">Используйте действие скрипта, во время создания кластера из hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5e064-218">Use a Script Action during cluster creation from hello Azure portal</span></span>

1. <span data-ttu-id="5e064-219">Начните создание кластера, как описано в разделе [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="5e064-220">Остановить при достижении hello __Сводка кластера__ раздела.</span><span class="sxs-lookup"><span data-stu-id="5e064-220">Stop when you reach hello __Cluster summary__ section.</span></span>

2. <span data-ttu-id="5e064-221">Из hello __Сводка кластера__ раздел, выберите hello __изменить__ связей для __Дополнительные параметры__.</span><span class="sxs-lookup"><span data-stu-id="5e064-221">From hello __Cluster summary__ section, select hello __edit__ link for __Advanced settings__.</span></span>

    ![Ссылка "Дополнительные параметры"](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="5e064-223">Из hello __Дополнительные параметры__ выберите __скрипт действия__.</span><span class="sxs-lookup"><span data-stu-id="5e064-223">From hello __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="5e064-224">Из hello __скрипт действия__ выберите __+ new отправки__</span><span class="sxs-lookup"><span data-stu-id="5e064-224">From hello __Script actions__ section, select __+ Submit new__</span></span>

    ![Отправка нового действия скрипта](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="5e064-226">Используйте hello __выберите сценарий__ tooselect входа готового скрипта.</span><span class="sxs-lookup"><span data-stu-id="5e064-226">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="5e064-227">toouse пользовательского скрипта, выберите __пользовательские__ и укажите hello __имя__ и __Bash универсальный код Ресурса скрипта__ для своего сценария.</span><span class="sxs-lookup"><span data-stu-id="5e064-227">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Добавить скрипт в виде выберите сценария hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="5e064-229">Привет, в следующей таблице описываются элементы hello в форме hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-229">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="5e064-230">Свойство</span><span class="sxs-lookup"><span data-stu-id="5e064-230">Property</span></span> | <span data-ttu-id="5e064-231">Значение</span><span class="sxs-lookup"><span data-stu-id="5e064-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5e064-232">Выберите скрипт</span><span class="sxs-lookup"><span data-stu-id="5e064-232">Select a script</span></span> | <span data-ttu-id="5e064-233">toouse собственный сценарий, выберите __настраиваемый__.</span><span class="sxs-lookup"><span data-stu-id="5e064-233">toouse your own script, select __Custom__.</span></span> <span data-ttu-id="5e064-234">В противном случае выберите один из hello предоставляются скриптов.</span><span class="sxs-lookup"><span data-stu-id="5e064-234">Otherwise, select one of hello provided scripts.</span></span> |
    | <span data-ttu-id="5e064-235">Имя</span><span class="sxs-lookup"><span data-stu-id="5e064-235">Name</span></span> |<span data-ttu-id="5e064-236">Укажите имя для действия сценария hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-236">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="5e064-237">URI bash-скрипта</span><span class="sxs-lookup"><span data-stu-id="5e064-237">Bash script URI</span></span> |<span data-ttu-id="5e064-238">Укажите сценарий toohello URI hello, вызванный toocustomize hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-238">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="5e064-239">Головной, рабочий или Zookeeper</span><span class="sxs-lookup"><span data-stu-id="5e064-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="5e064-240">Укажите узлы hello (**Head**, **рабочих**, или **ZooKeeper**) на какие hello настройки выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="5e064-240">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="5e064-241">Параметры</span><span class="sxs-lookup"><span data-stu-id="5e064-241">Parameters</span></span> |<span data-ttu-id="5e064-242">Укажите параметры hello, если это требуется для сценария hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-242">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="5e064-243">Используйте hello __сохранить этот скрипт__ tooensure входа, hello сценарий применяется во время операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="5e064-243">Use hello __Persist this script action__ entry tooensure that hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="5e064-244">Выберите __создать__ toosave hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="5e064-244">Select __Create__ toosave hello script.</span></span> <span data-ttu-id="5e064-245">Затем можно использовать __+ отправить новый__ tooadd другой сценарий.</span><span class="sxs-lookup"><span data-stu-id="5e064-245">You can then use __+ Submit new__ tooadd another script.</span></span>

    ![Несколько действий скриптов](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="5e064-247">Закончив добавление сценариев использования hello __выберите__ кнопку, а затем hello __Далее__ toohello tooreturn кнопку __Сводка кластера__ раздела.</span><span class="sxs-lookup"><span data-stu-id="5e064-247">When you are done adding scripts, use hello __Select__ button, and then hello __Next__ button tooreturn toohello __Cluster summary__ section.</span></span>

3. <span data-ttu-id="5e064-248">toocreate hello кластера, выберите __создать__ из hello __Сводка кластера__ выделения.</span><span class="sxs-lookup"><span data-stu-id="5e064-248">toocreate hello cluster, select __Create__ from hello __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="5e064-249">Использование действия сценария на основе шаблонов диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="5e064-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="5e064-250">Hello в примерах этого раздела показано, как toouse сценария действий с помощью шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5e064-250">hello examples in this section demonstrate how toouse script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="5e064-251">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="5e064-251">Before you begin</span></span>

* <span data-ttu-id="5e064-252">Сведения о настройке рабочей станции toorun командлеты HDInsight Powershell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5e064-252">For information about configuring a workstation toorun HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="5e064-253">Дополнительные сведения о toocreate шаблонов, см. раздел [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-253">For instructions on how toocreate templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="5e064-254">Сведения об использовании Azure PowerShell с Resource Manager см. в [этой статье](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="5e064-255">Создание кластеров с помощью действия скрипта</span><span class="sxs-lookup"><span data-stu-id="5e064-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="5e064-256">Скопируйте hello следующий шаблон tooa расположение на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5e064-256">Copy hello following template tooa location on your computer.</span></span> <span data-ttu-id="5e064-257">Этот шаблон устанавливает Giraph на hello headnodes и рабочих узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-257">This template installs Giraph on hello headnodes and worker nodes in hello cluster.</span></span> <span data-ttu-id="5e064-258">Можно также проверить допустимость шаблона JSON hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-258">You can also verify if hello JSON template is valid.</span></span> <span data-ttu-id="5e064-259">Вставьте содержимое шаблона в [JSONLint](http://jsonlint.com/) — интерактивное средство проверки JSON.</span><span class="sxs-lookup"><span data-stu-id="5e064-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

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
2. <span data-ttu-id="5e064-260">Запуск Azure PowerShell и вход в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="5e064-260">Start Azure PowerShell and Log in tooyour Azure account.</span></span> <span data-ttu-id="5e064-261">После предоставления учетных данных, hello команда возвращает сведения о вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5e064-261">After providing your credentials, hello command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="5e064-262">Если у вас несколько подписок, укажите идентификатор подписки hello нужно toouse для развертывания.</span><span class="sxs-lookup"><span data-stu-id="5e064-262">If you have multiple subscriptions, provide hello subscription ID you wish toouse for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="5e064-263">Можно использовать `Get-AzureRmSubscription` tooget список всех подписок, связанных с вашей учетной записи, включая идентификатор подписки hello для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="5e064-263">You can use `Get-AzureRmSubscription` tooget a list of all subscriptions associated with your account, which includes hello subscription ID for each one.</span></span>

4. <span data-ttu-id="5e064-264">Создайте группу ресурсов, если у вас нет существующей группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5e064-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="5e064-265">Укажите имя группы ресурсов hello и место, необходимое для решения hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-265">Provide hello name of hello resource group and location that you need for your solution.</span></span> <span data-ttu-id="5e064-266">Возвращается Сводка hello новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5e064-266">A summary of hello new resource group is returned.</span></span>

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

5. <span data-ttu-id="5e064-267">toocreate развертывания для группы ресурсов, запустите hello **New AzureRmResourceGroupDeployment** команду и укажите необходимые параметры hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-267">toocreate a deployment for your resource group, run hello **New-AzureRmResourceGroupDeployment** command and provide hello necessary parameters.</span></span> <span data-ttu-id="5e064-268">Параметры Hello hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="5e064-268">hello parameters include hello following data:</span></span>

    * <span data-ttu-id="5e064-269">имя развертывания;</span><span class="sxs-lookup"><span data-stu-id="5e064-269">A name for your deployment</span></span>
    * <span data-ttu-id="5e064-270">Hello имя группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="5e064-270">hello name of your resource group</span></span>
    * <span data-ttu-id="5e064-271">созданный шаблон toohello URL-адрес или путь Hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-271">hello path or URL toohello template you created.</span></span>

  <span data-ttu-id="5e064-272">Если для вашего шаблона требуются какие-либо параметры, необходимо также передать их.</span><span class="sxs-lookup"><span data-stu-id="5e064-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="5e064-273">В этом случае tooinstall действие hello сценария R в кластере hello параметры не требуются.</span><span class="sxs-lookup"><span data-stu-id="5e064-273">In this case, hello script action tooinstall R on hello cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="5e064-274">Используется запрос tooprovide значения для параметров hello, определенные в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-274">You are prompted tooprovide values for hello parameters defined in hello template.</span></span>

1. <span data-ttu-id="5e064-275">При развертывании группы ресурсов hello отображается сводка hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="5e064-275">When hello resource group has been deployed, a summary of hello deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="5e064-276">Если сбой развертывания, можно использовать следующие командлеты tooget сведения о сбоях hello hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-276">If your deployment fails, you can use hello following cmdlets tooget information about hello failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="5e064-277">Использование действия скрипта при создании кластера с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e064-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="5e064-278">В этом разделе мы используем hello [AzureRmHDInsightScriptAction добавить](https://msdn.microsoft.com/library/mt603527.aspx) сценариев tooinvoke командлет с помощью toocustomize действие сценария кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-278">In this section, we use hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts by using Script Action toocustomize a cluster.</span></span> <span data-ttu-id="5e064-279">Прежде чем продолжить, убедитесь, что вы установили и настроили Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e064-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="5e064-280">Сведения о настройке рабочей станции toorun командлеты HDInsight PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5e064-280">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="5e064-281">Hello следующий сценарий демонстрирует, каким образом tooapply действие скрипта, при создании кластера с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5e064-281">hello following script demonstrates how tooapply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="5e064-282">Он может занять несколько минут, перед созданием кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-282">It can take several minutes before hello cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="5e064-283">Используйте действие скрипта, во время создания кластера из hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5e064-283">Use a Script Action during cluster creation from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="5e064-284">Hello HDInsight .NET SDK предоставляет клиентские библиотеки, делает его проще toowork с HDInsight из приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="5e064-284">hello HDInsight .NET SDK provides client libraries that makes it easier toowork with HDInsight from a .NET application.</span></span> <span data-ttu-id="5e064-285">Пример кода см. в разделе [под управлением Linux, создание кластеров HDInsight с помощью hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="5e064-285">For a code sample, see [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-tooa-running-cluster"></a><span data-ttu-id="5e064-286">Применить действие сценария tooa под управлением кластера</span><span class="sxs-lookup"><span data-stu-id="5e064-286">Apply a Script Action tooa running cluster</span></span>

<span data-ttu-id="5e064-287">В этом разделе рассказано, как tooapply скрипт действия tooa под управлением кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-287">In this section, learn how tooapply script actions tooa running cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a><span data-ttu-id="5e064-288">Применить действие сценария tooa под управлением кластера из hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5e064-288">Apply a Script Action tooa running cluster from hello Azure portal</span></span>

1. <span data-ttu-id="5e064-289">Из hello [портал Azure](https://portal.azure.com), выберите кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e064-289">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="5e064-290">Обзор кластера HDInsight hello, выберите hello **действия скрипта** плитки.</span><span class="sxs-lookup"><span data-stu-id="5e064-290">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Элемент "Действия сценариев"](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="5e064-292">Можно также выбрать **все параметры** , а затем выберите **действия скрипта** из hello в разделе "Параметры".</span><span class="sxs-lookup"><span data-stu-id="5e064-292">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

3. <span data-ttu-id="5e064-293">С помощью hello hello раздел действия скрипта, выберите **отправить новый**.</span><span class="sxs-lookup"><span data-stu-id="5e064-293">From hello top of hello Script Actions section, select **Submit new**.</span></span>

    ![Добавить скрипт tooa под управлением кластера](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="5e064-295">Используйте hello __выберите сценарий__ tooselect входа готового скрипта.</span><span class="sxs-lookup"><span data-stu-id="5e064-295">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="5e064-296">toouse пользовательского скрипта, выберите __пользовательские__ и укажите hello __имя__ и __Bash универсальный код Ресурса скрипта__ для своего сценария.</span><span class="sxs-lookup"><span data-stu-id="5e064-296">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Добавить скрипт в виде выберите сценария hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="5e064-298">Привет, в следующей таблице описываются элементы hello в форме hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-298">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="5e064-299">Свойство</span><span class="sxs-lookup"><span data-stu-id="5e064-299">Property</span></span> | <span data-ttu-id="5e064-300">Значение</span><span class="sxs-lookup"><span data-stu-id="5e064-300">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5e064-301">Выберите скрипт</span><span class="sxs-lookup"><span data-stu-id="5e064-301">Select a script</span></span> | <span data-ttu-id="5e064-302">toouse собственный сценарий, выберите __пользовательские__.</span><span class="sxs-lookup"><span data-stu-id="5e064-302">toouse your own script, select __custom__.</span></span> <span data-ttu-id="5e064-303">В противном случае выберите предоставленный скрипт.</span><span class="sxs-lookup"><span data-stu-id="5e064-303">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="5e064-304">Имя</span><span class="sxs-lookup"><span data-stu-id="5e064-304">Name</span></span> |<span data-ttu-id="5e064-305">Укажите имя для действия сценария hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-305">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="5e064-306">URI bash-скрипта</span><span class="sxs-lookup"><span data-stu-id="5e064-306">Bash script URI</span></span> |<span data-ttu-id="5e064-307">Укажите сценарий toohello URI hello, вызванный toocustomize hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-307">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="5e064-308">Головной, рабочий или Zookeeper</span><span class="sxs-lookup"><span data-stu-id="5e064-308">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="5e064-309">Укажите узлы hello (**Head**, **рабочих**, или **ZooKeeper**) на какие hello настройки выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="5e064-309">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="5e064-310">Параметры</span><span class="sxs-lookup"><span data-stu-id="5e064-310">Parameters</span></span> |<span data-ttu-id="5e064-311">Укажите параметры hello, если это требуется для сценария hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-311">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="5e064-312">Используйте hello __сохранить этот скрипт__ убедиться, что скрипт hello запись toomake применяется во время операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="5e064-312">Use hello __Persist this script action__ entry toomake sure hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="5e064-313">Наконец, используйте hello **создать** кнопку tooapply hello сценария toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-313">Finally, use hello **Create** button tooapply hello script toohello cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a><span data-ttu-id="5e064-314">Применить действие сценария tooa под управлением кластера из Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e064-314">Apply a Script Action tooa running cluster from Azure PowerShell</span></span>

<span data-ttu-id="5e064-315">Прежде чем продолжить, убедитесь, что вы установили и настроили Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e064-315">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="5e064-316">Сведения о настройке рабочей станции toorun командлеты HDInsight PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5e064-316">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="5e064-317">Hello следующем примере показано, как tooapply действие сценария tooa запущенному кластеру:</span><span class="sxs-lookup"><span data-stu-id="5e064-317">hello following example demonstrates how tooapply a script action tooa running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="5e064-318">После завершения операции hello, появится примерно toohello сведения после текста:</span><span class="sxs-lookup"><span data-stu-id="5e064-318">Once hello operation completes, you receive information similar toohello following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a><span data-ttu-id="5e064-319">Применить действие сценария tooa под управлением кластера из hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e064-319">Apply a Script Action tooa running cluster from hello Azure CLI</span></span>

<span data-ttu-id="5e064-320">Прежде чем продолжить, убедитесь, что был установлен и настроен hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5e064-320">Before proceeding, make sure you have installed and configured hello Azure CLI.</span></span> <span data-ttu-id="5e064-321">Дополнительные сведения см. в разделе [Install hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-321">For more information, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="5e064-322">tooswitch tooAzure режим диспетчера ресурсов, используйте следующую команду в командной строке hello hello:</span><span class="sxs-lookup"><span data-stu-id="5e064-322">tooswitch tooAzure Resource Manager mode, use hello following command at hello command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="5e064-323">Используйте hello, следуя tooauthenticate tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="5e064-323">Use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="5e064-324">Используйте следующие команды tooapply tooa действие скрипта под управлением кластера hello</span><span class="sxs-lookup"><span data-stu-id="5e064-324">Use hello following command tooapply a script action tooa running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="5e064-325">Если параметры для этой команды не заданы, вам будет предложено сделать это.</span><span class="sxs-lookup"><span data-stu-id="5e064-325">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="5e064-326">Если hello указывается с помощью сценария `-u` принимает параметры, можно указать их с помощью hello `-p` параметра.</span><span class="sxs-lookup"><span data-stu-id="5e064-326">If hello script you specify with `-u` accepts parameters, you can specify them using hello `-p` parameter.</span></span>

    <span data-ttu-id="5e064-327">Допустимые типы узлов: `headnode`, `workernode` и `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="5e064-327">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="5e064-328">Если скрипт hello должен быть применен toomultiple типы узлов, задавать типы hello, разделенных «;».</span><span class="sxs-lookup"><span data-stu-id="5e064-328">If hello script should be applied toomultiple node types, specify hello types separated by a ';'.</span></span> <span data-ttu-id="5e064-329">Например, `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="5e064-329">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="5e064-330">toopersist Здравствуйте сценария, добавьте hello `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="5e064-330">toopersist hello script, add hello `--persistOnSuccess`.</span></span> <span data-ttu-id="5e064-331">Также можно сохранить скрипт hello позже с помощью `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="5e064-331">You can also persist hello script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="5e064-332">После завершения задания hello, появится примерно toohello выходных данных после текста:</span><span class="sxs-lookup"><span data-stu-id="5e064-332">Once hello job completes, you receive output similar toohello following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a><span data-ttu-id="5e064-333">Применить действие сценария tooa под управлением кластера с помощью API-интерфейса REST</span><span class="sxs-lookup"><span data-stu-id="5e064-333">Apply a Script Action tooa running cluster using REST API</span></span>

<span data-ttu-id="5e064-334">См. статью [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx) (Выполнение действий скрипта в работающем кластере).</span><span class="sxs-lookup"><span data-stu-id="5e064-334">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="5e064-335">Применить действие сценария tooa под управлением кластера из hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5e064-335">Apply a Script Action tooa running cluster from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="5e064-336">Пример использования hello .NET SDK tooapply сценариев tooa кластера см. в разделе [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="5e064-336">For an example of using hello .NET SDK tooapply scripts tooa cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="5e064-337">Просмотр журнала и изменения типа действий скриптов</span><span class="sxs-lookup"><span data-stu-id="5e064-337">View history, promote, and demote Script Actions</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="5e064-338">С помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="5e064-338">Using hello Azure portal</span></span>

1. <span data-ttu-id="5e064-339">Из hello [портал Azure](https://portal.azure.com), выберите кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e064-339">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="5e064-340">Обзор кластера HDInsight hello, выберите hello **действия скрипта** плитки.</span><span class="sxs-lookup"><span data-stu-id="5e064-340">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Элемент "Действия сценариев"](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="5e064-342">Можно также выбрать **все параметры** , а затем выберите **действия скрипта** из hello в разделе "Параметры".</span><span class="sxs-lookup"><span data-stu-id="5e064-342">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

4. <span data-ttu-id="5e064-343">Журнал скриптов для этого кластера отображается на hello разделе действий скрипта.</span><span class="sxs-lookup"><span data-stu-id="5e064-343">A history of scripts for this cluster is displayed on hello Script Actions section.</span></span> <span data-ttu-id="5e064-344">Эти сведения включают в себя список сохраняемых скриптов.</span><span class="sxs-lookup"><span data-stu-id="5e064-344">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="5e064-345">Hello снимке вы увидите, что hello Solr был скрипт запуска в этом кластере.</span><span class="sxs-lookup"><span data-stu-id="5e064-345">In hello screenshot below, you can see that hello Solr script has been ran on this cluster.</span></span> <span data-ttu-id="5e064-346">Снимок экрана приветствия не показывает все сохраненные сценарии.</span><span class="sxs-lookup"><span data-stu-id="5e064-346">hello screenshot does not show any persisted scripts.</span></span>

    ![Раздел "Действия скриптов"](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="5e064-348">При выборе сценарий из журнала hello отображаются hello разделе "Свойства" для этого скрипта.</span><span class="sxs-lookup"><span data-stu-id="5e064-348">Selecting a script from hello history displays hello Properties section for this script.</span></span> <span data-ttu-id="5e064-349">С помощью hello в верхней части экрана приветствия можно снова запустить сценарий hello или повысить его уровень.</span><span class="sxs-lookup"><span data-stu-id="5e064-349">From hello top of hello screen, you can rerun hello script or promote it.</span></span>

    ![Раздел "Свойства действий скрипта"](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="5e064-351">Можно также использовать hello **...**  toohello справа от записи в раздел tooperform hello действия скрипта действий.</span><span class="sxs-lookup"><span data-stu-id="5e064-351">You can also use hello **...** toohello right of entries on hello Script Actions section tooperform actions.</span></span>

    ![Использование действий скриптов](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="5e064-353">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e064-353">Using Azure PowerShell</span></span>

| <span data-ttu-id="5e064-354">Используйте следующие hello:</span><span class="sxs-lookup"><span data-stu-id="5e064-354">Use hello following...</span></span> | <span data-ttu-id="5e064-355">слишком...</span><span class="sxs-lookup"><span data-stu-id="5e064-355">too...</span></span> |
| --- | --- |
| <span data-ttu-id="5e064-356">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="5e064-356">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="5e064-357">Получение сведений о действиях сохраняемого скрипта</span><span class="sxs-lookup"><span data-stu-id="5e064-357">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="5e064-358">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="5e064-358">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="5e064-359">Получить журнал сценария действия, применяемые toohello кластера или сведений для конкретных сценариев</span><span class="sxs-lookup"><span data-stu-id="5e064-359">Retrieve a history of script actions applied toohello cluster, or details for a specific script</span></span> |
| <span data-ttu-id="5e064-360">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="5e064-360">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="5e064-361">Повышает уровень нерегламентированным tooa действие сценария сохраняются действие сценария</span><span class="sxs-lookup"><span data-stu-id="5e064-361">Promotes an ad hoc script action tooa persisted script action</span></span> |
| <span data-ttu-id="5e064-362">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="5e064-362">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="5e064-363">Можно понизить уровень сохраненный скрипт действие нерегламентированных action tooan</span><span class="sxs-lookup"><span data-stu-id="5e064-363">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="5e064-364">С помощью `Remove-AzureRmHDInsightPersistedScriptAction` не отменяет hello действия, выполняемые с помощью сценария.</span><span class="sxs-lookup"><span data-stu-id="5e064-364">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="5e064-365">Этот командлет удаляет только флаг материализованный hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-365">This cmdlet only removes hello persisted flag.</span></span>

<span data-ttu-id="5e064-366">Hello следующий пример сценария демонстрирует использование командлетов toopromote hello, а затем понижение уровня скрипта.</span><span class="sxs-lookup"><span data-stu-id="5e064-366">hello following example script demonstrates using hello cmdlets toopromote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a><span data-ttu-id="5e064-367">С помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e064-367">Using hello Azure CLI</span></span>

| <span data-ttu-id="5e064-368">Используйте следующие hello:</span><span class="sxs-lookup"><span data-stu-id="5e064-368">Use hello following...</span></span> | <span data-ttu-id="5e064-369">слишком...</span><span class="sxs-lookup"><span data-stu-id="5e064-369">too...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="5e064-370">Получение списка сохраняемых действий сценария</span><span class="sxs-lookup"><span data-stu-id="5e064-370">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="5e064-371">Получение сведений о конкретном сохраняемом действии сценария</span><span class="sxs-lookup"><span data-stu-id="5e064-371">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="5e064-372">Получить журнал кластера toohello действия, применяемые для сценария</span><span class="sxs-lookup"><span data-stu-id="5e064-372">Retrieve a history of script actions applied toohello cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="5e064-373">Получение сведений о конкретном действии сценария</span><span class="sxs-lookup"><span data-stu-id="5e064-373">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="5e064-374">Повышает уровень нерегламентированным tooa действие сценария сохраняются действие сценария</span><span class="sxs-lookup"><span data-stu-id="5e064-374">Promotes an ad hoc script action tooa persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="5e064-375">Можно понизить уровень сохраненный скрипт действие нерегламентированных action tooan</span><span class="sxs-lookup"><span data-stu-id="5e064-375">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="5e064-376">С помощью `azure hdinsight script-action persisted delete` не отменяет hello действия, выполняемые с помощью сценария.</span><span class="sxs-lookup"><span data-stu-id="5e064-376">Using `azure hdinsight script-action persisted delete` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="5e064-377">Этот командлет удаляет только флаг материализованный hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-377">This cmdlet only removes hello persisted flag.</span></span>

### <a name="using-hello-hdinsight-net-sdk"></a><span data-ttu-id="5e064-378">С помощью hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5e064-378">Using hello HDInsight .NET SDK</span></span>

<span data-ttu-id="5e064-379">Пример использования журнал hello .NET SDK tooretrieve скриптов из кластера, повысить или понизить уровень скриптов см. в разделе [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="5e064-379">For an example of using hello .NET SDK tooretrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="5e064-380">Этот пример также демонстрирует, как приложение HDInsight с помощью tooinstall hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5e064-380">This example also demonstrates how tooinstall an HDInsight application using hello .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="5e064-381">Поддержка программного обеспечения с открытым исходным кодом, используемого в кластере HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e064-381">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="5e064-382">Hello Microsoft Azure HDInsight service использует экосистему технологий открытым исходным кодом, сформированный вокруг Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5e064-382">hello Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="5e064-383">Microsoft Azure предоставляет общий уровень поддержки для технологий с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="5e064-383">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="5e064-384">Дополнительные сведения см. в разделе hello **области поддержки** раздел hello [ответы поддержки Azure веб-сайт](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="5e064-384">For more information, see hello **Support Scope** section of hello [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="5e064-385">Hello службы HDInsight обеспечивает дополнительный уровень поддержки встроенных компонентов.</span><span class="sxs-lookup"><span data-stu-id="5e064-385">hello HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="5e064-386">Существует два типа компонентов открытым исходным кодом, доступных в hello службы HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5e064-386">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="5e064-387">**Встроенные компоненты** -эти компоненты предустановлен в кластерах HDInsight и предоставляют основные функциональные возможности кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-387">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="5e064-388">Например YARN ResourceManager, язык запросов Hive hello (HiveQL) и библиотеку Mahout hello принадлежать toothis категории.</span><span class="sxs-lookup"><span data-stu-id="5e064-388">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="5e064-389">Полный список компонентов кластера доступен в [новые возможности, предоставляемые HDInsight версиями кластеров Hadoop hello](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-389">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="5e064-390">**Пользовательские компоненты** -, как пользователь кластера hello, можно установить или использовать любой компонент, доступные в сообществе hello или созданный вами в рабочей нагрузке.</span><span class="sxs-lookup"><span data-stu-id="5e064-390">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="5e064-391">Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="5e064-391">Components provided with hello HDInsight cluster are fully supported.</span></span> <span data-ttu-id="5e064-392">Службу технической поддержки Майкрософт помогает tooisolate и разрешить проблемы toothese связанные компоненты.</span><span class="sxs-lookup"><span data-stu-id="5e064-392">Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="5e064-393">Пользовательские компоненты получают toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-393">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="5e064-394">Службу технической поддержки Майкрософт может быть проблемой может tooresolve hello или они может попросить вас tooengage доступных каналов для hello открытых технологий, которых находится глубокие знания для данной технологии.</span><span class="sxs-lookup"><span data-stu-id="5e064-394">Microsoft support may be able tooresolve hello issue OR they may ask you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="5e064-395">Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).</span><span class="sxs-lookup"><span data-stu-id="5e064-395">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="5e064-396">Служба HDInsight Hello предоставляет несколько способов toouse пользовательские компоненты.</span><span class="sxs-lookup"><span data-stu-id="5e064-396">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="5e064-397">Hello же уровнем поддержки применяется независимо от того, как компонент используется, или установлен на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-397">hello same level of support applies, regardless of how a component is used or installed on hello cluster.</span></span> <span data-ttu-id="5e064-398">Hello следующий список описывает hello наиболее распространенными способами, что пользовательские компоненты можно использовать в кластерах HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5e064-398">hello following list describes hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="5e064-399">Отправки заданий - Hadoop или других типов заданий, обрабатываемых или использовать пользовательские компоненты может быть отправлено toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-399">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>

2. <span data-ttu-id="5e064-400">Настройка кластера - во время создания кластера можно указать дополнительные параметры и пользовательские компоненты, установленные на узлах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-400">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on hello cluster nodes.</span></span>

3. <span data-ttu-id="5e064-401">Примеры — для популярных пользовательские компоненты, корпорация Майкрософт и другие могут предоставлять примеры использования этих компонентов в кластерах HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-401">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="5e064-402">Эти примеры представляются без поддержки.</span><span class="sxs-lookup"><span data-stu-id="5e064-402">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5e064-403">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="5e064-403">Troubleshooting</span></span>

<span data-ttu-id="5e064-404">Можно использовать tooview Ambari web пользовательского интерфейса информация, зарегистрированная службой действий скрипта.</span><span class="sxs-lookup"><span data-stu-id="5e064-404">You can use Ambari web UI tooview information logged by script actions.</span></span> <span data-ttu-id="5e064-405">При сбое во время создания кластера скрипт hello hello журналы также доступны в учетной записи хранения по умолчанию hello связанные с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-405">If hello script fails during cluster creation, hello logs are also available in hello default storage account associated with hello cluster.</span></span> <span data-ttu-id="5e064-406">Информация о как tooretrieve hello журналов с помощью обоих этих параметров.</span><span class="sxs-lookup"><span data-stu-id="5e064-406">This section provides information on how tooretrieve hello logs using both these options.</span></span>

### <a name="using-hello-ambari-web-ui"></a><span data-ttu-id="5e064-407">С помощью hello Ambari веб-интерфейса</span><span class="sxs-lookup"><span data-stu-id="5e064-407">Using hello Ambari Web UI</span></span>

1. <span data-ttu-id="5e064-408">В браузере перейдите toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="5e064-408">In your browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="5e064-409">Замените ИМЯ_КЛАСТЕРА hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e064-409">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="5e064-410">При появлении запроса введите имя учетной записи администратора hello (администратор) и пароль для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-410">When prompted, enter hello admin account name (admin) and password for hello cluster.</span></span> <span data-ttu-id="5e064-411">В веб-формы могут содержаться учетных данных администратора tooreenter hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-411">You may have tooreenter hello admin credentials in a web form.</span></span>

2. <span data-ttu-id="5e064-412">На панели hello вверху hello страницы приветствия выберите hello **ops** входа.</span><span class="sxs-lookup"><span data-stu-id="5e064-412">From hello bar at hello top of hello page, select hello **ops** entry.</span></span> <span data-ttu-id="5e064-413">Отображается список текущих и предыдущих операций, выполняемых на hello кластера с помощью Ambari.</span><span class="sxs-lookup"><span data-stu-id="5e064-413">A list of current and previous operations performed on hello cluster through Ambari is displayed.</span></span>

    ![Веб-панель Ambari с выбранной записью ops](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="5e064-415">Поиск записей hello, имеющих **запуска\_customscriptaction** в hello **операции** столбца.</span><span class="sxs-lookup"><span data-stu-id="5e064-415">Find hello entries that have **run\_customscriptaction** in hello **Operations** column.</span></span> <span data-ttu-id="5e064-416">Эти записи создаются при запуске действия скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-416">These entries are created when hello Script Actions run.</span></span>

    ![Снимок экрана операций](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="5e064-418">tooview hello STDOUT и STDERR выходных данных, выберите элемент run\customscriptaction hello и прокрутите вниз список ссылок hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-418">tooview hello STDOUT and STDERR output, select hello run\customscriptaction entry and drill down through hello links.</span></span> <span data-ttu-id="5e064-419">Этот выход создается при запуске сценария hello и может содержать полезные сведения.</span><span class="sxs-lookup"><span data-stu-id="5e064-419">This output is generated when hello script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-hello-default-storage-account"></a><span data-ttu-id="5e064-420">Журналы событий из учетной записи хранения по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="5e064-420">Access logs from hello default storage account</span></span>

<span data-ttu-id="5e064-421">Сбой создания кластера hello из-за ошибки действие сценария tooa журналы hello может осуществляться из учетной записи хранилища кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-421">If hello cluster creation fails due tooa script action error, hello logs can be accessed from hello cluster storage account.</span></span>

* <span data-ttu-id="5e064-422">Hello журналы хранения можно найти по адресу `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="5e064-422">hello storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Снимок экрана операций](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="5e064-424">В этом каталоге журналы hello организована отдельно для головному узлу, workernode и zookeeper узлов.</span><span class="sxs-lookup"><span data-stu-id="5e064-424">Under this directory, hello logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="5e064-425">Ниже приведены некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="5e064-425">Some examples are:</span></span>

    * <span data-ttu-id="5e064-426">**Головной узел:** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="5e064-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="5e064-427">**Рабочий узел** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="5e064-427">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="5e064-428">**Узел Zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="5e064-428">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="5e064-429">Все потоки stdout и stderr hello соответствующего узла будет отправлен toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="5e064-429">All stdout and stderr of hello corresponding host is uploaded toohello storage account.</span></span> <span data-ttu-id="5e064-430">Для каждого действия скрипта создается файл **output-\*.txt** и файл **errors-\*.txt**.</span><span class="sxs-lookup"><span data-stu-id="5e064-430">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="5e064-431">Hello *.txt выходной файл содержит сведения о hello URI hello скрипта, который получен работать на узле hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-431">hello output-*.txt file contains information about hello URI of hello script that got run on hello host.</span></span> <span data-ttu-id="5e064-432">Например:</span><span class="sxs-lookup"><span data-stu-id="5e064-432">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="5e064-433">Можно повторно создать кластер действие сценария с hello таким же именем.</span><span class="sxs-lookup"><span data-stu-id="5e064-433">It's possible that you repeatedly create a script action cluster with hello same name.</span></span> <span data-ttu-id="5e064-434">В этом случае можно отличить hello журналы на основе имени папки hello даты.</span><span class="sxs-lookup"><span data-stu-id="5e064-434">In such case, you can distinguish hello relevant logs based on hello DATE folder name.</span></span> <span data-ttu-id="5e064-435">Например hello структуру папок для кластера (mycluster), созданные в разное время выглядит примерно toohello следующие записи журнала:</span><span class="sxs-lookup"><span data-stu-id="5e064-435">For example, hello folder structure for a cluster (mycluster) created on different dates appears similar toohello following log entries:</span></span>

    <span data-ttu-id="5e064-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="5e064-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="5e064-437">При создании кластера действие сценария с hello одинаковые имена на hello же день, можно использовать hello уникальный префикс tooidentify hello требуемых файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="5e064-437">If you create a script action cluster with hello same name on hello same day, you can use hello unique prefix tooidentify hello relevant log files.</span></span>

* <span data-ttu-id="5e064-438">При создании кластера рядом с 12:00 (полночь), возможно, файлы журнала hello охватывать два дня.</span><span class="sxs-lookup"><span data-stu-id="5e064-438">If you create a cluster near 12:00AM (midnight), it's possible that hello log files span across two days.</span></span> <span data-ttu-id="5e064-439">В таких случаях вы видите две папки другую дату hello одного кластера.</span><span class="sxs-lookup"><span data-stu-id="5e064-439">In such cases, you see two different date folders for hello same cluster.</span></span>

* <span data-ttu-id="5e064-440">Отправка контейнер по умолчанию toohello файлов журнала может занять too5 минут, особенно для больших кластеров.</span><span class="sxs-lookup"><span data-stu-id="5e064-440">Uploading log files toohello default container can take up too5 mins, especially for large clusters.</span></span> <span data-ttu-id="5e064-441">Таким образом Если требуется, чтобы журналы hello tooaccess, не следует удалять немедленно hello кластера при сбое действия сценария.</span><span class="sxs-lookup"><span data-stu-id="5e064-441">So, if you want tooaccess hello logs, you should not immediately delete hello cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="5e064-442">Модуль наблюдения Ambari</span><span class="sxs-lookup"><span data-stu-id="5e064-442">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="5e064-443">Не меняйте пароль hello для hello контрольного Ambari (hdinsightwatchdog) в кластере HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="5e064-443">Do not change hello password for hello Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5e064-444">Hello при смене пароля для этой учетной записи прерывается hello возможность toorun новые действия, сценарий на кластер HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-444">Changing hello password for this account breaks hello ability toorun new script actions on hello HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="5e064-445">Не удается импортировать BlobService имени</span><span class="sxs-lookup"><span data-stu-id="5e064-445">Can't import name BlobService</span></span>

<span data-ttu-id="5e064-446">__Симптомы__: hello сбоя действия сценария.</span><span class="sxs-lookup"><span data-stu-id="5e064-446">__Symptoms__: hello script action fails.</span></span> <span data-ttu-id="5e064-447">Аналогичные toohello текст следующая ошибка отображается при просмотре hello операции в Ambari:</span><span class="sxs-lookup"><span data-stu-id="5e064-447">Text similar toohello following error is displayed when you view hello operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="5e064-448">__Причина__: Эта ошибка возникает при обновлении клиента hello хранилища Azure Python, который входит в состав кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5e064-448">__Cause__: This error occurs if you upgrade hello Python Azure Storage client that is included with hello HDInsight cluster.</span></span> <span data-ttu-id="5e064-449">HDInsight требуется клиент службы хранилища Azure версии 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="5e064-449">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="5e064-450">__Разрешение__: tooresolve эту ошибку, установить соединение вручную tooeach узла кластера с помощью `ssh` и используйте hello следующая версия клиента правильного хранения hello tooreinstall команды:</span><span class="sxs-lookup"><span data-stu-id="5e064-450">__Resolution__: tooresolve this error, manually connect tooeach cluster node using `ssh` and use hello following command tooreinstall hello correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="5e064-451">Сведения о подключении toohello кластера с помощью SSH. в разделе [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5e064-451">For information on connecting toohello cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="5e064-452">Журнал не отображает скрипты, используемые во время создания кластера</span><span class="sxs-lookup"><span data-stu-id="5e064-452">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="5e064-453">Если кластер создан до 15 марта 2016 г., в журнале действий скриптов могут отсутствовать записи.</span><span class="sxs-lookup"><span data-stu-id="5e064-453">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="5e064-454">Если изменить размер кластера hello после 15 марта 2016 г., hello сценариев во время создания кластера отображаются в журнал как они применяются toonew узлов в кластере hello как часть hello операцию изменения размера.</span><span class="sxs-lookup"><span data-stu-id="5e064-454">If you resize hello cluster after March 15, 2016, hello scripts using during cluster creation appear in history as they are applied toonew nodes in hello cluster as part of hello resize operation.</span></span>

<span data-ttu-id="5e064-455">Есть два исключения.</span><span class="sxs-lookup"><span data-stu-id="5e064-455">There are two exceptions:</span></span>

* <span data-ttu-id="5e064-456">Если кластер создан до 1 сентября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="5e064-456">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="5e064-457">Это дата добавления действий скриптов.</span><span class="sxs-lookup"><span data-stu-id="5e064-457">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="5e064-458">Если кластер был создан раньше, действия скриптов не могли использоваться при его создании.</span><span class="sxs-lookup"><span data-stu-id="5e064-458">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="5e064-459">Если используется несколько действий скрипта во время создания кластера и использовать hello же имя для нескольких сценариев или hello одинаковые имена, одному URI, но различные параметры для нескольких сценариев.</span><span class="sxs-lookup"><span data-stu-id="5e064-459">If you used multiple Script Actions during cluster creation, and used hello same name for multiple scripts, or hello same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="5e064-460">В этих случаях появляется hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="5e064-460">In these cases, you receive hello following error:</span></span>

    <span data-ttu-id="5e064-461">Нет новый скрипт действия может быть выполнена для этого кластера из-за tooconflicting имен сценария в существующих скриптов.</span><span class="sxs-lookup"><span data-stu-id="5e064-461">No new script actions can be ran on this cluster due tooconflicting script names in existing scripts.</span></span> <span data-ttu-id="5e064-462">Имена скриптов, указанные при создании кластера, должны быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="5e064-462">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="5e064-463">Существующие скрипты выполняются при изменении размера.</span><span class="sxs-lookup"><span data-stu-id="5e064-463">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e064-464">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e064-464">Next steps</span></span>

* [<span data-ttu-id="5e064-465">Разработка скриптов действия сценария для HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e064-465">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="5e064-466">Установка и использование Solr в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e064-466">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="5e064-467">Установка и использование Giraph в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e064-467">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="5e064-468">Добавление дополнительного хранилища кластера HDInsight tooan</span><span class="sxs-lookup"><span data-stu-id="5e064-468">Add additional storage tooan HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Этапы создания кластера"
