---
title: "aaaRestrict доступ с помощью подписанных URL - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toorestrict подписей общего доступа toouse HDInsight доступ к toodata хранится в BLOB-объектов хранилища Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a><span data-ttu-id="df331-103">Использование подписей общего доступа Azure хранилища toorestrict доступа toodata в HDInsight</span><span class="sxs-lookup"><span data-stu-id="df331-103">Use Azure Storage Shared Access Signatures toorestrict access toodata in HDInsight</span></span>

<span data-ttu-id="df331-104">HDInsight имеет полный доступ toodata в учетных записях хранения Azure hello, связанные с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="df331-104">HDInsight has full access toodata in hello Azure Storage accounts associated with hello cluster.</span></span> <span data-ttu-id="df331-105">Подписанные URL-адреса можно использовать на toohello hello BLOB-объектов контейнера toorestrict доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="df331-105">You can use Shared Access Signatures on hello blob container toorestrict access toohello data.</span></span> <span data-ttu-id="df331-106">Например tooprovide данные toohello доступ только для чтения.</span><span class="sxs-lookup"><span data-stu-id="df331-106">For example, tooprovide read-only access toohello data.</span></span> <span data-ttu-id="df331-107">Подписи общего доступа (SAS) являются возможностью учетных записей хранилища Azure, которая позволяет вам toodata toolimit доступа.</span><span class="sxs-lookup"><span data-stu-id="df331-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you toolimit access toodata.</span></span> <span data-ttu-id="df331-108">Например предоставляя toodata доступ только для чтения.</span><span class="sxs-lookup"><span data-stu-id="df331-108">For example, providing read-only access toodata.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df331-109">Чтобы создать решение на основе Apache Ranger, попробуйте использовать HDInsight, присоединенный к домену.</span><span class="sxs-lookup"><span data-stu-id="df331-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="df331-110">Дополнительные сведения см. в разделе hello [настройки присоединенных к домену HDInsight](hdinsight-domain-joined-configure.md) документа.</span><span class="sxs-lookup"><span data-stu-id="df331-110">For more information, see hello [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="df331-111">HDInsight должны иметь полный доступ toohello по умолчанию хранилища для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="df331-111">HDInsight must have full access toohello default storage for hello cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="df331-112">Требования</span><span class="sxs-lookup"><span data-stu-id="df331-112">Requirements</span></span>

* <span data-ttu-id="df331-113">Подписка Azure</span><span class="sxs-lookup"><span data-stu-id="df331-113">An Azure subscription</span></span>
* <span data-ttu-id="df331-114">C# или Python.</span><span class="sxs-lookup"><span data-stu-id="df331-114">C# or Python.</span></span> <span data-ttu-id="df331-115">Пример кода на C# предоставлен в решении Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="df331-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="df331-116">Требуется Visual Studio версии 2013, 2015 или 2017.</span><span class="sxs-lookup"><span data-stu-id="df331-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="df331-117">Требуется Python версии 2.7 или более новой.</span><span class="sxs-lookup"><span data-stu-id="df331-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="df331-118">Кластер HDInsight под управлением Linux или [Azure PowerShell] [ powershell] -при наличии существующего кластера под управлением Linux, можно использовать Ambari tooadd кластера toohello подписи общего доступа.</span><span class="sxs-lookup"><span data-stu-id="df331-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari tooadd a Shared Access Signature toohello cluster.</span></span> <span data-ttu-id="df331-119">В противном случае можно использовать Azure PowerShell toocreate кластер и добавить подпись общего доступа во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="df331-119">If not, you can use Azure PowerShell toocreate a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="df331-120">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="df331-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="df331-121">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="df331-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="df331-122">Здравствуйте, файлы примеров из [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="df331-122">hello example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="df331-123">Этот репозиторий содержит hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="df331-123">This repository contains hello following items:</span></span>

  * <span data-ttu-id="df331-124">Проект Visual Studio, способный создать контейнер хранилища, хранимую политику и SAS для использования с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df331-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="df331-125">Сценарий Python, способный создать контейнер хранилища, хранимую политику и SAS для использования с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df331-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="df331-126">Сценарий PowerShell, можно создать HDInsight кластера и настроить его toouse hello SAS.</span><span class="sxs-lookup"><span data-stu-id="df331-126">A PowerShell script that can create a HDInsight cluster and configure it toouse hello SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="df331-127">Подписи коллективного доступа</span><span class="sxs-lookup"><span data-stu-id="df331-127">Shared Access Signatures</span></span>

