# System requirements
1. Un utilizator isi poate crea cont in platforma.
2. Un utilizator se poate autentifica in platforma.
3. Un vizitator neinregistrat poate cauta si vizualiza intrebari (si raspunsuri).
4. Un utilizator autentificat poate adauga atat intrebari noi, cat si raspunsuri la intrebarile altor utilizatori.
5. Un utilizator autentificat poate marca cel mai bun raspuns la intrebarea sa.
6. Un utilizator autentificat poate sugera imbunatiri/modificari la intrebari/raspunsuri.
7. Un utilizator autentificat poate primi puncte daca adauga raspunsuri, intrebari, sugestii sau daca ii este marcat raspunsul ca fiind best answer.


# Entities
1. User 
2. Badge
3. Question
4. Answer
5. Suggestion
   
# Diagrame
**1. Diagrama generala**:
![Diagrama generala (4)](https://github.com/DreamTeamAMSS/.github/assets/104629833/e6b54622-a0bf-4186-bd77-f3a19985d5cc)

   La deschiderea aplicatiei apare pagina HOME care are functionalitati pentru utilizatorii logati si vizitatori nelogati:
   - daca utilizatorul nu este logat:
      - poate cauta o intrebare introducand un keyword, dupa care daca sunt rezultate, vor fi afisate intr-o lista din care utilizatorul alege o intrebare si navigheaza la pagina acesteia unde vizualizeaza continutul intrebarii, raspunsurile si sugestiile acesteia dar nu poate face modificari pentru ca nu este logat; daca vrea sa se logheze o poate face din bara de navigare
      - are acces la optiunea de Log In
         - daca utilizatorul are un cont, acesta este redirectionat catre pagina de Log In, unde isi introduce datele:
              - daca datele contului nu sunt corecte, acesta ramane pe pagina de Log In pana introduce datele corecte ale contului, fiind afisat un mesaj de eroare
              - daca datele contului sunt corecte, acesta este redirectionat catre pagina HOME cu functionalitati pentru utilizatorul autentificat
         - daca utilizatorul nu detine un cont, acesta este redirectionat catre pagina de Sign Up unde completeaza campurile de email, username si parola:
              - daca datele nu corespun cerintelor campurilor, utilizatorul nu este lasat sa isi creeze cont pana nu introduce date corespunzatoare campurilor
              - daca datele corespund cerintelor campurilor utilizatorul este autentificat in aplicatie si redirectionat catre pagina HOME pentru utilizatorul autentificat
   - daca utilizatorul este logat, acesta are mai multe optiuni:
      - poate sa isi vizualizeze pagina de profil unde are acces la detalii si isi poate vizualiza badge-urile obtinute in urma punctelor acumulate
      - are optiunea de a iesi din cont apasand butonul de Log Out, fiind redirectionat inapoi catre pagina de Log In
      - are acces la o pagina care contine o lista cu intrebarile adaugate de el si de pe fiecare intrebare poate naviga la pagina individuala a intrebarii
      - are acces la o pagina care contine o lista cu raspunsurile adaugate de el si de pe fiecare intrebare poate naviga la pagina individuala a intrebarii
      - are acces la o pagina care contine o lista cu sugestiile adaugate de el 
      - poate naviga catre pagina "Adauga intrebare" si acolo dupa ce introduce datele unei intrebari (titlu, descriere), aceasta este postata si este redirectionat catre pagina intrebarii. Aici utilizatorul are mai multe optiuni fiind logat deja in aplicatie:
         - poate adauga un raspuns si daca doreste, poate adauga si sugestii la raspunsurile existente
         - poate adauga sugestii la intrebare
         - poate marca un raspuns ca fiind cel mai bun acordandu-i steluta
   
**2. Diagrama de obiecte**: 
![diagrama ER amss (1)](https://github.com/DreamTeamAMSS/.github/assets/104629833/b1f46ed1-0f21-4d6f-9335-3b26a98c0a0f)

Diagrama de obiecte reprezinta diagrama bazei de date si este alcatuita din 5 tabele. Fiecare tabel
are o cheie primara, iar relatiile dintre tabele sunt conturate astfel:
1. Utilizatorii inregistrati pot primi mai multe badge-uri in functie de punctele pe care le acumuleaza adaugand intrebari sau raspunsuri si sugestii la intrebarile existente (m:n badge - user)
2. Un utilizator inregistrat poate adauga mai multe intrebari. (1:n user - question)
3. Un utilizator inregistrat poate adauga mai multe raspunsuri la intrebarile existente, indiferent de cine este autorul respectivelor intrebari. (1:n user - answer)
4. Un utilizator inregistrat poate adauga mai multe sugestii la intrebarile sau raspunsurile existente, indiferent de cine este autorul respectivelor intrebari sau raspunsuri. (1:n user - suggestion)
5. O intrebare poate avea mai multe sugestii in cazul in care problema nu a fost formulata clar (1:n question - suggestion)
6. Un raspuns poate avea mai multe sugestii in cazul in care nu sunt suficient de clare sau necesita imbunatatiri. (1:n answer - suggestion)
7. O intrebare are un raspuns marcat ca Best Answer si acesta este marcat de catre autorul intrebarii. (1:1 question - answer)
   
**3. Diagrama de clase**:
![diagrama_clase](https://github.com/DreamTeamAMSS/.github/assets/63183691/35029b3a-ced5-4bd0-bcb0-92dc92074c09)
Am realizat diagrama de clasă pentru clasele de tip Entity din backend-ul aplicației pentru a surprinde relațiile, câmpurile și metodele din cadrul acestor tipuri de clase. Clasele entitate sunt reprezentări în cod Java ale modelului de date din baza de date. Practic, sunt mapări ale tabelelor din baza noastră de date relațională, astfel că vom avea următoarele 5 clase de tip entitate mapate la entitățile bazei nostre de date:
1. UserEntity
2. BadgeEntity
3. QuestionEntity
4. AnswerEntity
5. SuggestionEntity

Dat fiind că AnswerEntity, QuestionEntity și SuggestionEntity au în comun faptul că practic toate sunt comentarii, deci toate au fost scrise de către un user, au conținut text, data la care au fost create/modificate, acestea moștenesc clasa BaseCommentEntity(care conține field-urile comune enumerate). Am folosit class inheritance pentru a nu scrie cod redundant. Pentru celelalte entități care au în comun doar data la care au fost create/modificate am creat clasa BaseEntity.

**4. Diagrama arhitecturii aplicatiei**
![arh_app](https://github.com/DreamTeamAMSS/.github/assets/63183691/fedea3b4-cbbd-4933-8f86-64877bd64435)
Arhitectura aplicatiei este formata dintr o interfata web realizata cu React.js, un server implementat cu Spring Boot si baza de date a server-ului de tip SQL realizata in PostgreSQL.
Utilizatorul interactioneaza cu interfata web, interfata care la randul ei comunica cu server-ul prin metode de tip HTTP request-response pentru a furniza date din server catre interfata.
   
**5. Diagrama de secventa pentru autentificare**: 
![image](https://github.com/DreamTeamAMSS/.github/assets/63097668/966a499f-0bdb-4929-9d62-12df93a6954a)
In diagrama de secventa pentru autentificare prezentam flow-ul ce are loc in momentul in care un utilizator se logheaza in aplicatie si doreste sa posteze o intrebare.
Metoda POST legata la endpoint-ul protejat "/login" realizeaza logarea utilizatorului prin intermediul validarii email-ului si parolei, si transmite in response token-ul JWT de acces. Tot pe baza validarii acestui token, ulterior utilizatorul va putea posta o intrebare.

**6. Diagrama de secventa pentru cautarea unei intrebari care contine keyword-ul introdus de utilizator**:
![diagrama secventiala (1)](https://github.com/DreamTeamAMSS/.github/assets/104629833/cb0a1d7b-e1ab-4a12-9e87-dc08db37593d)

Clientul introduce keyword-ul in search bar realizandu-se o cerere de tip POST catre "/api/questions/search", apoi Serverul valideaza keyword-ul introdus returnand o lista cu intrebarile care contin acel cuvant, Clientul vizualizeaza intrebarile si selecteaza din lista intrebarea dorita, dupa care Serverul furnizeaza datele despre respectiva intrebare.

# Design Patters

**1. Backend**:

**2. Frontend**:
In partea de Frontend a aplicatiei au fost utilizate cateva concepte ce pot fi asociate cu Design Patterns:
   1. Creational Patterns:
      Factory Method și Abstract Factory:
      - `useState` este un fel de "factory method" deoarece lucreaza cu o instanta noua a starii componentei, permitand crearea de stari locale pentru componente, similar cu modul in care Factory Method creeaza si returneaza obiecte.<img width="528" alt="image" src="https://github.com/DreamTeamAMSS/.github/assets/104629833/9e529d8a-5443-4ce5-9803-3fcd2fe9e141">

   2. Structural Patterns:
      Facade:
      - Facade ofera o interfata simplificata catre un ansamblu mai mare de componente, astfel ca in React, am folosit o componenta de tip 'facade' care gestioneaza si ascunde detaliile complicate. (De exemplu pentru adaugarea intrebarii am facut o componenta separata pe care am apelat-o din componenta Home ca sa evitam incarcarea codului in componenta principala) <img width="278" alt="image" src="https://github.com/DreamTeamAMSS/.github/assets/104629833/1b2c130a-dde8-496c-bc4c-897626c13d0d">

   3. Behavioral Patterns
      Observer:
      - efectele secundare gestionate cu ajutorul useEffect pot fi asociate cu Observer Pattern. useEffect permite observarea și reacționarea la modificările în starea unei componente sau la alte evenimente. Astfel, când starea se modifică, efectul asociat este notificat și poate reacționa în consecință.<img width="200" alt="image" src="https://github.com/DreamTeamAMSS/.github/assets/104629833/3747a431-14d1-44a0-abf0-af19c5848ab0">

      Mediator:
      - compoentele pot comunica intre ele prin intermediul unui obiect mediator, in cazul nostru `Header` functioneaza mediator pentru evenimentele de cautare si pentru manipularea starii cautarii si `SearchBar` serveste ca o componenta controlata care primeste instructiuni de la parintele sau (`Header`) si furnizeaza rezultatele cautarii inapoi catre acesta<img width="244" alt="image" src="https://github.com/DreamTeamAMSS/.github/assets/104629833/b2c0bf68-a0da-4ff9-a1ff-ce97a1b4b14c">

      Strategy, Template Method
      - utilziarea functionalitatii `fetch` poate fi comparata cu Strategy pentru obtinerea datelor in aplicatie, iar modul incare se utilizeaza poate respecta un Template Method, deoarece `fetch` reprezinta o strategie pentru a realiza cereri HTTP in aplicatei, iar modul in care structuram si gestionam cererile respecta un template method (daca datele nu au fost preluate vom afisa un mesaj de eroare, iar daca au fost preluate cu succes randam continutul)<img width="439" alt="image" src="https://github.com/DreamTeamAMSS/.github/assets/104629833/8aa5d815-705b-47cd-accc-efd31174de13">




