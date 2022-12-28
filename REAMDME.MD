# Pasi in realizarea unui proiect de front end de la 0

## Pasul 1: Design System

-->DESIGN SISTEM
->noroc ca ne este oferit deja de frontendmentor (fonturi, culori, marimi ssmd)
Moduri de implementare: - custom properties - utility classes will allow us to save time in the long run
Max exact, trebuie sa: - to create a general reset ('cause css comes with some things that can be annoying) - then start with some more generic utility classes(pe care le poti crea in fiecare proiect) - create the design system itself

### What is a reset?

    -> it helps us to start on a good base before we dive into anything
    -> What could you reset: poti vedem pe site-ul css reset din chrome

### Utility classes

    -> do one thing, and do it very well
    -> often only have one declaration, but they can have multiple when required
    -> allow things to be much more modular, and allow us to write a lot less in the long run

#### OBS: 1)intotdeauna, pune o imagine intr-un div !! fiindc o imagine se comporta ciudat

          2) NU MAI FOLOSI SASS, fa exact ca in curs si viata o sa iti fie mai usoara
    	  3) Poti defini variabile globale in css in :root{--gap: 0.5rem} sau le poti reinitializa LOCAL in interiorul unei clase: .box { --gap: 2rem}

### Colors

    -> use rgb or hsl, cause you have a alpha value (for opacity)
    -> custom properties (variabilele din root) / :root{} will allways be on the top of the file
    -> cand declari variabile, ajuta daca le pui PREFIX
    	-> ex: --clr-dark: 230 35% 7%; // fara hsl
    -> ex de clase utility pentru culori: --bg-dark: var(--clr-dark); -text-light: var(--clr-light)
    -> set the color of all the text in body: <body class="white-text">

    OBS: primesti de ex. 3 culori, aceste culori vor fi atat de background cat si pentru text,
    	deci trebuie facute 6 clase utilitare pentru fiecare intrebuintare

### Typography

    -> in root mai trebuie sa iti definesti cate o variabila pentru fiecare font size si pentru fiecare font family !!!!!!!!!:
    	>> font-size(ex: --fs-200: 0.85rem) [the bolder you get, the bigger the number(size) is]
    	/* font-sizes */
    		--fs-900: 9.375rem;
    		--fs-800: 6.25rem;
    		--fs-700: 3.5rem;
    		--fs-600: 2rem;
    		--fs-500: 1.75rem;
    		--fs-400: 1.125rem;
    		--fs-300: 1rem;
    		--fs-200: 0.875rem;
    	>> font-family (ex: --ff-roboto: "roboto", sans-serif)
	-> pentru intreg body-ul paginii, font family-ul NU E SPECIFICAT
	dar la sectiunea Body Text il poti selecta si vedea exact care este

OBS:
	1) letter spacing could be declare as a utility class, cause it's not used as mush as the ff or fs 
	2) Cand folosesti culori punele intr-un HSL(var(--clr-dark))
	3) You can edit a thing once, and then all it will change, that's why you should love to use
	utility classes and custom properties --> it's easier to make big changes

	4) Uneori NU e nevoie sa creezi o clasa pt un element, poti faci in schimb:
	.numbered-title span {
		// properties
	}

	5) Alpha value has values: [0,1]

	6) How to add space between elements: .parent > * // * measns every direct child of parent{padding-top; 1rem}
	7) .parent > * + * {} // selects all the elements that have a neighbor before themselves.(select all the children of parent without first one...) or you can write
		-> .parent > *:not(:first-child) {}


### Interaction Elements
	-> COMPONENTS: are things that are a little bit bigger, they have more pieces going on, there are multiple things inside of them

OBS: How to center an element inside of parent:
	.parent {
		padding: 0 2rem; // add some space
		display: grid;   // allow us to use some modern css
		aspect-ratio: 1; // it makes a perfect square=> 
							width == height of the element
		place-items: center; // center the text on vertical and horizontal like a justify content and aling items ;))))))) with just a line of code
	}

	-> am invatat cum sa fac o animatie pe acel buton (larbe button) doar folosind proprietatea de tranzitie

OBS: How to edid multiple lines in VS CODE: hold ALT and press left click on the line you want to edit

	-> Cum sa faci o linie dedesubtul unui element din navbar?
		-> folosing border-bottom / pseudo-elements

-> EX:
.underline-indicators li {
  padding: 1.5rem 0;
  border-bottom: 2px solid hsl(var(--clr-white) / 0); // 0 ca sa nu se vada borderul de jos
  transition: border-color 0.3s ease-in-out;
}

.underline-indicators li:hover {
  border-color: hsl(var(--clr-white) / 0.5); // 0.5 ca sa se vada borderul cand facem hover
}

.underline-indicators .active {
  border-color: hsl(var(--clr-white) / 1);
}

OBS: cu aspect-ratio: 1; si un display: flex/grid setat, putem face ca un element sa aiba 				width = height !!

