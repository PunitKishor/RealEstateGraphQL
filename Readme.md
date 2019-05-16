## **Tutorial Videos**

https://www.youtube.com/watch?v=M0L2aqVOPnM&list=PLBMCyCQ4nalaWRYBDKrIOHkFK1Y5AxbrK

## **Follow these steps to run with docker and visual studio for mac**

### **Prerequisites**
1. Install Docker
2. Install Visual Studio for mac
3. Install Dotnet Core 2.2
4. Install Azure Data Studio

### **Steps**

1. Pull latest sql server docker image
    ```
    docker pull mcr.microsoft.com/mssql/server:2017-latest-ubuntu
    ```
    https://hub.docker.com/_/microsoft-mssql-server

2. Run SQl Server Express in docker

    ```
    docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=yourStrong(!)Password' -e 'MSSQL_PID=Express' -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest-ubuntu 
    ```

3. Connect Azure Data Studio to SQL server 

    * Server: localhost
    * Authentication Type: Sql Server
    * User Name: sa
    * Password: yourStrong(!)Password
    
4. Run this script to create DB and Table

    ```
    CREATE DATABASE myDataBase
    GO

    USE myDataBase
    GO

    CREATE TABLE Properties (
        Id INT IDENTITY(1,1) PRIMARY KEY,
        Name VARCHAR(200),
        City VARCHAR(200),
        Street VARCHAR(200),
        Value MONEY,
        Family VARCHAR(200)
    )
    GO
    CREATE TABLE Payments (
        Id INT IDENTITY(1,1) PRIMARY KEY,
        Value MONEY,
        DateCreated DATETIME,
        DateOverdue DATETIME,
        Paid BIT,
        PropertyId INT REFERENCES Properties(Id),
    )
    ```
5. Replace value of **RealEstateDb** with below value in **RealEstateAPI\appsettings.json**
    ```
     "Server=localhost;Database=myDataBase;User Id=sa;Password=yourStrong(!)Password;"
    ```