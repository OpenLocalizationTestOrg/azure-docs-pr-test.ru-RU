---
title: "хэш-алгоритм подписи aaaChange для доверия с проверяющей стороной Office 365 | Документы Microsoft"
description: "Эта страница содержит рекомендации по изменению алгоритма SHA для доверия федерации с Office 365"
keywords: "SHA1,SHA256,O365,федерация,aadconnect,adfs,ad fs,изменение sha,доверие федерации,отношение доверия с проверяющей стороной"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a>Изменение хэш-алгоритма подписи для отношения доверия с проверяющей стороной Office 365
## <a name="overview"></a>Обзор
Службы федерации Active Directory (AD FS) подписывает его tooensure Azure Active Directory tooMicrosoft маркеры, они не подделаны. Подпись основывается на алгоритме SHA1 или SHA256. Azure Active Directory теперь поддерживает маркеров, подписанных с помощью алгоритма SHA256, а рекомендуется задать для подписи токена алгоритм tooSHA256 hello для hello высокого уровня безопасности. В этой статье описывается hello необходимости toohello алгоритм подписи маркера hello tooset более безопасный уровень SHA256.

>[!NOTE]
>Корпорация Майкрософт рекомендует использование SHA256 hello-алгоритма для подписи маркеров, как это более безопасно, чем SHA1, но SHA1 по-прежнему остается поддерживаемый параметр.

## <a name="change-hello-token-signing-algorithm"></a>Измените алгоритм подписи маркера hello
После выбора алгоритма подписи hello с одним hello две следующие процедуры, службы федерации Active Directory подписывает маркеры hello для Office 365 с проверяющей стороной с помощью SHA256. Не требуется toomake изменения дополнительные конфигурации, а это изменение не оказывает влияния на вашей возможности tooaccess Office 365 или другие приложения Azure AD.

### <a name="ad-fs-management-console"></a>Консоль управления AD FS
1. Откройте консоль управления hello AD FS на сервере hello основной AD FS.
2. Разверните узел hello AD FS и щелкните **доверия с проверяющей стороной**.
3. Щелкните правой кнопкой мыши нужный объект отношений доверия с проверяющей стороной Office 365 или Azure и выберите пункт **Свойства**.
4. Выберите hello **Дополнительно** вкладку и выберите hello безопасного хэш-алгоритм SHA256.
5. Нажмите кнопку **ОК**.

![Алгоритм подписи SHA256 — MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a>Командлеты AD FS PowerShell
1. На любом сервере AD FS откройте PowerShell с правами администратора.
2. Набор hello безопасного хэш-алгоритм с помощью hello **AdfsRelyingPartyTrust набор** командлета.
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a>Также ознакомьтесь
* [Управление службами федерации Active Directory и их настройка с помощью Azure AD Connect](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

