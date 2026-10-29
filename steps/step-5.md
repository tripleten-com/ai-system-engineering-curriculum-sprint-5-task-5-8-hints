# Step 5: Prove it with tests and write the evidence note

## Your comparison tests need the stack

<details><summary>Hint 1</summary>

Is the comparison mixed into the code that starts runs? What would it take to call it with a plain object that stands for a run?

</details>

## Ignoring event order doesn't fail any test

<details><summary>Hint 1</summary>

Does any test give the comparison a run whose required events are present but out of order?

</details>

## The summary test passes with a wrong median

<details><summary>Hint 1</summary>

Do your fixed rows have an even or an odd count? Would a wrong median formula give a different answer on both?

</details>

## The classifier never returns `outside_authority`

<details><summary>Hint 1</summary>

Does any test send a well-formed tool call whose input falls outside your two lists?

</details>
