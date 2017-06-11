# Hulp oefeningen

## 1. Data inlezen/uitlezen in gegevenstructuur.

Lees data.csv in een geheugenstructuur met de naam data.
De eerste kolom is een cijfer (int), tweede kolom is een kleur (string), derde kolom is een cijfer (int), vierde kolom is een tabel van strings (met maximaal de vier windrichtingen in).

In de uiteindelijke structuur moeten volgende oproepen (mits correctie van de syntax) werken en de juiste uitvoer geven:

- data[0]{id} = 1
- data[5]{id} = 5
- data[5]{kleur} = Blauw
- data[5]{windrichting}[0] = noord
- data[5]{windrichting} = tabel van noord, west, zuid


Vervolgens schrijf je een functie die alle data gestructureerd (zelf te kiezen) wegschrijft naar standaarduitvoer.

Als laatste maak je nu terug de csv structuur van de datastructuur data. 



**Inhoud van data.csv:**

```csv
id;kleur;getal;windrichting
1;Rood;5;,oost,,
2;Blauw;1;,,,west
3;Geel;2;noord,,,
4;Groen;3;,oost,,west
5;Blauw;9;noord,oost,zuid,
6;Paars;0;,,zuid,
7;Zwart;5;,oost,zuid,
8;Wit;8;noord,oost,,
9;Oranje;7;noord,,,
10;Blauw;9;,,zuid,


```



## 2. Iets tussenpietsen in een file

In deze oefening is het de bedoeling dat je data inleest uit een file iets berekent en vervolgens weer wegschrijft.

De eerste variant is het berekenen van het gemiddelde en de standaarddeviatie van een reeks getallen. Gegeven file stat.md.

Hier is het de bedoeling dat stat.md aangepast zal worden met µ en s ingevuld! Maak dezelfde oefening op stat2.md.

**Inhoud van stat.md:**

```md

# Dieetonderzoek

In dit onderzoek onderzochten we een dieet. De gegevens zijn als volgt:

- n = 10
- d = 11,1;11,7;12,1;8,05;4,70;6,52;9,30;16,1;4,40;3,80
- µ = NULL
- s = NULL

Dit was het onderzoek.

```

**Inhoud van stat2.md:**

```md

# Dieetonderzoek

In dit onderzoek onderzochten we een dieet. De gegevens zijn als volgt:

- n = 10
- µ = NULL
- s = NULL
- d = 11,1;11,7;12,1;8,05;4,70;6,52;9,30;16,1;4,40;3,80

Dit was het onderzoek.

```


## 3. Grid inlezen + referentieleggen

In deze oefening is het de bedoeling om een tabel van temperaturen, een hash van prijzen en een grid in te lezen (een twee dimensionale tabel). Wanneer je ``data[0][0]`` oproept dan spreek je dus eigenlijk de eerste cel aan van de grid. Dit moet vervolgens een hash teruggeven want een cel heeft meerdere eigenschappen:

- een getal (lezen van invoerbestand)
- een boolean waarde (even/oneven) die je dus bepaalt op basis van het getal
- een referentie naar de array temperatuur, hiervan weet je dat elke cel refereert naar eenzelfde array
- een referentie naar de hash prijzen, hiervan weet je dat elke cel refereert naar eenzelfde hash

Na het inlezen van deze informatie print je de waarden van je datastructuur uit (hoe je dit doet, mag je zelf kiezen). Verander vervolgens een waarde in de temperatuur array **en** in de prijzen hash en print vervolgens alles opnieuw uit om te bewijzen dat de referentie zijn werk heeft gedaan. 

Kijk nadien of je datastructuur ook bestand is voor grid2 in te lezen.

De volgende opdracht is het aanpassen van data. We hebben zonet te horen gekregen dat onze meetapparatuur een foute meting heeft gedaan. Daarom moet elke waarde in de tabel temperatuur met 1 graad verminderd worden. 30 wordt 29, 27 wordt 26, enzoverder. Vervolgens is het black friday en krijgen we op alle prijzen 10 procent korting. Pas bijgevolg ook alle prijzen aan in de hash prijzen (let op dat je geen afrondingen of iets dergelijks doet). Als laatste moet je ook alle waarden (getallen) van de grid verdubbel.

