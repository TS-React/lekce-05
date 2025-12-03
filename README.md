# Lekce 5: Literal types, generics, utility types

## Literal Types

Většinou si vystačíme s takzvanými primitivními typy, které už dobře znáte - to je třeba `string` nebo `number`. Co když se ale stane, že potřebujeme pouze specifický string - tj. nechceme typ `string`, ale typ `yellow`? Použití konkrétní hodnoty místo obyčejného typu se říká *literal types* a v základu je to velice jednoduché. Představme si, že vyrábíme aplikaci pro květinářství a potřebujeme si vytvořit typ pro květiny:

```ts
type Flower = {
  name: 'rose' | 'tulip' | 'sunflower';
  color: 'yellow' | 'red' | 'pink';
  hasThorns: boolean;
}
```

Nemůžeme si jen tak vymyslet nový druh květiny nebo barvu, kterou naše květinářství nemá a nemůže prodávat. Kdyby `name` nebo `color` byly jen `string`, mohly by se nám do aplikace dostat vážné chyby. Když je ale zadefinujeme jako v příkladu nahoře, TypeScript na nás bude v kódu křičet, kdykoli bychom se pokusili definovat barvu/květinu, kterou jsme v typu nespecifikovali.

To těžší přichází ve chvíli, kdy květiny a barvy potřebujeme na více místech. Druh květin, které v našem květinářství prodáváme, potřebujeme ve vyhledávání, v hlavičce stránky, na detailu květiny pro doporučení ostatních... ale květiny v reálné aplikaci nebudeme mít pouze tři, takže bychom napříč aplikací museli pořád dokola v typech a props definovat třeba dvacet druhů květin. Nakonec by se nám někde stalo, že nám na jednom místě květiny chybí a na druhém přidáváme neexistující a nikdo by nevěděl, kde je vlastně pravda. Tady se můžete setkat s termínem *SSOT - "Single Source Of Truth"*, jediný zdroj pravdy, a zrovna při vývoji určitě chceme vědět, co pro nás SSOT je a odkazovat se k němu místo duplikace definicí.

```ts
const flowers = ['rose', 'sunflower', 'tulip'];
const colors = ['yellow', 'red', 'pink', 'white'];
```

To už je lepší. Náš SSOT budou proměnné `flowers` a `colors`, které máme v aplikaci vypsané pouze na jednom místě. Jejich typ si TypeScript ale odvodí jako `string[]` a to nám nestačí. Aby si TypeScript jejich typ odvodil jako *literal types*, musíme mu trochu pomoct a to napsáním `as const` za naše proměnné.

```ts
const flowers = ['rose', 'sunflower', 'tulip'] as const;
const colors = ['yellow', 'red', 'pink', 'white'] as const;
```

Super! Když teď najedeme myškou na `flowers`, TypeScript už nám zobrazí, že jejich typ není `string[]`, ale buď `rose` nebo `sunflower` nebo `tulip`. Teď už nám zbývá jenom tyhle typy použít v našem objektu a na to má TypeScript speciální syntaxi, kterou si budete muset zapamatovat.

```ts
type FlowerType = (typeof flowers)[number];
type ColorType = (typeof colors)[number];

type Flower = {
  name: FlowerType;
  color: ColorType;
  hasThorns: boolean;
}
```

`typeof flowers` říká "tohle bude typu flowers", ale `flowers` jsou pole, takže musíme specifikovat ještě `[number]`.

`[number]` funguje jako index (proto je taky v hranatých závorkách) a říká "tohle platí pro všechny jednotlivé možnosti tohohle pole".


---

Pokračuj s lektorem na → [Operátor keyof](operator-keyof.md)
