# Evidence and limitations

This anonymous record deliberately excludes the application's identity, identifying hashes, executable modifications, and proprietary content.

## How each claim was established

- **Local file inspection:** The distribution used a base package and an architecture-specific split, and localization data was tracked separately from executable changes.
- **Local static validation:** Rebuilt archive and signature checks succeeded, but cannot establish that an app will be accepted by Google Play or work on a physical device.
- **User-reported runtime result:** An early experimental build failed at startup. A later translated build successfully opened on one Android device and displayed translated text.
- **Local comparison:** The translation content in the last two standalone experiments did not differ; an executable member differed.

## What this does not prove

- There was no independent second-device replication.
- No complete Android crash trace was supplied for the failed experiment.
- No universal method is established for different applications, protection configurations, signatures, operating systems, or entitlement policies.
- Successful launch does not establish permission to redistribute proprietary binaries.

## Practice for authorized testing

Preserve originals, document changes, separate installer and runtime errors, collect only authorized logs, redact device/account identifiers, and distinguish direct inspection from user reports.
