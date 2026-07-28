# Cinatra Blog Post Matcher

The classification rules Cinatra applies when it has to decide whether an uploaded file is a finished blog post. It is the knowledge half of `@cinatra-ai/blog-post-artifact`, packaged as its own skill so the artifact extension declares a dependency on it instead of shipping it inside.

**Install:** Install `@cinatra-ai/blog-post-matcher-skill` in your Cinatra instance. `@cinatra-ai/blog-post-artifact` installs it automatically as a declared dependency.

**Usage:** The classifier worker loads this skill through the artifact extension's declared `matcher` dependency edge — you do not invoke it directly. It reads the attached file plus the recorded upload signals and answers with a match verdict, a confidence score and a short rationale.

**Configuration:** None. The skill carries no credentials and reads no settings; the host supplies the model runtime.

**Development:** Clone the repository and run `node extension-kind-gate.mjs --package-root .` to validate the manifest. The bundle lives in `skills/blog-post-matcher/` — a single `SKILL.md` router with no reference files.

**Troubleshooting:** If uploads are never typed as Blog Post, check that `@cinatra-ai/blog-post-artifact` is installed and that its declared dependency on this package resolved; an unresolved edge means the classifier has no rules to apply and the upload keeps its structural identity.

## Works with

- Cinatra Blog Post artifact extension
- Any extension declaring a skill dependency on this package

## Capabilities

- Decide whether an attached file is a finished blog post
- Name the look-alike document kinds that must NOT match
- Return a calibrated confidence score the host compares against the extension's threshold
- Answer as strict JSON with no surrounding prose
