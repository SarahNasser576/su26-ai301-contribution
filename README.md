# Contribution [1]: [Make a SVD implementation in Rust and remove the dependency of openblas]

**Contribution Number:** [1]
**Student:** [Sarah Nasser]  
**Issue:** [https://github.com/lance-format/lance/issues/984]  
**Status:** [Phase 3] [Complete]

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

- Test case 1: Ran the function multiply_a_by_vector() with the input: A = [5.0, 7.0, -1.0, 4.0], x = [-9.0, -2.0], m = 2, n = 2. Current and expected output: [-59.0, 1.0]. Test passed.
- Test case 2: Ran the function compute_ata() with the input: A = [3.0, 2.0, -4.0, 7.0, -2.0, -1.0, 5.0, 4.0], m = 2, n = 4. Current and expected output: [13.0, 8.0, -22.0, 13.0, 8.0, 5.0, -13.0, 10.0, -22.0, -13.0, 41.0, -8.0, 13.0, 10.0, -8.0, 65.0]. Test passed.
- Test case 3: Ran the function create_identity_matrix() with the input: n = 5. Current and expected output: [1.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1.0]. Test passed.

### Integration Tests

- Integration scenario 1: input matrix A = [3.0, 2.0, 2.0, 2.0, 3.0, -2.0], m = 2, n = 3. Current and expected output: sigma values are 5 and 3, U ≈ [0.7071, 0.7071, 0.7071, -0.7071], and V^T ≈ [0.7071, 0.7071, 0, 0.2357, -0.2357, 0.9428, 0.6667, -0.6667, -0.3333]. Test passed.
- Integration scenario 2: input matrix A = [7.0, -4.0, 5.0, 5.0, 8.0, -2.0, -10.0, 1.0, -1.0, -8.0, 9.0, 3.0, 8.0, 7.0, -3.0, 4.0], m = 4, n = 4. Current and expected output: sigma values are 17.834861, 13.682368, 8.433152, and 0.769723; U ≈ [0.1103, 0.7669, 0.1056, -0.6233, -0.5973, 0.3163, -0.7191, 0.1617, 0.5994, 0.4553, -0.1537, 0.6402, -0.5214, 0.3233, 0.6695, 0.4189], and V^T ≈ [-0.4921, -0.4312, 0.7560, -0.0187, 0.7330, -0.3713, 0.2777, 0.4977, 0.0588, 0.8219, 0.5131, 0.2402, -0.4659, -0.0249, -0.2968, 0.8332]. Test passed.
  
### Manual Testing

- Manual test 1: Ran the function svd() with the input: input matrix A = [-9.0, -5.0, -2.0, 4.0, -1.0, 6.0, 9.0, -2.0, -6.0], m = 3, n = 3. Current and expected output: sigma values are 13.503700, 8.990339, and 4.563320; U ≈ [-0.6955, -0.4291, -0.5763, 0.2417, 0.6157, -0.7500, 0.6767, -0.6609, -0.3245], and V^T ≈ [0.9861, 0.1394, -0.0903, 0.0419, 0.3172, 0.9474, -0.1607, 0.9381, -0.3070]. Test passed.
- Manual test 2: Ran the function svd() with the input: input matrix A = [], m = 0, n = 0. Current and expected output: U, sigma, and V^T are all empty matrices, and the error message is "Error: Matrix must have at least 1 row and at least 1 column." Test passed.
- Manual test 3: Ran the function svd() with the input: input matrix A = [9.0, -8.0, 3.0, -1.0], m = 1, n = 2. Current and expected output: U, sigma, and V^T are all empty matrices, and the error message is "Error: Data length of matrix must match the product of the specified number of rows and number of columns." Test passed.
- Manual test 4: Ran the function svd() with the input: input matrix A = [3.0, 1.0, f64::NAN, -4.0, -2.0, -1.0, 8.0, 3.0, 1.0], m = 3, n = 3. Current and expected output: U, sigma, and V^T are all empty matrices, and the error message is "Error: Matrix must not contain null or infinite entries." Test passed.
- Manual test 5: Ran the function svd() with the input: input matrix A = [9.0, f64::INFINITY, -1.0, 8.0], m = 2, n = 2. Current and expected output: U, sigma, and V^T are all empty matrices, and the error message is "Error: Matrix must not contain null or infinite entries." Test passed.
- Manual test 6: Ran the function jacobi_rotate() with the input: input matrix A = [4.0, 2.0, 2.0, 3.0], n = 2, p = 0, q = 1, (sn, c) = theta.sin_cos(). Current and expected output: [5.56155281280883, 0.0, 0.0, 1.4384471871911697], off-diagonal a[0,1] = 0.000000, and trace = 7.000000. Test passed.
- Manual test 7: Ran the function apply_givens_rotation_from_right() with the input: b = [1.0, 0.0, 0.0, 1.0], n = 2, p = 0, q = 1, c = angle.cos(), sn = s = angle.sin(). Current and expected output: [0.7071, -0.7071, 0.7071, 0.7071]. Test passed.
- Manual test 8: Ran the function jacobi_eigen() with the input: input matrix A = [4.0, 1.0, 1.0, 3.0], n = 2. Current and expected output: eigenvalues are [4.618, 2.382] (in any order) and the eigenvector is [0.85065080835204, -0.5257311121191336, 0.5257311121191336, 0.85065080835204]. Test passed.
- Manual test 9: Ran the function gram_schmidt() with the input: [[1.0, 1.0, 0.0], [1.0, 0.0, 1.0], [0.0, 1.0, 1.0]]. Current and expected output: col[0] = [0.7071067811865475, 0.7071067811865475, 0.0]  norm = 1.000000, col[1] = [0.40824829046386313, -0.40824829046386296, 0.8164965809277261]  norm = 1.000000, col[2] = [-0.5773502691896257, 0.5773502691896258, 0.5773502691896256]  norm = 1.000000, dot(col0,col1) = 0.000000, dot(col0,col2) = 0.000000, and dot(col1,col2) = 0.000000. Test passed.

Maintainers had not mentioned the edge cases I identified in manual tests 2–5.

---

## Implementation Notes

### Week 3 Progress

In week 3, I implemented an SVD algorithm in Rust without using OpenBLAS as a dependency. Claude Code was helpful when learning how to implement this algorithm in Rust, especially because I am new to Rust. A challenge I faced during the implementation process was that one integration test was not working. I shared my code with Claude and asked it why that test was not working. Claude told me that my algorithm did not cover all the eigenvalues and did not sort the eigenvalues before picking the top k eigenvalues. As a result, parts of my implementation were using the wrong indices. Claude also showed me how I could sort all the eigenvalues first and then take the top k eigenvalues. After correctly implementing the SVD algorithm, I decided to include input validation so that my algorithm runs only if the three statements below are all true:
- The input matrix has at least 1 row and at least 1 column.
- The data length of the input matrix matches the product of the specified number of rows and number of columns.
- The input matrix does not contain null or infinite entries.

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** I created and coded in a new file called svd.rs.
- **Key commits:** https://github.com/SarahNasser576/lance/commit/0cea39f1b3ca714f20f1042ac0d88c67688abc02, https://github.com/SarahNasser576/lance/commit/e26009ac6cd75d77264131ca18b71f94e3decb62, https://github.com/SarahNasser576/lance/commit/71fc8cb55cac34382cfada82e90aaf6088bafede, https://github.com/SarahNasser576/lance/commit/52972c8d68e279544daac006bbc435de4e746a6e
- **Approach decisions:** I chose to call built-in math functions rather than creating them from scratch in my code for simplicity purposes and to make my code more readable. I included input validation as I described in the paragraph above on my week 3 progress because it cannot be assumed that the user will always use valid input matrices (i.e., matrices with at least 1 row and at least 1 column, only non-null or finite entries, and a data length equal to the product of the specified number of rows and number of columns). I did not use OpenBLAS as a dependency because the maintainer stated that depending on it would result in problems across different systems. Neither the maintainer nor the commenters specified what these problems are. I also chose to implement my SVD algorithm in Rust because commenter I8dNLo suggested a pure-Rust implementation and the maintainer approved of this suggestion.
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

- GitHub discussion that helped: https://github.com/lance-format/lance/issues/984
- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
