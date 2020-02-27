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
- <Form>
- <Field>
- <FormSpy>: The new kid in the neighbourhood

Those components allow subscriptions to hooks to trigger re-renders so that it does not rerender it all.
<FormSpy> is to be able to display the <Form> information without having to rerender the whole form

Conclusion:
When working on a project, there are multiple considerations to take into account when choosing libraries to use:
- The complexity of your problem
- How extensible the library is
- Does it have an extensive amount of examples (example nextjs)
- The bundle size
- Most importantly does it make sense to you.

One metric that was noted as less important than it looks is github stars and npm downloads. Old projects always tend to have more of those just because they have been around for longer.



