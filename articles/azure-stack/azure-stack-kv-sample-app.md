---
title: "секреты хранилище ключей Azure стека tooretrieve приложения aaaAllow | Документы Microsoft"
description: "Использование образца приложения toowork с хранилищем ключей Azure стека"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/04/2017
ms.author: sngun
ms.openlocfilehash: 2ff3f0bab86d9d1934b463f72124863d29dbe696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-for-key-vault"></a>Запустить образец приложения hello для хранилища ключей

В этом руководстве используется образец приложения tooretrieve секреты и пароли из хранилища ключей.

## <a name="download-hello-samples-and-prepare"></a>Загрузка образцов hello и подготовка
Загрузка образцов клиента хранилища ключей Azure hello из hello [странице примеров из хранилища ключей Azure клиента](https://www.microsoft.com/en-us/download/details.aspx?id=45343).

Извлеките содержимое hello локального компьютера файл .zip tooyour hello.

Чтение hello **README.md** файла (это текстовый файл), а затем выполните инструкции hello.

## <a name="run-sample-1--hellokeyvault"></a>Запуск образца #1 — HelloKeyVault
HelloKeyVault представляет собой консольное приложение, которое проведет вас через hello основные сценарии, которые поддерживаются хранилищем ключей:

1. Создание и импорта ключа (ключ HSM или программного обеспечения)
2. Зашифровать секретный код, с помощью ключа контента
3. Перенос с помощью ключа хранилища ключей ключ содержимого hello
4. Извлечение из оболочки hello ключ содержимого
5. Расшифровать секретный код hello
6. Значение секрета

Что запуска консольного приложения следует без изменений, за исключением того, будут обновлены hello подходящие параметры конфигурации в файл App.Config toohello, выполните действия в соответствии с:

1. Обновите параметры конфигурации приложения hello в HelloKeyVault\App.config с URL-адрес хранилища, основной идентификатор приложения и секрет. сведения о Hello при необходимости можно создавать с помощью **scripts\GetAppConfigSettings.ps1**.
2. Обновление значений hello hello обязательной переменные в GetAppConfigSettings.ps1.
3. Откройте окно Windows PowerShell hello.
4. Запустите сценарий GetAppConfigSettings.ps1 hello в окне PowerShell hello.
5. Копирование результатов hello hello сценария toohello HelloKeyVault\App.config файла.

## <a name="next-steps"></a>Дальнейшие действия
[Развертывание виртуальной машины с помощью пароля из хранилища ключей](azure-stack-kv-deploy-vm-with-secret.md)

[Развертывание виртуальной Машины с помощью хранилища ключей сертификата](azure-stack-kv-push-secret-into-vm.md)