Print tot slot alles uit de datastructuur.

**Hints**

```perl
- print_data() # maak een functie om de datastructuur te printen
- data[0][0] # geeft een hash terug
- data[0][0]{"getal"} # geeft het getal terug van de eerste cel (hier 1)
- data[0][0]{"temperatuur"}[] # geeft de temperatuur van de eerste dag terug (hier 30)
- data[0][0]{"prijzen"}{"cola"} # geeft de prijs van cola terug

```

**Inhoud van invoer.txt**
```txt
De inhoud is:

temperatuur
30
27
22
20
10
12
13

prijzen
playstation=300
cola=2
pc scherm=500
chips en nootjes-mix=5

grid (3x3)
1;2;3
4;5;6
7;8;9

grid2 (2x4)
1;2;3;4
5;6;7;8



```


## 4. Brainies (volledige puzzel via bruteforce)

Deze oefening gaat een puzzel inlezen en via bruteforce oplossen. Het gaat om het vinden van 9 getallen zodat aan alle voorwaarden voldaan zijn. Bekijk even brainie.txt. Alle getallen die een 0 hebben moeten worden aangepast door een getal tussen 0 en 10 (=1..9) zodat de condities aan de zijkanten (2, 3, 13) en onderaan (3, 4, 19) voldaan zijn. De N'n zijn nullwaarden en plaatsen die genegeerd mogen worden door de structuur van het vierkant. x slaat op een vermenigvuldiging, : op een deling, + een optelling, - een aftrekking.
Concreet moet op de eerste lijn drie waarden (a, b en c) gevonden worden zodat a*b+c gelijk is aan 2. 

**Inhoud brainie.txt**

```
 _ _ _ _ _
|0|x|0|+|0| 2
|+|N|+|N|+|
|0|:|0|+|0| 3
|+|N|x|N|x|
|0|+|0|+|0| 13
 ¯ ¯ ¯ ¯ ¯
 3   4   19

```

**Werkwijze**

Wanneer je geen inspiratie hebt om dit op te lossen ga als volgt te werk:

**a.)** Lees de data uit de file in een geheugenstructuur. (Onderaan staan twee mogelijkheden)

**b.)** Je mag hier de operatoren statisch gebruiken (dit wil zeggen je hoeft deze niet in te lezen en te verwerken), en er van uitgaan dat ze niet veranderen. Zeer concreet: je zal ergens een stukje code hebben waarin je de conditites gaat testen op een set variabelen. Die testen mag je statisch (hardcoderen).

**c.)** Ga er ook maar van uit dat de grootte van de grid niet zal wijzigen (dus altijd 9 getallen die we zoeken).

**d.)** Maak een print procedure/functie die de datastructuur zijn data print.

**e.)** Na het inlezen van de data stel je al de waarden van de te zoeken getallen op 1.

**f.)** Je controleert of alle voorwaarden (dit zijn er 6) voldaan zijn. Zo nee, ga naar **g.)** zo ja, ga naar **i.)**

**g.)** Tel bij 1 element 1 op (kies hiervoor bij het element rechts onderaan, het element met de hoogste index). Dit omdat de oplossing van deze puzzel express zo gekozen is om sneller aan een oplossing te komen. Print ook opnieuw de data (dus bij elke iteratie print je, hou ook een tellertje bij die het aantal iteraties telt).

**h.)** Ga terug naar **f.)**

**i.)** Alle voorwaarden kloppen, de puzzel is dus opgelost. Print nog eenmaal de data met als melding dit is de oplossing van de puzzel.

**j.)** Zorg er nu voor dat de waarden correct in het brainie.txt bestand geplaatst worden. Dit wil zeggen dat de 0n aangepast worden met 
de correcte waarden maar dat alle andere zaken gelijk blijven. Zorg ervoor dat het oorspronkelijke brainie.txt-bestand ook bewaard wordt (onder een andere naam zoals .bak) en dat de nieuwe brainie.txt de opgeloste versie krijgt.






