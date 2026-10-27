# NEZĀĻU ARĒNA — LAUKA IZDEVUMS (REDESIGN)

Latviska, lokāli darbināma mācību aplikācija ar pieaugušu nezāļu fotogrāfijām, 50 augu sarakstu, bioloģiskās piederības pārbaudi un progresu pārlūkprogrammas LocalStorage.

## Palaišana

Nepieciešams **Node.js 20.19+ vai 22+**.

```bash
npm install
npm run dev
```

Atver adresi, ko parāda Vite (parasti **http://localhost:5173**).

Automātiskie testi: `npm test`. Produkcijas versija: `npm run build`.

## JAUNS VIZUĀLAIS VIRZIENS: LAUKA ŽURNĀLS × INDIE SPĒLE

Šajā versijā pilnībā mainīts dizains — gaišs fakturēta papīra fons, izteikta grāmatu tipogrāfija, tumši olīvzaļa tinta, oranži grafiskie akcenti, asas malas, maršrutu/misiju kartītes un uz fotografēšanu orientēts atpazīšanas ekrāns.

Nav ārēju fontu vai jaunu fotoatkarību. Saglabāti 50 augi, klasifikācija, spēles režīmi, XP, statistika un LocalStorage progresa formāts.

**Dizaina izmaiņas:** `src/editorial.css` — pārskatāmi, atsevišķā failā. `src/styles.css` — vēsturiskais stilu pamats. `src/main.tsx` ielādē abus, jauno failu pēdējo. `src/App.tsx` un `src/Arcade.tsx` — jaunais virsrakstu un navigācijas noformējums.

Lai viegli mainītu galvenās krāsas, labo `:root` mainīgos `src/editorial.css` sākumā.

## NEZĀĻU ARĒNA (Gamer Mode)

Sākuma lapā spied **Sākt ekspedīciju** vai augšējā navigācijā **Spēlēt**.

- **5 secīgi atslēdzami līmeņi:** Pirmais reids → Lauka medības → Sakņu pazeme → Haosa zona → Botānikas BOSS.
- **3–5 dzīvības** atkarībā no posma. Par kļūdu atņem vienu; pareizā atbilde un morfoloģiskā pazīme tiek paskaidrota.
- **XP un līmeņi:** 20 XP par pareizu atbildes daļu; combo bonuss pēc 3 pareiziem augiem pēc kārtas; +5 XP par atbildi pirmajās 8 sekundēs. Ik pēc 250 XP — jauns līmenis.
- **Boss cīņa:** 10 dažādi augi, divi jautājumi (nosaukums + bioloģiskā piederība), 20 iespējamie punkti, jāiegūst vismaz 14 un jāsaglabā dzīvība.
- **Zvaigznes:** 1–3 zvaigznes par uzvarētām misijām, atkarībā no precizitātes.
- **Dienas misija:** 5 augu tests, pirmā sekmīgā dienas misija dod +100 XP (tikai vienreiz lokālajā dienā).
- **Sasniegumi:** pirmā pareizā atbilde, combo, uzvaras, 500 XP, boss.
- **Mācību integrācija:** visas reida atbildes tiek reģistrētas esošajā statistikā un kļūdu atkārtošanā. Trūkstošu foto iespējams izlaist bez dzīvības zaudēšanas.
- **LocalStorage:** saglabājas līmeņi, zvaigznes, XP, misiju progress, sasniegumi un ikdienas bonuss, bez konta vai servera. Reidu var pārspēlēt.

**Uzmanību:** paši fotoattēli joprojām prasa interneta savienojumu, un tie nav visi manuāli vizuāli auditēti. Ja fotoattēlā nav skaidri redzams pareizais augs, izmanto `Attēlu pārbaude`.

## Mācību režīmi

- **Atpazīsti nezāli** — jautājumi par nosaukumu no fotogrāfijas.
- **Bioloģiskā piederība** — attēls un auga nosaukums, atbildēs īsmūža/daudzgadīgo u. c. grupas un apakšgrupas.
- **Kombinētais eksāmens** — visi 50 augi vienreiz, 100 punkti.
- **Ātrais tests** — 10 augi.
- **Mācīties** — augu fotogrāfijas ar nosaukuma atklāšanu.
- **Manas kļūdas** — grūtākos augus liek sākumā, nepareizās atbildes saglabā.
- **Statistika** — individuāls progress 50 augiem un rezultātu vēsture.
- **Attēlu pārbaude** — katra fotoattēla vizuāla kvalitātes kontrole.

## Datu izcelsme un drošums

- Visu 50 augu **kārtība, latviskie nosaukumi un klasifikācija** pārrakstīta no PDF `4__Nezāļu saraksts.pdf` (saīsinātā programma).
- Zinātniskie nosaukumi, kurus satur `Nezalu seklu kolekcija.pdf`, izmantoti kā otrs avots. Papildu taksoniem lietoti VAAD un Latvijas daba augu apraksti. Akļi, lāčauzas un vijas uzskaitītas kā **ģintis**, nevis patvaļīgi izvēlētas sugas.
- **Sēklu fotoattēli nav izmantoti.** Kur ir pārbaudīts ārējs auga fotoattēls, tas ievietots `src/data/weeds.ts` laukā `imageUrl`.
- Pārējo fotoattēliem klienta pusē, bez backend servera, tiek pieprasītas **iNaturalist** precīzi zinātniskajam nosaukumam atbilstošā taksona fotogrāfijas (`https://api.inaturalist.org/v1/taxa/autocomplete`), alternatīvi pārbaudot precīza nosaukuma Wikipedia taksona attēlu. Ja precīzas atbilstības nav, lietotne **neievieto nejaušu attēlu** un skaidri parāda kļūdu.
- Tāpēc **attēliem nepieciešams interneta pieslēgums**, kaut pati aplikācija darbojas localhost bez backend. Fotogrāfijas URL tiek ievietoti pārlūkprogrammas LocalStorage kešatmiņā. Attēlu failus nav jālejupielādē manuāli.
- Taksona fotoattēls var būt ziedoša auga tuvplāns, nevis pilns augums. **Visu 50 fotoattēlu manuāla morfoloģiskā pārbaude nav automātiski apliecināta**. Sadaļā “Attēlu pārbaude” ir rīki manuālai pārbaudei. Neizmantojam neprecīzu fotoattēlu kā aizvietotāju.
- Fotogrāfiju avoti / autori (ja to nodrošina API) tiek norādīti attēla apakšmalā pēc atbildes atklāšanas vai mācību režīmā.

## Koda struktūra

- `src/data/weeds.ts` — 50 augi, nosaukumi un grupas.
- `src/Arcade.tsx` — kampaņa, cīņas, HUD, XP, dzīvības un boss.
- `src/lib/arcade.ts` — pārbaudāma līmeņu, combo, misiju un dienas bonusa loģika.
- `tests/arcade.test.ts` — spēles punktu, līmeņu un misiju automātiskie testi.
- `src/lib/photos.ts` — precīzo taksonu ārējie fotoattēli, kešs un kļūdu apstrāde.
- `src/lib/quiz.ts` — testu ģenerators un vērtēšana.
- `src/lib/storage.ts` — progresa un vēstures saglabāšana.
- `src/App.tsx` — visas lapas / spēles režīmi.
- `src/styles.css` — sākotnējā stilu bāze un Tailwind CSS.
- `src/editorial.css` — jaunā vizuālā sistēma, ieskaitot telefonus un planšetes.
- `tests/quiz.test.ts` — automātiskie testi.

## Piezīme par zinātniskajiem nosaukumiem

Dažiem augiem nomenklatūrā sastopami sinonīmi (piemēram, *Elytrigia repens / Elymus repens*, *Polygonum lapathifolium / Persicaria lapathifolia*, *Matricaria perforata / Tripleurospermum inodorum*). Attēlu meklēšanā lietoti mūsdienīgi taxonQuery varianti.

## Konfidencialitāte

Rezultāti paliek tavā pārlūkprogrammā. Nav kontu, datubāzes, savu datu nosūtīšanas vai reģistrācijas. Interneta pieprasījumi vajadzīgi tikai botānisko fotoattēlu ielādei no publiskajiem avotiem.
