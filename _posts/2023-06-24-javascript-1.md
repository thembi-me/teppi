---
layout: post
title: Prima lezione di Javascript
subtitle: Iniziamo dalle basi
tags: [javascript]
comments: true
---

Questa è la prima lezione di un fantomatico, incostante, non-strutturato corso
di programmazione. In teoria, un corso serio dovrebbe iniziare con una lista di
"perché", seguita da una lista di "quando", "come", "chi", e robe simili.

Invece salto tutto quanto e arrivo subito al dunque. In più, parto dall'idea
che molti dei concetti base ti siano noti. Ma se dobbiamo ritornarci su,
fammi sapere.

Essendo un corso pratico, noi si partirà da un compito da fare. Creiamo una
pagina HTML che fa da contatore. Il risultato finale sarà una cosa tipo questa:

<iframe src="/assets/html/javascript_01.html"></iframe>

Se vuoi aprire direttamente questa pagina, clicca [qui](/assets/html/javascript_01.html).

## Lo scheletro HTML

Sull'HTML ne sai tanto. Qui si tratta di avere un titolo (H1) e 3 pulsanti, dentro ad un BODY:
```html
<html>
  <body style="text-align: center;">
    <h1>counter</h1>
    <button>Decrease</button>
    <button>Reset</button>
    <button>Increase</button>
  </body>
</html>
```

Come vedi ho messo uno style inline per centrare il tutto, ma non è essenziale.

Il prossimo passaggio è dare un nome agli elementi [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction) che ci interessano. Questi nomi saranno utili a javascript per identificare gli elementi HTML e manipolarli.

Ho chiamato il titolo `title_counter`, e i 3 pulsanti `button_down`, `button_reset` e `button_increase`. Questo si fa assegnando l'attributo `id` agli elementi HTML:

```html
<h1 id="title_counter">counter</h1>
<button id="button_down">Decrease</button>
<button id="button_reset">Reset</button>
<button id="button_up">Increase</button>
```

## Javascript!

Il nostro codice può essere incluso tramite un file separato, oppure inline.
Oggi, facciamo tutto inline, quindi, scrivremo il codice javascript
direttamente nell'HTML. Questa cosa non si fa nei programmi più strutturati per
una serie di ragioni di sicurezza, leggibilità e mantenibilità, ma per ora
queste cose le ignoriamo.

Il codice JS va scritto dentro al tag `<script>`. Tipo cosi':

```html
<script>
/* Qui va il nostro codice */
</script>
```

Questo tag `<script>` lo metteremo _dopo_ il tag di chiusura di `<body>`.
Perché? Principalmente perché in questo modo il codice nostro verrà eseguito
dopo che gli elementi HTML saranno già stati creati dal browser. Ci sono anche
ragioni di performance, ma le possiamo ignorare per una prima lezione.

## document.getElementById

La prima cosa che il nostro codice dovrà fare sarà quella di prelevare gli
elementi che ci interessano della pagina e salvari dentro a delle variabili.
Questa operazione permetterà al nostro codice di sapere dell'esistenza del
titolo e dei pulsanti e di operare qualche logica sopra di loro.

Il metodo che noi useremo per effettuare questa operazione si chiama: `getElementById` dell'oggetto `document`.

Semplificando molto, `document` è un oggetto che permette di manipolare l'HTML della pagina su cui il tuo javascript sta lavorando. Offre quindi tutta una serie di metodi per aggiungere, rimuovere, modificare elementi HTML.

Per oggi noi usiamo solo uno di questi metodi: `getElementById` che, come dice il nome, prende un elemento dato il suo ID.

Il valore di ritorno di questo metodo sarà il nostro elemento HTML così come lo può vedere javascript. Noi lo salveremo in una variabile.

```javascript
let title_counter = document.getElementById("title_counter");
let button_reset = document.getElementById("button_reset");
let button_down = document.getElementById("button_down");
let button_up = document.getElementById("button_up");
```

## Il contatore

Le quattro variabili create sopra le useremo fra poco. Ma prima di questo, serve creare la variabile principale: `count`, con cui faremo tutti i nostri giochi numeri. Una volta creata, scriveremo subito nel titolo il suo valore:

```javascript
let count = 0;
title_counter.innerText = count;
```

