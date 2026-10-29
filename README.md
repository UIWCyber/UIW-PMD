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
| **User friendly** | Clean tabs, inline editing, drag and drop, and light or dark mode that follows your system. |
| **Easy to navigate** | Four focused views, expand or collapse controls, and filters by milestone or teammate. |
| **Progress at a glance** | Burndown, velocity and per-member charts update the moment an issue changes. |
| **Accountability built in** | An "Acting as" selector records every edit in the activity log under the person who made it. |
| **Dependency aware** | Mark issues as blocked by other issues so bottlenecks are visible before they cause delays. |
| **Your data stays yours** | Work is saved in your browser and can be exported to or imported from JSON at any time. |

## The four views

### 1. Overview / Gantt
A timeline of every milestone, objective and issue, with start and due dates, story points and owners. Items follow one hierarchy: **Milestone → User Stories → Tasks / Issues → Sub-tasks / Sub-issues / Bugs**, with anything that has no type tagged **Untracked** and listed last. Each story is a parent row with its work nested and indented underneath, plus a done/total count (click the arrow to fold it).
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
3. **Edit.** Click any title, date or field to edit it inline, or open the full issue editor for assignee, status, story points, type, parent, milestone, sprint, labels and blockers.
4. **Save.** Changes are kept in your browser (press **Ctrl+S**) and can be exported as JSON to share with teammates or keep as a backup.

The dashboard ships with realistic mock data for a sample project so you can explore every feature before connecting a real repository.

## Getting started

1. Clone the repository:
   ```bash
   git clone https://github.com/UIWCyber/UIW-PMD.git
   ```
2. Open [`git_project-dashboard.html`](git_project-dashboard.html) in Chrome, Edge, Firefox or Safari.
3. Pick your name in **Acting as**, then explore the four tabs using the mock data.
4. When you are ready, open **•••** → **Connect a project…** to load your GitHub or GitLab project (below).

## Connecting GitHub or GitLab

No code changes needed. Click the **•••** menu (top right) → **Connect a project…**

1. **Project link:** paste the address of your repository from the browser, for example `https://github.com/owner/repo` or `https://gitlab.com/group/project`. The dashboard works out whether it is GitHub or GitLab (pick it by hand for a self-hosted GitLab with an unusual address).
2. **Access token:** a password made just for the dashboard that lets it *read* your project.
   - **Private projects need one.** Public GitHub repos work without one, but GitHub then allows only 60 requests an hour.
   - Open **What's a token, and how do I get one?** in the popup for step-by-step instructions and a link straight to the right page.
   - GitHub: a fine-grained token with **Contents**, **Issues** and **Pull requests** set to *Read-only* (starts with `github_pat_`).
   - GitLab: a personal access token with only the **read_api** scope (starts with `glpat-`).
   - **Using a GitHub Project board?** To read its *Estimate* / *Story Points* field and its *Status* column, use a classic token with **repo** and **read:project**. For a project owned by an organization, a fine-grained token also works with **Organization permissions → Projects** set to *Read-only*.
3. Click **Connect**.

Every project you connect is listed under **Recent projects** in the same menu, so you can jump between projects (or back to the demo) in one click. Each project keeps its own saved copy in your browser, and **Reload from GitHub/GitLab** in the menu pulls the latest data. Use **Edit** or **Remove** under *Saved projects* in the popup to change or forget a connection.

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
| Parent / sub-items | Sub-issues, "Parent: #7" in the description, or a `- [ ] #12` task list in the parent | "Parent: #7" or a task list |
| Story points | Project field *Estimate* / *Story Points*, an `sp: 5` label, or "Story points: 5" in the description. No default: unestimated items show **–** | Weight, an `sp: 5` label, or "Story points: 5" in the description |
| Status | Project *Status* column (with a token), or labels containing *ready*, *in progress* or *review*; closed = Done | Labels, e.g. `status::in progress`; closed = Done |
| Blocked by | "Blocked by #12" or "Depends on #12" in the description | Same |
| Sprints | 2-week calendar around the work | Iterations (Premium), otherwise a 2-week calendar |
| Activity | Commits, issues opened/closed, merged pull requests | Commits, issues opened/closed, merged merge requests |

Edits made in the dashboard stay in your browser; they are not written back to GitHub or GitLab.

After updating the dashboard file, use **•••** → **Reload from GitHub/GitLab** once. Copies saved by an older version keep the old layout, and the status line tells you so.

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

Inside every group and every story, items are listed in hierarchy order (tasks, issues, sub-tasks, bugs, untracked), then by start date. Bugs and untracked items count toward their milestone's progress like everything else. Changing an item's type in the issue form moves it to the group a reload would put it in.

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
- Milestone and group progress (the % on the timeline bars) uses story points only when every item in the group has an estimate. Otherwise it uses issues closed across all items, tracked or untracked, so a milestone where everything is done always shows 100%. Hover a bar to see which was used.
- "In a sprint" always means *due inside the sprint*. Every view uses the same totals.

**4. Mark blockers.** Write `Blocked by #12` or `Depends on #12` in the description.

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

## Open design decisions

The next round of features, such as progress without story points, stale-work alerts, real sprint dates and full assignee credit, depends on choices the team still has to make. They are laid out as a decision tree in [`docs/HANDOFF-telemetry-decisions.md`](docs/HANDOFF-telemetry-decisions.md). Record the team's choices there; the next change builds only what is marked *Decided*.

## Contributors

- [@je1805](https://github.com/je1805)
- [@juniorandchill](https://github.com/juniorandchill)
- [@gdparra-edu](https://github.com/gdparra-edu)

## License

Released under the [MIT License](LICENSE).
