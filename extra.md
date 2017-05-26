# Hulp oefeningen

## 1. Data inlezen/uitlezen in gegevenstructuur.

Lees data.csv in een geheugenstructuur met de naam data.
De eerste kolom is een cijfer (int), tweede kolom is een kleur (string), derde kolom is een cijfer (int), vierde kolom is een tabel van strings (met maximaal de vier windrichtingen in).

In de uiteindelijke structuur moeten volgende oproepen (mits correctie van de syntax) werken en de juiste uitvoer geven:

data[0]{id} = 1
data[5]{id} = 5
data[5]{kleur} = Blauw
data[5]{windrichting}[0] = noord
data[5]{windrichting} = tabel van noord, west, zuid


Vervolgens schrijf je een functie die alle data gestructureerd (zelf te kiezen) wegschrijft naar standaarduitvoer.

Als laatste maak je nu terug de csv structuur van de datastructuur data. 



**Inhoud van data.csv:**

```csv
id;kleur;getal;windrichting
1;Rood;5;oost
2;Blauw;1;west
3;Geel;2;noord
4;Groen;3;west, oost
5;Blauw;9;noord, west, zuid
6;Paars;0;zuid
7;Zwart;5;oost, zuid
8;Wit;8;noord, oost
9;Oranje;7;noord
10;Blauw;9;zuid

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