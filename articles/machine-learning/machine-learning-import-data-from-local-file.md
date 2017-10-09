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
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a>Импорт данных для обучения из файла на жестком диске в Студию машинного обучения
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Узнайте, как файл tooupload данных из вашего toouse жесткого диска с именем обучающие данные хранятся в студии машинного обучения Azure. Путем импорта файла данных hello, имеется набор данных модуль готов к использованию в рабочей области.

## <a name="steps-tooimport-data-from-a-local-file"></a>Данные шаги tooimport из локального файла
Здравствуйте tooimport данных с локального жесткого диска, следующие:

1. Нажмите кнопку **+ создать** hello нижней части окна hello студии машинного обучения.
2. Выберите **Набор данных** и **From local file** (Из локального файла).
3. В hello **отправить новый набор данных** диалогового окна обзора toohello файл tooupload
4. Введите имя, укажите тип данных hello и при необходимости введите описание. Описание рекомендуется — позволяет toorecord все характеристики данных hello требуется tooremember при использовании данных hello в будущем hello.
5. Здравствуйте, флажок **это hello новой версии существующего набора данных** позволяет tooupdate существующий набор данных с новыми данными. Установите этот флажок, а затем введите имя hello существующего набора данных.

![Передача нового набора данных](media/machine-learning-import-data-from-local-file/upload-dataset.png)

Во время передачи появится сообщение о том, что файл передается. Отправить время зависит от размера hello быстродействия данных и hello toohello службы подключения. Если известно, что файл hello займет много времени, можно сделать прочего в студии машинного обучения, во время ожидания. Тем не менее закрытие обозревателя hello приводит toofail передачи данных hello.

## <a name="dataset-module-is-ready-for-use"></a>Модуль набора данных готов к использованию
После загрузки данных, он хранится в модуле набора данных и доступных tooany эксперимента в рабочей области.

При редактировании эксперимента можно найти hello наборы данных, созданные в hello **Мои наборы данных** списке hello **сохраненные наборы данных** списка в палитре модуля hello. Вы можно перетаскивать hello набора данных на холст эксперимента hello при необходимости toouse hello dataset для дальнейшего анализа и машинного обучения.
