# React-conf-2020 Day 1

## Keynote:

From Max Stoiber @mxstbr

Ran down a little history of css-in-js. 
The first years were full of new ideas and improvments, open source projects were pushing each other to be better.
No major changes since 2017

Call out for us developers to experiment in that area. Using the following mantra:
- make it work, then make it right, then make it fast
- share early and share often
- document all the things

## Talk 1: Themability is the path to dark mode
@broccolini
Colors is something that always changes
Dark mode is one of the features that is asked the most for github
One line of code to update all the things

Experimented using:
- styled-components
- styled-system

Design system split in 3 layers:
- Layout
- Common
- Theme

css-in-js is the perfect tool to achieve that

jxnblk.com/blog/design-graph

The colors name are moved from presentational to functional i.e. `green` => `primary`

The path to dark mode is not as straight forward as just inverting the colors hue and saturation. The outcome of that is not the best
There is a lot of tweeking necessary, especially to keep the color scheme accessible.

To discover more about design systems => Rune Madsen

programmingdesignsystems.com
theme-ui.com

github.com/github/primer/components/css
github.com/github/actionview-component

`Perfect is the enemy of good - Voltaire`

## Talk 2 (Proto)Typing innovation at BBC

BBC Labs
- Experimenting new tools and ideas
- Releasing prototypes in 6 weeks

Examples: Skippy
using react-dnd and react-sortable-tree
Transcription: For 1 hour of media it takes 3-4 hours to curate

Led to OCTO

react-transcript-editor
using Draft.js => steep learning curve
immutable.js

Prolematic:
- Scaling a prototype is painful. Draft is unmainainted and does not scale well
- => <Advice> For anything complex: Build an abstraction layer over big external dependencies in case changes are needed </Advice>
- <Advice>Get what you can for free </Advice>

## Talk 3 - Modern forms in react

There are 2 forms of inputs for a form. Controlled and uncontrolled
Controlled: provided with a `value` prop
Uncontrolled: provided without a `value` prop

An undefined `value` makes it an uncontrolled value.

`useState` hook is great for smaller forms (such as google, twitter and facebook's most used forms)
But for more elaborate forms it gets complicated with `useState` because the state of a form is quite complex:
- Field
- Valid/Invalid
- Dirty/Pristine
- Validation errors: Form errors or Field errors
- For fields, are they: active, visited, touched, modified, submitting, submitsuccess/errors, dirty since last submit

Redux Forms:
The feedback on redux form was good but some people were asking:
- Why is it only react
- Why do I have to use redux
- Why so much rerendering
- Why is it over 27kB gzipped

So he decided to work on the perfect form library:
- Pure JS
- Framework agmostic
- Subscription based
- modular/pluggable solution

final-form.org
react-final-form

Migration guides are available to move from Redux Forms or Formik to react-final-form

There are 2 main components (the API is quite similar to redux forms):
- `<Form>`
- `<Field>`
- `<FormSpy>`: The new kid in the neighbourhood

Those components allow subscriptions to hooks to trigger re-renders so that it does not rerender it all.
`<FormSpy>` is to be able to display the <Form> information without having to rerender the whole form

Insert examples here

Conclusion:
When working on a project, there are multiple considerations to take into account when choosing libraries to use:
- The complexity of your problem
- How extensible the library is
- Does it have an extensive amount of examples (example nextjs)
- The bundle size
- Most importantly does it make sense to you.

One metric that was noted as less important than it looks is github stars and npm downloads. Old projects always tend to have more of those just because they have been around for longer.

## Talk 4: Beautiful drag and drop

Alex came on stage to explain to us the logic behind the beautifull drag n drop library he created. 
Write about magic, He is a magician, illusion.
It is sensor based.
Supports a11y
For more information: blog beautiful interaction

# Talk 5: Ten X your dev team with pair programming

An act by Michael and ..., starting with showing us what not to do when pair programming followed by a better approach to it, introducing ping-pong programming (one engineer writes test while the other one implements the functionnality)

The key points to take out of this act are:
- Prepare ergonomics, desk to be prepared for pairing
- Eliminate distractions as much as possible
- Take regular breaks
- Plan what you are going to pair on
- Work on the plan
- Have a retrospective at the end of the day

## Talk 6: Faster page load for react

There are several possible architecture when it comes to rendering:

Client side rendering, SSR, SSR + Data Hydration, Progressive Hydration (Suspens)

Your architecture and technical choices are not going to make the render faster. It should be an iterative work, of measuring and improving. The hard part is what to measure?

Existing tools: Lighthouse performances

It is a good tool but ultimately, the choice is yours on what metrics suits your needs
The metrics they used at ABC

|Initial Render|React hydration|Third parties|
|---|---|---|

Inital render:
- Fixed cache headers
- gzipped what was not gzipped
- Font swapping
- Preloading resources (not all of it, example, only 3 of the 3 necessary font files)
- Lazy loading images (Using the intersection observer)
- Above the fold should not wait for javascript

loading=lazy comming to html

React hydration:
- Use the nomodule hack
- Avoid transpilling for modern browsers
- Dynamic imports and bundke scripting ( use webpack analyse)
- `<loadable components>`
- react profiling for accidental re-render

Third parties:
2/3 of the javascript loaded on a page is third party (google analytics, etc)

- Looks for libraries helping you to load as less as possible
For example `lite-youtube` to load everything only once the user clicks on it


Conclusion:
Lighthouse is not a silver bullet, there is 15% treshold


