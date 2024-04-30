---
title: Domande frequenti
description: Query comuni o domande frequenti
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: introduction
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 3a29f8d4-8ea0-49eb-bfe0-0eab5f0c52c7
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '1777'
ht-degree: 3%

---

# Domande frequenti{#frequently-asked-questions}

1. **Quale versione di AEM Forms è supportata dal servizio di Automated forms conversion (AFCS)?**
   <p>Il servizio di automated forms conversion (AFCS) supporta AEM 6.4 Forms e AEM 6.5 Forms. Funziona sia con AEM Forms su OSGi che con i moduli AEM su JEE. Per utilizzare il servizio è necessario il pacchetto del componente aggiuntivo AEM Forms più recente oltre all’istanza di authoring dell’AEM. Per istruzioni dettagliate, consulta <a href="configure-service.md">Configurare il Automated forms conversion</a> servizio.</p> 
    <br>

1. **Il servizio può essere installato on-premise?**
   <p>Adobe addestra regolarmente gli algoritmi AI e ML del servizio di Automated forms conversion (AFCS) con nuovi set di dati per migliorare la precisione della conversione. Gli algoritmi aggiornati vengono distribuiti periodicamente al servizio di conversione in esecuzione su Adobe Cloud. Tutti i clienti del servizio usufruiscono degli algoritmi aggiornati. Pertanto, l’implementazione centrale ospitata sul cloud è ideale per il servizio di Automated forms conversion (AFCS) che consente di apprendere e migliorare continuamente tutti i clienti.</p> 
    <p>Il servizio converte i moduli vuoti in moduli adattivi. Il servizio non supporta i moduli compilati e l’estrazione di dati dai moduli compilati. Inserire nell'elenco Consentiti Rimuovere i dati dai moduli compilati e rimuovere o le informazioni proprietarie dai moduli prima di inviarli al servizio per la conversione</p> <br>

