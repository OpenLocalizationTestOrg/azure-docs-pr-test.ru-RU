---
title: "aaaOverview виртуальных машин Linux в Azure | Документы Microsoft"
description: "Здесь описываются вычислительные и сетевые ресурсы, а также ресурсы хранения, доступные для виртуальных машин Linux в Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: rickstercdn
manager: timlt
editor: 
ms.assetid: 7965a80f-ea24-4cc2-bc43-60b574101902
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/14/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 958e219d53026d787a7a41f2fd13c29c739a9238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux"></a>Azure и Linux
Microsoft Azure — это расширяющийся набор интегрированных общедоступных облачных служб, которые включают в себя возможности анализа, работы с виртуальными машинами и базами данных, мобильные средства, веб-технологии, а также возможности работы в сети и хранения данных &mdash; все для размещения ваших решений.  Microsoft Azure предоставляет масштабируемые вычислительная платформа, позволяющая tooonly оплаты по мере использования, если эти - без необходимости tooinvest локального оборудования.  Azure готова, если являются tooscale решениях вверх и ожидания toowhatever шкалы требуются tooservice hello потребностей клиентов.

Здравствуйте различные возможности Amazon, если вы знакомы с AWS, можно изучить hello Azure vs AWS [документ сопоставления определения](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/).

## <a name="regions"></a>регионы
Ресурсы Microsoft Azure, распространяются на нескольких географических регионах по всему Здравствуй, мир.  Под "регионом" подразумевается несколько центров обработки данных в отдельном географическом регионе.  У нас есть 34 областей, обычно доступных вокруг Здравствуй, мир! с других регионах 4 было объявлено. Поскольку мы продолжаем tooexpand нашей глобального покрытие - мы вести обновленный список существующих и вновь объявила о регионах.

