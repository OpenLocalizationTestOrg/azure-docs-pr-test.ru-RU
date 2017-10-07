---
title: "Научные aaaData на hello виртуальная машина анализа данных Linux | Документы Microsoft"
description: "Как tooperform несколько науки общих данных задач с hello обработки и анализа данных виртуальной Машины с Linux."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a><span data-ttu-id="da534-103">Обработки и анализа данных на hello виртуальная машина анализа данных Linux</span><span class="sxs-lookup"><span data-stu-id="da534-103">Data science on hello Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="da534-104">В этом пошаговом руководстве показано, как tooperform несколько науки общих данных задач с hello обработки и анализа данных виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="da534-104">This walkthrough shows you how tooperform several common data science tasks with hello Linux Data Science VM.</span></span> <span data-ttu-id="da534-105">Hello виртуальной машины обработки и анализа данных Linux (DSVM) — это изображение виртуальной машины, доступный в Azure, предварительно установлены с набор средств, которые обычно используются для анализа данных и машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="da534-105">hello Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="da534-106">Hello ключевых компонентов программного обеспечения перечислено в hello [подготовки hello виртуальная машина анализа данных Linux](machine-learning-data-science-linux-dsvm-intro.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="da534-106">hello key software components are itemized in hello [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="da534-107">Hello образа виртуальной Машины позволяет легко tooget начал делать обработки и анализа данных в минутах, без необходимости tooinstall и настройка каждого из средств hello по отдельности.</span><span class="sxs-lookup"><span data-stu-id="da534-107">hello VM image makes it easy tooget started doing data science in minutes, without having tooinstall and configure each of hello tools individually.</span></span> <span data-ttu-id="da534-108">Можно легко масштабировать hello виртуальной Машины, при необходимости и остановите ее не во время работы.</span><span class="sxs-lookup"><span data-stu-id="da534-108">You can easily scale up hello VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="da534-109">Таким образом, это гибкий и экономичный ресурс.</span><span class="sxs-lookup"><span data-stu-id="da534-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="da534-110">Hello задач обработки и анализа данных, представленный в данном руководстве, выполните hello действия, описанные в hello [процесс обработки и анализа данных для команды](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="da534-110">hello data science tasks demonstrated in this walkthrough follow hello steps outlined in hello [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="da534-111">Этот процесс предоставляет систематический подход toodata обработки и анализа, созданному tooeffectively совместно работать над hello жизненным циклом разработки интеллектуальных приложений специалистами по анализу данных.</span><span class="sxs-lookup"><span data-stu-id="da534-111">This process provides a systematic approach toodata science that enables teams of data scientists tooeffectively collaborate over hello lifecycle of building intelligent applications.</span></span> <span data-ttu-id="da534-112">процесс обработки и анализа данных Hello также предоставляет платформу последовательной обработки и анализа данных, может следовать отдельного.</span><span class="sxs-lookup"><span data-stu-id="da534-112">hello data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="da534-113">В ходе анализа hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) набора данных в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="da534-113">We analyze hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="da534-114">Это набор адресов электронной почты, которые помечены как нежелательной почты или ham (то есть они не являются нежелательной почты), и также содержит некоторые статистические данные на содержимом hello hello адресов электронной почты.</span><span class="sxs-lookup"><span data-stu-id="da534-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on hello content of hello emails.</span></span> <span data-ttu-id="da534-115">Статистика Hello включены Далее рассматриваются в hello, кроме одного раздела.</span><span class="sxs-lookup"><span data-stu-id="da534-115">hello statistics included are discussed in hello next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da534-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="da534-116">Prerequisites</span></span>
<span data-ttu-id="da534-117">Прежде чем использовать виртуальная машина анализа данных Linux, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="da534-117">Before you can use a Linux Data Science Virtual Machine, you must have hello following:</span></span>

* <span data-ttu-id="da534-118">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="da534-118">An **Azure subscription**.</span></span> <span data-ttu-id="da534-119">Если у вас ее нет, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="da534-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="da534-120">[**Виртуальная машина Linux для обработки и анализа данных.**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm)</span><span class="sxs-lookup"><span data-stu-id="da534-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="da534-121">Сведения о подготовке этой виртуальной Машины в разделе [подготовки hello виртуальная машина анализа данных Linux](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="da534-121">For information on provisioning this VM, see [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="da534-122">Клиент [X2Go](http://wiki.x2go.org/doku.php), установленный на компьютере, и открытый сеанс XFCE.</span><span class="sxs-lookup"><span data-stu-id="da534-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="da534-123">Сведения об установке и настройке **клиента X2Go** см. в разделе [Установка и настройка клиента X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="da534-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="da534-124">**Учетная запись машинного обучения Azure**.</span><span class="sxs-lookup"><span data-stu-id="da534-124">An **AzureML account**.</span></span> <span data-ttu-id="da534-125">Если вы уже нет, зарегистрироваться для нового на hello [AzureML Домашняя страница](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="da534-125">If you don't already have one, sign up for new one at hello [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="da534-126">Нет toohelp уровень свободного использования, вам начать работу.</span><span class="sxs-lookup"><span data-stu-id="da534-126">There is a free usage tier toohelp you get started.</span></span>

## <a name="download-hello-spambase-dataset"></a><span data-ttu-id="da534-127">Скачать набор данных spambase hello</span><span class="sxs-lookup"><span data-stu-id="da534-127">Download hello spambase dataset</span></span>
<span data-ttu-id="da534-128">Hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) набор данных является относительно небольшой набор данных, который содержит только 4601 примеры.</span><span class="sxs-lookup"><span data-stu-id="da534-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="da534-129">Это toouse компактные при демонстрации того, что некоторые ключевые функции hello hello ВМ обработки и анализа данных, как оно сохраняет потребности в ресурсах hello небольшой.</span><span class="sxs-lookup"><span data-stu-id="da534-129">This is a convenient size toouse when demonstrating that some of hello key features of hello Data Science VM as it keeps hello resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="da534-130">В этом пошаговом руководстве используется виртуальная машина Linux размера D2 v2.</span><span class="sxs-lookup"><span data-stu-id="da534-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="da534-131">Этот размер DSVM может обрабатывать hello процедуры в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="da534-131">This size DSVM is capable of handling hello procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="da534-132">Если вам требуется больше места для хранения, можно создать дополнительные диски и присоединить их tooyour виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="da534-132">If you need more storage space, you can create additional disks and attach them tooyour VM.</span></span> <span data-ttu-id="da534-133">Эти диски с использованием постоянного хранилища Azure, поэтому их данные сохраняются даже в том случае, если выполняется повторная Подготовка hello server из-за tooresizing или завершение работы.</span><span class="sxs-lookup"><span data-stu-id="da534-133">These disks use persistent Azure storage, so their data is preserved even when hello server is reprovisioned due tooresizing or is shut down.</span></span> <span data-ttu-id="da534-134">tooadd диск и присоединить ее tooyour виртуальной Машины, следуйте инструкциям в разделе hello [добавить диск tooa ВМ Linux](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da534-134">tooadd a disk and attach it tooyour VM, follow hello instructions in [Add a disk tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="da534-135">Эти шаги использовать интерфейс командной строки Azure (Azure CLI), который уже установлен на hello DSVM hello.</span><span class="sxs-lookup"><span data-stu-id="da534-135">These steps use hello Azure Command-Line Interface (Azure CLI), which is already installed on hello DSVM.</span></span> <span data-ttu-id="da534-136">Поэтому эти процедуры можно сделать из hello самой ВМ.</span><span class="sxs-lookup"><span data-stu-id="da534-136">So these procedures can be done entirely from hello VM itself.</span></span> <span data-ttu-id="da534-137">Другой параметр tooincrease хранилище — toouse [файлы Azure](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="da534-137">Another option tooincrease storage is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="da534-138">данные hello toodownload, откройте окно терминала и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="da534-138">toodownload hello data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="da534-139">загруженный файл Hello не иметь строку заголовка, поэтому давайте создадим другой файл, который имеет заголовка.</span><span class="sxs-lookup"><span data-stu-id="da534-139">hello downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="da534-140">Запустите файл toocreate этой команды с соответствующими заголовками hello:</span><span class="sxs-lookup"><span data-stu-id="da534-140">Run this command toocreate a file with hello appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="da534-141">Затем объединить два файла hello вместе с hello команды:</span><span class="sxs-lookup"><span data-stu-id="da534-141">Then concatenate hello two files together with hello command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="da534-142">Hello набор данных содержит несколько типов статистических данных на все сообщения электронной почты:</span><span class="sxs-lookup"><span data-stu-id="da534-142">hello dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="da534-143">Столбцы, например ***word\_freq\_WORD*** указывает процент hello слова в сообщении электронной почты hello, соответствующие *WORD*.</span><span class="sxs-lookup"><span data-stu-id="da534-143">Columns like ***word\_freq\_WORD*** indicate hello percentage of words in hello email that match *WORD*.</span></span> <span data-ttu-id="da534-144">Например если *word\_freq\_сделать* имеет значение 1, а затем были 1% от всех слов в сообщении электронной почты hello *сделать*.</span><span class="sxs-lookup"><span data-stu-id="da534-144">For example, if *word\_freq\_make* is 1, then 1% of all words in hello email were *make*.</span></span>
* <span data-ttu-id="da534-145">Столбцы, например ***char\_freq\_CHAR*** указывает процент hello все символы hello электронной почты, которые были *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="da534-145">Columns like ***char\_freq\_CHAR*** indicate hello percentage of all characters in hello email that were *CHAR*.</span></span>
* <span data-ttu-id="da534-146">***Прописная\_запуска\_длина\_длинного*** имеет длину самой длинной hello последовательности прописных букв.</span><span class="sxs-lookup"><span data-stu-id="da534-146">***capital\_run\_length\_longest*** is hello longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="da534-147">***Прописная\_запуска\_длина\_среднее*** — hello Средняя продолжительность всех последовательностей прописных букв.</span><span class="sxs-lookup"><span data-stu-id="da534-147">***capital\_run\_length\_average*** is hello average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="da534-148">***Прописная\_запуска\_длина\_общее*** — hello общая длина всех последовательностей прописных букв.</span><span class="sxs-lookup"><span data-stu-id="da534-148">***capital\_run\_length\_total*** is hello total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="da534-149">***нежелательной почты*** указывает hello электронной почты был считаются ли Нежелательная почта или нет (1 = нежелательной почты, 0 = не нежелательной почты).</span><span class="sxs-lookup"><span data-stu-id="da534-149">***spam*** indicates whether hello email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-hello-dataset-with-microsoft-r-open"></a><span data-ttu-id="da534-150">Просмотр набора данных hello с Microsoft R Open</span><span class="sxs-lookup"><span data-stu-id="da534-150">Explore hello dataset with Microsoft R Open</span></span>
<span data-ttu-id="da534-151">Давайте исследовать данные hello и выполнять некоторые основные машинного обучения с виртуальной Машины для обработки и анализа данных поставляется с hello R. [Microsoft R Open](https://mran.revolutionanalytics.com/open/) предварительно установлен.</span><span class="sxs-lookup"><span data-stu-id="da534-151">Let's examine hello data and do some basic machine learning with R. hello Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="da534-152">Hello многопоточных математические библиотеки в этой версии R обеспечивают более высокую производительность, чем различные версии одним потоком.</span><span class="sxs-lookup"><span data-stu-id="da534-152">hello multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="da534-153">Microsoft R Open также предоставляет повторяемость с помощью моментального снимка репозитория пакетов CRAN hello.</span><span class="sxs-lookup"><span data-stu-id="da534-153">Microsoft R Open also provides reproducibility by using a snapshot of hello CRAN package repository.</span></span>

<span data-ttu-id="da534-154">примеры, в данном пошаговом руководстве hello клонов кода tooget копии hello **Azure-Machine-обучения--обработки и анализа данных** репозитория git, с помощью которой уже установлены на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="da534-154">tooget copies of hello code samples used in this walkthrough, clone hello **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on hello VM.</span></span> <span data-ttu-id="da534-155">Из командной строки git hello выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="da534-155">From hello git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="da534-156">Откройте окно терминала и начать новый сеанс R с помощью интерактивной консоли hello R.</span><span class="sxs-lookup"><span data-stu-id="da534-156">Open a terminal window and start a new R session with hello R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="da534-157">RStudio также можно использовать для следующих процедур hello.</span><span class="sxs-lookup"><span data-stu-id="da534-157">You can also use RStudio for hello following procedures.</span></span> <span data-ttu-id="da534-158">tooinstall RStudio, выполнение этой команды на терминала:`./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="da534-158">tooinstall RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="da534-159">tooimport hello данные и настройки среды hello, выполните:</span><span class="sxs-lookup"><span data-stu-id="da534-159">tooimport hello data and set up hello environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="da534-160">toosee сводные статистические данные о каждом столбце:</span><span class="sxs-lookup"><span data-stu-id="da534-160">toosee summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="da534-161">Новое представление данных hello:</span><span class="sxs-lookup"><span data-stu-id="da534-161">For a different view of hello data:</span></span>

    str(data)

<span data-ttu-id="da534-162">Отображается тип каждой переменной hello и hello первые несколько значений в наборе данных hello.</span><span class="sxs-lookup"><span data-stu-id="da534-162">This shows you hello type of each variable and hello first few values in hello dataset.</span></span>

<span data-ttu-id="da534-163">Hello *нежелательной почты* столбца было прочитано как целое число, но это фактически категориальные переменной (или коэффициент).</span><span class="sxs-lookup"><span data-stu-id="da534-163">hello *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="da534-164">tooset его тип:</span><span class="sxs-lookup"><span data-stu-id="da534-164">tooset its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="da534-165">toodo некоторые исследовательский анализ, используйте hello [ggplot2](http://ggplot2.org/) пакета популярные библиотеки построения для R, уже установлены на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="da534-165">toodo some exploratory analysis, use hello [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on hello VM.</span></span> <span data-ttu-id="da534-166">Обратите внимание, из сводных данных hello, показанным ранее, что у нас есть сводные статистические данные о частоте hello hello восклицательный знак.</span><span class="sxs-lookup"><span data-stu-id="da534-166">Note, from hello summary data displayed earlier, that we have summary statistics on hello frequency of hello exclamation mark character.</span></span> <span data-ttu-id="da534-167">Давайте построения этих частот здесь с hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="da534-167">Let's plot those frequencies here with hello following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="da534-168">Так как строка hello ноль наклона рисунка hello, удалим его:</span><span class="sxs-lookup"><span data-stu-id="da534-168">Since hello zero bar is skewing hello plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="da534-169">Выше показателя 1 наблюдается необычная плотность.</span><span class="sxs-lookup"><span data-stu-id="da534-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="da534-170">Давайте взглянем только на эти данные.</span><span class="sxs-lookup"><span data-stu-id="da534-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="da534-171">Затем разобьем их на наборы с обычной и нежелательной почтой.</span><span class="sxs-lookup"><span data-stu-id="da534-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="da534-172">Эти примеры должны позволяют toomake аналогичные точечное hello tooexplore другие столбцы Здравствуйте, содержащиеся в них данные.</span><span class="sxs-lookup"><span data-stu-id="da534-172">These examples should enable you toomake similar plots of hello other columns tooexplore hello data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="da534-173">Обучение и тестирование модели машинного обучения</span><span class="sxs-lookup"><span data-stu-id="da534-173">Train and test an ML model</span></span>
<span data-ttu-id="da534-174">Теперь давайте обучения ряд машинного обучения моделей электронные сообщения hello tooclassify hello набора данных как содержащий либо span или ham.</span><span class="sxs-lookup"><span data-stu-id="da534-174">Now let's train a couple of machine learning models tooclassify hello emails in hello dataset as containing either span or ham.</span></span> <span data-ttu-id="da534-175">В этом разделе мы обучим модель дерева принятия решений и модель случайного леса, а затем протестируем точность получаемых прогнозов.</span><span class="sxs-lookup"><span data-stu-id="da534-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="da534-176">пакет Hello rpart (рекурсивное секционирование и для дерева регрессии), используемый в после кода hello уже установлены на hello ВМ обработки и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="da534-176">hello rpart (Recursive Partitioning and Regression Trees) package used in hello following code is already installed on hello Data Science VM.</span></span>
>
>

<span data-ttu-id="da534-177">Во-первых давайте разбиение hello набора данных на обучающие и проверочные наборы:</span><span class="sxs-lookup"><span data-stu-id="da534-177">First, let's split hello dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="da534-178">А затем создать hello tooclassify дерева принятия решений сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="da534-178">And then create a decision tree tooclassify hello emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="da534-179">Ниже приведен результат hello.</span><span class="sxs-lookup"><span data-stu-id="da534-179">Here is hello result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="da534-181">toodetermine, насколько хорошо выполняется на обучение hello задать, использовать hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="da534-181">toodetermine how well it performs on hello training set, use hello following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="da534-182">насколько хорошо toodetermine выполняемых в тестовом наборе hello:</span><span class="sxs-lookup"><span data-stu-id="da534-182">toodetermine how well it performs on hello test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="da534-183">Теперь давайте испробуем модель случайного леса.</span><span class="sxs-lookup"><span data-stu-id="da534-183">Let's also try a random forest model.</span></span> <span data-ttu-id="da534-184">Случайные леса обучения множество дерева принятия решений и выведите класс, который является режимом hello классификаций hello из всех деревьев принятия решений отдельных hello.</span><span class="sxs-lookup"><span data-stu-id="da534-184">Random forests train a multitude of decision trees and output a class that is hello mode of hello classifications from all of hello individual decision trees.</span></span> <span data-ttu-id="da534-185">Они предоставляют больше возможностей машинного обучения подход, как они исправления для hello тенденцию toooverfit модели дерева принятия решений обучающий набор данных.</span><span class="sxs-lookup"><span data-stu-id="da534-185">They provide a more powerful machine learning approach as they correct for hello tendency of a decision tree model toooverfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a><span data-ttu-id="da534-186">Развертывание модели tooAzure машинного Обучения</span><span class="sxs-lookup"><span data-stu-id="da534-186">Deploy a model tooAzure ML</span></span>
<span data-ttu-id="da534-187">[Студия машинного обучения](https://studio.azureml.net/) (AzureML) — это облачная служба, что делает его легко toobuild и развертывания моделей прогнозирования.</span><span class="sxs-lookup"><span data-stu-id="da534-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy toobuild and deploy predictive analytics models.</span></span> <span data-ttu-id="da534-188">Одной из удобных функций hello AzureML является его toopublish возможность работать любой R в качестве веб-службы.</span><span class="sxs-lookup"><span data-stu-id="da534-188">One of hello nice features of AzureML is its ability toopublish any R function as a web service.</span></span> <span data-ttu-id="da534-189">Hello AzureML R-пакет развертывания легко toodo прямо с нашей сеанса R на становится hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="da534-189">hello AzureML R package makes deployment easy toodo right from our R session on hello DSVM.</span></span>

<span data-ttu-id="da534-190">toodeploy hello код дерева принятия решений hello в предыдущем разделе, необходимо toosign в tooAzure студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="da534-190">toodeploy hello decision tree code from hello previous section, you need toosign in tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="da534-191">Требуется идентификатор вашей рабочей области и toosign маркер авторизации в.</span><span class="sxs-lookup"><span data-stu-id="da534-191">You need your workspace ID and an authorization token toosign in.</span></span> <span data-ttu-id="da534-192">toofind эти значения и переменные AzureML hello инициализации с ними:</span><span class="sxs-lookup"><span data-stu-id="da534-192">toofind these values and initialize hello AzureML variables with them:</span></span>

<span data-ttu-id="da534-193">Выберите **параметры** в левом меню hello.</span><span class="sxs-lookup"><span data-stu-id="da534-193">Select **Settings** on hello left-hand menu.</span></span> <span data-ttu-id="da534-194">Укажите значение в поле **Идентификатор рабочей области**.</span><span class="sxs-lookup"><span data-stu-id="da534-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="da534-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="da534-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="da534-196">Выберите **маркерах авторизации** hello издержек на меню и обратите внимание на **основного маркера авторизации**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="da534-196">Select **Authorization Tokens** from hello overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="da534-197">Hello нагрузки **AzureML** пакета и задайте значения переменных hello своим Идентификатором маркера и в рабочей области во время сеанса R на hello DSVM:</span><span class="sxs-lookup"><span data-stu-id="da534-197">Load hello **AzureML** package and then set values of hello variables with your token and workspace ID in your R session on hello DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="da534-198">Давайте упростить toomake hello модели проще tooimplement этой демонстрации.</span><span class="sxs-lookup"><span data-stu-id="da534-198">Let's simplify hello model toomake this demonstration easier tooimplement.</span></span> <span data-ttu-id="da534-199">Выберите три переменные hello в hello принятия решений ближайший toohello корневой элемент дерева и создания нового дерева, используя только эти три переменные:</span><span class="sxs-lookup"><span data-stu-id="da534-199">Pick hello three variables in hello decision tree closest toohello root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="da534-200">Мы должны Прогнозирующая функция, которая принимает в качестве входных данных функции hello и возвращает hello прогнозируемые значения:</span><span class="sxs-lookup"><span data-stu-id="da534-200">We need a prediction function that takes hello features as an input and returns hello predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="da534-201">Публикация hello predictSpam функция tooAzureML с помощью hello **publishWebService** функции:</span><span class="sxs-lookup"><span data-stu-id="da534-201">Publish hello predictSpam function tooAzureML using hello **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="da534-202">Эта функция принимает hello **predictSpam** функционировать, создает веб-службы с именем **spamWebService** с определенных входных и выходных данных и возвращает сведения о новой конечной точки hello.</span><span class="sxs-lookup"><span data-stu-id="da534-202">This function takes hello **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about hello new endpoint.</span></span>

<span data-ttu-id="da534-203">Просмотр сведений о hello публикации веб-службы, включая его API конечной точки и ключами доступа с помощью команды hello:</span><span class="sxs-lookup"><span data-stu-id="da534-203">View details of hello published web service, including its API endpoint and access keys with hello command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="da534-204">tootry его на hello первые 10 строк hello проверочного набора:</span><span class="sxs-lookup"><span data-stu-id="da534-204">tootry it out on hello first 10 rows of hello test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="da534-205">Использование других доступных средств</span><span class="sxs-lookup"><span data-stu-id="da534-205">Use other tools available</span></span>
<span data-ttu-id="da534-206">Hello оставшихся разделах показано, как некоторые средства hello установлены на toouse hello обработки и анализа данных виртуальной Машины с Linux. Ниже приведен список hello обсуждаются средства:</span><span class="sxs-lookup"><span data-stu-id="da534-206">hello remaining sections show how toouse some of hello tools installed on hello Linux Data Science VM.Here is hello list of tools discussed:</span></span>

* <span data-ttu-id="da534-207">XGBoost;</span><span class="sxs-lookup"><span data-stu-id="da534-207">XGBoost</span></span>
* <span data-ttu-id="da534-208">Python;</span><span class="sxs-lookup"><span data-stu-id="da534-208">Python</span></span>
* <span data-ttu-id="da534-209">Jupyterhub;</span><span class="sxs-lookup"><span data-stu-id="da534-209">Jupyterhub</span></span>
* <span data-ttu-id="da534-210">Rattle;</span><span class="sxs-lookup"><span data-stu-id="da534-210">Rattle</span></span>
* <span data-ttu-id="da534-211">PostgreSQL и Squirrel SQL;</span><span class="sxs-lookup"><span data-stu-id="da534-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="da534-212">хранилище данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="da534-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="da534-213">XGBoost;</span><span class="sxs-lookup"><span data-stu-id="da534-213">XGBoost</span></span>
<span data-ttu-id="da534-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) — инструмент, предоставляющий быструю и точную реализацию увеличивающегося дерева.</span><span class="sxs-lookup"><span data-stu-id="da534-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

<span data-ttu-id="da534-215">Его можно вызвать из командной строки или Python.</span><span class="sxs-lookup"><span data-stu-id="da534-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="da534-216">Python</span><span class="sxs-lookup"><span data-stu-id="da534-216">Python</span></span>
<span data-ttu-id="da534-217">Для разработки приложений с помощью Python hello распределения Anaconda Python 2.7 и 3.5 были установлены в hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="da534-217">For development using Python, hello Anaconda Python distributions 2.7 and 3.5 have been installed in hello DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="da534-218">включает дистрибутив Anaconda Hello [Condas](http://conda.pydata.org/docs/index.html), который может быть пользовательской среды используется toocreate для Python, имеют разные версии или пакеты, установленные в них.</span><span class="sxs-lookup"><span data-stu-id="da534-218">hello Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used toocreate custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="da534-219">Давайте чтения в некоторой части набора данных spambase hello и классифицировать hello сообщения электронной почты с машины опорных векторов в scikit-Дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="da534-219">Let's read in some of hello spambase dataset and classify hello emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="da534-220">toomake прогнозов:</span><span class="sxs-lookup"><span data-stu-id="da534-220">toomake predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="da534-221">tooshow как toopublish AzureML конечной точки, давайте создать простую модель hello три переменные, как мы делали, когда мы ранее опубликованные модели hello R.</span><span class="sxs-lookup"><span data-stu-id="da534-221">tooshow how toopublish an AzureML endpoint, let's make a simpler model hello three variables as we did when we published hello R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="da534-222">tooAzureML модели hello toopublish:</span><span class="sxs-lookup"><span data-stu-id="da534-222">toopublish hello model tooAzureML:</span></span>

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="da534-223">Это доступно только для Python 2.7 и еще не поддерживается для версии 3.5.</span><span class="sxs-lookup"><span data-stu-id="da534-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="da534-224">Выполните код с использованием **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="da534-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="da534-225">Jupyterhub;</span><span class="sxs-lookup"><span data-stu-id="da534-225">Jupyterhub</span></span>
<span data-ttu-id="da534-226">Дистрибутив Anaconda Hello в hello DSVM поставляется с записной книжке Jupyter, код Python, R или Юлия tooshare кросс платформенных среды и анализа.</span><span class="sxs-lookup"><span data-stu-id="da534-226">hello Anaconda distribution in hello DSVM comes with a Jupyter notebook, a cross-platform environment tooshare Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="da534-227">Hello книжке Jupyter осуществляется с помощью JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="da534-227">hello Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="da534-228">Для входа введите учетные данные локального пользователя Linux по адресу ***https://\<DNS-имя или IP-адрес ВМ\>:8000/***.</span><span class="sxs-lookup"><span data-stu-id="da534-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="da534-229">Все файлы конфигурации JupyterHub находятся в каталоге **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="da534-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="da534-230">Некоторые примеры записных книжек уже установлены на hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="da534-230">Several sample notebooks are already installed on hello VM:</span></span>

* <span data-ttu-id="da534-231">В разделе hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) для записной книжке образец Python.</span><span class="sxs-lookup"><span data-stu-id="da534-231">See hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="da534-232">См. [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) для примера записной книжки **R**.</span><span class="sxs-lookup"><span data-stu-id="da534-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="da534-233">В разделе hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) еще один пример **Python** ноутбука.</span><span class="sxs-lookup"><span data-stu-id="da534-233">See hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="da534-234">Hello Юлия языка также доступна из командной строки hello hello обработки и анализа данных виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="da534-234">hello Julia language is also available from hello command line on hello Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="da534-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="da534-235">Rattle</span></span>
<span data-ttu-id="da534-236">[Диска](https://cran.r-project.org/web/packages/rattle/index.html) (hello аналитические средства R tooLearn легко) — это графическое средство R для интеллектуального анализа данных.</span><span class="sxs-lookup"><span data-stu-id="da534-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (hello R Analytical Tool tooLearn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="da534-237">Он имеет интуитивно понятный интерфейс, который позволяет легко tooload, исследовать и преобразования данных и построения и оценивать модели.</span><span class="sxs-lookup"><span data-stu-id="da534-237">It has an intuitive interface that makes it easy tooload, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="da534-238">статья Hello [диска: GUI интеллектуального анализа данных для R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) Пошаговое руководство, демонстрируются ее возможности.</span><span class="sxs-lookup"><span data-stu-id="da534-238">hello article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="da534-239">Установка и запуск диска с hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="da534-239">Install and start Rattle with hello following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="da534-240">Установка на hello DSVM не требуется.</span><span class="sxs-lookup"><span data-stu-id="da534-240">Installation is not required on hello DSVM.</span></span> <span data-ttu-id="da534-241">Но погремушка могут потребоваться дополнительные пакеты tooinstall при загрузке.</span><span class="sxs-lookup"><span data-stu-id="da534-241">But Rattle may prompt you tooinstall additional packages when it loads.</span></span>
>
>

<span data-ttu-id="da534-242">В Rattle используется интерфейс на основе вкладок.</span><span class="sxs-lookup"><span data-stu-id="da534-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="da534-243">Большинство hello вкладок соответствует toosteps в hello [процесса обработки и анализа данных](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), такие как загрузка данных или его исследование.</span><span class="sxs-lookup"><span data-stu-id="da534-243">Most of hello tabs correspond toosteps in hello [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="da534-244">процесс обработки и анализа данных Hello поступает из левой tooright по вкладкам hello.</span><span class="sxs-lookup"><span data-stu-id="da534-244">hello data science process flows from left tooright through hello tabs.</span></span> <span data-ttu-id="da534-245">Но hello последнего вкладка содержит журнал hello R команд, выполняемых погремушка.</span><span class="sxs-lookup"><span data-stu-id="da534-245">But hello last tab contains a log of hello R commands run by Rattle.</span></span>

<span data-ttu-id="da534-246">tooload и настройки набора данных hello:</span><span class="sxs-lookup"><span data-stu-id="da534-246">tooload and configure hello dataset:</span></span>

* <span data-ttu-id="da534-247">файл hello tooload, выберите hello **данные** вкладке, нажмите</span><span class="sxs-lookup"><span data-stu-id="da534-247">tooload hello file, select hello **Data** tab, then</span></span>
* <span data-ttu-id="da534-248">Выберите селектор hello рядом слишком**Filename** и выберите **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="da534-248">Choose hello selector next too**Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="da534-249">файл tooload hello.</span><span class="sxs-lookup"><span data-stu-id="da534-249">tooload hello file.</span></span> <span data-ttu-id="da534-250">Выберите **Execute** в верхней строке hello кнопок.</span><span class="sxs-lookup"><span data-stu-id="da534-250">select **Execute** in hello top row of buttons.</span></span> <span data-ttu-id="da534-251">Должна появиться сводка каждого столбца, включая его тип данных, указанных входных данных, целевой объект или другой тип переменной и hello количество уникальных значений.</span><span class="sxs-lookup"><span data-stu-id="da534-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and hello number of unique values.</span></span>
* <span data-ttu-id="da534-252">Погремушка правильно идентифицировала hello **нежелательной почты** столбца в качестве целевой hello.</span><span class="sxs-lookup"><span data-stu-id="da534-252">Rattle has correctly identified hello **spam** column as hello target.</span></span> <span data-ttu-id="da534-253">Выберите hello столбца нежелательной почты, а затем набор hello **целевой тип данных** слишком**Categoric**.</span><span class="sxs-lookup"><span data-stu-id="da534-253">Select hello spam column, then set hello **Target Data Type** too**Categoric**.</span></span>

<span data-ttu-id="da534-254">данные hello tooexplore:</span><span class="sxs-lookup"><span data-stu-id="da534-254">tooexplore hello data:</span></span>

* <span data-ttu-id="da534-255">Выберите hello **Проводник** вкладки.</span><span class="sxs-lookup"><span data-stu-id="da534-255">Select hello **Explore** tab.</span></span>
* <span data-ttu-id="da534-256">Нажмите кнопку **сводки**, затем **Execute**, toosee некоторые сведения о типах переменной hello и некоторые сводные статистические данные.</span><span class="sxs-lookup"><span data-stu-id="da534-256">Click **Summary**, then **Execute**, toosee some information about hello variable types and some summary statistics.</span></span>
* <span data-ttu-id="da534-257">tooview другие статистические данные о каждой переменной, выберите другие параметры, такие как **описания** или **основы**.</span><span class="sxs-lookup"><span data-stu-id="da534-257">tooview other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="da534-258">Hello **Проводник** вкладке можно также toogenerate множество полезных графиков.</span><span class="sxs-lookup"><span data-stu-id="da534-258">hello **Explore** tab also allows you toogenerate many insightful plots.</span></span> <span data-ttu-id="da534-259">tooplot гистограммы hello данных:</span><span class="sxs-lookup"><span data-stu-id="da534-259">tooplot a histogram of hello data:</span></span>

* <span data-ttu-id="da534-260">Установите флажок **Distributions**(Дистрибутивы).</span><span class="sxs-lookup"><span data-stu-id="da534-260">Select **Distributions**.</span></span>
* <span data-ttu-id="da534-261">Выберите **Histogram** (Гистограмма) для выражений **word_freq_remove** и **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="da534-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="da534-262">Нажмите кнопку **Execute**(Выполнить).</span><span class="sxs-lookup"><span data-stu-id="da534-262">Select **Execute**.</span></span> <span data-ttu-id="da534-263">Вы увидите, что оба плотность отображаются в окне одной диаграммы, где было ясно, это слово hello, «вы» гораздо более часто появляется в сообщениях электронной почты, чем «удалить».</span><span class="sxs-lookup"><span data-stu-id="da534-263">You should see both density plots in a single graph window, where it is clear that hello word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="da534-264">График Hello корреляции также представляют интерес.</span><span class="sxs-lookup"><span data-stu-id="da534-264">hello Correlation plots are also interesting.</span></span> <span data-ttu-id="da534-265">toocreate один:</span><span class="sxs-lookup"><span data-stu-id="da534-265">toocreate one:</span></span>

* <span data-ttu-id="da534-266">Выберите **корреляции** как hello **тип**, затем</span><span class="sxs-lookup"><span data-stu-id="da534-266">Choose **Correlation** as hello **Type**, then</span></span>
* <span data-ttu-id="da534-267">Нажмите кнопку **Execute**(Выполнить).</span><span class="sxs-lookup"><span data-stu-id="da534-267">Select **Execute**.</span></span>
* <span data-ttu-id="da534-268">Rattle рекомендует использовать не более 40 переменных.</span><span class="sxs-lookup"><span data-stu-id="da534-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="da534-269">Выберите **Да** tooview hello построения.</span><span class="sxs-lookup"><span data-stu-id="da534-269">Select **Yes** tooview hello plot.</span></span>

<span data-ttu-id="da534-270">Существуют некоторые содержательные корреляции, возникающие: слишком сильно зависят от «технология» «HP» и «лаборатории», например.</span><span class="sxs-lookup"><span data-stu-id="da534-270">There are some interesting correlations that come up: "technology" is strongly correlated too"HP" and "labs", for example.</span></span> <span data-ttu-id="da534-271">Также настоятельно коррелирует слишком «650», так как код города hello доноров hello набора данных — 650.</span><span class="sxs-lookup"><span data-stu-id="da534-271">It is also strongly correlated too"650", because hello area code of hello dataset donors is 650.</span></span>

<span data-ttu-id="da534-272">в окне Просмотр hello доступны Hello числовые значения для hello корреляций между словами.</span><span class="sxs-lookup"><span data-stu-id="da534-272">hello numeric values for hello correlations between words are available in hello Explore window.</span></span> <span data-ttu-id="da534-273">Это интересно toonote, например, что «технология» отрицательно связаны с «вы» и «деньги».</span><span class="sxs-lookup"><span data-stu-id="da534-273">It is interesting toonote, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="da534-274">Погремушка может преобразовать некоторые распространенные проблемы toohandle hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="da534-274">Rattle can transform hello dataset toohandle some common issues.</span></span> <span data-ttu-id="da534-275">Например, он позволяет функции toorescale, добавить отсутствующие значения, обработать выбросы и удаления переменных и наблюдений всего отсутствующих данных.</span><span class="sxs-lookup"><span data-stu-id="da534-275">For example, it allows you toorescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="da534-276">Rattle также может определить правила взаимосвязей между наблюдениями и (или) переменными.</span><span class="sxs-lookup"><span data-stu-id="da534-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="da534-277">Эти вкладки не рассматриваются в этом вводном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="da534-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="da534-278">В Rattle также можно выполнять анализ кластеров.</span><span class="sxs-lookup"><span data-stu-id="da534-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="da534-279">Давайте исключить некоторые функции toomake hello вывода проще tooread.</span><span class="sxs-lookup"><span data-stu-id="da534-279">Let's exclude some features toomake hello output easier tooread.</span></span> <span data-ttu-id="da534-280">На hello **данные** выберите **Ignore** Далее tooeach переменных hello, за исключением следующих десяти элементов:</span><span class="sxs-lookup"><span data-stu-id="da534-280">On hello **Data** tab, choose **Ignore** next tooeach of hello variables except these ten items:</span></span>

* <span data-ttu-id="da534-281">word_freq_hp;</span><span class="sxs-lookup"><span data-stu-id="da534-281">word_freq_hp</span></span>
* <span data-ttu-id="da534-282">word_freq_technology;</span><span class="sxs-lookup"><span data-stu-id="da534-282">word_freq_technology</span></span>
* <span data-ttu-id="da534-283">word_freq_george;</span><span class="sxs-lookup"><span data-stu-id="da534-283">word_freq_george</span></span>
* <span data-ttu-id="da534-284">word_freq_remove;</span><span class="sxs-lookup"><span data-stu-id="da534-284">word_freq_remove</span></span>
* <span data-ttu-id="da534-285">word_freq_your;</span><span class="sxs-lookup"><span data-stu-id="da534-285">word_freq_your</span></span>
* <span data-ttu-id="da534-286">word_freq_dollar;</span><span class="sxs-lookup"><span data-stu-id="da534-286">word_freq_dollar</span></span>
* <span data-ttu-id="da534-287">word_freq_money;</span><span class="sxs-lookup"><span data-stu-id="da534-287">word_freq_money</span></span>
* <span data-ttu-id="da534-288">capital_run_length_longest;</span><span class="sxs-lookup"><span data-stu-id="da534-288">capital_run_length_longest</span></span>
* <span data-ttu-id="da534-289">word_freq_business;</span><span class="sxs-lookup"><span data-stu-id="da534-289">word_freq_business</span></span>
* <span data-ttu-id="da534-290">spam</span><span class="sxs-lookup"><span data-stu-id="da534-290">spam</span></span>

<span data-ttu-id="da534-291">Затем вернитесь toohello **кластера** выберите **KMeans**и набор hello *число кластеров* too4.</span><span class="sxs-lookup"><span data-stu-id="da534-291">Then go back toohello **Cluster** tab, choose **KMeans**, and set hello *Number of clusters* too4.</span></span> <span data-ttu-id="da534-292">Затем нажмите кнопку **Execute** (Выполнить).</span><span class="sxs-lookup"><span data-stu-id="da534-292">Then **Execute**.</span></span> <span data-ttu-id="da534-293">Hello результаты отображаются в окне вывода hello.</span><span class="sxs-lookup"><span data-stu-id="da534-293">hello results are displayed in hello output window.</span></span> <span data-ttu-id="da534-294">В одном кластере часто встречается слово "george" и "hp". Скорее всего, это деловое сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="da534-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="da534-295">toobuild модели машинного обучения дерева принятия решений простой:</span><span class="sxs-lookup"><span data-stu-id="da534-295">toobuild a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="da534-296">Выберите hello **модели** вкладке</span><span class="sxs-lookup"><span data-stu-id="da534-296">Select hello **Model** tab,</span></span>
* <span data-ttu-id="da534-297">Выберите **дерева** как hello **типа**.</span><span class="sxs-lookup"><span data-stu-id="da534-297">Choose **Tree** as hello **Type**.</span></span>
* <span data-ttu-id="da534-298">Выберите **Execute** toodisplay дерева hello в текстовой форме hello окно вывода.</span><span class="sxs-lookup"><span data-stu-id="da534-298">Select **Execute** toodisplay hello tree in text form in hello output window.</span></span>
* <span data-ttu-id="da534-299">Выберите hello **нарисовать** кнопку tooview графической версии.</span><span class="sxs-lookup"><span data-stu-id="da534-299">Select hello **Draw** button tooview a graphical version.</span></span> <span data-ttu-id="da534-300">Это выглядит довольно подобного дерева toohello, были получены ранее с помощью *rpart*.</span><span class="sxs-lookup"><span data-stu-id="da534-300">This looks quite similar toohello tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="da534-301">Один из удобных функций hello погремушка является его способность toorun методов несколько машинного обучения и быстро оценить их.</span><span class="sxs-lookup"><span data-stu-id="da534-301">One of hello nice features of Rattle is its ability toorun several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="da534-302">Ниже описана процедура hello.</span><span class="sxs-lookup"><span data-stu-id="da534-302">Here is hello procedure:</span></span>

* <span data-ttu-id="da534-303">Выберите **все** для hello **типа**.</span><span class="sxs-lookup"><span data-stu-id="da534-303">Choose **All** for hello **Type**.</span></span>
* <span data-ttu-id="da534-304">Нажмите кнопку **Execute**(Выполнить).</span><span class="sxs-lookup"><span data-stu-id="da534-304">Select **Execute**.</span></span>
* <span data-ttu-id="da534-305">После ее завершения можно щелкнуть любой отдельный **тип**, таких как **SVM**и просмотреть результаты hello.</span><span class="sxs-lookup"><span data-stu-id="da534-305">After it finishes you can click any single **Type**, like **SVM**, and view hello results.</span></span>
* <span data-ttu-id="da534-306">Вы также можете сравнить производительность hello hello моделей по результатам проверки hello, заданные с помощью hello **Evaluate** вкладки. Здравствуйте, например, **ошибка матрицы** выбора отображает hello матрицей, общая ошибка и ошибка усредненного класса для каждой модели на наборе проверки hello.</span><span class="sxs-lookup"><span data-stu-id="da534-306">You can also compare hello performance of hello models on hello validation set using hello **Evaluate** tab. For example, hello **Error Matrix** selection shows you hello confusion matrix, overall error, and averaged class error for each model on hello validation set.</span></span>
* <span data-ttu-id="da534-307">Вы также можете построить кривые ROC, выполнить анализ чувствительности и выполнить другие оценки модели.</span><span class="sxs-lookup"><span data-stu-id="da534-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="da534-308">После завершения построения модели, выберите hello **журнала** вкладке tooview hello R средой коде погремушка во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="da534-308">Once you're finished building models, select hello **Log** tab tooview hello R code run by Rattle during your session.</span></span> <span data-ttu-id="da534-309">Можно выбрать hello **Экспорт** кнопку toosave его.</span><span class="sxs-lookup"><span data-stu-id="da534-309">You can select hello **Export** button toosave it.</span></span>

> [!NOTE]
> <span data-ttu-id="da534-310">В текущем выпуске Rattle есть ошибка.</span><span class="sxs-lookup"><span data-stu-id="da534-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="da534-311">toomodify hello скрипт, или использовать его toorepeat шагов более поздней версии, необходимо вставить символ # поверх * экспортировать этот журнал... * в тексте hello hello журнала.</span><span class="sxs-lookup"><span data-stu-id="da534-311">toomodify hello script or use it toorepeat your steps later, you must insert a # character in front of *Export this log ... * in hello text of hello log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="da534-312">PostgreSQL и Squirrel SQL;</span><span class="sxs-lookup"><span data-stu-id="da534-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="da534-313">Hello DSVM поставляется с PostgreSQL установлен.</span><span class="sxs-lookup"><span data-stu-id="da534-313">hello DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="da534-314">PostgreSQL — продвинутая реляционная база данных с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="da534-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="da534-315">В этом разделе показано, как tooload нашей нежелательной почты набора данных в PostgreSQL и только затем запрос.</span><span class="sxs-lookup"><span data-stu-id="da534-315">This section shows how tooload our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="da534-316">Перед загрузкой данных hello, требуется проверка пароля tooallow с hello localhost.</span><span class="sxs-lookup"><span data-stu-id="da534-316">Before you can load hello data, you need tooallow password authentication from hello localhost.</span></span> <span data-ttu-id="da534-317">В окне командной строки:</span><span class="sxs-lookup"><span data-stu-id="da534-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="da534-318">Hello нижней части файла конфигурации hello являются несколько строк, в которых подробно hello разрешенных подключений:</span><span class="sxs-lookup"><span data-stu-id="da534-318">Near hello bottom of hello config file are several lines that detail hello allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="da534-319">Изменить md5 toouse строку hello «IPv4 локальных соединений» вместо ident, поэтому мы можете войти с использованием имени пользователя и пароля:</span><span class="sxs-lookup"><span data-stu-id="da534-319">Change hello "IPv4 local connections" line toouse md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="da534-320">И перезапустите службу postgres hello:</span><span class="sxs-lookup"><span data-stu-id="da534-320">And restart hello postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="da534-321">psql toolaunch, интерактивные терминалов для PostgreSQL, как пользователь встроенных postgres hello, выполните следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="da534-321">toolaunch psql, an interactive terminal for PostgreSQL, as hello built-in postgres user, run hello following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="da534-322">Создание учетной записи пользователя, с помощью hello же имя пользователя как hello Linux учетной записи, которую вы выполнили вход в качестве и задайте пароль:</span><span class="sxs-lookup"><span data-stu-id="da534-322">Create a new user account, using hello same username as hello Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="da534-323">Затем войти в toopsql учетной записью пользователя:</span><span class="sxs-lookup"><span data-stu-id="da534-323">Then log in toopsql as your user:</span></span>

    psql

<span data-ttu-id="da534-324">И импортировать данные hello в новую базу данных:</span><span class="sxs-lookup"><span data-stu-id="da534-324">And import hello data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="da534-325">Теперь давайте изучения данных hello и выполните несколько запросов с помощью **белка SQL**, графическое средство, которое служит для взаимодействия с базами данных через драйвер JDBC.</span><span class="sxs-lookup"><span data-stu-id="da534-325">Now, let's explore hello data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="da534-326">tooget запущен, запустите белка SQL из меню приложения hello.</span><span class="sxs-lookup"><span data-stu-id="da534-326">tooget started, launch Squirrel SQL from hello Applications menu.</span></span> <span data-ttu-id="da534-327">tooset копирование hello драйвера:</span><span class="sxs-lookup"><span data-stu-id="da534-327">tooset up hello driver:</span></span>

* <span data-ttu-id="da534-328">Выберите **Windows**, а затем — **View Drivers** (Просмотреть драйверы).</span><span class="sxs-lookup"><span data-stu-id="da534-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="da534-329">Щелкните **PostgreSQL** правой кнопкой мыши и выберите **Modify Driver** (Изменить драйвер).</span><span class="sxs-lookup"><span data-stu-id="da534-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="da534-330">Выберите **Extra Class Path** (Путь к дополнительным классам), а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="da534-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="da534-331">Введите ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** для hello **имя файла** и</span><span class="sxs-lookup"><span data-stu-id="da534-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for hello **File Name** and</span></span>
* <span data-ttu-id="da534-332">Щелкните **Open**(Открыть).</span><span class="sxs-lookup"><span data-stu-id="da534-332">Select **Open**.</span></span>
* <span data-ttu-id="da534-333">Щелкните "Список драйверов", выберите **org.postgresql.Driver** в области **Имя класса** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="da534-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="da534-334">tooset hello подключения toohello локального сервера:</span><span class="sxs-lookup"><span data-stu-id="da534-334">tooset up hello connection toohello local server:</span></span>

* <span data-ttu-id="da534-335">Выберите **Windows**, а затем — **View Aliases** (Просмотреть псевдонимы).</span><span class="sxs-lookup"><span data-stu-id="da534-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="da534-336">Выберите hello  **+**  toomake кнопку Новый псевдоним.</span><span class="sxs-lookup"><span data-stu-id="da534-336">Choose hello **+** button toomake a new alias.</span></span>
* <span data-ttu-id="da534-337">Назовите его *нежелательной почты базы данных*, выберите **PostgreSQL** в hello **драйвер** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="da534-337">Name it *Spam database*, choose **PostgreSQL** in hello **Driver** drop-down.</span></span>
* <span data-ttu-id="da534-338">Задать URL-адрес hello слишком*jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="da534-338">Set hello URL too*jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="da534-339">Введите *имя пользователя* и *пароль*.</span><span class="sxs-lookup"><span data-stu-id="da534-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="da534-340">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="da534-340">Click **OK**.</span></span>
* <span data-ttu-id="da534-341">tooopen hello **подключения** окно, дважды щелкните hello ***нежелательной почты базы данных*** псевдоним.</span><span class="sxs-lookup"><span data-stu-id="da534-341">tooopen hello **Connection** window, double-click hello ***Spam database*** alias.</span></span>
* <span data-ttu-id="da534-342">Нажмите кнопку **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="da534-342">Select **Connect**.</span></span>

<span data-ttu-id="da534-343">toorun некоторые запросы:</span><span class="sxs-lookup"><span data-stu-id="da534-343">toorun some queries:</span></span>

* <span data-ttu-id="da534-344">Выберите hello **SQL** вкладки.</span><span class="sxs-lookup"><span data-stu-id="da534-344">Select hello **SQL** tab.</span></span>
* <span data-ttu-id="da534-345">Введите простой запрос, например `SELECT * from data;` в текстовом поле запроса hello hello верхней части вкладки SQL hello.</span><span class="sxs-lookup"><span data-stu-id="da534-345">Enter a simple query such as `SELECT * from data;` in hello query textbox at hello top of hello SQL tab.</span></span>
* <span data-ttu-id="da534-346">Нажмите клавишу **Ctrl + Enter** toorun его.</span><span class="sxs-lookup"><span data-stu-id="da534-346">Press **Ctrl-Enter** toorun it.</span></span> <span data-ttu-id="da534-347">По умолчанию SQL белка возвращает hello первые 100 строк из запроса.</span><span class="sxs-lookup"><span data-stu-id="da534-347">By default Squirrel SQL returns hello first 100 rows from your query.</span></span>

<span data-ttu-id="da534-348">Существует множество запросов, можно выполнить tooexplore эти данные.</span><span class="sxs-lookup"><span data-stu-id="da534-348">There are many more queries you could run tooexplore this data.</span></span> <span data-ttu-id="da534-349">Например, как работает hello частоту слово hello *сделать* нежелательной почты и ham различаются?</span><span class="sxs-lookup"><span data-stu-id="da534-349">For example, how does hello frequency of hello word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="da534-350">Или Каковы характеристики hello электронной почты, которые часто содержат *3d*?</span><span class="sxs-lookup"><span data-stu-id="da534-350">Or what are hello characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="da534-351">Большинство сообщений электронной почты, имеющих высокую вхождения *3d* являются внешне нежелательной почты, поэтому он может быть полезной функцией для создания сообщений электронной почты типа hello tooclassify прогнозной модели.</span><span class="sxs-lookup"><span data-stu-id="da534-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model tooclassify hello emails.</span></span>

<span data-ttu-id="da534-352">Если требуется tooperform машинного обучения с данными, хранящимися в базе данных PostgreSQL, рассмотрите возможность использования [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="da534-352">If you wanted tooperform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="da534-353">хранилище данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="da534-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="da534-354">Хранилище данных SQL Azure — это развернутая в облаке база данных, способная обрабатывать большие объемы реляционных и нереляционных данных.</span><span class="sxs-lookup"><span data-stu-id="da534-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="da534-355">Дополнительные сведения см. в статье [Что такое хранилище данных SQL Azure?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="da534-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="da534-356">tooconnect toohello данных в хранилище и создайте таблицу hello выполнения hello следующую команду из командной строки:</span><span class="sxs-lookup"><span data-stu-id="da534-356">tooconnect toohello data warehouse and create hello table, run hello following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="da534-357">Затем в строке sqlcmd hello:</span><span class="sxs-lookup"><span data-stu-id="da534-357">Then at hello sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="da534-358">Скопируйте данные с помощью bcp:</span><span class="sxs-lookup"><span data-stu-id="da534-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="da534-359">разрывы строк Hello в загруженном файле hello, стиль Windows, но bcp ожидает стиле UNIX, поэтому необходимо tootell bcp, что при использовании hello флаг - r.</span><span class="sxs-lookup"><span data-stu-id="da534-359">hello line endings in hello downloaded file are Windows-style, but bcp expects UNIX-style, so we need tootell bcp that with hello -r flag.</span></span>
>
>

<span data-ttu-id="da534-360">Выполните запрос с использованием sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="da534-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="da534-361">Запросы также можно выполнять с помощью Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="da534-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="da534-362">Аналогичные действия можно использовать для PostgreSQL, с помощью hello MSSQL Server драйвера JDBC, которую можно найти в ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="da534-362">Follow similar steps for PostgreSQL, using hello Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da534-363">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="da534-363">Next steps</span></span>
<span data-ttu-id="da534-364">Обзор разделы с пошаговыми руководствами hello задачами, которые составляют hello процесса обработки и анализа данных в Azure см. в разделе [процесс обработки и анализа данных для команды](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="da534-364">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="da534-365">Описание других пошаговых руководств начала до конца, демонстрирующих hello инструкциям hello командного процесса обработки и анализа данных для конкретных сценариев см. в разделе [пошаговые руководства командного процесса обработки и анализа данных](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="da534-365">For a description of other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="da534-366">Пошаговые руководства Hello также показывают, как облачные toocombine и локальных средств и служб в рабочий процесс или конвейера toocreate интеллектуальной приложения.</span><span class="sxs-lookup"><span data-stu-id="da534-366">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>
