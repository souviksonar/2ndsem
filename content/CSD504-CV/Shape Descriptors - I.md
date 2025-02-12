

# Shape Analysis Applications

**(Image 6 Description):**  Six panels illustrating different shape analysis applications, with images and descriptions.

*   **Panel 1: Feature Detection**
    *   Image: A bicycle.
    *   Text: "Find salient feature points"
*   **Panel 2: Correspondences**
    *   Image: Two figures interacting.
    *   Text: "Find matching points between two shapes"
*   **Panel 3: Segmentation**
    *    Image: Human figures with body parts colored.
    *    Text: "Break a shape into meaningful parts"
    *   Legend:
        *   head
        *   torso
        *   upper
        *   lower
        *   hand
        *   upper
        *   lower
        *   foot

*   **Panel 4: Registration**
    *   Image: Two overlapping face scans.
    *   Text: "Bring two or more shapes into pointwise alignment"
*   **Panel 5: Symmetry Detection**
    *   Image: A complex, symmetrical 3D model of a creature.
    *   Text: "Find dominant symmetries of a shape"
*   **Panel 6: Labeling**
     *    Image: Human figures with body parts colored(same as panel 3).
    *   Text: "Assign labels (“hand”, “wheel”, “wing”...) to segments"
    *    Legend:
        *   head
        *   torso
        *   upper
        *   lower
        *   hand
        *   upper
        *   lower
        *   foot

# Shape Analysis Applications

**(Image 7 Description):** Six panels illustrating different shape analysis applications.

*   **Panel 1: Retrieval**
    *   Image: Multiple horse shapes.
    *   Text: "Find shapes matching the query shape"
*   **Panel 2: Classification**
    *   Image: A decision tree for classifying objects.
    *    Text:"Find the category (“human”, “car”, “bird”) of a shape"
    *    Category -> Instance
         *    Cereal -> Chex, Bran Flakes
         *   Apple
         *    Stapler
         *    Bowl -> Striped Bowl, Blue Bowl

*   **Panel 3: Recognition**
    *   Image: various objects in the scene.
    *   Text: "Find instances of a given shape in a scene"
*   **Panel 4: Clustering**
    *   Image: multiple bikes and cars.
    *   Text: "Group shapes by similarity"
    *    Text: "parameterized embedding"

# Shape Descriptor

**(Image/Diagram 8 Description):**  Illustrations relating to global and local shape descriptors.

*   **Definition:** A set of numbers that describes a shape in a way that is:
    *   **Concise:** A few numbers that capture the "essence" of the shape.
    *   **Quick to compute**
    *   **Efficient to compare**
    *   **Discriminative:**
        *   Different shapes have different descriptors.
        *   Similar shapes have similar descriptors.
*   **Vector Space:** Typically, the descriptors form a vector space with a meaningful distance metric.
*  **Global:** Examples with hand, horse, pot, and camel silhouette.
*  **Local:** Examples with camel.

# Global and Local Descriptors

**(Image/Diagram 9 Description):** Visual examples and explanations of global and local descriptors.

*   **Global Descriptor:**
    *   Captures the structure of the entire shape.
    *   Can tell different shapes apart.
    *   Useful for retrieval, object recognition, etc.
    *   (Image: Two very different vehicle silhouettes and a probability vs. distance graph.)
*   **Local Descriptor:**
    *   Captures the shape around a point.
    *   Can tell different points apart.
    *   Useful for segmentation, point correspondences, etc.
     *   (Image: Two teapots and two camels with heatmaps.)
*   **Relationship:** Each motivates the other: can modify any global descriptor to produce a local descriptor, and vice versa.

# Local and Global - Applications

**(Image 10 Description):** Summary of applications, categorized by whether they typically use local or global descriptors.

*   **Local:**
    *   Feature detection
    *   Correspondences
    *   Registration
    *   Symmetry detection
    *   Segmentation
    *   Labeling
*   **Global:**
    *   Retrieval
    *   Classification
    *   Recognition
    *   Clustering

# Local Descriptors

*   **Definition:** Describes the shape in a neighborhood around a point.
    *   Neighborhood may be surface-based or volume-based.
*   **Descriptors to be discussed:**
    *   Mean curvature
    *   Shape diameter
    *   Principal components
    *   Average distance
    *   Distance histogram

# Curvature

**(Image 12 Description):** Two images of a 3D face, one colored according to Gaussian curvature and the other according to mean curvature.

*   **Gaussian Curvature:** The product of the principal curvatures.
*   **Mean Curvature:** The average of the principal curvatures.

# Mean Curvature

*   **Computation:** How can we (approximately) compute the mean curvature at a point?
*   **Two Approximations:**
    *   **Average Projection:** Average projection of neighboring points onto the normal vector.
         *(Image: A curve with points and normal vectors, showing the projection.)*
    *   **Fraction of Unit Ball:** Fraction of a unit ball covered by the neighboring volume.
        *(Image: A curve and two circles showing the fraction of area covered, one < 0.5 and one > 0.5.)*

# Shape Diameter

**(Image 14 Description):** Several examples of 3D shapes (horses and humans) colored according to their shape diameter function (SDF).

*   **Shape Diameter Function (SDF):** Gives the "local thickness" of a shape at each point.

# Shape Diameter

**(Image 15 Description):** Examples showing how to calculate the SDF, including a hand and several human figures.

*   **Calculation:**
    *   Shoot rays randomly sampled from a cone surrounding the inward normal.
    *   SDF is the average distance (weighted by inverse angle) to the next intersection with the shape, after removing outliers.

# Principal Components

**(Image 16 Description):** A diagram illustrating principal components on a 2D shape.

*   **Definition:** The principal components (eigenvalues of the covariance matrix) of points in the neighborhood capture the directional variation of the shape.
*   **Interpretations:**
    *   One large principal component: line-like.
    *   Two large principal components: surface-like.
    *   Three large principal components: volume-like.

# Distance-Based Descriptors

**(Image 17 Description):** A rabbit model. The first image shows connections from one point to several others.  The second image is a color-mapped (composite plot) version of the rabbit.

*   **Average Distance:** Average (geodesic or Euclidean) distance to all other points on the shape.
*   **Histogram of Distances:** A more discriminative measure: plot a histogram of the distribution of distances.