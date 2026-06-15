# Contribution [1]: [Wynntils shows "ghost queues" for territories with similar names]

**Contribution Number:** [1]
**Student:** [Sarah Nasser]  
**Issue:** [https://github.com/Wynntils/Wynntils/issues/3180]  
**Status:** [Phase I] [Complete]

---

## Why I Chose This Issue

This issue interests me because Wynntils is a Wynncraft Mod that gamers can play. I find it very cool to contribute to a video game that is played by many people. I cannot wait to learn more about Wynntils, fix this issue, and improve gameplay. This issue also matches my skills and requires knowledge of Java and Shell. I am skilled in Java, and I will be able to learn Shell within a few days. There are also clear instructions in this project's README.md on how to access Wynntils and set up the code environment, and a Discord chat is also available if I have any questions while working on this issue within the next few weeks. This issue is also bounded and specific, and no one has claimed it. There are no open pull requests already solving it, and there is one comment that provided hints and insight on the issue. When contributing to this issue, I hope to learn Shell, gain experience in setting up a code environment, and practice using the codebase and Claude Code to understand which section of the code may be resulting in the issue and how I can approach the issue.

---

## Understanding the Issue

### Problem Description

Numerous issues occur when using OpenBLAS to implement Singular Value Decomposition (SVD) across different systems.

### Expected Behavior

I should implement SVD in Rust without using openblas-src as a dependency.

### Current Behavior

The package depends on OpenBLAS to compute SVD for the Optimized Product Quantization (OPQ) indexing process. This dependency results in many issues when building OpenBLAS in different systems.

### Affected Components

None of the files in the codebase contain an attempted SVD implementation. It seems that the attempted SVD implementation that depends on OpenBLAS has been removed, so I will need to create a file in the codebase in which I compute SVD in Rust without using openblas-src as a dependency.

## Reproduction Process

### Environment Setup

[Notes on setting up your local development environment - challenges you faced, how you solved them]

### Steps to Reproduce

It seems that the attempted SVD implementation that depends on OpenBLAS has been removed, so I may need to create in Rust a SVD implementation from scratch that does not depend on OpenBLAS. Therefore, I will be creating a new feature from scratch and there is no existing bug for me to trigger. However, I know from the issue description that building OpenBLAS in different systems and using it as a dependency when implementing SVD will cause problems. However, because there is no issue for me to visually reproduce and the issue description or comments do not specify what exactly these problems are, I do not know what these problems are. I will simply implement SVD in Rust without depending on OpenBLAS so I can minimize problems that occur across different systems.

### Reproduction Evidence

- **Commit showing reproduction:** [Link to commit in your fork]
- **Screenshots/logs:** [If applicable]
- **My findings:** [What you discovered during reproduction]

---

## Solution Approach

### Analysis

Using OpenBLAS as a dependency in SVD implementation results in problems in different systems. However, due to limited information from the issue description on what these problems are or why depending on OpenBLAS causes them, I cannot give a more specific analysis of the root cause.

### Proposed Solution

Despite limited information (see my analysis of the root cause for the issue) in the issue statement, I believe I can solve this issue by simply implementing SVD in Rust without depending on OpenBLAS. First, I will Google search and learn about the SVD algorithm. A commenter gave the link to a possible SVD implementation that can be used. This link does not work, so I will later check whether there is some other way I can access the link. If I cannot access this link, I will simply use a different website on the SVD algorithm. This same commenter does not have a strong opinion on how to implement SVD. Even though this commenter is not sure whether a different SVD implementation will cause major differences in output, they approved of a different commenter's suggestion to write a pure-Rust implementation, so the second step in my approach will be learn Rust through Claude Code and ask it for strategies and tips on implementing SVD solely using Rust without using OpenBLAS as a dependency.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** [Restate the problem]

**Match:** [What similar patterns/solutions exist in the codebase?]

**Plan:** [Step-by-step implementation plan]
1. [Modify file X to do Y]
2. [Add function Z]
3. [Update tests]

**Implement:** [Link to your branch/commits as you work]

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** [How will you verify it works?]

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
