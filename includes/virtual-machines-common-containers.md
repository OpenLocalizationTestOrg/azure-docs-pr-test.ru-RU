Облачные решения Azure на основе виртуальных машин(эмуляции оборудования физического компьютера) обеспечивают гибкую упаковку развертывания программного обеспечения и большую эффективность консолидации ресурсов, чем в случае использования физического оборудования. [Docker](https://www.docker.com) контейнеры и hello экосистеме docker имеет значительно развернутой hello способов разработки, поставляемых и управление распределенной программного обеспечения. Код приложения в контейнере изолирован от hello узла виртуальной Машины и другие контейнеры на hello одной виртуальной Машины. Такая изоляция обеспечивает большую гибкость при разработке и развертывании.

Azure предлагает следующие значения Docker hello.

* [Многие](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) [другой](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate способов Docker размещает для контейнеров toosuit вашей ситуации
* Hello [контейнера службы Azure](https://azure.microsoft.com/documentation/services/container-service/) создает кластеры узлов контейнера, например с помощью orchestrators **marathon** и **скапливаются**.
* [Диспетчер ресурсов Azure](../articles/azure-resource-manager/resource-group-overview.md) и [шаблоны группы ресурсов](../articles/resource-group-authoring-templates.md) toosimplify развертывание и обновление сложных распределенных приложений
* интеграцию с большим массивом частных инструментов управления конфигурациями и инструментов управления конфигурациями с открытым исходным кодом.

А поскольку возможность программно создавать виртуальные машины и Linux контейнеры в Azure, можно также использовать ВМ и контейнер *orchestration* средств toocreate группы виртуальных машин (ВМ) и toodeploy приложений в обоих Linux контейнеры и теперь [контейнеры Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

В этой статье описаны не только эти концепции высокого уровня, он также содержит множество ссылок toomore сведения, учебники, и продукты, связанные с использования toocontainer и кластер в Azure. Если вы знаете все это и просто нужно hello ссылки, они здесь, в [средства для работы с контейнерами](#tools-for-working-with-azure-vms-and-containers).

## <a name="hello-difference-between-virtual-machines-and-containers"></a>отличие Hello контейнеров и виртуальные машины
Виртуальные машины работают в изолированной аппаратной среде виртуализации, предоставляемой [гипервизором](http://en.wikipedia.org/wiki/Hypervisor). В Azure, hello [виртуальные машины](https://azure.microsoft.com/services/virtual-machines/) службы обрабатывает все, что для вас: создавать виртуальные машины, выбрав hello операционной системы и настройка &mdash;или путем передачи пользовательского образа виртуальной Машины. Виртуальные машины — это технология проверенное, «последний записал Битва», и можно использовать множество инструментов содержат доступные toomanage hello операционной системы и приложений.  Приложения на виртуальной машине, скрыты от ОС узла hello. С hello точки зрения приложения или пользователя на виртуальной Машине hello виртуальной Машины появится toobe автономной физического компьютера.

[Контейнеры Linux](http://en.wikipedia.org/wiki/LXC) и созданные и размещенных с помощью средства docker, не использующих изоляцию tooprovide низкоуровневой оболочки. С помощью контейнеров узла контейнера hello использует процесс и функции изоляции системы файл hello Linux ядра tooexpose toohello контейнера, его приложений, определенных функций ядра и свой собственный изолированной файловой системы. С hello точки зрения приложения, выполняющиеся внутри контейнера контейнер hello появляется toobe уникальный экземпляр операционной системы. Приложения в контейнере не могут видеть процессы или другие ресурсы за пределами своего контейнера.

В отличие от виртуальной машины, в контейнере Docker используется гораздо меньше ресурсов. Контейнеры docker использовать изоляцию и выполнения модели приложения, которой не поддерживает совместное использование hello ядро узла Docker hello. Hello контейнер имеет гораздо ниже дискового пространства, оно содержит hello всей операционной системы. Кроме того, он использует гораздо меньше места на диске и требует меньше времени для запуска, чем виртуальная машина.
Контейнеры Windows обеспечивают hello же преимущества как контейнеры Linux для приложений, работающих под управлением Windows. Контейнеры Windows поддерживают формат изображения Docker hello и Docker API, но они также можно управлять с помощью PowerShell. Для работы с контейнерами Windows, Windows Server и Hyper-V доступны две среды выполнения. Контейнеры Hyper-V обеспечивают дополнительный уровень защиты, так как каждый контейнер размещается на сверхоптимизированной виртуальной машине. см. Дополнительные сведения о контейнерах Windows toolearn [о контейнерах Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview). tooget работы с контейнерами Windows в Azure, узнайте, как слишком[развертывание кластера службы контейнера Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).

## <a name="what-are-containers-good-for"></a>Для чего же контейнеры подходят лучше всего?

Контейнеры могут улучшить следующие показатели:

* код приложения Hello скорость разработки и свободно распространять
* скорость Hello и достоверности, которые можно протестировать приложение
* скорость Hello и достоверности, которые можно развернуть приложение

Контейнеры выполняются на узле контейнеров (в операционной системе), и в Azure это означает виртуальную машину Azure. Даже в том случае, если уже лучшее представление hello контейнеров, по-прежнему ты tooneed инфраструктуры виртуальных Машин, размещения hello контейнеров, но преимущества hello, что контейнеры не обращают внимания на какие виртуальных Машин они работают (хотя ли контейнер hello хочет Linux или Windows Среда выполнения будет важно, например).


## <a name="what-are-containers-good-for"></a>Для чего же контейнеры подходят лучше всего?
Они отлично подходит для многих вещах, но они стимулировать&mdash;как [облачных служб Azure](https://azure.microsoft.com/services/cloud-services/) и [Azure Service Fabric](../articles/service-fabric/service-fabric-overview.md)&mdash;hello Создание одна служба, ориентированных на микрослужбу распределенные приложения в приложение, в котором архитектура основана на несколько частей небольшой, составное вместо крупных и более надежно соединенного компонентов.

Это особенно важно в общедоступном облаке, например в Azure, где можно сдавать виртуальные машины там, где нужно, и тогда, когда нужно. Вы получаете не только изоляцию, быстрое развертывание и инструменты оркестрации, но и можете создавать более эффективные решения для инфраструктуры приложений.

Например, у вас есть развертывание, состоящее из 9 виртуальных машин Azure большого размера для высокодоступного распределенного приложения. Если hello компоненты этого приложения может быть развернут в контейнерах, может быть toouse может только 4 виртуальных машин и развертывать компоненты приложения внутри 20 контейнеров для резервирование и балансировку нагрузки.

Это лишь пример, конечно, но для этого в сценарий, настройте пики toousage с несколько контейнеров, а не больше виртуальных машин Azure и использовать hello оставшихся общую нагрузку ЦП гораздо более эффективно, чем ранее.

Кроме того существует множество сценариев, которые не подходят подход микрослужбами tooa; Вы будете знать, оптимально ли микрослужбами и контейнеры помогут.

### <a name="container-benefits-for-developers"></a>Преимущества контейнеров для разработчиков
Как правило это просто toosee, что технология контейнера — это шаг вперед, но существуют также дополнительные преимущества. Рассмотрим пример hello контейнеры Docker. В этом разделе будет не провести детальное Docker в данный момент (чтение [возможности Docker?](https://www.docker.com/whatisdocker/) для этой истории или [Википедии](http://wikipedia.org/wiki/Docker_%28software%29)), но Docker и ее экосистема предоставляют значительные преимущества tooboth разработчикам и ИТ специалистов.

Разработчикам быстро, Уделите tooDocker контейнеров, так как над всеми упрощает использование контейнеров Linux и Windows легко.

* Их можно использовать простые, добавочное команды toocreate основных образ, который является простым toodeploy и автоматизировать построения этих образов с помощью dockerfile
* Они могут использовать эти образы, легко с помощью простого, [git](https://git-scm.com/)-стиля push и pull команды слишком[открытый](https://registry.hub.docker.com/) или [реестров закрытый docker](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Они могут использовать изолированные компоненты приложений вместо компьютеров.
* Они могут использовать большое количество инструментов, которые понимают контейнеры Docker и различные основные образы.

### <a name="container-benefits-for-operations-and-it-professionals"></a>Преимущества контейнеров для производственных и ИТ-специалистов
ИТ и операций специалисты также могут использовать сочетание hello контейнеров и виртуальных машин.

* Службы в контейнерах изолируются от среды выполнения узла виртуальной машины.
* Код в контейнерах идентичен, и это можно проверить.
* Службы в контейнерах можно запускать, останавливать и быстро перемещать между средами разработки, тестирования и рабочей средой.

Такие компоненты, как они&mdash;и имеются дополнительные&mdash;excite установленного организаций, где служебные сведения технологии организации имеют задания hello подгонки ресурсов&mdash;включая вычислительную мощность&mdash; требуется toonot toohello задачи только оставаться в бизнесе, но повысить степень удовлетворенности и достичь. Предприятий малого бизнеса, независимые поставщики программного обеспечения и их запуску имеют точно hello же требование, но они могут описывать это по-разному.

## <a name="what-are-virtual-machines-good-for"></a>Какие виртуальные машины подходят лучше всего?
Виртуальные машины предоставляют магистрали hello облачных вычислений и, не изменяется. Если виртуальные машины запуск медленнее, занимают больше места на диске и не сопоставлены напрямую tooa микрослужбами архитектуры, они имеют очень важные преимущества:

1. по умолчанию они обладают гораздо более надежной защитой для узла;
2. они поддерживают все основные операционные системы и конфигурации приложений;
3. они оснащены проверенными временем экосистемами инструментов управления;
4. Они предоставляют контейнеры toohost среды выполнения hello

последний элемент Hello важен, поскольку автономные приложения по-прежнему требует определенной операционной системой и типе ЦП, в зависимости от того hello вызовов, выполняемых сделает приложения hello. Это важные tooremember установить контейнеров на виртуальных машинах, из-за наличия hello приложения toodeploy; контейнеры не являются заменой виртуальных машин или операционных систем.

## <a name="high-level-feature-comparison-of-vms-and-containers"></a>Сравнение основных функций виртуальных машин и контейнеров
Hello следующей таблице описаны в очень высокая уровня hello вида функция различия,&mdash;без дополнительных усилий&mdash;существует между виртуальными машинами и Linux контейнеров. Обратите внимание, что некоторые функции может быть более или менее желательно зависимости приложения должен, как и все программное обеспечение, дополнительная работа предоставления увеличить поддержка функций, особенно в области безопасности hello.

| Функция | Виртуальные машины | Контейнеры |
|:--- | --- | --- |
| Поддержка безопасности «по умолчанию» |повышенный tooa |tooa немного меньшей степени |
| Требуется память на диске |Полная версия ОС и приложения |Только требования приложений |
| Время, затраченное toostart |Значительно дольше: загрузка ОС и приложений |Значительно короче: только для приложений требуется toostart, так как уже выполняется ядра |
| Переносимость |Переносимость при правильной подготовке |Переносимость в формате образа, обычно ниже |
| Автоматизация образов |Зависит от ОС и приложений |[Реестр Docker](https://registry.hub.docker.com/)и другие |

## <a name="creating-and-managing-groups-of-vms-and-containers"></a>Создание групп виртуальных машин и контейнеров и управление ими
На этом этапе любой архитектор, разработчик, производственный или ИТ-специалист может подумать, что можно ВСЕ это автоматизировать — ведь это НАСТОЯЩИЙ «ЦОД как служба».

Правильно, она может быть и существует несколько систем, многие из которых можно использовать, можно управлять группами виртуальных машин Azure и внедрить пользовательский код, с помощью скриптов, часто с hello [CustomScriptingExtension для Windows](https://msdn.microsoft.com/library/azure/dn781373.aspx) или Hello [CustomScriptingExtension для Linux](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/). Вы можете автоматизировать развертывание Azure (и возможно, вы уже сделали это) с помощью сценариев PowerShell или интерфейса командной строки Azure.

Чаще всего эти возможности, а затем как перенесенных tootools [Puppet](https://puppetlabs.com/) и [Chef](https://www.chef.io/) tooautomate Здравствуйте, создание и настройка для виртуальных машин в масштабе. (Вот некоторые ссылки слишком[с помощью этих средств, с помощью Azure](#tools-for-working-with-containers).)

### <a name="azure-resource-group-templates"></a>Шаблоны групп ресурсов Azure
В последнее время Azure выпустила hello [управления ресурсами Azure](../articles/resource-manager-deployment-model.md) REST API и обновленные toouse средства Azure CLI и PowerShell его легко. Развертывание, изменения или повторного развертывания всего приложения топологий, с помощью [шаблоны Azure Resource Manager](../articles/resource-group-authoring-templates.md) с использованием API управления hello ресурсов Azure:

* Hello [портал Azure с помощью шаблонов](https://github.com/Azure/azure-quickstart-templates)&mdash;подсказку, нажмите кнопку «DeployToAzure» hello
* Hello [Azure CLI](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="deployment-and-management-of-entire-groups-of-azure-vms-and-containers"></a>Развертывание всей группы виртуальных машин Azure и контейнеров и управление ими
Существует несколько популярных систем, которые позволяют развертывать целые группы виртуальных машин и устанавливать Docker (или другие узлы контейнеров Linux) в виде автоматизируемой группы. Прямые ссылки в разделе hello [контейнеров и средства](#containers-and-vm-technologies) ниже статьи. Существует несколько систем, которые выполняют этого экстента tooa большего или меньшего, и этот список не является исчерпывающим. В зависимости от доступных навыков и сценариев, они могут быть или не быть полезными.

У Docker есть собственный набор инструментов для создания виртуальных машин ([Docker machine](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) и инструмент управления кластерами контейнеров Docker с балансировкой нагрузки ([Swarm](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Здравствуйте, кроме того, [расширения виртуальной Машины Azure Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) с поддержкой по умолчанию [ `docker-compose` ](https://docs.docker.com/compose/), который можно развернуть настроен контейнеров приложений по нескольким контейнерам.

Вы также можете попробовать ОС [Data Center Operating System (DCOS)](http://docs.mesosphere.com)от Mesosphere. DCOS основан на открытым исходным кодом hello [mesos](http://mesos.apache.org/) «распределенных систем ядра», которая позволяет вам tootreat центра обработки данных как одна служба адресуемый. DCOS оснащена встроенными пакетами для нескольких важных систем, таких как [Spark](http://spark.apache.org/) и [Kafka](http://kafka.apache.org/) (и др.), а также встроенными службами, такими как [Marathon](https://mesosphere.github.io/marathon/) (система управления контейнерами) и [Chronos](https://mesos.github.io/chronos/) (распределенный планировщик). Mesos создан с учетом уроков, полученных при развитии Twitter, AirBnb и других веб-масштабируемых компаний. Можно также использовать **скапливаются** как hello orchestration engine.

Кроме того, [kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/) — это система для управления группами виртуальных машин и контейнеров с открытым исходным кодом, созданная с учетом опыта Google. Можно даже использовать [kubernetes с плетенка сетевой поддержки tooprovide](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave).

[Deis](http://deis.io/overview/) открыта источника «Платформа как служба» (PaaS), позволяет легко toodeploy и управлять приложениями на собственных серверах. Deis строится на Docker и CoreOS tooprovide упрощенных PaaS с обусловлены Heroku рабочего процесса.

[CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html) — это оптимизированный по размеру дистрибутив Linux с поддержкой Docker, собственной системой контейнеров [rkt](https://github.com/coreos/rkt) и инструментом управления группами контейнеров под названием [fleet](https://coreos.com/fleet/docs/latest/).

Ubuntu — другой популярный дистрибутив Linux, который очень хорошо поддерживает Docker и при этом также поддерживает [кластеры Linux (LXC)](https://help.ubuntu.com/lts/serverguide/lxc.html).

## <a name="tools-for-working-with-azure-vms-and-containers"></a>Инструменты для работы с виртуальными машинами и контейнерами Azure
Для работы с контейнерами и виртуальными машинами в Azure используются определенные инструменты. В этом разделе содержит перечень только некоторые из наиболее полезно или важные понятия hello и orchestration средств, используемых с ними и о контейнеров, групп и конфигурации большего hello.

> [!NOTE]
> В этой области изменяется невероятно быстро и пока мы выполним наши рекомендации tookeep в этом разделе и его ссылок вверх toodate, он может иметь задачу невозможно. Убедитесь, что поиск на интересные темы tookeep копирование toodate!
>
>

### <a name="containers-and-vm-technologies"></a>Технологии контейнеров и виртуальных машин
Некоторые технологии контейнеров Linux:

* [Docker](https://www.docker.com)
* [LXC](https://linuxcontainers.org/)
* [CoreOS и rkt](https://github.com/coreos/rkt)
* [Open Container Project](http://opencontainers.org/)
* [RancherOS](http://rancher.com/rancher-os/)

Ссылки на контейнеры Windows:

* [Контейнеры Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)

Ссылки на Visual Studio Docker:

* [Инструменты Visual Studio для Docker](https://docs.microsoft.com/en-us/dotnet/core/docker/visual-studio-tools-for-docker)

Инструменты Docker:

* [Управляющая программа Docker](https://docs.docker.com/installation/#installation)
* Клиенты Docker
  * [Клиент Windows Docker на Chocolatey](https://chocolatey.org/packages/docker)
  * [Указания по установке Docker](https://docs.docker.com/installation/#installation)

Docker в Microsoft Azure:

* [Расширение виртуальных машин Docker для Linux в Azure](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Руководство пользователя для Azure Docker VM Extension](https://github.com/Azure/azure-docker-extension/blob/master/README.md)
* [С помощью hello расширение ВМ Docker из hello Azure командной строки (CLI Azure)](../articles/virtual-machines/linux/classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [С помощью hello расширение ВМ Docker из hello портал Azure](../articles/virtual-machines/linux/classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Как toouse-машины docker в Azure](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Как toouse docker с группу мелких объектов в Azure](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Начало работы с решениями Docker и Compose в Azure](../articles/virtual-machines/linux/docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Быстро с помощью toocreate шаблона группы ресурсов Azure узла Docker в Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)
* [Здравствуйте, встроенная поддержка `compose` ](https://github.com/Azure/azure-docker-extension#11-public-configuration-keys) для автономных приложений
* [Реализация закрытого реестра Docker в Azure](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Дистрибутивы Linux и примеры для Azure:

* [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

настройка, управление кластером и оркестрация контейнеров:

* [Fleet в CoreOS](https://coreos.com/fleet/docs/latest/)
* Deis

  * [Завершение развертывания кластера Kubernetes tooautomated руководство с CoreOS и плетенка](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
  * [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Mesos](http://mesos.apache.org/)

  * [Mesosphere Data Center Operating System (DCOS)](https://docs.mesosphere.com/1.7/overview/design/azure-container-service/)
* [Jenkins](https://jenkins.io/) и [Hudson](http://hudson-ci.org/)

  * [Azure VM Agents plugin](https://wiki.jenkins.io/display/JENKINS/Azure+VM+Agents+plugin) (Подключаемый модуль агента виртуальной машины Jenkins для Azure)
  * [Репозиторий GitHub. Подключаемый модуль хранилища Jenkins для Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
  * [Сторонние решения. Подключаемый модуль ведомого режима Hudson для Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
  * [Сторонние решения. Подключаемый модуль хранилища Hudson для Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Служба автоматизации Azure](https://azure.microsoft.com/services/automation/)

  * [Видео: Как tooUse автоматизации Azure с виртуальными машинами Linux](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* Powershell DSC для Linux

  * [Блог: Как toodo Powershell DSC для Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
  * [Github. DSC клиента Docker](https://github.com/anweiss/DockerClientDSC)

## <a name="next-steps"></a>Дальнейшие действия
См. документацию по [Docker](https://www.docker.com) и [контейнерам Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

<!--Anchors-->
[microservices]: http://martinfowler.com/articles/microservices.html
[microservice]: http://martinfowler.com/articles/microservices.html
<!--Image references-->
