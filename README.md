# csheet

# OpenSUSE

## Yast

### Definition of Terms [origin](https://doc.opensuse.org/documentation/leap/startup/single-html/book.opensuse.startup/index.html#sec.onlineupdate.terms)

I termini seguenti sono importanti per comprendere l'installazione e la rimozione del software in OpenSUSE LEAP
> The following terms are important for understanding installing and removing software in openSUSE Leap.

#### Repository

Una directory locale o remota contenente pacchetti, più informazioni addizionali circa questi pacchetti (metadati dei pacchetti)
>    A local or remote directory containing packages, plus additional information about these packages (package metadata). 

#### (Repository) Alias/Repository Name

Un nome breve per un repository (chiamato Alias in Zypper e Repository Name in YaST). 
Esso può essere scelto dall'utente durante l'aggiunta del repository e deve essere unico.
>    A short name for a repository (called Alias within Zypper and Repository Name within YaST). 
>    It can be chosen by the user when adding a repository and must be unique. 

#### Repository Description Files

Ciascun repository fornisce files descriventi il contenuto del repository (package names, versions, etc.)
Questi files di descrizione del repository sono scaricati in una cache locale che è usata da YaST.
>    Each repository provides files describing content of the repository (package names, versions, etc.). 
>    These repository description files are downloaded to a local cache that is used by YaST. 

#### Product

Rappresenta l'intero prodotto, per esempio OpenSUSE Leap.
>   Represents a whole product, for example openSUSE® Leap. 

#### Pattern

Un pattern è un gruppo di pacchetti installabili dedicato ad un certo scopo. 
Per esempio, il pattern Laptop contiene tutti i pacchetti che sono necessari in un ambiente di elaborazione mobile.
I pattern definiscono le dipendenze dei pacchetti (ad esempio i pacchetti necessari e raccomandati) e vengono con una preselezione di pacchetti segnati per l'installazione.
Questo assicura che i pacchetti più importanti necessari per un certo scopo siano disponibili sul tuo sistema dopo l'installazione del pattern.
Se è necessario, puoi selezionare e deselezionare pacchetti all'interno del pattern.
>    A pattern is an installable group of packages dedicated to a certain purpose. 
>    For example, the Laptop pattern contains all packages that are needed in a mobile computing environment. 
>    Patterns define package dependencies (such as required or recommended packages) and come with a preselection of packages marked for installation.
>    This ensures that the most important packages needed for a certain purpose are available on your system after installation of the pattern. 
>    If necessary, you can manually select or deselect packages within a pattern. 

#### Package

Un pacchetto è un file compresso in formato rpm che contiene i file per un particolare programma.
>    A package is a compressed file in rpm format that contains the files for a particular program. 

#### Patch

Una patch consiste di uno o più pacchetti e può essere applicata mediante delta RPMs.
Può anche introdurre dipendenze a pacchetti che non sono ancora stati installati.
>    A patch consists of one or more packages and may be applied by means of delta RPMs. 
>    It may also introduce dependencies to packages that are not installed yet. 

#### Resolvable

Un termine generico per prodotto, modello, pacchetto o patch. Il tipo più comunemente usato di resolvable è un pacchetto o una patch.
>    A generic term for product, pattern, package or patch. The most commonly used type of resolvable is a package or a patch. 

#### Delta RPM

Un delta RPM è costituito solo dalla differenza binaria tra due versioni definite di un pacchetto, e quindi ha la dimensione di download più piccola. Prima di essere installato, il pacchetto RPM completo viene ricostruito sul computer locale.
>    A delta RPM consists only of the binary diff between two defined versions of a package, and therefore has the smallest download size. Before being installed, the full RPM package is rebuilt on the local machine. 

#### Package Dependencies