**Spiekbriefje**

>! Mogelijkheid 1: maak een 2D-array (hier drie op drie) die enkel de te zoeken waarden kent, Mogelijkheid 2: maak een 1D array die 9 elementen bevat (de te zoeken getallen).




## 5. Mappen en met svgs spelen

In deze oefening moet je een svg inlezen. De svg bevat een grid met cijfertjes in. De cijfers gaan van 1 tot 4 en stellen elk een kleur voor:

- 1 is blauw
- 2 is geel
- 3 is rood
- 4 is groen

Lees de data in en zorg ervoor dat elk vakje nu voorzien wordt van de juiste achtergrondkleur.

**Inhoud van svga.svg**

![svg](svgs/svga.svg)

```svg
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg width="192" height="160" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <rect width="192" height="160" fill="white" stroke="none" />
  <title>5 by 5 puzzle</title>
  <g fill="blue" stroke="none">
  </g>
  <g fill="red" stroke="none">
  </g>
  <g fill="yellow" stroke="none">
  </g>
  <g fill="green" stroke="none">
  </g>
<g fill="black" stroke="none" stroke-width="1">
    <text x="24" y="26" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">2</text>
    <text x="40" y="26" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">3</text>
    <text x="56" y="26" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">3</text>
    <text x="72" y="26" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">4</text>
    <text x="88" y="26" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">4</text>
    <text x="24" y="42" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">1</text>
    <text x="40" y="42" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">2</text>
    <text x="56" y="42" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">3</text>
    <text x="72" y="42" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">3</text>
    <text x="88" y="42" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">1</text>
    <text x="24" y="58" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">2</text>
    <text x="40" y="58" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">1</text>
    <text x="56" y="58" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">3</text>
    <text x="72" y="58" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">3</text>
    <text x="88" y="58" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">4</text>
    <text x="24" y="74" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">2</text>
    <text x="40" y="74" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">3</text>
    <text x="56" y="74" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">3</text>
    <text x="72" y="74" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">4</text>
    <text x="88" y="74" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">1</text>
    <text x="24" y="90" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">3</text>
    <text x="40" y="90" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">3</text>
    <text x="56" y="90" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">4</text>
    <text x="72" y="90" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">4</text>
    <text x="88" y="90" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">2</text>
  </g>
</svg>

```


## 6. Iteratie en svg vullen

Gebruik ![svg](svgs/iteratie.svg) en los deze op zodat deze ![svg](svgs/iteratieopl.svg) wordt.
Als kleine bijkomende extra: zorg ervoor dat de cellen waarmee we beginnen (hier op de diagonaal 4,2 en 4) een achtergrond kleur krijgen (zoals in oef 5). **De puzzel werkt als volgt:** Elk vierkantje (2 op 2 matrix) binnen deze 3 op 3 matrix moet de waarden 1,2,3,4 krijgen (zoals bij een sudoku). Hierin mag echter dezelfde waarde meerdere keren per lijn voorkomen. Zie de oplossing.

Om het op te lossen ga je als volgt te werk:

- Lees alle data in en bepaal voor elke cel de mogelijke waarden. In dit geval zijn de mogelijke waarden 1,2,3 of 4. Dit noemen we de init-fase.

- Nu begint de eerste iteratiefase. Je gaat voor elke cel de mogelijke waarden reduceren en dit door te kijken naar de onmiddelijke buren (links, rechts, onder, boven). Bijvoorbeeld in de tweede cel naast de vier (en ook de cel eronder) moet 4 verwijderd worden uit de mogelijke waarden!

- De tweede iteratiefase gaat naar de cellen diagonaal kijken. Zo zal de derde cel 2 uit zijn mogelijke waarden kunnen halen. 

- Zorg ervoor dat je continu itereert over deze twee iteratiefases. Het liefst doe je iteratiefase 1 tot je geen oplossingen meer hebt, dan doe je twee en vanzodra je nieuwe info hebt keer dan terug naar iteratiefase 1. Wijk hier gerust van af als dit programmatisch makkelijker is.



