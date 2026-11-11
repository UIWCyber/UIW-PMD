# UIW-PMD — Project Management Dashboard

> One page to plan the work, follow the team, and see exactly where a project stands.

UIW-PMD is a lightweight project management dashboard built for student and small-team software projects. It pulls milestones, issues, sprints and commit activity from **GitHub** and **GitLab** and turns them into a timeline, a board, an activity feed and progress charts, all in a single browser page.

---

## Table of contents

- [Main goal](#main-goal)
- [What the dashboard is for](#what-the-dashboard-is-for)
- [Key advantages](#key-advantages)
- [The four views](#the-four-views)
- [How it works](#how-it-works)
- [Getting started](#getting-started)
- [Connecting GitHub or GitLab](#connecting-github-or-gitlab)
- [Setting up your issues](#setting-up-your-issues)
- [Tracking your progress](#tracking-your-progress)
- [Keyboard shortcuts](#keyboard-shortcuts)
- [Open design decisions](#open-design-decisions)
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
| **Zero install** | It is one HTML file, [`git_project-dashboard.html`](git_project-dashboard.html). Open it in any modern browser and you are working. |
| **User friendly** | Clean tabs, click-to-open issue details, resizable columns, and light or dark mode. |
| **Easy to navigate** | Four focused views, five outline levels, and filters by milestone or teammate. |
| **Progress at a glance** | Burndown, velocity and per-member charts update the moment an issue changes. |
| **Live activity** | A Recent activity panel shows what the team did in the last 24 hours or 3 days (commits with their files, comments, label and status changes, merges), refreshed every minute. |
| **Dependency aware** | Mark issues as blocked by other issues so bottlenecks are visible before they cause delays. |
| **Always up to date** | The dashboard is read-only and keeps no copy of your project: it shows exactly what is on GitHub or GitLab, and **Refresh** loads the latest. |

## The four views

### 1. Overview / Gantt
A timeline of every milestone, objective and issue, with start and due dates, story points and owners. Items follow one hierarchy: **Milestone → User Stories → Tasks / Issues → Sub-tasks / Sub-issues / Bugs**, with anything that has no type tagged **Untracked** and listed last. Each story is a parent row with its work nested and indented underneath, plus a done/total count (click the arrow to fold it).
- Zoom the timeline by **Month**, **Sprint** or **Week**.
- Pick an outline level: **Milestones**, **Objectives**, **User Stories** (each story's tasks folded), **Stories + Tasks** (only stories that have linked tasks) or **Everything**.
- Show or hide the date columns, and drag the edge of the name column to widen it (double-click the edge to fit the longest name).

### 2. Activity
- **Recent activity:** everything done in the project in the last **24 hours** or **3 days**, read live and refreshed every minute while the tab is open. Filter by member and by kind (commits, comments, changes, issues and merge/pull requests). Click a commit to see its files, branches and +/- lines.
- A contribution graph, daily commits by member, a contributor list and a searchable activity stream. Perfect for stand-ups and weekly check-ins.

### 3. Issues / Board
A board grouped by status. Each column shows its total story points, and every card shows its labels, assignee and due date. Filter by milestone, the current sprint or a teammate, and drag a column's edge to widen it.

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
        ▲                                                                       │
        └──────────────  Refresh / Recent activity (every minute)  ◄────────────┘
```

1. **Load.** A data source fetches milestones, objectives (epics), issues, sprints (iterations) and commits from your repository host and shapes them into plain objects.
2. **Render.** Every view is drawn from that one shared state, so the timeline, the board and the charts always agree with each other.
3. **Read-only.** Click any issue to see its details (status, assignee, story points, type, parent, sub-items, sprint, labels, blockers and history), with a link to open it on GitHub or GitLab. To change something, change it there; it shows up here on **Refresh**.
4. **Nothing is stored.** The dashboard keeps no copy of your project. Only the list of projects you connected, your view settings and encrypted tokens stay in the browser. **••• → Download data (JSON)** saves a snapshot if you need one.

The dashboard ships with a read-only demo project, **Sprout** (a fictional community-garden platform with plot booking and soil sensors), so you can explore every feature before connecting a real repository.

## Getting started

1. Clone the repository:
   ```bash
   git clone https://github.com/UIWCyber/UIW-PMD.git
   ```
2. Open [`git_project-dashboard.html`](git_project-dashboard.html) in Chrome, Edge, Firefox or Safari.
3. Explore the four tabs using the demo project.
4. When you are ready, open **•••** → **Connect a project…** to load your GitHub or GitLab project (below).

## Connecting GitHub or GitLab

No code changes needed. Click the **•••** menu (top right) → **Connect a project…**

1. **Project link:** paste the address of your repository from the browser, for example `https://github.com/owner/repo` or `https://gitlab.com/group/project`. The dashboard works out whether it is GitHub or GitLab (pick it by hand for a self-hosted GitLab with an unusual address).
2. **Sprint 1 starts on (optional):** the date your team's first 2-week sprint begins. Leave it empty to use GitLab iterations, or a 2-week calendar around the work.
3. **Access token:** a password made just for the dashboard that lets it *read* your project.
   - **Private projects need one.** Public GitHub repos work without one, but GitHub then allows only 60 requests an hour, so Recent activity only refreshes when you click **Refresh**.
   - Open **What's a token, and how do I get one?** in the popup for step-by-step instructions and a link straight to the right page.
   - GitHub: a fine-grained token with **Contents**, **Issues** and **Pull requests** set to *Read-only* (starts with `github_pat_`).
   - GitLab: a personal access token with only the **read_api** scope (starts with `glpat-`).
   - **Using a GitHub Project board?** To read its *Estimate* / *Story Points* field and its *Status* column, use a classic token with **repo** and **read:project**. For a project owned by an organization, a fine-grained token also works with **Organization permissions → Projects** set to *Read-only*.
4. Click **Connect**.

Every project you connect is listed under **Projects** in the same menu, so you can jump between projects (or back to the demo) in one click. **Refresh** in the top bar loads the latest data. Use **Edit** or **Remove** under *Saved projects* in the popup to change or forget a connection.

**Self-hosted GitLab on a private network** (for example over Tailscale) works too, including plain `http://` addresses: turn the network on first. The popup warns you that the token is sent unencrypted over http.

**How tokens are kept safe**

- **Encrypted:** tokens are stored encrypted (AES-GCM). The key is created in your browser and can't be read out or copied to another computer.
- **Expires automatically:** you choose how long the computer keeps it: *only until you close the tab*, 1, 7 (default) or 30 days. After that it is deleted and the dashboard asks for it again.
- **Shared or lab computers:** pick *Only until I close this tab*, and use **Forget all tokens on this computer** in the popup before you leave.
- **Never leaves your browser** except in requests to GitHub or GitLab. It is not in exported JSON, and the page can't load outside scripts.
- **Use a read-only token** (the popup's steps create one), so even a leaked token can't change your project. Never commit a token to the repository.

What the dashboard reads, and how it maps it:

| Dashboard item | GitHub | GitLab |
| --- | --- | --- |
| Milestones | Milestones | Milestones |
| Objectives | `objective::Name` label, otherwise one group per item type (User Stories, Issues, Tasks, Sub-tasks) | Epic or `objective::Name` label, otherwise grouped by type |
| Issues | Issues (assignee, labels, open/closed) | Issues (assignee, labels, weight, due date) |
| Item type | Issue type, title prefix or label (see [below](#setting-up-your-issues)) | Task type, title prefix or label |
| Parent / sub-items | Sub-issues, "Parent: #7" in the description, or a `- [ ] #12` task list in the parent | Child items (work-item hierarchy), "Parent: #7" or a task list |
| Story points | Project field *Estimate* / *Story Points*, an `sp: 5` label, or "Story points: 5" in the description. No default: unestimated items show **–** | Weight, an `sp: 5` label, or "Story points: 5" in the description |
| Status | Project *Status* column (with a token), or labels containing *ready*, *in progress* or *review*; closed = Done | Labels, e.g. `status::in progress`; closed = Done |
| Blocked by | "Blocked by #12" or "Depends on #12" in the description | Same |
| Sprints | *Sprint 1 starts on* date, otherwise a 2-week calendar around the work | *Sprint 1 starts on* date, otherwise iterations (Premium), otherwise a 2-week calendar |
| Activity | Commits, issues opened/closed, merged pull requests | Commits, issues opened/closed, merged merge requests |
| Recent activity (live) | Commits on every branch, comments, issue/PR timeline (labels, milestone, assignees, title, closed, merged), branches, releases, reviews | Commits on every branch, comments and system notes, label and milestone changes, the project event stream |

The dashboard never writes to GitHub or GitLab. Copies of projects saved by older versions of the dashboard are removed from the browser the first time this version opens; your project list and tokens are kept.

## Setting up your issues

The dashboard reads a few simple conventions. You don't need all of them, but the more your issues follow them, the more accurate the timeline and charts are.

**1. Say what kind of item it is.** Start the title with its type, or add a label with the same name:

| Type | Title examples | Label examples |
| --- | --- | --- |
| User Story | `User Story - Define project scope`, `Story: Export reports` | `story`, `user story` |
| Issue | `Issue - Integration compatibility` | `issue` |
| Bug | `Bug: Login fails`, `Defect - Report crashes` | `bug`, `defect` |
| Task | `Task: Produce requirements document` | `task` |
| Sub-task / sub-issue | `Sub-task: Draft interview questions`, `Sub-issue: …` | `sub-task`, `subtask`, `sub-issue` |

A GitHub issue type set in the repository wins over the title, and the title wins over labels. An Issue, or an item with no type, that has a `bug` label counts as a Bug; a Task with a `bug` label stays a Task. The prefix is hidden in the dashboard because the type shows as a tag.

**Where items appear on the timeline:**

| Item | Where it shows |
| --- | --- |
| User story | Its milestone → **User Stories**, as a parent row with everything linked to it nested underneath |
| Issue, task or sub-task linked to a story | Under that story (and under its parent task, for sub-tasks) |
| Issue or task in a milestone with stories, but not linked to one | Its milestone → **Not linked to a story**, so missing links are easy to spot |
| Issue or task in a milestone with no stories | Its milestone, grouped by type |
| Sub-task, sub-issue or bug linked to a task, issue or story | Under that parent, after its tasks and issues |
| Bug not linked to anything | Its milestone, with the other unlinked items, after tasks and issues |
| Item with no type | Tagged **Untracked**, in its milestone's **Untracked** group, listed last |
| Item with no milestone | **No milestone**, at the bottom, grouped the same way |

Inside every group and every story, items are listed in hierarchy order (tasks, issues, sub-tasks, bugs, untracked), then by start date. Bugs and untracked items count toward their milestone's progress like everything else. Change an item's type on GitHub or GitLab and it moves to its new group on the next **Refresh**.

**2. Link tasks to their story.** Use any one of these:

- GitHub **sub-issues** (in the issue sidebar: *Create sub-issue* or *Add existing issue*).
- A line in the task's description: `Parent: #7`, `Part of #7` or `Sub-task of #7`.
- A task list in the story's description: `- [ ] #12`.

A linked task appears under its story when both are in the same milestone. Otherwise it stays in its own group and shows **↳ #7**.

**3. Estimate in story points.** Use any one of these (first match wins):

- A number field named **Estimate** or **Story Points** on your GitHub Project board (needs the token above).
- A label: `sp: 5`, `story points: 5` or `5 SP`.
- A line in the description: `Story points: 5` or `Estimate: 5`. In the class issue template, replace `TBD` under **Estimation of effort** with a number.

On GitLab, the issue's weight is used first.

**How points are counted:**

- Each estimate counts **once**. If a story has an estimate, that covers its tasks, so their points aren't added again.
- If a story has no estimate, it shows the total of its tasks, in grey.
- Unestimated items show **–**. The *Story points done* card counts them, so you can see what still needs an estimate.
- "In a sprint" always means *due inside the sprint*. Every view uses the same totals.

**4. Mark blockers.** Write `Blocked by #12` or `Depends on #12` in the description.

## Tracking your progress

- **Daily:** check **Recent activity** to see what changed and the **Board** to see where every card stands.
- **Each sprint:** watch the **Burndown** line against the ideal line and compare **Velocity** with previous sprints.
- **Each milestone:** use the **Gantt** summary view to confirm every objective is on schedule, and look for blocked issues.
- **Team health:** review **Workload by member** so no one is overloaded and every contribution is visible.

## Keyboard shortcuts

| Shortcut | Action |
| --- | --- |
| `Esc` | Close a dialog |
| `Enter` | Connect, in the connect popup |

## Open design decisions

The next round of features, such as progress without story points, stale-work alerts, real sprint dates and full assignee credit, depends on choices the team still has to make. They are laid out as a decision tree in [`docs/HANDOFF-telemetry-decisions.md`](docs/HANDOFF-telemetry-decisions.md). Record the team's choices there; the next change builds only what is marked *Decided*.

## Contributors

- [@je1805](https://github.com/je1805)
- [@juniorandchill](https://github.com/juniorandchill)
- [@gdparra-edu](https://github.com/gdparra-edu)

## License

Released under the [MIT License](LICENSE).
