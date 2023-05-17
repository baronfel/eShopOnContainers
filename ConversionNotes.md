# Notes from conversion to .NET SDK Containers

* Prereqs have changed - now must have Node and `ng` CLI installed
* SPA Client is now an `.esproj`, so it naturally fits with the SPA backend via `ProjectReference`
  * There may be feature gaps here - for example when publishing the SPA backend both the dev and prod builds of the SPA client are run
    * This should be taken up with the JSPS team
* One-stop run command: `dotnet build /t:Containerize <sln file> && docker-compose up`
* Container names are slightly changed - current .NET SDK Container tooling is being very aggressive here and rewriting `.` to `-`
  * having said that, `.` is _very_ uncommon in the wild and `-` is much more normalized
* I don't know enough about the app to verify all functionality - this should be vetted

Hacks/workarounds
* The .NET SDK Container tooling doesn't support solution-level publish at the moment. I've added a target I've been prototyping to `Directory.Build.targets` to facilitate this for the moment.  
  * We should be targeting this use case for .NET 8
* The .NET SDK Container tooling in preview 4 isn't fully embedded into the SDK, so I added the package and replicated some of the preview5 experience manually. 
  * When preview5 is available, make the following changes
    * remove PackageVersion for container builds from Directory.Package.props
    * remove PackageReferences in the SDK projects
    * remove the `EnableSdkContainerSupport` setting in the web projects (will be inferred automatically)
