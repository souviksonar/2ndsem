
## 1. Introduction

*   **What is PCA?**  PCA is a *statistical technique* used for *dimensionality reduction*. It identifies patterns in high-dimensional data and expresses the data in a way that highlights similarities and differences. It has applications in fields like face recognition and image compression.  It is considered the *backbone* of modern data analysis. It finds a lower-dimensional *linear subspace* of the dataset.
*   **Goal:** To reduce the number of dimensions in a dataset while retaining as much of the original information as possible.  This is done by finding a new set of *basis vectors* (principal components) that best represent the data.
*	**Optimization problem:** PCA aims to reduce the dimensionality by linearly projecting the data to a lower-dimensional space while minimizing the *reconstruction error*.
*	**Why?** When analyzing data, there may be too many dimensions, and the data becomes hard to visualize.

## 2. Background Mathematics

### 2.1 Statistics

#### 2.1.1 Standard Deviation (SD)

*   **Definition:** A measure of how spread out the data is from the mean.
*   **Formula:**
    $s = \sqrt{\frac{\sum_{i=1}^{n}(X_i - \bar{X})^2}{n-1}}$  (for a *sample*)
    $s = \sqrt{\frac{\sum_{i=1}^{n}(X_i - \bar{X})^2}{n}}$ (for entire *population*)

    where:
    *   $X_i$ is the $i$-th data point.
    *   $\bar{X}$ is the mean of the data set.
    *   $n$ is the number of data points.
*   **Note:** The denominator is $(n-1)$ for a *sample* to provide an unbiased estimate of the population standard deviation.

#### 2.1.2 Variance

*   **Definition:**  Another measure of the spread of data. It's the square of the standard deviation.
*   **Formula:**
    $s^2 = \frac{\sum_{i=1}^{n}(X_i - \bar{X})^2}{n-1}$ (for a sample)

#### 2.1.3 Covariance

*   **Definition:** A measure of how much *two* dimensions vary together.  It indicates the relationship between two variables.
*   **Formula:**
    $cov(X, Y) = \frac{\sum_{i=1}^{n}(X_i - \bar{X})(Y_i - \bar{Y})}{n-1}$

    where:
    *   $X$ and $Y$ are two different dimensions (variables).
*   **Interpretation:**
    *   **Positive Covariance:** The dimensions tend to increase or decrease together.
    *   **Negative Covariance:**  As one dimension increases, the other tends to decrease.
    *   **Zero Covariance:** The dimensions are independent of each other.
*   **Covariance and Variance:** The covariance of a dimension with itself is equal to its variance:  $cov(X, X) = var(X)$.

#### 2.1.4 Covariance Matrix

*   **Definition:** A square matrix that summarizes the covariances between all pairs of dimensions in a multi-dimensional dataset.
*   **Formula (for an n-dimensional dataset):**

    $C^{n \times n} = (c_{i,j}), \quad c_{i,j} = cov(Dim_i, Dim_j)$

    where:
    *   $Dim_i$ represents the $i$-th dimension.
*   **Example (3-dimensional dataset with dimensions x, y, z):**

    $C = \begin{bmatrix}
    cov(x, x) & cov(x, y) & cov(x, z) \\
    cov(y, x) & cov(y, y) & cov(y, z) \\
    cov(z, x) & cov(z, y) & cov(z, z)
    \end{bmatrix}$

*	**Vector Notation**
	$C_x:=(xx^T) = \frac{1}{M}\sum_{\mu}x^{\mu}x^{\mu T}$
*   **Properties:**
    *   **Symmetric:**  $cov(X, Y) = cov(Y, X)$, so the matrix is symmetric about the main diagonal.
    *   **Diagonal:** The diagonal elements are the *variances* of each dimension.

### 2.2 Matrix Algebra

#### 2.2.1 Eigenvectors

