# Primera Part - Quantitat d’aigua als embassaments de les Conques Internes de Catalunya


Per fer aquesta pràctica ens basem en les dades [Dades Obertes Gencat - Quantitat d’aigua als embassaments de les Conques Internes de Catalunya](https://analisi.transparenciacatalunya.cat/Medi-Ambient/Quantitat-d-aigua-als-embassaments-de-les-Conques-/gn9e-3qhr/about_data)

## Aplicació WEB per a usuaris

La teva aplicació ha de mostrar aquestes pantalles als usuaris:

* Dashboard
  * Total volum d'aigua
  * % Percentatge volum embassat
  * Anar al llistat d'estacions.
* Estació
  * Estat actual de l'estació.
  * Taula de dades: anys / mesos amb % Percentatge volum embassat amb codis de colors.
* Estació i dia
* Estació i mes/any: Veure l'estat d'un mes
  concret de l'estació (mitjana dels dies)

## API

Tindrà dos end points:

* Llistat d'estacions.
* Dades estació: Retornarà les tres mètriques que apareixen al dataset corresponents a la data més nova, i la data.

## Model de dades

Pensa el model de dades i fes el gràfic M/E-IR. Pensa que podem afegir informació addicional a les dades, per exemple, informació sobre l'`estació`, com ara la capacitat total del seu volum o informació de com arribar-hi, etc.

## Entitats C#

Pensa quines són les entitats C# per emmagatzamar el model de dades. Treballarem amb EF, llavors has de crear els models per tal que `dbcontext` s'encarregui del CRUD de les dades. Per aquesta part de la pràctica no farem servir migracions, usarem el [EnsureCreated](https://learn.microsoft.com/en-us/ef/core/managing-schemas/ensure-created):

>The EnsureCreatedAsync and EnsureDeletedAsync methods provide a lightweight alternative to Migrations for managing the database schema. These methods are useful in scenarios when the data is transient and can be dropped when the schema changes. For example during prototyping, in tests, or for local caches.

## ETL

Procés ETL de càrrega de dades. A partir del dataset s'informen les dades a la base de dades.

## Procediment emmagatzemat per registrar dades d’embassaments

<details>

<summary>Enunciat</summary>

### Context

Les Conques Internes de Catalunya publiquen diàriament dades agregades sobre l’estat dels embassaments. Per a cada embassament es registra la informació següent:

- **Dia**: data en què s’ha pres la mesura (corresponent al dia anterior).
- **Estació**: embassament on s’ha pres la mesura.
- **Nivell absolut (msnm)**: nivell de l’aigua mesurat a l’embassament en metres sobre el nivell del mar.
- **Percentatge volum embassat (%)**: percentatge del volum d’aigua respecte de la capacitat màxima de l’embassament.
- **Volum embassat (hm³)**: volum d’aigua emmagatzemat a l’embassament en hectòmetres cúbics.

Les dades es registren en una base de dades que conté, entre altres, una taula d’**estacions (embassaments)** i una taula amb les **mesures diàries**.

Per evitar errors en la introducció de dades, es vol crear un **procediment emmagatzemat** que centralitzi la inserció de noves mesures i realitzi totes les validacions necessàries abans de guardar-les.

Dissenya un **procediment emmagatzemat** que permeti inserir una nova mesura d’un embassament a la base de dades.

El procediment ha de rebre com a paràmetres:

- la data de la mesura
- la identificació de l’estació (embassament)
- el nivell absolut
- el percentatge de volum embassat
- el volum embassat

Abans d’inserir la nova fila, el procediment ha de realitzar les validacions següents:

### Validacions d’integritat

1. **Existència de l’estació**
   - S’ha de comprovar que l’estació indicada existeix a la taula d’estacions.

2. **Duplicats**
   - No es poden inserir dues mesures per al **mateix embassament i el mateix dia**.

3. **Data vàlida**
   - La data de la mesura no pot ser futura.
   - La data no pot ser anterior a un límit raonable definit pel sistema (per exemple, abans de l’inici del registre històric).

### Validacions de rang

4. **Percentatge**
   - El percentatge de volum embassat ha d’estar entre **0 i 100**.

5. **Volum**
   - El volum embassat ha de ser **positiu o zero**.

6. **Nivell absolut**
   - El nivell absolut ha de ser un valor positiu.

### Validacions de coherència amb dades anteriors

El sistema ha de comprovar l’última mesura disponible per al mateix embassament.

7. **Canvi excessiu en menys d’un mes**
   - Si l’última mesura disponible és de **menys d’un mes abans**, la variació del volum embassat no pot superar el **50%** respecte del valor anterior.

8. **Canvi excessiu en menys de tres mesos**
   - Si l’última mesura disponible és de **menys de tres mesos abans**, la variació del volum embassat no pot superar el **75%**.

9. **Control d’incoherències**
   - Si el percentatge i el volum embassat no són coherents amb la capacitat màxima de l’embassament, el sistema ha de rebutjar la inserció.

### Resultat del procediment

El procediment ha de:

- inserir la nova mesura si totes les validacions són correctes
- retornar un **missatge d’error clar** si alguna validació falla
- evitar que s’insereixin dades inconsistents a la base de dades.

</details>

## Desplegament

La base de dades ha d'estar al núvol (per exemple a AWS). L'aplicació també.

## Documentació

Cal fer  un document tècnic, explicant el funcionament intern de l'aplicatiu. Es demana mostrar tots els esquemes de la BDD i les funcionalitats programades documentades.

## Sistemes empresarials

Instal·la Oddo mitjançant docker:

Base de dades:

### 1. Iniciar PostgreSQL

Odoo necessita una base de dades :contentReference[oaicite:1]{index=1}:

```bash
docker run -d \
  -e POSTGRES_USER=odoo \
  -e POSTGRES_PASSWORD=odoo \
  -e POSTGRES_DB=postgres \
  --name db \
  postgres:15
```

Iniciar Odoo

```bash
docker run -d \
  -p 8069:8069 \
  --name odoo \
  --link db:db \
  odoo
```

Accedir a Odoo

```
http://localhost:8069
```

Un cop engegat, prepara una factura per facturar els serveis que has fet al projecte al client Cendrassos.

## Com organitzo el meu codi?

### Primera part

Molt segurament, la millor estratègia és començar per la càrrega de dades. Hauries de fer aquestes passes:
* Crees un projecte `console` (ex: `dotnet new console -o Importador`)
* Crees els models que serviran per persistir les dades.
* Crees el `dbcontext`
* Busques una llibreria per llegir `csv`
* Per cada línia de `csv`:
   * Busques l'embassament, si no hi és a la bd el crees.
   * Busques la dada a insertar, si no hi és a la bd la crees.

### Segona part

Per a fer la resta d'aplicacions: API i MVC necessitaràs els models que has fet servir abans. L'estragegia seria aquesta:
* Crea un nou projecte `classlib` (ex: `dotnet new classlib -o EmbassamentDB` ) i mou els models i el dbcontex a aquest nou projecte (recorda canviar namespace de les classes al namespace del nou projecte)
* Al projecte console posa una referència a aquest nou projecte (ex: `dotnet add reference ../EmbassamentsDB`)
* Comprova que tot sergueix funcionant (esborra la base de dades, torna a fer la càrrega)

A partir d'ara, ja tens els models i el dbcontex en un projecte que podràs usar des dels nous projectes.

Recorda crear una solution i posar-hi a dins els dos projectes:

```bash
dotnet new sln
dotnet sln add Importador
dotnet sln add EmbassamentsDB
```

> [!IMPORTANT] 
> Recorda posar cada projecte en una carpeta (directori) diferent i el solutiona a l'arrel. No barregis solution amb projecte.

> [!TIP]
> No et faci por tornar a començar o refer-ho tot.


### Tercera part

Pots procedir a fer les apis:

* Crea el projecte (ex: `dotnet new webapi -o EmbassamentAPI`)
* Afegeix-lo al solution (ex: `dotnet sln add EmbassamentAPI` )
* A la API posa la referència al projecte dbcontext (ex: `cd EmbassamentAPI; dotnet add reference ../EmbassamentDB` )
* Pensa les consultes Linq per obtenir les dades que et demanen.
* Fes les proves de la API i documenta-les.

### Quarta Part

Pots fer el projecte MVC. Recorda que els models de la base de dades ja els tens creats.

* Crea el projecte (ex: `dotnet new mvc -o EmbassamentMVC`)
* Afegeix-lo al solution (ex: `dotnet sln add EmbassamentMVC` )
* Al MVC posa la referència al projecte dbcontext (ex: `cd EmbassamentMVC; dotnet add reference ../EmbassamentDB` )
* Crea els `ModelView`. Cada ModelView és una classe que conté totes les dades que vols mostrar.
* Al controlador, fes les consultes Linq necessaries per poder posar les dades dins el ModelView
* Crida la vista passant com a paràmetre el model view.
* Al template, accedeix al modelview per renderitzar la pàgina HTML que s'enviarà al navegador de l'usuari.
* Fes això a cada controlador.

### Cinquena part

Prova a fusionar els projectes MVC i API. Per això, ens endurem les API al MVC.

#### Migrar una Minimal API a un projecte MVC (.NET Core)

Objectiu: tenir **MVC + API** dins del mateix projecte, de la manera més simple possible.

#### Situació inicial

Tens:

- Una app MVC:

```text
EmbassamentMVC
```

- Una app WebAPI minimalista:

```text
EmbassamentAPI
```

La WebAPI actual té endpoints tipus:

```csharp
app.MapGet("/embassaments", () => { ... });
```

---

#### Estratègia recomanada (la més simple)

NO fusionis dos projectes.

La manera més fàcil és:

1. Agafar els endpoints de la Minimal API
2. Copiar-los dins el `Program.cs` del projecte MVC
3. Posar-los sota `/api/...`

I ja està.

---

#### Pas 1 — Obrir el Program.cs del MVC

Edita:

```text
EmbassamentMVC/Program.cs
```

---

#### Pas 2 — Afegir OpenAPI (opcional)

Si vols Swagger/OpenAPI:

Afegeix:

```csharp
builder.Services.AddOpenApi();
```

Exemple:

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllersWithViews();

builder.Services.AddOpenApi();
```

---

#### Pas 3 — Activar OpenAPI en Development

Afegeix:

```csharp
if (app.Environment.IsDevelopment())
{
    app.MapOpenApi();
}
```

---

#### Pas 4 — Copiar els endpoints Minimal API

Copia els teus `MapGet`, `MapPost`, etc.

app.MapGet("/api/embassaments", () =>
{
    ...
});
```

IMPORTANT:

Posa sempre `/api/...`

Correcte:

```csharp
/api/embassaments
```

Incorrecte:

```csharp
/embassaments
```

Això evita conflictes amb MVC.


#### Estructura recomanada per aplicacions més grans

Quan el projecte creix, no és bona idea deixar totes les APIs dins `Program.cs`, perquè acaba sent difícil de mantenir.

L'estructura habitual és separar:

- `Controllers/` → MVC amb vistes
- `Endpoints/` → Minimal APIs
- `Services/` → lògica de negoci (pot estar en una classlib)
- `Models/` → models i DTOs
- `Data/` → accés a base de dades (pot estar en una classlib)

Exemple:

```text
EmbassamentMVC/
│
├── Controllers/
│   └── HomeController.cs
├── Endpoints/
│   ├── WeatherEndpoints.cs
│   └── EmbassamentEndpoints.cs
├── Services/
│   └── EmbassamentService.cs // millor a la seva pròpia classlib
├── Models/
│   └── Embassament.cs // millor a la seva pròpia classlib
├── Data/
│   └── AppDbContext.cs // millor a la seva pròpia classlib
└── Program.cs
```

El `Program.cs` queda molt net:

```csharp
app.MapEmbassamentEndpoints();
```

I cada fitxer `Endpoints/*.cs` defineix les seves rutes.

Aquesta estructura és molt més mantenible quan tens moltes APIs, autenticació, base de dades o equips de desenvolupament més grans.