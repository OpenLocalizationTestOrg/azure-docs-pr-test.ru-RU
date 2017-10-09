---
title: "Общие сведения о aaaConceptual пользовательские имена доменов в Azure Active Directory | Документы Microsoft"
description: "Объясняет hello концептуальной структуры с помощью пользовательских доменных имен в Azure Active directory, включая федерации для единого входа"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fd0c5def-0da2-43af-81bc-76f4cfe86afd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 0a3454ae6b733a8a13a71925df3cc664063f388e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="conceptual-overview-of-custom-domain-names-in-azure-active-directory"></a>Общие сведения об именах личных доменов в Azure Active Directory
Доменное имя может выступать важным идентификатором для многих ресурсов каталога как часть:

* имени или адреса электронной почты пользователя;
* адрес Hello для группы
* приложение Hello URI идентификатора приложения

Ресурс в Azure Active Directory (Azure AD) может включать имя домена, которое уже проверена, что владельцем toobe hello каталог, содержащий ресурс hello. Задачи управления доменами в Azure AD может выполнять только глобальный администратор.

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье. Как toomanage домена имена в центре администрирования hello Azure AD, в разделе [управление пользовательские имена доменов в Azure Active Directory](active-directory-domains-manage-azure-portal.md).

Доменные имена в Azure AD являются глобально уникальными. Пользовательское доменное имя в отдельно взятый момент времени может использовать только один клиент Azure AD. Если один каталог Azure AD проверил доменное имя, то другие каталоги Azure AD не могут проверять или использовать это же доменное имя.

## <a name="initial-and-custom-domain-names"></a>Имена исходных и личных доменов
Каждое доменное имя в Azure AD является именем либо исходного домена, либо личного домена.

Каждый Azure AD включает исходное имя домена в форме contoso.onmicrosoft.com hello. Это третий доменного имени уровня, в этом примере «contoso.onmicrosoft.com», было установлено при hello каталог был создан, как правило, Здравствуйте, администратор, создавшего каталог hello. не удается изменить или удалить Hello исходное имя домена для каталога. Hello исходное имя домена, хотя полностью функциональны предназначен проверенную в основном toobe используется как механизм начальной загрузки, пока пользовательского имени домена.

В большинстве рабочих средах каталог имеет по крайней мере один проверенный пользовательский домен, например «contoso.com», и это этого пользовательского домена, который является видимым tooend пользователей. Имя личного домена — это доменное имя, например contoso.com, которое принадлежит организации и используется ею в таких целях, как размещение веб-сайта. Это имя домена предоставляется знакомый tooemployees, так как он является частью имени пользователя hello они использовать toosign в корпоративной сети toohello или toosend и получения сообщений электронной почты.

Прежде чем его можно использовать с Azure AD, hello настраиваемое имя домена должно быть добавлено tooyour каталогом и проверены.

## <a name="verified-and-unverified-domain-names"></a>Проверенные и непроверенные доменные имена
Hello исходное имя домена для каталога неявно оценивается как протестирован Azure AD. Когда администратор добавляет tooan имя пользовательского домена Azure AD, она изначально находится в состоянии не проверено. Azure AD не позволит любой каталог ресурсов toouse непроверенные доменное имя. Это гарантирует, что только один каталог можно использовать имя определенного домена и что hello организация использует имя домена hello фактически является владельцем этого имени домена.

Azure AD проверяет принадлежность имени домена путем поиска определенной записи в файл зоны службы DNS имя домена hello hello доменного имени. владение tooverify имени домена, администратор получает hello DNS-запись из Azure AD будет искать Azure AD и добавление этой записи toohello файла зоны DNS для имени домена hello. файл зоны DNS Hello поддерживается всеми hello регистратора доменных имен для этого домена. tooverify действия Hello домена отображаются hello статьи для [Добавление пользовательского домена каталога Azure AD tooyour](active-directory-add-domain.md).

Добавление файла зоны toohello запись DNS для имени домена hello не влияет на другие службы, например адрес электронной почты или веб-размещения.

## <a name="federated-and-managed-domain-names"></a>Федеративные и управляемые доменные имена
Имя пользовательского домена в Azure AD могут быть пользователи настроенных toogive федеративный вход взаимодействие между вашей локальной Active Directory и Azure AD. Настройка домена для федерации требуется обновляет tooprivileged ресурсы в Azure AD, а также tooyour Windows Server Active Directory. Настройку федеративного домена следует выполнять из Azure AD Connect или с помощью PowerShell. Невозможно инициировать федерацию пользовательского домена из hello классический портал Azure. [Просмотрите это видео toolearn о настройке службы федерации Active Directory для пользователя вход с помощью Azure AD Connect](http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect).

Домены, которые не являются федеративными, иногда называют управляемыми доменами. первоначальный домен Hello для каталога Azure AD, неявно вычисляется как управляемый домен.

## <a name="primary-domain-names"></a>Основные доменные имена
Hello основное имя домена для каталога — hello имя домена, выбранного ранее как значение по умолчанию hello для домена «hello» часть имени пользователя hello, когда администратор создает нового пользователя в hello [портал Azure](https://portal.azure.com/), или другого портала Например, портал администрирования Office 365 hello или портале Microsoft Intune hello. Каталог может иметь только одно основное доменное имя. Администратор может изменить toobe имя основного домена hello проверенный пользовательский домен, который не является федеративным, ни toohello исходного домена.

## <a name="domain-names-in-azure-ad-and-other-microsoft-online-services"></a>Доменные имена в Azure AD и других службах Microsoft Online Services
Доменное имя должно быть проверено в Azure AD, чтобы его могли использовать другие службы Microsoft Online Services, например Exchange Online, SharePoint Online и Intune. Записи DNS, которые зависят от конкретного toohello службы tooadd администратор обычно требуются следующие службы.

Веб-приложение Azure использует собственный механизм tooverify владения доменом. Домен должен быть проверен для использования со службой Azure AD, даже если он ранее был проверен для использования веб-приложением Azure в подписке, которая зависит от этой службы Azure AD. Веб-приложение Azure можно использовать имя домена, проверена в другой каталог из каталога hello, обеспечивающую безопасность hello веб-приложения.

## <a name="managing-domain-names"></a>Управление доменными именами
Задачи управления доменами можно выполнить из классического портала Azure hello и PowerShell. Многие задачи можно выполнить с помощью API Azure AD Graph hello.

* [Использование имен личных доменов для упрощения входа пользователей в систему](active-directory-add-domain.md)
* [Управление доменами в hello классический портал Azure](active-directory-add-manage-domain-names.md)
* [С помощью PowerShell toomanage доменных имен в Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [С помощью API Azure AD Graph hello toomanage доменных имен в Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

