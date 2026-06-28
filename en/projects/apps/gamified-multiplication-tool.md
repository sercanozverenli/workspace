# Gamified Multiplication Tool

A web and mobile-based gamification application developed with a focus on educational technology. Designed for primary school-level users, it eliminates rote memorization by making multiplication engaging and interactive.

### 🎮 Game Mechanics ("Who Am I?")

The application is built around an interactive reward system:

* **Difficulty Selection:** The user selects the difficulty level of the multiplication table they want to practice.

  ![Difficulty Selection](../../../docs/assets/gamified-multiplication-tool/multiplication_1.png ':size=35%')

* **Dynamic Question Pool & Error Checking:** Multiplication questions are presented in randomized order. When the "Who Am I?" button is clicked at the end of the test, a background algorithm checks all answers. If any errors are found, the user is notified and encouraged to find the correct answers.

  ![Question Screen & Error Checking](../../../docs/assets/gamified-multiplication-tool/multiplication_2.png ':size=35%')

* **Reward System:** Upon completing all questions without errors, the user is redirected to a special reward page revealing the identity of a hidden character drawn from a pool specific to the selected difficulty level.

  ![Reward Screen](../../../docs/assets/gamified-multiplication-tool/multiplication_3.png ':size=35%')

### Tech Stack

* **UI & Design:** HTML5, CSS3, Bootstrap 4.0
* **JavaScript Ecosystem & Game Engine:** Vanilla JS, jQuery 3.5.1, Fabric.js *(Application logic, DOM manipulations, and character management on the Canvas were integrated with the support of the GPT-3.5 AI assistant.)*
* **Mobile Deployment:** The HTML/JS architecture was converted into a distributable Android (`.apk`) build using APK Builder.

---

### Source Code & Installation

The web-based source code and compiled Android build are available at the links below:

**[GitHub Source Code](https://github.com/sercanozverenli/web_and_mobile_apps/tree/main/Gamified_Multiplication_Tool/HTML_Source)** <br>
**[Android APK File](https://github.com/sercanozverenli/web_and_mobile_apps/blob/main/Gamified_Multiplication_Tool/Android_Build/Gamified_Multiplication_Tool_1_1.0.apk)**

---

> <small>*⚠️ **Legal Notice & Disclaimer**<br> This project was developed solely for educational, research, and personal portfolio purposes with no commercial intent. All third-party materials that may appear within the project (images, audio, text, etc.) remain the intellectual property of their respective owners.*</small>
>
> <small>*Any third party who uses, reproduces, or integrates the project or its source code into their own work bears sole responsibility for complying with the applicable license and copyright requirements of those materials. The project developer accepts no legal liability for unauthorized commercial use, distribution, or any copyright infringement that may arise. Anyone using this project is deemed to have accepted these terms in advance.*</small>
