---
title: "aaaPowerShell для управления устройствами StorSimple | Документы Microsoft"
description: "Узнайте, как toouse Windows PowerShell для StorSimple toomanage устройства StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0ff3bb0d-897a-4676-bdcb-402c2628dac5
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: alkohli@microsoft.com
ms.openlocfilehash: 1adcbb8bb89e3e3b4f328aac198690476c2a78cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-for-storsimple-tooadminister-your-device"></a>Использование Windows PowerShell для StorSimple tooadminister устройства
## <a name="overview"></a>Обзор
Windows PowerShell для StorSimple предоставляет интерфейс командной строки, которые можно использовать toomanage устройства Microsoft Azure StorSimple. Как hello названия, это интерфейс командной строки на основе Windows PowerShell, построенный в ограниченном пространстве выполнения. С точки зрения hello пользователя hello hello командной строки ограниченное пространство выполнения представляет собой ограниченную версию Windows PowerShell. Наряду с поддержкой некоторых основных возможностей Windows PowerShell hello, этот интерфейс имеет дополнительные специализированные командлеты, специально предназначенные для управления устройством Microsoft Azure StorSimple. 

В этой статье описывает hello Windows PowerShell для StorSimple функций, включая способ подключения интерфейс toothis и содержит ссылки toostep за шагом процедуры или рабочих процессов, которые можно выполнять с помощью этого интерфейса. рабочие процессы Hello включают как tooregister устройства, Настройка hello сетевого интерфейса на устройстве, устанавливать обновления, которые требуют hello toobe устройство в режим обслуживания, изменения состояния устройства hello, и устраните все проблемы, которые могут возникнуть.

Прочитав эту статью, вы сможете выполнять следующие действия.

* Подключите устройство StorSimple tooyour, с помощью Windows PowerShell для StorSimple.
* Администрировать устройство StorSimple с помощью Windows PowerShell для StorSimple.
* Получить справку по Windows PowerShell для StorSimple.

