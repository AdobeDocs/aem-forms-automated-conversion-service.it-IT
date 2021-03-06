---
title: Inviare i moduli adattivi convertiti con uno schema JSON al database
description: Inviare i moduli adattivi convertiti con uno schema JSON al database creando un modello dati modulo e facendone riferimento in un flusso di lavoro AEM.
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: c552f4073ac88ca9016a746116a27a5898df7f7d
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 2%

---


# Integrazione del modulo adattivo con il database utilizzando workflow AEM {#submit-forms-to-database-using-forms-portal}

Il servizio di automated forms conversion consente di convertire un modulo PDF non interattivo, un modulo Acro o un modulo PDF basato su XFA in un modulo adattivo. Quando si avvia il processo di conversione, è possibile generare un modulo adattivo con o senza binding dei dati.

Se si sceglie di generare un modulo adattivo senza binding dei dati, è possibile integrare il modulo adattivo convertito con un modello dati modulo, uno schema XML o uno schema JSON dopo la conversione. Per il modello dati del modulo, è necessario associare manualmente i campi modulo adattivi al modello dati del modulo. Tuttavia, se si genera un modulo adattivo con binding dei dati, il servizio di conversione associa automaticamente i moduli adattivi a uno schema JSON e crea un binding dei dati tra i campi disponibili nel modulo adattivo e nello schema JSON. È quindi possibile integrare il modulo adattivo con un database di propria scelta, compilare i dati del modulo e inviarlo al database. Analogamente, dopo l&#39;integrazione con il database, è possibile configurare i campi del modulo adattivo convertito per recuperare i valori dal database e precompilare i campi del modulo adattivo.

La figura seguente illustra diverse fasi dell&#39;integrazione di un modulo adattivo convertito con un database:

![integrazione del database](assets/integrate-adaptive-form-with-database.png)

Questo articolo descrive le istruzioni dettagliate per eseguire correttamente tutte queste fasi di integrazione.

## Prerequisiti {#pre-requisites}

