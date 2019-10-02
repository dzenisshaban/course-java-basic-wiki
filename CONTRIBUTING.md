## Pull Requests
Please follow these steps to have your contribution considered by the maintainers:
- Pull actual branch where need to do changes
- Follow the [styleguides](#styleguides) when making changes
- Create PR with [template](PULL_REQUEST_TEMPLATE.md)


## Styleguides
### Git Commit Messages
- Use the present tense ("add feature" not "added feature")
- Use the imperative mood ("move cursor to..." not "moves cursor to...")
- Limit the first line to 50 characters or less
- Limit body to 72 characters or less
- Reference issues and pull requests liberally after the first line
- The first line of the commit contains the name of the artifact (task/test/doc) and the name of the module
- Consider starting the commit message with:
    - `add:` when adding artifact
    - `rm:` when removing artifact
    - `fix:` when fixing mistake
    - `refactor:` when updating artifact or strong operation
    - `doc:` when adding/removing/fixing/updating documentation

### Artifactory naming
- Use only English
- For files and directories: kebab case (example: `stream-api`) expect:
    - `Markdown` files: where the first letter and keywords can be uppercase (example: `Method-overloading-in-Java.md`)
    - documentation