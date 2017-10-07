---
title: "aaaDeploy вашего первого приложения tooCloud Foundry в Microsoft Azure | Документы Microsoft"
description: "Развертывание приложения tooCloud Foundry в Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a>Развертывание вашего первого приложения tooCloud Foundry в Microsoft Azure

[Cloud Foundry](http://cloudfoundry.org) — это популярная платформа приложений с открытым кодом в Microsoft Azure. В этой статье показано, как toodeploy и управлять ими на Foundry облачные приложения в среду Azure.

## <a name="create-a-cloud-foundry-environment"></a>Создание среды Cloud Foundry

Существует несколько способов создания среды Cloud Foundry в Azure.

- Используйте hello [предложение жизненно важную Foundry облака] [ pcf-azuremarketplace] в Azure Marketplace hello toocreate стандартной среды, которые включают диспетчер Ops PCF и hello Azure Service Broker. Можно найти [завершения инструкции] [ pcf-azuremarketplace-pivotaldocs] развертывания hello marketplace предложить в hello жизненно важную документацию.
- Создайте пользовательскую среду, [развернув Pivotal Cloud Foundry вручную][pcf-custom].
- [Развертывание пакетов Foundry облака открытая hello непосредственно] [ oss-cf-bosh] , настроив [BOSH](http://bosh.io) директора виртуальной Машины, которая координирует развертывания hello hello Foundry облачной среды.

> [!IMPORTANT] 
> При развертывании PCF из hello Azure Marketplace, запишите hello SYSTEMDOMAINURL и требуемые учетные данные администратора hello tooaccess hello жизненно важную Диспетчер приложений, которые описаны в руководстве по развертыванию marketplace hello. Они имеют необходимые toocomplete этого учебника. Для развертываний marketplace hello SYSTEMDOMAINURL находится в форме https://system hello. *IP-адрес*. cf.pcfazure.com.

## <a name="connect-toohello-cloud-controller"></a>Подключение toohello контроллера облака

Hello контроллера облака — hello первичная запись точки tooa Foundry облачной среды для развертывания и управления приложениями. Hello core API контроллера облака (CCAPI) представляет собой API REST, однако он доступен с помощью различных средств. В этом случае мы взаимодействуют с его помощью hello [CLI Foundry облака][cf-cli]. Можно установить на Windows, Linux, MacOS или hello CLI, но если вы предпочитаете не tooinstall, он будет доступен предварительно установленных в hello [оболочки облако Azure][cloudshell-docs].

toolog в начале `api` toohello SYSTEMDOMAINURL, полученный из развертывания marketplace hello. Поскольку развертывание по умолчанию hello использует самозаверяющий сертификат, следует также добавить hello `skip-ssl-validation` переключения.

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

Все запрашиваемые toolog в toohello контроллера облака. Используйте hello учетных данных администратора, полученные из шагов развертывания marketplace hello.

Предоставляет облачные Foundry *организаций* и *пробелы* как пространства имен tooisolate hello групп и сред в рамках общего развертывания. Hello PCF marketplace развертывания включает по умолчанию hello *системы* организации и набор областей создания toocontain hello базовые компоненты, как автоматическое масштабирование службы hello и hello Azure service broker. Теперь нажмите кнопку hello *системы* пространства.


## <a name="create-an-org-and-space"></a>Создание организации и пространства

Если ввести `cf apps`, вы видите набор приложений системы, которые были развернуты в пространстве системы hello в системе org. hello 

Необходимо хранить hello *системы* организации, зарезервированных для приложений системы, таким образом создать toohouse организации и пространство приложении образца.

```bash
cf create-org myorg
cf create-space dev -o myorg
```

Используйте hello целевой команда tooswitch toohello новой организации и пространства:

```bash
cf target -o testorg -s dev
```

Теперь при развертывании приложения, он автоматически создается в новой организации hello и пространства. Введите tooconfirm, который в настоящее время нет приложений в новой организации hello дискового пространства, `cf apps` еще раз.

> [!NOTE] 
> Дополнительные сведения о организаций и пробелы и как они могут использоваться для управления доступом на основе ролей (RBAC) см. в разделе hello [документации Foundry облака][cf-orgs-spaces-docs].

## <a name="deploy-an-application"></a>Развертывание приложения

Используем образец приложения Foundry облака, вызывается Hello Spring облака, который написан на языке Java и основании hello [Spring Framework](http://spring.io) и [Spring загрузки](http://projects.spring.io/spring-boot/).

### <a name="clone-hello-hello-spring-cloud-repository"></a>Клонирование репозитория облака Spring Hello hello

Образец Hello Spring облачные приложения Hello можно найти в GitHub. Клонирует его tooyour среды и преобразовать в новый каталог hello:

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a>Создание приложения hello

С помощью приложения hello построения [Apache Maven](http://maven.apache.org).

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a>Развертывание приложения hello с принудительной отправкой cf

Большинство приложений tooCloud Foundry можно развернуть с помощью hello `push` команды:

```bash
cf push
```

Когда вы *принудительной* Foundry облачные приложения, определяет тип hello приложения (в данном случае приложение Java) и определяет его зависимости (в это случае framework Spring hello). Затем он упаковывает все необходимые toorun кода в автономный образ контейнера, известный как *дроплета*. Наконец расписания Foundry облака hello приложения на одном hello доступных компьютеров в вашей среде и создает URL-адрес, где можно получить доступ, который доступен в hello выходные данные команды hello.

![Выходные данные команды cf push][cf-push-output]

приложение hello spring облако hello toosee, откройте hello предоставленный URL-адрес в браузере:

![Пользовательский интерфейс по умолчанию для приложения Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> toolearn Дополнительные сведения о том, что происходит во время `cf push`, в разделе [как поэтапно приложений] [ cf-push-docs] в hello документации Foundry облака.

## <a name="view-application-logs"></a>Просмотр журналов приложения

Можно использовать журналы tooview hello облака Foundry CLI для приложения по имени:

```bash
cf logs hello-spring-cloud
```

По умолчанию hello журналы команда с помощью *заключительного*, который демонстрирует новые журналы, записываемые. отображается toosee новые журналы, обновите приложение hello spring облако hello в браузере hello.

tooview журналы, которые уже были записаны, добавить hello `recent` переключения:

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a>Масштабирование приложения hello

По умолчанию команда `cf push` создает только один экземпляр приложения. tooensure высокого уровня доступности и масштабирования включить более высокую пропускную способность, обычно требуется toorun более одного экземпляра приложения. Можно легко масштабировать уже развернутых приложений с помощью hello `scale` команды:

```bash
cf scale -i 2 hello-spring-cloud
```

Выполнение hello `cf app` команда приложения hello показывает, что облачные Foundry создает другой экземпляр приложения hello. После запуска приложения hello Foundry облака автоматически запускает tooit трафика балансировки нагрузки.


## <a name="next-steps"></a>Дальнейшие действия

- [Hello чтения документации Foundry облака][cloudfoundry-docs]
- [Настройка подключаемого модуля Visual Studio Team Services hello для облака Foundry][vsts-plugin]
- [Настройка hello сопел аналитика журналов Microsoft для облака Foundry][loganalytics-nozzle]

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png