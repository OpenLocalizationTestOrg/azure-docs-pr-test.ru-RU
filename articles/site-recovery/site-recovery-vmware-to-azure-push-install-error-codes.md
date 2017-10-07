---
title: "Устранение неполадок Site Recovery aaaAzure из VMware tooAzure | Документы Microsoft"
description: "Устранение ошибок при репликации виртуальных машин Azure."
services: site-recovery
documentationcenter: 
author: asgang
manager: srinathv
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/24/2017
ms.author: asgang
ms.openlocfilehash: 912097c8892540dd798ba025e0b10374ca51d664
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>Устранение неполадок с принудительной установкой службы Mobility Service

В этой статье указаны hello распространенных проблем при попытке hello tooinstall службы Mobility Service на сервере toosource для включения защиты.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>Не удалось включить защиту (код ошибки 95107)
**Код ошибки** | **Возможные причины** | **Рекомендации по устранению ошибки**
--- | --- | ---
95107 </br>***Сообщение —*** принудительной установки hello mobility service toohello исходной машины завершилось ошибкой с кодом ***EP0858***. <br> Предоставление hello учетные данные службы mobility service tooinstall неверный или hello учетная запись пользователя имеет недостаточно прав доступа | Учетные данные пользователя при условии, что неверный tooinstall служба mobility service на исходном компьютере | Проверьте, правильность hello учетным данным пользователя для hello исходного компьютера на сервере конфигурации. <br> tooadd или изменить учетные данные пользователя: перейдите tooconfiguration server > значок Cspsconfigtool > Управление учетной записью. </br> Кроме того, убедитесь, ниже предварительных требований отмеченных toosuccessfully завершения извещающей установки.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>Не удалось включить защиту (код ошибки 95015)
**Код ошибки** | **Возможные причины** | **Рекомендации по устранению ошибки**
--- | --- | ---
95105 </br>***Сообщение —*** принудительной установки hello mobility service toohello исходной машины завершилось ошибкой с кодом ***EP0856***. <br> «Файл и принтерам» запрещено на исходном компьютере hello или имеются проблемы с сетевым соединением между сервером обработки hello и hello исходного компьютера| Общий доступ к файлам и принтерам выключен. | Разрешить «Файла и общий доступ к принтеру» на исходном компьютере hello в hello брандмауэр Windows, Go toohello исходного компьютера > Параметры в группе брандмауэра Windows > «Разрешить запуск программы или компонента через брандмауэр» > выберите «Файл и совместного использования принтеров для всех профилей». </br> Кроме того, убедитесь, ниже предварительных требований отмеченных toosuccessfully завершения извещающей установки.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>Не удалось включить защиту (код ошибки 95117)
**Код ошибки** | **Возможные причины** | **Рекомендации по устранению ошибки**
--- | --- | ---
95117 </br>***Сообщение —*** принудительной установки hello mobility service toohello исходной машины завершилось ошибкой с кодом ***EP0865***. <br> Либо hello исходный компьютер не запущен, или возникли проблемы с сетевым соединением между сервером обработки hello и hello исходного компьютера | Проблемы с сетевым соединением между сервером обработки и исходным компьютером. | Проверьте сетевое соединение между сервером обработки и исходным компьютером. </br> Кроме того, убедитесь, ниже предварительных требований отмеченных toosuccessfully завершения извещающей установки.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>Не удалось включить защиту (код ошибки 95103)
**Код ошибки** | **Возможные причины** | **Рекомендации по устранению ошибки**
--- | --- | ---
95103 </br>***Сообщение —*** принудительной установки hello mobility service toohello исходной машины завершилось ошибкой с кодом ***EP0854***. <br> «Инструментария управления Windows (WMI) "не разрешен на исходном компьютере hello или имеются проблемы с сетевым соединением между сервером обработки hello и hello исходного компьютера| В брандмауэре Windows hello блокируется инструментария управления Windows (WMI) | Разрешает инструментария управления Windows (WMI) в брандмауэре Windows hello. В группе параметров брандмауэра Windows выберите параметр Allow an app or feature through Firewall (Разрешить запуск программы или компонента через брандмауэр) и выберите WMI для всех профилей. </br> Кроме того, убедитесь, ниже предварительных требований отмеченных toosuccessfully завершения извещающей установки.