La prima riga crea la variabile assegnandole il valore `0`. La seconda riga usa la variabile `title_counter` creata prima (vedi `getElementById`) e usa `innerText` per scrivere un contenuto testuale al suo interno. Il risultato sarà che la nostra pagina HTML mostrerà un grande `0` in centro schermo. Prova!

## I pulsanti

Ora diamo vita ai 3 pulsanti. Partiamo dal più semplice: Increase.

Quando l'utente cliccherà questo pulsante, noi vogliamo che il contatore vada su di un numero intero. La sintassi per farlo è la seguente:

```javascript
button_up.onclick = function() {
  count++;
  title_counter.innerText = count;
}
```

Noi stiamo dicendo che:
- `onclick`, ovvero, quando l'elemento `button_up` viene cliccato, javascript deve eseguire una funzione;
- `function() {`, la nostra funzione inizia qui e verrà eseguita ad ogni click;
- `count++`: aumentiamo il valore del contatore di 1. Questa sintassi è la versione compatta di: `count = count + 1`, o di `count += 1`;
- `title_counter.innerText = count;` questa riga l'abbiamo già vista prima e aggiorna il titolo.

Il secondo pulsante che vedremo è il reset:

```javascript
button_reset.onclick = function() {
  count = 0;
  title_counter.innerText = count;
}
```

Il codice è uguale al blocco di prima, ma al posto che fare `count++` facciamo `count = 0`, quindi riassegnamo il valore `0` a `count`.

Ora la funzione più interessante. Il decremento non deve andare in negativo! Quindi dobbiamo usare un `if`:

```javascript
button_down.onclick = function() {
  if (count > 0) {
    count--;
    title_counter.innerText = count;
  }
}
```

Vediamo assieme questa funzione:

- `button_down.onclick` - sappiamo già cosa fa.
- `if (count > 0) {` mi dice, solo se count è maggiore di `0` allora esegui il blocco successivo.
- il blocco tra le due `{}` è simile all'incremento, ma qui usuamo `count--`, che è la versione compatta di `count = count - 1` o di `count -= 1`.

## Finito!

Il nostro programma è concluso. Il codice è il seguente:

```html
<html>
<body style="text-align: center;">
  <h1 id="title_counter">counter</h1>
  <button id="button_down">Decrease</button>
  <button id="button_reset">Reset</button>
  <button id="button_up">Increase</button>
</body>
<script>
let title_counter = document.getElementById("title_counter");
let button_reset = document.getElementById("button_reset");
let button_down = document.getElementById("button_down");
let button_up = document.getElementById("button_up");

let count = 0;
title_counter.innerText = count;
button_up.onclick = function() {
  count++;
  title_counter.innerText = count;
}

button_down.onclick = function() {
  if (count > 0) {
    count--;
    title_counter.innerText = count;
  }
}

button_reset.onclick = function() {
  count = 0;
  title_counter.innerText = count;
}

</script>
</html>
```

Avremmo potuto farlo più compatto, più elegante, più ottimizzato, ma per oggi, lezione 1, ci piace.

Ma ora...

## Esercizio per la prossima lezione

Per la prossima lezione, partiamo da questo primo esercizio e aggiungiamo un poco di magia.

Esiste una funzione chiamata `setInterval` la cui sintassi è la seguente:

```javascript
let id = setInterval(function() {
  /* Qualcosa qui */
}, 1000);
```

Ecco la spiegazione:
- Questa funzione esegue `function` ogni `1000` millisecondi (1 secondo). Per sempre, ogni secondo.
- Il valore di ritorno, che noi abbiamo salvato dentro ad una variabile chiamata `id`, può essere usato per cancellare l'operazione. Si fa così: `clearInterval(id);`. Questo valore sarà un numero maggiore di 0 che identifica l'operazione.

Tramite queste due funzioni `setInterval` e `clearInterval`, vorrei che cambiassi il nostro programma `counter` nel seguente modo:

- 3 pulsanti: `start`, `stop`, `reset`.
- Pulsante `start`: fai partire il timer.
- Pulsante `stop`: ferma il timer.
- Pulsante `reset`: azzera il contatore senza fermare il timer se attivo.
- Il timer gira ogni secondo e aumenta il contatore di 1.

Praticamente, dovrebbe uscire una cosa tipo questa:

<iframe src="/assets/html/javascript_02.html"></iframe>

Se ci sono dubbi, oppure se sto andando troppo veloce, o troppo lento, sto qui per ricevere consigli!
