# Solutions of extra questions

## 0.

## 1.


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
### Versie Niels

```perl


$file = "data.csv";
$out = "outputdata.csv";

open FILE, '<', $file or die "Can't open file $_";
#open OUT, '>', $out or die "Can't open file $_"; 

$del = <FILE>;

while(<FILE>)
{
	($id, $kleur, $getal, $windrichting) = split /;/;
	($noord,$oost,$zuid,$west) = split /,/, $windrichting;
	
	$data[$id] = {
		kleur => $kleur,
		getal => $getal,
		windrichting => [ $noord,$oost,$zuid,$west ]  
	};
}

for (my $id = 0; $id < @data; $id++) {
	print $id . " {\n";
	print "\t" . $data[$id]{kleur} . "\n";
	print "\t" . $data[$id]{getal} . "\n";

	foreach(@{$data[$id]{windrichting}})	{		print "\t\t" . $_ . "\n";	}
}

#for (my $id = 1; $id < @data; $id++) {
#	print OUT $id . ";" . $data[$id]{kleur} . ";" . $data[$id]{getal} . ";"; 
#	print OUT join ",", @{$data[$id]{windrichting}};
#}

```


## 2.



## 3.

### Versie Niels

```perl
@ARGV="output.txt";
$/=undef;

@temp;
%artikel;
@grid;
@data;

$row;
$col;

sub print_data {
	for (my $i = 0; $i < $row; $i++) {
		for (my $j = 0; $j < $col; $j++) {
			
			print $data[$i][$j]{getal};
			print "\n";
			print join "; ", @{$data[$i][$j]{temperatuur}};
			print "\n";
			while(($key,$value)=each%{$data[$i][$j]{prijzen}}){
				print "$key => $value\n" ;
			}
			print "\n\n";

		}
	}
}

$in=<>;

if($in=~/temperatuur\n(([^\n]{2}\n)*)/ms){
	@temp = split "\n", $1; 
}

if($in=~/prijzen\n(([^\n]+\n)*)/ms){
	foreach(split "\n", $1){
		($n,$p) = split "=", $_;
		$artikel{$n}=$p;
	}

}

if($in=~/grid \((\d)x(\d)\)\n(([^\n]+\n)*)/ms){
#if($in=~/grid2 \((\d)x(\d)\)\n(([^\n]+\n)*)/ms){
	$row=$1;
	$col=$2;
	
	$i=0;
	foreach(split "\n", $3){
		@{$grid[$i]} = split ";", $_;
		$i++;
	}

	for (my $i = 0; $i < $row; $i++) {
		for (my $j = 0; $j < $col; $j++) {
			
			$data[$i][$j]={
				getal => $grid[$i][$j],
				temperatuur => \@temp,
				prijzen => \%artikel
			};
		}
	}
}

print "Data voor wijziging\n";
print_data();

$data[0][0]{prijzen}{cola}=200;
$data[0][0]{temperatuur}[0]=35;

print "Data na wijziging\n";
print_data();

##Fout in meetapparatuur
for (my $var = 0; $var < @temp; $var++) {
	$temp[$var]-=1
}

##Black friday
while(($key,$val)=each%artikel){
	$disc = $val-($val/10);
	$artikel{$key}=$disc
;}

##>Verdubbelen
for (my $i = 0; $i < $row; $i++) {
		for (my $j = 0; $j < $col; $j++) {
			
			$data[$i][$j]{getal}*=2;
		}
}


print "Data na fout/black friday/verdubbeling\n";
print_data();
```


## 5.

### Versie Thomas

