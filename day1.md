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
Measuring impact of changes is hard 
use pw metrics
perfomance.api
But one thing is to always record wins and losses.

## Talk 7: Engineering led design

A mindset of shars behaviours

Create a context together:
1. shared context for making good decisions
2. create a dictionary
3. teach as you work
4. play it back to validate
5. break dowm barrier language

1.
Everyone attends all problem solving meetings (initially)
Engineers to attend/facilitate user research sessions
Educate the designer about the __hard problems__ in software such as timezones

2. 
Naming is hard and language barrier exists, take time to define words

- create shared documents that anyone can add to
- define project specific terms (data-structure etc)
- DYFA: Define Your Freaking Acronyms, they might be different for everyone
- practice-specific jargon

3.

Learning from each others makes most of the diversity or thoughts
Adding short lessons (30mins) in a day to day or whenever needed.
make that a firt citizen of day to day to day.

4. Play it back to validate

playback often
always "let me play that back to you"
be playback aware

5. 
Practice empathy
Engineers need to do the translation for designer to get on board
Ask questions "Did that make sense"
Rephrase instead of saying the same things louder

Why should we bother?

- design more aligned to engineering thinking
- easier to negotiate constraints
- faster/better decisions

TALK 8: Take a load off

1. Common problems about data fetching
There are different ways of handling fetching:
- Fetch on render
- Fetch then render
- Render as you fetch

Details matter

Apollo client (not only for GraphQL0
urql
relay ( facebook's version of Apollo)

react-loads.dev
hooks for data fetching in react

TALK 9: From senior to leader: Taking the next step

The next step in a career can be:
- technical
- new direction
- better at current role

You can always grow in different directions

Front-enders might be perceived as:
- not technical enough
- their skillset is misunderstood
- have an unclear career path outside of specialty
- lack of senior mentors that share your experience

What would you do if you were asked "what would you say you do here"?
- What value can we demonstrate? 
- You need the skills to communicate your value
- what skills do we have
- How can we leverage and grow those skills

|technical expertise|Product stewardship|leadership and management|

We work on the interaction of human and technical concerns

1. 
Understand what engineering excellence is
Understand our environment, context, constraints
Understand system level architecture

We build reliabel, saclable technology in a complex and volatile environment every day
Awareness of entire systems, we need to communicate that

2
Understand and execute the big picture
Make sound product decisions
Advocate and communicate what is best for user 
Advocate and communicate what is best for tech decisions

We are the custodians of the User Experience and customer value
We advocate for the users all the time, a11y is important, make sure performance is OK, thinking about connectivity.

We make better tech decisions if we make better product decisions.

3. 
We take responsibility for long term outcomes
We lead coach and mentor effectively
We manage positive changes
We are a vibrant, supprtive tech community
We care about teaching and learning from each others
Developers should not hesitate to teach and mentor, go out to do it
We learn how to communicate

But as front end developers we should also learn to:
1
Broaden your tech knowledge
Participate in decision making
Develop your tech vocabulary
2
Participate in product meeting
develop well informed product opinions
3
Mentor, coach and teach
Seek opportunities to manage and delegate
Persuasive speaking and writing skills

TALK 10 Targeted Extensibility: Atlaskit 
@tetrisburger

Design Systems
