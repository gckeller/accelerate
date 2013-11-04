An Embedded Language for Accelerated Array Computations
=======================================================

`Data.Array.Accelerate` defines an embedded language of array computations for high-performance computing in Haskell. Computations on multi-dimensional, regular arrays are expressed in the form of parameterised collective operations (such as maps, reductions, and permutations). These computations are online-compiled and executed on a range of architectures.

For more details, see our papers [Accelerating Haskell Array Codes with Multicore GPUs][CKLM+11] and [Optimising Purely Functional GPU Programs][MCKL13]. There are also some slides of a fairly recent presentation: [Embedded Languages for High-Performance Computing in Haskell.][Embedded]

A simple example
----------------

As a simple example, consider the computation of a dot product of two vectors of single-precision floating-point numbers:

    dotp :: Acc (Vector Float) -> Acc (Vector Float) -> Acc (Scalar Float)
    dotp xs ys = fold (+) 0 (zipWith (*) xs ys)

Except for the type, this code is almost the same as the corresponding Haskell code on lists of floats. The types indicate that the computation may be online-compiled for performance — for example, using `Data.Array.Accelerate.CUDA.run` it may be on-the-fly off-loaded to a GPU.

For a complete introduction to Accelerate by example, see my talk _GPGPU Programming in Haskell with Accelerate_ from YOW! LambdaJam 2013 ([slides][yow13-slides]) ([video][yow13-video]).

Availability
------------

Package accelerate is available from

 * Hackage: [accelerate][Hackage] — install with `cabal install accelerate`
 * GitHub: [AccelerateHS/accelerate][GitHub] - get the source with `git clone https://github.com/AccelerateHS/accelerate.git`

Additional components
---------------------

The following supported addons are available as separate packages on Hackage and included as submodules in the GitHub repository:

  * [`accelerate-cuda`][accelerate-cuda] Backend targeting CUDA-enabled NVIDA GPUs — requires the NVIDIA CUDA SDK and hardware with compute capability 1.2 or greater (see the [table on Wikipedia][wiki-cc])
  * [`accelerate-examples`][accelerate-examples] Computational kernels and applications showcasing the use of Accelerate as well as a regression test suite (supporting function and performance testing)
  * [`accelerate-io`][accelerate-io] Fast conversion between Accelerate arrays and other array formats (including Repa arrays)
  * [`accelerate-backend-kit`][accelerate-backend-kit] Simplified internal AST to get going on writing backends
  * [`accelerate-buildbot`][accelerate-buildbot] Build bot for automatic performance & regression testing

Install them from Hackage with `cabal install PACKAGENAME`.

The following additional components are experimental and incomplete:

  * [`accelerate-opencl`][accelerate-opencl] Backend targeting GPUs via the OpenCL standard
  * [`accelerate-repa`][accelerate-repa] Backend targeting multicore CPUs via the [Repa][repa] parallel array library

Requirements
------------

  * Glasgow Haskell Compiler (GHC), 7.0.3 or later
  * Haskell libraries as specified in [`accelerate.cabal`][Cabal-file]
  * For the CUDA backend, CUDA version 3.0 or later

Examples and documentation
--------------------------

The GitHub repository contains a submodule [accelerate-examples][accelerate-examples], which provides a range of computational kernels and a few complete applications. To install these from Hackage, issue `cabal install accelerate-examples`.

  * Haddock documentation is included in the package and linked from the [Hackage page][Hackage].
  * Online documentation is on the [GitHub wiki][Wiki].
  * The idea behind the HOAS (higher-order abstract syntax) to de-Bruijn conversion used in the library is [described separately.][HOAS-conv]

Mailing list and contacts
-------------------------

  * Mailing list: [`accelerate-haskell@googlegroups.com`](mailto:accelerate-haskell@googlegroups.com) (discussions on both use and development are welcome)
  * Sign up for the mailing list at the [Accelerate Google Groups page][Google-Group].
  * Bug reports and issues tracking: [GitHub project page][Issues].

The maintainer of this package is Manuel M T Chakravarty <chak@cse.unsw.edu.au> (aka TacticalGrace on #haskell and related channels).

What's missing?
---------------

Here is a list of features that are currently missing:

 * Preliminary API (parts of the API may still change in subsequent releases)



  [CKLM+11]:                http://www.cse.unsw.edu.au/~chak/papers/CKLM+11.html
  [MCKL13]:                 http://www.cse.unsw.edu.au/~chak/papers/MCKL13.html
  [HIW'09]:                 http://haskell.org/haskellwiki/HaskellImplementorsWorkshop
  [Embedded]:               https://speakerdeck.com/mchakravarty/embedded-languages-for-high-performance-computing-in-haskell
  [Hackage]:                http://hackage.haskell.org/package/accelerate
  [accelerate-cuda]:        https://github.com/AccelerateHS/accelerate-cuda
  [accelerate-examples]:    https://github.com/AccelerateHS/accelerate-examples
  [accelerate-io]:          https://github.com/AccelerateHS/accelerate-io
  [accelerate-backend-kit]: https://github.com/AccelerateHS/accelerate-backend-kit
  [accelerate-buildbot]:    https://github.com/AccelerateHS/accelerate-buildbot
  [accelerate-repa]:        https://github.com/blambo/accelerate-repa
  [accelerate-opencl]:      https://github.com/hiPERFIT/accelerate-opencl
  [GitHub]:                 https://github.com/AccelerateHS/accelerate
  [Wiki]:                   https://github.com/AccelerateHS/accelerate/wiki
  [Issues]:                 https://github.com/AccelerateHS/accelerate/issues
  [Google-Group]:           http://groups.google.com/group/accelerate-haskell
  [HOAS-conv]:              http://www.cse.unsw.edu.au/~chak/haskell/term-conv/
  [Cabal-file]:             https://github.com/AccelerateHS/accelerate/accelerate.cabal
  [repa]:                   http://hackage.haskell.org/package/repa
  [wiki-cc]:                http://en.wikipedia.org/wiki/CUDA#Supported_GPUs
  [yow13-slides]:           https://speakerdeck.com/tmcdonell/gpgpu-programming-in-haskell-with-accelerate
  [yow13-video]:            http://youtu.be/ARqE4yT2Z0o

