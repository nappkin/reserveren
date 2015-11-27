# Nappkin reserveringen
Je kunt op verschillende manieren op je eigen website reserveringen aanmaken voor Nappkin. 

Als je WordPress gebruikt kun je de Nappkin reserveer plugin installeren. Dat is de makkelijkste manier.

Een eenvoudig alternatief is om de standaardimplementatie over te nemen op je website en die naar je eigen wensen aan te passen voor wat betreft kleur, lettertype etc.  

Als je je website in eigen beheer hebt en volledige controle wilt over het uiterlijk van de reserveerpagina of -sectie dan kan je als basis het script `js/nappkin_api.js` gebruiken. 

# WordPress

Installatie instructie:
- installeer de plugin `amr shortcode any widget`
Met deze plugin kun je widgets opnemen in een willekeurige pagina
- maak een zip van WordPress/
- kies in WordPress: `Add new plugin`
- upload de eerder gemaakte zip
- ga naar `Appearance widgets`
- sleep de Nappkin plugin naar het panel `Widgets for Shortcodes`
- vul het id in dat je van Nappkin hebt ontvangen
- maak een nieuwe pagina aan en neem daarin de code `[do_widget nappkin]` op

# Standaard

index.html is een referentie implementatie die gebruik maakt van `js/nappkin_api.js`.
Je kunt dit bestand en de inhoud van `js/` en `css/` overnemen op je website.


# Api 
Het script `js/nappkin_api.js` bevat de basiscode die nodig is voor de communicatie met de Nappkin server. Om de code te gebruiken instantieer je het Nappkin object als volgt:
```javascript
var locationId = 2; //  demo locatie - vraag de juiste code op bij Nappkin
var nappkin = new Nappkin(locationId);
```

Het object `Nappkin` bevat twee functies:

```javascript
// Opvragen beschikbaarheid per dag en per tijdslot over de maand van de  opgegeven datum
getAvailablityForMonth(date, success, failure);

//  Aanmaken nieuwe reservering
createNewReservation(reservation, success, failure)
```

### getAvailablityForMonth()

Retourneert een object met daarin per datum en per section (lunch of diner) de beschikbaarheid per tijdslot.
Het veld `available` bevat het aantal beschikbare plaatsen in het betreffende tijdslot.

```
{"result":
    {"dates":
        [
            {
            "date":"2015-11-01",
            "sections":
                [
                    {
                    "start":"12:00",
                    "name":"Lunch",
                    "countGuests":0,
                    "slots":
                        [
                            {
                            "start":"12:00",
                            "available":50
                            },
                            {
                            "start":"12:30",
                            "available":50
                            }
                         ]
                    },
                    {
                    "start":"18:00",
                    "name":"Dinner",
                    "countGuests":0,
                    "slots":
                        [
                            {
                            "start":"18:00",
                            "available":50
                            }
                        ]
                    }
                ]
            }
        ],
        "maxGroupSize":6
    }
}
```

### createNewReservation()

createNewReservation(reservation, success, failure)

```
reservation = {
    date: new Date(),
    pax: 2,
    name: "Jansen',
    email: "email@domain.com",
    phone: "06221123",
    notes: "Graag bij het raam",
    langauge: "nl"
}
```

# Support
Voor vragen en opmerkingen kan je contact opnemen met de servicedesk via `support@nappkin.nl`