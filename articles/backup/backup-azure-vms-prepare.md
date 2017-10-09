---
title: "aaaPreparing вашей среды tooback копирование виртуальных машин Azure | Документы Microsoft"
description: "Убедитесь, что ваша среда подготовлена для резервного копирования виртуальных машин в Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: "резервные копии; резервное копирование;"
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a>Подготовка к среде tooback копирование виртуальных машин Azure
> [!div class="op_single_selector"]
> * [Модель Resource Manager](backup-azure-arm-vms-prepare.md)
> * [Классическая модель](backup-azure-vms-prepare.md)
>
>

Прежде чем можно будет выполнять резервное копирование виртуальной машины Azure, необходимо обеспечить выполнение трех условий:

* Требуется toocreate резервное хранилище или определите существующий резервного хранилища *в hello же регионе, что ВМ*.
* Установите сетевое соединение между hello Azure общедоступный Интернет адреса и hello конечные точки хранилища Azure.
* Установите агент VM hello на hello виртуальной Машины.

Если известно, что эти условия уже существуют в вашей среде, то продолжить toohello [резервное копирование виртуальных машин статью](backup-azure-vms.md). В противном случае чтение, в этой статье поможет hello действия tooprepare вашей среды tooback копирование виртуальной Машины Azure.

##<a name="supported-operating-system-for-backup"></a>Поддерживаемые версии операционных систем для архивации
 * **Linux**: служба архивации Azure поддерживает весь [список дистрибутивов, рекомендуемых для использования в Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , за исключением CoreOS Linux. _Также другие перевести-Your-владельцем-дистрибутивы Linux могут работать, пока агент ВМ hello доступен на виртуальной машине hello и поддержку существует Python. Тем не менее мы не поддерживаем использование этих дистрибутивов для архивации._
 * **Windows Server**: версии до Windows Server 2008 R2 не поддерживаются.


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Ограничения при резервном копировании и восстановлении виртуальной машины
> [!NOTE]
> В Azure предусмотрены две модели развертывания, позволяющие создавать ресурсы и работать с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). Hello ниже приведены ограничения hello при развертывании в классической модели hello.
>
>

