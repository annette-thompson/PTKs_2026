# PTK–substrate docking and MD inputs

Inputs for the docking and molecular dynamics of c-Abl and c-Src with DDEVIYAVPQF (Ile) and DDEVHYAVPQF (-1His),
in the order of the Methods.

1. `structures/`: the crystal structures used (2QOH c-Abl, 3DQW c-Src, 1ATP for ATP and the two Mg2+, 2G2F for the
   c-Abl Gly-rich loop and as the substrate reference) and the minimized holo receptors (kinase, ATP, 2 Mg2+).
2. `docking/tables/`: the contacts conserved across substrate-bound PTK crystal structures and the restraints taken
   from them; the docking clusters, the four crystal criteria per start and each cluster's fate in MD.
3. `docking/<system>/`: the HADDOCK3 inputs of that system's docking run. `ambig.tbl` is built at run time from
   the active/passive residue files with `haddock3-restraints`, and the ATP restraints are appended to
   `unambig.tbl`, before `docking.cfg` is run; `ambig_as_run.tbl` is the file each run actually used.
4. `final_starts.tsv`: every simulated start (role catalytic or control; status kept or discarded, Methods "Pose
   retention") and its folder in `md/systems/`.
5. `md/systems/<system>/<model>_<role>/`: GROMACS inputs per start: `system.gro`, `topol.top` with its `.itp` files
   (AMBER ff14SB, phosaa14SB, ATP polyphosphate parameters, Li–Merz Mg2+, Joung–Cheatham ions, TIP3P; hydrogen mass
   repartitioning), `index.ndx`, and the docked model `start.pdb`.
6. `md/mdp/`: minimization (`01`), NVT and NPT equilibration with decreasing position restraints (`02`–`05`),
   unrestrained NPT (`06`) and production (`md_300ns_3fs.mdp`; 3 fs steps, three 300 ns replicates per start).
