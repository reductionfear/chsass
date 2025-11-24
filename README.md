# Chess Assist

A browser extension for chess assistance on popular chess platforms.

## Supported Platforms
- Lichess.org
- Chess.com
- ChessArena.com
- Immortal.game

## Chess Engines

### Lozza Engine
This extension now includes the **Lozza** chess engine by op12no2.

- **Repository**: https://github.com/op12no2/lozza
- **Type**: UCI JavaScript chess engine with NNUE evaluation
- **Location**: `assets/lozza.js`

#### Using Lozza in the Extension

The Lozza engine can be instantiated as a Web Worker for chess analysis:

```javascript
// Get the engine URL
const lozzaUrl = chrome.runtime.getURL('assets/lozza.js');

// Create a worker
const lozza = new Worker(lozzaUrl);

// Set up message handler
lozza.onmessage = function(e) {
  console.log('Lozza:', e.data);
};

// Initialize engine using UCI protocol
lozza.postMessage('uci');
lozza.postMessage('ucinewgame');
lozza.postMessage('position startpos');
lozza.postMessage('go depth 10');  // Search to depth 10
```

#### UCI Protocol Commands

Lozza implements the Universal Chess Interface (UCI) protocol:

- `uci` - Initialize the engine
- `ucinewgame` - Start a new game
- `position [fen | startpos] moves ...` - Set up a position
- `go [searchmoves | depth | movetime | infinite]` - Start calculating
- `stop` - Stop calculating
- `quit` - Quit the engine

For more information about Lozza, visit: https://op12no2.github.io/lozza-ui/play.htm

## License

Lozza is distributed under its own license. See: https://github.com/op12no2/lozza/blob/master/LICENSE