* Архивация виртуальных машин, к которым подключено более 16 дисков данных, не поддерживается.
* Архивация виртуальных машин с зарезервированным IP-адресом и без заданной конечной точки не поддерживается.
* Резервных копий данных не содержит tooVM диски, подключенные сети подключены.
* Замена существующей виртуальной машины во время восстановления не поддерживается. Сначала удалите существующую виртуальную машину hello и любые связанные диски, а затем восстановите hello данных из резервной копии.
* Резервное копирования и восстановление между регионами не поддерживается.
* Резервное копирование виртуальных машин с помощью службы архивации Azure hello поддерживается во всех регионах общих служб Azure (в разделе hello [контрольный список](https://azure.microsoft.com/regions/#services) поддерживаемых регионов). Если сегодня не поддерживается hello региона, который вы ищете, его не появятся в раскрывающемся списке hello во время создания хранилища.
* Резервное копирование виртуальных машин с помощью службы архивации Azure hello поддерживается только для выбора версий операционной системы:
* Восстановление контроллера домена виртуальной машины, которая входит в конфигурацию с несколькими контроллерами домена, поддерживается только с помощью PowerShell. Дополнительные сведения о [восстановлении контроллера домена в конфигурации с несколькими контроллерами домена](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Восстановление виртуальных машин, которые имеют специальные сетевые конфигурации hello поддерживается только с помощью PowerShell. Виртуальные машины, созданные с помощью рабочего процесса восстановления hello в hello пользовательского интерфейса не будет иметь эти конфигурации сети после завершения операции восстановления hello. toolearn более, в разделе [восстановление виртуальных машин с конфигурацией сети специальные](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Виртуальные машины в конфигурации балансировщика нагрузки (внутренняя и внешняя)
  * Виртуальные машины с несколькими зарезервированными IP-адресами
  * Виртуальные машины с несколькими сетевыми адаптерами

## <a name="create-a-backup-vault-for-a-vm"></a>Создание хранилища архивации для виртуальной машины
Резервное хранилище — это сущность, которой хранятся все резервные копии hello и точек восстановления, которые были созданы со временем. резервное хранилище Hello также содержит hello политики резервного копирования, которые будут применяться toohello виртуальных машин, резервная копия.

> [!IMPORTANT]
> Запуск марта 2017 г., можно использовать больше не hello классического портала toocreate резервное копирование хранилищ. Существующие хранилища резервной копии по-прежнему поддерживаются, и пользователь может слишком[использовать хранилищах службы архивации Azure PowerShell toocreate](./backup-client-automation-classic.md#create-a-backup-vault). Тем не менее, корпорация Майкрософт рекомендует создать хранилищами служб восстановления для всех развертываний, поскольку в будущем применить хранилищами служб tooRecovery, только.


На данном рисунке показан hello связи между hello различных сущностей резервного копирования Azure: ![резервного копирования Azure сущностей и связей](./media/backup-azure-vms-prepare/vault-policy-vm.png)



## <a name="network-connectivity"></a>Сетевое подключение
Моментальные снимки виртуальной Машины hello toomanage заказа, расширение резервного копирования hello должен toohello подключения к Azure общих IP-адресов. Без hello правой подключение к Интернету, hello виртуальной машины HTTP запросов время ожидания и hello, произойдет сбой архивации. Если для развертывания установлены ограничения доступа на месте, например, через группу безопасности сети (NSG), выберите один из следующих вариантов, чтобы открыть путь для трафика архивации:

* [Диапазоны IP-адресов белого списка hello центра обработки данных Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -см. в статье hello инструкции на как toowhitelist hello IP-адресов.
* Разверните прокси-сервер HTTP для маршрутизации трафика.

При определении того, какой параметр toouse, компромиссы hello находятся в диапазоне от управляемость, высокий уровень контроля и затрат.

| Параметр | Преимущества | Недостатки |
| --- | --- | --- |
| Разрешенные диапазоны IP-адресов |Нет дополнительных затрат.<br><br>Для открытия доступа в NSG, используйте hello <i>AzureNetworkSecurityRule набор</i> командлета. |Сложные toomanage как диапазоны IP hello затронутые изменяются с течением времени.<br><br>Предоставляет доступ целиком toohello Azure, а не только хранения. |
| Прокси-сервер HTTP |Четко контролировать в прокси hello hello хранилища допускается URL-адреса. детальный контроль toosetup в прокси hello https://\*.blob.core.windows.net/\* toobe входят требуется шаблон URL-адреса. toowhitelist только hello учетной записи хранения, используемые hello виртуальной Машины, https://\<storageAccount\>.blob.core.windows.net/\* toobe входят требуется шаблон URL-адреса. <br>Точка Интернет tooVMs доступа.<br>Не субъекта tooAzure изменения IP-адреса. |Дополнительные затраты для запуска виртуальной Машины с программным обеспечением hello прокси-сервера. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Диапазоны IP-адресов белого списка hello центра обработки данных Azure
диапазоны IP-toowhitelist hello центра обработки данных Azure, см. в разделе hello [веб-сайте Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) подробные сведения о диапазоны IP-адресов hello и инструкции.

### <a name="using-an-http-proxy-for-vm-backups"></a>Использование прокси-сервера HTTP для архивации виртуальных машин
При резервном копировании виртуальной Машины, hello расширение резервного копирования на hello ВМ отправляет команды управления tooAzure хранилища с помощью HTTPS API для hello моментального снимка. Маршрутизации трафика hello расширение резервного копирования через прокси-сервер hello HTTP, так как она является единственным компонентом hello настроен для доступа к toohello общедоступный Интернет.

> [!NOTE]
> Нет рекомендаций для прокси-сервера hello программного обеспечения, который следует использовать. Убедитесь, Выбор учетной записи-посредника, имеющий исходящих stickiness и совместимый с ниже действия по настройке hello. Убедитесь, что программное обеспечение сторонних производителей, не изменяйте параметры прокси-сервера hello
>
>

Изображение примера Hello ниже показаны шаги три конфигурации hello необходимые toouse HTTP прокси-сервера:

* Маршруты ВМ приложения привязаны весь трафик HTTP для hello общедоступный Интернет через прокси-сервера виртуальной Машины.
* Прокси-сервера виртуальной Машины позволяет входящий трафик из виртуальных машин в виртуальной сети hello.
* Hello сетевой безопасности группы (NSG) с именем денежным Покрытием блокировки должен безопасности правило разрешает исходящий Интернет-трафик от виртуальной Машины прокси-сервера.

![Диаграмма развертывания NSG с прокси-сервером HTTP](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toohello toocommunicating прокси-сервера toouse HTTP общедоступный Интернет, выполните следующие действия:

#### <a name="step-1-configure-outgoing-network-connections"></a>Шаг 1. Настройка исходящих сетевых подключений
###### <a name="for-windows-machines"></a>Для компьютеров Windows
Следующая процедура позволяет настроить конфигурацию прокси-сервера для учетной записи Local System.

1. Скачайте программу [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Выполните следующую команду из командной строки с повышенными привилегиями:

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Откроется окно Internet Explorer.
3. Go tooTools -> Параметры Интернета -> соединения -> Параметры локальной сети.
4. Проверьте параметры прокси-сервера для системной учетной записи. Задайте IP-адрес прокси-сервера и порт.
5. Закройте Internet Explorer.

В результате для компьютера будет настроен прокси-сервер, который будет использоваться для любого исходящего трафика HTTP или HTTPS.

Если вы настроили прокси-сервер для текущей учетной записи пользователя (не учетной записи Local System), используйте hello следующий скрипт tooapply их tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Если в журнале прокси-сервера отобразится сообщение "407 — Требуется проверка подлинности прокси", проверьте правильность настройки аутентификации.
>
>

###### <a name="for-linux-machines"></a>Для компьютеров Linux
Добавьте следующие строки toohello hello ```/etc/environment``` файла:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Добавьте следующие строки toohello hello ```/etc/waagent.conf``` файла:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>Шаг 2. Разрешить входящие подключения на hello прокси-сервера:
1. На hello прокси-сервера откройте брандмауэр Windows. Hello простым способом tooaccess hello брандмауэр — toosearch для брандмауэра Windows в режиме повышенной безопасности.

    ![Откройте брандмауэр hello](./media/backup-azure-vms-prepare/firewall-01.png)
2. В диалоговом окне брандмауэра Windows hello, щелкните правой кнопкой мыши **правила для входящих подключений** и нажмите кнопку **новое правило...** .

    ![Создание нового правила](./media/backup-azure-vms-prepare/firewall-02.png)
3. В hello **правило мастера**, выберите hello **настраиваемый** параметр для hello **тип правила** и нажмите кнопку **Далее**.
4. На hello tooselect страницы приветствия **программы**, выберите **все программы** и нажмите кнопку **Далее**.
5. На hello **протокол и порты** введите hello следующую информацию и нажмите кнопку **Далее**:

    ![Создание нового правила](./media/backup-azure-vms-prepare/firewall-03.png)

   * Для параметра *Тип протокола* выберите *TCP*.
   * для *локальный порт* выберите *определенные порты*, в следующее поле hello укажите hello ```<Proxy Port>``` был настроен.
   * В поле *Удаленный порт* выберите *Все порты*.

     REST hello приветствия мастера щелкните все завершаются toohello способом hello и укажите имя правила.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>Шаг 3. Добавьте toohello правило исключения NSG.
В командной строке Azure PowerShell введите следующую команду hello:

Привет, следующая команда добавляет исключение toohello NSG. Это исключение позволяет входящий TCP-трафик с любого порта на 10.0.0.5 tooany Интернет-адрес для порта 80 (HTTP) или 443 (HTTPS). Если требуется определенный порт в hello общедоступный Интернет быть убедиться, что tooadd, порт toohello ```-DestinationPortRange``` также.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

*Убедитесь, замените имена hello в примере hello hello сведения о соответствующих tooyour развертывания.*

## <a name="vm-agent"></a>Агент виртуальной машины
Перед тем как можно архивировать hello виртуальной машины Azure, необходимо убедиться, что агент ВМ Azure, hello на виртуальной машине hello установлен правильно. Так как агент виртуальной Машины hello созданных дополнительного компонента во время hello, hello виртуальной машины, убедитесь, установить его hello агент виртуальной Машины hello выбрано до подготовки hello виртуальной машины.

### <a name="manual-installation-and-update"></a>Ручная установка и обновление
агент виртуальной Машины Hello уже присутствует в виртуальных машинах, созданных на основе hello коллекции Azure. Однако виртуальные машины, которые переносятся с локальными центрами обработки данных не должны иметь установленного агента виртуальной Машины hello. Для таких виртуальных машин агент ВМ hello должен toobe установлен явным образом. Дополнительные сведения о [Установка агента ВМ hello на существующей виртуальной Машины](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

| **Операция** | **Windows** | **Linux** |
| --- | --- | --- |
| Установка агента ВМ hello |<li>Загрузите и установите hello [MSI агента](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Вам потребуется установки hello toocomplete права администратора. <li>[Обновить свойства виртуальной Машины hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate, hello агент установлен. |<li> Установить последние hello [агент Linux](https://github.com/Azure/WALinuxAgent) из GitHub. Вам потребуется установки hello toocomplete права администратора. <li> [Обновить свойства виртуальной Машины hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate, hello агент установлен. |
| Обновление агента ВМ hello |Обновление агента ВМ hello сводится переустановку hello [двоичные файлы агента виртуальной Машины](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br><br>Убедитесь, что операция резервного копирования, не запущен агент виртуальной Машины hello в процессе обновления. |Следуйте инструкциям hello на [обновление hello агент виртуальной Машины Linux ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br><br>Убедитесь, что операция резервного копирования, не запущен агент виртуальной Машины hello в процессе обновления. |
| Проверка установки агента виртуальной Машины hello |<li>Перейдите toohello *C:\WindowsAzure\Packages* папки в hello виртуальной Машине Azure. <li>Должен находиться файл WaAppAgent.exe hello присутствует.<li> Щелкните правой кнопкой мыши файл hello, перейдите в слишком**свойства**и затем выберите hello **сведения** версия продукта hello. поле должно быть 2.6.1198.718 или более поздней версии. |Недоступно |

Дополнительные сведения о hello [агент виртуальной Машины](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) и [как tooinstall его](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).

### <a name="backup-extension"></a>Расширение резервного копирования
tooback hello виртуальной машины hello службы архивации Azure устанавливает агент ВМ toohello расширения. Hello службы резервного копирования Azure легко обновления и исправления hello расширение резервного копирования без дополнительного вмешательства пользователя.

расширение резервного копирования Hello устанавливается в том случае, если выполняется hello виртуальной Машины. Работающей виртуальной Машины также предоставляет hello наибольшую вероятность нахождения точки восстановления, согласованные с приложениями. Однако hello Azure Backup будет продолжать работу службы tooback копирование hello виртуальной Машины — даже в том случае, если он был отключен, и расширение hello не может быть установлен (также называемого автономной виртуальной Машины). В этом случае hello точка восстановления будет *сбоям* как описано выше.

## <a name="questions"></a>Вопросы?
Если у вас есть вопросы или при наличии любой возможности, хотелось бы включены, toosee [отправить отзыв](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы подготовили среду для резервного копирования виртуальной Машины, логические следующим шагом является toocreate резервной копии. Планирование статьи Hello содержатся более подробные сведения о резервном копировании виртуальных машин.

* [Настройка виртуальных машин](backup-azure-vms.md)
* [Планирование инфраструктуры резервного копирования виртуальных машин в Azure](backup-azure-vms-introduction.md)
* [Управление резервными копиями виртуальной машины](backup-azure-manage-vms.md)
