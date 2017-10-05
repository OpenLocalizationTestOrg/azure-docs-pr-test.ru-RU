---
title: "Настройка кластеров Hadoop для процесса обработки и анализа данных группы | Документация Майкрософт"
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
ms.openlocfilehash: 53ff04ee66b08ae36f3550536c659a547c658fd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-the-team-data-science-process"></a><span data-ttu-id="0b3a6-103">Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы</span><span class="sxs-lookup"><span data-stu-id="0b3a6-103">Customize Azure HDInsight Hadoop clusters for the Team Data Science Process</span></span>
<span data-ttu-id="0b3a6-104">В этой статье рассказывается о том, как настроить кластер Hadoop под управлением службы HDInsight, установив 64-разрядную версию программы Anaconda (Python 2.7) на каждом узле в процессе подготовки кластера как службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-104">This article describes how to customize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when the cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="0b3a6-105">Здесь также приведена информация о том, как получить доступ к головному узлу для отправки пользовательских заданий в кластер.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-105">It also shows how to access the headnode to submit custom jobs to the cluster.</span></span> <span data-ttu-id="0b3a6-106">В результате этой настройки многие популярные модули Python, входящие в состав программы Anaconda, станут доступными для использования в определяемых пользователями функциях (UDF), предназначенных для обработки записей Hive в кластере.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed to process Hive records in the cluster.</span></span> <span data-ttu-id="0b3a6-107">Инструкции по процедурам, которые используются в этом сценарии, см. в разделе [Отправка запросов Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="0b3a6-107">For instructions on the procedures used in this scenario, see [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="0b3a6-108">Это меню содержит ссылки на разделы, описывающие настройку различных сред обработки и анализа данных, используемых [процессом обработки и анализа данных группы (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b3a6-108">The following menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="0b3a6-109"><a name="customize"></a>Настройка кластера Hadoop под управлением службы Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0b3a6-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="0b3a6-110">Чтобы создать настраиваемый кластер Hadoop под управлением службы HDInsight, необходимо войти на [**классический портал Azure**](https://manage.windowsazure.com/), щелкнуть **Создать** в левом нижнем углу, а затем выбрать "Службы данных > HDInsight" > **Настраиваемое создание**, чтобы открыть окно **Сведения о кластере**.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-110">To create a customized HDInsight Hadoop cluster, start by logging on to [**Azure classic portal**](https://manage.windowsazure.com/), click **New** at the left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** to bring up the **Cluster Details** window.</span></span> 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="0b3a6-112">Введите имя создаваемого кластера на 1-й странице настройки конфигурации и примите значения по умолчанию для других полей.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-112">Input the name of the cluster to be created on configuration page 1, and accept default values for the other fields.</span></span> <span data-ttu-id="0b3a6-113">Щелкните стрелку, чтобы перейти к следующей странице конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-113">Click the arrow to go to the next configuration page.</span></span> 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="0b3a6-115">На странице 2 конфигурации введите количество в поле **Узлы данных**, выберите значение в поле **Регион или виртуальная сеть** и выберите размеры в полях **Головной узел** и **Узел данных**.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-115">On configuration page 2, input the number of **DATA NODES**, select the **REGION/VIRTUAL NETWORK**, and select the sizes of the **HEAD NODE** and the **DATA NODE**.</span></span> <span data-ttu-id="0b3a6-116">Щелкните стрелку, чтобы перейти к следующей странице конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-116">Click the arrow to go to the next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="0b3a6-117">Значение, выбранное в поле **РЕГИОН ИЛИ ВИРТУАЛЬНАЯ СЕТЬ** , должно соответствовать региону, указанному для учетной записи хранения, которая будет использоваться для кластера Hadoop под управлением службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-117">The **REGION/VIRTUAL NETWORK** has to be the same as the region of the storage account that is going to be used for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="0b3a6-118">В противном случае учетная запись хранения не будет отображаться в раскрывающемся списке **Имя учетной записи** на четвертой странице настройки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-118">Otherwise, in the fourth configuration page, the storage account will not appear on the dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="0b3a6-120">На 3-й странице настройки конфигурации укажите имя пользователя и пароль для кластера Hadoop под управлением службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-120">On configuration page 3, provide a user name and password for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="0b3a6-121">**Не** устанавливайте флажок *Ввести куст или метахранилище Oozie*.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-121">**Do not** select the *Enter the Hive/Oozie Metastore*.</span></span> <span data-ttu-id="0b3a6-122">Затем щелкните стрелку, чтобы перейти к следующей странице конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-122">Then, click the arrow to go to the next configuration page.</span></span> 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="0b3a6-124">На 4-й странице настройки конфигурации задайте имя учетной записи хранения и контейнер кластера Hadoop под управлением службы HDInsight по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-124">On configuration page 4, specify the storage account name, the default container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="0b3a6-125">Если в раскрывающемся списке **Контейнер по умолчанию** выбрать параметр *Создать контейнер по умолчанию*, будет создан контейнер с тем же именем, что у кластера.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-125">If you select *Create default container* in the **DEFAULT CONTAINER** dropdown list, a container with the same name as the cluster will be created.</span></span> <span data-ttu-id="0b3a6-126">Щелкните стрелку, чтобы перейти к последней странице конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-126">Click the arrow to go to the last configuration page.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="0b3a6-128">На последней странице настройки конфигурации **Действия скрипта** нажмите кнопку **Добавить действие скрипта** и заполните текстовые поля следующими значениями.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-128">On the final **Script Actions** configuration page, click **add script action** button, and fill the text fields with the following values.</span></span>

* <span data-ttu-id="0b3a6-129">**Имя** — любая строка, соответствующая имени этого действия сценария.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-129">**NAME** - any string as the name of this script action</span></span>
* <span data-ttu-id="0b3a6-130">**Тип узла** — выберите значение **Все узлы**.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="0b3a6-131">**URI-адрес скрипта**  - —*http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="0b3a6-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="0b3a6-132">*publicscripts* — это общий контейнер в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-132">*publicscripts* is a public container in the storage account</span></span> 
  * <span data-ttu-id="0b3a6-133">*getgoing* — используется для совместного доступа к файлам сценариев PowerShell, чтобы упростить работу пользователей в Azure.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-133">*getgoing* we use to share PowerShell script files to facilitate users' work in Azure</span></span>
* <span data-ttu-id="0b3a6-134">**ПАРАМЕТРЫ** — оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="0b3a6-135">Наконец, щелкните значок с изображением флажка, чтобы начать создание настраиваемого кластера Hadoop под управлением службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-135">Finally, click the check mark to start the creation of the customized HDInsight Hadoop cluster.</span></span> 

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="0b3a6-137"><a name="headnode"></a> Получение доступа к головному узлу кластера Hadoop</span><span class="sxs-lookup"><span data-stu-id="0b3a6-137"><a name="headnode"></a> Access the Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="0b3a6-138">Чтобы получить доступ к головному узлу кластера Hadoop по протоколу RDP, необходимо включить удаленный доступ к кластеру Hadoop в Azure.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-138">You must enable remote access to the Hadoop cluster in Azure before you can access the head node of the Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="0b3a6-139">Перейдите на [**классический портал Azure**](https://manage.windowsazure.com/), щелкните **HDInsight** в левой части страницы, выберите кластер Hadoop в списке кластеров, перейдите на вкладку **Конфигурация**, а затем щелкните значок **Включить удаленный доступ** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-139">Log in to the [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on the left, select your Hadoop cluster from the list of clusters, click the **CONFIGURATION** tab, and then click the **ENABLE REMOTE** icon at the bottom of the page.</span></span>
   
    ![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="0b3a6-141">В окне **Настройка удаленного рабочего стола** введите значения в полях «ИМЯ ПОЛЬЗОВАТЕЛЯ» и «ПАРОЛЬ» и выберите дату окончания срока действия для удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-141">In the **Configure Remote Desktop** window, enter the USER NAME and PASSWORD fields, and select the expiration date for remote access.</span></span> <span data-ttu-id="0b3a6-142">Затем щелкните значок с изображением флажка, чтобы включить удаленный доступ к головному узлу кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-142">Then click the check mark to enable the remote access to the head node of the Hadoop cluster.</span></span>
   
    ![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="0b3a6-144">Имя пользователя и пароль для удаленного доступа должны отличаться от имени пользователя и пароля, которые использовались при создании кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-144">The user name and password for the remote access are not the user name and password that you use when you created the Hadoop cluster.</span></span> <span data-ttu-id="0b3a6-145">Это отдельный набор учетных данных.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-145">This is a separate set of credentials.</span></span> <span data-ttu-id="0b3a6-146">Срок действия удаленного доступа должен истечь не позднее чем через 7 дней с текущей даты.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-146">Also, the expiration date of the remote access has to be within 7 days from the current date.</span></span>
> 
> 

<span data-ttu-id="0b3a6-147">После включения удаленного доступа щелкните **ПОДКЛЮЧИТЬСЯ** в нижней части страницы, чтобы получить удаленный доступ к головному узлу.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-147">After remote access is enabled, click **CONNECT** at the bottom of the page to remote into the head node.</span></span> <span data-ttu-id="0b3a6-148">Войдите на головной узел кластера Hadoop, указав заданные ранее учетные данные для удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-148">You log on to the head node of the Hadoop cluster by entering the credentials for the remote access user that you specified earlier.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="0b3a6-150">Дальнейшие действия по подготовке и обработке аналитических данных можно найти в статье [Процесс обработки и анализа данных группы](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/). Они могут включать в себя операции с перемещением данных в HDInsight, их обработкой и выборкой для подготовки к обучению по данным с помощью Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0b3a6-150">The next steps in the advanced analytics process are mapped in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

<span data-ttu-id="0b3a6-151">Инструкции по получению доступа к модулям Python, которые входят в состав программы Anaconda, с головного узла кластера в пользовательских функциях, предназначенных для обработки записей Hive, которые хранятся в кластере, см. в разделе [Отправка запросов Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="0b3a6-151">See [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how to access the Python modules that are included in Anaconda from the head node of the cluster in user-defined functions (UDFs) that are used to process Hive records stored in the cluster.</span></span>

