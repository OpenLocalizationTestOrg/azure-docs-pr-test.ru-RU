Обладая адреса (SAS) URL-адрес, имеющей доступ tooresources в учетной записи хранения, можно использовать hello SAS в строке подключения. Поскольку hello SAS содержит необходимые tooauthenticate hello hello сведения запроса, строка подключения с SAS предоставляет протокола hello, конечная точка службы hello и hello необходимые учетные данные tooaccess hello ресурсов.

toocreate строку подключения, которая включает подпись общего доступа, укажите строку hello в hello следующий формат:

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

Каждая конечная точка службы является необязательным, несмотря на то, что hello строка соединения должна содержать по крайней мере один.

> [!NOTE]
> По соображениям безопасности с SAS рекомендуется использовать протокол HTTPS.
>
> Если указываются в строке подключения в файле конфигурации SAS, может потребоваться tooencode специальные символы в URL-адрес hello.
>
>

### <a name="service-sas-example"></a>Пример SAS службы
Ниже приведен пример строки подключения, которая включает подписанный URL-адрес службы для хранилища BLOB-объектов:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

А Вот пример hello одинаковой строки соединения с кодирования специальных символов:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a>Пример SAS учетной записи
Ниже приведен пример строки подключения, которая включает подписанный URL-адрес учетной записи для хранилища BLOB-объектов и файлового хранилища: Обратите внимание, что указаны конечные точки для обеих служб.

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

А Вот пример hello одинаковой строки соединения с кодировкой URL-адрес:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

