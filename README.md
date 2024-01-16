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

**4. Diagrama arhitecturii aplicatiei**
![arh_app](https://github.com/DreamTeamAMSS/.github/assets/63183691/fedea3b4-cbbd-4933-8f86-64877bd64435)
Arhitectura aplicatiei este formata dintr o interfata web realizata cu React.js, un server implementat cu Spring Boot si baza de date a server-ului de tip SQL realizata in PostgreSQL.
Utilizatorul interactioneaza cu interfata web, interfata care la randul ei comunica cu server-ul prin metode de tip request-response pentru a furniza date din server catre interfata.
   
**5. Diagrama de secventa pentru autentificare**: 
![image](https://github.com/DreamTeamAMSS/.github/assets/63097668/966a499f-0bdb-4929-9d62-12df93a6954a)
In diagrama de secventa pentru autentificare prezentam flow-ul ce are loc in momentul in care un utilizator se logheaza in aplicatie si doreste sa acceseze intrebarile.
Metoda POST legata la endpoint-ul "login" realizeaza logarea utilizatorului prin intermediul validarii atat a email-ului si parolei, cat si a token-ului JWT. Tot pe baza validarii acestui token, ulterior utilizatorul va accesa lista cu intrebarile adresate in cadrul aplicatiei web.

**6. Diagrama de secventa pentru cautarea unei intrebari care contine keyword-ul introdus de utilizator**:
![diagrama secventiala (1)](https://github.com/DreamTeamAMSS/.github/assets/104629833/cb0a1d7b-e1ab-4a12-9e87-dc08db37593d)

Clientul introduce keyword-ul in search bar realizandu-se o cerere de tip POST catre "/api/questions/search", apoi Serverul valideaza keyword-ul introdus returnand o lista cu intrebarile care contin acel cuvant, Clientul vizualizeaza intrebarile si selecteaza din lista intrebarea dorita, dupa care Serverul furnizeaza datele despre respectiva intrebare.