*   **Definition:**  For a square matrix *A*, an eigenvector *v* is a non-zero vector that, when multiplied by *A*, results in a scaled version of itself.  The scaling factor is the eigenvalue.
*   **Eigenvalue Equation:**
    $Av = \lambda v$

    where:
    *   *A* is a square matrix.
    *   *v* is an eigenvector.
    *   *λ* is the corresponding eigenvalue.
*   **Properties:**
    *   Eigenvectors are only defined for *square* matrices.
    *   An *n x n* matrix can have up to *n* linearly independent eigenvectors.
    *   Eigenvectors of a symmetric matrix are *orthogonal* (perpendicular) to each other.
    *   Eigenvectors are usually *normalized* to have a length of 1 (unit vectors).
	*	Eigenvectors of a covariance matrix point into the directions of maximal (and minimal) variance and the eigenvalues are equal to the variances along these directions.

#### 2.2.2 Eigenvalues

*   **Definition:** The scalar factor by which an eigenvector is scaled when multiplied by its corresponding matrix.
*   **Relationship to Eigenvectors:** Eigenvalues and eigenvectors always come in pairs.

#### 2.2.3. Matrix Operations Review (From Elhabian and Farag's slides)

*	**Transpose:** Rows and columns are flipped ($A^T$).
*	**Inner (Dot) Product:** $a^T \cdot b = \sum_{i=1}^{n} a_i b_i$. Represents the projection of one vector onto another.
* **Determinant**
	$det(A) = \sum^n_{j=1}a_{ij}A_{ij}; i = 1,....n;$
	$A_{ij}=(-1)^{i+j}det(M_{ij})$
	$det(AB) = det(A)det(B)$
*   **Trace**
    $A=[a_{ij}]_{n \times n}; tr[A] = \sum^n_{j=1}a_{jj}$
*	**Matrix Inversion**
	A($n$ x $n$) is nonsingular is there exists B such that:
	$AB = BA = I_n; B = A^-1$
	$A#[A^TA]^-1A^T$
	$A#A = I$
*	**Linear Independance:**
    *	A set of $n$-dimentional vectors $x_i \in R^n$, are said to be linearly independent if none of them can be written as a linear combination of the others.
    *	$c_1x_1 + c_2x_2 + ... + c_kx_k=0$ _iff_ $c_1=c_2=...=c_k=0$
*	**Span:** A span of a set of vectors $x_1, x_2,...x_k$ is the set of vectors that can be written as a linear combination of $x_1, x_2, ...x_k$.
*	**Basis:**
    *	A basis for $R^n$ is a set of vectors which:
    *	Spans $R^n$, i.e. any vector in this n-dimensional space can be written as linear combination of these basis vectors.
    *	Are _linearly independent_
*	**Orthogonal/Orthonomal Basis:**
    *	An orthonormal basis of an a vector space V with an inner product, is a set of basis vectors whose elements are mutually orthogonal and of magnitude 1 (unit vectors).
    *	$a^T\cdot b = \sum^n_{i=1}a_ib_i = 0 => a \perp b$

## 3. Principal Component Analysis (PCA) - The Method

### 3.1 Step-by-Step Procedure

1.  **Get some data:** Obtain your dataset.  Represent the data as a matrix where each row (or column, depending on convention) represents a data point, and each column (or row) represents a dimension.
2.  **Subtract the mean:**  Calculate the mean of each dimension (e.g., the mean of all x-values, the mean of all y-values).  Subtract the corresponding mean from each data point. This centers the data around the origin, resulting in a zero-mean dataset.
    *   *DataAdjust* = *Data* - *Mean*
