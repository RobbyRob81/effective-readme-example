# effective-readme-example



# Acquisition Squad (Static-rendered Marketing Pages)


## Contents

- [Project Dependencies](#technology)
- [Branching Strategy](#branching-strategy)
- [Setup](#setup)
- [Storybook](#storybook)
- [How to build UI](#how-to-build-ui)
- [Workflow](#workflow)
- [Contentful](#contentful)
- [Deployments](#deploying)
- [Troubleshooting](#troubleshooting)

## Project Dependencies

---

Each contributor will need to be familiar with or become familiar with the following

### Technology

- [NextJS](https://nextjs.org/): React framework for production (SSR, Hybrid, Static, Pre-fetching, etc)
- [React](https://reactjs.org/docs/thinking-in-react.html#gatsby-focus-wrapper): JS UI Library
- [React Hooks](https://reactjs.org/docs/hooks-faq.html#gatsby-focus-wrapper): Lifecycles/middleware for React
- [Jest](https://jestjs.io/): Testing Framework with a focus on simplicity
- [React-Testing-Library](https://testing-library.com/docs/react-testing-library/intro/): Testing components and the DOM from the users perspective
- [Apollo](https://www.apollographql.com/): Industry-standard GraphQL implementation
- [Storybook](https://storybook.js.org/): Open source tool for developing UI components in isolation
- [EsLint](https://eslint.org/): Statically analyzes your code to quickly find problems
- [Styled-Components](https://styled-components.com/docs): Visual primitives for the component age
- [EditorConfig](https://editorconfig.org/): Maintain consistent coding styles across IDEs

### Concepts

You will need to be familiar with the following concepts.

- [Smart and Naive Components](https://www.digitalocean.com/community/tutorials/react-smart-dumb-components)
- [Component Driven Development](https://cobwwweb.com/wtf-is-component-driven-development)
- [Atomic Design](https://bradfrost.com/blog/post/atomic-web-design/)
- [Common HTML UI Patterns](https://www.w3schools.com/howto/)
- [Common UI Patterns Using Grid](https://gridbyexample.com/examples/)
- [Common UI Patterns Using Flexbox](https://www.flexboxpatterns.com/)

## Branching Strategy

[More here](https://aspirationpartners.atlassian.net/wiki/spaces/EN/pages/89292957/Aspiration+Branching+Strategy+and+Deployments)

## Setup

Ping team (#engineering_frontend slack) for `.env` file contents.

---

Clone the repository

```sh
$ git clone git@github.com:AspirationPartners/acquisition-ui.git

Cloning into 'acquisition-ui'
Receiving objects, done
Receiving deltas, done
```

Install dependencies

```sh
$ yarn

info No lockfile found.
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 🔨  Building fresh packages...
success Saved lockfile.
✨  Done
```

You may now either start dev

```sh
$ yarn dev

info  - Loaded env from /Users/rrtrosario/Documents/Github/acquisition-ui/.env
The static directory has been deprecated in favor of the public directory. https://err.sh/vercel/next.js/static-dir-deprecated
Warning: Built-in CSS support is being disabled due to custom CSS configuration being detected.
See here for more info: https://err.sh/next.js/built-in-css-disabled

info  - Using external babel configuration from /Users/rrtrosario/Documents/Github/pyclite-ui/babel.config.js
event - compiled successfully
> Ready on http://localhost:3000
```

### Generators

---

The concept here is that everything that can be automated should be. Easily add to the project with the following scrips:

```bash
yarn g
```

or

```bash
yarn g <template> <name_you_want_to_give>
```

The available templates are as follows
|Definitions|
|---------|

#### Atoms

The simplest form of UI, consisting of things like headers, labels, input fields, buttons.

<img style="float:left; padding:.5rem; width:45%" src="https://uploads.toptal.io/blog/image/129104/toptal-blog-image-1549895602417-eb8217418e1c8f80914ae43b9f4e94fe.png"> 
<img src="https://uploads.toptal.io/blog/image/129102/toptal-blog-image-1549895581254-14d37d7c649932df1ba0d86d83bd3094.png" style="width: 45%; float:left; padding:.5rem">|


#### Molecules

A combination of atoms that form more complex pieces of our UI, such as a search field with a submit button.

#### Organisms

Build on top of molecules and orchestrate larger parts of the UI. This can include a list of products, a header, forms, etc. Organisms can even include other organisms.

#### Templates

Where our pages start to come together, giving context to all of our organisms and molecules by giving them a unified purpose. For example, a template for a contact page will have organisms for headers and forms, and molecules for text fields and navigation bars.

Resources: [Atomic-Design](https://www.toptal.com/designers/ui/atomic-design-sketch), [Atomic-Design for Engineering](https://www.newline.co/@kag359six/atomic-design-for-developers:-atomic-engineering--54fbebc5)

### Living Style Guide

```bash
yarn storybook
> Ready on http://localhost:9009
```

---

We use storybook to bring transparency into the development cycle and to achieve the following:

- Increased velocity
- Streamline the workflow
- Build components in isolation
- Mock hard to reach use cases
- Document use cases as stories
- Share and reuse everything
- Ship with confidence

- [Storybook.js.org](https://storybook.js.org/docs/basics/introduction/): for docs
- [learnstorybook.com](https://www.learnstorybook.com/): for tutorials

### Story structure

Component stories should capture each possible state individually. You can read more about it [here](https://www.learnstorybook.com/intro-to-storybook/react/en/simple-component/).
![Image of Todo List](https://www.learnstorybook.com/intro-to-storybook/task-states-learnstorybook.png)

## Storybook

- [Getting Started](https://storybook.js.org/docs/react/get-started/introduction)
- [Writing Stories](https://github.com/storybookjs/storybook/blob/next/addons/controls/README.md#writing-stories)

```JS
export default {
  title: 'Design System/Molecules/Card',
  component: Card,
  argTypes: {
    onClick: action("Click")
  }
}

const Template = (args) => <Card {...args} >Card Example</Card>
export const Primary = Template.bind({})
```

The argTypes property lets us set the control for our args. In our example, we set the backgroundColor prop to be controlled with the 'color' control, which is the color picker.

Below that, we have our stories code. We create a template from the Button component with our Template function. It takes the args we pass in and passes them all off to the Button.

Then, we call Template.bind to let us pass the args as props to Button by setting the args property to an object with the props.

> Template.bind returns a story object, which we can configure with args. This is a convenient way to set the props that we want to preview in our story.

## How to build UI

[Styled System Reference Table](https://styled-system.com/table/)

### Testing

---

• Storybook
• Jest
• addon-storyshots
• storyshots-puppeteer

We use the testing pyramid to ensure we deliver high quality user experiences. We've automated unit and most integration test cases by using jest, storybook and storyshots. Our stories generate tests to cover:

• Unit tests (good coverage)
• Integration tests, visual regression
• End-to-end test, cross-browser visual regression

Having React coupled with Storybook and Storyshots, unlocks a different model: the Diamond model.
The diamond model for your UI/App means: little to zero unit tests, massive amount of integration tests, and zero manual tests.

What changed? Integration tests were avoided in the early days because they had a reputation of running slowly; granted — with most technologies this is still very true.

With Jest, React, and Storybook/Storyshots, this is (arguably) no longer the case. No longer must you bring up a browser for each test that leaves its traces in your test environment, or have flaky test suites run and fail randomly, using a not-so-smart test runner that forces you to run everything exactly when you didn’t want to. It’s an era where frontend tooling really does work, and hard becomes easy.

#### Structural Tests

If you already write stories for every component, you already are writing tests, and you just don’t know it yet. Given the thesis above, each of your stories can automatically become a tests:

- Input is your story
- Processing is simply rendering a story (which storybook already does)
- Output is a generated snapshot

And this is what Storyshots does. Storyshots will verify that a React component renders correctly; and if you build multiple stories with a number of different properties then Storyshots can snapshot those as well, and those would be verified on every test run.

| Test Type          | Level       | Subject        | Solution   | Source    |
| ------------------ | ----------- | -------------- | ---------- | --------- |
| Browser Regression | Integration | Page/Component | Storyshots | Story     |
| Visual Regression  | Integration | Page/Component | Storyshots | Story     |
| Render             | Integration | Page/Component | Storyshots | Story     |
| Interaction        | Unit        | Component      | Storyshots | Unit Test |

That said, you should definitely keep your “classic” unit tests for logic, library and domain model code. All these things you put in /lib, external packages that deal with your domain model and so on.

You can read more about it [here](https://medium.com/hiredscore-engineering/how-to-test-a-full-react-app-using-nothing-but-storybook-15f4c584e30a)

#### Commands

- `yarn storybook`, starts storybook at [localhost:6006](http://localhost:6006/)
- `yarn test:imageshots`, compares updated UI to image snapshots
- `yarn test:snapshots`, compares react tree to previous tree
- `yarn test:coverage` view coverage report in the browser
- `yarn test:coverage:update` updates test coverage report
- `yarn coverage:wallaby` view coverage report in the browser via Wallaby extension

#### How to build using TDD (test driven development)

```shell
yarn storybook; yarn test --watchAll
```

This will launch storybook in a chrome and run both snapshot testing and visual regression tests as you build out your interfaces.

#### Wallaby inline IDE test coverage

You can get test coverage feedback in your editor if you use Wallaby.js More info about it can be found [here](https://wallabyjs.com). You'll need the pro version to use all the features, it's highly recommended.

1. Install IDE extension. More info [here](https://wallabyjs.com/download/)
2. Configure via Automatic Configuration, select `Automatic Configuration <project directory>` More info [here](https:/wallabyjs.com/docs/intro/config.html)
3. You Should now see test coverage in your editor.
4. Optional, you can view the app test coverage by going to [http://localhost:51245](http://localhost:51245) to see test coverage

---

### URL (Marketing) Redirects

The new model for URL redirects is now 50% self-service!

For example, to achieve a redirect like:

```
https://www.aspiration.com/green ➝ https://www.aspiration.com/get-account-100?utm_source=DirectResults
```

you would simply create a file in `./redirects/` named `green` with the content `/get-account-100?utm_source=DirectResults`

You can then push this to your dev branch, but will need to coordinate with DevOps to get the routing to your new redirect created in Alpha and Prod (for now).

---

### Storybook Deployment

Every push to origin results in a CircleCI build, and a Storybook. You need to be connected to VPN to view your Storybook, and they follow this pattern:

```
https://build-artifacts.aspiration.io/acquisition-ui/storybook/18490/index.html
                     Your CircleCI build number (found in URL) --^
```

The latest `master` Storybook is always available at: https://build-artifacts.aspiration.io/acquisition-ui/storybook/index.html

## Workflow

When working on a new feature, bug fix, or Jira ticket, branch off of master into a feature branch.

You must name your branch following this pattern.

```
 docs|feature|fix|hotfix + / + JIRA_TICKET_NUMBER + -pr-title-in-lowercase
```

When your work is complete, please run the tests with the coverage and update flags enabled.

```
yarn test:coverage:update
```

Then open a pull request against master for code review. Make sure to respect our commit convention. We follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification, and add the Jira ticket number in front of it.

I.E.

```
feature/AU-0000-improve-read-me
```

Every PR must have a sandbox URL associated with it. The sandbox must follow the next convention.

```
https://rebrand.alpha.aspiration.com/<branch-name>/<page>
https://rebrand.alpha.aspiration.com/feature/AU-0000-fix-ui/get-account
```

Eventually this will be enforced by git or a GitHub check. Make sure to include a link to the Jira ticket in your PR (preferably at the very beginning).

In your PR, include a description and/or screenshot(s) of the changes made. If you include a screenshot with multiple elements (such as an entire page), please markup the screenshot to pinpoint exactly what was changed or added. This will help give your code reviewers context into the changes you've made. See this PR for an example.

At least one other engineer must approve your PR before it goes to QA. If your PR is approved, but additional changes are made later, the PR must be reviewed again by the same engineer to ensure no breaking changes were introduced.

## Deploying

### Sandbox and Alpha

Every branch that is pushed up with the branching pattern listed above should trigger a sandbox build in [CircleCI](https://app.circleci.com/pipelines/github/AspirationPartners/acquisition-ui). This is deployed as a _static_ generated build, just like production, so [none of the SSR features](https://nextjs.org/docs/advanced-features/static-html-export#unsupported-features) of Next.js will be available. Once your sandbox is built, it should be available at the URL noted above in [workflow](#workflow).

To deploy a ticket to alpha specifically, an `-alpha` release tag may be used (see instructions below), otherwise your changes will automatically go to the base alpha environment upon merging to master.

### Production

All tickets being merged to master are assumed to be ready for a production release. After merging, be sure to trigger a production release via one of the methods below (if the time of day, etc. is appropriate). Merging to master does not trigger a production release on its own. Please reach out to the UA FE (@acq-fe) team for questions about this process.

_Note:_ Before deploying, be sure to make a release request in our #prod-approvals slack channel using the `/release` slack command. There should be instructions provided, but here you list the PRs and associated tickets (if any) for those PRs. Once the release is approved, you can publish the release. If you use the first method below, you can easily generate release notes and see which PRs have been merged since the last release.

There are two ways that production deployments can be triggered:

1. [Create a tagged release](#tagged-release) (_recommended_)
2. [Publishing a Contentful Page](#contentful-page-publish)

#### Tagged Release

This method should be used for the majority of code releases, especially when there are no Contentful changes associated it with it. Please use the conventions of previous releases to create the release.

##### Steps:

1. Access the `acquisition-ui` releases page [here](https://github.com/<organization>/<repository>/releases)
2. Make note of the current release version
3. Click the "Draft a new release" button
4. Enter the new tag number (see below for naming note) in the "Choose a tag" dropdown. Copy this tag name.
5. Enter/paste the tag name as the release title
6. From the "Target:" dropdown, access the "Recent Commits" tab and select the last PR merge commit that you are approved to release (usually the top one in the list).
7. Click the "Generate release notes" button on the right side. This should generate markdown release notes relative to the last release. You may need to edit this if anything was deployed through a publish.
8. Click "Publish release" and a build should be triggered in CircleCI.

##### Tag naming note:

Generally, the tag and title should be a patch version increment of the previous, for example `v0.2.45-prod` after `v0.2.44-prod`. Using the `-prod` postfix is essential to trigger the production build.

#### Contentful Page Publish

This method should be reserved for content updates made by the Product or Marketing teams or when content is needed for a new feature or page. Leaving this deployment specific to content allows us to better target when/how production failures may occur.

Publish builds are triggered by publishing a **Page** content type in Contentful. Note that publishing any other content type in Contentful will _not_ trigger a build, even if it's attached to a published page. You must first publish the content, then publish the Page itself to trigger the build. Any kind of change will allow the Page to be published.

One trick that has been used to force a Page publish is to make a simple change, such as adding and removing a space from the title and then publishing. This should not be used in place of a tagged prod build though.

#### Emergency Rollback (Operated by DevOps)
Each build is also stashed in a `/rollback/` directory in S3 so you can easily do an emergency rollback if needed.
1. Find the CircleCI build number of the version to rollback to, EG: `25346`
2. Run the command:
```
aws s3 cp s3://<bucket_name>/rollback/circle-25346/ s3://<bucket_name>/ --recursive --acl public-read --cache-control max-age=300 --dryrun
```
3. If the output makes sense, run again without the `--dryrun` flag
4. When the site is operational again, ask UA Squad to do a Prod deployment to reconcile any S3 object-level configuration differences, as well as clarical differences. Prod does not match what's in GitHub and Contentful until this is done!


## Contentful

### Development

New pages in the `/pages` folder should use the extension of `.dev.js` to indicate they are in development mode. These pages will be ignored in the production build. If they are using content that is not yet available in the `cms` environment, the production build will fail while fetching unmerged content changes.

### Environments

The main environment (similar to a git branch) for our project in Contentful is `cms`. The build-time environment can be configured locally in the environment variables with the key `CONTENTFUL_SPACE_ENV`. During run-time, you can set the environment via query param, for example: `?contentful_env=nyc`.

## Troubleshooting

### Unexpected snapshot failures/updates on test runs

Run `yarn test:clean`, then restart the tests. This is typically caused by a jest caching issue. Pages known to be flaky here are:
- Careers
- Press

### Unexpected snapshot updates when using interactive snapshot updating in `--watch` mode

This mode doesn't work properly. It appears to be because of the way the storyshots tests are programmatically generated in the various `tests/*Snapshots.test.js` files.

### Not getting expected data after updating GraphQL query model

Run `yarn build:clean` and restart `yarn dev`. Caused by Next.js/Babel caching. Queries are pre-compiled by Babel with `import-graphql`.

### Seeing warnings about `Missing field '*' while writing result` during test run

This is expected and does not directly affect test results. It's caused by queries being updated without updating the associated story mocks, so Apollo complains about the field missing from the incoming (mocked) data.
