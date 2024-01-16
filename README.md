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
1. Diagrama generala:![Diagrama generala (3)](https://github.com/DreamTeamAMSS/.github/assets/104629833/22193dcb-b824-42ea-b3ee-2c3729799534)

   
   La deschiderea aplicatiei apare pagina HOME care are functionalitati pentru utilizatorii logati si vizitatori nelogati:
   - daca utilizatorul nu este logat:
      - poate cauta o intrebare introducand un keyword, dupa care daca sunt rezultate, vor fi          afisate intr-o lista din care utilizatorul alege o intrebare si navigheaza la pagina             acesteia unde vizualizeaza continutul intrebarii, raspunsurile si sugestiile acesteia dar        nu poate face modificari pentru ca nu este logat
      - are acces la optiunea de Log In
         - daca utilizatorul are un cont, acesta este redirectionat catre pagina de Log In, unde          isi introduce datele:
              - daca datele contului nu sunt corecte, acesta ramane pe pagina de Log In pana                      introduce datele corecte ale contului, fiind afisat un mesaj de eroare
              - daca datele contului sunt corecte, acesta este redirectionat catre pagina HOME                   cu functionalitati pentru utilizatorul autentificat
         - daca utilizatorul nu detine un cont, acesta este redirectionat catre pagina de Sign               Up unde completeaza campurile de email, username si parola:
              - daca datele nu corespun cerintelor campurilor, utilizatorul nu este lasat sa isi                creeze cont pana nu introduce date corespunzatoare campurilor
              - daca datele corespund cerintelor campurilor utilizatorul este autentificat in                   aplicatie si redirectionat catre pagina HOME pentru utilizatorul autentificat
   - daca utilizatorul este logat, acesta are mai multe optiuni:
      - poate sa isi vizualizeze pagina de profil unde are acces la detalii si isi poate                vizualiza badge-urile obtinute in urma punctelor acumulate
      - are optiunea de a iesi din cont apasand butonul de Log Out, fiind redirectionat inapoi          catre pagina de Log In
      - are acces la o pagina care contine o lista cu intrebarile adaugate de el si de pe                fiecare intrebare poate naviga la pagina individuala a intrebarii
      - are acces la o pagina care contine o lista cu raspunsurile adaugate de el si de pe                fiecare intrebare poate naviga la pagina individuala a intrebarii
      - are acces la o pagina care contine o lista cu sugestiile adaugate de el 
      - poate naviga catre pagina "Adauga intrebare" si acolo dupa ce introduce datele unei             intrebari (titlu, descriere), aceasta este postata si este redirectionat catre pagina             intrebarii. Aici utilizatorul are mai multe optiuni fiind logat deja in aplicatie:
         - poate adauga un raspuns si daca doreste, poate adauga si sugestii la raspunsurile                existente
         - poate adauga sugestii la intrebare
         - poate marca un raspuns ca fiind cel mai bun acordandu-i steluta

  
   
   
3. Diagrama de obiecte: 
![diagrama ER amss](https://github.com/DreamTeamAMSS/.github/assets/104629833/aab49fd9-d0ec-44dd-a9da-3c6fb0d885b4)

4. Diagrama de clase:
![diagrama_clase](https://github.com/DreamTeamAMSS/.github/assets/63183691/35029b3a-ced5-4bd0-bcb0-92dc92074c09)

5. Diagrama arhitecturii aplicatiei
![arh_app](https://github.com/DreamTeamAMSS/.github/assets/63183691/fedea3b4-cbbd-4933-8f86-64877bd64435)
   
6. Diagrama de secventa pentru autentificare: 
![Diagrama de secventa](https://github.com/DreamTeamAMSS/.github/assets/104629833/dfa65615-57f4-467d-8166-6435930112da)
