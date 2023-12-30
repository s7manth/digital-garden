---
title: Emmet snippets for html
summary: Discover the beauty of Emmet expansions and start coding like a god!
publish_date: 2022-06-21
---

What if you knew a way to change your coding experience in HTML from a dull, monotonous, and boring one to something that sends chills down your spine? Let me introduce you to Emmet! 

### What is Emmet?

Emmet is a text editor plugin that greatly improves the HTML and CSS code writing workflow. It is built with the use of modular snippets that can be recursively used which allow us to produce code with godspeed. It is an open source tool developed by [Sergey Chikuyonok](https://github.com/sergeche) under the project titled *[Zen Coding](https://www.smashingmagazine.com/2009/11/zen-coding-a-new-way-to-write-html-code/)*. 

Its [syntax](http://docs.emmet.io/abbreviations/) is inspired by CSS selectors. Each abbreviation is transformed in runtime. With Emmet you can quickly [write a bunch of code](http://docs.emmet.io/actions/expand-abbreviation/), [wrap code with new tags](http://docs.emmet.io/actions/wrap-with-abbreviation/), quickly [traverse](http://docs.emmet.io/actions/go-to-edit-point/) and [select](http://docs.emmet.io/actions/select-item/) important code parts [and more](http://docs.emmet.io/actions/)! Emmet is written in pure JavaScript and works across different platforms: web browser, Node.js, Microsoft WSH and Mozilla Rhino. 

### Support and How to Install

VS Code has native support for Emmet snippets and abbreviations. Emmet has [wide support](https://emmet.io/download/) for other code editors as well including famous web hosted services like CodePen and SourceLiar among others. 

### Side Tip for VS Code Users

Emmet expansions can also be used for JSX (Extended JS) code. Writing HTML in React, hence, becomes much faster. In order to enable it on VS Code, one can go to the Text Editor Settings, and look for Emmet under Extensions section. Clicking on ‘Edit in settings.json’ will reveal the config file for Emmet. 

Simply add the following to the file to enable Emmet for JSX : 

```json
{
   "emmet.includeLanguages": {
      "javascript": "javascriptreact"
   }
}
```

### Basics

| Character | Description |
| --- | --- |
| > | specifies the parent child relationship among elements |
| + | specifies the sibling relationship among elements |
| . | class attribute's value |
| { } | specifies what will go inside the element ie text |
| ^ | climbing up the element scope |
| [ ] | custom attributes and their values |
| $ | placeholder for numbered things |
| * | multiply character for numerous instances of the same snippet |
| ( ) | grouping of the elements together |
| # | id attribute's value |

```html
! + <tab> or <enter> produces the template html code to get started 

<!-- snippet: -->
div>h1.heading{This is the heading of the page}+\
p#pid{Paragraph}+ul>li.element${no. $}*3
+ 
<tab> (some text editors allow this) or <enter>

<!-- the above snippet translates to: -->
<div>
    <h1 class="heading">This is the heading of the page</h1>
    <p id="pid">Paragraph</p>
    <ul>
        <li class="element1">no. 1</li>
        <li class="element2">no. 2</li>
        <li class="element3">no. 3</li>
    </ul>
</div>
```
