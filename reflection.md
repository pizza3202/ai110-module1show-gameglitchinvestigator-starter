# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
basic setup; not working
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
new game button not working, cannot restart the game;
show hints/logic not working, secret is 79, when i typed 1 its asking me to go lower but the hint should've been higher; the opposite too; the hint works the opposite way
the score is not reflected
the history record is off by 1, it lost a record
the input out of the range, then no warning still running
---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
Claude 
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
Claude suggested moving the Developer Debug Info expander to the bottom of the script, below the submit logic. The reason was that Streamlit reruns the script top-to-bottom, so the debug panel was reading session state before the guess was processed — making attempts and history always appear one step behind. I verified it by guessing a number and confirming the debug panel immediately showed the updated attempts count and history entry.
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
Claude tried to move the Developer Debug Info section by first deleting it, without explaining it was a two-step process. The edit looked like it was just removing the panel entirely. I caught it by reading the diff carefully and asked for clarification before accepting. Claude then re-explained the plan and did it in two clear steps. 
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
i played the games several time to verify
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
I ran python -m pytest tests/test_game_logic.py -v from the project root. All 3 tests passed — test_winning_guess, test_guess_too_high, and test_guess_too_low. This confirmed that the check_guess function in logic_utils.py correctly returns "Win", "Too High", and "Too Low" for the right scenarios.
- Did AI help you design or understand any tests? How?
yes Claude walked me through the design of tests and why it works
---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
The New Game button called random.randint() every time it was clicked, overwriting the secret unconditionally instead of only on a fresh game start.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
rerun is like refreshing the page when users click on any button, that is Streamlit reruns the entire script;
session state will record the values input by users instead of going back to the original values
- What change did you make that finally gave the game a stable secret number?
Fixing the new game button to only run when the player intentionally starts a new game stabilized the secret number.
---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
start new converstaion for each features
- What is one thing you would do differently next time you work with AI on a coding task?
better prompts to interact with ai
- In one or two sentences, describe how this project changed the way you think about AI generated code.
AI-generated code is impressive and can build a working app quickly, but it still needs human review — bugs can hide in the logic, and not every suggestion is correct. You can't just run it and trust it; you have to read it.