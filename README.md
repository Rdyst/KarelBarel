# Karel

Tenhle projekt je vzdelavaci (robot?) jménem Karel kterej neni barel. Mužete zadávat textové příkazy pro řízení pohybů, orientace a interakce Karla s mřížkou.

## Funkce

1. **Navigace na mřížce**: Karel operuje na mřížce 10x10 a pohybuje se krok za krokem podle zadaných příkazů.
2. **Příkazy**:
   - `KROK [n]`: Pohne Karlem o `n` kroků vpřed (výchozí: 1).
   - `VLEVOBOK [n]`: Otočí Karla vlevo `n`krát.
   - `POLOZ [A]`: Položí předmět `A` na aktuální pozici Karla.
   - `ERASE`: Odstraní jakýkoliv předmět z aktuální pozice Karla.
   - `ZVYRAZNI [BARVA]`: Zvýrazní aktuální políčko Karla zadanou barvou (`YELLOW`, `RED`, `GREEN`, `BLUE`).
   - `RESET`: Resetuje mřížku a pozici Karla.
3. **Historie příkazů**: Zobrazuje seznam vykonaných příkazů.
4. **Interaktivní UI**: Uživatelé mohou zadávat příkazy do textového pole a okamžitě vidět výsledky.
5. **Ošetření chyb**: Zobrazuje zprávy pro neznámé příkazy nebo pohyby mimo hranice gridu.

## Klíčové části kódu

### Zpracování příkazů pomocí `switch`
Místo více `if-else` bloků jsou příkazy zpracovávány pomocí struktury `switch` pro větší přehlednost a udržovatelnost
napad od pana Bubilka po jeho zmínění switche pri hodině:

```javascript
function processCommand(command) {
    switch (true) {
        case command.startsWith('KROK'):
            const steps = parseInt(command.split(' ')[1]) || 1;
            moveKarel(steps);
            break;
        case command.startsWith('VLEVOBOK'):
            const turns = parseInt(command.split(' ')[1]) || 1;
            turnLeft(turns);
            break;
        case command.startsWith('POLOZ'):
            const item = command.split(' ')[1] || '';
            placeItem(item);
            break;
        case command === 'ERASE':
            eraseItem();
            break;
        case command.startsWith('ZVYRAZNI'):
            const color = command.split(' ')[1] || 'YELLOW';
            highlightCell(color);
            break;
        case command === 'RESET':
            resetGame();
            break;
        default:
            output.textContent += `Neznámý příkaz: ${command}\n`;
            break;
    }
}
```

### Zvýrazňování políček
Políčka lze zvýraznit několika barvami, včetně `YELLOW`, `RED`, `GREEN` a `BLUE`:

```javascript
function highlightCell(color) {
    const cell = document.getElementById(`cell-${karel.x}-${karel.y}`);
    if (cell) {
        cell.classList.remove('highlighted-yellow', 'highlighted-red', 'highlighted-green', 'highlighted-blue');
        cell.classList.add(`highlighted-${color.toLowerCase()}`);
    }
}
```

### Inicializace mřížky
Mřížka je dynamicky vytvořena a aktualizována při pohybu Karla:

```javascript
function createGrid() {
    gameContainer.innerHTML = '';
    for (let y = 0; y < GRID_SIZE; y++) {
        for (let x = 0; x < GRID_SIZE; x++) {
            const cell = document.createElement('div');
            cell.classList.add('cell');
            cell.id = `cell-${x}-${y}`;
            gameContainer.appendChild(cell);
        }
    }
    updateKarelPosition();
}
```

## Možnosti využití

- **Vzdělávání**: Interaktivní způsob, jak se naučit programovací logiku a zabavit se zároveň.

## Budoucí vylepšení

- nic mě nenapadlo ngl

