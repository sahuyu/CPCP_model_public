# CPCP_model_public
Cell Populated Collagen‐PA (CPCP) double layer computational model

To understand roles of cellular adhesion, contractility and motility in the depth-sensitive epithelial cell clustering, a cell populated collagen‐PA (CPCP) double layer model was adopted and modified from previous research. The numerical computation and visualization for the model was accomplished in MATLAB (R2021a). In this model, cells are meshed on the col‐PA double layer matrixes. Each cell is defined as a set of nodes that directly attached to the collagen lattice nodes, with three individual parameters respectively to describe its migration, protrusion, and contraction and one collective parameter to describe the cell‐cell interaction. The collagen fiber network is defined as triangulated spring lattices that are linked to the polyacrylamide layer through the intermediate springs located at the lattice nodes. As cells deform and remodel the collagen lattices, the intermediate springs transfer the cell‐generated force to the PA layer. The PA gel layer is described using a linear 2D finite element model. In this CPCP model, the cellular behavior on the Col‐PA matrix is broadly divided into four steps:
1) Migration and protrusion of cells. Any cell node could move along the collagen lattices and find a new collagen lattice node to attach. The direction and magnitude of cell node movement is determined by its position and migration/protrusion parameters of the corresponding cell (or cells).
2) Contraction. Cells deform the collagen lattices by moving the collagen lattice nodes along with the attached cell nodes. The direction and magnitude of nodal movement are determined by the associated nodal position and contraction parameters. 
For instance, as illustrated in Fig. S10A, a given cell node (black) is attached to a collagen lattice node (green) and shared by three adjacent cells. Each cell has three individual displacement vectors due to migration, protrusion, and contraction whose magnitude are directly proportional their corresponding biochemical signaling parameters that vary with cells. The direction of migration vector is calculated using the orientation tensor of the collagen network and position vectors of adjacent cells. The protrusion vectors are directed outwards relative to the cell body, along the line connecting from the cell’s center of mass to the given node; the contraction vectors are oriented in the opposite direction, towards the cell center. Cell-cell interaction is regulated by a binding coefficient shared within the same cell cluster. Cell proliferation was achieved by enabling division of cells with the largest area.

$$\gamma\nu_{y_i}={F_i=\sum_{j}\ f_{i,j}+p}_i\ \ \ \ \ \ \ \ \ \ \ \ \ \ \left(1\right)$$

\[f_{i,j}=\left\{\begin{matrix}0\ \ \ \ \ \ \ \ \ \ \ \ ,d_{i,j}\le l_{i,j}\ and\ f_{i,j}\ is\ normal\\-\triangle_\beta\beta\left(d_{i,j}-{\triangle_ll}_{i,j}\right)\frac{y_i-y_j}{d_{i,j}}\delta_{i,j}\ ,\ if\ f_{i,j}\ is\ compacted\\-\beta\left(d_{i,j}-l_{i,j}\right)\frac{y_i-y_j}{d_{i,j}}\delta_{i,j}\ \ \ \ \ ,d_{i,j}>l_{i,j}\ and\ f_{i,j}\ is\ normal\\\end{matrix}\right.\ \ \ \ \ \ \ \left.\ \begin{matrix}(2.1)\\\begin{matrix}\\(2.2)\\\end{matrix}\\\begin{matrix}\\(2.3)\\\end{matrix}\\\end{matrix}\right\}\]

$$p_i=-\beta\left(1-\frac{h_0}{\sqrt{{h_0}^2+\left(y_i-z_i\right)^2}}\right)\ \left(y_i-z_i\right)\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ (3)$$
$$d_{i,j}=yi-yj                                                                                                  (4)$$

3) Collagen deformation. Collagen lattices are deformed and remodeled by the cells, as described above, to reach steady state. Eq. 1 describes the motion for the collagen lattice node i, where f_(i,j) describes the force due to lattice entanglement and p_i describes the force generated by the PA gel. y_i is the location in R^2 of the collagen lattice node, ν_(y_i ) represents the velocity of y_i, and γ is the drag coefficient of collagen lattice. Normal collagen fibers undergo stretching in a spring-like fashion (Eq. 2.3) and remain unstressed under compression (Eq. 2.1), with forces proportional to level of stretching. In this spring-like behavior, l_(i,j) is the spring initial length between two linked nodes i and j, and β is the spring constant of the collagen fibers. Compaction of fibers is a non‐reversible part of collagen remodeling induced by cells. The spring constant of compacted fibers increases according to coefficient △_β, and the spring initial length is reset to 〖△_l l〗_(i,j). Compacted fibers resist compression as described in Equation (Eq. 2.2). Since f_(i,j) is only available when node i and node j are linked, the δ_(i,j) in (Eq. 2.2) and (Eq. 2.3) indicates the link status, which is equal to 1 when node i and node j are linked and equal to 0 otherwise. At the beginning of simulation, all collagen fibers start as normal (i.e., not compacted) and get remodeled to compacted status when the distance between two linked nodes (d_(i,j)) becomes short enough (d_(i,j)≤△_l l_(i,j)) driven by cellular contraction. Node locations z_j are within R^2 region of the adhesion site of collagen on the PA gel surface, while initial thickness of the collagen layer is h_0. When y_i and z_i have the same initial value, force in col-PA intermediate springs ‖p_i ‖=0 is set at t_0 , which subsequently increases with mismatch of deformations in collagen and PA gels. These variables and parameters are listed and described in Table S1.

4) PA deformation and stiff sensing. The intermediate springs that connect collagen and PA layers transmit cellular forces to the PA layer through the collagen lattices. Deformation of PA layer is calculated with a linear 2D finite element solver, using the same triangular mesh as the collagen lattices. The depth-mechanosensing of cells is implemented by measuring the depth-sensing parameter (σ) as shown in Eq. 5. p_i (t)^' 
is the derivative of the remaining force within intermediate springs (p_i, shown in Eq. 3) versus its displacement in horizontal plane. σ_i (t) is the depth-sensing parameter of node i at time t, which is defined as the average of p_i (t)^' over time (∆t). ∆t is 30min in all the simulations.  As shown in Fig. 4B, stiffer PA layer undergoes smaller deformation, which leaves higher remnant force within intermediate springs causes higher depth‐mechanosensing feedback. This depth-sensing parameter (σ) directly influences the migration, protrusion and contraction parameters of the corresponding cell.
