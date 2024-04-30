---
title: Inviare moduli adattivi al database tramite Forms Portal
description: Estendi il metamodello predefinito per aggiungere pattern, convalide ed entità specifiche per la tua organizzazione e applica le configurazioni ai campi dei moduli adattivi durante l’esecuzione del servizio di Automated forms conversion (AFCS).
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 1%

---


# Integrare i moduli adattivi con il database utilizzando Forms Portal {#submit-forms-to-database-using-forms-portal}

Il servizio di automated forms conversion (AFCS) consente di convertire un modulo di PDF non interattivo, un modulo Acro o un modulo di PDF basato su XFA in un modulo adattivo. Quando si avvia il processo di conversione, è possibile generare un modulo adattivo con o senza associazioni di dati.

Se scegli di generare un modulo adattivo senza associazioni di dati, puoi integrare il modulo adattivo convertito con un modello di dati modulo, uno schema XML o uno schema JSON dopo la conversione. Tuttavia, se generi un modulo adattivo con associazioni di dati, il servizio di conversione associa automaticamente i moduli adattivi a uno schema JSON e crea un’associazione di dati tra i campi disponibili nel modulo adattivo e lo schema JSON. Puoi quindi integrare il modulo adattivo con un database a tua scelta, compilare i dati nel modulo e inviarlo al database utilizzando il portale Forms.

La figura seguente illustra diverse fasi dell’integrazione di un modulo adattivo convertito con un database tramite Forms Portal:

![integrazione del database](assets/database_integration.gif)

Questo articolo descrive le istruzioni dettagliate per eseguire correttamente tutte queste fasi di integrazione.

L&#39;esempio, discusso in questo articolo, è un&#39;implementazione di riferimento di dati e servizi di metadati personalizzati per integrare una pagina di Forms Portal con un database. Il database utilizzato nell&#39;implementazione di esempio è MySQL 5.6.24. È tuttavia possibile integrare la pagina di Forms Portal con qualsiasi database desiderato.

## Prerequisiti {#pre-requisites}

