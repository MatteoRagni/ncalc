---
layout: post
title:  "Installazione VM"
date:   2015-02-06 10:01:00
categories: post
permalink: /lecture00/
lecture: "Virtual Machine"
---

In questo post le istruzioni per installare la virtual machine.

* table of contents.
{:toc}

## Installazione Virtual Machine

<style>
.thumbsvm { height: 100px; }
</style>

Il centro di calcolo mette a disposizione una virtual machine per gli studenti del Dipartimento di Ingegneria Industriale, con una virtual machine installata e il software pronto per essere utilizzato (o registrato con licenza campus).

Per questo corso, non avremo bisogno di nessun sotware con licenza, ma dovremo utilizzare la virtual machine e la distribuzione linux in essa installata.

| **Link**         | [AulaVirtuale.zip (6.05GB)][link_zip] |
| **username**     | `studente` |
| **password**     | `studente` |
| **note**         | Per poter scaricare la VM dovete essere collegati alla rete di Ateneo |
| **Checksums**    | Hashes generati il 4 Marzo 2015 ([cosa sono?][digest]) |
| _CRC32_          | `46fc6a2f` |
| _MD5_            | `b54047dc48eb8ba2493cf9f0972a9dac` |
| _SHA_            | `1675d39f267f69b53623feaedf0a29121bef6035` |
| _SHA256_         | `ae6d9c50d489cdfc1fc090d9b6c2fabd157551e59349011706cf3be9a56f5f79` |

La VM è di tipo VMWare, potete utilizzarla (su WIndows e Linux) sfruttando [VMWare Player][vmplay], di cui esiste una versione base senza licenza, oppure le versioni con licenza di gestori di VM VMWare (Workstation, Player Pro). Per OS-X esiste [VMWare Fusion][vmfus].

> La VM è stata creata con la versione 7 della piattaforma di gestione Virtual Machine di VMWare, unica versione a disposizione dell'Università. La VM non è compatibile con la versione 6 del player. Se avete la versione 6 **dovete aggiornare il vostro software**.

Le virtual machine (e in particolare i dischi di tali `vmdk`) sono compatibili con [Oracle VirtualBox][vbox].

> La compatibilità con VirtualBox è state **testata**. Per caricare la VM, creare in VirtualBox una **nuova** VM per host Debian-64bit. Durante il processo di creazione, alla richiesta di quale HDD utilizzare per la VM, invece di crearne uno nuovo, mettere la spunta su **utilizza hard disk esistente** e caricare il file **AulaVirtuale.vmdk** come HDD.

Per eventuali istruzioni su come intallare questi software, fate riferimento alle guide specifiche del prodotto. Vedremo di seguito come installare questa VM su sistemi operativi diversi. Il file scaricato in versione zip deve essere estratto con un gestore di archivi (come [7zip][7zip] o altri)

### Windows

<a href="../assets/img/vm/win/win1.PNG" data-lightbox="windows" data-title="Cliccate su Open a Virtual Machine"><img src="../assets/img/vm/win/win1.PNG" class="thumbsvm"></a>
<a href="../assets/img/vm/win/win2.PNG" data-lightbox="windows" data-title="Andate nella directory dove avete estratto aula virtuale, selezionate il file AulaVirtuale.vmx"><img src="../assets/img/vm/win/win2.PNG" class="thumbsvm"></a>
<a href="../assets/img/vm/win/win3.PNG" data-lightbox="windows" data-title="Cliccate su Play Virtual Machine"><img src="../assets/img/vm/win/win3.PNG" class="thumbsvm"></a>
<a href="../assets/img/vm/win/win4.PNG" data-lightbox="windows" data-title="Al primo avvio vi chiederà dell'origine della VM. Cliccate su I copied it"><img src="../assets/img/vm/win/win4.PNG" class="thumbsvm"></a>
<a href="../assets/img/vm/win/win5.PNG" data-lightbox="windows" data-title="Vi chiederà di installare dei tools aggiuntivi, che sono molto utili"><img src="../assets/img/vm/win/win5.PNG" class="thumbsvm"></a>
<a href="../assets/img/vm/win/win6.PNG" data-lightbox="windows" data-title="L'installazione durerà qualche minuto"><img src="../assets/img/vm/win/win6.PNG" class="thumbsvm"></a>
<a href="../assets/img/vm/win/win7.PNG" data-lightbox="windows" data-title="Aspettate l'avvio della VM"><img src="../assets/img/vm/win/win7.PNG" class="thumbsvm"></a>
<a href="../assets/img/vm/win/win8.PNG" data-lightbox="windows" data-title="La password è studente (uguale allo username)"><img src="../assets/img/vm/win/win8.PNG" class="thumbsvm"></a>
<a href="../assets/img/vm/win/win9.PNG" data-lightbox="windows" data-title="E il gioco è fatto"><img src="../assets/img/vm/win/win9.PNG" class="thumbsvm"></a>

### Linux

