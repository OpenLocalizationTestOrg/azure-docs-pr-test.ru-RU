---
title: "aaaImplement Oracle золотые шлюза в виртуальной Машине Linux Azure | Документы Microsoft"
description: "Быстрое создание и запуск Oracle Golden Gate в среде Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a>Реализация Oracle Golden Gate на виртуальной машине Azure под управлением Linux 

Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях. В этом руководстве рассматривается как toouse hello Azure CLI toodeploy Oracle 12c базы данных из коллекции образов Azure Marketplace hello. 

В данном документе описывается пошаговые как toocreate, установки и настройки шлюза золотые Oracle на Виртуальной машине Azure.

Прежде чем начать, убедитесь, что hello Azure CLI был установлен. Дополнительные сведения см. в [руководстве по установке Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Подготовка среды hello

Установка шлюза золотые Oracle tooperform hello, необходимо toocreate две виртуальные машины Azure на hello одной группе доступности. — использовать toocreate hello ВМ образа Marketplace Hello **Oracle: Oracle-базы данных-Ee:12.1.0.2:latest**.

Также требуется знание Unix редактор vi toobe и иметь базовое понимание x11 (X Windows).

Hello ниже приводится сводка hello среды конфигурации:
> 
> |  | **Основной сайт** | **Сайт репликации** |
> | --- | --- | --- |
> | **Версия Oracle** |Версия 2 Oracle 12c — (12.1.0.2) |Версия 2 Oracle 12c — (12.1.0.2)|
> | **Имя компьютера** |myVM1 |myVM2 |
> | **Операционная система** |Oracle Linux 6.x |Oracle Linux 6.x |
> | **ИД безопасности Oracle** |CDB1 |CDB1 |
> | **Схема репликации** |TEST|TEST |
> | **Владелец/репликация Golden Gate** |C##GGADMIN |REPUSER |
> | **Процесс Golden Gate** |EXTORA |REPORA|


### <a name="sign-in-tooazure"></a>Войдите в tooAzure 

Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды. Затем выполните hello на экране инструкциям.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. 

Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westus` расположение.

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Создать группу доступности

Привет, даст необязательно, но рекомендуется. Дополнительные сведения см. в статье [Рекомендации по группам доступности Azure для виртуальных машин Windows](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Создание виртуальной машины

Создайте виртуальную Машину с hello [создания виртуальной машины az](/cli/azure/vm#create) команды. 

Hello следующий пример создает две виртуальные машины с именем `myVM1` и `myVM2`. а также ключи SSH, если они еще не существуют в расположении ключей по умолчанию. toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.

#### <a name="create-myvm1-primary"></a>Создайте myVM1 (основная):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

После hello создания виртуальной Машины hello Azure CLI показано toohello аналогичные сведения, следующий пример. (Обратите внимание hello `publicIpAddress`. Этот адрес будет hello используется tooaccess виртуальной Машины.)

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

#### <a name="create-myvm2-replicate"></a>Создайте myVM2 (репликация):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Запишите hello `publicIpAddress` также после его создания.

### <a name="open-hello-tcp-port-for-connectivity"></a>Привет открыть TCP-порт для подключения к

Hello следующим шагом является tooconfigure внешних конечных точек, которые позволяют базы данных Oracle hello tooaccess удаленно. tooconfigure hello внешние конечные точки, запустите следующие команды hello.

#### <a name="open-hello-port-for-myvm1"></a>Откройте порт hello для myVM1:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

Hello результаты должны выглядеть примерно toohello следующий ответ:

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

#### <a name="open-hello-port-for-myvm2"></a>Откройте порт hello для myVM2:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Подключение toohello виртуальной машины

Используйте hello следующая команда toocreate сеанс SSH с виртуальной машиной hello. Замените hello hello IP-адрес `publicIpAddress` вашей виртуальной машины.

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Создать hello базы данных на myVM1 (основной)

Hello программное обеспечение Oracle уже установлен на образа Marketplace hello, поэтому hello следующим шагом является база данных tooinstall hello. 

Запустите программное обеспечение hello как суперпользователь «oracle» hello:

```bash
sudo su - oracle
```

Создайте базу данных hello:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Выходные данные должен выглядеть примерно toohello следующий ответ:

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

Установка переменных ORACLE_SID и ORACLE_HOME hello.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

При необходимости можно добавить ORACLE_HOME и ORACLE_SID файла toohello .bashrc, чтобы эти параметры сохраняются для будущих входа в систему:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Запуск прослушивателя Oracle
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a>Создание базы данных hello на myVM2 (репликация)

```bash
sudo su - oracle
```
Создайте базу данных hello:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Установка переменных ORACLE_SID и ORACLE_HOME hello.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

При необходимости можно добавлены ORACLE_HOME и ORACLE_SID toohello .bashrc файла, чтобы эти параметры сохраняются для будущих входа в систему.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Запуск прослушивателя Oracle
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a>Настройка Golden Gate 
tooconfigure золотые шлюзом, примите меры hello в этом разделе.

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>Включение режима журнала архивирования на myVM1 (основная)

```bash
$ sqlplus / as sysdba
SQL> SELECT log_mode FROM v$database;

LOG_MODE
------------
NOARCHIVELOG

SQL> SHUTDOWN IMMEDIATE;
SQL> STARTUP MOUNT;
SQL> ALTER DATABASE ARCHIVELOG;
SQL> ALTER DATABASE OPEN;
```
Включите принудительное ведение журнала и убедитесь, что есть хотя бы один файл журнала.

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a>Загрузка программного обеспечения Golden Gate
toodownload и подготовки программного обеспечения Oracle золотые шлюза hello, полный hello, следующие шаги:

1. Загрузите hello **fbo_ggs_Linux_x64_shiphome.zip** файл из hello [страницу скачивания шлюза золотые Oracle](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html). Разделе hello Загрузите заголовок **12.x.x.x Oracle GoldenGate для Oracle Linux x86-64**, должен быть набором toodownload файлы .zip.

2. После загрузки hello .zip файлы tooyour клиентского компьютера, используйте протокол Secure копии (SCP) toocopy hello файлы tooyour виртуальной Машины:

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. Перемещение файлов toohello hello .zip **/ opt** папки. Затем измените владельца hello hello файлов следующим образом:

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. Распакуйте файлы hello (hello установки Linux Распакуйте программы, если она еще не установлена):

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. Измените разрешение:

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a>Подготовить клиент hello и ВМ toorun x11 (только для клиентов Windows)
Этот параметр является необязательным. Если вы используете клиента Linux или уже установили x11, этот шаг можно пропустить.

1. Загрузите компьютер Windows tooyour PuTTY и Xming:

  * [Скачать PuTTY](http://www.putty.org/).
  * [Скачать Xming](https://xming.en.softonic.com/).

2.  После установки PuTTY в hello PuTTY папку (например, C:\Program Files\PuTTY), запустите puttygen.exe (генератор ключа PuTTY).

3.  В генераторе ключей PuTTY сделайте следующее:

  - toogenerate ключей, выберите hello **формирования** кнопки.
  - Скопируйте содержимое hello hello ключа (**Ctrl + C**).
  - Выберите hello **Сохранить закрытый ключ** кнопки.
  - Игнорируйте сообщения hello появится, а затем выберите **ОК**.

    ![Снимок экрана со страницей hello PuTTY генератор ключей](./media/oracle-golden-gate/puttykeygen.png)

4.  В виртуальной машине выполните следующие команды:

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. Создайте файл с именем **authorized_keys**. Вставьте содержимое hello hello ключ в этом файле, а затем сохраните файл hello.

  > [!NOTE]
  > Hello ключ должен содержать строку hello `ssh-rsa`. Кроме того содержимое hello hello ключа должно быть одну строку текста.
  >  

6. Запустите PuTTY. В hello **категории** выберите **подключения** > **SSH** > **Auth**. В hello **файла закрытого ключа для проверки подлинности** поле, найдите toohello ключ, который был создан ранее.

  ![Снимок экрана со страницей hello задать закрытый ключ](./media/oracle-golden-gate/setprivatekey.png)

7. В hello **категории** выберите **подключения** > **SSH** > **X11**. Затем выберите hello **включить X11 пересылку** поле.

  ![Снимок экрана со страницей Enable X11 hello](./media/oracle-golden-gate/enablex11.png)

8. В hello **категории** панели перейдите слишком**сеанса**. Введите сведения об узле hello, а затем выберите **откройте**.

  ![Снимок экрана: страница приветствия сеанса](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a>Установка программного обеспечения Golden Gate

tooinstall шлюзом золотые Oracle, полный hello, следующие шаги:

1. Выполните вход в качестве пользователя oracle. (Вы должны иметь доступ toosign в без необходимости вводить пароль.) Убедитесь, что запущен Xming перед началом установки hello.
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. Выберите Oracle GoldenGate for Oracle Database 12c (Oracle GoldenGate для базы данных Oracle 12c). Выберите **Далее** toocontinue.

  ![Снимок экрана: страница установки выберите установщик hello](./media/oracle-golden-gate/golden_gate_install_01.png)

3. Изменить расположение hello программного обеспечения. Затем выберите hello **запустить диспетчер** и введите расположение базы данных hello. Выберите **Далее** toocontinue.

  ![Снимок экрана: страница приветствия выберите установки](./media/oracle-golden-gate/golden_gate_install_02.png)

4. Измените каталог инвентаризации hello, а затем выберите **Далее** toocontinue.

  ![Снимок экрана: страница приветствия выберите установки](./media/oracle-golden-gate/golden_gate_install_03.png)

5. На hello **Сводка** выберите **установить** toocontinue.

  ![Снимок экрана: страница установки выберите установщик hello](./media/oracle-golden-gate/golden_gate_install_04.png)

6. Запрос toorun сценарий может быть как «root». В этом случае откройте отдельный сеанс, ssh toohello ВМ sudo tooroot и запустите сценарий hello. Чтобы продолжить, нажмите кнопку **ОК**.

  ![Снимок экрана: страница приветствия выберите установки](./media/oracle-golden-gate/golden_gate_install_05.png)

7. По завершении установки hello выберите **закрыть** toocomplete hello процесса.

  ![Снимок экрана: страница приветствия выберите установки](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a>Настройка службы на myVM1 (основная)

1. Создать или обновить файл tnsnames.ora hello:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Создайте hello шлюза золотые владельца и учетные записи пользователей.

  > [!NOTE]
  > Учетная запись владельца Hello должна иметь префикс C ##.
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. Создайте шлюз золотые hello тестовую учетную запись пользователя:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. Настройте файл параметров извлечения hello.

 Запуск командной строки золотой шлюза hello (ggsci):

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. Добавьте следующий параметр ИЗВЛЕЧЬ toohello файлов (с помощью команды vi) hello. Нажмите клавишу ESC, ":wq!" файл toosave. 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. Зарегистрируйте извлечение, интегрированное с помощью EXTRACT:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. Настройте контрольные точки извлечения и запустите извлечение в режиме реального времени:

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
На этом шаге найти hello начиная уведомлений SCN, который будет использоваться позже в другом разделе:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a>Настройка службы на myVM2 (репликация)


1. Создать или обновить файл tnsnames.ora hello:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Создайте учетную запись репликации:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. Создайте тестовую учетную запись пользователя Golden Gate:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. Изменения tooreplicate файл параметров REPLICAT: 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  Содержимое файла параметров REPORA:

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. Настройте контрольную точку репликации:

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a>Настройка репликации hello (myVM1 и myVM2)

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a>1. Настройка репликации hello на myVM2 (репликация)

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
Обновите файл hello hello следующее:

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
Затем перезапустите службу диспетчера hello:

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a>2. Настройка репликации hello на myVM1 (основной)

Запуск начальной загрузки hello и проверьте наличие ошибок:

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a>3. Настройка репликации hello на myVM2 (репликация)

Изменить hello SCN номер с номером hello получен до:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
начало репликации Hello и протестируйте его путем вставки новых записей tooTEST таблиц.


### <a name="view-job-status-and-troubleshooting"></a>Просмотр состояния задания и устранение неполадок

#### <a name="view-reports"></a>Просмотр отчетов
tooview сообщает myVM1, запустите следующие команды hello.

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
tooview сообщает myVM2, запустите следующие команды hello.

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a>Просмотр сведений о состоянии и журналов
tooview состояние и журнал на myVM1, запустите hello, следующие команды:

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

tooview состояние и журнал на myVM2, запустите hello, следующие команды:

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
На этом завершается hello установки и настройки шлюза золотые в Oracle linux.


## <a name="delete-hello-virtual-machine"></a>Удалить виртуальную машину hello

Когда оно больше не нужно, может быть hello следующую команду, группа ресурсов используется tooremove hello, виртуальных Машин и все связанные ресурсы.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

Изучите [руководство по созданию высокодоступных виртуальных машин](../../linux/create-cli-complete.md).

[Изучите примеры развертывания виртуальных машин с помощью интерфейса командной строки](../../linux/cli-samples.md).
