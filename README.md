# AI-Powered-Password-Cracker-Detector
Crack Alert

Hey, I’m Raj—Master’s in Info Systems and Security, cybersecurity junkie. This project flips my Password Cracking Project on its head. Instead of cracking with Hashcat, I built an AI to spot when someone’s trying to crack my passwords—like catching a thief in the act.

What’s the Big Idea?

Hackers hammer systems with password guesses—think “password123” a million times. This AI watches login attempts and flags the shady ones, learning from patterns I’ve seen with tools like John the Ripper.

How I Made It Happen

Here’s the scoop, real talk:

Log Attempts: Simulated logins—like “user: raj, pass: 123” vs. “user: raj, pass: abc, xyz, qwe” fast.
Example: Normal: 1 try. Attack: 10 tries in 2 seconds.

Shape the Data: Turned logs into numbers—attempt count, time gaps. Like “5 tries, 0.1 sec apart.” Macro Detail: Used “pandas” to line it up nice.

Train the AI: Fed it normal logins (me signing in) vs. attack data (mimicked with a script). 

Example: 1 try/hour = safe; 100 tries/min = cracker! Macro Detail: “Logistic Regression”—simple but sharp for yes/no calls.

Spot the Attack: New logs come in—AI says, “Yo, this ain’t right!” Example: “10 tries in 5 sec—Alert!”


Stuff You’ll Need

Python: python.org—my go-to.


Helpers:

scikit-learn—AI juice.
pandas—data handler. Your Computer: No server needed—just your rig.



Let’s Build It—Step by Step with Commands

Install Python: python.org, 3.11, “Add to PATH” checked. Command: “python --version”—expect “3.11.x”.

Get Helpers: Command line, type:
“pip install scikit-learn” (AI bits).
“pip install pandas” (data pal).


Set Up Folder: Make “PassCrackDetector” on desktop. Command: “cd Desktop\PassCrackDetector” (Windows) or “cd ~/Desktop/PassCrackDetector” (Mac).

Fake Logs: In Notepad, save this as “logs.csv”:

text
tries,time_gap
1,10
5,0.1
2,5
(1 try, 10 sec = normal; 5 tries, 0.1 sec = attack)

Code It: Notepad, paste this, save as “crack_detector.py”:


python

# My AI crack spotter
import pandas as pd
from sklearn.linear_model import LogisticRegression

# Load logs
logs = pd.read_csv("logs.csv")
labels = [0, 1, 0]  # 0 = safe, 1 = attack—add more!

# Train AI
model = LogisticRegression()
model.fit(logs[["tries", "time_gap"]], labels)

# Test new log
new_log = pd.DataFrame([[10, 0.5]], columns=["tries", "time_gap"])  # 10 tries, 0.5 sec
pred = model.predict(new_log)
if pred[0] == 1:
    print("Alert! Someone’s cracking passwords!")
else:
    print("All good—normal login.")

    
Run It: Command line, “python crack_detector.py”—watch it catch the fake attack!
Bumps in the Road

Tiny Logs: 3 lines ain’t enough—add 20+ for real smarts.
Real Data: Simulate more attacks—script it if you can.
Tweak It: Too sensitive? Adjust the model later.

Why I Love It

Flips my Hashcat skills into defense—AI’s got my back. Perfect for my auditing passion.
