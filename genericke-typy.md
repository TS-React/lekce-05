# Generické typy

S generickými typy už jsme se několikrát setkali, i když jsme ještě nevěděli, že se tomu tak říká. Generické typy nám pomohou navrhovat naše aplikace lépe.

Možná už jste slyšeli o principu **DRY** (tj. *"Neopakujme se."*, *"Don't repeat yourself."*), který nám s tím pomůže. Jedním ze způsobů jak se vyhnout zbytečnému opakování je totiž právě generika.

Představte si, že programujete web pro svůj oblíbený časopis a často potřebujete potřebujete zvýraznit první element pole - jednou je to první článek na blogu, podruhé první písmeno článku a tak dále. Funkce na získání prvního elementu pole bude vypadat pokaždé stejně, liší se jenom pole, která jí předáváte. Jednou to můžou být čísla, jindy stringy. Mohli bychom napsat:

```ts
const getFirstLetter = (allLetters: string[]) => allLetters[0];

const getFirstBlogPost = (posts: BlogPost[]) => posts[0];

const getFirstNumber = (numbers: number[]) => numbers[0];
```

Hmmm...

Nezdá se vám to jako hodně opakování? V případě takhle krátké a jasné funkce to nemusí vadit, ale úplně stejný princip bude platit i s komponenty, které v Reactu budete chtít vyrábět maximálně znovupoužitelné. Stejně tak nebudete chtít psát logiku `useForm` hooku, který jsme si ukazovali minule, pokaždé znovu jen proto, že váš formulář zpracovává jiná data.

S použitím generiky můžeme naše tři funkce na získání prvního prvku pole spojit do jedné:

```ts
const getFirstItem = <T>(items: T[]): T => items[0];
```

Při zápisu s použitím `function` by to vypadalo takto:

```ts
funtion getFirstItem<T>(items: T[]): T {
  return items[0];
}
```

`getFirstItem([1, 2, 3])` nám vrátí číslo `1`. `getFirstItem([a, b, c])` nám vrátí `a`. A my už se nemusíme opakovat. :)


## Použití v Reactu

Pozor na zádrhel, na který narazíme v Reactu. Kdybychom chtěli vytvořit arrow funkci s generickým typem v Reactu uvnitř *.tsx* souboru, dostaneme chybu.

```ts
const getFirstItem = <T>(items: T[]): T => items[0];
```

React totiž bude předpokládat, že do proměnné `getFirstItem` ukládáme JSX značku/komponentu `<T>`, kterou jsme zapomněli uzavřít.

Tento problém můžeme obejít, když funkci nadefinujeme pomocí slova `function` (viz výše). Pokud bychom chtěli použít arror function, pomůžeme si malý trikem a zapíšeme za název generické typu čárku `<T,>`.

```tsx
const getFirstItem = <T,>(items: T[]): T => items[0];
```


---

Pokračuj samostatně na cvičení → [Cvičení 2: Generické typy](cviceni-2.md)
