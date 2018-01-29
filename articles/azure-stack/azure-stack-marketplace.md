---
title: "Публикация настраиваемого элемента Marketplace в Azure Stack (для оператора облака) | Документация Майкрософт"
description: "Сведения о том, как оператор Azure Stack может опубликовать настраиваемый элемент Marketplace в Azure Stack."
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
ms.openlocfilehash: 7b5f976eb2d51eb86761a2bd0be6adb45ca87681
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="the-azure-stack-marketplace-overview"></a>Общие сведения об Azure Stack Marketplace

*Область применения: интегрированные системы Azure Stack и пакет средств разработки Azure Stack*

Marketplace — это коллекция служб, приложений и ресурсов, настроенных для Azure Stack, таких как сети, виртуальные машины, хранилище и т. д. Здесь пользователи создают новые ресурсы и развертывают новые приложения. Это место можно рассматривать как каталог товаров, который пользователи просматривают, выбирая элементы для использования. Чтобы использовать элемент Marketplace, пользователям необходимо подписаться на предложение, которое предоставит им доступ к элементу.

Как оператор Azure Stack вы определяете, какие элементы следует добавить (опубликовать) в Marketplace. Опубликовать можно, например, базы данных, службы приложений и т. д. Это сделает их видимыми для всех пользователей. Вы можете опубликовать настраиваемые элементы, которые вы создали. Также можно опубликовать элементы из постоянно растущего [списка элементов Azure Marketplace](azure-stack-marketplace-azure-items.md). После публикации элемента в Marketplace он станет видимым для пользователей в течение пяти минут.

Чтобы открыть на Marketplace, щелкните **New**(Создать).

![](media/azure-stack-publish-custom-marketplace-item/image1.png)

## <a name="marketplace-items"></a>Элементы Marketplace
Элемент Azure Stack Marketplace — это служба, приложение или ресурс, которые пользователи могут скачать и использовать. Все элементы Azure Stack Marketplace видны всем вашим пользователям.

У каждого элемента Marketplace есть:

* Шаблон диспетчера ресурсов для подготовки ресурсов.
* Метаданные, например строки, значки и другие маркетинговые материалы.
* Форматирование сведений для отображения элемента на портале

Каждый элемент, опубликованный в Marketplace, использует формат пакета коллекции Azure (AZPKG). Ресурсы развертывания или среды выполнения (например, код, ZIP-файлы с программным обеспечением или образы виртуальных машин) следует добавлять в Azure Stack отдельно, а не в составе элемента Marketplace. 

## <a name="next-steps"></a>Дальнейшие действия
[Создание и публикация элемента Marketplace](azure-stack-create-and-publish-marketplace-item.md)

