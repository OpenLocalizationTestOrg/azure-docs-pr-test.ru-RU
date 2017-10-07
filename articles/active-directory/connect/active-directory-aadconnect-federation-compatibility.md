---
title: "список совместимости федерации aaaAzure AD"
description: "Эта страница содержит сторонних поставщиков удостоверений, которые могут быть tooimplement используется единый вход."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 22c8693e-8915-446d-b383-27e9587988ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: ac2f9ad324c8ca6b587b73ea465426ad6b074b03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-federation-compatibility-list"></a>Список совместимости с федерацией Azure AD
Azure Active Directory предоставляет возможность единого входа и обеспечивает повышенную безопасность доступа к приложениям для Office 365 и других служб Microsoft Online Services для гибридных и исключительно облачных реализаций без использования стороннего решения. Набор Office 365, как и большинство служб Microsoft Online Services, интегрируется с Azure Active Directory для служб каталогов, проверки подлинности и авторизации. Azure Active Directory также предоставляет toothousands единого входа для приложений SaaS и локальных веб-приложений. См. в разделе hello коллекции приложений Azure Active Directory для поддерживаемых приложений SaaS.

Для организаций, которые были вложены в решения федерации не Майкрософт в этом разделе содержатся рекомендации по настройке единого входа для пользователей Windows Server Active Directory со службами Microsoft Online services с помощью сторонних поставщиков hello «Azure Active Directory federation совместимости списке» ниже. 

