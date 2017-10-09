---
title: "aaaExcel-надстройка для служб веб-машины обучения | Документы Microsoft"
description: "Как toouse Azure Machine Learning Web services непосредственно в Microsoft Excel без написания кода."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a>Надстройка Excel для веб-служб машинного обучения Azure
Excel позволяет легко toocall веб-службы непосредственно без hello требуется toowrite любого кода.

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a>TooUse действия с существующие веб-службой в hello книги

1. Откройте hello [образец файла Excel](http://aka.ms/amlexcel-sample-2), содержащий hello надстройки и данные о пассажиров на hello Titanic.
2. Выберите веб-службу hello, щелкнув его-«Titanic выживших прогнозирования (пример надстройки Excel) [Оценка]» в этом примере.
   
    ![Выберите веб-службу][01]
3. После этого вы перейдете toohello **Predict** раздела.  Эта книга уже содержит образцы данных. В пустой книге можно выбрать ячейку в Excel и щелкнуть **Use sample data** (Использовать образцы данных).
4. Выберите данные hello с заголовками и щелкните значок диапазона hello входных данных.  Убедитесь, что поле «Мои данные содержат заголовки» hello.
5. В разделе **вывода**, введите номер ячейки hello, в котором требуется hello toobe выходных данных, например «H1» ниже.
6. Нажмите **Выполнить прогноз**.
   
    ![Раздел «Прогноз»][02]

Разверните новую веб-службу или используйте уже существующую. Дополнительные сведения о развертывании веб-службы см. в разделе [шаг 5 пошагового руководства: развертывание службы Azure Machine Learning Web hello](machine-learning-walkthrough-5-publish-web-service.md).

Получите ключ API hello веб-службы. Источник получения ключа зависит от способа публикации: как классическая или как новая веб-служба машинного обучения.

**Использование классической веб-службы** 

1. В студии машинного обучения, щелкните hello **веб-службы** статьи hello левой панели, а затем выберите hello веб-службы.
   
    ![Выбор веб-службы в студии машинного обучения][04]
2. Скопируйте ключ API hello hello веб-службы.
   
    ![Ключ API в Студии машинного обучения][05]
3. На hello **МОНИТОРИНГА** hello веб-службы, нажмите кнопку hello **запрос-ОТВЕТ** ссылку.
4. Найдите hello **URI запроса** раздела.  Скопируйте и сохраните URL-адрес hello.

> [!NOTE]
> Теперь стало возможно toosign в hello [веб-службы Azure Machine Learning](https://services.azureml.net) tooobtain портала ключ hello API веб-службы классический машинного обучения.
> 
> 

**Использование новой веб-службы**

1. В hello [веб-службы Azure Machine Learning](https://services.azureml.net) портала, нажмите кнопку **веб-служб**, затем выберите веб-службу. 
2. Щелкните **Consume**(Использование).
3. Найдите hello **потребления основные сведения о** раздела. Скопируйте и сохраните hello **первичного ключа** и hello **запрос-ответ** URL-адрес.

## <a name="steps-tooadd-a-new-web-service"></a>Действия tooAdd веб-службу

1. Разверните новую веб-службу или используйте уже существующую. Дополнительные сведения о развертывании веб-службы см. в разделе [шаг 5 пошагового руководства: развертывание службы Azure Machine Learning Web hello](machine-learning-walkthrough-5-publish-web-service.md).
2. Щелкните **Consume**(Использование).
3. Найдите hello **потребления основные сведения о** раздела. Скопируйте и сохраните hello **первичного ключа** и hello **запрос-ответ** URL-адрес.
4. В Excel, выберите toohello **веб-службы** раздела (в hello **Predict** щелкните стрелку Назад hello toogo список toohello веб-службы).
   
    ![Выбор службы tooWeb перейти][03]
5. Щелкните **Добавить веб-службу**.
6. Вставьте URL-адрес hello в Excel, добавьте в текстовое поле с меткой hello **URL-адрес**.
7. Вставьте ключ API-источник hello в hello текстовое поле с меткой **ключ API**.
8. Щелкните **Добавить**.
   
    ![URL-адрес и ключ API для классической веб-службы.][06]
9. toouse hello веб-службы, следуйте предшествующий направлениях hello, «Шаги tooUse существующая web Service.»

## <a name="sharing-your-workbook"></a>Предоставление общего доступа к книге
При сохранении книги также сохранить ключ API-источник hello hello веб-служб, которые были добавлены. Это означает, что совместно использовать hello книги следует только с тех пользователей, которым вы доверяете.

Вопросы в hello следующий раздел комментарий или на нашем [форум](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
