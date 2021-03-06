# Export SQL Script

Exports the schema for a Microsoft SQL Server database to one or more SQL files.

# Command Line Usage

ExportSqlScript.Console.exe "Server" "Database" [Object] [[Options](#Options)]

## Examples

##### Output the schema to the console

>ExportSqlScript.Console.exe .\sqlexpress AdventureWorks

##### Save the schema to a single file

>ExportSqlScript.Console.exe .\sqlexpress AdventureWorks /ot:SingleFile

*The file will be generated in the current directory with the name AdventureWorks.sql*

##### Save the schema to individual files by type

>ExportSqlScript.Console.exe .\sqlexpress AdventureWorks /ot:Files /of:CreationOrder.txt /od:"sql"

##### Save the schema to individual files by type and in a hierarchy of directories by object type

>ExportSqlScript.Console.exe .\sqlexpress AdventureWorks /ot:Tree /of:CreationOrder.txt /od:"sql"

## Options

| Parameter             | Description         |  Required | Values                     | Default Value |
|-----------------------|---------------------|-----------|-----------------|---------------|
| Server                | The server address. | **True** | | |
| Database              | The name of the database. | **True** | | |
| [Object]              | The name of the object to generate. If this parameter isn't specified, then all objects are included by default. | False | | |
| /ot:"OutputType"      | The type of output to generate. | False | None \| SingleFile \| Files \| Tree | None |
| /of:"OrderFile"       | The name of the file generated in the output directory which lists the SQL files in the appropriate order needed to satisfy any dependencies when re-creating the database. | False | | fileOrder.txt |
| /od:"OutputDirectory" | The output directory where the SQL files will be generated. | False | | The current directory |
| /xt:"ExcludeTypes"    | A list of types to exclude separated by a comma. | False | *See [Object Types](#Object-Types)* | |
| /U:"UserName"         | The user name to connect to the database. | False | | |
| /P:"UserPassword"     | The password to connect to the database. | False | | |

| Flag  | Description                    |
|-------|--------------------------------|
| /sdb  | Script database                |
| /sc   | Script collation               |
| /sfg  | Script file group              |
| /ssq  | Script schema qualify          |
| /sep  | Script extended properties     |
| /sfks | Script foreign keys separately |

## Object Types

| Type | Description |
|-------|--------------------------------|
| All | All objects |
| ApplicationRole | Application Role |
| AsymmetricKey | Asymmetric Key |
| Certificate | Certificate |
| DatabaseAuditSpecification | Database Audit Specification |
| DatabaseEncryptionKey | Database Encryption Key |
| DatabaseRole | Database Role |
| Default | Default |
| ExtendedStoredProcedure | Extended Stored Procedure |
| FullTextCatalog | Full Text Catalog |
| FullTextStopList | Full Text Stop List |
| MessageType | Message Type |
| PartitionFunction | Partition Function |
| PartitionScheme | Partition Scheme |
| PlanGuide | Plan Guide |
| RemoteServiceBinding | Remote Service Binding |
| Rule | Rule |
| Schema | Schema |
| ServiceBroker | Service Broker |
| ServiceContract | Service Contract |
| ServiceQueue | Service Queue |
| ServiceRoute | Service Route |
| SqlAssembly | SQL Assembly|
| StoredProcedure | Stored Procedure |
| SymmetricKey | Symmetric Key |
| Synonym | Synonym |
| Table | Table |
| User | User |
| UserDefinedAggregate | User Defined Aggregate |
| UserDefinedDataType | User Defined Data Type |
| UserDefinedFunction | User Defined Function |
| UserDefinedTableTypes | User Defined Table Types |
| UserDefinedType | User Defined Type |
| View | View |
| XmlSchemaCollection | XML Schema Collection |

# Re-create the database

1. Create the database

>sqlcmd -E -S .\sqlexpress -Q "CREATE DATABASE AdventureWorks2"

2. Execute the SQL files

*When multiple files were generating:*
>for /F "" %i in (CreationOrder.txt) do sqlcmd -E -S .\sqlexpress -d AdventureWorks2 -f 65001 -i %i

*When a single file was generated:*
>sqlcmd -E -S .\sqlexpress -d AdventureWorks2 -f 65001 -i AdventureWorks2.sql

# Compatibility

- SQL Server 2000
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017

# Requirements

[Microsoft® SQL Server® 2008 R2 Shared Management Objects](http://www.microsoft.com/downloads/en/details.aspx?displaylang=en&FamilyID=ceb4346f-657f-4d28-83f5-aae0c5c83d52)

# Credits

[Ivan Hamilton](http://ivan.blogs.chimerical.com.au) for the original source code from [codeplex](https://archive.codeplex.com/?p=exportsqlscript).