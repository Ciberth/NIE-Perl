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


## 4.

### Versie Niels

```
```
