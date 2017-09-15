<span data-ttu-id="970af-101">При наличии подписанного URL-адреса (SAS), предоставляющего доступ к ресурсам в учетной записи хранения, SAS можно использовать в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="970af-101">If you possess a shared access signature (SAS) URL that grants you access to resources in a storage account, you can use the SAS in a connection string.</span></span> <span data-ttu-id="970af-102">Так как SAS содержит сведения URI, необходимые для аутентификации запроса, строка подключения с SAS предоставляет протокол, конечную точку службы и учетные данные, необходимые для доступа к ресурсу.</span><span class="sxs-lookup"><span data-stu-id="970af-102">Because the SAS contains the information required to authenticate the request, a connection string with a SAS provides the protocol, the service endpoint, and the necessary credentials to access the resource.</span></span>

<span data-ttu-id="970af-103">Чтобы создать строку подключения, содержащую подписанный URL-адрес, задайте ее в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="970af-103">To create a connection string that includes a shared access signature, specify the string in the following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="970af-104">Несмотря на то что конечные точки службы необязательны, строка подключения должна содержать по крайней мере одну конечную точку.</span><span class="sxs-lookup"><span data-stu-id="970af-104">Each service endpoint is optional, although the connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="970af-105">По соображениям безопасности с SAS рекомендуется использовать протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="970af-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="970af-106">При указании SAS в строке подключения в файле конфигурации может потребоваться закодировать специальные символы в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="970af-106">If you are specifying a SAS in a connection string in a configuration file, you may need to encode special characters in the URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="970af-107">Пример SAS службы</span><span class="sxs-lookup"><span data-stu-id="970af-107">Service SAS example</span></span>
<span data-ttu-id="970af-108">Ниже приведен пример строки подключения, которая включает подписанный URL-адрес службы для хранилища BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="970af-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="970af-109">Еще один пример той же строки подключения с кодированием специальных символов:</span><span class="sxs-lookup"><span data-stu-id="970af-109">And here's an example of the same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="970af-110">Пример SAS учетной записи</span><span class="sxs-lookup"><span data-stu-id="970af-110">Account SAS example</span></span>
<span data-ttu-id="970af-111">Ниже приведен пример строки подключения, которая включает подписанный URL-адрес учетной записи для хранилища BLOB-объектов и файлового хранилища:</span><span class="sxs-lookup"><span data-stu-id="970af-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="970af-112">Обратите внимание, что указаны конечные точки для обеих служб.</span><span class="sxs-lookup"><span data-stu-id="970af-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="970af-113">Еще один пример той же строки подключения с кодированием URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="970af-113">And here's an example of the same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

