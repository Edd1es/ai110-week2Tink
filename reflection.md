# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").

When I first ran the game it looked functional, but the behavior quickly felt inconsistent. The most obvious bug was that the hints were backwards. If I guessed too high, it told me to go higher, and if I guessed too low it told me to go lower. I also noticed that clicking New Game always reset the secret to a 1–100 range even if I selected Easy or Hard. The Hard difficulty range was also smaller than Normal, which made it easier instead of harder.

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

I used ChatGPT while reviewing and refactoring the code. One helpful suggestion was moving logic functions into logic_utils.py so they could be tested independently from Streamlit. That made it much easier to write pytest tests. One misleading suggestion was converting both the guess and secret to strings to avoid a TypeError. That would have preserved incorrect comparison behavior instead of fixing the root cause, so I rejected it.

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I confirmed the hint bug was fixed by manually testing guesses above and below the secret to ensure the correct message appeared. I also wrote pytest tests for check_guess and get_range_for_difficulty to verify expected behavior. The tests helped confirm that the hint logic and difficulty ranges were correct. AI helped generate an initial test structure, but I reviewed the assertions to make sure they matched the intended behavior.

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

The secret number changed because Streamlit reruns the script every time a user interacts with the UI. If values are not properly stored in st.session_state, they can reset unexpectedly. I fixed this by ensuring the secret number was generated using the selected difficulty range during New Game and properly stored in session state.

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

This project reinforced the importance of separating logic from UI so code can be tested independently. Writing pytest tests gave me confidence that my fixes actually worked. It also showed me that AI generated code can run without crashing but still contain serious logic flaws, so careful human review is necessary.
