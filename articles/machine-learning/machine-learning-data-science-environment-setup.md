---
title: "Настройка сред обработки и анализа данных в Azure | Документация Майкрософт"
description: "Настройка сред обработки и анализа данных в Azure, используемых в процессе обработки и анализа данных группы."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 481cfa6a-7ea3-46ac-b0f9-2e3982c37153
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: bradsev
ms.openlocfilehash: 4f2f66288428aa0aa41abb40ce0e43c4848543ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-data-science-environments-for-use-in-the-team-data-science-process"></a><span data-ttu-id="d86d2-103">Настройка сред обработки и анализа данных для использования в процессе обработки и анализа данных группы</span><span class="sxs-lookup"><span data-stu-id="d86d2-103">Set up data science environments for use in the Team Data Science Process</span></span>
<span data-ttu-id="d86d2-104">Процесс обработки и анализа данных группы использует различные специализированные среды для хранения, обработки и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="d86d2-104">The Team Data Science Process uses various data science environments for the storage, processing, and analysis of data.</span></span> <span data-ttu-id="d86d2-105">Сюда относятся хранилище BLOB-объектов Azure, несколько типов виртуальных машин Azure, кластеры HDInsight (Hadoop) и рабочие области Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="d86d2-105">They include Azure Blob Storage, several types of Azure virtual machines, HDInsight (Hadoop) clusters, and Azure Machine Learning workspaces.</span></span> <span data-ttu-id="d86d2-106">Выбор используемой среды зависит от типа и количества данных, которые нужно моделировать, и места хранения этих данных в облаке.</span><span class="sxs-lookup"><span data-stu-id="d86d2-106">The decision about which environment to use depends on the type and quantity of data to be modeled and the target destination for that data in the cloud.</span></span> 

* <span data-ttu-id="d86d2-107">Сведения о том, какие факторы нужно учесть при выборе, см. в статье [Как определить сценарии и план для расширенной аналитической обработки данных](machine-learning-data-science-plan-your-environment.md).</span><span class="sxs-lookup"><span data-stu-id="d86d2-107">For guidance on questions to consider when making this decision, see [Plan Your Azure Machine Learning Data Science Environment](machine-learning-data-science-plan-your-environment.md).</span></span> 
* <span data-ttu-id="d86d2-108">Каталог, содержащий несколько сценариев, возможных при выполнении расширенной аналитики, доступен в статье [Scenarios for the Team Data Science Process](machine-learning-data-science-plan-sample-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="d86d2-108">For a catalog of some of the scenarios you might encounter when doing advanced analytics, see [Scenarios for the Team Data Science Process](machine-learning-data-science-plan-sample-scenarios.md)</span></span>

<span data-ttu-id="d86d2-109">Это меню содержит ссылки на разделы, описывающие настройку различных сред обработки и анализа данных, используемых процессом обработки и анализа данных группы.</span><span class="sxs-lookup"><span data-stu-id="d86d2-109">This menu links to topics that describe how to set up the various data science environments used by the Team Data Science Process.</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="d86d2-110">**Виртуальная машина Майкрософт для обработки и анализа данных (DSVM)** также доступна как образ виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="d86d2-110">The **Microsoft Data Science Virtual Machine (DSVM)** is also available as an Azure virtual machine (VM) image.</span></span> <span data-ttu-id="d86d2-111">В этой виртуальной машине Azure предварительно установлен и настроен ряд распространенных средств, которые обычно используются для анализа данных и машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d86d2-111">This VM is pre-installed and configured with several popular tools that are commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="d86d2-112">DSVM доступна в Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="d86d2-112">The DSVM is available on both Windows and Linux.</span></span> <span data-ttu-id="d86d2-113">Дополнительные сведения см. в статье [Introduction to the Data Science Virtual Machine for Linux and Windows, a cloud environment and toolkit](machine-learning-data-science-virtual-machine-overview.md) (Введение в виртуальные машины для анализа и обработки данных для Linux и Windows, облачную инфраструктуру и набор средств).</span><span class="sxs-lookup"><span data-stu-id="d86d2-113">For further information, see [Introduction to the cloud-based Data Science Virtual Machine for Linux and Windows](machine-learning-data-science-virtual-machine-overview.md).</span></span>

