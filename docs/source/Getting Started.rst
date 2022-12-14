Getting Started
=====

**Mini/Lite**
----

1. COM1 ( Console 115200 8/n/1)
2. Gigabit Ethernet (eth0)
3. Gigabit Ethernet (eth1)
4. Gigabit Ethernet (eth2)
5. USB 2.0
6. Power (12v, 1A)

Prima installazione
++++

- Collegate KalliopePBX alla vostra rete utilizzando l’interfaccia eth0
- Opzionale: collegate la porta seriale COM1 di KalliopePBX al vostro PC usando un cavo seriale (non incluso - impostazioni: 115200 8/n/1)
- Collegate l’alimentatore incluso a KalliopePBX e successivamente collegate l’alimentatore ad una presa di corrente (100-240V AC, 50-60 Hz). KalliopePBX si avvia automaticamente
- Puntate il vostro browser all’indirizzo http://192.168.0.100:10080 per effettuare la prima registrazione. È richiesto l’accesso da parte di KalliopePBX all’indirizzo https://license.kalliopepbx.it; la configurazione di rete può essere modificata attraverso il menu “Impostazioni” ). Nel caso compaia l'errore **UNSAFE_PORT** seguire questa procedura *(Clicca qui)*.
- Dopo la registrazione, installate il firmware desiderato tra quelli disponibili. È richiesto l’accesso da parte di KalliopePBX all’indirizzo https://updates.kalliopepbx.it. Il processo può richiedere alcuni minuti, in base alla dimensione del firmware e della velocità di download della vostra rete
- Seguite il progresso dell’installazione firmware; al termine, riavviate KalliopePBX ed accedete all’interfaccia di configurazione puntando il vostro browser all’indirizzo http://<Configured_ip> (porta standard http 80). Le credenziali di default per l'accesso sono: admin/admin.


**V4R/V4R+**
-----

KalliopePBX v4 Rackmount (Hw rev. 3)
++++
Gli apparati KalliopePBX v4 rackmount (nelle diverse varianti -R, -R+, -R-OPT-FO e -R-OPT-FO+) in hw rev. 3 sono basati su una piattaforma hardware headless che mette a disposizione:

- una interfaccia di rete Gigabit Ethernet equipaggiata con uno switch hardware 8 porte, tutte Gigabit Ethernet autosensing (ETH0)
- due interfacce di rete Gigabit Ethernet (ciascuna dual mode RJ45 e SFP 1GbE) a porta singola (ETH1 e ETH2).

  - **NOTA**: in caso di utilizzo di GBIC nello slot SFP di una di queste interfacce, se viene lasciato inserito il cavo di rete nella porta RJ45, quest'ultima avrà la precedenza.
  - **NOTA 2**: nel caso di utilizzo di GBIC 100 Mbps, il sistema non le riconosce in automatico ed è necessaria un'operazione di abilitazione da parte del nostro supporto tecnico.
  
Una volta collegato l'apparato tramite l'alimentatore in dotazione, il sistema si avvia in automatico ed entro pochi secondi sarà possibile accedere al KalliopePBX.

Il primo accesso a KalliopePBX avviene tramite una delle porte switch dell'interfaccia ETH0, puntando il browser all'indirizzo predefinito http://192.168.0.100:10080.

**NOTA**: Alcuni browser hanno iniziato a bloccare per impostazione predefinita l'accesso a pagine su porte diverse da quelle standard. In caso di visualizzazione di un errore che indica "ERR_UNSAFE_PORT", è necessario effettuare lo sblocco della porta 10080, mediante la procedura indicata alla pagina *Gestione errore ERR_UNSAFE_PORT*

Come per le VM e gli altri apparati fisici, è possibile modificare l'indirizzo IP di KalliopePBX collegando all'interfaccia ETH0 un PC configurato con un indirizzo IP sulla subnet 192.168.0.0/24 e accedendo al pannello "Impostazioni di rete" dal menu Strumenti, accessibile in alto a destra della GUI di Kalliope.