## <a name="check-push-install-logs-for-errors"></a>Проверка журналов принудительных установок на наличие ошибок

На сервере конфигурации или процесс hello, перейдите в «PushinstallService», расположенный toofile <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand hello источника проблемы hello, и используйте ниже устранения проблемы hello tooresolve действия.</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Необходимые компоненты для принудительной установки в Windows
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>Обеспечение общего доступа к файлам и принтерам
Разрешить «И принтера общего доступа» и «Инструментарий управления Windows» на исходном компьютере hello в брандмауэре Windows hello </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>Если исходный компьютер присоединен к домену, сделайте следующее: </br>
Настройте параметры брандмауэра с помощью консоли управления групповыми политиками (GPMC).
1. Машины домена directory tooActive входа в систему как администратор и откройте консоль управления групповыми политиками (GPMC. MSC, запустите из начала > запустить).</br>
3. Если консоль управления групповыми Политиками не установлен, по ссылке hello слишком[hello установки консоли управления групповыми Политиками](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. В дереве консоли управления групповыми Политиками hello, дважды щелкните объекты групповой политики в hello леса и домена и перейдите слишком «Политика домена по умолчанию». </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. Щелкните правой кнопкой мыши политику домена по умолчанию и выберите "Изменить". Откроется новое окно "Редактор управления групповыми политиками". </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. Hello редактор управления групповыми политиками перейдите tooComputer конфигурации > политики > Административные шаблоны > сеть > Сетевые подключения > брандмауэр Windows. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. Включить следующие параметры для профиля домена и стандартный профиль hello </br>
а) Дважды щелкните исключение "Брандмауэр Windows: разрешить исключение для входящего общего доступа к файлам и принтерам". Выберите "Включено" и нажмите кнопку ОК. </br>
б) Дважды щелкните исключение "Брандмауэр Windows: разрешить исключение для входящих сообщений удаленного администрирования". Выберите "Включено" и нажмите кнопку ОК. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>Если исходный компьютер не присоединен к домену и не является частью рабочей группы, выполните указанные ниже действия. </br>
Настройте параметры брандмауэра на удаленном компьютере (для рабочей группы).
1. Перейдите на исходном компьютере toohello</br>
2. в группе параметров брандмауэра Windows выберите параметр Allow an app or feature through Firewall (Разрешить запуск программы или компонента через брандмауэр) и File and Printer Sharing for all profiles (Общий доступ к файлам и принтерам для всех профилей). </br>
3. В группе параметров брандмауэра Windows выберите параметр Allow an app or feature through Firewall (Разрешить запуск программы или компонента через брандмауэр) и выберите WMI для всех профилей. </br>

#### <a name="disable-remote-user-account-control-uac"></a>Отключение функции удаленного контроля учетных записей (UAC)
Отключите контроль учетных Записей с помощью службы мобильности hello toopush ключа реестра.
1. Нажмите кнопку "Пуск > Выполнить", введите regedit и нажмите клавишу ВВОД.
2. Найдите и выделите следующий подраздел реестра hello: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. Если параметр реестра LocalAccountTokenFilterPolicy hello не существует, выполните следующие действия.
4. В меню Правка hello > Создать > щелкните значение DWORD.
5. Введите LocalAccountTokenFilterPolicy и нажмите клавишу ВВОД.
6. Щелкните правой кнопкой мыши LocalAccountTokenFilterPolicy и выберите "Изменить".
7. В значение hello введите значение 1 и нажмите кнопку ОК.
8. Закройте редактор реестра.


## <a name="push-install-pre-requisites-for-linux"></a>Необходимые компоненты для принудительной установки в Linux

