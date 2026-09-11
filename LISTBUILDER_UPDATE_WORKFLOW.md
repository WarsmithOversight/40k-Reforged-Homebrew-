# Listbuilder Update Workflow

This file records the normal maintenance workflow for 40k Reforged New Recruit catalogues.

## Minimal Update Contract

For routine rules updates, the maintainer only needs to provide:

- the faction / catalogue name;
- the new army-rules version;
- the changes that are relevant to list construction.

Example:

> World Eaters becomes 3.3.4. Butcher Surgeon goes from 130 to 70 points.

Everything else below is treated as normal maintenance work and should be handled automatically unless the maintainer says otherwise.

## Standard Update Procedure

1. Start from the latest healthy executable catalogue, not an older rules PDF or experimental branch.

2. Treat the supplied army-rules version as the new catalogue baseline.

3. Implement only listbuilder-relevant rules changes.
   - Do not reproduce rules changes that do not affect list construction.
   - Do not invent builder changes merely because the underlying datasheet changed.

4. Preserve existing stable IDs wherever the same semantic object still exists.
   - Rename or retune the existing object when appropriate.
   - Create deterministic IDs only for genuinely new semantic objects.

5. Preserve existing catalogue mechanics unless the update explicitly changes them.
   This includes:
   - categories and presentation;
   - attachments;
   - validation;
   - Additional Copy Cost arithmetic;
   - list-size logic;
   - configuration behavior;
   - existing compatibility structures.

6. Update player-facing version metadata.
   - Update the catalogue name to the new army-rules version.
   - Increment the catalogue revision by one.
   - Update the Patch Notes heading or other current player-facing notice as appropriate.

7. Patch Notes should contain only builder-relevant army changes.
   - Do not repeat changes already implemented in an earlier catalogue revision if the new rules publication merely makes them official.
   - **Catalogue Bugfixes are cumulative.** Keep all previous bugfix bullets, update the `## Catalogue Bugfixes ([latest date])` heading to the current work date, and append new fixes to the existing list.
   - Remove an older bugfix bullet only when that specific change has been explicitly reverted and is no longer true.
   - Do not reset, replace, or prune the bugfix history merely because a new work session, revision, or date has started.
   - Always retain the standard Reforged Discord reference when Patch Notes are used.

8. Keep the catalogue pointed at the current Game System revision.
   - A rules-version update is also an opportunity to catch an old `gameSystemRevision`.
   - Do not alter Game System mechanics merely to perform this compatibility sync.

9. When a portable/shared unit changes, synchronize every owned copy of that unit in the same pass.
   - In particular, generic Chaos Space Marines units exported through the Great Traitors’ Arsenal must be synchronized between the playable CSM catalogue and the Arsenal Library.
   - Preserve stable target IDs so consumer catalogues continue resolving the same unit identity.

10. If a linked library's mechanics have not changed, do not rebuild or rewrite it unnecessarily.
    Human-readable version labels may be refreshed when useful, but target IDs remain authoritative.

## Validation After Every Update

Before handing the file back:

- confirm the intended catalogue name and revision;
- confirm the intended Game System revision;
- confirm all requested points and option changes;
- verify stable IDs were preserved where expected;
- verify Additional Copy Cost arithmetic is unchanged unless intentionally modified;
- verify portable library roots exactly match their playable source where synchronization is required;
- verify no unrelated catalogue content changed;
- verify duplicate IDs = 0.

For a compatibility-only Game System sync, normalize the changed metadata back to the source and confirm the resulting object is otherwise byte-equivalent.

## Baseline-Only Updates

When a faction receives a new rules version with no listbuilder-relevant changes:

- update the catalogue rules-version name;
- increment the catalogue revision;
- update the Patch Notes baseline;
- retain any existing Catalogue Bugfixes section;
- point the catalogue at the current Game System revision;
- make no mechanical changes.

## Final Patch-Cycle Sweep

After a batch of army updates is complete, audit the active executable catalogue set for old Game System targets.

Any remaining live catalogue or owned shared library should be retargeted to the current Game System revision in a strict compatibility-only pass.

## Design Principle

The listbuilder is a companion to the army rules, not a second rules document.

Patch work should therefore be narrow:

**Implement the decisions a player must make while building a list, preserve everything that already works, and leave battlefield rules in the PDF.**
