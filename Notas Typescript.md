> ## Notas Typescript

- no sirve para validar datos en tiempo de ejecucion, es un lenguaje estatico que solo sirve para validar en tiempo de compilacion

```typescript
// Tipar arrow functions
const sumar = (a:number, b:number): number => {
    return a + b;
}


//Never, se usa cuando sabes que la funcion no va a retornar nada
function throwError(message: string): never {
    throw new Error(message); 
    // si usamos never hacemos un throw nunca llegaremos a ese return implicito

    // return implicito - te da igual con el void 
}

//inferencia funciones anonimas segun el contexto 
const lista = ['juan','baez']

const saludar = (nombre:string, apellido:string)
```

## Ejemplo de una funcion que saluda a un grupo de personas con Typescript

```typescriptag-0-1iqrgqalnag-1-1iqrgqaln
const lista = ['juan','valeria', "JULIAM", "matias"]
const saludosBase = ['Hola', 'Qué tal', 'Buenas', 'Ey', '¿como estas?']

const capitalize = (x: string): string => {
    return x.charAt(0).toUpperCase() + x.slice(1).toLowerCase()
}

const saludoPredefinido = () => {
   const i = Math.floor(Math.random() * saludosBase.length)
   return saludosBase[i]
}

const saludar = (nombre:string): string => {
    const saludo = saludoPredefinido()
    return `${saludo}  ${capitalize(nombre)}`
}


const saludos = (lista: string[]): string => {
    return lista.map(saludar). join(', ')
}

console.log(saludos(lista))
```

## Objetos

```typescript
let persona = {
    name: 'Juan'
    age: 20
}

// Afecta la inferencia 
// persona.age, se auto completa por la inferencia 
const createPersona = (name: string, age: 20) => {
    return{ name,age }
}


const persona1 = createPersona('Valeria', 21)
```

## Type Alias

```typescript
type Persona = { //Creamos nuestro propio tipo Persona
    name: string;
    age: number;
}


let persona: Persona = { //Asignamos el tipo persona que creamos
    name: 'Juan'
    age: 20
}

//tambien le asignamos el tipo
function createPerson(name: string, age: number): Persona { 
    return{ name,age }
}

//Otra forma de hacer la función
function createPersona2(persona: Persona): Persona {
    const { name, age } = hero;
    return {name, age }
}


const persona1 = createPersona('Valeria', 21)
```

## Optionals props

```typescript
type PersonaId = `${string}-${string}-${string}-${string}-${string}`


type Persona = { //Creamos nuestro propio tipo Persona
    readonly id?: PersonaId
    //solo lo podemos leer, no lo podemos mutar
    name: string;
    age: number;
    isActive?: boolean; //de forma opcional con el ? (podemos pasarlo o no)
}


let persona: Persona = { //Asignamos el tipo persona que creamos
    name: 'Juan'
    age: 20
}

//tambien le asignamos el tipo
function createPerson(name: string, age: number): Persona { 
    return{ name,age }
}

//Otra forma de hacer la función
function createPersona2(persona: Persona): Persona {
    const { name, age } = persona;
    return { 
    id: crypto.randomUUID(), //nativo de la plataforma web
    //id: "123", va a dar error pq no se espera ese tipo
    name, 
    age, 
    isActive: true }
}


const persona1 = createPersona('Valeria', 21)
console.log(persona1.isActive) // --> true


persona1.id = 2 //nos va a tirar error porque esta solo en modo lectura 
// no es inmutable ya que al pasarse a js cuando se compila se puede
//mutar de esta manera 
```

## Templates union type

```typescript
type HexadecimalColor = `${string}`


const color: HexadecimalColor = '0033ff' //nos va a dar error porque no es el tipo que queremos
const color2: HexadecimalColor = '#0033ff'
```

## Union type

