---
name: writing-decks
description: >-
  Write or edit a deck for Vignettes, the presentation engine built on Nuxt,
  MDC and reveal.js. Use when authoring a Vignettes .md deck in any project,
  writing its outline, titles and slide text for its purpose (presentation of
  finished work, proposal to approve, workshop, demo, explanation),
  choosing its frontmatter and how it splits into slides, placing annotations (`:layout`,
  `:subtitle`, `:slide-background`), using its components (`::Columns`,
  `::Notes`, `::Scheme`, `::Diagram`, `::Sequence`, `::JsonTour`), embedding live Storybook
  stories (`:layout{story=…}`, `::StoryFrame`, `::Screens`), or preparing a deck
  to import, republish or freeze.
---

# Writing a Vignettes deck

A deck is one markdown document with YAML frontmatter, written in the dialect that `@vignettes/core` defines and `@vignettes/nuxt` renders with reveal.js. The names this dialect accepts are listed in `references/format.md`, generated from the code; the syntax of each part is in the package documentation copied beside it:

- `references/format.md`: frontmatter keys, annotations, layouts, components.
- `references/render-module.md`: frontmatter, slide boundaries, annotations, layouts and the components every deck has.
- `references/explanation-kit.md`: `Scheme`, `Diagram`, `Sequence`, `JsonTour`.
- `references/storybook.md`: live story embeds and frozen decks.

Use only the names these files list. An unknown component renders nothing, and an unknown layout falls back to the default one.

## Where a deck is written

- In the studio editor of a Vignettes instance: several people edit the same draft live, and publishing makes a version. The database of the instance holds the published version.
- In a content space (the `presentations/` directory of an instance, or another repository): the file is an archive or a stub. `mise run content:import` imports the stubs the database does not own yet, `mise run content:republish -- <slug>` republishes a deck from its file, and `mise run content:push -- <slug>` sends a stub to a deployed instance.
- In any other project, for a deck that will be imported later: write the file, then import it on the instance. The new presentation dialog of the studio takes the `.md` file and reads its title and theme from the frontmatter, which must give a `title`; it names the key of a refused value. The menu of a deck's card in the catalog downloads its published Markdown for whoever may read the deck, and its draft for whoever may edit it; the editor downloads both.

A file changed after its import changes nothing on the instance until it is republished.

## Writing the deck

Start from the frontmatter:

```yaml
---
title: One sentence that names the subject
lang: fr
theme: dsfr
---
```

By default, `---` and `----` lines cut the slides. With `split: heading` under `syntax:` in the frontmatter, the headings cut them. Pick one per deck.

With either rule, a `##` slide that holds its heading and at most one paragraph of 140 characters or fewer is a section, which the themes paint in contrast. A `##` slide with more content, a list, a component or a `:layout` takes the layout of a content slide. Write a section as its `##` heading alone, or with one short sentence under it.

One idea per slide: the heading places the slide in the deck, the body states the idea, and the subtitle adds a precision such as the state the slide describes. The detail goes to `::Notes`, which the speaker view shows, and vertical slides hold the depth a question might call for.

Before writing the slides, read `references/writing.md`: establish the need the deck answers, then follow its principles for the outline, the titles and the composition of each slide. The rules of the project and of the author of the deck take precedence over these principles.

## Live Storybook stories

Declare one Storybook root in the frontmatter (`storybook: https://…`) and name each story by its id, `<componentId>--<storyName>`, as the Storybook manager shows it after `/story/` in its address. The components build the iframe address from these two; a Storybook address pasted in a slide breaks the frozen copy of the deck.

- One story beside the text: `:layout{media="right" size="2/3" story="…"}`.
- Several side by side: `::Screens` holding `::StoryFrame` blocks.
- A slide that shows screens, with the detail in `::Notes`: `:layout{screen}` gives the screens the height the one-line heading leaves (`heading="hidden"` gives them the whole slide). Leave `ratio` out so each screen fills its room; with a `ratio`, two screens side by side keep the height their width allows.
- A screen takes clicks once the audience clicks it, so a story with a `play` function leaves the keyboard to the deck.
- `viewport` sets the width the story renders at before it is scaled to its frame: raise it to show more of the page, lower it to zoom in. Galleries of three columns or more read better with a lower value or `ratio="portrait"`.
- A local Storybook that is stopped leaves empty frames; a deployed one must allow being framed by the instance. Freezing the deck (`references/storybook.md`, section on frozen decks) serves the stories from the deck itself.

## Checking the deck

Open it in the studio editor or on `/slides/<slug>` of the instance, and read each slide at presentation size. The editor preview follows the cursor, so the slide under edit is the one on screen.
