# Writing the text of a deck

This file gives principles for the outline of a deck and for the composition of its slides. Each principle holds for some kinds of decks and not for others: the source and the context come with it, so the author of a deck can judge when it applies.

## The need, before the first slide

A deck answers a need, and the same subject makes very different decks depending on it. Before writing, establish:

- the purpose: inform a team, convince, get a decision, teach how something works, run a workshop, show a demo;
- the audience, and what it already knows of the subject;
- how the deck is used: projected with a speaker, read alone, or both (presented, then sent or archived);
- the length expected, in time or in slides, and the level of detail;
- the density of text the audience expects on a slide;
- what happens after the deck: a decision, a discussion, nothing.

When the request does not say it and the project holds no example of the same kind of deck, ask the author before writing.

## Where the constraints are written

A constraint on a deck comes from one of four levels, and each level keeps its own rules:

- these principles, for any deck;
- the kind of deck: the outlines and the exceptions in this file;
- the project: its theme, its vocabulary, its conventions, written in the instructions of its repository;
- the author: their writing rules, written in their own instructions.

When two levels disagree, the narrower one applies: the author's rule over the project's, the project's over this file. Write a new constraint at the level it belongs to, so that it applies to the next decks of that level.

## The presentation as a whole

- Plan the narrative before the slides, and check that it holds as a text, without the slides. (Martin Fowler, [Nail your narrative](https://martinfowler.com/articles/never-send-slides/nail-your-narrative.html).)
- Give the frame before the content: start from what the audience already knows, then bring what is new. In an explanation, name the parts of the mechanism before showing them work. (David Ausubel, advance organizers; Richard Mayer, pre-training principle, *Multimedia Learning*.)
- Put the main idea early. To a person who has to decide, state the recommendation first, then the reasons and the evidence. (Barbara Minto, [The Pyramid Principle](https://barbaraminto.com/concept).) To an audience asked to adopt a concept, show the current state everyone recognizes, then what could be, why it matters to them, and only then how, the result and the risks. (John Maeda, [Preso Recipe 2024](https://www.linkedin.com/posts/johnmaeda_preso-recipe-2024-a-simple-presentation-activity-7148372968031629312-JCVy); Nancy Duarte, *Resonate*.)
- Mark the parts of the deck: a section slide at the start of each part, and a reminder of the part on its slides. (Kosslyn et al., [PowerPoint Presentation Flaws and Failures](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2012.00230/full), 2012; Mayer, signaling principle.)
- Vary the form of the slides when the content calls for it: text, a screen, a diagram. Reveal a slide step by step when the speaker walks through an order; otherwise the slide is complete when it appears. (Mayer, segmenting principle.)
- The ten-minute attention span is a weak basis for pacing a deck. (Neil Bradbury, [Attention span during lectures](https://pubmed.ncbi.nlm.nih.gov/28145268/), 2016.) The reason to put the goal early is that the audience understands the details once it knows what they serve.
- A deck projected with a speaker holds little text, and the speaker says the rest. (Garr Reynolds, *Presentation Zen*; Mayer, redundancy principle.) A deck read alone is written like a document, in full sentences. (Nancy Duarte, [Slidedocs](https://www.duarte.com/resources/books/slidedocs/).) A deck used both ways keeps the slides short enough to be projected and complete enough to be read; the speaker's detail goes in `::Notes`.
- For a decision that needs a close argument, a written document read at the start of the meeting can serve better than slides. (Edward Tufte, [The Cognitive Style of PowerPoint](https://www.edwardtufte.com/?p=579).)

## Outlines by kind of deck

These outlines are starting points, adapted to the need. Each lists the `##` sections in order; leave out a section the deck has nothing for. The title slide gives the subject in its `#` heading, then a line with the kind of deck, its audience and its date (`Proposal for the team, November 2026`).

- Concept pitch: Current state, Vision, Why, How, Result, Risks, Questions.
- Proposal to approve: Context (with the current state and the measures), The proposal, with one slide per part so the audience can accept one part and not another, Cost, Decisions to take, Next steps.
- Presentation of finished work: Context, What was done, Lessons learned, Next steps.
- Workshop: Purpose of the workshop, Background (what the participants need to know to take part), Current state, Exercise (the question and the board the participants work on), Decisions (who does what, by when).
- Demo: Context (the need of the users), Demo, with one slide per step of the journey and its screen, What remains, Next steps.
- Explanation of how something works: Context, Concepts, How it works, with one slide per step of the mechanism, Special cases, Further reading.

## Titles, pretitles and subtitles

By default, a title names the nature of what the slide shows, with a word the audience already has in mind: a current state, an analysis, a proposal, a recommendation, an objective, or the name of the subject as the audience calls it (`Accessibility`, `End-to-end tests`). The audience places the slide in what it knows before reading it, as with an advance organizer. Titles of this kind would fit a deck on another subject; titles that count (`Three measures`), formulas in two parts (`Three steps, one PR at a time`) and phrases made for one slide do not help the audience place the slide.

The `:pretitle` and the `:subtitle` place the slide in the narrative of the deck: the part it belongs to, the state it describes and its date. They hold a marker or a precision; the content of the slide goes in its body.

Another practice puts the conclusion in the title, as a sentence of two lines at most, with the evidence in the body. (Michael Alley, [assertion-evidence](https://www.assertion-evidence.com); the horizontal logic of consulting decks, Cole Nussbaumer Knaflic, [storytelling with data](https://www.storytellingwithdata.com/blog/2013/12/horizontal-logic).) Studies by Alley's group find better comprehension with these titles in technical teaching; these studies are small, and they compare sentence titles with a bare topic title. When a deck is read alone or by a person who decides, write the message of each slide as a sentence at the top of its body, under a title that names its nature.

## The state each slide describes

The audience has to know which state a slide describes. Each content slide says it in its title (`Current state`) or in its subtitle, as a short marker; when all the slides of a section describe the same state, the sentence under the `##` heading says it once:

- current state: what it was read from, and the date (`Main branch, 11 November 2026`);
- measure: what was measured, and the period;
- trial: where it was made (`Branch proto/msw-trial`);
- proposal: `Proposal`;
- desired state: `Desired state`, when the way to reach it is still open;
- decision: `Decision`, with who took it and when.

A slide that compares two states names both: `Current state and proposal` as its subtitle, `Current state` and `Proposal` as the headings of its two columns.

## Composition of a slide

- A projected slide passes the glance test: the audience gets its main idea in about three seconds, then turns back to the speaker. (Nancy Duarte, [The Glance Test](https://www.duarte.com/resources/guides-tools/the-glance-test/).)
- Remove what does not serve the point of the slide. (Mayer, coherence principle.)
- Keep lists short and group their items: working memory holds about four groups. A list that would fill the slide goes in two or three `::Columns`, spread evenly; side by side, columns read as comparable blocks, so each column holds a block of the same kind, opened by a `####` heading when the heading introduces its content. (Kosslyn et al., 2012, limited capacity and perceptual grouping.)
- In a deck that is also read alone, write each item of a list as a sentence with a subject and a verb.
- Make a person or a team the subject of action verbs: `The team reviews each PR`, `We run Stryker by hand on one feature`. A tool may be the subject of one sentence that says what it does, on the slide that introduces it. Elsewhere, a tool or a concept named as the subject of verb after verb (`Mock Service Worker intercepts`, `ESLint refuses`, `the coverage shows`) reads as if the tools did the work of the team: write what the team does with the tool, or the state that results. A measure or a proposal does not show, prove or decide: write who reads it and what they conclude.
- Use the words the audience uses. A tool, a library or a service the audience may not know gets its own slide, with the subtitle `The tool`, before the first slide that uses it: what it is and what it does. Another unknown term is defined on the slide where it first appears.
- A slide that brings two things together starts from how each one works today, with its figures, then says what changes between them.
- Write a count, a date or a measure in the body, with its unit and its period. Its source, the command that produced it and the list of cases go in `::Notes`.
- A slide with a screen, a live story or a capture says what to look at in the `label` of each frame.

## Diagrams

- Draw a `Scheme`, `Diagram`, `Sequence` or `Mermaid` block when it explains a mechanism: exchanges in an order, a flow where each step depends on the one before, links the audience follows from one box to the next. The audience retains words better with a picture the speaker comments. (Mayer, multimedia principle.)
- Make the visual form match the meaning: what belongs together is grouped, what matters most stands out, and a change of appearance signals a change of content. (Kosslyn et al., 2012.)
- Place each label next to the element it names. (Mayer, spatial contiguity.)
- Write a list for items with no link between them, even when they would fit in cards: before drawing, write the content as a list, and keep the list when it says as much.
- Show the whole system first, with only the parts that take part in the exchange on screen at the start, and add the rest with fragments. Each diagram of a part that follows shows the place of the part in the whole, by the same cards or by an `Area`. (Mark Richards and Neal Ford, representational consistency, *Fundamentals of Software Architecture*, 2nd ed., chapter 23.)
- A diagram that uses dashes, colors or card variants has a `legend` that names each code; `references/explanation-kit.md` gives the meaning of each code. (Simon Brown, [C4 model notation](https://c4model.com/diagrams/notation): "Every diagram should have a key/legend".)
- A color comes with a text or an icon, for the people who do not tell colors apart. (RGAA, criterion 3.1; WCAG 2, success criterion 1.4.1.)
- To choose the component that fits what the slide explains, read the [components page](https://vignettes.io/docs/ecrire/composants) of the documentation site.