```typescript
type PersonaId = `${string}-${string}-${string}-${string}-${string}`

type PersonaIQ = 'low' | 'medium' | 'high'
// |: significa o, puede ser low o medium o high
// Union de tipos

type Persona = {
    readonly id?: PersonaId
    name: string;
    age: number;
    isActive?: boolean;
    iq?: PersonaIQ
}


let persona: Persona = { 
    name: 'Juan'
    age: 20
}

//tambien le asignamos el tipo
function createPerson(name: string, age: number): Persona { 
    return{ name,age }
}

//Otra forma de hacer la función
function createPersona2(persona: Persona): Persona {
    const { name, age } = persona;
    return { 
    id: crypto.randomUUID(),
    name, 
    age, 
    isActive: true }
}


const persona1 = createPersona('Valeria', 21)
console.log(persona1.isActive) // --> true
```

## Intersection types

```typescript
type PersonaId = `${string}-${string}-${string}-${string}-${string}`

type PersonaIQ = 'low' | 'medium' | 'high'

type PersonaBasic = {
    name: string;
    age: number;
}

type PersonaOpp = {
    readonly id?: PersonaId
    isActive?: boolean;
    iq?: PersonaIQ
}

type Persona = PersonaBasic & PersonaOpp

let persona: Persona = { 
    name: 'Juan'
    age: 20
}

//tambien le asignamos el tipo
function createPerson(name: string, age: number): Persona { 
    return{ name,age }
}

//en el input especificamos los que tienen que pasar 
function createPersona2(input: PersonaBasic): Persona {
    const { name, age } = input;

    return { 
    id: crypto.randomUUID(),
    name, 
    age, 
    isActive: true 
    }
}


const persona1 = createPersona('Valeria', 21)
console.log(persona1.isActive) // --> true
```

## Types indexin

```typescript
type HeroProps = {
    isActive: boolean
    address: {
        planet: string
        city: string
    }
}

const addresHero: HeroProps['address'] = {
    city: 'Madrid'
    planet: ''
}
```

## Types from value

```typescript
const address = {
    planet: string,
    city: string
}

//typeof te permite crear tipos aprovechando codigo que la tienes 
type Address = typeof address
```

## Types from function return

```typescript
function createAddress() {
    return {
    planet: string,
    city: string
    }
}

//recuperas el tipo a partir del codigo que ya tienes
//typeof te permite crear tipos aprovechando codigo que la tienes 
type Address = ReturnType<typeof createAddress>
```

## Arrays

```typescript
//esto ca a permitir los tipos especificados
const languages: (string | number | boolean)[] = []


languages.push('JavaScript')


/*
[   
    ['x', '0', '0'],
    ['x', '0', '0'],
    ['x', '0', '0'] 
]
*/

type ValueCell = 'x' | '0' | ' '
//usamos una tupla para definir el gameBoard del juago (3x3)
type GameBoard = [
    [ValueCell, ValueCell, ValueCell],
    [ValueCell, ValueCell, ValueCell],
    [ValueCell, ValueCell, ValueCell]
]

const gameBoard: GameBoard = [
    ['x', '0', '0'],
    ['x', '0', '0'],
    ['x', '0', '0'] 
]

gameBoard[0][0] = 'x'

//Tuplas
type RGB = readonly [number, number, number]
//solo de modo lectura para que no lo puedan modificar

const black: RGB = [0, 0, 0]
const white: RGB = [255, 255, 255]
```

## Enums

