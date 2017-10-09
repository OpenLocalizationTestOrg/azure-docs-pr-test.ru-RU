Эмулятор хранилища Hello поддерживает фиксированной учетной записи и хорошо известных проверки подлинности с ключом для проверки подлинности Shared Key. Этой учетной записи и ключ, hello единственные Shared Key учетные данные для использования с эмулятором хранилища hello. К ним относятся:

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> Hello ключ проверки подлинности, поддерживаемых эмулятором хранилища hello предназначена только для тестирования функции hello кода проверки подлинности клиента. Его использование не гарантирует защиту. Нельзя использовать рабочую учетную запись хранилища и ключ с помощью эмулятора хранилища hello. Не следует использовать учетную запись hello разработки с рабочими данными.
> 
> Эмулятор хранилища Hello поддерживает только подключения по протоколу HTTP. Однако HTTPS — hello, рекомендуется использовать протокол для доступа к ресурсам в рабочей учетной записи хранилища Azure.
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a>Подключить эмулятор toohello учетную запись, с помощью ярлыка
Hello простым способом tooconnect toohello эмулятор хранилища из своего приложения — tooconfigure строку подключения в файле конфигурации приложения, ссылающийся на ярлык hello `UseDevelopmentStorage=true`. Ниже приведен пример эмулятора хранения toohello строку подключения в *app.config* файла: 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a>Подключиться с помощью hello хорошо известная учетная запись имени и ключа учетной записи эмулятора toohello
toocreate строку подключения, что ссылки hello эмулятор имя учетной записи и ключа, необходимо указать hello конечных точек для каждого из hello служб, которые следует toouse из эмулятора hello в строке подключения hello. Это необходимо, чтобы строка подключения hello будет ссылаться эмулятор hello конечных точек, которые отличаются от тех, для рабочую учетную запись хранилища. Например значение hello в строке подключения будет выглядеть следующим образом:

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

Это значение является показанный выше, контекстное идентичные toohello `UseDevelopmentStorage=true`.

#### <a name="specify-an-http-proxy"></a>Указание прокси-сервера HTTP
Можно также указать toouse прокси-сервер HTTP при тестировании службы со hello эмулятор хранилища. Это может быть полезна для отслеживания запросов и ответов HTTP, при отладке операций со службами хранилища hello. toospecify прокси-сервера, добавить hello `DevelopmentStorageProxyUri` toohello строку соединения и задайте его значение toohello URI прокси-сервера. Например вот строка подключения указывает toohello эмулятора хранилища и настраивает прокси-сервер HTTP.

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

