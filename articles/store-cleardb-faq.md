---
title: "aaaFAQ для баз данных ClearDB MySql службе приложений Azure | Документы Microsoft"
description: "Ответы на вопросы toocommon об использовании баз данных ClearDB MySQL службе приложений Azure."
documentationcenter: php
services: 
author: sunbuild
manager: yochayk
editor: 
tags: mysql
ms.assetid: c2ed5e78-6d7d-4d0c-b7ee-a52ae41ceab8
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: sumuth
ms.openlocfilehash: 3d9c9daca2b845ede8d3a1fdadefa7e668d62dee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="faq-for-cleardb-mysql-databases-with-azure-app-service"></a>Часто задаваемые вопросы о базах данных ClearDB MySql в службе приложений Azure
Ответы на часто задаваемые вопросы об использовании и покупке баз данных ClearDB MySql для службы веб-приложений Azure.

## <a name="what-options-do-i-have-for-mysql-on-azure"></a>Какие параметры баз данных MySQL доступны в Azure?
Доступно несколько параметров.

* [Общая база данных ClearDB MySQL](/marketplace/partners/cleardb/databases/)
* [Кластеры ClearDB MySQL Premium](/marketplace/partners/cleardb-clusters/cluster/)
* [Кластер MySQL на виртуальной машине Azure](https://github.com/azure/azure-quickstart-templates/tree/master/mysql-replication)
* [Отдельный экземпляр MySQL на виртуальной машине Azure](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

ClearDB является MySQL, в котором размещена служба и управляет hello MySQL инфраструктуры. При выполнении собственных кластер MySQL или базы данных на виртуальной машине Azure, вы имеют tooset сервера MySQL hello и обновлять исправлений.

## <a name="do-i-need-a-credit-card-for-hello-web-app--mysql-template-in-hello-azure-marketplace"></a>Требуются ли для веб-приложения hello + шаблона MySQL в Azure Marketplace hello кредитной карты?
Это зависит от типа hello подписку, которую вы используете. Чаще всего используются следующие типы подписки:

* [Оплата по мере использования:](/offers/ms-azr-0003p/) требуется кредитная карта. При покупке платной базы данных MySQL ее стоимость будет списана с вашей кредитной карты.
* [Бесплатная пробная версия:](https://azure.microsoft.com/pricing/free-trial/) включает кредиты на использование со службами Microsoft Azure, но не позволяет приобретение ресурсов сторонних производителей. Подписка, настроенная для toopurchase сторонние службы или платной базой данных MySQL, необходимо toouse кредитной карты. Для веб-приложений можно создать БЕСПЛАТНУЮ базу данных MySQL ClearDB.
* [Подписка MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/) и **MSDN для разработки тестирования повременную оплату**: аналогичные tooFree пробной подписки MSDN требует toohave кредитной карты toopurchase платные решения MySQL из ClearDB.
* [Соглашение Enterprise (EA):](https://azure.microsoft.com/pricing/enterprise-agreement/) клиенты с подпиской EA ежеквартально получают отдельный консолидированный счет на все совершенные ими покупки решений сторонних разработчиков в Azure Marketplace. Взимается плата за пределами hello денежную оплату за покупки в marketplace. Обратите внимание на то, что, в настоящее время хранилище Azure не доступные toocustomers, зарегистрированных в Азербайджан, Хорватия, Норвегия и Пуэрто-Рико. 
* [DreamSpark](https://www.dreamspark.com/Product/Product.aspx?productid=99): позволяет создавать только БЕСПЛАТНЫЕ базы данных ClearDB для веб-приложений. Нет ограничений на число hello свободного ClearDB MySQL баз данных, которые можно создать. Обратите внимание, что бесплатных баз данных не toobe, используемые для производственного веб-приложений, как эта служба предназначена только для пробной версии.

## <a name="why-was-i-charged-350-for-a-web-app--mysql-from-hello-azure-marketplace"></a>Почему оплачивалась 3,50 долларов для веб-приложение + MySQL из hello Azure Marketplace
параметр базы данных по умолчанию Hello является Titan, который является 3,50 долларов. Мы больше не показывать hello затрат при создании базы данных и базы данных, которые не планируется по ошибке можно приобрести. Мы пытаемся toofind в интерфейсе hello tooimprove способом, но до тех пор все вашей выбранного ценовые категории для веб-приложения и базы данных необходимо проверить перед нажатием кнопки **создать** и запуск развертывания hello hello ресурсов.

## <a name="i-am-running-mysql-on-my-own-azure-virtual-machine-can-i-connect-my-azure-web-app-toomy-database"></a>Я использую MySQL на собственной виртуальной машине Azure. Можно ли подключить базы данных Azure web app toomy?
Да. Можно подключиться к веб-приложения tooyour база данных до тех пор, пока ВМ Azure предоставил удаленного доступа tooyour веб-приложения. Дополнительные сведения см. в статье об [установке MySQL на виртуальной машине](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="in-which-countries-are-cleardb-premium-mysql-clusters-supported"></a>В каких странах поддерживаются кластеры ClearDB MySQL Premium?
[Кластеры ClearDB Premium MySQL](/marketplace/partners/cleardb-clusters/cluster/) доступны во всех регионах Azure по всему миру исключением hello Индии, Южной Бразилии, Австралии и Китая.

## <a name="can-i-create-a-new-cluster-prior-toocreating-a-database-with-cleardb-premium-cluster-solution"></a>Можно создать новый кластер toocreating предыдущей базы данных с ClearDB premium кластерное решение?
Нет, создание пустых кластеров ClearDB не поддерживается. Hello Azure портал позволяет toocreate баз данных в кластере, что может создать новый кластер в hello то же время.

## <a name="will-i-be-warned-if-i-try-toodelete-a-cleardb-mysql-database-that-is-in-use-by-one-of-my-applications"></a>Я предупреждение при попытке toodelete базы данных ClearDB MySQL, используемой одним Мои приложения?
Нет, Azure не предупреждает пользователя об удалении покупки из Azure Marketplace, от которой зависит приложение.

## <a name="which-regions-can-i-create-cleardb-databases-in"></a>В каких регионах можно создавать базы данных ClearDB?
Azure Marketplace нет доступных toocustomers, зарегистрированных в Азербайджан, Хорватия, Норвегия или Пуэрто-Рико. В этих регионах ClearDB недоступна.

## <a name="what-pricing-tier-should-i-choose-for-a-production-web-app-and-database"></a>Какую ценовую категорию лучше выбрать для рабочего веб-приложения и базы данных?
Для веб-приложений выбирайте базовую или более высокую ценовую категорию. Для ClearDB рекомендуется план "Сатурн" или "Юпитер". Просмотрите функции hello и ограничения каждой ценовой категории для обоих [веб-приложений](https://azure.microsoft.com/pricing/details/app-service/) и [баз данных ClearDB MySQL](/marketplace/partners/cleardb/databases/) toochoose hello, который соответствует вашим требованиям.

## <a name="how-do-i-upgrade-my-cleardb-database-from-one-plan-tooanother"></a>Как обновить базу данных ClearDB из одного плана tooanother?
В hello [портал Azure](https://portal.azure.com), можно масштабировать базу данных ClearDB общего размещения. Прочитать этот [статьи](https://blogs.msdn.microsoft.com/appserviceteam/2016/10/06/upgrade-your-cleardb-mysql-database-in-azure-portal/) toolearn дополнительные. Обновления в настоящее время не поддерживаются для кластеров ClearDB Premium в hello портал Azure.

## <a name="i-cant-see-my-cleardb-database-in-azure-portal"></a>Я не вижу свою базу данных ClearDB на портале Azure!
Если мы создадим базу данных ClearDB, с помощью диспетчера ресурсов Azure или [новый портал Azure](https://portal.azure.com), он не будет видимым в hello [старый портал Azure](https://manage.windowsazure.com). toowork-вокруг это является toolink базы данных вручную toohello веб-приложения. Аналогично Если создать базу данных ClearDB hello [старый портал](https://manage.windowsazure.com) не может быть может toosee базы данных в hello [новый портал Azure](https://portal.azure.com). Нет отсутствует способ решения в последнем сценарии hello.

## <a name="who-do-i-contact-for-support-when-my-database-is-down"></a>Куда обращаться за помощью в случае отказа базы данных?
По всем вопросам, связанным с базами данных, обращайтесь в [службу поддержки ClearDB](https://www.cleardb.com/developers/help/support) . Подготовить tooprovide их сведений о подписке Azure.

## <a name="can-i-create-additional-users-for-my-cleardb-mysql-database-cluster-solution"></a>Можно ли создавать дополнительных пользователей для кластера баз данных ClearDB MySQL?
Нет. Создавать дополнительных пользователей в кластере баз данных ClearDB нельзя, но можно создавать дополнительные базы данных.  

## <a name="can-basicpro-series-databases-be-upgraded-in-place-similar-tooplanetary-plans-today-on-cleardb-portal"></a>Можно баз данных Basic/Pro ряда обновленного на месте аналогичных tooPlanetary планов сегодня на портале ClearDB
Да, базы данных серии Basic (Basic 60 – Basic 500) можно обновить на месте. Вы можете обновить на месте базы данных серии Pro (Pro 125–1000), за исключением Pro 60. В настоящее время обновление базы данных Pro 60 не поддерживается. 

## <a name="when-i-migrate-my-resources-from-one-subscription-tooanother-does-my-cleardb-mysql-database-get-migrated-as-well"></a>Если перенести Мои ресурсы из одной подписки tooanother, Моя база данных ClearDB MySQL перенесены также?
При переносе ресурсов из одной подписки в другую действуют некоторые [ограничения](app-service-web/app-service-move-resources.md) . База данных ClearDB MySQL — это сторонняя служба, в связи с чем она не перемещается при переносе подписки Azure. Если вы не управляете hello миграции вашей MySQL базы данных предыдущей toomigrating Azure ресурсы вашего ClearDB MySQL баз данных могут быть отключены. Сначала вручную перенесите свои базы данных, а затем измените подписку веб-приложения. 

## <a name="i-hit-hello-spending-limit-on-my-subscription-i-removed-hello-limit-and-my-app-service-is-online-however-hello-database-is-not-accessible-how-do-i-re-enable-hello-cleardb-database"></a>Я нажимаю hello лимит на подписку. Я удалил предел hello и приложения в службе находится в оперативном режиме, однако hello база данных недоступна. Как повторно включить базу данных ClearDB hello?
Обратитесь к [ClearDB поддержки](https://www.cleardb.com/developers/help/support) базы данных включить toore hello. Сообщите данные вашей подписки Azure и имя базы данных.

## <a name="can-i-transfer-a-cleardb-database-from-a-credit-card-subscription-tooan-ea-subscription"></a>Можно перенести базу данных ClearDB из tooan EA кредитной карты подписки подписки?
Существующие базы данных ClearDB использовать hello кредитной карты, связанной с существующие подписки hello. toouse подписка EA необходимо toomigrate данных tooa новой базы данных:

* Приобретите новую базу данных ClearDB для своей подписки EA.
* Перенос данных tooyour новой базы данных.
* Обновите toouse hello новой базы данных приложения.
* Удалите старую базу данных ClearDB.

При создании нового веб-приложения с MySQL (ClearDB) или создать базу данных MySQL (ClearDB), подписку hello определяет, каким образом будет оплатить службы hello. При использовании подписки EA мы не будет блокировать hello поставка hello услуги третьих лиц, например ClearDB в hello портал Azure. Счета на подписку EA выставляются отдельно от абонентской платы. Консолидированные счета выставляются ежеквартально. Клиент EA Hello бы tooset способ оплаты, например toopay кредитной карты для всех служб marketplace сторонних разработчиков.

## <a name="where-can-i-see-hello-charges-for-cleardb-resources-in-an-ea-subscription"></a>Где просмотреть hello плата за ClearDB ресурсы в подписке EA?
Для клиентов EA прямые расходы Azure Marketplace, отображаются при приветствия корпоративного портала. Обратите внимание, что все покупки в Azure Marketplace оплачиваются отдельно от абонентской платы. Консолидированные счета выставляются ежеквартально. Клиенты, EA имеют toopay напрямую toohello службы сторонних поставщиков и может поэтому путем включения способ оплаты, например кредитной карты с их EA учетной записи.

Непрямых клиентов EA можно найти своих подписок Azure Marketplace на hello **управление подписками** страницы приветствия корпоративного портала, но цены скрыт. За информацией о сборах Azure Marketplace клиентам следует обращаться к поставщикам решений по лицензированию.

TooAzure доступа Marketplace для службы сторонних разработчиков могут управляться администраторов регистрации EA Azure. Их можно отключить или повторно включить доступ too3rd стороной покупки из hello хранилища в управление учетными записями и подписках в разделе "hello" учетные записи в приветствия корпоративного портала.

## <a name="who-do-i-contact-for-questions-about-my-bill-for-cleardb-services-in-my-ea-subscription"></a>К кому обращаться с вопросами по счету за службы ClearDB по подписке EA?
Обратитесь к [Корпоративная поддержка клиента](http://aka.ms/AzureEntSupport) с toobilling отношении при их регистрации EA. Hello группа поддержки EA портала будет ответить на ваши вопросы или помочь устранить проблему.

## <a name="more-information"></a>Дополнительные сведения
[Часто задаваемые вопросы об Azure Marketplace](/marketplace/faq/)

