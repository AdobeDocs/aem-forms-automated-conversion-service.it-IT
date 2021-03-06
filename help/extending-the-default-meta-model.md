---
title: Estensione del metamodello predefinito
seo-title: Extend the default meta-model
description: Estendi il metamodello predefinito per aggiungere pattern, convalide ed entità specifici all’organizzazione e applica configurazioni ai campi del modulo adattivo durante l’esecuzione del servizio Automated forms conversion.
seo-description: Extend the default meta-model to add pattern, validations, and entities specific to your organization and apply configurations to adaptive form fields while running the Automated Forms Conversion service.
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
exl-id: f679059c-18aa-4cb5-8368-ed27e96c20de
source-git-commit: e3ba3807668084495acb77f57ea2da6d5a53e626
workflow-type: tm+mt
source-wordcount: '2565'
ht-degree: 1%

---

# Estensione del metamodello predefinito {#extend-the-default-meta-model}

Il servizio di automated forms conversion identifica ed estrae gli oggetti modulo dai moduli di origine. La mappatura semantica consente al servizio di decidere in che modo gli oggetti estratti vengono rappresentati in una forma adattiva. Ad esempio, un modulo di origine può presentare diversi tipi di rappresentazioni di una data. La mappatura semantica consente di mappare tutte le rappresentazioni degli oggetti modulo data del modulo sorgente con il componente data dei moduli adattivi. La mappatura semantica consente inoltre al servizio di preconfigurare e applicare convalide, regole, pattern di dati, testo della Guida e proprietà di accessibilità ai componenti dei moduli adattivi durante la conversione.

![](assets/meta-model.gif)

Il metamodello è uno schema JSON. Prima di iniziare con il metamodello, assicurati di avere una buona conoscenza di JSON. Devi avere esperienza nella creazione, modifica e lettura dei dati salvati in formato JSON.

## Metamodello predefinito {#default-meta-model}

Il servizio di automated forms conversion ha un metamodello predefinito. Si tratta di uno schema JSON e risiede in Adobe Cloud con altri componenti del servizio Automated forms conversion. Puoi trovare una copia del metamodello sul server AEM locale all&#39;indirizzo: http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/`global.schema.json`. È inoltre possibile [fai clic qui](assets/en.globalschema.json) per accedere o scaricare lo schema della lingua inglese. Il metamodello per [Francese](assets/fr.globalschema.json), [Tedesco](assets/de.globalschema.json) [Spagnolo](assets/es.globalschema.json), [Italiano](assets/it.globalschema.json)e [Portoghese](assets/pt_br.globalschema.json) sono disponibili anche le lingue per il download.

Lo schema del metamodello viene derivato dalle entità dello schema in https://schema.org/docs/schemas.html. Dispone di Persona, IndirizzoPostale, BusinessLocale e più entità come definito in https://schema.org. Ogni entità del metamodello aderisce al tipo di oggetto schema JSON. Il codice seguente rappresenta una struttura del metamodello di esempio:

```
   "Entity": {
      "id": "Entity",
      "properties": {
        "name": {
          "type": "string"
        },

        "description": {
          "type": "string",
          "description": "Description of the item"
        }
      }
    }
```

## Scarica il metamodello predefinito {#download-the-default-meta-model}

Esegui i seguenti passaggi per scaricare il metamodello predefinito nel file system locale:

1. Accedi alla tua istanza AEM Forms.
1. Passa a **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** **>** **[!UICONTROL Meta Model]** cartella.
1. Seleziona la **[!UICONTROL global.schema.json]** file e tocca **[!UICONTROL Download]**. Viene visualizzata una finestra di dialogo di download. Seleziona la **[!UICONTROL Download asset(s) as binary files]** opzione . Toccare **[!UICONTROL Download]**. Viene scaricato un archivio.

   <!--
   Comment Type: draft

   <li><p>Extract the archive and open the global.schema.json file for editing. </p> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

## Comprensione del metamodello {#understanding-the-meta-model}

Un metamodello si riferisce a un file di schema JSON che contiene entità. Tutte le entità nel file di schema JSON includono un nome e un id. Ciascuna entità può includere più proprietà. Le entità e le relative proprietà possono variare a seconda del dominio . È possibile integrare un file di schema con parole chiave e configurazioni di campi per mappare le proprietà dello schema ai componenti dei moduli adattivi.

