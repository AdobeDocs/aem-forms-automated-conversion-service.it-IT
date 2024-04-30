---
title: Configurare il servizio di Automated forms conversion (AFCS)
description: Preparare l’istanza AEM a utilizzare il servizio di Automated forms conversion (AFCS)
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer, User
level: Beginner, Intermediate
exl-id: 8f21560f-157f-41cb-ba6f-12a4d6e18555
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '2655'
ht-degree: 4%

---

# Configurare il servizio di Automated forms conversion (AFCS) {#about-this-help}

Questa guida descrive come un amministratore AEM può configurare il servizio di Automated forms conversion (AFCS) per automatizzare la conversione dei PDF forms in moduli adattivi. Questa guida è rivolta agli amministratori IT e AEM della tua organizzazione. Le informazioni fornite si basano sul presupposto che chiunque legga questa Guida conosca le seguenti tecnologie:

* Installazione, configurazione e amministrazione di pacchetti Adobe Experience Manager e AEM,

* Utilizzo di sistemi operativi Linux® e Microsoft® Windows®

* Configurazione dei server di posta SMTP

<!--- >[!VIDEO](https://video.tv.adobe.com/v/29267/) 

**Watch the video or read the article to configure Automated Forms Conversion service (AFCS)** -->

## Onboarding{#onboarding}

Il servizio è disponibile gratuitamente per i clienti Forms AEM 6.4 e AEM 6.5 Forms On-Premise e per i clienti aziendali Adobe Managed Service. Puoi contattare il team di vendita Adobe o il tuo rappresentante Adobe per richiedere l’accesso al servizio. Il servizio è disponibile anche gratuitamente e preabilitato per i clienti as a Cloud Service di AEM Forms.

Adobe abilita l’accesso per la tua organizzazione e fornisce i privilegi richiesti alla persona designata come amministratore dell’organizzazione. L’amministratore può concedere agli sviluppatori di AEM Forms (utenti) dell’organizzazione l’accesso al servizio.

## Prerequisiti {#prerequisites}

Per utilizzare il servizio di Automated forms conversion (AFCS) è necessario quanto segue:

* Il servizio di automated forms conversion (AFCS) è abilitato per la tua organizzazione
* Un account Adobe ID con privilegi di amministratore per il servizio di conversione
* Un’istanza di authoring AEM 6.4, AEM 6.5 o AEM Forms as a Cloud Service in esecuzione con il Service Pack dell’AEM più recente o gli aggiornamenti più recenti.
* Un utente AEM (nell’istanza AEM) che è membro del gruppo di utenti forms

## Configurare l’ambiente {#setuptheservice}

Prima di utilizzare il servizio, prepara l’istanza di authoring AEM a connettersi al servizio in esecuzione su Adobe Cloud. Per preparare l’istanza per il servizio, effettua le seguenti operazioni nella sequenza elencata:

1. [Scarica e installa AEM 6.4, AEM 6.5 o AEM Forms as a Cloud Service a bordo](#aemquickstart)
1. [Scarica e installa il Service Pack AEM più recente](#servicepack)
1. [Scarica e installa l’ultimo pacchetto del componente aggiuntivo AEM Forms](#downloadaemformsaddon)
1. (facoltativo) [Scarica e installa il pacchetto del connettore più recente](#installConnectorPackage)
1. [Creare temi e modelli personalizzati](#referencepackage)

### Scarica e installa AEM 6.4 o AEM 6.5 o AEM Forms as a Cloud Service a bordo {#aemquickstart}


Il servizio di automated forms conversion (AFCS) viene eseguito sull’istanza di authoring AEM. Per configurare un’istanza Autore AEM è necessario disporre di AEM 6.4, AEM 6.5 o AEM Forms as a Cloud Service.

* Se non hai AEM 6.4 o AEM 6.5 funzionanti, scaricalo dalle seguenti posizioni. Dopo aver scaricato l’AEM, per istruzioni su come configurare un’istanza di authoring dell’AEM, consulta [distribuzione e manutenzione](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall).:

   * Se sei già cliente AEM, scarica AEM 6.4 o AEM 6.5 da [Sito Web Adobe Licensing](http://licensing.adobe.com).

   * Se sei un partner Adobe, utilizza [Programma di formazione per i partner Adobi](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) per richiedere AEM 6.4 o AEM 6.5.

* Se utilizzi AEM Forms as a Cloud Service, consulta integrato per [AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-forms-cloud-service.html?lang=en#setup-environment) e [configurare un ambiente di sviluppo locale](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?lang=en#setup-environment).

### (Solo per AEM 6.4 e AEM 6.5) Scarica e installa il Service Pack più recente per AEM {#servicepack}

Scarica e installa il Service Pack AEM più recente. Per istruzioni dettagliate consulta, oppure [Note sulla versione di AEM 6.4 Service Pack](https://helpx.adobe.com/it/experience-manager/6-4/release-notes/sp-release-notes.html) o [Note sulla versione di AEM 6.5 Service Pack](https://helpx.adobe.com/experience-manager/6-5/release-notes/sp-release-notes.html).

### (Solo per AEM 6.4 e AEM 6.5) Scarica e installa il pacchetto del componente aggiuntivo AEM Forms  {#downloadaemformsaddon}

Un’istanza AEM contiene funzionalità di base per i moduli. Il servizio di conversione richiede le funzionalità complete di AEM Forms. Scarica e installa il pacchetto del componente aggiuntivo AEM Forms per usufruire di tutte le funzionalità di AEM Forms. Il pacchetto è necessario per configurare ed eseguire il servizio di conversione. Per istruzioni dettagliate, consulta [Installare e configurare le funzionalità di acquisizione dei dati.](https://helpx.adobe.com/experience-manager/6-5/forms/using/installing-configuring-aem-forms-osgi.html)

>[!NOTE]
> Dopo l’installazione del pacchetto aggiuntivo, assicurati di eseguire le configurazioni obbligatorie di post-installazione.
>

<!-- ### (Optional) Download and install connector package  {#installConnectorPackage}

The connector package provides early access to the [Auto-detect logical sections](convert-existing-forms-to-adaptive-forms.md#run-the-conversion) features and improvements delivered in release AFC-2020.03.1. Do not install the package if you do not require feature and improvements delivered in AFC-2020.03.1.  You can [download the connector package from AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1). -->


### Creare temi e modelli personalizzati {#referencepackage}

Se inizia a prendere AEM 6,4 o AEM 6,5 pollici [modalità di produzione](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/production-ready.html) (modalità di esecuzione nosamplecontent), i pacchetti di riferimento non sono installati. I pacchetti di riferimento contengono temi e modelli di esempio. Il servizio di automated forms conversion (AFCS) richiede almeno un tema e un modello per convertire un modulo PDF in un modulo adattivo. Crea un tema e un modello personalizzato per il tuo punto e [configurazione del servizio](#configure-the-cloud-service) per utilizzare modelli e temi personalizzati prima di utilizzare il servizio.

È inoltre possibile scaricare e installare [Risorse di riferimento AEM Forms](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) nell’istanza Autore. Crea alcuni temi e modelli di riferimento.

## Configurare il servizio {#configure-the-service}

Prima di procedere alla configurazione del servizio e collegare l’istanza locale con il servizio in esecuzione su Adobe Cloud, scopri gli utenti tipo e i privilegi necessari per connettersi al servizio. Il servizio utilizza due diversi tipi di utenti tipo, amministratori e sviluppatori:

* **Amministratori**: gli amministratori sono responsabili della gestione del software e dei servizi Adobi per la propria organizzazione. Gli amministratori concedono agli sviluppatori della propria organizzazione l’accesso per connettersi al servizio di Automated forms conversion (AFCS) in esecuzione su Adobe Cloud. Quando viene eseguito il provisioning di un amministratore per un’organizzazione, l’amministratore riceve un messaggio e-mail con il titolo **[!UICONTROL 'You now have administrator rights to manage Adobe software and services for your organization']**. Se sei un amministratore, controlla la tua casella di posta elettronica con il titolo indicato in precedenza e procedi a [concedere l’accesso agli sviluppatori della tua organizzazione;](#adduseranddevs).

![E-mail concessione accesso amministratore](assets/admin-console-adobe-io-access-grantedx75.png)

* **Sviluppatori**: uno sviluppatore connette un’istanza di authoring AEM Forms locale al servizio di Automated forms conversion (AFCS) in esecuzione su Adobe Cloud. Quando un amministratore concede a uno sviluppatore i diritti per connettersi al servizio di Automated forms conversion (AFCS), allo sviluppatore viene inviata un’e-mail con il titolo Ora disponi dell’accesso per sviluppatori per gestire le integrazioni API Adobe per la tua organizzazione. Se sei uno sviluppatore, controlla la tua casella di posta elettronica per ricevere e-mail con il titolo precedentemente menzionato e procedi a [Connetti l’istanza AEM locale al servizio di Automated forms conversion su Adobe Cloud.](#connectafcadobeio)

![E-mail di concessione dell’accesso per sviluppatori](assets/email-developer-accessx94.png)

### (Solo per amministratori di AEM 6.4 e AEM 6.5) Concedi l’accesso agli sviluppatori della tua organizzazione {#adduseranddevs}

Dopo l’Adobe di abilita l’accesso per la tua organizzazione e fornisce i privilegi richiesti all’amministratore, quest’ultimo può accedere a Admin Console (istruzioni dettagliate di seguito), creare un profilo e aggiungere sviluppatori al profilo. Gli sviluppatori possono collegare un’istanza locale di AEM Forms al servizio Automated forms conversion (AFCS) su Adobe Cloud.

Gli sviluppatori sono membri dell’organizzazione designati per eseguire il servizio di conversione. Solo gli sviluppatori che vengono aggiunti al profilo del servizio Automated forms conversion Adobe (AFCS) sono autorizzati a utilizzare il servizio Automated forms conversion (AFCS). Per creare un profilo e aggiungervi sviluppatori, effettua le seguenti operazioni. È necessario almeno un profilo per concedere l’accesso richiesto agli sviluppatori dell’organizzazione:

1. Accedi a [Admin Console](https://adminconsole.adobe.com/). Utilizzare **Adobe ID** dell&#39;amministratore predisposto per l&#39;accesso tramite il servizio di Automated forms conversion (AFCS). Non utilizzare altri ID o Federated ID per effettuare l&#39;accesso.
1. Fai clic su **[!UICONTROL Automated Forms Conversion]** opzione.
1. Clic **[!UICONTROL New Profile]** nel **[!UICONTROL Products]** scheda.
1. Specifica **[!UICONTROL Name]**, **[!UICONTROL Display Name]**, e **[!UICONTROL Description]** per il profilo. Fai clic su **[!UICONTROL Done]**. Viene creato un profilo.

   ![Specifica i dettagli per il nuovo profilo.](assets/create-new-profile-details.png)

1. Aggiungi uno sviluppatore al profilo. Per aggiungere gli sviluppatori:
   1. In [Admin Console](https://adminconsole.adobe.com/enterprise), passa alla scheda Panoramica.
   1. Clic **[!UICONTROL Assign Developers]** sulla scheda prodotto richiesta.
   1. Immetti l’indirizzo e-mail degli sviluppatori e, facoltativamente, il nome e il cognome.
   1. Seleziona i profili di prodotto. Tocca **[!UICONTROL Save]**.

Ripeti i passaggi precedenti per tutti gli utenti. Per ulteriori dettagli sull’aggiunta di sviluppatori, consulta [Gestire gli sviluppatori](https://helpx.adobe.com/enterprise/using/manage-developers.html).

Quando un amministratore aggiunge sviluppatori al profilo di Adobe I/O, gli sviluppatori ricevono una notifica tramite e-mail. Dopo aver ricevuto l’e-mail, gli sviluppatori possono procedere a [collegare un’istanza AEM Forms locale con il servizio di Automated forms conversion su Adobe Cloud](#connectafcadobeio).

### Connetti l’istanza AEM Forms locale al servizio Automated forms conversion (AFCS) su Adobe Cloud (solo per sviluppatori) {#connectafcadobeio}

Se un amministratore ti fornisce l’accesso come sviluppatore, puoi collegare la tua istanza AEM Forms locale al servizio di Automated forms conversion (AFCS) in esecuzione su Adobe Cloud. Per connettere l’istanza AEM Forms al servizio, effettua le seguenti operazioni nella sequenza elencata:

* [Configurare le notifiche e-mail](configure-service.md#configureemailnotification)
* [Aggiungi utente al gruppo forms-users](#adduserstousergroup)
* [Ottenere certificati pubblici](#obtainpubliccertificates)
* [Configurare le API del servizio nella console Adobe Developer](#createintegration)
* [Configurare il servizio cloud](configure-service.md#configure-the-cloud-service)

#### Configurare le notifiche e-mail {#configureemailnotification}

Il servizio di automated forms conversion (AFCS) utilizza il servizio di posta Day CQ per inviare le notifiche e-mail. Queste notifiche e-mail contengono informazioni sulle conversioni riuscite o non riuscite. Se scegli di non ricevere le notifiche, ignora questi passaggi. Per configurare il servizio e-mail Day CQ, effettua le seguenti operazioni:

* Per i Forms AEM 6.4 Forms o AEM 6.5:

   1. Vai a Gestione configurazione AEM all’indirizzo `http://localhost:4502/system/console/configMgr`
   1. Apri la configurazione Day CQ Mail Service (Servizio posta Day CQ). Specifica un valore per **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port]**, e **[!UICONTROL From address]** campi. Fai clic su **[!UICONTROL Save]**.

      È possibile contattare il provider di servizi di posta elettronica o l&#39;amministratore IT per informazioni sul nome host e sulla porta del server SMTP. Puoi utilizzare qualsiasi indirizzo e-mail valido nel campo da. Ad esempio, notification@example.com o donotreply@example.com.

   1. Apri **[!UICONTROL Day CQ Link Externalizer]** configurazione. In **[!UICONTROL Domains]** , specificare il nome host o l&#39;indirizzo IP effettivo e il numero di porta per le istanze locali, di authoring e di pubblicazione. Fai clic su **[!UICONTROL Save]**.

* Per AEM Forms as a Cloud Service, [registra un ticket di supporto per abilitare il servizio e-mail](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).

#### Aggiungi utente al gruppo forms-users {#adduserstousergroup}

Specifica un indirizzo e-mail nel profilo dell’utente AEM designato per l’esecuzione del servizio. Assicurati che l&#39;utente sia membro di [utente Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/forms-groups-privileges-tasks.html) gruppo. Le e-mail vengono inviate all’indirizzo e-mail dell’utente che esegue la conversione. Per specificare un indirizzo e-mail per l&#39;utente e aggiungere l&#39;utente al gruppo di utenti dei moduli:

1. Accedi all’istanza di authoring di AEM Forms come amministratore AEM. Utilizza le credenziali AEM locali per accedere. Non utilizzare Adobe ID per accedere. Tocca **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.

1. Seleziona un utente designato per eseguire il servizio di conversione e tocca **[!UICONTROL Properties]**. Viene visualizzata la pagina Modifica impostazioni utente.
1. Specifica un indirizzo e-mail nel **[!UICONTROL Email]** campo e tocco **[!UICONTROL Save]**. Le e-mail vengono inviate all’indirizzo e-mail specificato al completamento o al fallimento della conversione.
1. Tocca il **Gruppi** scheda. Nella scheda Seleziona gruppo, digita e seleziona la **forms-users** gruppo. Tocca **Salva e chiudi**. L&#39;utente è ora membro del gruppo utenti di Forms.

#### Ottenere certificati pubblici (solo per AEM 6.4 e AEM 6.5) {#obtainpubliccertificates}

Un certificato pubblico consente di autenticare il profilo su Adobe I/O.

1. Accedi all’istanza Autore di AEM Forms. Accedi a **[!UICONTROL Tools]**> **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Tocca **[!UICONTROL Create]**. Il **[!UICONTROL Adobe IMS Technical Account Configuration]** viene visualizzata.

   ![Pagina Configurazione account tecnico Adobe IMS](assets/adobe-ims-technical-account-configuration.png)

1. Seleziona **[!UICONTROL Automated Forms Conversion Service]** nella soluzione Cloud.

1. Seleziona la **[!UICONTROL Create new certificate]** e specificare un alias. L’alias funge da nome della finestra di dialogo. Tocca **[!UICONTROL Create certificate]**. Viene visualizzata una finestra di dialogo. Fai clic su **[!UICONTROL OK]**. Il certificato viene creato.

1. Tocca **[!UICONTROL Download Public Key]** e salva *AEM-Adobe-IMS.crt* nel computer. Il file del certificato viene utilizzato per [Configurare le API del servizio nella console Adobe Developer](#createintegration). Tocca **[!UICONTROL Next]**.

1. Specifica quanto segue:

   * Title (Titolo): specifica un titolo.
   * Server autorizzazioni: [https://ims-na1.adobelogin.com](https://ims-na1.adobelogin.com)\

   Lascia vuoti gli altri campi per il momento (dovranno essere riempiti successivamente). Tieni aperta la pagina.

   <!--
   Comment Type: draft

   <li> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

#### (Solo per AEM 6.4 e AEM 6.5) Configura le API del servizio sulla console Adobe Developer {#createintegration}

Per utilizzare il servizio di Automated forms conversion (AFCS), crea un progetto e aggiungi l’API del servizio Configurazione automatica Forms al progetto nella console Adobe Developer. L’integrazione genera la chiave API, il segreto client, il payload (JWT).

1. Accedi a [https://console.adobe.io/](https://console.adobe.io/). Utilizza l’account Adobe ID per sviluppatori fornito dall’amministratore per accedere alla console Adobe I/O e accedervi.
1. Seleziona la tua organizzazione dall’angolo in alto a destra. Se non sai qual è la tua organizzazione, contatta l’amministratore.
1. Tocca **[!UICONTROL Create new project]**. Viene visualizzata una schermata per iniziare a utilizzare il nuovo progetto. Tocca **[!UICONTROL Add API]**. Viene visualizzata una schermata con l’elenco di tutte le API abilitate per l’account.
1. Seleziona **[!UICONTROL Automated Forms Conversion service]** e tocca **[!UICONTROL Next]**. Viene visualizzata una schermata per configurare l’API.
1. Seleziona la [!UICONTROL Upload your public key] , carica il file AEM-Adobe-IMS.crt scaricato in [Ottieni certificati pubblici](#obtainpubliccertificates) sezione e tocco **[!UICONTROL Next]**. Viene visualizzata l’opzione Create a new Service Account (JWT) credential (Crea una nuova credenziale account di servizio (JWT)). Tocca **[!UICONTROL Next]**.
1. Seleziona un profilo di prodotto e tocca **[!UICONTROL Save configured API]**. Seleziona il profilo creato durante [concedere l’accesso agli sviluppatori della tua organizzazione](#adduseranddevs). Se non conosci il profilo da selezionare, contatta l’amministratore.
1. Tocca **[!UICONTROL Service Account (JWT)]** per visualizzare la chiave API, il segreto client e altre informazioni necessarie per collegare l’istanza AEM locale al servizio di Automated forms conversion (AFCS). Le informazioni contenute nella pagina vengono utilizzate per creare la configurazione IMS sul computer locale.

1. Apri la pagina Configurazione IMS nell’istanza locale. Hai tenuto aperta questa pagina alla fine della sezione [Recuperare il certificato pubblico](#obtainpubliccertificates).

   ![Specifica titolo, chiave API, segreto client e payload ](assets/ims-configuration-details.png)

1. Nella pagina Tecnica Adobe IMS, specifica Chiave API e Segreto client. Utilizza i valori specificati in Service Account (JWT) (Account di servizio (JWT)) nella pagina della console Adobe Developer.

   >[!NOTE]
   >
   >
   >Per il payload, utilizza il codice fornito nella scheda Genera JWT della pagina Account di servizio (JWT) di Adobe Developer Console.

1. Tocca **[!UICONTROL Save]**. Viene creata la configurazione IMS.

   >[!CAUTION]
   >
   >Crea una sola configurazione IMS. Non creare più di una configurazione IMS.

1. Seleziona la configurazione IMS e tocca **[!UICONTROL Check Health]**. Viene visualizzata una finestra di dialogo. Tocca **[!UICONTROL Check]**. Una volta stabilita la connessione, viene visualizzato il messaggio *Token recuperato correttamente*.

   ![Una volta stabilita la connessione, viene visualizzato il messaggio token recuperato correttamente. ](assets/health-check.png)

   <br/> <br/>

#### Configurare il Cloud Service {#configure-the-cloud-service}

Crea una configurazione di Cloud Service per collegare l’istanza AEM al servizio di conversione. Consente inoltre di specificare un modello, un tema e frammenti di modulo per una conversione. Puoi creare più configurazioni del servizio cloud separate per ciascun set di moduli. Ad esempio, è possibile avere una configurazione separata per i moduli del reparto vendite e una distinta per i moduli dell&#39;assistenza clienti. Per creare una configurazione del servizio cloud, effettua le seguenti operazioni:

1. Nell’istanza di AEM Forms, tocca **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]**> **[!UICONTROL Cloud Services]** > **[!UICONTROL Automate Forms Conversion Configuration]**.
1. Tocca il **[!UICONTROL Global]** cartella e tocca **[!UICONTROL Create]**. Viene visualizzata la pagina per la creazione della configurazione del Automated forms conversion. La configurazione viene creata nella cartella Globale. Puoi anche creare la configurazione in un’altra cartella esistente o creare una cartella per le configurazioni.

1. Il giorno **[!UICONTROL Create Automated Forms Conversion Configuration]** , specifica il valore per i campi seguenti e tocca **[!UICONTROL Next]**.

   | Campo | Descrizione |
   |--- |--- |
   | Titolo | Titolo univoco per la configurazione. Il titolo viene visualizzato nell’interfaccia utente utilizzata per avviare la conversione. |
   | Nome | Nome univoco per la configurazione. La configurazione viene salvata nel CRX-Repository con il nome specificato. Il nome può corrispondere al titolo. |
   | Posizione miniature | Posizione della miniatura per la configurazione. |
   | URL del servizio | URL del servizio di Automated forms conversion (AFCS) su Adobe Cloud. Utilizza il `https://aemformsconversion.adobe.io/` URL. |
   | Modello | Modello predefinito da applicare ai moduli convertiti. Puoi sempre specificare un modello diverso prima di iniziare la conversione. Un modello contiene la struttura di base e il contenuto iniziale di un modulo adattivo. Puoi scegliere un modello tra quelli forniti come standard. Puoi anche creare un modello personalizzato. |
   | Tema | Tema predefinito da applicare ai moduli convertiti. Puoi sempre specificare un tema diverso prima di iniziare la conversione.  Puoi fare clic sull’icona per scegliere un tema fornito con il prodotto. Puoi anche creare un tema personalizzato. |
   | Frammenti esistenti | Posizione di eventuali frammenti esistenti. |
   | Metamodello personalizzato | Percorso del file .schema.json del metamodello personalizzato. Puoi creare metamodelli separati per le lingue inglese, francese, tedesco, spagnolo, italiano e portoghese. |

1. In **[!UICONTROL Advanced]** scheda di **[!UICONTROL Create Automated Forms Conversion Configuration]** , specificare il valore per il campo seguente:

   <table>
   <thead>
   <tr>
   <th>Campo</th>
   <th>Descrizione</th>
   </tr>
   </thead>
   <tbody>
   <tr>
   <td >Genera documento di record</td>
   <td>Selezionare l'opzione per generare automaticamente il documento di record per i moduli convertiti. L’opzione è disponibile solo per i moduli basati su XFA (XDP e PDF forms). Se si abilita l'opzione, dopo aver inviato un modulo è possibile consentire ai clienti di conservare una registrazione, in formato cartaceo o in formato documento, delle informazioni che hanno compilato nel modulo per riferimento futuro. Tale documento è denominato documento di record.</td>
   </tr>
   <tr>
   <td>Abilita Analytics</td>
   <td>(Solo per AEM 6.4 e AEM 6.5) Seleziona l’opzione per abilitare Adobe Analytics su tutti i moduli convertiti. Prima di utilizzare l’opzione, accertati che Adobe Analytics sia abilitato per la tua istanza di AEM Forms.</td>
   </tr>
   </tbody>
   </table>

   * Quando l’origine è un modulo basato su XFA con estensione .XDP, il DOR di output mantiene il layout XFA, altrimenti il servizio di conversione utilizza un modello preconfigurato per generare DOR per altri moduli basati su XFA.
   * Quando si invia un modulo XFA, i dati di invio del modulo vengono salvati come un elemento XML o un attributo. Ad esempio: `<Amount currency="USD"> 10.00 </Amount>`. La valuta viene salvata come attributo e come importo della valuta; 10.00 viene salvato come elemento. I dati di invio di un modulo adattivo non dispongono di attributi, ma solo di elementi. Pertanto, quando un modulo basato su XFA viene convertito in modulo adattivo, i dati di invio del modulo adattivo contengono un elemento per ciascun attributo di questo tipo. Ad esempio:

   ```css
      {
         "Type": "Principal",
   
         "Amount": "10.00",
   
         "currency": "USD"
      }
   ```

1. Tocca **[!UICONTROL Create]**. Viene creata la configurazione cloud. La tua istanza di AEM Forms è pronta per iniziare a convertire i moduli legacy in moduli adattivi.
