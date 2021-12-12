# Pak CLI

A common toolchain for building npm packages written as ES modules.

Inspired by [react-scripts][1]. Like that, but for a different set of technology choices.

## Features

 * Easy to use -- zero configuration necessary
 * Integrates cleanly with CI pipelines
 * Adopt in full or in part

## Installing

```bash
npm install --save-dev pak-cli
```

Yarn users, you know what to do instead.

## Usage

Run `npx pak-cli init` to get started.

This command will apply the following changes to your package.json:

 * Add `scripts` aliases for the `build`, `docs`, `lint`, `test`, and `test:coverage` commands.
 * Add Babel configuration (`babel`).
 * Add ESLint configuration (`eslintConfig`).
 * Configure CommonJS and ESM entry-points (`main`, `module`, `sideEffects`, and `exports`).

For more detailed usage information, run `npx pak-cli`.

## Design Philosophy

Pak is the result of lessons learned and practices adopted in production across hundreds of
npm packages I have written, maintained, and/or contributed to over the past several years.

The development process (and CI pipeline) for every npm package can be conceived as, minimally,
having the following operations:

 * install
 * lint
 * test
 * build
 * document
 * publish

Most npm packages differ not in whether the above operations are (or should be) performed,
but in *how* those operations work. Here, package authors must make choices among a wide
variety of technologies. For first-time package authors, researching the options can be a
daunting and time-consuming task. Even experienced package authors like myself become
fatigued at scaffolding a new project, in simply *implementing* the technologies for which
the research has already been done and a decision made.

Many teams and communities have pursued a *scaffolding* strategy -- where a CLI tool is used
to generate the boilerplate for a project which can then be fine-tuned. This works well enough,
but the mere **presence** of boilerplate, or the involvement of code generation at all, is a
signal that npm packages are just too complicated to begin with.

Now that modern web browsers and Node.js have a natively supported common dialect for JavaScript
code written as ES modules, the era of complicated build toolchains for JavaScript may be
finally coming to an end.

Pak embraces this change, and through its technology choices is designed to facilitate the
development of new and existing npm packages as native ES modules:

 * Babel is used to transpile ESM source files into minified modules suitable for consumption in multiple formats. Only **index.mjs** source files are considered for inclusion.
 * ESLint is used to check source files for errors and code style inconsistency.
 * Mocha is used as a test runner, looking for **spec.mjs** files in the source tree for test suites to run.
 * C8 is used to measure code coverage by the test suite, and will **fail if coverage drops below 100%**.
 * Marked is used to convert the README into HTML for publishing.

[1]: https://www.npmjs.com/package/react-scripts
