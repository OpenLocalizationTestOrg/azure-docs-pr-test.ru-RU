---
title: "Разрешить приложению получать секреты в хранилище ключей Azure стек | Документы Microsoft"
description: "Использование примера приложения для работы с хранилищем ключей Azure стека"
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
ms.openlocfilehash: 4b517526d89e7f6c2649e2f12810b4db705defa3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-the-sample-application-for-key-vault"></a>Запустить образец приложения для хранилища ключей

В этом руководстве используется образец приложения для получения секреты и пароли из хранилища ключей.

## <a name="download-the-samples-and-prepare"></a>Загрузка образцов и подготовка
Загрузка образцов клиента хранилища ключей Azure из [странице примеров из хранилища ключей Azure клиента](https://www.microsoft.com/en-us/download/details.aspx?id=45343).

Извлеките содержимое ZIP-файл на локальный компьютер.

Чтение **README.md** файла (это текстовый файл), а затем следуйте инструкциям.

## <a name="run-sample-1--hellokeyvault"></a>Запуск образца #1 — HelloKeyVault
HelloKeyVault представляет собой консольное приложение, которое проведет вас через основные сценарии, которые поддерживаются хранилищем ключей:

1. Создание и импорта ключа (ключ HSM или программного обеспечения)
2. Зашифровать секретный код, с помощью ключа контента
3. Ключ содержимого с помощью ключа хранилища ключей
4. Извлечение из оболочки ключ содержимого
5. Расшифровать секретный код
6. Значение секрета

Что запуска консольного приложения следует без изменений, за исключением того, что соответствующие настройки в файле App.Config обновляется с помощью следующих действий:

1. Обновите параметры конфигурации приложения в HelloKeyVault\App.config с URL-адрес хранилища, основной идентификатор приложения и секрет. Эти сведения можно при необходимости создаются с помощью **scripts\GetAppConfigSettings.ps1**.
2. Обновление значений обязательной переменные в GetAppConfigSettings.ps1.
3. Откройте окно Windows PowerShell.
4. Запустите сценарий GetAppConfigSettings.ps1 в окне PowerShell.
5. Скопируйте файл HelloKeyVault\App.config результаты работы скрипта.

## <a name="next-steps"></a>Дальнейшие действия
[Развертывание виртуальной машины с помощью пароля из хранилища ключей](azure-stack-kv-deploy-vm-with-secret.md)

[Развертывание виртуальной Машины с помощью хранилища ключей сертификата](azure-stack-kv-push-secret-into-vm.md)

