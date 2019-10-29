# Review

## Info

Reviewer Name: Ian Bridges
Paper Title: Efficient Software-Based Fault Isolation

## Summary

### Problem and why we care
Incorporating third-party library into your application code has become 
a fundamental practice. However, if an issue occurs in the third-party 
code, it may affect your application. Since we want to build secure 
applications, we need a way to ensure that issues in module code don't 
impact the security of the application.

### Gap in current approaches
Current approaches place unsafe code in a different address space. While 
this creates an isolated environment, it also forces expensive RPC calls 
to communicate between different address spaces.

### Hypothesis, Key Idea, or Main Claim
We can avoid the expense of RPC calls by placing unsafe code in contiguous 
memory regions in the same address space as the safe code. We can isolate 
these regions by instrumenting indirect writes and control transfers 
in such a way that the target address cannot point to a location outside 
the region containing the executing code.

### Method for Proving the Claim
The authors created a prototype that adds the SFI instrumentation to 
target binaries. This prototype was based on a static compiler pass, 
which inserted a series of instructions before each unsafe write 
and control flow transfer (determined earlier in the compiler pass) 
that check to ensure that the segment ID of the target address matches 
the segment ID of the current segment.

### Method for evaluating
The prototype described above was used to generate binaries with 
the SFI property that also performed benchmarking tests. The results 
of those benchmarks were compared to hypothetical overhead of RPC-based 
isolation techniques.

### Contributions: what we take away

## Pros (3-6 bullets)
- Low overhead
- Compiler pass = minimal overhead for consumers
- Extensible (supported by compiler = useable on all code supported 
by that compiler)

## Cons (3-6 bullets)
- Depends on adoption by library developers
- Attackers can still target un-instrumented libraries
- Fast path (sandboxing) doesn't track original target address, which 
makes debugging difficult (one of the original advantages of fault 
isolation)

## Details Comments, Observations, Questions
- The story of SFI sounds a lot like the story of ASLR
- There are two SFI implementations described in this paper: binary 
patching (dynamic) and compiler-enforced (static). Is the dynamic 
approach possible for x86/64?
- If we have to use a compiler-based implementation, is the efficacy 
of SFI dependant on its adoption rate by writers of third-party 
libraries?
- Does the SFI model work if it is dependent on developer adoption?




