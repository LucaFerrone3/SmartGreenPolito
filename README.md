# SmartGreen

SmartGreen is a smart greenhouse project focused on monitoring and supporting greenhouse management through software, hardware, and AI-based components.

## Project Structure

```text
smartgreen/
├── greenhouse-controller/  # Hardware, sensors, and actuators
├── ai-model/               # AI model, training, and inference code
├── docs/                   # Project and team documentation
│   └── team-guidelines/    # Team workflow, conventions, and guidelines
├── tests/                  # Cross-component and integration tests
├── .gitignore
└── README.md
```

> The structure may evolve as the project develops. Each component may include its own README with setup and usage instructions.

## Getting Started

1. Clone the repository:

   ```bash
   git clone https://github.com/LucaFerrone3/SmartGreenPolito.git
   cd smartgreen
   ```

2. Open the component you want to work on ( `greenhouse-controller/`, `ai-model/`, `docs/` or `tests/`).

3. Follow the setup and execution instructions in that component's README, when available.

## Development Workflow

The team follows an Agile approach based on Scrum, with four-week sprints.

Before contributing to SmartGreen, please read the following documents to understand the team's organization, development process, and coding standards.

- [Onboarding Guide](onboarding_smartgreen.md) — Introduction to SmartGreen, its projects, organizational units, development approach, Scrum events, team roles, and tools.

- [Software Development Guidelines](SmartGreen_Software_Development_Guidelines.md) — Development workflow, Git branching strategy, commits, pull requests, code reviews, Definition of Done, testing, and collaboration standards.

## Documentation

Project documentation is maintained in the `docs/` directory.

- `docs/team-guidelines/` — team processes, conventions, and collaboration rules

## Contributions

All team members are expected to:

- Follow the agreed coding and Git conventions.
- Keep their component's documentation up to date.
- Coordinate interface changes with the teams working on dependent components.
- Ensure that applicable Definition of Done criteria are met before marking a task as complete.
