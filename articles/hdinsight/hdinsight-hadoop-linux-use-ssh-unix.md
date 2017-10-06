---
title: "aaaUse SSH с Hadoop - Azure HDInsight | Документы Microsoft"
description: "Вы можете получить доступ к HDInsight с помощью Secure Shell (SSH). Этот документ содержит сведения о подключении с помощью hello ssh tooHDInsight и scp команды от клиентов Windows, Linux, Unix или macOS."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "команды hadoop в linux, команды linux hadoop, hadoop на платформе macos, ssh hadoop, кластер ssh hadoop"
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a>Подключиться с помощью SSH tooHDInsight (Hadoop)

Узнайте, как toouse [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely подключения tooHadoop на Azure HDInsight. 

HDInsight может служить Linux (Ubuntu) hello операционной системы для узлов в кластере Hadoop hello. Hello Следующая таблица содержит hello адреса и порта сведения, необходимые при подключении основе tooLinux HDInsight с помощью SSH-клиента.

| Адрес | Порт | Подключается к... |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | 22 | Граничный узел (R Server в HDInsight) |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | Граничный узел (любой другой тип кластера, если существует граничный узел) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | Основной головной узел |
| `<clustername>-ssh.azurehdinsight.net` | 23 | Дополнительный головной узел |

> [!NOTE]
> Замените `<edgenodename>` с именем hello hello граничного узла.
>
> Замените `<clustername>` с hello имя кластера.
>
> Если в кластере имеется граничного узла, мы рекомендуем вам __всегда подключаются toohello граничного узла__ с помощью SSH. Hello головного узла размещения службы, которые являются работоспособность критических toohello Hadoop. Hello граничного узла выполняется только то, что вводится на нем.
>
> Дополнительные сведения об использовании граничных узлов см. в разделе [Доступ к граничному узлу](hdinsight-apps-use-edge-node.md#access-an-edge-node).

## <a name="ssh-clients"></a>SSH-клиенты

Системы Linux, Unix и macOS обеспечивают hello `ssh` и `scp` команд. Hello `ssh` клиент — часто используемые toocreate удаленный сеанс командной строки с ОС Unix или Linux. Hello `scp` клиента — используется toosecurely копирования файлов между клиентом и hello удаленной системе.

Microsoft Windows не предоставляет клиенты SSH по умолчанию. Hello `ssh` и `scp` клиентов доступны для Windows hello следующие пакеты:

* [Azure облачной оболочки](../cloud-shell/quickstart.md): hello оболочки облако предоставляет среде Bash в браузере, а hello `ssh`, `scp`и других общих команд Linux.

* [Bash на Ubuntu в Windows 10](https://msdn.microsoft.com/commandline/wsl/about): hello `ssh` и `scp` команды доступны через hello Bash в командной строке Windows.

* [Git (https://git-scm.com/)](https://git-scm.com/): hello `ssh` и `scp` команды доступны через командную строку hello GitBash.

* [Рабочий стол GitHub (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` и `scp` команды доступны через hello GitHub оболочка командной строки. Рабочий стол GitHub могут быть настроенный toouse Bash hello командной строки Windows и PowerShell как hello командной строки для hello Git оболочки.

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello команды PowerShell является перенос OpenSSH tooWindows и предоставляет выпуски теста.

    > [!WARNING]
    > Hello OpenSSH пакет содержит компонент сервера SSH hello, `sshd`. Этот компонент запускается сервер SSH на компьютере, позволяя другим tooconnect tooit. Не настроить этот компонент и откройте порт 22, если не требуется toohost SSH-сервер в вашей системе. Это не требуется toocommunicate с HDInsight.

Существует также несколько графических SSH-клиентов, например [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) и [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/). Эти клиенты могут быть tooHDInsight используется tooconnect, процесс подключения hello отличается от использования hello `ssh` программы. Дополнительные сведения см. в документации hello hello графический клиента, которую вы используете.

## <a id="sshkey"></a>Проверка подлинности с помощью ключей SSH

SSH ключи используют [шифровании с открытым ключом](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate сеансов SSH. Ключи SSH более безопасны, чем пароли и предоставить кластера Hadoop tooyour легко toosecure доступа.

Если ваша учетная запись SSH, защищена с помощью ключа hello клиент должен предоставить hello сопоставления закрытый ключ, при подключении:

* Большинство клиентов может быть настроенный toouse __ключ по умолчанию__. Например, hello `ssh` клиент ищет закрытый ключ в `~/.ssh/id_rsa` в Linux и Unix.

* Можно указать hello __путь tooa закрытый ключ__. С hello `ssh` клиента, hello `-i` параметр — используется toospecify hello путь tooprivate ключ. Например, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.

* Если у вас есть __несколько закрытых ключей__ для использования на разных серверах, рассмотрите возможность использования служебных программ, например [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent). Hello `ssh-agent` программа может быть toouse ключа используется tooautomatically выберите hello при установлении сеанса SSH.

> [!IMPORTANT]
>
> Если защитить ваш закрытый ключ с помощью парольной фразы, необходимо ввести hello парольную фразу при использовании ключа hello. Служебные программы, такие как `ssh-agent` можно кэшировать пароль hello для вашего удобства.

### <a name="create-an-ssh-key-pair"></a>Создание пары ключей SSH

Используйте hello `ssh-keygen` командные файлы toocreate открытого и закрытого ключа. Hello следующая команда создает пару ключей RSA 2048 бит, который может использоваться с HDInsight.

    ssh-keygen -t rsa -b 2048

Сведения о процессе создания ключа hello запрашивается. Например, где хранятся ключи hello или ли toouse парольную фразу. После завершения процесса hello создаются два файла; открытый ключ и закрытый ключ.

* Hello __открытый ключ__ является toocreate используется кластер HDInsight. открытый ключ Hello имеет расширение `.pub`.

* Hello __закрытый ключ__ является используется tooauthenticate кластеру HDInsight toohello клиента.

> [!IMPORTANT]
> Эти ключи можно защитить с помощью парольной фразы. Парольная фраза — это, по сути, пароль закрытого ключа. Даже если кто-то получает ваш закрытый ключ, они должны иметь hello парольная фраза toouse hello ключ.

### <a name="create-hdinsight-using-hello-public-key"></a>Создание с помощью открытого ключа hello HDInsight

| Метод создания | Как toouse hello открытого ключа |
| ------- | ------- |
| **Портал Azure** | Снимите флажок __использовать одинаковый пароль в качестве учетной записи кластера__и выберите __открытый ключ__ как hello тип проверки подлинности SSH. Наконец, выберите файл открытого ключа hello, или вставьте hello текстовое содержимое файла hello в hello __открытый ключ SSH__ поля.</br>![Диалоговое окно открытого ключа SSH при создании кластера HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **Azure PowerShell** | Используйте hello `-SshPublicKey` параметр hello `New-AzureRmHdinsightCluster` командлета и передайте содержимое hello hello открытый ключ как строка.|
| **Azure CLI 1.0** | Используйте hello `--sshPublicKey` параметр hello `azure hdinsight cluster create` команды и передайте содержимое hello hello открытый ключ в виде строки. |
| **Шаблон Resource Manager** | Пример использования ключей SSH с помощью шаблона см. на странице [Deploy HDInsight on Linux (w/ Azure Storage, SSH key)](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/) (Развертывание HDInsight в Linux с использованием службы хранилища Azure и ключа SSH). Hello `publicKeys` элемент в hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) файл является tooAzure ключи hello toopass используется при создании кластера hello. |

## <a id="sshpassword"></a>Проверка подлинности с помощью пароля

Учетные записи SSH можно защитить с помощью пароля. При подключении с помощью SSH tooHDInsight их запрашиваемые tooenter hello пароль.

> [!WARNING]
> Мы не советуем использовать такой метод проверки подлинности для SSH. Пароли можно подобрать и являются уязвимыми toobrute атаки. Вместо этого рекомендуется использовать [проверку подлинности с помощью ключей SSH](#sshkey).

### <a name="create-hdinsight-using-a-password"></a>Создание кластера HDInsight с использованием пароля

| Метод создания | Как toospecify hello пароль |
| --------------- | ---------------- |
| **Портал Azure** | По умолчанию hello SSH учетная запись пользователя имеет hello паролем учетной записи входа кластера hello. toouse другой пароль, снимите флажок __использовать одинаковый пароль в качестве учетной записи кластера__, а затем введите пароль hello в hello __пароль SSH__ поля.</br>![Диалоговое окно пароля SSH при создании кластера HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **Azure PowerShell** | Используйте hello `--SshCredential` параметр hello `New-AzureRmHdinsightCluster` командлета и передать `PSCredential` , содержащий hello SSH учетное имя пользователя и пароль. |
| **Azure CLI 1.0** | Используйте hello `--sshPassword` параметр hello `azure hdinsight cluster create` команду и укажите значение пароля hello. |
| **Шаблон Resource Manager** | Пример использования пароля с помощью шаблона см. на странице [Deploy HDInsight cluster with Storage and SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/) (Развертывание HDInsight с использованием службы хранилища и пароля SSH). Hello `linuxOperatingSystemProfile` элемент в hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) файла при создании кластера hello не используется toopass hello SSH учетной записи имени и пароля tooAzure.|

### <a name="change-hello-ssh-password"></a>Изменение пароля SSH hello

Дополнительные сведения об изменении пароля учетной записи пользователя для SSH hello. в разделе hello __изменения паролей__ раздел hello [управления HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) документа.

## <a id="domainjoined"></a>Проверка подлинности при использовании присоединенного к домену кластера HDInsight

При использовании __домену кластера HDInsight__, необходимо использовать hello `kinit` команду после установки соединения с SSH. Эта команда запрашивает пользователя домена и пароль и проверяет подлинность сеанс с доменом Azure Active Directory hello, связанные с кластером hello.

Дополнительные сведения см. в статье [Настройка присоединенных к домену кластеров HDInsight (предварительная версия)](hdinsight-domain-joined-configure.md).

## <a name="connect-toonodes"></a>Подключение toonodes

Здравствуйте головного узла и граничного узла (если есть) могут быть доступны через hello Интернета на портах 22 и 23.

* При подключении toohello __head узлы__, используется порт __22__ tooconnect toohello основной головного узла и порта __23__ tooconnect toohello дополнительного головного узла. Hello toouse полное доменное имя является `clustername-ssh.azurehdinsight.net`, где `clustername` является hello имя кластера.

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* Когда connectiung toohello __граничного узла__, используется порт 22. Hello полное доменное имя — `edgenodename.clustername-ssh.azurehdinsight.net`, где `edgenodename` является имя обеспечено при создании hello граничного узла. `clustername`— Имя кластера hello hello.

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> Hello предыдущих примерах предполагается, что вы используете проверку подлинности пароль или, проверку подлинности сертификата велика автоматически. Если использовать пару ключ SSH для проверки подлинности и сертификат hello не используется автоматически, используйте hello `-i` параметр toospecify hello закрытый ключ. Например, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.

После подключения строку hello изменяет tooindicate hello SSH пользователем имя и hello узел, с которым вы подключены к. Например, при подключении toohello первичного головного узла в качестве `sshuser`, запрос hello — `sshuser@hn0-clustername:~$`.

### <a name="connect-tooworker-and-zookeeper-nodes"></a>Подключение tooworker и Zookeeper узлов

Здравствуйте рабочих узлов и узлов не доступны непосредственно из Zookeeper hello Интернета. Они могли быть доступны из головного узла кластера hello или краевым узлам. Здесь представлены Hello hello общие шаги tooconnect tooother узлов:

1. Используйте SSH tooconnect tooa head или край узла:

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. В hello head toohello подключения SSH или граничного узла используйте hello `ssh` команды tooconnect tooa рабочий узел в кластере hello:

        ssh sshuser@wn0-myhdi

    см. список имен домена hello hello узлов в кластере hello tooretrieve hello [Здравствуйте, управление HDInsight с помощью API-интерфейса REST Ambari](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) документа.

Если учетная запись SSH hello защищается с помощью __пароль__, введите пароль hello при подключении.

Если учетная запись SSH hello защищается с помощью __ключи SSH__, убедитесь, что включение SSH пересылки на приветствия клиента.

> [!NOTE]
> Другим способом, toodirectly доступа всем узлам в кластере hello является tooinstall HDInsight в виртуальной сети Azure. Затем вы можете присоединиться к toohello на удаленном компьютере же виртуальной сети и прямой доступ к все узлы в кластере hello.
>
> Дополнительные сведения см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md).

### <a name="configure-ssh-agent-forwarding"></a>Настройка перенаправления SSH-агента

> [!IMPORTANT]
> Hello следующие шаги предполагают, Linux или UNIX с системой и работать с Bash в Windows 10. Если эти шаги не работают для вашей системы, может потребоваться tooconsult hello документации для SSH-клиента.

1. Откройте в текстовом редакторе файл `~/.ssh/config`. Если этот файл отсутствует, его можно создать. Для этого в командной строке введите команду `touch ~/.ssh/config`.

2. Добавьте следующий текст toohello hello `config` файла.

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    Замените hello __узла__ сведения с адресом hello hello узла подключения toousing SSH. Hello в предыдущем примере hello граничного узла. Эта запись настраивает агент SSH, пересылки для hello указанного узла.

3. Агент SSH, пересылки, используя следующую команду из терминала hello hello тестирования:

        echo "$SSH_AUTH_SOCK"

    Эта команда возвращает сведения аналогичные toohello следующий текст:

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    Если сведения не возвращаются, то это значит, что `ssh-agent` не работает. Дополнительные сведения см. в разделе hello сведения сценариев запуска агента в [с помощью ssh агента с ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) или обратитесь к документации клиент SSH.

4. После проверки того, **ssh агента** -работает, используйте hello, следуя tooadd агента toohello закрытого ключа SSH:

        ssh-add ~/.ssh/id_rsa

    Если ваш закрытый ключ хранится в другой файл, замените `~/.ssh/id_rsa` с файлом toohello путь hello.

5. Подключите граничного узла кластера toohello или головного узла с помощью SSH. Затем можно используйте hello SSH команда tooconnect tooa рабочего процесса или zookeeper узла. Hello подключение выполняется с помощью ключа перенаправленных hello.

## <a name="copy-files"></a>Копирование файлов

Hello `scp` программа может быть используется toocopy tooand файлы из отдельных узлов в кластере hello. Здравствуйте, например, следующая команда копирует hello `test.txt` каталог hello локальной системы toohello основного головного узла:

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

Так как путь не указан после hello `:`, hello файл помещается в hello `sshuser` домашнего каталога.

Следующий пример копирует hello Hello `test.txt` файл из hello `sshuser` домашний каталог hello основного головного узла toohello локальной системе:

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> `scp`доступны только отдельные узлы в кластере hello hello файловой системе. Он не может быть используется tooaccess данные в HDFS-совместимой hello хранилища для кластера hello.
>
> Использовать `scp` при необходимости tooupload ресурса для использования из сеанса SSH. Например отправить скрипт на Python, а затем запустите сценарий hello из сеанса SSH.
>
> Сведения о непосредственно загрузки данных в хранилища HDFS-совместимой hello см hello следующие документы:
>
> * [Использование службы хранилища Azure с кластерами Azure HDInsight](hdinsight-hadoop-use-blob-storage.md).
>
> * [Использование Data Lake Store с кластерами Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md).

## <a name="next-steps"></a>Дальнейшие действия

* [Использование туннелирования SSH для доступа к веб-интерфейсу Ambari, JobHistory, NameNode, Oozie и другим веб-интерфейсам](hdinsight-linux-ambari-ssh-tunnel.md)
* [Расширение возможностей HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md)
* [Доступ к граничному узлу](hdinsight-apps-use-edge-node.md#access-an-edge-node)