# University of Nottingham Software Development

[![Build Status](https://travis-ci.org/UniversityOfNottingham/universityofnottingham.github.io.svg?branch=source)](https://travis-ci.org/UniversityOfNottingham/universityofnottingham.github.io)

## What is this?

This site documents **Policies**, **Standards**, **Guidelines** and **Processes** for Software Development in use at the University of Nottingham.

Refer to `docs/index.md` or the site itself for more information on what's here.

## Why is it here?

It's in a git repo so it can be kept up-to-date and changes can be tracked, and is presented in a way more familiar to developers (unlike other internal Wiki solutions).

It's publicly available because it can be, so it should be.

## How does it work?

Please use the `source` branch as the source of authority.

`master` is the branch used to serve the built documentation.

Any other branch is a work in progress or preserved for historical reasons.

`source` is built by [Travis] using [MkDocs] and deployed to `master` hosted by [GitHub Pages].

# Contributing

We welcome contributions from members of the Product Centre Application Development team.

These can be corrections, additions, or just suggestions.

1. Read the rest of this contributing section so you know your changes are appropriate.
1. Make a branch.
1. Make your changes / additions.
1. Submit a pull request to the `source` branch, adding Senior Application Developers as reviewers.
1. Await comments, or approval.

## What format should docs be in?

[Markdown]. All Markdown all the time.

- It's readable as source and readable when rendered.
- It's quick and easy to write without learning very much
- Many editors provide rendered previews
    - [Visual Studio Code]
    - [Atom]
    - ...
- It's portable if we decide to move it elsewhere.

### PyMdown Extensions

We have a bunch of `PyMdown` Extensions enabled. More can be enabled if required.

Refer to `mkdocs.yml` and the [MkDocs] and [PyMdown Extensions] documentation.

## Filenames

Please use `kebab-case` for filenames to be consistent.

## Images

Images can be added to the repo, provided they're not of a ridiculous size.

Add them to the `docs/images` so they can be easily linked to and will be included in the build

Link to images from a document relative to the document's location.

## Navigation

The navigation structure, including Page Names is managed via the `pages` dictionary in `mkdocs.yml`.

Refer to [MkDocs] documentation for further details.

[Markdown]: https://daringfireball.net/projects/markdown/syntax
[MkDocs]: https://www.mkdocs.org/
[Visual Studio Code]: https://code.visualstudio.com/
[Atom]: https://atom.io/
[PyMdown Extensions]: https://facelessuser.github.io/pymdown-extensions/
[travis]: https://travis-ci.org
[GitHub Pages]: https://pages.github.com/