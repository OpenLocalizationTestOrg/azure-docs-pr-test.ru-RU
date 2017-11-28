---
title: "aaaGet работы с сервером R в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toocreate Apache усилить в кластере HDInsight, включающей сервер R и отправьте сценарий R в кластере hello."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="569bc-103">Приступая к работе с R Server в HDInsight</span><span class="sxs-lookup"><span data-stu-id="569bc-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="569bc-104">HDInsight включает toobe параметр R Server интегрированы с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="569bc-104">HDInsight includes an R Server option toobe integrated into your HDInsight cluster.</span></span> <span data-ttu-id="569bc-105">Этот параметр позволяет R-скриптов toouse Spark и MapReduce toorun распределенных вычислений.</span><span class="sxs-lookup"><span data-stu-id="569bc-105">This option allows R scripts toouse Spark and MapReduce toorun distributed computations.</span></span> <span data-ttu-id="569bc-106">В этом документе вы узнаете, как toocreate сервера R на кластер HDInsight, а затем выполнения R-сценарий, который демонстрирует использование Spark для распределенных вычислений R.</span><span class="sxs-lookup"><span data-stu-id="569bc-106">In this document, you learn how toocreate an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="569bc-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="569bc-107">Prerequisites</span></span>

* <span data-ttu-id="569bc-108">**Подписка Azure**. Прежде чем приступать к изучению этого руководства, необходимо оформить подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="569bc-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="569bc-109">Статья перейдите toohello [бесплатной пробной версии Microsoft Azure получить](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="569bc-109">Go toohello article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="569bc-110">**Клиент Secure Shell (SSH)**: клиент SSH используется tooremotely подключения кластера HDInsight toohello и выполнения команд непосредственно в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-110">**A Secure Shell (SSH) client**: An SSH client is used tooremotely connect toohello HDInsight cluster and run commands directly on hello cluster.</span></span> <span data-ttu-id="569bc-111">Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="569bc-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="569bc-112">**Ключи SSH (необязательно)**: hello SSH учетная запись, используемая tooconnect toohello кластера с помощью пароля или открытый ключ можно защитить.</span><span class="sxs-lookup"><span data-stu-id="569bc-112">**SSH keys (optional)**: You can secure hello SSH account used tooconnect toohello cluster using either a password or a public key.</span></span> <span data-ttu-id="569bc-113">С помощью пароля проще и позволяет вам tooget работы без необходимости toocreate пару открытого и закрытого ключей.</span><span class="sxs-lookup"><span data-stu-id="569bc-113">Using a password is easier, and allows you tooget started without having toocreate a public/private key pair.</span></span> <span data-ttu-id="569bc-114">Тем не менее использовать ключ безопаснее.</span><span class="sxs-lookup"><span data-stu-id="569bc-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="569bc-115">Hello в этом документе предполагается, что вы используете пароль.</span><span class="sxs-lookup"><span data-stu-id="569bc-115">hello steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="569bc-116">Автоматизированное создание кластера</span><span class="sxs-lookup"><span data-stu-id="569bc-116">Automated cluster creation</span></span>

<span data-ttu-id="569bc-117">Можно автоматизировать создание hello серверов HDInsight R, с помощью диспетчера ресурсов Azure шаблоны, hello SDK, а также PowerShell.</span><span class="sxs-lookup"><span data-stu-id="569bc-117">You can automate hello creation of HDInsight R Servers using Azure Resource Manager templates, hello SDK, and also PowerShell.</span></span>

