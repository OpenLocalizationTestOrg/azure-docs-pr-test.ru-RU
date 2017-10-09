<span data-ttu-id="37394-101">Обладая адреса (SAS) URL-адрес, имеющей доступ tooresources в учетной записи хранения, можно использовать hello SAS в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="37394-101">If you possess a shared access signature (SAS) URL that grants you access tooresources in a storage account, you can use hello SAS in a connection string.</span></span> <span data-ttu-id="37394-102">Поскольку hello SAS содержит необходимые tooauthenticate hello hello сведения запроса, строка подключения с SAS предоставляет протокола hello, конечная точка службы hello и hello необходимые учетные данные tooaccess hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="37394-102">Because hello SAS contains hello information required tooauthenticate hello request, a connection string with a SAS provides hello protocol, hello service endpoint, and hello necessary credentials tooaccess hello resource.</span></span>

<span data-ttu-id="37394-103">toocreate строку подключения, которая включает подпись общего доступа, укажите строку hello в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="37394-103">toocreate a connection string that includes a shared access signature, specify hello string in hello following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="37394-104">Каждая конечная точка службы является необязательным, несмотря на то, что hello строка соединения должна содержать по крайней мере один.</span><span class="sxs-lookup"><span data-stu-id="37394-104">Each service endpoint is optional, although hello connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="37394-105">По соображениям безопасности с SAS рекомендуется использовать протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="37394-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="37394-106">Если указываются в строке подключения в файле конфигурации SAS, может потребоваться tooencode специальные символы в URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="37394-106">If you are specifying a SAS in a connection string in a configuration file, you may need tooencode special characters in hello URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="37394-107">Пример SAS службы</span><span class="sxs-lookup"><span data-stu-id="37394-107">Service SAS example</span></span>
<span data-ttu-id="37394-108">Ниже приведен пример строки подключения, которая включает подписанный URL-адрес службы для хранилища BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="37394-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="37394-109">А Вот пример hello одинаковой строки соединения с кодирования специальных символов:</span><span class="sxs-lookup"><span data-stu-id="37394-109">And here's an example of hello same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="37394-110">Пример SAS учетной записи</span><span class="sxs-lookup"><span data-stu-id="37394-110">Account SAS example</span></span>
<span data-ttu-id="37394-111">Ниже приведен пример строки подключения, которая включает подписанный URL-адрес учетной записи для хранилища BLOB-объектов и файлового хранилища:</span><span class="sxs-lookup"><span data-stu-id="37394-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="37394-112">Обратите внимание, что указаны конечные точки для обеих служб.</span><span class="sxs-lookup"><span data-stu-id="37394-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="37394-113">А Вот пример hello одинаковой строки соединения с кодировкой URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="37394-113">And here's an example of hello same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