```typescript
 //se usa para una coleccion de datos finita
 //El const se usa para generar menos codigo, y se recomienda casi siempre
 //pero en el caso que el codigo lo utilizen en otro programa externo es
 //recomendado usar sin el const
 /*
 codigo Js sin el const
 "use strict";
var ERROR_TYPE;
(function (ERROR_TYPE) {
    ERROR_TYPE[ERROR_TYPE["NOT_FOUND"] = 0] = "NOT_FOUND";
    ERROR_TYPE[ERROR_TYPE["UNAUTHORIZED"] = 1] = "UNAUTHORIZED";
    ERROR_TYPE[ERROR_TYPE["FORBIDDEN"] = 2] = "FORBIDDEN";
})(ERROR_TYPE || (ERROR_TYPE = {}));
function mostrarMensaje(tipoDeError) {
    if (tipoDeError === ERROR_TYPE.NOT_FOUND) {
        console.log('no se encuentra el recurso');
    }
    else if (tipoDeError === ERROR_TYPE.UNAUTHORIZED) {
        console.log('no tienes permisos para acceder');
    }
    else if (tipoDeError === ERROR_TYPE.FORBIDDEN) {
        console.log('no tienes permisos para acceder');
    }
}

 codigo Js con el const
 "use strict";
function mostrarMensaje(tipoDeError) {
    if (tipoDeError === 0 /* ERROR_TYPE.NOT_FOUND */) {
        console.log('no se encuentra el recurso');
    }
    else if (tipoDeError === 1 /* ERROR_TYPE.UNAUTHORIZED */) {
        console.log('no tienes permisos para acceder');
    }
    else if (tipoDeError === 2 /* ERROR_TYPE.FORBIDDEN */) {
        console.log('no tienes permisos para acceder');
    }
 */

 const enum ERROR_TYPE {
     NOT_FOUND,
     UNAUTHORIZED,
     FORBIDDEN
 }

 function mostrarMensaje(tipoDeError: ERROR_TYPE) {
     if (tipoDeError === ERROR_TYPE.NOT_FOUND) {
         console.log('no se encuentra el recurso')
     } else if  (tipoDeError === ERROR_TYPE.UNAUTHORIZED) {
         console.log('no tienes permisos para acceder')
     } else if (tipoDeError === ERROR_TYPE.FORBIDDEN) {
         console.log('no tienes permisos para acceder')
     }
 }
```

## Aserciones de tipos

```typescript
const canvas = getElementById('canvas') // as HTMLCanvasElement: esto NO!

//puede devolver: null | HTMLElement

//Inferencia: Typescript sabe que en canvas hay: HTMLCanvasElement
if (canvas instanceof HTMLCanvasElement) {
    const ctx = canvas.getContext('2d')
}
```

## Fetching de datos

