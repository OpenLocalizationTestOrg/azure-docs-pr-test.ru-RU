---
title: "Импорт данных из файла в Студию машинного обучения Azure | Документация Майкрософт"
description: "Узнайте, как отправить файл с данными для обучения с жесткого диска в Студию машинного обучения Azure. При этом в рабочей области создается модуль набора данных."
keywords: "импорт данных, формат данных, типы данных, источники данных, обучающие данные"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 18010864160ceb2d76aea37196e6944bbe426457
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="3c9a5-105">Импорт данных для обучения из файла на жестком диске в Студию машинного обучения</span><span class="sxs-lookup"><span data-stu-id="3c9a5-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="3c9a5-106">Узнайте, как отправить файл с данными с жесткого диска и использовать его в качестве данных для обучения в Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-106">Learn how to upload a data file from your hard drive to use as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="3c9a5-107">Импортируя файл с данными, вы получаете модуль набора данных, готовый к использованию в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-107">By importing the data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-to-import-data-from-a-local-file"></a><span data-ttu-id="3c9a5-108">Импорт данных из локального файла</span><span class="sxs-lookup"><span data-stu-id="3c9a5-108">Steps to import data from a local file</span></span>
<span data-ttu-id="3c9a5-109">Чтобы импортировать данные из локального жесткого диска, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="3c9a5-109">To import data from a local hard drive, do the following:</span></span>

1. <span data-ttu-id="3c9a5-110">В Студии машинного обучения щелкните **+СОЗДАТЬ** внизу окна.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-110">Click **+NEW** at the bottom of the Machine Learning Studio window.</span></span>
2. <span data-ttu-id="3c9a5-111">Выберите **Набор данных** и **From local file** (Из локального файла).</span><span class="sxs-lookup"><span data-stu-id="3c9a5-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="3c9a5-112">В диалоговом окне **Передать новый набор данных** перейдите к файлу, который необходимо передать</span><span class="sxs-lookup"><span data-stu-id="3c9a5-112">In the **Upload a new dataset** dialog, browse to the file you want to upload</span></span>
4. <span data-ttu-id="3c9a5-113">Введите имя, укажите тип данных и, при необходимости, введите описание.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-113">Enter a name, identify the data type, and optionally enter a description.</span></span> <span data-ttu-id="3c9a5-114">Рекомендуем ввести описание — оно позволяет записать все характеристики данных, которые необходимо помнить при использовании данных в будущем.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-114">A description is recommended - it allows you to record any characteristics about the data that you want to remember when using the data in the future.</span></span>
5. <span data-ttu-id="3c9a5-115">Флажок **Это новая версия существующего набора данных** позволяет обновить существующий набор данных новыми данными.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-115">The checkbox **This is the new version of an existing dataset** allows you to update an existing dataset with new data.</span></span> <span data-ttu-id="3c9a5-116">Установите этот флажок, а затем введите имя имеющегося набора данных.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-116">Click this checkbox and then enter the name of an existing dataset.</span></span>

![Передача нового набора данных](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="3c9a5-118">Во время передачи появится сообщение о том, что файл передается.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="3c9a5-119">Время передачи зависит от объема данных и скорости подключения к службе.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-119">Upload time depends on the size of your data and the speed of your connection to the service.</span></span> <span data-ttu-id="3c9a5-120">Если известно, что файл будет передаваться слишком долго, в это время можно заняться другими задачами в Студии машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-120">If you know the file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="3c9a5-121">Тем не менее закрытие браузера приведет к ошибке передачи данных.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-121">However, closing the browser causes the data upload to fail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="3c9a5-122">Модуль набора данных готов к использованию</span><span class="sxs-lookup"><span data-stu-id="3c9a5-122">Dataset module is ready for use</span></span>
<span data-ttu-id="3c9a5-123">После загрузки данные сохраняются в модуле набора данных и доступны для любого эксперимента в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-123">Once your data is uploaded, it's stored in a dataset module and is available to any experiment in your workspace.</span></span>

<span data-ttu-id="3c9a5-124">При редактировании эксперимента вы можете найти ранее созданные наборы данных в списке **My Datasets** (Мои наборы данных), который входит в список **Saved Datasets** (Сохраненные наборы данных), в палитре модулей.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-124">When you're editing an experiment, you can find the datasets you've created in the **My Datasets** list under the **Saved Datasets** list in the module palette.</span></span> <span data-ttu-id="3c9a5-125">Перетащите набор данных на холст эксперимента, где нужно использовать эти данные для последующего анализа и машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="3c9a5-125">You can drag and drop the dataset onto the experiment canvas when you want to use the dataset for further analytics and machine learning.</span></span>
