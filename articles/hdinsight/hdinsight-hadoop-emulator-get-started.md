---
title: "с помощью изолированной среде Hadoop — эмулятор — Azure HDInsight aaaLearn | Документы Microsoft"
description: "обучающие материалы по с помощью toostart Здравствуйте экосистема Hadoop, настройкой изолированной среде Hadoop из Hortonworks на виртуальной машине Azure. "
keywords: "эмулятор hadoop,песочница hadoop"
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 91e74f0823fd02e9bb812155a7d09357a77b0736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="cb8be-104">Начало работы с песочницей Hadoop, эмулятором на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="cb8be-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="cb8be-105">Узнайте, как tooinstall hello Hadoop «песочнице» Hortonworks на виртуальную машину toolearn о Hadoop экосистема hello.</span><span class="sxs-lookup"><span data-stu-id="cb8be-105">Learn how tooinstall hello Hadoop sandbox from Hortonworks on a virtual machine toolearn about hello Hadoop ecosystem.</span></span> <span data-ttu-id="cb8be-106">"песочница" Hello предоставляет toolearn среде местного разработки о Hadoop, система распределенного файла Hadoop (HDFS) и отправки заданий.</span><span class="sxs-lookup"><span data-stu-id="cb8be-106">hello sandbox provides a local development environment toolearn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="cb8be-107">Если вы знакомы с Hadoop, вы можете начать использовать Hadoop в Azure, создав кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb8be-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="cb8be-108">Дополнительные сведения о том, как tooget работы см. в разделе [Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cb8be-108">For more information on how tooget started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb8be-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cb8be-109">Prerequisites</span></span>
* <span data-ttu-id="cb8be-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="cb8be-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="cb8be-111">Скачайте и установите приложение [отсюда](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="cb8be-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-hello-virtual-machine"></a><span data-ttu-id="cb8be-112">Загрузите и установите hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cb8be-112">Download and install hello virtual machine</span></span>
1. <span data-ttu-id="cb8be-113">Обзор toohello [Hortonworks загружает](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="cb8be-113">Browse toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="cb8be-114">Нажмите кнопку **загрузки VIRTUALBOX** toodownload hello последнюю Hortonworks "песочницы" на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="cb8be-114">Click **DOWNLOAD FOR VIRTUALBOX** toodownload hello latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="cb8be-115">Все запрашиваемые tooregister с Hortonworks перед началом загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="cb8be-115">You are prompted tooregister with Hortonworks before hello download begins.</span></span> <span data-ttu-id="cb8be-116">Он принимает один toodownload tootwo часов в зависимости от скорости сети.</span><span class="sxs-lookup"><span data-stu-id="cb8be-116">It takes one tootwo hours toodownload depending on your network speed.</span></span>
   
    ![Изображение ссылки для скачивания песочницы Hortonworks для VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="cb8be-118">Из Здравствуйте одной веб-странице, щелкните hello **импорта на Virtual Box** связать toodownload PDF-ФАЙЛ, содержащий инструкции по установке для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cb8be-118">From hello same web page, click hello **Import on Virtual Box** link toodownload a PDF containing installation instructions for hello virtual machine.</span></span>

<span data-ttu-id="cb8be-119">toodownload изолированной более старые версии HDP разверните hello архива:</span><span class="sxs-lookup"><span data-stu-id="cb8be-119">toodownload an older HDP version sandbox, expand hello archive:</span></span>

![Архив песочницы Hortonworks](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a><span data-ttu-id="cb8be-121">Запустить виртуальную машину hello</span><span class="sxs-lookup"><span data-stu-id="cb8be-121">Start hello virtual machine</span></span>

1. <span data-ttu-id="cb8be-122">Откройте Oracle VirtualBox на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="cb8be-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="cb8be-123">Из hello **файл** меню, нажмите кнопку **устройство импорта**и укажите hello изображения Hortonworks "песочницы".</span><span class="sxs-lookup"><span data-stu-id="cb8be-123">From hello **File** menu, click **Import Appliance**, and then specify hello Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="cb8be-124">Выберите hello Hortonworks "песочницы", нажмите кнопку **запустить**, а затем **Обычный запуск**.</span><span class="sxs-lookup"><span data-stu-id="cb8be-124">Select hello Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="cb8be-125">После завершения процесса загрузки hello hello виртуальной машины она отображает инструкции имени входа.</span><span class="sxs-lookup"><span data-stu-id="cb8be-125">Once hello virtual machine has finished hello boot process, it displays login instructions.</span></span>
   
    ![Normal Start](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="cb8be-127">Откройте веб-браузер и перейдите toohello URL-адрес отображается (обычно http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="cb8be-127">Open a web browser and navigate toohello URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="cb8be-128">Задание паролей для песочницы</span><span class="sxs-lookup"><span data-stu-id="cb8be-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="cb8be-129">Из hello **начать** hello Hortonworks "песочницы", выберите шаг **Дополнительные параметры представления**.</span><span class="sxs-lookup"><span data-stu-id="cb8be-129">From hello **get started** step of hello Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="cb8be-130">Используйте hello сведения на этой странице toolog в песочнице toohello с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="cb8be-130">Use hello information on this page toolog in toohello sandbox using SSH.</span></span> <span data-ttu-id="cb8be-131">Используйте hello имя и пароль.</span><span class="sxs-lookup"><span data-stu-id="cb8be-131">Use hello name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cb8be-132">Если у вас установлен клиент SSH, можно использовать веб-SSH, предоставляемые в hello виртуальной машины в hello **http://localhost:4200 /**.</span><span class="sxs-lookup"><span data-stu-id="cb8be-132">If you do not have an SSH client installed, you can use hello web-based SSH provided at by hello virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="cb8be-133">Hello при первом подключении с помощью SSH, все запрашиваемые toochange hello пароль для учетной записи root hello.</span><span class="sxs-lookup"><span data-stu-id="cb8be-133">hello first time you connect using SSH, you are prompted toochange hello password for hello root account.</span></span> <span data-ttu-id="cb8be-134">Введите новый пароль, используемый при входе с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="cb8be-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="cb8be-135">После входа введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cb8be-135">Once logged in, enter hello following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="cb8be-136">При появлении запроса введите пароль для учетной записи администратора Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="cb8be-136">When prompted, provide a password for hello Ambari admin account.</span></span> <span data-ttu-id="cb8be-137">Это используется при доступе к hello Ambari веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="cb8be-137">This is used when you access hello Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="cb8be-138">Использование команд Hive</span><span class="sxs-lookup"><span data-stu-id="cb8be-138">Use Hive commands</span></span>

1. <span data-ttu-id="cb8be-139">В изолированной toohello SSH подключения используйте следующие командной оболочки Hive hello toostart hello:</span><span class="sxs-lookup"><span data-stu-id="cb8be-139">From an SSH connection toohello sandbox, use hello following command toostart hello Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="cb8be-140">После запуска оболочки hello, используйте следующие таблицы tooview hello, имеющиеся в "песочнице" hello hello:</span><span class="sxs-lookup"><span data-stu-id="cb8be-140">Once hello shell has started, use hello following tooview hello tables that are provided with hello sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="cb8be-141">Используйте hello следующую tooretrieve 10 строк из hello `sample_07` таблицы:</span><span class="sxs-lookup"><span data-stu-id="cb8be-141">Use hello following tooretrieve 10 rows from hello `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="cb8be-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cb8be-142">Next steps</span></span>
* [<span data-ttu-id="cb8be-143">Узнайте, как toouse Visual Studio с hello Hortonworks "песочницы"</span><span class="sxs-lookup"><span data-stu-id="cb8be-143">Learn how toouse Visual Studio with hello Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="cb8be-144">Изучение ropes hello объекта hello Hortonworks "песочницы"</span><span class="sxs-lookup"><span data-stu-id="cb8be-144">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* <span data-ttu-id="cb8be-145">[Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/) (Руководство по началу работы с Hadoop)</span><span class="sxs-lookup"><span data-stu-id="cb8be-145">[Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)</span></span>