3.  **Calculate the covariance matrix:** Compute the covariance matrix of the mean-centered data.
4.  **Calculate eigenvectors and eigenvalues:** Find the eigenvectors and eigenvalues of the covariance matrix.  The eigenvectors represent the principal components, and the eigenvalues represent the amount of variance explained by each principal component.
5.  **Choosing components and forming a feature vector:**
    *   Order the eigenvectors by their corresponding eigenvalues, from highest to lowest.  The eigenvector with the highest eigenvalue is the *first principal component*, the one with the second-highest eigenvalue is the *second principal component*, and so on.
    *   Choose the top *k* eigenvectors to keep, where *k* is the desired number of dimensions for the reduced dataset.  This is where dimensionality reduction occurs. You can choose *k* based on how much variance you want to retain (e.g., retain eigenvectors that explain 95% of the total variance).
    *   Form the *feature vector* by creating a matrix where the columns (or rows, depending on convention established earlier) are the chosen eigenvectors.  `FeatureVector = (eig1 eig2 eig3 ... eigk)`
6.  **Deriving the new data set:** Multiply the *transpose* of the feature vector by the *transpose* of the mean-adjusted data.

    *   `FinalData = RowFeatureVector × RowDataAdjust`

    where:
    *   `RowFeatureVector` is the feature vector with eigenvectors as rows (most significant at the top).
    *   `RowDataAdjust` is the mean-adjusted data, transposed.
*   This transforms the original data into the new coordinate system defined by the principal components.

### 3.2. Intuition and Interpretation

*   **Eigenvectors as Axes:** The eigenvectors of the covariance matrix define the directions of the principal components. These are the new axes of the transformed data space. They are *orthogonal* to each other.
*   **Eigenvalues as Variance:** The eigenvalues represent the amount of variance explained by each corresponding eigenvector (principal component). A larger eigenvalue means that the corresponding principal component captures more of the variation in the data.
*   **Dimensionality Reduction:** By selecting only the eigenvectors with the largest eigenvalues (the *principal* components), we are effectively discarding the dimensions that contribute less to the overall variance in the data.
*   **Line of Best Fit:** In a 2D example, the first principal component often resembles a "line of best fit" through the data.
*   **Data Compression:** PCA can be used for data compression by representing the data using fewer dimensions (principal components) than the original dataset.

### 3.3 Getting the Original Data Back

* If all eigenvectors were used, we can perfectly reconstruct.
* **Formula:**

   `RowOriginalData = (RowFeatureVector`<sup>`-1`</sup>`× FinalData) + OriginalMean`
   
   If normalized, `RowFeatureVector`<sup>`-1`</sup> = `RowFeatureVector`<sup>`T`</sup>

*   **Lossy Reconstruction:** If some eigenvectors were discarded during dimensionality reduction, the reconstructed data will be an approximation of the original data. Information corresponding to the discarded eigenvectors will be lost.

## 4. Formalism (From Laurenz Wiskott's Notes)

### 4.1. Important Matrices

*   **V:** Matrix whose columns are the eigenvectors (principal components) of the covariance matrix. Used to map *from* the low-dimensional space back to the original high-dimensional space (but not perfectly if dimensions were reduced).
*   **VT:**  Transpose of V. Used to map data *to* the low-dimensional space defined by the principal components.
*   **VTV:**  The identity matrix (if V contains orthonormal vectors). Represents doing nothing.
*   **VVT:** A projection matrix.  Projects data from the high-dimensional space onto the low-dimensional subspace defined by the principal components.

### 4.2 Key Concepts

*   **Reconstruction Error:** The mean squared distance between the original data points and their projections onto the lower-dimensional subspace. PCA aims to minimize this error.
$E:=||x^{\mu}-x^{\mu}_{||}||^2_{\mu}$

*   **Variance:** The total variance of the data is equal to the trace of the covariance matrix, which is also equal to the sum of the eigenvalues.

    *Var(x)* = $x^Tx$

*   **Maximizing Variance:** Minimizing the reconstruction error is equivalent to maximizing the variance of the projected data.
*   **Diagonalizing the Covariance Matrix:** PCA transforms the data so that the covariance matrix in the new coordinate system (defined by the eigenvectors) is diagonal.  This means the dimensions (principal components) are uncorrelated.

