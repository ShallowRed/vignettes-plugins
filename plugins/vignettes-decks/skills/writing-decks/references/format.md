# Deck format

The names a deck can use, read from the code that parses and renders it. The slide boundaries and the syntax of each component are in `render-module.md`, `explanation-kit.md` and `storybook.md`.

## Frontmatter

Validated against `DeckMetaSchema` of `@vignettes/core/deck`. An unknown key is kept and ignored; a malformed value is refused with the name of the key.

- `title`
- `lang`
- `theme`
- `syntax`, holding `split` (`separator`, `heading`)
- `storybook`
- `backgrounds`, holding `h1`, `h2`, `h3`, `default`
- `brand`
- `reveal`, holding `hash`, `transition`, `backgroundTransition`, `slideNumber`, `embedded`, `margin`, `minScale`, `maxScale`, `width`, `height`, `controls`, `progress`, `keyboard`, `touch`, `loop`, `fragments`, `fragmentInURL`, `help`, `showNotes`, `autoPlayMedia`, `preloadIframes`, `autoSlide`, `view`, `navigationMode` (`default`, `linear`, `grid`), `pdfMaxPagesPerSlide`, `pdfSeparateFragments`
- `code`
- `status`: `public`, `private`, `semi-private`
- `project`
- `accessPassword`

## Annotations

Written `:tag{…}` on a line of the slide. The parser reads them and removes them from the body.

- `:slide-background`: Background image of this slide
- `:pretitle`: Text above the title
- `:subtitle`: Text below the title
- `:layout`: Image, page or story beside, above, below or behind the text
- `:quicklink`: Link shown at the bottom of the slide

## Layouts

Set by the attributes of `:layout{…}`, read by `readLayout` of `@vignettes/core/deck`. A source without `media` goes to the right.

- `media` (`right`, `left`, `top`, `bottom`, `behind`), `right` by default: Place of the media: right, left, top, bottom or behind the text
- `size` (`1/3`, `1/2`, `2/3`, `3/4`): Share of the slide the media takes: of its width on a side, 1/2 by default; of its height at the top or the bottom, where the media takes by default the height the text leaves
- `src`: Address of the image or the web page
- `story`: Id of a story of the deck's Storybook, shown in the media pane
- `type` (`image`, `iframe`): Image or web page, for an address without an image extension
- `fit` (`cover`, `contain`), `cover` by default: cover fills the pane and may crop the edges, contain shows the whole media
- `position` (`center`, `top`, `bottom`, `left`, `right`), `center` by default: Part of the media kept when cover crops it
- `alt`: Description of the media for people who cannot see it
- `lightbox`: The media opens full screen on a click
- `hint`: Text at the bottom of the text column, with an arrow towards the media
- `viewport`, `1440` by default: Width in pixels the page or the story is laid out at before it is shrunk to the pane
- `veil`: Behind the text: dark veil over the image, as a percentage, with the text in a light color; without a veil, the text sits on a card
- `align` (`top`, `center`, `bottom`): Vertical alignment of the content: of the heading and the text on a title or a section slide, of the body under the heading on a content slide, of the text in its column beside a media, of the text card over an image. By default: centered; at the top for a caption column at 3/4 and for a text above or below a media; at the bottom for the card over an image
- `text` (`xs`, `sm`, `md`, `lg`, `xl`), `md` by default: Size of the body of the slide (text, lists, quotes and their spacing), from xs to xl around the size of the theme; the headings keep their size, and the text stays above the smallest size of the theme
- `inset` (`tight`): Margins of the slide halved, and lines of text without a maximum width (tight)
- `screen`: The body is a screen or a gallery of screens (`::StoryFrame`, `::Screens`): the heading keeps to one line and the screens take all the room it leaves. A screen without `ratio` fills its room, a screen with `ratio` takes the largest size at those proportions in it
- `heading` (`compact`, `hidden`, `print`): Heading on one line (compact), hidden, or hidden on screen only (print)

## Components

Written `::Name{…}` … `::` as a block, or `:Name{…}` inline.

`@vignettes/nuxt`, shipped with every deck:

- `Quote`: Quote, with its author
- `Iframe`: Web page shown in the slide
- `Image`: Image with its caption, also written `deck-image`
- `Mermaid`: Diagram of boxes and arrows, written as text
- `IconInline`: Icon in a sentence, also written `i`
- `Columns`: Blocks side by side, also written `TwoColumns`, `ThreeColumns`
- `Column`: One column of the block, also written `column`
- `Highlight`: Key message in bold, in the accent color, with a bar on its left
- `Notes`: Speaker notes, shown in the speaker view (S key), also written `notes`
- `Fragments`: List whose items appear one at a time, also written `fragments`

`@vignettes/schemas`, the explanation kit:

- `Scheme`: Illustrated steps linked by arrows, which appear one at a time, also written `scheme`
- `Step`: One illustrated step, also written `step`
- `Diagram`: Cards linked by arrows, placed on a grid, also written `diagram`
- `Node`: One card of the diagram, placed on the grid, also written `node`
- `Edge`: An arrow between two cards, also written `edge`
- `Area`: A region that groups cards, also written `area`
- `Sequence`: Exchanges between participants, one row per step, revealed one at a time, also written `sequence`
- `Actor`: One participant, at the head of its column, also written `actor`
- `Message`: An arrow from one participant to another, also written `message`
- `State`: The values the participants hold at that moment, also written `state`
- `Remark`: A text laid over the lifelines, also written `remark`
- `JsonTour`: File explained zone by zone, beside its explanations, also written `json-tour`
- `Zone`: Lines of the file, explained, also written `zone`

`@vignettes/storybook`, live story embeds:

- `StoryFrame`: Screen of a Storybook story, from its id
- `Screens`: Several Storybook screens side by side

## Earlier forms

Forms of the earlier format that a conversion rewrites into the current form, listed by `LEGACY_FORMS` of `@vignettes/core/deck`. Write the current form: the studio editor marks each earlier one and converts it.

- `parser` → `syntax.split`: Earlier form of `split` under the `syntax` key.
- `access` → `status`: Earlier form of `status`.
- `transition` → `reveal.transition`: No effect at the root: write the transition under the `reveal` key.
- `center`: No effect: write the vertical alignment of a slide in the `align` attribute of `:layout`.
- `:layout{name=…}` → `:layout{media=… size=…}`: Earlier form of the attributes of `:layout`: `name="media-right-wide"`, `previewWidth`, `title`, `raw`.