<span data-ttu-id="df331-128">Существуют две формы подписанных URL-адресов:</span><span class="sxs-lookup"><span data-stu-id="df331-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="df331-129">Нерегламентированный: hello время начала, время окончания и разрешения для hello SAS указаны на hello универсальный код Ресурса SAS.</span><span class="sxs-lookup"><span data-stu-id="df331-129">Ad hoc: hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span>

* <span data-ttu-id="df331-130">Хранимая политика доступа. Хранимая политика доступа определяется в контейнере ресурсов, например в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="df331-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="df331-131">Политики могут быть ограничения используемых toomanage для одного или нескольких подписей общего доступа.</span><span class="sxs-lookup"><span data-stu-id="df331-131">A policy can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="df331-132">При связывании подписанный URL-адрес с хранимой политикой доступа hello SAS наследует ограничения hello - hello время начала, время окончания и разрешения -, определенные для hello хранимые политики доступа.</span><span class="sxs-lookup"><span data-stu-id="df331-132">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span>

<span data-ttu-id="df331-133">Hello различия между hello двух форм являются важными для одного ключевого сценария: отзыва.</span><span class="sxs-lookup"><span data-stu-id="df331-133">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="df331-134">Подписанный URL-адрес является URL-адрес, поэтому любой пользователь получает hello SAS можно использовать, независимо от того, кто запросил toobegin с.</span><span class="sxs-lookup"><span data-stu-id="df331-134">A SAS is a URL, so anyone who obtains hello SAS can use it, regardless of who requested it toobegin with.</span></span> <span data-ttu-id="df331-135">Если открыто опубликована SAS, он может использоваться кем Здравствуй, мир!.</span><span class="sxs-lookup"><span data-stu-id="df331-135">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="df331-136">Распространяемая подпись общего доступа действительна до тех пор, пока не произойдет одно из четырех возможных событий:</span><span class="sxs-lookup"><span data-stu-id="df331-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="df331-137">Hello окончания времени, указанного на hello достижения SAS.</span><span class="sxs-lookup"><span data-stu-id="df331-137">hello expiry time specified on hello SAS is reached.</span></span>

2. <span data-ttu-id="df331-138">Hello срок действия указанного hello хранимой политике доступа, ссылается hello достижения SAS.</span><span class="sxs-lookup"><span data-stu-id="df331-138">hello expiry time specified on hello stored access policy referenced by hello SAS is reached.</span></span> <span data-ttu-id="df331-139">Hello следующие сценарии вызвать hello срок достигнут toobe:</span><span class="sxs-lookup"><span data-stu-id="df331-139">hello following scenarios cause hello expiry time toobe reached:</span></span>

    * <span data-ttu-id="df331-140">Hello время интервала времени.</span><span class="sxs-lookup"><span data-stu-id="df331-140">hello time interval has elapsed.</span></span>
    * <span data-ttu-id="df331-141">Hello хранимые политики доступа-измененный toohave время истечения срока действия в прошлом hello.</span><span class="sxs-lookup"><span data-stu-id="df331-141">hello stored access policy is modified toohave an expiry time in hello past.</span></span> <span data-ttu-id="df331-142">Изменение hello срок — один из способов toorevoke hello SAS.</span><span class="sxs-lookup"><span data-stu-id="df331-142">Changing hello expiry time is one way toorevoke hello SAS.</span></span>