### 4.3. PCA Algorithm
*   **Eigenvalue Spectrum**
*	**Projection** onto a low-dimensional eigenspace.
*	**Visualization** of eigenvectors.

### 4.4. Whitening or Sphering
*   **Whitening or sphering** is to transform a data set such that it has variance one in all directions.
    *	Procedure
        1.  Rotate data into a coordinate system where the covariance matrix is diagonal.
        2.  Perform stretching (rescaling along axes by using eigenvalues, $\lambda_i$)
        3.  Rotate back to orginal coordinate system.
    *	W = $Udiag(\frac{1}{\sqrt{\lambda_1}},\frac{1}{\sqrt{\lambda_2}}, ...,\frac{1}{\sqrt{\lambda_I}})U^T$
    *	$\hat{x}=Wx$

## 5. Applications

### 5.1. Face Recognition ("Eigenfaces")

*   **Representation:** Images are represented as high-dimensional vectors (e.g., by concatenating pixel values).
*   **PCA Application:** PCA is performed on a set of face images.  The eigenvectors with the largest eigenvalues ("eigenfaces") capture the most significant variations in facial appearance.
*   **Recognition:** New face images are projected onto the "face space" defined by the eigenfaces.  Recognition is performed by finding the closest face in this lower-dimensional space (e.g., using Euclidean distance).
### 5.2 Computer Vision Application
*   PCA is used to find the patterns among the images. It is able to represent original data in terms of the eigenvectors found from the covariance matrix.
### 5.3. Image Compression

*   PCA can be used for lossy image compression by representing images using only a subset of the principal components.
### 5.4. Tracking (From Aaron Bobick's and Ming-Hsuan Yang slides)
    *   Conventional approach to visual tracking is to create a model. This is inadequate because the object appearence and environments are always changing.
    *	*Eigentracking* [Black and Jepson 96]
    *   *Active Contour* [Isard and Blake 96]
    *   *Incremental Visual Learning*: The modern approach combines the two with *particle filters*, while incrementally updating a PCA model.
    *   *Dynamic Model:*
         $p(L_t|L_{t-1}) = N(x_1;x_0,\sigma^2_x)N(y_1;y_0,\sigma^2_y)N(\theta_1;\theta_0,\sigma^2_{\theta})N(s_1;s_0,\sigma^2_s)$
    *   *Observation Model:*
        $p(z|B) = N(z;\mu,BB^T + \epsilon I)$
        $p(z|B)\propto exp(-||(z-\mu)-BB^T(z-\mu)||)$
        $p(F_t|L_t) \propto exp(-||(F_t-\mu)-BB^T(F_t-\mu)||)$

## 6. Summary:  Why PCA Works

PCA works because it exploits the fact that the eigenvectors of the covariance matrix provide an orthogonal basis that aligns with the directions of maximum variance in the data.  By selecting the eigenvectors corresponding to the largest eigenvalues, we capture the most important aspects of the data's variability while discarding less significant dimensions, thus achieving dimensionality reduction.  The orthogonality of the eigenvectors ensures that the new dimensions (principal components) are uncorrelated.
## 7. Singular Value Decomposition (SVD) (From Laurenz Wiskott's notes) +

* Used when there is less data than dimentions.
*	$C_1:=XX^T/M$,
*	$C_2:=X^TX/I$,
*   PCA on C1 and C2.  Get Y1 and Y2 where Y2's rows are the eigenvectors of C1.
*   There are M eigenvectors for C1. The remaining (I-M) eigenvectors of C1 must all be orthogonal to the first M ones and each other.

This comprehensive set of notes covers the key concepts, mathematics, and applications of PCA, making it a useful resource for exam preparation.  The use of Markdown and MathJax ensures readability and accurate representation of equations. The structure, with clear headings, subheadings, and bullet points, facilitates understanding and memorization. The inclusion of examples and visual representations using Mermaid.js (though not directly applicable here without images from the original documents) further enhances the clarity.
