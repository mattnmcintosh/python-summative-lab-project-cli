Project Management Tool CLI
A modular, object-oriented Python command-line interface (CLI) application for managing users, projects, and tasks with local JSON data persistence and rich terminal output.

Architecture & Design
This application demonstrates a clean separation of concerns and object-oriented best practices, organized into distinct layers:

CLI Entry Point (main.py): Handles command-line argument parsing (argparse), subcommands routing, and displays formatted tabular data using the rich library.

Domain Models (lib/models/):

Person: Base class handling common attributes and validation (name, email).

User: Inherits from Person and manages a collection of projects (one-to-many relationship).

Project: Manages titles, descriptions, due dates, and a collection of tasks (one-to-many relationship).

Task: Tracks task status (Pending, In Progress, Completed), task assignment, and unique identifiers.

Storage Utility (lib/utils/storage.py): Encapsulates file I/O operations, safely serializing and deserializing domain objects to and from local JSON storage.

Key Features
Object-Oriented Programming: Utilizes inheritance (Person -> User), @property decorators with setter validation, and class-level ID counters.

Rich CLI Formatting: Clean, colorized tables and status indicators for users and projects.

Data Persistence: Automatically saves all changes to data/project_tracker.json.

Comprehensive Validation: Validates email formats, non-empty names, and restricted task statuses.

Prerequisites & Installation
Ensure Python 3.10+ is installed.

Install the required dependencies by running:
pip install rich pytest

Usage & Command Reference
Run commands from the project root directory using Python:

Add a User
python main.py add-user --name "Alex" --email "alex@example.com"

List All Users
python main.py list-users

Add a Project to a User
python main.py add-project --user "Alex" --title "CLI Tool" --description "Project tracker CLI" --due-date "2026-12-31"

List Projects
python main.py list-projects --user "Alex"

Add a Task to a Project
python main.py add-task --project "CLI Tool" --title "Implement add-task" --assigned-to "Alex"

Complete a Task
python main.py complete-task --project "CLI Tool" --task-id 1

Running Tests
Execute the unit test suite using pytest