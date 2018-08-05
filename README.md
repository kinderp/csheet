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
