# Word to mkdocs-material Instructions

## Goal

The goal is to convert all the Word `*.docx` files in the `import/` folder into a navigable multi-page mkdocs-material site of Markdown files, adopting the formatting and tables conventions of mkdocs-material and resolving all build and lint issues.

## Pre-Requisites

- Install `Pandoc`
- Install `markdownlint-cli2`
- Install `mkdocs` and `mkdocs-material`

## Approach

For each Word `.docx` file in the `import/` folder:

- Create a new folder under `docs/` with the title of the `.docx` file in snake-case for the mkdocs site files to be stored in.
- Use `Pandoc` to convert the Word file to a raw Markdown file of the same name with a `.md` extension.
- Analyse the raw converted `.md` file, if the file has a table of contents, use this to create a navigation that follows the structure of the original document.
- If there is no table of contents, use the main headings in the document as the navigation structure.
- The file should be split into separate Markdown files in the subfolder that was created under `docs/` as per the navigation structure above.
- Use snake-case naming for the separated Markdown files e.g. `this-is-a-heading.md`
- Process each separated Markdown file as per the Formatting rules below.

## Formatting

The following rules should be followed for the separated Markdown files:

- Utilise Markdown link format for links/URLs.
- Update any tables to be compatible with mkdocs tables format
- Tidy up the formatting of the tables to be more readable
- Use mkdocs-material admonitions blocks in the separated files as follows:
  - "Examples of practices to avoid" or similar use `!!! danger`
  - "Further reading and information" or similar use `!!! info`
  - "Practical tips" or similar use `!!! tip`
  - "Examples of good practice" or similar use `!!! example`
- Ignore/remove any images
- Attempt to preserve internal and external links in the separated files.
- The key words (when in all uppercase) "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" should be **BOLD**.

## Post-Conversion Steps

After converting the Word `.docx` file to the mkdocs site files do the following:

- Run  `markdownlint-cli2` with the `--fix` command with the `.markdownlint.json` config to resolve some linting issue automatically
- Do not attempt to fix any outstanding linting issues manually.
- Run the `mkdocs build` command and resolve any errors and warnings.
- Attempt to fix any broken internal links using high confidence fuzzy matching to account for any minor changes in heading names.

## Navigation

Once all post-conversion steps are complete:

- Update the site navigation config `nav` in `mkdocs.yml` to include the newly added files, matching the original order in the Word document.
- Ensure that each Word `.docx` file has a top-level navigation element and all converted subpages sit below this in the navigation.

## Other

- Commit any temporary scripts created whilst working on this into a `utils/` folder.
- Create a detailed log file of your work as you go and commit this with a unique name to an `output/` folder, only ever append to this log file.
- Once finished, create a formatted Markdown file in the `output/` folder that details the steps you took, the commands you ran and any work you undertook as part of this task.
