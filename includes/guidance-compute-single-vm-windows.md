В этой статье рассматриваются set проверенные методики ОС виртуальной машины (ВМ) Windows Azure, обращая внимание tooscalability, доступности, управляемости и безопасности.

> [!NOTE]
> Azure предоставляет две модели развертывания: с использованием [Azure Resource Manager][resource-manager-overview] и классическую. В этой статье описывается использование модели развертывания c использованием диспетчера ресурсов, которую рекомендует применять для новых развертываний корпорация Майкрософт.
>
>

Мы не рекомендуем использовать одну виртуальную машину для критически важных рабочих нагрузок, так как на ней создается единая точка отказа. Для повышения уровня доступности разверните несколько виртуальных машин в [группе доступности][availability-set]. Дополнительные сведения см. в статье [Running multiple VMs on Azure for scalability and availability][multi-vm] (Запуск нескольких виртуальных машин в Azure для обеспечения масштабируемости и доступности).

## <a name="architecture-diagram"></a>Схема архитектуры

Подготовка виртуальной Машины в Azure включает в себя больше частей, чем просто hello самой ВМ. К таким элементам относятся вычислительные, сетевые ресурсы и ресурсы хранения.

> Документ Visio, включающий это диаграмма архитектуры можно загрузить из hello [центра загрузки Майкрософт][visio-download]. Эта схема находится на hello «Compute - одной виртуальной Машины — страницы.
>
>

![[0]][0]

* **Группа ресурсов.** [*Группа ресурсов*][resource-manager-overview] представляет собой контейнер, содержащий связанные ресурсы. Создайте ресурс hello toohold группы ресурсов для этой виртуальной Машины.
* **Виртуальная машина**. Подготовка виртуальной Машины из списка опубликованные изображения или из файла виртуального жесткого диска (VHD), передаче tooAzure хранилища больших двоичных объектов.
* **Диск ОС.** диск ОС Hello — виртуального жесткого диска, хранящиеся в [хранилища Azure][azure-storage]. Это означает, что он будет повторяться, даже если хост-компьютере hello выходит из строя.
* **Временный диск.** Hello виртуальной Машины создается временный диск (hello `D:` диска в Windows). Этот диск хранится на физическом диске на компьютере размещения hello. Он *не* сохраняется в службе хранилища Azure и может быть удален во время перезагрузки и других событий жизненного цикла виртуальной машины. Используйте этот диск только для временных данных, таких как данные страниц или файлы подкачки.
* **Диски данных.** [Диск данных][data-disk] — это постоянный виртуальный жесткий диск, используемый для хранения данных приложений. Диски данных хранятся в хранилище Azure как диск ОС hello.
* **Виртуальная сеть и подсеть.** Каждая виртуальная машина в Azure развертывается в виртуальной сети, а виртуальные сети разделяются на подсети.
* **Общедоступный IP-адрес.** Общедоступный IP-адрес является необходимые toocommunicate с hello ВМ&mdash;например через удаленный рабочий стол (RDP).
* **Сетевой интерфейс (сетевой адаптер)**. Hello NIC позволяет toocommunicate hello виртуальной Машины с помощью виртуальной сети hello.
* **Группа безопасности сети**. Hello [NSG] [ nsg] — используется tooallow или запретить трафик toohello подсети. Группу безопасности сети можно связать с отдельной сетевой картой или подсетью. Если вы связываете с подсетью, правила NSG hello применяются tooall виртуальных машин в этой подсети.
* **Диагностика.** Сбор данных диагностики важно для управления и устранения неполадок hello виртуальной Машины.

## <a name="recommendations"></a>Рекомендации

для большинства сценариев применения Hello следующих рекомендаций. Следуйте этим рекомендациям, если они не противоречат особым требованиям для вашего случая.

### <a name="vm-recommendations"></a>Рекомендации по виртуальным машинам

Azure предлагает множество различных размеров виртуальной машины, но мы рекомендуем hello и GS-серии DS, так как эти машины размеры поддерживает [хранилище Premium][premium-storage]. Если отсутствует специализированная рабочая нагрузка, например высокопроизводительные вычисления, выберите виртуальную машину одного из этих размеров. Дополнительную информацию см. в статье [Размеры виртуальных машин в Azure][virtual-machine-sizes].

