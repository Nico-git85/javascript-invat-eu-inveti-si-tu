# Typed arrays

Sunt un tip special de array-uri menite să lucreze doar cu array-uri numerice. Pentru a folosi aceste array-uri ai nevoie de un *array buffer* pentru a stoca datele. Un *array buffer* este o alocare de memorie în care se pot introduce un anumit număr de bytes.

Își are originile în necesitatea de a avea o structură de date care să poată fi computată rapid. A venit ca o solicitare a WebGL, o adaptare pentru reprezentări 3D într-un element `canvas`.

A fost gândit ca o depășire a limitărilor pe care le impune reprezentarea numerelor pe 64 de biți în JavaScript. Pentru calculele rapide de care are nevoie mediul 3D, era nevoie de o înbunătățire a calculelor algebrice și cea mai rapidă este cea pe biți direct: *bitwise*. Conceptul este simplu: un număr poate fi reprezentat ca un array de biți cu posibilitatea de a folosi metodele aferente oricărui array.

Typed arrays permit stocarea și manipularea mai multor tipuri numerice:

- număr întreg pe 8 biți cu semn (**int8**),
- număr întreg pe 8 biți fără semn (**uint8**),
- număr pe 16 biți cu semn (**int16**),
- număr pe 16 biți fără semn (**uint16**),
- număr pe 32 de biți cu semn (**int32**),
- număr pe 32 de biți fără semn (**uint32**),
- număr cu virgulă mobilă pe 32 de biți (**float32**),
- număr cu virgulă mobilă pe 64 de biți (**float64**)

Logica este următoarea. Știm că orice număr în JavaScript are o reprezentare pe 64 de biți. În cazul în care avem un număr de doar 8 biți, restul de 56 ar sta inocupați și astfel, o mare risipă.
Typed arrays sunt instrumentul care adresează această problemă.

Pentru a crea un *array buffer* se va folosi constructorul `ArrayBuffer`.

```javascript
var tampon = new ArrayBuffer(4);
// alocă-mi un spațiu de 4 bytes în memorie
```

Un lucru care trebuie ținut mereu minte este acela că un array buffer va fi exact de dimeniunea specificată în bytes inițial. Nu poate fi extins.

Pentru a verifica câți bytes sunt în alocarea de memorie constituită cu `ArrayBuffer`, se va folosi proprietatea `byteLength`.

```javascript
console.log(tampon.byteLength); // 4
```

## Folosirea lui `slice()`

Metoda funcționează exact la fel ca și în cazul array-urilor clasice.

```javascript
var tampon2 = tampon.slice(2, 3);
console.log(tampon2.byteLength); // 1
```

## Manipularea datelor din `ArrayBuffer`

Singura metodă de a lucra cu datele din zonele tampon create în memorie este de a crea așa-numitele „views” (perspective).