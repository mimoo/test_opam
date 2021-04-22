# O(1) Labs - Crypto

This is a work in progress to move some of the cryptography packages of Mina in their own repository and packages.
You can see the relevant issue here: https://github.com/MinaProtocol/mina/issues/8621

## Todo

- [x] create `o1-labs/crypto` repo
- [ ] add snarky_backendless package to snarky repo
- [ ] extract `random_oracle`, `random_oracle_input`, `signature_lib`, `vrf_lib` and make sure they can build
- [ ] move all `/external` packages to the o1-labs opam repository
- [ ] get rid of `config.mlh` and `/config`
- [ ] split `signature_lib` into `schnorr_signature` and `mina_keypairs` (and move `mina_keypairs` to the Mina repo)
- [ ] publish the crypto packages to the o1-labs opam repository
- [ ] make Mina use these packages instead of the internal ones (and delete the internal ones)
- [ ] squash all commits
## What's here?

```
lib/
├── random_oracle/ # poseidon hash implementation
├── random_oracle_input/ # input encoding thing (should be inside random_oracle no?)
├── signature_lib/ # schnorr implementation (over tick and tock curves) and verification circuit
├── vrf_lib/ # VRF implementation
└── dune-project
```

## Pre-requesites

Some of the dependencies here are not published on the opam repository, so you'll have to add the [O(1) labs opam repository](https://github.com/o1-labs/opam-repository) first.

```
# create local switch
opam switch create . 4.07.1

# add o1labs opam repo to local switch
opam repository add --yes o1-labs https://github.com/o1-labs/opam-repository.git
```

## How to use?

There are several issues:

* packages in this repo rely on external packages that aren't published to an opam repository
* packages in this repo only seem to compile with ocaml 4.7.1 (perhaps due to dependencies)
* packages in this repo rely on some packages that are on a custom opam repository (o1labs opam repo)
* these constraints are not always detailed, because we can't (dune doesn't allow to pin versions) or we didn't (in opamp packaging files)

```
# not published on opam repository
opam pin add https://github.com/o1-labs/snarky.git -y # lots of packages there

# this is still needed for other non-pinned packages
opam install . --deps-only
```

this won't work if you're installing this via opam (e.g. `opam install ./signature_lib.opam`) unless all the `./external` packages are pinned 