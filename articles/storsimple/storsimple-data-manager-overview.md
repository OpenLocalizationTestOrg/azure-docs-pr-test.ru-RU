---
title: "Обзор диспетчера данных Azure StorSimple aaaMicrosoft | Документы Microsoft"
description: "Общие сведения о hello службы диспетчера StorSimple данных (личной предварительной версии)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="61c4e-103">Общие сведения о диспетчере данных StorSimple (закрытая предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="61c4e-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="61c4e-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="61c4e-104">Overview</span></span>

<span data-ttu-id="61c4e-105">Microsoft Azure StorSimple — это гибридное Облачное решение хранилища, адреса hello сложности неструктурированные данные, обычно связанные с общими файловыми ресурсами.</span><span class="sxs-lookup"><span data-stu-id="61c4e-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses hello complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="61c4e-106">StorSimple использует облачного хранилища, как локальное решение расширение hello и автоматически уровнями данных через hello локальное хранилище и Облачное хранилище.</span><span class="sxs-lookup"><span data-stu-id="61c4e-106">StorSimple uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="61c4e-107">Интегрируется с локальной защиты данных и облачных моментальных снимков, устраняет необходимость hello sprawling инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="61c4e-107">Integrated data protection, with local and cloud snapshots, eliminates hello need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="61c4e-108">Архивация и аварийного восстановления также не вызывает затруднений с облаком hello, выступающего в качестве удаленного расположения.</span><span class="sxs-lookup"><span data-stu-id="61c4e-108">Archival and disaster recovery is also seamless with hello cloud acting as an offsite location.</span></span>

<span data-ttu-id="61c4e-109">Hello службы DTS, мы представляем в этом документе, позволяет вам tooseamlessly доступа hello StorSimple данных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="61c4e-109">hello data transformation service that we are introducing in this document, allows you tooseamlessly access hello StorSimple data in hello cloud.</span></span> <span data-ttu-id="61c4e-110">Эта служба предоставляет API-интерфейсы tooextract данные из StorSimple и представлять их tooother Azure служб в форматах, которые могут быть сразу использованы.</span><span class="sxs-lookup"><span data-stu-id="61c4e-110">This service provides APIs tooextract data from StorSimple and present it tooother Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="61c4e-111">Hello форматы, поддерживаемые в этой предварительной версии — BLOB-объекты Azure и средств служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="61c4e-111">hello formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="61c4e-112">Это преобразование позволяет вам tooeasily подключения службы, такие как данные toooperate служб мультимедиа Azure, Azure HDInsight, машинного обучения Azure и поиска Azure на локального устройства серии StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="61c4e-112">This transformation enables you tooeasily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search toooperate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="61c4e-113">Ниже представлена общая блок-схема, иллюстрирующая этот процесс.</span><span class="sxs-lookup"><span data-stu-id="61c4e-113">A high-level block diagram illustrating this is shown below.</span></span>

![Общая схема](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="61c4e-115">В этом документе объясняется, как можно зарегистрироваться для получения закрытой предварительной версии этой службы.</span><span class="sxs-lookup"><span data-stu-id="61c4e-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="61c4e-116">Также объясняется, как можно использовать это приложение toowrite службы, использующие StorSimple данных и другими службами Azure в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="61c4e-116">It also explains how you can use this service toowrite applications that use StorSimple data and other Azure services in hello cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="61c4e-117">Регистрация для получения предварительной версии диспетчера данных</span><span class="sxs-lookup"><span data-stu-id="61c4e-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="61c4e-118">Перед регистрацией для службы данных Manager hello просмотрите hello следующие необходимые условия.</span><span class="sxs-lookup"><span data-stu-id="61c4e-118">Before you sign up for hello Data Manager service, review hello following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="61c4e-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="61c4e-119">Prerequisites</span></span>

<span data-ttu-id="61c4e-120">В этом упражнении предполагается, что у вас есть:</span><span class="sxs-lookup"><span data-stu-id="61c4e-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="61c4e-121">активная подписка Azure;</span><span class="sxs-lookup"><span data-stu-id="61c4e-121">an active Azure subscription.</span></span>
* <span data-ttu-id="61c4e-122">tooa доступа зарегистрированные устройства серии StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="61c4e-122">access tooa registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="61c4e-123">Здравствуйте, все ключи, связанные с устройства серии StorSimple 8000 hello.</span><span class="sxs-lookup"><span data-stu-id="61c4e-123">all hello keys associated with hello StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="61c4e-124">Регистрация</span><span class="sxs-lookup"><span data-stu-id="61c4e-124">Sign up</span></span>

<span data-ttu-id="61c4e-125">Hello данных StorSimple Manager находится в личной ознакомительной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="61c4e-125">hello StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="61c4e-126">Выполните следующие шаги toosign для частной предварительной версии этой службы hello.</span><span class="sxs-lookup"><span data-stu-id="61c4e-126">Perform hello following steps toosign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="61c4e-127">Войдите на hello портал Azure с расширением hello данных StorSimple Manager в: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="61c4e-127">Log into hello Azure portal with hello StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="61c4e-128">Используйте ваш toolog учетных данных Azure в.</span><span class="sxs-lookup"><span data-stu-id="61c4e-128">Use your Azure credentials toolog in.</span></span>

2.  <span data-ttu-id="61c4e-129">Нажмите кнопку hello  **+**  toocreate значок службы.</span><span class="sxs-lookup"><span data-stu-id="61c4e-129">Click hello **+** icon toocreate a service.</span></span> <span data-ttu-id="61c4e-130">Нажмите кнопку **хранения** и нажмите кнопку **разделе все** в колонке hello, открывающемся.</span><span class="sxs-lookup"><span data-stu-id="61c4e-130">Click **Storage** and then click **See All** in hello blade that opens up.</span></span>

    ![Поиск значка диспетчера данных StorSimple](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="61c4e-132">Значок hello данных StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="61c4e-132">You see hello StorSimple Data Manager icon.</span></span>

    ![Выбор значка диспетчера данных StorSimple](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="61c4e-134">Щелкните значок диспетчера данных StorSimple и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="61c4e-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="61c4e-135">Выбор подписки hello должны tooenable для получения личной предварительной версии hello и нажмите кнопку **зарегистрироваться me!**</span><span class="sxs-lookup"><span data-stu-id="61c4e-135">Pick hello subscription that you want tooenable for hello private preview and then click **Sign me up!**</span></span>

    ![Кнопка "Зарегистрироваться"](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="61c4e-137">Эта команда отправляет запрос tooonboard вы.</span><span class="sxs-lookup"><span data-stu-id="61c4e-137">This sends a request tooonboard you.</span></span> <span data-ttu-id="61c4e-138">Мы выполним эту операцию в кратчайшие сроки.</span><span class="sxs-lookup"><span data-stu-id="61c4e-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="61c4e-139">После включения подписки можно создать службу диспетчера данных StorSimple.</span><span class="sxs-lookup"><span data-stu-id="61c4e-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="61c4e-140">tooeasily доступа к службе диспетчера StorSimple данных hello, щелкните значок toopin hello его tooyour "Избранное".</span><span class="sxs-lookup"><span data-stu-id="61c4e-140">tooeasily access hello StorSimple Data Manager service, click hello star icon toopin it tooyour favorites.</span></span>

    ![Доступ к диспетчеру данных StorSimple](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="61c4e-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61c4e-142">Next steps</span></span>

<span data-ttu-id="61c4e-143">[Использовать пользовательский Интерфейс диспетчера данных StorSimple tootransform данные](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="61c4e-143">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
