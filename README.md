# Identifying-messages-from-images-of-hand-signs-language
Data Collection

	1-5
Se importa librariile necesare

		1
Biblioteca opencv ofera functionalitati pentru citirea, scrierea, manipularea si afisarea imaginilor, detectarea si urmarirea obiectelor, recunoastere faciala, procesare video, calibrarea camerei etc. cv2 este modulul principal al acesteia.

		2
Se importa clasa HandDetector din modulul HandTrackingModule(care se afla in cvzone). Acest modul este special creat pentru detectarea si urmarirea mainilor. Furnizeaza clase si functii predefinite, special concepute pentru sarcini legate de maini(astfel extinde functionalitatea OpenCV).

		3
Se importa biblioteca pentru calcul stiintific si numeric NumPy(Numerical Python) careia i se asociaza aliasul np(pentru o scriere mai usoara). Ne ofera acces la diverse functii si metode care faciliteaza lucrul cu structuri de date multidimensionale.

		4
Importarea modulului math. Modul standard care ofera functionalitati matematice si trigonometrice.

		5
Importarea modului time. Ofera functionalitati legate de timp si de masurarea acestuia.

	7-8
Initializarea capturii video si a detectorului mainii

		7
Se creeaza un obiect(cap) de tipul VideoCapture pentru a captura imaginile de la o sursa video, aici parametru 0 inseamna camera web integrata.
	
		8
Se creeaza un obiect de tip HandDetector. Argumentul maxHand indica numarul de maini pe care le detecteaza si urmareste in fluxul video

	10-13
Definirea variabilelor
	
		10
Valoarea de offset pentru decuparea în jurul regiunii mainii
Offsetul reprezinta o margine (un fel de largire) adaugata în jurul regiunii de interes, obtinuandu-se o regiune mai mare in care pot fi incluse elemente relevate in cadrul imagii decupare.

		11
Dimensiunea finala a imagii taiate

		12
Folderul cale la care se salveaza imaginile taiate(cele cu mana)
Imaginile sunt folosite ulterior pentru a construi seturi de date de antrenament.

		13
Variabila care care contorizeaza numarul de imagini salvate

	15-55
Bucla principala pentru procesarea videolui
		
		15
Procesarea are loc continuu atat timp cat programul nu este intrerupt manual sau prin inchisderea aplicatiei

		16
Citirea urmatorului cadru din sursa video(cu metoda read-predefinita).
Variabila succes este de tip boolean si indica daca citirea datelor a fost realizata cu succes sau nu(false-nu mai exista cadre de citit)
Variabila img este o matrice NumPy care contrice informatiile pixelilor pentru fiecare punct din cadrul citit.

		17
Detectarea si urmarirea mainii.
Metoda findHand primeste ca parametru img (imaginea originala) si returneaza in variabila hands informatii despre mana detectata, iar variabila img este imaginea originala modificata, avand incadrarea regiunii de interes.

		18-22
Detectarea mainii/mainilor si decuparea regiunii de interes.

			18
Se verifica daca exista maini detectate. Daca s-a detectat o mana atunci se executa codul din blocul if
			
			19
Se foloseste hands[0] (adica primul element al listei) care contine informatii despre prima mana detectata.

			20
bbox - bounding box
hand['bbox'] extrage informatiile necesare de la chenarul care incadreaza mana
x si y reprezinta coordonatele contului din stanga sus a chenarului
w si h sunt dimensiunile chenarului (latime, inaltime)
Aceste valori vor fi utilizate pentru redimensionarea imaginii la zona mainii(zona de interes)

			21
Se creeaza o imagine alba cu trei canale (rosu, verde si albastru). 
uint8 - tip de date care reprezinta un numar intreg pe 8 biti 
Metoda ones creeaza matricea de dimensiunile specificate cu toate elementele egale cu 1. Inmultind fiecare element al matricii cu 255 se obtine imagine complet alba(pentru fiecare canal se obtine valoarea maxima de luminozitate 255).
Imaginea se va umple cu continutul altei imagini(portiunea cu mana).

			22
Se decupeaza regiunea de interes din imagine(acea imagine care incadreaza mana intr-un chenar)  

		23-41
Redimensionarea si plasarea imaginii decupate pe un fundal alb

			23
In variabila imgCropShape (care este o tupla: inaltime, latime, nr de canale) se stocheaza dimensiunile portiunii decupate din imagine.

			24
Calcularea raportului de aspect al imaginii decupate(ajuta la a-ti da seama cum este distribuita latimea si inaltimea, un rezultat>1=>imagine portret, rezultat<1=>imagine cu aspect orizontal).

			26
Se verifica daca dimensiunile imaginii sunt nenule. Daca se indeplineste conditia se intra in bucla if

			27
