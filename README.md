# BrokenThorn Entertainment OS Development Series

## About this project

This repository is the base for generating static site documentation using DocFX (https://dotnet.github.io/docfx/).

The generated "conceptual documentation" aims to provide a better interface (compliant to more modern website/documentation standards) to navigate the OS dev series (http://www.brokenthorn.com/Resources/OSDevIndex.html) created by "BrokenThorn entertainment" (http://www.brokenthorn.com/) and at the same time correct any grammatical, spelling or conceptual errors in the tutorials.

>This project in no way intends to infringe on the copyright of the series and fully attributes the original documentation/tutorial series to "BrokenThorn entertainment Co.". I am not the author of this series which has been created with lots of expertise and effort by the original author.

**I'd like to thank the original creators for creating such a great starting point for systems developers. This is certainly the best starting point resource out there (created with a lot of effort), which I myself referred to during a "conceptual" project called `Lantern OS` which you can have a look at [here] (insert link here/coming soon) which has its own documentation (unlike this series, its documentation is not a tutorial, but is actually the software (OS) documentation).**

## Features of the project

This project uses markdown, more specifically [DFM (DocFX flavoured Markdown](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html), which enables to write formatted text in a much easier way. We can then generate static sites/ PDF documentation using the DocFX tool which is capable of making conceptual documentation among other things.

The generated site is hosted on github pages which takes it's content from `gh-pages` branch (which is a git orphan branch) whose contents are generated from the `master` branch and then transferred externally over to the `gh-pages` branch and committed whose changes will automatically get reflected [here] (insert link)

1. The website has a TOC (Table of contents) to the left hand side which can be used to easily navigate the tutorials while referring to them as you jump between sections.
2. There is a search box provided which helps you scour the tutorials for something you know is there, but just can't remember where!
3. There is a TOC given on the right hand side which helps you navigate between various heading/sections within a tutorials and see what's in the tutorial, at a glance.
4. The content itself is better that before with most spelling and grammatical errors corrected.
5. The content is now more readable with the latest docs styling used which puts code in boxes and has clearly marked boxes for warnings, notifications, and other type of alerts.
6. The UI in general is better with lots of documentation features resembling that of `docs.microsoft.com` which has a battle-tested documentation system. (more features are coming up in DocFX v3)
7. More features coming soon! (Scroll below for information on **contributing** to the project)

You can track upcoming features on the project boards [here] (insert link)

## Feedback: Issues and Suggestions

**Issues**: If you face issues while using the website, do file them in the issues section (you will obviously need a github account for that) and I or someone will take up the job of solving it. 

**Suggestions**: If you have an idea or suggestion, do file it in the `issues` section with the `enhancement` tag and I will consider taking it up, or one of the contributors might.

Please make sure that you don't file a duplicate issue/feature (not that it's much of a burden to remove it, but do check for duplicates!).

## Development and usage

This project consists of two branches, `master` and `gh-pages`. Both branches are independent of each other (orphan branches).

- The `master` branch consists of the base code in YAML and MarkDown where the actual documentation/tutorial is written.  
  This base can then be processed by `DocFX` which can generate a static docs website or a PDF. The site is generated in a folder called `_site` (which you can use to debug the documentation) and is **not tracked** by `git` (it is listed in `.gitignore` file).
- The `gh-pages` branch consists of nothing but the `_site` folder and an `index.html` file and is responsible for hosting the static site as part of `github pages`. Each time you commit to this branch the website gets updated within a few hours.
- When you generate the site from the `master` branch, copy it to an external location, checkout the `gh-pages` branch and then modify the website on the `gh-pages` branch.

To develop this project, you need

1. `DocFX`, which you can install using instruction provided [here](https://dotnet.github.io/docfx/index.html).
2. It is also recommended to use `Visual studio code` (download it [here](https://code.visualstudio.com/)) editor to edit the markdown files as we use [DFM (DocFX flavoured Markdown](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html) whose live website preview (while editing) is supported by the `Docs authoring pack` VS Code extension provided by microsoft (download it [here](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) or from the extensions tab in VS Code).

Once you have the tools installed on your machine, to generate the site,

- on the `master` branch, open a shell in the main project folder and run `docfx` which build the site
- then go into the `_site` folder (which contains the static site files) by running command `cd _site`
- serve the site as a webpage to view it using `docfx serve` which serves the webpage at `localhost:8080`, which you can view in your browser.
- Just use the `Ctrl+C` keyboard interrupt to stop the server.
- You can run `docfx help` or `docfx help serve` for mroe information on using the commands.

Each time you edit the files you will have to repeat the same process (DocFX v3, which is coming soon, will enable faster build times and live previews). For now you can use the `Docs authoring pack` VS Code extension provided by microsoft for live previews within the code editor. The preview will not be exactly like that of the website, but it will be close enough. Learn how to use it [here](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack).

## Contributions

I would love to receive contributions to the tutorials, not only in terms of new, helpful content, but also in correcting errors, making things clearer with better wording, more links and references to other resources that might be helpful to the community members, along with improvements in the UI (if you are experienced in using DocFX) and ANY OTHER THING that might be USEFUL!

Do not shy away from contributing anything that's useful. Though, before doing that you might want to check if someone else is working on the same feature or issue.

If you are working on a new feature or issues, please make sure you make a new `issue` in the issues sections to tell the community/audience that you are working on the aforementioned feature/issue so that there is no "duplicate" work done.

To contribute effectively, you must be familiar with the way `git` and `github` work and you must also have a github account.
You might also need to know how to use docfx, which you can learn [here](https://dotnet.github.io/docfx/)

To make changes to the code:

1. Just `fork` ([Here's](guides.github.com/activities/forking/) how to fork) the repository. (Make sure your fork is up-to-date if you have forked this repo before. [Here's](https://stefanbauer.me/articles/how-to-keep-your-git-fork-up-to-date) how to do that.)
2. Pull it to your machine it and make the changes. (I recommend you to work on a separate branch, so that you can work on another branch, say if you are working on an issue and a new feature at the same time, both of which are unrelated to each other, suggesting the use of different branches)
3. After you have made the changes to the code, make sure it works properly and nothing is broken due to the changes you made.
4. Then, commit it with a meaningful commit message with a heading and detailing all changes made. You can look at the commit messages of any of the commits to see the format for commit messages.
5. Then push it back to your version (the fork) of this repository. 
6. Then make a `pull request` (**you might want to use `github desktop` to do this kinda stuff**) from your fork to this repo and I will look into the changes and `merge` you pull request if everything works fine, or I will ask you to make any required changes before doing so.  
  Sometimes, the pull request may not be "merge-able" because of changes made to the repo by others/me after you forked the repo. In that case, you could either change your code, or wait until I've reviewed the situation and given my "verdict".

>When you make the pull request, make sure to mention any issues or conditions where the code won't work/ build when built with DocFX. Include any other details you deem necessary to share with me.

>NOTE: Do not make any changes to the `gh-pages` branch as that code is generated using DocFX. Any changes that have to be made, must be done on the `master` branch.

For the avoidance of doubt, you may not make any Submissions linking to third party materials if such Submission is prohibited by the applicable third party and/or otherwise violates such third party's rights. Also, by contributing to this repo, yuo are automatically agreeing to the condition that the community is free to use your contributions under the license of this project.

>**More information on how to contribute coming soon...**

## License

I created this project, but I certainly didn't write any of the documentation/tutorial series, whose contents belong to "BrokenThorn entertainment Co.". Thus, the actual content license belongs to them. You can view their **Privacy policy** [here](http://www.brokenthorn.com/Resources/Privacy.html) and their **Terms of use** [here](http://www.brokenthorn.com/Resources/terms.html). You can read their own legal statement [here](http://www.brokenthorn.com/Resources/OSDevIndex.html).

>The provided **Privacy policy** and **Terms of use** links don't seem to work.

Until I can confirm the legal structure to use with "BrokenThorn entertainment Co.", in interest of the community, I have assigned it a **AGPL-3.0 license** whose details you may read in the **`LICENSE`** file, or a shorter version [here](https://choosealicense.com/licenses/), which requires that whatever changes you make to this project to distribute publicly, you must share the source code which can in turn help our community make better software and learn more effectively.

## Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/).