Alcuni pacchetti dipendono da altri pacchetti, come le librerie condivise. 
In altri termini, un pacchetto potrebbe richiedere altri pacchetti: se i pacchetti richiesti non sono disponibili, il pacchetto non può essere installato. 
Oltre alle dipendenze (requisiti del pacchetto) che devono essere soddisfatte, alcuni pacchetti raccomandano altri pacchetti. 
Questi pacchetti consigliati vengono installati solo se sono effettivamente disponibili, altrimenti vengono ignorati e il pacchetto che li raccomanda è comunque installato.
>    Certain packages are dependent on other packages, such as shared libraries. 
>    In other terms, a package may require other packages—if the required packages are not available, the package cannot be installed. 
>    In addition to dependencies (package requirements) that must be fulfilled, some packages recommend other packages. 
>    These recommended packages are only installed if they are actually available, otherwise they are ignored and the package recommending them is installed nevertheless. 


# Managing Software with Command Line Tools [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#cha.sw_cl)

Questo capito descrie Zypper e RPM, due tool a riga di comando per la gestione del software.
Per una definizione della terminologia usate in questo contensto (per esemio, repository, patch, o update) fai rierimento a Book “Start-Up”, Chapter 10 “Installing or Removing Software”, Section 10.1 “Definition of Terms”.  
>    This chapter describes Zypper and RPM, two command line tools for managing software. 
>    For a definition of the terminology used in this context (for example, repository, patch, or update) refer to Book “Start-Up”, Chapter 10 “Installing or Removing Software”, Section 10.1 “Definition of Terms”. 


## Zypper

```
zypper [--global-options] COMMAND  [--command-options] [arguments]
```

Header | Comments | Command 
------------ | ------------- | -------------
Zypper Commands| The simplest way to execute Zypper is to type its name, followed by a command. For example, to apply all needed patches to the system | `sudo zypper patch`
Global Options | Additionally, you can choose from one or more global options by typing them immediately before the command. the option `--non-interactive` means that the command is run without asking anything (automatically applying the default answers).  | `sudo zypper --non-interactive patch`
Command-Specific Options | To use options that are specific to a particular command, type them immediately after the command. `--auto-agree-with-licenses` is used to apply all needed patches to a system without you being asked to confirm any licenses. Instead, license will be accepted automatically | `sudo zypper patch --auto-agree-with-licenses`
Arguments | Some commands require one or more arguments. For example, when using the command install, you need to specify which package or which packages you want to install | `sudo zypper install mplayer`
Arguments | Some options also require a single argument. The following command will list all known patterns | `zypper search -t pattern`


#### Installing and Removing Software with Zypper [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.softman)

Header | Comments | Command 
------------ | ------------- | -------------
| | To install | `sudo zypper install PACKAGE_NAME`
| | To remove | `sudo zypper remove PACKAGE_NAME`
 
 #### Selecting Which Packages to Install or Remove [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.selectpackage)
 
There are various ways to address packages with the commands zypper install and zypper remove

Header | Comments | Command 
------------ | ------------- | -------------
By Exact Package Name | | `sudo zypper install MozillaFirefox`
By Exact Package Name and Version Number | | `sudo zypper install MozillaFirefox-52.2`
By Repository Alias and Package Name | | `sudo zypper install mozilla:MozillaFirefox`
By Package Name Using Wild Cards | You can select all packages that have names starting or ending with a certain string. Use wild cards with care, especially when removing packages. The following command will install all packages starting with “Moz”| `sudo zypper install 'Moz*'`
Removing all -debuginfo Packages | When debugging a problem, you sometimes need to temporarily install a lot of -debuginfo packages which give you more information about running processes. After your debugging session finishes and you need to clean the environment, run the following | `sudo zypper remove '*-debuginfo'`
By Capability | For example, to install a package without knowing its name, capabilities come in handy. The following command will install the package MozillaFirefox | `sudo zypper install firefox`
By Capability, Hardware Architecture, or Version |  Together with a capability, you can specify a hardware architecture and a version | |
 | | The name of the desired hardware architecture is appended to the capability after a full stop. For example, to specify the AMD64/Intel 64 architectures (which in Zypper is named x86_64), use | `sudo zypper install 'firefox.x86_64'`
 | | Versions must be appended to the end of the string and must be preceded by an operator: < (lesser than), <= (lesser than or equal), = (equal), >= (greater than or equal), > (greater than).| `sudo zypper install 'firefox>=52.2'`
