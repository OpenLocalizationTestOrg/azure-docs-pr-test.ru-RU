---
title: "кластеры HDInsight, присоединенных к домену с помощью PowerShell, Azure aaaConfigure | Документы Microsoft"
description: "Узнайте, как tooset и настройке кластеров HDInsight, присоединенных к домену, с помощью Azure PowerShell"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a13b2f7a-612d-4800-bc92-7fc0524f3e89
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 49da3439513d1e51171f0f7f7f9c3d967d55cb7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview-using-azure-powershell"></a>Настройка присоединенных к домену кластеров HDInsight (предварительная версия) с помощью Azure PowerShell
Узнайте, как кластер tooset копирование Azure HDInsight с Azure Active Directory (Azure AD) и [круг Apache](http://hortonworks.com/apache/ranger/) с помощью Azure PowerShell. Сценарий Azure PowerShell, предоставляются toomake hello конфигурации быстрее и менее подвержен ошибкам. Присоединенный к домену кластер HDInsight можно настроить только с помощью кластеров под управлением Linux. Дополнительные сведения см. в статье [Introduce Domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md) (Введение в присоединенные к домену кластеры HDInsight).

> [!IMPORTANT]
> Диспетчер Oozie не включен в присоединенном к домену кластере HDInsight.

Типичная конфигурация кластера HDInsight, присоединенных к домену включает в себя hello следующие шаги:

1. Создайте классическую виртуальную сеть Azure для Azure AD.  
2. Создайте и настройте Azure AD и доменные службы Azure Active Directory.
3. Добавить toohello ВМ классической виртуальной сети для создания подразделения. 
4. Создайте подразделение для доменных служб Azure Active Directory.
5. Создание виртуальной сети HDInsight в режиме управления hello ресурсов Azure.
6. Настройка зоны обратного DNS для hello Azure AD DS.
7. Одноранговый hello двух виртуальных сетей.
8. Создание кластера HDInsight.

Hello сценарий PowerShell выполняет шаги с 3 по 7. Шаги 1–2 выполняются вручную.  Если вы предпочитаете toouse Azure PowerShell, см. [кластеров HDInsight, присоединенных к домену, настройте](hdinsight-domain-joined-configure.md). 

Пример топологии окончательного hello выглядит следующим образом:

![Топология присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Так как в настоящее время Azure AD поддерживает только классические виртуальные сети, а кластеры HDInsight под управлением Linux поддерживают только виртуальные сети на основе Azure Resource Manager, для интеграции HDInsight с Azure AD нужно создать две виртуальные сети и настроить пиринг между ними. Hello сравнения между моделями развертывания hello двух Подробнее [диспетчера ресурсов Azure и классическое развертывание: Обзор модели развертывания и hello состояния ресурсов](../azure-resource-manager/resource-manager-deployment-model.md). Две виртуальные сети должны находиться в hello Hello же регионе, что hello Azure AD DS.

> [!NOTE]
> В этом руководстве предполагается, что служба Azure AD не установлена. Если она есть, можно пропустить часть hello в шаге 2.
> 
> 

## <a name="prerequisites"></a>Предварительные требования
Необходимо иметь следующие элементы toogo этого учебника hello.

* Ознакомьтесь с [доменными службами Azure AD](https://azure.microsoft.com/services/active-directory-ds/) и их [ценовой](https://azure.microsoft.com/pricing/details/active-directory-ds/) структурой.
* Убедитесь, что ваша подписка внесена в список разрешенных подписок для этой общедоступной предварительной версии. Это можно сделать путем отправки сообщения электронной почты toohdipreview@microsoft.com вашим идентификатором подписки.
* SSL-сертификат, подписанный заверителем подписи для вашего домена. требуется сертификат Hello путем настройки защищенного протокола LDAP. Нельзя использовать самозаверяющие сертификаты.
* Установите Azure PowerShell.  См. руководство по [установке и настройке Azure PowerShell](/powershell/azure/overview).

## <a name="create-an-azure-classic-vnet-for-your-azure-ad"></a>Создайте классическую виртуальную сеть Azure для Azure AD.
Hello инструкции см. в разделе [здесь](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic).

## <a name="create-and-configure-azure-ad-and-azure-ad-ds"></a>Создайте и настройте Azure AD и доменные службы Azure Active Directory.
Hello инструкции см. в разделе [здесь](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).

## <a name="run-hello-powershell-script"></a>Запуск сценария PowerShell hello
Hello сценарий PowerShell можно загрузить из [GitHub](https://github.com/hdinsight/DomainJoinedHDInsight). Извлеките hello ZIP-файл и сохраните файлы hello локально.

**hello tooedit сценария PowerShell**

1. Откройте файл run.ps1 с помощью интегрированной среды сценариев Windows PowerShell или любого текстового редактора.
2. Заполните значения hello hello следующие переменные:
   
   * **$SubscriptionName** — hello имя hello подписки Azure, где требуется toocreate кластеру HDInsight. В этой подписки уже создан классической виртуальной сети и будут создавать виртуальной сетью Azure Resource Manager для кластера HDInsight hello в подписке.
   * **$ClassicVNetName** -hello классической виртуальной сети, содержащей hello Azure AD DS. Эта виртуальная сеть должна находиться в hello одной подписке, что приведенные выше. Эта виртуальная сеть должны создаваться с помощью hello портал Azure, а не с помощью классического портала. Если следовать инструкциям hello [кластеров HDInsight, присоединенных к домену, настройте (Предварительная версия)](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic), имя по умолчанию hello — contosoaadvnet.
   * **$ClassicResourceGroupName** — имя группы hello диспетчера ресурсов для hello классической виртуальной сети, который указан выше. Например, contosoaadrg. 
   * **$ArmResourceGroupName** — имя группы ресурсов hello в течение которого, требуется кластер HDInsight toocreate hello. Можно использовать hello $ArmResourceGroupName же группе ресурсов.  Если группа ресурсов hello не существует, сценарий hello создает hello группы ресурсов.
   * **$ArmVNetName** -имя виртуальной сети hello диспетчера ресурсов, в течение которого требуется кластер HDInsight toocreate hello. Эта виртуальная сеть будет помещена в группу $ArmResourceGroupName.  Если hello виртуальная сеть не существует, сценарий PowerShell hello создаст его. Если он существует, она должна входить hello ресурсов группы, введенного выше.
   * **$AddressVnetAddressSpace** — hello адресного пространства для виртуальной сети hello диспетчера ресурсов сети. Убедитесь, что это адресное пространство доступно. Это адресное пространство не может перекрывать адресное пространство hello классической виртуальной сети. Например, 10.1.0.0/16.
   * **$ArmVnetSubnetName** -в пределах которого будут ВМ кластера HDInsight hello tooplace подсети имя hello диспетчера ресурсов виртуальной сети. Если подсеть hello не существует, сценарий PowerShell hello создаст его. Если он существует, следует частью hello виртуальной сети, введенного выше.
   * **$AddressSubnetAddressSpace** — hello сетевой диапазон адресов для подсети виртуальной сети hello диспетчера ресурсов. Здравствуйте, виртуальная машина IP-адреса будет из диапазона адресов этой подсети кластера HDInsight. Например, 10.1.0.0/24.
   * **$ActiveDirectoryDomainName** — имя домена hello Azure AD, которые должны toojoin hello HDInsight кластера виртуальные машины. Например, contoso.onmicrosoft.com.
   * **$ClusterUsersGroups** — общее имя hello hello групп безопасности в AD, что требуется кластер HDInsight toohello toosync. Пользователи Hello в пределах этой группы безопасности будут может toolog на панели мониторинга кластера toohello, используя свои учетные данные домена active directory. Эти группы безопасности должен существовать в hello active directory. Например, hiveusers или clusteroperatorusers.
   * **$OrganizationalUnitName** -hello организационное подразделение в домене hello, в течение которого требуется кластер HDInsight tooplace hello виртуальных машин и Здравствуйте, участники службы, используемой кластером hello. Hello сценарий PowerShell создает этого Подразделения не существует. Например, HDInsightOU.
3. Сохраните изменения hello.

**сценарий toorun hello**

1. Запустите **Windows PowerShell** от имени администратора.
2. Найдите папку toohello run.ps1. 
3. Запустите скрипт hello, введя имя файла hello и нажмите кнопку **ввод**.  Откроется 3 диалоговых окна.
   
   1. **Войдите на классический портал tooAzure** — введите свои учетные данные, которые вы используете toosign tooAzure классического портала. Необходимо создать hello Azure AD и Azure AD DS с помощью этих учетных данных.
   2. **Войдите в портал диспетчера ресурсов tooAzure** — введите свои учетные данные, которые вы используете toosign tooAzure портала диспетчера ресурсов.
   3. **Имя пользователя домена** — ввести учетные данные, которые должны toobe администратором кластера HDInsight hello имя пользователя домена hello hello. Если вы создали службу Azure AD с нуля, вы также должны были создать этого пользователя (как описано в этой документации). 
      
      > [!IMPORTANT]
      > Введите имя пользователя hello в следующем формате: 
      > 
      > Имя_домена\имя_пользователя (например, contoso.onmicrosoft.com\clusteradmin).
      > 
      > 
      
      Этот пользователь должен иметь права на 3: toohello машины toojoin указанный домен Active Directory; toocreate субъекты-службы и объекты машины внутри hello предоставленный подразделения; и tooadd обратного DNS прокси-сервера правила.

При создании зоны обратного просмотра DNS, hello сценарий предложит tooenter сети по идентификатору. Этот идентификатор должен быть префикс адреса hello диспетчера ресурсов виртуальной сети. Например если 10.2.0.0/24 адресное пространство подсети виртуальной сети диспетчер ресурсов, введите 10.2.0.0/24 средство hello по запросу для hello сети. 

## <a name="create-hdinsight-cluster"></a>Создание кластера HDInsight
В этом разделе создайте кластер под управлением Linux Hadoop в HDInsight с помощью либо hello портал Azure или [шаблона Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Для других методов создания кластера и см. в основные сведения о настройке hello, [HDInsight, создания кластеров](hdinsight-hadoop-provision-linux-clusters.md). Дополнительные сведения об использовании диспетчера ресурсов шаблона toocreate Hadoop кластеров в HDInsight, см. в разделе [кластеров создать Hadoop в HDInsight с помощью шаблонов диспетчера ресурсов](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

**Здравствуйте, toocreate кластера HDInsight, присоединенных к домену с помощью портала Azure**

1. Войдите на toohello [портал Azure](https://portal.azure.com).
2. Щелкните **Создать**, **Аналитика** и **HDInsight**.
3. Из hello **кластера HDInsight новый** колонки, введите или выберите hello следующие значения:
   
   * **Имя кластера**: Введите имя кластера для кластера HDInsight, присоединенных к домену hello.
   * **Подписка**. Выберите подписку Azure, используемую для создания этого кластера.
   * **Конфигурация кластера**:
     
     * **Тип кластера**: Hadoop. В настоящее время присоединенный к домену кластер HDInsight поддерживают только кластеры Hadoop.
     * **Операционная система**: Linux.  Присоединенный к домену кластер HDInsight поддерживают только кластеры HDInsight под управлением Linux.
     * **Версия**: Hadoop 2.7.3 (HDI 3.5). Присоединенный к домену кластер HDInsight поддерживает только кластер HDInsight версии 3.5.
     * **Тип кластера**: PREMIUM.
       
       Нажмите кнопку **выберите** toosave hello изменения.
   * **Учетные данные**: Настройка hello учетные данные для пользователя кластера hello и hello пользователя SSH.
   * **Источник данных**: создать новую учетную запись хранилища или использовать существующую учетную запись хранения, как hello учетной записи хранения по умолчанию для кластера HDInsight hello. расположение Hello должен hello равна hello двух виртуальных сетей.  расположение Hello также является местоположением hello hello кластера HDInsight.
   * **Цены**: выберите hello число рабочих узлов кластера.
   * **Advanced configurations** (Расширенные настройки): 
     
     * **Domain-joining & Vnet/Subnet** (Присоединение к домену, виртуальная сеть и подсеть): 
       
       * **Параметры домена**: 
         
         * **Доменное имя**: contoso.onmicrosoft.com.
         * **Имя пользователя в домене**. Введите имя пользователя домена. Этот домен должен иметь следующие права hello: домену машины toohello и помещать их в подразделение hello ранее; Создавать субъекты-службы в пределах hello организационное подразделение, настроенных ранее; Создайте обратной записи DNS. Этот пользователь домена станет Здравствуйте, администратор этого кластера HDInsight, присоединенных к домену.
         * **Пароль домена**: Введите пароль пользователя домена hello.
         * **Организационное подразделение**: введите различающееся имя Подразделения, ранее hello hello. Например, OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com.
         * **LDAPS URL** (URL-адрес LDAPS): ldaps://contoso.onmicrosoft.com:636.
         * **Группа доступа пользователей**: hello группы безопасности пользователей, которых необходимо указать toosync toohello кластера. Например, HiveUsers.
           
           Нажмите кнопку **выберите** toosave hello изменения.
           
           ![Настройка параметров домена на портале для присоединенного к домену кластера HDInsight](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * **Виртуальная сеть**: contosohdivnet.
       * **Подсеть**: Subnet1.
         
         Нажмите кнопку **выберите** toosave hello изменения.        
         Нажмите кнопку **выберите** toosave hello изменения.
   * **Группа ресурсов**: hello выберите группы ресурсов, используемой для hello HDInsight виртуальной сети (contosohdirg).
4. Щелкните **Создать**.  

Другой вариант для создания кластера HDInsight, присоединенных к домену — шаблон toouse управления ресурсами Azure. Hello следующая процедура показывает, как:

**toocreate кластера HDInsight, присоединенных к домену, с помощью шаблона управление ресурсами**

1. Щелкните hello, следуя tooopen образ шаблона диспетчера ресурсов в hello портал Azure. шаблон диспетчера ресурсов Hello находится в большой двоичный объект открытого контейнера. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure-use-powershell/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Из hello **параметры** колонке введите hello следующие значения:
   
   * **Подписка**. Выберите подписку Azure.
   * **Группа ресурсов**: щелкните **использовать существующие**и укажите hello одну группу ресурсов, которые вы используете.  Например, contosohdirg. 
   * **Расположение**. Укажите расположение группы ресурсов.
   * **Имя кластера**: Введите имя для кластера Hadoop hello, который будет создан. Например, contosohdicluster.
   * **Тип кластера**. Выберите тип кластера.  значение по умолчанию Hello — **hadoop**.
   * **Расположение**: выберите расположение для hello кластера.  Hello по умолчанию учетной записи хранения, использует hello местоположения.
   * **Число рабочих узлов кластера**: выберите hello число узлов рабочих ролей.
   * **Имя входа и пароль кластера**: имя для входа по умолчанию hello **администратора**.
   * **SSH имя пользователя и пароль**: имя пользователя по умолчанию hello **sshuser**.  Это имя можно изменить. 
   * **Код виртуальной сети**: /subscriptions/&lt;идентификатор_подписки>/resourceGroups/&lt;имя_группы_ресурсов>/providers/Microsoft.Network/virtualNetworks/&lt;имя_виртуальной сети>.
   * **Подсеть виртуальной сети**: /subscriptions/&lt;идентификатор_подписки>/resourceGroups/&lt;имя_группы_ресурсов>/providers/Microsoft.Network/virtualNetworks/&lt;имя_виртуальной сети>/subnets/Subnet1.
   * **Доменное имя**: contoso.onmicrosoft.com.
   * **Organization Unit DN** (Различающееся имя подразделения): OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com.
   * **Cluster Users Group D Ns** (Различающиеся имена группы пользователей кластера): "\"CN=HiveUsers,OU=AADDC Users,DC=<DomainName>,DC=onmicrosoft,DC=com\"".
   * **LDAPUrls** (URL-адреса LDAPS): ["ldaps://contoso.onmicrosoft.com:636"].
   * **DomainAdminUserName**: (ввод hello домена имя пользователя администратора)
   * **DomainAdminPassword**: (введите пароль пользователя admin hello домена)
   * **Я принимаю условия, указанных выше, toohello**: (проверить)
   * **ПИН-код toodashboard**: (проверить)
3. Щелкните **Приобрести**. Вы увидите новый элемент под названием **Развертывание для развертывания шаблона**. Это занимает около toocreate около 20 минут кластера. После создания кластера hello hello кластера колонки в hello портала tooopen можно щелкнуть его.

После завершения учебника hello, может потребоваться toodelete hello кластера. В случае с HDInsight ваши данные хранятся в службе хранилища Azure, что позволяет безопасно удалить неиспользуемый кластер. Плата за кластеры HDInsight взимается, даже когда они не используются. Поскольку плата hello для кластера hello много раз больше, чем hello плата за хранилище, экономически выгодно toodelete кластеры, когда они не используются. Hello инструкции удаления кластера см. в разделе [кластеров управление Hadoop в HDInsight с помощью hello портал Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Дальнейшие действия

* Сведения о настройке политик Hive и выполнении запросов Hive для присоединенного к домену кластера HDInsight см. [здесь](hdinsight-domain-joined-run-hive.md).
* С помощью кластеров HDInsight присоединенных tooDomain tooconnect SSH, в разделе [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

