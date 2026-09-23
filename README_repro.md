# CMP Key Refresh - reproduction evidence

This repository hosts the reproduction for a Bugcrowd submission against
github.com/fireblocks/mpc-lib revision `00ae08b7f1bdbb887aedece384aca2f942aae432`.

## What this fork contains

- `.github/workflows/cmp_refresh_repro.yml` - builds the pinned revision,
  runs the bundled `cmp_offline_ecdsa` test (baseline), applies
  `ecdsa_offline_test__refresh_poc.patch` (one inserted line), rebuilds and
  runs again, then uploads all logs as an artifact.
- `ecdsa_offline_test__refresh_poc.patch` - the one-line proof-of-concept.

## Expected result

- Baseline run: the whole `cmp_offline_ecdsa` test case PASSES.
- After the one-line patch: the run FAILS deterministically at
  `test/cosigner/ecdsa_offline_test.cpp:336` with
  `cosigner_exception(INVALID_PARAMETERS)` and the library log
  `Failed to verify Bx*X^e == g^z1`.