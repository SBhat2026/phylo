# Phylo — UX/UI pass + roadmap

Branch: `ux-cinematic-tree`. Nothing pushed. Serve locally with
`python3 -m http.server 8777` then open http://localhost:8777.

## ✅ Shipped this pass

### 1. Cinematic "Tree of Life" (replaces Taxonomy + Phylogeny tabs)
- One unified tree instead of two overlapping views. Root at left,
  grows rightward through the 7 ranks to the tips.
- The answer's lineage is a glowing **gold trunk**; every guess is a
  curved, tapered branch that follows the trunk as far as it matches,
  then peels away. **Warmer guesses diverge closer to the tip** — the
  warmth signal is now spatial, not just a %.
- The mystery is a pulsing `❔` reached by a dashed-gold "leap into the
  unknown." On win it **blooms into `⭐ <animal>`** at the crown.
- Vanilla SVG + CSS only (no libraries) — negligible perf cost, honors
  `prefers-reduced-motion`, keeps the calm feel.
- Plain-language scaffolding built in: axis caption (`◀ broad groups /
  species ▶`) and legend (`very close / getting warm / far off`).

### 2. Smart search (the search bar now helps people who don't know animal names)
- Casual group words: "big cat" → Felidae, "shark", "bird", "monkey",
  "whale", "snake", "rodent"… (see `GROUP_TERMS`).
- Trait / description / place search over notes+diet+range ("striped",
  "carnivore", "africa") with a small tag showing *why* it matched.
- Typo tolerance (bounded edit distance): "elefant"→elephant,
  "tigr"→tiger. Only surfaces when exact hits are scarce.
- One precomputed index (`buildSearchIndex`), ~a few ms once at load.

## 🔜 Recommended next (biggest lever → smallest)

1. **Self-teaching first run.** The tutorial is a wall of text. Replace
   with a 3-step interactive coach on the live board (guess any animal →
   watch its branch grow → "warmer branches climb higher"). Keep the
   text modal behind a "?".
2. **Warmth coaching line.** After each guess, one plain sentence:
   "Same class (Reptilia) — getting warm!" / "Different phylum — cold."
   Turns the % into something a non-biologist feels.
3. **Friendly rank labels.** Show "Group / Family / Kind" style hints
   alongside Kingdom/Phylum/... on hover or first exposure.
4. **Share card.** Wordle-style emoji grid of your warmth path + the
   tree image. This is the #1 growth driver for daily puzzles.
5. **Gamification, kept chill:** streak flames, "first try / top 10%"
   badges, a daily "how the world did" bar, gentle end-of-round confetti
   tied to the ⭐ bloom.
6. **Onboarding difficulty.** Default new visitors to **Easy** (curated
   ~100 well-known animals); today it defaults to Hard (full 2,760).

## ♿ Accessibility backlog
- Green/red proximity is colorblind-risky. The tree adds gold + spatial
  distance as redundant cues; extend that to the guess-card badges
  (add icons or text, not color alone).
- Add `aria-label`s / a text summary to the SVG trees for screen readers.
- Keyboard: tree nodes and mini-guess pills aren't focusable yet.

## Files touched
- `index.html` only. New: `renderTreeOfLife` + helpers, `buildLifeTrie`,
  `GROUP_TERMS`, `buildSearchIndex`, `editDist`, rewritten
  `updateAutocomplete`. Old `renderBranchTree`/`renderPhylogeny` left in
  place (dead) for easy rollback.
