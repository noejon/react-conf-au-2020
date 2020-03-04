## [Redux Connect vs Redux Hooks: A play](https://reactconfau.com/talks/redux-connect-vs-redux-hooks-a-play)

By [Terence Jeong](https://twitter.com/terence_jeong) and friends

Play with 4 people, exposing how redux connect works but also how the equivalent with hooks works.
There are trade-offs, it is not as simple as just using the context and reducer hooks, as it needs some configuration to avoid unnecesary re-renders

## [Rethinking Design Practices](https://reactconfau.com/talks/rethinking-design-practices)

By [Mark Dalgleish](https://twitter.com/markdalgleish)

Intersection between design and implementation
Our industry is at crossroad
Design systems are not fully delivering on their potential
Design workflows are struggling to keep up
There are two approaches to the design process
Code in design tools VS Design in code. The talk is about design in code

Designers and developers should literally talk the same language.

### Tooling

Seek created Playroom (open source)
- it consists of JSX as a design tool, where the whole design system is loaded
- it is low entry level as it uses tags and props only
- it does not need any installation and has shareable urls
- it allows test driving the design systems

### Abstraction

A design system developer should accurately design:
- build up layers
- define tokens (typo, color, breakpoints)
- use primitives

Seek build the DLS leveraging styled-systems
```jsx
<Box/>
```
reinforces reusable values

Has responsive props => define values of breakpoint at the jsx level

WRITING CSS SHOULD BE THE EXCEPTION

##### Layout

The layout is always the struggling part

READ: space in design system (Curtis Nathan)
https://medium.com/eightshapes-llc/space-in-design-systems-188bcbae0d62

Components themselves should not contain surrounding white spaces. 
Margins should be avoided
The white spaces are owned by the layout components
This is problematic because HTML by default has white spaces (for example `<h1>`)

How to fix this?
- Sit the text on the baseline (see repo braid)
- Crop the top of the text node (css hack)

The line height remains untouched
Whitespaces are equally balanced and under control

All text should behave as all other components

Layouts

```jsx
<Stack>, <Inline> (for badges, tags, etc), <Column>

Responsive props

```jsx
space={["small", "large"]}
```

The components should make sense to non dev => prototyping in code
For that playroom now has: Predefined snippets

How can we make code part of the design process (with playroom)?

- Get involved with design
- Pay attention to how designers iterate, what did you try along the way
- Find early adopters and offer constant support
- Encourage pairing between designers and developers (try to break walls)

Welcome designer into the fold (running workshop with designer, force them if needed but make it fun)

In conclusion rethink design practices
It is not going to happen without us

## [5 things you should know about WordPress... wait, what?](https://reactconfau.com/talks/5-things-you-should-know-about-wordpress-wait-what)

By [Isabel Brison](https://twitter.com/ijayessbe)

5 things we already know:
- it is a CMS
- it is open source
- it is 16 years old
- it powers a 1/3 of websites
- it has a huge ecosystem of extensions

5 things we might not or don't know about WP:
1 - growing parts of WP are now built in react (edit post)
Existing functionalities (the monolith) are still implemented in php
Guthenberg - Post editor
@wordpress/element

2 - WP has a package that wraps react in a package. @wordpress/element
It ships only the parts of react that are up to date (does not ship proptypes (old ones) for example)
The reason why this wrapper is in place is to be able to switch if facebook decides to change mind on the license

3 - How does it fit with he php monolith

It uses REST APIs. The same way Gatsby can load the info from wordpress, the new react app uses those REST APIs.
The react app is in a monorepo, but is split into several npm packages (all open source)

4 - WP packages can be used anywhere outside of WP

As it has been open sourced, anyone can use it. And WP's biggest competitor, Drupal, now integrate Guthenberg, the post editor.

5 - Third Party extension developers don't have to use react unless they want to. But extensions can now be written in react as well

WP has a lot of scripts to create WP plugins in react. 
@wordpress/create-block (sort of CRAP)
https://github/com/wordpress/guthenberg

WP encourages people to build using react.

## [Write fewer tests! Model-based testing in React](https://reactconfau.com/talks/write-fewer-tests-model-based-testing-in-react)

By [David Khoursid](https://twitter.com/davidkpiano) 
Model base tesing in react

Writing all the tests is the most hated thing amongst front-end developers

E2E tests make sure the app works as expected
Integration test make sure the code works as expected
Unit tests make sure the dev works as expected

For front-ent projects,  see Kent C Dodds' pyramid

Unit testing is not the most important part of front end app testing

What if the tests can be generated without being written?

There are some patterns for that, Model Based testing for E2E tests (Property based testing for unit test)

Model Based Testing revolves around the state and transitions in the application

States are finite, transitions are finite as well. Think about applications as riddles (die hard gallon example)

### Introducing abstract models:

Requirements:
- Given [Precondition]
- When [Action]
- Then [Post Condition]

Which leads to a model of

Pre-con -----action-----> post-con

Here are the steps to automate the creation of unit tests

1. Create a model -> as a directed graph
2. Generate the abstraction path
3. Make the tests real
4. Execute the test
5. Profit from it (seriously) - Adding a functionality just needs the model to be changed

Test using:
React Testing Library - Jest - Xstate

Xstate: used to generate the finite state machine
We use that state machine to generate a path

shortest path vs simple path (no cycle)

Put the assertion in each state machine meta

Tests are then generated for us automatically

We can further improve the tests suite by using pupeteer to do e2e tests and run through all the tests

Time travel debugging in the future

@xstate equivalent => simulato graph-walker

BUT

it is harder: there is a learning curve and one has to learn how to model the application properly.
The model might be wrong (but that is your fault). this does not change from normal unit tests though as one can also write tests that are not testing anything or testing the wrong thing.

In a front-end application, the use case coverage is much more important than code lines coverage.

But the hard learning curves leads to 
Better: Requirements integrity, efficiency, Flexibility, Reduce cost/time, test generation, maintenance, edge case discovery, implementation agnostic.

Make your code model driven, generate tests, generate docs, generate prototypes
Make your code do more.

## [The tragedy of scale](https://reactconfau.com/talks/the-tragedy-of-scale)

By [Hannes Obweger](https://twitter.com/obweger) and [Nadia Makarevich](https://twitter.com/adevnadia)

Shared limited resources, tragedy of the common
Applies to software engineering too
Codebase is shared amongst everyone but limited by our own brains
Browser: limited bandwidth, CPU etc
If we all add different features it will become a post apocalyptic wasteland (compared to adding cows to a field)

We are better off having no common land (not shared). In terms of code, this is modularisation

functions, components, files, packages: Libraries vs product

Growing product with all of it in `src/` will grow as spaghetti code
We need to build composition boundaries within our projects
Think of a product as a composition of packages => Makes it easier to think about our code
Software devs take care of their own small packages

Splitting up exisiting fields in code is the component mindset is what react does

Care should be taken wwhen building a monolithic redux store

Rethink of state to build modular/composable/future-proof features seemelessly

Local state => Component has its own state and should not be added to redux
Shared state => components share info with each others:
- parents passing props to children => but that does not scale
- react context passes those layers we don't need
Remote state => Information that does not leave in the UI. How to solve:
- similarly to the Remote State: parent components (not scaling) or context

Context solves issues but also has gotchas:
- We can end up in a provider hell: easy to make mistake which will trigger too many re-renders

The solution in this case is to keep both redux and context

github.com/atlassian/react-sweet-state

As in real life there are ways to deal with shared resources when there is a bad actor:
- setup rule and conventions

Importing one package from another package is OK
It is not OK to reuse directly some of it
Fetching components can't use render
Use static code analysis - ESLINT

[github.com/atlassian/striker](https://github.com/atlassian/stricter)

Atlassian has set up a Police Team, in charge of making sure that the rules are followed in repos.

Recap:
Separating fields => moduralising software
Splitting up existing fields => components mindset
Protection against "bad actors" => Rules & conventions

Devs are all in this together

## [Building with Monorepos](https://reactconfau.com/talks/building-with-monorepos?from=schedule)

By [Mitchell Hamilton](https://twitter.com/mitchellhamiltn)

First, what are the issues with multi-repos?

- Slow iteration cycle
- dependency management (error prone)
- split identity, docs and issues

Mono-repo benefits

- PRs accross multiple packages
- single identity
- centralised docs and issues

The problem with Monorepos was the lack of tooling for problems like:

- Dependency management: 
Lerna, built Bolt with Atlassian: external packages versions have to be equal, external packages have to be on root, internal packages must be in range

Came along yarn workspace, that did the same. Except if different versions of react it becomes problematic.
This can be checked by using Manypkg:
- it is a linter for package.json
Available commands are `check`, `fix`
Those are constraints that are solving people's problems

2. Packaging problems:
- consistent package.json fields
- bundler
- babel
- multiple entrypoints
- able to dev without having to rebuild

preconstruct (npm)

bundling is hard, but is eased with Rollup
good at treeshaking
Babel (not in .babelrc but babel.config.js)
Multiple entrypoints
Rebuild issues
command `dev` creates dist files, there are no build scripts

3 Releasing
- Contributor declare their changes
- Not rely on git to document changes
- Bump dependency packages
- Easily automate releases

Build Changesets (npm)

There are more benefits to a MR:

- simple imports (package name rather than lengthy '../../..'
- strict API contracts (node exports field in package.json to come)
- structure

monorepo.guide (knowledge they gathered on their monorepo journey)

## [How to teach an old dev new tech: Learning React as a senior developer](https://reactconfau.com/talks/how-to-teach-an-old-dev-new-tech-learning-react-as-a-senior-developer)

By [Trent Willis](https://twitter.com/trentmwillis)

teach old devs new techs
Leraning react as a senior developer
Heavily using jquery
9 month lead dev did not know react => Reflection on the journey

Why was the journey successful?
- create a team culture where learning is encouraged

Old developer does not mean old in age, but old in solidity, in comfort zone, stuck into old tech stacks they know.
The comfort zone is what stops us from learning
In the CZ one can foresee issues and quick profits
CZ => no a bad thing inherently, we should not be scared of staying there BUT
it becomes bad when:
- When you stop trusting other's experience
- afraid to fail in front of the team
- want to remain the expert
- we don't celebrate people learning
All those points leads us to limit our productivity

How to create a culture of learning?

Why do we learn:
|extrinsic|Intrisic|
|--|--|
|money, fame, success (incentives), new job|Own motivation, want to do something, because it is interesting|

One type of motivation does not necessarely produce better results
Intrisic motivation is more likely to give better results
overjustification effect => you will be less motivated to do something because external asked you to
Understanding motivation creates an environment where success is more likely

Motivations can change:
No intrisic motivation can change, extrinsic -> intrisic
But the opposite can also happen and that can cause devs to burnout.
Create a culture that fosters positive and supportive motivation for learning.
Start by being honest about the knowledge that you have (admit when you don't know something)
"You should know that" vs "I'm not sure, let's figure that together"

The ability to learn is better than already knowing.
There is always a lot to learn and we should have a base to learn and relearn things faster.
This kind of cultures leads to newer technologies.
Build empathy about learning, You can't unlearn. Listen to those learning something for the first time. Understand their difficulties and help them understand.
LISTEN AND ACT TO CREATE POSITIVE EXPERIENCES
Try learning a few couple of skills every now and then (guitar or anything, to remind you what it is like to learn)
Learning a new skill is like climbing a mountain. 
Once you have that empathy around learning, give others the chances to learn and to teach you.
Encourage exploration of interests, build prototypes: the working ones will open to a bright future.
If someone is able to teach you something, let them play their strengths and their knowledge. Step back and give them more responsibilities. More importantly don't get good contribution unrecognised.
Celebrate work that you have done. And show people that you appreciate them.

How to learn effectively

Research the scope of what you need to learn. Step back and decide what all you need to learn. Build up knowledge in little __well defined increments__. This is also good for other people to help you.
pick your project/tickets/issues purposefully to learn new skills. If you feel overwhelmed, take breaks. Recharge and come back with a fresh mind. (more than one break a day, probably one per hour). It also restores motivation.
Don't understimate the power of rest (not REST, silly developer) Get good sleep (8h is the perfect amount (find ted talk)
Sleeping is important to learn. Be gentle to yourself (the journey is long, don't burn out)
Be a developer who celebrates learning

## [A GraphQL Survival Kit](https://reactconfau.com/talks/a-graphql-react-survival-kit-how-to-avoid-the-pitfalls-and-level-up-your-teams-creativity)

By [Petra Gulicher](https://twitter.com/petronbot)

A graphQL survival kit. Tales from an expeditiom @petronbot

What's GraphQL:
A query language + runtime for executing them

It is cool because:
- product centric
- hierarchical
- schema driven (contract to all our apps)

3 dangers:
1. Slow query responses
2. Not knowing what to call things
3. Not knowing what to do when an error happens

1. The tree is resolved as breadth first
response can be delayed by design or by weather conditions (bad internet)
It is dangerous to ignore delays and risk compounding them
You could try:
- cache graphQL API's responses. But careful how you decide what gets cached, expect requests to change
instead try to:
give a brain to your GraphQL app and make data available earlier (database or application cash)

Single endpoint but not single request

It's OK to make a bunch of small, granular requests.
... peel back the curtain, but needs to understand the backend to optimise

2. Knowing what to call things:
Create a modelling domain:

|Naming|Connections|
|-|-|
|Lists|Making changes|

Make sure that the user's behaviour is described by the operation

```js
type Mutation {
  updateX(...) // Too generic, not descriptive enough
  addXtoY(...) // better, more specific
```

Does it mean that we need to create an operation for each interaction in your model?
Yes, if a user can do it, your model should be able to do it

3. What to do when things go wrong

Seeing a 200 response with an error
Your app decides what to do when things go wrong when we receive

```js
success(200){
  data: {...},
  error: {...}
}
```
Two types of errors:
- Server errors: plumbing has gone wrong
- GraphQL errors: data has gone wrong

1. be aware of how queries are are resolved, be adaptable with requests
2. Be involved in the schema design process (all in the team should, design, QA, devs)
3. Make sure to do the work to handle errors

Conclusion:
Great coverage of tools and adapters
API odcs comes for free
does not care about your transport method
you can write less code and get more app (easy win)

GraphQL playground
https://petragulicher.com/talks

## [Powerful REST in a GraphQL world](https://reactconfau.com/talks/powerful-rest-in-a-graphql-world)
by [Tejas Kumar](https://twitter.com/tejaskumar_)
REST and GraphQL and stuff

Benefits of typescript
react style guides
github.com/operational-ui

Watch React Finland Conf with Tejas YT link

How TS helped with network errors
REST is not good because:
- There are no formal specsion
- it is guessing games: BE makes assumptions of FE and FE makes assumptions of BE.
- meaningless discussions (should we use a put or a patch)
- No contractual aggreements

A solution to that could be using GraphQL, which is good because:
- it has formal specs
- there are no guessing games
- meaningful discussions (should we cache, lazy load etc)
- strong contractual agreements

Some companies won't allow introducing new techs. 
In the face of constraints you can get bitter or you can get better
Lead the creation of restful-react (gh) => e2e type safety

The takeways of project:
- innovate against constraints
- choose better over bitter
- support open source
 
 ## Closing talk: The Value of Open Source
 
 By [Jed Watson](https://github.com/JedWatson)
 
 Innovation: Open source mentality
 The value of opensource is both everything and nothing.
 
 Read about 1000 Days of open source on medium
 
 Open source has a lot of value:
 - it increases the quality of life, makes us more productive and increases the quality of product
 - Open source builds on great abstractions
And we love abstractions
Open source is strong but it has weaknesses
It has a lot of value but has no value

Lifecycle of opens source:
enthusiasm -> opens -> growth -> maintenance

success !== success
investment !== sustainability

We need sustained investments.

If people NEED to pay for open source, it breaks

there are answers to this problem:

Social responsibility: companies are not charities, so that is not the answer
Virtuous cycle does

github.com/lemonadestand

- corporate stewardship (react/angular)
- Apollo - Sells services and support
- Nextjs - Zeit platform and now
- Gatsby - VC funding

What if we don't need abstraction

Babel is supported by donations. It is critical infrastructure and it is seriously underfunded

We can do better than that:
- Tragedy of the commons
Solution => the mid-way solution where everyone just does a little bit

Open source leans too much on individual value to be sustainable at scale.

Explain to your company the value of open source
Companies have budget for training, set up some budgetto contribute to open source.

API, docs, skilss are constrained resources.
There is no forced adoption in open source.

Contributing to open source you:
- are out of your comfort zone
- get a broad experience as a product owner, engineer, marketer, designer (missing one)

Companies spend money to avoid risk:
- legal
- retention
- insurance

What would be the cost if a company had to maintain one of the dependencies that saved us time? Unamintained packages might become vulnerable which could be a big risk for companies.

No individual company can (or should) pay for it all.

One solution could be tha companies allocate a small amount per year to spend on open source.

Salary $100k => give $100 to open source.

Your team is actually a mix of inhouse devs and open source devs..

As devs, we have the power to make that happen. 
We make decisions about what tools we use (Jira, Slack, Workplace)
We get free lunch or friday night drinks
For a company, open source is a good ROI, invest in open source

How did we get ping pong tables, free lunches etc?
By asking for it.

For each company this is a small contribution, but it is huge for open source

For that [budgetforopensource.org](https://budgetforopensource.org/)

Funding it fits the way company works


