# Tumoflip Remote 1.9

Selected hold/release fixes from upstream boundary
`a94f7c754f4e0f9881b7f3432906b46da4007e21` →
`df6334cdde0c88e22ab09ba16b12222cfccf834a`, not a wholesale UI replacement.

- Keep the Tumoflip radio broker and unknown-preset fail-closed policy.
- Release finishes the current frame; held RAW restarts after EOF; Back stops.
- Stop before switching map entries. Poll completion instead of posting late RAW
  callbacks to an app that may have exited.
- Deserialize once on start. Restore buttons with the radio off and counter
  multiplier zero; never start extra transmissions during cleanup.
- Checked saves use the Tumoflip `signal_file` FAP static library. It retains a
  verified `.tumo-bak` on error instead of deleting the original first. Existing
  backups block replacement; no promise of atomic power-loss protection.

Build inside the matching Tumoflip source/SDK (88.22 or newer **with** the
`signal_file` library/header); matching an upstream API number alone is not
sufficient. No new firmware core export is required by the static library.

Native regression/fault tests live in Tumoflip's
`tools/tumoflip/test_subremote_lifecycle.py`; RF/SD hardware checks remain separate.
