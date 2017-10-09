---
title: "проблемы с развертыванием StorSimple aaaTroubleshoot | Документы Microsoft"
description: "Описывает способ toodiagnose и исправление ошибок, возникающих при развертывании StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f8352eaa-193c-42d1-8818-0b8e02d8485d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 9a31a3cfb3be577500b226c2bc8172dd8664bad9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storsimple-device-deployment-issues"></a>Устранение неполадок в развертывании устройства StorSimple
## <a name="overview"></a>Обзор
Эта статья содержит полезные рекомендации по устранению неполадок в развертывании системы Microsoft Azure StorSimple. Он описывает распространенные проблемы, возможные причины и рекомендуемые действия toohelp решать проблемы, которые могут возникнуть при настройке StorSimple. Эти сведения относятся физических устройств StorSimple hello локальной tooboth и виртуальное устройство StorSimple hello.

> [!NOTE]
> При при первом развертывании hello устройства для hello, или они более поздней версии, может возникнуть при hello устройство работоспособно, могут возникать проблемы, связанные с конфигурации устройства, которыми вы можете столкнуться. В данной статье рассматривается устранение неполадок при развертывании устройства впервые. tootroubleshoot рабочего устройства go слишком[Устранение неполадок рабочего устройства](storsimple-troubleshoot-operational-device.md).
> 
> 

В этой статье также описывается hello средства по устранению неполадок развертываний StorSimple и примеры с пошаговыми инструкциями по устранению неполадок.

## <a name="first-time-deployment-issues"></a>Проблемы при первом развертывании
Если возникли проблемы при развертывании устройства для hello в первый раз, необходимо учитывайте следующие hello:

