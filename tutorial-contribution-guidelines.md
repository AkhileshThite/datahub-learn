# 👀 Tutorial Contribution Guidelines

So you've decided to write a tutorial for Figment Learn? We're excited to have you among our contributors! 
Please take the time to read and understand the guidelines below to ensure your contributions follow the style and tone of our other tutorials.

Please read and understand our [Contributor Terms](./terms-and-conditions/contributor-terms.md) before proceeding.

When you are ready to submit your tutorial, open a Pull Request on the GitHub repository.

# General

Some do's and dont's on how to write and submit a tutorial to Figment Learn.

---

Do not copy and paste existing content. If the tutorial is inspired by some existing content (for example forking an ETH tutorial to convert it to Avalanche), reference it and link to it. When you link to other tutorials/resources, do it with Figment Learn resources as much as possible.

Include any potential walkthrough video in the PR by uploading it to Google Drive.

Funding of accounts from faucets needs to be explained clearly as to which account is being funded, from where and why.

Display sample outputs to help learners know what to expect, in the form of Terminal snippets or screenshots. Trim long outputs.

Take an error-driven approach where you bump into errors on purpose to teach learners how to debug them. Eg. If you need to fund an account to be able to deploy a contract, first try and deploy without funding, observe the error that is returned, then fix the error (by funding the account) and try again.

Add potential errors and troubleshooting. Of course, the tutorial shouldn't list all potential errors but the main important one.

Use React or Vue for the client-side.

Before making the PR run the code by yourself first to avoid any future unknown errors and to make sure it works as expected. 

Provide pictures/screenshots where needed.

Avoid Including external/cross-links to different sources in between the tutorials. 

Image links need to be in a relative path format: ![](../../../.gitbook/assets/image_filename.png)

# Structure

The Title should be direct and clear, summarizing the tutorial's goal.

Include an Introduction section explaining why this tutorial matters and what the context is. Don't assume this it's obvious.

Include Prerequisites: any prior knowledge needed or existing tutorials that need to be completed first, any tokens needed.

Include Requirements: any technology that needs to be installed prior to starting the tutorial and that the tutorial will not cover (Metamask, node, truffle, etc). Do not list packages that will be installed in the tutorial (dotenv).

Include a Conclusion section that summarizes what was learned, reinforces key points and also congratulates the learner.

(Optional) Include a What's Next section pointing to good follow up tutorials or other resources (projects, articles, etc).

(Optional) Include an About The Author section at the end. Your bio should include your Github handle (which will have your name, website, etc) and a link to your Figment Forum profile (so users can contact/tag you on Forum for help and questions).

References section must be present if you have taken any help in writing this tutorial from other documents, GitHub repos and other tutorials. Credit sources by adding their name and a link to the document when possible (if it is not a digital document, include an ISBN or other means of reference).

# Style

Explain your code. Don't just ask learners to blindly copy and paste

Function names, variables and constants must be consistent across the entire document.

Use of UI tabs to indicate a relative path & filename [as in Polkadot tutorials] (?) - similarly, use a UI tab to indicate a block of expected terminal output

Use a linter & prettifier before submitting your code. We recommend eslint for Javascript/React & tslint for TypeScript.

Use Markdown properly throughout the tutorial. You can refer to GitHub's markdown guide [here](https://guides.github.com/features/mastering-markdown/).

Select the appropriate language for syntax highlighting in code blocks:
  * Use `text` for any Terminal output, or any unsupported languages.
  * Use `javascript` for Solidity.
  * Use `bash` ONLY if you need to have # style comments in a Terminal output block.

The code blocks should be well commented. Comments should be short (usually two or three lines max at a time) and effective.
If you require more space to explain a piece of code, do it outside of the code block.

Writing Tone - Learn Tutorials are written by community contributors for their peers. 
As such, we recommend creating a tone of inclusion and interaction throughout the tutorial. 
Use words like “we”, “us”, “our”, for example “We have successfully deployed our contract”. 
When providing direct instructions feel free to use “you”, “your” etc. for example “Your file should look like this”.

# App setup

Create a folder to hold all the code (eg. mkdir example && cd example).

If you use npm init explain the prompts or use the -y flag.

If you use npm install use the --save flag.

If you mention .env and .gitignore during the tutorial setup, you can reference this [Extra Guides document](https://docs.figment.io/network-documentation/extra-guides/dotenv-and-.env) on docs.figment.io!

# Sample Tutorial Structure

Before submitting, please check that your format follows the sample tutorial structure [here](./sample-tutorial-structure.md)
