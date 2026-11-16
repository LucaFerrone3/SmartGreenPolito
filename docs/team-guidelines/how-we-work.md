# How We Work

This guide explains how the SmartGreen software unit organizes its work. We follow our own Agile approach: it borrows several ideas from Scrum, but it is adapted to a student team. No prior knowledge is needed.

> Looking for the rules on Git branches, commits, pull requests, or the Definition of Done? See the [Software Development Guidelines](software-development-guidelines.md).

---

## 1. What is Agile?

**Agile** is a way of working that delivers value in **small, frequent pieces** instead of one big delivery at the end.

Think about building a car for a customer:

- **Traditional approach ("Waterfall"):** plan everything up front, build for a year, deliver the finished car. If the customer's needs changed in month three, we find out too late.
- **Agile approach:** first deliver a skateboard, then a scooter, then a bike, then a car. At every step the customer can use something, give feedback, and help us steer.

Agile is based on four core values (from the *Agile Manifesto*, 2001):

1. **People and interactions** over processes and tools
2. **Working results** over exhaustive documentation
3. **Collaboration with the customer** over rigid contracts
4. **Responding to change** over following a fixed plan

> **Key idea:** we don't try to predict everything in advance. We work in short cycles, check the results often, and adapt. This is called **inspect and adapt**.

---

## 2. Our Approach at a Glance

- We work in **four-week sprints**.
- The **Project Manager** keeps an ordered backlog of user stories in YouTrack.
- At the start of each sprint, user stories are assigned to the **five teams** of the software unit. Each team breaks its stories into tasks and decides who does what.
- Once a week we hold a short **Weekly Sync**. At the end of the sprint we **review** the results and hold a **retrospective** on how we worked.
- Work counts as finished only when it meets the **Definition of Done**.

---

## 3. Roles

