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
Zypper Commands| The simplest way to execute Zypper is to type its name, followed by a command. For example, to apply all needed patches to the system|     `sudo zypper patch`
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
