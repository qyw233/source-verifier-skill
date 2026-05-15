# Installation

Choose the package matching the language you want the agent to use:

```text
skills/source-verifier-en
skills/source-verifier-zh
```

Copy the chosen package directory into the skill directory used by your agent environment.

## Recommended Package Names

Keep package directory names stable:

```text
source-verifier-en
source-verifier-zh
```

Do not include version numbers in package directory names. Use the package `VERSION` file, Git tags, and GitHub Releases for versioning instead.

## GitHub Releases

For releases, publish zip artifacts with versioned names:

```text
source-verifier-en-v0.1.zip
source-verifier-zh-v0.1.zip
```

This keeps the repository layout stable while making release artifacts easy to identify.