| | You can also combine a hardware architecture and version requirement | `sudo zypper install 'firefox.x86_64>=52.2'`
By Path to the RPM file | You can also specify a local or remote path to a package | `sudo zypper install /tmp/install/MozillaFirefox.rpm` 
|| | `sudo zypper install http://download.example.com/MozillaFirefox.rpm`

#### Combining Installation and Removal of Packages [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.combineinstall)

Header | Comments | Command 
------------ | ------------- | -------------
| | To install and remove packages simultaneously, use the +/- modifiers. To install emacs and simultaneously remove vim , use | `sudo zypper install emacs -vim`
| | To remove emacs and simultaneously install vim , use | `sudo zypper remove emacs +vim`
| | To prevent the package name starting with the - being interpreted as a command option, always use it as the second argument. If this is not possible, precede it with -- | 
| |  | `sudo zypper install -emacs +vim `      # Wrong 
| |  | `sudo zypper install vim -emacs `       # Correct 
| |  | `sudo zypper install -- -emacs +vim`    # Correct 
| |  | `sudo zypper remove emacs +vim`         # Correct

#### Cleaning Up Dependencies of Removed Packages [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.clean)

Header | Comments | Command 
------------ | ------------- | -------------
| | If (together with a certain package), you automatically want to remove any packages that become unneeded after removing the specified package, use the --clean-deps option | `sudo zypper rm PACKAGE_NAME --clean-deps` |

#### Using Zypper in Scripts [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.script)

This option allows the use of Zypper in scripts and cron jobs

Header | Comments | Command 
------------ | ------------- | -------------
| | By default, Zypper asks for a confirmation before installing or removing a selected package, or when a problem occurs. You can override this behavior using the --non-interactive option. This option must be given before the actual command (install, remove, and patch), as can be seen in the following | `sudo zypper --non-interactive install PACKAGE_NAME` |

#### Installing or Downloading Source Packages [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.softman.sources)

Header | Comments | Command 
------------ | ------------- | -------------
| | To install the corresponding source package of a package. When executed as root, the default location to install source packages is /usr/src/packages/ and ~/rpmbuild when run as user. These values can be changed in your local rpm configuration | `zypper source-install PACKAGE_NAME`
| | The above command will also install the build dependencies of the specified package. If you do not want this, add the switch -D | `sudo zypper source-install -D PACKAGE_NAME`
| | To install only the build dependencies use -d. Of course, this will only work if you have the repository with the source packages enabled in your repository list (it is added by default, but not enabled). See Section [2.1.5, “Managing Repositories with Zypper”](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.instrepo) for details on repository management | `sudo zypper source-install -d PACKAGE_NAME`
| | A list of all source packages available in your repositories can be obtained with | `zypper search -t srcpackage`
| | You can also download source packages for all installed packages to a local directory. To download source packages, use the command this command. The default download directory is `/var/cache/zypper/source-download`. You can change it using the `--directory` option. To only show missing or extraneous packages without downloading or deleting anything, use the `--status` option. To delete extraneous source packages, use the `--delete` option. To disable deleting, use the `--no-delete` option| `zypper source-download`


#### Installing Packages from Disabled Repositories [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.softman.pluscontent)

Header | Comments | Command 
------------ | ------------- | -------------
| | Normally you can only install or refresh packages from enabled repositories. The `--plus-content` TAG option helps you specify repositories to be refreshed, temporarily enabled during the current Zypper session, and disabled after it completes.For example, to enable repositories that may provide additional `-debuginfo` or `-debugsource` packages, use `--plus-content debug`. You can specify this option multiple times. To temporarily enable such 'debug' repositories to install a specific `-debuginfo` package, use the option as follows | `sudo zypper --plus-content debug install "debuginfo(build-id)=eb844a5c20c70a59fc693cd1061f851fb7d046f4"`
   
 
#### Utilities [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.softman.util)