```typescript
// fetching de datos con TypeScript
// al usar esta forma de validacion con ts en tiempo de ejecucion puede
//fallar, pero podemos usar ts junto con zod que es una libreria que nos 
//ayuda a validar en tiempo de ejecucuion, cosa que no puede hacer ts
export type GitHubAPIResponse = {
    total_count:        number;
    incomplete_results: boolean;
    items:              Item[];
}

export type Item = {
    id:                          number;
    node_id:                     string;
    name:                        string;
    full_name:                   string;
    private:                     boolean;
    owner:                       Owner;
    html_url:                    string;
    description:                 null | string;
    fork:                        boolean;
    url:                         string;
    forks_url:                   string;
    keys_url:                    string;
    collaborators_url:           string;
    teams_url:                  string;
    hooks_url:                   string;
    issue_events_url:            string;
    events_url:                  string;
    assignees_url:               string;
    branches_url:                string;
    tags_url:                    string;
    blobs_url:                   string;
    git_tags_url:                string;
    git_refs_url:                string;
    trees_url:                   string;
    statuses_url:                string;
    languages_url:               string;
    stargazers_url:              string;
    contributors_url:            string;
    subscribers_url:             string;
    subscription_url:            string;
    commits_url:                 string;
    git_commits_url:             string;
    comments_url:                string;
    issue_comment_url:           string;
    contents_url:                string;
    compare_url:                 string;
    merges_url:                  string;
    archive_url:                 string;
    downloads_url:               string;
    issues_url:                  string;
    pulls_url:                   string;
    milestones_url:              string;
    notifications_url:           string;
    labels_url:                  string;
    releases_url:                string;
    deployments_url:             string;
    created_at:                  Date;
    updated_at:                  Date;
    pushed_at:                   Date;
    git_url:                     string;
    ssh_url:                     string;
    clone_url:                   string;
    svn_url:                     string;
    homepage:                    null | string;
    size:                        number;
    stargazers_count:            number;
    watchers_count:              number;
    language:                    Language | null;
    has_issues:                  boolean;
    has_projects:                boolean;
    has_downloads:               boolean;
    has_wiki:                    boolean;
    has_pages:                   boolean;
    has_discussions:             boolean;
    forks_count:                 number;
    mirror_url:                  null;
    archived:                    boolean;
    disabled:                    boolean;
    open_issues_count:           number;
    license:                     License | null;
    allow_forking:               boolean;
    is_template:                 boolean;
    web_commit_signoff_required: boolean;
    topics:                      string[];
    visibility:                  Visibility;
    forks:                       number;
    open_issues:                 number;
    watchers:                    number;
    default_branch:              DefaultBranch;
    score:                       number;
}

export enum DefaultBranch {
    Dev = "dev",
    Develop = "develop",
    Main = "main",
    Master = "master",
}

export enum Language {
    CSS = "CSS",
    HTML = "HTML",
    JavaScript = "JavaScript",
    TypeScript = "TypeScript",
}

export type License = {
    key:     string;
    name:    string;
    spdx_id: string;
    url:     null | string;
    node_id: string;
}

export type Owner = {
    login:               string;
    id:                  number;
    node_id:             string;
    avatar_url:          string;
    gravatar_id:         string;
    url:                 string;
    html_url:            string;
    followers_url:       string;
    following_url:       string;
    gists_url:           string;
    starred_url:         string;
    subscriptions_url:   string;
    organizations_url:   string;
    repos_url:           string;
    events_url:          string;
    received_events_url: string;
    type:                Type;
    user_view_type:      Visibility;
    site_admin:          boolean;
}

export enum Type {
    Organization = "Organization",
    User = "User",
}

export enum Visibility {
    Public = "public",
}

//Forma con TypeScript zod
//este codigo a la hora de compilar se pasa a js y funciona en tiempo de
//ejecucucion, se recomienda es mas completo
import * as z from "zod";


export const DefaultBranchSchema = z.enum([
    "dev",
    "develop",
    "main",
    "master",
]);
export type DefaultBranch = z.infer<typeof DefaultBranchSchema>;


export const LanguageSchema = z.enum([
    "CSS",
    "HTML",
    "JavaScript",
    "TypeScript",
]);
export type Language = z.infer<typeof LanguageSchema>;


export const TypeSchema = z.enum([
    "Organization",
    "User",
]);
export type Type = z.infer<typeof TypeSchema>;


export const VisibilitySchema = z.enum([
    "public",
]);
export type Visibility = z.infer<typeof VisibilitySchema>;

export const LicenseSchema = z.object({
    "key": z.string(),
    "name": z.string(),
    "spdx_id": z.string(),
    "url": z.union([z.null(), z.string()]),
    "node_id": z.string(),
});
export type License = z.infer<typeof LicenseSchema>;

export const OwnerSchema = z.object({
    "login": z.string(),
    "id": z.number(),
    "node_id": z.string(),
    "avatar_url": z.string(),
    "gravatar_id": z.string(),
    "url": z.string(),
    "html_url": z.string(),
    "followers_url": z.string(),
    "following_url": z.string(),
    "gists_url": z.string(),
    "starred_url": z.string(),
    "subscriptions_url": z.string(),
    "organizations_url": z.string(),
    "repos_url": z.string(),
    "events_url": z.string(),
    "received_events_url": z.string(),
    "type": TypeSchema,
    "user_view_type": VisibilitySchema,
    "site_admin": z.boolean(),
});
export type Owner = z.infer<typeof OwnerSchema>;

export const ItemSchema = z.object({
    "id": z.number(),
    "node_id": z.string(),
    "name": z.string(),
    "full_name": z.string(),
    "private": z.boolean(),
    "owner": OwnerSchema,
    "html_url": z.string(),
    "description": z.union([z.null(), z.string()]),
    "fork": z.boolean(),
    "url": z.string(),
    "forks_url": z.string(),
    "keys_url": z.string(),
    "collaborators_url": z.string(),
    "teams_url": z.string(),
    "hooks_url": z.string(),
    "issue_events_url": z.string(),
    "events_url": z.string(),
    "assignees_url": z.string(),
    "branches_url": z.string(),
    "tags_url": z.string(),
    "blobs_url": z.string(),
    "git_tags_url": z.string(),
    "git_refs_url": z.string(),
    "trees_url": z.string(),
    "statuses_url": z.string(),
    "languages_url": z.string(),
    "stargazers_url": z.string(),
    "contributors_url": z.string(),
    "subscribers_url": z.string(),
    "subscription_url": z.string(),
    "commits_url": z.string(),
    "git_commits_url": z.string(),
    "comments_url": z.string(),
    "issue_comment_url": z.string(),
    "contents_url": z.string(),
    "compare_url": z.string(),
    "merges_url": z.string(),
    "archive_url": z.string(),
    "downloads_url": z.string(),
    "issues_url": z.string(),
    "pulls_url": z.string(),
    "milestones_url": z.string(),
    "notifications_url": z.string(),
    "labels_url": z.string(),
    "releases_url": z.string(),
    "deployments_url": z.string(),
    "created_at": z.coerce.date(),
    "updated_at": z.coerce.date(),
    "pushed_at": z.coerce.date(),
    "git_url": z.string(),
    "ssh_url": z.string(),
    "clone_url": z.string(),
    "svn_url": z.string(),
    "homepage": z.union([z.null(), z.string()]),
    "size": z.number(),
    "stargazers_count": z.number(),
    "watchers_count": z.number(),
    "language": z.union([LanguageSchema, z.null()]),
    "has_issues": z.boolean(),
    "has_projects": z.boolean(),
    "has_downloads": z.boolean(),
    "has_wiki": z.boolean(),
    "has_pages": z.boolean(),
    "has_discussions": z.boolean(),
    "forks_count": z.number(),
    "mirror_url": z.null(),
    "archived": z.boolean(),
    "disabled": z.boolean(),
    "open_issues_count": z.number(),
    "license": z.union([LicenseSchema, z.null()]),
    "allow_forking": z.boolean(),
    "is_template": z.boolean(),
    "web_commit_signoff_required": z.boolean(),
    "topics": z.array(z.string()),
    "visibility": VisibilitySchema,
    "forks": z.number(),
    "open_issues": z.number(),
    "watchers": z.number(),
    "default_branch": DefaultBranchSchema,
    "score": z.number(),
});
export type Item = z.infer<typeof ItemSchema>;

export const GitHubApiResponseSchema = z.object({
    "total_count": z.number(),
    "incomplete_results": z.boolean(),
    "items": z.array(ItemSchema),
});
export type GitHubApiResponse = z.infer<typeof GitHubApiResponseSchema>;




// podemos transformar un archivo ts en un modulo usando la extencion .mts
const API_URL = "https://api.github.com/search/repositories?q=javascript"


const response = await fetch(API_URL)


if (!response.ok) {
    throw new Error('Request failed')
}

//type APIResponse = {
//    items: object[]
//}

//Hacerlo a mano lleva mucho tiempo es mejor usar quicktype

const data = await response.json() as GitHubAPIResponse

data.items.map(repo => {
    return {
        name: repo.name,
        id: repo.id,
        url: repo.html_url
    }
})
```

