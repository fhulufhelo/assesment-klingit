# Klingit Task Management System — Build Brief

You are a senior software engineer. Build a working task management application — data layer, backend API, and a basic UI — using the data model specified in [`data-model.md`](./data-model.md) as your single source of truth.

## System Overview

A task management system for an organisation with two roles: **project managers** and **team members**. Project managers create and oversee work; team members are assigned tasks and report time against them.

| Entity | Purpose |
|---|---|
| `User` | Person in the organisation; role is `project_manager` or `team_member` |
| `Project` | Container for tasks; created and owned by a project manager |
| `Task` | Core work item; assigned to one team member at a time; has a status lifecycle, date range, and time allocation |
| `TaskAllocationHistory` | Append-only audit log of hour-allocation events (original allocation and extensions) |
| `TimeEntry` | A single instance of an assignee reporting hours worked against a task |

## What to Build

- Implement all five entities with every attribute, constraint, and validation defined in `data-model.md`
- Enforce all role-based access rules (project managers vs. team members) at every write
- Enforce the full Task status transition graph exactly as specified — no undocumented transitions
- Expose create, read, update, and soft-delete operations for each entity
- Support the five reporting query patterns defined in the data model
- Build a basic UI sufficient to exercise the complete workflow: create a project, create and assign a task, log time, approve a time extension, view over-budget tasks

## Hard Constraints

- The data model is intentionally language-neutral — choose any stack, but do not deviate from the entity structure, types, or business rules as written
- `TaskAllocationHistory` is fully immutable — no updates or deletes on that table, ever
- All datetimes are UTC
- All active-record queries must filter `deleted_at IS NULL`
- If a rule is not in `data-model.md`, do not invent it

## Data Model Reference

**[`data-model.md`](./data-model.md)** is the authoritative spec. It contains:

- Entity definitions with language-neutral attribute types and constraints
- Cardinality and relationship table
- Exhaustive business rules and validation logic
- Mermaid ER diagram
- Five reporting query patterns
- Design rationale and trade-off notes
