---
title: "объединить aaaDomain архитектура Azure HDInsight | Документы Microsoft"
description: "Узнайте, как tooplan домену HDInsight."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 1c3ecedf3739b4f8fa54160225be9c1d6e2ca6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>Планирование архитектуры присоединенных к домену кластеров Hadoop в Azure HDInsight

Hello традиционных Hadoop — это кластер одного пользователя. Он подходит для большинства организаций с небольшими отделами по работе с приложениями, создающими объемные рабочие нагрузки данных. В связи с ростом популярности кластера Hadoop многие организации переходят на модель, когда ИТ-специалисты управляют кластерами и несколько отделов по работе с приложениями совместно используют кластеры. Таким образом функции, связанные с многопользовательской кластеров, среди hello наиболее запрошенного функций Azure HDInsight.

Вместо построения свой собственный сетевой проверки подлинности и авторизации, HDInsight использует наиболее популярные поставщика удостоверений hello--Active Directory (AD). функции Hello мощные безопасности в AD может быть многопользовательской авторизации используется toomanage в HDInsight. Интегрируя HDInsight в AD, могут взаимодействовать с кластерами hello, используя свои учетные данные AD. HDInsight сопоставляет пользователя tooa локального Hadoop пользователь AD, поэтому все hello служб, выполняющихся на HDInsight (Ambari, Hive thrift Spark server круг, сервера и другие) работают незаметно для пользователя с проверкой подлинности hello.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>Интеграция HDInsight с AD и AD на виртуальных машинах IaaS

Интегрируя HDInsight с помощью Azure AD или AD на виртуальной Машине Iaas, узлы кластера HDInsight hello являются домена tooa, присоединенных к домену. HDInsight создает субъекты-службы для hello службам Hadoop, работающих в кластере hello и помещает их в заданном подразделении (OU) в Azure AD или AD на виртуальной Машине IaaS. HDInsight также создает обратного сопоставления DNS в домене hello для hello IP-адреса узлов hello, которые присоединены к домену toohello домена.

Чтобы получить эту конфигурацию, нужно использовать несколько архитектур. Можно выбрать один из следующих архитектур hello.

**Интеграция HDInsight с Active Directory, выполняемой в Azure IaaS**

Это простейший архитектура hello для интеграции с Active Directory HDInsight. контроллер домена AD Hello выполняется на один (или несколько) виртуальных машин (ВМ в Azure). Обычно эти виртуальные машины находятся в виртуальной сети. Настройте другую виртуальную сеть для кластера HDInsight hello. Для HDInsight toohave tooActive прямой видимости каталога, необходимо toopeer эти виртуальные сети с помощью [пиринг VNet-VNet](../virtual-network/virtual-network-create-peering.md). При создании hello Active Directory в ARM, то можно создать hello Active Directory и HDInsight в hello одной виртуальной сети и не требуется toodo пиринга. 

![Топология присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> В этой архитектуре хранилища Озера данных Azure нельзя использовать с кластером HDInsight hello.


Предварительные требования для Active Directory:

* [Подразделение](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) должны создаваться, в которой можно разместить hello виртуальных машин кластера HDInsight и Здравствуйте, участники службы, используемой кластером hello.
* Для взаимодействия с AD необходимо настроить [протоколы LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md). tooset сертификат, используемый Hello копирование LDAPS должно быть реальный сертификат (самозаверяющий сертификат).
* Зоны обратного просмотра DNS должны создаваться в домене hello для hello диапазон IP-адресов подсети HDInsight hello (например, 10.2.0.0/24 на предыдущем рисунке hello).
* Потребуется учетная запись службы или учетная запись пользователя. Используйте этот кластер HDInsight hello toocreate учетной записи. Эта учетная запись должна иметь hello следующие разрешения:

    - Разрешения toocreate service principal-объекты и объекты машины внутри подразделения hello
    - Правила обратного DNS прокси-сервера для разрешения toocreate
    - Домен Active Directory toohello машины toojoin разрешения

**Интеграция HDInsight с облачной службой Azure AD**

Чтобы интегрировать HDInsight с облачной службой Azure AD, необходимо настроить контроллер домена. Его можно настроить с помощью [доменных служб Azure Active Directory](../active-directory-domain-services/active-directory-ds-overview.md). Azure AD DS создает машины контроллера домена в облаке hello и предоставляет IP-адресов для них. Чтобы обеспечить высокий уровень доступности, они создают два контроллера домена.

В настоящее время доменные службы Azure AD доступны только в классических виртуальных сетях. Он доступен только с помощью hello классический портал Azure. Hello HDInsight виртуальная сеть отсутствует в hello портал Azure, которая должна toobe по рангу со hello классической виртуальной сети с помощью пиринг VNet-VNet.

> [!NOTE]
> Пиринг между классической виртуальной сети и виртуальной сети необходимы обе виртуальные сети в диспетчер ресурсов Azure hello в одном регионе и в разделе hello же подписки Azure.

![Топология присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Необходимые условия для Azure AD:

* [Подразделение](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) должны создаваться в течение которого поместите hello виртуальных машин кластера HDInsight и Здравствуйте, участники службы, используемой кластером hello.
* При настройке доменных служб Azure AD вам необходимо настроить [протокол LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md). tooset сертификат, используемый Hello копирование LDAPS должно быть реальный сертификат (самозаверяющий сертификат).
* Зоны обратного просмотра DNS должны создаваться в домене hello для hello диапазон IP-адресов подсети HDInsight hello (например, 10.2.0.0/24 на предыдущем рисунке hello).
* [Хэши паролей](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) должны быть синхронизированы с Azure AD tooAzure AD DS.
* Потребуется учетная запись службы или учетная запись пользователя. Используйте этот кластер HDInsight hello toocreate учетной записи. Эта учетная запись должна иметь hello следующие разрешения:

    - Разрешения toocreate service principal-объекты и объекты машины внутри подразделения hello
    - Правила обратного DNS прокси-сервера для разрешения toocreate
    - Машины toohello Azure AD разрешения toojoin домена

## <a name="next-steps"></a>Дальнейшие действия
* tooconfigure кластера HDInsight присоединенных к домену, в разделе [настроить домену кластеров HDInsight](hdinsight-domain-joined-configure.md).
* toomanage домену кластеров HDInsight, в разделе [управление кластерами HDInsight на присоединенных к домену](hdinsight-domain-joined-manage.md).
* политики tooconfigure Hive и выполнения запросов Hive, см. [Hive настроить политики для присоединенных к домену кластеров HDInsight](hdinsight-domain-joined-run-hive.md).
* toorun запросов Hive с помощью SSH на присоединенных к домену кластеров HDInsight. в разделе [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
