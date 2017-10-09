---
title: "время существования маркера hello aaaHow toochange по умолчанию для приложения, разработанного | Документы Microsoft"
description: "Как политики tooupdate время существования маркера для приложения, которое вы разрабатываете в Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a>Как время существования маркера hello toochange по умолчанию для приложения, разработанного

Azure AD Premium позволяет разработчикам приложений и клиента администраторов tooconfigure hello временем существования маркеры, выпущенные для конфиденциальные клиентов. Время существования маркера политики задаются на уровне клиента или hello ресурсов, к которому выполняется доступ.

 * tooset политику времени существования маркера необходимо toodownload hello [модуля Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview).

 * Запустите hello **Connect AzureAD-Подтверждение** команды.

 * Ниже приведен пример политики, задает токен обновления дисперсионный max-age hello. Создайте политику hello.```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * Извлечение hello [время существования маркера Настройка](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) документа как toolearn toocreate другие пользовательские.

## <a name="next-steps"></a>Дальнейшие действия
[Настройка времени существования токенов](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Справочник по токенам в Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

