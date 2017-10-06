---
title: "aaaAccess хранилище ключей брандмауэром | Документы Microsoft"
description: "Узнайте, как tooaccess Azure ключ хранилища из приложения за брандмауэром"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: ab4bb0c27a41fef878a20dace6cab203df04e579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>Доступ к хранилищу ключей Azure из-за брандмауэра
### <a name="q-my-key-vault-client-application-needs-toobe-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-tooenable-access-tooa-key-vault"></a>Вопрос. у моего хранилища ключей клиентскому приложению требуется toobe за брандмауэром. Какие порты, узлов или IP-адреса необходимо открыть хранилище ключей tooa доступа tooenable?
tooaccess хранилища ключей хранилища ключей клиентское приложение имеет tooaccess несколько конечных точек для различных функций:

* Проверка подлинности с помощью Azure Active Directory (Azure AD).
* Управление хранилищем ключей Azure. Это включает в себя создание, чтение, обновление, удаление и настройку политик доступа с помощью Azure Resource Manager.
* Доступа и управления объектами (ключи и секретные коды) хранится в хранилище ключей сам, проходящий через hello конечной точки зависящие от ключа хранилища (например, [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).  

Требования отличаются в зависимости от конфигурации и среды.   

## <a name="ports"></a>порты;
Все трафика tooa хранилища ключей для всех трех функций (проверки подлинности, управления и данных плоскости доступ) переходит по протоколу HTTPS: порт 443. Однако для списка отзыва сертификатов время от времени трафик будет поступать через HTTP (порт 80). Клиентам, поддерживающим протокол OCSP, не следует обращаться к списку отзыва сертификатов. Иногда они могут перейти по ссылке [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl).  

## <a name="authentication"></a>Аутентификация
Хранилище ключей клиентские приложения потребуется tooaccess конечные точки Azure Active Directory для проверки подлинности. Hello конечная точка, используемая зависит hello конфигурации клиента Azure AD, типа hello участника (участника-пользователя или субъекта-службы) и hello тип учетной записи — например, учетную запись Майкрософт или рабочей или учебной учетной записи.  

| Тип субъекта | Конечная точка и порт |
| --- | --- |
| Пользователь, использующий учетную запись Майкрософт<br> (например, user@hotmail.com) |**Глобально:**<br> login.microsoftonline.com:443<br><br> **Azure для Китая:**<br> login.chinacloudapi.cn:443<br><br>**Azure для правительства США:**<br> login-us.microsoftonline.com:443<br><br>**Azure для Германии:**<br> login.microsoftonline.de:443<br><br> и <br>login.live.com:443 |
| Пользователя или участника службы с помощью рабочей или учебной учетной записи в Azure AD (например, user@contoso.com) |**Глобально:**<br> login.microsoftonline.com:443<br><br> **Azure для Китая:**<br> login.chinacloudapi.cn:443<br><br>**Azure для правительства США:**<br> login-us.microsoftonline.com:443<br><br>**Azure для Германии:**<br> login.microsoftonline.de:443 |
| Пользователя или участника службы с помощью рабочей или рабочую учетную запись, а также служб федерации Active Directory (AD FS) или других федеративной конечной точки (например, user@contoso.com) |Все конечные точки для рабочей или учебной учетной записи, а также службы федерации Active Directory или другие федеративные конечные точки |

Есть и другие возможные сложные сценарии. См. слишком[Active Directory аутентификации Azure](/documentation/articles/active-directory-authentication-scenarios/), [интеграция приложений с Azure Active Directory](/documentation/articles/active-directory-integrating-applications/), и [протоколы проверки подлинности Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) Для получения дополнительных сведений.  

## <a name="key-vault-management"></a>Управление хранилищем ключей
Для управления хранилищем ключей (CRUD и настройка политики доступа) клиентское приложение hello хранилища ключей должен tooaccess конечную точку диспетчера ресурсов Azure.  

| Тип операции | Конечная точка и порт |
| --- | --- |
| Операции уровня управления хранилищем ключей<br> с использованием Azure Resource Manager |**Глобально:**<br> management.azure.com:443<br><br> **Azure для Китая:**<br> management.chinacloudapi.cn:443<br><br> **Azure для правительства США:**<br> management.usgovcloudapi.net:443<br><br> **Azure для Германии:**<br> management.microsoftazure.de:443 |
| API Graph Azure Active Directory |**Глобально:**<br> graph.windows.net:443<br><br> **Azure для Китая:**<br> graph.chinacloudapi.cn:443<br><br> **Azure для правительства США:**<br> graph.windows.net:443<br><br> **Azure для Германии:**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>Операции с хранилищем ключей
Для всех объектов (ключи и секретные коды) Управление хранилищем ключей и криптографических операций hello хранилища ключей клиент должен tooaccess hello хранилища ключей, конечной точки. DNS-суффикс конечной точки Hello зависит от расположения hello хранилища ключей. Конечная точка хранилища ключей Hello имеет формат hello *имя хранилища*. *область —-dns суффикс*, как описано в следующей таблице hello.  

| Тип операции | Конечная точка и порт |
| --- | --- |
| Операции, в том числе криптографические операции для ключей; создание, чтение, обновление и удаление ключей и секретов; задание или получение тегов и других атрибутов для объектов хранилища ключей (ключи и секреты) |**Глобально:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure для Китая:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure для правительства США:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure для Германии:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>Диапазоны IP-адресов
Hello службы хранилища ключей использует другие ресурсы Azure, например PaaS инфраструктуры. Поэтому нет возможности tooprovide определенного диапазона IP-адресов, хранилище ключей, будут иметь конечные точки службы в определенный момент времени. Если брандмауэр поддерживает только диапазоны IP-адресов, см. toohello [диапазоны IP-адресов Microsoft Azure Datacenter](https://www.microsoft.com/download/details.aspx?id=41653) документа. Для проверки подлинности и удостоверение (Azure Active Directory), приложение должно быть toohello может tooconnect конечные точки, описанной в [проверка подлинности и удостоверение адреса](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="next-steps"></a>Дальнейшие действия
Если у вас есть вопросы о хранилище ключей, посетите hello [форумы хранилище ключей Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

