---
title: "Boost Your Python Testing Workflow with the Pytest Runner VS Code Extension"
slug: "boost-your-python-testing-workflow-with-the-pytest-runner-vs-code-extension"
date: 2024-12-09T12:52:43+01:00
draft: false
categories: ["Python", "Testing"]
tags: ["python", "test", "pytest"]
image: "cover.png"
socialShareLink: true
shareButtons: true
---

Are you tired of jumping through hoops to run Python tests, especially in complex environments like Docker? Meet the **Pytest Runner**, a Visual Studio Code extension designed to make running Python tests a breeze. Whether you’re executing single tests, modules, or working with local and containerized setups, Pytest Runner streamlines your workflow for a faster, more intuitive testing experience.

## Install Pytest Runner Plugin  

Getting started with **Pytest Runner** is easy! Install the plugin directly from the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=pamaron.pytest-runner). Click the link to install it instantly. Once installed, you’ll be ready to run Python tests effortlessly with just a few clicks or commands. Wanna know more? **Continue reading 👇**

## 🚀 Why Pytest Runner?

Modern testing can feel cumbersome. Take my job as an example: most tests run in a Docker-based architecture, requiring me to manage remote interpreters and lengthy pytest identifiers like `test_module.py::test_function`. This process wasn’t just slow—it was frustrating. I created Pytest Runner to simplify testing, inspired by tools like [pytest-vim](https://vimawesome.com/plugin/pytest-vim).  

This extension focuses on one goal: reducing friction in Python testing. With Pytest Runner, you can focus on writing great code while the extension handles the grunt work.  

## 🌟 Features  

- **Run tests locally or in Docker**: Execute individual tests or entire test modules effortlessly, using either local environments or Dockerized setups.  
- **Configuration checks**: Optional inspection of `setup.cfg` or `pyproject.toml` files ensures your test files follow your project's conventions.  
- **Customizable settings**: Tailor pytest commands, options, and configurations to fit your unique workflow.  

## 📋 Configuration Check: An Extra Layer of Validation  

Pytest Runner checks your project’s configuration files when enabled. For example, given a `pyproject.toml`:  

```toml
[tool.pytest.ini_options]
python_classes = ["Test", "Describe"]
python_functions = ["test_", "it_", "and_", "but_", "they_"]
python_files = ["test_*.py"]
testpaths = ["tests"]
```

or a `setup.cfg` file like:

```ini
[tool:pytest]
python_classes = Test Describe
python_files = test_*.py
python_functions = test_ it_ they_ but_ and_it_
testpaths =
    tests
```

If a test function doesn’t follow these naming conventions, Pytest Runner will halt and notify you with an error message.

## 🛠️ Requirements

- Pytest: The only hard requirement.
- Currently tested on macOS and Linux.

## 🎯 Usage

### Commands

- Run Test: Execute a single test locally.
- Run Test Docker: Execute a single test in Docker.
- Run Test Module: Run all tests in the current file locally.
- Run Test Module Docker: Run all tests in the current file via Docker.
- Access these commands via the VSCode command palette (⇧⌘P or Ctrl+⇧P) or use the custom buttons in the status bar.

Access these commands via the VSCode command palette `(⇧⌘P or Ctrl+⇧P)` or use the custom buttons in the status bar.

## ▶️ Running Tests

Place your cursor within a test function or class to execute it directly.
Alternatively, select the test name or a portion of it and run the desired command.
For module-level tests, use the appropriate command regardless of cursor location.

💡 Pro Tip: Create keyboard shortcuts for frequently used commands to save time!

## ⌨️ Keybindings

Define shortcuts for a more productive workflow:

```json
{
  "key": "ctrl+alt+1",
  "command": "pytest-runner.run-test"
},
{
  "key": "ctrl+alt+2",
  "command": "pytest-runner.run-module-test"
}
```

Run single tests with Ctrl+Alt+1 and module tests with Ctrl+Alt+2 (or any combination you prefer).

## Install Pytest Runner

[💾 Install pytest runner](vscode:extension/pamaron.pytest-runner)