## Interfaces

```typescript
// una interfaz es una forma que tiene que tener nuestro objeto
// no nos dice el eobjeto en si
// se usa para definir props y metodos
// pueden estar anidadas

interface Producto {
    id: number
    nombre: string
    precio: number
    quantity: number
}

// toma las props de Producto porque es una extención de este
interface Calzado extends Producto {
    talle: number
}

interface CarritoDeCompras {
    totalPrice: number
    productos: (Producto | Calzado)[]
}

interface CarritoOps {
    add: (product: Producto) => void,
    remove: (id: number) => void,
}

//si instanciamos carritoOps nos traera las funciones de ambas interfaces
//las toma como si fueran las mismas, esto con tipos no pasa
//se extiende automaticamente
interface CarritoOps {
    clear: () => void
}

const carrito: CarritoDeCompras = {
    totalprice: 10,
    productos: [
        {
            id: 1,
            nombre: 'Papas Lays'
            precio: 5
            quantity: 2
        }
    ]
}

const ops: CarritoOps = {
    add: (product: Producto) => {},
    remove: (id: number) => {},
    clear: () => {}
}
```

## Interfaces o tipos

Los tipos que son mas cercano a un tipo primitivo no los podemos hacer con interfaces

por ejemplo: 

```typescript
type RGB = readonly [number, number, number]
```

