Resumen de pasos:
1. PASO 1: Crear la aplicación **ASP.NET Core Web App MVC**
2. PASO 2: Instalar los paquetes necesarios dentro del proyecto `tualquiler`
3. PASO 3: Configurar el contexto de la Base de Datos:

    3.1 Crear la clase para el DbContext `tualquilerDbContext.cs` en la carpeta Data en la raíz de tu proyecto

    3.2 Configurar el `ConnectionStrings`
        
        3.2.1 Agregar la cadena de conexión en `appsettings.Development.json`
        3.2.2 Deshabilitar la encriptación SSL en la cadena de conexión
        3.2.3 Registrar nuestro ApplicatonDbContext `TuAlquiler_DefaultConnection` como un Servicio

4. PASO 4: Crear nuestra primera tabla a partir de una Entidad

    4.1 Crear la clase para la Entidad `EjemploTable.cs` en la carpeta Entidades en la raíz de tu proyecto

    4.2 Creando una Migración

    4.3 Actualizando una Migración




# --------------------------------------------------------------------------------

# PASO 1: Crear la aplicación **ASP.NET Core Web App MVC**

dotnet new mvc -n CCS_Test_01

Puedes darme la línea de comando en Visual Studio Code para crear un proyecto ASP.NET Core Web App MVC, así como los paquetes que debo tener previamente instalados.

Para crear un proyecto de **ASP.NET Core Web App MVC** en **Visual Studio Code** desde la línea de comandos, debes seguir estos pasos. A continuación, te proporcionaré la línea de comando y los paquetes necesarios que debes tener instalados.

### 1. **Instalar los paquetes necesarios**

Antes de crear el proyecto, asegúrate de tener los siguientes paquetes instalados:

