1. Скопируйте hello установщика tooa локальную папку (например, / TMP) на сервере hello, которое следует tooprotect. В конечном выполните следующие команды hello:
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. tooinstall службы Mobility Service, запустите hello следующую команду:

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. После завершения установки hello службы Mobility Service должна tooget зарегистрированных toohello конфигурации сервера. Запустите hello, следующая команда tooregister hello службы Mobility Service с сервера конфигурации.

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a>Командная строка установщика Mobility Service

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|Параметр|Тип|Описание|Возможные значения|
|-|-|-|-|
|-r |Обязательно|Указывает службу, которую нужно установить: Mobility Service (MS) или MasterTarget (MT)|MS </br> MT|
|-d |Необязательно|Расположение, в котором будет установлена служба Mobility Service|/usr/local/ASR|
|-v|Обязательно|Указывает платформу hello, на какие hello начало установлена служба Mobility </br> </br>- **VMware.** Используйте это значение при установке службы Mobility Service на виртуальной машине под управлением *узлов VMware vSphere ESXi*, *узлов Hyper-V* или *физических серверов* </br> - **Azure.** Используйте это значение при установке агента на виртуальной машине Azure IaaS| VMware </br> Таблицы Azure|
|-q|Необязательно|Указывает toorun установки в автоматическом режиме| Недоступно|


#### <a name="mobility-service-configuration-command-line"></a>Командная строка конфигурации службы Mobility Service

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|Параметр|Тип|Описание|Возможные значения|
|-|-|-|-|
|-i |Обязательно|IP-адрес сервера конфигурации hello|Любой допустимый IP-адрес|
|-P |Обязательно|Hello полный путь к файлу, сохранения парольной фразы подключения hello|Любая допустимая папка|
