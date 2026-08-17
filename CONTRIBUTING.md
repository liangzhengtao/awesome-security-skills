# Contributing to Awesome Security Skills

Thank you for your interest in contributing! This project thrives on community input, and we welcome contributions of all kinds.

## Ways to Contribute

- **Report errors** in existing skill files (outdated tools, incorrect commands, broken links)
- **Propose new skills** that fill a gap in our coverage
- **Improve existing skills** with additional techniques, tools, or templates
- **Translate skills** to other languages
- **Add examples and test cases** to existing skills

## How to Contribute

### Reporting Issues

1. Check existing issues to avoid duplicates.
2. Use the appropriate issue template (Bug Report, Feature Request, New Skill Proposal).
3. Include as much context as possible: file path, section, and the specific problem.

### Submitting Changes

1. **Fork** the repository.
2. **Create a branch** from `main`:
   ```bash
   git checkout -b feature/your-skill-name
   ```
3. **Make your changes** following the style guide below.
4. **Test your changes** — ensure all links work and formatting renders correctly.
5. **Submit a pull request** using the PR template.

### Creating a New Skill

New skill files must follow the established structure:

```markdown
# [Skill Name]

> One-line description of the skill.

## When to Use
[Scenarios and triggers]

## Prerequisites
[Required knowledge and access]

## Tools
[Table of tools with names, purposes, and licenses]

## Step-by-Step Procedure
[Phased workflow with commands and code examples]

## Templates
[Ready-to-use templates]

## Common Pitfalls
[Mistakes to avoid]

## Legal Considerations
[Authorization, disclosure, compliance]

## Further Reading
[Authoritative reference links]
```

### Style Guide

- **Markdown**: Use standard Markdown. No HTML unless absolutely necessary.
- **Line length**: Keep lines under 120 characters for readability.
- **Code blocks**: Use fenced code blocks with language identifiers (` ```bash `, ` ```python `, etc.).
- **Tables**: Use Markdown tables for structured data. Keep columns aligned.
- **Language**: Write primarily in English. Include Chinese translations for section headers where appropriate.
- **Tone**: Professional, direct, and actionable. Avoid marketing language.
- **Minimum length**: Each skill file must be at least 150 lines.
- **Links**: Use full URLs for external references. Use relative paths for internal links.

### Skill Naming Convention

- File names: `kebab-case.md` (e.g., `api-security.md`)
- Directory names: Use the original language name (e.g., `Web安全`, `代码审计`)
- Skill titles: Use the full descriptive name (e.g., "API Security Best Practices")

## Code of Conduct

By participating in this project, you agree to abide by our [Code of Conduct](CODE_OF_CONDUCT.md).

## License

By contributing, you agree that your contributions will be licensed under the [MIT License](LICENSE).

## Questions?

If you have questions about contributing, open a Discussion in the GitHub repository or reach out to the maintainers.

Thank you for helping make security knowledge more accessible!
