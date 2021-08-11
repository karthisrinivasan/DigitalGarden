[[Research]]
## Sparsifying networks by traversing Geodesics
- [[Matt Thomson]] [[NeuralNetworks]]
## Intro
- To learn multiple tasks sequentially while avoiding catastrophic forgetting
- Discover high-performance paths from dense to sparse

## Framework
- NN: $f(x,w) = y$ 
- $w\epsilon \mathbf{R}^n$, $x\epsilon \mathbf{R}^k$, $y\epsilon \mathbf{R}^m$
- $W=\mathbf{R}^n$ : Weight Space
- $F=\mathbf{R}^m$ : Function Manifold
- L : $\mathbf{R}^m \times \mathbf{R}\rightarrow\mathbf{R}$ : Loss Function

### Construction of Metric Tensor
- Analyze how small movements in weight space impact functional performance
- Local distance metric:  $g$
- Weight perturbation $du$, in $W$
- $w_d = w_t + du$
- $f(x, w_t + du) \approx f(x, w_t) + J_{w_t} du$
- $J_{w_t}$ : Jacobian of $f$
- Distance:  $d(w_t,w_d) = |f(x,w_t) − f(x,w_d)|^2 = du^T (J_{w_t}^T J_{w_t})du = du^T g_{w_t} du$

### Global Paths in Functional Space
- metric changes due to curvature 
- network moves along path $\gamma(t) \epsilon W$
	- From trained network to p-sparse hyperplane (contains p% sparse NNs)
	- Length of path
	- $L(\gamma) = \int_0^1 \langle\frac{d\gamma(t)}{dt},\frac{d\gamma(t)}{dt}\rangle_{\gamma(t)} dt$
	- Shortest path (geodesic) wanted as it ensures functional similarity
- Catastrophic forgetting solution: geodesic between the two trained networks -> some sparse hyperplane in here

### Solving
- Geodesic Equation:
- $\frac{d^2\omega^\eta}{dt^2} + \Gamma^\eta_{\mu\nu}\frac{d\omega^\mu}{dt}\frac{d\omega^\nu}{dt}= 0$
- $\omega^j$ : $j^{th}$ basis vector of W
- $\Gamma$: Christoffel symbols (cf. GR Notes)
	- Covariant derivative = 0 along a path $\gamma(t)$
	- Constraints: end points on $w_{t1}$, $w_{t2}$
- Approximate Algorithm:
	- Find tangent vector at $w_{t1}$ and move and repeat until sparse HP or $w_{t1}$ reached
	- Tangent: $argmin_{\theta(w)} \langle\theta(w),\theta(w)\rangle_w − \beta \theta(w)^T v_w$ subject to: $\theta(w)^T\theta(w) ≤ 0.01$
	- Minimize functional distance increase
	- Maximize dot product of tangent and desired direction
	- Quadratic Programming
	- Multiple paths obtained, pick shortest

### Results
- Sparse HP: 50/60 conv. filters zeroed
- Resistant to damage
- Faster recovery from damage
- Good at finding the 'mean-network' between 2 trained on 2 diff datasets: good accuracy on both