---
title: "кластеры aaaCustomize Hadoop для hello командного процесса обработки и анализа данных | Документы Microsoft"
description: "Популярные модули Python становятся доступными в настраиваемых кластерах Azure HDInsight Hadoop."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a><span data-ttu-id="5af12-103">Настроить кластеры Azure HDInsight Hadoop для hello командного процесса обработки и анализа данных</span><span class="sxs-lookup"><span data-stu-id="5af12-103">Customize Azure HDInsight Hadoop clusters for hello Team Data Science Process</span></span>
<span data-ttu-id="5af12-104">Данной статье рассмотрены как кластер HDInsight Hadoop toocustomize путем установки 64-разрядных Anaconda (Python 2.7) на каждом узле кластера hello предоставляется в качестве службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5af12-104">This article describes how toocustomize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when hello cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="5af12-105">Здесь также показано, как tooaccess hello головному узлу toosubmit пользовательские задания toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="5af12-105">It also shows how tooaccess hello headnode toosubmit custom jobs toohello cluster.</span></span> <span data-ttu-id="5af12-106">Такая настройка позволяет многие популярные Python модули, которые включены в Anaconda, поскольку удобно доступна для использования в пользователя определенные функции (UDF), которые являются предназначен tooprocess записей Hive в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="5af12-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed tooprocess Hive records in hello cluster.</span></span> <span data-ttu-id="5af12-107">Инструкции по hello процедуры, используемые в этом сценарии см. в разделе [как запросы Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="5af12-107">For instructions on hello procedures used in this scenario, see [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="5af12-108">Hello следующее меню ссылки, описывающие возможности tooset копирование hello различных средах обработки и анализа данных по использованию hello tootopics [процесса обработки и анализа данных Team (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5af12-108">hello following menu links tootopics that describe how tooset up hello various data science environments used by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="5af12-109"><a name="customize"></a>Настройка кластера Hadoop под управлением службы Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5af12-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="5af12-110">Запуск toocreate настроенные кластера HDInsight Hadoop, войдя в систему слишком[**классический портал Azure**](https://manage.windowsazure.com/), нажмите кнопку **New** на hello слева вниз углу, а затем выберите службы данных HDINSIGHT -> -> **НАСТРАИВАЕМОЕ создание** toobring копирование hello **сведения о кластере** окна.</span><span class="sxs-lookup"><span data-stu-id="5af12-110">toocreate a customized HDInsight Hadoop cluster, start by logging on too[**Azure classic portal**](https://manage.windowsazure.com/), click **New** at hello left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** toobring up hello **Cluster Details** window.</span></span> 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="5af12-112">Ввод hello имя кластера toobe hello, созданные на странице конфигурации 1 и примите значения по умолчанию для hello другие поля.</span><span class="sxs-lookup"><span data-stu-id="5af12-112">Input hello name of hello cluster toobe created on configuration page 1, and accept default values for hello other fields.</span></span> <span data-ttu-id="5af12-113">Щелкните hello стрелка toogo toohello следующей странице конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5af12-113">Click hello arrow toogo toohello next configuration page.</span></span> 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="5af12-115">На странице конфигурации 2, введите число hello **УЗЛЫ данных**выберите hello **регион или ВИРТУАЛЬНАЯ сеть**и выберите размеры hello hello **ГОЛОВНОГО узла** и hello **Узел данных**.</span><span class="sxs-lookup"><span data-stu-id="5af12-115">On configuration page 2, input hello number of **DATA NODES**, select hello **REGION/VIRTUAL NETWORK**, and select hello sizes of hello **HEAD NODE** and hello **DATA NODE**.</span></span> <span data-ttu-id="5af12-116">Щелкните hello стрелка toogo toohello следующей странице конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5af12-116">Click hello arrow toogo toohello next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="5af12-117">Hello **регион или ВИРТУАЛЬНАЯ сеть** имеет toobe Здравствуйте таким же, как область hello hello учетной записи хранения, что будет toobe для hello кластера HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5af12-117">hello **REGION/VIRTUAL NETWORK** has toobe hello same as hello region of hello storage account that is going toobe used for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="5af12-118">В противном случае hello четвертой странице конфигурации учетной записи хранилища hello не отображаются на раскрывающийся список hello **имя учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="5af12-118">Otherwise, in hello fourth configuration page, hello storage account will not appear on hello dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="5af12-120">На странице конфигурации 3 укажите имя пользователя и пароль для hello кластера HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5af12-120">On configuration page 3, provide a user name and password for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="5af12-121">**Не** выберите hello *ввод hello куст или Метахранилище Oozie*.</span><span class="sxs-lookup"><span data-stu-id="5af12-121">**Do not** select hello *Enter hello Hive/Oozie Metastore*.</span></span> <span data-ttu-id="5af12-122">Нажмите кнопку hello стрелка toogo toohello следующей странице конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5af12-122">Then, click hello arrow toogo toohello next configuration page.</span></span> 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="5af12-124">На странице конфигурации 4 укажите имя учетной записи хранения hello, контейнер по умолчанию hello hello кластера HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5af12-124">On configuration page 4, specify hello storage account name, hello default container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="5af12-125">При выборе *создать контейнер по умолчанию* в hello **КОНТЕЙНЕР по умолчанию** раскрывающийся список, контейнер с помощью hello точно такое же имя, как будет создан кластер hello.</span><span class="sxs-lookup"><span data-stu-id="5af12-125">If you select *Create default container* in hello **DEFAULT CONTAINER** dropdown list, a container with hello same name as hello cluster will be created.</span></span> <span data-ttu-id="5af12-126">Щелкните hello стрелка toogo toohello последней конфигурации страницы.</span><span class="sxs-lookup"><span data-stu-id="5af12-126">Click hello arrow toogo toohello last configuration page.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="5af12-128">На последней hello **действия скрипта** «конфигурация» нажмите кнопку **добавьте действия скрипта** кнопку и заполнения поля текст hello hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="5af12-128">On hello final **Script Actions** configuration page, click **add script action** button, and fill hello text fields with hello following values.</span></span>

* <span data-ttu-id="5af12-129">**ИМЯ** -любую строку как имя действия сценария hello</span><span class="sxs-lookup"><span data-stu-id="5af12-129">**NAME** - any string as hello name of this script action</span></span>
* <span data-ttu-id="5af12-130">**Тип узла** — выберите значение **Все узлы**.</span><span class="sxs-lookup"><span data-stu-id="5af12-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="5af12-131">**URI-адрес скрипта**  - —*http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="5af12-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="5af12-132">*publicscripts* — это открытый контейнер в учетной записи хранения hello</span><span class="sxs-lookup"><span data-stu-id="5af12-132">*publicscripts* is a public container in hello storage account</span></span> 
  * <span data-ttu-id="5af12-133">*getgoing* мы используем tooshare PowerShell скрипт файлы toofacilitate работы пользователей в Azure</span><span class="sxs-lookup"><span data-stu-id="5af12-133">*getgoing* we use tooshare PowerShell script files toofacilitate users' work in Azure</span></span>
* <span data-ttu-id="5af12-134">**ПАРАМЕТРЫ** — оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="5af12-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="5af12-135">Щелкните флажок hello toostart Создание hello hello настроить кластер HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5af12-135">Finally, click hello check mark toostart hello creation of hello customized HDInsight Hadoop cluster.</span></span> 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="5af12-137"><a name="headnode"></a>Доступ к hello головного узла кластера Hadoop</span><span class="sxs-lookup"><span data-stu-id="5af12-137"><a name="headnode"></a> Access hello Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="5af12-138">Прежде чем можно обращаться из головного узла кластера Hadoop hello hello протокола удаленного рабочего СТОЛА необходимо включить кластера Hadoop toohello удаленного доступа в Azure.</span><span class="sxs-lookup"><span data-stu-id="5af12-138">You must enable remote access toohello Hadoop cluster in Azure before you can access hello head node of hello Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="5af12-139">Войдите в toohello [ **классический портал Azure**](https://manage.windowsazure.com/)выберите **HDInsight** hello левой части экрана выберите кластер Hadoop из списка кластеров hello, щелкните hello  **КОНФИГУРАЦИЯ** , а затем щелкните hello **ВКЛЮЧИТЬ УДАЛЕННЫЙ** значок hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="5af12-139">Log in toohello [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on hello left, select your Hadoop cluster from hello list of clusters, click hello **CONFIGURATION** tab, and then click hello **ENABLE REMOTE** icon at hello bottom of hello page.</span></span>
   
    ![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="5af12-141">В hello **настроить удаленный рабочий стол** , введите hello ИМЕНИ пользователя и пароля и выберите пункт hello Дата окончания срока действия для удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="5af12-141">In hello **Configure Remote Desktop** window, enter hello USER NAME and PASSWORD fields, and select hello expiration date for remote access.</span></span> <span data-ttu-id="5af12-142">Нажмите кнопку hello флажок tooenable hello удаленного доступа toohello головного узла кластера Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="5af12-142">Then click hello check mark tooenable hello remote access toohello head node of hello Hadoop cluster.</span></span>
   
    ![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="5af12-144">Hello имя пользователя и пароль для удаленного доступа hello не hello имя пользователя и пароль, используемый при создании кластера Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="5af12-144">hello user name and password for hello remote access are not hello user name and password that you use when you created hello Hadoop cluster.</span></span> <span data-ttu-id="5af12-145">Это отдельный набор учетных данных.</span><span class="sxs-lookup"><span data-stu-id="5af12-145">This is a separate set of credentials.</span></span> <span data-ttu-id="5af12-146">Кроме того Дата окончания срока действия hello hello удаленного доступа имеет toobe в течение 7 дней после hello текущую дату.</span><span class="sxs-lookup"><span data-stu-id="5af12-146">Also, hello expiration date of hello remote access has toobe within 7 days from hello current date.</span></span>
> 
> 

<span data-ttu-id="5af12-147">После включения удаленного доступа щелкните **CONNECT** внизу hello tooremote страницы приветствия на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="5af12-147">After remote access is enabled, click **CONNECT** at hello bottom of hello page tooremote into hello head node.</span></span> <span data-ttu-id="5af12-148">Вход toohello головного узла кластера Hadoop hello, введя hello учетные данные пользователя удаленного доступа hello, указанный ранее.</span><span class="sxs-lookup"><span data-stu-id="5af12-148">You log on toohello head node of hello Hadoop cluster by entering hello credentials for hello remote access user that you specified earlier.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="5af12-150">Hello следующим шагам в hello advanced analytics процесса сопоставлены в hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) и могут содержать действия, которые перемещение данных в HDInsight, а затем обрабатывают и образец он существует в процессе подготовки для обучения на основе данных hello с помощью машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="5af12-150">hello next steps in hello advanced analytics process are mapped in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

<span data-ttu-id="5af12-151">В разделе [как запросы Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) инструкции как tooaccess hello Python модулей, включенных в Anaconda из hello головного узла кластера hello в определяемые пользователем функции (UDF), которые используется tooprocess Hive записей, хранимых в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="5af12-151">See [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how tooaccess hello Python modules that are included in Anaconda from hello head node of hello cluster in user-defined functions (UDFs) that are used tooprocess Hive records stored in hello cluster.</span></span>

