# Test Custom Action

A repository for testing and learning how to create custom GitHub Actions and publish them to the GitHub Marketplace.

## Overview

This project serves as a sandbox for experimenting with different types of GitHub Actions:

- JavaScript/TypeScript Actions
- Docker Actions
- Composite Actions

## Table of Contents

- [Getting Started](#getting-started)
- [Action Types](#action-types)
- [Development Setup](#development-setup)
- [Testing Actions](#testing-actions)
- [Publishing to Marketplace](#publishing-to-marketplace)
- [Examples](#examples)
- [Resources](#resources)

## Getting Started

### Prerequisites

- Git
- Node.js (for JavaScript/TypeScript actions)
- Docker (for Docker-based actions)
- GitHub account

### Clone this repository

```bash
git clone https://github.com/git-biswojit/test-custom-action.git
cd test-custom-action
```

## Action Types

### 1. JavaScript/TypeScript Actions

JavaScript actions run directly on the runner and are fast to execute. They're great for simple automations and API interactions.

**Pros:**

- Fast execution
- Easy to debug
- Rich ecosystem (npm packages)

**Cons:**

- Limited to JavaScript runtime
- Potential security concerns with dependencies

### 2. Docker Actions

Docker actions package your code in a Docker container, providing a consistent execution environment.

**Pros:**

- Language agnostic
- Consistent environment
- Full control over dependencies

**Cons:**

- Slower startup time
- Larger package size
- Only works on Linux runners

### 3. Composite Actions

Composite actions combine multiple workflow steps into a single reusable action.

**Pros:**

- Reuse existing actions
- Mix different action types
- No additional runtime overhead

**Cons:**

- Limited customization
- Debugging can be complex

## Development Setup

### For JavaScript Actions

1. Initialize a new Node.js project:

```bash
npm init -y
npm install @actions/core @actions/github
npm install -D @types/node typescript
```

2. Create basic action structure:

```
action.yml
src/
  index.js (or index.ts)
package.json
```

### For Docker Actions

1. Create Dockerfile:

```bash
touch Dockerfile
```

2. Create action metadata:

```bash
touch action.yml
```

## Testing Actions

### Local Testing

1. **Using act**: Test actions locally with act

```bash
# Install act
brew install act  # macOS
# or
curl https://raw.githubusercontent.com/nektos/act/master/install.sh | sudo bash

# Run workflow locally
act
```

2. **Unit Testing**: Write tests for your action logic

```bash
npm test
```

### Integration Testing

Create test workflows in `.github/workflows/test.yml` to verify your action works correctly.

## Publishing to Marketplace

### Prerequisites for Publishing

1. **action.yml file**: Must be in repository root
2. **README.md**: Comprehensive documentation
3. **Proper tagging**: Use semantic versioning
4. **License**: Include a license file

### Steps to Publish

1. **Prepare your action**:
   - Ensure `action.yml` is complete and valid
   - Test thoroughly
   - Document all inputs/outputs

2. **Create a release**:

   ```bash
   git tag -a v1.0.0 -m "First release"
   git push origin v1.0.0
   ```

3. **Publish to Marketplace**:
   - Go to your repository on GitHub
   - Navigate to "Releases"
   - Create a new release
   - Check "Publish this Action to the GitHub Marketplace"
   - Fill in required information

### Marketplace Requirements

- Repository must be public
- Must have an `action.yml` file in root
- Must have a README.md
- Must include proper branding (icon, color)
- Must follow GitHub's terms of service

## Examples

### Basic JavaScript Action

```yaml
# action.yml
name: 'Hello World'
description: 'Greet someone'
inputs:
  who-to-greet:
    description: 'Who to greet'
    required: true
    default: 'World'
outputs:
  time:
    description: 'The time we greeted you'
runs:
  using: 'node20'
  main: 'dist/index.js'
```

### Docker Action Example

```yaml
# action.yml
name: 'Container Action'
description: 'Run a command in a container'
inputs:
  command:
    description: 'Command to run'
    required: true
runs:
  using: 'docker'
  image: 'Dockerfile'
  args:
    - ${{ inputs.command }}
```

### Composite Action Example

```yaml
# action.yml
name: 'Composite Action'
description: 'Multiple steps in one action'
runs:
  using: 'composite'
  steps:
    - run: echo "Hello from composite action"
      shell: bash
    - uses: actions/checkout@v4
    - run: npm install
      shell: bash
```

## Best Practices

1. **Clear Documentation**: Always document inputs, outputs, and usage examples
2. **Error Handling**: Implement proper error handling and meaningful error messages
3. **Security**: Never hardcode secrets, use action inputs
4. **Versioning**: Use semantic versioning and maintain backward compatibility
5. **Testing**: Test on different operating systems and scenarios
6. **Performance**: Optimize for speed and resource usage

## Troubleshooting

### Common Issues

1. **Action not found**: Check action.yml syntax and file location
2. **Permission errors**: Verify token permissions
3. **Docker issues**: Ensure Dockerfile builds correctly
4. **Syntax errors**: Validate YAML syntax

### Debugging Tips

- Use `console.log()` for JavaScript actions
- Add debug steps in composite actions
- Check action logs in workflow runs
- Use `actions/toolkit` for better debugging

## Resources

### Official Documentation

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Creating Actions](https://docs.github.com/en/actions/creating-actions)
- [Publishing Actions](https://docs.github.com/en/actions/creating-actions/publishing-actions-in-github-marketplace)

### Tools and Libraries

- [@actions/toolkit](https://github.com/actions/toolkit) - Official toolkit for building actions
- [act](https://github.com/nektos/act) - Run GitHub Actions locally
- [action-validator](https://github.com/mpalmer/action-validator) - Validate action.yml files

### Examples and Templates

- [TypeScript Action Template](https://github.com/actions/typescript-action)
- [JavaScript Action Template](https://github.com/actions/javascript-action)
- [Docker Action Template](https://github.com/actions/container-action)

## Contributing

Feel free to experiment, create examples, and document learnings in this repository. This is a learning space for understanding GitHub Actions development and marketplace publishing.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