![](./media/active-directory-aadconnect-federation-compatibility/oxford2.jpg)   
Компания [Oxford Computer Group](http://oxfordcomputergroup.com/) (сторонний подрядчик) от имени корпорация Майкрософт тестировала интерфейсы единого входа с помощью сторонних поставщиков удостоверений в ряде сценариев использования, типичных для Azure Active Directory.

Для получения сведений о том, как добавить в этот список своего стороннего поставщика удостоверений, свяжитесь с Oxford Computer Group по адресу [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com).

> [!IMPORTANT]
> Группа компьютеров Оксфорд протестированы только hello функциональность федерации этих сценариев единого входа. Группа компьютеров Оксфорд не удалось выполнить тестирование hello синхронизации, двухфакторной проверки подлинности, и других компонентов этих сценариев единого входа.
> 
> Используется tooUPN альтернативного идентификатора входа в систему также не было проверено в этой программе.
> 
> 

* [Azure Active Directory](#azure-active-directory)
* [AuthAnvil Single Sign On 4.5](#authanvil-single-sign-on-45)
* [BIG-IP с Access Policy Manager BIG-IP версий 11.3x–11.6x](#big-ip-with-access-policy-manager-big-ip-ver-113x--116x) 
* [BitGlass](#bitglass)
* [CA Secure Cloud](#ca-secure-cloud) 
* [CA SiteMinder 12.52](#ca-siteminder-1252-sp1-cumulative-release-4) 
* [Centrify](#centrify) 
* [Dell One Identity Cloud Access Manager версии 7.1](#dell-one-identity-cloud-access-manager-v71) 
* [Составная аутентификация DigitalPersona](#digitalpersona-composite-authentication)
* [IBM Tivoli Federated Identity Manager 6.2.2](#ibm-tivoli-federated-identity-manager-622) 
* [IceWall Federation версии 3.0](#icewall-federation-version-30) 
* [Memority](#memority)
* [NetIQ Access Manager 4.x](#netiq-access-manager-4x) 
* [Okta](#okta) 
* [OneLogin](#onelogin) 
* [Службы федерации Optimal IDM Virtual Identity Server](#optimal-idm-virtual-identity-server-federation-services) 
* [PingFederate 6.11, 7.2, 8.x](#pingfederate-611-72-8x)
* [RadiantOne CFS 3.0](#radiantone-cfs-30) 
* [Sailpoint IdentityNow](#sailpoint-identitynow)
* [SecureAuth IdP 7.2.0](#secureauth-idp-720) 
* [Sign&go 5.3](#signgo-53) 
* [Шлюз веб-службы "Технология SoftBank"](#softbank)
* [Рабочая область 1 VMware](#vmware-workspace-one)



> [!IMPORTANT]
> Поскольку это сторонние продукты, корпорация Майкрософт не предоставляет поддержку для развертывания hello, конфигурации, устранению неполадок, рекомендациям, т. д. проблемы и вопросы, касающиеся этих поставщиков удостоверений. Для поддержки и по вопросам, касающимся этих поставщиков удостоверений обратитесь непосредственно к сторонним hello поддерживается.
> 
> Эти сторонние поставщики удостоверений тестировались на взаимодействие с облачными службами Майкрософт только с использованием протоколов WS-Federation и WS-Trust. Тестирование не включало использование протокола SAML hello.
> 


## <a name="azure-active-directory"></a>Azure Active Directory

Hello Далее приводится матрица поддержки сценария hello этот вход. 

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |None |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |
| Современные приложения, использующие ADAL, такие как Office 2016 |Поддерживаются |None |

Дополнительные сведения об использовании Azure Active Directory с AD FS см. в разделе [Настройка федерации с AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

Дополнительные сведения об использовании Azure Active Directory с синхронизацией паролей см. в статье [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).

## <a name="authanvil-single-sign-on-45"></a>AuthAnvil Single Sign On 4.5

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения см. на сайте AuthAnvil в [разделе, посвященном настройке единого входа](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-).


## <a name="big-ip-with-access-policy-manager-big-ip-ver-113x--116x"></a>BIG-IP с Access Policy Manager BIG-IP версий 11.3x–11.6x

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа: 

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Не поддерживается |Не поддерживается |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения о BIG-IP Access Policy Manager см. на сайте компании F5 Networks в разделе [BIG-IP Access Policy Manager](https://f5.com/products/modules/access-policy-manager). 

Инструкции BIG-IP Access Policy Manager hello tooconfigure hello tooyour интерфейса единого входа Active Directory-пользователи этого STS tooprovide скачиванию hello pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf).

## <a name="bitglass"></a>BitGlass

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения о BitGlass см. на веб-сайте [BitGlass](http://www.bitglass.com).

## <a name="ca-secure-cloud"></a>CA Secure Cloud

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения о CA Secure Cloud см. на [сайте компании CA](http://www.ca.com/us/products/security-as-a-service.aspx).

## <a name="ca-siteminder-1252-sp1-cumulative-release-4"></a>CA SiteMinder 12.52 с пакетом обновления 1 (SP1), накопительный выпуск 4

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа: 

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |None |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения о CA SiteMinder см. на [сайте компании CA](http://www.ca.com/us/products/ca-single-sign-on.html). 

## <a name="centrify"></a>Centrify

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |None |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |Контроль доступа клиентов не поддерживается. |

Дополнительные сведения о Centrify см. [на сайте Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp).

## <a name="dell-one-identity-cloud-access-manager-v71"></a>Dell One Identity Cloud Access Manager версии 7.1

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |None |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения о Dell One Identity Cloud Access Manager см. на сайте компании Dell в разделе [Cloud Access Manager](http://software.dell.com/products/cloud-access-manager).

 Инструкции hello tooconfigure hello tooyour интерфейса единого входа для пользователей Office 365 этот STS tooprovide в статье [настройки пользователей Office 365](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365). 

## <a name="digitalpersona-composite-authentication"></a>Составная аутентификация DigitalPersona  

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается.|
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается.|
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения см. в документе [DigitalPersona Composite Authentication](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf) (Составная аутентификация DigitalPersona).


## <a name="ibm-tivoli-federated-identity-manager-622"></a>IBM Tivoli Federated Identity Manager 6.2.2

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа: 

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |None |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения об IBM Tivoli Federated Identity Manager см. на сайте IBM в разделе, посвященном [IBM Security Access Manager для приложений Майкрософт](http://www-01.ibm.com/support/docview.wss?uid=swg24029517).

## <a name="icewall-federation-version-30"></a>IceWall Federation версии 3.0

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения об IceWall Federation см. на сайте компании HPE в разделах, посвященных [IceWall Federation версии 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) и [IceWall Federation с Office 365](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html).

## <a name="memority"></a>Memority

Hello Далее приводится матрица поддержки сценария hello этот вход. 

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |None |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения об использовании Memority см. на веб-сайте [Memority](http://www.memority.com).


## <a name="netiq-access-manager-4x"></a>NetIQ Access Manager 4.x

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None|
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |None|
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения о NetIQ Access Manager см. в [соответствующем разделе на сайте NetIQ](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m).

## <a name="okta"></a>Okta

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа: 

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |Для встроенной проверки подлинности Windows требуется настройка дополнительного веб-сервера и приложения Okta. |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения об Okta см. на веб-сайте [Okta](https://www.okta.com/).

## <a name="onelogin"></a>OneLogin

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа: 

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |Встроенная проверка подлинности Windows |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения об OneLogin см. на веб-сайте [OneLogin](https://www.onelogin.com/).

## <a name="optimal-idm-virtual-identity-server-federation-services"></a>Службы федерации Optimal IDM Virtual Identity Server

следующие Hello hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |

Дополнительные сведения о клиенте политики доступа см. в разделе [tooOffice ограничение доступа 365 Services основании hello расположение hello клиента](https://technet.microsoft.com/library/hh526961.aspx).





## <a name="pingfederate-611-72-8x"></a>PingFederate 6.11, 7.2, 8.x

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |None |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Для инструкции PingFederate hello как tooconfigure этот STS tooprovide hello единым входом возникают tooyour пользователей Active Directory, см. ниже hello: 

- [PingFederate 6.11](http://go.microsoft.com/fwlink/?LinkID=266321)
- [PingFederate 7.2](http://documentation.pingidentity.com/display/PF72/PingFederate+7.2)
- [PingFederate 8.x](http://documentation.pingidentity.com/display/PFS/SSO+to+Office+365+Introduction)

## <a name="radiantone-cfs-30"></a>RadiantOne CFS 3.0

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа: 

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения о RadiantOne CFS см. [в соответствующем разделе](http://www.radiantlogic.com/products/radiantone-cfs/) веб-сайта компании Radiant Logic .

## <a name="sailpoint-identitynow"></a>Sailpoint IdentityNow

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения о Sailpoint IdentityNow см. [в соответствующем разделе](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/) веб-сайта компании Sailpoint.

## <a name="secureauth-idp-720"></a>SecureAuth IdP 7.2.0

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа: 

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |None |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |None |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения о SecureAuth см. на [сайте компании SecureAuth](http://go.microsoft.com/?linkid=9845293).














## <a name="signgo-53"></a>Sign&go 5.3

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |Поддерживаются контракты Kerberos |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |None |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Sign&go 5.3 поддерживает проверку подлинности Kerberos в конфигурации контракта Kerberos.  Для получения помощи по этой конфигурации, обратитесь к Ilex или представления руководство по установке hello [Sign & go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)

## <a name="softbank-technology-online-service-gate"></a>Шлюз веб-службы "Технология SoftBank"

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения о шлюзе веб-службы "Технология SoftBank" см. на веб-сайте [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)

## <a name="vmware-workspace-one"></a>Рабочая область 1 VMware

Hello Вот hello Матрица поддержки сценария данного интерфейса единого входа:

| Клиент | Поддержка | Исключения |
| --- | --- | --- |
| Веб-клиенты, такие как Exchange Web Access и SharePoint Online |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные клиентские приложения, такие как Lync, подписка Office Subscription, CRM |Поддерживаются |Встроенная проверка подлинности Windows не поддерживается. |
| Полнофункциональные почтовые клиенты, такие как Outlook и ActiveSync |Поддерживаются |None |

Дополнительные сведения см. в документе [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf)

