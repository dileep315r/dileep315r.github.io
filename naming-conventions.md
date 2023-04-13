#### Naming conventions

Always follow existing repository conventions. For new projects, follow the following conventions.

### Repository naming convention
1. Use [```repo-case```](https://stackoverflow.com/questions/11947587/is-there-a-naming-convention-for-git-repositories) for repository names.
    1. [Do not](https://github.com/bcgov/BC-Policy-Framework-For-GitHub/blob/master/BC-Gov-Org-HowTo/Naming-Repos.md) prefix the name with organization name as the organization name may change in future.
    2. Use app, cmdapp, api, client etc.. postfix to denote the kind of component.
    3. Use ```smallcase``` naming convention for kotlin packages. Follow [this](https://kotlinlang.org/docs/coding-conventions.html#naming-rules) doc for kotlin naming convention.

### Git commit message naming conventions
1. Use all ```smallcase``` catenated words for package/directory names.
2. Use [```repo-case```](https://stackoverflow.com/questions/11947587/is-there-a-naming-convention-for-git-repositories) for repository names.
    1. [Do not](https://github.com/bcgov/BC-Policy-Framework-For-GitHub/blob/master/BC-Gov-Org-HowTo/Naming-Repos.md) prefix the name with organization name as the organization name may change in future.
    2. Use app, cmdapp, api, client etc.. postfix to denote the kind of component fot top level directories in www.
    3. Use ```smallcase``` naming convention for kotlin packages. Follow [this](https://kotlinlang.org/docs/coding-conventions.html#naming-rules) doc for kotlin naming convention.

### Commit message conventions
1. Use following format
    ```
    <type>[optional scope]: <description>

    [optional body]

    [optional footer(s)]
    ```

    1. Recommended type values: fix:, feat:, build:, chore:, ci:, docs:, style:, refactor:, perf:, test:
    1. Fix: Bug fix.
    2. Feat: New feature.
    3. Chore: Fix versions, bump versions.
    4. test: Add test cases.
    2. Scope examples: app, parser, api.
    3. Note the breaking change with ```!``` before :. For example ```feat(api)!``` denotes a breaking change.
    4. Example

        ```
        feat: allow provided config object to extend other configs

        BREAKING CHANGE: `extends` key in config file is now used for extending other config files
        ```

2. Other rules
    1. Separate subject from body with a blank line
    4. Limit the subject line to 50 characters
    5. Capitalize the subject line
    6. Do not end the subject line with a period
    7. Use the imperative mood in the subject line
    8. Wrap the body at 72 characters
    9. Use the body to explain what and why vs. how
3. Benefits
    1. A well-crafted Git commit message is the best way to communicate context about a change to fellow developers (and indeed to their future selves). A diff will tell you what changed, but only the commit message can properly tell you why. Re-establishing the context of a piece of code is wasteful. We can’t avoid it completely, so our efforts should go to reducing it [as much] as possible. Commit messages can do exactly that.
    2. Understanding why something happened months or years ago becomes not only possible but efficient.
    3. Automatically generating CHANGELOGs.
    4. Automatically determining a semantic version bump (based on the types of commits landed).
    5. Communicating the nature of changes to teammates, the public, and other stakeholders.
    6. Triggering build and publish processes.
    7. Making it easier for people to contribute to your projects, by allowing them to explore a more structured commit history.
4. Inspired from:
    1. https://cbea.ms/git-commit/
    2. https://www.conventionalcommits.org/en/v1.0.0/ 
