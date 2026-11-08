# Unity Android Localization & Integrity Checks — Anonymous Case Study

**English** | [Türkçe](README.tr.md)

> **Anonymous field report.** The application name, developer, package identifier, version and proprietary asset paths have deliberately been omitted.
>
> **Observed result:** After multiple failed experiments, a participant confirmed that a localized Unity Android build launched and displayed translated text on one physical device. This is **not** a universal fix or independently replicated result.

## What happened?

The unmodified app launched normally. A locally repackaged and re-signed copy with translated Unity strings produced a Google Play-related prompt. A first startup-code experiment crashed immediately. A later, more narrowly scoped modification in the application-startup path was followed by a successful user test.

This illustrates the importance of distinguishing:

- **Package signing:** A valid signature on a repackaged APK does not give it the original developer's identity.
- **Distribution/integrity checks:** Protection can verify installation source or whether an app has changed, including offline.
- **Startup dependencies:** A syntactically valid code modification may still cause a runtime crash.
- **Package format:** A base APK and ABI-specific split aren't interchangeable with a standalone APK unless all required resources and native libraries are present.

Google explains the relevant checks in its [automatic integrity protection documentation](https://developer.android.com/security/fraud-prevention/environment).

## Observed evidence

| Observation | Lesson |
| --- | --- |
| Original installation worked; rebuilt translation prompted for Play | Re-signing isn't the same as preserving original distribution identity |
| Source package contained base and architecture-specific APK parts | Extracting only the base may omit required native libraries |
| Translatable strings were stored in Unity data | Text changes can be analyzed separately from executable changes |
| Early startup experiment crashed | Broad initialization changes can break unrelated startup dependencies |
| Later, focused startup-path experiment launched (user report) | A narrowly scoped difference was associated with a different result |
| Translation data was unchanged between the final two experiments | The later outcome was not caused by rewriting the translations again |

**Important limits:** No second-device reproduction, no Android crash log for the failed build, no proof of applicability to other apps, and no inference about authorization or entitlement.

## Reusable troubleshooting approach

For software you **own or have explicit permission to test**:

1. Preserve and launch a known-good build on the same test device.
2. Inspect the distribution format: base APK, architecture splits, resource splits.
3. Track localized data separately from executable-code changes.
4. Verify rebuilt archive structure and APK signature; neither guarantees publisher authorization.
5. Classify the symptom: install rejection, Play prompt, Java exception, native crash, or Unity initialization failure.
6. Obtain authorized device logs and remove identifying details before sharing them.
7. Compare known-good and failing builds at file level instead of relying on guesses.
8. Record exactly what was tested and distinguish direct verification from user reports.

A Play Store uninstall does not automatically disable checks embedded in an app. Recombining split APKs addresses packaging, not licensing. One successful device test cannot establish a generic solution.

## Publication boundaries

This repository intentionally contains **documentation only**. It does **not** publish the application's identity, packages, binaries, translated proprietary assets, signing keys, executable patch bytes, offsets, hooks, or step-by-step instructions for defeating licensing checks.

This is a descriptive account, **not legal advice** and not permission to modify or distribute someone else's software. Local copyright, licensing and anti-circumvention rules may apply. For distributable translations, seek the rightsholder's approval or consider an external screen-translation layer.

Original prose in this repository is offered under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); this grants **no rights** to third-party applications or assets.

## Further reading

- [Android Developers — Automatic integrity protection](https://developer.android.com/security/fraud-prevention/environment)
- [Android Developers — Play App Signing](https://developer.android.com/guide/app-bundle/faq)
- [Android Developers — APK signing](https://developer.android.com/tools/apksigner)
- [Android Developers — Play Integrity API](https://developer.android.com/google/play/integrity/overview)

**Independent community documentation. Not affiliated with Google, Unity, or any application developer.**