Se verifica daca aspectul imaginii este de tip portret. In acaz afismativ se executa bucla if

			28
Calcularea factorului de scalare. Acesta se va folosi pentru o redimensionare corespunzatoare a portiunii decupate si pentru asigurarea ca se pastreaza proportiile imaginii(in functie de dimensiunea dorita).

			29
Calcularea latimii pentru imaginea redimensionata(se asigura ca nu se pierde informatie la redimensionare).

			30
Redimensionarea imaginii decupate cu dimensiunile dorite(in functie de rapotul de aspect al imaginii initiale).

			31
In variabila imgResizeShape (care este o tupla: inaltime, latime, nr de canale) se stocheaza dimensiunile imaginii redimensionate.

			32
Calcularea diferentei dintre dimensiunea dorita si cea rezultata prin calcul

			33
Inlocuirea submatricei selectate din imaginea alba cu imaginea redimensionata(si asigurarea ca se potriveste in chenar).

			35
In caul in care imaginea este cu aspect orizaontal se executa codul de pe else

			36
Se calculeaza facorul de scalare

			37
Se calculeaza inaltimea pentru imaginea redimansionata(prin ceil ne asiguram ca nu perdem informatie la redimensionare, va returna intregul mai mare sau egal cu argumentul dat).

			38
Redimensionarea imaginii decupate cu dimensiunile dorite(in functie de rapotul de aspect al imaginii initiale).

			39
In variabila imgResizeShape (care este o tupla: inaltime, latime, nr de canale) se stocheaza dimensiunile imaginii redimensionate

			40
Calcularea diferentei dintre inaltimea(imgSize) dorita si cea rezultata prin calcul(hCal)

			41
Inlocuirea submatricei selectate din imaginea alba cu imaginea redimensionata(si asigurarea ca se potriveste in chenar).

		43-45
Afisarea imaginii decupate si a celei redimensionate doar atunci cand dimensiunile imaginii sunt nenule

		47
Afisarea imaginii originale cu mana detectata

		48-52
Salvarea imaginii decupate atunci cand de apasa tasta 's'

			48
Se asteapta o milisecunda apasarea unei taste de catre utilizator si returneaza codul acesteia

			49
Daca tasta apasata este identica cu codul Unicode asociat caracterului s atunci se intra in if
			
			51
Se salveaza imaginea in directorul dat cu nume unic in functie de timpul la care a fost facuta.

		54-55
Daca se apasa tasta q se va iesi din program

OpenCV = Open Source Computer Vision


Testing

	3
ClasificationModule ofera functionalitati specifice clasificarii imaginilor
Clasa Clasifier realizeaza clasificarea imaginilor folosind un model pre-antrenat.
Un model pre-antrenat este un model de învățare automată care a fost antrenat pe un set de date mare și divers în prealabil, folosind o arhitectură specifică și o sarcină specifică. Modelul pre-antrenat a trecut prin etapa de antrenare, în care a învățat să recunoască și să extragă caracteristici dintr-un set de date de antrenare.

	10
Crearea unui obiect al clasei Classifier
Primul parametru este calea catre fisierul ce contine modelul pre-antrenat in format Keras
Al doilea parametru este calea catre fisierul care contine etichetele asociate celor prezise de model. Etichetele sunt utilizate pentru a atribui un nume corespunzator rezultatelor clasificarii si vor fi afisate in urma predictiilor.


	15
Variabila labels contine o lista de siruri de caractere care sunt etichetele asociate claselor prezise de modelul de clasificare a imaginilor.

	18
Se face o copie a imaginii originale captate de la camera pentru ca atunci cand se vor aduce modificari asupra imaginii, cea originala sa nu fie afectata.

	36
Functia getPrediction primeste ca parametru imaginea si returneaza doi parametri
Primul parametru este predictia, valoare care indica clasa la care sistemul de clasificare atribuie cea mai mare probabilitate pentru imaginea data
Al doilea parametru indica indicele din lista labels al clasei prezise 
Deoarece nu dorm modificarea imaginii vom seta draw = False, care nu va mai desena conturul mainii si eticheta 

	49
Se va desena un dreptunghi(pe care, ulterior, se va scrie mesajul decodificat) pe copia imaginii 
Funcita rectangle primeste ca parametru imaginea, coltul din stanga sus, dreapta jos, culoarea, si se doreste umplerea dreptungiului cu culoarea specificata

	51
Scrierea mesajului pe dreptunghiul tocmai desenat
Functia putText primeste ca parametru imaginea pe care se dorescte a scrie, mesajul de imprimat, coordonatele de start ale textului, fontul utilizat si dimensiunea textului, culoarea, grosimea liniei textului.

	52
Se va desena dreptunghiul care incadreaza mana
Ultimul parametru al functie reprezinta grosimea liniei de contur

