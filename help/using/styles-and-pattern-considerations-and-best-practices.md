---
title: Best practice e considerazioni
description: Best practice e considerazioni per il servizio di Automated forms conversion (AFCS)
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 9ada091a-e7c6-40e9-8196-c568f598fc2a
source-git-commit: 4b227a2cd0253b8ab471007b41787de60c2a1851
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 2%

---

# Best practice e modelli complessi noti {#Best-practices-and-considerations2}

Questo documento fornisce le linee guida e i consigli di cui possono beneficiare amministratori di moduli, autori e sviluppatori quando lavorano con [!DNL Automated Forms Conversion service] (AFCS). Descrive le best practice che vanno dalla preparazione dei moduli sorgente alla correzione di modelli complessi che richiedono un ulteriore sforzo per la conversione automatica. Queste best practice contribuiscono collettivamente alle prestazioni e all&#39;output complessivi di [!DNL Automated Forms Conversion service] (AFCS).

## Best practice

Il servizio di conversione converte i PDF forms disponibili nell&#39;istanza [!DNL Forms] dell&#39;AEM in moduli adattivi. Le best practice elencate di seguito consentono di migliorare la velocità e l’accuratezza di conversione. Inoltre, queste best practice consentono di risparmiare tempo dedicato alle attività successive alla conversione.

### Prima di caricare l’origine

Se necessario, puoi caricare tutti i PDF forms in una sola volta o in modo graduale. Prima di caricare i moduli, considera quanto segue:

