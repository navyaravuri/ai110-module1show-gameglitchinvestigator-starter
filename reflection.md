# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?

The game just looked like a normal streamlit web application game to guess a number. But when I actually played it, I realised that the game has bugs.

- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
  
  1. I guessed the number 99, and it told me to guess higher. Then I guessed the number 100, and it told me to go lower. I realised there was something wrong with the logic, it was reversed.
  2. It also allowed me to guess a 4 digit number, and it showed 'go higher'.
  3. If I click new game, the input does not get refreshed, my previous guess still shows. 


---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?

  I used Copilot

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).

When I mentioned that the game logic was not correct, it suggested to keep secret as int and removed string conversion. It also enforced guess range during parsing.


- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

It incorrectly said that the hint messages in check_guess were reversed. They were actually correct" "Too High" resturns "Go Lower" and "Too Low" returns "Go Higher".
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?

After it gave the fix, I ran and tested it on streamlit before moving on.  
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.

  I ran 0 to see what it would give since it does not lie in the range 1-100. 

- Did AI help you design or understand any tests? How?

Yes, about testing it with a number that does not lie within 1-100. It made sure it only allows guesses within that range. 
---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.

It was being reassigned in multiple places. Reruns and changing the widget keys made the UI behave like the secret changed. There was also a type mixing bug made behaviour seem inconsistent it compared the int to a str.

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

In Streamlit, the whole script reruns every time the user interacts with the app, and st.session_state is how you save variables so they don't reset on each rerun.

- What change did you make that finally gave the game a stable secret number?

I only set st.session_state.secret in 2 places: once on first load and again only in the new game handler. I removed any code that converted or regenerated the secret during normal submit/reruns and kept the secret as an int. I also kept widget keys stable so reruns dont recreate widgets and cause implicit resets. 


---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or      projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.

  I will keep testing my code frequently and using debug outputs to quickly identify where logic errors occur.

- What is one thing you would do differently next time you work with AI on a coding task?

Next time I will review AI-generated code more carefully and test edge cases instead of assuming the code is correct.

- In one or two sentences, describe how this project changed the way you think about AI generated code.

This project showed me that AI-generated code can look correct but still contain subtle bugs, so it should always be treated as a starting point rather than a finished solution.
