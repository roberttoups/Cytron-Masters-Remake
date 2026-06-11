# Cytron Masters (1982) — Deep Research Report

> Research foundation for a modern web remake. Compiled 2026-06-11 from five
> parallel research passes (mechanics, history, reception/technical, surviving
> resources/IP, design retrospectives), cross-verified against each other.
>
> **Verification caveats:** This environment's network policy blocked direct
> page fetches (archive.org, filfre.net, Wikipedia, etc. all returned 403), so
> findings were assembled from extensive web-search extracts of the cited
> pages rather than full-page reads. Facts below are marked **[verified]**
> (corroborated by 2+ independent sources), **[single-source]**, or
> **[unverified]**. The single most important follow-up is reading the
> original manual and Programmer's Notes (§8.1) — they will settle every open
> question in §11.

---

## 1. Executive summary

**Cytron Masters** is a real-time tactical battle game designed by **Dan
Bunten** (later **Danielle Bunten Berry**) with **Jim Rushing** and **Alan
Watson**, published by **Strategic Simulations, Inc. (SSI)** on its
action-oriented **RapidFire** label for the **Apple II** (original) and
**Atari 8-bit** (port) in **July/August 1982**. [verified]

Two players (or one player vs. a 3-level AI) each command an army of robotic
"CYTRONs" on a 12×6 battlefield, fueled by energy from eight capturable
generators, with the goal of destroying the opposing Command Center. It is
widely cited as **one of the earliest real-time strategy games** — Jimmy Maher
calls it "a prototype of the real-time strategy games that would become
popular a decade later" — though historians more precisely class it as
real-time *tactics* (no base-building). [verified]

It reviewed very well in 1982 but **sold only ~4,700 copies** (4,702 per the
Digital Antiquarian). Bunten's own diagnosis: "Rather than appealing to both
action gamers and strategy gamers, it seemed to fall in the crack between
them." The concept survived into her later games **Modem Wars** (1988) and
**Command HQ** (1990). [verified]

For the remake: the complete rules are recoverable (manual + Bunten's
Programmer's Notes are scanned on archive.org; disk images for both platforms
exist and run in emulators); **no prior fan remake exists** — this would
apparently be the first; the game is **not public domain** (US copyright runs
to ~2078), with the SSI catalog rights presumed at **Ubisoft** but possibly
reverted to the **Bunten estate** — a from-scratch reimplementation of the
mechanics is the standard low-risk path (see §9).

---

## 2. Quick facts