Las interfaces se identifican mas con los objetos y las clases pero en general se usan mas los type

```typescript
interface Clase {
    prop1: string,
    prop2: number,
    func1: (clase: Clase) => void,
    func2: () => void
}
```

## Narrowing

```typescript
// Forma muy basica de usar Narrowing
function mostrarLongitud(objeto: number | string) {
    if (typeof objeto === 'string') {
        return objeto.length
    }

    return objeto.toString().length
}


// ejemplo un poco mas avanzado
interface Mario {
    company: string,
    nombre: string,
    saltar: () => void
}


interface Sonic {
    company: string,
    nombre: string,
    correr: () => void
}


type Personaje = Sonic | Mario


// vamos a hacer una funcion para diferenciarlos sin 
// una propiedad discriminante
// Type guard
// dejame comprobar si el personaje es sonic
// esta funcion va a decir si el pj es sonic o no
// funcion que discrimina los tipos gracias a las func: correr y saltar
function checkIsSonic(personaje: Personaje): personaje is Sonic {
    return (personaje as Sonic).correr != undefined
}


function jugar(personaje: Personaje) {
    if (checkIsSonic(personaje)) {
        personaje.correr()
        return console.log(personaje.nombre)
    }

    personaje.saltar()
    return console.log(personaje.nombre)
}

//creamos instancias
const sonic: Sonic = {
    company: "SEGA",
    nombre: "Sonic el erizo",
    correr: () => console.log("¡Sonic está corriendo!")
}

const mario: Mario = {
    company: "Nintendo",
    nombre: "Mario Bros",
    saltar: () => console.log("¡Mario está saltando!")
}


jugar(sonic)
jugar(mario)
```

## Tipo Never

```typescript
function f(x: number | string) = {
    if (typeof x === 'number') {
        // x es un numero
    } else if (typeof === 'string') {
        // x es un string
    } else {
        // x es un Never
    }
}
```

## Instance of y class

```typescript
class Animal {
  nombre: string;
  constructor(nombre: string) {
    this.nombre = nombre;
  }
}

class Perro extends Animal {
  ladrar() {
    console.log("¡Guau!");
  }
}

const mascota = new Perro("Firulais");

//instanceof es para saber si mascota es una instancia de la clase perro
if (mascota instanceof Perro) {
  mascota.ladrar(); // Salida: ¡Guau!
}
```

## Modificadores de Acceso

```typescript
//public: Accesible desde cualquier lugar. Es el valor predeterminado si no se especifica un modificador.
//private: Accesible solo dentro de la clase donde se define.
//protected: Accesible dentro de la clase y en las clases que heredan de ella.

class Empleado {
  public nombre: string;
  private salario: number;
  protected departamento: string;

  constructor(nombre: string, salario: number, departamento: string) {
    this.nombre = nombre;
    this.salario = salario;
    this.departamento = departamento;
  }

  obtenerSalario(): number {
    return this.salario;
  }
}

class Gerente extends Empleado {
  constructor(nombre: string, salario: number, departamento: string) {
    super(nombre, salario, departamento);
  }

  obtenerDepartamento(): string {
    return this.departamento;
  }
}

const gerente = new Gerente("Ana", 75000, "Ventas");
console.log(gerente.nombre); // Accesible
// console.log(gerente.salario); // Error: 'salario' es privado
console.log(gerente.obtenerDepartamento()); // Accesible
```

## Interfaces en clases

```typescript
interface Volador {
  volar(): void;
}

class Pajaro implements Volador {
  volar() {
    console.log("El pájaro está volando.");
  }
}

const pajaro = new Pajaro();
pajaro.volar();
```

## Convención `.d.ts`

Los archivos de declaración `.d.ts` en TypeScript se utilizan para describir la forma de los módulos existentes (por ejemplo, bibliotecas JavaScript sin tipos). Estos archivos permiten que TypeScript entienda las estructuras y tipos de código que no está escrito en TypeScript

```typescript
// types.d.ts
export function saludar(nombre: string): string {
  return 'Hola ' + nombre + ' todo bien?'
}
```

```typescript
// app.ts
import { saludar } from "./types.d.ts";

saludar("Carlos");
```


