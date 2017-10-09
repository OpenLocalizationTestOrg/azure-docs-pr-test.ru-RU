# <a name="container-service-frequently-asked-questions"></a>Часто задаваемые вопросы о службе контейнеров

## <a name="orchestrators"></a>Оркестраторы

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Какие оркестраторы контейнеров поддерживает Служба контейнеров Azure? 

Служба контейнеров Azure поддерживает компоненты DC/OS, Docker Swarm и Kubernetes с открытым кодом. Дополнительные сведения см. в разделе hello [Обзор](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
 
### <a name="do-you-support-docker-swarm-mode"></a>Поддерживается ли режим Docker Swarm? 

В настоящее время не поддерживается режим группу мелких объектов, но он находится на план службы hello. 

### <a name="does-azure-container-service-support-windows-containers"></a>Поддерживает ли Служба контейнеров Azure контейнеры Windows?  

Сейчас для всех оркестраторов поддерживаются только контейнеры Linux. Поддержка контейнеров Windows в Kubernetes находится в на этапе предварительной версии.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>Советуете ли вы использовать конкретный оркестратор в Службе контейнеров Azure? 
Обычно мы не советуем использовать конкретный оркестратор. Есть опыт работы с одним из orchestrators hello поддерживается, можно применить этот процесс в службе контейнера Azure. Но на основе тенденций в данных DC/OS эффективно использовать для рабочих нагрузок Интернета вещей и больших данных, Kubernetes подходит для облачных рабочих нагрузок, а Docker Swarm отличается возможностью интеграции со средствами Docker и своей простотой.

В зависимости от сценария использования вы также можете создавать пользовательские решения по работе с контейнерами и управлять ими с помощью других служб Azure. К этим службам относятся [Виртуальные машины](../articles/virtual-machines/linux/overview.md), [Service Fabric](../articles/service-fabric/service-fabric-overview.md), [веб-приложения](../articles/app-service-web/app-service-web-overview.md) и [пакетная служба](../articles/batch/batch-technical-overview.md).  

### <a name="what-is-hello-difference-between-azure-container-service-and-acs-engine"></a>Что такое hello разницу между контейнера службы Azure и модуль ACS 
Служба Azure контейнер — это соглашение об уровне ОБСЛУЖИВАНИЯ резервного служба Azure с возможностями hello портал Azure, средств командной строки Azure и API-интерфейсов Azure. Служба Hello позволяет реализовать tooquickly и управление кластерами при запуске средств orchestration стандартный контейнер с помощью относительно небольшого числа вариантов конфигурации. 

[Модуль ACS](http://github.com/Azure/acs-engine) — это проект открытым исходным кодом, служит для настройки кластера hello toocustomize пользователей питания на каждом уровне. Эта возможность tooalter hello конфигурация инфраструктуры и программного обеспечения означает, что мы предлагаем нет соглашения об уровне ОБСЛУЖИВАНИЯ для модуля ACS. Поддержка обрабатываются через проект с открытым исходным hello на GitHub, а не по каналам официальный Microsoft. 

## <a name="cluster-management"></a>Управление кластерами

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>Как создавать ключи SSH для кластера?

Можно использовать стандартные средства для вашей операционной системы toocreate SSH-RSA пару открытого и закрытого ключа для проверки подлинности от виртуальных машин Linux hello для кластера. Пошаговые инструкции см. в разделе hello [OS X и Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) или [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) рекомендации. 

Если вы используете [команды Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy в контейнер службы кластеров, SSH ключи могут автоматически формироваться для кластера.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>Как создать субъект-службу для кластера Kubernetes?

Идентификатор участника службы Azure Active Directory и пароль, также требуется toocreate Kubernetes кластера в службе контейнера Azure. Дополнительные сведения см. в разделе [о hello участника-службы для кластера Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md).

Если вы используете [команды Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy Kubernetes, служба кластеров основной учетные данные могут автоматически формироваться для кластера.

### <a name="how-large-a-cluster-can-i-create"></a>Кластер какого размера можно создать?
Можно создать кластер с 1, 3 или 5 основными узлами. Для выбора узлов too100 агента.

> [!IMPORTANT]
> Для больших кластеров и в зависимости от hello размер виртуальной Машины, выбранный для узлов может потребоваться квоту ядер tooincrease hello в вашей подписке. Увеличение квоты, откройте toorequest [запрос на получение поддержки сети клиента](../articles/azure-supportability/how-to-create-azure-support-request.md) бесплатно. Если вы используете [бесплатную учетную запись Azure](https://azure.microsoft.com/free/), вам доступно ограниченное количество вычислительных ядер Azure.
> 

### <a name="how-do-i-increase-hello-number-of-masters-after-a-cluster-is-created"></a>Как увеличить число hello образцов после создания кластера? 
После создания кластера hello hello число образцов фиксируется и не может быть изменено. Во время создания кластера hello hello в идеале следует выбрать несколько образцов для обеспечения высокой доступности.

### <a name="how-do-i-increase-hello-number-of-agents-after-a-cluster-is-created"></a>Как увеличить количество hello агентов после создания кластера? 
С помощью hello портал Azure или средства командной строки можно масштабировать hello количество агентов в кластере hello. Дополнительные сведения см. в статье [Масштабирование кластера Службы контейнеров Azure](../articles/container-service/kubernetes/container-service-scale.md).

### <a name="what-are-hello-urls-of-my-masters-and-agents"></a>Что такое hello URL-адреса, образцов и агенты 
Hello URL-адреса кластера ресурсы в контейнере службы Azure основаны на hello DNS-имен префикс, укажите и hello имя hello Azure для развертывания выбранного региона. Например hello полное доменное имя (FQDN) главного узла hello имеет следующую форму:

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

Можно найти часто используемые URL-адресов для кластера в hello портал Azure, hello обозревателя ресурсов Azure или другие средства Azure.

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>Как узнать, какая версия оркестратора используется в кластере?

* DC/OS: В разделе hello [Mesosphere документации](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* в Docker Swarm используется `docker version`;
* в Kubernetes используется `kubectl version`.

### <a name="how-do-i-upgrade-hello-orchestrator-after-deployment"></a>Как обновить hello orchestrator после развертывания?

В настоящее время контейнера службы Azure не предоставляет средств tooupgrade hello версии orchestrator hello, развернутых в кластере. Если служба контейнеров поддерживает более позднюю версию, можно развернуть новый кластер. Другой вариант — средства, определяемые orchestrator toouse, если они доступны tooupgrade кластера на месте. Для примера можно ознакомиться с документацией об [обновлении DC/OS](https://dcos.io/docs/1.8/administration/upgrading/).
 
### <a name="where-do-i-find-hello-ssh-connection-string-toomy-cluster"></a>Где найти hello SSH соединения строки toomy кластера?

Строка подключения hello можно найти в hello портал Azure или с помощью средств командной строки Azure. 

1. На портале hello перейдите toohello группы ресурсов для развертывания кластера hello.  

2. Нажмите кнопку **Обзор** и щелкните ссылку hello **развертываний** под **Essentials**. 

3. В hello **журнала развертывания** колонка, щелкните развертывание hello, имя которого начинается с **microsoft acs** следуют даты развертывания. Например, microsoft-acs-201701310000.  

4. На hello **Сводка** в разделе **выходов**, предоставляются несколько ссылок кластера. **SSHMaster0** предоставляет SSH соединения строки toohello первый образец контейнера службы кластера. 

Как уже отмечалось также можно использовать средства Azure toofind hello полное доменное имя базы данных hello master. Назначить SSH-подключения основной toohello, используя полное доменное имя главного hello и hello имя пользователя, которое было указано при создании кластера hello hello. Например:

```bash
ssh userName@masterFQDN –A –p 22 
```

Дополнительные сведения см. в разделе [кластера контейнера службы Azure Connect tooan](../articles/container-service/kubernetes/container-service-connect.md).

## <a name="next-steps"></a>Дальнейшие действия

* Узнайте больше о [Службе контейнеров Azure](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
* Развертывание кластера службы контейнера с помощью hello [портала](../articles/container-service/dcos-swarm/container-service-deployment.md) или [Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md).
