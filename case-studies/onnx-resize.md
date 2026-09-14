# ONNX Resize: making interpolation separable

I contributed a change to ONNX's Python reference evaluator that replaces repeated recursive interpolation with batched operations along each axis. [PR #7920](https://github.com/onnx/onnx/pull/7920) was merged on May 12, 2026. This article describes that contribution at its merge revision, not the performance of every ONNX runtime.

## The problem

The previous implementation visited output coordinates and recursively interpolated through the input dimensions for each one. Much of the work was repeated. The opportunity was to change the computation's structure while preserving the operator's behavior.

For a simple two-dimensional linear resize, the weighted result can be written as:

`output[y, x] = sum_j wy[y, j] * sum_i wx[x, i] * input[j, i]`

The horizontal and vertical weights can be applied in separate passes. Instead of rebuilding the nested calculation for each output pixel, an implementation can resize one axis across the array, then resize the next. The same idea extends to additional axes when their interpolation is separable.

## What changed

The new [`_interpolate_1d_along_axis`](https://github.com/onnx/onnx/blob/4da22aa8c80e6c5f026993f4241ff7802c50cd5e/onnx/reference/ops/op_resize.py#L370) computes source coordinates, neighbor indices and weights for an axis. It gathers samples with `np.take`, broadcasts the weights, then sums along the neighbor dimension. Coefficient generation still includes a loop over output positions; vectorization applies to the larger gather and weighted calculation.

[`_interpolate_nd`](https://github.com/onnx/onnx/blob/4da22aa8c80e6c5f026993f4241ff7802c50cd5e/onnx/reference/ops/op_resize.py#L470) becomes a loop over the selected axes. Its identity check skips an axis only when scale, output size and region of interest allow that shortcut.

## The compatibility work

Separability alone does not settle which source pixels participate. The implementation retains coordinate transformation modes, neighbor tie-breaking, edge treatment, excluded samples and crop extrapolation. Integer and half-integer positions are useful cases to inspect because a different tie-break can change the selected neighborhood.

The merged source also handles an empty output axis before accessing the first coefficient row. These details matter in a reference evaluator: an optimization must preserve the behavior other implementations are compared against.

## Evidence and tradeoff

The [PR's validation record](https://github.com/onnx/onnx/pull/7920) reports 294 numerical comparisons with maximum difference below `1e-10`, 39 existing Resize backend cases, and 1,798 passing tests in the reference backend suite. Those are contribution-time results, not fresh results from today's upstream branch. Numerical tolerance is the relevant claim; floating-point operations are not promised to be bit-identical after reordering.

Batched gathers and weighted arrays exchange temporary memory for less repeated Python work. That tradeoff deserves measurement for large shapes. I do not use the PR's single-machine timing anecdote as a general speedup claim.

For a new benchmark, pin the revisions and environment, preserve mode/shape/coordinate settings, check numerical agreement, and report repeated timings and peak memory. Small representative cases should precede expensive scalar runs.

The contribution demonstrates a focused change taken through upstream review: identify repeated work, change the algorithm, and account for compatibility at the edges.