* Impostazione di un’istanza di creazione AEM 6.4 o 6.5
* Installare [l&#39;ultimo service pack](https://helpx.adobe.com/it/experience-manager/aem-releases-updates.html) per l&#39;istanza AEM
* Ultima versione del pacchetto  del componente aggiuntivo AEM Forms
* Configurare il servizio di Automated forms conversion [](configure-service.md)
* Configurare un database. Il database utilizzato nell&#39;implementazione di esempio è MySQL 5.6.24. Tuttavia, è possibile integrare il modulo adattivo convertito con qualsiasi database di propria scelta.

## Esempio di modulo adattivo {#sample-adaptive-form}

Per eseguire l&#39;esempio di utilizzo per integrare moduli adattivi convertiti nel database utilizzando un flusso di lavoro AEM, scaricare il seguente file PDF di esempio.

È possibile scaricare il modulo Contattaci di esempio utilizzando:

[Ottieni file](assets/sample_contact_us_form.pdf)

Il file PDF funge da input per il servizio Automated forms conversion. Il servizio converte questo file in un modulo adattivo. Nell&#39;immagine seguente è illustrato l&#39;esempio di modulo di contatto in formato PDF.

![modulo di richiesta di prestito di esempio](assets/sample_contact_us_form.png)

## Installare il file mysql-Connector-java-5.1.39-bin.jar {#install-mysql-connector-java-file}

Per installare il file mysql-Connector-java-5.1.39-bin.jar, eseguite i seguenti passaggi su tutte le istanze di creazione e pubblicazione:

1. Andate a `http://server:port/system/console/depfinder` e cercate il pacchetto com.mysql.jdbc.
1. Nella colonna Esportato da, verificate che il pacchetto sia esportato da un pacchetto qualsiasi. Continuate se il pacchetto non viene esportato da alcun bundle.
1. Passare a `http://server:port/system/console/bundles` e fare clic su **[!UICONTROL Install/Update]**.
1. Fate clic su **[!UICONTROL Choose File]** e selezionate il file mysql-Connector-java-5.1.39-bin.jar. Selezionare inoltre le caselle di controllo **[!UICONTROL Start Bundle]** e **[!UICONTROL Refresh Packages]**.
1. Fare clic su **[!UICONTROL Install]** o **[!UICONTROL Update]**. Al termine, riavviare il server.
1. (Solo Windows) Disattivate il firewall di sistema del sistema operativo in uso.

## Preparare i dati per il modello di modulo {#prepare-data-for-form-model}

 Integrazione dei dati AEM Forms consente di configurare e connettersi a origini dati diverse. Dopo aver generato un modulo adattivo utilizzando il processo di conversione, è possibile definire il modello di modulo in base a un modello dati del modulo, a uno schema XSD o JSON. È possibile utilizzare un database, Microsoft Dynamics o qualsiasi altro servizio di terze parti per creare un modello dati del modulo.

Questa esercitazione utilizza il database MySQL come origine per creare un modello dati del modulo. Create uno schema nel database e aggiungete la tabella **contactus** allo schema in base ai campi disponibili nel modulo adattivo.

![Dati di esempio mysql](assets/db_entries_sample_form.png)

È possibile utilizzare la seguente istruzione DDL per creare la tabella **contactus** nel database.

```sql
CREATE TABLE `contactus` (
   `name` varchar(45) NOT NULL,
   `email` varchar(45) NOT NULL,
   `phonenumber` varchar(10) DEFAULT NULL,
   `issuedesc` varchar(1000) DEFAULT NULL,
   PRIMARY KEY (`email`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

## Configurare la connessione tra AEM&#39;istanza e il database {#configure-connection-between-aem-instance-and-database}

Per creare una connessione tra AEM&#39;istanza e il database MYSQL, eseguire i seguenti passaggi di configurazione:

1. Vai AEM pagina Configurazione console Web all&#39;indirizzo `http://server:port/system/console/configMgr`.
1. Trova e fai clic per aprire **[!UICONTROL Apache Sling Connection Pooled DataSource]** in modalità di modifica nella configurazione della console Web. Specificare i valori delle proprietà come descritto nella tabella seguente:

   <table> 
    <tbody> 
    <tr> 
    <th><strong>Proprietà</strong></th> 
    <th><strong>Valore</strong></th> 
    </tr> 
    <tr> 
    <td><p>Nome origine dati</p></td> 
    <td><p>Nome origine dati per filtrare i driver dal pool di origini dati.</p></td>
    </tr>
    <tr> 
    <td><p>Classe driver JDBC</p></td> 
    <td><p>com.mysql.jdbc.Driver</p></td>
    </tr>
    <tr> 
    <td><p>URI connessione JDBC</p></td> 
    <td><p>jdbc:mysql://[host]:[porta]/[nome_schema]</p></td>
    </tr>
    <tr> 
    <td><p>Nome utente</p></td> 
    <td><p>Un nome utente per l'autenticazione e l'esecuzione di azioni sulle tabelle del database</p></td>
    </tr>
    <tr> 
    <td><p>Password</p></td> 
    <td><p>Password associata al nome utente</p></td>
    </tr>
    <tr> 
    <td><p>Isolamento transazione</p></td> 
    <td><p>READ_COMMTED</p></td>
    </tr>
    <tr> 
    <td><p>Numero massimo di connessioni attive</p></td> 
    <td><p>1000</p></td>
    </tr>
    <tr> 
    <td><p>Numero massimo di connessioni inattive</p></td> 
    <td><p>100</p></td>
    </tr>
    <tr> 
    <td><p>Connessioni con inattività minima</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>Dimensione iniziale</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>Max</p></td> 
    <td><p>100000</p></td>
    </tr>
     <tr> 
    <td><p>Test di credito</p></td> 
    <td><p>Selezionato</p></td>
    </tr>
     <tr> 
    <td><p>Test while Idle</p></td> 
    <td><p>Selezionato</p></td>
    </tr>
     <tr> 
    <td><p>Query convalida</p></td> 
    <td><p>I valori di esempio sono SELECT 1(mysql), select 1 from dual( oracle), SELECT 1(MS Sql Server) (validationQuery)</p></td>
    </tr>
     <tr> 
    <td><p>Timeout query di convalida</p></td> 
    <td><p>10000</p></td>
    </tr>
    </tbody> 
    </table>

## Crea modello dati modulo {#create-form-data-model}

Una volta configurato MYSQL come origine dati, eseguire i seguenti passaggi per creare un modello dati modulo:

1. Nell&#39;istanza di AEM autore, andate a **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**.

1. Toccare **[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**.

1. Nella procedura guidata **[!UICONTROL Create Form Data Model]**, specificare **workflow_submit** come nome per il modello dati del modulo. Toccare **[!UICONTROL Next]**.

1. Selezionare l&#39;origine dati MYSQL configurata nella sezione precedente e toccare **[!UICONTROL Create]**.

1. Toccate **[!UICONTROL Edit]** ed espandete l&#39;origine dati elencata nel riquadro a sinistra per selezionare la tabella **contactus**, **[!UICONTROL get]** e i servizi **[!UICONTROL insert]**, quindi toccate **[!UICONTROL Add Selected]**.

   ![Dati di esempio mysql](assets/fdm_details_workfdlow_submit.png)

1. Selezionare l&#39;oggetto modello dati nel riquadro a destra e toccare **[!UICONTROL Edit Properties]**. Selezionare **[!UICONTROL get]** e **[!UICONTROL insert]** dagli elenchi a discesa **[!UICONTROL Read Service]** e **[!UICONTROL Write Service]**. Specificare gli argomenti per il servizio di lettura e toccare **[!UICONTROL Done]**.

1. Nella scheda **[!UICONTROL Services]**, selezionare il servizio **[!UICONTROL get]** e toccare **[!UICONTROL Edit Properties]**. Selezionare la **[!UICONTROL Output Model Object]**, disabilitare l&#39;interruttore **[!UICONTROL Return array]** e toccare **[!UICONTROL Done]**.

1. Selezionare il servizio **[!UICONTROL Insert]** e toccare **[!UICONTROL Edit Properties]**. Selezionare il **[!UICONTROL Input Model Object]** e toccare **[!UICONTROL Done]**.

1. Toccare **[!UICONTROL Save]** per salvare il modello dati del modulo.

È possibile scaricare il modello dati modulo di esempio utilizzando:

[Ottieni file](assets/DownloadedFormsPackage_1497728018502500.zip)

## Generazione di moduli adattivi con binding JSON {#generate-adaptive-forms-with-json-binding}

Utilizzare il servizio [Automated forms conversion per convertire ](convert-existing-forms-to-adaptive-forms.md) il modulo [Contatti](#sample-adaptive-form) in un modulo adattivo con binding dei dati. Assicurarsi di non selezionare la casella di controllo **[!UICONTROL Generate adaptive form(s) without data bindings]** durante la generazione del modulo adattivo.

![Modulo adattivo con binding JSON](assets/generate_af_with_data_bindings.png)

Selezionare il modulo **Contatti** convertito disponibile nella cartella **[!UICONTROL output]** in **[!UICONTROL Forms & Documents]** e toccare **[!UICONTROL Edit]**. Toccate **[!UICONTROL Preview]**, immettete i valori nei campi modulo adattivo e toccate **[!UICONTROL Submit]**.

Accedete a **crx-repository** e andate a */content/forms/fp/admin/submit/data* per visualizzare i valori inviati in formato JSON. Di seguito sono riportati i dati di esempio in formato JSON quando si invia il modulo adattivo **Contact Us** convertito:

```json
{
  "afData": {
    "afUnboundData": {
      "data": {}
    },
    "afBoundData": {
      "data": {
        "name1": "Gloria",
        "email": "abc@xyz.com",
        "phone_number": "2346578965",
        "issue_description": "Test message"
      }
    },
    "afSubmissionInfo": {
      "computedMetaInfo": {},
      "stateOverrides": {},
      "signers": {},
      "afPath": "/content/dam/formsanddocuments/docs_conversion/output/sample_form_json",
      "afSubmissionTime": "20191204014007"
    }
  }
}
```

È necessario creare un modello di workflow che possa elaborare i dati e inviarli al database MYSQL utilizzando il modello dati modulo creato nelle sezioni precedenti.

## Creare un modello di workflow per l&#39;elaborazione dei dati JSON {#create-workflow-model}

Per creare un modello di workflow per l&#39;invio dei dati del modulo adattivo al database, eseguire la procedura seguente:

1. Aprite la console Modelli di workflow. L&#39;URL predefinito è `https://server:port/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`.

1. Selezionare **[!UICONTROL Create]**, quindi **[!UICONTROL Create Model]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Add Workflow Model]**.

1. Immettere **[!UICONTROL Title]** e **[!UICONTROL Name]** (facoltativo). Ad esempio, **workflow_json_submit**. Toccate **[!UICONTROL Done]** per creare il modello.

1. Selezionate il modello di workflow e toccate **[!UICONTROL Edit]** per aprire il modello in modalità di modifica. Toccate + e aggiungete il passaggio **[!UICONTROL Invoke Form Data Model Service]** al modello di workflow.

1. Toccate il passaggio **[!UICONTROL Invoke Form Data Model Service]** e toccate ![Configura](assets/configure_icon.png).

1. Nella scheda **[!UICONTROL Form Data Model]**, selezionare il modello dati del modulo creato nel campo **[!UICONTROL Form Data Model path]**, quindi selezionare **[!UICONTROL insert]** dall&#39;elenco a discesa **[!UICONTROL Service]**.

1. Nella scheda **[!UICONTROL Input for Service]**, selezionare **[!UICONTROL Provide input data using literal, variable, or a workflow metadata, and a JSON file]** dall&#39;elenco a discesa, selezionare la casella di controllo **[!UICONTROL Map input fields from input JSON]**, selezionare **[!UICONTROL Relative to payload]** e fornire **data.xml** come valore per il campo **[!UICONTROL Select input JSON document using]**.

1. Nella sezione **[!UICONTROL Service Arguments]**, fornire i seguenti valori per gli argomenti del modello dati del modulo:

   ![Richiama il servizio del modello di dati modulo](assets/invoke_form_data_model_service.png)

   Tenere presente che i campi del modello dati del modulo, ad esempio il nome del punto di contatto, sono mappati su **afData.afBoundData.data.name1**, che fa riferimento ai binding dello schema JSON per il modulo adattivo inviato.

## Configurare l&#39;invio del modulo adattivo {#configure-adaptive-form-submission}

Per inviare il modulo adattivo al modello di flusso di lavoro creato nella sezione precedente, eseguite i seguenti passaggi:

1. Selezionare il modulo Contatti convertito disponibile nella cartella **[!UICONTROL output]** in **[!UICONTROL Forms & Documents]** e toccare **[!UICONTROL Edit]**.

1. Aprire le proprietà del modulo adattivo toccando **[!UICONTROL Form Container]**, quindi toccando ![Configura](assets/configure_icon.png).

1. Nella sezione **[!UICONTROL Submission]**, selezionare **[!UICONTROL Invoke an AEM workflow]** dall&#39;elenco a discesa **[!UICONTROL Submit Action]**, selezionare il modello di workflow creato nella sezione precedente e specificare **data.xml** nel campo **[!UICONTROL Data File Path]**.

1. Toccate ![Salva](assets/save_icon.png) per salvare le proprietà.

1. Toccate **[!UICONTROL Preview]**, immettete i valori nei campi modulo adattivo e toccate **[!UICONTROL Submit]**. I valori inviati ora vengono visualizzati nella tabella del database MYSQL invece di **crx-repository**.

## Configurare il modulo adattivo per precompilare i valori dal database

Per configurare il modulo adattivo per la precompilazione dei valori del database MYSQL in base alla chiave primaria definita nella tabella, eseguire la procedura seguente (in questo caso, E-mail):

1. Toccate il campo **E-mail** nel modulo adattivo e toccate ![Modifica regola](assets/edit-rules.png).

1. Toccate **[!UICONTROL Create]** e selezionate **[!UICONTROL is changed]** dall&#39;elenco a discesa **[!UICONTROL Select State]** nella sezione **[!UICONTROL When]**.

1. Nella sezione **[!UICONTROL Then]**, selezionare **[!UICONTROL Invoke Service]** e **get** come servizio per il modello dati modulo creato in una sezione precedente di questo articolo.

1. Selezionare **E-mail** nella sezione **[!UICONTROL Input]** e gli altri tre campi del modello dati modulo, **Nome**, **Numero di telefono** e **Descrizione problema** nella sezione **[!UICONTROL Output]**. Toccate **[!UICONTROL Done]** per salvare le impostazioni.

   ![Configurare le impostazioni di precompilazione e-mail](assets/email_prefill_settings.png)

   Di conseguenza, in base alle voci E-mail esistenti nel database MYSQL, è possibile precompilare i valori per gli altri tre campi nella modalità **[!UICONTROL Preview]** del modulo adattivo. Ad esempio, se si specifica aya.tan@xyz.com nel campo **E-mail** (basato sui dati esistenti nella sezione [Prepara modello dati modulo](#prepare-data-for-form-model) di questo articolo) e si seleziona il campo, vengono visualizzati i tre campi rimanenti, **Nome**, **Numero di telefono** e **Descrizione problema** automaticamente nel modulo adattivo.

È possibile scaricare il modulo adattivo convertito di esempio utilizzando:

[Ottieni file](assets/DownloadedFormsPackage_1498226829041200.zip)
