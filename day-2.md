Talk 1:

Play with 4 people, exposing how redux connect works but also how the equivalent with hooks works.
There are trade-offs, it is not as simple as just using the context and reducer hooks, as it needs some configuration to avoid unnecesary re-renders

Talk 2: Mark Dalgleish

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

## Talk 3: 5 things you should know about wordpress... wait, what?

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

## TALK 4: Write fewer tests @davidkpiano
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

## Talk 5

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
