# Cvičení: Generické typy

## Cvičení 1: Refactoring pomocí DRY principu

V kódu máte tyto dvě funkce, které dělají v podstatě to samé (přijmou hodnotu a zabalí hodnotu do pole, tj. vrátí pole, kde je hodnota jako jediný prvek). Nahraďte je jednou **generickou** funkcí `wrapInArray`, která budět dělat to stejné pro jakýkoliv typ.

```ts
const wrapNumberInArray = (num: number): number[] => {
  return [num];
};

const wrapStringInArray = (str: string): string[] => {
  return [str];
};
```


## Cvičení 2: Naplnění pole hodnotou

Vytvořte **generickou** funkci `createFilledArray`, která přijme dva argumenty:
- `value` je hodnota libovolného typu, kterou chceme naplnit pole)
- `count` je počet, kolikrát se má hodnota v poli opakovat

Funkce vrátí pole, které obsahuje tuto hodnotu zadaný počet krát. Do funkce můžeme poslat hodnotu libovolného typu.

Pro vyplnění pole hodnotou můžete použít metodu `Array(count).fill(value)` → [dokuemntace MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)


## Cvičení 3: Generika s více typy

Napište funkci `mergeValues`, která přijme dva argumenty, přičemž každý může být jiného typu (například číslo a string). Funkce vrátí pole, které obsahuje oba tyto prvky. Takovému poli se obvykle říká **tuple**.

- Pokud tedy do funkce předám hodnoty `7` a `Alena`, funkce by měla vrátit hodnotu `[7, 'Alena']`.
- Předáme-li do funkce `true` a `{name: 'Alena', age: 27}`, funkce vrátí pole `[true, {name: 'Alena', age: 27}]`

**Nápověda:** Místo jednoho `<T>` budete potřebovat definovat dva typy, např. `<T, U>`.


---

Pokračuj s lektorem na → [Utility typy](utility-typy.md)