---
title: "toouse aaaHow Blitline для обработки изображений - функция руководство по Azure"
description: "Узнайте, как toouse hello Blitline обслуживания образов tooprocess приложении Azure."
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a>Как toouse Blitline с Azure и хранилища Azure
В этом руководстве объясняется, как tooaccess Blitline службы и как toosubmit заданий tooBlitline.

## <a name="what-is-blitline"></a>Что такое Blitline?
Blitline является служба, которая обеспечивает обработку образа на уровне предприятия в малую долю hello цену, что он будет стоить toobuild обработки изображений на основе облака его самостоятельно.

факт Hello является, что обработка изображений выполняются снова и снова, обычно перестроен с нуля hello для каждого веб-сайта. Мы понимаем это, так как сами множество раз делали это. Однажды мы решили, что пора создать универсальное решение. Мы знаем, как toodo его toodo он быстро и эффективно и сохраните все работать в hello это время.

Дополнительные сведения см. на веб-сайте [http://www.blitline.com](http://www.blitline.com).

## <a name="what-blitline-is-not"></a>Чем Blitline НЕ является...
tooclarify что Blitline полезно для — часто проще tooidentify Blitline не возможности перед продолжением.

* Blitline не поддерживает изображения tooupload мини-приложений HTML. Необходимо иметь изображений, доступных публично или с ограниченными разрешениями для Blitline tooreach.
* Blitline НЕ поддерживает функции динамической обработки изображений, аналогичных Aviary.com.
* Blitline не поддерживает отправку изображений, невозможно принудительно вашей tooBlitline изображения непосредственно. Необходимо отправить их tooAzure хранилища или других местах, который поддерживает Blitline и затем укажите, где toogo получить их Blitline.
* Blitline использует массовый параллелизм и НЕ выполняет синхронную обработку. То есть вы должны предоставить нам URL-адрес обратной передачи postback_url, чтобы мы могли сообщить, когда обработка завершена.

## <a name="create-a-blitline-account"></a>Создание учетной записи Blitline
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a>Как toocreate Blitline задания
Blitline использует JSON toodefine hello действия должны tootake на изображении. Эта JSON состоит из нескольких простых полей.

Простейший пример Hello выглядит следующим образом:

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

Здесь у нас есть JSON, которое займет изображения «src»»... boys.jpeg», а затем увеличить too240x140 этого образа.

Идентификатор приложения Hello-то можно найти в вашей **сведений о СОЕДИНЕНИИ** или **УПРАВЛЕНИЕ** вкладку в Azure. Это ваш идентификатор секрета, который позволяет toorun заданий на Blitline.

Привет, параметр «Сохранить» определяет сведения о нужное изображение hello tooput после мы еще обрабатываются. В этом простейшем случае такое расположение не задано. Если расположение не определено, Blitline сохраняет изображение локально (и временно) в уникальном расположении в облаке. Можно будет tooget, откуда hello JSON, возвращенные функцией Blitline при внесении hello Blitline. Идентификатор Hello «изображения» является обязательным и возвращается tooyou при tooidentify данного конкретного сохранении изображения.

Можно найти дополнительные сведения о hello *функции* мы поддерживаем здесь: <http://www.blitline.com/docs/functions>

Также можно найти документацию по hello здесь параметры задания: <http://www.blitline.com/docs/api>

При наличии JSON является все, что нужно toodo **POST** он слишком`http://api.blitline.com/job`

Обратно возвращается JSON следующего вида:

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


Это означает, что запрос получен Blitline, он помещена в очередь обработки, а после ее завершения hello изображения можно найти по адресу: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_приложения\_идентификатор /CK3f0xBF_2bV6wf7gEZE8w.jpg**

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a>Как toosave tooyour изображения учетной записи хранилища Azure
Если у вас есть учетная запись хранилища Azure, легко может иметь Blitline принудительной hello обработки изображений в контейнер Azure. Путем добавления «azure_destination» определяют расположение hello и разрешения для toopush Blitline для.

Пример:

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


Заполнив hello CAPITALIZED значения собственными, вы можете отправить этот toohttp://api.blitline.com/job JSON и hello «src» образ будет обрабатываться с помощью фильтра размытия и затем помещаются tooyou Azure назначения.

### <a name="please-note"></a>Обратите внимание на следующее:
Hello SAS должен содержать hello весь URL-адрес SAS, включая имя файла hello hello конечный файл.

Пример:

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


Также может считывать hello последний выпуск docs хранилища Azure Blitline [здесь](http://www.blitline.com/docs/azure_storage).

## <a name="next-steps"></a>Дальнейшие действия
Посетите tooread blitline.com о нашем остальные функции:

* Документы о конечных точках API Blitline: <http://www.blitline.com/docs/api>.
* Функции API Blitline: <http://www.blitline.com/docs/functions>.
* Примеры API Blitline: <http://www.blitline.com/docs/examples>.
* Библиотека Nuget стороннего поставщика: <http://nuget.org/packages/Blitline.Net>.

