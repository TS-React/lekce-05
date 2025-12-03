# Utility typy

TypeScript nám poskytuje takzvané *"utility types"*. Nemusíme je odnikud importovat, stačí rovnou použít, a slouží nám k vyjádření opakující se logiky.

Potřebujete vytvořit typ, který vypadá úplně stejně jako jiný, ale má nějaké property navíc? Potřebujete zduplikovat existující typ, ale všechny jeho properties jsou nepovinné? Tak to už je pro vás připravené. Fungují na principu generiky, což už poznáte podle `< >` zobáčků. To proto, že budou fungovat stejně pro jakýkoli typ, který jim předáme.

## Pick<Type, Keys>

`Pick<Type, Keys>` nám umožňuje vytvořit nový typ z properties jiného. Představte si, že má váš `User` v typu vlastnosti jako `{ hobbies: Hobby[]; favoriteAnimal: 'dog' | 'cat' }`. Až budete chtít třeba `favoriteAnimal` použít na vypsání těchto properties v nějaké komponentě nebo předáním v *props*, budete muset znovu specifikovat všechny možnosti. A pak se taky může lehce stát, že na jednom místě může být `favoriteAnimal` jenom pes nebo kočka, na jiném ale i papoušek, kterému se pak nezobrazí ikonka, protože o něm polovina typů neví.

Abyste se tomu vyhnuli, můžete si *props* komponenty `FavoriteAnimal` vytvořit přímo z typu uživatele.

```ts
type User = {
  name: string;
  age: number
  hobbies: Hobby[];
  favoriteAnimal: 'dog' | 'cat' | 'parrot';
}

type Props = Pick<User, 'favoriteAnimal'>;

export const FavoriteAnimal: FC<Props> = (props) => <div>{props.favoriteAnimal}</div>;
```

## Omit<Type, Keys>

`Omit<Type, Keys>` nám pomáhá vytvořit nový typ z již existujícího stejně jako `Pick`, ale navíc s možností vynechat properties, které nepotřebujeme.

Zůstaňme u předchozího příkladu. Komponenta `FavoriteAnimal` je hotová, property `favoriteAnimal` už tedy pro zobrazení zbytku informací o našem uživateli nepotřebujeme. `Omit` nám umožní tohle zadefinovat jediným řádkem.

```ts
type UserInfoProps = Omit<User, 'favoriteAnimal'>;

export function UserInfo({ name, age, hobbies }: UserInfoProps) {
  // tělo komponenty
};
```

## Partial<Type>

`Partial<Type>` nemusí mít na první pohled jasné využití. Zní, jako že si vybereme jen "part" (část) typu, ale na to přece máme `Pick`. Abychom mu porozuměli, musíme si nejdřív zopakovat, co v typu znamená `?`.

Otazník označuje nepovinnost. Například z typu `User`, který je `{ name: string; age?: number }`, tak můžeme na první pohled odvodit, že vždycky musí mít jméno, ale jen může (nebo nemusí) mít definovaný věk. A co tedy dělá `Partial`? Jednoduše všem properties přidá `?`. Jakýkoli typ, který mu genericky předáme, tak obsahuje jenom nepovinné properties.

A příklad použití v praxi? Představte si, že máte vyrobit formulář, ve kterém si uživatel mění svoje kontaktní údaje. Někdy si vyplní telefon, někdy e-mail, někdy adresu. Formulář ale může odeslat i kdyby vyplnil jen jednu z daných možností, tedy potřebuje typ, kde budou všechny možné properties uživatele, ale všechny nepovinné.

```ts
interface User {
  name: string;
  email: string;
  phone?: string;
  address?: string;
}

function updateUserDetails(user: User, details: Partial<User>): User {
  return { ...user, ...details };
}
```

### Record<Key, Type>

`Record<Key, Type>` za nás vytváří typ pro objekt, o kterém víme, že všechny jeho keys budou stejného typu a všechny jeho values budou stejného typu.

Co si pod tím představit? Děláme aplikaci pro květinářství a uživatelé si chtějí vybírat podle barev. Vytvoříme si (nebo dostaneme z backendu) seznam barev a seznam květin.

```ts
const flowers = ['rose', 'sunflower', 'tulip'] as const;
const colors = ['yellow', 'red', 'pink', 'white'] as const;

type Flower = (typeof flowers)[number];
type Color = (typeof colors)[number];
```

Spojit je dohromady je jednoduché a máme mnoho možností, pro účely našeho příkladu to bude následující objekt:

```ts
const flowerColors {
  yellow: ['sunflower'],
  red: ['rose', 'tulip'],
  pink: ['rose', 'tulip']
  white: ['rose']
}
```

Čeho si můžeme všimnout je, že klíč našeho objektu je vždycky `color` a value je pole `flowers`. `Record` nám umožní tohle shrnout do jednoho typu.

```ts
type FlowerColors = Record<Color, Flower>;
```

## Readonly<Type> & ReadonlyArray<Type>

Poslední utility type, který si představíme, je `Readonly<Type>` pro objekty a `ReadonlyArray<Type>` pro pole.

Tady nás nečeká žádný chyták, "read only" (pouze ke čtení) opravdu znamená, že typ je pouze ke čtení.

V Reactu je populární funkcionální přístup. Pod něj patří třeba princip immutability, se kterou jste se v tomhle kurzu už potkali a umíte do pole přidávat prvky takhle `[...previous, new]` místo `.push()` metody.

Problém je, že JavaScript nám dovoluje občas dělat dost ošklivé věci. I na pole definované pomocí `const` můžeme použít metodu `.push()` a přidat tak do něj další prvek. `Readonly` typ je taková bariéra, kterou si sami můžeme postavit, abychom měli jistotu, že se do našeho pole nebo objektu opravdu nedostane žádná nechtěnná změna - TypeScript by okamžitě křičel.

```ts
const arrayOfNumbers: ReadonlyArray<number> = [1, 2, 3]

type Props = Readonly<{
  name: string;
  age: number;
}>;
```

Tyhle dva utility typy pravděpodobně samy od sebe moc používat nebudete, ale měly bystě vědět, co znamenají, když na ně v budoucí práci narazíte.
