---
title: Best practice e considerazioni
description: DO NOT PUBLISH
seo-description: DO NOT PUBLISH
page-status-flag: never-activated
uuid: c2821264-39e2-44f8-b234-835c46f33fd5
topic-tags: introduction
discoiquuid: b786e40a-202e-4e17-a2f5-1f77c46538c2
privatebeta: true
index: false
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 6%

---


# Best practice e considerazioni {#do-not-publish-best-practices-and-considerations}

<!--
[DO NOT PUBLISH]
-->

Il servizio di conversione automatica di AEM Forms converte un modulo PDF in un modulo adattivo. Il servizio utilizza algoritmi di intelligenza artificiale e machine learning per comprendere il layout e i campi del modulo sorgente. Ogni servizio di apprendimento automatico apprende continuamente dai dati di origine e produce un output migliorato ad ogni abbandono. Questi servizi imparano dall&#39;esperienza come gli esseri umani.

Il servizio di automated forms conversion (AFCS) viene addestrato su un ampio insieme di moduli. Identifica facilmente i campi in un modulo di origine e produce moduli adattivi. Tuttavia, ci sono alcuni campi e stili nelle PDF forms che sono facilmente visibili all&#39;occhio umano, ma difficili da capire per il servizio. Il servizio può assegnare ad alcuni campi o stili tipi di campi diversi da quelli applicabili. Di seguito sono elencati tutti i modelli di campo e di stile.

Il servizio inizierebbe a identificare e assegnare campi o pannelli corretti a questi modelli man mano che impara dai dati sorgente. Per il momento, puoi utilizzare l&#39;editor [Rivedi e correggi](review-correct-ui-edited.md) per risolvere questi problemi. Prima di iniziare a risolvere i problemi o ad approfondire la lettura, acquisisci familiarità con [componenti per moduli adattivi](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html).

## Generale {#general}

<table border="1" cellpadding="1" cellspacing="0" style="border-collapse: separate; border-spacing: 0px;" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Modelli noti e risoluzione</td> 
   <td width="70%">Esempio</td> 
  </tr>
   <td><p><strong>Pattern</strong></p> <p>Il servizio non converte i PDF forms compilati in moduli adattivi.</p> <p> </p> <p><strong>Risoluzione</strong></p> <p>Utilizza moduli adattivi vuoti.</p> </td> 
   <td style="text-align: left;"><img src="assets/pre-filled-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Pattern</strong></p> <p>Il servizio potrebbe non riconoscere il testo e i campi in un modulo denso.</p> <p> </p> <p><strong>Risoluzione</strong></p> <p>Aumenta la larghezza tra il testo e i campi di un modulo denso prima di iniziare la conversione.</p> </td> 
   <td style="text-align: left;"><img src="assets/dense%20form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Pattern</strong></p> <p>Il servizio non supporta i moduli digitalizzati.</p> <p> </p> <p><strong>Risoluzione</strong></p> <p>Non utilizzare moduli digitalizzati. </p> </td> 
   <td><img src="assets/scanned-form.jpg" /></td> 
  </tr>
  <tr>
   <td><p><strong>Pattern</strong></p> <p>Il servizio non estrae immagini e testo all’interno delle immagini. </p> <p> </p> <p><strong>Risoluzione</strong></p> <p>Aggiungere manualmente immagini o testo ai moduli convertiti.</p> </td> 
   <td><img src="assets/image-in-adaptive-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Pattern</strong></p> <p>Le tabelle con bordi punteggiati o non chiari non vengono convertite.</p> <p><strong>Risoluzione</strong></p> <p>Utilizzare le tabelle con bordi e bordi espliciti e chiari. supportati.</p> </td> 
   <td><img src="assets/border-less-tables.png" /></td> 
  </tr>
 </tbody>
</table>

## Gruppo di scelta  {#choice-group}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Pattern</td> 
   <td width="70%">Esempio</td> 
  </tr>
  <tr>
   <td><p><strong>Pattern</strong></p> <p>Le opzioni del gruppo di scelte con forme diverse da riquadro o cerchio non vengono convertite nei corrispondenti componenti del modulo adattivo. </p> <p> </p> <p><strong>Risoluzione</strong></p> <p>Modificare le opzioni di scelta delle forme in caselle o cerchi oppure utilizzare l'editor di revisione e correzione per identificare le forme.</p> </td> 
   <td><img src="assets/shaded-box-patterns.png" /> </td> 
  </tr>
 </tbody>
