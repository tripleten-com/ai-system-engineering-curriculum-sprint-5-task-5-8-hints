# Step 1: Write the three evaluation cases and version the set

## The idea

The dispatcher's question is whether the agent will still do the right thing after the next change. A trail you read once answers that for one day. An evaluation case answers it every time someone runs it: "with this script and this decision, the run does this, and nothing else".

A good case judges a whole run, not one answer:

- **How it ended:** the final status, and the halt reason when it halted.
- **What it did:** the complete, ordered list of proposal kinds.
- **What it recorded:** the events that must appear in the trail, in order. Other events may sit between them.
- **What it changed:** a review opened, or nothing.

The last part matters as much as the first. A refusal case that checks only the status would pass a run that opened a review and then refused. "And nothing else" is what the kinds list and the side effect add.

Three runs cover the vaccine workflow: everything goes right, the agent says no, and the tool fails once and the run recovers. Take every expectation from a trail you kept, in the order the trail shows it, never from memory.

The set that lists the cases carries a version, and the version changes whenever a case does. Then a passing result always names the exact set it passed against. A later Task reads that version.

> Covered in **3.6 Evaluating an Agent Run**.

## What's expected

- Three case files exist: success, refusal and recovery. Each states these:
  - its script
  - how the exception is prepared
  - the decision at every pause
  - the final status
  - the full kinds list
  - the required events in order
  - the side effect
  - the halt reason, where the case halts
- The success case plays the approval script `poe demo` plays and requires a review opened.
- The refusal case requires no side effect and no `call_tool` or `ask_approval` among its kinds.
- The recovery case requires `finished`, a review opened, and a failed tool call before the one that opens the review.
- The set file has a field named `version` and a comment stating when the version changes.

## When you're stuck

### Your success case never opens a review

<details><summary>Hint 1</summary>

Which script does the case play? Read its entries.

</details>

<details><summary>Hint 2</summary>

Does that script ever propose a tool call, or does it only finish?

</details>

<details><summary>Hint 3</summary>

Which of your scripts does `poe demo` play? Run it with approval and read its trail.

</details>

<details><summary>Hint 4</summary>

Point the success case at the demo's script, decision approve, and take its kinds and events from that trail.

</details>

### Your recovery case has no `tool_failed`

<details><summary>Hint 1</summary>

Run your recovery script with every pause approved and read its trail. Is there a failed call followed by one that opens a review?

</details>

<details><summary>Hint 2</summary>

If the script stops after its first call, would adding a second, valid call change a trail your Task 7 tests pin?

</details>

<details><summary>Hint 3</summary>

The approach: write a new recovery-shaped script whose first tool call is turned down and whose later call opens the review, and point the recovery case at it. The old script and its tests stay as they are.

</details>

### You can't decide how a case says "no answer" or "no side effect"

<details><summary>Hint 1</summary>

Both are values the runner has to read. What spelling would be unambiguous next to approve and reject?

</details>

<details><summary>Hint 2</summary>

For the side effect, what are the two possible observations: a review opened, or nothing?

</details>

<details><summary>Hint 3</summary>

Pick a spelling for each, put both in a comment at the top of your first case, and use them in every case.

</details>

### The refusal case fails on the side effect

<details><summary>Hint 1</summary>

How does your case say "no side effect", and how does the runner read it? Are they the same word?

</details>

<details><summary>Hint 2</summary>

Did anything else open a review for that exception, such as an earlier case run on the same one?

</details>

<details><summary>Hint 3</summary>

Check that each case gets a fresh exception, and that the word in the case matches the runner's.

</details>

### Your expectations don't match the run

<details><summary>Hint 1</summary>

Where did you take the kinds and events from: a trail, or your memory of the script?

</details>

<details><summary>Hint 2</summary>

Run the script again with the case's decision and print its trail.

</details>

<details><summary>Hint 3</summary>

Copy the kinds and the required events from the trail, in the order it shows them.

</details>

### You're not sure when to change the version

<details><summary>Hint 1</summary>

If two different sets shared one version, what would a passing result tell a reader?

</details>

<details><summary>Hint 2</summary>

Does tightening one expectation count as a change?

</details>

<details><summary>Hint 3</summary>

Write the rule at the top of the set file: any change to any case, or to the list of cases, changes the version.

</details>
