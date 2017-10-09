---
title: "aaaPublish элемент пользовательского marketplace в стек Azure (оператор облака) | Документы Microsoft"
description: "Оператор облака Узнайте, как toopublish пользовательские marketplace элемента в стек Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 60871cbb-eed2-433c-a76d-d605c7aec06c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: e33e1c6574d43ada1c1c85bf77df7d0d191116aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-azure-stack-marketplace-overview"></a>Обзор Azure Marketplace стека Hello
Hello Marketplace — это совокупность служб, приложений и ресурсы, настроенные для стека Azure как сетей, виртуальных машин, хранилища и т. д. Пользователи приглашением toocreate новые ресурсы и разворачивать новые приложения. Трактовать как корзину каталога, где пользователям можно просмотреть и выбрать элементы hello, они выполнялись toouse. toouse элемент Marketplace, пользователям необходимо подписаться tooan предложение, которое предоставит им доступ toohello элемента.

В качестве оператор облака, решите, какие элементы tooadd toohello Marketplace (публикации). Вы можете опубликовать таких вещей, как базы данных, службы приложений и т. д. Это делает их видимыми tooall пользователей. Вы можете опубликовать создаваемые пользовательские элементы. Также можно опубликовать элементы рост [список элементов Azure Marketplace](azure-stack-marketplace-azure-items.md). При публикации элемента toohello Marketplace, пользователи могут видеть его в течение пяти минут.

Щелкните tooopen hello Marketplace, **New**.

![](media/azure-stack-publish-custom-marketplace-item/image1.png)

## <a name="marketplace-items"></a>Элементы Marketplace
Элемент стека Azure Marketplace — службы, приложения или ресурса, который пользователи могут загрузить и использовать. Все элементы стека Azure Marketplace являются видимыми tooall пользователей.

У каждого элемента Marketplace есть:

* Шаблон диспетчера ресурсов для подготовки ресурсов.
* Метаданные, например строки, значки и другие маркетинговые материалы.
* Форматирование элемента hello toodisplay сведения на портале hello

Каждый элемент опубликованного toohello Marketplace использует формат вызываемой hello пакет коллекции Azure (azpkg). Добавление ресурсов развертывания и среды выполнения (например, код ZIP-файлов с программным обеспечением и образы виртуальных машин) tooAzure стека отдельно, не являющийся частью hello Marketplace элемента. 

## <a name="next-steps"></a>Дальнейшие действия
[Создание и публикация элементов marketplace](azure-stack-create-and-publish-marketplace-item.md)

