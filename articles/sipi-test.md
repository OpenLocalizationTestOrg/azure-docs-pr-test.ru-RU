---
title: "Файл теста SIPI | Документы Microsoft"
description: "Тестовый файл, чтобы проверить ReadyForTest зависимости"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a>Файл SIPI теста

Из этого краткого руководства вы узнаете, как зарегистрировать приложение в клиенте Microsoft Azure Active Directory (Azure AD) B2C за несколько минут. Ознакомившись с этим руководством, вы зарегистрируете приложение для использования в клиенте Azure AD B2C.

## <a name="prerequisites"></a>Предварительные требования

Чтобы создать приложение с поддержкой регистрации и входа пользователей, его сначала нужно зарегистрировать с использованием клиента Azure Active Directory B2C. Получите собственный клиент, следуя указаниям в статье о [создании клиента Azure AD B2C](active-directory-b2c-get-started.md).

Управление приложениями, созданными в колонке Azure AD B2C на портале Azure, должно осуществляться в том же расположении. Если вы измените приложения B2C с помощью PowerShell или другого портала, их поддержка прекратится и они не будут работать с Azure AD B2C. Дополнительные сведения см. в разделе [Неисправные приложения](#faulted-apps). 

## <a name="navigate-to-b2c-settings"></a>Переход к параметрам B2C

Войдите на [портал Azure](https://portal.azure.com/) как глобальный администратор клиента B2C. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

Выберите следующие действия в зависимости от типа приложения, которое регистрируется:
