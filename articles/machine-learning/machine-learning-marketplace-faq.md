---
title: "часто задаваемые вопросы — AAA(deprecated) публикации и использования машинного обучения приложений в Azure Marketplace | Документы Microsoft"
description: "(устарело) Часто задаваемые вопросы о публикации приложения hello Azure Marketplace машинного обучения"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a>(устарело) Публикация и использование приложений машинного обучения в Azure Marketplace hello: вопросы и ответы

> [!NOTE]
> Работа DataMarket и служб данных прекращается. Начиная с 31 марта 2017 г. имеющиеся подписки выводятся из эксплуатации и будут отменены. Поэтому мы не рекомендуем использовать эту статью. 
> 
> В качестве альтернативы можно опубликовать эксперименты в машинное обучение toohello [коллекции аналитики Cortana](https://gallery.cortanaintelligence.com/) преимущество hello сообщества обработки и анализа данных hello. Дополнительные сведения см. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).


## <a name="questions-about-consuming-from-marketplace"></a>Вопросы об использовании приложений из Marketplace
**1. Почему я получаю hello следующие сообщение об ошибке после ввода входных данных для hello веб-службы:**

**запрос Hello привела к серверной части времени ожидания или внутренней ошибки. Команда Hello изучает проблему hello. Приносим извинения за неудобства hello. (500)**

Ваш входные параметры могут не соответствовать требуемому формату toohello для hello конкретной веб-службы. Для входных параметров и ограничения веб-службу hello см toohello соответствующей документации toofind hello правильный формат ссылки.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. Если скопировать ссылку hello API для hello веб-службу, которая отображается на Здравствуйте, страница «Просмотр этого набора данных» и вставьте его в другом окне браузера, какие учетные данные, следует ли использовать результаты tooaccess hello и как я могу узнать их?**

Учетной записи Marketplace следует использовать как имя пользователя hello и hello первичный ключ учетной записи пароль hello. Hello первичный ключ учетной записи можно найти на hello **Просмотр этого набора данных** страницы в поле Описание hello hello веб-службы (щелкните hello **Показать** кнопка). результат Hello могут отображаться в браузере hello или он может находиться слишком загрузки, в зависимости от того, какой именно браузер используется.

**3. Почему я получаю hello следующие сообщение об ошибке после ввода hello входные данные для hello веб-службы на странице «Просмотр этого набора данных» hello:** 

**При обработке запроса произошла непредвиденная ошибка. Повторите попытку позже.**

Один или несколько входных параметров веб-службу превышена предельная длина hello при использовании веб-службу hello в hello marketplace **Просмотр этого набора данных** страницы. Hello службы могут вызываться в больше длины ввода с помощью методов HTTP POST. Примеры см. в разделе [образца решения с помощью R на машинного обучения и опубликованных tooMarketplace](machine-learning-r-csharp-web-service-examples.md).

**4. Почему я не вижу ничего в hello «ОБОЗРЕВАТЕЛЬ API» вкладку int hello хранилища в hello классический портал Azure?** 

Это известная проблема с hello Azure Marketplace классического портала. Hello работает команда tooresolve эту проблему. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>Вопросы о публикации с помощью веб-служб машинного обучения Azure в магазине Marketplace
**1. Почему в моей веб-службе не отражаются транзакции логотипов или изображений?** 

Эмблем и изображений, кэшируются в портал публикации hello и может пройти до too10 дней для hello новый логотип или tooupdate образа на портале hello.

**2. Почему — вкладка «Detail» hello мой веб-службы на рынке, отображается сообщение об ошибке?**

При подключении tooAzure машинного обучения для сведений о службе имеется известная проблема Marketplace. Hello работает команда tooresolve эту проблему.

**3. Почему hello примеры кода R в веб-службы машинного обучения Azure hello не работает для использования веб-сервисов hello в Marketplace?**

Hello системы проверки подлинности отличаются, сравнивая непосредственное подключение веб-службы машинного обучения tooAzure tooconnecting toothese веб-служб через hello Marketplace. службы Hello в Marketplace — это службы OData и их можно вызывать с помощью методов GET или POST. 

**4. Почему являются hello ссылки поддержки веб-служба и предлагает не обновляется правильно, для некоторых Мои предложения?**

Hello поддержки ссылки являются глобальными, на издателе, а не для предложения. 

**5. Как опубликовать в Marketplace веб-службу с пакетным режимом ввода?**

режим ввода пакета Hello в настоящее время не поддерживается в веб-службах Marketplace.

**6. Кто следует обращаться к справке tooget вопросом о том, как стать издателем данных, или если возникли проблемы во время публикации?**

Обращайтесь в службу Azure Marketplace hello в < mailto:datamarketbd@microsoft.com > для получения дополнительной информации.