```
"Event": {
      "id": "Eventid",
      "allOf": [
        {
          "$ref": "#Entity"
        },
        {
          "properties": {
            "startDate": {
              "type": "string",
              "format": "date",
              "description": "Specify the start date and time of the event in ISO 8601 date format."
            },
            "endDate": {
              "type": "string",
              "format": "date",
              "description": "Specify the end date and time of the event in ISO 8601 date format."
            },
            "location": {
              "$ref": "#PostalAddress",
              "description": "Specify the location of the event."
            }
          }
        }
      ]
    }
```

In questo esempio, **Evento** rappresenta il nome di un&#39;entità con un valore per **id** come **Eventid**. L’entità Evento include più proprietà:

* startDate
* endDate
* luogo

La **allOf** nel metamodello abilita l&#39;ereditarietà tra le entità.

Ogni proprietà può includere inoltre:

* [Proprietà dello schema JSON](#jsonschemaproperties)
* [Ricerca basata su parole chiave per applicare proprietà ai campi modulo adattivo generati](#keywordsearch)
* [Proprietà aggiuntive](#additionalproperties)

![Proprietà del metamodello](assets/meta_model_elements.gif)

In base alle parole chiave a cui si fa riferimento utilizzando **aem:affKeyword**, il servizio di conversione esegue un’operazione di ricerca nei campi del modulo di origine. Il servizio di conversione applica le proprietà dello schema JSON e le proprietà aggiuntive ai campi che soddisfano i criteri di ricerca.

In questo esempio, il servizio di conversione cerca il telefono, il telefono, il telefono cellulare, il telefono di lavoro, il telefono di casa, il numero di telefono, il numero di telefono e le parole chiave del numero di telefono nel modulo di origine. In base ai campi che includono queste parole chiave, il servizio di conversione applica il tipo, il pattern e aem:afProperties ai campi del modulo adattivo dopo la conversione.

### Proprietà dello schema JSON per i campi modulo adattivo generati {#jsonschemaproperties}

Il metamodello supporta le seguenti proprietà comuni dello schema JSON per i campi del modulo adattivo generati utilizzando il servizio di Automated forms conversion:

<table> 
 <tbody> 
  <tr> 
   <th><strong>Nome proprietà</strong></th> 
   <th><strong>Descrizione</strong></th> 
  </tr> 
  <tr> 
   <td><p>titolo</p></td> 
   <td> 
    <p>Il testo menzionato nella proprietà title in un metamodello funge da parola chiave di ricerca per eseguire azioni sui campi del modulo adattivo generati. Ad esempio, modificare l’etichetta di un campo modulo adattivo. Per ulteriori informazioni, consulta <strong>Modificare l’etichetta di un campo modulo</strong> in <a href="#custommetamodelexamples">Esempi di metamodello personalizzati.</a></p> </td> 
  </tr>
  <td><p>descrizione</p></td> 
   <td> 
    <p>La proprietà description imposta il testo della Guida per il campo modulo adattivo generato. Per ulteriori informazioni, consulta <strong>Aggiunta di testo della Guida a un campo modulo</strong> in <a href="#custommetamodelexamples">Esempi di metamodello personalizzati.</a></p> </td> 
  </tr>
  <td><p>tipo</p></td> 
   <td> 
    <p>La proprietà type definisce il tipo di dati per il campo modulo adattivo generato. I valori possibili per la proprietà title includono:</p>
    <ul> 
     <li>stringa: Genera un campo modulo adattivo del tipo di dati di testo.</li> 
     <li>numero: Genera un campo modulo adattivo di tipo dati numerico.</li>
     <li>numero intero: Genera un campo modulo adattivo di tipo dati numerico con sottotipo impostato su integer.</li>
     <li>booleano: Genera un componente per modulo adattivo per switch.</li>
     </ul><p>Per ulteriori informazioni sull'utilizzo della proprietà type in un metamodello, vedere <strong>Modificare il tipo di campo modulo</strong> in <a href="#custommetamodelexamples">Esempi di metamodello personalizzati.</a></p></td> 
  </tr>
  <td><p>pattern</p></td> 
   <td> 
    <p>La proprietà pattern limita il valore del campo modulo adattivo generato in base a un’espressione regolare. Ad esempio, il seguente codice nel metamodello limita il valore del campo modulo adattivo generato a dieci cifre:<br>"pattern": "/\\d{10}/"<br>Analogamente, il seguente codice nel metamodello limita il valore di un campo a un formato di data specifico.<br> "pattern": "date{DD MMMM, AAAA}",</p> </td> 
  </tr>
  <td><p>format</p></td> 
   <td> 
    <p>La proprietà format limita il valore del campo modulo adattivo generato in base a un pattern denominato anziché a un’espressione regolare. I valori possibili per la proprietà format includono:<ul><li>e-mail: Genera un componente modulo adattivo per e-mail.</li><li>hostname: Genera un componente modulo adattivo casella di testo.</li></ul>Per ulteriori informazioni sull'utilizzo della proprietà format in un metamodello, vedere <strong>Modificare il formato di un campo modulo</strong> in <a href="#custommetamodelexamples">Esempi di metamodello personalizzati.</a></p> </td> 
  </tr>
  <td><p>enum e enumNames</p></td> 
   <td> 
    <p>Le proprietà enum e enumNames limitano i valori dei campi a discesa, casella di controllo o pulsante di scelta a un set fisso. I valori elencati in enumNames vengono visualizzati sull'interfaccia utente. I valori elencati utilizzando la proprietà enum vengono utilizzati per il calcolo.<br>Per ulteriori informazioni, consulta <strong>Convertire un campo modulo in caselle di controllo a scelta multipla nel modulo adattivo</strong>, <strong>Convertire un campo di testo in un elenco a discesa nel modulo adattivo</strong>e <strong>Aggiungi ulteriori opzioni all’elenco a discesa</strong> in <a href="#custommetamodelexamples">Esempi di metamodello personalizzati.</a></p> </td> 
  </tr>
 </tbody> 
</table>

### Ricerca basata su parole chiave per applicare proprietà ai campi modulo adattivo generati {#keywordsearch}

Il servizio di automated forms conversion esegue una ricerca per parola chiave nel modulo di origine durante la conversione. Dopo aver filtrato i campi che soddisfano i criteri di ricerca, il servizio di conversione applica le proprietà definite per tali campi nel metamodello ai campi del modulo adattivo generato.

Le parole chiave sono referenziate utilizzando **aem:affKeyword** proprietà.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

In questo esempio, il servizio di conversione utilizza il testo all’interno di **aem:affKeyword** come parola chiave di ricerca. Dopo aver recuperato il **Numero del conto bancario** nel modulo, il servizio di conversione converte il campo in un **numero** utilizzando **type** proprietà.

### Proprietà aggiuntive per i campi modulo adattivo generati {#additionalproperties}

È possibile utilizzare **aem:afProperties** nel metamodello per definire le seguenti proprietà aggiuntive per i campi dei moduli adattivi generati utilizzando il servizio Automated forms conversion:

<table> 
 <tbody> 
  <tr> 
   <th><strong>Nome proprietà</strong></th> 
   <th><strong>Descrizione</strong></th> 
  </tr> 
  <tr> 
   <td><p>multiLine</p></td> 
   <td> 
    <p>La proprietà multiLine converte un campo modulo di origine in un campo a più righe nel modulo adattivo dopo la conversione. Per ulteriori informazioni, consulta <strong>Convertire un campo stringa in un campo a più righe</strong> in <a href="#custommetamodelexamples">Esempi di metamodello personalizzati.</a></p> </td> 
  </tr>
  <td><p>mandatory</p></td> 
   <td> 
    <p>La proprietà mandatory imposta come obbligatorio l’input per un campo modulo adattivo dopo la conversione.<br>Per ulteriori informazioni, consulta <strong>Aggiungere convalide ai campi del modulo adattivo</strong> in <a href="#custommetamodelexamples">Esempi di metamodello personalizzati.</a></p>
    </td> 
  </tr>
  <td><p>jcr:title</p></td> 
   <td> 
    <p>La proprietà jcr:title, con la proprietà dello schema JSON del titolo, consente di modificare l’etichetta di un campo modulo adattivo dopo la conversione.<br>Per ulteriori informazioni, consulta <strong>Modificare l’etichetta di un campo modulo</strong> in <a href="#custommetamodelexamples">Esempi di metamodello personalizzati.</a><br>Vedi <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html" target="_blank">Creazione di moduli adattivi tramite lo schema JSON</a> per informazioni su più proprietà che è possibile applicare ai campi del modulo adattivo utilizzando lo schema JSON.</p>
    <p></p></td> 
  </tr>
  <td><p>sling:resourceType e guideNodeClass</p></td> 
   <td> 
    <p>le proprietà sling:resourceType e guideNodeClass consentono di mappare un campo modulo a un componente modulo adattivo corrispondente.<br>Per ulteriori informazioni, consulta <strong>Convertire un campo modulo in caselle di controllo a scelta multipla nel modulo adattivo</strong> e <strong>Convertire un campo di testo in un elenco a discesa nel modulo adattivo</strong> in <a href="#custommetamodelexamples">Esempi di metamodello personalizzati.</a></p> </td> 
  </tr>
  <td><p>validatePictureClause</p></td> 
   <td> 
    <p>La proprietà validatePictureClause imposta una convalida sul formato consentito nel campo modulo adattivo dopo la conversione.<br>Per ulteriori informazioni, consulta <strong>Aggiungere convalide ai campi del modulo adattivo</strong> in <a href="#custommetamodelexamples">Esempi di metamodello personalizzati.</p> </td> 
  </tr>
 </tbody> 
</table>

## Creare un modello di metamodello personalizzato nella propria lingua{#language-specific-meta-model}

È possibile creare un metamodello specifico per il linguaggio. Questo metamodello consente di creare regole di mappatura nel linguaggio desiderato. Il servizio di automated forms conversion consente di creare metamodello nelle seguenti lingue:

* Inglese (en)
* Francese (fr)
* Tedesco (de)
* Spagnolo (es)
* Italiano (it)
* Portoghese (pt-br)

Aggiungi il *aem:Language* tag metatag nella parte superiore di un metamodello per specificarne la lingua. Ad esempio:

```JSON
"metaTags": {
        "aem:Language": "fr"
    }
```

Quando non viene specificata alcuna lingua, il servizio considera che il metamodello sia in lingua inglese.

### Considerazioni sulla creazione di un metamodello specifico per il linguaggio

* Assicurati che il nome di ogni chiave sia in lingua inglese. Ad esempio, emailAddress.
* Assicurati che tutti i riferimenti di entità e i valori predefiniti di tutte le chiavi id comprendano solo caratteri ASCII. Ad esempio &quot;id&quot;: &quot;ContactPoint&quot; / &quot;$ref&quot;: &quot;#ContactPoint&quot;.
* Assicurati che tutti i valori corrispondenti alle seguenti chiavi siano nel linguaggio del metamodello specificato:
   * aem:affKeyword
   * titolo
   * descrizione
   * enumNames
   * shortDescription
   * validatePictureClauseMessage

   Ad esempio, quando la lingua del metamodello è francese (&quot;aem:Language&quot;): &quot;fr&quot;), garantire che tutte le descrizioni e i messaggi siano in lingua francese.

* Assicurati che [Proprietà dello schema JSON](#jsonschemaproperties) utilizza solo i valori supportati. Ad esempio, la proprietà type può estendere solo i valori selezionati di String, Number, Integer e Boolean.

L&#39;immagine seguente mostra alcuni esempi di metamodello in lingua inglese e del corrispondente metamodello in lingua francese:

![](assets/language-specific-meta-model-comparison.png)

## Modificare i campi del modulo adattivo utilizzando il metamodello personalizzato {#modify-adaptive-form-fields-using-custom-meta-model}

L&#39;organizzazione può disporre di pattern e convalide oltre a quelli elencati nel metamodello predefinito. È possibile estendere il metamodello predefinito per aggiungere pattern, convalide ed entità specifici all’organizzazione. Il servizio automated forms conversion applica il metamodello personalizzato ai campi del modulo durante la conversione. È possibile continuare ad aggiornare il metamodello man mano che vengono rilevati nuovi pattern, convalide ed entità specifici per la propria organizzazione.

Il servizio di automated forms conversion utilizza un metamodello predefinito salvato nel percorso seguente per mappare i campi del modulo di origine ai campi del modulo adattivo durante la conversione:

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json

Tuttavia, puoi salvare un metamodello personalizzato in una cartella e modificare le proprietà del servizio di conversione per utilizzare il metamodello personalizzato durante la conversione.

### Utilizza un metamodello personalizzato durante la conversione {#use-custom-meta-model-during-conversion}

Esegui i seguenti passaggi per utilizzare un metamodello personalizzato durante la conversione:

1. Crea una cartella in **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** e carica il file di schema JSON del metamodello personalizzato nella cartella .
1. Apri le proprietà del servizio di conversione utilizzando:

   **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **&lt;properties of=&quot;&quot; selected=&quot;&quot; configuration=&quot;&quot;>**

1. In **[!UICONTROL Basic]** , specifica la posizione del metamodello personalizzato nel **[!UICONTROL Custom Meta-model]** campo e tocco **[!UICONTROL Save & Close]**.
1. [Eseguire la conversione](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) per applicare il metamodello personalizzato al processo di conversione.

### Esempi di metamodello personalizzati {#custommetamodelexamples}

Alcuni esempi comuni di utilizzo di un metamodello personalizzato per modificare le proprietà dei campi del modulo adattivo includono:

* Modificare l’etichetta di un campo modulo
* Modificare il tipo di campo modulo
* Aggiunta di testo della Guida a un campo modulo
* Convertire un campo modulo in pulsanti di scelta a scelta multipla nel modulo adattivo
* Modificare il formato di un campo modulo
* Aggiungere convalide ai campi del modulo adattivo
* Convertire un campo modulo in opzioni elenco a discesa nel modulo adattivo
* Aggiungi ulteriori opzioni all’elenco a discesa
* Convertire un campo stringa in un campo a più righe

#### Modificare l’etichetta di un campo modulo {#modify-the-label-of-a-form-field}

**Esempio:** Modificare l’etichetta del numero di conto bancario nel modulo in Numero di conto personalizzato nel modulo adattivo dopo la conversione.

In questo metamodello personalizzato, il servizio di conversione utilizza il **title** come parola chiave di ricerca. Dopo aver recuperato il **Numero del conto bancario** nel modulo, il servizio di conversione sostituisce il testo con il **Numero dell&#39;account cliente** stringa menzionata con **jcr:title** nella **aem:afProperties** sezione .

```
{
  "numberfields": {
      "type": "number",
   "title": "Bank account number",
   "aem:afProperties" : {
    "jcr:title" : "Customer account number"
   }
   }
}
```

#### Modificare il tipo di campo modulo {#modify-the-type-of-a-form-field}

**Esempio**: Modifica la **Numero del conto bancario** campo del tipo di testo nel modulo prima della conversione in un campo del tipo di numero nel modulo adattivo dopo la conversione.

In questo metamodello personalizzato, il servizio di conversione utilizza il testo all’interno di **aem:affKeyword** come parola chiave di ricerca. Dopo aver recuperato il **Numero del conto bancario** nel modulo, il servizio di conversione converte il campo in un tipo di numero utilizzando **type** proprietà.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

#### Aggiunta di testo della Guida a un campo modulo {#add-help-text-to-a-form-field}

**Esempio**: Aggiungi il testo della Guida al **Numero del conto bancario** campo del modulo adattivo.

In questo metamodello personalizzato, il servizio di conversione utilizza il testo all’interno di **aem:affKeyword** come parola chiave di ricerca. Dopo aver recuperato il **Numero del conto bancario** nel modulo, il servizio di conversione aggiunge il testo della Guida al campo del modulo adattivo utilizzando **descrizione** proprietà.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "description": "Specify your bank account number."
 }
}
```

#### Convertire un campo modulo in caselle di controllo a scelta multipla nel modulo adattivo {#convert-a-form-field-to-multiple-choice-check-boxes-in-the-adaptive-form}

**Esempio**: Converti **Paese** campo di tipo stringa nel modulo prima della conversione in caselle di controllo nel modulo adattivo dopo la conversione.

In questo metamodello personalizzato, il servizio di conversione utilizza il testo all&#39;interno di **aem:affKeyword** come parola chiave di ricerca. Dopo aver recuperato il **Paese** nel modulo, il servizio di conversione converte il campo nelle seguenti caselle di controllo utilizzando **enum** proprietà:

* India
* Inghilterra
* Australia
* Nuova Zelanda

**sling:resourceType** e **guideNodeClass** le proprietà mappano un campo modulo al componente modulo adattivo della casella di controllo.

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidecheckbox",
      "guideNodeClass": "guidecheckbox"
    }
  }
}
```

#### Modificare il formato di un campo modulo {#modify-the-format-of-a-form-field}

**Esempio**: Modificare il formato del **Indirizzo e-mail** in un formato e-mail.

In questo metamodello personalizzato, il servizio di conversione utilizza il testo all&#39;interno di **aem:affKeyword** come parola chiave di ricerca. Dopo aver recuperato il **Indirizzo e-mail** nel modulo, il servizio di conversione converte il campo in un formato e-mail utilizzando **format** proprietà.

```
{
   "additionalDetails" : {
      "aem:affKeyword": ["E-mail Address"],
       "type" : "string",
       "format" : "email"
  } 
}
```

#### Aggiungere convalide ai campi del modulo adattivo {#add-validations-to-adaptive-form-fields}

**Esempio 1:** Aggiungi una convalida al **Codice postale** del modulo adattivo.

In questo metamodello personalizzato, il servizio di conversione utilizza il testo all&#39;interno di **aem:affKeyword** come parola chiave di ricerca. Dopo aver recuperato il **Codice postale** nel modulo, il servizio di conversione aggiunge una convalida al campo utilizzando **validatePictureClause** definita nella **aem:afProperties** sezione . In base alla convalida, l’input specificato per **Codice postale** nel modulo adattivo dopo la conversione deve essere presente sei caratteri.

```
{
   "postalCode" : {
      "aem:affKeyword": ["Postal Code"],
      "type" : "string",
      "aem:afProperties" : {
        "validatePictureClause" : "\\d{6}"
      } 
   }
}
```

**Esempio 2:** Aggiungi una convalida al **Numero del conto bancario** del modulo adattivo.

In questo metamodello personalizzato, il servizio di conversione utilizza il testo all&#39;interno di **aem:affKeyword** come parola chiave di ricerca. Dopo aver recuperato il **Numero del conto bancario** nel modulo, il servizio di conversione aggiunge una convalida al campo utilizzando **obbligatorio** definita nella **aem:afProperties** sezione . In base alla convalida, è necessario specificare un valore per **Numero del conto bancario** prima di inviare il modulo dopo la conversione.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "aem:afProperties" : {
        "mandatory": "true"
      }   
   }
}
```

#### Convertire un campo di testo in un elenco a discesa nel modulo adattivo {#convert-a-text-field-to-drop-down-list-in-the-adaptive-form}

**Esempio**: Converti **Paese** campo di tipo stringa nel modulo prima della conversione in opzioni a discesa nel modulo adattivo dopo la conversione.

In questo metamodello personalizzato, il servizio di conversione utilizza il testo all&#39;interno di **aem:affKeyword** come parola chiave di ricerca. Dopo aver recuperato il **Paese** nel modulo, il servizio di conversione converte il campo nelle seguenti opzioni dell’elenco a discesa utilizzando **enum** proprietà:

* India
* Inghilterra
* Australia
* Nuova Zelanda

**sling:resourceType** e **guideNodeClass** le proprietà mappano un campo modulo al componente modulo adattivo a discesa.

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidedropdownlist",
      "guideNodeClass": "guideDropDownlist"
    }
  }
}
```

