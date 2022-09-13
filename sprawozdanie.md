# Integracja projektu Open Source z systemem DevOps

# Wybór projektu

Wybrany projekt to Laravel - framework do aplikacji internetowych napisany w języku PHP bazujący na wzorcu architektonicznym Model-View-Controller.

# Licencja projektu

Licencja MIT – jedna z najprostszych i najbardziej liberalnych licencji otwartego oprogramowania. Daje użytkownikom nieograniczone prawo do używania, kopiowania, modyfikowania i rozpowszechniania oryginalnego lub zmodyfikowanego programu w postaci binarnej lub źródłowej.


# Przygotowanie środowiska DevOps
  
Aby uruchomić aplikację Laravel za pomocą Dockera definujemy następujące serwisy w pliku docker-compose.yml

![image](https://user-images.githubusercontent.com/58239029/176698062-f25f8033-f54b-4f4f-8ed2-bd3cbf69fe4b.png)

nginx – serwer WWW oraz serwer proxy dla HTTP i IMAP/POP3 stworzony przez Igora Sysojewa a rozwijany i wspierany przez założoną przez niego firmę, Nginx, Inc. Zaprojektowany z myślą o wysokiej dostępności i silnie obciążonych serwisach. Wydawany jest na licencji BSD.

Aby nginx został poprawnie uruchomiony tworzymy plik konfiguracyjny serwera

![image](https://user-images.githubusercontent.com/58239029/176699764-660819ec-6418-421d-baed-ad6274874c2c.png)


![image](https://user-images.githubusercontent.com/58239029/176698169-fc48cb25-925d-4861-a0c7-096af9e3031c.png)

MySQL – wolnodostępny, otwartoźródłowy system zarządzania relacyjnymi bazami danych. MySQL rozwijany jest przez firmę Oracle. Wcześniej przez większość czasu jego tworzeniem zajmowała się szwedzka firma MySQL AB.

![image](https://user-images.githubusercontent.com/58239029/176698244-57af1795-97f3-4f9e-ac4a-e5b49eea20ed.png)

PHP – interpretowany, skryptowy język programowania zaprojektowany do generowania stron internetowych i budowania aplikacji webowych w czasie rzeczywistym.

# Uruchomenie aplikacji

Kontenery uruchamiamy za pomocą polecnia : docker-compose build && docker-compose up -d
![image](https://user-images.githubusercontent.com/58239029/176700613-262399ee-4498-4d01-9a14-20a529012467.png)

# Komunikacja z aplikacją

Z aplikacją możemy komunikować się za pomocą portu w przęglądarce internetowej: 
![image](https://user-images.githubusercontent.com/58239029/176701461-2c4e8482-d788-4b72-9c4d-4012860f3f77.png)

Lub z poziomu wiersza poleceń:

![Zrzut ekranu 2022-06-29 144249](https://user-images.githubusercontent.com/58239029/176701773-70ee8f24-fbf6-4e7f-9123-cd1bc7671fa0.png)


# Integracja projektu z Jenkins

Jenkins to serwer automatyzacji. Chociaż można go użyć do zautomatyzowania niemal każdego zadania, najczęściej wiąże się to z tworzeniem kodu źródłowego i wdrażaniem wyników. Dla wielu Jenkins jest synonimem ciągłej integracji i ciągłego dostarczania (CI/CD).

Jedną z najpotężniejszych funkcji Jenkinsa jest jego zdolność do rozdzielania zadań na wiele węzłów. Kontroler Jenkins wysyła zadania do odpowiedniego agenta na podstawie wymagań zadania i dostępnych w danym momencie zasobów.


# Zestawienie nowej instancji Jenkinsa za pomocą środowiska Docker
Uruchamianie Jenkinsa za pomocą Docker Compose
Możesz uruchomić kontroler Jenkins za pomocą jednego polecenia Docker:

$ docker run -it -p 8080:8080 jenkins/jenkins:lts

To da ci działający kontroler Jenkins. Możesz go skonfigurować, zalogować się i rozpocząć wykonywanie zadań. Ale jeśli uruchomisz go ponownie, stracisz wszystkie swoje dane. Musisz skonfigurować wolumin, aby uruchomić dane instancji Jenkins.

Użyjemy do tego Docker Compose.

![image](https://user-images.githubusercontent.com/58239029/189926683-6fc83eb2-d14a-4e18-8257-ebade1b3cd82.png)
 
Kontenery, które dotychczas nie zostały zaincjowane w naszym systsemie uruchamiamy za pomocą polecenia

docker-compose build && docker-compose up -d

# Pro-Tip

Jeśli korzystamy z edytora kodu VScode możemy doinstalować wtyczkę Docker, która ułatwi nam proces maniupulowania kontenerami

![image](https://user-images.githubusercontent.com/58239029/189929111-50c45c32-8e4f-47f2-9054-86c9145522ee.png)

Możemy za jej pomocą uruchamiać i wyłączać kontenery oraz możemy zajrzeć do środka i zobaczyć pliki, które są zawarte w środku

# Uruchomienie i konfiguracja Jenkinsa

![image](https://user-images.githubusercontent.com/58239029/189929953-897cb773-8e1d-4288-8694-c1907cc74865.png)

Przy pierwszym uruchomieniu Jenkins poprosi nas o podanie hasła admina, hasło to możemy wyciągnąć z pliku, który znajduję się pod wskazaną ścieżką

/var/jenkins_home/secrects/initialAdminPassword

Do naszej instacji Jenkinsa dostajemy się wpisując komendę w bashu:
docker exec -it jenkins /bin/bash
Następnie kierujemy się do pliku, w którym zawarte jest hasło i kopiujemy je do naszego Jenkinsowego GUI

Następnym krokiem jest stworzenie profilu użytkownika
![Zrzut ekranu 2022-09-06 191742](https://user-images.githubusercontent.com/58239029/189931737-45c395d1-4f8e-4cb5-8501-634ec81a2511.png)

Następnie rozpoczynamy pracę nad definiowaniem naszego rurociągu

# Integracja naszego pipelina z repozytorium na github

Podajemy link do naszego repozytorium

![image](https://user-images.githubusercontent.com/58239029/189933411-ad0e6f44-64d0-4f65-aed3-3b57fe5a6541.png)

Dodajemy webhooka w ustawieniach naszego repozytorium

![image](https://user-images.githubusercontent.com/58239029/189934385-f7747826-cd6b-47d6-b76b-bb37c8e944bd.png)

Oraz zaznaczamy stosowne dla nas opcje

![image](https://user-images.githubusercontent.com/58239029/189934619-b5359674-4f42-485c-b78a-145800893de1.png)

W moim przypadku rurociąg poinformuję nas o wykonywanych zmianach w kodzie t.j w tym przypadku: 
![image](https://user-images.githubusercontent.com/58239029/189935268-22d22151-e0c2-48bd-aa5c-d8299324d2b3.png)




# Deklaracja rurociągu

Stworzenie obiektu pipeline, przeprowadzającego następujące kroki: 
- Build
- Test
- Deploy

![image](https://user-images.githubusercontent.com/58239029/176706071-4686d1a6-2842-4b4b-acc4-a6514bc25568.png)

Uruchomienie rurociągu 

![image](https://user-images.githubusercontent.com/58239029/176707038-3ab88646-1f26-4abc-bd11-1153b76729aa.png)

Wizualizacja historii budowania rurociągu

![image](https://user-images.githubusercontent.com/58239029/176708415-c27c2016-495e-4797-abb2-dc5e036678d3.png)

# Publish

Aplikacja musi znajdywać się na serwerze, ponieważ komunikacja z nią odbywa się za pomocą protokołu HTTP.



