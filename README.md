# Contribution [#]: Workbench commit dialog: the "Commit" button stays greyed out (looks disabled) after typing a commit message
 

**Contribution Number:** 2

**Student:** Shuja Waraich

**Issue:** [[GitHub issue link]  ](https://github.com/future-agi/future-agi/issues/1384)

**Status:** Phase II

---

## Why I Chose This Issue

I chose this issue because it is a focused frontend bug in an AI-related open-source project, and it looks realistic for a first contribution. The issue is clearly described, labeled as a good first issue, and has a small scope with a specific affected file and suggested fix. It is also currently unassigned and has no linked branches or pull requests, which makes it a good candidate to work on without competing with an existing implementation.

This issue matches my learning goals because I want to practice contributing to a real codebase by making a small, reviewable change. Although the bug is frontend-focused, it still gives me experience reading unfamiliar project code, understanding component state, checking UI behavior, and submitting a clean pull request. I also like that the issue involves a real user experience problem: the button’s visual state does not match its actual enabled state, which can confuse users.

---

## Understanding the Issue

### Problem Description

In the Workbench prompt commit dialog, the outlined **Commit** button continues to look disabled after a user enters a commit message. The button becomes clickable, but its grey text color incorrectly suggests that it is still unavailable. This creates a confusing mismatch between the button's appearance and its actual state.

### Expected Behavior

The outlined **Commit** button should be greyed out and unclickable while the commit-message field is unchanged or while a commit request is pending. After the user enters a message, it should switch to the active primary outlined style and become clickable, matching the state change shown by the adjacent **Commit and set as a default version** button.

### Current Behavior

After the user types a commit message, the button's disabled state is removed and clicking it works. However, the button text remains grey because `color: "text.disabled"` is applied unconditionally. As a result, the enabled and disabled states look nearly identical.

### Affected Components

- `frontend/src/sections/workbench/createPrompt/promptActions/SaveAndCommit.jsx`
- The outlined **Commit** Material UI `LoadingButton` inside the component's `DialogActions`
- The button's `sx` color styling; its existing `isDirty` and `isPending` state logic is involved in determining behavior but does not need to be changed

---

## Reproduction Process

### Environment Setup

The Future AGI application can be run locally using its documented self-hosted Docker setup. Docker Desktop (or Docker Engine with Docker Compose) must be running first. I used the project's installer from the repository root:

```bash
git clone https://github.com/future-agi/future-agi.git
cd future-agi
./bin/install
```

After installation, the application is available at `http://localhost:3000`. The main setup requirement is ensuring Docker is installed and running before executing the installer. No additional workaround is required for this issue because it can be reproduced through the Workbench user interface once the application is running.

### Steps to Reproduce

1. Install and start Docker Desktop (or Docker Engine with Docker Compose).
2. Clone the project and enter its directory:
   ```bash
   git clone https://github.com/future-agi/future-agi.git
   cd future-agi
   ```
3. Start the self-hosted application:
   ```bash
   ./bin/install
   ```
4. Open `http://localhost:3000` in a browser and sign in or create an account if prompted.
5. Open **Workbench**, select **Prompt**, and open any existing prompt (or create and save one first).
6. Click **Commit** in the top bar to open the **Commit changes to prompt** dialog.
7. Before entering a message, confirm that the outlined **Commit** button is greyed out and cannot be clicked.
8. Type any text into the commit-message field, such as `Test commit`.
9. Observe that **Commit and set as a default version** changes to an active style, but the outlined **Commit** button still looks greyed out even though it is now clickable. This visual mismatch reproduces issue #1384.

### Reproduction Evidence

- **Branch in my fork:** [master](https://github.com/shuja-waraich-03/github-contribution-log2/tree/master)
- **Screenshots/logs:** [If applicable]
- **My findings:** The button's disabled logic changes correctly after the commit message is edited, but its hardcoded `color: "text.disabled"` styling keeps it visually grey in the enabled state.

---

## Solution Approach

### Analysis

[Your analysis of the root cause - what's causing the issue?]

### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

- Update the outlined **Commit** `LoadingButton` in `frontend/src/sections/workbench/createPrompt/promptActions/SaveAndCommit.jsx`.
- Remove the unconditional `color: "text.disabled"` value from its `sx` prop and set `color="primary"`, allowing Material UI to apply its normal enabled and disabled styles.
- Leave the existing `disabled={!isDirty || isPending}` logic unchanged because it already controls click behavior correctly.
- Manually verify the empty-message, entered-message, and pending-request states, and confirm that the outlined button's visual state matches the adjacent **Commit and set as a default version** button.
- Run the relevant frontend formatting, linting, and tests before submitting the change.

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
