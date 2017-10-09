---
title: "Azure AD Connect: оборудование и необходимые компоненты | Документация Майкрософт"
description: "В этом разделе описываются hello необходимые условия и требования к оборудованию hello для Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 91b88fda-bca6-49a8-898f-8d906a661f07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2ec8b5da9440c92e8f9d6702d5e5e20de952b588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-for-azure-ad-connect"></a>Необходимые условия для Azure AD Connect
В этом разделе описываются hello необходимые условия и требования к оборудованию hello для Azure AD Connect.

## <a name="before-you-install-azure-ad-connect"></a>Перед установкой Azure AD Connect
Прежде чем установить Azure AD Connect и обновить DirSync, вам потребуется ряд элементов.

### <a name="azure-ad"></a>Azure AD
* Подписка Azure или [пробная подписка Azure](https://azure.microsoft.com/pricing/free-trial/). Эта подписка является только необходимые для доступа к hello портал Azure и не с помощью Azure AD Connect. При использовании PowerShell или Office 365, то подписка Azure toouse Azure AD Connect не требуется. Если у вас есть лицензия на Office 365, можно также использовать портал Office 365 hello. С платной лицензией Office 365 можно также получить в hello портал Azure с портала Office 365 hello.
  * Можно также использовать hello [портал Azure](https://portal.azure.com). Для этого не нужна лицензия Azure AD.
* [Добавление и Проверка домена hello](../active-directory-domains-add-azure-portal.md) планирование toouse в Azure AD. Например если план toouse contoso.com для пользователей, а затем убедитесь, что этот домен проверен и домен по умолчанию contoso.onmicrosoft.com hello только не используется.
* Клиент Azure AD по умолчанию может вмещать 50 тыс. объектов. При проверке домена hello ограничен Повышенная too300k объектов. Если требуются даже дополнительные объекты в Azure AD, то необходимо tooopen еще больше увеличить ограничение hello toohave вариантов поддержки. Если вам необходимо более 500 тыс. объектов, то потребуется лицензия, например на Office 365, Azure AD Basic, Azure AD Premium или Enterprise Mobility + Security.

### <a name="prepare-your-on-premises-data"></a>Подготовка локальных данных
* Используйте [IdFix](https://support.office.com/article/Install-and-run-the-Office-365-IdFix-tool-f4bd2439-3e41-4169-99f6-3fabdfa326ac) tooidentify ошибки, например повторяющиеся значения и проблем с форматированием в вашем каталоге, прежде чем синхронизировать tooAzure AD и Office 365.
* Просмотрите [необязательные функции синхронизации, которые можно включить в Azure AD](active-directory-aadconnectsyncservice-features.md) , и решите, какие их них необходимо использовать.

### <a name="on-premises-active-directory"></a>Локальная служба Active Directory
* Hello AD версии и лесом функциональном уровне схемы должен быть Windows Server 2003 или более поздней версии. контроллеры домена Hello можно запустить любой версии, при условии, что hello схемы и леса уровня требований.
* При планировании функции hello toouse **обратной записи паролей**, то должен быть hello контроллеров домена в Windows Server 2008 (с последней SP) или более поздней версии. Если контроллеры доменов используют версию Windows Server 2008, предшествующую R2, необходимо также применить [исправление KB2386717](http://support.microsoft.com/kb/2386717).
* контроллер домена Hello, используемый Azure AD должен быть доступным для записи. Это **не поддерживается** toouse RODC (контроллер домена только для чтения) и Azure AD Connect не соблюдаются все записи перенаправления.
* Это **не поддерживается** toouse локальных лесов и доменов с помощью кодам (отдельные домены метки).
* Это **не поддерживается** toouse локальных лесов и доменов с помощью «точками» (имя содержит точку «.») NetBIOS-имена.
* Рекомендуется слишком[включить корзину Active Directory hello](active-directory-aadconnectsync-recycle-bin.md).

### <a name="azure-ad-connect-server"></a>Сервер Azure AD Connect
* Службу Azure AD Connect нельзя установить на Small Business Server или Windows Server Essentials. Hello server необходимо использовать Windows Server standard и более.
* Hello Azure AD Connect сервере должен быть полным графическим пользовательским Интерфейсом установлен. Это **не поддерживается** tooinstall на server core.
* Azure AD Connect необходимо установить на сервер под управлением ОС Windows Server, начиная с версии 2008. Это может быть контроллер домена или рядовой сервер, если используются стандартные параметры. При использовании настраиваемых параметров сервера hello также может быть автономного и не имеет toobe присоединены к домену tooa домена.
* Если установить Azure AD Connect на Windows Server 2008 или Windows Server 2008 R2, убедитесь в том tooapply hello последние исправления из центра обновления Windows. Установка Hello не может toostart с исходными сервером.
* Если планируется функции hello toouse **синхронизации паролей**, то hello Azure AD Connect server должен быть Windows Server 2008 R2 SP1 или более поздней версии.
* Если планируется toouse **групповой управляемой учетной записи службы**, то должен быть hello Azure AD Connect-server в Windows Server 2012 или более поздней версии.
* Hello Azure AD Connect сервер должен иметь [.NET Framework 4.5.1](#component-prerequisites) или более поздней версии и [Microsoft PowerShell 3.0](#component-prerequisites) или более поздней версии.
* сервер Hello Azure AD Connect не должен иметь PowerShell транскрипции групповой политикой.
* При развертывании служб федерации Active Directory, hello серверов, где установлены службы AD FS или прокси веб-приложения должен быть Windows Server 2012 R2 или более поздней версии. [удаленное управление Windows](#windows-remote-management) .
* При развертывании служб федерации Active Directory необходимы [SSL-сертификаты](#ssl-certificate-requirements).
* Если выполняется развертывание служб федерации Active Directory, то вы должны tooconfigure [разрешение имен](#name-resolution-for-federation-servers).
* Глобальные администраторы имеют многофакторной проверки Подлинности включена, затем hello URL-адрес **https://secure.aadcdn.microsoftonline-p.com** должен находиться в список надежных сайтов hello. Все запрашиваемые tooadd, которую этот список сайтов toohello надежных узлов при появлении запрос многофакторной проверки Подлинности, и он не добавил до. Можно использовать Internet Explorer tooadd его tooyour надежные сайты.

### <a name="sql-server-used-by-azure-ad-connect"></a>SQL Server, используемый Azure AD Connect
* Azure AD Connect требуется база данных SQL Server toostore удостоверений. По умолчанию устанавливается SQL Server 2012 Express LocalDB (облегченная версия SQL Server Express). SQL Server Express имеет ограничение размера в 10 ГБ, что позволяет toomanage около 100 000 объектов. Если вам требуется toomanage больше объектов каталога, необходимо toopoint hello установки мастер tooa другая установка SQL Server.
* При использовании отдельного SQL Server действуют следующие требования:
  * Azure AD Connect поддерживает все выпуски Microsoft SQL Server от SQL Server 2008 (с последним пакетом) tooSQL Server 2016 SP1. База данных SQL Microsoft Azure в качестве базы данных **не поддерживается** .
  * Необходимо использовать параметры сортировки SQL без учета регистра. Их можно определить по суффиксу \_CI_ в имени. Это **не поддерживается** toouse — параметры сортировки с учетом регистра, обозначенную \_CS_ в их именах.
  * На один экземпляр SQL может приходиться только один модуль синхронизации. Это **не поддерживается** tooshare SQL экземпляр синхронизации FIM или MIM DirSync и Azure AD Sync.

### <a name="accounts"></a>Учетные записи
* Учетная запись глобального администратора Azure AD для клиента hello Azure AD, которого нужно toointegrate с. Это должна быть **учебная или рабочая учетная запись**. **Учетную запись Майкрософт** использовать нельзя.
* Учетная запись администратора предприятия для локальной службы Active Directory при использовании экспресс-параметров или обновлении с DirSync.
* [Учетные записи в Active Directory](active-directory-aadconnect-accounts-permissions.md) при использовании пути установки hello настраиваемые параметры.

### <a name="connectivity"></a>Соединение
* Hello Azure AD Connect server требуется разрешение DNS для интрасети и Интернета. Hello DNS server должен иметь tooresolve имена обоих tooyour локальной Active Directory и hello конечные точки Azure AD.
* При наличии брандмауэров в интрасети и требуются порты tooopen между hello Azure AD Connect серверов и контроллеров домена, затем в разделе [Azure AD Connect порты](active-directory-aadconnect-ports.md) для получения дополнительной информации.
* Если лимита прокси-сервер или брандмауэр, к которому можно получить URL-адреса, затем hello URL-адреса, описаны в [Office 365 URL-адреса и IP-адресов](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) должен быть открыт.
  * При использовании Microsoft Cloud в Германии и облако Microsoft Azure для государственных hello hello, а затем в разделе [служба синхронизации Azure AD Connect экземпляров вопросы](active-directory-aadconnect-instances.md) для URL-адресов.
* По умолчанию, с помощью toocommunicate TLS 1.0 в Azure AD — Azure AD Connect. Это tooTLS 1.2 можно изменить с помощью инструкции hello в [включить TLS 1.2 для Azure AD Connect](#enable-tls-12-for-azure-ad-connect).
* При использовании исходящего прокси-сервера для подключения toohello Интернет hello следующий параметр в hello **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config** файл должен быть добавлен для приветствия мастера установки и Azure AD Connect sync toobe может tooconnect toohello Интернета и Azure AD. Необходимо указать этот текст hello нижней части файла hello. В этом коде &lt;PROXYADRESS&gt; представляет hello прокси IP адрес или имя узла.

```
    <system.net>
        <defaultProxy>
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Если прокси-сервер требует проверки подлинности, то hello [учетной записи службы](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) должен быть размещен в hello домен и вам необходимо использовать hello настроенные параметры установки пути toospecify [учетной записи пользовательские службы](active-directory-aadconnect-get-started-custom.md#install-required-components). Необходимо также toomachine.config другое изменение. После этого изменения в файле machine.config hello установки мастера и синхронизации модуль отвечать tooauthentication запросы hello прокси-сервера. На всех страницах мастера установки, за исключением hello **Настройка** страница hello вход пользователя используются учетные данные. На hello **Настройка** страницы в конце приветствия мастера установки hello, hello контекста является коммутируемой toohello [учетной записи службы](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) , созданного пользователем. раздел Hello machine.config должна выглядеть следующим образом.

```
    <system.net>
        <defaultProxy enabled="true" useDefaultCredentials="true">
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Когда Azure AD Connect tooAzure запрос web AD отправляет как часть синхронизации каталогов, Azure AD может занять toorespond too5 минут. Чаще всего настройки времени ожидания простоя подключения toohave серверы прокси. Убедитесь, что конфигурация hello настроена tooat как минимум 6 минут или более.

Дополнительные сведения см. в разделе MSDN о hello [по умолчанию прокси элемент](https://msdn.microsoft.com/library/kd3cf2ex.aspx).  
В случае проблем с подключением изучите статью [Устранение неполадок подключения в Azure AD Connect](active-directory-aadconnect-troubleshoot-connectivity.md).

### <a name="other"></a>Другие
* Необязательно: Тестового пользователя учетной записи tooverify синхронизации.

## <a name="component-prerequisites"></a>Предварительные требования к компонентам
### <a name="powershell-and-net-framework"></a>PowerShell и .Net Framework
Работа Azure AD Connect основана на Microsoft PowerShell и .NET Framework 4.5.1. На сервере должна быть установлена эта или более поздняя версия. В зависимости от установленной версии Windows Server hello следующие:

* Windows Server 2012R2
  * Microsoft PowerShell устанавливается по умолчанию. Никаких действий не требуется.
  * Платформа .NET Framework 4.5.1 и более поздних версий распространяется через Центр обновления Windows. Убедитесь, что вы установили последнюю tooWindows обновления сервера hello hello панели управления.
* Windows Server 2008R2 и Windows Server 2012
  * Hello последнюю версию Microsoft PowerShell доступна в **Windows Management Framework 4.0**, которые доступны на [центра загрузки Майкрософт](http://www.microsoft.com/downloads).
  * .NET Framework 4.5.1 и более поздние версии платформы доступны в [центре загрузки Майкрософт](http://www.microsoft.com/downloads).
* Windows Server 2008
  * Hello поддерживается последней версии PowerShell доступна в **Windows Management Framework 3.0**, которые доступны на [центра загрузки Майкрософт](http://www.microsoft.com/downloads).
  * .NET Framework 4.5.1 и более поздние версии платформы доступны в [центре загрузки Майкрософт](http://www.microsoft.com/downloads).

### <a name="enable-tls-12-for-azure-ad-connect"></a>Включение протокола TLS 1.2 для Azure AD Connect
Azure AD Connect с использованием TLS 1.0 по умолчанию для шифрования передаваемых данных hello сервер подсистемы синхронизации hello и Azure AD. Это можно изменить путем настройки приложений .net toouse TLS 1.2 по умолчанию на сервере hello. Дополнительные сведения о протоколе TLS 1.2 см. в статье [Советы по безопасности (Microsoft) (2960358)](https://technet.microsoft.com/security/advisory/2960358).

1. В Windows Server 2008 включить протокол TLS 1.2 нельзя. Требуется Windows Server 2008 R2 или более поздней версии. Убедитесь, что установлено исправление .net 4.5.1 hello для вашей операционной системы см. в разделе [2960358 советы по безопасности Майкрософт](https://technet.microsoft.com/security/advisory/2960358). Это исправление или его более поздняя версия может быть уже установлена на вашем сервере.
2. Если вы используете Windows Server 2008 R2, убедитесь, что протокол TLS 1.2 включен. На сервере с Windows Server 2012 или более поздней версии протокол TLS 1.2 должен быть уже включен.
   ```
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2]
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   ```
3. Для всех операционных систем значение этого раздела реестра и перезапустите сервер hello.
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319
   "SchUseStrongCrypto"=dword:00000001
   ```
4. Если также требуется tooenable TLS 1.2 между сервер подсистемы синхронизации hello и удаленный экземпляр SQL Server, а затем убедитесь, что установлены необходимые hello версии для [поддержка TLS 1.2 для Microsoft SQL Server](https://support.microsoft.com/kb/3135244).

## <a name="prerequisites-for-federation-installation-and-configuration"></a>Предварительные требования для установки и настройки федерации
### <a name="windows-remote-management"></a>Удаленное управление Windows
При использовании Azure AD Connect toodeploy служб федерации Active Directory или hello прокси веб-приложения, необходимо проверьте следующие требования.

* Если hello целевой сервер присоединен к домену, затем включить удаленный управляемых Windows
  * В командном окне PSH с повышенными привилегиями выполните команду `Enable-PSRemoting –force`.
* Если целевой сервер hello неприсоединенных к домену компьютере WAP, то существует несколько дополнительных требований
  * На конечном компьютере hello (WAP по умолчанию):
    * Обеспечить hello winrm (удаленное управление Windows / WS-Management) службы выполняется через оснастку служб hello
    * В командном окне PSH с повышенными привилегиями выполните команду `Enable-PSRemoting –force`.
  * На компьютере hello, на какие hello выполняется мастер (если hello целевой машине недоменных присоединены к домену или недоверенном домене):
    * В окне команд с повышенными привилегиями PSH команда hello`Set-Item WSMan:\localhost\Client\TrustedHosts –Value <DMZServerFQDN> -Force –Concatenate`
    * В диспетчере серверов:
      * Добавьте пул toomachine узлов сети Периметра WAP (диспетчера сервера -> Управление -> Добавить серверы... Используйте вкладку «DNS»)
      * Вкладка диспетчера сервера всем серверам: щелкните правой кнопкой мыши WAP-серверу и выбрать управлять как...., введите учетные данные локальной (не домен) для машины WAP hello
      * подключения удаленных PSH toovalidate, в hello вкладку Server Manager все серверы: щелкните правой кнопкой мыши WAP-сервера и выберите команду Windows PowerShell. Должен открыться удаленный сеанс PSH tooensure удаленных сеансов PowerShell может быть установлено.

### <a name="ssl-certificate-requirements"></a>Требования к сертификатам SSL
* Настоятельно рекомендуется toouse hello же SSL-сертификат на всех узлах фермы AD FS и прокси-серверы все веб-приложения.
* Hello сертификат должен быть X509 сертификат.
* На серверах федерации в тестовой лабораторной среде можно использовать самозаверяющий сертификат. Тем не менее для рабочей среды рекомендуется получать сертификат hello в общедоступном ЦС.
  * Если с помощью сертификата, который не является доверенным публично, убедитесь, что hello установить сертификат на каждый сервер прокси веб-приложения является доверенным на локальном сервере оба hello и на всех серверах федерации
* удостоверение Hello hello сертификата должно соответствовать имени службы федерации hello (например, sts.contoso.com).
  * удостоверение Hello является либо расширение альтернативного имени СУБЪЕКТА субъекта типа dnsname, или в случае операций SAN hello имя субъекта, указанное как общее имя.  
  * Несколько значений SAN может присутствовать в сертификате hello, предоставляемых один из них соответствует имени службы федерации hello.
  * Если вы планируете toouse присоединения к рабочему месту, дополнительные сети хранения данных должен иметь значение hello **enterpriseregistration.** за которым следует суффикс основного имени пользователя (UPN) hello вашей организации, например, **enterpriseregistration.contoso.com**.
* Сертификаты на основе ключей CryptoAPI следующего поколения (CNG) и поставщики хранилища ключей не поддерживаются. Это означает, что необходимо использовать сертификаты, выданные CSP (поставщиком служб шифрования), а не KSP (поставщиком хранилища ключей).
* Поддерживаются групповые сертификаты.

### <a name="name-resolution-for-federation-servers"></a>Разрешение имен для серверов федерации
* Настройка записей DNS для hello имя службы федерации AD FS (например sts.contoso.com) для интрасети hello (внутренние DNS-сервере) и hello экстрасети (общедоступном DNS-Сервере через вашего регистратора домена). Для записи DNS интрасети hello, обязательно используйте значение записи и не записи CNAME. Это необходимо для toowork проверки подлинности windows Forms из ваш компьютер присоединен к домену.
* Если выполняется развертывание более одного сервера AD FS или веб-приложения прокси-сервера, то убедитесь, что вы настроили балансировки нагрузки и, hello DNS-записи для федерации hello AD FS службой toohello точки имя (например sts.contoso.com) подсистемы балансировки нагрузки.
* Toowork встроенную проверку подлинности windows для приложений браузера с помощью Internet Explorer в интрасети убедитесь, что в IE, hello имя службы федерации AD FS (например sts.contoso.com) добавляется toohello зоны интрасети. Этим значением можно управлять с помощью групповой политики и развернутых tooall вашей, присоединенных к домену компьютеров.

## <a name="azure-ad-connect-supporting-components"></a>Вспомогательные компоненты Azure AD Connect
Hello ниже приведен список компонентов, которые Azure AD Connect устанавливает на сервер hello, где установлен Azure AD Connect. Этот список предназначен для базовой установки Express. Если выбрать другой SQL Server toouse на hello установить страницы службы синхронизации, затем SQL Express LocalDB не установлен локально.

* Azure AD Connect Health
* Помощник по входу в Microsoft Online Services для ИТ-специалистов (установлен, но не обязателен)
* Программы командной строки Microsoft SQL Server 2012
* Microsoft SQL Server 2012 Express LocalDB
* Microsoft SQL Server 2012 Native Client
* Распространяемый пакет Microsoft Visual C++ 2013

## <a name="hardware-requirements-for-azure-ad-connect"></a>Требования к оборудованию для Azure AD Connect
в следующей таблице Hello показывает hello минимальным требованиям для компьютера синхронизации Azure AD Connect hello.

| Количество объектов в Active Directory | ЦП | Память | Размер жесткого диска |
| --- | --- | --- | --- |
| Менее 10 000 |1,6 ГГц |4 ГБ |70 ГБ |
| 10 000–50 000 |1,6 ГГц |4 ГБ |70 ГБ |
| 50 000–100 000 |1,6 ГГц |16 ГБ |100 ГБ |
| Для 100 000 или более объектов требуется hello полную версию SQL Server | | | |
| 100 000–300 000 |1,6 ГГц |32 ГБ |300 ГБ |
| 300 000–600 000 |1,6 ГГц |32 ГБ |450 ГБ |
| Более 600 000 |1,6 ГГц |32 ГБ |500 ГБ |

Здравствуйте, минимальным требованиям для компьютеров под управлением AD FS или серверов веб-приложений необходимо hello в следующем:

* процессор: двухъядерный с тактовой частотой 1,6 ГГц или выше;
* память: 2 ГБ или более;
* виртуальная машина Azure: конфигурация A2 или выше.

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
