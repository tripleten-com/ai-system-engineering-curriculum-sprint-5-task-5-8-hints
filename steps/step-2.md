# Step 2: Build the command that runs every case

## The second case fails with `review_already_open`

<details><summary>Hint 1</summary>

Which exception does each case run on? Does each one get a fresh exception?

</details>

## A "no answer" case never finishes

<details><summary>Hint 1</summary>

What does a paused run do on its own when nobody answers? Does anything halt it?

</details>

<details><summary>Hint 2</summary>

How did the timeout row of your Task 6 check command end its run? Does your runner do the same?

</details>

## Changing an expectation makes the loader refuse the case

<details><summary>Hint 1</summary>

Which code reported the mismatch: the comparison, or the loader? The failure you want to see comes from comparing a run with a case.

</details>

<details><summary>Hint 2</summary>

Is there a field your loader doesn't enforce that you could change instead, so the run happens and the comparison names the mismatch?

</details>

## Adding a new event breaks every case

<details><summary>Hint 1</summary>

Does your comparison require the trail to equal a list, or require some events to appear in order?

</details>

## A case flips between pass and fail with no change

<details><summary>Hint 1</summary>

Does the runner read the result before the run has finished, or before the trail has been written? Where could timing enter?

</details>
