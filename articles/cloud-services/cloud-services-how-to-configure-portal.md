---
title: "aaaHow tooconfigure облачной службы (портал) | Документы Microsoft"
description: "Узнайте, как tooconfigure облачных служб в Azure. Дополнительные сведения конфигурации tooupdate hello облачной службы и настраивают экземпляры toorole удаленного доступа. В этих примерах используются hello портал Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>Как tooConfigure облачных служб
> [!div class="op_single_selector"]
> * [Портал Azure](cloud-services-how-to-configure-portal.md)
> * [классическом портале Azure](cloud-services-how-to-configure.md)
>
>

Можно настроить параметры наиболее часто используемые hello для облачной службы в hello портал Azure. Или, если вам нравится tooupdate файлы конфигурации напрямую, загрузите tooupdate файла конфигурации службы, а затем отправьте hello обновления файла и обновление hello облачной службы с hello изменения конфигурации. В любом случае hello обновления конфигурации применяются tooall экземпляров роли.

Можно также управлять hello экземпляров роли облачной службы или удаленного рабочего стола в них.

Azure можете только обеспечить доступность службы 99,95% при hello обновлений конфигурации при наличии по крайней мере двух экземпляров роли для каждой роли. Которая позволяет одной виртуальной машины tooprocess клиентские запросы других hello в процессе обновления. Дополнительные сведения см. в разделе [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Изменение облачной службы
После открытия hello [портал Azure](https://portal.azure.com/), перейдите tooyour облачной службы. Здесь можно управлять множеством параметров.

![Страница «Параметры»](./media/cloud-services-how-to-configure-portal/cloud-service.png)

Hello **параметры** или **все параметры** ссылки будут открывать копию hello **параметры** колонки, где можно изменить hello **свойства**, измените hello **Конфигурации**, управлять hello **сертификаты**, программа установки **предупреждения правила**и управлять ими hello **пользователей** которые имеют доступ toothis облачной службы.

![Колонка параметров облачной службы Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>Управление версией гостевой ОС

По умолчанию Azure периодически обновляет гостевой toohello последние поддерживаемые образа ОС в hello семейство ОС, заданные в конфигурации службы (.cscfg), такие как Windows Server 2016.

Если вам требуется tootarget конкретной версии ОС, может быть задана в hello **конфигурации** колонку.

![Настройка версии ОС](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> В случае выбора конкретной версии ОС автоматические обновления операционной системы отключаются, а ответственность за установку исправлений ложится на вас. Убедитесь, что экземпляры роли получают обновления, или может привести к уязвимостям toosecurity приложения.

## <a name="monitoring"></a>Мониторинг
Можно добавлять оповещения tooyour облачной службы. Щелкните **Параметры** > **Правила оповещений** > **Добавить оповещение**.

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

Здесь можно настроить оповещение. С hello **метрика** раскрывающийся список, можно настроить оповещения для hello следующие типы данных.

* Скорость чтения с диска
* Скорость записи на диск
* Входящая скорость сети
* Исходящая скорость сети
* Процент использования ЦП

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>Настройка мониторинга с использованием плиток метрик
Вместо использования **параметры** > **правила оповещения**, можно щелкнуть один из hello плитки с метрикой hello **мониторинг** раздел hello **облака Служба** колонку.

![Мониторинг облачной службы](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

Здесь можно настроить hello диаграммы, используемой Плитка hello, или добавить правило оповещения.

## <a name="reboot-reimage-or-remote-desktop"></a>Перезагрузка, повторное создание образа и использование удаленного рабочего стола
В настоящее время не удается настроить удаленный рабочий стол с помощью hello **портал Azure**. Тем не менее, можно задать через hello [классический портал Azure](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), либо с помощью [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).

Во-первых щелкните экземпляр службы hello облака.

![Экземпляр облачной службы](./media/cloud-services-how-to-configure-portal/cs-instance.png)

В hello колонку, вы может инициировать подключение к удаленному рабочему столу, удаленно перезагрузить экземпляр hello, или удаленно экземпляр hello повторное создание образа (запуск с помощью нового образа).

![Кнопки экземпляра облачной службы](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>Изменение CSCFG-файла
Может потребоваться tooreconfigure облачной службы через hello [файла конфигурации службы (cscfg)](cloud-services-model-and-package.md#cscfg) файла. Сначала необходимо toodownload вашей .cscfg файл, измените его, а затем передать его.

1. Щелкните hello **параметры** значок или hello **все параметры** связать tooopen копирование hello **параметры** колонку.

    ![Страница «Параметры»](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. Щелкните hello **конфигурации** элемента.

    ![Колонка «Конфигурация»](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. Щелкните hello **загрузки** кнопки.

    ![Загрузить](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. После обновления файла конфигурации службы hello, загрузить и установить обновления конфигурации hello:

    ![Отправить](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. Выберите файл cscfg hello и нажмите кнопку **ОК**.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[развертывание облачной службы](cloud-services-how-to-create-deploy-portal.md).
* Настройте [пользовательское доменное имя](cloud-services-custom-domain-name-portal.md).
* [Управление облачной службой](cloud-services-how-to-manage-portal.md).
* Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate-portal.md).
