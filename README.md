# O(1) Labs - Crypto

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
opam repository add --yes --all --set-default o1-labs https://github.com/o1-labs/opam-repository.git
opam install snarky
```

## How to use?

There are several issues:

* packages in this repo rely on external packages that aren't published to an opam repository
* packages in this repo only seem to compile with ocaml 4.7.1 (perhaps due to dependencies)
* packages in this repo rely on some packages that are on a custom opam repository (o1labs opam repo)
* these constraints are not always detailed, because we can't (dune doesn't allow to pin versions) or we didn't (in opamp packaging files)

```
opam pin ppx_version ./external/ppx_version # doesn't use dune to build, so needs to be installed
opam pin ppx_snarky https://github.com/o1-labs/snarky.git # not published on opam repository

opam install . --deps-only # install pinned packages
```

this won't work if you're installing this via opam (e.g. `opam install ./signature_lib.opam`) unless all the `./external` packages are pinned 