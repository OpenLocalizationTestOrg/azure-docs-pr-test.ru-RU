## <a name="next-steps"></a><span data-ttu-id="4681e-101">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4681e-101">Next steps</span></span>

<span data-ttu-id="4681e-102">После включения интеграции хранилища ключей Azure вы сможете включить шифрование SQL Server на своей виртуальной машине с SQL.</span><span class="sxs-lookup"><span data-stu-id="4681e-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="4681e-103">Во-первых, необходимо создать асимметричный ключ в вашем хранилище ключей и симметричный ключ в SQL Server на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4681e-103">First, you will need to create an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="4681e-104">После этого вы сможете выполнять инструкции T-SQL для включения шифрования базы данных и резервных копий.</span><span class="sxs-lookup"><span data-stu-id="4681e-104">Then, you will be able to execute T-SQL statements to enable encryption for your databases and backups.</span></span>

<span data-ttu-id="4681e-105">Существует несколько способов шифрования, преимуществами которых вы можете воспользоваться.</span><span class="sxs-lookup"><span data-stu-id="4681e-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="4681e-106">Прозрачное шифрование данных (TDE)</span><span class="sxs-lookup"><span data-stu-id="4681e-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="4681e-107">Зашифрованные резервные копии</span><span class="sxs-lookup"><span data-stu-id="4681e-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="4681e-108">Шифрование на уровне столбцов (CLE)</span><span class="sxs-lookup"><span data-stu-id="4681e-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="4681e-109">Следующие сценарии Transact-SQL содержат примеры для каждого из этих вариантов.</span><span class="sxs-lookup"><span data-stu-id="4681e-109">The following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="4681e-110">Предварительные требования для примеров</span><span class="sxs-lookup"><span data-stu-id="4681e-110">Prerequisites for examples</span></span>

<span data-ttu-id="4681e-111">Каждый пример основан на двух компонентах: асимметричном ключе из хранилища ключей **CONTOSO_KEY** и учетных данных, созданных интеграцией AKV, с именем **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="4681e-111">Each example is based on the two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by the AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="4681e-112">Следующие команды Transact-SQL настраивают эти предварительные требования для запуска примеров.</span><span class="sxs-lookup"><span data-stu-id="4681e-112">The following Transact-SQL commands setup these prerequisites for running the examples.</span></span>

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="4681e-113">Прозрачное шифрование данных (TDE)</span><span class="sxs-lookup"><span data-stu-id="4681e-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="4681e-114">Создайте имя входа SQL Server для использования компонентом Database Engine для прозрачного шифрования данных, а затем добавьте учетные данные.</span><span class="sxs-lookup"><span data-stu-id="4681e-114">Create a SQL Server login to be used by the Database Engine for TDE, then add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the TDE Login to add the credential for use by the
   -- Database Engine to access the key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="4681e-115">Создайте ключ шифрования базы данных, который будет использоваться для прозрачного шифрования данных.</span><span class="sxs-lookup"><span data-stu-id="4681e-115">Create the database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the database to enable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="4681e-116">Зашифрованные резервные копии</span><span class="sxs-lookup"><span data-stu-id="4681e-116">Encrypted backups</span></span>

1. <span data-ttu-id="4681e-117">Создайте имя входа SQL Server для использования компонентом Database Engine для шифрования резервных копий, а затем добавьте учетные данные.</span><span class="sxs-lookup"><span data-stu-id="4681e-117">Create a SQL Server login to be used by the Database Engine for encrypting backups, and add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it is encrypting the backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the Encrypted Backup Login to add the credential for use by
   -- the Database Engine to access the key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="4681e-118">Выполните резервное копирование базы данных, указав шифрование с помощью асимметричного ключа, хранящегося в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="4681e-118">Backup the database specifying encryption with the asymmetric key stored in the key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   TO DISK = N'[PATH TO BACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="4681e-119">Шифрование на уровне столбцов (CLE)</span><span class="sxs-lookup"><span data-stu-id="4681e-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="4681e-120">Этот скрипт создает симметричный ключ, защищенный асимметричным ключом в хранилище ключей, и затем использует симметричный ключ для шифрования данных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="4681e-120">This script creates a symmetric key protected by the asymmetric key in the key vault, and then uses the symmetric key to encrypt data in the database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open the symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close the symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="4681e-121">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4681e-121">Additional resources</span></span>

<span data-ttu-id="4681e-122">Дополнительные сведения об использовании этих возможностей шифрования см. в статье [Использование расширенного управления ключами с функциями шифрования SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="4681e-122">For more information on how to use these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="4681e-123">Обратите внимание, что действия, описанные в этой статье, предполагают, что у вас уже есть SQL Server на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="4681e-123">Note that the steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="4681e-124">Если нет, см. статью [Подготовка виртуальной машины с SQL Server в Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="4681e-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="4681e-125">Другие темы, связанные с запуском SQL Server на виртуальных машинах Azure, см. в статье [Общие сведения об SQL Server на виртуальных машинах Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4681e-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>