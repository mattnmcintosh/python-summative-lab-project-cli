# Project Management Tool CLI

A modular, object-oriented Python command-line interface (CLI) application for managing users, projects, and tasks with local JSON data persistence and rich terminal output.

## Project Overview

This application provides an administrative system for managing development teams, tracking projects, and assigning tasks through structured CLI commands. It demonstrates a clean separation of concerns and object-oriented best practices across domain models, storage utilities, and presentation layers.

## Setup Instructions

1. Ensure Python 3.10 or higher is installed on your system.
2. Clone or download the project repository to your local machine.
3. Open your terminal and navigate to the project root directory.

## Dependency Installation Instructions

Install the required external packages (`rich` and `pytest`) using pip:

```bash
pip install rich pytest
```

Alternatively, if managing via Pipenv:

```bash
pipenv install rich
pipenv install --dev pytest
```

## How to Run the CLI

Execute commands from the project root directory by invoking the main script with Python:

```bash
python main.py [command] [options]
```

## Example Commands

### Add a User
```bash
python main.py add-user --name "Alex" --email "alex@example.com"
```

### List All Users
```bash
python main.py list-users
```

### Add a Project to a User
```bash
python main.py add-project --user "Alex" --title "CLI Tool" --description "Project tracker CLI" --due-date "2026-12-31"
```

### List Projects
```bash
python main.py list-projects --user "Alex"
```

### Add a Task to a Project
```bash
python main.py add-task --project "CLI Tool" --title "Implement add-task" --assigned-to "Alex"
```

### Complete a Task
```bash
python main.py complete-task --project "CLI Tool" --task-id 1
```

## Explanation of the File Structure

* `main.py`: CLI entry point handling argument parsing (`argparse`), subcommand routing, and rich tabular output.
* `lib/models/`: Contains core object-oriented domain classes:
  * `person.py`: Base class providing shared attributes and validation.
  * `user.py`: Manages user profiles and project collections (one-to-many relationship).
  * `project.py`: Manages project metadata and task collections (one-to-many relationship).
  * `task.py`: Tracks task assignment, status (`Pending`, `In Progress`, `Completed`), and unique identifiers.
* `lib/utils/`: Encapsulates file I/O operations (`storage.py`) for JSON serialization/deserialization.
* `data/`: Stores local persistence files (`project_tracker.json`).
* `testing/`: Houses the Pytest automated unit test suite.

## Overview of Features

* **Object-Oriented Design:** Utilizes class inheritance (`Person` -> `User`), encapsulation via `@property` setters with data validation, and class-level ID counters.
* **Rich Terminal Output:** Renders clean, colorized tables and status indicators using the `rich` library.
* **Local Data Persistence:** Automatically saves system state to JSON and gracefully recovers from missing or malformed data files.
* **Comprehensive Test Coverage:** Unit tests verifying model validations, storage handling, and CLI workflows.

## Known Issues or Limitations

* Data persistence is handled locally in a single JSON file; concurrent multi-process writes are not supported.