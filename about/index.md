---
title: About
layout: page
---

This website recounts the known history of Okupi, a weird fantasy world initialized with [Fractal Terrains](https://secure.profantasy.com/products/ft.asp), brought to some form of perfection with the [Dawn of Worlds](http://www.clanwebsite.org/games/rpg/Dawn_of_Worlds_game_1_0Final.pdf) RPG.  Further stories are created by yet to determine characters which will live their lives according to the rules of *Dungeons and Dragons, fifth edition*.

---

Some other basic information:

- The posts are meant for our group only.
- Sometimes you will encounter some secret text, encrypted by GPG.  To decrypt this nicely in your browser, we advice you to install the [WebPG](https://webpg.org/) plugin, which is available for Firefox and Chrome.
- Writing some secret text follows the following format:

  > <pre>
  > BEGIN SECRET INFO
  > For: $NAMES
  >
  > $MESSAGE
  > END SECRET INFO
  > </pre>

  A [vim plugin](https://github.com/pkok/vim-gnupg-snippets) can automatically decrypt and encrypt a `SECRET INFO` block, if you are allowed to read the text.  `$NAMES` is a comma-separated list of unique identifiers ((parts of) names, email addresses and public key fingerprints).  The colon (`:`) is optional.  
- Referring to parts of the map can be done in two ways:
  - Named areas and paths can be referred to by linking to `/map/#AreaName`.  If the object is not contained in `_data/map_areas.yml` yet, please add it, and consider using only `a-z` and `A-Z`.
  - Unnamed areas can be referred to by linking to `/map/#x1,y1,x2,y2,...`.  Unnamed paths can be referred by adding a `p`: `/map/#px1,y1,x2,y2,...`.
