# TorchScript Unsupported PyTorch Constructs

## Torch and Tensor Unsupported Attributes

TorchScript supports most methods defined on `torch` and `torch.Tensor`, but we do not have full coverage.
Here are specific known ops and categories of ops which have diverging behavior between
Python and TorchScript. If you encounter something else that is not supported please
file a GitHub issue. Deprecated ops are not listed below.

<!-- automodule:: torch.jit.unsupported_tensor_ops -->

### Functions Not Correctly Bound on Torch

The following functions will fail if used in TorchScript, either because they
are not bound on `torch` or because Python expects a different schema than
TorchScript.

* `torch.tensordot`
* `torch.nn.init.calculate_gain`
* `torch.nn.init.eye_`
* `torch.nn.init.dirac_`
* `torch.nn.init.kaiming_normal_`
* `torch.nn.init.orthogonal_`
* `torch.nn.init.sparse`

### Ops With Divergent Schemas Between Torch & Python

The following categories of ops have divergent schemas:

Functions which construct tensors from non-tensor inputs do not support the `requires_grad`
argument, except for `torch.tensor`. This covers the following ops:

* `torch.norm`
* `torch.bartlett_window`
* `torch.blackman_window`
* `torch.empty`
* `torch.empty_like`
* `torch.empty_strided`
* `torch.eye`
* `torch.full`
* `torch.full_like`
* `torch.hamming_window`
* `torch.hann_window`
* `torch.linspace`
* `torch.logspace`
* `torch.normal`
* `torch.ones`
* `torch.rand`
* `torch.rand_like`
* `torch.randint_like`
* `torch.randn`
* `torch.randn_like`
* `torch.randperm`
* `torch.tril_indices`
* `torch.triu_indices`
* `torch.vander`
* `torch.zeros`
* `torch.zeros_like`

The following functions require `dtype`, `layout`, `device` as parameters in TorchScript,
but these parameters are optional in Python.

* `torch.randint`
* `torch.sparse_coo_tensor`
* `torch.Tensor.to`

## PyTorch Unsupported Modules and Classes

TorchScript cannot currently compile a number of other commonly used PyTorch
constructs. Below are listed the modules that TorchScript does not support, and
an incomplete list of PyTorch classes that are not supported. For unsupported modules
we suggest using `torch.jit.trace`.

* `torch.nn.RNN`
* `torch.nn.AdaptiveLogSoftmaxWithLoss`
* `torch.autograd.Function`
* `torch.autograd.enable_grad`
