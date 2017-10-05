---
title: "Сведения об использовании эмулятора песочницы Hadoop в Azure HDInsight | Документация Майкрософт"
description: "Чтобы начать ознакомление с экосистемой Hadoop, можно настроить на виртуальной машине Azure песочницу Hadoop с платформы Hortonworks. "
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
ms.openlocfilehash: b701879464205860edd1c097651b532f87bae388
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="e6679-104">Начало работы с песочницей Hadoop, эмулятором на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="e6679-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="e6679-105">Узнайте, как настроить на виртуальной машине песочницу Hadoop с платформы Hortonworks, чтобы ознакомиться с экосистемой Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e6679-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span></span> <span data-ttu-id="e6679-106">Песочница представляет собой локальную среду разработки для ознакомления с Hadoop, распределенной файловой системой Hadoop (HDFS) и отправкой заданий.</span><span class="sxs-lookup"><span data-stu-id="e6679-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="e6679-107">Если вы знакомы с Hadoop, вы можете начать использовать Hadoop в Azure, создав кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6679-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="e6679-108">Дополнительные сведения см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e6679-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6679-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e6679-109">Prerequisites</span></span>
* <span data-ttu-id="e6679-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="e6679-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="e6679-111">Скачайте и установите приложение [отсюда](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="e6679-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-the-virtual-machine"></a><span data-ttu-id="e6679-112">Скачивание и установка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e6679-112">Download and install the virtual machine</span></span>
1. <span data-ttu-id="e6679-113">Перейдите на [страницу загрузок Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="e6679-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="e6679-114">Щелкните **DOWNLOAD FOR VIRTUALBOX** (Файл загрузки для VirtualBox), чтобы скачать последнюю песочницу Hortonworks на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="e6679-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="e6679-115">Перед началом скачивания вам будет предложено зарегистрироваться в Hortonworks.</span><span class="sxs-lookup"><span data-stu-id="e6679-115">You are prompted to register with Hortonworks before the download begins.</span></span> <span data-ttu-id="e6679-116">Скачивание может длиться один-два часа в зависимости от скорости сети.</span><span class="sxs-lookup"><span data-stu-id="e6679-116">It takes one to two hours to download depending on your network speed.</span></span>
   
    ![Изображение ссылки для скачивания песочницы Hortonworks для VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="e6679-118">На этой же веб-странице щелкните ссылку **Import on Virtual Box** (Импорт в VirtualBox), чтобы скачать PDF-файл, содержащий инструкции по установке для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e6679-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span></span>

<span data-ttu-id="e6679-119">Чтобы скачать старую песочницу версии HDP, разверните архив:</span><span class="sxs-lookup"><span data-stu-id="e6679-119">To download an older HDP version sandbox, expand the archive:</span></span>

![Архив песочницы Hortonworks](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a><span data-ttu-id="e6679-121">Запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e6679-121">Start the virtual machine</span></span>

1. <span data-ttu-id="e6679-122">Откройте Oracle VirtualBox на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e6679-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="e6679-123">В меню **Файл** щелкните **Import Appliance** (Импорт устройства), а затем укажите образ песочницы Hortonworks.</span><span class="sxs-lookup"><span data-stu-id="e6679-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="e6679-124">Выберете песочницу Hortonworks, щелкните **Start** (Запустить) > **Normal Start** (Обычный запуск).</span><span class="sxs-lookup"><span data-stu-id="e6679-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="e6679-125">После завершения процесса загрузки в виртуальной машине отобразятся инструкции для входа.</span><span class="sxs-lookup"><span data-stu-id="e6679-125">Once the virtual machine has finished the boot process, it displays login instructions.</span></span>
   
    ![Normal Start](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="e6679-127">Откройте веб-браузер и перейдите по отображаемому URL-адресу (как правило, http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="e6679-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="e6679-128">Задание паролей для песочницы</span><span class="sxs-lookup"><span data-stu-id="e6679-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="e6679-129">На **начальном шаге** на странице песочницы Hortonworks выберите **View Advanced Options** (Просмотр дополнительных параметров).</span><span class="sxs-lookup"><span data-stu-id="e6679-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="e6679-130">Используйте сведения на этой странице, чтобы войти в песочницу с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="e6679-130">Use the information on this page to log in to the sandbox using SSH.</span></span> <span data-ttu-id="e6679-131">Введите указанные имя и пароль.</span><span class="sxs-lookup"><span data-stu-id="e6679-131">Use the name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e6679-132">Если клиент SSH не установлен, можно использовать веб-SSH, предоставляемый виртуальной машиной по адресу **http://localhost:4200/**.</span><span class="sxs-lookup"><span data-stu-id="e6679-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="e6679-133">При первом подключении с помощью SSH вам будет предложено изменить пароль для учетной записи root.</span><span class="sxs-lookup"><span data-stu-id="e6679-133">The first time you connect using SSH, you are prompted to change the password for the root account.</span></span> <span data-ttu-id="e6679-134">Введите новый пароль, используемый при входе с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="e6679-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="e6679-135">После входа в систему введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e6679-135">Once logged in, enter the following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="e6679-136">При появлении запроса укажите пароль для учетной записи администратора Ambari.</span><span class="sxs-lookup"><span data-stu-id="e6679-136">When prompted, provide a password for the Ambari admin account.</span></span> <span data-ttu-id="e6679-137">Он используется при получении доступа к веб-интерфейсу Ambari.</span><span class="sxs-lookup"><span data-stu-id="e6679-137">This is used when you access the Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="e6679-138">Использование команд Hive</span><span class="sxs-lookup"><span data-stu-id="e6679-138">Use Hive commands</span></span>

1. <span data-ttu-id="e6679-139">Используя подключение SSH к песочнице, запустите оболочку Hive с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e6679-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="e6679-140">После запуска оболочки просмотрите таблицы, представленные в песочнице, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e6679-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="e6679-141">Используйте следующую команду, чтобы извлечь 10 строк из таблицы `sample_07` :</span><span class="sxs-lookup"><span data-stu-id="e6679-141">Use the following to retrieve 10 rows from the `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="e6679-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e6679-142">Next steps</span></span>
* [<span data-ttu-id="e6679-143">Использование средств Azure Data Lake для Visual Studio с песочницей Hortonworks</span><span class="sxs-lookup"><span data-stu-id="e6679-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="e6679-144">Learning the ropes of the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="e6679-144">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* <span data-ttu-id="e6679-145">[Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/) (Руководство по началу работы с Hadoop)</span><span class="sxs-lookup"><span data-stu-id="e6679-145">[Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)</span></span>

