---
title: Risoluzione dei problemi - Servizio di conversione automatica dei moduli (AFCS)
description: Problemi comuni di AFCS e relative soluzioni
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
contentOwner: khsingh
exl-id: e8406ed9-37f5-4f26-be97-ad042f9ca57c
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 85%

---

# Risoluzione dei problemi - Servizio di conversione automatica dei moduli (AFCS)

Questo documento illustra le procedure di base per la risoluzione dei problemi causati da errori comuni.

<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. -->

## Errori comuni {#commonerrors}

| Errore | Esempio |
|--- |--- |
| **Messaggio di errore** <br> L’intestazione del token di accesso non è disponibile. <br><br> **Causa** <br> L’amministratore ha creato più configurazioni IMS o la configurazione IMS non è in grado di raggiungere il servizio AFCS su Adobe Cloud. <br><br>**Risoluzione** <br> Se sono presenti più configurazioni, eliminale tutte e [creane una nuova](configure-service.md#obtainpubliccertificates). <br> Se è presente una singola configurazione, utilizza **Verifica integrità** per effettuare un [controllo della connettività](configure-service.md#createintegrationoption). | ![L’intestazione del token di accesso non è disponibile](assets/invalid-ims-configurations.png) |
| **Messaggio di errore** <br> Impossibile connettersi al servizio.  <br><br>**Motivo** <br> Nei servizi cloud AFCS (Automated forms conversion Service) viene menzionato un URL di servizio errato o non è menzionato alcun URL di servizio. <br><br>**Risoluzione** <br> Corretto [URL servizio](configure-service.md#configure-the-cloud-service) nei servizi cloud di Automated forms conversion Service (AFCS). | ![Impossibile connettersi al servizio.](assets/wrong-service-url-configured.png) |
| **Messaggio di errore** <br> Conversione del modulo non riuscita.  <br><br>**Causa** <br> Problemi di connettività di rete nel sistema dell’utente, inattività del servizio a causa di manutenzione programmata o interruzione su Adobe Cloud. <br><br>**Risoluzione** <br> Risolvi i problemi di connettività di rete nel tuo sistema e verifica lo stato del servizio su https://status.adobe.com/ per sapere se è in corso un’interruzione programmata/non programmata. | ![Impossibile connettersi al servizio.](assets/conversion-failure.png) |
| **Messaggio di errore** <br> Il numero di pagine è superiore a 15.  <br><br>**Causa** <br> La lunghezza del modulo di origine supera le 15 pagine.  <br><br>**Risoluzione** <br> Utilizza Adobe Acrobat per dividere i moduli con più di 15 pagine. Assegna a ciascun modulo un numero di pagine inferiore a 15. | ![Impossibile connettersi al servizio.](assets/number-of-pages.png) |
| **Messaggio di errore** <br> Il numero di file è superiore a 15.  <br><br>**Causa** <br>   La cartella contiene più di 15 moduli. <br><br>**Risoluzione** <br> Assegna a ciascuna cartella un numero di moduli inferiore o uguale a 15. Il numero totale di pagine contenute in ciascuna cartella deve essere inferiore a 50. Le dimensioni della cartella devono essere inferiori a 10 MB. Non salvare i moduli in sottocartelle. Organizza i moduli di origine in un batch di 8-15 moduli. | ![Impossibile connettersi al servizio.](assets/number-of-pages.png) |
| **Messaggio di errore** <br> Il formato del file di origine non è supportato.  <br><br>**Causa** <br> La cartella dei moduli di origine contiene alcuni file non supportati. <br><br>**Risoluzione** <br> Il servizio supporta solo file .xdp e .pdf. Rimuovi i file con qualsiasi altra estensione dalla cartella ed esegui la conversione. | ![Impossibile connettersi al servizio.](assets/unsupported-file-formats.png) |
| **Messaggio di errore** <br>I moduli digitalizzati non sono supportati.  <br><br>**Causa** <br> Il modulo PDF contiene solo immagini digitalizzate del modulo e non contiene alcuna struttura di contenuto. <br><br>**Risoluzione** <br> Il servizio non supporta la conversione di moduli digitalizzati o di immagini di moduli in moduli adattivi pronti all’uso. Tuttavia è possibile utilizzare Adobe Acrobat per convertire l’immagine del modulo in un modulo PDF, quindi utilizzare il servizio per convertire il modulo PDF in un modulo adattivo. Utilizza sempre un’immagine di alta qualità del modulo in Acrobat per migliorare la qualità della conversione. | ![Impossibile connettersi al servizio.](assets/scanned-forms-error.png) |
| **Messaggio di errore** <br> Moduli PDF crittografati non supportati.  <br><br>**Causa** <br> La cartella contiene moduli PDF crittografati. <br><br>**Risoluzione** <br> Il servizio non supporta la conversione di moduli PDF crittografati in moduli adattivi. Rimuovi la crittografia, carica il modulo non crittografato ed esegui la conversione. | ![Impossibile connettersi al servizio.](assets/secured-pdf-form.png) |
| **Messaggio di errore** <br> Impossibile analizzare lo schema JSON del metamodello.  <br><br>**Causa** <br> Lo schema JSON fornito al servizio non è formattato correttamente, contiene caratteri non validi o utilizza una sintassi non valida per la mappatura dei componenti.  <br><br>**Risoluzione** <br> Verifica la formattazione del file JSON. È possibile utilizzare qualsiasi convalida JSON online per verificare la formattazione e la struttura dello schema. Consulta l’articolo [Estensione del metamodello predefinito](extending-the-default-meta-model.md) per informazioni sulla sintassi del metamodello. | ![Impossibile connettersi al servizio.](assets/invalid-meta-model-schema.png) |
| **Errore (solo ambienti locali)** <br> Il **[!UICONTROL Source Language]** non elenca la lingua corretta di un modulo adattivo. <br><br>**Motivo** <br> La proprietà jcr:language del modulo adattivo non è impostata correttamente.  <br><br>**Risoluzione** <br> Apri CRX-DE lite e passa a `/content/forms/af/`, apri `jcr:content` e impostare il valore del nodo sulla lingua corretta. Per un elenco delle lingue supportate, consulta [Aggiunta del supporto per la localizzazione per le lingue non supportate](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/supporting-new-language-localization.html#add-localization-support-for-non-supported-locales). | ![Impossibile connettersi al servizio.](assets/aem-forms-translation-project-language-unavailable.png) |

<!--

<table>
<thead>
<tr>
<th>Error</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Error Message</strong> <p> The access token header is not available. </p><br><strong>Reason</strong> <br> An administrator has created multiple IMS configurations or IMS configuration is not able to reach AFCS service on Adobe Cloud. <br><br><strong>Resolution</strong> <br> If there are multiple configurations, delete all the configurations and <a href="configure-service.md#obtainpubliccertificates">create a new configuration</a>. <br> If there is a single configuration, use <strong> Health Check </strong> to <a href="configure-service.md#createintegrationoption">check connectivity</a>.</td>
<td><img alt="The access token header is not available" src="assets/invalid-ims-configuration.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Unable to connect to the service.  <br><br><strong>Reason</strong> <br> Incorrect service URL or no service URL is mentioned in Automated Forms Conversion Service (AFCS) cloud services. <br><br><strong>Resolution</strong> <br> Correct <a href="configure-service.md#configure-the-cloud-service">Service URL</a> in Automated Forms Conversion Service (AFCS) Cloud services.</td>
<td><img alt="Unable to connect to the service." src="assets/wrong-endpoint-configured.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The service failed to convert the form.  <br><br><strong>Reason</strong> <br> Network connectivity issues at your end, the service is down due to scheduled maintenance, or outage on Adobe Cloud. <br><br><strong>Resolution</strong> <br> Resolve network connectivity issues at your end and check the status of the service on <a href="https://status.adobe.com/">https://status.adobe.com/</a> for a planned or unplanned outage.</td>
<td><img alt="The service failed to convert the form." src="assets/service-failure.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The number of pages is more than 15.  <br><br><strong>Reason</strong> <br> The source form is more than 15 pages long.  <br><br><strong>Resolution</strong> <br> Use Adobe Acrobat to split forms with more than 15 pages. Bring the number of pages in a form to less than 15.</td>
<td><img alt="The number of pages is more than 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The number of files is more than 15.  <br><br><strong>Reason</strong> <br>  The folder contains more than 15 forms. <br><br><strong>Resolution</strong> <br> Bring the number of forms in a folder to less than or equal to 15. Bring the total number of pages in a folder less than 50. Bring the size of the folder to less than 10 MB. Do not keep forms in a sub-folder. Organize source forms into a batch of 8-15 forms.</td>
<td><img alt="The number of files is more than 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The source file format is not supported.  <br><br><strong>Reason</strong> <br> The folder containing source forms have some unsupported files. <br><br><strong>Resolution</strong> <br> The service supports only .xdp and .pdf files. Remove files with any other extension from the folder and run the conversion.</td>
<td><img alt="The source file format is not supported." src="assets/unsupported-file-formats.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Scanned forms are not supported.  <br><br><strong>Reason</strong> <br> The PDF form contains only scanned images of the form and contains no content structure. <br><br><strong>Resolution</strong> <br> The service does not support converting scanned forms or an image of a form to an adaptive out-of-the-box. However, you use Adobe Acrobat to convert the image of a form to a PDF Form. Then, use the service to convert the PDF Form to an adaptive form. Always use a high-quality image of the form for conversion in Acrobat. It improves the quality of the conversion.</td>
<td><img alt="Scanned forms are not supported." src="assets/scanned-forms-error.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Encrypted PDF form is not supported.  <br><br><strong>Reason</strong> <br> The folder contains encrypted PDF forms. <br><br><strong>Resolution</strong> <br> The service does not support converting an encrypted PDF form to an adaptive form. Remove the encryption, upload the non-encrypted form, and run the conversion.</td>
<td><img alt="Encrypted PDF form is not supported." src="assets/secured-pdf-form.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Unable to parse meta-model JSON schema.  <br><br><strong>Reason</strong> <br> The JSON schema supplied to the service is not properly formatted, contains invalid characters, or uses invalid syntax to map components.  <br><br><strong>Resolution</strong> <br> Check the formatting of the JSON file. You can use any online JSON validator to check the formatting and structure of the schema. See, <a href="extending-the-default-meta-model.md">Extend the default meta-model</a> article for information on meta-model syntax.</td>
<td><img alt="Unable to parse meta-model JSON schema" src="assets/invalid-meta-model-schema.png" /></td>
</tr>
</tbody>
</table>
-->