People currently holding each role are listed in the [Onboarding Guide](onboarding.md#roles).

### Project Manager

Responsible for **what** the software unit works on and **in which order**.

- Writes the user stories and keeps the backlog ordered by priority in YouTrack
- Assigns user stories to the teams at Sprint Planning
- Decides whether urgent requests can enter a sprint that has already started
- Invites members of the research projects to the Sprint Review when the work concerns them

### Software Unit Lead

Responsible for **how well the unit works**. Think of a coach, not a boss.

- Facilitates the sprint events
- Helps the teams remove blockers and coordinates work that involves more than one team
- Decides when `dev` is released to `main`, and merges the release

### Teams

The software unit is divided into five teams: `team-1` to `team-5`. The same codes are used in branch names.

Teams are **self-organizing**: there is no team lead, and nobody assigns individual tasks from above. Each team:

- Breaks its user stories into tasks and agrees who owns each task, based on skills, availability, and mutual agreement
- Decides **how** to do the work
- Reviews pull requests, including those of other teams when a change affects them
- Raises blockers as soon as they appear

> The Project Manager and the Software Unit Lead are currently the same person. The two roles are described separately because they may be assigned to different people in the future.

---

## 4. The Sprint

A sprint lasts **four weeks**. A new sprint starts right after the previous one ends.

All events are **timeboxed**: they have a maximum duration, and we respect it.

| Event | When | Max duration | Who attends |
|---|---|---|---|
| Sprint Planning | First day of the sprint | ~4 hours | Whole software unit |
| Weekly Sync | Every week | 30 minutes | Whole software unit |
| Sprint Review | End of the sprint | ~2 hours | Whole software unit, plus guests when relevant |
| Sprint Retrospective | After the Sprint Review | ~1.5 hours | Whole software unit |

### Sprint Planning

1. The Project Manager presents the highest-priority user stories and assigns them to the teams.
2. Each team checks that its stories are clear and fit its members' availability. If they don't, the team discusses the scope with the Project Manager.
3. Each team breaks its stories into tasks in YouTrack and agrees who owns each one.

**Result:** every task in the sprint has an owner.

### Weekly Sync

Each team gives a short update:

1. What did we complete since the last sync?
2. What will we work on next?
3. Is anything blocking us?

The Weekly Sync is **not** the place to solve problems in detail: those discussions happen afterward, with only the people involved. Don't wait for the sync to raise a blocker; raise it as soon as it appears.

### Sprint Review

The teams **show what they completed** during the sprint, with a live demo whenever possible. Only work that meets the Definition of Done is presented.

The attendees depend on what is being presented. Some reviews involve only the software unit. When the work concerns one of the research projects (for example, a new dataset or a new greenhouse feature), the Project Manager also invites the members of that project who will use it.

The feedback is collected by the Project Manager, who updates the backlog. Unfinished stories go back to the backlog and are prioritized again.

### Sprint Retrospective

The unit reflects on **how it worked**, not on the product:

- What went well?
- What didn't go well?
- What will we try to improve in the next sprint?

The unit leaves with 1–3 concrete actions, and checks at the next retrospective whether they worked.

---

## 5. Backlog, User Stories, and Tasks

Everything is tracked in **YouTrack**.

### Backlog

An ordered list of **everything** that could be done: features, improvements, bug fixes, documentation. The most important items are at the top. It is never "finished": it evolves constantly.

The Project Manager writes and orders the backlog. If you have an idea or find a bug, report it to the Project Manager, who decides whether and where it goes in the backlog.

### User Stories

Backlog items are written as **user stories**:

> *As a* **[type of user]**, *I want* **[something]**, *so that* **[benefit]**.
>
> Example: *As a researcher on the SaS project, I want the greenhouse temperature and humidity readings exported as a daily CSV file, so that I can compare growing conditions across experiments.*

Each story includes **acceptance criteria**: the conditions that must be true for the story to be accepted. For the example above:

- Each reading includes the timestamp, sensor ID, value, and unit.
- Missing readings are marked explicitly, not silently skipped.

### Tasks

During Sprint Planning, each team breaks its stories into **tasks**. A task:

- Has exactly one owner
- Is small enough to be completed within the sprint, ideally in a few days
- Corresponds to exactly one Git branch (see the branch naming rules in the [Software Development Guidelines](software-development-guidelines.md#2-branching-strategy))

No task, no branch: if the work you need to do has no task, ask your team to create one in YouTrack first.

---

## 6. What a Sprint Delivers

At the end of each sprint, the teams should have work that is **finished and usable**: working code, firmware, a data pipeline, a dataset, or documentation.

Many greenhouse experiments last longer than one sprint. In that case, split the work into steps that can each be completed within a sprint, for example: sensor calibration, then the data collection script, then a first analysis of the collected data.

A piece of work is finished only when it meets the [Definition of Done](software-development-guidelines.md#6-definition-of-done). If it doesn't, it's **not done**, and it isn't presented at the Sprint Review.

---

## 7. Changes During a Sprint

New requests that arrive during a sprint go to the Project Manager, who adds them to the backlog for a future sprint.

If a request is truly urgent, the Project Manager decides, together with the team concerned, whether it enters the current sprint and which work leaves the sprint to make room for it.

---

## 8. How It All Fits Together

```text
      Backlog in YouTrack (ordered by the Project Manager)
                 │
                 ▼
      ┌──────── Sprint Planning ─────────┐
      │  stories assigned to the teams   │
      │  teams split them into tasks     │
      └──────────┬───────────────────────┘
                 ▼
      ┌──────── THE SPRINT (4 weeks) ─────────┐
      │  work on tasks + Weekly Sync (30 min) │
      └──────────┬────────────────────────────┘
                 ▼
      Completed stories (meet the DoD)
                 │
                 ▼
      Sprint Review  → feedback on the WORK
                 │
                 ▼
      Sprint Retrospective → improve the PROCESS
                 │
                 └──────► next sprint begins
```

---

## 9. What We Took from Scrum, and What We Changed

You may have heard of **Scrum**, the most popular Agile framework. Our approach is inspired by it but is **not** Scrum. If you know Scrum, this table shows the differences.

| In Scrum | In our approach |
|---|---|
| A **Product Owner** orders the backlog | The **Project Manager** writes and orders the backlog and assigns stories to the teams |
| A **Scrum Master** facilitates the events and removes impediments | The **Software Unit Lead** has a similar role |
| One team of up to ~10 people | **Five self-organizing teams** sharing one backlog and one `dev` branch |
| Sprints of 1–4 weeks, often 2 | Sprints of **4 weeks** |
| **Daily Scrum**, 15 minutes every day | **Weekly Sync**, 30 minutes every week |
| Each sprint has a **Sprint Goal** | **No Sprint Goal**: progress is measured by the user stories completed |
| Sprint Review, Retrospective, Definition of Done, timeboxes | **Same as Scrum** |

For further reading (optional), see the official [Scrum Guide](https://scrumguides.org/).

---

## 10. Common Mistakes to Avoid

- **Turning the Weekly Sync into a long problem-solving meeting.** Keep it to 30 minutes.
- **Waiting for the Weekly Sync to raise a blocker.** Raise it as soon as it appears.
- **Starting work without a YouTrack task.** No task, no branch.
- **Adding work mid-sprint without going through the Project Manager.**
- **Skipping the Retrospective** because "we're busy". It's how we stop repeating the same problems.
- **Calling work "done" when it isn't.** Respect the Definition of Done.
- **Using the number of completed tasks to judge individuals.** We succeed or fail as a unit.

---

*Questions? Ask the Software Unit Lead, or bring them to the next Weekly Sync.*
