---
title: "aaaSigning смене ключей в Azure AD | Документы Microsoft"
description: "В этой статье описывается hello подписи смены ключей советы и рекомендации для Azure Active Directory"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a>Смена ключей подписывания Azure Active Directory
В этом разделе рассматриваются необходимые tooknow о hello открытые ключи, которые используются в токенах безопасности toosign Azure Active Directory (Azure AD). Это важные toonote, эти ключи меняются каждые периодически и в случае чрезвычайной ситуации удалось перезаписаны немедленно. Все приложения, которые используют Azure AD необходимо процесс смены ключей hello дескриптора может tooprogrammatically или определение процесса периодической смены вручную. Продолжить чтение toounderstand как ключи hello работают, как tooassess hello влияние приложения tooyour продолжения hello и как tooupdate приложения или установить периодической смены вручную смены ключей процесса toohandle при необходимости.

## <a name="overview-of-signing-keys-in-azure-ad"></a>Общие сведения о ключах подписывания в Azure AD
Azure AD использует шифрование с открытым ключом лежит отраслевых стандартов tooestablish доверия между собой и hello приложений, которые его используют. На практике это работает hello следующими способами: Azure AD использует ключ подписывания, состоящий из пары открытого и закрытого ключей. Когда пользователь входит в tooan приложение, использующее Azure AD для проверки подлинности, Azure AD создает маркер безопасности, содержащий сведения о пользователе hello. Этот маркер подписывается с помощью Azure AD, используя свой закрытый ключ, перед отправкой приложения toohello назад. tooverify, hello токен действителен и получен из Azure AD, hello приложение должно проверить подпись токена hello, с помощью hello открытого ключа, предоставленного Azure AD, который содержится в клиенте hello [OpenID Connect документ обнаружения](http://openid.net/specs/openid-connect-discovery-1_0.html) или SAML, WS-Fed [документа метаданных федерации](active-directory-federation-metadata.md).

В целях безопасности Azure AD подписывание ключей выполняется накат периодически и в случае чрезвычайной hello удалось следует развертывать по немедленно. Любое приложение, которое интегрируется с Azure AD должен быть подготовлен toohandle событие смены ключа независимо от того, насколько часто эта проблема может возникнуть. Если это не так, и ваше приложение попытается toouse hello tooverify с истекшим сроком действия ключа подписи в токене, hello вход запрос завершится ошибкой.

В документе discovery OpenID Connect hello и документа метаданных федерации hello доступен более чем один допустимый ключ. Приложение должно быть подготовлено toouse все ключи hello указывать в документе hello, так как один ключ может быть сменен раньше, другой может оказаться его заменой и т. д.

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a>Как tooassess Если повлияет на приложения и какие toodo о нем
Как приложение обрабатывает смены ключей зависит от переменных, например приложения или использовался какие протокол идентификации и библиотеки типа hello. в следующих разделах Hello оцениваться hello наиболее распространенных типов приложений затрагивает hello смены ключей, а также сведения о tooupdate автоматическую смену toosupport приложения hello, или вручную обновить ключ hello.

* [Собственные клиентские приложения, осуществляющие доступ к ресурсам](#nativeclient)
* [Веб-приложения и интерфейсы API, осуществляющие доступ к ресурсам](#webclient)
* [Защищающие ресурсы веб-приложения и интерфейсы API, созданные с помощью служб приложений Azure](#appservices)
* [Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации Microsoft Azure Active Directory, .NET OWIN OpenID Connect или WS-Fed](#owin)
* [Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации на основе токена носителя JWT или OpenID Connect .NET Core](#owincore)
* [Веб-приложения и интерфейсы API, защищающие ресурсы с помощью модуля Node.js passport-azure-ad](#passport)
* [Защищающие ресурсы веб-приложения и интерфейсы API, созданные в Visual Studio 2015 или Visual Studio 2017](#vs2015)
* [Защищающие ресурсы веб-приложения, созданные в Visual Studio 2013](#vs2013)
* [Защищающие ресурсы веб-интерфейсы, созданные в Visual Studio 2013](#vs2013_webapi)
* [Защищающие ресурсы веб-приложения, созданные в Visual Studio 2012](#vs2012)
* [Защищающие ресурсы веб-приложения, созданные с помощью Visual Studio 2008, 2010 или Windows Identity Foundation](#vs2010)
* [Веб-приложений и защите ресурсов API-интерфейсов с помощью любого другие библиотеки или вручную реализации любого из hello поддерживаются протоколы](#other)

Это руководство **не** применимо к:

* Приложения, добавленные из коллекции Azure AD приложения (включая пользовательские) имеют отдельные инструкции с ключами toosigning отношении. [Дополнительные сведения](../active-directory-sso-certs.md).
* Локальных приложений, опубликованных через прокси-сервер приложения нет tooworry о ключей подписывания.

### <a name="nativeclient"></a>Собственные клиентские приложения, осуществляющие доступ к ресурсам
Как правило, приложения, только осуществляющие доступ к ресурсам Microsoft Graph, KeyVault, API-Интерфейс Outlook и другие API-интерфейсы Microsoft) обычно только получение токена и передать его дальше toohello владельца ресурса. Учитывая, что они не используются для защиты всех ресурсов, они не проверять токен hello и не требуется tooensure, которые он подписан должным образом.

Собственные клиентские приложения, ли настольных компьютеров или мобильных устройств, попадают в эту категорию и таким образом не затронуты hello продолжения.

### <a name="webclient"></a>Веб-приложения и интерфейсы API, осуществляющие доступ к ресурсам
Как правило, приложения, только осуществляющие доступ к ресурсам Microsoft Graph, KeyVault, API-Интерфейс Outlook и другие API-интерфейсы Microsoft) обычно только получение токена и передать его дальше toohello владельца ресурса. Учитывая, что они не используются для защиты всех ресурсов, они не проверять токен hello и не требуется tooensure, которые он подписан должным образом.

Веб-приложений и веб-API, в которых используется только для приложений потока hello (учетные данные клиента и сертификат клиента), попадают в эту категорию и, таким образом не подвержены hello продолжения.

### <a name="appservices"></a>Защищающие ресурсы веб-приложения и интерфейсы API, созданные с помощью служб приложений Azure
Проверка подлинности Azure службы приложений и функциональные возможности авторизации (EasyAuth) уже имеет смены ключей toohandle необходимую логику hello автоматически.

### <a name="owin"></a>Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации Microsoft Azure Active Directory, .NET OWIN OpenID Connect или WS-Fed
Если приложение использует hello .NET OWIN OpenID Connect, WS-Fed или WindowsAzureActiveDirectoryBearerAuthentication по промежуточного слоя, он уже имеется смены ключей toohandle необходимую логику hello автоматически.

Убедитесь, что приложение использует любой из этих ищет все следующие фрагменты кода в файле Startup.cs или Startup.Auth.cs приложения hello

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a>Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации на основе токена носителя JWT или OpenID Connect.NET Core
Если приложение использует .NET Core OWIN OpenID Connect hello или JwtBearerAuthentication по промежуточного слоя, он уже имеется смены ключей toohandle необходимую логику hello автоматически.

Убедитесь, что приложение использует любой из этих ищет все следующие фрагменты кода в файле Startup.cs или Startup.Auth.cs приложения hello

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a>Веб-приложения и интерфейсы API, защищающие ресурсы с помощью модуля Node.js passport-azure-ad
Если приложение использует модуль passport ad Node.js hello, он уже имеется смены ключей toohandle необходимую логику hello автоматически.

Вы можете убедитесь, что приложение passport рекламы, выполняя поиск следующий фрагмент кода в файле app.js приложения hello

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a>Защищающие ресурсы веб-приложения и интерфейсы API, созданные в Visual Studio 2015 или Visual Studio 2017
Если приложение создано с помощью шаблона веб-приложения в Visual Studio 2015 или Visual Studio 2017 г. и выбрано **рабочих и учебных учетных записей** из hello **изменить аутентификацию** меню, он уже автоматически имеет смены ключей toohandle необходимую логику hello. Эта логика, внедренных в hello OWIN OpenID Connect по промежуточного слоя, получает и кэширует hello ключи из документа обнаружения OpenID Connect hello и периодически обновляет их.

Если вручную добавлен решение tooyour проверки подлинности, приложение может не иметь hello необходимая логика смены ключей. Вам потребуется toowrite его самостоятельно, либо hello выполните шаги в [веб-приложений и протоколы, поддерживаемые интерфейсы API используются любые другие библиотеки или вручную реализации любого из hello.](#other).

### <a name="vs2013"></a>Защищающие ресурсы веб-приложения, созданные в Visual Studio 2013
Если приложение создано с помощью шаблона веб-приложения в Visual Studio 2013 и вы выбрали **учетные записи организации** из hello **изменить проверку подлинности** меню, оно уже имеет необходимости hello Логика toohandle ключа продолжения автоматически. Логика хранит уникальный идентификатор вашей организации и подписи ключевые данные в двух таблицах базы данных, связанные с проектом hello hello. Hello строку подключения для базы данных hello можно найти в файле Web.config проекта hello.

Если вручную добавлен решение tooyour проверки подлинности, приложение может не иметь hello необходимая логика смены ключей. Вам потребуется toowrite его самостоятельно, либо hello выполните шаги в [веб-приложений и протоколы, поддерживаемые интерфейсы API используются любые другие библиотеки или вручную реализации любого из hello.](#other).

Hello следующие шаги помогут проверить правильность работы логики hello в приложении.

1. В Visual Studio 2013 откройте решение hello и щелкните hello **обозревателя серверов** вкладку в правом окне приветствия.
2. Разверните узлы **Подключения данных**, **DefaultConnection**, а затем — **Таблицы**. Найдите hello **IssuingAuthorityKeys** , щелкните его правой кнопкой мыши, а затем выберите пункт **Показать таблицу данных**.
3. В hello **IssuingAuthorityKeys** таблицы, будут существовать по крайней мере одна строка, соответствующая toohello отпечатка для ключа hello. Удаляет все строки в таблице hello.
4. Щелкните правой кнопкой мыши hello **клиентов** , а затем выберите пункт **Показать таблицу данных**.
5. В hello **клиентов** таблицы, будут существовать по крайней мере одна строка, соответствующая tooa уникальному идентификатору клиента каталога. Удаляет все строки в таблице hello. Если вы не удалите hello строк в обоих hello **клиентов** таблицы и **IssuingAuthorityKeys** таблицы, вы получите ошибку во время выполнения.
6. Постройте и запустите приложение hello. После входа в учетную запись tooyour, можно остановить приложение hello.
7. Вернуть toohello **обозревателя серверов** и просмотрите значения hello в hello **IssuingAuthorityKeys** и **клиентов** таблицы. Вы заметите, что они были автоматически повторно с hello нужные сведения из документа метаданных федерации hello.

### <a name="vs2013"></a>Защищающие ресурсы веб-интерфейсы, созданные в Visual Studio 2013
Если создать веб-API в Visual Studio 2013 с помощью шаблона веб-API hello и последующего выбора **учетные записи организации** из hello **изменить аутентификацию** меню, вы уже имеют hello необходимую логику в приложение.

Если вы настроили проверку подлинности вручную, следуйте инструкциям hello ниже toolearn как tooconfigure вашего веб-API tooautomatically обновить сведения о его.

Hello следующий фрагмент кода демонстрирует способ tooget hello последние ключи из документа метаданных федерации hello, а затем использовать hello [обработчик токенов JWT](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello маркер. фрагмент кода Hello предполагается, что необходимо использовать собственный механизм для сохранения будущих toovalidate ключа hello кэширования токены из Azure AD ли в базе данных, файл конфигурации или в другом месте.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a>Защищающие ресурсы веб-приложения, созданные в Visual Studio 2012
Если приложение создано в Visual Studio 2012, вы вероятно использовали hello удостоверений и средства доступа к tooconfigure приложения. Вероятно, что вы используете hello [проверки издателя имя реестра (VINR)](https://msdn.microsoft.com/library/dn205067.aspx). Hello VINR отвечает за поддержание сведений о доверенных поставщиках удостоверений (Azure AD) и использования выданных ими токенов toovalidate hello ключей. Hello VINR также упрощает легко tooautomatically hello ключевые сведения об обновлении хранятся в файле Web.config, загрузив hello последнего документа метаданных федерации связанной с вашим каталогом, проверки конфигурации hello устарела с hello последняя версия документ и обновить hello приложения toouse hello новый ключ при необходимости.

Если вы создали приложение с помощью любого из примеров кода hello или пошаговой документации, предоставляемой корпорацией Майкрософт, логика смены ключей hello уже включены в проект. Обратите внимание, что приведенный ниже код hello уже существует в проекте. Если приложение не имеет этой логики, действуйте hello ниже tooadd его и tooverify, в которой он работает правильно.

1. В **обозревателе решений**, добавьте toohello ссылки **System.IdentityModel** сборки для hello соответствующий проект.
2. Откройте hello **Global.asax.cs** файл и добавьте следующее hello директивы using:
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. Добавьте следующий метод toohello hello **Global.asax.cs** файла:
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. Вызвать hello **RefreshValidationSettings()** метод в hello **Application_Start()** метод в **Global.asax.cs** следующим:
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

После выполнения этих действий файл Web.config приложения будет обновляться с последними сведениями hello из документа метаданных федерации hello, включая последние ключи hello. Это обновление будет выполняться каждый раз при перезапуске пула приложений в IIS; по умолчанию службы IIS установлен toorecycle приложения каждые 29 часов.

Выполните действия hello ниже tooverify работы логики смены ключей hello.

1. После проверки ваше приложение использует кода hello выше, откройте hello **Web.config** файл и перейдите toohello  **<issuerNameRegistry>**  блок специально hello следующие несколько строк:
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. В hello  **<add thumbprint=””>**  измените значение отпечатка hello, заменив любой символ на другой. Сохранить hello **Web.config** файла.
3. Создание приложения hello и запустите его. Если вы можете завершить процесс входа hello, приложение успешно обновляет ключ hello, загрузив hello необходимые сведения из документа метаданных федерации вашего каталога. Если возникли проблемы со входом, обеспечивают hello изменений в приложении правильный, считывая hello [Добавление входа tooYour Web приложения с помощью Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) разделе, или загрузка и проверка hello следующий образец кода: [ Многопользовательского облачного приложения для Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).

### <a name="vs2010"></a>Защищающие ресурсы веб-приложения, созданные с помощью Visual Studio 2008 или 2010 и Windows Identity Foundation v1.0 для .NET 3.5
При построении приложения на платформе WIF 1.0 нет tooautomatically не предоставленного механизм обновления конфигурации приложения toouse новый ключ.

* *Наиболее простым способом* использовать hello fedutil, включенное в hello WIF SDK, который можно получить hello последнего документа метаданных и обновить конфигурацию.
* Обновление вашего приложения too.NET 4.5, включая hello новейшую версию WIF, расположенных в пространстве имен System hello. Затем можно использовать hello [проверки издателя имя реестра (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform автоматические обновления конфигурации приложения hello.
* Выполните вручную продолжения согласно инструкциям, приведенным hello в конце hello в этом документе рекомендации.

Инструкции toouse hello FedUtil tooupdate конфигурации:

1. Убедитесь, что hello WIF 1.0 SDK, установленный на компьютере разработки для Visual Studio 2008 или 2010. Если этот пакет не установлен, его можно [скачать отсюда](https://www.microsoft.com/en-us/download/details.aspx?id=4451).
2. В Visual Studio откройте решение hello, а затем щелкните правой кнопкой мыши соответствующий проект hello и выберите **обновление метаданных федерации**. Если этот параметр недоступен, FedUtil и (или) hello WIF 1.0 SDK не установлен.
3. В строке приветствия выберите **обновление** toobegin обновление метаданных федерации. При наличии доступа к toohello серверной среде, где размещается приложение hello, при необходимости можно использовать в FedUtil [планировщик метаданных автоматического обновления](https://msdn.microsoft.com/library/ee517272.aspx).
4. Нажмите кнопку **Готово** процесс обновления toocomplete hello.

### <a name="other"></a>Веб-приложений и защите ресурсов API-интерфейсов с помощью любого другие библиотеки или вручную реализации любого из hello поддерживаются протоколы
Если вы используете другой библиотеки или вручную реализовать один из поддерживаемых hello протоколов, вам потребуется tooreview hello библиотеки или вашей tooensure реализацию, hello ключ извлекается из документа обнаружения OpenID Connect hello или hello документ метаданных федерации. Одним из способов toocheck для этого является toodo поиск в коде или в код библиотеки hello все вызовы tooeither hello OpenID обнаружения документа или документа метаданных федерации hello.

Если ключ хранятся в другом или жестко задано в приложении, можно вручную извлечь ключ hello и его соответствующим образом выполнять вручную продолжения согласно инструкциям, приведенным hello в конце hello в этом документе инструкции update. **Настоятельно рекомендуется усилить автоматическую смену toosupport приложения** с помощью любого hello приближается структуры в этой статье tooavoid будущих перебои и служебных данных, если Azure AD увеличивает периодичности переключения или аварийный продолжения по каналу.

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a>Как tootest toodetermine вашего приложения, если будут затронуты
Вы можете проверить, является ли ваше приложение поддерживает автоматическую смену ключей, загрузив hello сценариев и следуйте инструкциям hello в [этот репозиторий GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a>Как tooperform вручную продолжения, если после этого приложение не поддерживает автоматическую смену
Если приложение **не** поддерживает автоматическую смену, вы должны будете tooestablish процесс, который периодически подписывающий мониторы Azure AD, ключи и выполняет вручную продолжения соответствующим образом. [Этот репозиторий GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) содержит сценарии и инструкции о том, как toodo это.

