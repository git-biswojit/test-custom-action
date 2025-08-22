# Test Custom Action

A repository for testing and learning how to create custom GitHub Actions and publish them to the GitHub Marketplace.

## Overview

This project serves as a sandbox for experimenting with different types of GitHub Actions:

- JavaScript/TypeScript Actions
- Docker Actions
- Composite Actions

## Using the Hello Echo Action

This repository includes a ready-to-use GitHub Action that echoes customizable messages. Perfect for learning GitHub Actions or as a simple greeting action in your workflows.

### Quick Start

```yaml
# Basic usage with defaults
- name: Say hello
  uses: git-biswojit/test-custom-action@main

# Custom message and name
- name: Custom greeting
  uses: git-biswojit/test-custom-action@main
  with:
    message: "Good morning"
    name: "GitHub Actions"

# Using outputs in subsequent steps
- name: Greet and capture outputs
  id: greeting
  uses: git-biswojit/test-custom-action@main
  with:
    message: "Welcome"
    name: "Developer"

- name: Use the outputs
  run: |
    echo "Full message: ${{ steps.greeting.outputs.full-message }}"
    echo "Timestamp: ${{ steps.greeting.outputs.timestamp }}"
```

### Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `message` | The message to echo | No | `"hello"` |
| `name` | Name to greet | No | `"World"` |

### Outputs

| Output | Description | Example |
|--------|-------------|---------|
| `timestamp` | ISO 8601 timestamp when the action ran | `"2024-01-15T14:30:25Z"` |
| `full-message` | The complete constructed message | `"hello, World!"` |

### Examples

#### Example 1: Default greeting

```yaml
- uses: git-biswojit/test-custom-action@main
```

**Output:** `"hello, World!"`

#### Example 2: Custom message

```yaml
- uses: git-biswojit/test-custom-action@main
  with:
    message: "Good afternoon"
```

**Output:** `"Good afternoon, World!"`

#### Example 3: Custom message and name

```yaml
- uses: git-biswojit/test-custom-action@main
  with:
    message: "Happy coding"
    name: "Developer"
```

**Output:** `"Happy coding, Developer!"`

#### Example 4: Using outputs in a workflow

```yaml
name: Greeting Workflow
on: [push]

jobs:
  greet:
    runs-on: ubuntu-latest
    steps:
      - name: Generate greeting
        id: hello
        uses: git-biswojit/test-custom-action@main
        with:
          message: "Welcome to our repository"
          name: "Contributor"

      - name: Display results
        run: |
          echo "Message: ${{ steps.hello.outputs.full-message }}"
          echo "Generated at: ${{ steps.hello.outputs.timestamp }}"

      - name: Create issue comment (example)
        run: |
          echo "Creating comment: ${{ steps.hello.outputs.full-message }}"
          # You could use this output to create comments, notifications, etc.
```
