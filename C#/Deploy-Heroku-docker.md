# Deploy to Heroku

---

Table of contents

1. [Useful Docker Commands](#Useful-Docker-Commands)

2. [Before you get started](#Before-you-get-started)

3. [Change your Database](#Change-your-Database)

4. These notes were based on [this Article](https://medium.com/faun/deploy-dotnet-core-api-docker-container-with-mysql-on-heroku-ed387eab4222)

   - This artical's instructions did not work correctly. So I sourced other info from a few sources. 
   - These notes are based on all of my research. 

   

---

#### Useful Docker Commands

list all running dockers

```shell
docker ps
```

list all docker images

```shell
docker images
```

Stop a docker from running

```shell
docker stop $(docker ps -a -q) 
```

Remove a docker image

```shell
docker rm $(docker ps -a -q)
```



## Before you get started 

Go to [Heroic.com](https://www.heroku.com/) and create an account and 'Create New App' by click on the 'New' button in the top right. 

1. Create production build

   ```shell
   dotnet publish -c release -o app/ .
   ```

2. Create a Dockerfile
   [Microsoft Docs](https://docs.docker.com/engine/examples/dotnetcore/)

   **remember to change project file name on the last line**

   file name = **dockerfile**

   ```shell
   FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
   WORKDIR /app
   
   # Copy csproj and restore as distinct layers
   COPY *.csproj ./
   RUN dotnet restore
   
   # Copy everything else and build
   COPY . ./
   RUN dotnet publish -c Release -o out
   
   # Build runtime image
   FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
   WORKDIR /app
   COPY --from=build-env /app/out .
   CMD ASPNETCORE_URLS=http://*:$PORT dotnet <TreasureSweepGame.dll> // <----- change out app name 
   
   ```

3. Create Docker Ignore

   file name = **.dockerignore**

   ```shell
   bin\
   obj\
   ```

4. Build a docker container

   Make sure you have [docker installed](https://www.docker.com/products/docker-desktop)

   Replace <appname> with your app

   ```shell
   docker build -t <aspnetapp> .
   ```

5. Run the docker 

   Check to see if the docker built Correctly by running the image you just made.

   If the container is running would hould be able to go to **localhost:8080** and see your site

   ```shell
    docker run -d -p 8080:80 --name <containername> <aspnetapp>
   ```

6. Login to Heroku

   This should pop up a sight and direct you to login with Heroku. 

   ```shell
   heroku login
   ```

7. Login to Heroku Container

   ```shell
   heroku container:login
   ```

8. Create a Heroku Target
   This command will create a Target Image tag for source image.

   ```shell
   docker tag <YourProjectImageName> registry.heroku.com/<YourHerokuAppName>/web
   ```

9. Push Registry

   ```shell
   docker push registry.heroku.com/<YourHerokuAppName>/web
   ```

10. Release the container

    ```shell
    heroku container:release web -a <YourHerokuAppName>
    ```

    

## Change your Database

---

The best database to use with Heroku is Heroku Postgress. The following are instructions on how to change out your projects database.

### Posgress

1. *Update database link in Appsettings.json*

   - *Find the     details needed in heroku app, click on postgres in your add-ons*

   - *Click on     settings, view Credentials*

   - change the DefaultConnect settings to the heroku postrgress database details

     ```shell
     "ConnectionStrings": {
     "DefaultConnection": "Server=[host];Port=[5432];database=[database name];uid=[user];pwd=[password];"
     },
     
     ```

2. Add postgress to your .csproj file.

   ```shell
   <PackageReference Include="Npgsql.EntityFrameworkCore.PostgreSQL" Version="2.2.0" />
   ```

   

3. Update Startup.cs

   Add this using statement 

   ```shell
   using System.Reflection;
   ```

   ```shell
   public void ConfigureServices(IServiceCollection services)
       {
         services.Configure<CookiePolicyOptions>(options =>
         {
           options.CheckConsentNeeded = context => true;
           options.MinimumSameSitePolicy = SameSiteMode.None;
         });
   
         // const string connectionString = @"Data Source=treasuresweep.db";
         var migrationsAssembly = typeof(Startup).GetTypeInfo().Assembly.GetName().Name;
   
         services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
   
         services.AddDbContext<TreasureSweepGameContext>(builder =>
                   builder.UseSqlite(Configuration["ConnectionStrings:DefaultConnection"], sqlOptions => sqlOptions.MigrationsAssembly(migrationsAssembly)));
   
         services.AddDefaultIdentity<ApplicationUser>()
                         .AddRoles<IdentityRole>()
                         .AddEntityFrameworkStores<TreasureSweepGameContext>();
   ```

4. Check database migrations at there

    I think this update should check if your project has a migration to the database.

   in your porject.js file add this.

   ```shell
   using System;
   using System.Collections.Generic;
   using System.IO;
   using System.Linq;
   using System.Threading.Tasks;
   using Microsoft.AspNetCore;
   using Microsoft.AspNetCore.Hosting;
   using Microsoft.Extensions.Configuration;
   using Microsoft.Extensions.Logging;
   using TreasureSweepGame.Models;
   using Microsoft.EntityFrameworkCore;
   using Microsoft.Extensions.DependencyInjection;
   
   
   namespace TreasureSweepGame
   {
     public class Program
     {
       public static void Main(string[] args)
       {
         var host = CreateWebHostBuilder(args).Build();
         using (var scope = host.Services.CreateScope())
         {
           var services = scope.ServiceProvider;
           try
   
           {
             var context = services.GetRequiredService<TreasureSweepGameContext>();
             context.Database.Migrate();
   
           }
           catch (Exception ex)
           {
             var logger = services.GetRequiredService<ILogger<Program>>();
             logger.LogError(ex, "An error occured during migration");
           }
         }
   
   
         host.Run();
       }
   
       public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
           WebHost.CreateDefaultBuilder(args)
               .UseStartup<Startup>();
     }
   }
   ```

   9. Delete all migration files

      Now that you have wired up a new database you will want to delete your old migration files. 

      Then Rerun your ef migration command

      ```shell
      dotnet ef migrations add AddPostgress
      ```

      ```shell
      dotnet ef  database update
      ```

      