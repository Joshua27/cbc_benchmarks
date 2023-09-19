# B and Event-B Benchmarks from Constraint Based Checking

To solve a constraint, the corresponding B or Event-B model has to be loaded.
The constraints' paths are the same as their corresponding models' paths in ProB's public specification repository: https://github.com/hhu-stups/specifications

## Run Benchmark
- download [prob_prolog source files](https://prob.hhu.de/w/index.php?title=Download#Sourcecode) (benchmarking not available in ProB's release)
- build ProB CLI using `make`
- download [ProB's public specification repository](https://github.com/hhu-stups/specifications)
- place specification repository and this benchmark repository beside prob_prolog source folder
- use `-bench_smt_bmc`, `-bench_smt_cbc_deadlock` or `-bench_smt_cbc_inv` CLI commands passing the path of a model corresponding to a constraint

## Example
`probcli -bench_smt_cbc_deadlock 'public_examples/EventBPrologPackages/ProofDirected/benchmarks/earley_3_autoproof.eventb'`
This call will automatically select the corresponding deadlock benchmark from `deadlock_checking/public_examples/EventBPrologPackages/ProofDirected/benchmarks/earley_3_autoproof_deadlock_freedom.eval`

## Benchmark Description
- bounded model checking: constraint is true if any invariant is violated after k steps (generated constraints for k in 0..25)
- deadlock freedom checking: constraint is true if there exists a deadlock state independent from the machine invariants, i.e., the state is not necessarily reachable
- inductive invariant checking: constraint is true if there exists a state satisfying the invariant and it is possible to transition into a state violating the invariant (not necessarily a reachable state; generated independent constraints for each machine operation or event)

## Constraint Solvers
- prob: ProB's default constraint solver (CLP(FD))
- prob_cse: additionally using common subexpression elimination
- prob_chr: additionally using ProB's backend with specialized constraint-handling rules (CHR)
- prob_comp: additionally using ProB's compiler before constraint solving
- prob_prover: ProB's prover
- z3axm: ProB's integration of Z3 using an axiomatic translation to SMT-LIB (quantified formulas)
- z3cns: ProB's integration of Z3 using a constructive translation to SMT-LIB (lambda functions instead of quantified formulas)
- z3par: parallelization of both translations to SMT-LIB
- z3dec: same as z3par but additional decomposition of constraints into independent components prior to the translation to SMT-LIB
- raw_smt: ProB's custom SMT solver
- sym_raw_smt: additionally using static symmetry breaking
- smt: additionally using a static syntax analysis inferring constraints that imply eachother
- sym_smt: same as smt but additionally using static symmetry breaking
- setlog: ProB's interface to {log}
