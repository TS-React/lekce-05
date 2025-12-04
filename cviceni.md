# Cvičení: Literal types a operátor keyof

## Cvičení 1: Jazyky

1. Máš seznam povolených jazyků UI:
   ```ts
   const languages = ['cs', 'en', 'de'] as const;
   ```

2. Vytvoř typ `Language`, který bude `cs | en | de` odvozený z proměnné `languages`.

3. Vytvoř typ `Settings` pro objekt, který bude představovat nastavení aplikace a bude obsahovat vlastnosti:
   - `language` typu `Language` vytvořeného dříve
   - `currency` typu `string`
   - `darkMode` typu `boolean`

4. Vytvoř proměnnou `currentSettings` typu `Settings` a nastav ji nějaké výchozí hodnoty

5. Napiš funkci `changeLanguage(settings, newLanguage)`, která jako parametr přijme aktuální nastavení a nový jazyk. Vrátí nový objekt nastavení se změněným jazykem. Funkce musí přijímat jen platné hodnoty typu `Language`.

6. Vyzkoušej si:
   - volání funkce s platnou hodnotou `'cs'`
   - volání s neplatnou hodnotou `'fr'` – tohle by měl TypeScript odmítnout a hlásit chybu.


## Cvičení 2: Překlady

1. Máš jednoduchý překladový slovník:

   ```ts
   const translations = {
     hello: 'Ahoj',
     goodbye: 'Na shledanou',
     thanks: 'Děkuji',
   } as const;
   ```

2. Vytvoř typ `TranslationKey` jako union klíčů (názvů vlastností)objektu `translations`, tj. typ by měl dovolit hodnoty `'hello' | 'goodbye' | 'thanks'`.

3. Napiš funkci `t` (ano, název funkce je jen písmeno `t`), která:
   - přijímá jako parametr `key' typu `TranslationKey`
   - vrací odpovídající český text z `translations`.

4. Vyzkoušej volání:
   - `t('hello')` by mělo v pořádku proběhnout a vrátit `'Ahoj'`
   - `t('welcome')` by měl TypeScript hlásit chybu


## Cvičení 3: Varianty tlačítka

Na toto cvičení budeš **potřebovat React**, založ si nový prázdný projekt nebo řešení přidej do jakéhokoliv existujícího.

1. Založ si soubor pro komponentu `Button`. Do souboru, ale mimo komponentu, si přidej povolené varianty tlačítka (to bychom v praxi získali např. z design systému, který připravil UX designer):

   ```ts
   const buttonVariants = ['primary', 'secondary', 'danger'] as const;
   ```

2. Vytvoř typ `ButtonVariant`, který bude union `'primary' | 'secondary' | 'danger'` odvozený z hodnot v poli `buttonVariants`.

3. Komponenta `Button` bude přijímat 2 props:
   - `label` typu `string` (text na tlačítku)
   - `variant` typu `ButtonVariant` (barevná varianta tlačítka)

   Vytvoř odpovídající typ `ButtonProps`.

4. Dopiš React komponentu Button, která:
   - přijímá ButtonProps,
   - tlačítku v komponentě nastaví vždy CSS třídu `btn` (můžeš ji v CSS nastylovat, pokud máš čas)
   - podle varianty v props se tlačítku přidá ještě další CSS třída (např. `btn-primary`, `btn-secondary`, `btn-danger`)

5. Vyzkoušej komponentu použít:
   - `<Button label="Uložit" variant="primary" />` by mělo být OK
   - `<Button label="Smazat" variant="danger" />` by mělo být OK
   - `<Button label="Nápověda" variant="ghost" />` TypeScript by měl hlásit chybu

---

Pokračuj s lektorem na → [Generické typy](genericke-typy.md)