</table>

## Campi modulo {#form-fields}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Pattern</td> 
   <td width="70%">Esempio</td> 
  </tr>
  <tr>
   <td width="25%"><p><strong>Pattern</strong></p> <p>Il servizio non identifica i campi senza bordi chiari.</p> <p> </p> <p><strong>Risoluzione</strong></p> <p>Utilizza l’editor di revisione e correzione per identificare tali campi.</p> <p> </p> <p> </p> </td> 
   <td width="50%"><br /> <img src="assets/fields-without-clear-borders.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Pattern</strong></p> <p>Il servizio lascia alcuni campi modulo con didascalie in basso o a destra non identificati.</p> <p> </p> <p><strong>Risoluzione</strong></p> <p>Utilizza l’editor di revisione e correzione per identificare tali campi</p> </td> 
   <td><br /> <img src="assets/forms-with-clear-borders-scale.png" /><br /> </td> 
  </tr>
  <tr>
   <td><p><strong>Pattern</strong></p> <p>Il servizio unisce o assegna un tipo errato ad alcuni campi modulo che sono molto vicini tra loro o che non hanno bordi chiari. </p> <p> </p> <p><strong>Risoluzione</strong></p> <p>Utilizza l’editor di revisione e correzione per identificare tali campi.</p> </td> 
   <td><img src="assets/forms-with-fields-placed-nearby.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Pattern</strong></p> <p>Il servizio potrebbe non riconoscere i campi con didascalie lontane o con una linea tratteggiata tra la didascalia e il campo di input.</p> <p> </p> <p><strong>Risoluzione</strong></p> <p>Per risolvere questi problemi, utilizza i campi dei moduli con limiti chiari oppure utilizza l’editor di revisione e correzione.</p> </td> 
   <td><img src="assets/form-fields-with-far-away-captions.png" /></td> 
  </tr>
 </tbody>
</table>

## Elenchi {#lists}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Pattern</td> 
   <td width="70%">Esempio</td> 
  </tr>
  <tr>
   <td><p><strong>Pattern</strong></p> <p>Gli elenchi contenenti campi modulo vengono uniti o non convertiti nei corrispondenti componenti del modulo adattivo</p> <p><strong>Risoluzione</strong></p> <p>Per risolvere questi problemi, utilizza i campi dei moduli con limiti chiari oppure utilizza l’editor di revisione e correzione.</p> </td> 
   <td><img src="assets/lists-with-fields.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Pattern</strong></p> <p>Il servizio può lasciare non identificati alcuni elenchi nidificati</p> <p> </p> <p><strong>Risoluzione</strong></p> <p>Per risolvere questi problemi, utilizza l’editor di revisione e correzione.</p> </td> 
   <td><img src="assets/nested-lists.png" /> </td> 
  </tr>
  <tr>
   <td><p><strong>Pattern</strong></p> <p>Il servizio unisce tra loro alcuni elenchi contenenti gruppi di scelta</p> <p><strong>Risoluzione</strong></p> <p>Per risolvere questi problemi, utilizza l’editor di revisione e correzione.</p> </td> 
   <td><img src="assets/lists-containing-choice-groups.png" /> </td> 
  </tr>
 </tbody>
</table>

<!--
Comment Type: draft

<h3>Choice groups</h3>
-->

<!--
Comment Type: draft

<ul>
<li>Lists with form fields, nested lists, and nested choice groups are not supported.</li>
<li>Form fields with captions at bottom or right are not supported.</li>
<li>Form fiields without bordes are not supported.</li>
<li>Hidden form fields are not supported.</li>
<li>Button in PDF forms are not converted to adaptive form buttons.<br /> </li>
<li>Tables with clear explicit boundaries and borders are supported.</li>
<li>Fields with far away captions are not supported.<br /> </li>
<li>Choice groups with only box or circle shaped selectors are supported. </li>
</ul>
-->

