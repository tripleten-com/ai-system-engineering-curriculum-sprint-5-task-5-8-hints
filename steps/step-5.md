# Step 5: Prove it with tests and write the evidence note

## The idea

The evaluation command and the live comparison need the stack and the network, so they aren't tests. Their outputs go into your note. What you test is the logic beneath them:

- how a case and a set are loaded
- how a run is compared with a case
- how an answer is classified
- how the summary is computed

All four are plain functions once they're separated from the commands that call them.

Each needs a test that can fail for the right reason:

- **Loading:** a case missing a required field is rejected, and so is a set without its version.
- **Comparing:** build the "run" as a plain object in the test. A matching run passes. A wrong status, a missing kind, events out of order, or a wrong side effect each fail with that field named. Without an out-of-order case, a comparison that ignores order passes everything.
- **Classifying:** three answers, one for each outcome: one that fits, one that doesn't, and a well-formed tool call outside your lists.
- **Summarizing:** a fixed list of rows with known counts and latencies. Pick the number of rows with care: a median computed wrongly can still give the right answer on some lists.

As before, break each group once and watch a test fail.

> Covered in **CI Gates and Release Verification**.

## What's expected

- Your test file sits where `poe student-tests` collects it and needs no stack.
- The loading tests reject a case missing a field and a set without `version`.
- The comparison tests pass a matching run and fail four broken ones, each naming its field:
  - a wrong status
  - a missing kind
  - events out of order
  - a wrong side effect
- The classifier tests give `parsed`, `malformed` and `outside_authority`.
- The summary test checks kind matches, the median and the maximum on fixed rows.
- You broke each group once and saw a test fail:
  - a comparison that ignores order
  - a classifier that accepts everything
  - a summary that miscounts
- `poe demo` still passes, and `poe verify` passes after your last edit.

## When you're stuck

### Your comparison tests need the stack

<details><summary>Move 1</summary>

Is the comparison mixed into the code that starts runs?

</details>

<details><summary>Move 2</summary>

What would it take to call the comparison with one object that stands for a finished run?

</details>

<details><summary>Move 3</summary>

Move the comparison into its own function that takes a case and an observed-run object, and have the runner build that object. The tests build it too.

</details>

### Ignoring event order doesn't fail any test

<details><summary>Move 1</summary>

Does any test give the comparison a run whose required events are present but out of order?

</details>

<details><summary>Move 2</summary>

Add one: the same events as a passing run, with two swapped.

</details>

<details><summary>Move 3</summary>

Assert it fails and names the events field, then make the comparison ignore order and watch the test fail.

</details>

### The summary test passes with a wrong median

<details><summary>Move 1</summary>

Do your fixed rows have an even or an odd number of latencies?

</details>

<details><summary>Move 2</summary>

Would a wrong median formula give a different answer on both?

</details>

<details><summary>Move 3</summary>

Test at least one list where the two middle values differ, so averaging them and picking one give different results.

</details>

### The classifier never returns `outside_authority`

<details><summary>Move 1</summary>

Does any test send a well-formed tool call whose input falls outside your lists?

</details>

<details><summary>Move 2</summary>

Which list does your classifier check first?

</details>

<details><summary>Move 3</summary>

Add one test per list: one tool call with a disallowed reason code and one with a disallowed next step.

</details>
