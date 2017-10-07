---
title: "aaaUse образов клиента Windows в Azure | Документы Microsoft"
description: "Как toouse подписки Visual Studio использует преимущества toodeploy Windows 7, Windows 8 или Windows 10 в Azure для сценариев разработки и тестирования"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>Использование клиента Windows в Azure для сценариев разработки и тестирования
В сценариях разработки и тестирования Azure можно использовать Windows 7, Windows 8 или Windows 10 при условии, что у вас есть соответствующая подписка Visual Studio (прежнее название — MSDN). В этой статье рассматриваются требования hello. для работы клиента Windows Azure и использование hello образов коллекции Azure.

## <a name="subscription-eligibility"></a>Доступность в зависимости от подписки
Активные подписчики Visual Studio (пользователи, которые приобрели лицензию на подписку Visual Studio) могут использовать клиент Windows в целях разработки и тестирования. Вы можете использовать клиент Windows на собственном оборудовании и виртуальных машинах Azure, работающих в любом типе подписки Azure. Клиент Windows не может быть развернутой tooor используемого в Azure для использования в рабочей среде обычный, или пользователи, которые не являются действующими подписками Visual Studio.

Для вашего удобства мы внесли некоторые образы Windows 10 доступен из коллекции Azure hello в [предлагает подходящие для разработки и тестирования](#eligible-offers). Visual Studio, использующих любого типа предложения можно также [адекватно подготовки и создания](prepare-for-upload-vhd-image.md) 64-разрядный образ Windows 7, Windows 8 или Windows 10 и затем [отправить tooAzure](upload-generalized-managed.md). Использование Hello остается ограниченной toodev и тестирования с действующими подписками Visual Studio.

## <a name="eligible-offers"></a>Доступные предложения
Следующая таблица сведений hello Hello предлагают идентификаторам подходящих toodeploy Windows 10 через hello коллекции Azure. образы Hello Windows 10 — это только видимым toohello следующие предложения. Visual Studio, использующих, требуется клиент Windows toorun в типе другое предложение требует слишком[адекватно подготовки и создания](prepare-for-upload-vhd-image.md) 64-разрядный образ Windows 7, Windows 8 или Windows 10 и [затем отправьте tooAzure](upload-generalized-managed.md).

| Название предложения | Номер предложения | Доступные образы клиента |
|:--- |:---:|:---:|
| [Разработка и тестирование с оплатой по мере использования](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Подписчики Visual Studio Enterprise (MPN)](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Подписчики Visual Studio Professional](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Подписчики Visual Studio Test Professional](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium с подпиской MSDN (преимущество)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Подписчики Visual Studio Enterprise](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Подписчики Visual Studio Enterprise (BizSpark)](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Enterprise — разработка и тестирование](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>Проверка подписки Azure
Если вы не знаете Идентификатором предложения, его можно получить через hello портал Azure в одном из двух следующих способов:  

- В колонке «Подписки» hello:

  ![Подробные сведения о предложении идентификатор из hello портал Azure](./media/client-images/offer-id-azure-portal.png) 

- Или щелкните **Выставление счетов** и выберите свой идентификатор подписки. Идентификатор предложения Hello появляется в колонке hello выставления счетов.

Вы также можете просмотреть hello идентификатор предложения из hello [вкладки «Подписки»](http://account.windowsazure.com/Subscriptions) hello портала учетной записи Azure:

![Предоставляют подробные сведения о КОДЕ из портала учетной записи Azure hello](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a>Дальнейшие действия
Теперь вы можете развернуть виртуальные машины с помощью [PowerShell](quick-create-powershell.md), [шаблонов Resource Manager](ps-template.md) или [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