1. Создайте привилегированного пользователя на сервере Linux hello источника. (Используйте эту учетную запись только для hello принудительной установки и обновления)</br>
2. Проверьте этот файл hello/etc/hosts на исходном hello Linux, сервер имеет записей, которые сопоставления адресов tooIP hello локальному имени узла, связанный со всеми сетевыми адаптерами. </br>
3. Убедитесь, что hello последнюю openssh openssh сервера и openssl пакеты устанавливаются на исходном сервере Linux. </br>
Убедитесь, что SSH-порт 22 включен и работает. </br>
4. Проверьте, если устаревшие записи агентов уже присутствуют на исходном сервере hello, удалите старую агенты hello и перезагрузите сервер hello, переустановите агент. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a>Включить SFTP подсистемы и проверку подлинности в файле sshd_config hello
1. Выполните вход в качестве привилегированного пользователя на исходном сервере. </br>
2. В файле /etc/ssh/sshd_config файл hello</br> найти строку hello, начинающееся с PasswordAuthentication. </br>
3. d.   Раскомментируйте строку hello и измените значение «Нет» hello слишком «Да». </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. Найдите строку hello, начинающимся с «Подсистемы» и раскомментируйте строку hello. </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Сохранить изменения hello и перезапустите службу hello sshd. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>Проверка принудительной установки на сервере конфигурации или сервере обработки
#### <a name="validate-credentials-for-discovery-and-installation"></a>Проверка учетных данных для обнаружения и установки

1. На сервере конфигурации запустите файл Cspsconfigtool.</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. Убедитесь, что hello учетной записи, используемой для защиты имеет права администратора на исходном компьютере hello. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>Проверка сетевого соединения между сервером обработки и исходным компьютером
1. Убедитесь, что сервер обработки имеет подключение к Интернету.
2. Проверьте подключение WMI с помощью wbemtest.exe. </br>
На сервере обработки hello, нажмите кнопку Пуск > выполнить > wbemtest.exe > будет открыть окно Тестер инструментария управления Windows, как показано.</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
Щелкните подключение > введите IP-адрес сервера источника hello в приветствия имен входных данных пользователя и пароль (если исходный компьютер присоединен к домену, укажите имя домена hello вместе с именем пользователя «Имя_домена\имя_пользователя». Если исходный компьютер входит в рабочую группу, укажите только hello имя пользователя.) Выберите уровень проверки подлинности hello как защита пакетов. </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   Щелкните "Подключение". Теперь hello WMI-соединения, должна быть установлена с помощью предоставленных данных hello и должны отображаться окна Тестер инструментария управления Windows hello, как показано ниже: </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   Если при подключении к WMI произойдет сбой, отобразится всплывающее окно сообщения об ошибке. Привет, приведенном ниже снимке экрана показано Неудачная попытка включения WMI и удаленного администрирования в брандмауэре Windows, приложение может не. </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. Проверьте состояние WMI hello и подключения.</br>
На сервере конфигурации или процесс hello </br>
Нажмите кнопку Пуск > выполнить > wmimgmt.msc > действия > Дополнительные действия > подключения компьютера tooanother (исходной машины). </br>
Введите учетные данные hello hello учетной записи, используемой для защиты и проверки, если подключение к нормально. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>Убедитесь, что вы можете получить удаленный доступ к общим сетевым папкам исходного компьютера с сервера обработки с помощью указанных учетных данных.
  1. TooProcess сервера (PS) входа в систему компьютера, откройте проводник > в адрес hello bar-тип > "\\\source-machine-ip\C$» > нажмите клавишу ВВОД. </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. Обозреватель файлов запросит учетные данные. Введите hello пользователя и пароль > нажмите кнопку ОК.</br>
   Если исходный компьютер присоединен к домену, укажите имя домена hello вместе с именем пользователя как «Имя_домена\имя_пользователя».</br>
   Если исходный компьютер входит в рабочую группу, укажите только hello «username». </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. Если подключение установлено успешно, можно просмотреть папки hello исходной машины удаленно из процесса сервера (PS). </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> Если подключение завершилось сбоем, проверьте, соблюдены ли все предварительные требования.
>

Если вы не хотите tooopen «Инструментарий управления Windows», можно также установить службу mobility service вручную на исходном компьютере hello.</br> [Установка службы Mobility Service вручную с помощью графического пользовательского интерфейса](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[Автоматизация установки Mobility Service с использованием средств развертывания программного обеспечения](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>Дальнейшие действия
- [Шаг 11. Включение репликации для виртуальных машин VMware, реплицируемых в Azure](vmware-walkthrough-enable-replication.md)