#### Aggiungi ulteriori opzioni all’elenco a discesa {#add-additional-options-to-the-drop-down-list}

**Esempio:** Aggiungi **Sri Lanka** come opzione aggiuntiva per un elenco a discesa esistente utilizzando un metamodello personalizzato.

Per aggiungere un’opzione aggiuntiva, aggiorna la sezione **enum** con la nuova opzione. In questo esempio, aggiorna la **enum** proprietà con **Sri Lanka** come opzione aggiuntiva. Valori elencati in **enum** nell&#39;elenco a discesa.

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand",
   "Sri Lanka"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidecheckbox",
      "guideNodeClass": "guidecheckbox"
    }
  }
}
```

#### Convertire un campo stringa in un campo a più righe {#convert-a-string-field-to-a-multi-line-field}

**Esempio:** Converti **Indirizzo** campo di tipo stringa in un campo a più righe nel modulo dopo la conversione.

In questo metamodello personalizzato, il servizio di conversione utilizza il testo all&#39;interno di **aem:affKeyword** come parola chiave di ricerca. Dopo aver recuperato il **Indirizzo** nel modulo, il servizio converte il campo di testo in un campo a più righe utilizzando **multiLine** definita nella **aem:afProperties** sezione .

```
{
 "multiLine" : {
   "aem:affKeyword": [
      "Address"
    ],
    "type" : "string",
    "aem:afProperties": {
      "multiLine": "true"
    }
  }
}
```
