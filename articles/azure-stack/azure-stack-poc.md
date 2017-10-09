---
title: "aaaWhat — стек Azure? | Документация Майкрософт"
description: "Пакет разработчика Azure стек — это среда для оценки Azure стека функции и сценарии."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: helaw
ms.custom: mvc
ms.openlocfilehash: 3f7c84f2302a6411f49a07de171501fbd72812e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-stack"></a>Что такое Azure Stack?

Стека Microsoft Azure — это платформа гибридного облака, которая позволяет получать служб Azure из центра обработки данных вашей организации.  Стек Azure — спроектированный toohelp в основные сценарии, например соблюдения требований безопасности и соответствия требованиям, или когда нужен tooaccess ресурсы Azure без подключения к Интернету.  

## <a name="azure-stack-development-kit"></a>Набор разработки Azure Stack
Пакет средств разработки Microsoft Azure стек — это версия одного узла Azure стека, который затем можно использовать tooevaluate и получить дополнительные сведения о стеке Azure.  Также можно использовать пакет средств разработки стек Azure как среды разработки, можно было разрабатывать с помощью согласованные API-интерфейсы и средства.  

Следует учитывать эти точки с Azure стека Development Kit.

* Пакет разработчика Azure стека не должны использоваться в производственной среде и должен использоваться только для оценки, тестирования и демонстрации.  
* Развертывание стека Azure связана с одного поставщика удостоверений Azure Active Directory или служб федерации Active Directory. Можно создать несколько пользователей в этом каталоге и назначить пользователя tooeach подписки.
* Со всеми компонентами, развернуты на одном компьютере hello доступны только физические ресурсы для ресурсов клиента. Эта конфигурация не предназначен для оценки масштабирования и производительности.
* Сценарии сети ограничены из-за требований toohello одного узла или сетевого Адаптера.

## <a name="next-steps"></a>Дальнейшие действия
[Основные возможности и концепции](azure-stack-key-features.md)

[Инновации гибридных приложений с Azure и Azure стека (pdf)](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409)