При перемещении существующего tooAzure рабочей нагрузки, начинаются с Привет размер виртуальной Машины, hello ближайшее соответствие tooyour локальных серверов. Затем мера hello производительности на уровне фактической нагрузки с учитывают tooCPU, памяти и дисковых операций ввода вывода в секунду (IOPS) и размер hello при необходимости. Если требуется несколько сетевых адаптеров для виртуальной Машины, следует учитывать, что максимальное количество сетевых адаптеров для hello функции hello [размер виртуальной Машины][vm-size-tables].   

При подготовке hello виртуальной Машины и другие ресурсы, необходимо указать область. Как правило, выберите регион, ближайший tooyour внутренних пользователей или клиентов. Но некоторые размеры виртуальных машин доступны не для всех регионов. Дополнительные сведения см. на странице [Службы по региону][services-by-region]. toosee список hello размеров виртуальных Машин, доступных в заданном регионе, запустите следующую команду Azure командной строки (CLI) hello:

```
azure vm sizes --location <location>
```

Дополнительные сведения о выборе опубликованных образов виртуальных машин см. в статье [Просмотр и выбор образов виртуальных машин Windows в Azure с помощью оболочки PowerShell или интерфейса командной строки][select-vm-image].

### <a name="disk-and-storage-recommendations"></a>Рекомендации по дискам и хранилищам

Для лучшей производительности дисковых операций ввода-вывода мы рекомендуем использовать [хранилище класса Premium][premium-storage], в котором данные хранятся на твердотельных накопителях (SSD). Стоимость зависит от размера hello hello подготовленном диске. Скорость выполнения операций ввода-вывода и пропускная способность также зависят от размера диска. Поэтому во время подготовки диска следует учитывать все эти факторы.

Создайте учетные записи отдельных хранилища Azure для каждой виртуальной Машины toohold hello виртуальные жесткие диски (VHD) в порядке tooavoid попадание hello ограничения операций ввода-ВЫВОДА для учетных записей хранения.

Добавьте один или несколько дисков данных. При создании виртуальный машины жесткий диск не форматируется. Войдите на диск hello tooformat hello виртуальной Машины. Если имеется большое количество дисков данных, имейте в виду hello всего операций ввода-вывода ограничений hello учетной записи хранения. Дополнительные сведения см. в разделе [Ограничения для дисков виртуальной машины][vm-disk-limits].

Если это возможно, установки приложений на диск данных, hello диска ОС. Тем не менее некоторые устаревшие приложения может потребоваться tooinstall компоненты на диске c: hello. В этом случае вы можете [изменения размера диска hello ОС] [ resize-os-disk] с помощью PowerShell.

Для повышения производительности рекомендуется создайте отдельную учетную запись хранилища toohold журналы диагностики. Учетной записи локально избыточного хранилища достаточно для хранения журналов диагностики.

### <a name="network-recommendations"></a>Рекомендации по сети

Hello общедоступный IP-адрес может быть динамический или статический. по умолчанию Hello является динамическим.

* Резерв [статический IP-адрес] [ static-ip] случай фиксированный IP-адрес, который не будет изменяться &mdash; к примеру, если вам требуется toocreate запись в DNS, или требуется hello безопасный список добавленных tooa toobe IP-адресов.
* Можно также создать полного доменного имени (FQDN) для hello IP-адреса. Затем можно зарегистрировать [запись CNAME] [ cname-record] в DNS, которая указывает toohello полное доменное имя. Дополнительные сведения см. в разделе [Создание полного доменного имени в hello портал Azure][fqdn].

Все группы безопасности сети содержат набор [правил по умолчанию][nsg-default-rules], включая правило, которое блокирует весь входящий интернет-трафик. правила по умолчанию Hello не может быть удалена, но их можно переопределять другие правила. tooenable Интернет-трафика, создать правила, разрешающие входящий трафик порты toospecific &mdash; например, порт 80 для HTTP.  

tooenable RDP, добавьте правило NSG, которое разрешает входящий трафик tooTCP порт 3389.

## <a name="scalability-considerations"></a>Вопросы масштабируемости

Можно масштабировать виртуальной Машины вверх или вниз, [изменение размера виртуальной Машины hello](../articles/virtual-machines/windows/sizes.md). tooscale out горизонтально, поместите две или несколько виртуальных машин в группу доступности в подсистему балансировки нагрузки. Подробные сведения см. в статье [Running multiple VMs on Azure for scalability and availability][multi-vm] (Использование нескольких виртуальных машин в Azure для обеспечения масштабируемости и доступности).