3. <span data-ttu-id="df331-143">Hello хранимой политики доступа, ссылается hello удаляется SAS, который является другим способом toorevoke hello SAS.</span><span class="sxs-lookup"><span data-stu-id="df331-143">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="df331-144">При повторном создании hello хранимые политики доступа в hello точно такое же имя, все маркеры SAS для предыдущей политики hello действительны (если не прошел срок hello на hello SAS).</span><span class="sxs-lookup"><span data-stu-id="df331-144">If you recreate hello stored access policy with hello same name, all  SAS tokens for hello previous policy are valid (if hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="df331-145">Если предполагается toorevoke hello SAS, быть убедиться, что toouse другое имя при повторном создании hello политики доступа в будущем hello срока истечения срока действия.</span><span class="sxs-lookup"><span data-stu-id="df331-145">If you intend toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>

4. <span data-ttu-id="df331-146">ключ учетной записи Hello, используемые toocreate hello SAS повторно.</span><span class="sxs-lookup"><span data-stu-id="df331-146">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="df331-147">Идет повторное создание ключа hello в результате все приложения, использующие hello предыдущих toofail ключа, проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="df331-147">Regenerating hello key causes all applications that use hello previous key toofail authentication.</span></span> <span data-ttu-id="df331-148">Обновите все компоненты toohello новый ключ.</span><span class="sxs-lookup"><span data-stu-id="df331-148">Update all components toohello new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df331-149">URI подписи коллективного доступа связан с сигнатурой hello toocreate ключа используется учетная запись hello и hello связанных хранимой политики доступа (если таковые имеются).</span><span class="sxs-lookup"><span data-stu-id="df331-149">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="df331-150">Если хранимая политика доступа не указан, hello только способом toorevoke подписанный URL-адрес является ключ учетной записи toochange hello.</span><span class="sxs-lookup"><span data-stu-id="df331-150">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

<span data-ttu-id="df331-151">Рекомендуется всегда использовать хранимые политики доступа.</span><span class="sxs-lookup"><span data-stu-id="df331-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="df331-152">При использовании хранимых политик, можно отменить подписи или расширить hello даты истечения срока действия при необходимости.</span><span class="sxs-lookup"><span data-stu-id="df331-152">When using stored policies, you can either revoke signatures or extend hello expiry date as needed.</span></span> <span data-ttu-id="df331-153">Hello в данном пошаговом руководстве используется toogenerate политики доступа SAS.</span><span class="sxs-lookup"><span data-stu-id="df331-153">hello steps in this document use stored access policies toogenerate SAS.</span></span>

<span data-ttu-id="df331-154">Дополнительные сведения о подписей общего доступа см. в разделе [основные сведения о модели SAS hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="df331-154">For more information on Shared Access Signatures, see [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="df331-155">Создание хранимой политики и SAS с использованием C\#</span><span class="sxs-lookup"><span data-stu-id="df331-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="df331-156">Откройте решение hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="df331-156">Open hello solution in Visual Studio.</span></span>

2. <span data-ttu-id="df331-157">В обозревателе решений щелкните правой кнопкой мыши на hello **SASToken** проект и выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="df331-157">In Solution Explorer, right-click on hello **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="df331-158">Выберите **параметры** и добавьте значения для hello следующие записи:</span><span class="sxs-lookup"><span data-stu-id="df331-158">Select **Settings** and add values for hello following entries:</span></span>

   * <span data-ttu-id="df331-159">StorageConnectionString: hello строка соединения для hello хранилища учетной записи, которую toocreate хранимых политик и SAS для.</span><span class="sxs-lookup"><span data-stu-id="df331-159">StorageConnectionString: hello connection string for hello storage account that you want toocreate a stored policy and SAS for.</span></span> <span data-ttu-id="df331-160">Hello формат должен быть `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` где `myaccount` hello имя вашей учетной записи хранилища и `mykey` hello ключ для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="df331-160">hello format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is hello name of your storage account and `mykey` is hello key for hello storage account.</span></span>

   * <span data-ttu-id="df331-161">Имя контейнера: hello контейнер в учетной записи хранения hello, которым требуется доступ toorestrict.</span><span class="sxs-lookup"><span data-stu-id="df331-161">ContainerName: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="df331-162">SASPolicyName: hello toouse имя для hello хранятся toocreate политики.</span><span class="sxs-lookup"><span data-stu-id="df331-162">SASPolicyName: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="df331-163">FileToUpload: hello путь tooa файл, отправленный toohello контейнера.</span><span class="sxs-lookup"><span data-stu-id="df331-163">FileToUpload: hello path tooa file that is uploaded toohello container.</span></span>

4. <span data-ttu-id="df331-164">Запустите проект hello.</span><span class="sxs-lookup"><span data-stu-id="df331-164">Run hello project.</span></span> <span data-ttu-id="df331-165">После создания hello SAS, отображаются сведения аналогичные toohello после текста:</span><span class="sxs-lookup"><span data-stu-id="df331-165">Information similar toohello following text is displayed once hello SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="df331-166">Сохраните hello маркера политики SAS, имя учетной записи хранилища и имя контейнера.</span><span class="sxs-lookup"><span data-stu-id="df331-166">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="df331-167">Эти значения используются при связывании учетной записи хранилища hello с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df331-167">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="df331-168">Создание хранимой политики и SAS с использованием Python</span><span class="sxs-lookup"><span data-stu-id="df331-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="df331-169">Откройте файл SASToken.py hello и измените hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="df331-169">Open hello SASToken.py file and change hello following values:</span></span>

   * <span data-ttu-id="df331-170">политика\_name: hello toouse имя для hello хранимых toocreate политики.</span><span class="sxs-lookup"><span data-stu-id="df331-170">policy\_name: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="df331-171">хранилище\_учетной записи\_name: hello имя вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="df331-171">storage\_account\_name: hello name of your storage account.</span></span>

   * <span data-ttu-id="df331-172">хранилище\_учетной записи\_ключ: hello ключ учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="df331-172">storage\_account\_key: hello key for hello storage account.</span></span>

   * <span data-ttu-id="df331-173">хранилище\_контейнера\_name: hello контейнера в учетной записи хранения hello, которым требуется доступ toorestrict.</span><span class="sxs-lookup"><span data-stu-id="df331-173">storage\_container\_name: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="df331-174">Пример\_файл\_путь: hello путь tooa файл, отправленный toohello контейнера.</span><span class="sxs-lookup"><span data-stu-id="df331-174">example\_file\_path: hello path tooa file that is uploaded toohello container.</span></span>

2. <span data-ttu-id="df331-175">Запустите сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="df331-175">Run hello script.</span></span> <span data-ttu-id="df331-176">Она отображает hello SAS маркера аналогичные toohello после текста после завершения сценария hello:</span><span class="sxs-lookup"><span data-stu-id="df331-176">It displays hello SAS token similar toohello following text when hello script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="df331-177">Сохраните hello маркера политики SAS, имя учетной записи хранилища и имя контейнера.</span><span class="sxs-lookup"><span data-stu-id="df331-177">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="df331-178">Эти значения используются при связывании учетной записи хранилища hello с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df331-178">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

## <a name="use-hello-sas-with-hdinsight"></a><span data-ttu-id="df331-179">Использовать hello SAS с HDInsight</span><span class="sxs-lookup"><span data-stu-id="df331-179">Use hello SAS with HDInsight</span></span>

<span data-ttu-id="df331-180">При создании кластера HDInsight необходимо указать основную учетную запись хранения; дополнительные учетные записи хранения указываются по желанию.</span><span class="sxs-lookup"><span data-stu-id="df331-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="df331-181">Оба метода добавления хранилища требуется полный доступ учетных записей хранения toohello и контейнеров, которые используются.</span><span class="sxs-lookup"><span data-stu-id="df331-181">Both of these methods of adding storage require full access toohello storage accounts and containers that are used.</span></span>

<span data-ttu-id="df331-182">toouse контейнер tooa доступа toolimit подписи общего доступа, добавьте toohello настраиваемой записи **сайта основные** конфигурации для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="df331-182">toouse a Shared Access Signature toolimit access tooa container, add a custom entry toohello **core-site** configuration for hello cluster.</span></span>

* <span data-ttu-id="df331-183">Для **на основе Windows** или **под управлением Linux** кластеров HDInsight, вы можете добавить запись hello во время создания кластера с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df331-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add hello entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="df331-184">Для **под управлением Linux** кластеров HDInsight изменить конфигурацию hello после создания кластера, с помощью Ambari.</span><span class="sxs-lookup"><span data-stu-id="df331-184">For **Linux-based** HDInsight clusters, change hello configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-hello-sas"></a><span data-ttu-id="df331-185">Создать кластер, который использует hello SAS</span><span class="sxs-lookup"><span data-stu-id="df331-185">Create a cluster that uses hello SAS</span></span>

<span data-ttu-id="df331-186">Пример создания кластера HDInsight, hello использует SAS включается в hello `CreateCluster` каталог репозитория hello.</span><span class="sxs-lookup"><span data-stu-id="df331-186">An example of creating an HDInsight cluster that uses hello SAS is included in hello `CreateCluster` directory of hello repository.</span></span> <span data-ttu-id="df331-187">toouse, которую он hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="df331-187">toouse it, use hello following steps:</span></span>

1. <span data-ttu-id="df331-188">Откройте hello `CreateCluster\HDInsightSAS.ps1` файл в текстовом редакторе и измените следующие значения в начале документа hello hello hello.</span><span class="sxs-lookup"><span data-stu-id="df331-188">Open hello `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify hello following values at hello beginning of hello document.</span></span>

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="df331-189">Например, изменить `'mycluster'` toohello имя кластера hello требуется toocreate.</span><span class="sxs-lookup"><span data-stu-id="df331-189">For example, change `'mycluster'` toohello name of hello cluster you want toocreate.</span></span> <span data-ttu-id="df331-190">Hello SAS значения должны совпадать значения hello hello предыдущих шагах, при создании учетной записи хранилища и маркер SAS.</span><span class="sxs-lookup"><span data-stu-id="df331-190">hello SAS values should match hello values from hello previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="df331-191">После изменения значения hello сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="df331-191">Once you have changed hello values, save hello file.</span></span>

2. <span data-ttu-id="df331-192">Откройте командную строку Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df331-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="df331-193">Если вы не знакомы с модулем Azure PowerShell или он у вас не установлен, см. статью [Установка и настройка служб Azure PowerShell][powershell].</span><span class="sxs-lookup"><span data-stu-id="df331-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="df331-194">В строке приветствия используйте hello, следующая команда tooauthenticate tooyour подписки Azure:</span><span class="sxs-lookup"><span data-stu-id="df331-194">From hello prompt, use hello following command tooauthenticate tooyour Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="df331-195">При появлении соответствующего запроса войдите в систему hello учетной записи для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="df331-195">When prompted, log in with hello account for your Azure subscription.</span></span>

    <span data-ttu-id="df331-196">Если ваша учетная запись связана с несколькими подписками Azure, может потребоваться toouse `Select-AzureRmSubscription` tooselect hello подписки нужно toouse.</span><span class="sxs-lookup"><span data-stu-id="df331-196">If your account is associated with multiple Azure subscriptions, you may need toouse `Select-AzureRmSubscription` tooselect hello subscription you wish toouse.</span></span>

4. <span data-ttu-id="df331-197">Из строки hello измените каталоги toohello `CreateCluster` каталог, содержащий файл HDInsightSAS.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="df331-197">From hello prompt, change directories toohello `CreateCluster` directory that contains hello HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="df331-198">Затем используйте следующий сценарий hello toorun hello</span><span class="sxs-lookup"><span data-stu-id="df331-198">Then use hello following command toorun hello script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="df331-199">Как сценарий выполняется hello она записывает выходные данные командной строки PowerShell toohello при создании ресурса hello группы и хранения учетных записей.</span><span class="sxs-lookup"><span data-stu-id="df331-199">As hello script runs, it logs output toohello PowerShell prompt as it creates hello resource group and storage accounts.</span></span> <span data-ttu-id="df331-200">Вы являетесь пользователем hello HTTP запрос tooenter для hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df331-200">You are prompted tooenter hello HTTP user for hello HDInsight cluster.</span></span> <span data-ttu-id="df331-201">Эта учетная запись является кластера toohello доступа используется toosecure HTTP в секунду.</span><span class="sxs-lookup"><span data-stu-id="df331-201">This account is used toosecure HTTP/s access toohello cluster.</span></span>

    <span data-ttu-id="df331-202">При создании кластера под управлением Linux запрашивается имя учетной записи пользователя SSH и пароль.</span><span class="sxs-lookup"><span data-stu-id="df331-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="df331-203">Эта учетная запись является журнала используется tooremotely toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="df331-203">This account is used tooremotely log in toohello cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="df331-204">Когда появится сообщение hello HTTP/s или SSH имя пользователя и пароль, необходимо указать пароль, отвечающий hello следующие условия:</span><span class="sxs-lookup"><span data-stu-id="df331-204">When prompted for hello HTTP/s or SSH user name and password, you must provide a password that meets hello following criteria:</span></span>
   >
   > * <span data-ttu-id="df331-205">содержит не меньше 10 символов;</span><span class="sxs-lookup"><span data-stu-id="df331-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="df331-206">содержит хотя бы одну цифру;</span><span class="sxs-lookup"><span data-stu-id="df331-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="df331-207">содержит хотя бы один специальный символ;</span><span class="sxs-lookup"><span data-stu-id="df331-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="df331-208">содержит хотя бы одну букву в верхнем или нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="df331-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="df331-209">Это занимает немного времени для этого сценария toocomplete, обычно около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="df331-209">It takes a while for this script toocomplete, usually around 15 minutes.</span></span> <span data-ttu-id="df331-210">По завершении сценария hello без ошибок после создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="df331-210">When hello script completes without any errors, hello cluster has been created.</span></span>

### <a name="use-hello-sas-with-an-existing-cluster"></a><span data-ttu-id="df331-211">Использовать hello SAS с существующего кластера</span><span class="sxs-lookup"><span data-stu-id="df331-211">Use hello SAS with an existing cluster</span></span>

<span data-ttu-id="df331-212">При наличии существующего кластера под управлением Linux, можно добавить hello SAS toohello **сайта основные** конфигурации с помощью hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="df331-212">If you have an existing Linux-based cluster, you can add hello SAS toohello **core-site** configuration by using hello following steps:</span></span>

1. <span data-ttu-id="df331-213">Откройте hello Ambari web пользовательского интерфейса для кластера.</span><span class="sxs-lookup"><span data-stu-id="df331-213">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="df331-214">Hello адрес для этой страницы является https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="df331-214">hello address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="df331-215">В ответ на запрос проверки подлинности toohello кластер, использующий имя администратора hello (администратор) и пароль, который используется при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="df331-215">When prompted, authenticate toohello cluster using hello admin name (admin) and password you used when creating hello cluster.</span></span>

2. <span data-ttu-id="df331-216">Hello слева от оператора hello Ambari web пользовательского интерфейса, выберите **HDFS** , а затем выберите hello **Configs** tab в середине hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="df331-216">From hello left side of hello Ambari web UI, select **HDFS** and then select hello **Configs** tab in hello middle of hello page.</span></span>

3. <span data-ttu-id="df331-217">Выберите hello **Дополнительно** вкладку, а затем найдите hello **сайта основные настраиваемый** раздела.</span><span class="sxs-lookup"><span data-stu-id="df331-217">Select hello **Advanced** tab, and then scroll until you find hello **Custom core-site** section.</span></span>

4. <span data-ttu-id="df331-218">Разверните hello **сайта основные настраиваемый** раздела, а затем toohello конец прокрутки и выберите hello **добавить свойство...**  ссылку.</span><span class="sxs-lookup"><span data-stu-id="df331-218">Expand hello **Custom core-site** section, then scroll toohello end and select hello **Add property...** link.</span></span> <span data-ttu-id="df331-219">Используйте hello следующие значения для hello **ключ** и **значение** поля:</span><span class="sxs-lookup"><span data-stu-id="df331-219">Use hello following values for hello **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="df331-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="df331-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="df331-221">**Значение**: hello SAS, возвращенных hello приложение C# или Python, выполненных ранее</span><span class="sxs-lookup"><span data-stu-id="df331-221">**Value**: hello SAS returned by hello C# or Python application you ran previously</span></span>

     <span data-ttu-id="df331-222">Замените **CONTAINERNAME** в имени контейнера hello вместе с hello приложение C# или SAS.</span><span class="sxs-lookup"><span data-stu-id="df331-222">Replace **CONTAINERNAME** with hello container name you used with hello C# or SAS application.</span></span> <span data-ttu-id="df331-223">Замените **STORAGEACCOUNTNAME** вы использовали имя учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="df331-223">Replace **STORAGEACCOUNTNAME** with hello storage account name you used.</span></span>

5. <span data-ttu-id="df331-224">Нажмите кнопку hello **добавить** toosave этот ключ и значение, а затем щелкните hello **Сохранить** кнопку изменения конфигурации toosave hello.</span><span class="sxs-lookup"><span data-stu-id="df331-224">Click hello **Add** button toosave this key and value, then click hello **Save** button toosave hello configuration changes.</span></span> <span data-ttu-id="df331-225">При появлении запроса добавьте описание изменения hello («Добавление доступа к хранилищу SAS» например) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df331-225">When prompted, add a description of hello change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="df331-226">Нажмите кнопку **ОК** после завершения изменений hello.</span><span class="sxs-lookup"><span data-stu-id="df331-226">Click **OK** when hello changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="df331-227">Перед hello изменения вступят в силу, необходимо перезапустить несколько служб.</span><span class="sxs-lookup"><span data-stu-id="df331-227">You must restart several services before hello change takes effect.</span></span>

6. <span data-ttu-id="df331-228">В веб-Ambari hello пользовательского интерфейса, выберите **HDFS** из списка hello hello слева, а затем выберите **перезапустите все** из hello **действий службы** раскрывающемся списке в правом hello.</span><span class="sxs-lookup"><span data-stu-id="df331-228">In hello Ambari web UI, select **HDFS** from hello list on hello left, and then select **Restart All** from hello **Service Actions** drop down list on hello right.</span></span> <span data-ttu-id="df331-229">При появлении запроса выберите **Turn on maintenance mode** (Включить режим обслуживания) и щелкните "Conform Restart All" (Подтвердить перезапуск).</span><span class="sxs-lookup"><span data-stu-id="df331-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="df331-230">Повторите эту процедуру для MapReduce2 и YARN.</span><span class="sxs-lookup"><span data-stu-id="df331-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="df331-231">После перезапуска службы hello выделить каждую таблицу и отключать режим обслуживания из hello **действий службы** раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="df331-231">Once hello services have restarted, select each one and disable maintenance mode from hello **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="df331-232">Тестирование ограниченного доступа</span><span class="sxs-lookup"><span data-stu-id="df331-232">Test restricted access</span></span>

<span data-ttu-id="df331-233">tooverify, ограничен доступ hello используйте следующие методы:</span><span class="sxs-lookup"><span data-stu-id="df331-233">tooverify that you have restricted access, use hello following methods:</span></span>

* <span data-ttu-id="df331-234">Для **на основе Windows** кластеров HDInsight использование удаленного рабочего стола tooconnect toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="df331-234">For **Windows-based** HDInsight clusters, use Remote Desktop tooconnect toohello cluster.</span></span> <span data-ttu-id="df331-235">Дополнительные сведения см. в разделе [подключиться с помощью протокола удаленного рабочего СТОЛА tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="df331-235">For more information, see [Connect tooHDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="df331-236">После подключения использовать hello **командной строки Hadoop** значок рабочего стола tooopen hello командную строку.</span><span class="sxs-lookup"><span data-stu-id="df331-236">Once connected, use hello **Hadoop Command-Line** icon on hello desktop tooopen a command prompt.</span></span>

* <span data-ttu-id="df331-237">Для **под управлением Linux** кластеров HDInsight использование SSH tooconnect toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="df331-237">For **Linux-based** HDInsight clusters, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="df331-238">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="df331-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="df331-239">После подключения toohello кластера, используйте следующие шаги tooverify можно только чтение и список элементов в учетной записи хранения SAS hello hello:</span><span class="sxs-lookup"><span data-stu-id="df331-239">Once connected toohello cluster, use hello following steps tooverify that you can only read and list items on hello SAS storage account:</span></span>

1. <span data-ttu-id="df331-240">содержимое hello toolist hello контейнера, используйте следующую команду из строки hello hello:</span><span class="sxs-lookup"><span data-stu-id="df331-240">toolist hello contents of hello container, use hello following command from hello prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="df331-241">Замените **SASCONTAINER** с именем hello hello контейнера, созданные для учетной записи хранения SAS hello.</span><span class="sxs-lookup"><span data-stu-id="df331-241">Replace **SASCONTAINER** with hello name of hello container created for hello SAS storage account.</span></span> <span data-ttu-id="df331-242">Замените **SASACCOUNTNAME** с именем hello hello учетной записи хранения для hello SAS.</span><span class="sxs-lookup"><span data-stu-id="df331-242">Replace **SASACCOUNTNAME** with hello name of hello storage account used for hello SAS.</span></span>

    <span data-ttu-id="df331-243">Список Hello включает файл hello, отправленный при создании hello контейнера и SAS.</span><span class="sxs-lookup"><span data-stu-id="df331-243">hello list includes hello file uploaded when hello container and SAS were created.</span></span>

2. <span data-ttu-id="df331-244">Используйте следующие команды tooverify, вы можете узнать hello содержимое файла hello hello.</span><span class="sxs-lookup"><span data-stu-id="df331-244">Use hello following command tooverify that you can read hello contents of hello file.</span></span> <span data-ttu-id="df331-245">Замените hello **SASCONTAINER** и **SASACCOUNTNAME** как в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="df331-245">Replace hello **SASCONTAINER** and **SASACCOUNTNAME** as in hello previous step.</span></span> <span data-ttu-id="df331-246">Замените **FILENAME** с именем hello файла hello, отображенный в предыдущей команде hello:</span><span class="sxs-lookup"><span data-stu-id="df331-246">Replace **FILENAME** with hello name of hello file displayed in hello previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="df331-247">Эта команда перечисляет hello содержимое файла hello.</span><span class="sxs-lookup"><span data-stu-id="df331-247">This command lists hello contents of hello file.</span></span>

3. <span data-ttu-id="df331-248">Используйте hello следующая команда toodownload hello файл toohello локальной файловой системы:</span><span class="sxs-lookup"><span data-stu-id="df331-248">Use hello following command toodownload hello file toohello local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="df331-249">Эта команда загрузки hello tooa локальный файл с именем **testfile.txt**.</span><span class="sxs-lookup"><span data-stu-id="df331-249">This command downloads hello file tooa local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="df331-250">Используйте hello следующая команда tooupload hello локальный файл tooa новый файл с именем **testupload.txt** на hello хранилище SAS:</span><span class="sxs-lookup"><span data-stu-id="df331-250">Use hello following command tooupload hello local file tooa new file named **testupload.txt** on hello SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="df331-251">Появится toohello аналогичные сообщения после текста:</span><span class="sxs-lookup"><span data-stu-id="df331-251">You receive a message similar toohello following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="df331-252">Эта ошибка возникает, так как место хранения hello чтения + только список.</span><span class="sxs-lookup"><span data-stu-id="df331-252">This error occurs because hello storage location is read+list only.</span></span> <span data-ttu-id="df331-253">Используйте следующие команды tooput hello данные в хранилище по умолчанию hello hello кластер, который доступен для записи hello.</span><span class="sxs-lookup"><span data-stu-id="df331-253">Use hello following command tooput hello data on hello default storage for hello cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="df331-254">На этот раз hello операция должна завершиться успешно.</span><span class="sxs-lookup"><span data-stu-id="df331-254">This time, hello operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="df331-255">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="df331-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="df331-256">Задача была отменена</span><span class="sxs-lookup"><span data-stu-id="df331-256">A task was canceled</span></span>

<span data-ttu-id="df331-257">**Симптомы**: при создании кластера с помощью сценария PowerShell hello, может появиться сообщение об ошибке после hello:</span><span class="sxs-lookup"><span data-stu-id="df331-257">**Symptoms**: When creating a cluster using hello PowerShell script, you may receive hello following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="df331-258">**Причина**: Эта ошибка может возникать, если использовать пароль для пользователя admin/HTTP hello для кластера hello, или (для кластеров под управлением Linux) hello пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="df331-258">**Cause**: This error can occur if you use a password for hello admin/HTTP user for hello cluster, or (for Linux-based clusters) hello SSH user.</span></span>

<span data-ttu-id="df331-259">**Разрешение**: использовать пароль, отвечающий hello следующие условия:</span><span class="sxs-lookup"><span data-stu-id="df331-259">**Resolution**: Use a password that meets hello following criteria:</span></span>

* <span data-ttu-id="df331-260">содержит не меньше 10 символов;</span><span class="sxs-lookup"><span data-stu-id="df331-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="df331-261">содержит хотя бы одну цифру;</span><span class="sxs-lookup"><span data-stu-id="df331-261">Must contain at least one digit</span></span>
* <span data-ttu-id="df331-262">содержит хотя бы один специальный символ;</span><span class="sxs-lookup"><span data-stu-id="df331-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="df331-263">содержит хотя бы одну букву в верхнем или нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="df331-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="df331-264">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df331-264">Next steps</span></span>

<span data-ttu-id="df331-265">Теперь, когда вы узнали, как tooyour tooadd ограниченным доступом хранилища кластера HDInsight, узнайте toowork другие способы, с данными в кластере:</span><span class="sxs-lookup"><span data-stu-id="df331-265">Now that you have learned how tooadd limited-access storage tooyour HDInsight cluster, learn other ways toowork with data on your cluster:</span></span>

* [<span data-ttu-id="df331-266">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="df331-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="df331-267">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="df331-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="df331-268">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="df331-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