<a href="../assets/img/vm/linux/linux1.png" data-lightbox="linux" data-title="Cliccate su Open a Virtual Machine"><img src="../assets/img/vm/linux/linux1.png" class="thumbsvm"></a>
<a href="../assets/img/vm/linux/linux2.png" data-lightbox="linux" data-title="Andate nella directory dove avete estratto aula virtuale, selezionate il file AulaVirtuale.vmx"><img src="../assets/img/vm/linux/linux2.png" class="thumbsvm"></a>
<a href="../assets/img/vm/linux/linux3.png" data-lightbox="linux" data-title="Cliccate su Play Virtual Machine. Al primo avvio vi chiederà dell'origine della VM. Cliccate su I copied it."><img src="../assets/img/vm/linux/linux3.png" class="thumbsvm"></a>
<a href="../assets/img/vm/linux/linux4.png" data-lightbox="linux" data-title="Aspettate l'avvio della virtual machine"><img src="../assets/img/vm/linux/linux4.png" class="thumbsvm"></a>
<a href="../assets/img/vm/linux/linux5.png" data-lightbox="linux" data-title="La password è studente, come l'username"><img src="../assets/img/vm/linux/linux5.png" class="thumbsvm"></a>
<a href="../assets/img/vm/linux/linux6.png" data-lightbox="linux" data-title="E il gioco è fatto!"><img src="../assets/img/vm/linux/linux6.png" class="thumbsvm"></a>

### OS-X

<a href="../assets/img/vm/mac/mac1.png" data-lightbox="mac" data-title="Cliccate su Open a Virtual Machine"><img src="../assets/img/vm/mac/mac1.png" class="thumbsvm"></a>
<a href="../assets/img/vm/mac/mac2.png" data-lightbox="mac" data-title="Andate nella directory dove avete estratto aula virtuale, selezionate il file AulaVirtuale.vmx"><img src="../assets/img/vm/mac/mac2.png" class="thumbsvm"></a>
<a href="../assets/img/vm/mac/mac3.png" data-lightbox="mac" data-title="Cliccate su Play Virtual Machine. Al primo avvio vi chiederà dell'origine della VM. Cliccate su I copied it."><img src="../assets/img/vm/mac/mac3.png" class="thumbsvm"></a>
<a href="../assets/img/vm/mac/mac4.png" data-lightbox="mac" data-title="Aspettate l'avvio della virtual machine"><img src="../assets/img/vm/mac/mac4.png" class="thumbsvm"></a>
<a href="../assets/img/vm/mac/mac5.png" data-lightbox="mac" data-title="La password è studente, come l'username"><img src="../assets/img/vm/mac/mac5.png" class="thumbsvm"></a>
<a href="../assets/img/vm/mac/mac6.png" data-lightbox="mac" data-title="E il gioco è fatto!"><img src="../assets/img/vm/mac/mac6.png" class="thumbsvm"></a>

## VirtualBox

Le immagine sono tratte da OSX, ma sono valide per tutti i sistemi operativi.

<a href="../assets/img/vm/vb/vb1.png" data-lightbox="virtualbox" data-title="Scaricate e estraete la VM. Dovete conoscere con esattezza la posizione del file AulaVirtuale.vmdk"><img src="../assets/img/vm/vb/vb1.png" class="thumbsvm"></a>
<a href="../assets/img/vm/vb/vb2.png" data-lightbox="virtualbox" data-title="Aprite VirtualBox e cliccate su New. Create una nuova virtual machine con le caratteristiche mostrate nelle immagini"><img src="../assets/img/vm/vb/vb2.png" class="thumbsvm"></a>
<a href="../assets/img/vm/vb/vb3.png" data-lightbox="virtualbox" data-title="Impostate la RAM a disposizione della VM (almeno 512MB)"><img src="../assets/img/vm/vb/vb3.png" class="thumbsvm"></a>
<a href="../assets/img/vm/vb/vb4.png" data-lightbox="virtualbox" data-title="Alla richiesta dell'HDD, selezionate 'Use an existing virtual hard drive'"><img src="../assets/img/vm/vb/vb4.png" class="thumbsvm"></a>
<a href="../assets/img/vm/vb/vb5.png" data-lightbox="virtualbox" data-title="Cercate nel vostro file system il file AulaVirtuale.vmdk identificato al passo 1"><img src="../assets/img/vm/vb/vb5.png" class="thumbsvm"></a>
<a href="../assets/img/vm/vb/vb6.png" data-lightbox="virtualbox" data-title="Create la virtual machine"><img src="../assets/img/vm/vb/vb6.png" class="thumbsvm"></a>
<a href="../assets/img/vm/vb/vb7.png" data-lightbox="virtualbox" data-title="La virtual Machine è pronta. Avviamola"><img src="../assets/img/vm/vb/vb7.png" class="thumbsvm"></a>
<a href="../assets/img/vm/vb/vb8.png" data-lightbox="virtualbox" data-title="E il gioco è fatto"><img src="../assets/img/vm/vb/vb8.png" class="thumbsvm"></a>



[vmplay]: http://www.vmware.com/products/player/
[vmfus]: http://www.vmware.com/products/fusion/
[vbox]: https://www.virtualbox.org/
[7zip]: http://www.7-zip.org/
[link_zip]: http://distrib.ing.unitn.it/vm/AulaVirtuale.zip
[digest]: http://en.wikipedia.org/wiki/File_verification