| Field | Value | Confidence |
|---|---|---|
| Title | Cytron Masters ("CYTRON" = **CY**bernetic elec**TRON**ic units) | verified |
| Designer/programmer | Dan Bunten (Danielle Bunten Berry) | verified |
| Other credits | Jim Rushing, Alan Watson (per manual title page) | verified |
| Publisher / label | Strategic Simulations Inc. (SSI) / RapidFire line | verified |
| Release | July or August 1982 (Apple II); Atari 8-bit port late 1982 | verified |
| Platforms | Apple II (original), Atari 400/800 (port); later dual-format flippy disk | verified |
| Price | $39.95 (RapidFire line price point) | unverified for this title |
| Language | 100% assembly/machine language (Bunten's first large ASM project) | verified |
| Players | 1 vs AI, or 2 on one machine (simultaneous input) | verified |
| Sales | ~4,702 units | verified (filfre.net + zeitgame.net, both from SSI's published figures) |
| Genre placement | Proto-RTS / real-time tactics | verified |
| Sequel/descendants | None direct; Modem Wars (1988) expanded its ideas | verified |
| Note | Some databases (old-games.com, hypoid.com, squakenet) list "1980" — metadata error; 1982 is solid | verified |

---

## 3. Complete gameplay mechanics

### 3.1 Battlefield

- **12×6 grid** of unit locations. [single-source: zeitgame.net, detailed modern playthrough]
- Each player's **Command Center (CC)** sits mid-height on opposite edges, at
  grid (1,3) and (12,3). [single-source: zeitgame.net]
- **Eight neutral energy generators ("power centers")** arranged in **two rows
  of four near mid-field** in the standard setup. [verified: Wikipedia,
  GameFAQs, MyAbandonware]
- At the hardest AI level, CC placement "can be (not always) asymmetric" and
  power centers are spread out, with at least one near mid-field.
  [single-source: zeitgame.net]
- Each game begins with a starting configuration of units already on the
  field. [single-source: GameFAQs]
- Scale: each player can field **up to 50 CYTRONs at once** (~100 units on
  screen). [verified: CGW Nov/Dec 1982 designer notes; filfre.net]
- A **game clock** runs at the top of the screen; each player has an
  **energy bar**. [verified: GameFAQs, zeitgame.net]

### 3.2 Units

Five buildable CYTRON types plus Command-Center-launched anti-missiles.
Units are built with the MAKE command and materialize at your movable
**Transport Beam Point** (see §3.4), paid for in energy. Costs and combat numbers below are from the Wargaming Scribe's
modern playthrough (zeitgame.net), the most detailed rules source found;
they should be re-verified against the manual. [single-source unless noted]

| Unit | Cost | Role & behavior | Survivability |
|---|---|---|---|
| **Mine** | 1 | Destroys any enemy CYTRON *except bunkers* on contact; detonates when an enemy approaches. **Moving a mine into the enemy Command Center wins the game.** | 25% chance of destruction per incoming shot |
| **Bunker** | 2 | Mobile damage sponge; placed at the head of assault columns to draw fire; immune to mine contact kills | The only unit with hit points: absorbs **10 shots or 2 mine blasts** (or any combination) |
| **Shooter** | 4 | Automatically fires at the **closest** enemy unit within a **3-space range** [verified: Wikipedia + zeitgame] | 50% chance of destruction per incoming shot |
| **Commander** | 4 | Weaponless, fragile relay unit. One order issued through a Commander commands **all friendly units within 3 spaces** simultaneously [verified: Wikipedia, Hypoid, zeitgame] | Fragile (treated like other 1-shot units) |
| **Missile** | 8 | Launched from your CC; flies up and over the battlefield; the player **steers it directly in flight** within a limited time; detonates destroying everything within ~1-space radius of impact (GameFAQs: "up to four units") | Can be intercepted by enemy anti-missiles |
| **Anti-missile** | **unknown** (not in any retrievable source — check manual) | Launched from the CC to intercept an enemy missile in flight; interception **can fail** | — |

**Combat rules:** [single-source: zeitgame.net]

- No hit points except bunkers — every other unit is either destroyed by a
  hit or unharmed (probabilistic, per the percentages above).
- **Stationary bonus:** units that are not moving are **20 percentage points
  less likely** to be destroyed when shot (e.g., a stationary shooter: 30%
  instead of 50%... note: zeitgame's wording says "40%" for an immobile
  shooter — i.e. 50% − 20% *relative* reduction is ambiguous; the quoted text
  reads "an immobile shooter has 40% chance of being destroyed when shot
  at," implying the modifier is −10pp or ×0.8. **Re-verify against manual.**)
- **Missile/anti-missile geometry:** both launch from the CCs, so missiles
  are strong defensively (short interception window for the opponent) but
  are very likely to be intercepted when fired deep into the enemy half.

### 3.3 Energy economy

- **Energy is the only resource.** It pays for creating units and (per
  Wikipedia/Hypoid) for moving them and other actions — per-action costs were
  not retrievable; the manual will have them. [verified that energy gates
  commands; per-action numbers unverified]
- **Generation:** each controlled power center produces **¼ energy unit per
  clock tick** (a tick = several seconds); income scales with the number of
  generators you control. [verified: zeitgame.net + GameFAQs]
- **Capture:** power centers **cannot be destroyed**; they switch allegiance
  when **occupied by any unit**. Map control = economy, the genre's core loop
  in embryo. [verified: zeitgame.net, MyAbandonware]
- Starting energy and energy cap: **unknown** (manual). The Grand Master AI
  receives "a significant bonus to energy (both starting and production)" —
  i.e., the AI cheats at the top level. [single-source: zeitgame.net]

### 3.4 Command system (the signature mechanic)

The fiction: you are the Cytron Master inside the Command Center, and orders
propagate from the CC to field units. [verified]

- Orders are issued in real time through a menu. The **Main Menu has exactly
  four options: MAKE, LOCATE, DIRECT, ORDER** — confirmed by the primary
  source "Special Note to Atari Owners" insert (transcribed in
  `primary-sources/atari-owners-note.md`). [verified — primary source]
  - **MAKE** — create a unit (paid in energy). New units materialize at the
    **Transport Beam Point** (see LOCATE).
  - **LOCATE** — reposition the **Transport Beam**: the spawn point can be
    moved "almost anywhere on your side of the battlefield." The spawn
    location is therefore a relocatable strategic asset, not fixed at the
    Command Center. Left player's Beam Point is blue; right player's is
    orange/green. [verified — primary source]
  - **DIRECT** — order a single unit via a cursor (you can hover enemy units
    but not command them). Sub-menu: **four arrows (up/down/left/right),
    "halt", and "destruct"** (self-destruct). [verified — primary source]
  - **ORDER** — command through a Commander: the cursor auto-snaps to one of
    your Commanders and cycles between them. **A player may have at most
    three Commanders at once.** [verified — primary source]
- **Movement deltas (critical design quirk):** an individually-ordered unit
  moves **exactly 5 spaces** then halts; a unit ordered through a Commander
  moves **10 spaces**. There is no free destination selection. The Commander
  doubling was a deliberate incentive to use the relay mechanic.
  [verified: zeitgame.net + Wikipedia]
- Orders are instantaneous (no simulated transmission delay found in any
  source); the Commander's value is *batching* (one tap orders everything
  within 3 spaces) and *endurance* (10-space moves).

### 3.5 Win/loss conditions

- Win by **destroying the enemy Command Center**. [verified: all sources]
- The one documented kill method is **moving a mine onto the enemy CC**
  ("running one into your opponent's base being the ultimate win condition" —
  GameFAQs; zeitgame states it as *the* objective). Whether shooters or
  missiles can damage the CC, and whether the CC has hit points, is
  **unresolved** — check the manual. [open question]

### 3.6 Controls and UI

- **Atari:** joystick-driven; "the game is played entirely with the joystick,
  with all information available on the screen at all times," orders given
  quickly through a menu, any unit freely selectable with the pointer.
  A keyboard shortcut path exists and "it is faster to select a unit with
  the keyboard than with the joystick." [single-source: zeitgame.net]
- **Apple II:** game paddles (Bunten: Apple's "goofy little knobs") and/or
  keyboard; the manual has "lengthy instructions" for paddle-guided
  missiles. [verified: CGW + MobyGames + Atari insert]
- **Atari console keys:** OPTION = difficulty level, SELECT = 1-player vs
  2-player, START = begin/restart. Two-player: left player joystick port #1,
  right player port #2; port #2 is used when playing the computer (implying
  the human takes the right side vs the AI — verify in emulator).
  [verified — primary source]
- **Missiles and anti-missiles are manually steered in flight** (joystick on
  Atari, paddles on Apple). [verified — primary source]
- Two-player mode takes **simultaneous input from both players on one
  machine**. [verified: CGW designer notes]

### 3.7 Real-time engine, speed, modes

- Fully real-time; MobyGames credits it with first-of-its-kind
  "multi-thread software routines to enable all the units to move in real
  time," and on Atari it used vertical-blank interrupts to run game logic
  and display "apparently at once." [verified]
- **Three speed levels**, added so players could learn the game — these are
  **distinct from** the three AI difficulty levels. [verified: Wikipedia +
  zeitgame; flagged as easily-conflated] (Note: the Atari insert's OPTION
  key selects "difficulty levels" named Novice/Master/Grand Master; whether
  speed is a separate Atari setting or an Apple-only option needs emulator
  verification.)
- **Pause confirmed (Atari):** "At any time during the match, you may pause
  the action by pressing the 'space' bar... Pressing the 'space' bar again
  will resume the game exactly where you left off." While paused,
  OPTION/SELECT/START can restart or reconfigure the game.
  [verified — primary source]
- **Interactive tutorial** included — claimed as one of the first interactive
  tutorials in a computer game — plus a dedicated **missile/anti-missile
  practice scenario**. [verified: Wikipedia/MobyGames]

### 3.8 AI opponent (3 levels) [single-source: zeitgame.net]

| Level | Behavior |
|---|---|
| **Novice** | Passive and slow; sends isolated units; barely uses anti-missiles |
| **Master** | Anti-missiles with delay; occasional (inaccurate) missiles; single-column attacks; map shifts to put 1–2 of your power centers near mid-field |
| **Grand Master** | Instant anti-missile response (its half of the board is effectively missile-proof); counters pushes with missiles; multi-column attacks; **cheats with bonus starting + production energy**; possible asymmetric CC placement |

Universal verdict, 1982 and now: the AI is weak ("predictably atrocious" —
Digital Antiquarian; the Space Gamer's lone complaint), and the game was
designed human-vs-human first. A trained player "will consistently beat the
'Grand Master' AI after a couple of hours." [verified]

---

## 4. Development history

### 4.1 The designer

Dan Bunten (1949–1998; transitioned in 1992 to Danielle Bunten Berry) is one
of the most influential designers in the medium's history — "the master of
the multiplayer game" (James Hague), creator of M.U.L.E., honored with the
CGDA Lifetime Achievement Award. Career arc into this game: [verified]

1. **Wheeler Dealers** (1978, Speakeasy Software, Apple II) — 4-player
   real-time auction game shipped with a custom 4-paddle controller; sold
   ~50 copies. Taught her "how engaging a real time auction could be" and
   set her criteria: the underlying model must be "very easy to describe,"
   and decisions should be entered "by 'doing' rather than 'telling'."
2. **Computer Quarterback** (1980, SSI) and **Cartels & Cutthroat$**
   (1981, SSI) — turn-based multiplayer designs. (Encyclopedia of Arkansas
   gives 1978/1979 — wrong; SSI was founded 1979.)
3. **Cytron Masters** (1982, SSI) — her third and final SSI title, ~**eight
   months of development on the Apple II**, her **first large
   assembly-language project** and "by far his most challenging programming
   project yet" (Maher): animation + sound + simple AI for up to a hundred
   on-screen units + simultaneous two-player input, without losing
   action-game speed. [verified: filfre.net, CGW]

### 4.2 The team and the proto-Ozark question

- Manual credit: "Dan Bunten, Jim Rushing and Alan Watson." [verified]
- Atari version credits (from the boxed "Special Note to Atari Owners"
  insert): Game Design: Dan Bunten; Program: Dan Bunten, Jim Rushing and
  Alan Watson; Special Effects: Jim Rushing and Alan Watson.
  [verified — primary source]
- Halcyon Days interview (Bunten's only direct comment found): "The next
  game I did was 'Cytron Masters,' and we added another programmer to help
  with the graphics and the Atari port." That programmer was **Alan Watson**.
- **Wikipedia/MobyGames credit "Ozark Softscape," but this is anachronistic.**
  Per the Digital Antiquarian, Ozark Softscape was *in the process of
  forming* during this project; Cytron Masters is the transitional,
  pre-Ozark game made by the proto-team (Dan, Jim Rushing, Alan Watson, with
  brother Bill Bunten advising). Ozark formalized with the Electronic Arts
  deal and M.U.L.E. (1983). [verified: filfre.net, Encyclopedia of Arkansas,
  Carpe Ludum 2023 team interview]
- Caution: ozarksoftscape.com is now a hijacked/spam domain — never cite it.

### 4.3 The Atari port — a formative clash

Alan Watson (ANTIC podcast interview #23): Dan "never really had any use for
graphics" — "I don't care about color, I don't care about graphics. We just
want to get the game converted." The Atari guys pushed back: "the reason
people buy Atari is for the sound and color. Otherwise they woulda bought an
Apple." [single-source: ANTIC interview]

Bunten's own bylined CGW article ("Cytron Masters for Atari," CGW Vol. 2
No. 6, Nov/Dec 1982 — full scan at vgpavilion.com) describes the port:
four-voice POKEY sound ("truly impressive sound effects, at least as
compared to the Apple"), display lists + display-list interrupts for
on-the-fly color changes, player/missile graphics for extra colors and fast
animation, vertical-blank interrupts; conclusion: for a machine-language
game running its own OS, "the Atari was unbeatable." [verified]

Consequence: **Bunten never wrote another Apple II game**; Ozark Softscape
became an Atari shop, which directly shaped M.U.L.E. [verified: filfre.net]

### 4.4 SSI and the RapidFire line

- Joel Billings (SSI founder) had no personal interest in the non-historical
  theme but found a real-time wargame "intriguing and unique," and it fit
  the new **RapidFire** label — SSI's 1982 push beyond hardcore wargamers
  toward the arcade-leaning youth market. [verified: zeitgame, Retro365]
- First two RapidFire releases: **Cytron Masters** and **Galactic
  Gladiators**; later 1982: The Cosmic Balance, S.E.U.I.S. The line was
  short-lived (1982–83). [verified]
- SSI bought the prized second-page ad slot in CGW July 1982 for it; Bunten
  simultaneously began writing a CGW column. [single-source: zeitgame.net]

---

## 5. Place in real-time-strategy history

- **The claim:** historian Matt Barton calls it "one of the first (if not
  the first) real-time strategy game"; Wikipedia: "one of the earliest video
  games that can be considered a real-time strategy game, or a real-time
  tactics predecessor to the genre." Its energy-generator economy is the
  embryonic form of RTS resource gathering. [verified]
- **The counter:** Scott Sharkey (1UP): it "attempted real time strategy"
  but was "much more tactical than strategic" given limited
  construction/resource management. VGChartz: "could be considered the first
  real RTS title ever developed... perhaps better described as a real-time
  tactics game." [verified]
- **Competing precursors:** *War of Nerves* (Odyssey², 1979), *Utopia*
  (Intellivision, 1981 — Ars Technica's "arguably the earliest ancestor,"
  though it runs on regular turn cycles), *Legionnaire* (Crawford, 1982 —
  real-time tactics, no economy). Cytron Masters' distinction is combining
  **real time + unit production + a capturable resource economy** in one
  design. [verified]
- **Influence: essentially none.** The Wargaming Scribe: "it had almost no
  influence on what RTS subsequently became... to a large extent a design
  dead-end." The actual lineage to Dune II ran through **Herzog Zwei**
  (1989), which independently converged on strikingly similar ideas (a
  central commander unit building/ordering units). Cytron Masters' obscurity
  (platform + sales) kept it out of the chain. [verified]
- **The Wertzone's summary of what it did pioneer:** "action unfolding in
  real-time with the player controlling multiple units where the loss of
  individual units did not lead to a game-ending state."

---

## 6. Reception and sales

### 6.1 Contemporary reviews (1982–83) — strongly positive

| Outlet | Reviewer / issue | Verdict |
|---|---|---|
| Computer Gaming World | Mark Botner, "Cytron Masters: Review and Analysis," Vol. 2 No. 5 (Sep–Oct 1982); PDF: cgwmuseum.org/galleries/issues/cgw_2.5.pdf | "An exciting game offering multiple levels of play with variations to suit the individual: Play on all levels guarantees an action-packed episode of futuristic combat." |
| The Space Gamer | Chris Smith, #59 (Jan 1983), reviewing the RapidFire line | "Requires a bit of tactical know-how, and its real-time command system gives it a slight arcade feel. I think this is the perfect combination of arcade and board game." Line-wide: "the best line of computer games I've ever seen." Lone complaint: weak AI. |
| Softalk | Sep 1982 | High marks for playability, intelligence, excitement; "control processes are the essence of what makes CYTRON Masters unique." |
| inCider | Aug 1983 | Only complaint: "there is no award for best game of the year to give it." |
| Page 6 (UK) | Dave Beech, issue 6 (1983), p. 14 — page6.org/archive/issue_06/page_14.htm | Atari version review; text not retrievable this session. |

(Quote attributions above were triangulated across three research passes —
one search extract misattributed Smith's "perfect combination" line to
Botner; majority evidence assigns it to Smith/Space Gamer.)

No BYTE, Creative Computing, Electronic Games, or Antic review was found.

### 6.2 Retrospective cooling

- CGW's 1992 survey of science-fiction games: **2 of 5 stars**. [verified]
- The Wargaming Scribe (modern playthrough): "Well-designed, but obsolete.
  It is just not that fun as a solitaire game" — while suspecting it "would
  have been exhilarating" head-to-head.
- Digital Antiquarian: technically impressive; "the computer opponent's AI
  was predictably atrocious."

### 6.3 Sales

- **4,702 units** (Digital Antiquarian; corroborated as "4,700" by the
  Wargaming Scribe; ultimate source is SSI's published per-title sales data,
  catalogued in Carl Lund's "History of SSI Games" —
  sites.google.com/site/ssihistory/Home). A flop by SSI standards despite
  the reviews. [verified, second-hand from SSI data]
- Bunten's verdict: "Rather than appealing to both action gamers and
  strategy gamers, it seemed to fall in the crack between them." (Via
  filfre.net; likely original source is her offline game-design memoir.
  The often-quoted "between two stools" phrasing is a **paraphrase** — it
  appears verbatim in no accessible source.) [verified]
- Her contemporary framing (CGW, Nov/Dec 1982): the game is a "half-breed" —
  "either a strategy game with action or an action game with strategic
  elements." [verified]

---

## 7. Technical details

| Aspect | Apple II (original) | Atari 8-bit (port) |
|---|---|---|
| Code | 100% machine language; runs its own routines (SSI titles of the era typically needed 48K — **unverified** for this title) | Machine language; **boots its own OS replacement** (per Bunten's CGW article) |
| Graphics | Hi-res; Bunten was indifferent to visual polish | Display lists + DLIs (color changes per scanline), player/missile graphics for extra colors + fast animation |
| Sound | Apple speaker ("What are those little noises?") | POKEY, 4 voices — "truly impressive sound effects (at least as compared to the Apple)" |
| Timing | Multi-threaded software routines for real-time unit movement | Vertical-blank interrupts: logic + display "apparently at once" |
| Input | Game paddles + keyboard | Joysticks + keyboard shortcuts |
| Media | 5.25" disk; RDOS 2.1 format (per preserved image); later release was a **flippy disk** — Apple II one side, Atari the other | Same flippy or dedicated disk; a variant **"with prologue"** (added animated intro) is preserved separately |

Box art: futuristic robot-battle scene; artist uncredited — SSI house art of
the era was by **Louis Hsu Saekow / Louis Saekow Design** ("designed artwork
for most of [SSI's] products"), so Saekow attribution is *likely but
unconfirmed*. [unverified]

---

## 8. Surviving resources (with URLs)

### 8.1 Primary documents — START HERE

| Resource | URL |
|---|---|
| **Manual + "Programmer's Notes"** (scans + OCR text/EPUB). **Correction (2026-06-11):** the ~20 MB `Cytron_Masters_SSI_Programmers_Notes.pdf` is *not* a programmer's document — it is the 2-page **"Special Note to Atari Owners"** insert by Dan Bunten, scanned at very high resolution. It has been obtained and fully transcribed in `primary-sources/atari-owners-note.md`. The **Game Manual** scan in the same item remains the outstanding source for unit costs and energy numbers (it covers "Symbolic Warcraft," unit types, and troop management per the insert). | https://archive.org/details/CytronMastersStrategicSimulations (downloads: https://archive.org/download/CytronMastersStrategicSimulations/) |
| Manual mirror (login-walled) | https://www.scribd.com/document/529723010/Cytron-Masters |
| Bunten's own CGW article on the Atari port (full text) | https://vgpavilion.com/mags/1982/11/cgw/cytron-masters-for-atari/ |
| CGW review issue PDF (Vol 2.5) | https://cgwmuseum.org/galleries/issues/cgw_2.5.pdf |
| Atarimania page (box/manual scans, ads, instructions, ROMs) | https://www.atarimania.com/game-atari-400-800-xl-xe-cytron-masters_1476.html |
| Page 6 review | https://www.page6.org/archive/issue_06/page_14.htm |

### 8.2 Disk images

**Apple II:**
- archive.org `.dsk` (RDOS 2.1): https://archive.org/details/a2_Cytron_Masters_1982_SSI_b_RDOS
  — disk contains a `MAN.P` manual text file; `a2_` items are normally
  playable in-browser via Emularity.
- **4am crack** (clean deprotected dump, best for analysis/disassembly):
  "Cytron Masters (4am and san inc crack).zip" in
  https://mirrors.apple2.org.za/ftp.apple.asimov.net/images/games/strategy/ssi/
- Flux-level preservation (.a2r, original protected disk):
  https://archive.org/details/apple-ii-a2r

**Atari 8-bit:**
- https://archive.org/details/a8b_Cytron_Masters_1982_SSI_US_k_file
- With prologue: https://archive.org/details/a8b_Cytron_Masters_1982_SSI_US_with_prologue_k_file
- .ATR / .XEX mirrors: wowroms.com (IDs 69040, 74366); myabandonware.com/game/cytron-masters-l

### 8.3 Emulation

- Apple II: AppleWin, MAME, OpenEmulator, microM8 (cracked .dsk); WOZ-capable
  emulators for the flux dump.
- Atari: **Altirra** (most accurate), atari800, MAME a800.
- In-browser: archive.org Emularity players on the items above; Vizzed
  (http://www.vizzed.com/playonlinegames/game.php?id=5522).

### 8.4 Videos

- Apple II gameplay: https://www.youtube.com/watch?v=9D-z3dQwxcg
- Atari 800XL gameplay (closest to a longplay): https://www.youtube.com/watch?v=Sjs2qfpOGmU
- https://www.youtube.com/watch?v=csGW_kK9iQw ; https://www.youtube.com/watch?v=CgNIOkkGTQc
- Annotated screenshot playthrough: https://zeitgame.net/archives/3414

### 8.5 Source code & prior remakes

- **No public source code exists.** Possible lead: The Strong Museum of
  Play's **Dan Bunten / Dani Bunten Berry papers** (1949–2012) include
  "corporate agreements, notes, sketches... computer code" —
  https://archives.museumofplay.org/repositories/3/resources/42 (finding aid:
  museumofplay.org/app/uploads/2021/09/Finding-Aid-to-the-Dan-Bunten-Dani-Bunten-Berry-papers_091018.pdf).
  No confirmed Cytron Masters source in the indexed summaries — worth
  contacting The Strong. Note: M.U.L.E. and Seven Cities of Gold materials
  are donor-restricted until **2060**; Cytron Masters is not named in that
  restriction.
- **No fan remake found anywhere** (GitHub, awesome-game-remakes lists,
  forums). This project would apparently be the first.

---

## 9. Copyright / IP status

**Ownership chain of SSI's catalog [verified]:**
SSI → **Mindscape** (1994) → The Learning Company (1998) → **Mattel** (1999)
→ Gores Technology Group (2000) → **Ubisoft** (March 7, 2001; SSI brand
retired ~2002). Retro publisher **SNEG** actively licenses SSI classics from
this catalog for GOG/Steam (Gold Box, Phantasie, etc.) — **Cytron Masters is
not among them** and is not sold anywhere.

**Key uncertainties [important]:**
- It is **not verified that Ubisoft specifically owns Cytron Masters.**
  Early SSI titles were authored by outside developers under royalty
  contracts, and Bunten-family precedent exists for rights staying with /
  reverting to the estate: the **M.U.L.E. rights are controlled by the
  Bunten heirs**, who licensed M.U.L.E. Returns (2013). (M.U.L.E. was an
  EA-published Ozark title — a different contract — so this is precedent,
  not proof.) The original SSI publishing agreement may survive in The
  Strong's Bunten papers ("corporate agreements").
- **Copyright term:** a 1982 published US work is protected ~95 years →
  **under copyright until ~2078. It is not public domain**; "abandonware"
  listings have no legal force.
- **Trademark:** no USPTO registration for "Cytron Masters" surfaced;
  almost certainly never registered or long lapsed — verify at
  https://tmsearch.uspto.gov before shipping under the name.

**Practical guidance for the remake:**
1. Game **rules and mechanics are not copyrightable** — a from-scratch
   reimplementation with original code, art, sound, and text is the standard
   low-risk path.
2. Do **not** reuse original graphics, sounds, manual text, or box art.
3. The title itself is a (modest) risk; a new name or clearly-marked-homage
   title is safer until rights are clarified.
4. For a clean answer — or a blessing — the two concrete leads are **SNEG**
   (sneg.games; they deal with Ubisoft's SSI catalog) and the **Bunten
   family** (track record of licensing Dani's games; reachable via the
   M.U.L.E. projects / The Strong).

---

## 10. Design analysis — lessons for the remake

### 10.1 What the design got right (keep these)

1. **Map-control economy.** Capturable, indestructible generators that feed
   a single resource create constant, legible incentive to fight over the
   middle. Modern critics judge this core "very solid" (Wargaming Scribe:
   "this sure seems like a very solid proto-RTS in terms of design").
2. **The Commander as vulnerable force-multiplier.** Group orders + doubled
   movement range routed through a fragile, weaponless unit is the game's
   signature idea — a risk/reward command topology that most modern RTS
   still lacks. Protect-the-relay creates natural front-line structure.
3. **Tight asymmetric unit roster with hard counters.** Mine/bunker/shooter/
   commander/missile/anti-missile is a rock-paper-scissors web: bunkers
   absorb shots and block mines, mines kill everything else, shooters
   auto-fire, anti-missiles deny missiles. Cheap (1) to expensive (8) costs
   make build choices meaningful.
4. **Bunten's design criteria** (from her own retrospectives): model "very
   easy to describe"; decisions made "by 'doing' rather than 'telling'";
   multiplayer-first ("No one ever said on their deathbed, 'Gee, I wish I
   had spent more time alone with my computer.'"). Modem Wars' restatement:
   "a wargame for the rest of us — fast moving... not bogged down in
   minutiae."
5. **Onboarding.** An interactive tutorial plus a missile-practice scenario,
   in 1982. Keep that spirit.

### 10.2 Known failures (fix these)

1. **Fixed movement deltas.** Units move exactly 5 (solo) or 10 (commanded)
   spaces then halt — no destination selection. The Wargaming Scribe calls
   the "messiness of movement deltas" the design's biggest shame. A remake
   should allow free move targets while preserving the Commander's
   batching/range advantage by other means (e.g., order radius, cooldowns,
   or order-throughput limits).
2. **Weak AI.** Even "Grand Master" only challenges via energy cheating and
   is beaten after a couple hours of practice. The 1982 design was
   two-player-first with AI as fallback; a web remake can make online
   head-to-head the centerpiece (truest to Bunten) but still needs a
   credible bot for the empty-lobby problem.
3. **Battlefield legibility.** Period and modern players report the game
   "quickly sinks into confusion" at scale (up to 100 units). Modern UI —
   selection feedback, order queues, health/state indicators, minimal HUD —
   directly addresses the era's hardware-imposed opacity.
4. **APM pressure.** The real-time menu interface rewarded raw
   orders-per-minute. Decide deliberately how much dexterity should matter;
   Bunten's own trajectory (Modem Wars' simplified "war as sport") suggests
   she wanted *tempo*, not *twitch*.

### 10.3 Positioning

- Market it honestly as a revival of an **RTS precursor / real-time tactics**
  game: no base-building, one resource, small roster — "chess at speed with
  an energy economy." Its natural modern comparables are micro-RTS and
  head-to-head mobile tactics games, not StarCraft.
- The 1982 failure mode ("fall in the crack between" action and strategy
  audiences) is inverted today: that crack *is* the RTS audience. The modern
  risk is being judged against 30 years of refined conventions — hence fix
  §10.2 while keeping §10.1.
- Historical hook for marketing/press: first-ever remake of one of the first
  real-time strategy games, by the designer of M.U.L.E.

---

## 11. Open questions (answerable from the manual / Programmer's Notes / play)

Resolved 2026-06-11 from the "Special Note to Atari Owners" insert
(`primary-sources/atari-owners-note.md`):

- ~~Names/functions of all four main commands~~ → **MAKE, LOCATE, DIRECT,
  ORDER**; LOCATE moves the Transport Beam spawn point; DIRECT sub-menu is
  4 arrows + halt + destruct; ORDER cycles through up to **3 Commanders**.
- ~~Pause feature?~~ → **Yes (Atari): space bar pauses/resumes**; while
  paused, OPTION/SELECT/START reconfigure/restart. (Apple II pause still
  unconfirmed.)

Still open:

| # | Question | Best source |
|---|---|---|
| 1 | Anti-missile energy cost | Manual |
| 2 | Starting energy, energy cap, per-move/per-shot energy costs | Manual |
| 3 | Exact power-center coordinates; layout variation by level | Manual + emulator play |
| 4 | Command Center durability — mine-contact instant win only, or can shooters/missiles damage it? | Manual |
| 5 | Exact stationary-defense modifier (−20pp vs ×0.8 — sources ambiguous) | Manual / play |
| 6 | Missile blast radius (1-space radius vs "up to 4 units") | Manual / play |
| 7 | Apple II memory requirement (48K presumed) | Box/manual scans |
| 8 | $39.95 price confirmation | Period CGW ads (cgwmuseum PDFs) |
| 9 | Contents of the Atari "prologue" variant | Emulator play |
| 10 | Apple II pause; "three speed levels" vs Atari difficulty levels — how the options differ per platform | Manual + emulator play |
| 11 | Transport Beam placement limits ("almost anywhere on your side") and whether MAKE is interruptible | Manual + play |
| 12 | Commander order radius vs the insert (manual says 3 spaces) and 5/10-space movement verification | Manual + play |
| 13 | Who actually holds the rights (Ubisoft vs Bunten estate) | SNEG / Bunten family / The Strong's contract papers |

**Recommended next step:** obtain the **Game Manual** scan from the same
archive.org item (this environment's network blocks archive.org — upload it
to the session the same way as the insert) and extract the exact rule
constants into a `docs/research/rules-spec.md`. The 4am-cracked Apple II
disk is the ground truth for anything the manual leaves ambiguous.

---

## 12. Sources

Primary / period:
- Cytron Masters manual + Programmer's Notes (SSI, 1982) — archive.org/details/CytronMastersStrategicSimulations
- Dan Bunten, "Cytron Masters for Atari," Computer Gaming World Vol. 2 No. 6 (Nov/Dec 1982) — vgpavilion.com/mags/1982/11/cgw/cytron-masters-for-atari/
- Mark Botner, "Cytron Masters: Review and Analysis," CGW Vol. 2 No. 5 (Sep/Oct 1982) — cgwmuseum.org/galleries/issues/cgw_2.5.pdf
- Chris Smith, The Space Gamer #59 (Jan 1983); Softalk (Sep 1982); inCider (Aug 1983); Page 6 #6 (1983)

Retrospective / scholarly:
- Jimmy Maher, "Dan Bunten and M.U.L.E." (2013) and "The Designer's Designer" (2018), The Digital Antiquarian — filfre.net
- The Wargaming Scribe, "Game #40: Cytron Masters (1982)" — zeitgame.net/archives/3414 (most detailed modern rules/AI documentation)
- James Hague (ed.), Halcyon Days: Danielle Berry interview — dadgum.com/halcyon/BOOK/BERRY.HTM
- ANTIC Atari 8-bit Podcast, Interview 23: Alan Watson — ataripodcast.libsyn.com
- Carpe Ludum, 2023 interview with Bill Bunten, Jim Rushing, Alan Watson — carpeludum.com
- Carl Lund, The History of SSI Games — sites.google.com/site/ssihistory/Home
- Encyclopedia of Arkansas: Danielle Bunten Berry; Game Designers Remembered
- Wikipedia: Cytron Masters; Real-time strategy; Danielle Bunten Berry; Modem Wars; Strategic Simulations; RapidFire
- MobyGames; Atarimania; VideoGameGeek; GameFAQs review 167313; Hypoid RTS Retrospectives; VGChartz "History of Real-Time Strategy: The Birth (1981–1991)"; The Wertzone; Retro365 "RapidFire, Games from SSI"
- The Strong Museum of Play, Dan Bunten (Dani Bunten Berry) papers finding aid
- IP chain: Wikipedia (Strategic Simulations), gamepressure.com SSI history, TechRaptor/DLH on SNEG's SSI re-releases, Wikipedia (M.U.L.E. Returns)
