# About

Using the published powershell functions and this repo content:
1. You can answer question in which DevExpress nuget package can I find my solution assemblies.
2. Providing a packagesource for the DevExpress assemblies you can download and flatten all in a folder.
3. Update your projects references HintPath for the DevExpress assemblies.
4. Build the solution with success without having to install DevExpress.

## How to consume the csv files
For example let's assume we look which packages are related to `Xpo` for the `18.2.4` version.
```ps1
(new-object System.Net.WebClient).DownloadString("https://raw.githubusercontent.com/eXpandFramework/DevExpress.PackageContent/master/Contents/18.2.4.csv")|ConvertFrom-csv|Where{$_.Name -like "*xpo*"}
```
the above outputs:
```
Name                                         File
----                                         ----
DevExpress.ExpressApp.Security.Xpo.18.2.4    DevExpress.ExpressApp.Security.Xpo.v18.2
DevExpress.ExpressApp.Security.Xpo.de.18.2.4 DevExpress.ExpressApp.Security.Xpo.v18.2.resources
DevExpress.ExpressApp.Security.Xpo.es.18.2.4 DevExpress.ExpressApp.Security.Xpo.v18.2.resources
DevExpress.ExpressApp.Security.Xpo.ja.18.2.4 DevExpress.ExpressApp.Security.Xpo.v18.2.resources
DevExpress.ExpressApp.Security.Xpo.ru.18.2.4 DevExpress.ExpressApp.Security.Xpo.v18.2.resources
DevExpress.ExpressApp.Xpo.18.2.4             DevExpress.ExpressApp.Xpo.v18.2
DevExpress.ExpressApp.Xpo.18.2.4             DevExpress.Persistent.BaseImpl.v18.2
DevExpress.RichEdit.Export.18.2.4            DevExpress.RichEdit.v18.2.Export
DevExpress.RichEdit.Export.18.2.4            DevExpress.RichEdit.v18.2.Export
DevExpress.Xpo.18.2.4                        DevExpress.Xpo.v18.2
DevExpress.Xpo.18.2.4                        DevExpress.Xpo.v18.2
DevExpress.Xpo.de.18.2.4                     DevExpress.Xpo.v18.2.resources
DevExpress.Xpo.de.18.2.4                     DevExpress.Xpo.v18.2.resources
DevExpress.Xpo.es.18.2.4                     DevExpress.Xpo.v18.2.resources
DevExpress.Xpo.es.18.2.4                     DevExpress.Xpo.v18.2.resources
DevExpress.Xpo.Extensions.18.2.4             DevExpress.Xpo.v18.2.Extensions
DevExpress.Xpo.ja.18.2.4                     DevExpress.Xpo.v18.2.resources
DevExpress.Xpo.ja.18.2.4                     DevExpress.Xpo.v18.2.resources
DevExpress.Xpo.ru.18.2.4                     DevExpress.Xpo.v18.2.resources
DevExpress.Xpo.ru.18.2.4                     DevExpress.Xpo.v18.2.resources
```

Having the above list we can now use the `Install-DX` cmdLet from the same `XpandPosh` module we installed before.

```ps1
Install-DX -binPath $(Default.SystemDirectory)\Xpand.DLL -dxSources $(Get-PackageSourceLocations -join ";") -sourcePath $(Default.SystemDirectory) -dxVersion 18.2.4 

```
The above command copies all DevExpress assemblies used from `eXpandFramework` in the `Xpand.Dll` folder.

Finally we can update the `HintPath` to all project references, so we can build.

```ps1
Update-HintPath -OutputPath "c:\eXpandFramework\Xpand.Dll" -SourcesPath "c:\eXpandFramework"
```

## How to create a content file.
Open a powershell command prompt and type the next commands.

```ps1
Install-Module XpandPosh
Get-NugetPackageAssembly "C:\Program Files (x86)\DevExpress 18.2\Components\System\Components\Packages"|Export-Csv 18.2.4.csv
Install
```

The above script will create a csv file that contains all packages used `eXpandFramework`.

PR are welcome if you generated unlisted data. 