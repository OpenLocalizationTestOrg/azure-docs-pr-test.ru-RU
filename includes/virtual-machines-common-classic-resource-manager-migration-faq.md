# <a name="frequently-asked-questions-about-classic-tooazure-resource-manager-migration"></a>Часто задаваемые вопросы о классическом tooAzure переноса диспетчера ресурсов

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>Влияет ли этот план миграции на существующие службы или приложения, которые выполняются на виртуальных машинах Azure? 

Нет. виртуальные машины Hello (классической) — это службы, полностью поддерживается в общедоступной. Вы можете продолжить toouse эти ресурсы tooexpand объем в Microsoft Azure.

## <a name="what-happens-toomy-vms-if-i-dont-plan-on-migrating-in-hello-near-future"></a>Что произойдет toomy виртуальных машин, если я не планируете переносить по hello ближайшее будущее? 

Мы не являются неподдерживаемые hello существующей классический API-интерфейсы и ресурсов модели. Нам нужно просто, учитывая hello дополнительные функции, доступные в модели развертывания диспетчера ресурсов hello toomake миграции. Настоятельно рекомендуется ознакомиться с [некоторые улучшения hello](../articles/azure-resource-manager/resource-manager-deployment-model.md) , которые являются частью IaaS в области диспетчера ресурсов.

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>Как изменятся существующие средства с этим планом миграции? 

Обновление модели развертывания диспетчера ресурсов toohello инструменты — hello наиболее важные изменения, которые имеют tooaccount для планов перехода.

## <a name="how-long-will-hello-management-plane-downtime-be"></a>Как долго будет hello плоскости управления простоя? 

Это зависит от hello количество ресурсов, которые переносятся. Для небольших систем (нескольких десятков виртуальных машин) весь миграции hello займет менее часа. Для крупномасштабных развертываний (сотни виртуальных машин) hello миграция может занять несколько часов.

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>Можно ли выполнить откат после фиксации переносимых ресурсов в Resource Manager? 

Можно прервать миграции до тех пор, пока hello ресурсы находятся в состояние подготовки hello. После hello ресурсы были успешно перенесены через hello операции фиксации, отката не поддерживается.

## <a name="can-i-roll-back-my-migration-if-hello-commit-operation-fails"></a>Можно ли выполнить откат my миграции при сбое операции фиксации hello? 

Не удается прервать миграции при сбое операции фиксации hello. Все операции миграции, включая операции фиксации hello, являются идемпотентными. Поэтому рекомендуется повторить попытку hello операцию через некоторое время. Если вы по-прежнему приходится ошибку, создайте запрос в службу поддержки или создать сообщение на форуме с тега ClassicIaaSMigration hello нашей [ВМ форум](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).

## <a name="do-i-have-toobuy-another-express-route-circuit-if-i-have-toouse-iaas-under-resource-manager"></a>Нужно ли toobuy другой контура express route у toouse IaaS в диспетчере ресурсов? 

Нет. Мы недавно включена [перемещение каналы ExpressRoute от модели развертывания диспетчера ресурсов hello классический toohello](../articles/expressroute/expressroute-move.md). У вас нет toobuy новый канал ExpressRoute, если она уже есть.

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>Что произойдет, если для классических ресурсов IaaS настроено управление доступом на основе ролей? 

Во время миграции ресурсов hello преобразования из классической tooResource диспетчера. Таким образом, рекомендуется планировать hello RBAC политики обновления, требующие toohappen после миграции.

## <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Резервные копии классических виртуальных машин находятся в хранилище службы архивации. Можно ли выполнить миграцию виртуальных машин из классического режима tooResource Manager режима и защитить их в хранилище служб восстановления? 

Классический точек восстановления виртуальной Машины в резервном хранилище не автоматически перенести tooa хранилище служб восстановления, при перемещении hello виртуальной Машины из tooResource классический режим Manager. Выполните эти шаги tootransfer резервных копий виртуальной Машины.

