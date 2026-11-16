# SmartGreen

SmartGreen is a smart greenhouse project focused on monitoring and supporting greenhouse management through software, hardware, and AI-based components.

## Project Structure

```text
SmartGreenPolito/
├── .github/                # Branch flow checks, branch rulesets, PR template
├── greenhouse-controller/  # Hardware, sensors, and actuators (planned)
├── ai-model/               # AI model, training, and inference code (planned)
├── docs/                   # Project and team documentation
│   └── team-guidelines/    # Team workflow, conventions, and guidelines
├── tests/                  # Cross-component and integration tests (planned)
├── .gitignore
└── README.md
```

> Folders marked *(planned)* will be added as development progresses. The structure may evolve, and each component may include its own README with setup and usage instructions.

## Getting Started

1. Clone the repository and switch to the `dev` branch, where all work starts:

   ```bash
   git clone https://github.com/LucaFerrone3/SmartGreenPolito.git
   cd SmartGreenPolito
   git switch dev
   ```

2. Open the component you want to work on.

3. Follow the setup and execution instructions in that component's README, when available.

## Development Workflow

The software unit follows its own Agile approach, inspired by Scrum, with four-week sprints.

Before contributing to SmartGreen, please read the following documents to understand the team's organization, development process, and coding standards:

- [Onboarding Guide](docs/team-guidelines/onboarding.md) — Introduction to SmartGreen, its research projects, how the software unit is organized, roles, and tools.

- [How We Work](docs/team-guidelines/how-we-work.md) — Our Agile approach: roles, sprint events, backlog, user stories, and tasks.

- [Software Development Guidelines](docs/team-guidelines/software-development-guidelines.md) — Git branching strategy, commits, pull requests, code reviews, Definition of Done, testing, and collaboration standards.

## Documentation

Project documentation is maintained in the `docs/` directory.

- [Digital Twins for Greenhouses](docs/Digital_Twins_for_Greenhouses.pdf) — Project onboarding and architecture guide (hardware, data stack, and AI roadmap).
- `docs/team-guidelines/` — team processes, conventions, and collaboration rules

## Contributions

All team members are expected to:

- Follow the agreed coding and Git conventions.
- Keep their component's documentation up to date.
- Coordinate interface changes with the teams working on dependent components.
- Ensure that applicable Definition of Done criteria are met before marking a task as complete.
