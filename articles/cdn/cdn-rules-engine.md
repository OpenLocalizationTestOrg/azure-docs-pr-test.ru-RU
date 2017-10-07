---
title: "Использование обработчика правил hello Azure CDN поведение aaaOverride HTTP | Документы Microsoft"
description: "Обработчик правил Hello позволяет toocustomize обработке HTTP-запросов Azure CDN, такие как блокировка доставки hello определенных типов содержимого и определить политику кэширования изменения заголовков HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a>Переопределить поведение HTTP с помощью модуля правил hello Azure CDN
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Обзор
Обработчик правил Hello позволяет toocustomize обработку HTTP-запросов, таких как блокировки доставки hello определенных типов содержимого, определяющий политику кэширования и изменение заголовков HTTP.  Этот учебник покажем, что создания правила, которые будут изменяться hello кэширование CDN активов.  Отсутствуют также видео-контента в hello»[см. также](#see-also)» раздела.

   > [!TIP] 
   > Синтаксис toohello ссылка подробно см [ссылку на модуль правил](cdn-rules-engine-reference.md).
   > 


## <a name="tutorial"></a>Учебник
1. В колонке профиля CDN hello выберите hello **управление** кнопки.
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    Открытие портала управления CDN Hello.
2. Щелкните hello **HTTP больших** пользовательская вкладка, **обработчик правил**.
   
    Появятся параметры для нового правила.
   
    ![Параметры нового правила CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > Hello порядок, в котором перечислены несколько правил влияет на способ обработки. Последующие правила могут переопределять hello действия, указанные с помощью предыдущего правила.
   > 
   > 
3. Введите имя в hello **имя и описание** текстового поля.
4. Укажите тип hello hello правила будут применяться к запросов.  По умолчанию hello **всегда** выбрано условие соответствия.  В этом учебнике будет использоваться условие **Всегда** , поэтому не изменяйте его.
   
   ![Условие соответствия CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > Существует много типов совпадения условия, доступные в раскрывающемся списке hello.  Щелкнув синий hello toohello информационный значок слева от условия соответствия hello объясняется, выбранного в данный момент hello условие подробно.
   > 
   >  Hello полный список условные выражения подробное описание см. в разделе [условного выражения правила ядра](cdn-rules-engine-reference-match-conditions.md).
   >  
   > Hello полный список условия совпадения подробное описание см. в разделе [условия соответствует обработчик правил](cdn-rules-engine-reference-match-conditions.md).
   > 
   > 
5. Нажмите кнопку hello  **+**  рядом слишком**функции** tooadd новую функцию.  В раскрывающемся списке hello hello слева, выберите **Force внутренней Max-Age**.  В появившемся текстовом hello введите **300**.  Оставьте hello, оставшиеся значения по умолчанию.
   
   ![Функция CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > Как с условиями соответствия, щелкнув синий hello toohello информационный значок слева от hello новые функции будут отображаться сведения об этой функции.  В случае hello **Force внутренней Max-Age**, мы переопределении hello активов **Cache-Control** и **Expires** toocontrol заголовки при hello CDN граничного узла будет обновлен hello ресурс из источника hello.  Наш пример 300 секунд означает, что hello CDN граничного узла будет кэшировать активов hello в течение 5 минут до обновления активов hello от начала координат.
   > 
   > Hello полный список компонентов подробно см. в разделе [подробные сведения о возможностях обработчик правил](cdn-rules-engine-reference-features.md).
   > 
   > 
6. Нажмите кнопку hello **добавить** кнопку toosave hello новое правило.  новое правило Hello теперь ожидает утверждения. После его утверждения hello состояние изменится с **ожидающие XML** слишком**Active XML**.
   
   > [!IMPORTANT]
   > Правила изменения может занять toopropagate минут too90 через hello CDN.
   > 
   > 

## <a name="see-also"></a>См. также
* [Обзор Azure CDN](cdn-overview.md)
* [Справочник по обработчику правил](cdn-rules-engine-reference.md)
* [Условия соответствия обработчика правил](cdn-rules-engine-reference-match-conditions.md)
* [Условные выражения обработчика правил](cdn-rules-engine-reference-conditional-expressions.md)
* [Функции обработчика правил](cdn-rules-engine-reference-features.md)
* [Переопределение поведения по умолчанию HTTP с помощью модуля правил hello](cdn-rules-engine.md)
* [Пятничный видеоролик об Azure. Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (Новые возможности Azure CDN уровня "Премиум")