In alternativa, è possibile accedere alla console di KalliopePBX (operativa solo in modalità "recovery" o "console di ripristino", in cui il sistema è avviato quindi su bootloader e non su un firmware) e effettuare la configurazione utilizzando la CLI integrata (a cui si accede con le credenziali predefinite manager/manager). A differenza delle precedenti versioni hardware, l'accesso alla console di KalliopePBX non avviene direttamente tramite la porta seriale presente sull'apparato, ma tramite il servizio VNC.

In questa revision hardware, difatti, KalliopePBX gira come macchina virtuale all'interno di un ambiente di virtualizzazione basato su KVM. L'accesso a KalliopePBX è quindi mediato dal sistema operativo nativo che gira sull'apparato fisico, tramite il quale è possibile effettuare alcune semplici operazioni di configurazione, come dettagliato di seguito.

Nel caso sia possibile accedere all'interfaccia web di KalliopePBX con le impostazioni di rete predefinite (192.168.0.100/24), la procedura di prima attivazione segue quella standard comune alle altre versioni, ed è composta dai seguenti passi:

1. Configurazione dell'indirizzo IP, default gateway e DNS tramite web GUI e nuovo accesso al nuovo indirizzo IP assegnato. Verifica della corretta impostazione data/ora e eventuale sincronizzazione forzata usando i server NTP di sistema (o quelli personali eventualmente configurati).
2. Attivazione della licenza della VM KalliopePBX. In questo caso, a differenza delle VM tradizionali, non è necessario inserire una chiave di attivazione perché questa sarà disponibile a bordo dell'apparato, pertanto l'attivazione consiste solamente nel premere il corrispondente pulsante dall'interfaccia web
3. Registrazione del prodotto. Analogamente agli altri sistemi Kalliope, questa operazione sblocca la possibilità di procedere con l'installazione dei firmware, e determina l'inizio del periodo previsto per la garanzia sull'apparato e per l'accesso agli aggiornamenti
4. Aggiornamento bootloader, se necessario, ed installazione firmware. Al termine dell'installazione firmware sarà necessario effettuare il riavvio da GUI di KalliopePBX e, terminato il boot, verrà automaticamente effettuata la redirezione verso la pagina di login (su porta standard 80)

Nel caso in cui non sia possibile effettuare l'accesso all'IP predefinito 192.168.0.100 e si debba o voglia procedere con la sua modifica utilizzando la CLI di KalliopePBX, è necessario comunque avere accesso al sistema operativo nativo dell'apparato, per poter configurare l'accesso VNC alla console di KalliopePBX. Nello specifico, una volta effettuata la configurazione di un IP al sistema operativo nativo, in base alle indicazioni presenti nella sezione successiva, è sufficiente avviare un client VNC (es. TightVNC Viewer) configurando la connessione verso l'host <IP_OS_nativo:5900>, per ottenere accesso alla CLI di KalliopePBX su cui poter effettuare login (utilizzando l'utente cablato manager/manager)

Accesso al sistema operativo nativo ATOS dell'apparato
++++
L'accesso al sistema operativo nativo dell'apparato (ATOS) può essere necessario per configurarne le impostazioni di rete al fine di poter accedere tramite VNC alla console di KalliopePBX, oltre che per poter effettuare, laddove necessario, l'arresto forzato e il riavvio di KalliopePBX.

L'accesso ad ATOS può avvenire tramite la porta seriale ("Console") presente sul fronte del dispositivo (con impostazioni 115200/8/N/1), oppure mediante accesso ssh. In modo simile a quanto avviene con i sistemi di gestione fuori banda di molti server (iLO per HP, DRAC per Dell, ecc.) ATOS ha un proprio stack di rete, che per impostazione predefinita è configurato come DHCP client sull'interfaccia ETH0 (con un MAC della famiglia 00:D0:D6:xx:xx:xx, come riportato sull'etichetta presente sull'apparato).

