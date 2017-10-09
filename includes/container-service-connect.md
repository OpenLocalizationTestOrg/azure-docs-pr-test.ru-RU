# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a>Создания кластера, Kubernetes, DC/OS или с помощью Docker Swarm tooa удаленного подключения
После создания кластера контейнера службы Azure, требуется toodeploy кластера toohello tooconnect и управление рабочими нагрузками. В этой статье описывается, как главный toohello tooconnect виртуальная машина hello кластера с удаленного компьютера. 

Hello Kubernetes, DC/OS и с помощью Docker Swarm кластеры обеспечивают локально конечные точки HTTP. Для Kubernetes, эта конечная точка безопасно предоставляется hello Интернет и доступ к нему, запустив hello `kubectl` средство командной строки с любого компьютера, подключенного к Интернету. 

Для контроллера домена/OS и помощью Docker Swarm рекомендуется создавать туннеля безопасного shell (SSH) из системы управления кластера toohello локального компьютера. После установления туннеля hello запуском команды, которые используют конечные точки HTTP hello и представление hello orchestrator веб-интерфейса (если он доступен) с локального компьютера. 

## <a name="prerequisites"></a>Предварительные требования

* Кластер Kubernetes, DC/OS или Docker Swarm, [развернутый в службе контейнеров Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).
* SSH-RSA файла закрытого ключа, соответствующего открытого ключа добавлены toohello кластера toohello во время развертывания. Эти команды предполагают, что hello закрытого SSH-ключ находится в `$HOME/.ssh/id_rsa` на компьютере. Дополнительные сведения см. в статьях [Как создать и использовать пару из открытого и закрытого ключей SSH для виртуальных машин Linux в Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md) и [Использование ключей SSH с Windows в Azure](../articles/virtual-machines/linux/ssh-from-windows.md). Если hello SSH-подключение не работает, может потребоваться слишком [сброс ключей SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

## <a name="connect-tooa-kubernetes-cluster"></a>Подключите кластер Kubernetes tooa

Выполните эти шаги tooinstall и настройте `kubectl` на компьютере.

> [!NOTE] 
> В Linux или macOS, может потребоваться toorun hello команды в этом разделе с помощью `sudo`.
> 

### <a name="install-kubectl"></a>Установка kubectl
Одним из способов tooinstall это средство — toouse hello `az acs kubernetes install-cli` команда Azure CLI 2.0. toorun эту команду, убедитесь, что вы [установлен](/cli/azure/install-az-cli2) hello последнюю Azure CLI 2.0 и войти в учетную запись Azure tooan (`az login`).

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

Кроме того, вы можете загрузить hello последней `kubectl` клиента непосредственно из hello [Kubernetes освобождает страницу](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md). Дополнительные сведения см. в разделе [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Установка и настройка kubectl).

### <a name="download-cluster-credentials"></a>Скачивание учетных данных кластера
После получения `kubectl` установлен, нужна tooyour учетные данные машина, toocopy hello кластера. Является одним из способов toodo get hello, учетные данные с hello `az acs kubernetes get-credentials` команды. Передайте hello имя группы ресурсов hello и hello для ресурса службы hello контейнера:

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

Эта команда загружает учетные данные кластера hello слишком`$HOME/.kube/config`, где `kubectl` ожидает ее найти toobe.

Кроме того, можно использовать `scp` toosecurely Копировать файл hello из `$HOME/.kube/config` на hello основной виртуальной Машины tooyour локального компьютера. Например:

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

При работе в Windows можно использовать Bash на Ubuntu на Windows, клиент копирования PuTTy защищенный файл hello или аналогичное средство.

### <a name="use-kubectl"></a>Использование kubectl

После получения `kubectl` настроен, проверка соединения hello, перечисляя hello узлов в кластере:

```bash
kubectl get nodes
```

Можно использовать другие команды `kubectl`. Например можно просмотреть hello Kubernetes панели мониторинга. Сначала необходимо запустите учетную запись-посредник сервера API-интерфейса Kubernetes toohello:

```bash
kubectl proxy
```

Hello Kubernetes пользовательского интерфейса теперь доступен на: `http://localhost:8001/ui`.

Дополнительные сведения см. в разделе hello [Kubernetes краткого](http://kubernetes.io/docs/user-guide/quick-start/).

## <a name="connect-tooa-dcos-or-swarm-cluster"></a>Подключите кластер tooa DC/OS или группу мелких объектов

hello toouse DC/OS и кластеры с помощью Docker Swarm развернут контейнер службой Azure выполните эти инструкции toocreate туннель SSH из локальной системы Windows, Linux или macOS. 

> [!NOTE]
> В статье рассматриваются инструкции по туннелированию TCP-трафика по протоколу SSH. Можно также запустить интерактивный сеанс SSH с одной из систем управления hello внутри кластера, но это не рекомендуется. Работа непосредственно во внутренней системе, вы рискуете случайно изменить конфигурацию.  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a>Создание туннеля SSH в Linux или macOS
Hello первое, что при создании туннель SSH в Linux или macOS — toolocate hello открытому DNS-имени hello образцов балансировки нагрузки. Выполните следующие действия.


1. В hello [портал Azure](https://portal.azure.com), Обзор toohello группы ресурсов, содержащий контейнер службы кластера. Разверните группу ресурсов hello, для отображения каждого ресурса. 

2. Нажмите кнопку hello **контейнера службы** ресурс и нажмите кнопку **Обзор**. Hello **полное доменное имя главного** из hello кластера отображается под **Essentials**. Сохраните это имя для последующего использования. 

    ![Общедоступное DNS-имя](./media/container-service-connect/pubdns.png)

    Кроме того, запустите hello `az acs show` в контейнере службы. Найдите hello **Master профиля: полное доменное имя** свойства в выходных данных команды hello.

3. Теперь откройте оболочку и запустите hello `ssh` команду, указав hello следующие значения: 

    **LOCAL_PORT** используется TCP-порт hello на стороне службы hello hello tooconnect туннеля для. Для группу мелких объектов значение этого too2375. Для контроллера домена/OS значение этого too80. 
    **REMOTE_PORT** — порт hello hello конечной точки, которые должны tooexpose. Для Swarm используется порт 2375. Для DC/OS используется порт 80.  
    **Имя пользователя** hello именем пользователя, предоставленный при развертывании кластера hello.  
    **DNSPREFIX** — префикс DNS hello, указанный при развертывании кластера hello.  
    **ОБЛАСТЬ** — hello область, в которой находится в группе ресурсов.  
    **PATH_TO_PRIVATE_KEY** [необязательно] является hello путь toohello закрытый ключ, соответствующий toohello открытый ключ, указанный при создании кластера hello. Используйте этот параметр с hello `-i` флаг.

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > Hello порт SSH-подключения является 2200 и не hello стандартный порт 22. В кластере с более чем один основной виртуальной Машины это hello подключения порт toohello первый образец виртуальной Машины.
  > 

  Команда Hello возвращает без выходных данных.

В следующих разделах hello см. Примеры hello для контроллера домена/OS и группу мелких объектов.    

### <a name="dcos-tunnel"></a>Туннель DC/OS
tooopen туннеля для контроллера домена/OS конечные точки, выполните команду hello следующим образом:

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> Убедитесь, что у вас нет другого локального процесса, привязанного к порту 80. При необходимости в качестве локального порта вместо 80 можно указать, например, 8080, но в этом случае некоторые ссылки в пользовательском веб-интерфейсе могут не работать.
>

Теперь вы можете использовать конечные точки контроллера домена/OS hello из локальной системы, используя hello следующие URL-адреса (при условии, что локальный порт 80):

* DC/OS: `http://localhost:80/`
* Marathon: `http://localhost:80/marathon`
* Mesos: `http://localhost:80/mesos`

Аналогичным образом может достигать hello API rest для каждого приложения через этот туннель.

### <a name="swarm-tunnel"></a>Туннель Swarm
tooopen конечной точки группу мелких объектов toohello туннеля, выполните команду hello следующим образом:

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> Убедитесь, что у вас нет другого локального процесса, привязанного к порту 2375. Например управляющая программа Docker hello выполняются локально, устанавливается по умолчанию toouse порт 2375. При необходимости вместо 2375 можно указать локальный порт.
>

Теперь можно получить доступ к hello помощью Docker Swarm кластера, с помощью интерфейса командной строки Docker hello (Docker CLI) в локальной системе. Инструкции по установке Docker см. в [этом руководстве](https://docs.docker.com/engine/installation/).

Задайте ваш toohello переменную среды DOCKER_HOST локального порта, настроенного для hello туннеля. 

```bash
export DOCKER_HOST=:2375
```

Выполните команды Docker, туннеля toohello помощью Docker Swarm кластера. Например:

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a>Создание туннеля SSH в Windows
Создавать туннели SSH в Windows можно несколькими способами. При выполнении Bash на Ubuntu в Windows или аналогичное средство, вы можете использовать hello SSH туннелирования инструкции, приведенные ранее в этой статье macOS и Linux. В качестве альтернативы для Windows в этом разделе описываются как toouse PuTTY toocreate hello туннеля.

1. [Загрузить PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour системы Windows.

2. Запустите приложение hello.

3. Введите имя узла, который состоит из имени пользователя администратора кластера hello и hello открытому DNS-имени первый образец hello в кластере hello. Hello **имя узла** выглядит примерно`azureuser@PublicDNSName`. Введите 2200 hello **порт**.

    ![Конфигурация PuTTY 1](./media/container-service-connect/putty1.png)

4. Выберите **SSH > Проверка подлинности**. Добавьте путь tooyour файл закрытого ключа (формат .ppk) для проверки подлинности. Можно использовать это средство, например [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate, этот файл из hello SSH ключа используется toocreate hello кластера.

    ![Конфигурация PuTTY 2](./media/container-service-connect/putty2.png)

5. Выберите **SSH > туннели** и настройте ниже hello пересылаться порты:

    * **исходный порт** — используйте порт 80 для DC/OS или 2375 для Swarm;
    * **конечный порт** — используйте localhost:80 для DC/OS или localhost:2375 для Swarm.

    Следующий пример Hello настроен для контроллера домена/OS, но будет выглядеть для помощью Docker Swarm.

    > [!NOTE]
    > При создании этого туннеля нужно, чтобы порт 80 больше нигде не использовался.
    > 

    ![Конфигурация PuTTY 3](./media/container-service-connect/putty3.png)

6. Закончив, нажмите кнопку **сеанса > Сохранить** конфигурация подключения toosave hello.

7. tooconnect toohello PuTTY сеанс, нажмите кнопку **откройте**. При подключении, вы увидите, что конфигурация порта hello в журнале событий PuTTY hello.

    ![Журнал событий PuTTY](./media/container-service-connect/putty4.png)

После настройки туннеля hello для контроллера домена/OS, доступ к hello связанных конечных точек по адресу:

* DC/OS: `http://localhost/`
* Marathon: `http://localhost/marathon`
* Mesos: `http://localhost/mesos`

После настройки туннеля hello для помощью Docker Swarm Откройте ваш tooconfigure параметры Windows системную переменную среды с именем `DOCKER_HOST` со значением `:2375`. Затем можно обращаться из кластера группу мелких объектов hello hello Docker CLI.

## <a name="next-steps"></a>Дальнейшие действия
Развертывание контейнеров в кластере и управление ими.

* [Работа со службой контейнеров Azure и Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [Работа со службой контейнеров Azure и DC/OS](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [Работа с hello контейнера службы Azure и помощью Docker Swarm](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

