# Kleine Oefeningen & Snippets

## Niet unieke regex capturen (door middel van verwijdering)

### Gegeven

Lees alle x1, y1, x2 en y2 waarden correct in van de (eerste of) tweede g tag.

```xml
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg width="192" height="160" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <rect width="192" height="160" fill="white" stroke="none" />
  <title>Sudoku</title>
  <g fill="none" stroke="#000000" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
    <line x1="16" y1="16" x2="160" y2="16" />
    <line x1="16" y1="64" x2="160" y2="64" />
    <line x1="16" y1="112" x2="160" y2="112" />
    <line x1="16" y1="16" x2="16" y2="160" />
    <line x1="64" y1="16" x2="64" y2="160" />
    <line x1="112" y1="16" x2="112" y2="160" />
    <line x1="160" y1="16" x2="160" y2="160" />
    <line x1="16" y1="160" x2="160" y2="160" />
  </g>
  <g fill="none" stroke="#000000" stroke-width="1" stroke-linecap="round" stroke-linejoin="round">
    <line x1="16" y1="32" x2="160" y2="32" />
    <line x1="16" y1="48" x2="160" y2="48" />
    <line x1="16" y1="80" x2="160" y2="80" />
    <line x1="16" y1="96" x2="160" y2="96" />
    <line x1="16" y1="128" x2="160" y2="128" />
    <line x1="16" y1="144" x2="160" y2="144" />
    <line x1="32" y1="16" x2="32" y2="160" />
    <line x1="48" y1="16" x2="48" y2="160" />
    <line x1="80" y1="16" x2="80" y2="160" />
    <line x1="96" y1="16" x2="96" y2="160" />
    <line x1="128" y1="16" x2="128" y2="160" />
    <line x1="144" y1="16" x2="144" y2="160" />
  </g>
</svg>
```

### Oplossing

```perl
# Todo
```

## Geneste structuren opvullen en printen.

### Gegeven

Schrijf code die volgende datastructuren opvult en print. Maak ook een versie via functies:

- Vul Op/Print HoH
- Vul Op/Print HoA
- Vul Op/Print AoH
- Vul Op/Print AoA

### Oplossing

```perl
# Todo
```



## Hoe maak je een copy van een bestaande structuur in een andere (zodat ze genest en gelijk zijn)

### Gegeven

```perl

%diep = (
	"een" => 1,
	"twee"=> 2
);

# dit is dus een HoH
%data = (
	
	"a" => copy van diep
	"b" => copy van diep
)

# Hoe doe je hetzelfde met de andere datastructuren
```


## Mapfunctie

### Gegeven

Schrijf een functie die twee parameters verwacht. Als eerste een string/getal van twee cijfers die rij/kolom voorstellen (bvb 00: rij 0, kolom 0), en als tweede een getal (bvb 4).

Je roept de functie dus bvb op als volgt: functie('00', 4).

De functie moet vervolgens een mapping maken van een correcte svg tag (x en y berekenen) op basis van de parameters.