---
title: "aaaInstall леса Active Directory в виртуальной сети Azure | Документы Microsoft"
description: "Учебник, в котором объясняется, как леса toocreate новый Active Directory на виртуальной машине (ВМ) в виртуальной сети Azure."
services: active-directory, virtual-network
keywords: "виртуальная машина active directory, установка леса active directory, видео azure active directory  "
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
tags: 
ms.assetid: eb7170d0-266a-4caa-adce-1855589d65d1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: joflore
ms.openlocfilehash: 08121130777cc3c206d7b5b38974982884dca1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-new-active-directory-forest-on-an-azure-virtual-network"></a>Установка нового леса Active Directory в виртуальной сети Azure
В этом разделе показано, как toocreate новый Windows Server Active Directory среды в Azure виртуальные сети для виртуальной машины (VM) на [виртуальной сети Azure](../virtual-network/virtual-networks-overview.md). В этом случае hello виртуальная сеть Azure не подключенных tooan локальной сети.

Вас также могут заинтересовать следующие связанные статьи.

* Видео, в котором показаны следующие действия, в разделе [как леса tooinstall новый Active Directory в виртуальной сети Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* Вы можете при необходимости [настройки VPN сайтами](../vpn-gateway/vpn-gateway-site-to-site-create.md) и затем установить новый лес или расширить tooan леса локальной виртуальной сети Azure. Инструкции по выполнению этих действий см. в разделе [Установка реплики контроллера домена Active Directory в виртуальной сети Azure](active-directory-install-replica-active-directory-domain-controller.md).
* Концептуальное руководство об установке доменных служб Active Directory (AD DS) в виртуальной сети Azure см. в статье [Руководства по развертыванию Windows Server Active Directory на виртуальных машинах Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Схема сценария
В этом случае внешние пользователи должны tooaccess приложения, которые выполняются на серверах, входящих в домен. Hello виртуальные машины под управлением серверов приложений hello и hello виртуальных машин, работающих на контроллерах домена устанавливаются в их собственных облачной службы в виртуальной сети Azure. Для повышения отказоустойчивости их также включает в себя группа доступности.

![Лес Active Directory на виртуальных машинах виртуальной сети Azure][1] 7

## <a name="how-does-this-differ-from-on-premises"></a>В чем отличие от локальной версии?
Этот процесс не сильно отличается от установки контроллера домена в локальной версии Azure. в hello в следующей таблице перечислены основные различия Hello.

| tooconfigure... | Локальная система | виртуальной сети Azure |
| --- | --- | --- |
| **IP-адреса для контроллера домена hello** |Назначить статический IP-адрес на hello свойств сетевого адаптера |Запустите tooassign командлета Set-AzureStaticVNetIP hello статический IP-адрес |
| **Сопоставитель DNS-клиента** |Задает предпочитаемый и Альтернативный DNS-адрес сервера hello свойств сетевого адаптера членов домена |Задать для свойства виртуальной сети hello hello адрес DNS-сервера |
| **Хранилище базы данных Active Directory** |При необходимости изменить место хранения по умолчанию hello из C:\ |Требуется toochange место хранения по умолчанию из C:\ |

## <a name="create-an-azure-virtual-network"></a>Создание виртуальной сети Azure
1. Войдите в систему toohello классический портал Azure.
2. Создайте виртуальную сеть. Щелкните **Сети** > **Создать виртуальную сеть**. Используйте значения hello в следующие таблицы toocomplete приветствия мастера hello.

   | На странице мастера… | Укажите такие значения |
   | --- | --- |
   |  **Сведения о виртуальной сети** |<p>Имя: введите имя виртуальной сети.</p><p>Область: Выберите ближайший регион hello</p> |
   |  **DNS и VPN** |<p>Оставьте поле DNS-сервера пустым</p><p>Не выбирайте также и параметр VPN</p> |
   |  **Адресные пространства виртуальной сети** |<p>Имя подсети: введите имя своей подсети.</p><p>Начальный IP-адрес: <b>10.0.0.0</b></p><p>CIDR: <b>/24 (256)</b></p> |

## <a name="create-vms-toorun-hello-domain-controller-and-dns-server-roles"></a>Создание контроллера домена hello toorun виртуальные машины и роли сервера DNS
Повторите следующие шаги toocreate роль контроллера домена toohost hello виртуальных машин при необходимости hello. Следует развернуть по крайней мере два виртуальных контроллеров домена tooprovide отказоустойчивость и избыточность. Если hello виртуальной сети Azure включает по крайней мере двух контроллеров домена, которые настроены аналогично (то есть они являются оба глобальных каталогов выполнения DNS-сервера и не содержит все роли FSMO и т. д) поместите hello виртуальных машин, которые выполняются те контроллеры домена в группу доступности для повышения отказоустойчивости.

hello toocreate виртуальных машин с помощью Windows PowerShell вместо hello пользовательского интерфейса, в разделе [toocreate использование Azure PowerShell и предварительной настройки виртуальных машин на основе Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. Hello классического портала щелкните **New** > **вычислений** > **виртуальной машины** > **из коллекции**. Используйте следующие значения toocomplete приветствия мастера hello. Примите значение параметра по умолчанию hello, если рекомендуемые или необходимые значения.

   | На странице мастера… | Укажите такие значения |
   | --- | --- |
   |  **Выбор образа** |Центр обработки данных Windows Server 2012 R2; |
   |  **Конфигурация виртуальной машины** |<p>Имя виртуальной машины: введите одно описательное имя (например, AzureDC1).</p><p>Новое имя пользователя: Имя типа hello пользователя. Этот пользователь будет членом hello локальной группы администраторов на hello виртуальной Машины. Необходимо будет это имя toosign в toohello ВМ для hello первый раз. Встроенная учетная запись Hello «администратор» не будет работать.</p><p>Новый пароль/Подтвердить: введите пароль.</p> |
   |  **Конфигурация виртуальной машины** |<p>Облачную службу: Выберите <b>создать новую облачную службу</b> для hello первая виртуальная машина и выберите нужный же облако имя службы при создании дополнительных виртуальных машин, которые будут размещаться hello роль контроллера домена.</p><p>DNS-имя облачной службы: укажите глобальное уникальное имя.</p><p>Регион, территориальная группа или виртуальная сеть: укажите имя виртуальной сети hello (например WestUSVNet).</p><p>Учетную запись хранения: Выберите <b>использовать автоматически созданную учетную запись хранения</b> для hello первая виртуальная машина, затем выберите, что имя одной учетной записи хранения при создании дополнительных виртуальных машин, которые будут размещаться hello роль контроллера домена.</p><p>Группа доступности: выберите <b>Создать группу доступности</b>.</p><p>Имя группы доступности: тип имя hello доступности задается при создании hello первая виртуальная машина, а затем выберите, точно такое же имя, при создании дополнительных виртуальных машин.</p> |
   |  **Конфигурация виртуальной машины** |<p>Выберите <b>hello установки агента виртуальной Машины</b> и другие расширения, необходимо.</p> |
2. Присоедините диск tooeach виртуальной Машине, которая будет выполняться роль сервера контроллера домена hello. дополнительный диск Hello — базы данных необходимые toostore hello AD, журналов и SYSVOL. Укажите размер для диска hello (например, 10 ГБ) и оставить hello **настройки кэша узла** значение слишком**нет**. Привет, содержится [как tooAttach tooa диска данных виртуальной машины Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. После первой регистрации в toohello виртуальной Машины, откройте **диспетчера сервера** > **файловых служб и служб хранилища** toocreate тома на этом диске, в системе NTFS.
4. Зарезервируйте статический IP-адрес для виртуальных машин, которые будет выполняться роль контроллера домена hello. tooreserve статический IP-адрес загрузки hello Microsoft Web Platform Installer и [установите Azure PowerShell](/powershell/azure/overview) и запустите командлет Set-AzureStaticVNetIP hello. Например:

    `Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM`

Дополнительные сведения о настройке статического IP-адреса см. в разделе [Как задать статический внутренний частный IP-адрес с помощью PowerShell (классическая модель)](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-windows-server-active-directory"></a>установка Windows Server Active Directory
Используйте hello же подпрограмму слишком[установку AD DS](https://technet.microsoft.com/library/jj574166.aspx) используемая локальной (то есть, можно использовать hello пользовательского интерфейса, файл ответов или Windows PowerShell). Необходимо tooinstall учетные данные администратора tooprovide нового леса. расположение hello toospecify hello базы данных Active Directory, журналам и SYSVOL, измените место хранения по умолчанию hello с hello операционной системы диска toohello дополнительный диск с данными вложенный toohello виртуальной Машины.

После завершения установки контроллера домена hello попытку подключения toohello ВМ и войдите toohello контроллера домена. Запомнить учетные данные домена toospecify.

## <a name="reset-hello-dns-server-for-hello-azure-virtual-network"></a>Сброс hello DNS-сервера для hello виртуальной сети Azure
1. Сбросьте настройку сервера пересылки DNS hello на hello нового контроллера домена или DNS-сервера.
   1. В диспетчере серверов щелкните **Инструменты** > **DNS**.
   2. В **диспетчер DNS**, щелкните правой кнопкой мыши имя hello hello DNS-сервера и нажмите кнопку **свойства**.
   3. На hello **пересылки** щелкните hello IP-адрес сервера пересылки hello и нажмите кнопку **изменить**.  Выберите hello IP-адрес и нажмите кнопку **удалить**.
   4. Нажмите кнопку **ОК** tooclose редактор hello и **ОК** снова tooclose hello свойства DNS-сервера.
2. Обновление параметра сервера hello DNS для виртуальной сети hello.
   1. Нажмите кнопку **виртуальных сетей** > дважды щелкните созданную виртуальную сеть hello > **Настройка** > **DNS-серверы**, введите имя hello и hello DIP-адрес одного из Hello виртуальные машины под управлением роли сервера DC/DNS hello и нажмите кнопку **Сохранить**.
   2. Выберите hello виртуальной Машины и нажмите кнопку **перезапустите** tootrigger hello ВМ tooconfigure параметры сопоставителя DNS с IP-адресом hello hello новый DNS-сервера.

## <a name="create-vms-for-domain-members"></a>Создание виртуальных машин для членов домена
1. Повторите следующие шаги toocreate виртуальные машины toorun как серверы приложений hello. Примите значение параметра по умолчанию hello, если рекомендуемые или необходимые значения.

   | На странице мастера… | Укажите такие значения |
   | --- | --- |
   |  **Выбор образа** |Центр обработки данных Windows Server 2012 R2; |
   |  **Конфигурация виртуальной машины** |<p>Имя виртуальной машины: введите одно описательное имя (например, AppServer1).</p><p>Новое имя пользователя: Имя типа hello пользователя. Этот пользователь будет членом hello локальной группы администраторов на hello виртуальной Машины. Необходимо будет это имя toosign в toohello ВМ для hello первый раз. Встроенная учетная запись Hello «администратор» не будет работать.</p><p>Новый пароль/Подтвердить: введите пароль.</p> |
   |  **Конфигурация виртуальной машины** |<p>Облачную службу: Выберите **создать новую облачную службу** для hello первой виртуальной Машины и выберите же облако имя службы при создании дополнительных виртуальных машин, будет размещаться приложение hello.</p><p>DNS-имя облачной службы: укажите глобальное уникальное имя.</p><p>Регион, территориальная группа или виртуальная сеть: укажите имя виртуальной сети hello (например WestUSVNet).</p><p>Учетную запись хранения: Выберите **использовать автоматически созданную учетную запись хранения** для hello первая виртуальная машина, затем выберите, что имя одной учетной записи хранения при создании дополнительных виртуальных машин, будет размещаться приложение hello.</p><p>Группа доступности: выберите **Создать группу доступности**.</p><p>Имя группы доступности: тип имя hello доступности задается при создании hello первая виртуальная машина, а затем выберите, точно такое же имя, при создании дополнительных виртуальных машин.</p> |
   |  **Конфигурация виртуальной машины** |<p>Выберите <b>hello установки агента виртуальной Машины</b> и другие расширения, необходимо.</p> |
2. После подготовки каждой виртуальной Машины, войдите и присоедините его toohello домена. В **диспетчере серверов** щелкните **Локальный сервер** > **РАБОЧАЯ ГРУППА** > **Изменить…**, а затем выберите **домена** и имя типа hello локального домена. Укажите учетные данные пользователя домена, а затем перезапустите присоединение к домену hello toocomplete hello виртуальной Машины.

hello toocreate виртуальных машин с помощью Windows PowerShell вместо hello пользовательского интерфейса, в разделе [toocreate использование Azure PowerShell и предварительной настройки виртуальных машин на основе Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Дополнительные сведения об использовании Windows PowerShell см. в разделах [Начало работы с командлетами Azure](/powershell/azure/overview) и [Справка по командлетам Azure](/powershell/azure/get-started-azureps).

## <a name="see-also"></a>См. также
* [Как tooinstall новый Active Directory леса в виртуальной сети Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* [Рекомендации по развертыванию Windows Server Active Directory на виртуальных машинах Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Настроить VPN типа «сеть-сеть»](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Установка реплики контроллера домена Active Directory в виртуальной сети Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IaaS для профессионалов в сфере IT. (01) Основная информация о виртуальных машинах](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS для профессионалов в сфере IT. (05) Создание виртуальных сетей и подключений между организациями](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Обзор виртуальной сети](../virtual-network/virtual-networks-overview.md)
* [Как tooinstall и настройка Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Справка по командлетам Azure](/powershell/azure/get-started-azureps)
* [Настройка статического IP-адреса для виртуальной машины Azure](http://windowsitpro.com/windows-azure/set-azure-vm-static-ip-address)
* [Как tooAzure tooassign статический IP-адрес виртуальной Машины](http://www.bhargavs.com/index.php/2014/03/13/how-to-assign-static-ip-to-azure-vm/)
* [Установка нового леса Active Directory](https://technet.microsoft.com/library/jj574166.aspx)
* [Введение tooActive доменных служб Directory (AD DS) Virtualization (Level 100)](https://technet.microsoft.com/library/hh831734.aspx)

<!--Image references-->
[1]: ./media/active-directory-new-forest-virtual-machine/AD_Forest.png
