---
title: "aaaEnable удаленного рабочего стола в облачной службе Azure | Документы Microsoft"
description: "Как tooconfigure azure облачной службы подключения удаленного рабочего стола tooallow приложения"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Включение подключения к удаленному рабочему столу для роли в облачных службах Azure

> [!div class="op_single_selector"]
> * [Портал Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Классический портал Azure](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)

Можно включить удаленный рабочий стол в данной роли во время разработки, включая модули, удаленный рабочий стол hello в определении службы или вы можете tooenable удаленного рабочего стола через hello расширения удаленного рабочего стола. Hello рекомендуется расширение удаленного рабочего стола hello toouse как можно включить удаленный рабочий стол, даже после развертывания приложения hello без необходимости tooredeploy приложения.

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a>Настроить удаленный рабочий стол из hello классический портал Azure
Hello классический портал Azure использует подход hello расширения удаленного рабочего стола, поэтому можно включить удаленный рабочий стол, даже после развертывания приложения hello. Hello **Настройка** страницы для облачной службы можно tooenable удаленного рабочего стола, изменение hello локальную учетную запись администратора используется tooconnect toohello виртуальных машин, сертификат hello, используемые в проверке подлинности и задайте hello Дата окончания срока действия.

1. Нажмите кнопку **облачные службы**, щелкните имя hello hello облачной службы и нажмите кнопку **Настройка**.
2. Нажмите кнопку hello **удаленного** кнопку в нижней части hello.

    ![Удаленный доступ к облачным службам](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > Если включить удаленный рабочий стол и нажать кнопку «ОК» (флажок), все экземпляры роли будут перезапущены. tooprevent перезагрузки пароль hello hello сертификата используется tooencrypt должен устанавливаться на роли hello. tooprevent перезагрузки [отправка сертификата для облачной службы hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , а затем возвращают toothis диалогового окна.

3. В **ролей**, выберите роль hello tooupdate или выберите **все** для всех ролей.
4. Внесите любые hello следующие отличия.

   * Удаленный рабочий стол, выберите hello tooenable **включить удаленный рабочий стол** флажок. toodisable удаленного рабочего стола, hello, снимите флажок.
   * Создайте toouse учетной записи подключения удаленного рабочего стола toohello экземпляров роли.
   * Обновление пароля hello hello существующей учетной записи.
   * Выберите toouse отправленный сертификат для проверки подлинности (сертификат hello передачи с помощью **отправить** на hello **сертификаты** страницы) или создать новый сертификат.
   * Измените дату окончания срока действия hello hello настройки удаленного рабочего стола.

5. По завершении обновления настроек нажмите кнопку **OK** (флажок).

## <a name="remote-into-role-instances"></a>Удаленное подключение к экземплярам ролей
После включения удаленного рабочего стола с ролями hello можно удаленного в экземпляре роли через различные средства.

tooconnect tooa экземпляра роли из hello классического портала Azure:

1. Нажмите кнопку **экземпляров** tooopen hello **экземпляров** страницы.
2. Выберите экземпляр роли, где настроен удаленный рабочий стол.
3. Нажмите кнопку **Connect**и выполните инструкции tooopen hello hello-рабочего стола.
4. Нажмите кнопку **откройте** и затем **Connect** toostart hello подключения удаленного рабочего стола.

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a>Используйте Visual Studio tooremote в экземпляр роли
В обозревателе сервера Visual Studio выполните следующие действия:

1. Разверните hello **Azure** > **облачные службы** > **[имя облачной службы]** узла.
2. Разверните узел **Промежуточные** или **Рабочие**.
3. Разверните роль отдельных hello.
4. Щелкните правой кнопкой мыши один из экземпляров роли hello, щелкните **подключиться с помощью удаленного рабочего стола...** , а затем введите hello имя пользователя и пароль.

![Удаленный рабочий стол обозревателя сервера](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a>Использовать файл протокола удаленного рабочего СТОЛА hello tooget PowerShell
Можно использовать hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) tooretrieve hello командлет RDP-файл. Затем можно использовать hello RDP-файл с помощью удаленного рабочего стола tooaccess hello облачной службы.

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a>Программным образом Загрузите RDP-файл hello через hello API REST управления службами
Можно использовать hello [загрузить файл RDP](https://msdn.microsoft.com/library/jj157183.aspx) REST операции toodownload hello RDP-файл.

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a>tooconfigure удаленного рабочего стола в файле определения службы hello
Этот метод позволяет tooenable удаленного рабочего стола для приложения hello во время разработки. Этот подход требует зашифрованные пароли храниться в конфигурации службы файлов и любые обновления toohello конфигурацию удаленного рабочего стола потребуется повторное развертывание приложения hello. Если требуется, чтобы tooavoid этих недостатков, следует использовать hello удаленного рабочего стола расширения на основе подход, описанный выше.  

Можно также использовать Visual Studio[включить подключение удаленного рабочего стола](../vs-azure-tools-remote-desktop-roles.md) подход файла определения службы hello.  
Hello перечисленные ниже шаги описывают hello изменения toohello необходимые службы модели файлы tooenable удаленного рабочего стола. Visual Studio автоматически выполнит эти изменения при публикации.

### <a name="set-up-hello-connection-in-hello-service-model"></a>Настройка подключения hello в модели службы hello
Используйте hello **Imports** hello элемент tooimport **RemoteAccess** модуль и hello **RemoteForwarder** toohello модуль [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) файл.

Hello файла определения службы должен быть примерно toohello следующий пример с hello `<Imports>` добавлен элемент.

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
Hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) файла должен быть примерно toohello следующий пример, обратите внимание, hello `<ConfigurationSettings>` и `<Certificates>` элементы. Hello указанный сертификат должен быть [отправлен toohello облачной службы](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a>Дополнительные ресурсы
[Как облачные службы tooConfigure](cloud-services-how-to-configure.md)
[облачных служб часто задаваемые вопросы — удаленного рабочего стола](cloud-services-faq.md)
