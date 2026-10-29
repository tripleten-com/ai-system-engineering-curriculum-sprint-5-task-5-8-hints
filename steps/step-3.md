# Step 3: Compare a hosted model with the emulator on a fixed request set

## Every hosted answer comes back malformed

<details><summary>Hint 1</summary>

Which fields does the contract require? Can a model know every one of them, such as how many tokens its answer used?

</details>

<details><summary>Hint 2</summary>

Where does the response report usage? Which fields should the request ask the model for, and which should your script fill in before the contract reads the answer?

</details>

<details><summary>Hint 3</summary>

Print one raw answer. Is it plain JSON, or wrapped in other text? What does your parser expect?

</details>

## The model proposes things your configuration doesn't allow

<details><summary>Hint 1</summary>

Read the procedure text you sent. Does it contain an instruction the model could follow?

</details>

<details><summary>Hint 2</summary>

Is that a malformed answer, or a well-formed one asking for something outside your authority? Which outcome does your row give it, and would your tool accept it?

</details>

## The script can't reach the endpoint

<details><summary>Hint 1</summary>

Did the failure happen before the first call, or in the middle of the set? The lesson treats those two differently.

</details>

<details><summary>Hint 2</summary>

Check the address and the model name against the lesson, and check that the key you read through the secret port is the one you stored. Never print the key to check it.

</details>

## Two answers look the same but tell the dispatcher different things

<details><summary>Hint 1</summary>

Does your row compare only the kinds? What about the reason and the tool input?

</details>

## The request sends personal data

<details><summary>Hint 1</summary>

Which function does the worker run on text before it reaches the model? Do you run the same one, at the same points?

</details>
