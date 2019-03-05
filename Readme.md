[![Build Status](https://dev.azure.com/eXpandDevOps/eXpandFramework/_apis/build/status/Populate-DevExpress-Packages-Contents?branchName=master)](https://dev.azure.com/eXpandDevOps/eXpandFramework/_build/latest?definitionId=36&branchName=master)
# About

In this repository you can find an `index` of all DevExpress Nuget packages assemblies in the form of `csv` files. The [Populate-DevExpress-Packages-Contents](https://github.com/eXpandFramework/Azure-Tasks/blob/master/Populate-DevExpress-Packages-Contents.yml) pipeline runs daily indexing any new packages found. The csv file is then commited to this repo and a release is tagged. 

Subscribe to Github release notifications to get notified the day a new DevExpress nuget packaged is in your nuget feed.

## Prerequisites
Install [XpandPosh](https://www.powershellgallery.com/packages/XpandPosh/) from [PSGallery](https://www.powershellgallery.com/)

```ps1
Install-Module XpandPosh
```
## How to consume the csv files
For example let's assume we look which packages are related to `Xpo` for the `18.2.4` version.
```ps1
Get-DxNugets 18.2.4|Where{$_.Assembly -like "*xpo*"}
```
the above outputs:
```
Package                               Version Assembly
-------                               ------- --------
DevExpress.ExpressApp.Security.Xpo.ja 18.2.5  DevExpress.ExpressApp.Security.Xpo.v18.2.resources
DevExpress.ExpressApp.Security.Xpo.ru 18.2.5  DevExpress.ExpressApp.Security.Xpo.v18.2.resources
DevExpress.ExpressApp.Security.Xpo    18.2.5  DevExpress.ExpressApp.Security.Xpo.v18.2
DevExpress.ExpressApp.Security.Xpo.de 18.2.5  DevExpress.ExpressApp.Security.Xpo.v18.2.resources
DevExpress.ExpressApp.Xpo             18.2.5  DevExpress.ExpressApp.Xpo.v18.2
DevExpress.RichEdit.Export            18.2.5  DevExpress.RichEdit.v18.2.Export
DevExpress.Xpo.es                     18.2.5  DevExpress.Xpo.v18.2.resources
DevExpress.Xpo.de                     18.2.5  DevExpress.Xpo.v18.2.resources
DevExpress.Xpo.es                     18.2.5  DevExpress.Xpo.v18.2.resources
DevExpress.Xpo.Extensions             18.2.5  DevExpress.Xpo.v18.2.Extensions
DevExpress.Xpo.ru                     18.2.5  DevExpress.Xpo.v18.2.resources
DevExpress.Xpo                        18.2.5  DevExpress.Xpo.v18.2
DevExpress.Xpo.ja                     18.2.5  DevExpress.Xpo.v18.2.resources
```

Having the above list we can now use the `Install-DX` cmdLet from the same `XpandPosh` module we installed before.

```ps1
Register-PackageSource –ProviderName Nuget –Name DX_private –Location https://nuget.devexpress.com/YOURTOKEN
Install-DX -binPath $(Default.SystemDirectory)\Xpand.DLL -dxSources $(Get-PackageSourceLocations -join ";") -sourcePath $(Default.SystemDirectory) -dxVersion 18.2.5 

```
The above command copies all DevExpress assemblies used from `eXpandFramework` in the `Xpand.Dll` folder.

Finally we can update the `HintPath` to all project references, so we can build.

```ps1
Update-HintPath -OutputPath "c:\eXpandFramework\Xpand.Dll" -SourcesPath "c:\eXpandFramework"
```

