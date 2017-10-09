---
title: "aaaIntegrate хранилища ключей с SQL Server на виртуальных машинах Windows в Azure (диспетчера ресурсов) | Документы Microsoft"
description: "Узнайте, как tooautomate hello конфигурация шифрования SQL Server для использования с хранилищем ключей Azure. Этот раздел объясняет, как toouse интеграция хранилища ключей Azure с виртуальными машинами SQL Server создавать с помощью диспетчера ресурсов."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a>Настройка интеграции Azure Key Vault для SQL Server на виртуальных машинах Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](virtual-machines-windows-ps-sql-keyvault.md)
> * [Классический](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Обзор
Существует несколько функций шифрования SQL Server, например [прозрачное шифрование данных (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [шифрование на уровне столбцов (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) и [шифрование резервной копии](https://msdn.microsoft.com/library/dn449489.aspx). Эти формы шифрования требуют toomanage и хранения hello криптографических ключей, который используется для шифрования. Hello службы хранилища ключей Azure (AKV) — спроектированный tooimprove hello безопасности и управления из этих ключей в расположении высокой надежности и безопасности. Hello [соединителя SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) позволяет SQL Server toouse эти ключи из хранилища ключей Azure.

При работе с приложением SQL Server с локальной машины, существует, [действия можно выполнить tooaccess хранилище ключей Azure с локального компьютера SQL Server](https://msdn.microsoft.com/library/dn198405.aspx). Но для SQL Server в виртуальных машинах Azure, вы можете сэкономить время с помощью hello *интеграция хранилища ключей Azure* компонентов.

Если эта функция включена, автоматически устанавливает hello соединителя SQL Server, настраивает tooaccess поставщика расширенного управления Ключами hello хранилище ключей Azure и создает tooallow hello учетных данных вы tooaccess вашего хранилища. Если был рассмотрен hello инструкциям hello упомянутых выше локальной документации, вы увидите, что эта функция автоматизирует шаги 2 и 3. Единственное Hello по-прежнему необходимо toodo вручную — хранилище ключей toocreate hello и ключи. После этого выполняется автоматически hello всю настройку ВМ SQL. После завершения программы установки эту функцию можно выполнить toobegin инструкции T-SQL, шифрование баз данных или резервного копирования, как обычно.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a>Включение и настройка интеграции AKV
Интеграцию AKV можно включить во время подготовки или настроить ее для существующих виртуальных машин.

### <a name="new-vms"></a>Новые виртуальные машины
При подготовке новой виртуальной машины SQL Server с помощью диспетчера ресурсов hello портал Azure предоставляет tooenable шаг интеграцию хранилища ключей Azure. функция хранилища ключей Azure Hello доступна только для hello Enterprise, Developer и Evaluation выпусками SQL Server.

![Интеграция SQL с хранилищем ключей Azure](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

Подробное пошаговое руководство подготовки см. в разделе [подготовки виртуальной машины SQL Server в портале Azure hello](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Существующие виртуальные машины
Выберите существующую виртуальную машину SQL Server. Затем выберите hello **конфигурации SQL Server** раздел hello **параметры** колонку.

![Интеграция AKV SQL для существующих виртуальных машин](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

В hello **конфигурации SQL Server** колонка, щелкните hello **изменить** кнопку в hello разделе автоматическое хранилище ключей.

![Настройка интеграции AKV SQL для существующих виртуальных машин](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

По завершении нажмите кнопку hello **ОК** кнопку внизу hello hello **конфигурации SQL Server** toosave колонке изменения.

> [!NOTE]
> Можно также настроить интеграцию AKV с помощью шаблона. Чтобы получить дополнительные сведения, ознакомьтесь с [шаблоном быстрого запуска Azure для интеграции с хранилищем ключей Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