1. **Il servizio supporta tutti i formati di PDF forms? Quali sono tutte le lingue supportate?**
   <p>Il servizio può convertire PDF forms non interattivi, XDP e PDF forms basati su XFA e AcroForms in moduli adattivi. Il servizio non supporta moduli digitalizzati o compilati. Per altre limitazioni, consulta <a href="known-issues.md">problemi noti</a> articolo.<br /> </p> 
    <p>Stiamo aggiungendo regolarmente il supporto per altri tipi di origine. Mantieni <a href="introduction.md">moduli PDF supportati</a> nella tua watchlist per un aggiornamento regolare sulle nuove funzioni e funzionalità aggiunte.</p>

   Il servizio può convertire in moduli adattivi solo i moduli in lingua inglese, francese, tedesca, spagnola, italiana e portoghese. Puoi tradurre i moduli adattivi generati in un’altra lingua utilizzando [Flusso di lavoro di traduzione AEM.](https://helpx.adobe.com/it/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)</br> </br>

1. **Il servizio può produrre un XDP invece di un modulo adattivo?**
   <p>Il servizio non produce un output XDP. Aggiungiamo regolarmente funzionalità e al servizio. Mantieni <a href="introduction.md">lingue e PDF forms supportati</a> nella tua watchlist per un aggiornamento regolare sulle nuove funzioni e funzionalità aggiunte.</p> <br>

1. **Qual è il tipo di schema generato?**
   <p>Puoi utilizzare il servizio per generare: </p>

   * un modulo adattivo associato a uno schema JSON e
   * un modulo adattivo non associato ad alcun schema <br><br>

1. **Il servizio può convertire un modulo di Microsoft Word in moduli adattivi?**
   <p>No, il servizio non converte un modulo di Microsoft Word in un modulo adattivo. È possibile salvare un modulo di Microsoft Word in un modulo di PDF e convertire il modulo di PDF in un modulo adattivo. Il processo completo è </p> <br>

   1. Utilizza Adobe Acrobat per [convertire un documento Word in un PDF non interattivo](https://helpx.adobe.com/acrobat/how-to/create-pdf-files-word-excel-website.html).
   1. Utilizza Adobe Acrobat per [convertire i PDF forms prodotti in PDF compilabili](https://helpx.adobe.com/acrobat/how-to/convert-word-excel-paper-pdf-forms.html).
   1. Utilizza Adobe Acrobat per aggiornare e correggere manualmente i campi del modulo.
   1. Salvare il modulo PDF. Ora è possibile utilizzare il modulo con il servizio di conversione per generare un modulo adattivo. È inoltre possibile utilizzare il modulo come modello di documento di record.


1. **Il servizio può convertire i moduli cartacei digitalizzati e i moduli colorati in moduli adattivi?**
   <p>Il servizio può convertire i PDF forms a colori in moduli adattivi. Il servizio non supporta moduli digitalizzati o compilati. Per altre limitazioni, consulta <a href="known-issues.md">problemi noti</a> articolo.</p> <br>

1. **Il servizio può convertire un modulo digitalizzato o solo l’immagine di un modulo in un modulo adattivo?**
   <p>Il servizio non supporta la conversione di moduli digitalizzati o di immagini di moduli in moduli adattivi pronti all’uso. Tuttavia è possibile utilizzare Adobe Acrobat per convertire l’immagine del modulo in un modulo PDF, quindi utilizzare il servizio per convertire il modulo PDF in un modulo adattivo. Utilizza sempre un’immagine di alta qualità del modulo in Acrobat per migliorare la qualità della conversione.</p> <br>

1. **Alcuni moduli basati su XDP utilizzano frammenti di modulo. Dove devono essere caricati?**
   <p class="MsoNormal">Carica i frammenti di modulo nella cartella di conversione e mantieni la struttura originale delle cartelle. Consente di preservare i percorsi relativi utilizzati nei moduli basati su XDP e nei frammenti di modulo.</p> <br>

1. **Il servizio supporta i moduli XDP associati a schema? Se dispongo di un XDP associato a uno schema, devo incorporare lo schema in XDP?**
   <p>Sì, il servizio supporta moduli XDP associati a schema e richiede che lo schema sia incorporato nel modulo XDP di origine. Quando si converte un modulo XDP associato a schema, il servizio genera uno schema JSON. Lo schema JSON è strutturalmente simile allo schema XSD dei moduli XDP di origine.</p> <br>

1. **Impossibile convertire i moduli. Qual è il motivo e come risolvere il problema?**
I motivi più comuni per cui la conversione non riesce sono:</p>
   * Per la conversione vengono forniti PDF forms protetti. Non utilizzare PDF forms protetti da password o protetti per la conversione.
   * Connessione Internet interrotta. Assicurati di essere connesso a Internet durante la conversione.
   * Il PDF di origine ha un’immagine del modulo invece del modulo effettivo.
   * Il servizio non è configurato correttamente, l’URL del servizio non è stato fornito o l’URL del servizio fornito non è corretto. Controlla la [configurazione del servizio](configure-service.md#configure-the-cloud-service) a **[!UICONTROL AEM]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion configuration]**.
   * Configurazione IMS non configurata correttamente. Esegui un controllo di integrità sulla configurazione IMS per assicurarti che funzioni correttamente. Per verificare se la configurazione IMS è corretta o meno:
      1. Vai a `http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. Seleziona la configurazione. Fai clic su **[!UICONTROL Check Health]** dall’intestazione e fai clic su **[!UICONTROL Check]**. In caso di esito positivo, **[!UICONTROL Token retrieved successfully!]** messaggio. <br> <br>

1. **L’utilizzo di font personalizzati influisce sulla conversione?**
   <p>Quando un modulo PDF non interattivo viene convertito in un modulo adattivo, per migliorare la qualità della conversione, i font vengono incorporati nel modulo PDF. Il supporto per l'incorporamento di font è limitato ai PDF forms non interattivi. Per ottimizzare la conversione dei PDF forms basati su AcroForm e XFA, vengono utilizzati font di fallback.</p> 
    <p>Solo i moduli disponibili nella directory dei caratteri personalizzati elencata nella <strong>Directory font cliente</strong> campo del <strong> Servizio Gestione caratteri CQ-DAM-Handler-Gibson</strong> sono incorporate in un modulo di PDF non interattivo.</p> 
    <p> </p> <br>

1. **Il servizio identifica e utilizza i font di source PDF nei moduli adattivi generati?**
   <p>Lo stile e il layout di un modulo responsive HTML sono generalmente diversi da quelli di un modulo PDF o cartaceo. Per supportare layout e stili coerenti tra le organizzazioni, i moduli adattivi utilizzano <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html">temi per assegnare uno stile a un modulo</a>. Il servizio di conversione utilizza i font e gli stili di font specificati nel tema applicato durante la conversione. È possibile modificare i font e gli stili dei font del tema per conferire un aspetto distinto ai componenti di un modulo adattivo.</p> <br>

1. **Il servizio estrae automaticamente JavaScript dai moduli basati su XDP e lo applica ai moduli adattivi corrispondenti?**
   <p>Il servizio non converte automaticamente gli script di moduli basati su XFA o Acro Forms nelle regole dei moduli adattivi corrispondenti. Gli autori dei moduli possono utilizzare <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html">Editor regole</a> per aggiungere interattività a un modulo adattivo.</p> <br>

1. **Alcuni oggetti modulo non vengono convertiti correttamente in componenti modulo adattivi. Come risolvere il problema?**
   <p>Il servizio di automated forms conversion (AFCS) viene addestrato su un ampio insieme di moduli. Tuttavia, le applicazioni basate su AI/ML sono limitate dai relativi dati e modelli di formazione. Potrebbero esistere più tipi di campo, layout, pattern e contesto distinguibili dalla percezione umana, ma difficili per il riconoscimento automatico. Il servizio potrebbe non identificare tali oggetti o riconoscerli in modo errato. È possibile utilizzare <a href="review-correct-ui-edited.md" target="_blank">Revisione e correzione</a> per apportare le modifiche necessarie nel formato cartaceo del modulo di input.</p> <br/>

1. **Alcune correzioni vengono ripetute tra i moduli. Il servizio è in grado di identificare e correggere tutte queste istanze nelle conversioni future?**

   Il servizio fornisce una formazione coerente sui moduli e sui modelli. Apprende nuovi pattern su base giornaliera. Deve ancora iniziare ad applicare automaticamente le correzioni ripetute nei moduli. Tieni d’occhio i moduli in prerelease per verificare la disponibilità di questa funzione. <br/><br/>

   Puoi utilizzare il metamodello per mappare gli oggetti modulo al componente modulo adattivo desiderato e preconfigurare convalide, regole, pattern di dati, testo della guida e proprietà di accessibilità per i componenti. Tutte le proprietà specificate vengono applicate durante la conversione. Puoi utilizzare il metamodello per applicare proprietà comuni ai campi. Può aiutarti a ridurre alcuni problemi ripetuti tra i moduli.<br/><br/>

1. **Quali sono le opzioni per i moduli con dati sensibili, ad esempio informazioni personali (PII, personally identifiable information)?**
Il servizio supporta solo moduli vuoti o non compilati. Non caricare moduli compilati o con informazioni personali (PII, personally identifiable information). Inoltre, rimuovi i dati precompilati, le informazioni personali identificabili (PII), riservate e proprietarie nei moduli sorgente. <br/>

1. **Dove posizionare intestazione e piè di pagina?**
   <p>Posiziona intestazione e piè di pagina in un modello di moduli adattivi. Se il modulo PDF di origine include intestazione e piè di pagina, durante la conversione il servizio rileva e sostituisce l’intestazione e il piè di pagina rilevati con l’intestazione e il piè di pagina disponibili nel modello di modulo adattivo. Se nel modulo adattivo sono inclusi un’intestazione o un piè di pagina aggiuntivi, puoi utilizzare <a href="review-correct-ui-edited.md">Revisione e correzione</a> per correggere o rimuovere tale intestazione o piè di pagina.</p> <br />

1. **Quanto tempo risparmia il servizio rispetto al processo manuale di pianificazione, creazione di risorse (temi, modelli), creazione e pubblicazione di un modulo adattivo?**
   <p>La quantità di tempo dipende dalle dimensioni e dalla complessità dei moduli di input e dal numero di richieste. Il servizio intende ridurre in modo significativo il time-to-value convertendo i PDF forms in moduli adattivi a un ritmo molto più rapido rispetto alla conversione manuale dei moduli. </p> <br />

1. **Cosa fare se si verifica un errore relativo alle librerie RSA? Il messaggio di errore è simile al messaggio indicato di seguito:** <br/>
   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` <br>
L&#39;errore sopra riportato si verifica quando la delega di avvio non è configurata per le librerie RSA/BouncyCastle. Per risolvere il problema, effettua le seguenti operazioni:
   <p> </p>

   1. Arresta l’istanza AEM. Accedi a `[AEM installation directory]\crx-quickstart\conf\` cartella. Apri il file sling.properties per la modifica. Se usa `[AEM installation directory]\crx-quickstart\bin\start.bat` per avviare un’istanza AEM, modifica il file sling.properties che si trova in `[AEM_root]\crx-quickstart\`.
   1. Aggiungi le seguenti proprietà al file sling.properties:<br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. Salva e chiudi il file. <br/>
   1. Avvia l’istanza AEM.<br/>
   <br/>

1. **Come modificare automaticamente le maiuscole/minuscole del testo di un modulo adattivo?**
   <p>Puoi utilizzare l’editor di stili o temi adattivo per modificare le maiuscole/minuscole di un campo di modulo adattivo. Ad esempio, puoi aprire l’editor tema e impostare il valore della proprietà Case di tutto il testo del modulo su maiuscolo, minuscolo o camelCase. Puoi anche utilizzare l’opzione CSS Override nell’editor di temi per creare diversi tipi di stili.</p>

1. **Posso utilizzare i tag di testo di Adobe Sign con il servizio di Automated forms conversion (AFCS)?**
   <p> Quando si utilizza il servizio di Automated forms conversion (AFCS) per convertire un modulo di PDF in un modulo adattivo e il modulo di PDF dispone di tag di testo Adobe Sign, tali tag vengono convertiti nei campi del modulo adattivo corrispondenti e i dettagli del firmatario vengono popolati automaticamente.  La funzione è disponibile solo per Acro Forms e i moduli adattivi supportano un numero limitato di campi Adobe Sign.</p>  </br>

1. **Come si crea un modulo PDF abilitato per Adobe Sign?**
   </p>Per creare un modulo PDF abilitato per Adobe Sign:</p>

   Aggiungi [Tag di testo Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html) ai nomi dei campi o utilizzare [Converti in Adobe Sign Form](https://helpx.adobe.com/sign/using/create-forms-with-acrobat.html) opzione.
