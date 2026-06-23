# Contribution [1]: [Make a SVD implementation in Rust and remove the dependency of openblas]

**Contribution Number:** [1]
**Student:** [Sarah Nasser]  
**Issue:** [https://github.com/lance-format/lance/issues/984]  
**Status:** [Phase 2] [Complete]

---

## Why I Chose This Issue

I chose this issue because I am interested in Linear Algebra and its real-world applications. This issue requires knowledge of Rust, HTML, and Python. I know Python and HTML, and I will only need a few days to learn Rust. There are also clear instructions in this project's README.md and CONTRIBUTING.md on code environment setup. This issue is bounded and specific, and no one has claimed it. There are no open pull requests already solving it. When contributing to this issue, I hope to learn Rust, do an open source contribution, and have a better understanding of software engineering beyond my coursework.

---

## Understanding the Issue

### Problem Description

Numerous issues occur when using OpenBLAS to implement Singular Value Decomposition (SVD) across different systems.

### Expected Behavior

I should implement SVD in Rust without using OpenBLAS as a dependency.

### Current Behavior

When computing SVD for the Optimized Product Quantization (OPQ) indexing process, many problems occur in building and using OpenBLAS as a dependency in different systems. No maintainers or commenters specified what these problems are.

### Affected Components

None of the files in the codebase contain an attempted SVD implementation. It seems that the attempted SVD implementation that depends on OpenBLAS has been removed, so I will need to create a new file named svd.rs in the directory rust/lance-linalg/src/. In this new file, I will compute SVD using Rust and without using openblas-src as a dependency.

## Reproduction Process

### Environment Setup

To set up my local development environment, I installed VS Code, Rust, Python version 3.9+, Pylance, protocol buffers, commit hooks, and the Dev Containers extension. Installing VS Code, Rust, Python version 3.9+, and Pylance was easy and straightforward, and to install both these languages, I simply used the links the maintainers provided for the development environment. Links were also provided for installing protocol buffers, commit hooks, and the Dev Containers extension, but I struggled with installing these three tools because the instructions were more confusing. To understand how to install commit hooks, protocol buffers, and the Dev Containers extension, I discussed installation errors I got in the terminal with Claude Code and asked it how to resolve these errors.

### Steps to Reproduce

It seems that the attempted SVD implementation that depends on OpenBLAS has been removed, so I need to create in Rust a SVD implementation from scratch that does not depend on OpenBLAS. Therefore, I will be creating a new feature from scratch and there is no existing bug for me to trigger. However, I know from the issue description that building OpenBLAS in different systems and using it as a dependency when implementing SVD will cause problems. However, because there is no issue for me to reproduce and the issue description or comments do not specify what exactly these problems are, I do not know what these problems are. I will simply implement SVD in Rust without depending on OpenBLAS so I can minimize problems that occur across different systems.

### Reproduction Evidence

- **Commit showing reproduction:** https://github.com/SarahNasser576/lance/commit/1983fc90fe32b4ef3ff2881761ca363a3839ff3b
- **Screenshots/logs:** N/A
- **My findings:** The attempted SVD implementation that depends on OpenBLAS has been removed, and neither the post nor the comments state the specific problems depending on OpenBLAS causes. Thus, there is no issue for me to reproduce. I will be creating a SVD implementation from scratch in Rust without depending on OpenBLAS, explaining why my commit "showing reproduction" is simply a commit depicting that I created a new empty file named svd.rs in the directory rust/lance-linalg/src/. In this new file, I will be coding my SVD implementation.

---

## Solution Approach

### Analysis

Using OpenBLAS as a dependency in SVD implementation results in problems in different systems. However, due to limited information from the issue description on what these problems are or why depending on OpenBLAS causes them, I cannot give a more specific analysis of the root cause.

### Proposed Solution

Despite limited information in the issue statement, I believe I can solve this issue by simply implementing SVD in Rust without depending on OpenBLAS. First, I will Google search and learn about the SVD algorithm. Next, I will implement all steps in the SVD algorithm in Rust without using OpenBLAS as a dependency.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** When computing SVD for the Optimized Product Quantization (OPQ) indexing process, many issues occur in building and using OpenBLAS as a dependency in different systems. I should implement SVD in Rust without using OpenBLAS as a dependency.

**Match:** The file rust/lance-index/src/vector/bq/builder.rs has a few functions that are similar to my issue. These functions are:
- householder_qr(), which performs a QR decomposition of matrices using only Rust, is relevant to SVD because QR decomposition is one of the building blocks used in iterative SVD algorithms.
- random_orthogonal(), which uses the QR decomposition to generate orthogonal matrices, is relevant to SVD because the two output matrices from SVD are orthogonal matrices. Unlike random_orthogonal(), the SVD implementation should produce the two output matrices from the input and not randomly.

Code from householder_qr() that does something similar to what I need (My SVD implementation will use a very similar bidiagonalization step as the one shown by this code from householder_qr()):

```
let sign = if x[0] >= 0.0 { 1.0 } else { -1.0 };

        x[0] += sign * x_norm;
        
        let u = &x / x.dot(&x).sqrt();
```
and
```
let h = ndarray::Array2::eye(m - k) - 2.0 * u_outer;
```
Code from random_orthogonal() that does something similar to what I need (Q here is an orthogonal matrix, and my SVD implementation will decompose a matrix into three matrices, which includes an orthogonal matrix and the transpose of a different orthogonal matrix):
```
let (q, _) = householder_qr(a);
```
**Plan:**
1. Google search and learn about the SVD algorithm
2. Implement all steps in the SVD algorithm using Rust and without using OpenBLAS as a dependency

**Implement:** Link to my branch/commits as I work: https://github.com/SarahNasser576/lance/commits/fix-issue-SVDImplementation

**Review:** I should include corresponding tests in my pull request. I described these tests in the Evaluate section of the UMPIRE framework. This project does not require automated testing.

**Evaluate:** I will test my code by running it on various matrices and comparing my output to solutions generated by the online SVD calculator found at the link https://www.emathhelp.net/calculators/linear-algebra/svd-calculator.

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

### Week 3 Progress

In week 3, I implemented an SVD algorithm in Rust without using OpenBLAS as a dependency. Claude Code was helpful when learning how to implement this algorithm in Rust, especially because I am new to Rust. One integration test was not working, so I shared my code with Claude and asked it why that test was not working. Claude told me that my algorithm does not cover all the eigenvalues and that it does not sort the eigenvalues before picking the top k eigenvalues. As a result, parts of my implementation were using the wrong indices. Claude also showed me how I can sort all the eigenvalues first and then take the top k eigenvalues. After implementing the SVD algorithm, I decided to include input validation so that my algorithm runs only if the three statements below are all true:
- The input matrix has at least 1 row and at least 1 column.
- The data length of the input matrix matches the product of the specified number of rows and number of columns.
- The input matrix does not contain null or infinite entries.

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
