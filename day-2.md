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



