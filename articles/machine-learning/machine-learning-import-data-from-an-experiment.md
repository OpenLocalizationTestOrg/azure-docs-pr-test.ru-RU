---
title: "Импорт данных из другого эксперимента в Студию машинного обучения | Документация Майкрософт"
description: "В статье описывается, как сохранить учебные данные в студию машинного обучения Azure и использовать их в другом эксперименте."
keywords: "импорт данных, данные, источники данных, обучающие данные"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 7da9dcec-5693-4bb6-8166-15904e7f75c3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: ecfa2110d0d51511ceb5bd07b730732ecfa2e9e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-data-into-azure-machine-learning-studio-from-another-experiment"></a><span data-ttu-id="1a8cf-104">Импорт данных в студию машинного обучения Azure из другой среды</span><span class="sxs-lookup"><span data-stu-id="1a8cf-104">Import your data into Azure Machine Learning Studio from another experiment</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="1a8cf-105">Иногда понадобится получить в эксперименте промежуточный результат, который будет использоваться в другом эксперименте.</span><span class="sxs-lookup"><span data-stu-id="1a8cf-105">There will be times when you'll want to take an intermediate result from one experiment and use it as part of another experiment.</span></span> <span data-ttu-id="1a8cf-106">Для этого сохраните модуль как набор данных, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="1a8cf-106">To do this, you save the module as a dataset:</span></span>

1. <span data-ttu-id="1a8cf-107">Щелкните выходные данные модуля, которые требуется сохранить в виде набора данных.</span><span class="sxs-lookup"><span data-stu-id="1a8cf-107">Click the output of the module that you want to save as a dataset.</span></span>
2. <span data-ttu-id="1a8cf-108">Щелкните **Сохранить как набор данных**.</span><span class="sxs-lookup"><span data-stu-id="1a8cf-108">Click **Save as Dataset**.</span></span>
3. <span data-ttu-id="1a8cf-109">При появлении запроса введите имя и описание, которое позволит легко идентифицировать набор данных.</span><span class="sxs-lookup"><span data-stu-id="1a8cf-109">When prompted, enter a name and a description that would allow you to identify the dataset easily.</span></span>
4. <span data-ttu-id="1a8cf-110">Установите флажок **ОК** .</span><span class="sxs-lookup"><span data-stu-id="1a8cf-110">Click the **OK** checkmark.</span></span>

<span data-ttu-id="1a8cf-111">После завершения сохранения набор данных будет доступен для использования в любом эксперименте в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="1a8cf-111">When the save finishes, the dataset will be available for use within any experiment in your workspace.</span></span> <span data-ttu-id="1a8cf-112">Его можно найти в списке **Сохраненные наборы данных** в палитре модулей.</span><span class="sxs-lookup"><span data-stu-id="1a8cf-112">You can find it in the **Saved Datasets** list in the module palette.</span></span>

