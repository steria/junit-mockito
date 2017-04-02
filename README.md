# Introduksjon til JUnit og Mockito

Denne introduksjonen forutsetter at Maven 3 er installert (https://maven.apache.org/download.cgi)

## Del 1: Oppsett
1. Kjør `mvn test` i rotmappa til prosjektet
2. Legg til JUnit som avhengighet i `pom.xml`:

```
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.12</version>
  <scope>test</scope>
</dependency>
```

3. Opprett en testpakke `com.soprasteria.kalkulator` i src/test/java/
4. Opprett en testklasse `KalkulatorTest.java` i testpakken
5. Kjør `mvn test` igjen, og sammenlign utskriften med første kjøring

## Del 2: Første test
1. Lag en metode i `KalkulatorTest.java` med følgende signatur
```
public void skal_få_4_når_1_og_3_adderes()
```
2. Kjør `mvn test` og se på resultatet
3. Legg til annotasjonen `@Test` over metoden for å markere at det er en test
4. Kjør `mvn test` og se på resultatet
5. Gjør et kall til `Kalkulator#adder` i testmetoden, og bruk `Assert.assertEquals` til å sjekke at resultatet blir som forventet.
6. Kjør `mvn test` og se på resultatet
7. Fiks koden i `Kalkulator#add`!
8. Kjør `mvn test` og se på resultatet

### Oppgave:
9. Test `Kalkulator#subtraher` og `Kalkulator#multipliser`
    1. Skriv nye testmetoder i `KalkulatorTest.java`. Husk `@Test`-annotasjonen
    2. Kjør `mvn test` og verifiser at testene feiler
    3. Fiks koden i `Kalkulator`
    4. Kjør `mvn test` og verifiser at testene kjører grønt!

## Del 3: Bedre assertions
1. Legg til AssertJ som avhengighet i `pom.xml`, like under `junit`:
```
<dependency>
    <groupId>org.assertj</groupId>
    <artifactId>assertj-core</artifactId>
    <version>3.6.2</version>
    <scope>test</scope>
</dependency>
```
2. Skriv om testmetoden `KalkulatorTest#skal_få_4_når_1_og_3_adderes` til å bruke AssertJ i stedet for junit.core.Assert
    1. Fjern `Assert.assertEquals...`
    2. Kall `Assertions.assertThat(...).isEqualTo(...)` i stedet
    3. Legg til en statisk import av `Assertions.assertThat` for bedre lesbarhet
    4. Kjør testen og se at den fremdeles er grønn

### Oppgave:
4. Skriv om resten av testen til å bruke AssertJ
    1. Skriv om testmetodene for `Kalkulator#subtraher` og `Kalkulator#multipliser`
    2. Kjør testene og se at de fremdeles er grønne

## Del 4: Testing med exceptions
1. Opprett en metode i `Kalkulator` med følgende signatur som returnerer 0:
```
public int divider(int dividend, int divisor) {}
```
2. Opprett en testmetode i `KalkulatorTest` med følgende signatur:
```
public void skal_få_2_når_8_divideres_med_4()
```
3. Implementer testen, kjør `mvn test` og se at den feiler
4. Implementer metoden `Kalkulator#divider`, kjør `mvn test` og se at testen går grønt
5. Opprett en testmetode i `KalkulatorTest`med følgende signatur:
```
public void skal_få_IllegalArgumentException_når_divisor_er_0()
```
6. Bruk parameteret `exåected` til `@Test`-annotasjonen til å si at vi forventer enn IllegalArgumentException
7. Implementer testmetoden og gjør et kall til `Kalkulator#divider` med 0 som divisor
8. Kjør testen og se at den feiler
9. Implementer en sjekk på divisorens verdi i `Kalkulator#divider` der en exception kastes dersom den er 0
10. Kjør testen og se at den går grønt

## Del 5: Forberedelser og etterarbeid
1. Opprett en testklasse FileHandlerTest.java i src/test/java
2. Lag en testmetode med følgende signatur
```
public void should_read_first_line_from_file() {}
```
3. Implementer metoden:
    1. Opprett en fil `tempfile.txt` med en linje tekst (f. eks. "Lisa gikk til skolen"). Tips: Du kan opprette en fil ved å skrive `new File("filnavn")`.
    2. Gjør et kall til `FileHandler#readFirstLineFromFile` for å hente første linje
    3. Bruk assertions til å sjekke om returverdien er som forventet
4. Kjør testen!
5. Fiks koden i `FileHandler#readFirstLineFromFile`
6. Kjør testen en gang til! Hva ble resultatet?
7. Lag en testmetode til med følgende signatur. Husk annotasjonen!
```
public void should_read_second_line_from_file() {}
```
8. Implementer testen på tilsvarende måte som sist. Husk å legge til to linjer med tekst i filen, og bruk `FileHandler#readFirstLineFromFile` for å lese den andre linjen.
9. Kjør begge testene!
10. Opprett en metode med følgende signatur i `FileHandlerTest`:
```
public void setUp() {}
```
11. Legg til annotasjonen `@Before` over metoden
12. Flytt koden som oppretter `tempFile.txt` inn i den nye metoden, og fjern den fra begge testmetodene
13. Kjør begge testene!
14. Se i rotmappen til prosjektet. Ser du noe som ikke burde vært der?
15. Opprett en metode med følgende signatur i `FileHandlerTest`:
```
public void tearDown() {}
```
16. Legg til annotasjonen `@After` over metoden
17. Implementer kode til å slette den midlertidige filen i `tearDown()`
18. Kjør begge testene! Hvordan ser rotmappa til prosjektet ut nå?
