TypeScript Cheat Sheet 
=== 

[![NPM version](https://img.shields.io/npm/v/typescript.svg?style=flat)](https://www.npmjs.com/package/ typescript) 
[![Downloads](https://img.shields.io/npm/dm/typescript.svg?style=flat)](https://www.npmjs.com/package/typescript) 
[![Repo Dependents](https://badgen.net/github/dependents-repo/Microsoft/TypeScript)](https://github.com/Microsoft/TypeScript/network/dependents) 
[![Github repo](https:// badgen.net/badge/icon/Github?icon=github&label)](https://github.com/Microsoft/TypeScript) 

A quick reference that contains the most important basics, generics, methods, classes, etc. TypeScript strongly typed programming language syntax Forgot the order. A complete quick reference for beginners 
<!--rehype:style=padding-top: 12px;--> 

Getting Started Interface 
---- 

### Introduction 

TypeScript is JavaScript with typed syntax. Interfaces are built to match their runtime behavior. 

- [JavaScript Cheat List](./javascript.md) _(jaywcjlove.github.io)_ 
- [TypeScript Official Website](https://www.typescriptlang.org/) _(typescriptlang.org)_ 

### Built-in type primitives 

````ts 
any, void, 
boolean, string, number, 
undefined, null, 
unknown, never, 
bigint, symbol 
``` 

### Common built-in JS objects 

```ts 
Date, Error, 
Array, Map, Set, 
Regexp, Promise 
``` 

### Built-in 

#### Type literal 

Object: 

```ts 
{ field: string } 
``` 

Function: 

```ts 
(arg: number) => string 
` `` 

Arrays: 

```ts 
string[] or Array<string> 
``` 

Tuple: 

```ts 
[string, number] 
``` 

#### Avoid 

```` 
Object, String, Number, Boolean 
`` ` 

### General syntax 
<!--rehype:wrap-class=col-span-2--> 

```ts 
/** Optionally get attributes from existing interfaces or types (Response, HTTPAble)*/ 
interface JSONResponse extends Response, HTTPAble { 
  version: number; 
  // 👇 Append the JSDoc comment displayed in the editor 
  /** In bytes */ 
  payloadSize: number; 
  // 👇 This property may not be on the object 
  outOfStock?: boolean; 
  // 👇 Here are two ways to describe properties that are functions 
  update: (retryTimes: number) => void; 
  update(retryTimes: number): void; 
  // 👇 You can call this object via () - (functions in JS can the object being called) 
  (): JSONResponse 
  // 👇 You can use new on the object described by this Interface new 
  new(s: string): JSONResponse; 
  // 👇 Any properties not described are assumed to be present, and all properties must be numbers 
  [ key: string]: number; 
  // 👇 Tell TypeScript that a property cannot be changed 
  readonly body: string; 
} 
``` 

### Generic 
<!--rehype:wrap-class=row-span-2--> 

declaration A type that can be changed in your 

Interface```ts
interface APICall<Response> { 
  data: Response 
} 
``` 

#### Usage 

```ts 
const api: APICall<ArtworkCall> = ... 

api.data // Artwork 
``` 

You can pass the `extends` keyword Limit the types accepted by generic parameters. 

```ts 
interface APICall<Response extends { status: number }> { 
  data: Response 
} 

const api: APICall<ArtworkCall> = ... 

api.data.status 
``` 

### Overloaded 

```ts 
interface Expect { 
  (matcher: boolean): string 
  (matcher: string): boolean; 
} 
``` 

A callable Interface can have multiple definitions for different parameter sets. 

### Class consistency 

```ts 
interface Syncable { 
  sync(): void 
} 
class Account implements Syncable { ... } 
``` 

You can ensure that a class conforms to the Interface through implementation. 

### Get & Set 

objects can have custom `getter` or `setter`. 

```ts 
interface Ruler { 
  get size(): number 
  set size(value: number | string); 
} 
``` 
Usage```ts 

const 
r: Ruler = ... 
r.size = 12 
r.size = " 36" 
``` 
### Extension by merging 
```ts 
interface APICall { 
  data: Response 
} 
interface APICall { 
  error?: Error 
} 
``` 
Interface is merged, multiple declarations will add new fields to the type definition. 
Type 
---- 
### Type vs Interface 
<!--rehype:wrap-class=row-span-2--> 
- Interface can only describe the shape of an object 
- Interface can be extended through multiple declarations 
- Type is the key to performance , the Interface comparison check can be faster. 
#### Think of types as variables 
Just like how you create variables with the same name in different scopes, types have similar semantics. 
#### Building with utility types 
TypeScript includes a number of global types that will help you complete common tasks in the type system. Check their website. 
### Primitive type 
```ts 
type SanitizedInput = string; 
type MissingNo = 404; 
``` 
Mainly used for documents 
### Object literal type 
```ts 
type Location = { 
  x: number; 
  y: number; 
}; 
``` 
### Union types 
```ts 
type Size = "small" | "medium" | "large" 
``` 
Describes one type among many options, such as a list of known strings. 
### Intersection type```ts 
type 
Location = { x: number } 
              & { y: number } 
// { x: number, y: number } 
``` 
A way to merge/extend types 
### From Value types 
```ts 
const data = { ... } 
type Data = typeof data 
``` 
Reuse types from existing JavaScript runtime values ​​via the typeof operator. 
### Return type from function 
```ts 
const createFixtures = () => { ... }




























type Fixtures = ReturnType<typeof createFixtures> 
function test(fixture: Fixtures) {} 
``` 

Reuse the return value of the function as a type. 

### From module types 

```ts 
const data: import("./data").data 
``` 

These functions are great for building libraries, describing existing JavaScript code, and you may find that in most TypeScript applications They are rarely used in . 

### Object literal syntax 
<!--rehype:wrap-class=col-span-2--> 

```ts 
type JSONResponse = { 
  version: number; // Field 
  /** In bytes */ // Append Document 
  payloadSize: number; 
  outOfStock?: boolean; // Optional 
  update: (retryTimes: number) => void; // Arrow function field 
  update(retryTimes: number): void; // Function 
  (): JSONResponse // Type is callable 
  [key: string]: number; // accepts any index 
  new (s: string): JSONResponse; // new object 
  readonly body: string; // read-only property 
} 
``` 

Terser for space saving , see the Interface Cheat Sheet for more information, everything except "static" matching. 

### Mapping type```ts 

type 
Artist = { 
  name: string, bio: string 
} 

type Subscriber<Type> = { 
  [Property in keyof Type]: 
      (newValue: Type[Property]) => void 
} 
type ArtistSub = Subscriber<Artist> 
// { name: (nv: string) => 
// void, bio: (nv: string) => void } 
``` 

Map statement similar to the type system, allowing the input type to change the structure of the new type . 

### Template union type 
<!--rehype:wrap-class=col-span-3--> 

```ts 
type SupportedLangs = "en" | "pt" | "zh"; 
type FooterLocaleIDs = "header" | "footer"; 
type AllLocaleIDs = `${SupportedLangs}_${FooterLocaleIDs}_id`; 

// "en_header_id" | "en_footer_id" 
// | "pt_header_id" | "pt_footer_id" 
// | "zh_header_id" | "zh_footer_id" 
` `` 

### Conditional type 
<!--rehype:wrap-class=col-span-3--> 

```ts 
type HasFourLegs<Animal> = Animal extends { legs: 4 } ? Animal : never 
type Animals = Bird | Dog | Ant | Wolf; 
type FourLegs = HasFourLegs<Animals> 
// Dog | Wolf 
```` 

acts as an "if statement" in the type system. Created via generics and then often used to reduce the number of options in a type union. 

Control flow analysis 
---- 

### If statement 
<!--rehype:






if ('error' in input) { 
  input // { error: ... } 
} 
``` 

#### instanceof (for classes) 

```ts 
const input = getUserInput() 
  input // number | number[ ] 

if (input instanceof Array) { 
  input // number[] 
} 
``` 

#### Type guard function (applies to anything) 

```ts 
const input = getUserInput() 
   input // number | number[] 

if (Array.isArray(input)) { 
  input // number[] 
} 
``` 

### Task 
<!--rehype:wrap-class=row-span-3--> 

```ts 
const data1 = { 
  name : "Zagreus" 
} 
// typeof data1 = { 
// name: string 
// } 
``` 

👇 Use `as const` to narrow the type 👇 

```ts 
const data2 = { 
  name: "Zagreus" 
} as const 
// typeof data1 = { 
// name: 'Zagreus' 
// } 
``` 

Tracking related variables```ts 

const 
response = getResponse() 
const isSuccessResponse = 
    res instanceof SuccessResponse 

if (isSuccessResponse) { 
  res.data // SuccessResponse 
} 
``` 

Reassign the update type 

```ts 
let data: string | number = ... 
data // string | number 
data = "Hello" 
data // string 
`` 

### Key Points 

CFA almost always uses a union, and based on The logic in the code reduces the number of types within the union. 

Most of the time CFA works within natural JavaScript Boolean logic, but there are ways to define your own functions that affect how TypeScript shrinks types. 

### Expression 

```ts 
const input = getUserInput() 
input // string | number 
const inputLength = 
  (typeof input === "string" && input.length) 
  || input 
   // input: string 
``` 

in When doing boolean operations, narrowing also occurs on the same line as the code 

### Recognized unions 

```ts 
type Responses = 
  | { status: 200, data: any } 
  | { status: 301, to: string } 
  | { status: 400, error: Error } 
``` 

#### Usage 

```ts 
const response = getResponse() 
response // Responses 
switch(response.status) { 
  case 200: return response.data 
  case 301: return redirect (response.to) 
  case 400: return response.error 
} 
``` 

### Assertion function 
<!--rehype:wrap-class=col-span-2--> 

A function that describes CFA changes that affect the current scope, because It throws instead of returning false. 

```ts 
function assertResponse(obj: any): asserts obj is SuccessResponse { 
  if (!(obj instanceof SuccessResponse)) { 
    throw new Error('Not a success!') 
  } 
}
``` 

#### Usage 

```ts 
const res = getResponse(): 
res // SuccessResponse | ErrorResponse 

// Assert function changes the current scope or throws 
assertResponse(res) 

res // SuccessResponse 
``` 

### in operator```ts 
interface A { 

x 
  : number; 
} 
interface B { 
  y: string; 
} 
function doStuff(q: A | B) { 
  if ('x' in q) { 
    // q: A 
  } else { 
    // q: B 
  } 
} The 
``` 
operator can safely check whether an attribute exists on an object. It is usually also used as a type guard 
Class 
---- ### Create 
a class 
instance```ts 
class ABC { ... } 
const abc = new ABC() 
```` 
The parameters of new ABC come from the constructor. 
#### private x with #private 
prefixed with private is a type-only addition and has no impact at runtime. Code outside the class can enter the project under the following circumstances: 
```ts 
class Bag { 
  private item: any 
} 
``` 
Vs #private is runtime private and enforced internally by the JavaScript engine, it can only be Intra-class access: 
```ts 
class Bag { #item: any } 
``` 
#### "this" function on Class 
The value of 'this' inside the function depends on how the function is called. It's not guaranteed to always be an instance of a class you might use in other languages. 
You can use this parameter, use the binding function, or the arrow function to solve the problem. 
#### Types and Values 
​​A class can be used as both a type and a value. 
```ts 
const a:Bag = new Bag() 
``` 
So, be careful not to do this: 
```ts 
class C implements Bag {} 
``` 
### General syntax 
<!--rehype:wrap-class =col-span-2--> 
```ts 
// Ensure that the class conforms to a set of interfaces or types ┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈▶┈┈╮ 
/
​ 
  ​/ A field 
  displayName?: boolean; // Optional field 
  name!: string; // 'Trust me, where is it' field 
  #attributes: Map<any, any>; // Private field 
  roles = ["user"] ; // Field with default value 
  readonly createdAt = new Date() // Read-only field with default value 
  // 👇 Code calls "new" 
  constructor(id: string, email: string) { 
    super(id); 
    // 👇 In `strict: true`, this code is checked against the field to make sure it is set correctly 
    this.email = email; 
    // .... 
  }; 
  // 👇 How to describe class methods (and arrow function fields) 
  setName( name: string) { this.name = name } 
  verifyName = (name: string) => { /* ... */ } // 👇 Function 
  sync() 
  with 2 overloaded definitions : Promise<{ ... }> 
  sync(cb: ((result: string) => void)): void 
  sync(cb?: ((result: string) => void)): void | Promise<{ ... }> {} 
  // 👇 Getters and setters 
  get accountID() { } 
  set accountID(value: string) { }






















  // 👇 Private access is only for this class, protected allowed subclasses. For type checking only, public is the default. 
  private makeRequest() { ... } 
  protected handleRequest() { ... } 
  // 👇 Static field/method 
  static #userCount = 0; 
  static registerUser(user: User) { ... } 
  // 👇 Used to set static Static block of variables. 'this' refers to the static class 
  static { this.#userCount = -1 } 
} 
``` 

### Generics 

declare a type that can be changed in your class method. 

```ts 
class Box<Type> { 
  contents: Type 
  constructor(value: Type) { 
    this.contents = value; 
  } 
} 
const stringBox = new Box("a package") 
``` 

These features are TypeScript-specific language extensions , it may never be possible to get into JavaScript using the current syntax. 
### 

Parameter attributes```ts 
class Location { 
  constructor( 
    public x: number, 
    public y: number 
  ) {} 
} 
const loc = new Location(20, 40); 
loc.x // 20 
loc.y // 40 
``` 
TypeScript class-specific extension that automatically sets instance fields as input parameters. 
### Abstract class```ts 
abstract 
class Animal { 
  abstract getName(): string; 
  printName() { 
   console.log("Hello, " + this.getName()); 
  } 
} 
class Dog extends Animal { 
  getName() : { ... } 
} 
``` 
A class can be declared not implementable, but can be subclassed in the type system. Class members are also available. 
### Decorators and properties```ts 
import 
{ 
  Syncable, triggersSync, preferCache, 
  required 
} from "mylib" 
@Syncable 
class User { 
  @triggersSync() 
  save() { ... } 
  @preferCache(false) 
  get displayName( ) { ... } 
  update(@required info: Partial<User>) { 
    //... 
  } 
} 
You can use decorators on classes, class methods, accessors, properties, and method parameters 
. 
### Index signature 
```ts 
class MyClass { 
  // It is better to store the index data in another place 
  // rather than the class instance itself. 
  [s: string]: 
    boolean | ((s: string) => boolean); 
  check(s: string) { 
    return this[s] as boolean; 
  } 
} 
``` 
Classes can declare index signatures, as with other object types The index signature is the same. 
### Declare the generic ```ts 
on forwardRef 
export const Wrapper = forwardRef( 
  <T extends object> 
( 
  props: RootNodeProps<T>, 
  ref: React.LegacyRef<HTMLDivElement> 
) => { 
  return ( 
    <div ref= {ref}></div> 
  ); 
} 
``` 
Utility type 
---- 
### Awaited\<Type> 
```ts 
type A = Awaited<Promise<string>>;



















// type A = string 

type B = Awaited<Promise<Promise<number>>>; 
// type B = number 

type C = Awaited<boolean|Promise<number>>; 
// type C = number | boolean 
``` 

This type is intended to simulate operations such as await in async functions or the .then() method on Promises - specifically the way they unwrap Promises recursively. 

### Required\<Type> 

```ts 
interface Props { 
  a?: number; 
  b?: string; 
} 

const obj: Props = { a: 5 }; 
const obj2: Required<Props> = { a: 5 } ; 
// ❌ Property 'b' is missing in type '{ a: number;' }' 
// but is required in type 'Required<Props>'. 
``` 

Make all properties in Type required 

### Readonly\<Type> 

```ts 
interface Todo { 
  title: string; 
} 
const todo: Readonly<Todo> = { 
  title: "Delete inactive users", 
}; 
todo.title = "Hello"; 
// ❌ Cannot be assigned to "title" because it is a read-only property. 

function freeze<Type>(obj: Type) 
            : Readonly<Type>; 
``` 

Set all properties in Type to **read-only** 

### Partial\<Type> 

```ts 
interface Todo { 
  title: string; 
  description: string; 
} 
function updateTodo( 
  todo: Todo, 
  fieldsToUpdate: Partial<Todo> 
) { 
  return { ...todo, ...fieldsToUpdate }; 
} 
const todo1 = { 
  title: "organize desk", 
  description: " clear clutter", 
}; 
const todo2 = updateTodo(todo1, { 
  description: "throw out trash", 
}); 
``` 

Set all properties in `Type` to optional 

### Record\<Keys, Type> 

```ts 
interface CatInfo { 
  age: number; 
  breed: string; 
} 

type CatName = "miffy" | "boris"; 
const cats: Record<CatName, CatInfo> = { 
  miffy: {age:10, breed: "Persian" }, 
  boris: {age:5, breed: "Maine Coon" }, 
}; 

cats.boris; 
// 👉 const cats: Record<CatName, CatInfo> 
``` 

Construct a type with a set of properties Type of Keys type 

### Pick\<Type, Keys> 

```ts 
interface Todo { 
  name: string; 
  description: string; 
  completed: boolean; 
} 
type TodoPreview = Pick< 
  Todo, "name" | "load" 
>; 
const todo: TodoPreview = { 
  name: "Clean room", 
  load: false, 
}; 

todo; 
 // 👉 const todo:



// 👉 type T0 = "b" | "c" 

type T1 = Exclude<"a"|"b"|"c", "a" | "b">; 
// 👉 type T1 = "c" 

type T2 = Exclude<string | number | 
    (() => void), Function>; 
// 👉 type T2 = string | number 
`` 

`Exclude** those types from `UnionType` that can be assigned to `ExcludedMembers` 

# ## Extract\<Type, Union> 

```ts 
type T0 = Extract< 
  "a" | "b" | "c", "a" | "f" 
>; 
// type T0 = "a" 
type T1 = Extract< 
  string | number | (() => void), 
  Function 
>; 
// type T1 = () => void 
``` 

Constructs a Union by **extracting** all union members assignable to Union from Type type. 

### NonNullable\<Type> 

```ts 
type T0 = NonNullable< 
  string | number | undefined 
>; 
// type T0 = string | number 

type T1 = NonNullable< 
  string[] | null | undefined 
>; 
// type T1 = string[] 
`` 

Constructs a type by **exclude** null and undefined from Type. 

### Omit\<Type, Keys> 

```ts 
interface Todo { 
  name: string; 
  completed: boolean; 
  createdAt: number; 
} 
 
type TodoPreview = Omit<Todo, "name">; 

const todo: TodoPreview = { 
  completed: false, 
  createdAt: 1615544252770, 
}; 
 
todo; 
 // 👉 const todo: TodoPreview 
`` 

Constructs a type with a Type property, except for the properties in the type Keys. 

### Parameters\<Type> 

```ts 
declare function f1( 
  arg: { a: number; b: string } 
): void; 

type T0 = Parameters<() => string>; 
// type T0 = [] 
type T1 = Parameters<(s: string) => void>; 
// type T1 = [s: string] 
type T2 = Parameters<<T>(arg: T) => T>; 
// type T2 = [arg : unknown] 
type T3 = Parameters<typeof f1>; 
// type T3 = [arg: { 
// a: number; 
// b: string; 
// }] 
type T4 = Parameters<any>; 
// type T4 = unknown[] 
type T5 = Parameters<never>; 
// type T5 = never 
``` 

Constructs a tuple type from the type used in the parameters of the function type Type. 

### ConstructorParameters\<Type> 

```ts 
type T0 = ConstructorParameters< 
  ErrorConstructor 
>; 
// type T0 = [message?:
// ] 
type T3 = ConstructorParameters<any>; 
// type T3 = unknown[] 
``` 

Constructs a tuple or array type from the type of the constructor type. It produces a tuple type containing all parameter types (type never if Type is not a function). 

### Intrinsic string operation types 

#### Uppercase\<StringType> 

```ts 
type Greeting = "Hello, world" 
type ShoutyGreeting = Uppercase<Greeting> 
// type ShoutyGreeting = "HELLO, WORLD" 

type ASCIICacheKey<Str extends string> = `ID-${Uppercase<Str>}` 
type MainID = ASCIICacheKey<"my_app"> 
// type MainID = "ID-MY_APP" 
``` 

Convert each character** in the string to uppercase **Version. 

#### Lowercase\<StringType> 

```ts 
type Greeting = "Hello, world" 
type QuietGreeting = Lowercase<Greeting> 
// type QuietGreeting = "hello, world" 

type ASCIICacheKey<Str extends string> = `id-$ {Lowercase<Str>}` 
type MainID = ASCIICacheKey<"MY_APP"> 
// type MainID = "id-my_app" 
``` 

Converts each character in the string to its equivalent **lowercase**. 

#### Capitalize\<StringType> 

```ts 
type LowercaseGreeting = "hello, world"; 
type Greeting = Capitalize<LowercaseGreeting>; 
// type Greeting = "Hello, world" 
``` 

replace the first character in the string characters are converted to their **uppercase equivalent**. 

#### Uncapitalize\<StringType> 

```ts 
type UppercaseGreeting = "HELLO WORLD"; 
type UncomfortableGreeting = Uncapitalize<UppercaseGreeting>; 
// type UncomfortableGreeting = "hELLO WORLD" 
``` 

Change the first character in the string Convert to the equivalent **lowercase**. 

### ReturnType\<Type> 

```ts 
declare function f1(): { 
  a: number; b: string 
}; 

type T0 = ReturnType<() => string>; 
// type T0 = string 

type T1 = ReturnType <(s: string) => void>; 
// type T1 = void 

type T2 = ReturnType<<T>() => T>; 
// type T2 = unknown 

type T3 = ReturnType<< 
  T extends U, U extends number[] 
>() => T>; 
// type T3 = number[] 

type T4 = ReturnType<typeof f1>; 
// type T4 = { 
// a: number; 
// b: string; 
// } 

type T5 = ReturnType<any>; 
// type T5 = any 

type T6 = ReturnType<never>; 
// type T6 = never 
``` 

Constructs a type consisting of the **return type** of the function Type. 

### ThisType\<Type> 

```ts 
type ObjectDescriptor<D, M> = { 
  data?: D; 
  // The type of "this" in the method is D & M 
  methods?:
 
  let methods: object = desc.methods || {}; 
  return { ...data, ...methods } as D & M; 
} 
 
let obj = makeObject({ 
  data: { x: 0, y: 0 }, 
  methods : { 
    moveBy(dx: number, dy: number) { 
      this.x += dx; // Strongly typed this 
      this.y += dy; // Strongly typed this 
    }, 
  }, 
}); 
 
obj.x = 10; 
obj.y = 20; 
obj.moveBy(5, 5); 
``` 

This utility does not return the converted type. Instead, it is used as a marker of the context's this type. Note that the [noImplicitThis](https://www.typescriptlang.org/tsconfig#noImplicitThis) flag must be enabled to use this utility. 

### InstanceType\<Type> 

```ts 
class C { 
  x = 0; 
  y = 0; 
} 
type T0 = InstanceType<typeof C>; 
// type T0 = C 
type T1 = InstanceType<any>; 
// type T1 = any 
type T2 = InstanceType<never>; 
// type T2 = never 
``` 

Constructs a type consisting of the instance type of the constructor in Type. 

### ThisParameterType\<Type> 

```ts 
function toHex(this: Number) { 
  return this.toString(16); 
} 
 
function numberToString( 
  n: ThisParameterType<typeof toHex> 
) { 
  return toHex.apply(n); 
} 
``` 

Extract the type of the `this` parameter of the function type. If the function type does not have a `this` parameter, it is unknown. 

### OmitThisParameter\<Type> 

```ts 
function toHex(this: Number) { 
  return this.toString(16); 
} 
const fiveToHex 
  : OmitThisParameter<typeof toHex> 
  = toHex.bind(5); 

console.log(fiveToHex ()); 
``` 

Remove this parameter from Type. If Type does not explicitly declare this parameter, the result is simply Type. Otherwise, create a new function type from Type without this parameter. Generics are removed and only the last overload signature is propagated into the new function type. 

JSX 
---- 

### Introduction to JSX 

The JSX specification is an XML-like syntax extension to ECMAScript. 

- Name your files with a `.tsx` extension 
- Enable the `jsx` option 
- Disallow angle bracket type assertions in `.tsx` files. 
- [JSX Specification](https://facebook.github.io/jsx/) 

### as operator 

```ts 
const foo = <foo>bar; 
// ❌ Points are not allowed in .tsx 👆 files Bracket type assertion. 

const foo = bar as foo; The 
` 

as` operator is available in both `.ts` and `.tsx` files and behaves in the same **angle bracket** style of type assertion. 

### Value-based elements 

```tsx 
import MyComponent from "./myComponent"; 

<MyComponent />; // ok 
<SomeOtherComponent />; // ❌ error 
``` 

Value-based elements are only identified by the range character search. 

### Intrinsic elements 

```tsx 
declare namespace JSX { 
  interface IntrinsicElements { 
    foo: any; 
  } 
} 
<foo />; // ok 
<bar />; // error 
```

\<bar /> is not specified on JSX.IntrinsicElements. 

```tsx 
declare namespace JSX { 
  interface IntrinsicElements { 
    [elemName: string]: any; 
  } 
} 
``` 

### Function component 
<!--rehype:wrap-class=col-span-2--> 

``` tsx 
interface 
FooProp 
{ 
name 
  : 
  string 
  ; 
  ​; 
} 
const Button = (prop: { value: string }, context: { color: string }) => ( 
  <button /> 
); 
```` 
The component is defined as a JavaScript function, and its first parameter is a props object. TS enforces that its return type must be assignable to JSX.Element. 
### Function component overloading```tsx 
interface 
CeProps { 
  children: JSX.Element[] | JSX.Element; 
} 
interface HomeProps extends CeProps { 
  home: JSX.Element; 
} 
interface SideProps extends CeProps { 
  side: JSX.Element | string; 
} 
function Dog(prop:HomeProps): JSX.Element; 
function Dog(prop:SideProps): JSX.Element; 
function Dog(prop:CeProps): JSX.Element { 
  // ... 
} 
``` 
## # Function subcomponent 
<!--rehype:wrap-class=col-span-2--> 
```tsx 
interface MenuProps extends React.LiHTMLUListElement> { ... }; 
const InternalMenu = React.forwardRef<HTMLUListElement, MenuProps>((props, ref) => ( 
  <ul {...props} ref={ref} /> 
)); 
type MenuComponent = typeof InternalMenu & { 
  Item: typeof MenuItem; // MenuItem function component 
  SubMenu: typeof SubMenu ; // SubMenu function component 
}; 
const Menu: MenuComponent = InternalMenu as unknown as MenuComponent; 
Menu.Item = MenuItem; 
Menu.SubMenu = SubMenu; 
<Menu.Item /> // ✅ ok 
<Menu.SubMenu /> // ✅ ok 
`` 
### Valid component 
<!--rehype:wrap-class=row-span-2--> 
``tsx 
declare namespace JSX { 
  interface ElementClass { 
    render: any; 
  } 
} 
class MyComponent { 
  render() {} 
} 
function MyFactoryFunction() { 
  return { render: () => {} }; 
} 
<MyComponent />; // ✅ Valid class component 
<MyFactoryFunction />; // ✅ Valid function component 
```` 
element instance type must be Can be assigned to `JSX.ElementClass`, otherwise an error will result. 
```tsx 
class NotAValidComponent {} 
function NotAValidFactoryFunction() { 
  return {}; 
}




 
 
 










<NotAValidComponent />; // ❌ error 
<NotAValidFactoryFunction />; // ❌ error 
``` 

By default, `JSX.ElementClass` is {}, but it can be extended to limit the use of `JSX` to Only types that conform to the appropriate interface. 

### Class component 
<!--rehype:wrap-class=col-span-2--> 

```ts 
type Props = { 
  header: React.ReactNode; 
  body: React.ReactNode; 
}; 

class MyComponent extends React. Component<Props, {}> { 
  render() { 
    return ( 
      <div> 
        {this.props.header} 
        {this.props.body} 
      </div> 
    ); 
  } 
} 

<MyComponent header={<h1>Header</ h1>} body={<i>body</i>} /> 
``` 

### Generic component 
<!--rehype:wrap-class=col-span-2--> 

```tsx 
// A generic component 
type SelectProps<T> = { items: T[] }; 
class Select<T> extends React.Component<SelectProps<T>, any> {} 

// Use 
const Form = () => <Select< string> items={['a', 'b']} />; 
``` 

### Function component ref 
<!--rehype:wrap-class=col-span-3--> 

```tsx 
import { FC, ForwardedRef, forwardRef, PropsWithRef } from "react"; 

function InternalProgress(props: ProgressProps, ref?: ForwardedRef<HTMLDivElement>) { 
  return ( 
    <div {...props} ref={ref}> 
      {props.children } 
    </div> 
  ) 
} 

export interface ProgressProps extends React.DetailedHTMLProps<React.HTMLAttributes<HTMLDivElement>, HTMLDivElement> {} 
export const Progress: FC<PropsWithRef<ProgressProps>> = forwardRef<HTMLDivElement>(InternalProgress) 
```` 

## # Component 'as' attribute 
<!--rehype:wrap-class=col-span-2--> 

```tsx 
import React, { ElementType, ComponentPropsWithoutRef } from "react"; 

export const Link = <T extends ElementType< any> = "a">( 
  props: { as?: T; } & ComponentPropsWithoutRef<T> 
) => { 
  const Comp = props.as || "a"; 
  return <Comp {...props}></ Comp>; 
}; 


<Link as="div">Text</Link>; 
``` 

Allow custom `React` components to be passed in, or `div`, `a` tag 

### components to be passed as 

Props`` `tsx 
type RowProps = { 
  element: React.ElementType<{ 
    className?: string; 
  }>; 
} 
const Row = (props: RowProps) => { 
  return ( 
    <props.
 



type Capitalize<T extends string> = T extends `${infer U}${infer V}`
  ? `${Uppercase<U>}${V}`
  : T
type capitalized = Capitalize<"hello world"> // Hello world
```

也可以在 infer 中使用条件约束（`extends`）

```ts
type SomeBigInt = "100" extends `${infer U extends bigint}` ? U : never;
// 100n
```

### keyof 取 interface 的键

```ts
interface Point { x: number; y: number; }
 
// type keys = "x" | "y"
type keys = keyof Point;

type Arrayish = {
    [n: number]: unknown;
};
type A = keyof Arrayish; 
// type A = number
```

### 两个数组合并成一个新类型
<!--rehype:wrap-class=col-span-2 row-span-2-->

```ts
const named = ["aqua", "aquamarine", "azure"] as const;
const hex = ["#00FFFF", "#7FFFD4", "#F0FFFF"] as const;

type Colors = {
  [key in (typeof named)[number]]: (typeof hex)[number];
};
// Colors = {
//   aqua: "#00FFFF" | "#7FFFD4" | "#F0FFFF"; 
//   .... 
// }
```

### 索引签名

```ts
interface NumberOrString {
  [index: string]: string | number;
  length: number;
  name: string;
}
```

### 只读元组类型

```ts
const point = [3, 4] as const
// type 'readonly [3, 4]'
```

### 从数组中提取类型

```ts
type Point = { x: number; y: number; }
type Data = Point[];
// Data 是个数组，提取里面的元素类型
type PointDetail = Data[number];
// type PointDetail = { x: number; y: number; }
```
<!--rehype:className=wrap-text-->

### satisfies
<!--rehype:wrap-class=row-span-3-->

`satisfies` 允许将验证表达式的类型与某种类型匹配，而无需更改该表达式的结果类型。

```ts
type Colors = 'red' | 'green' | 'blue';
type RGB = [
  red: number,
  green: number,
  blue: number
];
type Palette = Record<Colors, string | RGB>

const palette: Palette = {
  red: [255, 0, 0],
  green: '#00ff00',
  blue: [0, 0, 255],
};

// 通常的方式会推导出 redComponent 为
// => string | number | undefined
const redComponent = palette.red.at(0);
```

#### 使用 satisfies

```ts
const palette = {
  red: [255, 0, 0],
  green: '#00ff00',
  blue: [0, 0, 255],
} satisfies Record<Colors, string | RGB>

// undefined | number
const redComponent = palette.red.at(0) 
``` 
<!--rehype:className=wrap-text--> 

### Generic instantiation expression 
<!--rehype:wrap-class=row-span -3--> 

When not used: 

```ts 
const errorMap: Map<string, Error> 
        = new Map() 
// Or use type to define an alias 
type ErrorMapType = Map<string, Error> 
``` 

Use generic Type instantiation expression: 

```ts 
const ErrorMap = Map<string, Error> 
const errorMap = new ErrorMap() 
``` 

#### Generic instantiation function 

```ts 
function makeBox<T>(value: T) { 
    return { value }; 
} 
``` 

--- 

Not used: 

```ts 
function makeHammerBox(hammer: Hammer) { 
  return makeBox(hammer); 
} 
// or... 
const makeWrenchBox: (wrench: Wrench ) 
    => Box<Wrench> = makeBox; 
``` 

Use: ` 
` 

`ts 
const makeStringBox = makeBox<string>; 
makeStringBox(42); 
``` 

### Identify global modification module```ts 
declare global { 
  interface String { 
    fancyFormat(opts: FancyOption): string; 
  } 
} 
export interface FancyOption { 
  fancinessLevel: number; 
} 
``` 
### Get the type of array element```ts 
const MyArray = [ 
{ 
  name: "Alice", age: 15 }, 
  { name: "Bob", age: 23 }, 
  { name: "Eve", age: 38 }, 
]; 
type Person = typeof MyArray[number]; 
// type Person = { 
// name: string; 
// age: number; 
// } 
type Age = typeof MyArray[number]["age"]; 
// type Age = number 
type Age2 = Person["age"]; 
// type Age2 = number 
```` 
## # Generic derivation of list literal 
```ts 
const a = <T extends string>(t: T) => t; 
const b = <T extends number>(t: T) => t; 
const c = < T extends boolean>(t: T) => t; 
const d = a("a"); // const d: 'a' 
const e = b(1); // const d: 1 
const f = c( true); // const d: true 
// The type of t here uses an expansion operation 
const g = 
  <T extends string[]>(t: [...T]) => t; 
// The type becomes [ "111", "222"] 
const h = g(["111", "222"]); 
``` 
### Object.keys type declaration 
<!--rehype:wrap-class=col-span- 2--> 
```ts 
const keys = Object.keys(options) as (keyof typeof options)[]; 
keys.forEach(key => {
  if (options[key] == null) {
    throw new Error(`Missing option ${key}`);
  }
});
```
.d.ts 模版
---



 










### Module: Plugin 

For example, when you want to use JavaScript code that extends another library```ts 

import 
{ greeter } from "super-greeter"; 
// Normal welcome API 
greeter(2); 
greeter("Hello world "); 
// Now we extend the object at runtime with a new function 
import "hyper-super-greeter"; 
greeter.hyperGreet(); 
``` 

Definition of "`super-greeter`": 

​​```ts 
/* This example shows how to set multiple overloads for your function */ 
export interface GreeterFunction { 
  (name: string): void 
  (time: number): void 
} 
/* This example shows how to export an interface-specified function */ 
export const greeter : GreeterFunction; 
``` 

We can extend an existing module like this: 

```ts 
/* Import the module this module is added to*/ 
import { greeter } from "super-greeter"; 
/* Declare the same module as the one imported above same module, then we extend the existing declaration of greeter function */ 
export module "super-greeter" { 
  export interface GreeterFunction { 
    /** Greets even better! */ 
    hyperGreet(): void; 
  } 
} 
``` 
<!- -rehype:className=wrap-text--> 

### Global library template Global .d.ts 
<!--rehype:wrap-class=row-span-2--> 

The global library may look like the following: 

``` ts 
function createGreeting(s) { 
  return "Hello, " + s; 
} 
``` 

Or like this: 

```ts 
window.createGreeting = function (s) { 
  return "Hello, " + s; 
}; 
``` 

< pur>Type declaration example</pur> 

```ts 
/* Can be used as myLib(3) These call signatures are included here*/ 
declare function myLib(a: string): string; 
declare function myLib(a: number): number ; 
/* If you want the name of this library to be a valid type name, you can do so here. For example, this allows us to write 'var x: myLib'; Make sure this actually makes sense! If not, just remove this declaration and add the type inside the namespace below */ 
interface myLib { 
  name: string; 
  length: number; 
  extras?: string[]; 
} 
/* if your library exposes on global variables Properties, please place them here. You should also put types (interfaces and type aliases) here */ 
declare namespace myLib { 
  // We can write 'myLib.timeout = 50;' 
  let timeout: number; 
  // We can access 'myLib.version' but Can't change it 
  const version: string; 
  // We can create some class or reference by 'let c = new myLib.Cat(42)' for example 'function f(c: myLib.Cat) { ... } 
  class Cat { 
    constructor (n: number); 
    // We can read 'c.age' from a 'Cat' instance 
    readonly age: number; 
    // We can call 'c.purr()' from a 'Cat' instance 
    purr(): void ; 
  } 
  // We can declare the variable as 
  // 'var s: myLib.CatSettings = { weight: 5, name: "Maru" };' 
  interface CatSettings { 
    weight: number; 
    name: string; 
    tailLength?:
  // or 'const v: myLib.VetID = "bob";' 
  type VetID = string | number; 
  // We can call 'myLib.checkCat(c)' or 'myLib.checkCat(c, v);' 
  function checkCat (c: Cat, s?: VetID); 
} 
``` 
<!--rehype:className=wrap-text--> 

### Module: Function 
<!--rehype:wrap-class=row-span-2 --> 

```ts 
import greeter from "super-greeter"; 
greeter(2); 
greeter("Hello world"); 
``` 

To handle imports via `UMD` and modules: 

```ts 
/* if this The module is a UMD module and when loaded outside the module loader environment exposes the global variable "myFuncLib", declare the global variable here. Otherwise, delete this declaration */ 
export as namespace myFuncLib; 
/* This declaration specifies that the function is an object exported from a file */ 
export = Greeter; 
/* This example shows how to set up multiple overloads for your function */ 
declare function Greeter(name: string): Greeter.NamedReturnType; 
declare function Greeter(length: number): Greeter.LengthReturnType; 
``` 
<!--rehype:className=wrap-text--> 

If you also want to use this function from your module For public types, you can put them in this block. Typically you will want to describe the shape of a function's return type; as in this example, the type should be declared here. Note that if you decide to include this namespace, the module may be imported incorrectly as a namespace object. Unless `--esModuleInterop` is turned on: `import * as x from '[~THE MODULE~]';` Wrong! Don't do this! 

```ts 
declare namespace Greeter { 
  export interface LengthReturnType { 
    width: number; 
    height: number; 
  } 
  export interface NamedReturnType { 
    firstName: string; 
    lastName: string; 
  } 
  /** 
   * If the module also has attributes, declare them here they. For example, this declaration says that this code is legal: 
   * import f = require('super-greeter'); 
   * console.log(f.defaultName); 
   */ 
  export const defaultName: string; 
  export let defaultLength: number; 
} 
` `` 
<!--rehype:className=wrap-text--> 

### Module: Class 

For example, when you want to use `JavaScript` code as shown below: 

```ts 
const Greeter = require("super -greeter"); 
const greeter = new Greeter(); 
greeter.greet(); 
``` 

To handle imports via `UMD` and modules: 

```ts 
export as namespace "super-greeter"; 
/* This declaration specifies The class constructor is an object exported from the file */ 
export = Greeter; 
/* Write the methods and properties of the module in this class */ 
declare class Greeter { 
  constructor(customGreeting?: string); 
  greet: void; 
  myMethod(opts: MyClass.MyClassMethodOptions): number; 
} 
``` 
<!--rehype: 

className=wrap-text--> If you also want to expose types from your module, you can put them in this block, if you decide to include this namespace, the module may be imported as a namespace object incorrectly , unless --esModuleInterop is turned on: 
 `import * as x from '[~THE MODULE~]';` Wrong! Do not do this! 

```ts 
declare namespace MyClass { 
  export interface MyClassMethodOptions { 
    width?: number;
    height?: number; 
  } 
} 
``` 
<!--rehype:className=wrap-text--> 

JSDoc Reference 
--- 

### @type 
<!--rehype:wrap-class=row-span-2- -> 

```javascript 
/** @type {string} */ 
var s; 
/** @type {Window} */ 
var win; 
/** @type {PromiseLike<string>} */ 
var promisedString; 
// You can specify HTML elements with DOM attributes 
/** @type {HTMLElement} */ 
var elm = document.querySelector(selector); 
elm.dataset.myData = ""; 
/** @type {number[]} */ 
var ns; 
/** @type {Array.<number>} */ 
var jsdoc; 
/** @type {Array<number>} */ 
var nas; 
/** @type {string | boolean} */ 
var sb ; 
/** @type {{ a: string, b: number }} */ 
var var9; 
/** 
 * Map-like object that maps any "string" attribute to "number" 
 * @type {Object.<string , number>} 
 */ 
var stringToNumber; 
/** @type {Object.<number, object>} */ 
var arrayLike; 
/** @type {function(string, boolean): number} Closure syntax */ 
var sbn; 
/** @type {(s: string, b: boolean) => number} TypeScript syntax */ 
var sbn2; 
/** @type {Function} */ 
var fn7; 
/** @type {function} */ 
var fn6; 
/** 
 * @type {*} - can be 'any' type 
 */ 
var star; 
/** 
 * @type {?} - unknown type (same as 'any') 
 */ 
var question; 
/** @type {number | string} */ 
var numberOrString = Math.random() < 0.5 ? "hello" : 100; 
var typeAssertedNumber = /** @type {number} */ (numberOrString); 
let one = /** @ type {const} */(1); 
``` 

### Import 

type```javascript 
// @filename: types.d.ts 
export type Pet = { 
  name: string, 
}; 
// @filename: main. js 
/** @param { import("./types").Pet } p */ 
function walk(p) { 
  console.log(`Walking ${p.name}...`); 
} 
``` 

Import Types can be used in type alias declarations 

```javascript 
/** 
 * @typedef {import("./types").Pet} Pet 
 */ 
/** @type {Pet} */ 
var myPet; 
myPet.name; 
``` 

If you don't know the type, or if it has an annoyingly large type, `import types` can be used to get the type of the value from the module: 

```javascript 
/** 
 * @type {typeof import(" ./accounts").userAccount} 
 */ 
var x = require("./accounts").userAccount; 
``` 

### @param and @returns 

```javascript 
/**
 * @param {string} p1 - a string parameter 
 * @param {string=} p2 - an optional parameter (Google Closure syntax) 
 * @param {string} [p3] - another optional parameter (JSDoc syntax) 
 * @ param {string} [p4="test"] - Optional parameter with default value 
 * @returns {string} This is the result 
 */ 
function stringsStrings(p1, p2, p3, p4) { 
  // TODO 
} 
``` 

Same , for the return type of the function: 

```javascript 
/** 
 * @return {PromiseLike<string>} 
 */ 
function ps() {} 
 
/** 
 * @returns {{ a: string, b: number }} - OK Use "@returns" and "@return" 
 */ 
function ab() {} 
``` 

### @typedef, @callback, and @param 
<!--rehype:wrap-class=col-span-2 row- span-2--> 

```javascript 
/** 
 * @typedef {Object} SpecialType - Creates a new type named "SpecialType" 
 * @property {string} prop1 - The string property of SpecialType 
 * @property {number} prop2 - a numeric property for SpecialType 
 * @property {number=} prop3 - an optional numeric property for SpecialType 
 * @prop {number} [prop4] - an optional numeric property for SpecialType 
 * @prop {number} [prop5=42] - has Optional numeric property of SpecialType with default value 
 */ 
 
/** @type {SpecialType} */ 
var specialTypeObject; 
specialTypeObject.prop3; 
``` 

You can use object or Object in the first line 

```javascript 
/** 
 * @ typedef {object} SpecialType1 - creates a new type called "SpecialType" 
 * @property {string} prop1 - a string property of SpecialType 
 * @property {number} prop2 - a numeric property of SpecialType 
 * @property {number=} prop3 - Optional numeric properties for SpecialType 
 */ 
 
/** @type {SpecialType1} */ 
var specialTypeObject1; 
``` 

**@param** Allows similar syntax for one-time type specifications. Note that nested property names must be prefixed with the parameter name: 

```javascript 
/** 
 * @param {Object} options - same shape as SpecialType above 
 * @param {string} options.prop1 
 * @param {number } options.prop2 
 * @param {number=} options.prop3 
 * @param {number} [options.prop4] 
 * @param {number} [options.prop5=42] 
 */ 
function special(options) { 
  return (options. prop4 || 1001) + options.prop5; 
} 
``` 

**@callback** is similar to **@typedef**, but it specifies the function type instead of the object type: 

```javascript 
/** 
 * @ callback Predicate 
 * @param {string} data 
 * @param {number} [index] 
 * @returns {boolean} 
 */ 
 
/** @type {Predicate} */ 
const ok = (s) => !(s.length % 2); 
``` 

Of course, any of these types can be declared in a single line **@typedef** using TypeScript syntax: 

```javascript 
/** @typedef {{ prop1: string, prop2: string, prop3?: number }} SpecialType */
/** @typedef {(data: string, index?: number) => boolean} Predicate */ 
``` 

### @template 

You can use the **@template** tag to declare type parameters. This allows you to create generic functions, classes or types: 

```javascript 
/** 
 * @template T 
 * @param {T} x - generic parameters flowing to the return type 
 * @returns {T} 
 */ 
function id(x ) { 
  return x; 
} 
 
const a = id("string"); 
const b = id(123); 
const c = id({}); 
``` 

Use commas or multiple labels to declare multiple type parameters: 

` ``javascript 
/** 
 * @template T,U,V 
 * @template W,X 
 */ 
``` 

You can also specify type constraints before the type parameter name. Only the first type parameter in the list is constrained: 

```javascript 
/** 
 * @template {string} K - K must be a string or a string literal 
 * @template {{ serious(): string }} Seriousalizable - There must be a serious method 
 * @param {K} key 
 * @param {Seriousalizable} object 
 */ 
function seriousalize(key, object) { 
  // ???? 
} 
``` 

Finally, you can specify default values ​​for type parameters : 

```javascript 
/** @template [T=object] */ 
class Cache { 
  /** @param {T} initial */ 
  constructor(T) { 
  } 
} 
let c = new Cache() 
``` 

CLI 
- -- 

### Using CLI 

```bash 
# Run compile based on fs looking backwards at tsconfig.json 
$tsc 
# Use compiler defaults to only emit JS for index.ts 
$ tsc index.ts 
# Use defaults for folders Emit JS for any .ts file in src 
$ tsc src/*.ts 
# Emit referenced files using the compiler settings in tsconfig.production.json 
$ tsc --project tsconfig.production.json 
# Emit d.ts for js files File, compiler option showing boolean 
$tsc index.js --declaration --emitDeclarationOnly 
# Emit a single .js file from two files by compiler option taking string argument 
$tsc app.ts util.ts --target esnext --outfile index.js 
``` 
<!--rehype:className=wrap-text--> 

### Compiler options 
<!--rehype:wrap-class=col-span-2--> 

:- | -- 
:- | -- 
`--all` _boolean_ | Show all compiler options 
`--generateTrace` _string_ | Generate event traces and type lists 
`--help` _boolean_ | Provide local information about CLI 
help`-- init` _boolean_ | Initialize the TypeScript project and create the tsconfig.json file 
`--listFilesOnly` _boolean_ | Print filenames as part of compilation, then stop processing 
`--locale` _string_ | Set the messaging language from TypeScript. This does not affect emitting 
`--project` _string_ | Compile a project given the path to its configuration file, or a folder with 'tsconfig.json' 
`--showConfig` _boolean_ | Print the final configuration instead of building 
`--version` _boolean_ | Print compiler version 
<!--rehype:className=left-align--> 

### Build options 

:- | -- 
:- | -- 
`--build` _boolean_ | Build one or more projects and Its dependencies (if out of date) 
`--clean` _boolean_ | Remove the output of all projects
`--dry` _boolean_ | Show what will be built (or removed if specified with "--clean") 
`--force` _boolean_ | Build all projects, including those that appear to be the latest 
`--verbose` _boolean_ | Enable verbose logging 
<!--rehype:className=style-list--> 

### Listening options 
<!--rehype:wrap-class=col-span-2--> 

:- | -- 
:- | -- 
`--excludeDirectories` _list_ | Remove the directory list from the watch process 
`--excludeFiles` _list_ | Remove the file list from the watch mode process 
`--fallbackPolling` _fixedinterval_, _priorityinterval_, _dynamicpriority_, _fixedchunksize_ | Specify when the system has run out Methods that observers should use when using native file watchers 
`--synchronousWatchDirectory` _boolean_ | Synchronously invoke callbacks and update the status of the directory watcher on platforms that do not natively support recursive monitoring 
`--watch` _boolean_ | Watch input 
files` --watchDirectory` _usefsevents_, _fixedpollinginterval_, _dynamicprioritypolling_, _fixedchunksizepolling | Specify how directories are watched on systems that lack recursive file monitoring 
`--watchFile` _fixedpollinginterval_, _prioritypollinginterval_, _dynamicprioritypolling_, _fixedchunksizepolling_, _usefsevents_, _usefseventson parentdirectory_ | Specifies how TypeScript watch mode works 
< !--rehype:className=style-list--> 

TSConfig Ref 
--- 

### Can complete 90% of the tasks 
<!--rehype:wrap-class=row-span-2--> 

```js 
" compilerOptions": { 
  /* Basic options: */ 
  "esModuleInterop": true, 
  "skipLibCheck": true, 
  "target": "es2022", 
  "verbatimModuleSyntax": true, 
  "allowJs": true, 
  "resolveJsonModule": true, 
  " moduleDetection": "force", 
  /* strict*/ 
  "strict": true, 
  "noUncheckedIndexedAccess": true, 
  /* If using TypeScript for translation: */ 
  "moduleResolution": "NodeNext", 
  "module": "NodeNext", 
  /* If not using TypeScript for transpilation: */ 
  "moduleResolution": "Bundler", 
  "module": "ESNext", 
  "noEmit": true, 
  /* If your code runs in the DOM: */ 
  "lib": ["es2022", "dom", "dom.iterable"], 
  /* If your code does not run in the DOM: */ 
  "lib": ["es2022"], 
  /* If you are building a library: */ 
  "declaration": true, 
  /* If you are building the library in monorepo: */ 
  "composite": true, 
  "sourceMap": true, 
  "declarationMap": true 
} 
``` 

### Top-level configuration 

:- | -- 
: - | -- 
`files` [#](https://www.typescriptlang.org/zh/tsconfig#files) | Specifies an allowed list of files to `include` in the program 
`extends` [#](https: //www.typescriptlang.org/zh/tsconfig#extends) | Contains the path to another configuration file to `inherit` 
`include` [#](https://www.typescriptlang.org/zh/tsconfig#include) | Specify the file name or pattern array 
`exclude` to be included in the program [#](https://www.typescriptlang.org/zh/tsconfig#exclude) | Specify the parsing include An array of file names or patterns that should be skipped when using 
`references` [#](https://www.typescriptlang.org/zh/tsconfig#references) | Project references are a way of structuring a TypeScript program into smaller parts method
<!--rehype:className=style-list-arrow--> 

--- 

```js 
{ 
  "extends": "./tsconfig", 
  "compilerOptions": { 
    "strictNullChecks": false 
  } 
} 
``` 

# ## Type checking (compilerOptions) 
<!--rehype:wrap-class=row-span-3--> 

:- | -- 
:- | -- 
`allowUnreachableCode` [#](https://www.typescriptlang. org/zh/tsconfig#allowUnreachableCode) | Allow unreachable code 
`allowUnusedLabels` [#](https://www.typescriptlang.org/zh/tsconfig#allowUnusedLabels) | Allow unused labels 
`alwaysStrict` [#]( https://www.typescriptlang.org/zh/tsconfig#alwaysStrict) | Always strict 
`exactOptionalPropertyTypes` [#](https://www.typescriptlang.org/zh/tsconfig#exactOptionalPropertyTypes) | When enabled, TypeScript applies more strict What are the rules for how it handles a type or has? prefix `noFallthroughCasesInSwitch` [#](https://www.typescriptlang.org/zh/tsconfig#noFallthroughCasesInSwitch) | Report error 
`noImplicitAny` 
for failed cases in switch statement [ #](https://www.typescriptlang.org/zh/tsconfig#noImplicitAny) | In some cases where no type annotation is present, TypeScript will fall back to any type of the variable `noImplicitOverride` when the type cannot be inferred 
[# [ 
​#](https://www.typescriptlang.org/zh/tsconfig#noImplicitReturns) | No implicit returns 
`noImplicitThis` [#](https://www.typescriptlang.org/zh/tsconfig#noImplicitThis) | Use implicit Containing "any" types throws an error 
`noPropertyAccessFromIndexSignature` on the "this" expression [#](https://www.typescriptlang.org/zh/tsconfig#noPropertyAccessFromIndexSignature) | This setting ensures that passing the "dot" (obj.key ) syntax for accessing fields and "indexes" (obj["key"]) and the way properties are declared in types 
`noUncheckedIndexedAccess` [#](https://www.typescriptlang.org/zh/tsconfig# noUncheckedIndexedAccess) | TypeScript has a way to describe objects with unknown keys but known values ​​on objects via index signatures 
`noUnusedLocals` [#](https://www.typescriptlang.org/zh/tsconfig#noUnusedLocals) | Report unusedLocals Error 
`noUnusedParameters` [#](https://www.typescriptlang.org/zh/tsconfig#noUnusedParameters) | Error reporting unused parameters in a function 
`strict` [#](https://www .typescriptlang.org/zh/tsconfig#strict) | The strict flag enables a wide range of type checking behaviors, thus more effectively guaranteeing program correctness 
`strictBindCallApply` [#](https://www.typescriptlang.org/ en/tsconfig#strictBindCallApply) | TypeScript will check that built-in methods for function calls, bindings, and applications call 
`strictFunctionTypes` with the correct arguments for the underlying function [#](https://www.typescriptlang.org/zh/tsconfig#strictFunctionTypes ) | This flag causes more correct checking of function parameters 
`strictNullChecks` [#](https://www.typescriptlang.org/zh/tsconfig#strictNullChecks) | Strict null checking 
`strictPropertyInitialization` [#](https:/ /www.typescriptlang.org/en/tsconfig#strictPropertyInitialization) | Strict property initialization 
`useUnknownInCatchVariables` [#](https://www.typescriptlang.org/en/tsconfig#useUnknownInCatchVariables) | In TypeScript 4.0, support was added To allow changing the variable type in the catch clause from any to unknown 
<!--rehype:className=style-list-arrow-->

### Module (compilerOptions) 
<!--rehype:wrap-class=row-span-3--> 

:- | -- 
:- | -- 
`allowUmdGlobalAccess` [#](https://www.typescriptlang. org/zh/tsconfig#allowUmdGlobalAccess) | When true, you will be allowed to access UMD's exported `baseUrl` as a global variable in the module file 
[#](https://www.typescriptlang.org/zh/tsconfig# baseUrl) | Allows you to set the base directory 
`module` when resolving non-absolute path module names [#](https://www.typescriptlang.org/zh/tsconfig#module) | Set the module system 
`moduleResolution` of the program [ #](https://www.typescriptlang.org/zh/tsconfig#moduleResolution) | Specify module resolution strategy: 'node' (Node.js) or 'classic' 
`moduleSuffixes` [#](https://www. typescriptlang.org/zh/tsconfig#moduleSuffixes) | Provides a way to override the default list of filename suffixes to be searched when resolving a module 
`noResolve` [#](https://www.typescriptlang.org/zh/tsconfig# noResolve) | By default, TypeScript will check the initial set of files for imports and `<reference` directives, and add these resolved files to your program's 
`paths` [#](https://www.typescriptlang.org /zh/tsconfig#paths) | Some configurations that remap module imports to paths relative to baseUrl 
`resolveJsonModule` [#](https://www.typescriptlang.org/zh/tsconfig#resolveJsonModule) | Allow imports with " .json” extension, this is a common practice in node projects 
`rootDir` [#](https://www.typescriptlang.org/zh/tsconfig#rootDir) | Default: all input non-declaration files The longest public path 
`rootDirs` [#](https://www.typescriptlang.org/zh/tsconfig#rootDirs) | Through rootDirs, you can tell the compiler that there are many "virtual" directories as a root directory 
`typeRoots` [#](https://www.typescriptlang.org/zh/tsconfig#typeRoots) | By default, all visible "@types" packages will be included in your compilation process 
`types` [#](https ://www.typescriptlang.org/zh/tsconfig#types) | By default, all visible "@types" packages will be included in your compilation process 
<!--rehype:className=style-list-arrow --> 

### Emit(compilerOptions) 
<!--rehype:wrap-class=row-span-5--> 

:- | -- 
:- | -- 
`declaration` [#](https://www .typescriptlang.org/zh/tsconfig#declaration) | Generate a .d.ts file 
`declarationDir` [#](https://www.typescriptlang.org/zh/tsconfig#declarationDir for each TypeScript or JavaScript file in the project ) | Provides a way to configure the root directory of emitted declaration files 
`declarationMap` [#](https://www.typescriptlang.org/zh/tsconfig#declarationMap) | A .d that maps back to the original .ts source file. ts file generates source mapping 
`downlevelIteration` [#](https://www.typescriptlang.org/zh/tsconfig#downlevelIteration) | Downgrade is a TypeScript term for translating to an older version of JavaScript 
`emitBOM` [#]( https://www.typescriptlang.org/en/tsconfig#emitBOM) | Controls whether TypeScript emits a byte order mark (BOM) when writing output files 
`emitDeclarationOnly` [#](https://www.typescriptlang. org/zh/tsconfig#emitDeclarationOnly) | Only emit .d.ts files; do not emit .js files 
`importHelpers` [#](https://www.typescriptlang.org/zh/tsconfig#importHelpers) | For some downgrades Operations, TypeScript uses some helper code to perform operations such as extending classes, unwinding arrays or objects, and asynchronous operations 
`importsNotUsedAsValues` [#](https://www.typescriptlang.org/zh/tsconfig#importsNotUsedAsValues) | This flag controls the imported How it works, there are 3 different options: `remove`, `preserve`, `error` 
`inlineSourceMap` [#](https://www.typescriptlang.org/zh/tsconfig#inlineSourceMap) | After setting, TypeScript does not A .js.map file is written out to provide the source map, but the source map content is embedded in the .js file
`inlineSources` [#](https://www.typescriptlang.org/zh/tsconfig#inlineSources) | When set, TypeScript will include the original content of the .ts file as an embedded string in the source map (using the source map's sourcesContent attribute) 
`mapRoot` [#](https://www.typescriptlang.org/zh/tsconfig#mapRoot) | Specifies the location where the debugger should locate the map file instead of the build location 
`newLine` [#](https:/ /www.typescriptlang.org/en/tsconfig#newLine) | Specifies the line-ending order to use when emitting files: "CRLF" (dos) or "LF" (unix) 
`noEmit` [#](https://www .typescriptlang.org/zh/tsconfig#noEmit) | Do not emit compiler output files such as JavaScript source code, source maps, or declarations 
`noEmitHelpers` [#](https://www.typescriptlang.org/zh/tsconfig#noEmitHelpers ) | You can provide implementations for the helpers you use in the global scope and turn off the emitting of helper functions completely, instead of using importHelpers import helpers 
`noEmitOnError` [#](https://www.typescriptlang.org/zh/tsconfig #noEmitOnError) | If any errors are reported, do not emit compiler output files such as JavaScript source code, source maps, or declarations 
`outDir` [#](https://www.typescriptlang.org/zh/tsconfig#outDir) | If specified, .js (and .d.ts, .js.map, etc.) files will be sent to this directory 
`outFile` [#](https://www.typescriptlang.org/zh/tsconfig#outFile) | If specified, all global (non-module) files will be concatenated into the single output file specified by 
`preserveConstEnums` [#](https://www.typescriptlang.org/zh/tsconfig#preserveConstEnums) | Do not delete generated code const enum declaration 
`preserveValueImports` [#](https://www.typescriptlang.org/zh/tsconfig#preserveValueImports) | In some cases, TypeScript cannot detect that you are using import 
`removeComments` [#](https ://www.typescriptlang.org/zh/tsconfig#removeComments) | Remove all comments 
`sourceMap` [#](https://www.typescriptlang.org/zh/tsconfig#sourceMap) from TypeScript files when converted to JavaScript | Enable generation of source map files 
`sourceRoot` [#](https://www.typescriptlang.org/zh/tsconfig#sourceRoot) | Specify that the debugger should locate the location of TypeScript files rather than relative to the source location 
`stripInternal` [ #](https://www.typescriptlang.org/zh/tsconfig#stripInternal) | Do not issue declarations for code that has an @internal annotation in its JSDoc annotation 
<!--rehype:className=style-list-arrow-- > 

### Integrity (compilerOptions) 

:- | -- 
:- | -- 
`skipDefaultLibCheck` [#](https://www.typescriptlang.org/zh/tsconfig#skipDefaultLibCheck) | Please use `skipLibCheck` instead 
. skipLibCheck` [#](https://www.typescriptlang.org/zh/tsconfig#skipLibCheck) | Skip type checking of declaration files 

### Editor support (compilerOptions) 

:- | -- 
:- | -- 
` disableSizeLimit` [#](https://www.typescriptlang.org/zh/tsconfig#disableSizeLimit) | There is an upper limit on the amount of allocated memory. Turning this flag on will remove the restriction 
`plugins` [#](https://www.typescriptlang.org/zh/tsconfig#plugins) | List of language service plugins that can be run within the editor 
<!--rehype:className=style -list-arrow--> 

### Output format (compilerOptions) 

:- | -- 
:- | -- 
`noErrorTruncation` [#](https://www.typescriptlang.org/zh/tsconfig#noErrorTruncation) | Don’t Truncate error message 
`preserveWatchOutput` [#](https://www.typescriptlang.org/zh/tsconfig#preserveWatchOutput) | Preserve watch output 
`pretty` [#](https://www.typescriptlang.org/zh/tsconfig #pretty) | Stylize errors and messages using color and context, enabled by default 
<!--rehype:className=style-list-arrow-->

### JavaScript support (compilerOptions) 

:- | -- 
:- | -- 
`allowJs` [#](https://www.typescriptlang.org/zh/tsconfig#allowJs) | Allow JavaScript files in your project Introduced instead of just allowing .ts and .tsx files 
`checkJs` [#](https://www.typescriptlang.org/zh/tsconfig#checkJs) | Used with allowJs, when checkJs is enabled, JavaScript files An error will be reported in 
`maxNodeModuleJsDepth` [#](https://www.typescriptlang.org/zh/tsconfig#maxNodeModuleJsDepth) | Maximum dependency depth for searching and loading JavaScript files under node_modules 
<!--rehype:className=style- list-arrow--> 

### Interoperability constraints (compilerOptions) 

:- | -- 
:- | -- 
`allowSyntheticDefaultImports` [#](https://www.typescriptlang.org/zh/tsconfig#allowSyntheticDefaultImports) | Allow Synthesis default import 
`esModuleInterop` [#](https://www.typescriptlang.org/zh/tsconfig#esModuleInterop) | ES module interop 
`forceConsistentCasingInFileNames` [#](https://www.typescriptlang.org/zh/ tsconfig#forceConsistentCasingInFileNames) | Force consistent casing in file names 
`isolatedModules` [#](https://www.typescriptlang.org/zh/tsconfig#isolatedModules) | Isolate modules 
`preserveSymlinks` [#](https: //www.typescriptlang.org/zh/tsconfig#preserveSymlinks) | Preserve symbolic links 
<!--rehype:className=style-list-arrow--> 

### Compiler diagnostics (compilerOptions) 

:- | -- 
:- | -- 
`diagnostics` [#](https://www.typescriptlang.org/zh/tsconfig#diagnostics) | Used to output debugging information 
`explainFiles` [#](https://www.typescriptlang.org/zh /tsconfig#explainFiles) | Print the names of files that TypeScript considers part of the project and the reason why they are part of the compilation 
`extendedDiagnostics` [#](https://www.typescriptlang.org/zh/tsconfig#extendedDiagnostics) | You can use This flag to discover where TypeScript spends its time at compile time 
`generateCpuProfile` [#](https://www.typescriptlang.org/zh/tsconfig#generateCpuProfile) | This option gives you the opportunity to have TypeScript spend its time while the compiler is running Issue v8 CPU configuration file 
`listEmittedFiles` [#](https://www.typescriptlang.org/zh/tsconfig#listEmittedFiles) | Print the names of files generated during compilation to the terminal 
`listFiles` [#](https: //www.typescriptlang.org/zh/tsconfig#listFiles) | Print the name of the compiled part of the file 
`traceResolution` [#](https://www.typescriptlang.org/zh/tsconfig#traceResolution) | When you try to debug the When including the reason for the module 
<!--rehype:className=style-list-arrow--> 

### Backward compatibility (compilerOptions) 

:- | -- 
:- | -- 
`charset` [#](https: //www.typescriptlang.org/en/tsconfig#charset) | In earlier versions of TypeScript, this controlled the encoding 
`keyofStringsOnly` used when reading text files from disk [#](https://www.typescriptlang. org/zh/tsconfig#keyofStringsOnly) | This flag changes the `keyof` type operator to return `string` instead of `string | number` when applied to a type with a string index signature 
`noImplicitUseStrict` [#](https ://www.typescriptlang.org/en/tsconfig#noImplicitUseStrict) | By default, TypeScript emits `"use strict"` when emitting module files to non-ES6 targets; preamble at the top of the file. This setting disables the prologue 
`noStrictGenericChecks` [#](https://www.typescriptlang.org/zh/tsconfig#noStrictGenericChecks) | TypeScript unifies type parameters when comparing two generic functions
`out` [#](https://www.typescriptlang.org/zh/tsconfig#out) | Please use `outFile` instead 
`suppressExcessPropertyErrors` [#](https://www.typescriptlang.org/zh/tsconfig #suppressExcessPropertyErrors) | Suppress excessive property errors 
`suppressImplicitAnyIndexErrors` [#](https://www.typescriptlang.org/zh/tsconfig#suppressImplicitAnyIndexErrors) | Suppress implicit any index errors 
<!--rehype:className=style- list-arrow--> 

### Language and environment (compilerOptions) 
<!--rehype:wrap-class=row-span-2--> 

:- | -- 
:- | -- 
`emitDecoratorMetadata` [#]( https://www.typescriptlang.org/zh/tsconfig#emitDecoratorMetadata) | Emit decorator metadata 
`experimentalDecorators` [#](https://www.typescriptlang.org/zh/tsconfig#experimentalDecorators) | Experimental 
decorators` jsx` [#](https://www.typescriptlang.org/zh/tsconfig#jsx) | Control how JSX is output in JavaScript files 
`jsxFactory` [#](https://www.typescriptlang.org/zh /tsconfig#jsxFactory) | Change the function `jsxFragmentFactory` called in a .js file when compiling JSX elements using the classic JSX runtime 
[#](https://www.typescriptlang.org/zh/tsconfig#jsxFragmentFactory) | Specify in Use the jsxFactory compiler option to specify the JSX fragment factory function to use when react JSX emit, such as `Fragment` 
`jsxImportSource` [#](https://www.typescriptlang.org/zh/tsconfig#jsxImportSource) | Declare module specifier Used to import jsx and the jsxs factory function 
`lib` [#](https://www.typescriptlang.org/zh/tsconfig #lib) | TypeScript includes a set of default type definitions for built-in JS interfaces (such as Math), as well as type definitions for objects that exist in the browser environment (such as document) 
`moduleDetection` [#](https://www .typescriptlang.org/zh/tsconfig#moduleDetection) | Module detection 
`noLib` [#](https://www.typescriptlang.org/zh/tsconfig#noLib) | Disable automatic inclusion of any library files 
`reactNamespace` [#] (https://www.typescriptlang.org/zh/tsconfig#reactNamespace) | Please use jsxFactory 
`target` [#](https://www.typescriptlang.org/zh/tsconfig#target) | Modern browser support All ES6 features, so ES6 is a good choice 
`useDefineForClassFields` [#](https://www.typescriptlang.org/zh/tsconfig#useDefineForClassFields) | Use definitions for class fields 
<!--rehype:className=style -list-arrow--> 

### Project(compilerOptions) 

:- | -- 
:- | -- 
`composite` [#](https://www.typescriptlang.org/zh/tsconfig#composite) | composite options Will enforce certain constraints so that build tools (including TypeScript itself in --build mode) can quickly determine whether a project has established 
`disableReferencedProjectLoad` [#](https://www.typescriptlang.org/zh/tsconfig #disableReferencedProjectLoad) | Disable reference project loading 
`disableSolutionSearching` [#](https://www.typescriptlang.org/zh/tsconfig#disableSolutionSearching) | Disable solution search 
`disableSourceOfProjectReferenceRedirect` [#](https://www.typescriptlang .org/zh/tsconfig#disableSourceOfProjectReferenceRedirect) | Disable source project reference redirection 
`incremental` [#](https://www.typescriptlang.org/zh/tsconfig#incremental) | Make TypeScript compile the last compiled drawing information Save to a file on disk
`tsBuildInfoFile` [#](https://www.typescriptlang.org/zh/tsconfig#tsBuildInfoFile) | This option allows you to specify a file to store incremental compilation information as part of a composite project, allowing for faster Building a larger TypeScript code base 
<!--rehype:className=style-list-arrow--> 

### WatchOptions (watchOptions) 

:- | -- 
:- | -- 
`watchFile` [#](https ://www.typescriptlang.org/zh/tsconfig#watch-watchFile) | How to monitor a single file's policy 
`watchDirectory` [#](https://www.typescriptlang.org/zh/tsconfig#watch-watchDirectory) | A strategy for monitoring the entire directory tree 
`fallbackPolling` [#](https://www.typescriptlang.org/zh/tsconfig#watch-fallbackPolling) | This option specifies when using file system events Polling strategy `synchronousWatchDirectory` used when the system runs out of native file watchers and/or does not support native file watchers 
[#](https://www.typescriptlang.org/zh/tsconfig#watch-synchronousWatchDirectory) | To synchronously invoke a callback and update the directory watcher's status 
`excludeDirectories` [#](https://www.typescriptlang.org/zh/tsconfig#watch-excludeDirectories) | You can use excludeFiles to significantly reduce the number of files watched during --watch 
`excludeFiles` [#](https://www.typescriptlang.org/zh/tsconfig#watch-excludeFiles) | You can use excludeFiles to remove a file from watched files. Group-specific files 
<!--rehype:className=style-list-arrow--> 

--- 

```js 
{ 
  "watchOptions": { 
    "synchronousWatchDirectory": true 
  } 
} 
``` 

### Type Acquisition (typeAcquisition) 

:- | -- 
:- | -- `enable` [#](https://www.typescriptlang.org/zh/tsconfig#type-enable) | Provides configuration 
`include 
for disabling type retrieval in JavaScript projects ` [#](https://www.typescriptlang.org/zh/tsconfig#type-include) | If you have a JavaScript project where TypeScript needs additional guidance to understand global dependencies, or has disabled the built-in via disableFilenameBasedTypeAcquisition Reasoning 
`exclude` [#](https://www.typescriptlang.org/zh/tsconfig#type-exclude) | Provides configuration 
`disableFilenameBasedTypeAcquisition` [#](https: //www.typescriptlang.org/zh/tsconfig#type-disableFilenameBasedTypeAcquisition) | TypeScript's type acquisition can infer which types should be added based on the file names in the project 
<!--rehype:className=style-list-arrow--> 

--- 

```js 
{ 
  "typeAcquisition": { 
    "enable": false 
  } 
} 
``` 

See also 
---- 

- [JavaScript Cheat List](./javascript.md) 
- [TypeScript Official Website](https ://www.typescriptlang.org/) _(typescriptlang.org)_
