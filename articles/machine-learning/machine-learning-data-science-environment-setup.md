---
title: "aaaSet среды обработки и анализа данных в Azure | Документы Microsoft"
description: "Настройка данных среды обработки и анализа в Azure для использования в hello командного процесса обработки и анализа данных."
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
ms.openlocfilehash: 11e16416296d687c15fdaf17558aebc2d04737c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-data-science-environments-for-use-in-hello-team-data-science-process"></a><span data-ttu-id="7ad8e-103">Настройка данных среды обработки и анализа для использования в hello командного процесса обработки и анализа данных</span><span class="sxs-lookup"><span data-stu-id="7ad8e-103">Set up data science environments for use in hello Team Data Science Process</span></span>
<span data-ttu-id="7ad8e-104">Hello командного процесса обработки и анализа данных использует различные среды обработки и анализа данных для hello хранения, обработки и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="7ad8e-104">hello Team Data Science Process uses various data science environments for hello storage, processing, and analysis of data.</span></span> <span data-ttu-id="7ad8e-105">Сюда относятся хранилище BLOB-объектов Azure, несколько типов виртуальных машин Azure, кластеры HDInsight (Hadoop) и рабочие области Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad8e-105">They include Azure Blob Storage, several types of Azure virtual machines, HDInsight (Hadoop) clusters, and Azure Machine Learning workspaces.</span></span> <span data-ttu-id="7ad8e-106">Hello решение о выборе среды toouse зависит от типа hello и количество данных toobe моделировать и hello целевого назначения для данных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="7ad8e-106">hello decision about which environment toouse depends on hello type and quantity of data toobe modeled and hello target destination for that data in hello cloud.</span></span> 

* <span data-ttu-id="7ad8e-107">Рекомендации по tooconsider вопросы при принятия этого решения см. в разделе [планирование Azure машины обучения данных обработки и анализа среды](machine-learning-data-science-plan-your-environment.md).</span><span class="sxs-lookup"><span data-stu-id="7ad8e-107">For guidance on questions tooconsider when making this decision, see [Plan Your Azure Machine Learning Data Science Environment](machine-learning-data-science-plan-your-environment.md).</span></span> 
* <span data-ttu-id="7ad8e-108">Каталог некоторые сценарии hello, могут возникнуть при выполнении расширенной аналитики. в разделе [сценарии для hello командного процесса обработки и анализа данных](machine-learning-data-science-plan-sample-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="7ad8e-108">For a catalog of some of hello scenarios you might encounter when doing advanced analytics, see [Scenarios for hello Team Data Science Process](machine-learning-data-science-plan-sample-scenarios.md)</span></span>

<span data-ttu-id="7ad8e-109">Это меню связывает tootopics, которые описывают возможности tooset копирование hello различных средах обработки и анализа данных по использованию hello командного процесса обработки и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="7ad8e-109">This menu links tootopics that describe how tooset up hello various data science environments used by hello Team Data Science Process.</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="7ad8e-110">Hello **виртуальной машины обработки и анализа данных Microsoft (DSVM)** доступен также в виде образа виртуальной машины (VM) Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad8e-110">hello **Microsoft Data Science Virtual Machine (DSVM)** is also available as an Azure virtual machine (VM) image.</span></span> <span data-ttu-id="7ad8e-111">В этой виртуальной машине Azure предварительно установлен и настроен ряд распространенных средств, которые обычно используются для анализа данных и машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="7ad8e-111">This VM is pre-installed and configured with several popular tools that are commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="7ad8e-112">Hello DSVM доступен в Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="7ad8e-112">hello DSVM is available on both Windows and Linux.</span></span> <span data-ttu-id="7ad8e-113">Дополнительные сведения см. в разделе [toohello введение облачного виртуальная машина анализа данных для Linux и Windows](machine-learning-data-science-virtual-machine-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7ad8e-113">For further information, see [Introduction toohello cloud-based Data Science Virtual Machine for Linux and Windows](machine-learning-data-science-virtual-machine-overview.md).</span></span>

