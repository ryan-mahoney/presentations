# HTML Email
May 22, 2018

---

## Overview

On T-Alerts Concierge we have taken steps to ease the pain of creating and testing HTML emails. This presentation covers the major issues and the mitigations we chose.

---

## Main Issues

### Difficult to Write
There are [more than 40](https://cdn.tutsplus.com/webdesign/uploads/2013/06/demystifying-email-rendering.png) mainstream rendering engines with drastic differences in their supported subsets of HTML/CSS.

### Difficult to Test
- How many email clients can you run?
- Does your local environment send emails?

---

## Difficult to Write

- there are no standards for HTML email
- doesn't consistently support "responsive", many email designers are going with mobile-first (monbile-only)
- maximum width of content should be ~600px
- layouts should typically be done using HTML tables
- styles should be inlined
- can not use SVG images
- should use some well established hacks for IE engines
- limited support for custom fonts

Some really good looking HTML emails use images heavily for text, etc as a cheat because SEO is not a concern.

---

## Difficult to Test

- it can be hard to have local environments be setup to send some local emails but not all
- if the emails looks good on one client, it may give a false sense of confidence
- unlikely and laborious for one person to have direct access to so many different email clients and services

---

## Mitigation for Writing
- Use transpilation approach with [MJML](https://mjml.io/) 
- Start with a default MJML template
- only drop to `raw` when fully necessary
- save images directly to S3 (or similar)
- save `.mjml` file in git repo
- use generate `HTML` in application templates

---

## Mitigations for Testing
- Use a service that allows preview of HTML in many clients using integration or HTML paste.

- Litmus
- Email on Acid

---

## End

Send HTML Email with confidence!