# @vignettes/storybook

Embeds a live Storybook story in a slide. The slide loads the story from the published Storybook, and shows the component as that Storybook renders it when the deck opens.

```bash
pnpm add @vignettes/storybook
```

```ts
export default defineNuxtConfig({
  modules: ['@vignettes/nuxt', '@vignettes/storybook'],
})
```

A deck names its Storybook root in the frontmatter, and each embed names a story id:

```yaml
---
title: A deck
storybook: https://storybook.example.com
---
```

## One story beside the text

A `story` on the `:layout` annotation resolves to `<storybook>/iframe.html?id=<story>&viewMode=story` and renders as an iframe:

```markdown
### My component, live

:layout{media="right" size="2/3" story="home-scenario-a--page" lightbox}

What we are testing, next to the live story.
```

The value is the Storybook story id, `<componentId>--<storyName>`. `lightbox` lets a click open the story full-screen.

## Several screens side by side

`Screens` lays its `StoryFrame` children in a row. An iframe renders at its logical width and the frame scales it down to fit, so the frame shows the whole page. `StoryFrame` also works on its own in a slide body, without `Screens`.

A screen takes clicks from the first click on it: a story whose `play` function clicks, types or opens a drawer leaves the keyboard to the deck and to the editor. The first click on the screen outlines it and lets the next clicks reach the page; the pointer back on the slide, a click outside the screen or the next slide gives the keyboard back to the deck. A screen with `lightbox` opens full-screen on that first click.

## A slide made of screens

`:layout{screen}` gives the screens of the body the whole height the heading leaves, and keeps the heading to one line. A screen without `ratio` fills its room; with a `ratio`, it takes the largest size at that ratio, with its caption under it. `heading="hidden"` gives the screens the whole slide, and the notes hold the text:

```markdown
### Changer d'étape

:layout{screen}

::::Screens{cols="2"}
::StoryFrame{story="kanban--today" label="Aujourd'hui"}
::
::StoryFrame{story="kanban--proposal" label="Proposition"}
::
::::

::Notes
What the two screens show.
::
```

Side by side, two screens at `ratio="desktop"` keep the height their width allows; without `ratio`, each one shows the page at `viewport` width over the whole height.

### Screens

<!-- component: Screens -->

```markdown
:::Screens{cols="2"}
::StoryFrame{story="story-id" label="Label" lightbox}
::
::StoryFrame{story="story-id" label="Label" lightbox}
::
:::
```

Attributes:

- `cols` (`string | number`): Column count; defaults to an even auto-fit row.
- `gap` (`string`): CSS gap between the frames.
- `align` (`'start' | 'center' | 'stretch'`, default `'stretch'`): Vertical alignment of the frames in their row.

Content: The `::StoryFrame` blocks.

<!-- /component -->

### StoryFrame

<!-- component: StoryFrame -->

```markdown
::StoryFrame{story="story-id" ratio="16/9" viewport="760" label="Label" lightbox}
::
```

Attributes:

- `story` (`string`): Storybook story id (`<componentId>--<storyName>`).
- `src` (`string`): Explicit URL, used when `story` is absent.
- `type` (`'iframe' | 'image'`): Kind of media; without it, a story or an address is a page, and an address that ends with an image extension an image.
- `fit` (`'cover' | 'contain'`, default `'cover'`): CSS `object-fit` of an image in the frame.
- `ratio` (`string`): Aspect ratio: a name (`desktop` 16/10, `wide` 16/9, `classic` 4/3, `photo` 3/2, `square`, `mobile` 9/16, `portrait` 3/4) or a ratio such as `16/9`. Without it, the frame is `wide` outside a gallery, and fills its room on a `:layout{screen}` slide.
- `viewport` (`string | number`): Logical width (px) the iframe renders at before scaling; a higher value shows more of the page.
- `previewWidth` (`string | number`): Another name of `viewport`, read in the existing presentations.
- `raw` (`boolean`, default `false`): Renders the frame at its native size, without scaling.
- `label` (`string`): Caption under the frame; overrides the default slot.
- `lightbox` (`boolean`, default `false`): Opens the screen full-screen on click.
- `title` (`string`): Accessible title of the frame, or the text alternative of an image.
- `grow` (`boolean`, default `false`): Lets the frame grow to fill the available height, in a gallery.
- `hint` (`string`): Incentive text shown beside the frame to invite interaction.

Content: The caption under the frame, in markdown.

<!-- /component -->

## Frozen decks

`@vignettes/freeze` copies a built Storybook into the bundle and rewrites the embeds to point at that copy, so a frozen deck renders its stories from the bundle.