Le credenziali di accesso sono riportate sull'etichetta presente sull'apparato. L'utente è "manager" e la password è univocamente assegnata a ciascun apparato (in seguito modificabile previo accesso ad ATOS).

**NOTA**: questo utente manager non ha alcun legame con l'utente manager che si utilizza per accedere alla CLI di Kalliope in modalità bootloader.

Una volta effettuata la connessione tramite console seriale, o tramite ssh (qualora si conosca l'IP acquisito da ATOS, ad esempio grazie ai log del server DCP eventualmente presente nella rete), si procede con il login usando l'utente "manager" e la password riportata sull'etichetta presente sull'apparato:

.. code-block:: console

   login as: manager
   manager@192.168.23.60's password: *******
   ATOSNT Remote CLI

   CTRL+d to exit

   Init Command Line Interface...
   ATOS Version: 7.2.7 (mcccfvitbkovsc)
   ATOS Date: 06/10/2022 13:34
   ATOS License: NFVSBC
   Hardware: XV8800 - 4C8R120D - 2518D
   Product Code: 708190501
   Serial Number: xxxxxx
   MAC Address: 00:D0:D6:xx:xx:xx
   BARCODE: AE70819050110204xxxxxx

   User name :manager
   Password :*******
   <manager> logged at MANAGER level
   KPBXv4_kvm>  
   
Digitando "?" seguito dal tasto invio, il sistema presenta le voci di configurazione ed i comandi disponibili:

.. code-block:: console

   KPBXv4_kvm>?

   Available nodes:
                           system
                           interfaces
                           dns
                           nfv
   Available commands:
   up                      Move one step up from the current node
   top                     Back to the root of the tree
   quit                    Exit from CLI session
   set                     Set node options
   add                     Add a new option
   del                     Remove an added option
   show                    Show 'KPBXv4_kvm' settings
   help                    Help of item
   info                    Show the system informations
   date                    Show or setting system date and time
   save                    Save configuration data
   restart                 Restart device
   ping                    Send an ICMP ECHO request
   tracert                 Display a trace of packet
   show-logging-level      Show logged level

   password                Set user/others password on node KPBXv4_kvm\system>>


Di seguito si riportano i comandi di visualizzazione delle impostazioni correnti, seguite poi dai comandi dispositivi, con cui effettuare le modifiche alla configurazione di ATOS.

Nota: tutti i comandi dispongono di un aiuto in linea, è sufficiente completare il comando in corso con il carattere "?" per avere dal sistema l'informazione di tutte le possibili opzioni disponibili per quel comando. Ad esempio:

.. code-block:: console

   KPBXv4_kvm>set interfaces vswitch-0 ip ?
 
   Set command parameters:
   ip address          [address]             Current value: 0.0.0.0
   default router      [defaultrouter]       Current value: 0.0.0.0
   dhcp client         [dhcp-client]         Current value: on


Inoltre, il tasto "Tab" effettua il completamento del comando inserito:

.. code-block:: console

   KPBXv4_kvm>set interfaces vswitch-0 ip dh<tab>
   
produce l'autocompletamento

.. code-block:: console

  KPBXv4_kvm>set interfaces vswitch-0 ip dhcp-client

In caso di più possibilità di autocompletamento, la pressione ripetuta del tasto "Tab" causa il ciclare attraverso tutte le possibili opzioni.

Comandi di visualizzazione informazioni di stato ATOS
+++++

Visualizzazione indirizzo IP assegnato e stato interfacce
++++

.. code-block:: console

   KPBXv4_kvm>show interfaces status

   Show status of KPBXv4_kvm interfaces
   INTERFACES      IPV4-ADDRESS    MAC-ADDRESS        STATUS     PROTOCOL  STATUS-DETAILS                            VRF
   eth0            unassigned      00:D0:D6:xx:xx:xx  up         up        operational/running/bundled               global
   eth1            unassigned      00:D0:D6:xx:xx:xx  down       down      operational/not running                   global
   eth2            unassigned      00:D0:D6:xx:xx:xx  down       down      operational/not running                   global
   tap-vdev0       unassigned      02:09:C0:17:8C:24  up         up        operational/running/bundled               global
   tap-vdev1       unassigned      02:09:C0:CE:2D:08  up         up        operational/running/bundled               global
   tap-vdev2       unassigned      02:09:C0:FA:F0:9E  up         up        operational/running/bundled               global
   vswitch-0       192.168.23.60   00:D0:D6:xx:xx:xx  up         up        operational/running/ip4 address assigned  global

In questo output, le interfacce eth0-1-2 sono le porte fisiche dell'apparato (eth1 e eth2 sono "not running" in quanto non ci sono cavi di rete connessi), le tap-vdev0-1-2 sono porte logiche usate internamente per interconnettere le interfacce di rete della VM Kalliope con le porte fisiche. La vswitch-0 è l'interfaccia di rete di accesso ad ATOS, che in questo esempio ha ricevuto l'indirizzo 192.168.23.60 tramite DHCP.

Visualizzazione server DNS impostato su ATOS
+++++
.. code-block:: console

   KPBXv4_kvm>show dns work
   Show of KPBXv4_kvm dns
   Enable                : on
   Level of log          : 1
   Max retries           : 3
   Timeout retries (sec) : 20
   Local resolution      : preferred-v4

   LIST OF DOMAIN NAME SERVERS
   VRF                : global
   Domain Name        : anydomain
   Interface          : vswitch-0
   Primary address    : 8.8.8.8
   Secondary address  : 4.4.4.4
   Priority           : 1
   
I DNS preimpostati in ATOS sono 8.8.8.8 e 4.4.4.4

Visualizzazione server NTP per sincronizzazione orario ATOS
++++


.. code-block:: console

   KPBXv4_kvm>show system timesync work
   Show of KPBXv4_kvm system timesync
   Level of log                 : 1
   Enable                       : on
   Sync frequency (sec)         : 300
   GMT offset (min)             : 60
   Daylight saving time period  : last Sun Mar 02:00 last Sun Oct 03:00
   Local IP Address             : 0.0.0.0
   Local IPv6 Address           : ::
   VRF                          : global

   LIST OF SERVERS
   Server                                   Type
   it.pool.ntp.org                          sntp
   
   
Visualizzazione stato di esercizio della VM KalliopePBX
+++++

.. code-block:: console

   KPBXv4_kvm>show nfv kpbxv4 status

   Show status of KPBXv4_kvm nfv kpbxv4
   Status     : on
   UUID       : 614c20db-8219-4804-b27b-ca9afe91398c
   Huge pages : 4096
   Nic model  : virtio-net-pci
   

Comandi dispositivi e di modifica configurazione
+++++


.. warning::
   Per rendere persistenti al riavvio i comandi seguenti è necessario eseguire, al termine delle modifiche, il comando "save".
   
Arresto/avvio della VM KalliopePBX
++++

.. code-block:: console
   KPBXv4_kvm> set nfv kpbxv4 off
   KPBXv4_kvm> set nfv kpbxv4 on

Gestione indirizzo IP interfaccia vswitch-0 di ATOS
+++++
Disabilitazione/abilitazione DHCP client (**attenzione**, se si è connessi via ssh e non via seriale, la disattivazione del client DHCP causa il rilascio dell'indirizzo e quindi la disconnessione!)

.. code-block:: console
   KPBXv4_kvm>set interfaces vswitch-0 ip dhcp-client off 
   KPBXv4_kvm>set interfaces vswitch-0 ip dhcp-client on

**Impostazione indirizzo IP statico**


.. code-block:: console

   KPBXv4_kvm>set interfaces vswitch-0 ip address ?

     ip address  [aa.bb.cc.dd[/0-32]]

     Current value:    0.0.0.0
     Default fw value: 0.0.0.0
     
es:

.. code-block:: console
   
   KPBXv4_kvm>set interfaces vswitch-0 ip address 192.168.55.200/24
   
**Impostazione default gateway (per eventuale accesso da remoto):**

.. code-block:: console
   KPBXv4_kvm>set interfaces vswitch-0 ip defaultrouter ?
 
   default router  [aa.bb.cc.dd]
 
   Current value:    0.0.0.0
   Default fw value: 0.0.0.0
   
es:
.. code-block:: console

   KPBXv4_kvm>set interfaces vswitch-0 ip defaultrouter 192.168.55.1   
   
Modifica server DNS utilizzati da ATOS (utilizzati per risoluzione dei server NTP configurati)
++++
In questo caso si utilizza il comando "del" per rimuovere il set di DNS configurati, ed il comando "add" per aggiungere un nuovo set di server:

.. code-block:: console

   KPBXv4_kvm>del dns SERVER anydomain 1

Questo comando rimuove il set a priorità 1 (l'unico presente di default) a cui sono associati i DNS con IP 8.8.8.8 e 4.4.4.4. L'informazione delle priorità definite e dei relativi server associati sono ottenibili con il comando "show dns work"

Per aggiungere un nuovo set di server DNS, si utilizza invece il comando

.. code-block:: console

   KPBXv4_kvm>add dns SERVER anydomain 8.8.8.8 4.4.4.4 1

Modifica server NTP utilizzati da ATOS
++++
Anche in questo caso si utilizza il comando "add" per aggiungere un nuovo server e il comando "del" per rimuovere quello da cancellare:

.. code-block:: console

   KPBXv4_kvm>del system timesync it.pool.ntp.org
 
.. code-block:: console

   KPBXv4_kvm>add system timesync ntp1.inrim.it
   
   
Qualora desiderato, è possibile aggiungere più server NTP, senza necessariamente cancellare l'esistente.

Descrizione porte
++++

*jpg*

- Power (12v, 5A)
- VGA (unused)
- USB 2.0/USB 3.0
- Gigabit Ethernet (eth0)
- Gigabit Ethernet (eth1)
- HDMI (unused)
- Audio jack (unused)
- COM1 (Console 115200 8/n/1)

Prima installazione
+++++

- Collegate KalliopePBX alla vostra rete utilizzando l’interfaccia eth0
- Opzionale: collegate la porta seriale COM1 di KalliopePBX al vostro PC usando un cavo seriale (non incluso - impostazioni: 115200 8/n/1)
- Collegate l’alimentatore incluso a KalliopePBX e successivamente collegate l’alimentatore ad una presa di corrente (100-240V AC, 50-60 Hz)
- Avviare KalliopePBX premendo il tasto di accensione posto sul frontale; in caso di interruzione imprevista dell’alimentazione, al ripristino dell’alimentazione il sistema si avvia automaticamente
- Puntate il vostro browser all’indirizzo http://192.168.0.100:10080 per effettuare la prima registrazione. È richiesto l’accesso da parte di KalliopePBX all’indirizzo https://license.kalliopepbx.it; la configurazione di rete può essere modificata attraverso il menu “Impostazioni”. Nel caso compaia l'errore UNSAFE_PORT seguire questa procedura (Clicca qui)
- Dopo la registrazione, installare il firmware desiderato tra quelli disponibili. È richiesto l’accesso da parte di KalliopePBX all’indirizzo https://updates.kalliopepbx.it. Il processo può richiedere alcuni minuti, in base alla dimensione del firmware e della velocità di download della vostra rete
- Seguite il progresso dell’installazione firmware; al termine, riavviate KalliopePBX ed accedete all’interfaccia di configurazione puntando il vostro browser all’indirizzo http://<Configured_ip> (porta standard http 80). Le credenziali di default per l'accesso sono: admin/admin.
   
   
   
Virtual Machine
-----

VMWare
++++++++++

1. Scaricare l'immagine virtuale di KalliopePBX. KalliopePBX VM è disponibile in ambiente VMWare ESXi 5.x o superiore ai link seguenti. Le due immagini differiscono per il numero massimo di virtual CPU che sono visibili dal kernel (fino a 8 per la seconda, e oltre le 8 fino ad un massimo teorico di 128 per la prima) e per la dimensione del disco di sistema, che per la prima è 120 GB mentre per la seconda è limitato a 40GB (valori incrementabili con una semplice procedura eseguibile da console VMWare).

.. list-table::  
   :widths: 25 25
   :header-rows: 1

   * - Immagine
     - Link Download
   * - KalliopePBX v4 (supporta oltre le 8vCPU)
     - https://areaclienti.vianova.it/drive/download/BeWHIH36hbF12cM1/ (KalliopePBXv4_esxi5_128vcpu_120GB.ova)
   * - KalliopePBX v4 (supporta un massimo di 8 vCPU)
     - https://areaclienti.vianova.it/drive/download/bmOBoFRXDaSlcH2K/ (KalliopePBXv4_esxi5_bl-1.0.5-7156.ova)
   
   
2. Importare l'immagine scaricata nell'ambiente di virtualizzazione. Al primo avvio la macchina viene avviata in modalità recovery, ossia con il solo bootloader e senza firmware telefonico.

3. Accedere alla GUI all'indirizzo predefinito 192.168.0.100:10080 . Nel caso compaia l'errore UNSAFE_PORT seguire questa procedura (Clicca qui).

**NOTA**: E' disponibile un accesso console (con credenziali manager/manager, accessibile solo nella modalità recovery) che permette di effettuare la modifica dell'indirizzo IP dell'interfaccia eth0, nel caso in cui non sia possibile accedere all'indirizzo predefinito viq web browser.

4. Cambiare la configurazione di rete dal Menu Strumenti (cliccare sul simbolo Menu tools button.png) in alto a destra in modo che la centrale possa uscire su internet e quindi raggiungere il license server.

5. Attivare la licenza KalliopePBX VM con la chiave di attivazione fornita.

*jpg*

6. Una volta accettata la licenza cliccare sul pulsante "Esegui registrazione prodotto" per accedere alla Console di Ripristino.

*jpg*

7. Aggiornare per prima cosa il bootloader all'ultima versione disponibile. Seguire la seguente procedura per l'aggiornamento del bootloader.

8. Una volta completato l'aggiornamento cliccare sul pulsante "Riavvia bootloader" per riavviare la macchina.
La macchina verrà riavviata sempre in modalità recovery.

9. Cliccare nuovamente sul bottone "Cerca aggiornamenti" per scaricare la lista degli aggiornamenti firmware disponibili e selezionare la versione firmware desiderata.

*jpg*

10. Cliccare sul bottone "Installa sulla partizione primaria (p5)". Il KalliopePBX avviserà che tale operazione resetta la partizione cancellando tutti i dati e quindi chiederà conferma dell'operazione.

Trattandosi di una prima installazione confermare la richiesta per avviare l'installazione.
**NOTA**: L'installazione di un firmware dalla console di ripristino equivale ad un ripristino alle condizioni di fabbrica. Quindi tale operazione può essere utile per resettare completamente una macchina.

11. Una volta completata l'installazione del firmware selezionato verificare nella console di ripristino la versione firmware installata.

*jpg*

12. Tramite il menu tools selezionare la voce "Menu di spegnimento->Riavvia", scegliere la voce "Firmware primario" dal menu di riavvio e cliccare sul pulsante "Riavvia".

*jpg*

13. Al riavvio si è ridiretti al login principale (sulla porta 80).

Le credenziali di login di default sono:
Username: **admin**
Password: **admin**

Si consiglia di modificare la password di default al primo avvio.


Promox
+++++

**Aggiornamento del 10/05/2020**: E' disponibile una nuova immagine Kalliope per ambiente Proxmox VE, che supera i limiti della precedente immagine di poter utilizzare un massimo di 8 vCPU e di avere un disco di dimensioni predefinite pari a 22GB. La nuova immagine, predisposta su ambiente Proxmox VE versione 6.1 e che dispone di un disco di 120 GB, gestisce fino ad un massimo di 128 vCPU. 
**NOTA**: Non è possibile aggiornare la VM con 8vCPU a quella che ne supporta oltre 8, per cui in caso di nuove installazioni si raccomanda comunque di installare la nuova immagine, anche se le saranno assegnate un numero di vCPU pari o inferiore a 8.

Per installare KalliopPBX su ambiente Proxmox è necessario per prima cosa scaricare i due file .vma.lzo e .log nella cartella /var/lib/vz/dump/

.. list-table::  
   :widths: 25 25
   :header-rows: 1

   * - Immagine
     - Link Download
   * - KalliopePBX v4 (max 128 vCPU)
     - https://areaclienti.vianova.it/drive/download/6qmKASR4EfpHbG11/ (vzdump-qemu-100-2020_05_10-23_03_40.vma.lzo - 1,4 GB)                       https://areaclienti.vianova.it/drive/download/F9zgxpv8UAhcJerD/ (vzdump-qemu-100-2020_05_10-23_03_40.log)
   * - KalliopePBX v4 (max 8 vCPU)
     - 	https://areaclienti.vianova.it/drive/download/0hh0XCroc9AOsFzt/ (vzdump-qemu-200-2017_06_28-10_06_39.vma.lzo - 1,0 GB)     https://areaclienti.vianova.it/drive/download/vcZYocwlyIeqoHHd/ (vzdump-qemu-200-2017_06_28-10_06_39.log)

Una volta copiati i due file relativi all'immagine che si intende installare all'interno della cartella /var/lib/vz/dump della macchina host (mantenendo i nomi originali, indicati sopra), deve essere eseguito il comando di ripristino in una nuova VM:

.. code-block:: console

   # qmrestore vzdump-qemu-<versione>.vma.lzo <nnn> --storage <storage_name>
   
dove:

- **<nnn>** è l'id da assegnare alla VM (non deve essere già assegnato ad altre VM del nodo/cluster Proxmox).
- **<storage_name>** è il nome dello storage su cui ripristinare la VM (normalmente è "local" o "storage").
A questo punto la VM è operativa, è possibile avviarla e accedere alla console per effettuare la configurazione dell'indirizzo di rete.

**NOTA IMPORTANTE**: prima di avviare la macchina virtuale è necessario modificare le impostazioni della VM abilitando il flag **"KVM hardware virtualization"** che nell'immagine esportata è disabilitato, altrimenti le prestazioni sono estremamente rallentate. La nuova immagine ha già questo flag attivo di default, per cui non è più necessario effettuare la modifica di tale impostazione; si raccomanda comuqnue di controllarne l'effettivo valore.

**NOTA**: la VM viene distribuita con un modello di vCPU generico, che emula un processore Pentium 4, per la massima compatibilità. Nel caso in cui si utilizzi la VM su singolo nodo, o si disponga di nodi Proxmox VE omogenei in termini di CPU fisiche, è possibile modificare il modello del processore al valore "host", che rimappa direttamente le funzioni del processore fisico, rendendo quindi disponibili al S.O. della VM tutte le estensioni hardware presenti sulle CPU del server. A tale proposito si rimanda alla pagina di documentazione Proxmox, sezione "CPU Type": https://pve.proxmox.com/wiki/Qemu/KVM_Virtual_Machines#_emulated_devices_and_paravirtualized_devices


A questo punto si opera come per le altre VM, ossia si accede con credenziali manager/manager, e un wizard permette di effettuare le impostazioni di rete.

Una volta in rete, l'attivazione e la configurazione avviene tramite interfaccia web (inizialmente sulla porta 10080, e dopo l'installazione del firmware telefonico sulla porta standard 80). Nel caso compaia l'errore UNSAFE_PORT seguire questa procedura (Clicca qui).

E' necessario che la VM abbia la raggiungibilità in HTTPS dei nostri server di licenza e di aggiornamenti (license.kalliopepbx.it e updates.kalliopepbx.it) che attualmente risolvono entrambi l'IP 77.72.27.4

   
   
