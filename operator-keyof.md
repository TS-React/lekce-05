## Operátor Keyof

`keyof` operátor nám pomůže získat typ z klíčů objektu.

```ts
const fontWeights = {
  normal: '400',
  semibold: '600',
  medium: '500',
  bold: '700',
  extrabold: '800',
};

type FontWeight = keyof typeof fontWeights;
```

`FontWeight` type je teď `'normal' | 'semibold' | 'medium' | 'bold' | 'extrabold'`.

Kdy se nám něco takového může hodit? Podle výše zmíněného příkladu třeba když budeme chtít uživateli umožnit změnit v jeho blog postu font weight.

```ts
const [fontWeight, setFontWeight] = useState<FontWeight>('normal')

function changeFontWeight(weight: FontWeights): string {
  setFontWeight(weight);
}
```

---

Pokračuj samostatně na cvičení → [Cvičení: Literal types a operátor keyof](cviceni.md)
