# @vignettes/schemas

Deck components that explain a system on a slide: pictogram steps linked by arrows, diagrams whose cards sit on a grid or are ranked automatically, exchanges between participants over time, one row at a time, and a file read beside the description of what it holds.

```bash
pnpm add @vignettes/schemas
```

```ts
export default defineNuxtConfig({
  modules: ['@vignettes/nuxt', '@vignettes/schemas'],
})
```

The module registers its components globally and declares them to the deck contract, so `::Scheme` and the others resolve in a deck body and the parser knows their shape.

Pictograms come from `/pictograms/<folder>/<name>.svg`, served by the application from its public directory or its content space. A pictogram of the content space follows the DSFR file format: the symbols `artwork-decorative`, `artwork-minor` and `artwork-major`, which the studio draws in the colors of its color mode. A `boolean` or `number` attribute takes a colon and a JSON value, as `:fragments="false"`.

## Scheme

`Scheme` lays its `Step` children in a row linked by arrows. Each step is a fragment by default, so the row builds up as the speaker talks. With `dim`, the steps already shown fade once a later one is current, and the current step takes an accent frame.

<!-- component: Scheme -->

Also written `scheme`.

```markdown
:::Scheme
::Step{n="1" picto="buildings/city-hall" title="First step"}
Caption
::
::Step{n="2" picto="digital/coding" title="Second step"}
::
:::
```

Attributes:

- `fragments` (`boolean`, default `true`): Reveals each step as a fragment; `:fragments="false"` shows the whole row at once.
- `dim` (`boolean`, default `true`): Dims the steps already shown once a later one is current.
- `arrows` (`boolean`, default `true`): Links the steps with arrows; `:arrows="false"` gives a plain row of cards.
- `size` (`'sm' | 'md' | 'lg'`, default `'md'`): Scale of the pictograms.
- `tiles` (`'column' | 'row'`, default `'column'`): Card shape for every `::Step`: pictogram above the text, or beside it.

Content: The `::Step` blocks of the row.

<!-- /component -->

### Step

<!-- component: Step -->

Also written `step`.

```markdown
::Step{picto="digital/coding" title="Step"}
Caption
::
```

Attributes:

- `picto` (`string`): Pictogram, as its path under `/pictograms` without the extension: `digital/coding`.
- `icon` (`string`): Remix icon, `ri:server-line`, lighter than a pictogram.
- `title` (`string`): Title of the step.
- `n` (`string | number`): Step number shown in a badge.

Content: The caption, in markdown.

<!-- /component -->

## Diagram

`Diagram` places cards on a grid or ranks them automatically, and links them by drawn arrows. `step` on a node or an edge moves it in the order of the fragments.

<!-- component: Diagram -->

Also written `diagram`.

```markdown
:::Diagram{layout="grid" cols="2"}
::Node{id="a" at="1,1" title="Source"}
::
::Node{id="b" at="2,1" title="Destination"}
::
::Edge{from="a" to="b" label="feeds"}
::
:::
```

Attributes:

- `layout` (`'grid' | 'auto'`, default `'grid'`): `grid` places each node at its `at` cell; `auto` ranks the nodes with dagre and ignores `at`.
- `cols` (`string | number`, default `3`): Number of grid columns.
- `columns` (`string`): Column tracks as a CSS `grid-template-columns` value; overrides `cols`.
- `rows` (`string | number`): Number of grid rows; the grid takes as many as its nodes need when absent.
- `direction` (`'LR' | 'TB'`, default `'LR'`): Rank direction for the automatic layout: left to right or top to bottom.
- `size` (`'xs' | 'sm' | 'md' | 'lg'`, default `'md'`): Scale of the cards; `xs` leaves room for the arrows and their labels in a stack of cards.
- `fragments` (`boolean`, default `true`): Shows the nodes and the edges one at a time, in writing order; each edge appears with the later of its nodes.
- `dim` (`boolean`, default `true`): Dims the nodes already shown once a later one is current.
- `nodeWidth` (`string | number`, default `200`): Card width in px for the automatic layout (grid cells size their own).
- `height` (`string | number`, default `460`): Height budget in px for the automatic layout; a taller graph is scaled down. The legend adds its own height below this budget.
- `gap` (`string`, default `'1.2em 3em'`): Grid gaps as `row column` CSS lengths.
- `route` (`'curve' | 'orthogonal'`, default `'curve'`): Default edge route: curved, or orthogonal elbows.
- `cards` (`'outlined' | 'plain'`, default `'outlined'`): Card surface: `outlined`, a white card with a border, or `plain`.
- `tiles` (`'column' | 'row'`, default `'column'`): Card shape for every `::Node`: pictogram above the text, or beside it.
- `legend` (`string`): Key of the codes the diagram uses, `code=meaning` separated by `|`: `dashed` for a dashed arrow, `solid` for a plain one, `planned` for a dashed card, `emphasis` for the accent card, `flow` for a data pill, or a color as `color` takes it: `dashed=Asynchronous message|planned=Target state`. Shown under the diagram with the slide.