* Configurare un’istanza di authoring AEM 6.4 o 6.5
* Installa [service pack più recente](https://helpx.adobe.com/it/experience-manager/aem-releases-updates.html) per l’istanza AEM
* Versione più recente del pacchetto del componente aggiuntivo AEM Forms
* Configura [Servizio di automated forms conversion (AFCS)](configure-service.md)
* Configurare un database. Il database utilizzato nell&#39;implementazione di esempio è MySQL 5.6.24. Tuttavia, puoi integrare il modulo adattivo convertito con qualsiasi database di tua scelta.

## Configurare la connessione tra l’istanza AEM e il database {#set-up-connection-aem-instance-database}

L&#39;impostazione di una connessione tra un&#39;istanza AEM e un database MYSQL consiste in:

* [Installazione di un pacchetto del connettore MYSQL](#install-mysql-connector-java-file)

* [Creazione di schemi e tabelle nel database](#create-schema-and-tables-in-database)

* [Configurazione delle impostazioni di connessione](#configure-connection-between-aem-instance-and-database)

* [Impostazione e configurazione del pacchetto di esempio per l’integrazione con Forms Portal](#set-up-and-configure-sample)

### Installare il file mysql-connector-java-5.1.39-bin.jar {#install-mysql-connector-java-file}

Per installare il file mysql-connector-java-5.1.39-bin.jar, su tutte le istanze di authoring e pubblicazione, effettua le seguenti operazioni:

1. Passa a http://[server]:[porta]/system/console/depfinder e cercare il pacchetto com.mysql.jdbc.
1. Nella colonna Esportato da, controlla se il pacchetto viene esportato da un bundle. Procedi se il pacchetto non viene esportato da alcun bundle.
1. Passa a http://[server]:[porta]/system/console/bundles e fai clic su **[!UICONTROL Install/Update]**.
1. Clic **[!UICONTROL Choose File]** e seleziona il file mysql-connector-java-5.1.39-bin.jar. Inoltre, seleziona **[!UICONTROL Start Bundle]** e **[!UICONTROL Refresh Packages]** caselle di controllo.
1. Clic **[!UICONTROL Install]** o **[!UICONTROL Update]**. Al termine, riavviare il server.
1. (Solo per Windows) Disattivare il firewall di sistema per il sistema operativo in uso.

### Creare schemi e tabelle nel database {#create-schema-and-tables-in-database}

Per creare schemi e tabelle nel database, effettuare le operazioni riportate di seguito.

1. Creare uno schema nel database utilizzando la seguente istruzione SQL:

   ```sql
   CREATE SCHEMA `formsportal` ;
   ```

   dove **sportivo formale** fa riferimento al nome dello schema.

1. Creare un **dati** nello schema del database utilizzando la seguente istruzione SQL:

   ```sql
    CREATE TABLE `data` (
        `owner` varchar(255) DEFAULT NULL,
        `data` longblob,
        `metadataId` varchar(45) DEFAULT NULL,
        `id` varchar(45) NOT NULL,
        PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Creare un **metadati** nello schema del database utilizzando la seguente istruzione SQL:

   ```sql
   CREATE TABLE `metadata` (
       `formPath` varchar(1000) DEFAULT NULL,
       `formType` varchar(100) DEFAULT NULL,
       `description` text,
       `formName` varchar(255) DEFAULT NULL,
       `owner` varchar(255) DEFAULT NULL,
       `enableAnonymousSave` varchar(45) DEFAULT NULL,
       `renderPath` varchar(1000) DEFAULT NULL,
       `nodeType` varchar(45) DEFAULT NULL,
       `charset` varchar(45) DEFAULT NULL,
       `userdataID` varchar(45) DEFAULT NULL,
       `status` varchar(45) DEFAULT NULL,
       `formmodel` varchar(45) DEFAULT NULL,
       `markedForDeletion` varchar(45) DEFAULT NULL,
       `showDorClass` varchar(255) DEFAULT NULL,
       `sling:resourceType` varchar(1000) DEFAULT NULL,
       `attachmentList` longtext,
       `draftID` varchar(45) DEFAULT NULL,
       `submitID` varchar(45) DEFAULT NULL,
       `id` varchar(60) NOT NULL,
       `profile` varchar(255) DEFAULT NULL,
       `submitUrl` varchar(1000) DEFAULT NULL,
       `xdpRef` varchar(1000) DEFAULT NULL,
       `agreementId` varchar(255) DEFAULT NULL,
       `nextSigners` varchar(255) DEFAULT NULL,
       `eSignStatus` varchar(45) DEFAULT NULL,
       `pendingSignID` varchar(45) DEFAULT NULL,
       `agreementDataId` varchar(255) DEFAULT NULL,
       `enablePortalSubmit` varchar(45) DEFAULT NULL,
       `submitType` varchar(45) DEFAULT NULL,
       `dataType` varchar(45) DEFAULT NULL,
       `jcr:lastModified` varchar(45) DEFAULT NULL,
       PRIMARY KEY (`id`),
       UNIQUE KEY `ID_UNIQUE` (`id`)
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Creare un **metadati aggiuntivi** nello schema del database utilizzando la seguente istruzione SQL:

   ```sql
   CREATE TABLE `additionalmetadatatable` (
       `value` text,
       `key` varchar(255) NOT NULL,
       `id` varchar(60) NOT NULL,
       PRIMARY KEY (`id`,`key`),
       CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Creare un **commenttable** nello schema del database utilizzando la seguente istruzione SQL:

   ```sql
   CREATE TABLE `commenttable` (
       `commentId` varchar(255) DEFAULT NULL,
       `comment` text DEFAULT NULL,
       `ID` varchar(255) DEFAULT NULL,
       `commentowner` varchar(255) DEFAULT NULL,
       `time` varchar(255) DEFAULT NULL);
   ```

### Configurare la connessione tra l’istanza AEM e il database {#configure-connection-between-aem-instance-and-database}

Per creare una connessione tra l&#39;istanza AEM e il database MYSQL, effettuare le seguenti operazioni di configurazione:

1. Vai alla pagina Configurazione della console web AEM all’indirizzo *http://[host]:[porta]/system/console/configMgr*.
1. Fai clic per aprire **[!UICONTROL Forms Portal Draft and Submission Configuration]** in modalità di modifica.
1. Specificare i valori per le proprietà come descritto nella tabella seguente:

   <table> 
    <tbody> 
    <tr> 
    <th><strong>Proprietà</strong></th> 
    <th><strong>Descrizione</strong></th>
    <th><strong>Valore</strong></th> 
    </tr> 
    <tr> 
    <td><p>Servizio dati bozza portale Forms</p></td> 
    <td><p>Identificatore per bozza di servizio dati</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Servizio metadati bozza portale Forms</p></td> 
    <td><p>Identificatore per bozza servizio metadati</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Servizio di invio dati per Forms Portal</p></td> 
    <td><p>Identificatore per il servizio dati di invio</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Servizio metadati invio portale Forms</p></td> 
    <td><p>Identificatore per il servizio di invio metadati</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Servizio dati di firma in sospeso di Forms Portal</p></td> 
    <td><p>Identificatore per il servizio dati di firma in sospeso</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Servizio metadati firma in sospeso di Forms Portal</p></td> 
    <td><p>Identificatore per il servizio metadati di firma in sospeso</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    </tbody> 
    </table>
1. Lascia invariate le altre configurazioni e fai clic su **[!UICONTROL Save]**.
1. Trova e fai clic per aprire **[!UICONTROL Apache Sling Connection Pooled DataSource]** in modalità di modifica nella configurazione della console web. Specificare i valori per le proprietà come descritto nella tabella seguente:

   <table> 
    <tbody> 
    <tr> 
    <th><strong>Proprietà</strong></th> 
    <th><strong>Valore</strong></th> 
    </tr> 
    <tr> 
    <td><p>Nome origine dati</p></td> 
    <td><p>Nome dell'origine dati per filtrare i driver dal pool di origini dati. L’implementazione di esempio utilizza FormsPortal come nome dell’origine dati.</p></td>
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
    <td><p>Un nome utente per autenticare ed eseguire azioni sulle tabelle del database</p></td>
    </tr>
    <tr> 
    <td><p>Password</p></td> 
    <td><p>Password associata al nome utente</p></td>
    </tr>
    <tr> 
    <td><p>Isolamento transazione</p></td> 
    <td><p>READ_COMMIT</p></td>
    </tr>
    <tr> 
    <td><p>Numero massimo connessioni attive</p></td> 
    <td><p>1000</p></td>
    </tr>
    <tr> 
    <td><p>Numero massimo di connessioni inattive</p></td> 
    <td><p>100</p></td>
    </tr>
    <tr> 
    <td><p>Connessioni inattive minime</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>Dimensione iniziale</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>Attesa massima</p></td> 
    <td><p>100000</p></td>
    </tr>
     <tr> 
    <td><p>Test su prestito</p></td> 
    <td><p>Selezionato</p></td>
    </tr>
     <tr> 
    <td><p>Test durante inattività</p></td> 
    <td><p>Selezionato</p></td>
    </tr>
     <tr> 
    <td><p>Query di convalida</p></td> 
    <td><p>I valori di esempio sono SELECT 1(mysql), select 1 from dual(oracle), SELECT 1(MS Sql Server) (validationQuery)</p></td>
    </tr>
     <tr> 
    <td><p>Timeout query di convalida</p></td> 
    <td><p>10000</p></td>
    </tr>
    </tbody> 
    </table>

### Impostare e configurare l’esempio {#set-up-and-configure-sample}

Per installare e configurare l’esempio in tutte le istanze di authoring e pubblicazione, effettua le seguenti operazioni:

1. Scarica quanto segue **aem-fp-db-integration-sample-pkg-6.1.2.zip** nel file system.

[Ottieni file](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Vai al gestore di pacchetti AEM all’indirizzo *http://[host]:[porta]/crx/packmgr/*.
1. Fai clic su **[!UICONTROL Upload Package]**.
1. Sfoglia per selezionare **aem-fp-db-integration-sample-pkg-6.1.2.zip** pacchetto e fai clic su **[!UICONTROL OK]**.
1. Clic **[!UICONTROL Install]** accanto al pacchetto per installarlo.

## Configurare il modulo adattivo convertito per l’integrazione con Forms Portal {#configure-converted-adaptive-form-for-forms-portal-integration}

Per abilitare l’invio di moduli adattivi tramite la pagina Forms Portal, effettua le seguenti operazioni:
1. [Eseguire la conversione](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) per convertire un modulo di origine in un modulo adattivo.
1. Apri il modulo adattivo in modalità di modifica.
1. Tocca Contenitore modulo e seleziona Configura ![Configurare un modulo adattivo](assets/configure-adaptive-form.png).
1. In **[!UICONTROL Submission]** sezione, seleziona **[!UICONTROL Forms Portal Submit Action]** dal **[!UICONTROL Submit Action]** elenco a discesa.
1. Tocca ![Salva criterio modello](assets/edit_template_done.png) per salvare le impostazioni.

## Creare e configurare la pagina di Forms Portal {#create-configure-forms-portal-page}

Per creare una pagina di Forms Portal e configurarla in modo da poter inviare moduli adattivi utilizzando questa pagina, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring dell’AEM e tocca **[!UICONTROL Adobe Experience Manager]** >  **[!UICONTROL Sites]**.
1. Seleziona il percorso in cui desideri salvare la nuova pagina del portale Forms e tocca **[!UICONTROL Create]** > **[!UICONTROL Page]**.
1. Seleziona il modello per la pagina e tocca **[!UICONTROL Next]**, specifica un titolo per la pagina e tocca **[!UICONTROL Create]**.
1. Tocca **[!UICONTROL Edit]** per configurare la pagina.
1. Nell’intestazione della pagina, tocca ![Modifica modello](assets/edit_template_sites.png)  > **[!UICONTROL Edit Template]** per aprire il modello della pagina.
1. Tocca Contenitore di layout e tocca ![Modifica criterio modello](assets/edit_template_policy.png). In **[!UICONTROL Allowed Components]** , abilita **[!UICONTROL Document Services]** e **[!UICONTROL Document Services Predicates]** opzioni e tocca ![Salva criterio modello](assets/edit_template_done.png).
1. Inserisci **[!UICONTROL Search & Lister]** nella pagina. Di conseguenza, tutti i moduli adattivi esistenti disponibili nell’istanza AEM sono elencati nella pagina.
1. Inserisci **[!UICONTROL Drafts & Submissions]** nella pagina. Due schede, **[!UICONTROL Draft Forms]** e **[!UICONTROL Submitted Forms]**, vengono visualizzati nella pagina del portale Forms. Il **[!UICONTROL Draft Forms]** nella scheda viene visualizzato anche il modulo adattivo convertito generato mediante i passaggi indicati in [Configurare il modulo adattivo convertito per l’integrazione con Forms Portal](#configure-converted-adaptive-form-for-forms-portal-integration)

1. Tocca **[!UICONTROL Preview]**, tocca il modulo adattivo convertito, specifica i valori per i campi del modulo adattivo e invialo. I valori specificati per i campi del modulo adattivo vengono inviati al database integrato.
