# csheet

# OpenSUSE

## Yast

### Definition of Terms [origin](https://doc.opensuse.org/documentation/leap/startup/single-html/book.opensuse.startup/index.html#sec.onlineupdate.terms)

I termini seguenti sono importanti per comprendere l'installazione e la rimozione del software in OpenSUSE LEAP
> The following terms are important for understanding installing and removing software in openSUSE Leap.

#### Repository

Una directory locale o remote contenente pacchetti, più informazioni addizinali circa questi pacchetti (metadati dei pacchetti)
>    A local or remote directory containing packages, plus additional information about these packages (package metadata). 

#### (Repository) Alias/Repository Name

Un nome breve per un repository (chiamato Alias in Zypper e Repository Name in YaST). 
Esso può essere scelto dall'utente durante l'aggiunta del repository e deve essere unico.
>    A short name for a repository (called Alias within Zypper and Repository Name within YaST). 
>    It can be chosen by the user when adding a repository and must be unique. 

#### Repository Description Files

Ciascun repository fornisce files descriventi il contenuto del repository (package names, versions, etc.)
Questi files di descrizione del repository sono scaricati in una cache local che è usata da YaST.
>    Each repository provides files describing content of the repository (package names, versions, etc.). 
>    These repository description files are downloaded to a local cache that is used by YaST. 

#### Product

Rappresenta l'intero prodotto, per esempio OpenSUSE Leap.
>   Represents a whole product, for example openSUSE® Leap. 

#### Pattern

Un pattern è un gruppo di pacchetti installabili dedicato ad un certo scopo. 
Per esempio, il pattern Laptop contiene tutti i pacchetti che sono necessari in un ambiente di elaborazione mobile.
I pattern definiscono le dipendenze dei pacchetti (ad esempio i pacchetti necessari e raccomandati) e vengono con una preselezione di pacchetti segnati per l'installazione.
Questo assicura che i pacchetti più importanti necessari per un certo scopo siano disponibili sul tuo sistema dopo l'installazione del pattern
Se è necessario, puoi selezionare e deselezionare pacchetti all'interno del pattern.
>    A pattern is an installable group of packages dedicated to a certain purpose. 
>    For example, the Laptop pattern contains all packages that are needed in a mobile computing environment. 
>    Patterns define package dependencies (such as required or recommended packages) and come with a preselection of packages marked for installation.
>    This ensures that the most important packages needed for a certain purpose are available on your system after installation of the pattern. 
>    If necessary, you can manually select or deselect packages within a pattern. 

#### Package

Un pacchetto è un file compresso in formato rpm che contiene i file per un particolare programma
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
Zypper Commands| CThe simplest way to execute Zypper is to type its name, followed by a command. For example, to apply all needed patches to the system|     sudo zypper patch
Global Options | Additionally, you can choose from one or more global options by typing them immediately before the command. the option --non-interactive means that the command is run without asking anything (automatically applying the default answers).  | sudo zypper --non-interactive patch
Command-Specific Options | To use options that are specific to a particular command, type them immediately after the command. --auto-agree-with-licenses is used to apply all needed patches to a system without you being asked to confirm any licenses. Instead, license will be accepted automatically | sudo zypper patch --auto-agree-with-licenses
Arguments | Some commands require one or more arguments. For example, when using the command install, you need to specify which package or which packages you want to install | sudo zypper install mplayer
Arguments | Some options also require a single argument. The following command will list all known patterns | zypper search -t pattern 


#### Installing and Removing Software with Zypper [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.softman)

Header | Comments | Command 
------------ | ------------- | -------------
| | To install | sudo zypper install PACKAGE_NAME
| | To remove | sudo zypper remove PACKAGE_NAME
 
 #### Selecting Which Packages to Install or Remove [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.selectpackage)
 
There are various ways to address packages with the commands zypper install and zypper remove

Header | Comments | Command 
------------ | ------------- | -------------
By Exact Package Name | | sudo zypper install MozillaFirefox
By Exact Package Name and Version Number | | sudo zypper install MozillaFirefox-52.2
By Repository Alias and Package Name | | sudo zypper install mozilla:MozillaFirefox
By Package Name Using Wild Cards | You can select all packages that have names starting or ending with a certain string. Use wild cards with care, especially when removing packages. The following command will install all packages starting with “Moz”:| sudo zypper install 'Moz*'
Removing all -debuginfo Packages | When debugging a problem, you sometimes need to temporarily install a lot of -debuginfo packages which give you more information about running processes. After your debugging session finishes and you need to clean the environment, run the following | sudo zypper remove '*-debuginfo'
By Capability | For example, to install a package without knowing its name, capabilities come in handy. The following command will install the package MozillaFirefox | sudo zypper install firefox
By Capability, Hardware Architecture, or Version |  Together with a capability, you can specify a hardware architecture and a version | |
 | The name of the desired hardware architecture is appended to the capability after a full stop. For example, to specify the AMD64/Intel 64 architectures (which in Zypper is named x86_64), use | sudo zypper install 'firefox.x86_64'
 | Versions must be appended to the end of the string and must be preceded by an operator: < (lesser than), <= (lesser than or equal), = (equal), >= (greater than or equal), > (greater than).| sudo zypper install 'firefox>=52.2'
 | You can also combine a hardware architecture and version requirement | udo zypper install 'firefox.x86_64>=52.2'
By Path to the RPM file | You can also specify a local or remote path to a package | sudo zypper install /tmp/install/MozillaFirefox.rpm | sudo zypper install http://download.example.com/MozillaFirefox.rpm

#### Combining Installation and Removal of Packages [origin](https://doc.opensuse.org/documentation/leap/reference/single-html/book.opensuse.reference/index.html#sec.zypper.combineinstall)

Header | Comments | Command 
------------ | ------------- | -------------
| | To install and remove packages simultaneously, use the +/- modifiers. To install emacs and simultaneously remove vim , use | sudo zypper install emacs -vim
| | To remove emacs and simultaneously install vim , use | sudo zypper remove emacs +vim
| | To prevent the package name starting with the - being interpreted as a command option, always use it as the second argument. If this is not possible, precede it with -- | sudo zypper install -emacs +vim       # Wrong sudo zypper install vim -emacs       # Correct sudo zypper install -- -emacs +vim    # Correct sudo zypper remove emacs +vim         # Correct