Header | Comments | Command 
------------ | ------------- | -------------
| |To verify whether all dependencies are still fulfilled and to repair missing dependencies, use| `zypper verify`
| |In addition to dependencies that must be fulfilled, some packages “recommend” other packages. These recommended packages are only installed if actually available and installable. In case recommended packages were made available after the recommending package has been installed (by adding additional packages or hardware), use the following command. This command is very useful after plugging in a Web cam or Wi-Fi device. It will install drivers for the device and related software, if available. Drivers and related software are only installable if certain hardware dependencies are fulfilled| `sudo zypper install-new-recommends`

#### Updating Software with Zypper [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.softup)

There are three different ways to update software using Zypper: by installing patches, by installing a new version of a package or by updating the entire distribution. The latter is achieved with zypper dist-upgrade. Upgrading openSUSE Leap is discussed in Book “Start-Up”, [Chapter 13 “Upgrading the System and System Changes”](https://doc.opensuse.org/documentation/leap/startup/single-html/book.opensuse.startup/index.html#cha.update.osuse). 

#### Installing All Needed Patches [origin]()

Header | Comments | Command 
------------ | ------------- | -------------
| | To install all officially released patches that apply to your system, run.ll patches available from repositories configured on your computer are checked for their relevance to your installation. If they are relevant (and not classified as optional or feature), they are installed immediately.If a patch that is about to be installed includes changes that require a system reboot, you will be warned before.  | `sudo zypper patch`
| | The plain `zypper patch` command does not apply patches from third party repositories. To update also the third party repositories, use the with-update command option as follows| `sudo zypper patch --with update`
| | To install also optional patches | `sudo zypper patch --with-optional`
| | To install all patches relating to a specific Bugzilla issue | `sudo zypper patch --bugzilla=NUMBER`
| | To install all patches relating to a specific CVE database entry | `sudo zypper patch --cve=NUMBER`
| ex.| Install a security patch with the CVE number CVE-2010-2713 | `sudo zypper patch --cve=CVE-2010-2713`
| ex.| To install only patches which affect Zypper and the package management itself.Bear in mind that other command options that would also update other repositories will be dropped if you use the updatestack-only command option.| `sudo zypper patch --updatestack-only`


#### Listing Patches [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.softup.listpatch)

TODO!

#### Installing New Package Versions [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.softup.update)

Header | Comments | Command 
------------ | ------------- | -------------
| | If a repository contains only new packages, but does not provide patches, zypper patch does not show any effect. To update all installed packages with newer available versions (while maintaining system integrity), use| `sudo zypper update`
| | To update individual packages, specify the package with either the update or install command | `sudo zypper update PACKAGE_NAME`
| | | `sudo zypper install PACKAGE_NAME`
| | A list of all new installable packages can be obtained with the command [1](https://github.com/kinderp/csheet/blob/master/README.md#installing-new-package-versions_1) | `zypper list-updates`
| | A list of all new available packages (regardless whether installable or not) can be obtained with. To find out why a new package cannot be installed, use the zypper install or zypper update command.| `sudo zypper list-updates --all`

#### Identifying Orphaned Packages [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.softup.orphaned)

Header | Comments | Command 
------------ | ------------- | -------------
| | Whenever you remove a repository from Zypper or upgrade your system, some packages can get in an “orphaned” state. These orphaned packages belong to no active repository anymore. The following command gives you a list of these. With this list, you can decide if a package is still needed or can be removed safely | `sudo zypper packages --orphaned` |

#### dentifying Processes and Services Using Deleted Files [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.ps)

TODO!

#### Managing Repositories with Zypper [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.instrepo)

Header | Comments | Command 
------------ | ------------- | -------------
| | All installation or patch commands of Zypper rely on a list of known repositories. To list all repositories known to the system, use the command | `zypper repos`
| | By default, details such as the URI or the priority of the repository are not displayed. Use the following command to list all details [1](https://github.com/kinderp/csheet/blob/master/README.md#managing-repositories-with-zypper_1) | `zypper repos -d`

#### Adding Repositories [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.instrepo.add)


Header | Comments | Command 
------------ | ------------- | -------------
| To add a repository |  URI can either be an Internet repository, a network resource, a directory or a CD or DVD (see [this](http://en.opensuse.org/openSUSE:Libzypp_URIs) for details). The ALIAS is a shorthand and unique identifier of the repository. You can freely choose it, with the only exception that it needs to be unique. Zypper will issue a warning if you specify an alias that is already in use.
 | `sudo zypper addrepo URI ALIAS`
 
 #### Refreshing Repositories [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.instrepo.refresh)
 
 Header | Comments | Command 
------------ | ------------- | -------------
 |  | zypper enables you to fetch changes in packages from configured repositories. To fetch the changes, run | `sudo zypper refresh` |
 |  | The refresh command enables you to view changes also in disabled repositories, by using the `--plus-content` option. This option fetches changes in repositories, but keeps the disabled repositories in the same state—disabled | `sudo zypper --plus-content refresh`
 
 ##### Removing Repositories [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.instrepo.rm)
 
 Header | Comments | Command 
------------ | ------------- | -------------
 | | To remove a repository from the list, use the command zypper removerepo together with the alias or number of the repository you want to delete. For example, to remove the repository Leap-42.3-NOSS from Example 2.1, [“Zypper—List of Known Repositories”](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#ex.zypper.repos), use one of the following commands | `sudo zypper removerepo 4` |
 | | | `sudo zypper removerepo "Leap-42.3-NOSS"`|
 

#### Modifying Repositories [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.instrepo.mofify)

Header | Comments | Command 
------------ | ------------- | -------------
Enable or disable repositories with zypper modifyrepo | You can also alter the repository's properties (such as refreshing behavior, name or priority) with this command. The following command will enable the repository named updates, turn on auto-refresh and set its priority to 20 | `sudo zypper modifyrepo -er -p 20 'updates'`
| Modifying repositories is not limited to a single repository—you can also operate on groups | `-a: all repositories` `-l: local repositories` `-t: remote repositories` `-m TYPE: repositories of a certain type (where TYPE can be one of the following: http, https, ftp, cd, dvd, dir, file, cifs, smb, nfs, hd, iso) ` | | 
| To rename a repository alias, use the `renamerepo` command | The following example changes the alias from Mozilla Firefox to firefox | `sudo zypper renamerepo 'Mozilla Firefox' firefox`

#### Querying Repositories and Packages with Zypper [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.query)

Header | Comments | Command 
------------ | ------------- | -------------
| Zypper offers various methods to query repositories or packages. To get lists of all products, patterns, packages or patches available, use the following commands | To query all repositories for certain packages, use `search`. To get information regarding particular packages, use the `info` command | `zypper products` `zypper patterns` `zypper packages` `zypper patches`

#### Searching for Software [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.query.search)

Header | Comments | Command 
------------ | ------------- | -------------
| The zypper search command works on package names, or, optionally, on package summaries and descriptions | Strings wrapped in / are interpreted as regular expressions. By default, the search is not case-sensitive | |
| | Simple search for a package name containing fire | `zypper search "fire"`|
| | Simple search for the exact package MozillaFirefox | `zypper search --match-exact "MozillaFirefox"`
| | Also search in package descriptions and summaries | `zypper search -d fire`
| | Only display packages not already installed | `zypper search -u fire`
| | Display packages containing the string fir not followed be e | `zypper se "/fir[^e]/"`

#### Searching for Specific Capability [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.query.what-provides)

Header | Comments | Command 
------------ | ------------- | -------------
| To search for packages which provide a special capability, use the command `what-provides` [1](https://github.com/kinderp/csheet/blob/master/README.md#searching-for-specific-capability_1) | For example, if you want to know which package provides the Perl module SVN::Core, use the following command | `zypper what-provides 'perl(SVN::Core)'`


#### Showing Package Information [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.query.info)

Header | Comments | Command 
------------ | ------------- | -------------
| To query single packages, use `info` with an exact package name as an argument. This displays detailed information about a package. | In case the package name does not match any package name from repositories, the command outputs detailed information for non-package matches. If you request a specific type (by using the -t option) and the type does not exist, the command outputs other available matches but without detailed information. If you specify a source package, the command displays binary packages built from the source package. If you specify a binary package, the command outputs the source packages used to build the binary package. To also show what is required/recommended by the package, use the options `--requires` and `--recommends` | `zypper info --requires MozillaFirefox`
 
#### Configuring Zypper [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.configure)

Zypper now comes with a configuration file, allowing you to permanently change Zypper's behavior (either system-wide or user-specific)

Header | Comments | Command 
------------ | ------------- | -------------
For system-wide changes, edit | | `/etc/zypp/zypper.conf` |
For user-specific changes, edit | If `~/.zypper.conf` does not yet exist, you can use `/etc/zypp/zypper.conf` as a template: copy it to `~/.zypper.conf` and adjust it to your liking. Refer to the comments in the file for help about the available options.| `~/.zypper.conf` |

#### Troubleshooting [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.trouble)

Header | Comments | Command 
------------ | ------------- | -------------
| Refreshing the repositories | If you have trouble accessing packages from configured repositories (for example, Zypper cannot find a certain package even though you know it exists in one the repositories), refreshing the repositories may help | `sudo zypper refresh`
| Complete refresh and rebuild of the database | If that does not help, try to force a complete refresh and rebuild of the database, including a forced download of raw metadata. This forces a complete refresh and rebuild of the database, including a forced download of raw metadata. | `sudo zypper refresh -fdb`


#### Zypper Rollback Feature on Btrfs File System [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.rollback)

If the Btrfs file system is used on the root partition and snapper is installed, Zypper automatically calls snapper when committing changes to the file system to create appropriate file system snapshots. These snapshots can be used to revert any changes made by Zypper. See Chapter 3, [System Recovery and Snapshot Management with Snapper](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#cha.snapper) for more information. 

#### For More Information [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.more)

For more information on managing software from the command line, enter zypper help, zypper help  COMMAND or refer to the zypper(8) man page. For a complete and detailed command reference, cheat sheets with the most important commands, and information on how to use Zypper in scripts and applications, refer to [link](http://en.opensuse.org/SDB:Zypper_usage). A list of software changes for the latest openSUSE Leap version can be found at [link](http://en.opensuse.org/openSUSE:Zypper) versions.

# Notes

###### Installing-New-Package-Versions_1
 
 Note that this command only lists packages that match the following criteria

* has the same vendor like the already installed package,
* is provided by repositories with at least the same priority than the already installed package,
* is installable (all dependencies are satisfied). 

###### Managing-Repositories-with-Zypper_1
The result will look similar to the following output
```
zypper repos
#  | Alias                 | Name             | Enabled | GPG Check | Refresh
---+-----------------------+------------------+---------+-----------+--------
 1 | Leap-42.3-Main        | Main (OSS)       | Yes     | (r ) Yes  | Yes
 2 | Leap-42.3-Update      | Update (OSS)     | Yes     | (r ) Yes  | Yes
 3 | Leap-42.3-NOSS        | Main (NON-OSS)   | Yes     | (r ) Yes  | Yes
 4 | Leap-42.3-Update-NOSS | Update (NON-OSS) | Yes     | (r ) Yes  | Yes
[...]
```
When specifying repositories in various commands, an alias, URI or repository number from the zypper repos command output can be used. A repository alias is a short version of the repository name for use in repository handling commands. Note that the repository numbers can change after modifying the list of repositories. The alias will never change by itself

###### Searching-for-Specific-Capability_1

The what-provides PACKAGE_NAME is similar to rpm -q --whatprovides PACKAGE_NAME, but RPM is only able to query the RPM database (that is the database of all installed packages). Zypper, on the other hand, will tell you about providers of the capability from any repository, not only those that are installed
