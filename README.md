# UIW-PMD — Project Management Dashboard

> One page to plan the work, follow the team, and see exactly where a project stands.

UIW-PMD is a lightweight project management dashboard built for student and small-team software projects at the University of the Incarnate Word. It pulls milestones, issues, sprints and commit activity from **GitHub** and **GitLab** and turns them into a timeline, a board, an activity feed and progress charts, all in a single browser page.

---

## Table of contents

- [Main goal](#main-goal)
- [What the dashboard is for](#what-the-dashboard-is-for)
- [Key advantages](#key-advantages)
- [The four views](#the-four-views)
- [How it works](#how-it-works)
- [Getting started](#getting-started)
- [Connecting GitHub or GitLab](#connecting-github-or-gitlab)
- [Tracking your progress](#tracking-your-progress)
- [Keyboard shortcuts](#keyboard-shortcuts)
- [Contributors](#contributors)
- [License](#license)

---

## Main goal

Give every team member a clear, honest picture of the project in seconds:

- **What** needs to be done (milestones, objectives and issues)
- **Who** is doing it (assignees and workload)
- **When** it is due (sprints and the Gantt timeline)
- **How far along** the team is (burndown, velocity and contributions)

No digging through repository tabs, no spreadsheets to keep in sync, and no setup sessions before anyone can use it.

## What the dashboard is for

Repository hosts are great at storing code and issues, but they make it hard to see the big picture. UIW-PMD sits on top of your GitHub or GitLab project and answers the questions teams and instructors ask every week:

- Are we on track for the next milestone?
- Which issues are blocked, and by what?
- Is the work spread fairly across the team?
- What changed since the last stand-up?

It works for a semester capstone, a class project, a club app or any small team that plans in sprints.

## Key advantages

| Advantage | What it means for you |
| --- | --- |
| **Pulls from GitHub and GitLab** | Your existing milestones, issues and commits show up automatically. No double entry. |
| **Zero install** | It is one HTML file. Open it in any modern browser and you are working. |
| **User friendly** | Clean tabs, inline editing, drag and drop, and light or dark mode that follows your system. |
| **Easy to navigate** | Four focused views, expand or collapse controls, and filters by milestone or teammate. |
| **Progress at a glance** | Burndown, velocity and per-member charts update the moment an issue changes. |
| **Accountability built in** | An "Acting as" selector records every edit in the activity log under the person who made it. |
| **Dependency aware** | Mark issues as blocked by other issues so bottlenecks are visible before they cause delays. |
| **Your data stays yours** | Work is saved in your browser and can be exported to or imported from JSON at any time. |

## The four views

### 1. Overview / Gantt
A timeline of every milestone, objective and issue, with start and due dates, story points and owners.
- Zoom the timeline by **Month**, **Sprint** or **Week**.
- Switch between **Summary view**, **Collapse all** and **Expand all** to go from the big picture to the details.
- Show or hide date columns, add milestones and objectives in place, and spot deadlines that were extended.

### 2. Activity
A live stream of what the team did: commits, issue updates and edits, each stamped with who and when. Perfect for stand-ups and weekly check-ins.

### 3. Issues / Board
A drag-and-drop board grouped by status. Each column shows its total story points, and every card shows its labels, assignee and due date. Filter by milestone or by teammate to focus on what matters to you.

### 4. Analytics
Charts that show progress without any extra work:
- **Burndown** for the current sprint or milestone
- **Velocity** per sprint
- **Issue status** breakdown
- **Workload by member** and **member contributions** in story points
- **Daily commits by member** and top **contributors**

## How it works

```
 GitHub / GitLab API  ──►  Data source  ──►  Dashboard state  ──►  Gantt · Activity · Board · Analytics
                                                   │
                                                   └──►  Browser storage  ·  JSON export / import
```

1. **Load.** A data source fetches milestones, objectives (epics), issues, sprints (iterations) and commits from your repository host and shapes them into plain objects.
2. **Render.** Every view is drawn from that one shared state, so the timeline, the board and the charts always agree with each other.
3. **Edit.** Click any title, date or field to edit it inline, or open the full issue editor for assignee, status, story points, milestone, sprint, labels and blockers.
4. **Save.** Changes are kept in your browser (press **Ctrl+S**) and can be exported as JSON to share with teammates or keep as a backup.

The dashboard ships with realistic mock data for a sample project so you can explore every feature before connecting a real repository.

## Getting started

1. Clone the repository:
   ```bash
   git clone https://github.com/UIWCyber/UIW-PMD.git
   ```
2. Open the dashboard HTML file in Chrome, Edge, Firefox or Safari.
3. Pick your name in **Acting as**, then explore the four tabs using the mock data.
4. When you are ready, connect your GitHub or GitLab project (below) or use **Reset to mock data** to start over.

## Connecting GitHub or GitLab

The dashboard reads from your repository host through a small configuration block at the top of the script:

```js
const GITLAB = {
  enabled: false,
  baseUrl: "https://gitlab.example.edu/api/v4",
  projectId: null,
  groupId: null,
  token: ""
};
```

| Dashboard item | GitLab endpoint | GitHub equivalent |
| --- | --- | --- |
| Milestones | `GET /projects/:id/milestones` | `GET /repos/:owner/:repo/milestones` |
| Objectives | `GET /groups/:gid/epics` | Labels or project fields |
| Issues | `GET /projects/:id/issues` | `GET /repos/:owner/:repo/issues` |
| Sprints | `GET /groups/:gid/iterations` | Project iteration fields |
| Commits | `GET /projects/:id/repository/commits` | `GET /repos/:owner/:repo/commits` |

Set `enabled: true`, fill in your project details and a read-only personal access token, and reload the page. Never commit a real token to the repository.

## Tracking your progress

- **Daily:** check **Activity** to see what changed and **Board** to move your own cards.
- **Each sprint:** watch the **Burndown** line against the ideal line and compare **Velocity** with previous sprints.
- **Each milestone:** use the **Gantt** summary view to confirm every objective is on schedule, and look for blocked issues.
- **Team health:** review **Workload by member** so no one is overloaded and every contribution is visible.

## Keyboard shortcuts

| Shortcut | Action |
| --- | --- |
| `Ctrl+S` / `Cmd+S` | Save to this browser |
| `Enter` | Confirm an inline edit |
| `Esc` | Cancel an edit or close a dialog |

## Contributors

- [@je1805](https://github.com/je1805)
- [@juniorandchill](https://github.com/juniorandchill)
- [@gdparra-edu](https://github.com/gdparra-edu)

## License

Released under the [MIT License](LICENSE).