1. В резервное хранилище hello, перейдите toohello **защищенные элементы** и выберите hello виртуальной Машины. Щелкните [Остановить защиту](../articles/backup/backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). *Снимите* флажок **Удаление связанных архивируемых данных**.
2. Удалите расширение резервного копирования или создания моментального снимка hello hello виртуальной Машины.
3. Миграция виртуальной машины hello из диспетчера tooResource классический режим. Убедитесь, что hello хранилища и сети миграцию информации о соответствующая виртуальная машина toohello также является режим tooResource Manager.
4. Создайте хранилище служб восстановления и настройка виртуальной машины с помощью резервной копии на hello перенести **резервного копирования** действия на основе мониторинга хранилища. Подробные сведения о резервном копировании виртуальной Машины tooa восстановления службы хранилища, см. в статье hello [защиты виртуальных машин Azure в хранилище служб восстановления](../articles/backup/backup-azure-vms-first-look-arm.md).

## <a name="can-i-validate-my-subscription-or-resources-toosee-if-theyre-capable-of-migration"></a>Можно ли проверить Мои подписки или toosee ресурсы если они поддерживают миграции? 

Да. В случае миграции, поддерживаемые платформой hello hello первым шагом при подготовке к миграции является toovalidate, что ресурсы hello способны миграции. В случае, если hello проверка завершается с ошибкой, сообщения для всех причин hello hello миграции не может быть завершена.

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-hello-iaas-resources-for-migration"></a>Что произойдет, если у меня возникли ошибки квоты при подготовке ресурсов IaaS hello миграции? 

Рекомендуется, чтобы прервать выполнение переноса и войдите в регионе hello, откуда производится миграция hello виртуальных машин Квота hello tooincrease запрос на поддержку. После утверждения запроса квоты hello можно запустить выполнение шагов миграции hello еще раз.

## <a name="how-do-i-report-an-issue"></a>Как сообщить о проблеме? 

Проблемы и вопросы о миграции tooour [ВМ форум](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows), с ключевым словом hello ClassicIaaSMigration. Рекомендуется публиковать на этом форуме все свои вопросы. Если у вас есть контрактом на поддержку, вы toolog Добро пожаловать в службу поддержки.

## <a name="what-if-i-dont-like-hello-names-of-hello-resources-that-hello-platform-chose-during-migration"></a>Что делать, если не устраивает hello имена ресурсов hello, hello платформы выбраны во время миграции? 

Все ресурсы hello, которые явно предоставить имена в hello классической модели развертывания сохраняются во время миграции. В некоторых случаях будут создаваться новые ресурсы. Например, для каждой виртуальной машины создается сетевой интерфейс. В настоящее время не поддерживается возможность hello toocontrol имена hello эти новые ресурсы, созданные во время миграции. Войдите на голоса для этой функции hello [форуме обратной связи Azure](http://feedback.azure.com).

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>Можно ли перенести каналы ExpressRoute, используемые в подписках со ссылками авторизации? 

Каналы ExpressRoute, использующие ссылки авторизации между подписками, невозможно перенести автоматически без простоев. У нас есть рекомендации о том, как их можно перенести вручную. В разделе [перенести ExpressRoute каналов и связанные виртуальные сети из модели развертывания диспетчера ресурсов hello классический toohello](../articles/expressroute/expressroute-migration-classic-resource-manager.md) действия и Дополнительные сведения.

## <a name="i-got-a-message-vm-is-reporting-hello-overall-agent-status-as-not-ready-hence-hello-vm-cannot-be-migrated-ensure-that-hello-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-hello-vm-hence-this-vm-cannot-be-migrated-"></a>Получено сообщение *» виртуальной Машины сообщает hello общее состояние агента в качестве не готово. Таким образом нельзя перенести hello виртуальной Машины. Убедитесь, что hello агент виртуальной Машины сообщает общее состояние агента готовой к использованию»* или * «виртуальная машина содержит расширения, состояние которого не возвращается из hello виртуальной Машины. Hence, this VM cannot be migrated" (Виртуальная машина содержит расширение, о состоянии которого она не сообщает. Поэтому виртуальную машину нельзя перенести). *

Это сообщение выдается в том случае, когда hello виртуальная машина не имеет toohello исходящие подключения к Интернету. агент виртуальной Машины Hello использует учетную запись хранилища Azure hello tooreach исходящие подключения для обновления состояния агента hello каждые пять минут.
