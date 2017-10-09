1. Скопируйте hello установщика tooa локальную папку (например, C:\Temp) на сервере hello, которое следует tooprotect. Выполните следующие команды от имени администратора, в командной строке hello.

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. tooinstall службы Mobility Service, запустите hello следующую команду:

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. Теперь агент hello должен toobe зарегистрирована hello сервера конфигурации.

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a>Команда установщика службы Mobility Service: аргументы строки

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| Параметр|Тип|Описание|Возможные значения|
|-|-|-|-|
|/Role|Обязательно|Указывает службу, которую нужно установить: Mobility Service (MS) или MasterTarget (MT)|MS </br> MT|
|/InstallLocation|Необязательно|Расположение, в котором установлена служба Mobility Service|Любой папке на компьютере hello|
|/Platform|Обязательно|Указывает платформу hello, на какие hello начало установлена служба Mobility </br> </br>- **VMware.** Используйте это значение при установке службы Mobility Service на виртуальной машине под управлением *узлов VMware vSphere ESXi*, *узлов Hyper-V* или *физических серверов* </br> - **Azure.** Используйте это значение при установке агента на виртуальной машине Azure IaaS| VMware </br> Таблицы Azure|
|/Silent|Необязательно|Задает установщик toorun hello в автоматическом режиме| Нет данных|

>[!TIP]
> журналы установки Hello можно найти в разделе %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log

#### <a name="mobility-service-registration-command-line-arguments"></a>Аргументы командной строки регистрации службы Mobility Service

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | Параметр|Тип|Описание|Возможные значения|
  |-|-|-|-|
  |/CSEndPoint |Обязательно|IP-адрес сервера конфигурации hello| Любой допустимый IP-адрес|
  |/PassphraseFilePath|Обязательно|Расположение hello парольная фраза |Любой допустимый локальный путь к файлу или UNC|


>[!TIP]
> Hello AgentConfiguration журналы можно найти в разделе %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log
