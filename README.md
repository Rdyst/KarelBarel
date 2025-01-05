# Karel

Tenhle projekt je vzdelavaci (robot?) jménem Karel kterej neni barel. Mužete zadávat textové příkazy pro řízení pohybů, orientace a interakce Karla s políčky gridu.
Vyzkoušet si ho mužete zde https://rdyst.github.io/KarelBarel/ (hitorie z nejakeho duvodu nefunguje na githubu)

![image](https://github.com/user-attachments/assets/059cae27-ed3b-4e3e-88c0-39316a6be905)

## Funkce

1. **Navigace gridu a velikost**: Karel operuje na gridu 5-20 na druhou a pohybuje se krok za krokem podle zadaných příkazů.
2. **Příkazy**:
   - `KROK [n]`: Pohne Karlem o `n` kroků vpřed (výchozí: 1).
   - `VLEVOBOK [n]`: Otočí Karla vlevo `n`krát.
   - `POLOZ [A]`: Položí předmět `A` na aktuální pozici Karla.
   - `ERASE`: Odstraní jakýkoliv předmět z aktuální pozice Karla.
   - `ZVYRAZNI [BARVA]`: Zvýrazní aktuální políčko Karla zadanou barvou (`YELLOW`, `RED`, `GREEN`, `BLUE`).
   - `RESET`: Resetuje mřížku a pozici Karla.
3. **Historie příkazů**: Zobrazuje seznam vykonaných příkazů.
4. **Interaktivní UI**: Uživatelé mohou zadávat příkazy do textového pole a okamžitě vidět výsledky.
5. **Chyby**: Zobrazuji se zprávy pro neznámé příkazy nebo pohyby mimo hranice gridu.

## Kod

### Zpracování příkazů pomocí `switch`
Místo více `if-else` bloků jsou příkazy zpracovávány pomocí struktury `switch` pro větší přehlednost a rychlost myslim 
napad od pana Bubilka po jeho zmínění switche pri hodině:

```javascript
        function processCommand(command) {
            const [action, param] = command.split(' ');
            const listItem = document.createElement('li'); 
            listItem.textContent = command; 
            historyList.appendChild(listItem); 

    switch (action) {
        case 'KROK': {
            const steps = parseInt(param) || 1;
            moveKarel(steps);
            break;
        }
        case 'VLEVOBOK': {
            const turns = parseInt(param) || 1;
            turnLeft(turns);
            break;
        }
        case 'POLOZ': {
            const item = param || '';
            placeItem(item);
            break;
        }
        case 'ERASE': {
            eraseItem();
            break;
        }
        case 'ZVYRAZNI': {
            const color = param || 'YELLOW';
            highlightCell(color);
            break;
        }
        case 'RESET': {
            resetGame();
            break;
        }
        default: {
            output.textContent += `Neznámý příkaz: ${command}\n`;
            break;
        }
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
                if (color === 'RED') {
                    cell.classList.add('highlighted-red');
                } else if (color === 'GREEN') {
                    cell.classList.add('highlighted-green');
                } else if (color === 'BLUE') {
                    cell.classList.add('highlighted-blue');
                } else {
                    cell.classList.add('highlighted-yellow');
                }
            }
        }
```

### Inicializace gridu
Grid je dynamicky vytvořen a aktualizován při pohybu Karla:

```javascript
function createGrid() {
            gameContainer.innerHTML = '';
            gameContainer.style.gridTemplateColumns = `repeat(${GRID_SIZE}, 40px)`;
            gameContainer.style.gridTemplateRows = `repeat(${GRID_SIZE}, 40px)`;
            grid = Array.from({ length: GRID_SIZE }, () => Array(GRID_SIZE).fill(null));
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

