# Mini Projecte DAW 2025-26

[Obtenir el repositori de GIT](https://classroom.github.com/a/L0BqADCy)

## Què i perquè el MiniProjecte DAW

L'objectiu és que l'alumnat es capaciti per aprofitar l'EE.

El currículum DAW actual preveu 515h d'EE (Estada en Empresa). Per poder finalitzar el cicle en 2 anys l'alumne ha d'avançar l'inici d'EE i començar a finals de primer o començaments de segon curs, quan encara no s'han impartit conceptes claus necessaris a l'EE. El MiniProjecte DAW avança aquests continguts del currículum.

## Calendari

Del 4 al 22 de maig

## Quins mòduls professionals contempla

* BD - 0484 - Base de Dades
* LM - 0373 - Llenguatges de marques i sistemes de gestió d’informació
* PR - 0485 - Programació
* ED - 0487 - Entorns de Desenvolupament
* SI - 0483 - Sistemes Informàtics

## Enunciats

Tria una d'aquestes pràctiques o proposa tu la teva. Per a cada enunciat hi ha dos nivells, el bàsic i l'avançat. El bàsic és obligatori, de l'avançat mira d'arribar fins on puguis.

### embassaments de les Conques Internes de Catalunya

* [Pràctica bàsica](./enunciat-embassaments-01.md)
* [Pràctica avançada](./enunciat-embassaments-02.md)

## Introducció a .NET Core MVC

**.NET Core MVC** (actualment conegut com a **ASP.NET Core MVC**) és un framework de Microsoft per construir aplicacions web modernes seguint el patró **Model-View-Controller (MVC)**. Està dissenyat per ser multiplataforma (Windows, Linux, macOS), altament eficient i escalable.

### 🧱 Patró MVC

- **Model**: Representa les dades i la lògica de negoci.
- **View**: És la interfície d’usuari (HTML, CSS, Razor).
- **Controller**: Gestiona les peticions de l’usuari, processa dades i retorna respostes.

### ⚙️ Característiques principals

- Multiplataforma
- Injecció de dependències integrada
- Routing flexible (URL → accions)
- Integració amb Razor per generar HTML dinàmic
- Alt rendiment i modularitat

### 🔄 Flux bàsic

1. L’usuari fa una petició HTTP.
2. El sistema de routing la dirigeix a un **Controller**.
3. El controller interactua amb el **Model**.
4. Es retorna una **View** amb les dades processades.

### 📦 Exemple simple

```csharp
public class HomeController : Controller
{
    public IActionResult Index()
    {
        return View();
    }
}
```

### Doc

* [Patrón de MVC de ASP.NET](https://dotnet.microsoft.com/es-es/apps/aspnet/mvc)
* [Scaffolding](./scaffolding.md)



## Conceptes clau

| Concepte | Nivell | Descripció | Mòduls |
|---|:---:|---|---|
| Web API | Bàsic | Servei web per publicar dades en llenguatge de marques | PR LM |
| Patró Model-View-Controller | Bàsic | Distribució del codi en projectes web | PR LM |
| Ús d'ORM | Bàsic | Accés a la base de dades des de la capa d'abstracció d'objectes | PR BD |
| UI | Bàsic | HTML bàsic | LM |
| Disseny de classes | Bàsic | Disseny adequat de les classes i diagrama de classes | PR ED |
| Desplegament Docker | Bàsic | Desplegar aplicació amb `docker-compose` | SI ED|
| Testos unitaris | Avançat | Testar el codi per funcionalitats independents | ED PR |
| UI Forms | Avançat | Formularis HTML | LM |
| Patró Post-Get-Redirect | Avançat | Gestionar formularis HTML | LM PR |
| Desplegament AWS | Avançat | Desplegar aplicació al núvol | ED SI |
| Còpies de seguretat | Bàsic | Realitzar còpies de la base de dades i el sistema | SI |

## Avaluació

Resultats d'aprenentatge i criteris d'avaluació per Mòdul Professional i RA.

### 0484 - Base de Dades

#### RAs del mòdul professional:
* RA1. Reconeix els elements de les bases de dades analitzant-ne les funcions i valorant la utilitat dels sistemes gestors.
* RA2. Crea bases de dades definint-ne l'estructura i les característiques dels elements segons el model relacional.
* RA3. Consulta la informació emmagatzemada en una base de dades fent servir assistents,
* RA4. Modifica la informació emmagatzemada a la base de dades utilitzant assistents, eines gràfiques i el llenguatge de manipulació de * dades.
* RA5. Desenvolupa procediments emmagatzemats avaluant i utilitzant les sentències del llenguatge incorporat al sistema gestor de bases de * dades.
* RA6. Dissenya models relacionals normalitzats interpretant diagrames entitat/relació.
* RA7. Gestiona la informació emmagatzemada en bases de dades no relacionals, avaluant i utilitzant les possibilitats que proporciona el sistema gestor.

#### Criteris d'avaluació i afectació a la nota

* S'avaluaran els entregables que apareixen als enunciats.
* 10% de la nota dels RAs 2, 3, 4, 6.

### 0373 - Llenguatges de marques i sistemes de gestió d’informació

#### RAs del mòdul professional

* RA1. Reconeix les característiques de llenguatges de marques analitzant i interpretant fragments de codi.
* RA2. Utilitza llenguatges de marques per a la transmissió i presentació de informació a través del web analitzant l'estructura dels * documents i identificant-ne els elements.
* RA3. Accedeix i manipula documents web utilitzant llenguatges de guions de client.
* RA4. Estableix mecanismes de validació de documents per a l'intercanvi d'informació utilitzant mètodes per definir-ne la sintaxi i * l'estructura.
* RA5. Realitza conversions sobre documents per a l'intercanvi de informació utilitzant tècniques, llenguatges i eines de processament.
* RA6. Gestiona la informació en formats d'intercanvi de dades analitzant i utilitzant tecnologies d'emmagatzematge i llenguatges de * consulta.
* RA7. Efectua operacions amb sistemes empresarials de gestió d'informació realitzant tasques d'importació,

#### Criteris d'avaluació i afectació a la nota

* S'havaluaran els entregables que apareixen als enunciats.
* 10% de la nota dels RAs 1, 2, 6, 7.

### 0485 - Programació

- RA1. Reconeix l'estructura d'un programa informàtic, identificant i relacionant els elements propis del llenguatge de programació utilitzat.
- RA2. Escriu i prova programes senzills, reconeixent i aplicant els fonaments de la programació orientada a objectes
- RA3. Escriu i depura codi, analitzant i utilitzant les estructures de control del llenguatge.
- RA4. Desenvolupa programes organitzats en classes analitzant i aplicant els principis de la programació orientada a objectes.
- RA5. Realitza operacions d'entrada i sortida d'informació, utilitzant procediments específics del llenguatge i llibreries de classes
- RA6. Escriu programes que manipulin informació seleccionant i utilitzant tipus avançats de dades.
- RA7. Desenvolupa programes aplicant característiques avançades dels llenguatges orientats a objectes i de l'entorn de programació
- RA8. Utilitza bases de dades orientades a objectes, analitzant-ne les característiques i aplicant tècniques per mantenir la persistència de la informació.
- RA9. Gestiona informació emmagatzemada en bases de dades mantenint la integritat i consistència de les dades

#### Criteris d'avaluació i afectació a la nota

- S'avaluarà el que entreguin els alumnes que tingui relació amb el mòdul
- Les notes afecten tots els RA i representarà el 10% de la nota del Level 3.

### 0487 - Entorns de Desenvolupament

- RA1. Reconeix els elements i les eines que intervenen en el desenvolupament d'un programa informàtic, analitzant-ne les característiques i les fases en què actuen fins a arribar a la posada en funcionament.
- RA2. Avalua entorns integrats de desenvolupament analitzant-ne les característiques per editar codi font i generar executables.
- RA3. Verifica el funcionament de programes dissenyant i realitzant proves.
- RA4. Optimitza codi utilitzant les eines disponibles a l'entorn de desenvolupament
- RA5. Genera diagrames de classes valorant-ne la importància en el desenvolupament d'aplicacions i emprant eines específiques.
- RA6. Genera diagrames de comportament valorant-ne la importància en el desenvolupament d'aplicacions i emprant eines específiques.

#### Criteris d'avaluació i afectació a la nota

- S'avaluarà el que entreguin els alumnes que tingui relació amb el mòdul
- Les notes afecten tots els RA i representarà el 10% de la nota del Level 3.

### 0483 - Sistemes Informàtics

* RA2. Instal·la sistemes operatius planificant el procés i interpretant documentació tècnica.
* RA7. Elabora documentació valorant i utilitzant aplicacions informàtiques de propòsit general.