* При устранении неполадок физического устройства, убедитесь, что оборудование hello установлен и настроен, как описано в [установки устройства StorSimple 8100](storsimple-8100-hardware-installation.md) или [установки устройства StorSimple 8600](storsimple-8600-hardware-installation.md).
* Проверьте, соблюдены ли предварительные требования, связанные с развертыванием. Убедитесь, что все hello сведения, описанные в hello [контрольный список для настройки развертывания](storsimple-deployment-walkthrough.md#deployment-configuration-checklist).
* Изучите заметки о выпуске StorSimple toosee hello, если описание проблемы hello. Hello заметки о выпуске содержат пути решения известных проблем установки. 

Во время развертывания устройства hello наиболее распространенных проблем у пользователей возникают начертания, во время выполнения мастера установки hello и при их регистрации hello устройство с помощью Windows PowerShell для StorSimple. (Чтобы использовать Windows PowerShell для StorSimple tooregister и настроить устройства StorSimple. Подробные сведения о регистрации устройства см. в разделе [Шаг 3. Настройка и регистрация устройства средствами Windows PowerShell для StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)).

Hello в следующих разделах помогут вам решить проблемы, возникающие при настройке устройства StorSimple hello для hello первый раз.

## <a name="first-time-setup-wizard-process"></a>Работа с мастером установки в первый раз
Привет, следующие шаги описывают мастер установки hello. Подробные сведения об установке и настройке см. в статье [Развертывание локального устройства StorSimple](storsimple-deployment-walkthrough.md).

1. Запустите hello [Invoke-HcsSetupWizard](https://technet.microsoft.com/library/dn688135.aspx) командлет toostart hello мастер установки, который поможет выполнить hello, оставшиеся шаги. 
2. Настройка сети hello: hello мастер установки позволяет настроить параметры сети для hello сетевого интерфейса DATA 0 на устройстве StorSimple. Эти параметры включают hello следующее:
   * Виртуальный IP-адресов, маску подсети и шлюз — hello [Set-HcsNetInterface](https://technet.microsoft.com/library/dn688161.aspx) выполняется в фоновом режиме hello. Настраивает hello IP-адрес, маску подсети и шлюз для hello сетевого интерфейса DATA 0 на устройстве StorSimple.
   * Основной DNS-сервер — hello [Set-HcsDnsClientServerAddress](https://technet.microsoft.com/library/dn688172.aspx) выполняется в фоновом режиме hello. Настраивает параметры DNS hello для решения StorSimple.
   * NTP-сервер — hello [Set-HcsNtpClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) выполняется в фоновом режиме hello. Настраивает параметры NTP-сервера hello для решения StorSimple.
   * Необязательный веб-прокси-сервер — hello [Set-HcsWebProxy](https://technet.microsoft.com/library/dn688154.aspx) выполняется в фоновом режиме hello. Задает и включает hello конфигурацию веб-прокси для решения StorSimple.
3. Настроить пароли hello: hello следующим шагом является tooset администратора устройства и диспетчера моментальных снимков StorSimple пароли. При выполнении обновления 1 будет не быть необходимых tooset пароль диспетчера моментальных снимков StorSimple hello.
   
   * пароль администратора устройства Hello — используется toolog tooyour устройства. пароль устройства по умолчанию Hello **Password1**.
   * пароль диспетчера моментальных снимков StorSimple Hello необходим при настройке toouse устройства диспетчера моментальных снимков StorSimple. Вам необходим пароль hello набор toofirst приветствия мастера установки, и затем можно задать и изменить его из hello в службе StorSimple Manager. Этот пароль проверяет hello устройство StorSimple Snapshot Manager.
     
     > [!IMPORTANT]
     > Пароли собираются до регистрации, но применяются только после успешной регистрации устройства hello. Если имеется tooapply сбоя пароль, будет запрашиваемые toosupply hello пароль еще раз до hello необходимые пароли (отвечающие требованиям сложности hello) будут собраны.
     > 
     > 
4. Регистрация устройства hello: hello последний шаг — tooregister hello устройства в службе StorSimple Manager hello, работающие в Microsoft Azure. Hello регистрации требует слишком[получить ключ регистрации службы hello](storsimple-manage-service.md#get-the-service-registration-key) из классического портала Azure hello и предоставить его приветствия мастера установки. После успешной регистрации устройства hello, ключ шифрования данных службы предоставляется tooyou. Убедитесь, что шифрование ключей в безопасном месте, так как они будут tookeep необходимые tooregister всех последующих устройств со службой hello.

## <a name="common-errors-during-device-deployment"></a>Распространенные ошибки при развертывании устройства
Здравствуйте, следующие таблицы список hello распространенные ошибки, могут возникнуть, когда вы:

* Настройка параметров сети требуется hello.
* Настройка hello необязательный веб-прокси.
* Настройка диспетчера моментальных снимков StorSimple паролей администратора устройства hello и. 
* Регистрация устройства hello. 

## <a name="errors-during-hello-required-network-settings"></a>Ошибки во время hello необходимые параметры сети
| Нет. | Сообщение об ошибке | Возможные причины | Рекомендуемое действие |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: Эта команда может выполняться только на активном контроллере hello. |Настройка выполнялась на пассивном контроллере hello. |Выполните следующую команду из активного контроллера hello. Дополнительные сведения см. в разделе [Определение активного контроллера устройства](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device). |
| 2 |Invoke-HcsSetupWizard: устройство не готово. |Имеются проблемы с сетевым подключением DATA 0 hello. |Проверьте hello физическое подключение сети к DATA 0. |
| 3 |Invoke-HcsSetupWizard: Имеется конфликт IP-адресов с другой системой в сети hello (исключение из HRESULT: 0x80070263). |Hello IP, предоставленный для DATA 0, уже используется другой системой. |Укажите новый IP-адрес, который еще не используется. |
| 4 |Invoke-HcsSetupWizard: сбой ресурса кластера (исключение из HRESULT: 0x800713AE). |Дублирование виртуальных IP-адресов. Hello указан IP-адрес уже используется. |Укажите новый IP-адрес, который еще не используется. |
| 5 |Invoke-HcsSetupWizard: недопустимый IPv4-адрес. |Hello IP-адрес указан в неверном формате. |Проверьте формат hello и снова введите IP-адреса. Дополнительные сведения см. на странице [Адресация IPv4][1]. |
| 6 |Invoke-HcsSetupWizard: недопустимый IPv6-адрес. |Hello IP-адрес указан в неверном формате. |Проверьте формат hello и снова введите IP-адреса. Дополнительные сведения см. на странице [Адресация IPv6][2]. |
| 7 |Invoke-HcsSetupWizard: Доступны дополнительные конечные точки из сопоставителя конечных точек hello. (Исключение из HRESULT: 0x800706D9) |функция кластерного Hello не работает. |[Обратитесь в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md) , чтобы узнать, что делать дальше. |

## <a name="errors-during-hello-optional-web-proxy-settings"></a>Ошибки во время hello необязательный веб-параметры прокси-сервера
| Нет. | Сообщение об ошибке | Возможные причины | Рекомендуемое действие |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: недопустимый параметр (исключение из HRESULT: 0x80070057) |Один из параметров hello, указанных для hello параметры прокси-сервера является недопустимым. |Hello URI не указан в неправильном формате hello. Hello используйте следующий формат: http://*<IP address or FQDN of hello web proxy server>*:*<TCP port number>* |
| 2 |Invoke-HcsSetupWizard: RPC-сервер недоступен (исключение из HRESULT: 0x800706ba) |Hello основной причиной является одна из следующих hello:<ol><li>Hello кластер не работает.</li><li>Hello пассивный контроллер не может взаимодействовать с активным контроллером hello и hello команду из пассивного контроллера.</li></ol> |В зависимости от основной причины hello:<ol><li>[Обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md) toomake убедиться, что кластер hello работает.</li><li>Выполните команду hello из активного контроллера hello. Если вы хотите toorun hello команду из пассивного контроллера hello, необходимо будет tooensure, hello пассивный контроллер может взаимодействовать с активным контроллером hello. Необходимо будет слишком[обратитесь в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md) Если подключение будет прервано.</li></ol> |
| 3 |Invoke-HcsSetupWizard: сбой вызова RPC (исключение из HRESULT: 0x800706be) |Кластер не работает. |[Обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md) toomake убедиться, что кластер hello работает. |
| 4. |Invoke-HcsSetupWizard: ресурс кластера не найден (исключение из HRESULT: 0x8007138f) |ресурс кластера Hello не найден. Это может произойти, если установка hello не была правильно. |Может потребоваться tooreset hello устройства toohello заводские настройки по умолчанию. [Обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md) toocreate ресурса кластера. |
| 5 |Invoke-HcsSetupWizard: ресурс кластера не подключен к сети (исключение из HRESULT: 0x8007138c) |Ресурсы кластера отключены от сети. |[Обратитесь в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md) , чтобы узнать, что делать дальше. |

## <a name="errors-related-toodevice-administrator-and-storsimple-snapshot-manager-passwords"></a>Ошибки, связанные с toodevice администратора и пароль диспетчера моментальных снимков StorSimple
пароль администратора устройства по умолчанию Hello **Password1**. Этот пароль становится недействительным после первого входа hello; Таким образом, вам потребуется toochange мастер установки hello toouse его. При регистрации устройства hello для hello первый раз, необходимо указать новый пароль администратора устройства. 

При использовании hello диспетчера моментальных снимков StorSimple программного обеспечения на устройство hello toomanage узла Windows Server hello, то необходимо также указать пароль StorSimple Snapshot Manager во время первоначальной регистрации. 

Убедитесь, что пароли соответствуют hello следующие требования:

* Требуемая длина пароля администратора устройства: от 8 до 15 символов.
* Требуемая длина пароля диспетчера моментальных снимков StorSimple: 14 или 15 символов.
* Пароли должны содержать 3 из hello следующие 4 типов знаков: строчные, верхнем регистре, цифры и специальные. 
* Пароль не может hello равна hello последние 24 пароля.

Кроме того Имейте в виду, что каждый год истечении срока действия паролей и могут быть изменены только после успешной регистрации устройства hello. Если какой-либо причине произошел сбой регистрации hello, hello пароли не будут изменены. Дополнительные сведения о StorSimple Snapshot Manager паролей администратора устройства и перейти слишком[используйте hello toochange службы диспетчера StorSimple паролей StorSimple](storsimple-change-passwords.md).

Может появиться одно или несколько следующие ошибки при настройке диспетчера моментальных снимков StorSimple паролей администратора устройства hello и hello.

| Нет. | Сообщение об ошибке | Рекомендуемое действие |
| --- | --- | --- |
| 1 |Превышена максимальная длина hello Hello пароля. |Используйте пароль, который отвечает следующим требованиям:<ul><li>Требуемая длина пароля администратора устройства: от 8 до 15 знаков.</li><li>Требуемая длина пароля StorSimple Snapshot Manager: 14 или 15 знаков.</li></ul> |
| 2 |Hello пароль не соответствует длине необходимые hello. |Используйте пароль, который отвечает следующим требованиям:<ul><li>Требуемая длина пароля администратора устройства: от 8 до 15 знаков.</li><li>Требуемая длина пароля StorSimple Snapshot Manager: 14 или 15 знаков.</lu></ul> |
| 3 |Hello пароль должен содержать символы нижнего регистра. |Пароли должны содержать 3 из hello следующие 4 типов знаков: строчные, верхнем регистре, цифры и специальные. Убедитесь, что пароль отвечает этим требованиям. |
| 4. |Hello пароль должен содержать цифры. |Пароли должны содержать 3 из hello следующие 4 типов знаков: строчные, верхнем регистре, цифры и специальные. Убедитесь, что пароль отвечает этим требованиям. |
| 5 |Hello пароль должен содержать специальные символы. |Пароли должны содержать 3 из hello следующие 4 типов знаков: строчные, верхнем регистре, цифры и специальные. Убедитесь, что пароль отвечает этим требованиям. |
| 6 |Hello пароль должен содержать 3 из hello следующие 4 типов знаков: верхнем регистре, нижнем регистре, цифры и специальные. |Пароль не содержит hello необходимых типов знаков. Убедитесь, что пароль отвечает этим требованиям. |
| 7 |Параметр не соответствует подтверждению. |Убедитесь, что пароль отвечает всем требованиям и введен правильно. |
| 8 |Пароль не может совпадать с по умолчанию hello. |пароль по умолчанию Hello — *Password1*. Потребуется toochange пароля после входа в систему для hello первый раз. |
| 9 |Hello пароль, введенный пароль устройства hello не соответствует. Повторите ввод пароля hello. |Проверьте пароль hello и введите его еще раз. |

Пароли собираются до hello устройство зарегистрировано, но применяются только после успешной регистрации. Hello рабочего процесса восстановления требуется toobe устройства hello зарегистрирован. 

> [!IMPORTANT]
> Как правило если попытка tooapply пароля завершается ошибкой, то программное обеспечение hello периодически пытается toocollect hello пароль вплоть до завершения. В редких случаях не может применяться hello пароль. В этой ситуации можно зарегистрировать устройство hello и продолжить работу, однако hello пароли не будут изменены. Вы не получите сигнала как toowhich пароль не был изменен — пароль администратора устройства hello или пароль диспетчера моментальных снимков StorSimple hello. В такой ситуации рекомендуется сменить оба пароля.
> 
> 

Можно сбросить пароли hello в hello классический портал Azure через hello в службе StorSimple Manager. Дополнительную информацию см. в разделе 

* [Пароль администратора устройства hello изменение](storsimple-change-passwords.md#change-the-device-administrator-password).
* [Изменение пароля диспетчера моментальных снимков StorSimple hello](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

## <a name="errors-during-device-registration"></a>Ошибки во время регистрации устройства
Используется в Microsoft Azure tooregister hello устройства в службе StorSimple Manager hello. Может появиться в один или несколько из следующих ситуаций во время регистрации устройства hello.

| Нет. | Сообщение об ошибке | Возможные причины | Рекомендуемое действие |
| --- | --- | --- | --- |
| 1 |: 350027 ошибка устройство hello tooregister с hello StorSimple Manager. | |Подождите несколько минут и повторите попытку hello. Если не удается устранить проблему hello, [обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md). |
| 2 |Ошибка 350013: Произошла ошибка при регистрации устройства hello. Это могло произойти из-за tooincorrect ключ регистрации службы. | |Зарегистрируйте устройство hello снова hello правильный ключ регистрации службы. Дополнительные сведения см. в разделе [ключ регистрации службы hello Get.](storsimple-manage-service.md#get-the-service-registration-key) |
| 3 |Ошибка 350063: Передано tooStorSimple проверки подлинности Manager service, но не удалось выполнить регистрацию. Повторите операцию hello через некоторое время. |Эта ошибка означает, что прошел проверку подлинности с помощью ACS, но сбой вызова, сделанного toohello hello регистрации службы. Это может быть результатом случайного сбоя в сети. |Если hello проблема повторится, [обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md). |
| 4. |Ошибка 350049: hello службы не удалось связаться во время регистрации. |При hello вызов службы toohello, будет получено исключение веб-сайта. В некоторых случаях это можно исправить, повторив попытку hello позже. |Проверьте IP-адрес и DNS-имя, а затем повторите операцию hello. При повторном возникновении проблемы hello, [обратитесь в службу поддержки Майкрософт.](storsimple-contact-microsoft-support.md) |
| 5 |Ошибка 350031: hello устройство уже зарегистрировано. | |Никаких действий не требуется. |
| 6 |Ошибка 350016: не удалось выполнить регистрацию устройства. | |Убедитесь, что задан правильный регистрационный ключ hello. |
| 7 |Invoke-HcsSetupWizard: Произошла ошибка при регистрации устройства; Это могло произойти из-за tooincorrect IP-адрес или DNS-имя. Проверьте параметры сети и повторите попытку. При повторном возникновении проблемы hello, [обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md). (Ошибка 350050) |Убедитесь, что устройства можно выполнить команду ping hello вне сети. При отсутствии подключения к сети toooutside hello регистрации может завершиться с этой ошибкой. Эта ошибка может быть комбинация одного или нескольких из следующих hello:<ul><li>неправильный IP-адрес;</li><li>неправильная подсеть;</li><li>неправильный шлюз;</li><li>неправильные параметры DNS.</li></ul> |См. шаги hello в hello [пример с пошаговыми инструкциями по устранению неполадок](#step-by-step-storsimple-troubleshooting-example). |
| 8 |Invoke-HcsSetupWizard: hello текущую операцию из-за tooan внутренней ошибки службы [0x1FBE2]. Повторите операцию hello через некоторое время. Если hello проблема повторится, обратитесь в службу поддержки Майкрософт. |Это общая ошибка, возникающая при наличии любых невидимых пользователю ошибок в службе или агенте. Hello наиболее распространенной причиной может быть сбой проверки подлинности hello ACS. Возможная причина сбоя hello — что возникли проблемы с конфигурацией сервера NTP hello и времени на устройстве hello задано неверно. |Исправьте время hello (при наличии проблемы), а затем повторите операцию регистрации hello. Если вы используете hello команду Set-HcsSystem - часовой пояс tooadjust hello часового пояса, прописных hello часового пояса (например «стандартное тихоокеанское время»).  Если проблема будет повторяться, [обратитесь в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md) для получения дальнейших инструкций. |
| 9 |Предупреждение: Не удалось активировать устройство hello. Пароли администратора устройства и диспетчера моментальных снимков StorSimple не поменялись. |При сбое регистрации hello диспетчера моментальных снимков StorSimple паролей администратора устройства hello и не изменяются. | |

## <a name="tools-for-troubleshooting-storsimple-deployments"></a>Средства для устранения неполадок в развертываниях StorSimple
StorSimple включает в себя несколько средств, которые можно использовать tootroubleshoot решения StorSimple. В частности, описаны такие возможности:

* Пакеты поддержки и журналы устройств. 
* Командлеты, специально разработанные для устранения неполадок. 

## <a name="support-packages-and-device-logs-available-for-troubleshooting"></a>Пакеты поддержки и журналы устройств, доступные для устранения неполадок
Пакет поддержки содержит все hello журналы, которые могут помочь специалистам службы поддержки Microsoft hello устранения неполадок устройства. Можно использовать Windows PowerShell для StorSimple toogenerate зашифрованный пакет поддержки, которую затем можно предоставить службу поддержки.

### <a name="tooview-hello-logs-or-hello-contents-of-hello-support-package"></a>пакет поддержки tooview hello журналы или содержимое hello hello
1. Использование Windows PowerShell для StorSimple toogenerate пакет поддержки, как описано в [Создание и управление ими пакет поддержки](storsimple-create-manage-support-package.md).
2. Загрузите hello [расшифровки сценария](https://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) локально на клиентском компьютере.
3. Этот метод следует использовать [пошаговая процедура](storsimple-create-manage-support-package.md#edit-a-support-package) tooopen и расшифровки пакета поддержки hello.
4. Hello расшифровать пакет поддержки, журналы имеют формат etw или etvx. Можно выполнить следующие шаги tooview hello эти файлы в средстве просмотра событий Windows.
   
   1. Запустите hello **eventvwr** на клиенте Windows. Эта команда запустит hello в окне просмотра событий.
   2. В hello **действия** области, нажмите кнопку **открыть сохраненный журнал** точки toohello файлов и журналов в формате etvx или etw (пакет поддержки hello). Теперь можно просмотреть файл hello. После открытия файла hello, можно правой кнопкой мыши и сохраните файл hello как текст.
      
      > [!IMPORTANT]
      > Можно также использовать hello **Get-WinEvent** tooopen командлет эти файлы в Windows PowerShell. Дополнительные сведения см. в разделе [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx) в hello справочной документации по командлетам Windows PowerShell.
      > 
      > 
5. Открыв журналы hello в окне просмотра событий найдите следующие файлы журналов, содержащие проблемы конфигурации устройства связанные toohello hello:
   
   * hcs_pfconfig/Operational Log.
   * hcs_pfconfig/Config.
6. В файлах журналов hello для поиска строк toohello связанные командлеты, вызываемые приветствия мастера установки. Список этих командлетов см. в разделе [Работа с мастером установки в первый раз](#first-time-setup-wizard-process). 
7. Если вы не могли toofigure out hello причины проблемы hello, вы можете [обратитесь в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md) для следующих действий. Используйте hello шагов в [Создание запроса на поддержку](storsimple-contact-microsoft-support.md#create-a-support-request) при службу поддержки Майкрософт за помощью.

## <a name="cmdlets-available-for-troubleshooting"></a>Командлеты, доступные для устранения неполадок
Используйте следующие ошибки подключения к toodetect командлеты Windows PowerShell hello.

* `Get-NetAdapter`: Используйте этот командлет toodetect hello работоспособности сетевых интерфейсов. 
* `Test-Connection`: Используйте этот командлет toocheck hello сетевого подключения внутри и вне сети hello.
* `Test-HcsmConnection`: Используйте этот командлет toocheck hello подключения успешно зарегистрированного устройства.

Выполняется обновление 1 на устройстве StorSimple, также доступны следующие командлеты диагностики hello.

* `Sync-HcsTime`: Используется время устройства toodisplay этот командлет и принудительной синхронизации времени с NTP-сервером hello.
* `Enable-HcsPing`и `Disable-HcsPing`: использовать эти командлеты tooallow hello узлов tooping hello сетевые интерфейсы на устройстве StorSimple. По умолчанию hello StorSimple сетевых интерфейсов не отвечают tooping запросов.
* `Trace-HcsRoute`: этот командлет выполняет трассировку маршрута. Отправляет пакеты tooeach маршрутизатор в конечное место назначения tooa способом hello за период времени и вычисляет результаты на основании приветственных пакетов, возвращенных каждым маршрутизатором. Поскольку `Trace-HcsRoute` показывает степень hello потери пакетов для каждого маршрутизатора или связи, вы можете точно определить, какие маршрутизаторы или ссылки может вызвать проблемы с сетью. 
* `Get-HcsRoutingTable`: Используйте этот командлет toodisplay hello локальной таблицы IP-маршрутизации.

## <a name="troubleshoot-with-hello-get-netadapter-cmdlet"></a>Устранение неполадок с командлета Get-NetAdapter hello
При настройке сетевых интерфейсов для развертывания устройства первое состояние оборудования hello не доступен в hello пользовательского интерфейса в службе StorSimple Manager, поскольку hello устройство еще не зарегистрирован со службой hello. Кроме того страница приветствия состояние оборудования может не отражать всегда правильно hello состояния устройства hello, особенно в том случае, если возникли проблемы, влияющие на службы синхронизации. В этих случаях можно использовать hello `Get-NetAdapter` toodetermine командлет hello работоспособности и состояние сетевых интерфейсов.

### <a name="toosee-a-list-of-all-hello-network-adapters-on-your-device"></a>список всех сетевых адаптеров hello на вашем устройстве toosee
1. Запустите Windows PowerShell для StorSimple, а затем введите `Get-NetAdapter`. 
2. Используйте выходные данные hello hello `Get-NetAdapter` командлета и hello, следуя рекомендациям toounderstand hello состояние сетевого интерфейса.
   
   * Если интерфейс hello работоспособен и включен, hello **ifIndex** состояние отображается как **копирование**.
   * Здравствуйте, если интерфейс hello находится в работоспособном состоянии, но физически не подключен (с помощью сетевого кабеля), **ifIndex** отображается как **отключено**.
   * Если интерфейс hello работоспособен, но не включено, hello **ifIndex** состояние отображается как **NotPresent**.
   * Если интерфейс hello не существует, он не отображается в этом списке. Hello пользовательского интерфейса в службе StorSimple Manager по-прежнему будет отображаться этот интерфейс в состоянии сбоя.

Дополнительные сведения о том, как toouse этот командлет go слишком[GetNetAdapter](https://technet.microsoft.com/library/jj130867.aspx) в hello справочника по командлетам Windows PowerShell. 

Hello следующих разделах показаны примеры выходных данных hello `Get-NetAdapter` командлета. 

 В этих примерах контроллер 0 был hello пассивного контроллера и была настроена следующим образом:

* DATA 0, DATA 1, DATA 2 и DATA 3 сетевые интерфейсы существовали на устройстве hello.
* DATA 4 и сетевые карты DATA 5 отсутствовали; Таким образом они не перечислены в выходных данных hello.
* Интерфейс DATA 0 включен.

Контроллер 1 был активным контроллером hello и была настроена следующим образом:

* DATA 0, DATA 1, DATA 2, DATA 3, DATA 4 и DATA 5 сетевые интерфейсы существовали на устройстве hello.
* Интерфейс DATA 0 включен.

**Образец выходных данных, контроллер 0**

Hello Приведем hello выходные данные контроллера 0 (пассивного контроллера hello). Интерфейсы DATA 1, DATA 2 и DATA 3 не подключены. DATA 4 и DATA 5 не указываются, так как они не присутствуют на устройстве hello. 

     Controller0>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter #2     17       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter        14       NotPresent
     Ethernet 2           HCS VNIC                                    13       Up
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up


**Образец выходных данных, контроллер 1**

Hello Приведем hello выходные данные контроллера 1 (hello активного контроллера). Только hello настройки сетевого интерфейса на устройстве hello DATA 0 и работе.

     Controller1>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter        18       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter #2     19       NotPresent
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up
     Ethernet 2           HCS VNIC                                    13       Up
     DATA5                Intel(R) Gigabit ET Dual Port Server...     14       NotPresent
     DATA4                Intel(R) Gigabit ET Dual Port Serv...#2     17       NotPresent


## <a name="troubleshoot-with-hello-test-connection-cmdlet"></a>Устранение неполадок с командлета Test-Connection hello
Можно использовать hello `Test-Connection` toodetermine командлет ли устройства StorSimple подключиться toohello вне сети. Если все hello сетевые параметры, включая hello DNS, настроены правильно приветствия мастера установки, можно использовать hello `Test-Connection` tooping командлет с известным адресом вне сети hello, например outlook.com. 

При отключении проверки связи, следует включить проблемы с подключением tootroubleshoot проверки связи с этим командлетом.

См. следующие примеры выходных данных из hello hello `Test-Connection` командлета. 

> [!NOTE]
> В первом примере hello hello устройство настроено с помощью неверные DNS. В втором примере hello hello DNS является правильным.
> 
> 

**Пример вывода: неверные параметры DNS**

В следующий образец hello отсутствуют выходные данные для hello IPV4 и IPV6-адреса, который указывает, что приветствия DNS не разрешается. Это означает, что нет подключения к toohello вне сети и правильное DNS должен toobe указано. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com

**Пример вывода: верные параметры DNS**

В следующий образец hello hello DNS возвращает hello IPV4-адрес, указывающее, что служба DNS настроена правильно приветствия. Это подтверждает, что имеется подключение toohello вне сети. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194

## <a name="troubleshoot-with-hello-test-hcsmconnection-cmdlet"></a>Устранение неполадок с hello командлета Test-HcsmConnection
Используйте hello `Test-HcsmConnection` командлета для устройства, которое уже подключен tooand, зарегистрированные в службе StorSimple Manager. Этот командлет позволяет проверить hello подключение между зарегистрированным устройством и hello соответствующий службе StorSimple Manager. Эту команду можно выполнить в Windows PowerShell для StorSimple. 

### <a name="toorun-hello-test-hcsmconnection-cmdlet"></a>командлет Test-HcsmConnection hello toorun
1. Убедитесь, что зарегистрированные устройства hello.
2. Проверьте состояние устройства hello. Если устройство hello отключена в режиме обслуживания или автономном режиме, может появиться hello следующие ошибки: 
   
   * ErrorCode.CiSDeviceDecommissioned — это означает, что деактивации устройства hello.
   * ErrorCode.DeviceNotReady — это означает, что это устройство hello находится в режиме обслуживания.
   * ErrorCode.DeviceNotReady — это означает, что это устройство hello не находится в оперативном режиме.
3. Убедитесь, что hello в службе StorSimple Manager запущена (использовать hello [Get-ClusterResource](https://technet.microsoft.com/library/ee461004.aspx) командлет). Если hello служба не запущена, возможны следующие ошибки hello:
   
   * ErrorCode.CiSApplianceAgentNotOnline.
   * ErrorCode.CisPowershellScriptHcsError: при выполнении командлета Get-ClusterResource возникло исключение.
4. Проверьте маркер службы контроля доступа (ACS) hello. Если он вызывает исключение веб-сайта, возможно результат hello проблема шлюза, отсутствует проверка подлинности прокси-сервера, DNS или сбой проверки подлинности. Возможны следующие ошибки hello:
   
   * ErrorCode.CiSApplianceGateway — указывает на исключение HttpStatusCode.BadGateway: hello служба разрешения имен не может разрешить имя узла hello. 
   * ErrorCode.CiSApplianceProxy — указывает на исключение HttpStatusCode.ProxyAuthenticationRequired (код состояния HTTP 407): hello клиента не удалось проверить подлинность hello прокси-сервере. 
   * ErrorCode.CiSApplianceDNSError — указывает на исключение WebExceptionStatus.NameResolutionFailure: hello служба разрешения имен не может разрешить имя узла hello.
   * ErrorCode.CiSApplianceACSError — это означает, что hello служба возвратила ошибку проверки подлинности, но отсутствует связь.
     
     Если веб-исключение не создается, проверьте, не появилась ли ошибка ErrorCode.CiSApplianceFailure. Это указывает на сбой устройства, hello.
5. Проверьте подключение к облачной службе hello. Если служба hello вызывает исключение веб-сайта, может появиться hello следующие ошибки:
   
   * ErrorCode.CiSApplianceGateway — указывает на исключение HttpStatusCode.BadGateway: промежуточный прокси-сервер получил неверный запрос из другого прокси-сервера или с исходного сервера hello.
   * ErrorCode.CiSApplianceProxy — указывает на исключение HttpStatusCode.ProxyAuthenticationRequired (код состояния HTTP 407): hello клиента не удалось проверить подлинность hello прокси-сервере. 
   * ErrorCode.CiSApplianceDNSError — указывает на исключение WebExceptionStatus.NameResolutionFailure: hello служба разрешения имен не может разрешить имя узла hello.
   * ErrorCode.CiSApplianceACSError — это означает, что hello служба возвратила ошибку проверки подлинности, но отсутствует связь.
     
     Если веб-исключение не создается, проверьте, не появилась ли ошибка ErrorCode.CiSApplianceSaasServiceError. Это указывает на проблему с hello в службе StorSimple Manager.
6. Проверьте подключение к служебной шине Azure. ErrorCode.CiSApplianceServiceBusError означает, что это устройство hello не удается подключиться к toohello Service Bus.

Здравствуйте, файлы журналов CiSCommandletLog0Curr.errlog и CiSAgentsvc0Curr.errlog будут содержать дополнительные сведения, например сведения об исключении. 

Дополнительные сведения о как toouse hello командлет go слишком[Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx) в Windows PowerShell hello справочной документации.

> [!IMPORTANT]
> Можно запустить этот командлет для hello активного и пассивного контроллера hello. 
> 
> 

См. следующие примеры выходных данных из hello hello `Test-HcsmConnection` командлета. 

**Образец вывода – успешно зарегистрированное устройство под управлением выпуска StorSimple (июль 2014 г.)**

Первый пример Hello является устройство, которое будет успешно зарегистрировано в службе StorSimple Manager hello и имеет нет проблем с подключением. 

     Controller1>Test-HcsmConnection -verbose
     Checking device state  ... Success.
     Device registered successfully
     Checking device authentication.  ... This operation will take few minutes toocomplete....
     Checking device authentication.  ... Success.
     Checking connectivity from device tooStorSimple Manager service.  ... This operation will take few minutes toocomplete....
     Checking connectivity from device tooStorSimple Manager service.  ... Success.
     Checking connectivity from StorSimple Manager service tooStorSimple device. .... Success.
     Controller1>

**Образец вывода — успешно зарегистрированное устройство под управлением обновления 1 для StorSimple**

При выполнении на устройстве StorSimple с обновлением 1 не потребуется toorun его с параметром verbose hello.

      Controller1>Test-HcsmConnection

      Checking device registration state  ... Success
      Device registered successfully

      Checking primary NTP server [time.windows.com] ... Success

      Checking web proxy  ... NOT SET

      Checking primary IPv4 DNS server [10.222.118.154] ... Success
      Checking primary IPv6 DNS server  ... NOT SET
      Checking secondary IPv4 DNS server [10.222.120.24] ... Success
      Checking secondary IPv6 DNS server  ... NOT SET

      Checking device online  ... Success

      Checking device authentication  ... This will take a few minutes.
      Checking device authentication  ... Success

      Checking connectivity from device tooservice  ... This will take a few minutes.

      Checking connectivity from device tooservice  ... Success

      Checking connectivity from service toodevice  ... Success

      Checking connectivity tooMicrosoft Update servers  ... Success
      Controller1>

**Образец вывода – автономное устройство под управлением выпуска StorSimple (июль 2014 г.)**

В этом примере — с устройства, которое находится в состоянии **Offline** в hello классический портал Azure.

     Checking device state: Success 
     Device is registered successfully 
     Checking connectivity from device tooSaaS.. Failure

Hello устройству не удалось подключиться с помощью hello текущей конфигурации веб-прокси. Это может быть проблема с конфигурацией прокси-сервера веб-hello или ли неполадки сетевого подключения. В этом случае следует убедиться в правильности параметров веб-прокси и в том, что веб-прокси-серверы подключены к сети и доступны. 

## <a name="troubleshoot-with-hello-sync-hcstime-cmdlet"></a>Устранение неполадок с hello синхронизации HcsTime командлета
Используйте этот командлет toodisplay hello устройства времени. Если время hello устройства имеют смещение с NTP-сервером hello, затем можно использовать этот командлет tooforce-синхронизировать hello время с NTP-сервером. Если смещение hello между hello устройства и NTP-сервера превышает 5 минут, появится предупреждение. Если смещение hello превышает 15 минут, затем устройства hello перейдет в автономный режим. По-прежнему можно использовать этот командлет tooforce синхронизация времени. Если смещение hello превышает 15 часов, затем будет время hello может tooforce синхронизации и отображается сообщение об ошибке.

**Образец вывода – время принудительной синхронизации с помощью командлета Sync-HcsTime**

     Controller0>Sync-HcsTime
     hello current device time is 4/24/2015 4:05:40 PM UTC.

     Time difference between NTP server and appliance is 00.0824069 seconds. Do you want tooresync time with NTP server?
     [Y] Yes [N] No (Default is "Y"): Y
     Controller0>

## <a name="troubleshoot-with-hello-enable-hcsping-and-disable-hcsping-cmdlets"></a>Устранение неполадок с командлетами HcsPing Включение и отключение HcsPing hello
Используйте эти командлеты tooensure, что hello сетевые интерфейсы на вашем устройстве отвечает на запросы проверки связи tooICMP. По умолчанию hello StorSimple сетевых интерфейсов не отвечают tooping запросов. С помощью этого командлета является наиболее простым способом tooknow hello, если ваше устройство находится в оперативном режиме и доступен.  

**Пример выходных данных – Enable-HcsPing и Disable-HcsPing**

     Controller0>
     Controller0>Enable-HcsPing
     Successfully enabled ping.
     Controller0>
     Controller0>
     Controller0>Disable-HcsPing
     Successfully disabled ping.
     Controller0>

## <a name="troubleshoot-with-hello-trace-hcsroute-cmdlet"></a>Устранение неполадок с hello трассировки HcsRoute командлета
Этот командлет выполняет трассировку маршрута. Отправляет пакеты tooeach маршрутизатор в конечное место назначения tooa способом hello за период времени и вычисляет результаты на основании приветственных пакетов, возвращенных каждым маршрутизатором. Поскольку командлет hello показывает hello степень потери пакетов на любом маршрутизаторе или ссылку, вы можете точно определить, какие маршрутизаторы или ссылки может вызвать проблемы с сетью.

**Пример выходных данных, показывающих, как tootrace hello маршрут пакета с HcsRoute трассировки**

     Controller0>Trace-HcsRoute -Target 10.126.174.25

     Tracing route toocontoso.com [10.126.174.25]
     over a maximum of 30 hops:
       0  HCSNode0 [10.126.173.90]
       1  contoso.com [10.126.174.25]

     Computing statistics for 25 seconds...
                 Source tooHere   This Node/Link
     Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
       0                                           HCSNode0 [10.126.173.90]
                                     0/ 100 =  0%   |
       1    0ms     0/ 100 =  0%     0/ 100 =  0%  contoso.com
      [10.126.174.25]

     Trace complete.

## <a name="troubleshoot-with-hello-get-hcsroutingtable-cmdlet"></a>Устранение неполадок с командлета Get-HcsRoutingTable hello
Используйте этот командлет tooview hello маршрут для устройства StorSimple. Таблица маршрутизации — это набор правил, которые выполняют определение направления пакетов данных, передаваемых по сети, построенной по межсетевому протоколу (IP). 

Hello таблицу маршрутизации показана интерфейсы hello и hello шлюза, что маршруты hello toohello данных задается сетей. Она также предоставляет hello маршрутизации метрики, которые являются hello принятие решений для tooreach путь, пройденный hello конкретного места назначения. Hello нижней hello метрики, hello выше hello предпочтения маршрутизации. 

Например, если у вас есть 2 сетевые интерфейсы DATA 2 и 3 данных, подключенных toohello Интернет. Если hello маршрутизации метрики для DATA 2 и DATA 3 являются 15 и 261 соответственно, затем 2 данных с меньшей метрикой маршрутизации hello — hello удобного интерфейса используемых hello tooreach Интернет.

При выполнении на устройстве StorSimple с обновлением 1 вашего сетевого интерфейса DATA 0 имеет наивысший приоритет hello для hello облачного трафика. Это означает, что даже если существуют другие интерфейсы облако, будет перенаправлен hello облачного трафика через DATA 0. 

При запуске hello `Get-HcsRoutingTable` командлет без указания любые параметры (как hello следующие примере), hello командлет выдаст таблиц маршрутов IPv4 и IPv6. Кроме того, можно указать `Get-HcsRoutingTable -IPv4` или `Get-HcsRoutingTable -IPv6` tooget соответствующей таблице маршрутизации.

      Controller0>
      Controller0>Get-HcsRoutingTable
      ===========================================================================
      Interface List
       14...00 50 cc 79 63 40 ......Intel(R) 82574L Gigabit Network Connection
       12...02 9a 0a 5b 98 1f ......Microsoft Failover Cluster Virtual Adapter
       13...28 18 78 bc 4b 85 ......HCS VNIC
        1...........................Software Loopback Interface 1
       21...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
       22...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
      ===========================================================================

      IPv4 Route Table
      ===========================================================================
      Active Routes:
      Network Destination        Netmask          Gateway       Interface  Metric
                0.0.0.0          0.0.0.0  192.168.111.100  192.168.111.101     15
              127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
              127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
        127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
            169.254.0.0      255.255.0.0         On-link     169.254.1.235    261
          169.254.1.235  255.255.255.255         On-link     169.254.1.235    261
        169.254.255.255  255.255.255.255         On-link     169.254.1.235    261
          192.168.111.0    255.255.255.0         On-link   192.168.111.101    266
        192.168.111.101  255.255.255.255         On-link   192.168.111.101    266
        192.168.111.255  255.255.255.255         On-link   192.168.111.101    266
              224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
              224.0.0.0        240.0.0.0         On-link     169.254.1.235    261
              224.0.0.0        240.0.0.0         On-link   192.168.111.101    266
        255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        255.255.255.255  255.255.255.255         On-link     169.254.1.235    261
        255.255.255.255  255.255.255.255         On-link   192.168.111.101    266
      ===========================================================================
      Persistent Routes:
        Network Address          Netmask  Gateway Address  Metric
                0.0.0.0          0.0.0.0  192.168.111.100       5
      ===========================================================================

      IPv6 Route Table
      ===========================================================================
      Active Routes:
       If Metric Network Destination      Gateway
        1    306 ::1/128                  On-link
       13    276 fd99:4c5b:5525:d80b::/64 On-link
       13    276 fd99:4c5b:5525:d80b::1/128
                                          On-link
       13    276 fd99:4c5b:5525:d80b::3/128
                                          On-link
       13    276 fe80::/64                On-link
       12    261 fe80::/64                On-link
       13    276 fe80::17a:4eba:7c80:727f/128
                                          On-link
       12    261 fe80::fc97:1a53:e81a:3454/128
                                          On-link
        1    306 ff00::/8                 On-link
       13    276 ff00::/8                 On-link
       12    261 ff00::/8                 On-link
       14    266 ff00::/8                 On-link
      ===========================================================================
      Persistent Routes:
        None

      Controller0>

## <a name="step-by-step-storsimple-troubleshooting-example"></a>Пример с пошаговыми инструкциями по устранению неполадок в устройстве StorSimple
Hello пример пошаговые Устранение неполадок развертывания StorSimple. В примере сценария hello завершается сообщение об ошибке, параметры сети hello или DNS-имя hello неправильный регистрацию устройств.

— Hello возвращаемых сообщений об ошибках:

     Invoke-HcsSetupWizard: An error has occurred while registering hello device. This could be due tooincorrect IP address or DNS name. Please check your network settings and try again. If hello problems persist, contact Microsoft Support.
     +CategoryInfo: Not specified
     +FullyQualifiedErrorID: CiSClientCommunicationErros, Microsoft.HCS.Management.PowerShell.Cmdlets.InvokeHcsSetupWizardCommand

Hello ошибка может быть вызвана любой из следующих hello:

* Неверная установка оборудования.
* Неисправные сетевые интерфейсы.
* Неправильный IP-адрес, маска подсети, шлюз, основной DNS-сервер или веб-прокси.
* Неверный ключ регистрации.
* Неверные настройки брандмауэра.

### <a name="toolocate-and-fix-hello-device-registration-problem"></a>toolocate и исправление hello проблемы с регистрацией устройства
1. Проверьте конфигурацию устройства: hello active контроллере, выполните `Invoke-HcsSetupWizard`.
   
   > [!NOTE]
   > необходимо запустить мастер настройки Hello на активном контроллере hello. tooverify, подключенных toohello активный контроллер, рассмотрим hello баннер в последовательной консоли hello. объявления Hello указывает, являетесь ли вы подключенных toocontroller 0 или 1, и является ли контроллер hello активный или пассивный. Дополнительные сведения см. слишком[определение активного контроллера на вашем устройстве](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
   > 
   > 
2. Убедитесь, что это устройство hello подключен правильно: Проверьте hello сетевых кабелей на задней стороне устройства hello. кабели Hello — модель toohello конкретного устройства. Дополнительные сведения см. слишком[установки устройства StorSimple 8100](storsimple-8100-hardware-installation.md) или [установки устройства StorSimple 8600](storsimple-8600-hardware-installation.md).
   
   > [!NOTE]
   > При использовании сетевых портов 10 GbE, необходимо будет toouse hello, предоставленные адаптеры QSFP SFP и кабели SFP. Дополнительные сведения см. в разделе hello [список кабелей, коммутаторов и приемопередатчиков, рекомендуемых для портов hello 10 GbE](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
   > 
   > 
3. Проверьте работоспособность hello hello сетевой интерфейс:
   
   * Используйте работоспособности hello toodetect командлет Get-NetAdapter hello hello сетевых интерфейсов для DATA 0. 
   * Здравствуйте, если hello ссылка не работает, **ifindex** состояние будет указывать этот интерфейс hello не работает. Затем необходимо будет toocheck hello сетевое подключение устройства toohello порт hello и toohello коммутатора. Необходимо также toorule отсутствии поврежденных кабелей. 
   * Если есть подозрение, что hello DATA 0 порт на активном контроллере hello произошел сбой, вы можете проверить, подключившись toohello порт DATA 0 на контроллере 1. tooconfirm это, отключите hello сетевой кабель hello задняя сторона устройства hello от контроллера 0, подключение toocontroller кабеля hello 1, затем снова запустите командлет Get-NetAdapter hello. 
     Если hello DATA 0, происходит сбой порт на контроллере, [обратитесь в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md) для следующих действий. Может потребоваться tooreplace hello контроллера в системе.
4. Проверка коммутатора toohello hello подключения:
   
   * Убедитесь, что сетевые интерфейсы DATA 0 на контроллере 0 и контроллера 1 в основном корпусе находятся на hello одной подсети. 
   * Проверьте hello концентратор или маршрутизатор. Как правило, необходимо подключить обоих контроллеров toohello одному концентратору или маршрутизатору. 
   * Убедитесь, что коммутаторы hello, используются для соединения hello DATA 0 для обоих контроллеров в hello одной виртуальной ЛС.
5. Исключите ошибки пользователей:
   
   * Снова запустите мастер установки hello (запустить **Invoke-HcsSetupWizard**) и введите hello снова значения toomake том, что отсутствуют ошибки. 
   * Проверка регистрации hello ключ, используемый. Здравствуйте, же регистрационный ключ можно использовать tooconnect tooa несколько устройств в службе StorSimple Manager. Используйте процедуру hello в [ключ регистрации службы hello Get](storsimple-manage-service.md#get-the-service-registration-key) tooensure, в которых используется hello правильный регистрационный ключ.
     
     > [!IMPORTANT]
     > Если запущено несколько служб, необходимо будет tooensure этого ключа регистрации hello для устройства используется tooregister hello hello соответствующую службу. Если вы зарегистрировали устройство в службе StorSimple Manager неправильный hello, необходимо будет слишком[обратитесь в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md) для следующих действий. Возможно, tooperform заводские настройки устройства hello (что может привести к потере данных) toothen подключения службы toohello предназначен.
     > 
     > 
6. Используйте tooverify командлета Test-Connection hello наличие подключения к toohello за пределами сети. Дополнительные сведения см. слишком[Устранение неполадок с помощью командлета Test-Connection hello](#troubleshoot-with-the-test-connection-cmdlet).
7. Проверьте на помехи со стороны брандмауэра. Если вы убедились, что hello виртуальных IP-адресов, подсети, шлюза и DNS заданы правильно и вы по-прежнему видите проблемы с подключением, а затем это возможно, ваш брандмауэр блокирует обмен данными между устройством и hello вне сети. Необходимо tooensure, что на устройстве StorSimple для исходящей связи доступны порты 80 и 443. Дополнительные сведения см. в разделе [Требования к сети для устройства StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
8. Просмотрите журналы hello. Go слишком[поддерживает пакеты и журналы устройств доступны для устранения неполадок](#support-packages-and-device-logs-available-for-troubleshooting).
9. Если hello описанные выше шаги не устранили проблему hello [обратитесь в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md) для получения помощи.

## <a name="next-steps"></a>Дальнейшие действия
[Узнайте, как tootroubleshoot рабочего устройства](storsimple-troubleshoot-operational-device.md).

<!--Link references-->

[1]: https://technet.microsoft.com/library/dd379547(v=ws.10).aspx
[2]: https://technet.microsoft.com/library/dd392266(v=ws.10).aspx 
