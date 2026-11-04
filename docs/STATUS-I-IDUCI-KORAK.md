# AI-Oglasnik — stanje projekta i primopredaja

**Ažurirano:** 4. 11. 2026.  
**Repozitorij:** https://github.com/hariskaraicic-blip/AI-oglasnik  
**Svrha:** nastavak rada nakon prekida chata bez ponovnog objašnjavanja projekta.

> GitHub je izvor istine. Prije izmjene provjeriti aktualni branch, datoteke i commit. Ovo je sažetak poznatog stanja na datum iznad; lokalne datoteke mogu se promijeniti.

## 1. Cilj projekta

AI-Oglasnik je prototip koji prima običan tekst korisnika i pretvara ga u strukturiran oglas. Fokus je stabilnost i kvaliteta AI-generiranja, a ne izgradnja velikog marketplacea.

Predviđeni tok:
1. Korisnik napiše opis proizvoda.
2. AI pripremi strukturirani oglas.
3. Korisnik pregleda i uredi rezultat.
4. Oglas se sprema tek nakon potvrde korisnika.
5. Korisnik može pregledati spremljene oglase.

**Pravilo:** AI ne smije izmišljati cijenu, stanje, lokaciju, specifikacije, garanciju ni druge tvrdnje. Nedostajuće vrijednosti ostaviti praznima/neutralnima ili pitati korisnika.

## 2. Što je potvrđeno da je urađeno

### GitHub i dokumentacija
- Repozitorij postoji: https://github.com/hariskaraicic-blip/AI-oglasnik
- Posljednje zabilježeno lokalno usklađenje bilo je s origin/main; zadnji poznati commit: 7e500a5 („Add Grok project handoff brief”).
- Dokumenti u repozitoriju: README.md, docs/AI-Oglasnik-Dokumentacija.md, docs/GROK-PRIMOPREDAJA.md i docs/PLAN-I-PRIMOPREDAJA.md.
- Lokalno je napravljen .gitignore koji isključuje .env, Python cache i virtualna okruženja. Prije dodavanja datoteka u Git treba potvrditi da ignorira i lokalne SQLite baze.

### Lokalno pregledane backend datoteke
U posljednjoj provjeri postojale su:
- backend/agents/parser_agent.py
- backend/db/database.py
- backend/db/oglasnik.db

Tada nisu pronađeni backend/main.py, app.py ni requirements.txt. FastAPI API iz dokumentacije zato nije bio potvrđen kao implementiran.

### AI parser
- Koristi Python, requests i python-dotenv.
- Čita Gemini ključ iz varijable GEMINI_API_KEY.
- Funkcija parse_ad_input(raw_text) šalje tekst Gemini API-ju i očekuje JSON polja: title, category, price, condition, location, description.
- Cijena je zamišljena kao broj u KM ili 0; stanje kao „Novo”/„Polovno”.
- Poznati nedostaci: provjera ključa pri importu modula, nema eksplicitnog HTTP timeouta, obrada API grešaka i parsiranje JSON-a trebaju biti otporniji. Model/endpoint i API kompatibilnost potvrditi testom.

### SQLite baza
- Putanja: backend/db/oglasnik.db.
- Tablica ads postoji sa stupcima id, title, category, price, condition, location, description, created_at.
- Zadnja readonly provjera pokazala je jedan testni zapis: „Bager JCB 3CX”, kategorija „Industrija”, cijena 35000 KM, Polovno, Tuzla.
- **Sačuvati postojeću bazu i testni zapis.** Ne brisati, prepisivati ni mijenjati shemu bez kopije i jasnog razloga.

### Okruženje
U Termuxu su u zadnjem zabilježenom pregledu bili instalirani FastAPI, Pydantic, requests i python-dotenv. Uvicorn nije bio vidljiv u tadašnjem popisu paketa. Prije instalacije ovisnosti ponovno provjeriti trenutno stanje.

## 3. Što još nije potvrđeno / nedostaje

- Pokretljiva FastAPI aplikacija i stvarni endpointovi.
- Validacijski Pydantic modeli i ugovor request/response.
- POST kreiranje oglasa i GET dohvat oglasa.
- Jasna granica između AI generiranja, korisničkog pregleda i spremanja.
- Pouzdana obrada API grešaka, timeouta, neispravnog JSON-a i nedostajućih polja.
- Minimalni automatizirani testovi.
- requirements.txt i provjerene upute za pokretanje.
- Jednostavno web sučelje prilagođeno mobitelu.
- Testiranje AI rezultata na više stvarnih primjera.
- Provjera da tajne i SQLite baza nisu slučajno praćene Gitom.

