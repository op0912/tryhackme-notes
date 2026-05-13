# How Websites Work — THM

## Context

This room introduced the fundamental structure of modern websites and basic client-side web behavior.

Main concepts explored:
- Front-End vs Back-End
- HTML structure
- CSS styling
- JavaScript interactivity
- Source code visibility
- Dynamic page modification
- Sensitive Data Exposure
- HTML Injection
- DevTools observations

---

# Front-End vs Back-End

## Front-End (Client-Side)

The front-end is the part rendered and interpreted by the browser.

Main technologies:
- HTML → structure
- CSS → appearance/style
- JavaScript → interactivity/dynamic behavior

The browser:
- receives resources
- interprets them
- renders the webpage visually

Examples:
- buttons
- text
- images
- menus
- animations
- dynamic page updates

---

## Back-End (Server-Side)

The back-end handles:
- authentication
- permissions
- databases
- APIs
- server-side logic

Important understanding:
Sensitive logic and sensitive data should remain server-side.

---

# Website Flow Understanding

Modern websites are not a single object.

Browsers may load:
- HTML
- CSS
- JavaScript
- images
- API responses

Observation:
multiple resources may create multiple HTTP/TCP requests.

---

# HTML Understanding

HTML defines the structure of a webpage.

Example:

```html
<h1>Main Title</h1>
<p>Hello World</p>
<button>Click Me</button>
```

Important concepts:
- `<head>` contains page information/resources
- `<body>` contains visible page content
- elements may contain attributes
- `id=""` uniquely identifies an element

---

# JavaScript Understanding

Initial difficulty:
JavaScript syntax was initially difficult to visualize conceptually.

Main realization:
JavaScript dynamically modifies webpage content after page load.

Example explored:

```javascript
document.getElementById("demo").innerHTML = "Hack the Planet";
```

Understanding breakdown:
- `document` = current webpage
- `getElementById("demo")` = locate HTML element
- `innerHTML` = element contents
- `=` = replace contents

Meaning:
Find the HTML element with id="demo" and replace its contents dynamically.

---

# Dynamic Web Behavior

Without JavaScript:
- pages are mostly static

With JavaScript:
- pages become interactive
- content changes dynamically
- buttons react to events
- APIs can be queried
- pages update without full reloads

Key realization:
Modern websites continuously modify HTML dynamically.

---

# Source Code Understanding

Website source code can be inspected using:
- View Page Source
- Browser DevTools (F12)

Observation:
Everything sent to the browser can potentially be viewed by the user.

Examples:
- HTML
- CSS
- JavaScript
- comments
- hidden links

---

# Sensitive Data Exposure

Sensitive information may accidentally remain exposed inside:
- HTML comments
- JavaScript files
- source code

Example discussed:

```html
<!-- TODO: remove test credentials admin:password123 -->
```

Important realization:
Hidden visually does NOT mean secure.

If data is sent to the browser:
- users may inspect it
- attackers may discover it

---

# HTML Injection

If user input is not sanitised:
- attackers may inject HTML
- attackers may inject JavaScript
- pages may be manipulated dynamically

Example concept:
User-controlled input may become interpreted HTML instead of plain text.

General rule:
Never trust user input.

---

# DevTools / DOM Observations

Real observations performed manually using:
- DevTools
- Sources tab
- Element inspection

Websites tested:
- facebook.com
- entretiengazon.com

---

## Facebook Observation

Observed:
- frontend structure extremely complex
- difficult to modify visually
- heavy JavaScript/framework usage
- large amount of dynamically generated content

Conclusion:
Large modern web applications contain highly complex frontend systems.

---

## entretiengazon.com Observation

Observed:
- modified CSS values directly in DevTools
- changed font-size values
- page updated visually in real-time

Example:
- changed values from ~1.8 to 3.8 and 9.8
- text became significantly larger

Also explored:
- disabling CSS rules with DevTools checkboxes

Observed:
- some disabled properties produced visible changes
- others produced little/no visible difference

Possible reasons:
- CSS overrides
- dependent layout behavior
- subtle visual changes

---

# Heading Tag Observation

Observed HTML heading elements:
- h1
- h2
- h3
- h4
- h5
- h6

Understanding:
- h1 = largest heading
- h6 = smallest heading

CSS rules were attached to these elements.

---

# JavaScript Source Observation

While exploring DevTools > Sources, observed:
- large JavaScript files
- minified/compressed code
- complex regular expressions (Regex)

Example observed:

```javascript
ID: new RegExp("^#(" + R + ")")
CLASS: new RegExp("^\\.(" + R + ")")
TAG: new RegExp("^(" + R + "|[*])")
```

Understanding:
This code is used to recognize/select HTML elements such as:
- IDs → `#demo`
- Classes → `.button`
- Tags → `h1`, `div`
- Attributes → `[required]`

Important realization:
Modern websites use large JavaScript libraries and frameworks.

These files:
- may appear unreadable
- are often minified/optimized automatically
- are designed for browser execution efficiency

Important distinction:
Humans usually write readable JavaScript first.
Build/minification tools then compress and optimize the code before it is sent to browsers.

---

# Local Browser Modification Understanding

Important realization:
Changes made in DevTools are LOCAL ONLY.

Modifying:
- HTML
- CSS
- DOM

inside the browser:
- does NOT modify the real server
- does NOT affect other users

However:
if malicious input is stored and redistributed by the server,
other users may be affected.

---

# Core Mental Model Built

Websites are:
- code
- resources
- requests
- dynamic interactions

NOT static images.

Modern web applications continuously:
- load resources
- execute JavaScript
- modify the DOM
- communicate with APIs
- update content dynamically

---

# Key Takeaways

- Front-End = browser-rendered content
- Back-End = server-side logic
- HTML = structure
- CSS = appearance
- JavaScript = dynamic behavior
- Everything sent to the browser may be inspected
- User input must never be trusted
- JavaScript can dynamically manipulate HTML
- DevTools modify local client-side rendering only
- Modern websites rely heavily on complex JavaScript systems
