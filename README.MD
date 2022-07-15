# ASP.NET CORE SET UP INSTRUCTIONS
Replace {ProjName} with your project's name
## Create New Project
1. In terminal, navigate to where you want to place your project folder
2. In terminal, enter, `dotnet new mvc --no-https -o ProjName` **Don't forget to change _ProjName_**
3. In terminal, enter, `cd ProjName`
## Install Dependencies
1. In terminal, in your project folder, enter `dotnet add package Pomelo.EntityFrameworkCore.MySql --version 6.0.1`. This is an Entity Framework Core provider built on to of MySqlConnector that enables the use of the Entity Framework ORM with MySQL.
2. In terminal, in your project folder, enter `dotnet add package Microsoft.EntityFrameworkCore.Design --version 6.0.2` This will add an install EF Core into your project and can be seen as a line in your .csproj file.
3. In terminal, in your project folder, enter `code .`
4. If a box that says, "Required assets are missing" click, "Yes" ONLY if we are opening the actual project folder, NOT the parent folder.
## Update DB Name and Password (appsettings.json)
Copy and paste into the appsettings.json file. **Don't forget to change _YOUR-DB-NAME_**
```
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*",
  "DBInfo": {
    "Name": "MySqlConnect",
    "ConnectionString": "server=localhost;userid=root;password=YOUR_PASSWORD;port=3306;database=YOUR_DB_NAME;SslMode=None"
  }
}
```
## Create ProjectNameContext.cs model (ProjNameContext.cs)
Create a new file under the <sup>Models</sup> project directory.

Name it, <sup>ProjNameContext.cs</sup> (but replace ProjName with your projects's name. For example, if your project name was, "CatFeeder", name the file, <sup>CatFeederContext.cs<cs>)

This file will direct the ORM to connect each DB table to the correct model/class.

Once it's created, copy and paste the below
```
using Microsoft.EntityFrameworkCore;
 
namespace ProjName.Models
{
    public class ProjNameContext : DbContext
    {
        public ProjNameContext(DbContextOptions options) : base(options) { }
 
        // for every model / entity that is going to be part of the db
        // the names of these properties will be the names of the tables in the db
        // Example dbsets below
        // public DbSet<User> Users { get; set; }
 
        // public DbSet<Widget> Widgets { get; set; }
        // public DbSet<Item> Items { get; set; }
    }
}
```
- the `DbContextOptions` options come from <sup>Startup.cs</sup> which will come when we add our dependencies in a later step- aka _dependency injection_.
- `DbSet` is an **IEnumerable** of all rows in that DB table
- `base(options)` is calling the inherited base constructor from inherited `DbContext` and passing the `options` to the parent.