Ovo su stavke nepotvrđene ili nedovršene, a ne tvrdnja da ništa od toga nije naknadno dodano. Provjeriti aktualno stanje prije rada.

## 4. Plan — idući koraci redom

### Korak 1 — pregled i sigurnosna provjera
- Provjeriti git status, branch i zadnji commit.
- Pregledati aktualne datoteke i .gitignore.
- Potvrditi da .env, ključevi i SQLite baze nisu praćeni Gitom.
- Napraviti kopiju SQLite baze prije bilo kakve promjene baze.

**Gotovo kada:** stanje repozitorija i datoteka je jasno, a tajne/baza nisu izložene.

### Korak 2 — stabilizirati parser
- Ukloniti potrebu da se API ključ validira prilikom importa modula.
- Dodati timeout i jasnu obradu HTTP/API grešaka.
- Validirati AI JSON i tipove polja; neispravne vrijednosti sigurno odbaciti ili neutralno obraditi.
- Ne dopunjavati činjenice koje korisnik nije naveo.
- Testirati parser uz mock odgovor, bez nepotrebnog trošenja API poziva.

**Gotovo kada:** parser pouzdano vraća očekivani oblik ili razumljivu grešku.

### Korak 3 — implementirati minimalni API
- Napraviti FastAPI ulaznu datoteku i modele.
- POST /oglasi: generira prijedlog i vraća ga korisniku; spremanje tek nakon korisnikove potvrde.
- Odvojiti generiranje od spremanja.
- GET /oglasi: vraća spremljene oglase.
- Zadržati postojeću tablicu i zapis; ne raditi destruktivnu migraciju.

**Gotovo kada:** endpointovi rade lokalno i imaju osnovne testove.

### Korak 4 — testovi i pokretanje
- Dodati requirements.txt s ovisnostima koje projekt stvarno koristi.
- Dodati testove za validaciju, spremanje/dohvat i greške parsera.
- Pokrenuti testove i zabilježiti točan rezultat.
- Dokumentirati naredbu za pokretanje u Termuxu.

### Korak 5 — jednostavno sučelje
- Mobilni obrazac za unos.
- Prikaz AI prijedloga u uređivim poljima.
- Jasna tipka za potvrdu/spremanje.
- Prikaz spremljenih oglasa i poruka o učitavanju/pogreškama.

### Korak 6 — mali pilot
- Testirati s 10–20 korisnika.
- Zabilježiti što ispravljaju, koliko vremena štede i žele li alat opet koristiti.
- Tek iz povratnih informacija odabrati sljedeću funkciju.

**Ne širiti sada opseg** na račune, plaćanja, poruke, fotografije, naprednu pretragu ili promovirane oglase.

## 5. Sigurnosne i Git smjernice

- Nikad ne objavljivati .env, API ključeve, tokene ili osobne podatke.
- Ako je API ključ zalijepljen u chat ili javni repozitorij, tretirati ga kao kompromitiranog i rotirati ga kod pružatelja usluge.
- SQLite baza je lokalni razvojni podatak; ne dodavati je u Git bez izričitog dogovora.
- Raditi male izmjene na zasebnom branchu i koristiti PR; ne spajati bez Harisove potvrde.
- Prije DB izmjena napraviti kopiju i objasniti posljedice.
- Ne tvrditi da je funkcija testirana ako test nije pokrenut.

## 6. Upute za novi chat / nastavak

Korisnik može napisati:

**„Provjeri GitHub AI-Oglasnik i nastavi od idućeg koraka.”**

Asistent treba:
1. Otvoriti https://github.com/hariskaraicic-blip/AI-oglasnik.
2. Pročitati ovaj dokument i aktualni README.md.
3. Provjeriti aktualni branch, commit, datoteke i status promjena.
4. Usporediti stvarno stanje s planom iz odjeljka 4.
5. Odabrati prvi nedovršeni korak i dati jednu sigurnu radnju/naredbu odjednom, zatim čekati rezultat.
6. Ne tražiti korisnika da ponavlja kontekst koji je već u repozitoriju.
7. Ne mijenjati bazu ni objavljivati tajne.

**Sljedeća planirana aktivnost prema dosad poznatom stanju:** Korak 1 — provjeriti aktualni GitHub i sigurnost datoteka, zatim pregledati i stabilizirati parser_agent.py.