Content: The `::Node`, `::Edge` and `::Area` blocks.

<!-- /component -->

### Node

<!-- component: Node -->

Also written `node`.

```markdown
::Node{id="id" at="1,1" title="Title"}
::
```

Attributes:

- `id` (`string`, required): Name the `::Edge` blocks use to reach the node.
- `at` (`string`): Grid cell as `col,row` (1-based), for `layout="grid"`.
- `span` (`string`): Cells spanned as `cols,rows`.
- `picto` (`string`): Pictogram, as its path under `/pictograms` without the extension: `digital/coding`.
- `icon` (`string`): Remix icon, `ri:server-line`, lighter than a pictogram.
- `color` (`string`): Color of the icon and the title: a palette name of the theme, such as `green`, or a hexadecimal color or a color function, such as `#2a7f62`.
- `title` (`string`): Title of the card.
- `n` (`string | number`): Number in a badge.
- `planned` (`boolean`): Draws a dashed card, for a target state.
- `step` (`string | number`): Fragment step; defaults to the writing order.
- `variant` (`'card' | 'entity' | 'flow' | 'plain'`): `entity`: left-aligned box whose caption lists attributes, one per list item. `flow`: a pill for the data that travels between two machines. `plain`: title and caption without a card, for a row or column heading.
- `emphasis` (`boolean`): Fills the card with the accent, for the node the slide is about.
- `orientation` (`'column' | 'row'`): Pictogram above the text or beside it; defaults to the diagram's `tiles`.

Content: The caption, in markdown; with `variant="entity"`, a list of attributes, one per item.

<!-- /component -->

### Edge

<!-- component: Edge -->

Also written `edge`.

```markdown
::Edge{from="a" to="b" label="label"}
::
```

Attributes:

- `from` (`string`, required): `id` of the node the arrow leaves.
- `to` (`string`, required): `id` of the node the arrow reaches.
- `label` (`string`): Text on the arrow.
- `dashed` (`boolean`): Draws a dashed arrow, for an asynchronous message: the sender goes on without waiting for an answer.
- `arrow` (`boolean`): `false` leaves the arrowhead off, for the leg that reaches a flow box.
- `step` (`string | number`): Fragment step; defaults to the later of the two nodes.
- `anchors` (`string`): Sides to leave and enter by, `from,to` (`top` | `right` | `bottom` | `left`); without it, the sides follow the position of the cards.
- `route` (`'curve' | 'orthogonal'`): Route of this arrow, over the `route` of the diagram.

<!-- /component -->

### Area

`Area` draws a named region behind the cards, so an arrow leaving it reads as data going from one machine to another. Regions show with the slide, outside the fragment order.

<!-- component: Area -->

Also written `area`.

```markdown
::Area{at="1,1" span="2,1" title="Area"}
::
```

Attributes:

- `at` (`string`): Grid cell the region starts at, `col,row` (1-based).
- `span` (`string`): Cells spanned as `cols,rows`.
- `title` (`string`): Name of the region.
- `picto` (`string`): Pictogram, as its path under `/pictograms` without the extension: `digital/coding`.
- `icon` (`string`): Remix icon (`ri:server-line`), lighter than a pictogram on a dense diagram.
- `tone` (`'neutral' | 'subject'`): `subject` tints the region the slide is about; `neutral` is the default.
- `color` (`string`): Color of the title, the surface and the outline of the region: a palette name of the theme, such as `green`, or a hexadecimal color or a color function, such as `#2a7f62`.
- `label` (`'legend' | 'header'`): Where the title sits: on the top border like a legend, or as a header band inside.

<!-- /component -->

## Sequence

`Sequence` shows exchanges between participants over time. Each `Actor` heads a column and draws its lifeline. Each row child takes one row of the grid and appears as one fragment: `Message` draws an arrow between two lifelines, `State` lays side by side the value each participant holds at that moment, and `Remark` lays a short text over some lifelines. The time of a row, or the name of a state, sits in the left margin. The rules of the rows are drawn from the start, so the sequence keeps its height while it builds up.

<!-- component: Sequence -->

Also written `sequence`.

```markdown
:::Sequence
::Actor{id="a" icon="ri:user-line" title="User"}
::
::Actor{id="b" icon="ri:server-line" title="API"}
::
::Message{from="a" to="b" time="10 h 00" label="Request"}
::
::State{label="State" values="a=Draft|b=Sent"}
::
:::
```

Attributes:

- `fragments` (`boolean`, default `true`): Reveals the rows one at a time; `:fragments="false"` shows the whole sequence at once.
- `dim` (`boolean`, default `true`): Dims the rows already shown once a later one is current.
- `size` (`'sm' | 'md'`, default `'md'`): Scale of the cards and the text; `sm` fits about ten rows on a slide.
- `enter` (`'start' | 'first-row'`, default `'start'`): When the participants appear: `start`, all of them with the slide; `first-row`, those of the first row and those no row names with the slide, each other one with the first row that names it, in a column kept for it from the start.
- `legend` (`string`): Key of the codes the sequence uses, `code=meaning` separated by `|`: `dashed` for a dashed arrow, `solid` for a plain one, or a color as `color` takes it: `dashed=Answer`. Shown under the sequence with the slide.

Content: The `::Actor` blocks, then the `::Message`, `::State` and `::Remark` rows in reading order.

<!-- /component -->

### Actor

<!-- component: Actor -->

Also written `actor`.

```markdown
::Actor{id="id" icon="ri:user-line" title="Participant"}
::
```

Attributes:

- `id` (`string`, required): Name the rows use to reach the participant.
- `title` (`string`): Name of the participant.
- `icon` (`string`): Remix icon, `ri:user-line`, lighter than a pictogram.
- `picto` (`string`): Pictogram, as its path under `/pictograms` without the extension: `digital/coding`.
- `color` (`string`): Color of the icon and the title: a palette name of the theme, such as `green`, or a hexadecimal color or a color function, such as `#2a7f62`.

<!-- /component -->

### Message

<!-- component: Message -->

Also written `message`.

```markdown
::Message{from="a" to="b" label="label"}
::
```

Attributes:

- `from` (`string`, required): `id` of the participant that sends.
- `to` (`string`, required): `id` of the participant that receives.
- `via` (`string`): `id` of the participants the arrow goes through, separated by commas; each takes a dot.
- `label` (`string`): Text above the arrow.
- `time` (`string`): Time written in the left margin, `10 h 00`.
- `dashed` (`boolean`): Draws a dashed arrow, for an answer.
- `step` (`string | number`): Fragment step; defaults to the reading order.

<!-- /component -->

### State

<!-- component: State -->

Also written `state`.

```markdown
::State{label="State" values="a=value|b=value"}
::
```

Attributes:

- `values` (`string`, required): Values on the lifelines, `id=value` separated by `|`: `a=Draft|b=Sent`.
- `label` (`string`): Name of the state, written in the left margin.
- `color` (`string`): Tints the row and frames the values: a palette name of the theme, such as `orange`, or a hexadecimal color or a color function.
- `mark` (`string`): `id` of the values framed in `color`, separated by commas; all of them when absent.
- `step` (`string | number`): Fragment step; defaults to the reading order.

