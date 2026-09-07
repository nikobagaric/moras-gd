# Geometry Dash u Jack-u (MORAS)

Ovaj repozitorij napravljen je u sklopu projekta za Moderne racunalne sustave.
Projekt se temelji na popularnoj rhytm-platformer video igrici Geometry Dash, te
sadrzi jedan level koji (jedva, ali donekle uspjesno) je pokrenut pomocu Jack
"programskog jezika" i VM emulatora iz Nand2Tetris-a.

## Klase

`Main` - Ulazna tocka programa. Sadrzi glavnu petlju koja cita tipkovnicu, poziva update/draw na Level/Player objektima i pokrece restart nakon smrti igraca.

`Player` - Predstavlja igraca. Polja: pozicija (`xPos`, `yPos`), vertikalna brzina i prethodna pozicija (`yVel`, `yPrev`), dimenzije (`width`, `height`), pozicija poda (`groundY`) te zastavice `grounded`/`alive`. Metode: `update` (gravitacija i pomicanje), `jump`/`boostJump`, `draw`, `die`, `isAlive`, `landOnBlock`, getteri za poziciju/dimenzije/brzinu i `dispose`.

`Level` - Drzi cijeli sadrzaj levela: polja `spikes`, `blocks`, `jumpPads` (s pripadnim brojacima) i referencu na `finish`, plus `scrollX`/`scrollSpeed`/`floorY` za scrolling. Metode: `update` (scrollanje), `draw`, `checkCollisions` (provjera sudara igraca sa svim preprekama) i `checkWin`.

`Block` - Staticka prepreka/platforma s poljima `xPos`, `yPos`, `width`, `height`. Metode: `draw`, `collides` (sudar s igracem), `isLandingOn` (provjera slijetanja odozgo) i `getTop`.

`Spike` - Prepreka trokutastog oblika s poljima `xPos`, `yPos`, `width`, `height`. Metode: `draw` i `collides` - sudar s igracem znaci smrt.

`JumpPad` - Prepreka koja izbacuje igraca u zrak. Uz standardna polja pozicije/dimenzija ima `armed` zastavicu. Metode: `draw`, `collides` i `trigger` (aktivira skok kad igrac dotakne pad).

`Finish` - Oznacava kraj levela. Polja pozicije/dimenzija, metode `draw` i `collides` (detekcija pobjede).

`Texture` - Staticka klasa s funkcijama za crtanje: `drawSolid`, `drawTriangleUp`, `drawBrick`, `drawPlayerTexture`, `drawPlayerDeadTexture`, `drawJumpPad`, `drawFinish`. Sve se crta rucno pravokutnicima i linijama jer Jack nema podrsku za sprite-ove.

## Pokretanje

1. Provjeriti Java instalaciju (Nand2Tetris alati su Java aplikacije).
2. Iz root foldera repozitorija pokreniti `./JackCompiler.sh` da kompajlira sve `.jack` datoteke u `.vm` datoteke.
3. Pokrenuti `./VMEmulator.sh`, kroz njega ucitati direktorij projekta i kliknuti Run.
4. Space je za skok.

Mape poput `bin/`, `OS/`, `builtInChips/` i `builtInVMCode/` su standardni Nand2Tetris alati, najbolje ih je ne dirati.
