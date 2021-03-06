### Build status - Master

| AppVeyor (Windows)       | Travis CI (Linux / macOS) |
|--------------------------|--------------------------|
| [![av-image][]][av-site] | [![tv-image][]][tv-site] |

[tv-image]: https://travis-ci.org/OneGet/oneget.svg?branch=master
[tv-site]: https://travis-ci.org/OneGet/oneget/branches
[av-image]: https://ci.appveyor.com/api/projects/status/0q1frhm84pp83syh/branch/master?svg=true
[av-site]: https://ci.appveyor.com/project/jianyunt/oneget


# PackageManagement (aka OneGet)


### What's New
Follow our [News Panel](https://github.com/OneGet/oneget/wiki/News-Panel).

Check out the PackageManagement and PowershellGet Modules in [PowerShellGallery.com](https://www.PowerShellGallery.com)


### Get Started!

OneGet is shipped in Win10 and Windows Server 2016! For downlevel OS, you can install the [WMF 5.0 RTM][WMF5.0] or [WMF5.1 Preview][WMF5.1] and then start using the OneGet.

You can follow [@PSOneGet on Twitter](http://twitter.com/PSOneGet) to be notified of every new build.


* Learn how to [use the PowerShell cmdlets](https://github.com/OneGet/oneget/wiki/cmdlets), [try some samples](https://github.com/PowerShell/PowerShell-Docs/blob/staging/wmf/5.0/oneget_cmdlets.md), or read [our MSDN Technet docs](https://technet.microsoft.com/en-us/library/mt422622.aspx)
* Read our [General Q and A](https://github.com/OneGet/oneget/wiki/Q-and-A)
* Learn about the [8 Laws of Software Installation](https://github.com/OneGet/oneget/wiki/8-Laws-of-Software-Installation)
* [General Troubleshooting](https://github.com/OneGet/oneget/wiki/General-Troubleshooting)
* Check out more help information [in our wiki page](https://github.com/oneget/oneget/wiki)


[WMF5.0]: https://www.microsoft.com/en-us/download/details.aspx?id=50395
[WMF5.1]: https://www.microsoft.com/en-us/download/details.aspx?id=53347

#### What is PackageManagement (OneGet)?

OneGet is a Windows package manager, renamed as PackageManagement. It is a unified interface to package management systems and aims to make Software Discovery, Installation and Inventory (SDII) work via a common set of cmdlets (and eventually a set of APIs). Regardless of the installation technology underneath, users can use these common cmdlets to install/uninstall packages, add/remove/query package repositories, and query a system for the software installed.

With OneGet, you can
* Manage a list of software repositories in which packages can be searched, acquired, and installed
* Search and filter your repositories to find the packages you need
* Seamlessly install and uninstall packages from one or more repositories with a single PowerShell command

#####PackageManagement Architecture#####

![Image](./assets/OneGetArchitecture.PNG?raw=true)

<br/>


### Let's Try it

#### Prerequisites
 - Windows 10, Windows Server 2016, or down-level Windows OS + WMF5
 - Linux or Mac with the [PowerShellCore][pscore]


#### Working with PowerShellGallery.com

 ```powershell
 # 1.check available providers

 PS E:\> get-packageprovider

Name                     Version          DynamicOptions
----                     -------          --------------
msi                      3.0.0.0          AdditionalArguments
msu                      3.0.0.0
PowerShellGet            1.1.0.0          PackageManagementProvider, Type...
Programs                 3.0.0.0          IncludeWindowsInstaller,...

# 2. find a module from the PowerShell gallery, for example, xjea

PS E:\> find-module xjea

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program
Files\PackageManagement\ProviderAssemblies' or 'C:\Users\jianyunt\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by
running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y

Version    Name           Repository           Description
-------    ----           ----------           -----------
0.3.0.0    xJea           PSGallery             Module with DSC Resources for Just Enough...

# 3. install a module from the PowerShell gallery

PS E:\> Install-Module xjea

Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its InstallationPolicy value by running the Set-PSRepository cmdlet. Are
you sure you want to install the modules from 'gallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): y

# 4. Find out if a module installed

PS E:\> Get-InstalledModule -name xjea

Version    Name        Repository      Description
-------    ----        ----------       -----------
0.3.0.0    xJea        gallery          Module with DSC Resources for Just Enough Admin (JEA)..

# 5. Unisntall a module

PS E:\> Uninstall-Module -name xjea
```
<br/>
#### Working with http://www.NuGet.org repository
<br/>
```powershell

# find a package from the nuget repository

PS E:\> find-package -name jquery -provider Nuget -Source https://www.nuget.org/api/v2

Name           Version          Source           Summary
----           -------          ------           -------
jQuery          3.1.1            nuget.org        jQuery is a new kind of JavaScript Library....

# install a package from NuGet repository

PS E:\> install-package -name jquery -provider Nuget -Source https://www.nuget.org/api/v2

The package(s) come(s) from a package source that is not marked as trusted.
Are you sure you want to install software from 'nuget.org'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): y

Name             Version          Source           Summary
----             -------          ------           -------
jQuery           3.1.1            nuget.org        jQuery is a new kind of JavaScript Library....

# Uninstall the package

PS E:\> uninstall-package jquery

Name            Version          Source           Summary
----            -------          ------           -------
jQuery          3.1.1            C:\Program Fi... jQuery is a new kind of JavaScript Library....

# Register a package Source

PS E:\> Register-PackageSource -name test -ProviderName NuGet -Location https://www.nuget.org/api/v2

Name             ProviderName     IsTrusted  Location
----              ------------     ---------  --------
test              NuGet            False      https://www.nuget.org/api/v2

# find a package from the registered package Source

PS E:\> find-package -Source test -name jquery

Name                Version          Source           Summary
----                -------          ------           -------
jQuery              3.1.1            test             jQuery is a new kind of JavaScript Library....

```

<br/>

### Try the latest PackageManagement (OneGet)

You can run `install-module PowerShellGet` to install the latest PackageManagment and PowerShellGet from [PowerShellGallery](https://www.powershellgallery.com).
[pscore]:https://github.com/PowerShell/PowerShell

### Downloading the Source Code
OneGet repo has a number of other repositories embeded as submodules. To make things say, you can just clone recursively:
```powershell
git clone --recursive https://github.com/OneGet/oneget.git
```
If you already cloned but forgot to use --recursive, you can update submodules manually:
```powershell
git submodule update --init
```

### Building the code

``` powershell

After clone this repository, go to the project folder

> cd oneget
> cd src

# download the dotnet cli tool
> .\bootstrap.ps1

# building OneGet for fullclr
> .\build.ps1 net451

#building OneGet for coreclr
> .\build.ps1 netstandard1.6

If successfully built above, you should be able to see a folder:
\oneget\src\out\PackageManagement gets created. The layout looks like below:

      coreclr
      fullclr
      PackageManagement.format.ps1xml
      PackageManagement.psd1
      PackageManagement.psm1
      PackageProviderFunctions.psm1
```

### Deploying it

#### Generate PackageManagement.nupkg
We can use `publish-module` to create a .nupkg. Assuming you want to put the generated .nupkg in c:\test folder.  You can do something like below. Note I cloned to E:\OneGet folder.
 ```powershell
cd E:\OneGet\oneget\src\out\PackageManagement
Register-PSRepository -name local -SourceLocation c:\test
Get-PSRepository
Publish-Module -path .\ -Repository local
PS E:\OneGet\oneget\src\out\PackageManagement> dir c:\test\PackageManagement*.nupkg

    Directory: C:\test


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        11/4/2016   4:15 PM        1626335 PackageManagement.1.1.0.0.nupkg
```
Then you can do
```powershell
find-module -Repository local
install-module -Repository local -Name PackageManagement
```
to get the newly built PackageManagement on your machines.

#### Manual copy
You can also manually copy the OneGet binaries. For example, copy the entire `E:\OneGet\oneget\src\out\PackageManagement` folder you just built to your
`$env:Programfiles\WindowsPowerShell\Modules\PackageManagement\#onegetversion\`

If you are running within PowerShellCore,
similarily drop the PackageManagement folder to your `$env:Programfiles\PowerShell\#psversion\Modules\PackageManagement\#onegetversion\`,

or copy to `/opt/microsoft/powershell/<psversion>/Modules/PackageManagement/#onegetversion/`,
if you are running on Linux or Mac.

**Note**: OneGet version number can be found from the PackageManagement.psd1 file.

### Testing the code
```PowerShell
> cd oneget
> cd Test
> & '.\run-tests.ps1' fullclr
> & '.\run-tests.ps1' coreclr


```


### Understanding the OneGet code repository

OneGet is under rapid development, and so you get to see just how the sausage is being made. I try to keep the master branch clean and buildable, but my own working branch can get pretty damn wild and I make no bones about some of this. I work fast, I make big changes, and I try to keep my eye on the target.

Feel free to clone the repository, and check out the different branches:

#### Branches

There are currently three branches in the git repository:

| Branch/Tag | Purpose |
| ------- | ---------------------------|
|`master`|  The `master` branch is where the daily builds of OneGet will be made from.  |
|`WMF5_RTM`|  The `WMF5_RTM` tag is to mark the WMF 5.0 RTM release point. |
|`TP5`|  The `TP5` tag is to mark the TP5 release point. |
|`wip`|  The `wip` branch is where the current **unstable** and **not-likely-working** coding is taking place. This lets you see where I'm at before stuff actually hits the master branch. Fun to read, but really, the wild-west of code branches. |


### Contributing to OneGet

Contributions to the OneGet project will require the signing of a CLA -- contact @jianyunt for details...

In the immediate time frame, we won't be taking pull requests to the core itself, as we still have many masters at Microsoft to keep happy, and I have a lot of release process stuff I have to go thru to make them happy.

There are some exceptions to the where I can take Pull Requests immediately:

> Pull Requests to the Package Providers are instantly welcome

> Any unit tests, BVT tests or -Edge only features, we can take pull requests for as well

> Docs, Wiki, content, designs, bugs -- everything gleefully accepted :D


### Participating in the OneGet Community

I'm eager to work with anyone who wants to help shape the future of Package Management on Windows -- your opinions, feedback and code can help everyone.


### Online Meeting

We have an online meetings. We will twitter the exact time as well as put a note on GitHub site.  (everyone welcome!)

You can see archives of the previous meetings available on

All meeting notes are recorded under [OneDrive PackageManagement](https://onedrive.live.com/?authkey=%21ABehsy6i3rzQdxE&id=EF4B329A5EB9EA4D%21127&cid=EF4B329A5EB9EA4D)


### Project Dashboard

You can see issues, pull requests, backlog items, etc. in the [OneGet Dashboard](https://waffle.io/oneget/oneget)

[![Stories in Progress](https://badge.waffle.io/oneget/oneget.svg?label=Bug&title=Bug)](http://waffle.io/OneGet/OneGet)
[![Stories in Progress](https://badge.waffle.io/oneget/oneget.svg?label=Investigate&title=Investigate)](http://waffle.io/OneGet/OneGet)
[![Stories in Progress](https://badge.waffle.io/oneget/oneget.svg?label=Discussion&title=Discussion)](http://waffle.io/OneGet/OneGet)
[![Stories in Progress](https://badge.waffle.io/oneget/oneget.svg?label=New%20Feature&title=New%20Feature)](http://waffle.io/OneGet/OneGet)
[![Stories in Progress](https://badge.waffle.io/oneget/oneget.svg?label=PowerShellGet&title=PowerShellGet)](http://waffle.io/OneGet/OneGet)

Throughput Graph

[![Throughput Graph](https://graphs.waffle.io/OneGet/oneget/throughput.svg)](https://waffle.io/OneGet/oneget/metrics)


### Team Members

| Branch | Purpose |
| ------- | ---------------------------|
|@Xumin|  Program Manager on OneGet. Xumin is the sheriff, trying to keep the law. If there are rules that we need to play by, Xumin make us follow them.   |
|@Jianyun|  Engineer owner on OneGet & its providers. |
|@Krishna|  Our engineer manager on OneGet, also owner for PowerShell Gallery.   |
|@Quoc|  Engineer on the team.   |

[Follow us on Twitter](https://twitter.com/PSOneGet)

### More Resources
- [NuGet Provider](https://github.com/OneGet/NuGetProvider)
- [PowerShellGet Provider](https://github.com/PowerShell/PowerShellGet)
- [MicrosoftDockerProvider](https://github.com/OneGet/MicrosoftDockerProvider)
- [NanoServerPackage](https://github.com/OneGet/NanoServerPackage)
- Checkout OneGet providers from our Community such as Gistprovider, OfficeProvider, 0Install and more from powershellgallery.com or simply run [Find-PackageProvider cmdlet](https://msdn.microsoft.com/en-us/powershell/gallery/psget/oneget/packagemanagement_cmdlets)
- Want to write a provider? Checkout our [sample provider](https://www.powershellgallery.com/packages/MyAlbum/)
- Wanna to download packages from http://Chocolatey.org, try out [ChocolateyGet provider](https://www.powershellgallery.com/items?q=ChocolateyGet&x=15&y=13)
- Wanna to control which packages to use and where to get them from based on your organization, checkout [PSL provider](https://github.com/OneGet/PSLProvider)
