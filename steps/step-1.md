# Step 1: Write the three evaluation cases and version the set

## Your success case never opens a review

<details><summary>Hint 1</summary>

Which script does the case play? Does that script ever propose a tool call, or does it only finish?

</details>

<details><summary>Hint 2</summary>

Which of your scripts does `poe demo` play? Does that one reach the tool?

</details>

## Your recovery case has no `tool_failed`

<details><summary>Hint 1</summary>

Run the recovery script with approval and read its trail. Is there a failed call followed by one that opens a review?

</details>

<details><summary>Hint 2</summary>

If your recovery script stops after its first call, could a new recovery-shaped script with a second, valid call serve the case, so the tests that pin the old one keep passing?

</details>

## The refusal case fails on the side effect

<details><summary>Hint 1</summary>

How does your case say "no side effect", and how does the runner read it? Are they the same word?

</details>

## Your expectations don't match the run

<details><summary>Hint 1</summary>

Where did you take the kinds and events from: the trail you kept, or your memory of the script?

</details>
