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

### Versie Sander

```perl
@ARGV = "data.csv";

$header = <>;         #eerste lijn niet gebruiken
while(<>){             #lijn per lijn want csv

    ($id, $kleur, $getal, $windrichting) = split /;/; 
    ($noord, $oost, $zuid, $west) = split /,/, $windrichting; 

    # Data is een array (index = id) (want id in csv wss uniek) van hashes (hash bevat kleur=value,getal=value,windrichting=array)
    $data[$id] = {
        "kleur" => $kleur,
        "getal" => $getal,
        "windrichting" => [ $noord, $oost, $zuid, $west ]
    };
}

for (my $i = 0; $i < $#data; $i++) {
    print "$i\t";
    print $data[$i]->{"kleur"}, "\t";
    print $data[$i]->{"getal"}, "\t";
    @ingevuldeWindrichtingen = grep { $_ ne '' } @{ $data[$i]->{"windrichting"} };        #haal lege velden uit array
    print join " ", @ingevuldeWindrichtingen;
    print "\n";
}

```


### Versie Thomas

```perl
print "---Begin of script---\n";


print "*Reading in csv-file*\n";

@AoH; # Array of Hashes
@arr;

while($line = <>){
	next if $. < 2; # skip the first line = the headerline of the csv
	
	($id, $kleur, $getal, $fullstringwindrichting) = split /;/, $line;
	

	print "**Filling in datastructure**\n";

	# Data is an array of hashes (id, kleur, getal, windrichting) and it's last hash is a hash of an array

	$h = {}; # small hash

	# $h->{key} = value;

	$h->{"id"} = $id;
	$h->{"kleur"} = $kleur;
	$h->{"getal"} = $getal;

	#$h->{"windrichting"} = $windrichting; # but windrichting is here still a string so not good

	# so this should be an hash of an array

	($noord, $oost, $zuid, $west) = split /,/, $fullstringwindrichting;

	$arr[0]=$noord;
	$arr[1]=$oost;
	$arr[2]=$zuid;
	$arr[3]=$west;

	$h->{"windrichting"} = [@arr];

	# OF (en miss wel iets makkelijker)

	#$h->{"windrichting"} = [ $noord, $oost, $zuid, $west ];
	
	push @AoH, $h;

}

print "*Temp testing*\n";

print $AoH[2]{"id"}, "\n"; 				
print $AoH[5]{"id"}, "\n"; 				
print $AoH[5]{"kleur"}, "\n"; 			
print $AoH[5]{"getal"}, "\n";			

print $AoH[2]{"windrichting"}[0], "\n";	

print $AoH[5]{"windrichting"}, "\n"; # geeft array ok

print "*End Temp testing*\n";

print "\n*** Printing datastructure ***\n";

for (0..$#AoH){
	print $AoH[$_]{"id"}, "\t\t";
	print $AoH[$_]{"kleur"}, "\t\t";
	print $AoH[$_]{"getal"}, "\t\t";
	print $AoH[$_]{"windrichting"}[0], ",",
			$AoH[$_]{"windrichting"}[1], ",",
			$AoH[$_]{"windrichting"}[2], ",",
			$AoH[$_]{"windrichting"}[3], "\n";
}



print "\n*** End Printing datastructure ***\n";


print "\n---End of script---";

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

a.) Lees de data uit de file in een geheugenstructuur. (Onderaan staan twee mogelijkheden)
b.) Je mag hier de operatoren statisch gebruiken (dit wil zeggen je hoeft deze niet in te lezen en te verwerken), en er van uitgaan dat ze niet veranderen. Zeer concreet: je zal ergens een stukje code hebben waarin je de conditites gaat testen op een set variabelen. Die testen mag je statisch (hardcoderen).
c.) Ga er ook maar van uit dat de grootte van de grid niet zal wijzigen (dus altijd 9 getallen die we zoeken).
d.) Maak een print procedure/functie die de datastructuur zijn data print.
e.) Na het inlezen van de data stel je al de waarden van de te zoeken getallen op 1.
f.) Je controleert of alle voorwaarden (dit zijn er 6) voldaan zijn. Zo nee ga naar g.) zoja ga naar i.)
g.) Tel bij 1 element 1 op (kies hiervoor bij het element rechts onderaan, het element met de hoogste index). Dit omdat de oplossing van deze puzzel express zo gekozen is om sneller aan een oplossing te komen. Print ook opnieuw de data (dus bij elke iteratie print je, hou ook een tellertje bij die het aantal iteraties telt).
h.) Ga terug naar f.)
i.) Alle voorwaarden kloppen, de buzzel is dus opgelost. Print nog eenmaal de data met als melding dit is de oplossing van de puzzel.
j.) Zorg er nu voor dat de waarden correct in het brainie.txt bestand geplaatst worden. Dit wil zeggen dat de 0n aangepast worden met de correcte waarden maar dat alle andere zaken gelijk blijven. Zorg ervoor dat het oorspronkelijke brainie.txt-bestand ook bewaard wordt (onder een andere naam zoals .bak) en dat de nieuwe brainie.txt de opgeloste versie krijgt.






**Spiekbriefje**

>! Mogelijkheid 1: maak een 2D-array (hier drie op drie) die enkel de te zoeken waarden kent, Mogelijkheid 2: maak een 1D array die 9 elementen bevat (de te zoeken getallen).







