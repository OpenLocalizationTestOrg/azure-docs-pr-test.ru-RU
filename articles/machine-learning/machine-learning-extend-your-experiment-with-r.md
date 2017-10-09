---
title: "aaaExtend эксперимента с помощью R | Документы Microsoft"
description: "Как tooextend hello функциональность студии машинного обучения Azure посредством языка hello R с помощью модуля выполнение скрипта R hello."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="88b5e-103">Расширение возможностей эксперимента с помощью R</span><span class="sxs-lookup"><span data-stu-id="88b5e-103">Extend your experiment with R</span></span>
<span data-ttu-id="88b5e-104">Можно расширить функциональность hello студии машинного обучения Azure посредством языка hello R с помощью hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="88b5e-104">You can extend hello functionality of Azure Machine Learning Studio through hello R language by using hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="88b5e-105">Этот модуль принимает несколько входных наборов данных и выдает один выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="88b5e-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="88b5e-106">Можно ввести сценарий R в hello **R-сценарий** параметр hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="88b5e-106">You can type an R script into hello **R Script** parameter of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="88b5e-107">Доступ к каждому входному порту hello модуль, используя код, аналогичный toohello следующий:</span><span class="sxs-lookup"><span data-stu-id="88b5e-107">You access each input port of hello module by using code similar toohello following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="88b5e-108">Вывод списка всех установленных пакетов</span><span class="sxs-lookup"><span data-stu-id="88b5e-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="88b5e-109">Hello список установленных пакетов можно изменить.</span><span class="sxs-lookup"><span data-stu-id="88b5e-109">hello list of installed packages can change.</span></span> <span data-ttu-id="88b5e-110">Список установленных пакетов см. в статье [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx) (Пакеты R, поддерживаемые в Машинном обучении Azure).</span><span class="sxs-lookup"><span data-stu-id="88b5e-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="88b5e-111">Список завершения, текущее hello установленных пакетов можно получить, введя следующий код в hello hello [выполнение скрипта R] [ execute-r-script] модуля:</span><span class="sxs-lookup"><span data-stu-id="88b5e-111">You also can get hello complete, current list of installed packages by entering hello following code into hello [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="88b5e-112">Эта команда отправляет список hello пакеты toohello выходной порт hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="88b5e-112">This sends hello list of packages toohello output port of hello [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="88b5e-113">пакет hello tooview списка, такие как подключения модуля преобразования [преобразовать tooCSV] [ convert-to-csv] toohello слева выходные данные hello [выполнение скрипта R] [ execute-r-script]модуля, запустите эксперимент hello выберите выходной hello hello модуля преобразования и выберите **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="88b5e-113">tooview hello package list, connect a conversion module such as [Convert tooCSV][convert-to-csv] toohello left output of hello [Execute R Script][execute-r-script] module, run hello experiment, then click hello output of hello conversion module and select **Download**.</span></span> 

![Скачать выходные данные модуля «Преобразование tooCSV»](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="88b5e-115">Импорт пакетов</span><span class="sxs-lookup"><span data-stu-id="88b5e-115">Importing packages</span></span>
<span data-ttu-id="88b5e-116">Можно импортировать пакеты, которые еще не установлены с помощью следующих команд в hello hello [выполнение скрипта R] [ execute-r-script] модуля:</span><span class="sxs-lookup"><span data-stu-id="88b5e-116">You can import packages that are not already installed by using hello following commands in hello [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="88b5e-117">Здравствуйте, где `my_favorite_package.zip` файл содержит пакет.</span><span class="sxs-lookup"><span data-stu-id="88b5e-117">where hello `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
