## Scaffolding a ASP.NET Core MVC

### 🧩 Què és l’scaffolding?

L’**scaffolding** és una tècnica que permet generar automàticament codi base (controladors, vistes, formularis, etc.) a partir d’un model. En el context de **ASP.NET Core MVC**, serveix per crear ràpidament funcionalitats CRUD (Create, Read, Update, Delete) sense haver d’escriure-ho tot manualment.

Això et dona una estructura funcional immediata sobre la qual pots treballar.

---

### 🤔 Per què és útil?

- Estalvia temps en tasques repetitives
- Proporciona una estructura estàndard
- Ajuda a entendre com funciona MVC en la pràctica
- Ideal per prototips o primers desenvolupaments

---

### ⚠️ No tinguis por de modificar-lo

El codi generat per scaffolding **no és sagrat**. És només un punt de partida.

De fet, és recomanable modificar-lo perquè:

- Sovint genera controladors massa grans
- Accedeix directament al `DbContext` (acoblament fort)
- No aplica patrons més avançats (serveis, repositoris, etc.)

👉 Si el deixes tal qual en projectes reals, acabaràs amb codi difícil de mantenir.

👉 Si l’adaptes, es converteix en una base molt útil.

---

### 🛠️ Comandes bàsiques

#### Instal·lar l’eina

'''bash
dotnet tool install -g dotnet-aspnet-codegenerator
'''

#### Afegir el paquet necessari

'''bash
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
'''

---

### 📦 Crear un controlador buit

'''bash
dotnet aspnet-codegenerator controller -name ProductController -outDir Controllers
'''

---

### 🔄 Crear controlador amb CRUD i vistes

'''bash
dotnet aspnet-codegenerator controller \
  -name ProductController \
  -m Product \
  -dc AppDbContext \
  --relativeFolderPath Controllers \
  --useDefaultLayout \
  --referenceScriptLibraries
'''

---

### 🎨 Crear una vista

'''bash
dotnet aspnet-codegenerator view Index List -m Product
'''

---

### 🧠 Resum

- L’scaffolding genera codi automàticament
- És una eina per anar ràpid, no una solució final
- Cal revisar i adaptar el codi generat
- És especialment útil per aprendre i prototipar

---