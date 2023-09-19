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
