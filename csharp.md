# C Sharp
======

## Dotnet Commands
------
#### Information about dotnet version/environment
dotnet -info
#### Create new project
dotnet new console
#### Compile & Run C# Program
dotnet run
#### Create New sln File
dotnet new sln
#### Build/Compile Program
dotnet build (looks for sln file in current directory) //  all projects build
#### Variable Scoping
Everything scoped to the smallest block (usually curly braces)

## Logic
------
#### If Statement
if(){}
#### If...Else Statement
if(){}else if(){}
#### Do While Loop
do{ } while();
#### While Loop
while(){};
#### For Loop
foreach(foo in foos){}
#### For Loop
for(var i = 1; i <= 10; i++){};
#### Case/Switch Statement
switch(a){case 1: var c=1;break; case 2: var c=2; break; default: var c=3; break;}
#### Try/Catch/Finally
try{}catch{}catch{}finally{}

## Jump over code
------
#### Stop loop early
break;
#### Skip iteration of loop
continue;
#### Goto another area of code
goto <label>;   <label>:
#### Evaluate a condition at runtime
when (case var d when d >= 90)
#### Thrown an exception
throw new ArgumentException("foo");
#### Catch an exception


## ASP.NET
------
#### wwwroot
static files such as images/scripts/external libs
#### controllers
contains the controller files
#### models
model files
#### views
view files
#### appsettings.json
config settings of the app, db connection string, application variables, etc.
#### bundleconfig.json
create bundles and minifications of CSS files/scripts
#### program.cs
app entry point w/host,web server,startup.cs file
#### startup.cs
add services & config HTTP pipeline & URL routes

## Compiling
------
#### Create Self-contained application
dotnet publish -c Release -r win10-x64 /p:PublishSingleFile=true /p:PublishTrimmed=true