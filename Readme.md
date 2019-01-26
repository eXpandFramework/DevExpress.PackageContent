# About
This repository contains files that you may find useful when DevExpress is not install and you need to download the DevExpress assemblies used to build your solution.

Using the published powershell functions you can answer the question in which DevExpress nuget package can I find this assembly.

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



## How to create a content file.
Open a powershell command prompt and type the next commands.

```ps1
Install-Module XpandPosh
Get-NugetPackageAssembly -sourcePath "C:\Work\eXpandFramework\expand" -nupkgPath $sources|Export-Csv 18.2.4.csv
Install
```

The above script will create a csv file that contains all packages used `eXpandFramework`.

PR are welcome if you generated unlisted data. 