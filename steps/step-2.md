# Step 2: Build the command that runs every case

## The idea

A case nobody can run is just a note. The evaluation command turns your three cases into a check anyone can run after any change. It prints pass or fail for each case, and for a failure it names the first thing that didn't match.

The command is two separate pieces:

- **The runner:** for each case, it prepares a fresh exception, runs the case's script through the server the way your dev command does, and answers every pause with the case's decision. Then it reads what happened: the status, the kinds, the trail and the side effect. "No answer" needs care. A paused run waits forever on its own, so the runner waits past your configured timeout, then sends a decision, and the run halts on the timeout.
- **The comparison:** a plain function that takes a case and what the run showed, checks the fields in a fixed order, and returns the first mismatch: which field, what was expected, what was seen. The required events must appear in order, with other events allowed between them. That way a new event you add next week doesn't break every case.

Keeping the comparison apart from the runner is what makes it testable without a stack. And the command exits non-zero when any case fails, so a script that calls it notices.

> Covered in **3.6 Evaluating an Agent Run**.

## What's expected

- Your evaluation command runs every case in the set, and only those. It can also run one case by name.
- Each case runs on a fresh exception and prints pass, or fail with the field, the expected value and the observed one.
- The command exits non-zero when any case fails.
- With the stack up and the emulator answering, all three cases pass.
- Changing one expectation in one case and running that case alone makes it fail, and the comparison names the field. Change it back after.
- Running the set twice in a row gives the same results.

## When you're stuck

### The second case fails with `review_already_open`

<details><summary>Hint 1</summary>

Which exception does each case run on?

</details>

<details><summary>Hint 2</summary>

Does the runner create a fresh exception before every case, or reuse one?

</details>

<details><summary>Hint 3</summary>

Create one in `NEEDS_REVIEW` per case, the way `poe demo` does, and pass its id to that case's run only.

</details>

### A "no answer" case never finishes

<details><summary>Hint 1</summary>

What does a paused run do on its own when nobody answers?

</details>

<details><summary>Hint 2</summary>

How did the timeout row of your Task 6 check command end its run?

</details>

<details><summary>Hint 3</summary>

The approach: for no answer, the runner reads the timeout from your configuration, waits just past it, then sends a decision as a dispatcher. The run halts on the timeout, and the case expects exactly that.

</details>

### Changing an expectation makes the loader refuse the case

<details><summary>Hint 1</summary>

Which code reported the problem: the comparison, or the loader?

</details>

<details><summary>Hint 2</summary>

Does your loader enforce rules such as "a success case must expect finished"? Then a changed status never reaches the run.

</details>

<details><summary>Hint 3</summary>

Either keep the loader to shape only, or change a field it doesn't enforce, such as one kind in the list, so the comparison is what fails.

</details>

### Adding a new event breaks every case

<details><summary>Hint 1</summary>

Does your comparison require the trail to equal a list exactly?

</details>

<details><summary>Hint 2</summary>

What did the case promise: these events in this order, or only these events?

</details>

<details><summary>Hint 3</summary>

The approach: walk the observed trail once, moving to the next required event each time you meet the current one. The case passes when every required event has been met in order, whatever sits between them.

</details>

### A failing case still exits 0

<details><summary>Hint 1</summary>

Where does your command set its exit code?

</details>

<details><summary>Hint 2</summary>

Does it remember that any case failed, after printing all of them?

</details>

<details><summary>Hint 3</summary>

Run every case, print every line, then exit non-zero if any case failed.

</details>

### A case flips between pass and fail with no change

<details><summary>Hint 1</summary>

Does the runner read the result before the run has finished, or before the trail has been written?

</details>

<details><summary>Hint 2</summary>

Where could timing enter: reading the trail, reading the queue depth, or reading the store?

</details>

<details><summary>Hint 3</summary>

Read the results only after the run reports its final status, and read the side effect against a value you took before the run started.

</details>