#### a. **.NET SDK**
El SDK de .NET Core es necesario para crear y ejecutar aplicaciones de .NET. Puedes descargarlo e instalarlo desde la página oficial de [.NET](https://dotnet.microsoft.com/download).

Para verificar si ya tienes el SDK instalado, puedes usar el siguiente comando:

```bash
dotnet --version
```

Si está instalado correctamente, te mostrará la versión del SDK.

#### b. **Visual Studio Code**
También necesitarás tener **Visual Studio Code** instalado. Si no lo tienes, puedes descargarlo desde su página oficial: [Visual Studio Code](https://code.visualstudio.com/).

#### c. **Extensiones de Visual Studio Code**
Es recomendable instalar las siguientes extensiones en Visual Studio Code:
- **C#**: para tener soporte completo para C#.
- **ASP.NET Core Snippets**: para autocompletar y facilitar el desarrollo en ASP.NET Core.

### 2. **Crear el Proyecto ASP.NET Core Web App MVC**

Una vez que tengas los requisitos previos listos, sigue estos pasos:

#### a. **Abrir una terminal**

Puedes abrir una terminal en Visual Studio Code usando la combinación de teclas `Ctrl + ` (la tecla justo debajo de `Esc`), o desde el menú `Ver > Terminal`.

#### b. **Crear el Proyecto**

Ejecuta el siguiente comando para crear un nuevo proyecto de tipo **Web App MVC** con ASP.NET Core:

```bash
dotnet new mvc -n NombreDeTuProyecto
```

- `mvc` especifica que el proyecto será una aplicación de tipo MVC (Model-View-Controller).
- `-n NombreDeTuProyecto` define el nombre del proyecto. Cambia `NombreDeTuProyecto` por el nombre que desees.

#### c. **Entrar en la carpeta del proyecto**

Una vez creado el proyecto, navega a la carpeta del proyecto usando el siguiente comando:

```bash
cd NombreDeTuProyecto
```

#### d. **Abrir el Proyecto en Visual Studio Code**

Una vez dentro de la carpeta de tu proyecto, puedes abrirlo en Visual Studio Code con el siguiente comando:

```bash
code .
```

### 3. **Ejecutar el Proyecto**

Para ejecutar el proyecto en la terminal, solo tienes que usar:

```bash
dotnet run
```

Esto iniciará el servidor web integrado de ASP.NET Core y podrás acceder a tu aplicación en `http://localhost:5000`. 

### 4. **Usar el comando `dotnet watch run` (opcional)**

Si deseas que tu aplicación se recargue automáticamente cada vez que realices cambios en el código fuente, puedes utilizar el comando `dotnet watch run`:

```bash
dotnet watch run
```

Este comando no solo ejecuta tu aplicación, sino que también activa el 🔥 Hot reload enabled. Es decir, el `Hot Reload` observa cambios en el código fuente y recarga el servidor automáticamente, lo cual es muy útil durante el desarrollo. Sin embargo, no abre el navegador automáticamente por sí mismo. Desde la terminal, puedes recargar y compilar (Reload and Build) tu proyecto pulsado "Ctrl + R": 💡 Press "Ctrl + R" to restart. Para cancelar la ejecución pulse "Ctrl + C" desde la terminal: 🛑 Shutdown requested. Press Ctrl+C again to force exit.

Si deseas que cuando se ejecute tu aplicación, lo haga usando el protocolo `https` en forma predeterminada, debemos ir al archivo `TuProyecto/Properties/launchSettings.json` y modificar la propiedad "applicationUrl" del perfil/profile "http" y agregar la URL https correspondiente, con el número del puerto, que la podemos tomar y copiar de la propiedad "applicationUrl" del perfil/profile "https": `https://localhost:7257` y separarla con punto y coma ";" sin las comillas dobles. El perfil/profile `http` final quedaría así:
```json
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "https://localhost:7257;http://localhost:5105",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
```

- **Si tu navegador no se abre automáticamente, debes cerrar y volver a abrir Visual Studio Code, recompilar tu proyecto usando dotnet build y ejecutarlo con dotnet watch run.**

### Resumen de los pasos en la terminal

1. **Verificar si tienes .NET SDK instalado**:
   ```bash
   dotnet --version
   ```

2. **Crear el proyecto**:
   ```bash
   dotnet new mvc -n NombreDeTuProyecto
   ```

3. **Entrar a la carpeta del proyecto**:
   ```bash
   cd NombreDeTuProyecto
   ```

4. **Abrir el proyecto en Visual Studio Code**:
   ```bash
   code .
   ```

5. **Ejecutar el proyecto**:
   ```bash
   dotnet run
   ```

Con estos pasos, habrás creado y ejecutado un proyecto **ASP.NET Core Web App MVC** en Visual Studio Code.



# PASO 2: Instalar los paquetes necesarios dentro del proyecto `tualquiler`

## Instalar los paquetes necesarios según tu versión de .NET SDK :
```bash
dotnet add package Microsoft.EntityFrameworkCore --version 7.*
dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 7.*
dotnet tool install --global dotnet-ef --version 7.*
dotnet add package Microsoft.EntityFrameworkCore.Tools --version 7.*
dotnet add package Microsoft.EntityFrameworkCore.Design --version 7.*
dotnet add package Microsoft.AspNetCore.Identity.EntityFrameworkCore --version 7.*
```

## Elegir el manejador de base de datos:

```bash
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 7.*

dotnet add package Microsoft.EntityFrameworkCore.Sqlite
dotnet add package Microsoft.EntityFrameworkCore.Sqlite --version 7.*

dotnet add package Microsoft.EntityFrameworkCore.PostgreSQL
dotnet add package Microsoft.EntityFrameworkCore.PostgreSQL --version 7.*
```

# PASO 3: Configurar el contexto de la Base de Datos:

## 3.1 **Crear la clase para el DbContext** `TualquilerDbContext.cs` en la carpeta Data en la raíz de tu proyecto

La primera letra del nombre de la clase debe estar en mayúsculas.

```csharp
using Microsoft.EntityFrameworkCore;

namespace tualquiler.Data
{
    public class TualquilerDbContext : DbContext
    {
        public TualquilerDbContext(DbContextOptions opciones) : base(opciones)
        {
            //
        }
    }
}
```

## 3.2  **Configurar el `ConnectionStrings`**

### 3.2.1.  **Agregar la cadena de conexión en `appsettings.Development.json`**

```json
{
  "ConnectionStrings": {
    "TuAlquiler_DefaultConnection": "Server=localhost;Database=tualquiler;User Id=netwebuser;Password=M%4b~*DzaA0Np7);TrustServerCertificate=true"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  }
}
```

### 3.2.2. **Deshabilitar la encriptación SSL en la cadena de conexión**:

Usar `TrustServerCertificate=true` en ambientes de desarrollo, es especialmente útil ya que no tendremos ningún tipo de problema de seguridad a la hora de conectarnos con nuetsra instancia de MSSQLSERVER. En Producción no es necesario . Si no necesitas encriptación SSL para la conexión, puedes deshabilitarla en la cadena de conexión. Para hacerlo, simplemente agrega el parámetro `TrustServerCertificate=true` en tu cadena de conexión en `appsettings.Development.json`.

### 3.2.3. **Registrar nuestro ApplicatonDbContext `TuAlquiler_DefaultConnection` como un Servicio**:

Ahora debemos pasar nuestro ConnectionStrings `TuAlquiler_DefaultConnection` a nuestro DbContext `TualquilerDbContext` a través del DbContextOptions. Para ello, vamos a la clase `Program.cs` para configurar nuestro DbContext como un servicio usando AddDbContext. En `Program.cs` vamos a agregar la siguiente línes en la sección comentada bajo el texto: "Add services to the container:"

```csharp
builder.Services.AddDbContext<TualquilerDbContext>(opciones => opciones.UseSqlServer("name=TuAlquiler_DefaultConnection"));
```

A medida que se escribe, hacemos clic en la tecla "Tab" y automáticamente se agregarán las siguinetes líneas en nuestro archivo `Program.cs`:

```csharp
using Microsoft.EntityFrameworkCore;
using tualquiler.Data;
```

# PASO 4: Crear nuestra primera tabla a partir de una Entidad

Una **Entidad** es una clase la cual se corresponde con una tabla de una Base de Datos. Es decir, una Entidad es la respresentación en CSharp de una tabla.

Vamos a crear una Entidad de ejemplo que se llama `EjemploTable` para ilustrar los pasos a seguir para la creación de una Entidad.

## 4.1 **Crear la clase para la Entidad** `EjemploTable.cs` en la carpeta Entidades en la raíz de tu proyecto

```csharp
namespace tualquiler.Entidades
{
    public class EjemploTable
    {
        public int Id { get; set;}
        public string Titulo { get; set; }
        public string Descripcion { get; set; }
        public int Orden { get; set; }
        public DateTime FechaCreacion { get; set; }
    }
}
```

Así como está, esta es una simple clase. Esta clase no es una Entidad. Se va a transformar en una Entidad, cuando la configuremos con EntityFrameworkCore para que represente una tabla en SQL SERVER. Para ello, vamos a ir a la pieza central de EntityFrameworkCore que es nuestro DbContext `TualquilerDbContext` y allí vamos a configurar la clase EjemploTable como una Entidad para indicar que se debe crear una tabla de tareas en la base de datos.

En el archivo `TualquilerDbContext` vamos a agregar una línea como esta con su respectivo namespace:

```csharp
using tualquiler.Entidades;
public DbSet<EjemploTable> TablasDeEjemplo { get; set; }
```

Utilizamos `DbSet<EjemploTable> TablasDeEjemplo` para indicar que deseamos crear una tabla a partir de la clase `EjemploTable` y el nombre de esa tabla será `TablasDeEjemplo`

De este modo, nuestro archivo `TualquilerDbContext` debería lucir así:

```csharp
using Microsoft.EntityFrameworkCore;
using tualquiler.Entidades;

namespace tualquiler.Data
{
    public class TualquilerDbContext : DbContext
    {
        public TualquilerDbContext(DbContextOptions opciones) : base(opciones)
        {
            //
        }
        public DbSet<EjemploTable> TablasDeEjemplo { get; set; }
    }
}
```

Ahora bien, ¿cómo hacemos ahora para crear nuestra base de datos y la tabla `TablasDeEjemplo` a partir de nuestra aplicación? Para ello, debemos hablar de las Migraciones.

## 4.2 **Creando una Migración**

Para poder crear nuestra base de datos y nuestras tablas a partir de código CSharp, vamos a utilizar las migraciones. Una **Migración** es una representación en código csharp de los cambios que van a ocurrir en nuestra base de datos. Pensemos en una migración como un paso intermedio entre el código de nuestra aplicación, y la implementación de dicho código a la base de datos. Este paso intermedio es fundamental, ya que nos permite ver exactamente, qué es lo que va a ocurrir con nuestra base de datos. Incluso si se quiere, podemos hacer cambios de lo que va a ocurrir dentro de la migración antes de migrar los cambios.

Para crear una migración en Visual Studio Code, debemos abrir una Terminal y colocarnos en la misma ruta en que se encuentra nuestro archivo `tualquiler.csproj` de nuestro proyecto de MVC y ejecutamos el siguiente comando del paquete `EF Core CLI` que instalas mediante el comando `dotnet tool install --global dotnet-ef`:


```bash
dotnet ef migrations add NombreDeLaMigracion
```

Para nuestro ejemplo, podemos nombrar nuestra migración como **TablasDeEjemplo**:

```bash
dotnet ef migrations add TablasDeEjemplo
```

Una salida como esta se mostrará:
```bash
PS C:\Oswaldo\.NET_Projects\tualquiler> dotnet ef migrations add TablasDeEjemplo
Build started...
Build succeeded.
Done. To undo this action, use 'ef migrations remove'
```

**NOTA:** Si deseas descartar una migración antes de "migrarla" debes ejecutar el comando `ef migrations remove` tal como lo dice el mensaje anterior.

Este es el comando para crear una migración si estás utilizando Visual Studio:

```bash
Add-Migration NombreDeLaMigracion
```

Y para removerla en Visual Studio, usamos el comando `Remove-Migrations`:

```bash
Build started...
Build succeeded.
To undo this action, use Remove-Migrations
```

Esto, creará una carpeta llamada `Migrations` en la raíz de nuestro proyecto donde se colocarán los archivos correspondientes a las migraciones.

## 4.3 **Actualizando una Migración**

Para actualizar o ejecutar una migración previamente creada, usamos el siguiente comnando:

```bash
dotnet ef database update
```

Este comando va a aplicar las migraciones a nuestra base de datos, como no existe la va a crear. Si ya existiera, la va a actualizar.

