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
# <a name="extend-your-experiment-with-r"></a>Расширение возможностей эксперимента с помощью R
Можно расширить функциональность hello студии машинного обучения Azure посредством языка hello R с помощью hello [выполнение скрипта R] [ execute-r-script] модуля.

Этот модуль принимает несколько входных наборов данных и выдает один выходной набор данных. Можно ввести сценарий R в hello **R-сценарий** параметр hello [выполнение скрипта R] [ execute-r-script] модуля.

Доступ к каждому входному порту hello модуль, используя код, аналогичный toohello следующий:

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a>Вывод списка всех установленных пакетов
Hello список установленных пакетов можно изменить. Список установленных пакетов см. в статье [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx) (Пакеты R, поддерживаемые в Машинном обучении Azure).

Список завершения, текущее hello установленных пакетов можно получить, введя следующий код в hello hello [выполнение скрипта R] [ execute-r-script] модуля:

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

Эта команда отправляет список hello пакеты toohello выходной порт hello [выполнение скрипта R] [ execute-r-script] модуля.
пакет hello tooview списка, такие как подключения модуля преобразования [преобразовать tooCSV] [ convert-to-csv] toohello слева выходные данные hello [выполнение скрипта R] [ execute-r-script]модуля, запустите эксперимент hello выберите выходной hello hello модуля преобразования и выберите **загрузить**. 

![Скачать выходные данные модуля «Преобразование tooCSV»](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a>Импорт пакетов
Можно импортировать пакеты, которые еще не установлены с помощью следующих команд в hello hello [выполнение скрипта R] [ execute-r-script] модуля:

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

Здравствуйте, где `my_favorite_package.zip` файл содержит пакет.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