> [!NOTE]
> * Windows PowerShell для StorSimple командлетов разрешить toomanage устройства StorSimple через последовательную консоль или удаленно с помощью удаленного взаимодействия Windows PowerShell. Дополнительные сведения о каждом hello отдельных командлетов, которые можно использовать в этом интерфейсе см. слишком[справочнике по командлетам Windows PowerShell для StorSimple](https://technet.microsoft.com/library/dn688168.aspx).
> * командлеты PowerShell Azure StorSimple Hello: изменить набор командлетов, которые позволяют tooautomate уровня службы StorSimple и задачи миграции из командной строки hello. Дополнительные сведения о hello командлетов Azure PowerShell для StorSimple go toohello [Справочник по командлетам Azure StorSimple](/powershell/module/azure/?view=azuresmps-3.7.0).
> 
> 

Вы можете использовать hello Windows PowerShell для StorSimple, с помощью одного из следующих методов hello:

* [Подключение tooStorSimple последовательной консоли устройства](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [Удаленное подключение с помощью Windows PowerShell tooStorSimple](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-toowindows-powershell-for-storsimple-via-hello-device-serial-console"></a>Подключение tooWindows PowerShell для StorSimple через последовательную консоль устройства hello
Вы можете [загрузить PuTTY](http://www.putty.org/) или аналогичные tooWindows tooconnect программное обеспечение эмуляции терминала PowerShell для StorSimple. Требуется tooconfigure PuTTY специально tooaccess hello устройство Microsoft Azure StorSimple. Hello следующих разделах содержится подробная информация о том, как tooconfigure PuTTy и подключить устройство toohello. Также описаны различных параметров меню последовательной консоли hello.

### <a name="putty-settings"></a>Параметры PuTTY
Убедитесь, что используется hello следующую toohello tooconnect параметры PuTTY в интерфейсе Windows PowerShell из последовательной консоли hello.

#### <a name="tooconfigure-putty"></a>tooconfigure PuTTY
1. В hello PuTTY **перенастройки** диалогового окна hello **категории** выберите **клавиатуры**.
2. Убедитесь, что выбраны hello, что следующие параметры (это параметры по умолчанию hello при запуске нового сеанса). 
   
   | Клавиша | Выберите пункт |
   | --- | --- |
   | BACKSPACE |Control-? (127) |
   | Клавиши HOME и END |Стандартная |
   | Функциональные клавиши и дополнительная клавиатура |ESC[n~ |
   | Начальное состояние клавиш управления курсором |В обычном режиме |
   | Начальное состояние числовой клавиатуры |В обычном режиме |
   | Включение компонентов на дополнительной клавиатуре |Control-Alt отличается от AltGr |
   
    ![Поддерживаемые параметры PuTTY](./media/storsimple-windows-powershell-administration/IC740877.png)
3. Нажмите кнопку **Применить**.
4. В hello **категории** выберите **перевода**.
5. В hello **удаленного кодировка** выберите **UTF-8**.
6. В разделе **Handling of line drawing characters** (Обработка знаков рисования линии) выберите пункт **Use Unicode line drawing code points** (Использовать кодовые точки графических объектов Юникод). Hello ниже показан Выбор параметров PuTTY правильный hello.
   
    ![Параметры UTF PuTTY](./media/storsimple-windows-powershell-administration/IC740878.png)
7. Нажмите кнопку **Применить**.

Теперь можно использовать PuTTY tooconnect toohello последовательной консоли устройства, выполнив следующие шаги hello.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-hello-serial-console"></a>О hello последовательной консоли
При доступе к hello в интерфейсе Windows PowerShell устройства StorSimple через последовательную консоль hello, текст заголовка вместе с параметрами меню. 

текст заголовка Hello содержит основные сведения об устройстве StorSimple например hello модели, имя, версию установленного программного обеспечения и состояния hello контроллера, к которому выполняется подключение. Следующие изображения Hello приведен пример текста заголовка.

![Заглавное сообщение в последовательной консоли](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> Можно использовать tooidentify сообщение hello баннера, контроллер hello ли подключение toois активный или пассивный.
> 
> 

следующие показано изображение Hello hello различные параметры пространства выполнения, доступные в меню последовательной консоли hello.

![Регистрация устройства 2](./media/storsimple-windows-powershell-administration/IC740906.png)

Можно выбрать из hello следующие параметры:

1. **Войти с полным доступом** этот параметр позволяет tooconnect (с подходящими учетными данными hello) toohello **SSAdminConsole** выполнения на локальном контроллере hello. (hello локальный контроллер является hello, выполняется доступ через последовательную консоль устройства StorSimple hello.) Этот параметр можно также использовать tooallow tooaccess поддержки Майкрософт неограниченное пространство выполнения (сеанс поддержки) tootroubleshoot возможных проблем в устройстве. После использовании toolog вариант 1, можно предоставить специалисту службы поддержки Microsoft hello tooaccess неограниченное пространство выполнения с помощью специального командлета. Дополнительные сведения приведены слишком[начало сеанса поддержки](storsimple-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple).
2. **Войдите в контроллер toopeer с полным доступом** этот параметр является Здравствуйте таким же, как вариант 1, за исключением того, могут подключаться (с подходящими учетными данными hello) toohello **SSAdminConsole** пространству выполнения однорангового контроллера hello. Так как устройство StorSimple hello высокодоступное устройство с двумя контроллерами в конфигурации активны пассивный, одноранговый контроллер указывает toohello другой контроллер устройства hello, к которому осуществляется доступ через последовательную консоль hello).
   Аналогичные toooption 1, этот параметр также может быть tooaccess неограниченное пространство выполнения технической поддержки Майкрософт используется tooallow на одноранговом контроллере.
3. **Подключиться с ограниченным доступом** данный параметр является tooaccess используется интерфейс Windows PowerShell в режиме limited. Учетные данные для доступа не запрашиваются. Этот параметр обеспечивает подключение tooa более ограниченные пространства выполнения по сравнению toooptions 1 и 2.  Некоторые задачи hello, доступных через параметр 1, **нельзя* выполняться в этом пространстве выполнения являются:
   
   * Сброс toohello заводских настроек
   * Изменение пароля hello
   * включение или отключение доступа для службы поддержки;
   * установка обновлений;
   * установка исправлений. 

    > [!NOTE]
    > Это параметр hello предпочтительно, если вы забыли пароль администратора устройства hello и нельзя подключиться с помощью параметров 1 и 2.

4. **Изменить язык** этот параметр позволяет язык отображения hello toochange hello в интерфейсе Windows PowerShell. поддерживаемые Hello языки: английский, японский, русский, французский, южно-корейский, испанский, итальянский, немецкий, китайский и португальский (Бразилия).

## <a name="connect-remotely-toostorsimple-using-windows-powershell-for-storsimple"></a>Удаленное подключение с помощью Windows PowerShell для StorSimple tooStorSimple
Можно использовать устройство StorSimple tooyour tooconnect удаленного взаимодействия Windows PowerShell. При таком способе подключения меню не отображается. (Увидеть меню только в том случае, если вы используете hello последовательной консоли на устройстве tooconnect hello. Удаленное подключение осуществляется непосредственно toohello, равное «вариант 1 — полный доступ» на последовательную консоль hello.) С помощью удаленного взаимодействия Windows PowerShell подключитесь tooa определенной среде выполнения. Можно также указать язык отображения приветствия. 

Hello язык интерфейса не зависит от языка hello, заданного с помощью hello **изменить язык** в меню последовательной консоли hello. Remote PowerShell автоматически получат hello языкового стандарта hello устройства вы подключаетесь с, если он не задан.

> [!NOTE]
> При работе с Microsoft Azure виртуальными узлами и виртуальными устройствами StorSimple можно использовать Windows PowerShell удаленное взаимодействие и hello виртуального узла tooconnect toohello виртуального устройства. Если настраивается общая папка на узле hello на какие toosave сведения из сеанса Windows PowerShell hello должны учитывать, что приветствия этого участника все включает в себя только прошедшие проверку пользователи. Таким образом Если настройки hello tooallow доступ к ним всем пользователям, а подключение выполняется без указания учетных данных, будет использоваться без проверки подлинности анонимных участника hello и появится сообщение об ошибке. эту проблему, на hello совместного использования узла необходимо включить гостевую учетную запись hello и предоставьте hello гостевой учетной записи полный доступ toohello общий ресурс или вы toofix необходимо указать действительные учетные данные с hello командлета Windows PowerShell.
> 
> 

Можно использовать HTTP или HTTPS tooconnect через удаленное взаимодействие Windows PowerShell. Используйте инструкции hello в hello следующие учебники:

* [Подключение по протоколу HTTP](storsimple-remote-connect.md#connect-through-http)
* [Подключение по протоколу HTTPS](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a>Вопросы безопасности подключения
При выборе как tooconnect tooWindows PowerShell для StorSimple, рассмотрим следующие hello:

* Непосредственное подключение toohello последовательной консоли устройства защищено, но подключения последовательной консоли toohello через сетевые коммутаторы не. Будьте осторожны hello угрозу безопасности при подключении серийный toodevice через сетевые коммутаторы.
* Подключение через сеанс HTTP является более безопасным, чем подключение через последовательную консоль hello по сети. Несмотря на то, что это не самый безопасный метод hello, он допустим для надежных сетей.
* Подключение через сеанс HTTPS — hello наиболее безопасный и рекомендуемый параметр hello.

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a>Администрировать устройство StorSimple с помощью Windows PowerShell для StorSimple.
Hello Следующая таблица показывает сводку всех hello общие задачи управления и сложных рабочих процессов, которые могут быть выполнены в hello в интерфейсе Windows PowerShell устройства StorSimple. Дополнительные сведения о каждом рабочем процессе щелкните hello соответствующую запись в таблице hello.

#### <a name="windows-powershell-for-storsimple-workflows"></a>Рабочие процессы Windows PowerShell для StorSimple
| Если требуется toodo... | Используйте эту процедуру. |
| --- | --- |
| Зарегистрировать устройство |[Настройка и регистрация устройства hello, с помощью Windows PowerShell для StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| Настроить веб-прокси</br>Посмотреть параметры веб-прокси |[Настройка веб-прокси для устройства StorSimple](storsimple-configure-web-proxy.md) |
| Изменить параметры сетевого интерфейса DATA 0 на устройстве StorSimple |[Изменение сетевого интерфейса DATA 0 на устройстве StorSimple](storsimple-modify-data-0.md) |
| Остановить контроллер  </br> Перезагрузка или завершение работы контроллера </br> Завершение работы устройства</br>Сброс параметров по умолчанию toofactory устройства hello |[Управление контроллерами устройства](storsimple-manage-device-controller.md) |
| Установка обновлений и исправлений в режиме обслуживания |[Обновление устройства](storsimple-update-device.md) |
| Перейти в режим обслуживания </br>Выйти из режима обслуживания |[Режимы устройств StorSimple](storsimple-device-modes.md) |
| Создать пакет поддержки</br>Расшифровать и изменить пакет поддержки |[Создание пакетов поддержки и управление ими](storsimple-create-manage-support-package.md) |
| Запуск сеанса поддержки</br> |[Запуск сеанса поддержки в Windows PowerShell для StorSimple](storsimple-create-manage-support-package.md#manually-create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a>Получить справку по Windows PowerShell для StorSimple
В Windows PowerShell для StorSimple доступна справка по командлетам. Оперативные, текущие версии справки также доступна, которую можно использовать tooupdate hello справки в системе.

Получение справки в своем интерфейсе аналогичные toothat в Windows PowerShell, и большая часть командлетов, связанных со справкой hello будет работать. Справку по Windows PowerShell через Интернет можно найти в библиотеке TechNet hello: [использование скриптов Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=108518).

Hello Вот краткое описание типов hello справки для этого интерфейса Windows PowerShell, включая как tooupdate hello справки.

#### <a name="tooget-help-for-a-cmdlet"></a>tooget справки по командлету
* tooget справку для любого командлета или функции hello используйте следующую команду:`Get-Help <cmdlet-name>`
* tooget справки в Интернете для любого командлета используйте hello Предыдущий командлет с hello `-Online` параметр:`Get-Help <cmdlet-name> -Online`
* Для получения полной справки можно использовать hello `–Full` параметра и примеры использования hello `–Examples` параметра.

#### <a name="tooupdate-help"></a>tooupdate справки
Можно легко обновить hello справки в интерфейсе Windows PowerShell hello. Выполните следующие шаги tooupdate hello справки в системе hello.

#### <a name="tooupdate-cmdlet-help"></a>Справка по командлету tooupdate
1. Запустите Windows PowerShell с hello **Запуск от имени администратора** параметр.
2. Hello командной строки введите следующую команду:`Update-Help`
3. Hello обновления будут установлены файлы справки.
4. После установки hello файлов справки, введите: `Get-Help Get-Command`. Появится список командлетов, для которых доступна справка.

> [!NOTE]
> список всех доступных командлетов hello пространство выполнения, tooget войти toohello соответствующий параметр меню и запустить hello `Get-Command` командлета.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Если возникают проблемы с устройством StorSimple при выполнении одного из hello выше рабочих процессов, см. слишком[средства для устранения неполадок развертываний StorSimple](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments).