* Mantenere il numero di moduli in una cartella inferiore a 15 e il numero totale di pagine in una cartella inferiore a 50.
* Mantieni le dimensioni della cartella inferiori a 10 MB. Non mantenere i moduli in una sottocartella.
* Mantieni il numero di pagine in un modulo inferiore a 15.
* Organizzare i documenti di origine in un batch di 8-15 documenti. Mantieni i moduli sorgente con i frammenti di moduli adattivi comuni in un singolo batch.
* Non caricare i moduli protetti. Il servizio non converte i moduli protetti da password e protetti.
* Non caricare [Portfoli PDF](https://helpx.adobe.com/it/acrobat/using/overview-pdf-portfolios.html). Il servizio non converte un Portfolio di PDF in un modulo adattivo.
* Non caricare moduli di origine con spazi nel nome file. Rimuovere lo spazio dal nome del file prima di caricare i moduli.
* Non caricare moduli digitalizzati, compilati e in lingue diverse da inglese, francese, tedesco, spagnolo, italiano e portoghese. Tali moduli non sono supportati.

Quando utilizzi un modulo XDP per la conversione, esegui i seguenti passaggi prima di caricare i moduli XPD di origine:

* Analizza il modulo XDP e correggi i problemi visivi. Assicurarsi che il documento di origine utilizzi i controlli e le strutture previsti. Ad esempio, è possibile che nel modulo di origine siano presenti caselle di controllo anziché pulsanti di scelta per una singola selezione. Per produrre un modulo adattivo con i componenti desiderati, modifica le caselle di controllo in pulsanti di scelta.
* [Aggiungere associazioni al modulo XDP](http://www.adobe.com/go/learn_aemforms_designer_65) prima di avviare la conversione. Quando le associazioni sono disponibili nel modulo XDP di origine, il servizio applica automaticamente le associazioni ai campi del modulo adattivo corrispondenti durante la conversione. Consente di risparmiare il tempo necessario per applicare manualmente le associazioni.
* [Aggiungere tag Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html) al file XDP. Il servizio converte automaticamente i tag Adobe Sign nei campi del modulo adattivo corrispondenti. Forms adattivo supporta un numero limitato di campi Adobe Sign. Per l&#39;elenco completo dei campi supportati, consulta [Utilizzo di Adobe Sign in un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/working-with-adobe-sign.html?lang=en).
* Se possibile, convertire tabelle complesse in documenti XDP in tabelle semplici. Una tabella con campi modulo in celle di tabella, celle di dimensioni irregolari, celle con estensione di riga o colonna, celle unite, bordi parziali o nessun bordo visibile è considerata una tabella complessa. Una tabella con uno qualsiasi degli elementi sopra menzionati è considerata una tabella complessa.
<!-- * Use sub-forms in XDP documents to create panels in adaptive forms. Service converts each sub-form to one or more adaptive form panels during conversion. -->

### Prima di avviare la conversione

* Creare modelli di moduli adattivi. I modelli consentono di specificare una struttura uniforme per i moduli dell&#39;organizzazione o del reparto.
* Specifica l’intestazione e il piè di pagina nei modelli di moduli adattivi. Il servizio ignora l’intestazione e il piè di pagina dei documenti di origine e utilizza l’intestazione e il piè di pagina specificati nel modello di modulo adattivo.
* Crea temi per moduli adattivi. I temi consentono di conferire un aspetto uniforme alle forme dell&#39;organizzazione o del reparto.
* Configura modello dati modulo per il salvataggio e il recupero da un&#39;origine dati. Crea e configura servizi di lettura e scrittura per il modello dati modulo.
* Crea frammenti di moduli adattivi e configura il servizio in modo che utilizzi i frammenti di moduli adattivi.
* Preparare modelli di flusso di lavoro comuni per i moduli che richiedono l&#39;automazione dei processi aziendali.
* Configura Adobe Analytics, se necessario


## Conoscere pattern complessi

L&#39;AEM [!DNL Forms Automated Conversion service] utilizza algoritmi di intelligenza artificiale e machine learning per comprendere il layout e i campi del modulo di origine. Ogni servizio di apprendimento automatico apprende continuamente dai dati di origine e produce un output migliorato ad ogni abbandono. Questi servizi imparano dall&#39;esperienza come gli esseri umani.

[!DNL Automated Forms Conversion service] è addestrato su un set di moduli di grandi dimensioni. Identifica facilmente i campi in un modulo di origine e produce moduli adattivi. Tuttavia, ci sono alcuni campi e stili nelle PDF forms che sono facilmente visibili all&#39;occhio umano, ma difficili da capire per il servizio. Il servizio può assegnare ad alcuni campi o stili diversi dai tipi di campi o pannelli applicabili. Di seguito sono elencati tutti i modelli di campo e di stile.

Il servizio inizierebbe a identificare e assegnare campi o pannelli corretti a questi modelli man mano che impara dai dati sorgente. Per il momento, puoi utilizzare l&#39;editor [Rivedi e correggi](review-correct-ui-edited.md) per risolvere questi problemi. Prima di iniziare a risolvere i problemi o ad approfondire la lettura, acquisisci familiarità con [componenti per moduli adattivi](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html).

### Pattern generali {#general}

| Pattern | Esempio |
|--- |--- |
| **Pattern** <br>Il servizio non converte i PDF forms compilati in un modulo adattivo. <br><br>**Risoluzione** <br>Utilizza moduli adattivi vuoti. | ![Modulo compilato](assets/best-practice-filled-forms.png) |
| **Pattern** <br>Il servizio potrebbe non riconoscere il testo e i campi in un formato denso. <br><br>**Risoluzione** <br> Aumenta la larghezza tra il testo e i campi di un modulo denso prima di avviare la conversione. |  |
| **Pattern** <br>Il servizio non supporta i moduli digitalizzati. <br><br>**Risoluzione** <br>Non utilizzare moduli digitalizzati. | ![Modulo digitalizzato](assets/scanned-forms.png) |
| **Pattern** <br>Il servizio non estrae immagini e testo all&#39;interno delle immagini. <br><br>**Risoluzione** <br> Aggiungere manualmente immagini o testo ai moduli convertiti. | ![Immagine con modulo testo](assets/best-practice-image-with-text.png) |
| **Pattern** <br>Le tabelle con limiti e bordi punteggiati o non chiari non vengono convertite. <br><br>**Risoluzione** <br>Utilizzare tabelle con bordi e bordi espliciti. supportati. | ![Modulo tabella non chiaro](assets/best-practice-table-dotted-non-clear.png) |
| **Pattern** <br> I moduli adattivi non supportano il testo verticale preconfigurato. Pertanto, il servizio non converte il testo verticale nel testo di Adaptive Forms corrispondente. <br><br>**Risoluzione** <br> Utilizza l&#39;editor di moduli adattivi per aggiungere testo verticale, se necessario. | ![Modulo tabella non chiaro](assets/vertical-text.png) |



### Gruppo di scelta  {#choice-group}

| Pattern | Risoluzione |
|--- |--- |
| **Pattern** <br> Le opzioni del gruppo di scelte con forme diverse da riquadro o cerchio non vengono convertite nei corrispondenti componenti del modulo adattivo. <br><br>**Risoluzione** <br> Modifica le opzioni di scelta delle forme in forma di riquadro o cerchio oppure utilizza l&#39;editor di revisione e correzione per identificare le forme. | ![Campo scelta ](assets/best-practice-choice-group-options.png) |

### Campi modulo {#form-fields}

| Pattern | Risoluzione |
|--- |--- |
| Il servizio **Pattern** <br> non identifica i campi senza cancellare i bordi. <br><br>**Risoluzione** <br> Utilizza l&#39;editor di revisione e correzione per identificare tali campi. | ![campi con limiti non chiari](assets/best-practice-fields-without-clear-borders.png) |
| **Pattern** <br> Il servizio potrebbe non identificare alcuni campi modulo del gruppo di scelte con didascalie nella parte inferiore o destra di un modulo. <br><br>**Risoluzione** <br> Utilizza l&#39;editor di revisione e correzione per identificare tali campi | ![Campo di scelta](assets/best-practice-caption-bottom-right.png) |
| **Pattern** <br> Il servizio unisce o assegna un tipo errato ad alcuni campi modulo che sono molto vicini tra loro o che non hanno bordi chiari. <br><br>**Risoluzione** <br> Utilizza l&#39;editor di revisione e correzione per identificare tali campi. | ![Campo di scelta](assets/best-practice-placed-very-near.png) |
| **Pattern** <br> Il servizio potrebbe non riconoscere i campi con didascalie lontane o una linea tratteggiata tra la didascalia e il campo di input. <br><br>**Risoluzione** <br> Utilizza i campi dei moduli con limiti chiari o utilizza l&#39;editor di revisione e correzione per risolvere tali problemi. | ![Campi lontani o linea tratteggiata tra il campo della didascalia](assets/best-practice-far-away-captions-or-a-dotted-line.png) |

### Elenchi {#lists}

| Pattern | Risoluzione |
|--- |--- |
| **Pattern** <br>Gli elenchi contenenti campi modulo sono stati uniti o non sono stati convertiti nei corrispondenti componenti del modulo adattivo <br><br>**Risoluzione** <br>Utilizza i campi dei moduli con limiti chiari oppure utilizza l&#39;editor di revisione e correzione per risolvere tali problemi. | ![elenchi contenenti gruppi di scelta](assets/best-practice-lists-containing-form-fields.png) |
| **Pattern** <br>Il servizio può lasciare alcuni elenchi nidificati non identificati <br><br>**Risoluzione** <br> Utilizza l&#39;editor di revisione e correzione per risolvere questi problemi. | ![elenchi contenenti gruppi di scelta](assets/best-practice-nested-lists.png) |
| **Pattern** <br> Il servizio unisce tra loro alcuni elenchi contenenti gruppi di scelta <br><br>**Risoluzione** <br> Utilizza l&#39;editor di revisione e correzione per risolvere questi problemi. | ![elenchi contenenti gruppi di scelta](assets/best-practice-check-box-in-table-cells.png) |

<!--
Comment Type: draft

<h3>Choice groups</h3>
-->

<!--
Comment Type: draft

<ul>
<li>Lists with form fields, nested lists, and nested choice groups are not supported.</li>
<li>Form fields with captions at bottom or right are not supported.</li>
<li>Form fields without borders are not supported.</li>
<li>Hidden form fields are not supported.</li>
<li>Button in PDF forms are not converted to adaptive form buttons.<br /> </li>
<li>Tables with clear explicit boundaries and borders are supported.</li>
<li>Fields with far away captions are not supported.<br /> </li>
<li>Choice groups with only box or circle shaped selectors are supported. </li>
</ul>
-->
