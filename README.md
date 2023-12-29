# ASP.NET-Core-MVC-ElectronNET
Short instruction of how to implement ASP.NET Core MVC (.NET 8.0) with ElectronNET (23.6.1).

1. Create new project with `dotnet` tool:
    ```
    dotnet new mvc --use-program-main
    ```
2. Add package `ElectronNET.API` to project:
    ```
    dotnet add package ElectronNET.API
    ```

3. Add `electronize` to `dotnet` tools:
    ```
    dotnet tool install ElectronNET.CLI -g
    ```

4. Add following code to `Program.cs`:

    ```cs
    // Add using statements
    using ElectronNET.API;
    using ElectronNET.API.Entities;

    // ...
    
    // Add after var builder = WebApplication.CreateBuilder(args);
    builder.WebHost.UseElectron(args);
    builder.Services.AddElectron();

    // ...

    // Add instead of app.Run();
    // Remember to add async to Main method
    await app.StartAsync();
    await Electron.WindowManager.CreateWindowAsync();
    app.WaitForShutdown();
    ```

5. Electronize app:
    ```
    electronize init
    ```

6. Start app (first time is slow beacause of `npm install`):
    ```
    electronize start
    ```

7. If you want to build with `electronize`, you will need `electron-builder` tool:

    ```
    npm install -g electron-builder
    ```

8. Now build app with command:
    ```
    electronize build /target win-x64
    ```