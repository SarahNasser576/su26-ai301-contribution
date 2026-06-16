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

When computing SVD for the Optimized Product Quantization (OPQ) indexing process, many issues occur in building and using OpenBLAS as a dependency in different systems.

### Affected Components

None of the files in the codebase contain an attempted SVD implementation. It seems that the attempted SVD implementation that depends on OpenBLAS has been removed, so I will need to create a new file named svd.rs in the directory rust/lance-linalg/src/. In this new file, I will compute SVD using Rust and without using openblas-src as a dependency.

## Reproduction Process

### Environment Setup

To set up my local development environment, I installed VS Code, Rust, Python version 3.9+, Pylance, protocol buffers, commit hooks, and the Dev Containers extension. Installing VS Code, Rust, Python version 3.9+, and Pylance was easy and straightforward, and to install both these languages, I simply used the links the maintainer provided for the development environment. Links were also provided for installing protocol buffers, commit hooks, and the Dev Containers extension, but I still struggled with installing these three tools because the instructions were more confusing and I have never installed them before for a previous project. To understand how to install commit hooks, protocol buffers, and the Dev Containers extension, I discussed installation errors I got in the terminal with Claude Code and asked it how to resolve these errors.

### Steps to Reproduce

It seems that the attempted SVD implementation that depends on OpenBLAS has been removed, so I may need to create in Rust a SVD implementation from scratch that does not depend on OpenBLAS. Therefore, I will be creating a new feature from scratch and there is no existing bug for me to trigger. However, I know from the issue description that building OpenBLAS in different systems and using it as a dependency when implementing SVD will cause problems. However, because there is no issue for me to reproduce and the issue description or comments do not specify what exactly these problems are, I do not know what these problems are. I will simply implement SVD in Rust without depending on OpenBLAS so I can minimize problems that occur across different systems.

### Reproduction Evidence

- **Commit showing reproduction:** https://github.com/SarahNasser576/lance/commit/1983fc90fe32b4ef3ff2881761ca363a3839ff3b
- **Screenshots/logs:** N/A
- **My findings:** The attempted SVD implementation that depends on OpenBLAS has been removed and neither the post nor the commentds state which specific problems depending on OpenBLAS causes. Thus, I discovered that there is no issue for me to reproduce. I will be creating a SVD implementation from scratch in Rust without depending on OpenBLAS, explaining why my commit "showing reproduction" is simply a commit depicting that I created a new empty file named svd.rs in the directory rust/lance-linalg/src/. In this new file, I will be coding my SVD implementation.

---

## Solution Approach

### Analysis

Using OpenBLAS as a dependency in SVD implementation results in problems in different systems. However, due to limited information from the issue description on what these problems are or why depending on OpenBLAS causes them, I cannot give a more specific analysis of the root cause.

### Proposed Solution

Despite limited information (see my analysis of the root cause for the issue) in the issue statement, I believe I can solve this issue by simply implementing SVD in Rust without depending on OpenBLAS. First, I will Google search and learn about the SVD algorithm. Next, I will implement all steps in the SVD algorithm in Rust without using OpenBLAS as a dependency.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** When computing SVD for the Optimized Product Quantization (OPQ) indexing process, many issues occur in building and using OpenBLAS as a dependency in different systems. I should implement SVD in Rust without using OpenBLAS as a dependency.

**Match:** The file rust/lance-index/src/vector/bq/builder.rs have a few functions that are similar to my issue. These functions are:
- householder_qr(), which performs a QR decomposition of matrices using only Rust, is relevant to SVD because QR decomposition is one of the building blocks used in iterative SVD algorithms.
- random_orthogonal(), which uses the QR decomposition to generate orthogonal matrices, is relevant to SVD because the two output matrices from SVD are orthogonal matrices. Unlike random_orthogonal(), the SVD implementation should produce the two output matrices from the input and not randomly.

Code from householder_qr() that does something similar to what I need (My SVD implementation will use a very similar bidiagonalization step as the one shown by this code from householder_qr()):
let sign = if x[0] >= 0.0 { 1.0 } else { -1.0 };
        x[0] += sign * x_norm;
        let u = &x / x.dot(&x).sqrt();

and

let h = ndarray::Array2::eye(m - k) - 2.0 * u_outer;

Code from random_orthogonal() that does something similar to what I need (Q here is an orthogonal matrix, and my SVD implementation will decompose a matrix into three matrices, which includes an orthogonal matrix and the transpose of a different orthogonal matrix):
let (q, _) = householder_qr(a);

**Plan:**
1. Google search and learn about the SVD algorithm
2. Implement all steps in the SVD algorithm using Rust and without using OpenBLAS as a dependency

**Implement:** Link to my branch/commits as I work: https://github.com/SarahNasser576/lance/commits/fix-issue-SVDImplementation

**Review:** I should include corresponding tests in my pull request. Code without tests will not be merged.

**Evaluate:** I will Google search practice problems and solutions where the SVD algorithm used in my code is performed on matrices. I will compare these solutions to my program's output. This project does not require automated testing.

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
