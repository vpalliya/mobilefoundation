---

copyright:
  years: 2018, 2019
lastupdated: "2018-10-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}

# Offusca le risorse
{: #obfuscate_resources}

L'offuscamento è il processo di modifica di un eseguibile in modo che non sia più utile a un hacker ma che rimanga pienamente operativo. L'offuscamento del codice automatizzato rende difficile deingegnerizzare un programma. 

Mediante l'offuscamento, la deingegnerizzazione di un'applicazione diventa più difficile ed è inoltre protetta dal furto di segreti commerciali (proprietà intellettuale), dall'accesso non autorizzato, dal tralasciamento delle licenze o di altri controlli e da vulnerabilità.

L'offuscamento del codice consiste in molte tecniche differenti e molte tecniche di sicurezza dell'applicazione.

* Offuscamento mediante rinominazione - la rinominazione altera il nome di metodi e variabili e rende il codice sorgente decompilato di più difficile comprensione per gli esseri umani ma non modifica l'esecuzione dell'applicazione. Il metodo di offuscamento preferito dagli obfuscator NET, iOS, Java e Android. 
* Crittografia delle stringhe
* Offuscamento del flusso di controllo
* Trasformazione del modello di istruzioni
* Inserimento di codice fittizio
* Antimanomissione ecc.

Con l'offuscamento, è più difficile per gli utenti malintenzionati l'esame del codice e l'analisi dell'applicazione. Per l'offuscamento, sono disponibili diversi strumenti di terze parti.

* Per l'offuscamento di un'applicazione android, fai riferimento a questo [blog](https://mobilefirstplatform.ibmcloud.com/blog/2016/09/19/mfp-80-obfuscating-android-code-with-proguard/).
    >**Nota**: devi creare il file di configurazione (proguard-project.txt) per l'offuscamento Android ProGuard con un'applicazione MobileFirst Android.

* Per l'offuscamento di base dell'applicazione Cordova, fai riferimento alla sezione relativa alla [crittografia dell'applicazione Cordova](#encryptingcordovapackage).

## Crittografia delle risorse web dei tuoi pacchetti Cordova
{: #encryptingcordovapackage}

Per ridurre al minimo il rischio che qualcuno visualizzi o modifichi le tue risorse web mentre si trovano nei pacchetti ``.apk`` o ``.ipa``, puoi utilizzare il comando mfpdev app webencrypt della CLI MobileFirst oppure l'indicatore mfpwebencrypt per crittografare le informazioni. Questa procedura non fornisce una crittografia impossibile da risolvere ma fornisce un livello di offuscamento di base.

**Prerequisiti**:

* Devi avere gli strumenti di sviluppo Cordova installati. Questo esempio utilizza la CLI Apache Cordova. Se utilizzi altri strumenti di sviluppo Cordova, alcuni dei passi saranno differenti. Fai riferimento alla tua documentazione dello strumento Cordova per le istruzioni.
* Devi avere la CLI MobileFirst installata.
* Devi avere il plug-in MobileFirst Cordova installato.

Il momento migliore per completare questa procedura è dopo che hai terminato il tuo sviluppo dell'applicazione e sei pronto a distribuirla. Se esegui qualcuno dei seguenti comandi dopo che hai completato la procedura di crittografia delle risorse web, il contenuto che era stato crittografato viene decrittografato:

* cordova prepare
* cordova build
* cordova run
* cordova emulate
* mfpdev app webupdate
* mfpdev app preview

Se esegui uno dei comandi elencati dopo che hai crittografato le risorse web, devi completare nuovamente questa procedura per crittografare le risorse web.

1. Apri una finestra del terminale e vai alla directory root dell'applicazione Cordova che desideri crittografare.
2. Prepara l'applicazione immettendo uno dei seguenti comandi:
    * ``cordova prepare``
    * ``mfpdev app webupdate
``
3. Completa una delle seguenti procedure per crittografare il contenuto:
    * Immetti il seguente comando: ``mfpdev app webencrypt``.
        >**Suggerimento**: puoi visualizzare le informazioni sul comando ``mfpdev app webencrypt`` immettendo ``mfpdev help app webencrypt``.
    * Puoi anche crittografare le risorse web dei tuoi pacchetti Cordova aggiungendo l'indicatore ``mfpwebencrypt`` al comando ``cordova compile`` o al comando ``cordova build`` quando crei i tuoi pacchetti.
       * ``cordova compile -- --mfpwebencrypt`` | ``cordova build -- --mfpwebencrypt``
            Le informazioni sul sistema operativo nella cartella **www** vengono sostituite da un file **resources.zip** che contiene il contenuto crittografato.
            Se la tua applicazione è per il sistema operativo Android e il file **resources.zip** è più grande di 1 MB, il file **resources.zip** viene diviso in file .zip da 768 KB più piccoli denominati **resources.zip.nnn**. La variabile nnn è un numero da 001 a 999.
4. Verifica l'applicazione con le risorse crittografate utilizzando l'emulatore fornito con gli strumenti specifici per la piattaforma. Ad esempio, puoi utilizzare l'emulatore in Android Studio per Android o Xcode per iOS.

>**Nota**: non utilizzare i seguenti comandi Cordova per verificare l'applicazione dopo che l'hai crittografata.

>* ``cordova run``
>* ``cordova emulate``

>Questi comandi aggiornano il contenuto che era stato crittografato nella cartella www e lo salvano nuovamente come contenuto decrittografato. Se utilizzi questi comandi, ricordati di completare nuovamente la procedura per rieseguirne la crittografia prima di pubblicare l'applicazione.