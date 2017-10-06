---
title: "aaaHow toogenerate и передача ключей, защищенных HSM для хранилища ключей Azure | Документы Microsoft"
description: "Используйте этот toohelp статьи для планирования, создания и затем перенести собственные ключей, защищенных HSM toouse с хранилищем ключей Azure. Также известные как собственные ключи или BYOK."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a>Как toogenerate и передача ключей, защищенных HSM для хранилища ключей Azure
## <a name="introduction"></a>Введение
При использовании хранилища ключей Azure, для повышения надежности можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM), никогда не покидают границ HSM hello. Этот сценарий часто является ссылка tooas *Используй свой ключ*, или BYOK. Hello аппаратные модули безопасности являются FIPS 140-2 уровня 2 проверки. Хранилище ключей Azure использует семейство Thales nShield HSM tooprotect ключей.

Используйте hello сведения в этой статье toohelp планирования, создания и затем перенести собственные ключей, защищенных HSM toouse с хранилищем ключей Azure.

Эта функция недоступна для Китая.

> [!NOTE]
> Дополнительные сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)  
>
> Указания по началу работы, включая создание хранилища для ключей, защищенных аппаратным модулем безопасности, см. в статье [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md).
>
>

Дополнительные сведения о создании и передаче Перенос аппаратно защищенного ключа по Интернету hello:

* Вы создаете ключ hello рабочую станцию вне сети, что снижает уязвимость hello.
* Hello ключ шифруется с помощью ключа обмена ключ Ключами, который остается зашифрованным, пока он не переносятся toohello HSM хранилища ключей Azure. Hello только зашифрованная версия ключа покидает исходную рабочую станцию hello.
* Hello набор средств задает свойства ключа клиента, который привязывает вашего ключа toohello системы безопасности хранилища ключей Azure. Поэтому после HSM хранилища ключей Azure hello получат и расшифруют ключ, только эти аппаратные модули безопасности смогут использовать его. Экспортировать ключ нельзя. Эта привязка применяется hello аппаратные модули безопасности Thales.
* Hello обмена ключ (Ключами), используемые tooencrypt ваш ключ создается в HSM хранилища ключей Azure hello и не может быть экспортирован. Hello аппаратные модули безопасности принудительно, что может быть не точной версии hello ключа обмена Ключами вне hello аппаратные модули безопасности. Кроме того hello набор средств включает аттестацию Thales, hello ключа обмена Ключами не может быть экспортирован и был создан в подлинном аппаратном модуле безопасности, изготовленным Thales.
* Hello набор средств включает аттестацию Thales, hello world безопасности также была создана в подлинном аппаратном модуле безопасности, изготовленном Thales хранилище ключей Azure. Это аттестации доказывает tooyou, что корпорация Майкрософт использует подлинное оборудование.
* Корпорация Майкрософт применяет отдельные ключи шифрования ключей, а также отдельные системы безопасности в каждом географическом регионе. Такое разделение гарантирует, что ключ можно использовать только в центрах обработки данных в регионе hello, в котором он зашифрован. Например, ключ европейского клиента нельзя использовать в центрах обработки данных в Северной Америке или Азии.

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a>Дополнительные сведения об аппаратных модулях безопасности Thales и службах Майкрософт
Thales e-Security является ведущий глобальный поставщик шифрование данных и кибер безопасности решений toohello финансовых услуг, высоких технологий, производства, государственных организаций и секторов технологии. 40-летнем опыте защиты корпоративной и государственной информации 4 hello пяти крупнейших энергетических и аэрокосмическое оборудование компаний при использовании решения Thales. Эти решения также используются в 22 странах НАТО и защищают более 80 процентов платежных транзакций по всему миру.

Майкрософт сотрудничает с Thales tooenhance hello технического развития аппаратных модулей безопасности. Эти улучшения позволяют tooget hello стандартные преимущества размещаемых служб, не уменьшая контроль над ключами. В частности эти усовершенствования позволят корпорации Майкрософт управлять hello аппаратные модули безопасности, чтобы не нужно. Как облако, хранилище ключей service, Azure легко масштабируется в краткое уведомление toomeet резко возрастает использования вашей организации. AT hello же время ваш ключ защищен аппаратными модулями безопасности корпорации Майкрософт: вы получаете контроль над жизненным циклом ключа hello, так как создание ключа hello и передать его в tooMicrosoft аппаратные модули безопасности.

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a>Реализация сценария BYOK для хранилища ключей Azure
Hello используйте следующие сведения и процедуры, если будет создавать Перенос аппаратно защищенного ключа, а затем перенести tooAzure хранилище ключей — hello перевести сценарию ключа (BYOK).

