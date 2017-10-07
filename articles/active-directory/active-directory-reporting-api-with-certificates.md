---
title: "aaaGet данных с помощью hello Azure Reporting API AD с сертификатами | Документы Microsoft"
description: "Объясняет, как toouse hello Azure AD API Reporting с данными tooget учетные данные сертификата из каталогов без вмешательства пользователя."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a>Получение данных с помощью API отчетов hello Azure AD с помощью сертификатов
В этой статье рассматриваются как toouse hello Azure AD API Reporting с данными tooget учетные данные сертификата из каталогов без вмешательства пользователя. 

## <a name="use-hello-azure-ad-reporting-api"></a>Здравствуйте, используйте API отчетов Azure AD 
API отчетов Azure AD требует выполнения hello следующие шаги:
 *  установить необходимые компоненты;
 *  Задать сертификат hello в приложении
 *  Получение маркера доступа
 *  Использовать hello toocall токена доступа hello Graph API

Сведения об исходном коде см. в [практическом руководстве по использованию модуля API отчетов](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils). 

### <a name="install-prerequisites"></a>установить необходимые компоненты;
Необходимо будет toohave Azure AD PowerShell V2 и AzureADUtils модуль установлен.

1. Загрузите и установите Azure AD Powershell V2, следуя инструкциям hello в [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).
2. Загрузите модуль Azure AD Odatautils hello из [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1). 
  Этот модуль предоставляет несколько служебных командлетов, позволяющих получить:
   * Hello последнюю версию ADAL с помощью Nuget
   * маркеры доступа пользователя, ключи приложений и сертификаты с использованием ADAL;
   * обработку результатов с разбивкой на страницы с помощью API Graph.

**модуль Odatautils AD Azure hello tooinstall:**

1. Создать модуль программы hello toosave каталог (например, c:\azureAD) и загрузите hello модуля из GitHub.
2. Откройте сеанс PowerShell и перейдите в каталог toohello, который вы только что создали. 
3. Импорт модуля hello и установите его в путь к модулю hello PowerShell с помощью командлета Install AzureADUtilsModule hello. 

Hello сеанса должен выглядеть примерно toothis экрана.

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a>Задать сертификат hello в приложении
1. Если уже имеется приложение, получите его идентификатор объекта из hello портала Azure. 

  ![Портал Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. Откройте сеанс PowerShell и подключитесь tooAzure AD с помощью командлета Connect AzureAD hello.

  ![Портал Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. С помощью командлета New-AzureADApplicationCertificateCredential hello из AzureADUtils tooadd tooit учетные данные сертификата. 

>[!Note]
>Вам необходимы приложения hello tooprovide идентификатор объекта, которые собраны в более ранних версий, а также hello объекта сертификата (получить это с помощью hello Cert: диск).
>


  ![Портал Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a>Получение маркера доступа

tooget маркер доступа с помощью командлета Get-AzureADGraphAPIAccessTokenFromCert hello из AzureADUtils. 

>[!NOTE]
>Необходимо toouse hello идентификатор приложения, вместо hello идентификатор объекта, который использовался в последний раздел hello.
>

 ![Портал Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a>Использовать hello toocall токена доступа hello Graph API

Теперь можно создать сценарий hello. Ниже приведен пример использования командлета Invoke-AzureADGraphAPIQuery hello из hello AzureADUtils. Этот командлет обрабатывает результаты нескольких страниц, а затем отправляет эти конвейер PowerShell toohello результаты. 

 ![Портал Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

Теперь вы готовы tooexport tooa CSV и сохранить tooa системы SIEM. Также можно включить сценарий в назначенное задание tooget данных Azure AD из вашего клиента периодически без необходимости toostore приложения ключей в исходном коде hello. 

## <a name="next-steps"></a>Дальнейшие действия
[Основные принципы управления удостоверениями Azure Hello](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



