# Dealership Manager — Curso de Ruby on Rails

Proyecto guiado para aprender desarrollo web con **Ruby on Rails** desde cero.

Vamos a construir, poco a poco, un **gestor de concesionarios**: una aplicación web que
lleva el inventario de coches, registra las ventas y calcula las comisiones que se lleva
cada comercial según el precio del coche vendido.

No hace falta saber programar para empezar. Este README te lleva de la mano desde
"tengo un ordenador con Windows" hasta "tengo la aplicación funcionando en mi navegador".

> **Convenio del curso:** las explicaciones están en español, pero **todo el código,
> los nombres de clases, los comentarios y los mensajes de commit se escriben en inglés**.
> Es el estándar en la industria y conviene acostumbrarse desde el primer día.

---

## Índice

1. [Cómo funciona el curso](#1-cómo-funciona-el-curso)
2. [Qué vas a necesitar](#2-qué-vas-a-necesitar)
3. [Montar la máquina virtual con Ubuntu](#3-montar-la-máquina-virtual-con-ubuntu)
4. [Primeros pasos en Ubuntu: la terminal](#4-primeros-pasos-en-ubuntu-la-terminal)
5. [Instalar las herramientas de desarrollo](#5-instalar-las-herramientas-de-desarrollo)
6. [Crear el proyecto Rails](#6-crear-el-proyecto-rails)
7. [Configurar Git y GitHub](#7-configurar-git-y-github)
8. [El enunciado: qué vamos a construir](#8-el-enunciado-qué-vamos-a-construir)
9. [Roadmap de hitos](#9-roadmap-de-hitos)
10. [Cómo trabajamos: TDD y commits](#10-cómo-trabajamos-tdd-y-commits)
11. [Chuleta de comandos](#11-chuleta-de-comandos)
12. [Problemas frecuentes](#12-problemas-frecuentes)
13. [Anexo A: alternativa con WSL2](#anexo-a-alternativa-con-wsl2)
14. [Anexo B: glosario](#anexo-b-glosario)

---

## 1. Cómo funciona el curso

El curso está dividido en **hitos**. Cada hito:

- añade una funcionalidad nueva a la aplicación,
- introduce dos o tres conceptos nuevos de Rails,
- y termina con algo que puedes abrir en el navegador y enseñar.

No saltes hitos. Cada uno se apoya en el anterior, y la gracia está en ver cómo un
proyecto pequeño se va complicando igual que se complican los proyectos de verdad.

Cada hito tiene:

| Apartado | Qué significa |
|---|---|
| **Objetivo** | Qué debe hacer la aplicación al terminar el hito |
| **Conceptos nuevos** | Lo que vas a aprender por el camino |
| **Criterios de aceptación** | La lista de comprobación: si todo pasa, el hito está cerrado |

---

## 2. Qué vas a necesitar

- Un ordenador con **Windows 10 u 11** (si tienes Mac o Linux, avisa y adaptamos las instrucciones).
- **Al menos 8 GB de RAM** (16 GB es cómodo). La máquina virtual se va a comer 4 GB.
- **30 GB de disco libre.**
- Conexión a internet decente: la primera instalación descarga bastante.
- Paciencia el primer día. Montar el entorno es la parte más aburrida y la que menos
  se parece a programar. Es normal que algo falle; para eso está el apartado
  [Problemas frecuentes](#12-problemas-frecuentes).

### ¿Por qué una máquina virtual?

Una **máquina virtual (VM)** es un ordenador simulado que corre dentro de tu ordenador.
Le instalamos Ubuntu (una distribución de Linux) y trabajamos ahí dentro.

Lo hacemos por tres razones:

1. **Los servidores del mundo real corren Linux.** Cuanto antes te familiarices, mejor.
2. **Ruby y Rails funcionan mucho mejor en Linux** que en Windows. Menos sorpresas.
3. **Si la lías, no pasa nada.** Borras la VM, creas otra y tu Windows sigue intacto.

Versiones que vamos a usar (fijadas para que todos tengamos lo mismo):

| Herramienta | Versión |
|---|---|
| Ubuntu | 26.04 LTS |
| Ruby | 3.4.x |
| Rails | 8.1.x |
| PostgreSQL | la que traiga Ubuntu por defecto (17 o superior) |
| VirtualBox | 7.x |

---

## 3. Montar la máquina virtual con Ubuntu

### 3.1. Descargar lo necesario

Descarga estas dos cosas **antes de empezar** (tardan un rato):

1. **VirtualBox** — el programa que crea máquinas virtuales.
   👉 https://www.virtualbox.org/wiki/Downloads → *Windows hosts*
2. **La imagen de Ubuntu** — un archivo `.iso`, que es el "CD de instalación".
   👉 https://ubuntu.com/download/desktop → *Ubuntu 26.04 LTS*

El `.iso` ocupa unos 5-6 GB. Déjalo descargando y sigue leyendo.

### 3.2. Instalar VirtualBox

Ejecuta el instalador y dale a *Siguiente* en todo. Windows te avisará de que va a
instalar controladores de red: acepta. En algún momento la red se cortará un segundo,
es normal.

> ⚠️ Si el instalador se queja de **Hyper-V** o de que la virtualización está desactivada,
> ve al apartado [Problemas frecuentes](#12-problemas-frecuentes) antes de continuar.

### 3.3. Crear la máquina virtual

Abre VirtualBox y pulsa **Nueva**.

**Pantalla 1 — Nombre y sistema operativo**

| Campo | Valor |
|---|---|
| Nombre | `rails-dev` |
| Carpeta | déjala como está |
| Imagen ISO | selecciona el `.iso` de Ubuntu que descargaste |
| Skip Unattended Installation | **márcalo** ✅ |

Marcar esa casilla es importante: queremos hacer la instalación a mano para ver qué pasa.

**Pantalla 2 — Hardware**

| Campo | Valor |
|---|---|
| Memoria base | `4096 MB` (si tienes 16 GB de RAM, pon `8192 MB`) |
| Procesadores | `2` |

**Pantalla 3 — Disco duro**

| Campo | Valor |
|---|---|
| Tamaño | `30 GB` |
| Preasignar tamaño completo | déjalo sin marcar |

Pulsa **Finalizar**. La máquina aparece en la lista de la izquierda.

### 3.4. Instalar Ubuntu dentro de la VM

Selecciona `rails-dev` y pulsa **Iniciar**. Se abre una ventana negra y arranca el
instalador de Ubuntu. Sigue estos pasos:

1. **Idioma:** Español (o English, como prefieras — recomiendo English para que los
   mensajes de error coincidan con lo que encuentres en Google).
2. **Teclado:** Spanish. **Pruébalo** en la caja de texto: escribe `ñ` y `@`. Si no salen,
   has elegido mal la distribución.
3. **Tipo de instalación:** *Interactive installation* → *Default selection*.
4. **Actualizaciones:** marca *Install third-party software*.
5. **Disco:** *Erase disk and install Ubuntu*. Esto borra el disco **de la máquina virtual**,
   no el tuyo. Es seguro.
6. **Tu cuenta:**

   | Campo | Valor sugerido |
   |---|---|
   | Nombre | tu nombre |
   | Nombre del equipo | `rails-dev` |
   | Usuario | algo corto y en minúsculas, p. ej. `dev` |
   | Contraseña | una que recuerdes — **la vas a escribir mucho** |

   Marca *Log in automatically* para ahorrarte escribirla al arrancar.

7. Espera a que termine (10-20 minutos) y pulsa **Restart Now**.
8. Cuando te pida *"Please remove the installation medium"*, pulsa **Enter**.

Si arranca y ves el escritorio morado de Ubuntu: ya tienes Linux. 🎉

### 3.5. Instalar las Guest Additions

Sin esto, la ventana de Ubuntu se queda pequeña y no puedes copiar y pegar entre
Windows y la VM. Dentro de la VM, abre una terminal (`Ctrl` + `Alt` + `T`) y ejecuta:

```bash
sudo apt update
sudo apt install -y build-essential dkms linux-headers-$(uname -r)
```

Luego, en el menú de la **ventana de VirtualBox** (arriba):
*Dispositivos* → *Insertar imagen de CD de las Guest Additions*. Acepta ejecutar el
instalador, espera y reinicia:

```bash
sudo reboot
```

Al volver, activa el portapapeles compartido:
*Dispositivos* → *Portapapeles compartido* → *Bidireccional*.

Y redimensiona la ventana: el escritorio debería ajustarse solo.

> 💾 **Haz una instantánea ahora.** Con la VM apagada, en VirtualBox:
> *Instantáneas* → *Tomar*. Llámala `ubuntu-limpio`. Si más adelante rompes algo sin
> arreglo posible, vuelves aquí en 30 segundos en lugar de reinstalar todo.

---

## 4. Primeros pasos en Ubuntu: la terminal

La terminal es una ventana donde escribes órdenes en lugar de hacer clic. Da respeto al
principio y a las dos semanas no querrás usar otra cosa.

Ábrela con `Ctrl` + `Alt` + `T`. Verás algo así:

```
dev@rails-dev:~$
```

Eso significa: usuario `dev`, en el equipo `rails-dev`, dentro de la carpeta `~`
(que es tu carpeta personal, `/home/dev`).

### Los diez comandos que necesitas hoy

| Comando | Qué hace |
|---|---|
| `pwd` | dime en qué carpeta estoy |
| `ls` | lista lo que hay en esta carpeta |
| `ls -la` | lo mismo, con detalles y archivos ocultos |
| `cd carpeta` | entra en `carpeta` |
| `cd ..` | sube un nivel |
| `cd ~` | vuelve a mi carpeta personal |
| `mkdir nombre` | crea una carpeta |
| `cat archivo` | muestra el contenido de un archivo |
| `code .` | abre la carpeta actual en VS Code |
| `sudo <algo>` | ejecuta `<algo>` como administrador (te pedirá la contraseña) |

Dos teclas que te van a ahorrar la vida:

- **`Tab`** autocompleta nombres de archivos y carpetas. Úsalo siempre. Escribir
  nombres enteros a mano es de novatos y de gente que se equivoca.
- **`↑`** recupera el comando anterior.

Y para parar un programa que se ha quedado colgado: **`Ctrl` + `C`**.

### Ejercicio de calentamiento

```bash
cd ~
mkdir projects
cd projects
pwd
```

Si la última línea dice `/home/dev/projects`, lo has hecho bien. Ahí va a vivir el proyecto.

---

## 5. Instalar las herramientas de desarrollo

Copia y pega los bloques **uno a uno**, y lee lo que hace cada uno. No pegues los cinco
seguidos: si algo falla, quieres saber dónde.

### 5.1. Actualizar el sistema y las dependencias base

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y build-essential git curl libssl-dev libreadline-dev \
  zlib1g-dev libyaml-dev libffi-dev libgmp-dev
```

*Qué es esto:* compiladores y librerías que Ruby necesita para instalarse. Sin ellas
la instalación de Ruby falla con errores crípticos.

### 5.2. Instalar `mise` (gestor de versiones de Ruby)

No instalamos Ruby directamente desde `apt` porque ahí viene una versión vieja. Usamos
`mise`, que permite tener varias versiones de Ruby y cambiar entre ellas por proyecto.

```bash
curl https://mise.run | sh
echo 'eval "$(~/.local/bin/mise activate bash)"' >> ~/.bashrc
source ~/.bashrc
mise --version
```

Si `mise --version` responde con un número, vamos bien.

### 5.3. Instalar Ruby

```bash
mise use --global ruby@3.4
ruby -v
```

La compilación tarda **varios minutos**. Es buen momento para un café. Al terminar,
`ruby -v` debe mostrar algo como `ruby 3.4.x`.

### 5.4. Instalar PostgreSQL

PostgreSQL es la base de datos donde se guardarán los coches, las ventas y todo lo demás.

```bash
sudo apt install -y postgresql postgresql-contrib libpq-dev
sudo systemctl status postgresql
```

El `status` debe decir `active (exited)` o `active (running)`. Pulsa `q` para salir.

Ahora creamos un usuario de base de datos que se llame igual que tu usuario de Ubuntu,
para que Rails pueda conectarse sin líos:

```bash
sudo -u postgres createuser --superuser $USER
sudo -u postgres createdb $USER
psql -c "SELECT version();"
```

Si la última línea escupe la versión de PostgreSQL, la base de datos está lista.

> 🔐 **Sobre `--superuser`:** en producción jamás darías permisos de superusuario a la
> aplicación. En tu máquina de desarrollo es lo cómodo y no pasa nada. Lo hablaremos
> cuando lleguemos al hito de despliegue.

### 5.5. Instalar Rails

```bash
gem install rails -v 8.1
rails -v
```

`gem` es el gestor de paquetes de Ruby; una "gema" es una librería. Rails es, de hecho,
una gema más.

### 5.6. Instalar VS Code

```bash
sudo snap install code --classic
```

Ábrelo con `code .` desde cualquier carpeta. Instala estas extensiones (icono de los
cuadraditos en la barra lateral):

- **Ruby LSP** (de Shopify) — autocompletado y navegación por el código
- **Ruby Sorbet** o **Ruby Extensions Pack** — coloreado y utilidades
- **ERB Formatter/Beautify** — para las plantillas HTML de Rails
- **GitLens** — para ver el historial de Git cómodamente

### 5.7. Comprobación final

```bash
ruby -v && rails -v && psql --version && git --version && code --version
```

Cinco líneas con cinco versiones. Si alguna falla, resuélvela antes de seguir.

> 💾 **Segunda instantánea:** apaga la VM y toma una llamada `entorno-listo`.

---

## 6. Crear el proyecto Rails

```bash
cd ~/projects
rails new dealership-manager --database=postgresql
cd dealership-manager
```

*Qué acaba de pasar:* Rails ha generado unas cuantas decenas de archivos y carpetas.
Parece abrumador; en realidad al principio solo tocarás cuatro sitios:

| Carpeta | Qué hay dentro |
|---|---|
| `app/models/` | Las **clases de negocio**: `Car`, `Sale`, `Dealership`… |
| `app/controllers/` | Los **controladores**: reciben peticiones del navegador y responden |
| `app/views/` | Las **plantillas HTML** que ve el usuario |
| `db/migrate/` | Las **migraciones**: cambios en la estructura de la base de datos |
| `test/` | Los **tests**: código que comprueba que el código funciona |
| `config/routes.rb` | El **mapa de URLs** de la aplicación |

Crea las bases de datos y arranca el servidor:

```bash
bin/rails db:create
bin/rails server
```

Abre Firefox dentro de la VM y ve a **http://localhost:3000**.

Si ves la página de bienvenida de Rails con el logo rojo: **enhorabuena, tienes una
aplicación web funcionando**. Para el servidor con `Ctrl` + `C`.

### El ciclo petición → respuesta

Antes de escribir nada, quédate con este dibujo mental. Es el 80% de Rails:

```
   Navegador
      │  GET /cars
      ▼
   routes.rb ──────► decide qué controlador atiende la URL
      │
      ▼
   CarsController#index ──────► pide los datos al modelo
      │
      ▼
   Car (modelo) ──────► consulta la base de datos (PostgreSQL)
      │
      ▼
   app/views/cars/index.html.erb ──────► pinta el HTML
      │
      ▼
   Navegador (ve la lista de coches)
```

Cada vez que algo no funcione, pregúntate: *¿en qué paso de esta cadena se ha roto?*

---

## 7. Configurar Git y GitHub

**Git** guarda el historial de tu código. **GitHub** guarda ese historial en internet.

### 7.1. Presentarte a Git

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu-email@ejemplo.com"
git config --global init.defaultBranch main
```

### 7.2. Crear una clave SSH

Es la forma de que GitHub sepa que eres tú sin escribir la contraseña cada vez.

```bash
ssh-keygen -t ed25519 -C "tu-email@ejemplo.com"
```

Pulsa `Enter` tres veces (ubicación por defecto, sin contraseña). Luego:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copia todo lo que sale (empieza por `ssh-ed25519`) y pégalo en GitHub:
*Settings* → *SSH and GPG keys* → *New SSH key*.

Comprueba que funciona:

```bash
ssh -T git@github.com
```

Debe saludarte por tu nombre de usuario.

### 7.3. Subir el proyecto

Crea un repositorio vacío en GitHub llamado `dealership-manager` (sin README, sin
`.gitignore` — Rails ya te ha creado uno). Después:

```bash
git add .
git commit -m "chore: initial Rails application skeleton"
git remote add origin git@github.com:TU-USUARIO/dealership-manager.git
git push -u origin main
```

Recarga la página de GitHub: ahí está tu código.

---

## 8. El enunciado: qué vamos a construir

**Dealership Manager** es la herramienta interna de un grupo de concesionarios de coches.

Los que la usan son:

- **Comerciales**, que consultan el stock y registran las ventas que cierran.
- **Responsables de concesionario**, que dan de alta coches y ven cómo va su tienda.
- **Administración**, que revisa las comisiones que hay que pagar cada mes.

### 8.1. El dominio

**Coches.** Cada coche pertenece a un concesionario y tiene marca, modelo, año,
matrícula (o número de bastidor), kilómetros, precio de venta y precio de coste.
Un coche está `available`, `reserved` o `sold`. Los hay de gama normal y de gama lujo,
y esa distinción acabará afectando a las comisiones.

**Ventas.** Cuando un comercial cierra una operación se registra una venta: qué coche,
a qué cliente, qué comercial, por cuánto dinero y en qué fecha. El precio final puede
no ser el de catálogo, porque casi siempre hay regateo. Al vender, el coche pasa a
`sold` y deja de estar disponible: **un coche no se puede vender dos veces**.

**Comisiones.** Es la parte interesante. Cada venta genera una comisión para el comercial,
calculada por tramos sobre el precio final:

| Precio final de la venta | Comisión |
|---|---|
| Hasta 10.000 € | 3 % |
| De 10.000 € a 30.000 € | 4 % |
| Más de 30.000 € | 5 % |

Y encima de eso, unas reglas que iremos añadiendo:

- Los coches de **gama lujo** llevan **un punto porcentual extra**.
- Si el precio final baja del **90 % del precio de catálogo**, la comisión se **reduce a la mitad**:
  la casa no premia malvender.
- Una venta **con pérdidas** (precio final por debajo del coste) **no genera comisión**.

Esas reglas son deliberadamente enrevesadas. Son la excusa perfecta para aprender a
escribir tests primero y a separar la lógica de negocio del resto de la aplicación.

### 8.2. Lo que NO vamos a hacer

Para que el proyecto no se nos vaya de las manos, queda fuera: pasarela de pagos real,
financiación, gestión de talleres, facturación fiscal y app móvil. Si llegamos con
ganas al final, ya hablaremos.

---

## 9. Roadmap de hitos

> Los hitos 1 a 4 son el curso "de verdad". Del 5 en adelante ya se parece bastante a
> trabajar en una empresa.

### Hito 0 — El entorno *(los apartados 3 a 7 de este README)*

**Objetivo:** VM montada, Rails arrancando en `localhost:3000` y el repositorio en GitHub.

**Conceptos nuevos:** terminal, gestor de paquetes, gestor de versiones, cliente/servidor,
control de versiones.

**Criterios de aceptación**

- [ ] `ruby -v`, `rails -v` y `psql --version` responden
- [ ] `bin/rails server` arranca y la página de bienvenida carga
- [ ] Hay un commit inicial en GitHub

---

### Hito 1 — Inventario de coches

**Objetivo:** dar de alta, listar, editar y borrar coches. Un CRUD completo.

**Conceptos nuevos**

- Modelos, migraciones y esquema de base de datos
- El ciclo petición → respuesta al completo
- Rutas RESTful y las siete acciones de un controlador
- Vistas ERB y formularios
- Validaciones
- Los primeros tests: modelo y controlador

**Trabajo**

- Modelo `Car`: `brand`, `model`, `year`, `plate`, `mileage`, `price_cents`, `cost_cents`, `status`
- Validaciones: marca y modelo obligatorios; matrícula única; año entre 1900 y el que viene;
  precio positivo
- `status` como enum: `available` / `reserved` / `sold`
- Pantallas de listado, detalle, alta y edición
- Seeds con una veintena de coches para no trabajar sobre una pantalla vacía

**Criterios de aceptación**

- [ ] Puedo crear un coche desde el navegador y verlo en la lista
- [ ] Si dejo la marca vacía, el formulario me lo dice en lugar de reventar
- [ ] No puedo dar de alta dos coches con la misma matrícula
- [ ] `bin/rails test` pasa en verde
- [ ] Los precios se muestran como `24.500,00 €`, no como `2450000`

**Discusión del hito:** ¿por qué guardamos el dinero en céntimos y en un entero, y nunca
en un `float`?

---

### Hito 2 — Varios concesionarios

**Objetivo:** los coches dejan de flotar en el vacío y pasan a pertenecer a un concesionario.

**Conceptos nuevos**

- Asociaciones `belongs_to` / `has_many`
- Claves foráneas e índices
- Rutas anidadas
- Scopes
- El problema N+1 y cómo detectarlo

**Trabajo**

- Modelo `Dealership`: `name`, `city`, `address`, `phone`
- `Car belongs_to :dealership`, `Dealership has_many :cars`
- Migración que añade la columna a la tabla existente **sin perder los datos**
- Filtro de coches por concesionario
- Ficha de concesionario con su stock y un par de cifras: unidades disponibles y valor del inventario

**Criterios de aceptación**

- [ ] Todo coche tiene concesionario y no se puede guardar sin él
- [ ] Desde la ficha de un concesionario veo solo sus coches
- [ ] Borrar un concesionario con coches dentro **no** deja coches huérfanos (decidimos la política)
- [ ] El listado no dispara una consulta por cada coche (mira los logs)

---

### Hito 3 — Ventas

**Objetivo:** registrar ventas y que el estado del inventario sea consecuente.

**Conceptos nuevos**

- Modelos con más de una asociación
- Validaciones que dependen del estado de otro objeto
- Transacciones de base de datos
- Callbacks (y por qué conviene usarlos con moderación)
- Tests de casos límite

**Trabajo**

- Modelo `Customer`: `name`, `email`, `phone`, `document_number`
- Modelo `Sale`: `car`, `customer`, `salesperson`, `final_price_cents`, `sold_at`
- Por ahora `salesperson` puede ser un simple campo de texto; en el hito 5 será un usuario de verdad
- Al crear una venta, el coche pasa a `sold`
- **Regla dura:** no se puede vender un coche que no esté `available`
- Listado de ventas con filtro por fechas

**Criterios de aceptación**

- [ ] Al vender un coche, desaparece del stock disponible
- [ ] Intentar vender un coche ya vendido devuelve un error claro, no una excepción
- [ ] Si la venta no se puede guardar, el coche **no** se queda marcado como vendido
- [ ] Hay un test que cubre el intento de venta doble

**Discusión del hito:** ¿qué pasa si dos comerciales venden el mismo coche a la vez?
Primera conversación sobre condiciones de carrera.

---

### Hito 4 — El sistema de comisiones

**Objetivo:** implementar las reglas de comisión del enunciado, con tests primero.

**Conceptos nuevos**

- **TDD en serio**: test que falla → código mínimo → refactor
- Objetos de dominio fuera de `app/models` (los famosos POROs)
- Separar el cálculo de la persistencia
- Tablas de casos de prueba

**Trabajo**

- `CommissionCalculator`: recibe una venta y devuelve el importe
- Tramos del 3 / 4 / 5 %
- Extra por gama lujo
- Penalización por descuento agresivo
- Cero comisión si la venta pierde dinero
- Modelo `Commission` que guarda el resultado junto a la venta
- Pantalla de comisiones por comercial y por mes

**Criterios de aceptación**

- [ ] Existe un test por cada regla y por cada frontera exacta (9.999,99 € / 10.000 € / 10.000,01 €)
- [ ] El cálculo no toca la base de datos: se le puede pasar una venta en memoria
- [ ] Cambiar un porcentaje se hace en **un solo sitio**
- [ ] La suma de comisiones del mes cuadra con la suma de las ventas

**Discusión del hito:** este es el hito donde se ve para qué sirven los tests. Cambiar
una regla de comisión sin tests da miedo; con tests, dos minutos.

---

### Hito 5 — Usuarios, login y permisos

**Objetivo:** que la aplicación sepa quién la está usando y qué puede hacer.

**Conceptos nuevos**

- Autenticación (el generador de Rails 8)
- Sesiones y cookies
- Hashing de contraseñas
- Autorización por roles
- Tests de integración

**Trabajo**

- Modelo `User` con roles `salesperson`, `manager`, `admin`
- Login y logout
- `Sale belongs_to :salesperson, class_name: "User"`
- Un comercial ve solo las ventas de su concesionario; un admin las ve todas
- Solo `manager` y `admin` pueden dar de alta o borrar coches

**Criterios de aceptación**

- [ ] Sin login no se ve nada más allá de la pantalla de acceso
- [ ] Un comercial que fuerza la URL de otro concesionario recibe un 403, no los datos
- [ ] Las contraseñas no aparecen en claro ni en la base de datos ni en los logs
- [ ] Las comisiones se asignan al usuario que registró la venta

---

### Hito 6 — Informes y rendimiento

**Objetivo:** un panel que responda a las preguntas del negocio, y que sea rápido.

**Conceptos nuevos**

- Agregaciones en SQL desde Active Record (`group`, `sum`, `count`)
- Query objects
- Índices y `EXPLAIN`
- Caché de fragmentos
- Datos de prueba a escala (miles de registros)

**Trabajo**

- Panel: ventas del mes, margen, top comerciales, rotación de stock
- Coches parados: más de 90 días en inventario sin vender
- Exportación a CSV
- Un `seed` grande para que se note la diferencia entre una consulta buena y una mala

**Criterios de aceptación**

- [ ] El panel carga en menos de un segundo con 10.000 ventas
- [ ] Ninguna consulta del panel se ejecuta dentro de un bucle
- [ ] El CSV abre correctamente en Excel, con los decimales bien

---

### Hito 7 — Refactor: gama normal y gama lujo

**Objetivo:** meter los tipos de coche sin llenar el código de `if`.

**Conceptos nuevos**

- Herencia y polimorfismo aplicados a un problema real
- Single Table Inheritance vs. objetos de política
- Principio abierto/cerrado
- Refactorizar apoyándose en los tests que ya existen

**Trabajo**

- `StandardCar` y `LuxuryCar`
- Reglas propias de la gama lujo: comisión extra, aprobación del responsable por encima de
  cierto descuento, campos específicos
- Reescribir `CommissionCalculator` para que admita reglas nuevas sin tocar las viejas
- Añadir una tercera gama (comerciales / industriales) **como ejercicio final**: si el
  diseño es bueno, cuesta poco

**Criterios de aceptación**

- [ ] Añadir una gama nueva no obliga a modificar el cálculo existente
- [ ] Los tests del hito 4 siguen pasando sin tocarlos
- [ ] No hay ningún `if car.luxury?` repartido por las vistas

---

### Hito 8 — Salir al mundo

**Objetivo:** que la aplicación viva fuera de tu portátil.

**Conceptos nuevos**

- API JSON y serialización
- Trabajos en segundo plano
- Variables de entorno y secretos
- Despliegue
- Logs y monitorización básica

**Trabajo**

- Endpoints JSON para consultar el stock
- Email al comercial cuando se le registra una comisión, en segundo plano
- Despliegue a un servidor real
- README de producción: cómo arrancar, cómo desplegar, cómo mirar los logs

**Criterios de aceptación**

- [ ] Hay una URL pública que funciona
- [ ] Los secretos no están en el repositorio
- [ ] Un despliegue nuevo se hace con un comando

---

## 10. Cómo trabajamos: TDD y commits

### Una rama por hito

```bash
git switch -c milestone-1-car-inventory
```

Al terminar el hito, subes la rama y abres un Pull Request. Yo lo reviso ahí y comentamos
el código línea a línea, igual que en una empresa.

### El ciclo de trabajo

1. **Escribe el test primero.** Debe fallar. Si pasa a la primera, el test no prueba nada.
2. **Escribe el código mínimo** para que pase. Feo está bien de momento.
3. **Refactoriza** con la red de seguridad de los tests en verde.
4. **Commit.**

Sí, es más lento los tres primeros días. Después es más rápido, y esa es la única razón
por la que la gente lo hace.

### Mensajes de commit

Formato **conventional commits**, en inglés:

```
feat: add Car model with validations
fix: prevent selling a car that is already sold
test: cover commission tier boundaries
refactor: extract CommissionCalculator from Sale
chore: bump rails to 8.1.3
docs: document the commission rules
```

Un commit por cosa. Nada de `wip`, `cambios` ni `asdasd`.

---

## 11. Chuleta de comandos

```bash
# Servidor
bin/rails server                  # arranca en localhost:3000
bin/rails console                 # consola interactiva con la app cargada

# Base de datos
bin/rails db:create               # crea las bases de datos
bin/rails db:migrate              # aplica las migraciones pendientes
bin/rails db:rollback             # deshace la última migración
bin/rails db:seed                 # carga datos de prueba
bin/rails db:reset                # borra, recrea y vuelve a sembrar

# Generadores
bin/rails generate model Car brand:string price_cents:integer
bin/rails generate controller Cars index show
bin/rails generate migration AddDealershipToCars dealership:references
bin/rails destroy model Car       # deshace un generate

# Tests
bin/rails test                    # todos
bin/rails test test/models        # solo los modelos
bin/rails test test/models/car_test.rb:42   # solo una línea

# Inspección
bin/rails routes | grep car       # qué URLs existen
bin/rails about                   # versiones de todo

# Git
git status
git add .
git commit -m "feat: ..."
git push
git switch -c nombre-de-rama
```

---

## 12. Problemas frecuentes

**La VM va lentísima o VirtualBox dice que la virtualización está desactivada**

Hay que activar VT-x/AMD-V en la BIOS. Reinicia Windows, entra en la BIOS (`F2`, `Supr`
o `F10` según el fabricante) y busca *Intel Virtualization Technology* o *SVM Mode*.
Actívalo y guarda.

**VirtualBox solo ofrece sistemas de 32 bits**

Mismo problema que el anterior, o Hyper-V está activo. En PowerShell **como administrador**:

```powershell
bcdedit /set hypervisorlaunchtype off
```

Reinicia. (Ojo: esto desactiva WSL2. Si quieres WSL2, ve al [Anexo A](#anexo-a-alternativa-con-wsl2).)

**`gem install rails` falla con errores de compilación**

Faltan las librerías del apartado 5.1. Vuelve a ejecutar ese bloque.

**`rails db:create` dice `FATAL: role "dev" does not exist`**

No creaste el usuario de PostgreSQL. Repite el apartado 5.4.

**`could not connect to server: No such file or directory`**

PostgreSQL no está arrancado:

```bash
sudo systemctl start postgresql
sudo systemctl enable postgresql   # para que arranque solo al encender
```

**`Address already in use - bind(2) for "127.0.0.1" port 3000`**

Tienes otro servidor corriendo. Ciérralo con `Ctrl` + `C` en su terminal, o:

```bash
pkill -f puma
```

**`ruby: command not found` tras reiniciar**

`mise` no se está cargando. Comprueba que la línea del apartado 5.2 está en `~/.bashrc`:

```bash
tail -3 ~/.bashrc
```

**La pantalla de Ubuntu se queda pequeña**

Faltan las Guest Additions (apartado 3.5).

**Se me ha roto todo y no sé por qué**

Restaura la instantánea `entorno-listo` desde VirtualBox. Tu código está en GitHub, así
que no pierdes nada: vuelves a clonar y sigues.

---

## Anexo A: alternativa con WSL2

Si la máquina virtual te va lenta, **WSL2** es otra vía: Windows ejecuta un Ubuntu real,
pero integrado, sin ventana aparte y con mucho menos consumo. A cambio no ves un
escritorio Linux, solo la terminal (que es lo que vamos a usar el 95% del tiempo).

### Instalación

En PowerShell **como administrador**:

```powershell
wsl --install -d Ubuntu-26.04
```

Reinicia. Al arrancar te pedirá usuario y contraseña para Ubuntu.

### Diferencias con la VM

A partir de ahí, **los apartados 4 a 7 de este README valen igual**, con estos matices:

| Tema | En WSL2 |
|---|---|
| VS Code | Instálalo en **Windows**, no dentro de Ubuntu, y añade la extensión *WSL*. Desde la terminal de Ubuntu, `code .` abre el VS Code de Windows conectado a Linux. |
| PostgreSQL | No hay `systemd` completo en algunas versiones. Si `systemctl` falla, usa `sudo service postgresql start`. |
| Navegador | `localhost:3000` se abre en tu Chrome/Firefox de Windows directamente. |
| Archivos | **Guarda el proyecto dentro de Linux** (`~/projects`), nunca en `/mnt/c/…`. Ahí Rails va diez veces más lento. |
| Guest Additions | No aplican, sáltate el apartado 3.5. |

Recomendación: si tu portátil tiene 8 GB de RAM, tira de **WSL2**. Si tiene 16 GB o más
y quieres ver un Linux completo con su escritorio, tira de **VirtualBox**.

---

## Anexo B: glosario

| Término | Qué es |
|---|---|
| **Ruby** | El lenguaje de programación que vamos a usar |
| **Rails** | El framework: el andamiaje que evita reescribir lo de siempre |
| **Gema (gem)** | Una librería de Ruby |
| **Bundler / Gemfile** | La lista de gemas del proyecto y quien las instala |
| **Modelo** | Clase que representa algo del negocio y habla con la base de datos |
| **Migración** | Archivo que describe un cambio en la estructura de la base de datos |
| **Controlador** | Recibe una petición HTTP y decide qué responder |
| **Vista** | Plantilla que genera el HTML |
| **ERB** | El formato de esas plantillas: HTML con Ruby incrustado |
| **CRUD** | Create, Read, Update, Delete: las cuatro operaciones básicas |
| **REST** | Convenio para nombrar URLs según el recurso y la acción |
| **Active Record** | La parte de Rails que traduce entre objetos Ruby y filas de SQL |
| **Migración pendiente** | Un cambio de base de datos que aún no has aplicado |
| **Seed** | Datos de ejemplo que se cargan de golpe |
| **TDD** | Test Driven Development: escribir el test antes que el código |
| **Repositorio** | La carpeta del proyecto con su historial de Git |
| **Commit** | Una foto guardada del código en un momento dado |
| **Rama (branch)** | Una línea de trabajo paralela |
| **Pull Request** | Propuesta de fusionar una rama, con revisión de por medio |

---

## Y ahora qué

1. Termina el **Hito 0** completo.
2. Haz que `bin/rails server` arranque y enséñame la captura.
3. Sube el commit inicial a GitHub.
4. Nos vemos y empezamos el **Hito 1**.

Si te atascas más de veinte minutos en algo, pregunta. Atascarse forma parte del oficio;
perder una tarde entera, no.
