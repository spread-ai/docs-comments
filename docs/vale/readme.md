# Documentation templates
This repository has the templates for writing documentation, which include instructions and guidance. Our documentation is stored as Markdown files (.md). Markdown is a lightweight markup language. For more information on using Markdown, see the [Markdown Cheatsheet](https://www.markdownguide.org/cheat-sheet/).

## Documentation process
The main **docs-internal** repository consumes **docs** folders from the repositories of each of the SPREAD products and features. This repository isn't editable, so to create documentation for your feature you need to create a **docs** folder in your respective repo. Here are the steps to contributing your documentation:

1. Copy, clone, or fork the folders in this repository to your repo and rename it to **docs**. The templates, for different types of content, are: 
	* **overview:** An overview page template to introduce the topic. Importantly this needs to divert any readers who are confused and need to go elsewhere.
	* **conceptual:** The template for creating overview and conceptual content to help readers understand. You may have only one overview page per section, but as many conceptual pages as necessary.
	* **task:** The template for creating task pages that help readers to do something tangible. You may add as many task pages as necessary. The task page includes a Troubleshooting section.
	* **reference:** The template for strictly reference content.
	* **glossary:** The template for adding new terms alongside their definitions.
2.  Each template page is commented to help you write your content and create the appropriate Markdown. Read the comments in the code view and answer the questions posed in each section. You may answer the questions in bullet point format if you prefer, and it will be edited into prose later.]
3. You can find documentation that has already been written about your area of interest in the [2024.02 Documentation Audit](https://spreadai.sharepoint.com/:x:/s/ProductManagement/EY6G_k8C8_RNp66b3wsKQA0B5v00RKVydHEwEJmwZa0W-w?e=ePERPp) (incomplete). Copy anything useful.
4. Place any media (images, etc) in the **docs/src** folder and link to it where necessary.
5. Once your draft content is complete, notify the Documentation team by creating a ticket on the [DOC Jira board](https://solveit.atlassian.net/jira/software/projects/DOC/boards/156) asking for a content review.
6. When the content review is complete, the **docs-internal** repo consumes your **docs** folder as a submodule.
7. The **docs-internal** repo is published, with your documentation included.

## Writing documentation for technical users

Technical users who want to contribute to documentation can use GitHub's [web-based editor](https://docs.github.com/en/codespaces/the-githubdev-web-based-editor), [Visual Studio Code](https://code.visualstudio.com/), [JetBrains](https://www.jetbrains.com/products/#type=ide-vs), or any other text editor or Integrated Development Environment (IDE). The benefit of using Visual Studio Code or JetBrains is that you can lint your language while writing content (see [Language linting using Vale](#language-linting-using-vale)).

### Language linting using Vale

![An image of Vale inside Visual Studio Code](src/vale-inside-vscode-1280x800.png)

Vale is a lightweight writing tool that checks your writing for errors, and suggests fixes for better technical writing. We use Vale in the publish pipeline for creating our documentation, so it makes sense that you use it too when creating documentation. To enable Vale in Visual Studio Code:

1. Copy this repository into your project's repository and rename it `docs`. Make sure that it is a top-level directory.

2. Install the Vale CLI: `brew install vale`

3. Inside Visual Studio Code, install the [Vale-VSCode](https://marketplace.visualstudio.com/items?itemName=ChrisChinchilla.vale-vscode) extension.

4. Select **Code** > **Settings** > **Settings** or use the **⌘**-**,** shortcut to open Settings.

5. Select **Extensions** in the right-hand side menu and then select **Vale**. In the **Vale > Vale CLI: Config** field enter: `/Users/YOUR_USER_NAME/.../docs-template/.vale.ini`. Make sure to replace YOUR_USER_NAME with your user name and to replace the ellipsis with the path to the repository.

![An image of Vale inside Visual Studio Code](src/vale-extension-setting-1974x468.png)

6. In the **Vale > Vale CLI: Path** field enter: `/opt/homebrew/bin/vale`

6. Inside the `docs` directory run the following command in your terminal or console: `vale sync` 

7. Restart Visual Studio Code and start writing your content. Errors and suggestions will appear as you are writing.

For instructions on how to use Vale with JetBrains, see [JetBrains Integration](https://vale.sh/docs/integrations/jetbrains/) in the Vale Documentation.

## Writing documentation for non-technical users

Users who aren't developers can contribute to the documentation using tools such as TextEdit (already installed on macOS, save the file as a .md for Markdown), [MacDown](https://macdown.uranusjr.com/), [Bear](https://bear.app/), [Zettlr](https://www.zettlr.com/), or [Obsidian](https://obsidian.md/).

To start working on documentation, download the template that you want to develop, open it in your preferred editor, and create documentation. If you are working on existing documentation, download the **docs** folder from the GitHub repository of the feature you want to edit. 

After completing your work send the completed Markdown files to the documentation team for review.


