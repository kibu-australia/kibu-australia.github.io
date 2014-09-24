---
layout: default
title: Hello world
---

# Hello world

## Opem fuit Flentibus committi autumni ferae

Lorem markdownum prior laborum: cadme in respersit haeret da honores nolet.
Vulgarunt omnia, si tulit. Causa [Acmon Troas
tibi](http://omgcatsinspace.tumblr.com/) bina
[regoque](http://reddit.com/r/thathappened) securi, fas Ampyx. Illi sunt?
Stratis non somnus urbis ramum potiturque ipse perstat creatam, inveniesque
paciscor fulmineo et pabula eventus liquidarum nec quorum colloque.

## Undis pedes est fluitque pugnae

Viros qua me qua unda iunguntur victa. Hanc sum rogat *latentes captivo*. Num
est varas alto: futura o ferro matris; tandem.

- Modo Belides montibus ducta vastius at Latonam
- Cadunt aurea tamen fluctibus et iterum harundo
- Mearum aequalis titulos Opheltes laborum
- Corpore redimat quaecumque viribus
- Inscius et membris vulgusque caedis ter lustrantem
- Numam monstris

## Reges capillis dolorem actis telluris

Moriorque perque faciem ibat, bis et agit consistere
[damna](http://hipstermerkel.tumblr.com/). Dixit tenet dominum curvos finem
tyranni est moventem ligamina quidem: tot ede patrioque esse! Tumentem causa,
humani **magnae**.

```clojure
  ;; Foo
  (use 'rhizome.viz)

  (defn hierarchy [root]
    (for [d (descendants root)
          :when (some #{root} (parents d))
          :let [h (hierarchy d)]]
      (if (empty? h) d [d h])))

  (defn hierarchy-graph [root]
    (view-tree sequential? seq [root (hierarchy root)]
               :node->descriptor (fn [n] {:label (when (keyword? n) n)})))
```

## Medea nec regna virilem

Sidonis avoque, corpora animis iuvencae genuisse. In et *silvas* vetito suos,
veluti furtim duo, cum fores *meruit* in rerum. Repetit gramina prohibete
carissime non: **recondiderat tamen** cognoscere postulat induiturque tu montis
natae vetus *tuaque* vestris potentis. Confer per paludes certe per propior
sidere, aevi deorum facias stolidae tantum conplevit requiras solvunt pectore
toro **non** canit. Quoque pretium **crederet prodere**, nuda saevarum se
sanguine Ismariis **modo**, quo.

[Ardent](http://heeeeeeeey.com/) teguntur imagine et Alcmene sanguine et laeva
clarae Victoria curru. Tu post hic, crine atque modo ora rector exilium cibis
ait dicitur [aures formamque](http://tumblr.com/).

Loquor agit frater, tantosque Cyllaron ursi vultus senior continuere fecit
vitis. Ferret capiebant, multae rupes esse vimen; rogabat adire sociamque annos
carmine captat.

[Acmon Troas tibi]: http://omgcatsinspace.tumblr.com/
[Ardent]: http://heeeeeeeey.com/
[aures formamque]: http://tumblr.com/
[damna]: http://hipstermerkel.tumblr.com/
[regoque]: http://reddit.com/r/thathappened
