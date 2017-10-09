---
title: "aaaImport данных из файла в студии машинного обучения Azure | Документы Microsoft"
description: "Узнайте, как файл tooupload обучающие данные из вашего жесткого диска tooAzure студии машинного обучения. Это создает модуль набора данных в рабочей области hello."
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
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="987ff-105">Импорт данных для обучения из файла на жестком диске в Студию машинного обучения</span><span class="sxs-lookup"><span data-stu-id="987ff-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="987ff-106">Узнайте, как файл tooupload данных из вашего toouse жесткого диска с именем обучающие данные хранятся в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="987ff-106">Learn how tooupload a data file from your hard drive toouse as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="987ff-107">Путем импорта файла данных hello, имеется набор данных модуль готов к использованию в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="987ff-107">By importing hello data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-tooimport-data-from-a-local-file"></a><span data-ttu-id="987ff-108">Данные шаги tooimport из локального файла</span><span class="sxs-lookup"><span data-stu-id="987ff-108">Steps tooimport data from a local file</span></span>
<span data-ttu-id="987ff-109">Здравствуйте tooimport данных с локального жесткого диска, следующие:</span><span class="sxs-lookup"><span data-stu-id="987ff-109">tooimport data from a local hard drive, do hello following:</span></span>

1. <span data-ttu-id="987ff-110">Нажмите кнопку **+ создать** hello нижней части окна hello студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="987ff-110">Click **+NEW** at hello bottom of hello Machine Learning Studio window.</span></span>
2. <span data-ttu-id="987ff-111">Выберите **Набор данных** и **From local file** (Из локального файла).</span><span class="sxs-lookup"><span data-stu-id="987ff-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="987ff-112">В hello **отправить новый набор данных** диалогового окна обзора toohello файл tooupload</span><span class="sxs-lookup"><span data-stu-id="987ff-112">In hello **Upload a new dataset** dialog, browse toohello file you want tooupload</span></span>
4. <span data-ttu-id="987ff-113">Введите имя, укажите тип данных hello и при необходимости введите описание.</span><span class="sxs-lookup"><span data-stu-id="987ff-113">Enter a name, identify hello data type, and optionally enter a description.</span></span> <span data-ttu-id="987ff-114">Описание рекомендуется — позволяет toorecord все характеристики данных hello требуется tooremember при использовании данных hello в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="987ff-114">A description is recommended - it allows you toorecord any characteristics about hello data that you want tooremember when using hello data in hello future.</span></span>
5. <span data-ttu-id="987ff-115">Здравствуйте, флажок **это hello новой версии существующего набора данных** позволяет tooupdate существующий набор данных с новыми данными.</span><span class="sxs-lookup"><span data-stu-id="987ff-115">hello checkbox **This is hello new version of an existing dataset** allows you tooupdate an existing dataset with new data.</span></span> <span data-ttu-id="987ff-116">Установите этот флажок, а затем введите имя hello существующего набора данных.</span><span class="sxs-lookup"><span data-stu-id="987ff-116">Click this checkbox and then enter hello name of an existing dataset.</span></span>

![Передача нового набора данных](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="987ff-118">Во время передачи появится сообщение о том, что файл передается.</span><span class="sxs-lookup"><span data-stu-id="987ff-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="987ff-119">Отправить время зависит от размера hello быстродействия данных и hello toohello службы подключения.</span><span class="sxs-lookup"><span data-stu-id="987ff-119">Upload time depends on hello size of your data and hello speed of your connection toohello service.</span></span> <span data-ttu-id="987ff-120">Если известно, что файл hello займет много времени, можно сделать прочего в студии машинного обучения, во время ожидания.</span><span class="sxs-lookup"><span data-stu-id="987ff-120">If you know hello file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="987ff-121">Тем не менее закрытие обозревателя hello приводит toofail передачи данных hello.</span><span class="sxs-lookup"><span data-stu-id="987ff-121">However, closing hello browser causes hello data upload toofail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="987ff-122">Модуль набора данных готов к использованию</span><span class="sxs-lookup"><span data-stu-id="987ff-122">Dataset module is ready for use</span></span>
<span data-ttu-id="987ff-123">После загрузки данных, он хранится в модуле набора данных и доступных tooany эксперимента в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="987ff-123">Once your data is uploaded, it's stored in a dataset module and is available tooany experiment in your workspace.</span></span>

<span data-ttu-id="987ff-124">При редактировании эксперимента можно найти hello наборы данных, созданные в hello **Мои наборы данных** списке hello **сохраненные наборы данных** списка в палитре модуля hello.</span><span class="sxs-lookup"><span data-stu-id="987ff-124">When you're editing an experiment, you can find hello datasets you've created in hello **My Datasets** list under hello **Saved Datasets** list in hello module palette.</span></span> <span data-ttu-id="987ff-125">Вы можно перетаскивать hello набора данных на холст эксперимента hello при необходимости toouse hello dataset для дальнейшего анализа и машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="987ff-125">You can drag and drop hello dataset onto hello experiment canvas when you want toouse hello dataset for further analytics and machine learning.</span></span>