O


	1)e mult mai bine pentru browser sa folosesti proprietatea de transition decat sa faci o animatie !!!
	2) cand folosesti pseudoclasa :hover NU UITA SA incluzi si pe :focus !!
	3) foloseste em cand declari un spatiu de padding/margin
	4)  <button aria-selected="true">Moon</button>
		<button aria-selected="false">Mars</button>
		<button aria-selected="false">Europa</button>
			-> what means that aria => Accessible Rich Internet Applications
				-> folosim pentru a da un extra context tehnologiilor asistente, cand aria e pe true
					ii spune asistentului ca noi am selectat elemetul cu aria:true
						-> spune tehnologiilor asistente ce tab este pornit
	5) foloseste clasa utilitara sr-only cand definesti un buton fara continut,iar screen readerul o sa citeasca ce scrie in acel element ASCUNS de noi restul

============================================================
## Pasul 2: Home Page

	->  Mobile or Desktop first? 
		-> cand stilizezi, fa layout-ul pentru desktop in media query, daca abordezi asa o sa ai de 2x mai putine linii de cod !!
		-> cand faci html, fa pentru desktop
		-> foloseste cat de multe clase utilitare poti
	
	-> da elementului BODY, o clasa numita home/ destinatin/ crew => astfel o sa iti fie foarte usor sa setezi un backgrund diferit pentru fiecare pagina in parte :))

### Layout
	-> grid/flex: daca vezi ca ai un pattern unde pe fiecare pagina ai 2 coloane la fel de late, foloseste GRID
		-> THE POWER OF GRID: ====defineste 4 coloane=== 
			-->2 pt continut
			-->2 pt spatiere (ca sa fie continutul centrat)
				->grid-template-columns: minmax(2rem, 1fr) repeat(2, minmax(auto, 30rem))  minmax(2rem, 1fr);
				 	first child {gird-column: 2}
					last child {gird-column: 3}

### Responsivness
	-> lui body dai display: grid; ca tot continutul sa se intinga pe acei 100vh.
		-> mai ii dai: grid-template-row: min-content 1fr; min content ca linie sa fie la fel de inalta linia cat nav barul iar 1fr sa se intinda pana in partea de jos a paginii linia 2 ca sa poti centra continutul principal din pagina
	
#### Responsize Typography
	-> Daca te uiti atent in figma file, poti observa fapul ca font-size-ul se schimba in functe de device, asa ca trebuie modificat font-size in functe de latimea dispozitivului
		-> SMART WAY: intr-un media query pt tableta si telefon, redefinesti DOAR variabilele de fs CARE SE SCHIMBA astfel o sa se ajusteze fs AUTOMAT
			-> din pacate font-size urile din figma file sunt bazate doar pe varianta de DESKTOP, asa ca pt cea de mobile si tableta trebuie sa ma uit pe macheta sa vad unde apar diferente...
				-> aceste media le pui chair dedesubt de :root {}

OBS: daca trebuie sa faci o clasa care faci un lucru, doar un singur lucru, atunci fa o clasa utilitara :))
	-> flex sau grid pt layout? Daca vezi un pattern: 2 coloane la del de late => fol GRID, poti si cu flexbox dar este mult de lucru si pot aparea erori, flex se foloseste cand e un design mai flexibil, mai diferit !

	-> cum pui textul pe centru ? NU CU FLEXBOX 
		foloseste => .grid-container {text-align: center}

	-> cum faci ca textul sa nu fie mai lung de o anumita latime in pagina?
		-> .parent > * { max-width: 50ch; } // ch = caractere
	
	-> place-items: center; //short form for justify items & align-items // pune spatiu intre copii
	-> place-content: center; // short form for align-content & place-content // lipeste copii unul de altul

	-> cum faci ca continutul unui div sa nu se lipeasca de marginile unui mobile device? dai un padding-inline containerului parinte si aia e

	-> minmax(minValue, maxValue)
	-> max(6rem, 20vh); it will take the biggher value between those 2
	-> clamp(minValue, mediumValue , maxValue);
		-> clamp(5rem, 8vw + 1rem, 9rem) //pt font size responsive


### Adding the background images
	-> va aparea in partea cea mai de jos din style.css
/* ------------------------- */
/* Page specific background  */
/* ------------------------- */
body {
  background-size: cover;
  background-position: bottom center;
}

/* home */
.home {
  background-image: url(assets/home/background-home-mobile.jpg);
}

@media (min-width: 35rem) {
  .home {
    background-position: center center;
    background-image: url(/starter-code/assets/home/background-home-tablet.jpg);
  }
}
@media (min-width: 45rem) {
  .home {
    background-image: url(/starter-code/assets/home/background-home-desktop.jpg);
  }
}

============================================================
## Pasul 3: NAVIGATION MENU
============================================================

### padding-block: 3rem;   == padding-top: 3rem  && padding-bottom: 3rem;
### padding-inline: 2rem  === padding-left: 2rem && padding-right: 2rem;