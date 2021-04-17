# Nuclear :atom_symbol:

_[![nuget-clear version](https://img.shields.io/nuget/v/nuget-clear.svg?style=flat&label=NuGet:%20nuget-clear)](https://www.nuget.org/packages/nuget-clear)_

Need to delete many NuGet packages? Do it quickly using `nuclear`! 

## Installation

You can install `nuclear` as a [.NET tool](https://docs.microsoft.com/en-us/dotnet/core/tools/global-tools):

```
dotnet tool install --global nuget-clear --version 1.0.0-preview1
```

## Examples

List your package's versions:

```
nuclear list My.Package
```

Too many results? Try filtering the package list using [floating version notation](#version-ranges):

```
nuclear list My.Package 1.1.*   # Includes 1.1.1 and 1.1.2, but not 1.2 or 1.1.0-prerelease
nuclear list My.Package 1.0.0-* # List all prereleases for version 1.0.0
```

Time to nuke some packages! 🚀

```
nuclear delete My.Package 2.0.* -k NUGET_API_KEY
```

To create API keys on nuget.org, refer to [this documentation](https://docs.microsoft.com/en-us/nuget/nuget-org/publish-a-package#create-api-keys). Make sure to select the `Unlist package` scope when creating your API key.

## Version ranges

NuGet versions have the form `Major.Minor.Patch[-PrereleaseLabel]`. Examples include `1.0.0` or `1.0.0-preview1`. A package is considered *pre-release* if it has a pre-release label, or *stable* otherwise.

Nuclear supports floating notation. For example:

Notation | Accepted | Rejected | Notes
-- | -- | -- | --
1.0.0 | 1.0.0 | 2.0.0 | Exact version match
1.0.\* | 1.0.0, 1.0.1 | 1.1.0, 2.0.0,<br />1.0.0-prerelease | Excludes pre-releases.
1.\* | 1.0.0, 1.2.0 | 2.0.0,<br />1.0.0-prerelease | Excludes pre-releases.
\* | 0.0.0, 1.2.3 | 1.0.0-prerelease | Matches all stable versions
1.0.0-\* | 1.0.0-alpha, 1.0.0-beta | 1.0.0 | Excludes stable releases
\*-\* | 1.0.0-alpha, 3.4.5-beta | 1.0.0 | Matches all pre-release versions

