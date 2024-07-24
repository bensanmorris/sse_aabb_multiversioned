### About

In a [previous side-project](https://github.com/bensanmorris/sse_aabb) I experimented with SSE / non-SSE variants of updating an AABB (Axis Aligned Bounding Box) by rotating the original AABB. In this revisiting I modified my code to make use of the auto cpu-dispatch mechanism support available in gcc (aka 'multiversioning'). If you're not familiar with multi-versioning, it's a mechanism that lets you write multiple implementations of the same function targetting a specific set of instruction set architecture instructions (SSE / SIMD for instance) for potentially large performance gains on specific cpus by taking advantage of vector registers / associated instructions. If you're in control of the hardware then multiversioning is something you should definitely be considering. Contrary to the idea that targetting specific cpus makes the code less portable multiversioning requires you provide a "default" implementation of your function that you can make cpu-agnostic (nb. compiler options that you build with need to be taken into consideration i.e. if you target sse / avx then your cpu-agnostic version could be vectorised by the compiler when building).

### Results

To build: 
```
(linux)
cmake -B build -G "Unix Makefiles"
cd build
cmake --build . --config Release
./sse2

To verify the SSE variant is executed run on a machine with SSE support and put a breakpoint in the SSE implementation.
```

### Links

- Function multi-versioning: https://gcc.gnu.org/wiki/FunctionMultiVersioning
- Intel intrinsics guide: https://software.intel.com/sites/landingpage/IntrinsicsGuide/#
- Intel assembler guide: https://software.intel.com/sites/default/files/managed/a4/60/325383-sdm-vol-2abcd.pdf
