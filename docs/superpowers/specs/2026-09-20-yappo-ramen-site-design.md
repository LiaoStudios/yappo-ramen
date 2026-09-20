# Yappo Ramen — design del sito

## Obiettivo

Realizzare una landing page responsive in italiano per Yappo — Ramen & Izakaya, prendendo come riferimento la struttura e la qualità esecutiva del sito CHE STILE! senza copiarne l'identità visiva. Il sito deve presentare il ristorante, valorizzare i piatti e portare l'utente alla prenotazione.

## Direzione visiva

L'identità sarà “Giappone contemporaneo”: luminosa, editoriale e accogliente. La palette userà bianco caldo, nero inchiostro, beige sabbia e azzurro polvere. La tipografia unirà un display deciso per i titoli a un sans leggibile per testi e informazioni pratiche. Accenti giapponesi saranno usati con misura, come elementi di orientamento e atmosfera, non come decorazione stereotipata.

Le fotografie presenti in `GoogleBusiness/` saranno selezionate in base a qualità, soggetto e orientamento. Verranno privilegiate immagini autentiche di ramen, piatti, interni e dettagli del locale. La pagina non userà tutte le 114 immagini: una selezione ridotta mantiene ritmo e qualità.

## Architettura della pagina

1. Navigazione fissa con logo tipografico, ancore e pulsante “Prenota”.
2. Hero con immagine protagonista, posizionamento “Tradizione contemporanea”, descrizione breve e due CTA: prenotazione e menu.
3. Fascia informativa con tipologia di cucina, località, fascia di prezzo e orari sintetici.
4. Sezione “La nostra idea di Giappone” con storia e filosofia di Yappo.
5. Sezione “Piatti firma” con una selezione verificata dal menu pubblico: Yappo Ramen, Tantanmen, Chashu Ramen, yakitori e piccoli piatti.
6. Sezione scura dedicata a brodi, tecnica e convivialità izakaya.
7. Galleria fotografica con lightbox accessibile.
8. Sezione informazioni con indirizzo, telefono, orari completi, mappa e collegamenti esterni.
9. CTA finale e footer con Instagram e dati essenziali.

## Contenuti e fonti

I testi descrittivi saranno adattati dalla pagina ufficiale Yappo. Indirizzo, telefono, orari e valutazione saranno verificati tramite la scheda Google fornita dall'utente. Nomi, descrizioni e prezzi dei piatti saranno ricavati dal menu pubblico aggiornato di TheFork. Il sito eviterà dichiarazioni non verificabili.

## Interazioni

La navigazione userà scorrimento fluido e un menu mobile accessibile. Le CTA esterne apriranno prenotazione, menu, telefono, Google Maps e Instagram. La galleria consentirà apertura, avanzamento, chiusura tramite pulsanti, tastiera e clic sullo sfondo. Le animazioni saranno leggere e rispetteranno `prefers-reduced-motion`.

## Implementazione

Il sito sarà statico e autonomo, realizzato in HTML, CSS e JavaScript senza dipendenze di build. Le immagini selezionate saranno copiate in una cartella `assets/` dedicata e ottimizzate per il web. Metadati, dati strutturati Restaurant, testi alternativi, focus visibile e semantica HTML garantiranno SEO e accessibilità di base.

## Verifica

Saranno controllati: validità dei riferimenti alle immagini, presenza dei dati essenziali, navigazione da tastiera, comportamento del menu mobile e lightbox, assenza di errori JavaScript, resa alle larghezze desktop e mobile e caricamento locale della pagina.
