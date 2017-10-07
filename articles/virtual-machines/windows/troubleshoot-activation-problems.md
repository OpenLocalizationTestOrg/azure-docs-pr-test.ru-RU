---
title: "aaaTroubleshoot проблемы активации виртуальной машины Windows в Azure | Документы Microsoft"
description: "Предоставляет hello устранения шаги по устранению неполадок активации виртуальной машины Windows в Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a>Устранение неполадок при активации виртуальных машин Windows в Azure

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Если возникли проблемы при активации Azure Windows виртуальной машины (VM), созданной из образа, можно использовать hello сведения, представленные в этом выпуске hello tootroubleshoot документа. 

## <a name="symptom"></a>Симптом

При попытке tooactivate ВМ Windows Azure, появляется сообщение об ошибке сообщений напоминает следующий образец hello:

**Ошибка: hello 0xC004F074 LicensingService программного обеспечения сообщила, что не удалось активировать этот компьютер hello. Связаться со службой управления ключами (KMS) не удалось. См. в разделе hello журнал событий приложений для получения дополнительных сведений.**

## <a name="cause"></a>Причина:
Обычно проблемами активации виртуальной Машины Azure выполняться Если hello виртуальной Машины Windows не настроен с помощью hello соответствующий ключ установки клиента KMS или виртуальной Машине Windows hello имеет toohello проблемы подключения службы Azure KMS (kms.core.windows.net, порт 1668). 

## <a name="solution"></a>Решение

>[!NOTE]
>Если используется сеть сеть VPN и принудительного туннелирования, в разделе [пользовательские используйте Azure направляет tooenable активации KMS с помощью принудительного туннелирования](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx). 
>
>Если вы используете ExpressRoute и опубликован маршрут по умолчанию см. в разделе [ВМ Azure может завершиться ошибкой tooactivate по ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a>Шаг 1 Настройка hello соответствующий ключ установки клиента KMS (для Windows Server 2016 и Windows Server 2012 R2)

Для hello виртуальной Машины, которая создается на основе пользовательского образа Windows Server 2016 или Windows Server 2012 R2 необходимо настроить hello соответствующий ключ установки клиента KMS для hello виртуальной Машины.

Этот шаг не применяется tooWindows 2012 или Windows 2008 R2. Она использует функции hello автоматизации активации виртуальной машины (AVMA), которая поддерживается только Windows Server 2016 и Windows Server 2012 R2.

1. В командной строке с повышенными привилегиями выполните команду **slmgr.vbs /dlv**. Проверьте значение описания в выходных данных hello hello и определить, является ли он был создан из розничной торговли (РОЗНИЧНОГО канала) или корпоративного (VOLUME_KMSCLIENT) лицензирования:
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. Если **slmgr.vbs/dlv** показывает РОЗНИЧНОГО канала, запустите следующие команды tooset hello hello [ключ установки клиента KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) используется для hello версии Windows Server и заставить его tooretry активации: 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    Например для Windows Server 2016 центра обработки данных, нужно будет выполнить hello следующую команду:

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a>Шаг 2 Проверьте hello соединение между hello виртуальной Машины и службы Azure KMS

1. Загрузите и извлеките hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) средство tooa локальную папку в виртуальной Машине, которая не активирует hello. 

2. Go tooStart, поиск на основе Windows PowerShell, щелкните правой кнопкой мыши Windows PowerShell и затем выберите Запуск от имени администратора.

3. Убедитесь, что этой hello ВМ настроен правильный сервер Azure KMS toouse hello. toodo это, выполните следующую команду:
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    Команда Hello должен возвращать: tookms.core.windows.net:1688 успешно установлено на имя компьютера службы управления ключами.

4. Проверьте с помощью Psping, наличие сервера службы KMS toohello подключения. Переключение toohello папку, которую было извлечено hello Pstools.zip загрузки, а затем запустите hello следующее:
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  В секунду за последней строку hello hello выходные данные, убедитесь, что вы видите: отправлено = 4, получено = 4, потеряно = 0 (0% потерь).

  Если потерянные больше 0 (ноль), hello виртуальной Машины отсутствует сервер KMS toohello подключения. В этом случае если hello виртуальная машина находится в виртуальной сети и имеет пользовательского DNS-сервера указан, убедитесь, что DNS-сервер является может tooresolve kms.core.windows.net. Или измените hello DNS server tooone, разрешить kms.core.windows.net.

  Обратите внимание, что при удалении из виртуальной сети всех DNS-серверов виртуальные машины используют внутреннюю службу DNS Azure. Эта служба может разрешать kms.core.windows.net.
  
Также убедитесь, что гостевой брандмауэром, hello не был настроен таким образом, чтобы заблокирует попытки активации.

5. После проверки успешного подключения tookms.core.windows.net, выполните следующую команду в этой строке с повышенными привилегиями Windows PowerShell hello. Эта команда пытается выполнить активацию несколько раз.

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

Успешной активации возвращает сведения, аналогичные hello ниже:

**Активация Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Активация выполнена успешно.**

## <a name="faq"></a>Часто задаваемые вопросы 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a>Я создал hello Windows Server 2016 из Azure Marketplace. Зачем мне tooconfigure ключ KMS для активации hello Windows Server 2016? 
 
Нет. изображение Hello в Azure Marketplace имеет hello соответствующий ключ установки клиента KMS уже настроен. 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a>Рабочих активации Windows hello одинаково независимо от того, каким образом Если hello виртуальная машина использует преимущество использования гибридной Azure (HUB) или нет? 
 
Да. 
 
### <a name="what-happens-if-windows-activation-period-expires"></a>Что произойдет, если истечет период активации Windows? 
 
Если hello льготный период уже истек, и по-прежнему не будет выполнена, Windows Server 2008 R2 и более поздних версиях Windows будут выведены дополнительные уведомления об активации. Hello стола остается черным, а установит обновления Windows, безопасности и только критические обновления, но не необязательные обновления. Видеть уведомления hello раздела внизу hello hello [условия лицензирования](http://technet.microsoft.com/en-us/library/ff793403.aspx) страницы.   

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.