<!-- /component -->

### Remark

<!-- component: Remark -->

Also written `remark`.

```markdown
::Remark{over="a,b"}
Remark
::
```

Attributes:

- `over` (`string`): `id` of the first and the last participant the remark covers, separated by a comma; all of them when absent.
- `time` (`string`): Time written in the left margin, `10 h 00`.
- `color` (`string`): Color of the remark: a palette name of the theme, such as `orange`, or a hexadecimal color or a color function.
- `step` (`string | number`): Fragment step; defaults to the reading order.

Content: The text of the remark.

<!-- /component -->

## JsonTour

`JsonTour` shows a file beside the description of what it holds. The fenced code block of its content becomes a panel pinned to the right of the slide. Each `Zone` is a fragment that highlights the `lines` it names and scrolls the panel to them.

A deck that spreads a tour over several slides, one zone per slide, sets `:fragments="false"` and `:current="true"` on the zone of each slide, which takes the accent frame of the current step. With `image`, each `Zone` names with `spot` the area of the image it frames while the rest dims.

<!-- component: JsonTour -->

Also written `json-tour`.

````markdown
:::JsonTour{file="example.json"}
::Zone{lines="2-3" title="Identity"}
What these lines hold.
::

```json
{
  "name": "example",
  "version": 1
}
```

:::
````

Attributes:

- `file` (`string`): File name shown above the code panel.
- `height` (`string`, default `'330px'`): Maximum height of the code panel, in slide pixels.
- `panel` (`string`, default `'47%'`): Width of the code panel, any CSS length.
- `size` (`'xs' | 'sm' | 'md'`, default `'sm'`): Scale of the zone cards.
- `fragments` (`boolean`, default `true`): Shows the zones one at a time.
- `stack` (`boolean`, default `false`): Puts the code panel under the zones, at full width, for a narrow column beside a media pane.
- `image` (`string`): Screenshot shown beside the tour; the current zone's `spot` is highlighted on it.
- `alt` (`string`): Text alternative of `image`.
- `mark` (`string`): Words of the file to paint, separated by `|`; a word matches whole.
- `underline` (`string`): Words of the file to underline, separated by `|`; a word matches whole.

Content: The `::Zone` blocks, then a fenced code block: the file shown in the panel.

<!-- /component -->

### Zone

<!-- component: Zone -->

Also written `zone`.

```markdown
::Zone{lines="1-4" title="Title"}
What these lines hold
::
```

Attributes:

- `lines` (`string`): Line range in the file, `12` or `12-24`.
- `spot` (`string`): Area to highlight on the tour's image, `x,y,w,h` in percent.
- `picto` (`string`): Pictogram, as its path under `/pictograms` without the extension: `digital/coding`.
- `icon` (`string`): Remix icon (`ri:shield-check-line`), sharper than a pictogram at the xs and sm sizes.
- `title` (`string`): Title of the zone card.
- `n` (`string | number`): Number in a badge.
- `step` (`string | number`): Fragment step; defaults to the writing order.
- `current` (`boolean`): The step this slide is on, for a tour whose steps a deck spreads over several slides.
- `mark` (`string`): Words of its lines to paint while the zone is current, separated by `|`.
- `underline` (`string`): Words of its lines to underline while the zone is current, separated by `|`.

Content: What these lines hold, in markdown.

<!-- /component -->

## Colors

`color` on a `Node` or an `Area` takes the name of a palette entry of the theme, such as `color="green"`, or a hexadecimal color or a color function, such as `color="#2a7f62"` or `color="oklch(55% 0.1 160)"`. The node takes the color for its title and its icon; the region takes it for its title, and mixes from it its surface and its outline. `@vignettes/theme-kit` defines `blue`, `green`, `yellow`, `orange`, `brown`, `pink`, `purple` and `grey`, and a theme adds names of its own: the `dsfr` theme adds the DSFR illustrative palette, such as `green-emeraude`. A name the theme leaves undefined takes the accent.
