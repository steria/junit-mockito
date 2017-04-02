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
public void skal_få_4_når_1_og_3_adderes() {}
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
    1. Skriv nye testmetoder i `KalkulatorTest.java`
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