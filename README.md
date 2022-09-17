# NStack

![Build](https://github.com/migueldeicaza/NStack/actions/workflows/build.yml/badge.svg)
[![Version](https://img.shields.io/nuget/v/NStack.Core.svg)](https://www.nuget.org/packages/NStack.Core)
[![Downloads](https://img.shields.io/nuget/dt/NStack.Core)](https://www.nuget.org/packages/NStack.Core)
[![License](https://img.shields.io/github/license/migueldeicaza/NStack.svg)](LICENSE)
![Bugs](https://img.shields.io/github/issues/migueldeicaza/NStack)

NOTE: NStack has moved to the guo-cs org: https://github.com/orgs/gui-cs/Currently, this library contains a port of the Go string, and Go rune support as well as other Unicode helper methods.

Currently, this library contains a port of the Go string, and Go rune support as well as other Unicode helper methods.

You can browse the [API documentation](https://migueldeicaza.github.io/NStack/api/NStack.html).

Install the [NuGet package from NuGet.org](https://www.nuget.org/packages/NStack.Core) by installing `NStack.Core`.

# Future Additions

The long term goal is to make this module an exploration of what the .NET APIs for IO looked like if they only
used exceptions for either invalid parameters being passed to
methods and used results/error codes for most IO operations:

* Exceptions have a role, but IO code tends to become ugly in its presence.

* Other areas include making an IO layer that does not surface "string" for
filenames, as in Unix there are really no filenames as we treat them in
.NET, but rather file names are a collection of bytes, which do not necessarily
can be decoded into UTF8 [1].  

To make things simple, this assumes that UTF8 strings (ustring in this code)
can exist without them being valid UTF8 strings, but rather a collection of bytes.

[1] For example, older file systems can have filenames that made sense with
a particular character set and are effectively not possible to map into strings.


# Version Numbers

Version info for NStack is managed by [gitversion](https://gitversion.net).

Install `gitversion`:

```powershell
dotnet tool install --global GitVersion.Tool
dotnet-gitversion
```

The project version (the nuget package and in `NStack.dll`) is determined from the latest `git tag`. 

The format of version numbers is `vmajor.minor.patch.build.height` and follows the [Semantic Versioning](https://semver.org/) rules.

To define a new version (e.g. with a higher `major`, `minor`, `patch`, or `build` value) tag a commit using `git tag`:

```powershell
git tag v1.3.4-beta.5 -a -m "Release v1.3.4 Beta 5"
dotnet-gitversion /updateprojectfiles
dotnet build -c Release
```

**DO NOT COMMIT AFTER USING `/updateprojectfiles`!**

Doing so will update the `.csproj` files in your branch with version info, which we do not want.