* <span data-ttu-id="569bc-118">toocreate R Server, с помощью шаблона управления ресурсами Azure, в разделе [развертывания кластера HDInsight R server](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span><span class="sxs-lookup"><span data-stu-id="569bc-118">toocreate an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="569bc-119">toocreate значение R Server с помощью hello .NET SDK, в разделе [создавать кластеры под управлением Linux в HDInsight с помощью hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="569bc-119">toocreate an R Server using hello .NET SDK, see [create Linux-based clusters in HDInsight using hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="569bc-120">toodeploy R Server с помощью powershell, см. в статье hello на [создание сервера R на HDInsight с помощью PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="569bc-120">toodeploy R Server using powershell, see hello article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a><span data-ttu-id="569bc-121">Создать кластер hello hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="569bc-121">Create hello cluster using hello Azure portal</span></span>

1. <span data-ttu-id="569bc-122">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="569bc-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="569bc-123">Выберите **Создать** -> **Аналитика** -> **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="569bc-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Изображение, на котором показано создание нового кластера](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="569bc-125">В hello **быстрое создание** возникают, введите имя кластера hello в hello **имя кластера** поля.</span><span class="sxs-lookup"><span data-stu-id="569bc-125">In hello **Quick create** experience, enter a name for hello cluster in hello **Cluster Name** field.</span></span> <span data-ttu-id="569bc-126">Если у вас несколько подписок Azure, используйте hello **подписки** входа tooselect hello один требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="569bc-126">If you have multiple Azure subscriptions, use hello **Subscription** entry tooselect hello one you want toouse.</span></span>

    ![Выбор имени кластера и подписки](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="569bc-128">Выберите **кластера типа** tooopen hello **конфигурации кластера** колонку.</span><span class="sxs-lookup"><span data-stu-id="569bc-128">Select **Cluster type** tooopen hello **Cluster configuration** blade.</span></span> <span data-ttu-id="569bc-129">На hello **конфигурации кластера** колонке выберите hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="569bc-129">On hello **Cluster Configuration** blade, select hello following options:</span></span>

    * <span data-ttu-id="569bc-130">**Тип кластера**: R Server.</span><span class="sxs-lookup"><span data-stu-id="569bc-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="569bc-131">**Версия**: hello выберите версию tooinstall R Server на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-131">**Version**: select hello version of R Server tooinstall on hello cluster.</span></span> <span data-ttu-id="569bc-132">в настоящее время доступная версия Hello ***9.1 R Server (HDI 3.6)***.</span><span class="sxs-lookup"><span data-stu-id="569bc-132">hello version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="569bc-133">Заметки о выпуске для hello доступные версии R Server доступны [здесь](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="569bc-133">Release notes for hello available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="569bc-134">**R Studio community edition для R Server**: это интегрированная среда разработки на основе браузера устанавливается по умолчанию на узле edge hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on hello edge node.</span></span> <span data-ttu-id="569bc-135">Если вы предпочитаете toonot установить его, а затем снимите флажок "hello".</span><span class="sxs-lookup"><span data-stu-id="569bc-135">If you would prefer toonot have it installed, then uncheck hello check box.</span></span> <span data-ttu-id="569bc-136">При выборе toohave он установлен, hello URL-адрес для доступа к приветствия входа RStudio сервер находится в колонке приложения портала для кластера после ее создания.</span><span class="sxs-lookup"><span data-stu-id="569bc-136">If you choose toohave it installed, hello URL for accessing hello RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="569bc-137">Для других параметров оставьте hello в значения по умолчанию hello и использовать hello **выберите** toosave hello кластера тип кнопки.</span><span class="sxs-lookup"><span data-stu-id="569bc-137">Leave hello other options at hello default values and use hello **Select** button toosave hello cluster type.</span></span>

        ![Снимок экрана колонки "Тип кластера"](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="569bc-139">Введите **имя пользователя** и **пароль** для входа в кластер.</span><span class="sxs-lookup"><span data-stu-id="569bc-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="569bc-140">Укажите **имя пользователя SSH**.</span><span class="sxs-lookup"><span data-stu-id="569bc-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="569bc-141">SSH находится используется tooremotely подключения кластера с помощью toohello **Secure Shell (SSH)** клиента.</span><span class="sxs-lookup"><span data-stu-id="569bc-141">SSH is used tooremotely connect toohello cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="569bc-142">В этом диалоговом окне, или после создания кластера hello (на вкладке конфигурации hello для hello кластера) можно указать hello пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="569bc-142">You can either specify hello SSH user in this dialog or after hello cluster has been created (in hello Configuration tab for hello cluster).</span></span> <span data-ttu-id="569bc-143">R Server является настроенным tooexpect **имя пользователя SSH** из «remoteuser».</span><span class="sxs-lookup"><span data-stu-id="569bc-143">R Server is configured tooexpect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="569bc-144">**Если используется другое имя пользователя, необходимо выполнить дополнительные действия после создания кластера hello.**</span><span class="sxs-lookup"><span data-stu-id="569bc-144">**If you use a different username, you must perform an additional step after hello cluster is created.**</span></span>

    <span data-ttu-id="569bc-145">Оставьте поле hello, проверяется на **использовать одинаковый пароль в качестве учетной записи кластера** toouse **пароль** как hello тип проверки подлинности, если вы предпочитаете использовать открытый ключ.</span><span class="sxs-lookup"><span data-stu-id="569bc-145">Leave hello box checked for **Use same password as cluster login** toouse **PASSWORD** as hello authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="569bc-146">Необходимо tooaccess пары открытого и закрытого ключей R Server на кластере hello посредством удаленного клиента, как, например, RTVS, RStudio или другого рабочего стола интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="569bc-146">You need a public/private key pair tooaccess R Server on hello cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="569bc-147">При установке hello RStudio Server community edition необходимо toochoose пароль SSH.</span><span class="sxs-lookup"><span data-stu-id="569bc-147">If you install hello RStudio Server community edition, you need toochoose an SSH password.</span></span>     

    <span data-ttu-id="569bc-148">toocreate и используйте пару открытого и закрытого ключей, снимите флажок **использовать одинаковый пароль в качестве учетной записи кластера** , а затем выберите **ОТКРЫТЫЙ ключ** и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="569bc-148">toocreate and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="569bc-149">При выполнении этих указаний предполагается, что установлена среда Cygwin с программой ssh-keygen или эквивалентным средством.</span><span class="sxs-lookup"><span data-stu-id="569bc-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="569bc-150">Создать пару открытого и закрытого ключей из командной строки hello переносного компьютера:</span><span class="sxs-lookup"><span data-stu-id="569bc-150">Generate a public/private key pair from hello command prompt on your laptop:</span></span>

        <span data-ttu-id="569bc-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="569bc-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="569bc-152">Выполните запрос tooname hello файл ключа, а затем введите парольную фразу для повышения безопасности.</span><span class="sxs-lookup"><span data-stu-id="569bc-152">Follow hello prompt tooname a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="569bc-153">Экран должен выглядеть примерно hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="569bc-153">Your screen should look something like hello following image:</span></span>

        ![Командная строка SSH в Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="569bc-155">Эта команда создает файл закрытого ключа и файл открытого ключа в формате PUB имя < имя_файла закрытый ключ > hello, например furiosa и furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="569bc-155">This command creates a private key file and a public key file under hello name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![Каталог SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="569bc-157">Затем укажите hello файла открытого ключа (&#42;. pub) при назначении HDI кластера учетные данные и окончательный своей группы ресурсов и область и выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="569bc-157">Then specify hello public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Колонка учетных данных](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="569bc-159">Изменить разрешения для закрытого keyfile hello переносного компьютера:</span><span class="sxs-lookup"><span data-stu-id="569bc-159">Change permissions on hello private keyfile on your laptop:</span></span>

        <span data-ttu-id="569bc-160">chmod 600 <имя_файла_закрытого ключа></span><span class="sxs-lookup"><span data-stu-id="569bc-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="569bc-161">Используйте файл закрытого ключа hello с SSH для удаленного входа:</span><span class="sxs-lookup"><span data-stu-id="569bc-161">Use hello private key file with SSH for remote login:</span></span>

        <span data-ttu-id="569bc-162">ssh –i <имя_файла_закрытого_ключа> remoteuser@<hostname public ip>.</span><span class="sxs-lookup"><span data-stu-id="569bc-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="569bc-163">Кроме того, как часть определения hello Hadoop Spark контекста вычислений R сервера на приветствия клиента.</span><span class="sxs-lookup"><span data-stu-id="569bc-163">Or, as part hello definition of your Hadoop Spark compute context for R Server on hello client.</span></span> <span data-ttu-id="569bc-164">В разделе hello **с помощью Microsoft R Server как клиент Hadoop** подраздела в [создать контекст вычислений для Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span><span class="sxs-lookup"><span data-stu-id="569bc-164">See hello **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="569bc-165">Hello быстрое создание переходов, которые toohello **хранения** колонке учетной записи для хранения tooselect hello toobe параметры, используемые для первичного расположения hello hello HDFS файловой системы, используемой кластером hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-165">hello quick create transitions you toohello **Storage** blade tooselect hello storage account settings toobe used for hello primary location of hello HDFS file system used by hello cluster.</span></span> <span data-ttu-id="569bc-166">Выберите новую или существующую учетную запись хранения Azure или существующую учетную запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="569bc-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="569bc-167">При выборе учетной записи хранилища Azure, выбрав выбран существующую учетную запись хранения **выберите учетную запись хранения** и выбрав соответствующий счет hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting hello relevant account.</span></span> <span data-ttu-id="569bc-168">Создание учетной записи с помощью hello **создать новый** ссылку в hello **выберите учетную запись хранения** раздела.</span><span class="sxs-lookup"><span data-stu-id="569bc-168">Create a new account using hello **Create New** link in hello **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="569bc-169">При выборе **New** необходимо ввести имя для новой учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-169">If you select **New** you must enter a name for hello new storage account.</span></span> <span data-ttu-id="569bc-170">Зеленый флажок отображается, если принимается имя hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-170">A green check appears if hello name is accepted.</span></span>

      <span data-ttu-id="569bc-171">Hello **контейнер по умолчанию** имя toohello значения по умолчанию hello кластера.</span><span class="sxs-lookup"><span data-stu-id="569bc-171">hello **Default Container** defaults toohello name of hello cluster.</span></span> <span data-ttu-id="569bc-172">Оставьте это значение по умолчанию значение hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-172">Leave this default as hello value.</span></span>

      <span data-ttu-id="569bc-173">Если был выбран новый параметр учетной записи хранилища prompt tooselect **расположение** является данный tooselect какой области toocreate hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="569bc-173">If a new storage account option was selected a prompt tooselect **Location** is given tooselect which region toocreate hello storage account.</span></span>  

         ![Колонка "Источник данных"](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="569bc-175">Выбор расположения hello для источника данных по умолчанию hello также устанавливает hello расположение кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-175">Selecting hello location for hello default data source  also sets hello location of hello HDInsight cluster.</span></span> <span data-ttu-id="569bc-176">Hello кластер и по умолчанию источник данных должен быть в hello одного региона.</span><span class="sxs-lookup"><span data-stu-id="569bc-176">hello cluster and default data source must be in hello same region.</span></span>

    - <span data-ttu-id="569bc-177">Если вы хотите toouse существующее хранилище Озера данных, выберите hello toouse учетной записи хранения ADLS кластер и добавьте hello *добавить* toohello удостоверение tooyour кластера tooallow доступа к магазину.</span><span class="sxs-lookup"><span data-stu-id="569bc-177">If you want toouse an existing Data Lake Store, then select hello ADLS storage account toouse and add hello cluster *ADD* identity tooyour cluster tooallow access toohello store.</span></span> <span data-ttu-id="569bc-178">Дополнительные сведения об этом процессе см. в статье [Создание кластера HDInsight с хранилищем Data Lake Store с помощью портала Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span><span class="sxs-lookup"><span data-stu-id="569bc-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="569bc-179">Используйте hello **выберите** конфигурации источника данных hello toosave кнопки.</span><span class="sxs-lookup"><span data-stu-id="569bc-179">Use hello **Select** button toosave hello data source configuration.</span></span>


7. <span data-ttu-id="569bc-180">Hello **Сводка** колонке выведет toovalidate все параметры.</span><span class="sxs-lookup"><span data-stu-id="569bc-180">hello **Summary** blade then displays toovalidate all your settings.</span></span> <span data-ttu-id="569bc-181">Здесь можно изменить ваш **размер кластера** toomodify hello количества серверов в кластере, а также указать любой **скрипт действия** требуется toorun.</span><span class="sxs-lookup"><span data-stu-id="569bc-181">Here you can change your **Cluster size** toomodify hello number of servers in your cluster and also specify any **Script actions** you want toorun.</span></span> <span data-ttu-id="569bc-182">Если нет уверенности, что требуется больший размер кластера, оставьте hello число узлов рабочих ролей по умолчанию hello `4`.</span><span class="sxs-lookup"><span data-stu-id="569bc-182">Unless you know that you need a larger cluster, leave hello number of worker nodes at hello default of `4`.</span></span> <span data-ttu-id="569bc-183">Hello оценочная стоимость hello кластера отображается в колонке hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-183">hello estimated cost of hello cluster is shown within hello blade.</span></span>

    ![Сводка по кластерам](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="569bc-185">При необходимости можно изменить размер кластера позже через портал hello (**кластера** -> **параметры** -> **кластера масштабирования**) tooincrease или Уменьшите число рабочих узлов в hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-185">If needed, you can resize your cluster later through hello Portal (**Cluster** -> **Settings** -> **Scale Cluster**) tooincrease or decrease hello number of worker nodes.</span></span>  <span data-ttu-id="569bc-186">Это изменение размера можно использовать на переход из состояния простоя работу кластера hello не во время работы, или добавление потребностях hello toomeet крупных задач.</span><span class="sxs-lookup"><span data-stu-id="569bc-186">This resizing can be useful for idling down hello cluster when not in use, or for adding capacity toomeet hello needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="569bc-187">Некоторые факторы tookeep в виду при планировании размера вашего кластера, узлы данных hello и hello граничного узла включают:</span><span class="sxs-lookup"><span data-stu-id="569bc-187">Some factors tookeep in mind when sizing your cluster, hello data nodes, and hello edge node include:</span></span>  

   * <span data-ttu-id="569bc-188">Hello производительность распределенных анализа R Server Spark при пропорционально toohello число рабочих узлов hello данных велик.</span><span class="sxs-lookup"><span data-stu-id="569bc-188">hello performance of distributed R Server analyses on Spark is proportional toohello number of worker nodes when hello data is large.</span></span>  

   * <span data-ttu-id="569bc-189">R Server анализ производительности Hello линейно hello размер анализируемые данные.</span><span class="sxs-lookup"><span data-stu-id="569bc-189">hello performance of R Server analyses is linear in hello size of data being analyzed.</span></span> <span data-ttu-id="569bc-190">Например:</span><span class="sxs-lookup"><span data-stu-id="569bc-190">For example:</span></span>  

     * <span data-ttu-id="569bc-191">Для данных небольшого toomodest производительности лучше при анализе в локальный контекст вычислений на hello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="569bc-191">For small toomodest data, performance is best when analyzed in a local compute context on hello edge node.</span></span>  <span data-ttu-id="569bc-192">Дополнительные сведения о сценариях hello, при которых локального hello и Spark вычислительных контекстов лучше всего работают см. в разделе параметры контекста вычислений R Server на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="569bc-192">For more information on hello scenarios under which hello local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="569bc-193">При входе в toohello граничного узла, выполнить сценарий R, а затем выполняются все, кроме hello функциям rx ScaleR <strong>локально</strong> на hello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="569bc-193">If you log in toohello edge node and run your R script, then all but hello ScaleR rx-functions are executed <strong>locally</strong> on hello edge node.</span></span> <span data-ttu-id="569bc-194">Поэтому hello памяти и количество ядер hello edge узла должен определяться соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="569bc-194">So hello memory and number of cores of hello edge node should be sized accordingly.</span></span> <span data-ttu-id="569bc-195">Здравствуйте, же правило применяется при использовании R Server на HDI качестве контекста удаленных вычислений на ноутбуке.</span><span class="sxs-lookup"><span data-stu-id="569bc-195">hello same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Колонка "Ценовые категории узла"](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="569bc-197">Используйте hello **выберите** кнопку toosave hello узел цены конфигурации.</span><span class="sxs-lookup"><span data-stu-id="569bc-197">Use hello **Select** button toosave hello node pricing configuration.</span></span>

   <span data-ttu-id="569bc-198">Обратите внимание на ссылку для **скачивания шаблона и параметров**.</span><span class="sxs-lookup"><span data-stu-id="569bc-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="569bc-199">Щелкните этот сценарии toodisplay ссылки, используемые tooautomate hello создания кластера с выбранной конфигурацией hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-199">Click on this link toodisplay scripts that can be used tooautomate hello creation of a cluster with hello selected configuration.</span></span> <span data-ttu-id="569bc-200">Эти сценарии также доступны из hello Azure портала запись для кластера после его создания.</span><span class="sxs-lookup"><span data-stu-id="569bc-200">These scripts are also available from hello Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="569bc-201">Потребуется некоторое время для hello кластера toobe создана, обычно около 20 минут.</span><span class="sxs-lookup"><span data-stu-id="569bc-201">It takes some time for hello cluster toobe created, usually around 20 minutes.</span></span> <span data-ttu-id="569bc-202">Используйте плитки приветствия на начальной панели hello или hello **уведомления** входа на hello слева от toocheck страницы приветствия на процесс создания hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-202">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a><span data-ttu-id="569bc-203">Подключение tooRStudio сервера</span><span class="sxs-lookup"><span data-stu-id="569bc-203">Connect tooRStudio Server</span></span>

<span data-ttu-id="569bc-204">Если вы выбрали tooinclude RStudio Server community edition в вашей установке, то можно получить доступ к hello RStudio входа через два метода.</span><span class="sxs-lookup"><span data-stu-id="569bc-204">If you’ve chosen tooinclude RStudio Server community edition in your installation, then you can access hello RStudio login via two different methods.</span></span>

1. <span data-ttu-id="569bc-205">Go toohello URL-адреса (где **CLUSTERNAME** — имя кластера hello hello):</span><span class="sxs-lookup"><span data-stu-id="569bc-205">Go toohello following URL (where **CLUSTERNAME** is hello name of hello cluster you've created):</span></span>

    <span data-ttu-id="569bc-206">https://**имя_кластера**.azurehdinsight.net/rstudio/.</span><span class="sxs-lookup"><span data-stu-id="569bc-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="569bc-207">Откройте hello запись для кластера в hello портал Azure, выберите hello **панели мониторинга сервера R** быструю ссылку и выбрав hello **R Studio мониторинга**:</span><span class="sxs-lookup"><span data-stu-id="569bc-207">Open hello entry for your cluster in hello Azure portal, select hello **R Server Dashboards** quick link and then selecting hello **R Studio Dashboard**:</span></span>

     ![Панель мониторинга studio hello R доступа](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Панель мониторинга studio hello R доступа](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="569bc-210">Независимо от того, используется метод hello hello при первом входе необходимо tooauthenticate дважды.</span><span class="sxs-lookup"><span data-stu-id="569bc-210">Regardless of hello method used, hello first time you log in you need tooauthenticate twice.</span></span>  <span data-ttu-id="569bc-211">В первой проверки подлинности hello предоставляют hello *кластера Admin userid* и *пароль*.</span><span class="sxs-lookup"><span data-stu-id="569bc-211">At hello first authentication, provide hello *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="569bc-212">Во второй строке hello предоставляют hello *SSH userid* и *пароль*.</span><span class="sxs-lookup"><span data-stu-id="569bc-212">At hello second prompt, provide hello *SSH userid* and *password*.</span></span> <span data-ttu-id="569bc-213">Последующие журнала модулей требуются только hello *пароль SSH* и *userid*.</span><span class="sxs-lookup"><span data-stu-id="569bc-213">Subsequent log ins only require hello *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a><span data-ttu-id="569bc-214">Подключить узел edge toohello R Server</span><span class="sxs-lookup"><span data-stu-id="569bc-214">Connect toohello R Server edge node</span></span>

<span data-ttu-id="569bc-215">Подключение tooR сервера граничного узла кластера HDInsight hello, с помощью SSH с hello команды:</span><span class="sxs-lookup"><span data-stu-id="569bc-215">Connect tooR Server edge node of hello HDInsight cluster using SSH with hello command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="569bc-216">Можно найти hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` адрес в hello портал Azure, затем выбрав кластера **все параметры** -> **приложения** -> **сценария RServer**.</span><span class="sxs-lookup"><span data-stu-id="569bc-216">You can find hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in hello Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="569bc-217">При этом отображаются сведения о конечной точке SSH для hello граничного узла hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-217">This displays hello SSH Endpoint information for hello edge node.</span></span>
>
> ![Изображение hello конечной точки SSH для hello граничного узла](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="569bc-219">Если вы использовали toosecure пароль учетной записи пользователя SSH, не запрошенные tooenter его.</span><span class="sxs-lookup"><span data-stu-id="569bc-219">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="569bc-220">Если используется открытый ключ, возможно, toouse hello `-i` toospecify параметр hello соответствующим закрытым ключом.</span><span class="sxs-lookup"><span data-stu-id="569bc-220">If you used a public key, you may have toouse hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="569bc-221">Например:</span><span class="sxs-lookup"><span data-stu-id="569bc-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="569bc-222">Дополнительные сведения см. в разделе [tooHDInsight (Hadoop) с помощью SSH подключения](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="569bc-222">For more information, see [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="569bc-223">После подключения вы прибудете в запрос примерно следующие toohello:</span><span class="sxs-lookup"><span data-stu-id="569bc-223">Once connected, you arrive at a prompt similar toohello following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="569bc-224">Включение нескольких параллельных подключений пользователей</span><span class="sxs-lookup"><span data-stu-id="569bc-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="569bc-225">Можно включить несколько одновременных пользователей путем добавления дополнительных пользователей для hello граничного узла, на какие hello сообщества RStudio работает версия.</span><span class="sxs-lookup"><span data-stu-id="569bc-225">You can enable multiple concurrent users by adding more users for hello edge node on which hello RStudio community version runs.</span></span>

<span data-ttu-id="569bc-226">При создании кластера HDInsight необходимо указать двух пользователей: для HTTP и SSH.</span><span class="sxs-lookup"><span data-stu-id="569bc-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Параллельное подключение пользователя 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="569bc-228">**Кластер пользователя для входа**: пользователь с HTTP для проверки подлинности через шлюз hello HDInsight, используемых tooprotect hello HDInsight кластеры был создан.</span><span class="sxs-lookup"><span data-stu-id="569bc-228">**Cluster login username**: an HTTP user for authentication through hello HDInsight gateway that is used tooprotect hello HDInsight clusters you created.</span></span> <span data-ttu-id="569bc-229">Этот пользователь HTTP является hello используется tooaccess Ambari пользовательского интерфейса, YARN пользовательского интерфейса, а также другие компоненты пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="569bc-229">This HTTP user is used tooaccess hello Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="569bc-230">**Безопасное имя пользователя Shell (SSH)**: tooaccess hello SSH пользователя кластера через безопасный оболочки.</span><span class="sxs-lookup"><span data-stu-id="569bc-230">**Secure Shell (SSH) username**: an SSH user tooaccess hello cluster through secure shell.</span></span> <span data-ttu-id="569bc-231">Этот пользователь является пользователем в системе Linux для всех hello головного узла, рабочих узлов и узлов edge hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-231">This user is a user in hello Linux system for all hello head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="569bc-232">Чтобы можно было использовать безопасные оболочки tooaccess любой из узлов hello в удаленном кластере.</span><span class="sxs-lookup"><span data-stu-id="569bc-232">So you can use secure shell tooaccess any of hello nodes in a remote cluster.</span></span>

<span data-ttu-id="569bc-233">R Studio Server Community Hello, используемой в hello Microsoft R Server в кластере HDInsight типа принимает только Linux имя пользователя и пароль как механизм входа.</span><span class="sxs-lookup"><span data-stu-id="569bc-233">hello R Studio Server Community version used in hello Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="569bc-234">Эта версия не поддерживает передачу токенов.</span><span class="sxs-lookup"><span data-stu-id="569bc-234">It does not support passing tokens.</span></span> <span data-ttu-id="569bc-235">Таким образом, если вы создали новый кластер и хотите tooaccess toouse R Studio, необходимо toolog в два раза.</span><span class="sxs-lookup"><span data-stu-id="569bc-235">So if you have created a new cluster and want toouse R Studio tooaccess it, you need toolog in twice.</span></span>

- <span data-ttu-id="569bc-236">Сначала вход с использованием учетных данных пользователя hello HTTP через hello HDInsight шлюз:</span><span class="sxs-lookup"><span data-stu-id="569bc-236">First log in using hello HTTP user credentials through hello HDInsight Gateway:</span></span> 

    ![Параллельное подключение пользователя 2а](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="569bc-238">Затем используйте toolog учетные данные пользователя SSH hello в tooRStudio:</span><span class="sxs-lookup"><span data-stu-id="569bc-238">Then use hello SSH user credentials toolog in tooRStudio:</span></span>
  
    ![Параллельное подключение пользователя 2б](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="569bc-240">Сейчас при подготовке кластера HDInsight можно создать только одну учетную запись пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="569bc-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="569bc-241">Поэтому tooenable кластеры tooaccess несколько пользователей Microsoft R Server на HDInsight, нужно toocreate дополнительных пользователей в системе Linux hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-241">So tooenable multiple users tooaccess Microsoft R Server on HDInsight clusters, we need toocreate additional users in hello Linux system.</span></span>

<span data-ttu-id="569bc-242">Поскольку сообщества RStudio сервер работает под управлением кластера hello граничного узла, существуют несколько шагов в здесь:</span><span class="sxs-lookup"><span data-stu-id="569bc-242">Because RStudio Server Community is running on hello cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="569bc-243">Используйте toolog пользователя SSH hello создан в toohello граничного узла</span><span class="sxs-lookup"><span data-stu-id="569bc-243">Use hello created SSH user toolog in toohello edge node</span></span>
2. <span data-ttu-id="569bc-244">добавить нескольких пользователей Linux на граничный узел;</span><span class="sxs-lookup"><span data-stu-id="569bc-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="569bc-245">Сообщество RStudio версию использовать созданные пользователем hello</span><span class="sxs-lookup"><span data-stu-id="569bc-245">Use RStudio Community version with hello user created</span></span>

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a><span data-ttu-id="569bc-246">Шаг 1: Используйте toolog пользователя SSH hello создан в toohello граничного узла</span><span class="sxs-lookup"><span data-stu-id="569bc-246">Step 1: Use hello created SSH user toolog in toohello edge node</span></span>

<span data-ttu-id="569bc-247">Загрузить все средства SSH (например, Putty) и использовать существующие toolog пользователя SSH hello в.</span><span class="sxs-lookup"><span data-stu-id="569bc-247">Download any SSH tool (such as Putty) and use hello existing SSH user toolog in.</span></span> <span data-ttu-id="569bc-248">Затем следуйте инструкциям hello в [подключения tooHDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="569bc-248">Then follow hello instructions provided in [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello edge node.</span></span> <span data-ttu-id="569bc-249">адрес узла Hello edge для R Server в кластере HDInsight: *имя_кластера ed ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="569bc-249">hello edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="569bc-250">Шаг 2. Добавление дополнительных пользователей Linux на граничный узел</span><span class="sxs-lookup"><span data-stu-id="569bc-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="569bc-251">tooadd граничного узла toohello пользователя, выполнения команд hello:</span><span class="sxs-lookup"><span data-stu-id="569bc-251">tooadd a user toohello edge node, execute hello commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="569bc-252">Вы должны увидеть следующие элементы, которые возвращаются hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-252">You should see hello following items returned:</span></span> 

![Параллельное подключение пользователя 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="569bc-254">При появлении запроса «текущий пароль Kerberos:», просто нажмите клавиши **ввод** tooignore его.</span><span class="sxs-lookup"><span data-stu-id="569bc-254">When prompted for “Current Kerberos password:”, just press **Enter** tooignore it.</span></span> <span data-ttu-id="569bc-255">Hello `-m` в диалоговом окне `useradd` команда указывает, что hello система будет создавать домашнюю папку пользователя hello, необходимый для версия RStudio сообщества.</span><span class="sxs-lookup"><span data-stu-id="569bc-255">hello `-m` option in `useradd` command indicates that hello system will create a home folder for hello user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a><span data-ttu-id="569bc-256">Шаг 3: Использование RStudio сообщества версии с созданные пользователем hello</span><span class="sxs-lookup"><span data-stu-id="569bc-256">Step 3: Use RStudio Community version with hello user created</span></span>

<span data-ttu-id="569bc-257">Используйте созданные пользователем toolog hello в tooRStudio:</span><span class="sxs-lookup"><span data-stu-id="569bc-257">Use hello user created toolog in tooRStudio:</span></span>

![Параллельное подключение пользователя 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="569bc-259">Обратите внимание, что RStudio указывает, что вы используете hello нового пользователя (здесь, например, *sshuser6*) toolog hello кластера:</span><span class="sxs-lookup"><span data-stu-id="569bc-259">Notice that RStudio indicates that you are using hello new user (here, for example, *sshuser6*) toolog in hello cluster:</span></span> 

![Параллельное подключение пользователя 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="569bc-261">Вы можете также войти с использованием учетных данных исходной hello (по умолчанию — *sshuser*) одновременно в другом окне браузера.</span><span class="sxs-lookup"><span data-stu-id="569bc-261">You can also log in using hello original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="569bc-262">Вы можете отправлять задания с помощью функций scaleR.</span><span class="sxs-lookup"><span data-stu-id="569bc-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="569bc-263">Ниже приведен пример команды, используемые toorun hello задания:</span><span class="sxs-lookup"><span data-stu-id="569bc-263">Here is an example of hello commands used toorun a job:</span></span>

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="569bc-264">Обратите внимание, что задания hello отправлен под другим именем пользователя в пользовательском Интерфейсе YARN:</span><span class="sxs-lookup"><span data-stu-id="569bc-264">Notice that hello jobs submitted are under different user names in YARN UI:</span></span>

![Параллельное подключение пользователя 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="569bc-266">Обратите внимание также, hello новых добавленных пользователей нет корневого привилегии в системе Linux, но они имеют hello в одном получить доступ к файлам hello tooall в hello HDFS и WASB хранилище.</span><span class="sxs-lookup"><span data-stu-id="569bc-266">Note also that hello newly added users do not have root privileges in Linux system, but they do have hello same access tooall hello files in hello remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a><span data-ttu-id="569bc-267">С помощью консоли hello R</span><span class="sxs-lookup"><span data-stu-id="569bc-267">Use hello R console</span></span>

1. <span data-ttu-id="569bc-268">Из сеанса SSH hello используйте следующие командной консоли hello R toostart hello:</span><span class="sxs-lookup"><span data-stu-id="569bc-268">From hello SSH session, use hello following command toostart hello R console:</span></span>  

        R

2. <span data-ttu-id="569bc-269">Вы увидите примерно toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="569bc-269">You should see output similar toohello following:</span></span>
    
    <span data-ttu-id="569bc-270">R версии 3.2.2 (2015-08-14) — «Пожара Safety» авторское право (C) 2015 hello R Foundation для платформы статистических вычислений: x86_64-pc-linux-gnu (64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="569bc-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 hello R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="569bc-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span><span class="sxs-lookup"><span data-stu-id="569bc-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="569bc-272">Вы являетесь приветствия tooredistribute его при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="569bc-272">You are welcome tooredistribute it under certain conditions.</span></span>
    <span data-ttu-id="569bc-273">Type 'license()' or 'licence()' for distribution details.</span><span class="sxs-lookup"><span data-stu-id="569bc-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="569bc-274">Natural language support but running in an English locale</span><span class="sxs-lookup"><span data-stu-id="569bc-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="569bc-275">R is a collaborative project with many contributors.</span><span class="sxs-lookup"><span data-stu-id="569bc-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="569bc-276">Введите «contributors()» Дополнительные сведения и «citation()» на как пакеты toocite R или R в публикациях.</span><span class="sxs-lookup"><span data-stu-id="569bc-276">Type 'contributors()' for more information and 'citation()' on how toocite R or R packages in publications.</span></span>

    <span data-ttu-id="569bc-277">Введите «demo()» для некоторых демонстрациям, «help()» для интерактивной справки или «help.start()» для toohelp интерфейс браузера HTML.</span><span class="sxs-lookup"><span data-stu-id="569bc-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface toohelp.</span></span>
    <span data-ttu-id="569bc-278">Введите «q()» tooquit R.</span><span class="sxs-lookup"><span data-stu-id="569bc-278">Type 'q()' tooquit R.</span></span>

    <span data-ttu-id="569bc-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="569bc-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="569bc-280">Type 'readme()' for release notes.</span><span class="sxs-lookup"><span data-stu-id="569bc-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="569bc-281">Из hello `>` запрос, можно ввести код R.</span><span class="sxs-lookup"><span data-stu-id="569bc-281">From hello `>` prompt, you can enter R code.</span></span> <span data-ttu-id="569bc-282">R server содержит пакеты, которые позволяют вам tooeasily взаимодействовать с Hadoop и выполнения распределенных вычислений.</span><span class="sxs-lookup"><span data-stu-id="569bc-282">R server includes packages that allow you tooeasily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="569bc-283">Например можно используйте следующие команды tooview hello корневой hello по умолчанию файловой системы для кластера HDInsight hello hello:</span><span class="sxs-lookup"><span data-stu-id="569bc-283">For example, use hello following command tooview hello root of hello default file system for hello HDInsight cluster:</span></span>

    <span data-ttu-id="569bc-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="569bc-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="569bc-285">Также можно использовать hello WASB стиль адресации.</span><span class="sxs-lookup"><span data-stu-id="569bc-285">You can also use hello WASB style addressing.</span></span>

    <span data-ttu-id="569bc-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="569bc-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="569bc-287">Использование R Server в HDI из удаленного экземпляра Microsoft R Server или клиента Microsoft R Client</span><span class="sxs-lookup"><span data-stu-id="569bc-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="569bc-288">Это возможно tooset контекст вычислений HDI Hadoop Spark toohello доступа из удаленного экземпляра Microsoft R Server или Microsoft R клиента, запущенного на настольном ПК или ноутбуке.</span><span class="sxs-lookup"><span data-stu-id="569bc-288">It is possible tooset up access toohello HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="569bc-289">В разделе **с помощью Microsoft R Server как клиент Hadoop** подразделов в hello [создание контекста вычислений для Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="569bc-289">See **Using Microsoft R Server as a Hadoop Client** subsection in hello [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="569bc-290">toodo таким образом, требуются следующие параметры при определении контекста вычислений RxSpark hello на вашем ноутбуке hello toospecify: hdfsShareDir shareDir, sshUsername, sshHostname sshSwitches и sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="569bc-290">toodo so, you need toospecify hello following options when defining hello RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="569bc-291">Например:</span><span class="sxs-lookup"><span data-stu-id="569bc-291">For example:</span></span>


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a><span data-ttu-id="569bc-292">Использование контекста вычислений</span><span class="sxs-lookup"><span data-stu-id="569bc-292">Use a compute context</span></span>

<span data-ttu-id="569bc-293">Контекст вычислений позволяет toocontrol ли вычисление выполнить локально на узле edge hello или распределяется hello узлов в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-293">A compute context allows you toocontrol whether computation is performed locally on hello edge node or distributed across hello nodes in hello HDInsight cluster.</span></span>

1. <span data-ttu-id="569bc-294">В RStudio сервер или консоль hello R (в сеанс SSH) используйте следующий код tooload пример данных в хранилище по умолчанию hello для HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="569bc-294">From RStudio Server or hello R console (in an SSH session), use hello following code tooload example data into hello default storage for HDInsight:</span></span>

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="569bc-295">Теперь давайте создавать некоторые сведения о данных и определены два источника данных, чтобы мы могли работать с данными hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-295">Next, let's create some data info and define two data sources so that we can work with hello data.</span></span>

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="569bc-296">Запустим логистической регрессии hello данных с помощью hello Локальный Контекст вычислений.</span><span class="sxs-lookup"><span data-stu-id="569bc-296">Let's run a logistic regression over hello data using hello local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="569bc-297">Вы увидите выходные данные, заканчивающиеся строки аналогично toohello следующие:</span><span class="sxs-lookup"><span data-stu-id="569bc-297">You should see output that ends with lines similar toohello following:</span></span>

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. <span data-ttu-id="569bc-298">Далее запустим hello же логистической регрессии, используя контекст Spark hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-298">Next, let's run hello same logistic regression using hello Spark context.</span></span> <span data-ttu-id="569bc-299">контекст Spark Hello распределяет обработку всех hello рабочих узлов в кластере HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-299">hello Spark context distributes hello processing over all hello worker nodes in hello HDInsight cluster.</span></span>

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="569bc-300">Также можно использовать toodistribute вычислений MapReduce узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="569bc-300">You can also use MapReduce toodistribute computation across cluster nodes.</span></span> <span data-ttu-id="569bc-301">Дополнительные сведения о контексте вычислений см. в статье с описанием [параметров контекста вычислений для R Server в HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span><span class="sxs-lookup"><span data-stu-id="569bc-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-toomultiple-nodes"></a><span data-ttu-id="569bc-302">Распространение узлов toomultiple кода R</span><span class="sxs-lookup"><span data-stu-id="569bc-302">Distribute R code toomultiple nodes</span></span>

<span data-ttu-id="569bc-303">R Server позволяет легко использования существующего кода R и запустите его на нескольких узлах в кластере hello с помощью `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="569bc-303">With R Server, you can easily take existing R code and run it across multiple nodes in hello cluster by using `rxExec`.</span></span> <span data-ttu-id="569bc-304">Эта функция удобна при очистке параметров или моделировании.</span><span class="sxs-lookup"><span data-stu-id="569bc-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="569bc-305">Hello следующий код является примером toouse `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="569bc-305">hello following code is an example of how toouse `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="569bc-306">Если по-прежнему используется hello Spark или контекст MapReduce, эта команда возвращает значение имя_узла hello для hello рабочих узлов кода hello `(Sys.info()["nodename"])` выполняется на.</span><span class="sxs-lookup"><span data-stu-id="569bc-306">If you are still using hello Spark or MapReduce context, this  command returns hello nodename value for hello worker nodes that hello code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="569bc-307">Например на четыре узла кластера, ожидается, что tooreceive вывода аналогичные toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="569bc-307">For example, on a four node cluster, you expect tooreceive output similar toohello following:</span></span>

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="569bc-308">Доступ к данным в Hive и Parquet</span><span class="sxs-lookup"><span data-stu-id="569bc-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="569bc-309">Компонент, доступный в R Server 9.1 позволяет toodata прямой доступ в Hive и Parquet для использования функций ScaleR в контексте вычислений Spark hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-309">A feature available in R Server 9.1 allows direct access toodata in Hive and Parquet for use by ScaleR functions in hello Spark compute context.</span></span> <span data-ttu-id="569bc-310">Эти возможности доступны в новых данных источника функций ScaleR RxHiveData и RxParquetData, работающие с использованием данных tooload Spark SQL непосредственно в кадр данных под Spark для анализа, ScaleR.</span><span class="sxs-lookup"><span data-stu-id="569bc-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL tooload data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="569bc-311">После кода Hello предоставляет пример кода на использование новых функций hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-311">hello following code provides some sample code on use of hello new functions:</span></span>

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="569bc-312">Дополнительные сведения об использование этих новых функций см hello R Server с использованием hello `?RxHivedata` и `?RxParquetData` команд.</span><span class="sxs-lookup"><span data-stu-id="569bc-312">For additional info on use of these new functions see hello online help in R Server through use of hello `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-hello-edge-node"></a><span data-ttu-id="569bc-313">Установка дополнительных пакетов R на hello граничного узла</span><span class="sxs-lookup"><span data-stu-id="569bc-313">Install additional R packages on hello edge node</span></span>

<span data-ttu-id="569bc-314">Если необходима поддержка дополнительных пакетов R tooinstall на hello граничного узла, можно использовать `install.packages()` непосредственно из среды hello консоли R: При подключенном toohello ребро узел через SSH.</span><span class="sxs-lookup"><span data-stu-id="569bc-314">If you would like tooinstall additional R packages on hello edge node, you can use `install.packages()` directly from within hello R console when connected toohello edge node through SSH.</span></span> <span data-ttu-id="569bc-315">Тем не менее если вам требуется tooinstall пакеты R на узлах рабочих hello hello кластера, необходимо использовать действие сценария.</span><span class="sxs-lookup"><span data-stu-id="569bc-315">However, if you need tooinstall R packages on hello worker nodes of hello cluster, you must use a Script Action.</span></span>

<span data-ttu-id="569bc-316">Действия сценариев, Bash-скриптов, используемых toomake конфигурации изменения toohello HDInsight кластера или tooinstall дополнительное программное обеспечение, например дополнительных пакетов R.</span><span class="sxs-lookup"><span data-stu-id="569bc-316">Script Actions are Bash scripts that are used toomake configuration changes toohello HDInsight cluster or tooinstall additional software, such as additional R packages.</span></span> <span data-ttu-id="569bc-317">tooinstall дополнительных пакетов с помощью действия сценария, hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="569bc-317">tooinstall additional packages using a Script Action, use hello following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="569bc-318">С помощью дополнительных пакетов R действия скрипта tooinstall может использоваться только после создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-318">Using Script Actions tooinstall additional R packages can only be used after hello cluster has been created.</span></span> <span data-ttu-id="569bc-319">Не используйте эту процедуру при создании кластера как hello сценария зависит от сервера R, полностью установлен и настроен.</span><span class="sxs-lookup"><span data-stu-id="569bc-319">Do not use this procedure during cluster creation, as hello script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="569bc-320">Из hello [портал Azure](https://portal.azure.com), выберите R-сервер в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="569bc-320">From hello [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="569bc-321">Из hello **параметры** колонке выберите **действия скрипта** и затем **отправить новый** toosubmit новое действие скрипта.</span><span class="sxs-lookup"><span data-stu-id="569bc-321">From hello **Settings** blade, select **Script Actions** and then **Submit New** toosubmit a new Script Action.</span></span>

   ![Изображение колонки "Действия скрипта"](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="569bc-323">Из hello **отправить действие скрипта** колонке предоставляют hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="569bc-323">From hello **Submit script action** blade, provide hello following information:</span></span>

   * <span data-ttu-id="569bc-324">**Имя**: понятное имя tooidentify этот сценарий</span><span class="sxs-lookup"><span data-stu-id="569bc-324">**Name**: A friendly name tooidentify this script</span></span>

   * <span data-ttu-id="569bc-325">**URI bash-скрипта**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="569bc-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="569bc-326">**Заголовок**: флажок для этого элемента должен быть **снят**.</span><span class="sxs-lookup"><span data-stu-id="569bc-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="569bc-327">**Рабочая роль**: флажок для этого элемента должен быть **установлен**.</span><span class="sxs-lookup"><span data-stu-id="569bc-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="569bc-328">**Пограничные узлы**: флажок для этого элемента должен быть **снят**.</span><span class="sxs-lookup"><span data-stu-id="569bc-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="569bc-329">**Zookeeper**: флажок для этого элемента должен быть **снят**.</span><span class="sxs-lookup"><span data-stu-id="569bc-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="569bc-330">**Параметры**: hello R пакеты toobe установлен.</span><span class="sxs-lookup"><span data-stu-id="569bc-330">**Parameters**: hello R packages toobe installed.</span></span> <span data-ttu-id="569bc-331">Например, `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="569bc-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="569bc-332">**Сохранить этот скрипт…**: флажок для этого элемента должен быть **установлен**.</span><span class="sxs-lookup"><span data-stu-id="569bc-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="569bc-333">По умолчанию все пакеты R установлены из моментального снимка репозитория Microsoft MRAN hello согласование с версией hello сервера R, который был установлен.</span><span class="sxs-lookup"><span data-stu-id="569bc-333">By default, all R packages are installed from a snapshot of hello Microsoft MRAN repository consistent with hello version of R Server that has been installed.</span></span> <span data-ttu-id="569bc-334">Если требуется более новых версий пакетов tooinstall нет риску несовместимости.</span><span class="sxs-lookup"><span data-stu-id="569bc-334">If you want tooinstall newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="569bc-335">Тем не менее возможна установка такого рода, указав `useCRAN` как hello перечисления первый элемент hello пакета, например `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="569bc-335">However this kind of install is possible by specifying `useCRAN` as hello first element of hello package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="569bc-336">Для некоторых пакетов R требуются дополнительные системные библиотеки Linux.</span><span class="sxs-lookup"><span data-stu-id="569bc-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="569bc-337">Для удобства имеют предварительно установленное Затребован hello top 100 наиболее популярных пакетов r. зависимости hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-337">For convenience, we have pre-installed hello dependencies needed by hello top 100 most popular R packages.</span></span> <span data-ttu-id="569bc-338">Тем не менее если пакеты R hello устанавливаемого необходимы библиотеки Помимо этих затем необходимо загрузить здесь используется базовый скрипт hello и добавить действия tooinstall hello системные библиотеки.</span><span class="sxs-lookup"><span data-stu-id="569bc-338">However, if hello R package(s) you install require libraries beyond these then you must download hello base script used here and add steps tooinstall hello system libraries.</span></span> <span data-ttu-id="569bc-339">Необходимо затем public tooa скрипт изменения hello передачи больших двоичных объектов контейнера в хранилище Azure и использовать пакеты hello tooinstall скрипт изменения hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-339">You must then upload hello modified script tooa public blob container in Azure storage and use hello modified script tooinstall hello packages.</span></span>
   >    <span data-ttu-id="569bc-340">Дополнительные сведения см. в статье [Разработка действий сценариев с помощью HDInsight](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="569bc-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Добавление действия сценария](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="569bc-342">Выберите **создать** toorun hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="569bc-342">Select **Create** toorun hello script.</span></span> <span data-ttu-id="569bc-343">После завершения сценария hello hello R-пакеты доступны на всех рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="569bc-343">Once hello script completes, hello R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="569bc-344">Ввод в эксплуатацию для Microsoft R Server</span><span class="sxs-lookup"><span data-stu-id="569bc-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="569bc-345">По завершении моделирование данных вы ввода в эксплуатацию hello модели toomake прогнозов.</span><span class="sxs-lookup"><span data-stu-id="569bc-345">When your data modeling is complete, you can operationalize hello model toomake predictions.</span></span> <span data-ttu-id="569bc-346">tooconfigure для ввода в эксплуатацию Microsoft R Server, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-346">tooconfigure for Microsoft R Server operationalization, perform hello following steps:</span></span>

<span data-ttu-id="569bc-347">Во-первых, ssh в hello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="569bc-347">First, ssh into hello Edge node.</span></span> <span data-ttu-id="569bc-348">Например,</span><span class="sxs-lookup"><span data-stu-id="569bc-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="569bc-349">После использования ssh, измените каталог для соответствующей версии hello и sudo hello dotnet dll:</span><span class="sxs-lookup"><span data-stu-id="569bc-349">After using ssh, change directory for hello relevant version and sudo hello dotnet dll:</span></span> 

- <span data-ttu-id="569bc-350">Для Microsoft R Server 9.1:</span><span class="sxs-lookup"><span data-stu-id="569bc-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="569bc-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0 sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="569bc-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="569bc-352">Для Microsoft R Server 9.0:</span><span class="sxs-lookup"><span data-stu-id="569bc-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="569bc-353">cd /usr/lib64/microsoft-deployr/9.0.1 sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="569bc-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="569bc-354">tooconfigure Microsoft R Server ввода в эксплуатацию в одно поле конфигурации hello следующие:</span><span class="sxs-lookup"><span data-stu-id="569bc-354">tooconfigure Microsoft R Server operationalization with a One-box configuration do hello following:</span></span>

1. <span data-ttu-id="569bc-355">Выберите Configure R Server for Operationalization (Настройка R Server для ввода в эксплуатацию).</span><span class="sxs-lookup"><span data-stu-id="569bc-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="569bc-356">Выберите "A.</span><span class="sxs-lookup"><span data-stu-id="569bc-356">Select “A.</span></span> <span data-ttu-id="569bc-357">One-box (web + compute nodes)" (A. Универсальная (веб + вычислительные узлы)).</span><span class="sxs-lookup"><span data-stu-id="569bc-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="569bc-358">Введите пароль для hello **администратора** пользователя</span><span class="sxs-lookup"><span data-stu-id="569bc-358">Enter a password for hello **admin** user</span></span>

![Универсальная конфигурация](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="569bc-360">В качестве дополнительного шага можно запустить диагностический тест, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="569bc-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="569bc-361">Выберите "6.</span><span class="sxs-lookup"><span data-stu-id="569bc-361">Select “6.</span></span> <span data-ttu-id="569bc-362">Run diagnostic tests" (6. Запуск диагностических тестов).</span><span class="sxs-lookup"><span data-stu-id="569bc-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="569bc-363">Выберите "A.</span><span class="sxs-lookup"><span data-stu-id="569bc-363">Select “A.</span></span> <span data-ttu-id="569bc-364">Test configuration" (А. Проверка конфигурации).</span><span class="sxs-lookup"><span data-stu-id="569bc-364">Test configuration”</span></span>
3. <span data-ttu-id="569bc-365">Введите имя пользователя admin и пароль, настроенный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="569bc-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="569bc-366">Убедитесь, что общая проверка работоспособности проходит успешно (Overall Health = pass).</span><span class="sxs-lookup"><span data-stu-id="569bc-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="569bc-367">Программа администрирования hello выхода</span><span class="sxs-lookup"><span data-stu-id="569bc-367">Exit hello Admin Utility</span></span>
6. <span data-ttu-id="569bc-368">Завершите сеанс SSH.</span><span class="sxs-lookup"><span data-stu-id="569bc-368">Exit SSH</span></span>

![Диагностика перед вводом в эксплуатацию](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="569bc-370">**Длительные задержки при использовании веб-службы на Spark**</span><span class="sxs-lookup"><span data-stu-id="569bc-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="569bc-371">Если возникают значительные задержки при попытке tooconsume веб-службы с mrsdeploy функции в контексте вычислений Spark, может потребоваться tooadd некоторые отсутствующие папки.</span><span class="sxs-lookup"><span data-stu-id="569bc-371">If you encounter long delays when trying tooconsume a web service created with mrsdeploy functions in a Spark compute context, you may need tooadd some missing folders.</span></span> <span data-ttu-id="569bc-372">Spark приложения Hello принадлежит tooa пользователя с именем "*rserve2*" каждый раз, когда она вызывается из веб-службы с помощью функции mrsdeploy.</span><span class="sxs-lookup"><span data-stu-id="569bc-372">hello Spark application belongs tooa user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="569bc-373">toowork этой проблемы:</span><span class="sxs-lookup"><span data-stu-id="569bc-373">toowork around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="569bc-374">На этом этапе будет завершена настройка hello для ввода в эксплуатацию.</span><span class="sxs-lookup"><span data-stu-id="569bc-374">At this stage, hello configuration for Operationalization is complete.</span></span> <span data-ttu-id="569bc-375">Теперь вы можете использовать mrsdeploy «hello» пакет в вашей toohello tooconnect RClient ввода в эксплуатацию на граничного узла и приступить к использованию, ее функции, такие как [удаленное выполнение](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) и [веб-службы](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="569bc-375">Now you can use hello ‘mrsdeploy’ package on your RClient tooconnect toohello Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="569bc-376">В зависимости от того, является ли кластер настроен в виртуальной сети или нет может понадобиться tooset копирование прямой туннелирования порта с помощью имени входа SSH.</span><span class="sxs-lookup"><span data-stu-id="569bc-376">Depending on whether your cluster is set up on a virtual network or not, you may need tooset up port forward tunneling through SSH login.</span></span> <span data-ttu-id="569bc-377">Hello следующих разделах объясняется, как tooset копирование этот туннель.</span><span class="sxs-lookup"><span data-stu-id="569bc-377">hello following sections explain how tooset up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="569bc-378">Кластер R Server в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="569bc-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="569bc-379">Убедитесь, что прохождение трафика через порт 12800 toohello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="569bc-379">Make sure you allow traffic through port 12800 toohello edge node.</span></span> <span data-ttu-id="569bc-380">Таким образом, можно использовать функция hello edge узла tooconnect toohello ввода в эксплуатацию.</span><span class="sxs-lookup"><span data-stu-id="569bc-380">That way, you can use hello edge node tooconnect toohello Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="569bc-381">Если hello `remoteLogin()` невозможно подключение toohello граничного узла, но можно SSH toohello граничного узла, затем требуется tooverify ли hello правило tooallow трафик через порт 12800 установлено должным образом или не.</span><span class="sxs-lookup"><span data-stu-id="569bc-381">If hello `remoteLogin()` cannot connect toohello edge node, but you can SSH toohello edge node, then you need tooverify whether hello rule tooallow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="569bc-382">В случае продолжения tooface hello проблему можно обойти путем настройки прямого туннелирования порта с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="569bc-382">If you continue tooface hello issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="569bc-383">Инструкции см. в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-383">For instructions, see hello following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="569bc-384">Кластер RServer не настроен в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="569bc-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="569bc-385">Если ваш кластер не настроен в виртуальной сети или с подключением через виртуальную сеть возникают проблемы, можно использовать туннелирование с перенаправлением портов через SSH:</span><span class="sxs-lookup"><span data-stu-id="569bc-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="569bc-386">Также это можно настроить с помощью программы Putty.</span><span class="sxs-lookup"><span data-stu-id="569bc-386">On Putty, you can set it up as well.</span></span>

![Подключение SSH через Putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="569bc-388">Hello трафика с порта компьютера 12800 активен сеанс SSH, будут отправлены toohello граничного узла порт 12800 через сеанс SSH.</span><span class="sxs-lookup"><span data-stu-id="569bc-388">Once your SSH session is active, hello traffic from your machine’s port 12800 is forwarded toohello edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="569bc-389">Убедитесь, что вы используете `127.0.0.1:12800` в методе `remoteLogin()`.</span><span class="sxs-lookup"><span data-stu-id="569bc-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="569bc-390">Регистрирует ввода в эксплуатацию toohello граничного узла через перенаправления портов.</span><span class="sxs-lookup"><span data-stu-id="569bc-390">This logs in toohello edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="569bc-391">Как tooscale Microsoft R Server ввода в эксплуатацию вычислительных узлов на HDInsight рабочих узлов</span><span class="sxs-lookup"><span data-stu-id="569bc-391">How tooscale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-hello-worker-nodes"></a><span data-ttu-id="569bc-392">Списание узлы рабочих hello</span><span class="sxs-lookup"><span data-stu-id="569bc-392">Decommission hello worker node(s)</span></span>

<span data-ttu-id="569bc-393">Управление Microsoft R Server через Yarn сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="569bc-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="569bc-394">Hello рабочих узлов, не выводится из эксплуатации, hello Yarn диспетчер ресурсов не будет работать, как ожидается, поскольку он не будет знать о они занимают hello server ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="569bc-394">If hello worker nodes are not decommissioned, hello Yarn Resource Manager will not work as expected because it will not be aware of hello resources being taken up by hello server.</span></span> <span data-ttu-id="569bc-395">В порядке tooavoid этой ситуации рекомендуется списание hello рабочих узлов, прежде чем масштабировать hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="569bc-395">In order tooavoid this situation, we recommend decommissioning hello worker nodes before you scale out hello compute nodes.</span></span>

<span data-ttu-id="569bc-396">Действия toodecommissioning рабочих узлов:</span><span class="sxs-lookup"><span data-stu-id="569bc-396">Steps toodecommissioning worker nodes:</span></span>

* <span data-ttu-id="569bc-397">Войдите в консоль Ambari tooHDI кластера и нажмите на вкладке «узлы»</span><span class="sxs-lookup"><span data-stu-id="569bc-397">Log in tooHDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="569bc-398">Выберите рабочих узлов (toobe вывода из эксплуатации), щелкните «Действия» > «Выбранные узлы» > «Узлы» > щелкните «Включить режим обслуживания ON».</span><span class="sxs-lookup"><span data-stu-id="569bc-398">Select worker nodes (toobe decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="569bc-399">Например в следующие изображения hello мы выбрали wn3 и wn4 toodecommission.</span><span class="sxs-lookup"><span data-stu-id="569bc-399">For example, in hello following image we have selected wn3 and wn4 toodecommission.</span></span>  

   ![Вывод рабочих узлов из эксплуатации](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="569bc-401">Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **DataNodes** (Узлы данных) и щелкните **Decommission** (Вывести из эксплуатации).</span><span class="sxs-lookup"><span data-stu-id="569bc-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="569bc-402">Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **NodeManagers** (Диспетчеры узлов) и щелкните **Decommission** (Вывести из эксплуатации).</span><span class="sxs-lookup"><span data-stu-id="569bc-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="569bc-403">Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **DataNodes** (Узлы данных) и щелкните **Stop** (Остановить).</span><span class="sxs-lookup"><span data-stu-id="569bc-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="569bc-404">Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **NodeManagers** (Диспетчеры узлов) и щелкните **Stop** (Остановить).</span><span class="sxs-lookup"><span data-stu-id="569bc-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="569bc-405">Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **Hosts** (Узлы) и щелкните **Stop All Components** (Остановить все компоненты).</span><span class="sxs-lookup"><span data-stu-id="569bc-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="569bc-406">Снимите флажок hello рабочих узлов, а затем выберите hello головного узла</span><span class="sxs-lookup"><span data-stu-id="569bc-406">Unselect hello worker nodes and select hello head nodes</span></span>
* <span data-ttu-id="569bc-407">Выберите **Actions** (Действия) > **Selected Hosts** (Выбранные узлы) > **Hosts** (Узлы) > **Restart All Components** (Перезапустить все компоненты).</span><span class="sxs-lookup"><span data-stu-id="569bc-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="569bc-408">Настройка вычислительных узлов на каждом из рабочих узлов, выведенных из эксплуатации</span><span class="sxs-lookup"><span data-stu-id="569bc-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="569bc-409">Поочередно откройте сеанс SSH для каждого рабочего узла, выведенного из эксплуатации.</span><span class="sxs-lookup"><span data-stu-id="569bc-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="569bc-410">Запустите служебную программу администрирования с помощью `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span><span class="sxs-lookup"><span data-stu-id="569bc-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="569bc-411">Введите «1» tooselect параметр «Настройка R Server для ввода в эксплуатацию».</span><span class="sxs-lookup"><span data-stu-id="569bc-411">Enter "1" tooselect option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="569bc-412">Введите «c» tooselect параметр «C.</span><span class="sxs-lookup"><span data-stu-id="569bc-412">Enter "c" tooselect option "C.</span></span> <span data-ttu-id="569bc-413">Compute node" (C. Вычислительный узел).</span><span class="sxs-lookup"><span data-stu-id="569bc-413">Compute node".</span></span> <span data-ttu-id="569bc-414">Это настраивает hello вычислительных узлов на узле hello работника.</span><span class="sxs-lookup"><span data-stu-id="569bc-414">This configures hello compute node on hello worker node.</span></span>
5. <span data-ttu-id="569bc-415">Программа администрирования hello выхода.</span><span class="sxs-lookup"><span data-stu-id="569bc-415">Exit hello Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="569bc-416">Добавление сведений о вычислительных узлах на веб-узел</span><span class="sxs-lookup"><span data-stu-id="569bc-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="569bc-417">После настройки всех списанных рабочих узлов toorun вычислительного узла, вернитесь на hello граничного узла и добавления узлов Отмененный рабочий IP-адресов в конфигурации узла для hello Microsoft R Server web:</span><span class="sxs-lookup"><span data-stu-id="569bc-417">Once all decommissioned worker nodes have been configured toorun compute node, come back on hello edge node and add decommissioned worker nodes' IP addresses in hello Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="569bc-418">SSH в hello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="569bc-418">SSH into hello edge node.</span></span>
* <span data-ttu-id="569bc-419">Запустите `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="569bc-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="569bc-420">Найдите раздел «Идентификаторы URI» hello и добавьте рабочий узел IP-адрес и сведения о порте.</span><span class="sxs-lookup"><span data-stu-id="569bc-420">Look for hello "URIs" section, and add worker node's IP and port details.</span></span>

    ![Командная строка для выведенных из эксплуатации рабочих узлов](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="569bc-422">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="569bc-422">Troubleshoot</span></span>

<span data-ttu-id="569bc-423">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="569bc-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="569bc-424">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="569bc-424">Next steps</span></span>

<span data-ttu-id="569bc-425">Теперь следует понимать, как toocreate новый кластер HDInsight, включающий hello R Server и hello основные принципы использования hello консоль R из сеанса SSH.</span><span class="sxs-lookup"><span data-stu-id="569bc-425">Now you should understand how toocreate a new HDInsight cluster that includes hello R Server and hello basics of using hello R console from an SSH session.</span></span> <span data-ttu-id="569bc-426">Hello следующих разделах описаны другие способы управления и работы с сервером R в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="569bc-426">hello following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="569bc-427">Добавить tooHDInsight RStudio сервера (если не устанавливается во время создания кластера)</span><span class="sxs-lookup"><span data-stu-id="569bc-427">Add RStudio Server tooHDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="569bc-428">Варианты контекста вычислений для R Server в HDInsight</span><span class="sxs-lookup"><span data-stu-id="569bc-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="569bc-429">Параметры службы хранилища Azure для R Server в HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="569bc-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
