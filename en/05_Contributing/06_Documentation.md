---
title: Documentation
summary: Writing guide for contributing to SilverStripe developer and CMS user help documentation. 
icon: file-alt
---

# Contributing documentation

Documentation for a software project is a continuing, collaborative effort. We encourage everybody to contribute in any way they can, from simply fixing spelling mistakes, to writing recipes, reviewing existing documentation and translation to other languages.

Modifying documentation requires basic knowledge of [PHPDoc](https://en.wikipedia.org/wiki/PHPDoc) and 
[Markdown](https://daringfireball.net/projects/markdown/) as well as a GitHub user account.

[info]
Note that there are two sources of documentation, depending on the intended audience. You can see where each of those lives in the [repositories](#repositories) section below.
[/info]

## Editing online

The easiest way of editing any documentation is by clicking the "Edit on GitHub" button at the bottom of the
page you want to edit. Alternatively, locate the appropriate .md file in the
[silverstripe/developer-docs](https://github.com/silverstripe/developer-docs/) repository and press the "edit" button. **You will need a free GitHub account to do this**.


 * After editing the documentation, describe your changes in the "commit summary" and "extended description" fields below then press "Commit Changes".
 * After committing you changes, you will see a form to submit a Pull Request: "[pull requests](https://support.github.com/features/pull-requests)". You should be able to adjust the version to which your documentation changes apply before submitting the form. Any changes submitted in a pull request will be sent to the core committers for approval.

[warning]
You should make your changes in the lowest major branch they apply to. For instance, if you fix a spelling issue that you found in the CMS 5 documentation, submit your fix to the `5` branch in Github and it'll be copied to the most recent major version of the documentation automatically. *Don't submit multiple pull requests for the same change*.
[/warning]

## Editing on your computer

If you prefer to edit content on your local machine, you can "[fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo)" the 
[silverstripe/developer-docs](https://github.com/silverstripe/developer-docs) repository, make changes locally, and then [send us a pull request](https://github.com/silverstripe/developer-docs/compare) to incorporate your changes.

[warning]
If you submit a new feature or an API change, we strongly recommend and request that you include a PR to update the necessary documentation. This helps prevent our documentation from getting out of date.
[/warning]

## Repositories

* End-user help: [silverstripe/silverstripe-userhelp-content](https://github.com/silverstripe/silverstripe-userhelp-content/)
* Developer guides: [silverstripe/developer-docs](https://github.com/silverstripe/developer-docs/)
* Website code for user and developer docs: [silverstripe/doc.silverstripe.org](https://github.com/silverstripe/doc.silverstripe.org)
* Developer API documentation: [silverstripe/api.silverstripe.org](https://github.com/silverstripe/api.silverstripe.org)

## Source control

Contributing documentation is the same process as providing any other patch (see [Contributing code](code)).

If you are fixing incorrect or incomplete information for the current major version, you should create a PR that targets the branch for the latest stable release (e.g. `5.1`).

If you are adding documentation for functionality that has not yet been released, you should target the most recent _major_ branch (e.g. `5`)

## What to write

See [what to write (jacobian.org)](https://jacobian.org/writing/great-documentation/what-to-write/) for an excellent introduction to the different types of documentation. Also see [producing OSS: "documentation"](https://producingoss.com/en/getting-started.html#documentation) for good rules of thumb 
for documenting open source software.

## Structure

* Keep documentation lines shorter than 120 characters.
* Don't duplicate: Search for existing places to put your documentation. Do you really require a new page, or just a new paragraph of text somewhere?
* Use PHPDoc in source code: Leave low level technical documentation to code comments within PHP, in [PHPDoc](https://en.wikipedia.org/wiki/PHPDoc) format. 
* API and developer guides are two forms of source code documentation that complement each other.
* API documentation should provide context, ie, the "bigger picture", by referring to developer guides inside your PHPDoc.
* Make your documentation easy to find: Documentation is useful only when it is interlinked so please make sure your contribution doesn't become an inaccessible island. At the very least, put a link to your index page in the same folder. A link to your page can also appear
as "related content" on other resource (e.g. `/tutorials/site_search` might link to `/developer_guides/forms/introduction`).

## Writing style

* Write in second person plural form: Use "we" instead of "I". It gives the text an instructive and collaborative style.
* It's okay to address the reader: For example "First you'll install a webserver" is good style.
* Write in an active and direct voice.
* Mark up correctly: The use of preformatted text, emphasis and bold make technical writing easier to scan.
* Avoid FAQs: FAQs are not a replacement for coherent, well explained documentation. If you've done a good job
documenting, there shouldn't be any "frequently asked questions" left.
* "SilverStripe" should always appear without a space with both "S"s capitalised.
* Use simple language and words. Avoid uncommon jargon and overly long words.
* Use UK English and not US English. SilverStripe is proudly a New Zealand open source project we use the UK spelling and forms of English. The most common of these differences are -ize vs -ise, or -or vs our (eg color vs colour).
* We use sentence case for titles so only capitalise the first letter of the first word of a title. The only exceptions to this are when using brand names (e.g. SilverStripe), acronyms (e.g. PHP) and class names (e.g. ModelAdmin).
* Use gender neutral language throughout the document, unless referencing a specific person. Use them, they, their, instead of he and she, his or her.
* URLs: if the end of your sentence is a URL then you don't need to use a full stop.
* Bullet points: Sentence case your bullet points. If a bullet point is a full sentence then end with a full stop. If it is a sentence fragment or a comma separated list, full stops are not required.

## Highlighted blocks

There are several built-in block styles for highlighting a paragraph of text. Please use these graphical elements 
sparingly.

[hint]
"Tip box": A tip box is great for adding, deepening or accenting information in the main text. They can be used for background knowledge, or to provide links to further information (ie, a "see also" link).
[/hint]

Code for a Tip box:

```
[hint]
...
[/hint]
```

[notice]
"Notification box": A notification box is good for technical notifications relating to the main text. For example, notifying users about a deprecated feature.
[/notice]

Code for a Notification box:

```
[notice]
...
[/notice]
```

[warning]
"Warning box": A warning box is useful for highlighting a severe bug or a technical issue requiring a user's attention. For example, suppose a rare edge case sometimes leads to a variable being overwritten incorrectly. A warning box can be used to alert the user to this case so they can write their own code to handle it.  
[/warning]

Code for a Warning box:

```
[warning]
...
[/warning]
```

See [markdown extra documentation](https://michelf.com/projects/php-markdown/extra/#html) for more restrictions
on placing HTML blocks inside Markdown.

## Translating documentation

Documentation is kept alongside the source code, typically in a module subdirectory like `framework/docs/en/`. Each language has its own subfolder, which can duplicate parts of or the entire body of documentation. German documentation would, for example, live in `framework/docs/de/`. The 
[docsviewer](https://github.com/silverstripe/silverstripe-docsviewer) module that drives 
[docs.silverstripe.org](https://docs.silverstripe.org) automatically resolves these subfolders into a language dropdown.

## Further reading

* [Writing great documentation (jacobian.org)](https://jacobian.org/writing/great-documentation/)
* [How tech writing sucks: Five sins](https://www.slash7.com/articles/2006/11/15/tech-writing-the-five-sins)
