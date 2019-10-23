# SystemWebSdk
 Exploration of using new .NET SDK-style projects with ASP.NET (System.Web) projects

## Goal
Enable a reasonable (unblocking) experience for customers to use the new SDK-based project system and files for their System.Web-based ASP.NET projects (Web Forms, MVC, and Web API). This will provide a stepping-stone for customers looking to migrate from .NET Framework to .NET Core that provides immediate benefits (e.g. simpler project file, new NuGet experience, better interoperability with .NET Standard class libraries, etc.).

## Scenarios to consider enabling
- Editing pages/views (ASPX and CSHTML)
- Managing dependencies (NuGet, BCL)
- Build (output should be identical to old csproj)
- Launch & debug (use the new launch experience, launchSettings.json, IIS Express, IIS, etc.)
- Binding redirects
- Publish (local, Azure)
  - Web.config transforms
- File nesting in Solution Explorer
- Default globs
- Templates (project & item)
- Localization (RESX files)
	
## Scenarios almost certainly out of scope
- Scaffolding
- Client dependency management (same story as ASP.NET Core, aka manual, LibMan, etc.)
- Old-style NuGet content files
- NuGet Install/Uninstall.ps1 files

## Strawman desired experience 
Create a package-based SDK, `Microsoft.NET.Sdk.SystemWeb`, that can be configured in the project file and would be resolved directly from NuGet (i.e. NuGet package SDK resolution, already supported), e.g.

    ``` xml
	<Project Sdk="Microsoft.NET.Sdk.SystemWeb">
	  <PropertyGroup>
	    <TargetFramework>net472</TargetFramework>
	  </PropertyGroup>
	  
	  <ItemGroup>
	    <PackageReference Include="Microsoft.AspNet.Mvc" Version="5.2.7" />
	    <PackageReference Include="Microsoft.AspNet.Web.Optimization" Version="1.1.3" />
	    <PackageReference Include="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" Version="2.0.0" />
	    <PackageReference Include="Newtonsoft.Json" Version="11.0.1" />
	    <PackageReference Include="WebGrease" Version="1.6.0" />
	  </ItemGroup>
	</Project>
   ```