```perl




$/ = undef;

@OARGV=@ARGV;


$svg = <>;
# Datastructuur: array (aflopen cellen) met daarin een hash ("coordx1 x2 y1 y2", "kleur", "getal") 
@data;

sub print_data {
	
	print "De datastructuur bevat momenteel:\n";

	foreach(@data){

		# OFWEL %{$_}->{"getal"} maar depricated

		print "celnr: ";
		print ${$_}{"celnr"}, " [", ${$_}{"rijnr"}, ",", ${$_}{"kolnr"}, "]", " ; ";
		print "getal: ";
		print ${$_}{"getal"}, " ; ";
		print "kleur: ";
		print ${$_}{"kleur"}, " ; ";
		print "poly: ";
		print ${$_}{ "poly" }, "\n";
		
	}

	print "Einde van de inhoud van de datastructuur!\n";
}


# Aantal rijen en kolommen inlezen nxm

($nrijen, $mkolommen) = ($svg =~ /(\d+) by (\d+) puzzle/ ) ;

# Aantal cellen is gelijk aan n maal m 

$ncellen = $nrijen * $mkolommen;

sub begin_inlezen {
	print "**Inlezen**\n";
	print "Rijen:", $nrijen, "\n";
	print "Kolommen:", $mkolommen, "\n";
	print "Cellen:", $ncellen, "\n";
}



#begin_inlezen();






# Geen idee of we nu best nen for doen van 0 tot ncellen
# Of dat we regexen en alles pushen :/

# even in aparte array inlezen

(@xcoord) = ($svg =~ m|<text x="(\d+)" y="\d+" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">\d+</text>|g); 
(@ycoord) = ($svg =~ m|<text x="\d+" y="(\d+)" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">\d+</text>|g); 
(@getal) = ($svg =~ m|<text x="\d+" y="\d+" text-anchor="middle" style="font-family:Arial Narrow; font-size: xx-small;">(\d+)</text>|g); 


sub arrays_printen {
	print "****Arrays printen:****\n";
	print "x\n";
	print join " ", @xcoord;
	print "\ny\n";
	print join " ", @ycoord;
	print "\ngetal\n";
	print join " ", @getal;
	print "\n";
}




#arrays_printen();





@kleur;

foreach(@getal){
	#print $_, " ";
	if($_ == 1){
		push @kleur, "blue";
	} elsif ($_ == 2){
		push @kleur, "yellow";
	} elsif ($_ == 3){
		push @kleur, "red";
	} elsif ($_ == 4){
		push @kleur, "green";
	} else {
		push @kleur, "other";
	}
}


# data structuur opvullen
# data[i]{"getal"} = getal[i]
# data[i]{"kleur"} = mappen op getal[i]
# data[i]{"x1"}
# data[i]{"x2"}
# data[i]{"y1"}
# data[i]{"y2"}

for ($i = 0; $i < $ncellen; $i++) {
	$data[$i]{"getal"} = $getal[$i];
	$data[$i]{"kleur"} = $kleur[$i];
	$data[$i]{"celnr"} = $i;
	#print int $data[$i]{"celnr"}/$mkolommen, " ";
	#print $data[$i]{"celnr"} % $mkolommen, " ";
	#print "\n";
	$data[$i]{"rijnr"} = int $data[$i]{"celnr"}/$mkolommen;
	$data[$i]{"kolnr"} = int $data[$i]{"celnr"}%$mkolommen;


	$x1=32+$data[$i]{"kolnr"}*16;
	$x2=16+$data[$i]{"kolnr"}*16;
	$x3=16+$data[$i]{"kolnr"}*16;
	$x4=32+$data[$i]{"kolnr"}*16;

	$y1=16+$data[$i]{"rijnr"}*16;
	$y2=16+$data[$i]{"rijnr"}*16;
	$y3=32+$data[$i]{"rijnr"}*16;
	$y4=32+$data[$i]{"rijnr"}*16;
	

	$data[$i]{"poly"} = "$x1,$y1 $x2,$y2 $x3,$y3 $x4,$y4";
}


# Begin van svg tellen is denk ik 16,0 0,0 0,16 16,16
# bij alle eerstes bijtellen voor van kolom 0 naar 1 te gaan
# bij de tweedes (na de kommas) voor via rijen te gaan
# Dus eigenlijk wil ik nog een {"polygon"}= "64,16 48,16 48,32 64,32" formaat is
# "64,16 48,16 48,32 64,32" = "x1,y1 x2,y2 x3,y3 x4,y4"
# dit zijn 8 cijfers die we telkens moeten bepalen afh van rij en kol nr van de cel
# FORMULE voor grid in 1 dimentionale array alles 0 based
# celnr omzetten naar rijnr en kolomnr:
# celnr / nkolommen = rijnr
# celnr % nkolommen = kolomnr 



#print_data();



#print $data[19]{"getal"};
#print $data[19]{"poly"};

$blue; # dit is alles wat in de blue tag moet komen
$red;
$yellow;
$green;


# polygons maken
# elke cel overlopen checken op welk kleur het is en dan polygon toevoegen


for ($i = 0; $i < $ncellen; $i++) {
	
	if($data[$i]{"kleur"} eq "blue"){

		$blue.= "<polygon points=\"$data[$i]{'poly'}\" />\n";

	}elsif($data[$i]{"kleur"} eq "red"){

		$red.= "<polygon points=\"$data[$i]{'poly'}\" />\n";

	}elsif($data[$i]{"kleur"} eq "yellow"){

		$yellow.= "<polygon points=\"$data[$i]{'poly'}\" />\n";

	}elsif($data[$i]{"kleur"} eq "green"){

		$green.= "<polygon points=\"$data[$i]{'poly'}\" />\n";

	}


}

# Terug opnieuw inlezen en polygon tags toevoegen!
$^I=".bak";
@ARGV = @OARGV;

#wegschrijven
$weg = <>;

$weg =~ s/<g fill="blue" stroke="none">/<g fill="blue" stroke="none">\n$blue/;
$weg =~ s/<g fill="red" stroke="none">/<g fill="red" stroke="none">\n$red/;
$weg =~ s/<g fill="yellow" stroke="none">/<g fill="yellow" stroke="none">\n$yellow/;
$weg =~ s/<g fill="green" stroke="none">/<g fill="green" stroke="none">\n$green/;



print $weg;






```
