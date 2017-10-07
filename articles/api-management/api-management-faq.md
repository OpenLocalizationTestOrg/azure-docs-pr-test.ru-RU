---
title: "часто задаваемые вопросы об API управления aaaAzure | Документы Microsoft"
description: "Дополнительные сведения hello ответы на вопросы toocommon, шаблоны и рекомендации в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 9e7cdf1b881a4dfed4bd2cfd7fbb4994f48b5f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-faqs"></a>Часто задаваемые вопросы о службе управления API Azure
Получение hello ответы toocommon вопросы, шаблоны и рекомендации для управления API Azure.

## <a name="contact-us"></a>Свяжитесь с нами
* [Как можно задать группы Microsoft Azure API Management hello вопрос?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы
* [Что означает, если функция пребывает в предварительной версии?](#what-does-it-mean-when-a-feature-is-in-preview)
* [Как защитить соединения hello между шлюзом управления API hello и внутренней службы](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [Как копировать my API управления службы tooa экземпляра нового?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [Можно ли управлять экземпляром службы управления API программными средствами?](#can-i-manage-my-api-management-instance-programmatically)
* [Как добавить группу администраторов toohello пользователей?](#how-do-i-add-a-user-to-the-administrators-group)
* [Почему необходимо hello политики, что я tooadd недоступна в редакторе hello политики?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [Как использовать управление версиями в службе управления API?](#how-do-i-use-api-versioning-in-api-management)
* [Как настроить несколько сред в одном API?](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [Можно ли использовать SOAP в управлении API?](#can-i-use-soap-with-api-management)
* [Такое hello API управления шлюз IP адрес константа? Можно ли использовать его в правилах брандмауэра?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [Можно ли настроить на сервере авторизации OAuth 2.0 систему безопасности служб федерации Active Directory?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [Какой метод маршрутизации API управления использовать в развертываниях toomultiple географических расположений?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [Можно использовать toocreate шаблона диспетчера ресурсов Azure экземпляра службы управления API](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [Можно ли использовать самозаверяющий сертификат SSL для сервера?](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [Почему при попытке tooclone репозитория получить сбоя проверки подлинности?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [Работает ли управление API с Azure ExpressRoute?](#does-api-management-work-with-azure-expressroute)
* [Зачем требуется выделенная подсеть в виртуальных сетях типа Resource Manager, если в них развернута служба управления API?](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [Каков размер минимальное подсети hello необходимы при развертывании управления API в виртуальную сеть?](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [Можно переместить службу управления API из одной подписки tooanother?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [Существуют ли ограничения на импорт API или известные проблемы, связанные с этим процессом?](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-hello-microsoft-azure-api-management-team-a-question"></a>Как можно задать группы Microsoft Azure API Management hello вопрос?
С нами можно связаться одним из следующих способов:

* Свои вопросы вы можете разместить на нашем [форуме MSDN для службы управления API](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt).
* Отправить сообщение электронной почты слишком<mailto:apimgmt@microsoft.com>.
* Отправьте запрос на функции в hello [форуме обратной связи Azure](https://feedback.azure.com/forums/248703-api-management).

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>Что означает, если функция пребывает в предварительной версии?
Компонент находится в предварительной версии, означает, что мы активно нужна отзывы о как hello функция работает автоматически. Функция в предварительной версии функционально завершена, но это возможно, мы выполним критические изменения в ответ toocustomer отзывы. Мы рекомендуем не закладывать в основу рабочей среды функции в предварительной версии. При наличии любых отзывов на предварительные версии компонентов, сообщите нам через один hello параметры контакта в [как можно задать группы Microsoft Azure API Management hello вопрос?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question).

### <a name="how-can-i-secure-hello-connection-between-hello-api-management-gateway-and-my-back-end-services"></a>Как защитить соединения hello между шлюзом управления API hello и внутренней службы
Имеется несколько параметров toosecure hello подключение между шлюзом управления API hello и внутренней службы. Вы можете:

* Использование обычной проверки подлинности HTTP. Дополнительные сведения см. в разделе [Настройка параметров API](api-management-howto-create-apis.md#configure-api-settings).
* Использовать взаимную проверку подлинности SSL, как описано в [как toosecure внутренней службы с помощью проверки подлинности сертификата клиента в Azure API Management](api-management-howto-mutual-certificates.md).
* использовать разрешенный список IP-адресов во внутренних службах. Если у вас есть экземпляра управления API уровня Standard или Premium, hello IP-адрес шлюза hello остается постоянным. Можно задать этот IP-адрес вашего tooallow белого списка. Hello IP-адрес вашего экземпляра управления API можно получить на hello панели мониторинга в hello портал Azure.
* Подключиться к API управления экземпляр tooan виртуальной сети Azure.

### <a name="how-do-i-copy-my-api-management-service-instance-tooa-new-instance"></a>Как копировать my API управления службы tooa экземпляра нового?
Существует несколько вариантов, если требуется, чтобы toocopy API экземпляра tooa нового экземпляра службы управления. Вы можете:

* Программа hello архивации и восстановления функции в службе управления API. Дополнительные сведения см. в разделе [как tooimplement аварийного восстановления с помощью службы резервного копирования и восстановления в Azure API Management](api-management-howto-disaster-recovery-backup-restore.md).
* Создавать резервные копии и восстановления с помощью hello [API REST управления](https://msdn.microsoft.com/library/azure/dn776326.aspx). И восстановления hello сущностей из hello экземпляр службы, который вы хотите использовать toosave hello REST API.
* Конфигурация службы hello загрузки с помощью Git, а затем передать его tooa новый экземпляр. Дополнительные сведения см. в разделе [как toosave и настроить конфигурацию службы управления API с помощью Git](api-management-configuration-repository-git.md).

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>Можно ли управлять экземпляром службы управления API программными средствами?
Да, вы можете управлять службой управления API с помощью программных средств:

* Hello [API REST управления](https://msdn.microsoft.com/library/azure/dn776326.aspx).
* Hello [ApiManagement службы управления библиотеки пакета SDK Microsoft Azure](http://aka.ms/apimsdk).
* Hello [развертывания службы](https://msdn.microsoft.com/library/mt619282.aspx) и [управление службой](https://msdn.microsoft.com/library/mt613507.aspx) командлеты PowerShell.

### <a name="how-do-i-add-a-user-toohello-administrators-group"></a>Как добавить группу администраторов toohello пользователей?
Вот, как можно добавить группу администраторов toohello пользователя.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Go toohello группы ресурсов, имеющий hello управления API экземпляра tooupdate.
3. В службе управления API, назначение hello **участника Api управления** toohello пользователя роли.

Теперь hello добавления участника можно использовать Azure PowerShell [командлеты](https://msdn.microsoft.com/library/mt613507.aspx). Вот как toosign в качестве администратора:

1. Используйте hello `Login-AzureRmAccount` toosign командлета в.
2. Задать hello контекста toohello подписки с hello службы с помощью `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`.
3. Получите URL-адрес единого входа, выполнив `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`.
4. Используйте портал администрирования hello tooaccess URL-адрес hello.

### <a name="why-is-hello-policy-that-i-want-tooadd-unavailable-in-hello-policy-editor"></a>Почему необходимо hello политики, что я tooadd недоступна в редакторе hello политики?
Hello политику что tooadd отображается серым цветом или закрашены редактор политики hello, убедитесь, что находятся в неправильной области hello hello политики. Каждая инструкция политика предназначена для toouse в определенной области и разделы политики. Использование политик hello см. разделы политики tooreview hello и области для политики, статьи [политиках управления интерфейсами API](https://msdn.microsoft.com/library/azure/dn894080.aspx).

### <a name="how-do-i-use-api-versioning-in-api-management"></a>Как использовать управление версиями в службе управления API?
У вас есть несколько управление версиями API toouse параметры управления API:

* В службе управления API можно настроить различные версии toorepresent API-интерфейсы. Например, может понадобиться настроить два разных API, MyAPIv1 и MyAPIv2. Разработчик можно выбрать версию hello, hello разработчик хочет toouse.
* Вы также можете настроить для API URL-адрес службы без учета версии, например https://my.api. Затем необходимо настроить сегмент версии для шаблона [перезаписи URL-адреса](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) каждой операции. Например, есть операция, в которой используется [шаблон URL-адреса](api-management-howto-add-operations.md#url-template) /resource и [перезаписи URL-адреса](api-management-howto-add-operations.md#rewrite-url-template) /v1/Resource. Можно изменить значение сегмента версии hello отдельно для каждой операции.
* При желании tookeep сегмент версии «default» в URL-адрес службы hello API-интерфейса, на выбранной операции задать политики, использующей hello [задать серверной службы](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) политики toochange hello серверной части запроса пути.

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>Как настроить несколько сред в одном API?
tooset копирование нескольких средах, например, в среде тестирования и рабочей среде, в единый интерфейс API, у вас есть два варианта. Вы можете:

* Различные интерфейсы API на узле hello того же клиента.
* Узел hello те же API для разных клиентов.

### <a name="can-i-use-soap-with-api-management"></a>Можно ли использовать SOAP в управлении API?
Сейчас поддерживается [сквозная передача SOAP](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/). Администраторы могут импортировать hello WSDL службы SOAP и API управления Azure создаст внешнего интерфейса SOAP. Для служб SOAP доступны документация портала для разработчиков, консоль тестирования, политики и средства анализа.

### <a name="is-hello-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>Такое hello API управления шлюз IP адрес константа? Можно ли использовать его в правилах брандмауэра?
На уровнях Standard и Premium hello hello общедоступный IP-адрес (VIP) hello управления API клиента является статическим hello время существования клиента hello, за некоторыми исключениями. Hello изменения IP-адреса в следующих ситуациях:

* Hello службы удаляется и создается снова.
* — Подписка на службу Hello [приостановки](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) или [предупреждение](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) (например, nonpayment) и затем восстановлен.
* Добавление или удаление виртуальной сети Azure (только на hello разработчика и уровня Premium можно использовать виртуальную сеть).

Для развертываний с несколькими регионами, hello изменения региональных адреса, если область hello освободившиеся, а затем активирует (только на уровне Premium hello можно использовать развертывание в нескольких регионах).

Клиентам уровня "Премиум", для которых настроено развертывание в нескольких регионах, назначается один общедоступный IP-адрес на регион.

На странице приветствия клиента в hello портал Azure можно получить IP-адрес (или адреса, в развертывание в нескольких регионах).

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>Можно ли настроить на сервере авторизации OAuth 2.0 систему безопасности служб федерации Active Directory?
tooconfigure сервера авторизации OAuth 2.0 безопасности служб федерации Active Directory (AD FS). в статье toolearn [с помощью служб федерации Active Directory в службе управления API](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/).

### <a name="what-routing-method-does-api-management-use-in-deployments-toomultiple-geographic-locations"></a>Какой метод маршрутизации API управления использовать в развертываниях toomultiple географических расположений?
API управления использует hello [метод маршрутизации трафика производительности](../traffic-manager/traffic-manager-routing-methods.md#priority) в развертываниях toomultiple географических регионах. Входящий трафик — перенаправленное toohello ближайший API шлюза. Если одной области переходит в автономный режим, входящий трафик будет автоматически перенаправленное toohello Далее ближайший шлюза. Дополнительные сведения о методах маршрутизации см. в статье [Методы маршрутизации трафика диспетчером трафика](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="can-i-use-an-azure-resource-manager-template-toocreate-an-api-management-service-instance"></a>Можно использовать toocreate шаблона диспетчера ресурсов Azure экземпляра службы управления API
Да. В разделе hello [службы управления API Azure](http://aka.ms/apimtemplate) примеры использования шаблонов.

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>Можно ли использовать самозаверяющий сертификат SSL для сервера?
Да. Вот, как toouse самозаверяющий Secure Sockets Layer (SSL) сертификат для серверной части.

1. Создайте [серверную](https://msdn.microsoft.com/library/azure/dn935030.aspx) сущность с помощью службы управления API.
2. Набор hello **skipCertificateChainValidation** свойство слишком**true**.
3. Если вы больше не требуется tooallow самозаверяющие сертификаты, удалите сущность серверной части hello, или задайте hello **skipCertificateChainValidation** свойство слишком**false**.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-tooclone-a-git-repository"></a>Почему при попытке tooclone репозитория получить сбоя проверки подлинности?
При использовании Git диспетчер учетных данных или если вы пытаетесь tooclone репозитория с помощью Visual Studio, вы можете столкнуться с известными проблемами диалоговое окно учетных данных Windows hello. диалоговое окно «Hello» ограничивает символов too127 длины пароля и усекает hello пароль созданный корпорацией Майкрософт. Мы работаем над сокращение hello пароль. Теперь используйте tooclone Git Bash репозиторий Git.

### <a name="does-api-management-work-with-azure-expressroute"></a>Работает ли управление API с Azure ExpressRoute?
Да. Служба управления API работает с Azure ExpressRoute.

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>Зачем требуется выделенная подсеть в виртуальных сетях типа Resource Manager, если в них развернута служба управления API?
требование Hello выделенная подсеть для управления API поступает из факт hello и она была основана на модели развертывания классический (слой PAAS V1). Хотя мы можно развернуть в виртуальной сети (слой V2) диспетчера ресурсов, существуют toothat последствия. Hello классической модели развертывания в Azure не является тесно связанным с модели hello диспетчера ресурсов, поэтому при создании ресурса на уровне V2, слой V1 hello не знает о нем и проблемы может произойти, например попытки toouse IP-адрес, который выделен управления API tooa сетевой Адаптер (основан на версии 2).
Дополнительные сведения о различие моделей классический и диспетчер ресурсов в Azure см. слишком toolearn[разница в модели развертывания](../azure-resource-manager/resource-manager-deployment-model.md).

### <a name="what-is-hello-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>Каков размер минимальное подсети hello необходимы при развертывании управления API в виртуальную сеть?
размер минимальное подсети Hello необходимости toodeploy — API управления [/29](../virtual-network/virtual-networks-faq.md#configuration), который является размер hello минимальное подсети, которая поддерживает Azure.

### <a name="can-i-move-an-api-management-service-from-one-subscription-tooanother"></a>Можно переместить службу управления API из одной подписки tooanother?
Да. toolearn, изучите раздел [переместить ресурсы tooa группы ресурсов или подписку](../azure-resource-manager/resource-group-move-resources.md).

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>Существуют ли ограничения на импорт API или известные проблемы, связанные с этим процессом?
[Известные проблемы и ограничения](api-management-api-import-restrictions.md) для форматов Open API (Swagger), WSDL и WADL.