## <a name="availability-considerations"></a>Вопросы доступности

Для повышения уровня доступности разверните несколько виртуальных машин в группе доступности. Это также обеспечивает [соглашение об уровне обслуживания][vm-sla] (SLA) с более высоким уровнем услуг.

На виртуальную машину могут влиять процедуры [планового][planned-maintenance] и [внепланового технического обслуживания][manage-vm-availability]. Можно использовать [журналы перезагрузки виртуальной Машины] [ reboot-logs] toodetermine ли перезагрузка виртуальной Машины было вызвано планового обслуживания.

Виртуальные жесткие диски хранятся в [службе хранилища Azure][azure-storage], которая реплицируется для обеспечения надежности и доступности.

tooprotect от случайной потери данных во время обычной работы (например, из-за ошибки пользователя), необходимо также реализовать резервные копии на момент, используя [больших двоичных объектов моментальные снимки] [ blob-snapshot] или другого средства.

## <a name="manageability-considerations"></a>Вопросы управляемости

**Группы ресурсов.** Помещать тесно связанные ресурсы этой общей папке hello, же жизненным циклом в hello же [группы ресурсов][resource-manager-overview]. Группы ресурсов позволяют toodeploy и монитор ресурсов в группу и сведение выставления счетов затрат по группе ресурсов. Можно также удалить ресурсы в виде набора, что очень удобно для тестирования развернутых служб. Присваивайте ресурсам информативные имена. Который позволяет упростить toolocate определенного ресурса и его восприятие. См. статью [Recommended naming conventions for Azure resources][naming conventions] (Рекомендуемые соглашения об именовании для ресурсов Azure).

**Диагностика виртуальной машины.** Включите мониторинг и диагностику, в том числе базовые метрики работоспособности, а также ведение журналов инфраструктуры диагностики и [диагностику загрузки][boot-diagnostics]. Если виртуальную машину невозможно загрузить, для обнаружения неисправностей можно использовать диагностику загрузки. Дополнительные сведения см. в статье [Включение мониторинга и диагностики][enable-monitoring]. Используйте hello [сбор журналов Azure] [ log-collector] toocollect расширения платформы Azure, журналы и загрузить их tooAzure хранилища.   

Привет, выполнив команду CLI обеспечивает диагностики:

```
azure vm enable-diag <resource-group> <vm-name>
```

**Остановка виртуальной машины.** Azure различает состояния "Остановлена" и "Освобождена". Взимается плата при остановке hello состояние виртуальной Машины, но не освобождается hello виртуальной Машины.

Используйте hello, выполнив команду CLI toodeallocate виртуальной Машины:

```
azure vm deallocate <resource-group> <vm-name>
```

В hello портал Azure, hello **остановить** кнопку освобождает hello виртуальной Машины. Тем не менее, при завершении работы через hello ОС, войдя в систему hello виртуальная машина остановлена, но *не* освобождена, чтобы вас по-прежнему будет взиматься плата.

**Удаление виртуальной машины.** При удалении виртуальной Машины, виртуальные жесткие диски hello не удаляются. Это означает, что можно безопасно удалить hello виртуальных Машин без потери данных. Тем не менее плата за хранение по-прежнему будет взиматься. hello toodelete виртуальный жесткий ДИСК, удалите файл hello из [хранилище больших двоичных объектов][blob-storage].

tooprevent случайного удаления, используйте [блокировка ресурса] [ resource-lock] toolock hello весь ресурс группы или блокировки отдельных ресурсы, такие как hello виртуальной Машины.

## <a name="security-considerations"></a>Вопросы безопасности

Используйте [центра безопасности Azure] [ security-center] tooget центра представление состояния безопасности hello ресурсам Azure. Центр обеспечения безопасности наблюдает за потенциальных проблем безопасности и предоставляет полную картину работоспособности hello безопасности развертывания. Центр безопасности настраивается на уровне подписки Azure. Включите сбор данных безопасности, как описано в разделе [об использовании центра безопасности]. Когда сбор данных включен, центр безопасности автоматически проверяет все виртуальные машины, созданные для этой подписки.

**Управление исправлениями.** Если эта функция включена, то Центр безопасности проверяет, отсутствуют ли какие-либо обновления для системы безопасности и критические обновления. Используйте [параметры групповой политики] [ group-policy] на hello ВМ tooenable системы автоматического обновления.