* [Регионы Azure](https://azure.microsoft.com/regions/)

## <a name="availability"></a>Доступность
Мы объявили о отрасли начальные один экземпляр виртуальной машине соглашение об уровне обслуживания 99,9%, если развертывание hello виртуальной Машины с хранилищем premium для всех дисков.  В порядке для вашего развертывания tooqualify для наших стандартные 99,95% соглашение об уровне обслуживания виртуальных Машин необходимо toodeploy двух или более виртуальных машин, запущенных внутри группы доступности рабочей нагрузки. Таким образом виртуальные машины распределяются по несколькими доменам сбоя в центрах обработки данных, а также развертываются на узлах с разными периодами обслуживания. Полный Hello [соглашения об уровне ОБСЛУЖИВАНИЯ Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) объясняет hello гарантируется доступность Azure в целом.

## <a name="managed-disks"></a>Управляемые диски

Управляемые диски дескрипторы хранилища Azure учетных записей, создания и управления в фоновом режиме hello для вас и гарантирует, что у вас tooworry об ограничениях масштабируемости hello hello учетной записи хранения. Просто укажите размер диска hello и уровня производительности hello (Standard или Premium) и Azure создает и управляет hello диска. Даже в том случае, если добавить диски или увеличение и уменьшение масштаба hello виртуальной Машины, у вас нет tooworry о используется хранилище hello. При создании новых виртуальных машин, [использовать hello Azure CLI 2.0](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или hello Azure портала toocreate виртуальных машин с управляемых ОС и дисков данных. Если имеются виртуальные машины с дисками неуправляемые, вы можете [преобразовать вашей toobe виртуальных машин, управляемых дисков в резервные](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Можно управлять пользовательских образов в одну учетную запись хранения в одном регионе Azure и использовать их toocreate сотен виртуальных машин в hello одной подписке. Дополнительные сведения о дисках управляемых см. в разделе hello [Обзор управляемых дисков](../windows/managed-disks-overview.md).

## <a name="azure-virtual-machines--instances"></a>Виртуальные машины Azure и экземпляры
Microsoft Azure поддерживает различные дистрибутивы Linux, которые предоставляются и обслуживаются партнерами.  Вы найдете распределения, например Red Hat Enterprise, CentOS, Debian, Ubuntu, CoreOS, RancherOS, FreeBSD и многое другое в Azure Marketplace hello. Мы активно работаем различных tooadd сообщества Linux еще больше разновидности toohello [Azure одобренных дистрибутивы Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) списка.

Если ваш предпочитаемый дистрибутив Linux, по выбору не существует в коллекции hello, можно «восстановить собственные Linux» виртуальная машина по [Создание и отправка виртуального жесткого диска Linux в Azure](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Виртуальные машины Azure позволяют toodeploy широкий спектр решений вычислительных систем agile способом. Вы можете развернуть практически любую рабочую нагрузку, используя любой язык на практически любой ОС, включая Windows, Linux или пользовательскую (на основе решений наших многочисленных партнеров). По-прежнему не нашли подходящий образ?  Не волнуйтесь, вы также можете перенести свои собственные образы из локальных сред.

## <a name="vm-sizes"></a>Размеры виртуальных машин
При развертывании виртуальной Машины в Azure, вы собираетесь tooselect размер виртуальной Машины в одной серии размеры, подходящий tooyour рабочей нагрузки. Hello размер также влияет на hello вычислительных мощностей, памяти и емкость хранилища hello виртуальной машины. Взимается плата hello объем времени hello виртуальная машина работает и использования его ресурсов. Вы можете ознакомиться с полным списком [размеров виртуальных машин](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Ниже приведены основные рекомендации по выбору подходящего размера виртуальной машины (A, D, DS, G и GS).
* Виртуальные машины серии A — это недорогие виртуальные машины начального уровня для небольших рабочих нагрузок и несложных сценариев разработки и тестирования. Они широко доступны во всех регионах и можно подключиться и использовать все стандартные ресурсы доступны toovirtual машины.
* Размеры виртуальных машин A8–A11 предназначены для кластерных приложений с высокопроизводительными вычислениями.
* Виртуальные машины серии D, разработанные toorun приложений, требующих высокой вычислительной мощности и производительности временного диска. Виртуальные машины серии D предоставляют более быстрые процессоры, более высокий коэффициент памяти для ядра и твердотельный накопитель (SSD) для временного диска hello.
* Серии Dv2 hello последнюю версию серии D, функции более мощных ЦП. Hello серии Dv2 ЦП — около 35% быстрее, чем hello серии D ЦП. Он основан на hello поколения 2,4 ГГц Intel® Xeon® E5-2673 v3 процессора (Haskell) и с hello Boost технология Intel оборотов 2.0, можно перейти вверх too3.2 ГГц. Hello Dv2 ряда имеет hello и те же конфигурации памяти и диска, как hello серии D.
* Виртуальные машины серии G предлагают наибольший объем памяти hello и запустите на узлах, которые имеют семейство процессоров Intel Xeon E5 V3.

Примечание: Серии DS и виртуальные машины серии GS имеют доступ tooPremium хранилища — нашей SSD резервного хранилища высокой производительности и малой задержкой для рабочих нагрузок с большим объемом операций ввода-вывода. Хранилище класса Premium доступно в определенных регионах. Дополнительные сведения см. в статье:

* [Хранилище Premium: высокопроизводительное хранилище для рабочих нагрузок виртуальных машин Azure](../../storage/common/storage-premium-storage.md)

## <a name="automation"></a>Служба автоматизации
tooachieve правильную DevOps языка и региональных параметров, все инфраструктуры должен быть код.  Когда все hello инфраструктуры живет в коде, его можно легко воссоздать (Финиксе серверы).  Azure работает для всех основных автоматизации hello средства, такие как Ansible, Chef, SaltStack и Puppet.  Кроме того, в Azure имеются собственные средства автоматизации:

* [Шаблоны Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json);
* [Azure VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

В Azure вводится поддержка пакета [cloud-init](http://cloud-init.io/) для большинства дистрибутивов Linux, которые поддерживают его.  В настоящее время разворачиваются виртуальные машины Ubuntu Canonical, в которых пакет cloud-init включен по умолчанию.  RHEL шляпы красный, CentOS и Fedora поддерживает облако init, однако hello Azure обслуживается RedHat образы имеют облака init установлен.  toouse облака инициализацией RedHat семейство ОС, необходимо создать пользовательский образ с облака init установлен.

* [Использование cloud-init на виртуальных машинах Linux в Azure](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quotas"></a>Квоты
Каждая подписка Azure имеет квоту по умолчанию в месте, которое может повлиять на развертывание hello большое число виртуальных машин для проекта. Привет текущее ограничение на каждой подписки — 20 виртуальных машин в одном регионе.  Чтобы быстро увеличить квоту, следует отправить соответствующий запрос в службу поддержки.  Дополнительные сведения об ограничениях квоты:

* [Подписка Azure, границы, квоты и ограничения службы](../../azure-subscription-service-limits.md)

## <a name="partners"></a>Партнеры
Корпорация Майкрософт работает в тесном сотрудничестве с партнерами tooensure hello образы, имеющиеся обновления и оптимизирован для среды выполнения Azure.  С дополнительными сведениями о наших партнерах можно ознакомиться на приведенных ниже страницах Marketplace.

* Linux в Azure — [рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* SUSE — [Azure Marketplace — SUSE Linux Enterprise Server](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=%27SUSE%27)
* Redhat — [Azure Marketplace — RedHat Enterprise Linux 7.2](https://azure.microsoft.com/marketplace/partners/redhat/redhatenterpriselinux72/)
* Canonical — [Azure Marketplace — Ubuntu Server 16.04 LTS](https://azure.microsoft.com/marketplace/partners/canonical/ubuntuserver1604lts/)
* Debian — [Azure Marketplace — Debian 8 "Jessie"](https://azure.microsoft.com/marketplace/partners/credativ/debian8/)
* FreeBSD — [Azure Marketplace —FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
* CoreOS — [Azure Marketplace —CoreOS (стабильная версия)](https://azure.microsoft.com/marketplace/partners/coreos/coreosstable/)
* RancherOS — [Azure Marketplace —RancherOS](https://azure.microsoft.com/marketplace/partners/rancher/rancheros/)
* Bitnami — [Bitnami Library для Azure](https://azure.bitnami.com/)
* Mesosphere — [Azure Marketplace — Mesosphere DC/OS в Azure](https://azure.microsoft.com/marketplace/partners/mesosphere/dcosdcos/)
* Docker — [Azure Marketplace — служба контейнеров Azure с Docker Swarm](https://azure.microsoft.com/marketplace/partners/microsoft/acsswarms/)
* Jenkins — [Azure Marketplace — платформа CloudBees Jenkins](https://azure.microsoft.com/marketplace/partners/cloudbees/jenkins-platformjenkins-platform/)

## <a name="getting-started-with-linux-on-azure"></a>Приступая к работе с Linux в Azure
toobegin с помощью Azure требуется учетная запись Azure, hello Azure CLI установлен и пару открытого и закрытого ключей SSH.

### <a name="sign-up-for-an-account"></a>Регистрация учетной записи
Первым шагом Hello в с помощью hello облако Azure является toosign для использования учетной записи Azure.  Go toohello [получить учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/) страница tooget работы.

### <a name="install-hello-cli"></a>Установить CLI hello
С вашей новой учетной записи Azure вы можете начать немедленно с помощью hello Azure портала — это панель администрирования веб сервера.  hello toomanage облако Azure через hello командной строки, установите hello `azure-cli`.  Установка hello [Azure CLI 2.0](/cli/azure/install-azure-cli) на рабочей станции Mac или Linux.

### <a name="create-an-ssh-key-pair"></a>Создание пары ключей SSH
Теперь у вас учетная запись Azure, hello Azure веб-портале и hello Azure CLI.  Hello следующим шагом является toocreate пару ключей SSH, используемые tooSSH в Linux, не с помощью пароля.  [Создание ключей SSH в Linux и Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooenable имена входа без пароля и более высокий уровень безопасности.

### <a name="create-a-vm-using-hello-cli"></a>Создайте виртуальную Машину с помощью hello CLI
Создание виртуальной Машины Linux hello CLI с помощью — быстро toodeploy виртуальной Машины, не покидая hello терминалов вы работаете в.  Все, что можно указать на веб-портале hello доступна через флага командной строки или коммутатора.  

* [Создайте виртуальную Машину Linux с помощью hello CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="create-a-vm-in-hello-portal"></a>Создание виртуальной Машины на портале hello
Создание виртуальной Машины Linux hello Azure веб-портале — это способ tooeasily точки и просмотрите hello развертывания tooa tooget различные параметры.  Вместо использования командной строки флаги и коммутаторов, являются tooview возможности работы с низким приоритетом веб-макет из различных параметров и настроек.  Все компоненты доступны через интерфейс командной строки hello доступна на портале hello.

* [Создайте виртуальную Машину Linux с помощью портала hello](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="login-using-ssh-without-a-password"></a>Вход по протоколу SSH без пароля
Hello виртуальной Машины, теперь работает на Azure и будут готовы toolog в.  С помощью toolog пароли в через SSH небезопасен и требующим много времени.  Использование ключей SSH Здравствуйте, самым безопасным способом, а также самый быстрый способ toologin hello.  Когда вы создаете ВМ Linux через портал hello или hello CLI, имеется два варианта проверки подлинности.  Если выбрать пароль для SSH, Azure настраивает hello ВМ tooallow входа через пароли.  Если вы выбрали toouse открытый ключ SSH, Azure настраивает hello ВМ tooonly разрешить вход через SSH ключам и отключает имена входа пароль. ВМ Linux, только учетные записи ключа SSH, что позволяет использовать toosecure hello SSH параметра открытого ключа во время создания виртуальной Машины на портале hello или CLI hello.

## <a name="related-azure-components"></a>Связанные компоненты Azure
## <a name="storage"></a>Хранилище
* [Введение tooMicrosoft хранилища Azure](../../storage/common/storage-introduction.md)
* [Добавить диск tooa виртуальных Машин Linux с помощью hello azure-cli](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Как tooattach данных на диске tooa виртуальных Машин Linux в hello портал Azure](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Сеть
* [Обзор виртуальной сети](../../virtual-network/virtual-networks-overview.md)
* [IP-адреса в Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)
* [Открытие портов tooa виртуальных Машин Linux в Azure](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Создание полного доменного имени в hello портал Azure](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="containers"></a>Контейнеры
* [Виртуальные машины и контейнеры в Azure](containers.md)
* [Общие сведения о службе контейнеров Azure](../../container-service/container-service-intro.md)
* [Развертывание кластера службы контейнеров Azure](../../container-service/dcos-swarm/container-service-deployment.md)

## <a name="next-steps"></a>Дальнейшие действия
Вы ознакомились с общими сведениями об использовании Linux в Azure.  Следующий шаг Hello toodive в и создать несколько виртуальных машин!

* [См. наш обновляемый список с примерами скриптов для выполнения стандартных задач с помощью Azure CLI](cli-samples.md)