## <a name="prerequisites-for-byok"></a>Предварительные требования для BYOK
См. в следующей таблице список предварительных требований для hello личной передачи собственного ключа (BYOK) для хранилища ключей Azure.

| Требование | Дополнительные сведения |
| --- | --- |
| TooAzure подписки |toocreate хранилище ключей Azure, необходимо получить подписку Azure: [Подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/) |
| Здравствуйте, хранилище ключей Azure Premium службы уровня toosupport ключей, защищенных HSM |Дополнительные сведения об уровнях обслуживания hello и возможностях для хранилища ключей Azure см. в разделе hello [цены на хранилище ключей Azure](https://azure.microsoft.com/pricing/details/key-vault/) веб-сайта. |
| Аппаратный модуль безопасности Thales, смарт-карты и программное обеспечение поддержки |Необходимо иметь доступ к tooa аппаратный модуль безопасности Thales и базовые знания о аппаратные модули безопасности Thales. В разделе [аппаратный модуль безопасности Thales](https://www.thales-esecurity.com/msrms/buy) hello список совместимых моделей или toopurchase модуль HSM, если не имеется. |
| Здравствуйте, следующие оборудования и программного обеспечения:<ol><li>Автономная рабочая станция x64 с операционной системой Windows версии не ниже Windows 7 и программным обеспечением Thales nShield версии не ниже 11.50.<br/><br/>Если рабочая станция выполняется на ОС Windows 7, [установите Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</li><li>На рабочей станции, подключенной toohello Интернета с минимальной операционной системы Windows, Windows 7 и [Azure PowerShell](/powershell/azure/overview) **минимальной версии 1.1.0** установлен.</li><li>USB-накопитель или другое переносное устройство хранения, на котором имеется не менее 16 МБ свободного места.</li></ol> |По соображениям безопасности рекомендуется первую рабочую станцию, hello не является tooa подключенной сети. Однако это не применяется принудительно программным путем.<br/><br/>Обратите внимание, что в дальнейших инструкциях hello этой рабочей станции рабочей станции ссылка tooas hello отключен.</p></blockquote><br/>Кроме того Если ваш ключ клиента предназначен для производственной сети, рекомендуется использовать вторую, отдельную рабочую станцию toodownload hello набор средств и отправки hello ключ клиента. Однако в целях тестирования можно использовать hello рабочую станцию, как первое hello.<br/><br/>Обратите внимание, что в hello, следуйте инструкциям, вторая рабочая станция hello ссылка tooas подключенного к Интернету рабочей станции.</p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a>Создание и передача вашего ключа tooAzure HSM хранилища ключей
Будет использовать следующие пять шагов toogenerate hello и передача вашего ключа tooan HSM хранилища ключей Azure:

* [Шаг 1. Подготовка рабочей станции, подключенной к Интернету](#step-1-prepare-your-internet-connected-workstation)
* [Шаг 2. Подготовка отключенной рабочей станции](#step-2-prepare-your-disconnected-workstation)
* [Шаг 3. Создание ключа](#step-3-generate-your-key)
* [Шаг 4. Подготовка ключа к передаче](#step-4-prepare-your-key-for-transfer)
* [Шаг 5: Передача вашего ключа tooAzure хранилища ключей](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a>Шаг 1. Подготовка рабочей станции, подключенной к Интернету
Для первого шага hello следующих процедур на рабочей станции, подключенной toohello Интернета.

### <a name="step-11-install-azure-powershell"></a>Шаг 1.1. Установка Azure PowerShell
С компьютера, подключенного к Интернету hello Загрузите и установите модуль Azure PowerShell hello, содержащий toomanage hello командлеты хранилища ключей Azure. Требуется версия не ниже 0.8.13.

Инструкции по установке см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

### <a name="step-12-get-your-azure-subscription-id"></a>Шаг 1.2. Получение идентификатора подписки Azure
Запустите сеанс Azure PowerShell и войдите в tooyour учетная запись Azure с помощью hello следующую команду:

        Add-AzureAccount
В hello всплывающем окне браузера введите имя пользователя учетной записи Azure и пароль. Затем с помощью hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) команды:

        Get-AzureSubscription
Hello в выходных данных найдите идентификатор hello для hello подписки, которая будет использоваться для хранилища ключей Azure. Этот идентификатор подписки понадобится позже.

Не закрывайте окно Azure PowerShell hello.

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a>Шаг 1.3: Загрузите набор средств BYOK hello для хранилища ключей Azure
Go toohello центра загрузки Майкрософт и [скачайте набор средств BYOK для хранилища ключей Azure hello](http://www.microsoft.com/download/details.aspx?id=45345) для географической области или экземпляр Azure. Используйте следующие hello сведения tooidentify hello пакета имя toodownload и его соответствующие SHA-256 пакета хэширования:

- - -
**США:**

KeyVault-BYOK-Tools-UnitedStates.zip

760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B

- - -
**Европа**

KeyVault-BYOK-Tools-Europe.zip

7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D

- - -
**Азия**

KeyVault-BYOK-Tools-AsiaPacific.zip

813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8

- - -
**Латинская Америка**

KeyVault-BYOK-Tools-LatinAmerica.zip

3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0

- - -
**Япония**

KeyVault-BYOK-Tools-Japan.zip

453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90

- - -
**Корея**

KeyVault-BYOK-Tools-Korea.zip

C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A

- - -
**Австралия**

KeyVault-BYOK-Tools-Australia.zip

4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B

- - -
[**Azure для государственных организаций:**](https://azure.microsoft.com/features/gov/)

KeyVault-BYOK-Tools-USGovCloud.zip

3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64

- - -
**Министерство обороны США**

KeyVault-BYOK-Tools-USGovernmentDoD.zip

A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D

- - -
**Канада**

KeyVault-BYOK-Tools-Canada.zip

30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7

- - -
**Германия**

KeyVault-BYOK-Tools-Germany.zip

5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261

- - -
**Индия**

KeyVault-BYOK-Tools-India.zip

136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7

- - -
**Великобритания:**

KeyVault-BYOK-Tools-UnitedKingdom.zip

ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268

- - -

целостность загруженных инструментов BYOK, из сеанса Azure PowerShell, используйте hello hello toovalidate [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) командлета.

    Get-FileHash KeyVault-BYOK-Tools-*.zip

Hello набор включено следующее hello.

* Пакет ключей обмена ключами с именем, начинающимся с **BYOK-KEK-pkg-.**
* Пакет Security World с именем, начинающимся с **BYOK-SecurityWorld-pkg-**
* Сценарий на Python с именем **verifykeypackage.py.**
* Исполняемый файл командной строки с именем **KeyTransferRemote.exe** и связанными библиотеками DLL.
* Распространяемый пакет Visual C++ с именем **vcredist_x64.exe.**

Скопируйте hello пакета tooa USB-накопитель или другое переносное устройство.

## <a name="step-2-prepare-your-disconnected-workstation"></a>Шаг 2. Подготовка отключенной рабочей станции
Для выполнения этого шага второй hello следующих процедур на рабочей станции hello, не подключенной tooa сеть (hello Интернета или внутренней сети).

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a>Шаг 2.1: Подготовка рабочей станции hello отключен с аппаратным модулем безопасности Thales
Установка hello программное обеспечение поддержки nCipher (Thales) на компьютере Windows, а затем подключите компьютер toothat аппаратный модуль безопасности Thales.

Убедитесь, что hello средства Thales находятся в вашем пути (**%nfast_home%\bin**). Например введите ниже hello:

        set PATH=%PATH%;"%nfast_home%\bin"

Дополнительные сведения см. в руководстве пользователя hello, входящий в состав hello аппаратный модуль безопасности Thales.

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a>Шаг 2.2: Набор средств BYOK установки hello на рабочей станции hello отключен
Скопируйте пакет набора средств BYOK hello с hello USB-накопитель или другое переносное устройство, а затем hello следующие:

1. Извлеките файлы hello из hello загрузки пакета в любую папку.
2. Запустите файл vcredist_x64.exe из этой папки.
3. Следуйте инструкциям hello toohello установить hello компонентов среды выполнения Visual C++ для Visual Studio 2013.

## <a name="step-3-generate-your-key"></a>Шаг 3. Создание ключа
Для выполнения этого шага третий hello следующих процедур на рабочей станции hello отключен. toocomplete этот шаг должен быть вашего аппаратного модуля безопасности в режим инициализации. 


### <a name="step-31-change-hello-hsm-mode-tooi"></a>Шаг 3.1: Изменение режима too'I hello аппаратный модуль безопасности "
Если вы используете Thales nShield границы, режим hello toochange: 1. Используйте hello режиме кнопка toohighlight hello нужный режим работы. 2. Через несколько секунд нажмите и удерживайте кнопку "Сброс" hello несколько секунд. При изменении режима hello hello новый режим Индикатор перестанет мигать и остается подсветкой. Hello Индикатор состояния может нерегулярно flash на несколько секунд и затем мигает регулярно при готовности устройства hello. В противном случае горит hello устройство остается в текущем режиме hello режимом hello соответствующий Индикатор.

### <a name="step-32-create-a-security-world"></a>Шаг 3.2. Создание системы безопасности
Откройте командную строку и запустите hello программы Thales новой системы.

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

Эта программа создает **системы безопасности** файл в каталоге % NFAST_KMDATA%\local\world, который соответствует папке C:\ProgramData\nCipher\Key Management Data\local toohello. Можно использовать разные значения для кворума hello, но в нашем примере выполняется запрос tooenter три пустых карты и закрепления для каждой из них. После этого любые две карты присвойте системы безопасности toohello полный доступ. Эти карты станут hello **набором карт администратора** для hello новой системы безопасности.

Затем hello следующие:

* Создайте резервную копию файла hello world. Защитите файл hello world hello карты администратора и их закрепления и убедитесь, что никто имеет toomore доступ, чем к одной карте.

### <a name="step-33-change-hello-hsm-mode-tooo"></a>Шаг 3.3: Изменение режима too'O hello аппаратный модуль безопасности "
Если вы используете Thales nShield границы, режим hello toochange: 1. Используйте hello режиме кнопка toohighlight hello нужный режим работы. 2. Через несколько секунд нажмите и удерживайте кнопку "Сброс" hello несколько секунд. При изменении режима hello hello новый режим Индикатор перестанет мигать и остается подсветкой. Hello Индикатор состояния может нерегулярно flash на несколько секунд и затем мигает регулярно при готовности устройства hello. В противном случае горит hello устройство остается в текущем режиме hello режимом hello соответствующий Индикатор.


### <a name="step-34-validate-hello-downloaded-package"></a>Шаг 3.4: Проверка пакета загружаются hello
Этот шаг необязателен, но рекомендуется, чтобы вы могли проверить следующее hello.

* Hello ключа обмена ключами, которое включено в набор инструментов hello был создан в подлинном аппаратном модуле безопасности Thales.
* хэш Hello hello World безопасности, включенный в набор инструментов hello был создан в подлинном аппаратном модуле безопасности Thales.
* Hello ключа обмена ключами не экспортируется.

> [!NOTE]
> toovalidate hello загружен пакет, hello аппаратный модуль безопасности должен быть подключен, включен и должен иметь систему безопасности его (например, «hello, который вы только что создали).
>
>

пакет загружен hello toovalidate:

1. Запустите скрипт verifykeypackage.py hello, введите одно из следующих hello, в зависимости от географической области или экземпляр Azure:

   * Для Северной Америки:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * Для Европы:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * Для Азии:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * Для Латинской Америки:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * Для Японии:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * Для Кореи:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * Для Австралии:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * Для [Azure для государственных](https://azure.microsoft.com/features/gov/), которая использует экземпляр правительства США hello Azure:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * Для министерства обороны США:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * Для Канады:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * Для Германии:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * Для Индии:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > Hello программное обеспечение Thales включает файл python в %NFAST_HOME%\python\bin
     >
     >
2. Подтвердите, что вы видите следующее hello, что указывает на успешную проверку: **результат: успех**

Этот скрипт проверяет цепочку подписавшего hello вверх toohello корневого ключа Thales. Hello хэш этого корневого ключа встроен в скрипт hello и его значение должно быть **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Вы можете также подтвердить это значение отдельно, посетив hello [веб-сайт Thales](http://www.thalesesec.com/).

Теперь вы готовы toocreate новый ключ.

### <a name="step-35-create-a-new-key"></a>Шаг 3.5. Создание ключа
Создать ключ с помощью hello Thales **generatekey** программы.

Выполните следующие команды toogenerate hello ключ hello.

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

При выполнении команды следуйте приведенным ниже инструкциям.

* Здравствуйте, параметр *защиты* необходимо присвоить значение toohello **модуль**, как показано. В результате будет создан ключ, защищенный модулем. набор средств BYOK Hello не поддерживает ключи, защищенные периодически подключаемыми системами.
* Замените значение hello *contosokey* для hello **ident** и **plainname** с любым строковым значением. toominimize административные затраты и уменьшить риск hello ошибок, рекомендуется использовать одинаковое значение для обоих hello. Hello **ident** значение должно содержать только цифры, тире и буквы нижнего регистра.
* в этом примере Hello значение pubexp остается пустым (по умолчанию), но можно указать конкретные значения. Дополнительные сведения см. в разделе hello документации Thales.

Эта команда создает файл ключа с токеном в папке %NFAST_KMDATA%\local с именем, начинающимся с **key_simple_**, а затем hello **ident** , указанный в команде hello. Пример: **key_simple_contosokey**. Этот файл содержит зашифрованный ключ.

Создайте резервную копию файла ключа с токеном в безопасном расположении.

> [!IMPORTANT]
> Позже при передаче вашего ключа tooAzure хранилище ключей, корпорация Майкрософт не может экспортировать этого ключа tooyou назад, поэтому крайне важно сделать резервную копию ключа и безопасности системы безопасно. За инструкциями и рекомендациями по резервному копированию ключа обращайтесь в компанию Thales.
>
>

Вы являются теперь готовы tootransfer вашего ключа tooAzure хранилища ключей.

## <a name="step-4-prepare-your-key-for-transfer"></a>Шаг 4. Подготовка ключа к передаче
Для выполнения этого шага четвертый hello следующих процедур на рабочей станции hello отключен.

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a>Шаг 4.1. Создание копии ключа с ограниченными разрешениями

Откройте новую командную строку и измените hello расположение текущего каталога toohello где распаковал hello BYOK ZIP-файл. tooreduce hello разрешения в ключе, из командной строки, выполните одну из следующих hello, в зависимости от географической области или экземпляр Azure.

* Для Северной Америки:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* Для Европы:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* Для Азии:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* Для Латинской Америки:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* Для Японии:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* Для Кореи:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* Для Австралии:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* Для [Azure для государственных](https://azure.microsoft.com/features/gov/), которая использует экземпляр правительства США hello Azure:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* Для министерства обороны США:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* Для Канады:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* Для Германии:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* Для Индии:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

При выполнении этой команды замените *contosokey* hello таким же значением, которое указано в **3.5 шаг: Создание нового ключа** из hello [Создание ключа](#step-3-generate-your-key) шаг.

Будет предложено tooplug карты администратора системы безопасности.

После завершения команды hello, вы видите **результат: успех** и hello копии ключа с ограниченными разрешениями, находятся в файле hello, с именем key_xferacId_<contosokey>.

Возможно проверяет hello списки управления ДОСТУПОМ с помощью следующих команд с помощью служебных программ Thales "hello":

* aclprint.py:

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* kmfile-dump.exe:

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  При выполнении этих команд замените contosokey hello таким же значением, которое указано в **3.5 шаг: Создание нового ключа** из hello [Создание ключа](#step-3-generate-your-key) шаг.

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a>Шаг 4.2. Шифрование ключа с помощью ключа обмена ключами Майкрософт
Выполните одну из следующих команд в зависимости от географического региона или экземпляр Azure hello.

* Для Северной Америки:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Для Европы:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Для Азии:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Для Латинской Америки:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Для Японии:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Для Кореи:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Для Австралии:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Для [Azure для государственных](https://azure.microsoft.com/features/gov/), которая использует экземпляр правительства США hello Azure:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Для министерства обороны США:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Для Канады:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Для Германии:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Для Индии:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

При выполнении команды следуйте приведенным ниже инструкциям.

* Замените *contosokey* с идентификатором hello, который вы использовали toogenerate hello в **3.5 шаг: Создание нового ключа** из hello [Создание ключа](#step-3-generate-your-key) шаг.
* Замените *SubscriptionID* с Идентификатором hello hello подписку Azure, содержащий ваше хранилище ключа. Вы получили это значение раньше, в **пункте 1.2: получить идентификатор подписки Azure** из hello [Подготовка рабочей станции, подключенного к Интернету](#step-1-prepare-your-internet-connected-workstation) шаг.
* Замените *ContosoFirstHSMKey* меткой, которая используется для имени выходного файла.

При этом завершается успешно, отображается **результат: успех** , и новый файл в папке hello с именем hello: KeyTransferPackage -*ContosoFirstHSMkey*.byok

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a>Шаг 4.3: Копирование к передаче ключа пакета toohello подключенного к Интернету рабочей станции
Используйте USB-накопитель или другие переносное устройство toocopy hello выходной файл hello предыдущего шага (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour подключенного к Интернету рабочей станции.

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a>Шаг 5: Передача вашего ключа tooAzure хранилища ключей
На этом этапе hello подключенного к Интернету, на рабочей станции использовать hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) пакет передачи ключа hello tooupload командлета, скопированный из hello отключен toohello рабочей станции HSM хранилища ключей Azure:

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

Если hello Отправка завершена успешно, можно увидеть свойства отображаемого hello hello ключа, который был только что добавлен.

## <a name="next-steps"></a>Дальнейшие действия
Теперь ключ, защищенный с помощью аппаратного модуля безопасности, можно использовать в хранилище ключей. Дополнительные сведения см. в разделе hello **следует toouse аппаратный модуль безопасности (HSM)** раздела hello [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md) учебника.
