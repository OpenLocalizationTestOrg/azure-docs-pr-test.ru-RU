---
title: "Виртуальные машины научных вычислений Azure данных как серверы ноутбук IPython aaaProvision | Документы Microsoft"
description: "Настройка виртуальной машины для обработки и анализа данных в качестве сервера IPython Notebook с помощью вспомогательных средств."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 95e1fa87-794a-4d03-80a4-af4f3f3ac31e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 7c0abcbcb822918332f76a9f16690a72b90f4b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a>Подготовка виртуальных машин Azure для обработки и анализа данных в качестве серверов IPython Notebook
Инструкции приведены ниже, описывающих, как tooset ВМ Azure и ВМ со службой SQL Azure, как ноутбук IPython серверы. Виртуальная машина Windows Hello настраивается с вспомогательными средствами, например ноутбук IPython, обозреватель хранилища Azure и AzCopy, а также других средств, которые полезны для проектов научных вычислений. Azure Storage Explorer и AzCopy, например, предоставляют удобный способы хранения tooAzure tooupload данных с локального компьютера или toodownload его tooyour локального компьютера из хранилища. 

Это меню ссылки, описывающие возможности tooset копирование hello различных средах обработки и анализа данных по использованию hello tootopics [процесса обработки и анализа данных Team (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Несколько типов виртуальных машин Azure можно подготовить и настроить toobe используются как часть среды обработки и анализа данных на основе облака. Hello принятия решений о какой версия виртуальной машины toouse зависит от типа hello и количество toobe данных моделируются с помощью машинного обучения и hello целевое место назначения для данных в облаке hello. 

* Рекомендации по tooconsider вопросы hello при принятии решения о этого разделе [планирование Azure машины обучения данных обработки и анализа среды](machine-learning-data-science-plan-your-environment.md). 
* Каталог некоторые сценарии hello, могут возникнуть при выполнении расширенной аналитики. в разделе [сценарии для hello расширенное аналитика и технологии в машинном обучении Azure](machine-learning-data-science-plan-sample-scenarios.md)

Рассмотрите два набора инструкций.

* [Настройка виртуальной машины Azure как ноутбук IPython сервер для расширенной аналитики](machine-learning-data-science-setup-virtual-machine.md) показано использование tooprovision виртуальной машине Azure с ноутбук IPython и другими средствами обработки и анализа данных toodo для случаев, когда один из видов хранилища Azure, отличные от SQL можно указывать данные, используемые toostore hello.
* [Настройка виртуальной машине Azure SQL Server как ноутбук IPython сервер для расширенной аналитики](machine-learning-data-science-setup-sql-server-virtual-machine.md) показано использование tooprovision виртуальной машине Azure SQL Server с ноутбук IPython и другими средствами обработки и анализа данных toodo для случаев, когда база данных SQL можно указывать данные, используемые toostore hello.

После подготовленных настроенных, эти виртуальные машины будут готовы к использованию как ноутбук IPython серверов для просмотра hello и обработку данных и другие задачи, необходимые в сочетании с машинного обучения Azure и hello процесса обработки и анализа данных Team (TDSP). Hello следующим шагам в процессе обработки и анализа данных hello сопоставлены в hello [план обучения TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) и могут содержать действия, которые выполняют перемещение данных в SQL Server или HDInsight, обработки и образец он существует в процессе подготовки для обучения на основе hello данные с помощью Azure Машинное обучение.

> [!NOTE]
> За виртуальные машины Azure вы **платите только по факту использования**. tooensure, не выполняется выставлен счет, без использования виртуальной машины, он имеет toobe hello **остановлена (освобождена)** состояния из hello [классический портал Azure](http://manage.windowsazure.com/). Пошаговые инструкции или как toodeallocate вы виртуальной машины, в разделе [завершения работы и освободить виртуальную машину в случае использования](machine-learning-data-science-setup-virtual-machine.md#shutdown)
> 
> 

