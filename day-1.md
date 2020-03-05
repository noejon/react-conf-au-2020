# React-conf-2020 Day 1

## [Keynote CSS-in-JS](https://reactconfau.com/talks/css-in-js)

By [Max Stoiber](https://twitter.com/mxstbr)

past, present and future of CSS in JS/styled components.

CSS in JS =>  CSS  -> applied via a hash-based class in the HTML.

Benefits

- confidence: any given style is only used in one known place
- painless maintenance: stylesheets becoming too big and maintaining it appending new classes at the bottom
- enhanced teamwork: no need for the whole team to have an encyclopedic knowledge of CSS
- fast performance: only the CSS you need for the current view is loaded
- dynamic styling: theming in CSS in JS is highly dynamic

CSS in JS guides you to the “pit of success”.
Does not mean you can’t fuck it up!
But it means you won’t have some of the common problems. 
It’s popular – 60% of React installs also install a CSS-in-JS library.

Ran down a little history of css-in-js. 

- Nov 2014: [JSS](https://github.com/cssinjs/jss)
- Nov 2014: [@vjeux](https://github.com/vjeux)
- Jan 2015: [Radium](https://github.com/FormidableLabs/radium)
- Feb 2015: [Rebass](https://github.com/rebassjs/rebass)
- May 2015: [CSS Modules](https://github.com/css-modules) - not CSS-in-JS but popularised hashed classnames
- Sep 2015: [CSJS](https://github.com/rtsao/csjs) - introduced strings of CSS instead of CSS in JS objects
- Oct 2015: [Aphrodite](https://github.com/Khan/aphrodite) - critical CSS extraction
- Jun 2016: [Fela](https://github.com/robinweser/fela) - style as function of state
- Jul 2016: [Glamor](https://github.com/threepointone/glamor) - performance by skipping DOM
- Oct 2016: [jsxstyle](https://github.com/jsxstyle/jsxstyle)
- Oct 2016: [styled-components](https://github.com/styled-components) - popularised the styled API
- Dec 2016: [styletron](https://github.com/styletron/styletron)
- Dec 2016: [styled-jsx](https://github.com/zeit/styled-jsx)
- Mar 2017: [Astroturf](https://github.com/4Catalyzer/astroturf) - extracted styles out to .css file
- Apr 2017: [Glamorous](https://github.com/paypal/glamorous)
- May 2017: [styled-components v2](https://github.com/styled-components/styled-components) - stylis as CSS parser of choice
- Jul 2017: [Emotion](https://github.com/emotion-js/emotion) - pushed performance
- Sep 2017: [Linaria](https://github.com/callstack/linaria)
- Nov 2018: [Emotion v 10](https://github.com/emotion-js/emotion)  - css prop
- Jun 2019: [theme-ui](https://github.com/system-ui/theme-ui) - consistency via theming

The first years were full of new ideas and improvments, open source projects were pushing each other to be better.
No major changes since 2017

Call out for us developers to experiment in that area. Using the following mantra:
- make it work, then make it right, then make it fast
- share early and share often
- document all the things

## [Themability is the path to dark mode](https://reactconfau.com/talks/themeability-is-the-path-to-dark-mode)

by [Diana Mounter](https://twitter.com/broccolini)

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

[jxnblk.com/blog/design-graph](https://jxnblk.com/blog/design-graph/)

The colors name are moved from presentational to functional i.e. `green` => `primary`

The path to dark mode is not as straight forward as just inverting the colors hue and saturation. The outcome of that is not the best
There is a lot of tweeking necessary, especially to keep the color scheme accessible.

To discover more about design systems => Rune Madsen

[programmingdesignsystems.com](https://programmingdesignsystems.com/introduction/)
[theme-ui.com](https://theme-ui.com/)

[Primer on github](https://github.com/primer)
[Primer components](https://github.com/primer/components)
[Primer css][https://github.com/primer/css]
[Primer website](https://primer.style/)
[Experimenting dark mode in ](https://github.com/github/actionview-component)

`Perfect is the enemy of good - Voltaire`

## [(Proto)yyping innovation in BBC News](https://reactconfau.com/talks/prototyping-innovation-in-bbc-news)

by James Dooley

BBC Labs
- Experimenting new tools and ideas
- Releasing prototypes in 6 weeks

Examples: [Skippy](https://bbcnewslabs.co.uk/projects/voice-user-interfaces/) ([read more here](https://www.bbc.co.uk/blogs/internet/entries/9e4ce480-2eca-4fa5-be25-1af0e12befc6))
using [react-dnd](https://github.com/react-dnd/react-dnd) and [react-sortable-tree](https://github.com/frontend-collective/react-sortable-tree)

Transcription: For 1 hour of media it takes 3-4 hours to curate

Led to [OCTO](https://bbcnewslabs.co.uk/projects/octo/)

[react-transcript-editor](https://github.com/bbc/react-transcript-editor)
using [Draft.js](https://github.com/facebook/draft-js) => steep learning curve
and [immutable.js](https://github.com/immutable-js/immutable-js)

Prolematic:
- Scaling a prototype is painful. Draft is unmainainted and does not scale well
- => <Advice> For anything complex: Build an abstraction layer over big external dependencies in case changes are needed </Advice>
- <Advice>Get what you can for free </Advice>

## [Modern forms in react](https://reactconfau.com/talks/modern-forms-in-react)

By [Erik Rasmussen](https://twitter.com/erikras) creator of [Redux Form](https://github.com/redux-form/redux-form), [final-form](https://github.com/final-form/final-form#-final-form) and [React Final Form](https://github.com/final-form/react-final-form)

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

[final-form.org](https://final-form.org/) and [react-final-form](https://final-form.org/react)

Migration guides are available to move from Redux Forms or Formik to react-final-form

There are 2 main components (the API is quite similar to redux forms):
- `<Form>`
- `<Field>`
- `<FormSpy>`: The new kid in the neighbourhood

Those components allow subscriptions to hooks to trigger re-renders so that it does not rerender it all.
`<FormSpy>` is to be able to display the <Form> information without having to rerender the whole form

[Here is an example](https://final-form.org/docs/react-final-form/examples/subscriptions)

Conclusion:
When working on a project, there are multiple considerations to take into account when choosing libraries to use:
- The complexity of your problem
- How extensible the library is
- Does it have an extensive amount of examples (example [nextjs](https://github.com/zeit/next.js/tree/canary/examples))
- The bundle size
- Most importantly does it make sense to you.

One metric that was noted as less important than it looks is github stars and npm downloads. Old projects always tend to have more of those just because they have been around for longer.

## [react-beautiful-dnd: Behind the magic](https://reactconfau.com/talks/react-beautiful-dnd-behind-the-magic)

By [Alexander Reardon](https://twitter.com/alexandereardon)

[react-beautiful-dnd](https://github.com/atlassian/react-beautiful-dnd)

Alex came on stage to explain to us the logic behind the beautifull drag n drop library he created. 
Write about magic, He is a magician, illusion.
It is sensor based.
Supports a11y
For more information: blog beautiful interaction

# [10 x your teamwork through pair programming](https://reactconfau.com/talks/10-x-your-teamwork-through-pair-programming)

By [Selena Small](https://twitter.com/selenasmall88) and [Michael Milewski](https://twitter.com/saramic)

An act by Michael and ..., starting with showing us what not to do when pair programming followed by a better approach to it, introducing ping-pong programming (one engineer writes test while the other one implements the functionnality)

The key points to take out of this act are:
- Prepare ergonomics, desk to be prepared for pairing
- Eliminate distractions as much as possible
- Take regular breaks
- Plan what you are going to pair on
- Work on the plan
- Have a retrospective at the end of the day

## [The first two seconds: Faster page loads with React](https://reactconfau.com/talks/the-first-two-seconds-faster-page-loads-with-react)

By [Josh Duck](https://twitter.com/joshduck)

There are several possible architecture when it comes to rendering:

Client side rendering, SSR, SSR + Data Hydration, Progressive Hydration (Suspens)

Your architecture and technical choices are not going to make the render faster. It should be an iterative work, of measuring and improving. The hard part is what to measure?

Existing tools: [Lighthouse](https://developers.google.com/web/tools/lighthouse) performances [github](https://github.com/GoogleChrome/lighthouse)

It is a good tool but ultimately, the choice is yours on what metrics suits your needs

The metrics they used at [ABC](https://www.abc.net.au/)

|Initial Render|React hydration|Third parties|
|---|---|---|

Inital render:
- Fixed cache headers
- gzipped what was not gzipped
- Font swapping
- Preloading resources (not all of it, example, only 3 of the 3 necessary font files)
- Lazy loading images (Using the intersection observer)
- Above the fold should not wait for javascript

`loading=lazy` comming to html

React hydration:
- Use the [nomodule hack](https://www.reddit.com/r/javascript/comments/8unymn/can_we_use_the_nomodule_attribute_to_safely/) to avoid transpilling for modern browsers
- Dynamic imports and bundle scripting ( use webpack analyse)
- [loadable components](https://github.com/gregberge/loadable-components) (personal note: [React Lazy](https://reactjs.org/docs/code-splitting.html#reactlazy) could be used)
- react profiling for accidental re-render

Third parties:
2/3 of the javascript loaded on a page is third party (google analytics, etc)

- Looks for libraries helping you to load as less as possible
For example [lite-youtube](https://github.com/paulirish/lite-youtube-embed) to load everything only once the user clicks on it


Conclusion:
Lighthouse is not a silver bullet, there is 15% treshold
Measuring impact of changes is hard 
use [pw metrics](https://github.com/paulirish/pwmetrics)
[perfomance api](https://developer.mozilla.org/en-US/docs/Web/API/Performance)
But one thing is to always record wins and losses.

## [Engineering led design](https://reactconfau.com/talks/engineering-led-design)

From Lauren Argenta 

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

## [Take a load off with React](https://reactconfau.com/talks/take-a-load-off-with-react)

By [Jake Moxey](https://twitter.com/jxom_)

1. Common problems about data fetching
There are different ways of handling fetching:
- Fetch on render
- Fetch then render
- Render as you fetch

Details matter

[Apollo client](https://github.com/apollographql/apollo-client) (not only for GraphQL)
[urql](https://github.com/FormidableLabs/urql)
[relay](https://github.com/facebook/relay) ( facebook's version of Apollo)

[react-loads.dev](https://github.com/jxom/react-loads)

hooks for data fetching in react

## [Senior to leader: Taking the next step](https://reactconfau.com/talks/senior-to-leader-taking-the-next-step)

By [Cathy Lill](https://twitter.com/cathyblabla)

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

## [Targeted extensibility: Lessons learned from building Atlaskit](https://reactconfau.com/talks/targeted-extensibility-lessons-learned-from-building-atlaskit)

By [Charles Lee](https://twitter.com/tetrisburger)
[Atlaskit](https://atlaskit.atlassian.com/) and its [bitbucket repository](https://bitbucket.org/atlassian/atlaskit-mk-2/src/master/)

What is a design system?

A system of design guidelines and artifacts that allows an organisation to consolidate:
- design decisions
- Non differiating work

- They help organisations save time

It is not simple to find the perfect implementation

Too open and flexible VS too locked anad constrained
Too locked => hacks, unreliable and forces to rebuild logic

The problem with DS:
1 team writting it and 50 consuming (Atlassian example)

The choice for the new design system was to use react and leverage components.
Led to: What does the user want to change in the components?
- State - No (closed)
- Styles - OK (open)
- DOM - OK (open)

but for anything that is open => want to protect some values

So what are the solutions in place to create a components API?

- Basic props - primitive prop types
- Theme

Basic props: 
- abstracts implementation details

```jsx
<Button appearance="primary">
```
this is a solution, but what about new feature requests:
- Ending up with a prop soup that slows down the ability to ship new things when bugs occur
Another problem with props
Forcing users to adopt bundle size and features they might not need

Theming is a solution to prop soup
A theme is not maintained by the design system team. With some blocks in place anyone can create their own theme.

But basic props and theme still have limitations: 
- usage is constrained with the system
- users need to wait for the system to release the features

What can we do to make it better and not force the users to adopt a bundle?

1 - exporting hooks => the state is passed from the hooks to the components
2 - HOC: performance cost
3- Render props: A pattern to hand of the implementation details. The downside is that it becomes hard for big chunks of interconnected components
4 - Targeted customisation (overrrides): For complex elements such as modal and selects. The tradeoff is that it exposes private APIs, so devs need to be careful about.
 Those 4 solutions are escape hatches but they complete basic props and themes
 
 Props and Theme are still the core features
 Hooks, HOC, render props and targeted customisation are escape hatches completing props and themes
 
 ## [What is an XSS attack - and why should you care?](https://reactconfau.com/talks/what-is-an-xss-attack-and-why-should-you-care)
 
 By [Carmen Chung](https://twitter.com/carmenhchung)
 
 What is a cross site scripting attack? 
 
 When someone injects some javascript into your website (via comments for example). They most likely happen when your javascript is not sanitized
 40% of all attacks on the internet are XSS attacks
 
 React offers us out of the box protection but also allows us to expose our apps to XSS:
 dangerouslySetInnerHTML
 What we can we do about it:
 - remove dangerouslySetInnerHTML when possible
 - sanitise inputs, both on the front end and the back-end
 
 ## [Creating custom form handler with hooks](https://reactconfau.com/talks/creating-a-custom-form-handler-with-hooks)
 
 By [Hannah Thompson](https://twitter.com/hannahcancode)
 
 useForm custom hook
 -> a function that takes a validation function, a callback and initial values and returns
 handlers (change, blur, submit), values and errors)
 
 - Make sure to keep the business logic out of it
 - Typescript and forms are tricky
 
 ## [Reactronica - music as a function of state](https://reactconfau.com/talks/reactronica-music-as-a-function-of-state)
 
 By [Kaho Cheung](https://twitter.com/unkleho)
 
 I don't have notes about this particular talk. But for a good reason, it was really a demonstration of how the library @unkleho created works. And it was simply amazing, I recommend anyone to have a look at the video when it becomes available.
[reactronica.com](https://reactronica.com/) and its [github repository](https://github.com/unkleho/reactronica)
Using [tone.js](https://github.com/Tonejs/Tone.js) and inspired by [react-music](https://github.com/FormidableLabs/react-music)
The slides where created using [spectacle-(https://github.com/FormidableLabs/spectacle) and [react live](https://github.com/FormidableLabs/react-live)
