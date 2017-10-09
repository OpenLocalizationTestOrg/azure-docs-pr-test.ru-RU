# <a name="scale-agent-nodes-in-a-container-service-cluster"></a>Масштабирование узлов агента в кластере службы контейнеров
После [развертывание кластера службы контейнера Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), может потребоваться toochange hello числу узлов, агент. Например, будут нужны дополнительные узлы агентов для запуска большего количества контейнеров или экземпляров приложения. 

Можно изменить с помощью портала Azure hello hello количество узлов агента в кластере DC/OS помощью Docker Swarm и Kubernetes или hello Azure CLI 2.0. 

## <a name="scale-with-hello-azure-portal"></a>Масштабирование с hello портал Azure

1. В hello [портал Azure](https://portal.azure.com), поиск **служб контейнеров**, а затем нажмите кнопку hello контейнер службы, которые должны toomodify.
2. В hello **контейнера службы** колонка, щелкните **агенты**.
3. В **число виртуальных Машин**, введите номер требуемого hello агентов узлов.

    ![Масштабирование пула hello портала](./media/container-service-scale/container-service-scale-portal.png)

4. Конфигурация toosave hello, нажмите кнопку **Сохранить**.

## <a name="scale-with-hello-azure-cli-20"></a>Масштабирование с hello Azure CLI 2.0

Убедитесь, что вы [установлен](/cli/azure/install-az-cli2) hello последнюю Azure CLI 2.0 и вход tooan учетная запись azure (`az login`).

### <a name="see-hello-current-agent-count"></a>В разделе hello текущее количество агентов
количество агентов в настоящее время hello toosee в кластере hello запуска hello `az acs show` команды. Это показано hello конфигурации кластера. Здравствуйте, например, следующая команда отображает hello конфигурации hello контейнер службы с именем `containerservice-myACSName` в группе ресурсов hello `myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

Команда Hello возвращает hello количество агентов в hello `Count` в разделе `AgentPoolProfiles`.

### <a name="use-hello-az-acs-scale-command"></a>Используйте hello az команды масштаб acs
количество узлов агента выполните hello hello toochange `az acs scale` команды и указывайте hello **группы ресурсов**, **имя контейнера службы**и требуемого hello **количество новых агента**. Используя меньшее или большее количество агентов, можно уменьшать или увеличивать масштаб соответственно.

Например количество агентов в предыдущих hello hello toochange кластеров too10 типа hello следующую команду:

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

Hello Azure CLI 2.0 возвращает строку JSON, представляющую hello новую конфигурацию службы hello контейнера, включая количество новых агента hello.

Чтобы увидеть дополнительные параметры команды, запустите `az acs scale --help`.

## <a name="scaling-considerations"></a>Рекомендации по масштабированию

* Номер Hello узлов агент должен быть от 1 до 100 включительно. 

* Свою квоту ядер можно ограничить число hello агента узлов в кластере.

* Операции масштабирования узла агента задаются примененных tooan виртуальной машины Azure шкалы, содержащий пул агентов hello. В кластере DC/OS только узлы агентов в пуле закрытый hello масштабируются операциями hello, приведенными в этой статье.

* В зависимости от того, orchestrator hello, развертываемым в кластере можно отдельно масштабировать hello число экземпляров контейнера, запущенного в кластере hello. Например, в кластере DC/OS использовать hello [пользовательского интерфейса Marathon](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello число экземпляров приложения-контейнера.

* В настоящее время не поддерживается автоматическое масштабирование узлов агентов в кластере службы контейнеров.

## <a name="next-steps"></a>Дальнейшие действия
* Изучите [дополнительные примеры](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) использования команд Azure CLI 2.0 для работы со службой контейнеров Azure.
* См. дополнительные сведения о [пулах агентов DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) в службе контейнеров Azure.

