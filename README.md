Člani ekipe:
Jernej Krum
Marko Žugelj

![alt text](https://github.com/KrumJ12/SoccerHeads/blob/master/Slike/menu.PNG "Menu")

Povezava na igrico:
http://scratch.mit.edu/projects/32428776/

![alt text](https://github.com/KrumJ12/SoccerHeads/blob/master/Slike/igra.PNG "Igra")

Opis igrice: 
Igra Soccer Heads je namenjena dvema igralcema, ki se pomerita med seboj.
Cilj vsakega igralca je, da v časovnem okviru (v minuti in 40 sekund), čimvečkrat
zatresemo nasprotnikov gol. Streljamo lahko z glavo in nogo. 

Levega igralca upravljamo z naslednjimi tipkami:

W   - skok
A   - premik levo
D   - premik desno
F   - udarec z nogo

Desnega igralca pa upravljamo z naslednjimi tipkami:

Puščica gor   -  skok
Puščica levo  -  premik levo
Puščica desno -  premik desno
L             -  udarec z nogo

Seveda so možne tudi kombinacije, npr. med skokom v stran udarimo žogo z nogo.
Levi igralec strelja samo desno, desni igralec pa samo levo.

Da bi bila igra atraktivnejša, sva dodala precej bonusov/dodatkov,
ki popestrijo samo igro. Ti se prikažejo naključno nad igralno površino in 
nam lahko pomagajo ali pa škodujejo pri doseganju končne zmage.
Praviloma so rdeče obarvani v našo škodo, zeleni pa v našo korist.
Dodatki se nas “držijo” dokler ne pade zadetek na kateri strani oz. dokler se
tekma ne zaključi.

Dodatki so naslednji:

- zlom noge (ne moremo več uporabljati tipke za udarec z nogo)
- počasno gibanje (naš igralec se giba počasneje v smeri osi X)
- zamrzni sebe (nekaj sekund se ne moremo gibati, igra pa teče naprej)
- pomanjšaj zogo (žoga je potem manjša in predstavlja večjo nevarnost za naš gol (vendar tudi nasprotnikov))
- skoči manj (naš igralec ne more več skočiti tako visoko)
- povečaj svoj gol (naš gol se poveča in ga je obraniti še težje)

+ hitro gibanje (naš igralec se giba hitreje v smeri osi X)
+ zamrzni nasprotnika (nekaj sekund se nasprotnik ne more gibati, igra pa teče naprej)
+ povečaj žogo (žoga je večja in lažje je obraniti svoj gol (vendar ima tudi nasprotnik lažje delo))
+ skoči več (naš igralec skoči višje kot ponavadi)

V primeru, da je po izteku igralnega časa rezultat izenačen,
gre igra v podaljsek, v katerem zmaga tisti igralec, ki prvi doseže zadetek.

Lahko pa se zgodi, da je igre konec že predčasno, če eden od igralcev prejme rdeči karton.
To se lahko zgodi, če sodnik oceni, da smo naredili pregrob prekršek (če brcamo nasprotnega igralca).


O implementaciji: 

30 sličic:

- žoga
- levi igralec
- desni igralec
- levi gol
- desni gol
- leva gol črta
- desna gol črta
- rumeni karton
- rdeči karton
- slika ob zmagi levega igralca
- slika ob zmagi desnega igralca
- 9 oblakov, ki potujejo v ozadju
- 10 bonusov med igro


ŽOGA:
Začetni položaj žoge je (0,130). Začetna hitrost v smeri x se izbere naključno. Žoga se giblje s simulacijo gravitacije. 
Odbija se od tal, sten, prečke in igralcev. Kadar jo brcne eden od igralcev se hitrost žoge v smeri x in y naključno spremeni. 
Na začetku čas nastavimo na 100. Počakamo eno sekundo, nato pa zmnajšamo čas za 1. Če se žoga dotika desne gol črte, prištejemo gol levemu in obratno.  
Po vsakem golu se žoga postavi v začetni položaj, spremenljivke vezane na bonuse pa se ponastavijo. S tem dosežemo, da je po vsakem zadetku 
stanje na igrišču enako kot na začetku. Ko se čas izteče in imata igralca isto golov, aktiviramo igro zlati gol. Prikažemo obvestilo za zlati gol, 
takoj ko pade gol pa prikažemo zmagovalca.  Vsake 4 sekunde se naključno izbere ali bomo prikazali bonus ali ne. Če da, naključno izberermo 
položaj x in y bonusa in pa kateri bonus bomo izbrali. Odvisno od bonusov pa se velikost žoge lahko poveča ali pomanjša.


LEVI IGRALEC:
Ob začetku igre se prikaže pred levim golom. Če se dotikamo podlage in je hitrost v smeri y majhna, postane 0 (obmiruje v smeri y), drugače 
pa se hitrost množi z -0.2. S tem dosežemo, da se igralec približno naravno odbije od podlage. Če z bonusi dosežemo, da je igralec zazidan, 
potem spremeni videz (postane zazidan), če ni zazidan pa ga lahko premikamo (s pritiski na tipki a in d spremenimo hitrost v smeri x, z w pa hitrost v smeri y). 
Kadar pade gol se igralec postavi na začetni položaj, pred svoj gol. Če ni zazidan in nima zlomljene noge (kar je vedno res, če seveda nismo pobrali dodatka, 
lahko brca. Pri brcu se poleg igralca za pol sekunde pokaže nogometni čevelj. Če smo  zadeli nasprotnika se bo sodnik naključno odločil, kaj bo storil 
(več o tem pri kartonih). V vsakem primeru pa se po brci nasprotnika gibanje tega v smeri x in y smeri upočasni, dokler ne pade zadetek.


DESNI IGRALEC:
Podobno kot levi igralec.

LEVI GOL:
Privzeta velikost je 90% originalne slike. Če zadanemo dodatek za povečanje gola, se gol poveča na 120% originalne slike.


DESNI GOL:
Podobno kot levi gol.


LEVA GOL ČRTA:
Na začetku je skrita. Kadar poženemo igro se prikaže. Če prejemo obvestilo, da je gol povečan, se tudi črta poveča na 
130% prvotne velikosti. Kadar je igre konec jo skrijemo in velikost postavimo nazaj na 100%. Kadar pade gol ponastavimo velikost na 100%.


DESNA GOL ČRTA:
Enako kot leva gol črta, le da je na desni strani.


RUMENI KARTON:
Pokaže se za eno sekundo levemu ali desnemu igralcu, če je le ta brcnil nasprotnika in je sodnik pokazal rumeni karton 
(verjetnost da sodnik pokaže rumeni karton je 1/3).


RDEČI KARTON:

Če igralec zaradi brcanja nasprotnika prejme neposredni rdeči karton (verjetnost da sodnik pokaže rdeči karton je 1/6) 
ali drugi rumeni karton se na njegovi strani pokaže rdeč karton, nato pa se pokaže obvestilo, da je zmagal nasprotnik.


SLIKA OB ZMAGI LEVEGA IGRALCA:

Pokaže se ob zmagi levega igralca, sicer skrita.


SLIKA OB ZMAGI DESNEGA IGRALCA:

Pokaže se, kadar zmaga desni igralec, sicer skrita.


9 OBLAKOV:

Vsem je skupno to, da ghost effect spremenimo za 80. Tako bo izgledalo, da je oblak nekje v ozadju. Ko oblak prispe na drugi konec, se zopet pojavi na začetku. Med seboj se razlikujejo
po tem, kje začnejo gibanje in kako hitro se gibljejo.


10 BONUSOV:

Vsi bonusi so privzeto skriti, pojavljajo pa se naključno nad igralno površino.
Če ga igralec zadane z žogo, mu ta lahko pomaga/škodi na poti do zmage.

	- POVEČAJ GOL

	V primeru, da je bil izbran iz seznama Bonusi, se bonus “Povečaj gol” pokaže za 5 sekund. 
	Če se v tem času dotakne žoge, ustrezen gol (v primeru, da ga je zadel
 	levi igralec, se poveča levi gol) poveča na 120%. V primeru zadetka/konca igre,
	se gol pomanjša na privzeto velikost (90%).

	- POMANJŠAJ ŽOGO

	V primeru, da je bil izbran iz seznama Bonusi, se bonus “Pomanjšaj žogo” pokaže za 5
	sekund. Če se v tem času dotakne žoge, se bo, neodvisno od tega, kateri igralec je žogo
	zadnji brcnil, spremenila na velikost 50 (50% velikosti slike). Obenem se bo sprožil
	dogodek pomanjsajZogo, ki bo javil spremembo “sliki” žoga.	

	- POVEČAJ ŽOGO

	Podobno kot v prejšnjem primeru, le da se žoga tokrat poveča na 100%. Privzeto je žoga
	velikosti 70%.

	- POČASNO GIBANJE

	V primeru, da je bil izbran ta bonus, se prikaže za 5 sekund. Če se v tem času dotakne
	žoge, se bo tistemu igralcu, ki je nazadnje brcnil žogo, faktor gibanja v smeri osi x,
	ki je sicer privzeto 1, nastavil na 0,3.

	- HITRO GIBANJE

	V primeru, da je bil izbran, se prikaže za 5 sekund. Če se v tem času dotakne žoge,
	se bo tistemu igralcu, ki je nazadnje brcnil žogo, faktor gibanja v smeri osi x,
	nastavil na 3.

	- ZAZIDAJ NASPROTNIKA

	V primeru, da zadenemo ta bonus, se spremenljivka DesniZazidan oz. LeviZazidan nastavi na
	1, odvisno od tega, kdo se je žoge zadnji dotaknil. Dogodek odvisen od spremenljivke
	LeviZazidan/DesniZazidan se izvede v okviru “sličice” Žoga.

	- ZAZIDAJ SEBE

	Podobno kot zgoraj, le da se tokrat, če je žogo brcnil levi igralec, nastavi LeviZazidan 
	nastavi na 1. V tem primeru zazidamo sebe.	

	- SKOČI VISOKO

	V primeru, da je bil izbran bonus “visoko”, se ta prikaže za 5 sekund. Če se v tem času
	dotakne žoge, se bo tistemu igralcu, ki je nazadnje brcnil žogo, faktor gibanja v smeri
	osi y, nastavil na 2. Faktor se na začetku oziroma ob zadetku nastavi na 1.

	- SKOČI NIŽJE

	Podobno, kot zgoraj, le da se faktor nastavi na 0,1 .

	- ZLOM NOGE

	V primeru, da je izbran ta bonus, se prikaže za 5 sekund. Če se v tem času dotakne
	žoge, se bo tistemu igralcu, ki je nazadnje brcnil žogo, spremenljivka zlomLevi/zlomDesni,
	nastavila na 1, odvisno, za katerega igralca gre. Igralec do naslednjega zadetka ne bo 
	mogel streljati.


Možne izboljšave: 

- fizika žoge in odboja od igralcev/okolja
- možnost izbire menija v več jezikih
- enoigralski način (igramo proti računalniku)
- novi dodatki