**Защита от вредоносных программ.** Если эта функция включена, то Центр безопасности проверяет, установлена ли антивредоносное ПО. Можно также использовать Центр обеспечения безопасности tooinstall защиты от вредоносных программ из внутри hello портал Azure.

**Операции.** Используйте [управления доступом на основе ролей] [ rbac] toohello доступа toocontrol (RBAC) Azure ресурсы, которые можно развернуть. RBAC позволяет назначить авторизации ролей toomembers команды DevOps. Например роль модуля чтения hello можно просматривать ресурсы Azure, но не создание, управление или удалить их. Некоторые роли являются tooparticular определенных типов ресурсов Azure. Например роль виртуальной машины участника hello можно перезапустить или освободить виртуальную Машину, сбросить пароль администратора hello, создания новой виртуальной Машины и пр. Для этой архитектуры могут оказаться полезными и другие [встроенные роли RBAC][rbac-roles], например [Пользователь DevTest Labs][rbac-devtest] и [Участник сетей][rbac-network]. Пользователю можно назначить роли toomultiple и можно создать пользовательские роли для еще более детально настроенные разрешения.

> [!NOTE]
> RBAC не ограничивает hello действия, которые может выполнять пользователь выполнил вход в виртуальную Машину. Эти разрешения определяются типом учетной записи hello hello гостевой ОС.   
>
>

пароль локального администратора tooreset hello, запустите hello `vm reset-access` команду Azure CLI.

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

Используйте [журналы аудита] [ audit-logs] toosee подготовки действия и другие события виртуальной Машины.

**Шифрование данных.** Рассмотрим [шифрование диска Azure] [ disk-encryption] при необходимости hello tooencrypt ОС и дисков данных.

## <a name="solution-deployment"></a>Развертывание решения

Пример развертывания для этой архитектуры можно найти на портале [GitHub][github-folder]. Он содержит виртуальную сеть, NSG и одну виртуальную машину. toodeploy Здравствуйте архитектуры, выполните следующие действия:

1. Щелкните правой кнопкой мыши кнопку hello и выберите либо «открыть ссылку в новой вкладке» или «Открыть ссылку в новом окне».  
   [![Развертывание tooAzure](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)
2. После связи hello открытых в hello портал Azure, необходимо ввести значения для некоторых параметров hello.

   * Hello **группы ресурсов** имя уже определен в файле параметров hello, поэтому выберите **создать новый** и введите `ra-single-vm-rg` в текстовом поле hello.
   * Выберите hello регион из hello **расположение** раскрывающийся список.
   * Не изменяйте hello **Uri корневого шаблона** или hello **параметр корневой Uri** текстовые поля.
   * Выберите **windows** в hello **тип ОС** раскрывающийся список.
   * Прочитайте условия hello, затем нажмите кнопку hello **я принимаю условия, указанных выше, toohello** флажок.
   * Щелкните hello **покупки** кнопки.
3. Дождитесь toocomplete развертывания hello.
4. файлы параметров Hello включают жестко администратора имя пользователя и пароль и настоятельно рекомендуется немедленно изменить обе. Щелкните Виртуальную машину с именем hello `ra-single-vm0 `в hello портал Azure. Щелкните на **сброс пароля** в hello **поддержки + Устранение неполадок** колонку. Выберите **сброс пароля** в hello **режим** поле раскрывающегося списка, затем выберите новые **имя пользователя** и **пароль**. Нажмите кнопку hello **обновление** toopersist hello новое имя пользователя и пароль, нажмите кнопку.

Сведения о дополнительных способов toodeploy этой ссылки архитектуры, см. в файле readme hello в hello [руководство по одной виртуальной машины][github-folder]] папку GitHub.

## <a name="customize-hello-deployment"></a>Настройка развертывания hello
При необходимости развертывания toomatch toochange hello вашим потребностям, следуйте инструкциям hello hello [readme][github-folder].

## <a name="next-steps"></a>Дальнейшие действия
Для повышения доступности разверните две или несколько виртуальных машин за подсистемой балансировки нагрузки. Дополнительные сведения см. в статье [Running multiple VMs on Azure for scalability and availability][multi-vm] (Запуск нескольких виртуальных машин в Azure для обеспечения масштабируемости и доступности).

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
[об использовании центра безопасности]: ../articles/security-center/security-center-get-started.md#use-security-center
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
[0]: ./media/guidance-blueprints/compute-single-vm.png "Архитектура с одной виртуальной машиной Windows в Azure"
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks
