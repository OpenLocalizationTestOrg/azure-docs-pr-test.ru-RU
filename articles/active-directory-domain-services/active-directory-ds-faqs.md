---
title: "aaaFAQs - доменных служб Active Directory Azure | Документы Microsoft"
description: "Часто задаваемые вопросы о доменных службах Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 42a6d659f6408bf694cb2aa6ec24bff7a76b0565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Доменные службы Azure Active Directory: часто задаваемые вопросы
Эта страница ответы на часто задаваемые вопросы о hello доменных служб Active Directory Azure. Следите за обновлениями.

### <a name="troubleshooting-guide"></a>Руководство по устранению неполадок
См. tooour [руководство по устранению неполадок](active-directory-ds-troubleshooting.md) для решения toocommon проблемы при администрировании доменные службы Azure AD и настройке.

### <a name="configuration"></a>Конфигурация
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>Можно ли создать несколько доменов для одного каталога Azure AD?
Нет. Для одного каталога Azure AD можно создать только один домен, поддерживаемый доменными службами Azure AD.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>Можно ли включить доменные службы Azure AD в виртуальной сети Azure Resource Manager?
Нет. Доменные службы Azure AD можно включить только в классической виртуальной сети Azure. Можно подключить hello классической виртуальной сети tooa диспетчера ресурсов виртуальной сети с помощью виртуальной сети пиринга toouse управляемого домена в виртуальной сети диспетчер ресурсов.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-tooauthenticate-users-for-access-toooffice-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>Можно ли включить доменные службы Azure AD в федеративном каталоге Azure AD? Я использую tooauthenticate пользователей служб федерации Active Directory для доступа к tooOffice 365. Можно включить доменные службы Azure AD для этого каталога?
Нет. Доменные службы Azure AD требуется получить доступ к toohello хэши паролей учетных записей пользователей, tooauthenticate пользователей с помощью NTLM или Kerberos. В федеративной каталога хэшей паролей не хранятся в hello каталог Azure AD. Поэтому доменные службы Azure AD не работает с такими каталогами Azure AD.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>Можно ли сделать доменные службы AD Azure доступными в нескольких виртуальных сетях в рамках подписки?
саму службу Hello непосредственно не поддерживает этот сценарий. Доменные службы AD Azure доступны в только одной виртуальной сети одновременно. Тем не менее можно настроить подключение между несколькими виртуальными сетями tooexpose доменные службы Azure AD tooother виртуальных сетей. В этой статье описывается, как можно [подключить виртуальные сети в Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>Можно ли включить доменные службы Azure AD с помощью PowerShell?
Автоматическое развертывание доменных служб AD Azure или развертывание с помощью PowerShell в настоящее время недоступны.

#### <a name="is-azure-ad-domain-services-available-in-hello-new-azure-portal"></a>Доменные службы Azure AD доступен hello новом портале Azure?
Нет. Доменные службы Azure AD можно настроить только в hello [классический портал Azure](https://manage.windowsazure.com). Ожидается, что поддержка tooextend hello [портал Azure](https://portal.azure.com) в будущем hello.

#### <a name="can-i-add-domain-controllers-tooan-azure-ad-domain-services-managed-domain"></a>Можно добавить управляемый домен доменных контроллеров tooan доменные службы Azure AD?
Нет. домен Hello, предоставленный доменные службы Azure AD — это управляемый домен. Нет необходимости tooprovision, настройки или в противном случае управление контроллерами домена для этого домена - эти действия, предоставляемые корпорацией Майкрософт как служба управления. Таким образом невозможно добавить дополнительные контроллеры домена (чтения и записи или только для чтения) для управляемого домена hello.

### <a name="administration-and-operations"></a>Администрирование и операции
#### <a name="can-i-connect-toohello-domain-controller-for-my-managed-domain-using-remote-desktop"></a>Можно подключиться toohello контроллера домена в домене управляемых с помощью удаленного рабочего стола?
Нет. У вас разрешения tooconnect toodomain контроллеры домена управляемого hello через удаленный рабочий стол. Члены группы «Администраторы контроллера домена AAD» hello можно администрировать hello управляемого домена с помощью средства администрирования AD, например hello Центр администрирования Active Directory (ADAC) или AD PowerShell. Эти средства устанавливаются с помощью hello «средства удаленного администрирования сервера» компонентов на Windows server присоединен к домену управляемых toohello.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-toodomain-join-machines-toothis-domain"></a>Я включил доменные службы Azure AD. Какую учетную запись пользователя использовать машины toothis toodomain присоединение к домену?
Члены hello административную группу «Администраторы AAD контроллера домена» могут машины присоединения к домену. Кроме того члены этой группы предоставляются toomachines удаленного доступа к рабочему столу, которые были присоединены к домену toohello домена.

#### <a name="do-i-have-domain-administrator-privileges-for-hello-managed-domain-provided-by-azure-ad-domain-services"></a>У привилегии администратора домена для домена управляемого hello, предоставляемые доменные службы Azure AD?
Нет. Права администратора на управляемый домен hello не предоставляются. Права "Администратор" и "Администратор предприятия" недоступны для toouse внутри домена hello. Существующие администратора домена или группы администратора предприятия в каталоге Azure AD также не предоставляются права администратора домена или предприятия в домене hello.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>Можно ли изменить членство в группах с помощью LDAP или других инструментов администрирования AD для управляемых доменов?
Нет. В доменах, поддерживаемых доменными службами Azure AD, членство в группах изменить нельзя. Здравствуйте, тоже относится к атрибутов пользователя. Однако членство в группах или атрибуты пользователей можно изменить в Azure AD или в локальном домене. Такие изменения будут автоматически синхронизированы tooAzure AD доменных служб.

#### <a name="how-long-does-it-take-for-changes-i-make-toomy-azure-ad-directory-toobe-visible-in-my-managed-domain"></a>Как долго длится изменения ли сделать видимым toobe toomy Azure AD directory управляемый домен?
Изменения, внесенные в каталоге Azure AD с помощью PowerShell или hello пользовательского интерфейса Azure AD, синхронизированные tooyour управляемый домен. Этот процесс синхронизации выполняется в фоновом режиме hello. После завершения hello одноразовый начальной синхронизации каталога он обычно занимает примерно 20 минут для изменения, внесенные в Azure AD toobe отражаются в управляемый домен.

#### <a name="can-i-extend-hello-schema-of-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Можно расширить схему hello hello управляемый домен, предоставленный доменные службы Azure AD
Нет. Схема Hello управляется корпорацией Майкрософт для управляемого домена hello. Расширения схемы не поддерживаются в доменных службах Azure AD.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>Можно ли изменять или добавлять записи DNS в управляемом домене?
Да. Члены группы администраторов контроллера домена, hello «AAD» предоставляются права администратора DNS, toomodify записи DNS в домене управляемого hello. Они могут использовать консоль диспетчера DNS hello на машины запущенной Windows Server присоединены к домену toohello управляемого домене, toomanage DNS. hello toouse консоль диспетчера DNS, установите «Средства DNS-сервера», который является частью дополнительный компонент «Средства удаленного администрирования сервера» hello на сервере hello. Дополнительные сведения о [служебных программам для администрирования, мониторинга и устранения неполадок DNS](https://technet.microsoft.com/library/cc753579.aspx) доступны в библиотеке TechNet.

### <a name="billing-and-availability"></a>Выставление счетов и доступность
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Являются ли доменные службы Azure AD платной службой?
Да. Дополнительные сведения см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-hello-service"></a>Существует бесплатная пробная версия для hello службы?
Эта служба входит в hello бесплатной пробной версии Azure. Вы можете зарегистрировать [бесплатную пробную версию Azure на один месяц](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-toouse-azure-ad-domain-services"></a>Можно ли получить доменные службы Azure AD в составе Enterprise Mobility Suite (EMS)? Использовать доменные службы Azure AD Premium toouse Azure AD?
Нет. Доменные службы Azure — это служба Azure с оплатой по мере использования, не входящая в предложение EMS. Доменные службы Azure AD можно использовать со всеми выпусками Azure AD ("Бесплатный", "Базовый" и "Премиум"). Счет выставляется каждый час в зависимости от использования.

#### <a name="what-azure-regions-is-hello-service-available-in"></a>Какие регионы Azure доступна служба hello в?
См. toohello [служб Azure по регионам](https://azure.microsoft.com/regions/#services/) toosee страницы список hello регионах Azure, где находится доменные службы Azure AD.
