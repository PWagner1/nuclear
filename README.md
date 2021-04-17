# Nuclear :atom_symbol:

_[![nuget-clear version](https://img.shields.io/nuget/v/nuget-clear.svg?style=flat&label=NuGet:%20nuget-clear)](https://www.nuget.org/packages/nuget-clear)_

Does your NuGet package have too many versions? Do you want to bulk delete or unlist them? Do it quickly using [Nuclear](https://www.nuget.org/packages/nuget-clear)!

## Installation

You can install `nuclear` as a [.NET tool](https://docs.microsoft.com/en-us/dotnet/core/tools/global-tools):

```
dotnet tool install --global nuget-clear --version 1.0.0-preview1
```

## Examples

Let's find some versions of your package to delete:

```
nuclear list My.Package
```

Too many results? Try filtering the package list using [floating version notation](#version-ranges):

```
nuclear list My.Package 1.1.*
```

Let's nuke some packages! 🤯

```
nuclear delete My.Package 2.0.0-* --api-key NUGET_API_KEY
```

This [unlists](https://docs.microsoft.com/en-us/nuget/nuget-org/policies/deleting-packages) pre-releases of v2.0.0 of `My.Package` on nuget.org.

You can create API keys on nuget.org using [this documentation](https://docs.microsoft.com/en-us/nuget/nuget-org/publish-a-package#create-api-keys). Make sure to select the `Unlist package` scope when creating your API key.

## Reference

### Version ranges

NuGet packages use [semantic versioning](https://semver.org/) and has the form `Major.Minor.Patch[-PreleaseLabel]`. Examples include `1.0.0` or `1.0.0-preview1`. A package is considered *pre-release* if it has a pre-release label, or *stable* otherwise.

Nuclear supports floating notation. For example:

Notation | Accepted | Rejected | Notes
-- | -- | -- | --
1.0.0 | 1.0.0 | 2.0.0 | Exact version match
1.0.\* | 1.0.0, 1.0.1 | 1.1.0, 2.0.0,<br />1.0.0-prerelease | Excludes pre-releases
1.\* | 1.0.0, 1.2.0 | 2.0.0,<br />1.0.0-prerelease | Excludes pre-releases
\* | 0.0.0, 1.2.3 | 1.0.0-prerelease | Matches all stable versions
1.0.0-\* | 1.0.0-alpha, 1.0.0-beta | 1.0.0 | Excludes stable releases
\*-\* | 1.0.0-alpha, 3.4.5-beta | 1.0.0 | Matches all pre-release versions

