# Interactive Quiz App (Exam Simulator)

A comprehensive exam simulator that consolidates multiple courses from the Computer Information Systems and Computer Programming curriculum (Data Structures, Unix System Administration, Mobile Application Development, etc.) under a single platform, enabling students to practice for midterms, finals, and unit assessments.

### ⚙️ System Mechanics & Features

The application is designed with an architecture that reduces cognitive load and reinforces learning:

* **Multi-Course & Category Selection:** Users select the relevant semester, the specific course they want to study, and the test type (Unit Test, Midterm, or Final) to access a targeted question pool.

  ![Semester and Course Selection](../../../docs/assets/interactive-quiz-app/int_quiz_1.PNG ':size=35%')  ![Subcategory Selection](../../../docs/assets/interactive-quiz-app/int_quiz_2.PNG ':size=35%')

* **Instant Feedback & Detailed Explanations:** Beyond the classic quiz format, the system responds immediately with color-coded feedback (Correct: Green, Incorrect: Red) when an answer is selected. An "Explanation" button below each question allows users to instantly review the reasoning behind the correct answer. Pagination (Part 1, Part 2) is included to facilitate navigation between test sections.

  ![Quiz Interface](../../../docs/assets/interactive-quiz-app/int_quiz_3.PNG ':size=35%')

* **Dark Mode Integration:** A fully integrated Dark Mode is included to prevent eye strain during extended study sessions. The user's theme preference is persisted via browser storage (`localStorage`) across page transitions.

  ![Dark Mode](../../../docs/assets/interactive-quiz-app/int_quiz_4.PNG ':size=35%')

* **Advanced Results Analysis (Modal):** Upon test completion, an algorithm calculates the user's performance and reports the number of correct, incorrect, and unanswered questions in a dynamic pop-up (modal) screen. Randomization algorithms ensure questions test understanding rather than memorization.

  ![Results Screen](../../../docs/assets/interactive-quiz-app/int_quiz_5.PNG ':size=35%')

### Tech Stack

* **UI & Design:** HTML5, CSS3, Bootstrap 4.5.2
* **Interaction, Logic & Mobile Deployment:** jQuery 3.5.1, Vanilla JS, LocalStorage, and APK Builder *(For all systems beyond UI and design — including question validation, theme switching, page filtering algorithms, in-memory data persistence, and Android `.apk` conversion — **ChatGPT 3.5** was used as an AI assistant.)*

---

### Source Code & Installation

The web-based source code and compiled Android build are available at the links below:

**[GitHub Source Code](https://github.com/sercanozverenli/web_and_mobile_apps/tree/main/Interactive_Quiz_App/HTML_Source)** <br>
**[Android APK File](https://github.com/sercanozverenli/web_and_mobile_apps/blob/main/Interactive_Quiz_App/Android_Build/Interactive_Quiz_App_1_1.0.apk)**

---

> <small>*⚠️ **Legal Notice & Disclaimer**<br> This project was developed solely for educational, research, and personal portfolio purposes with no commercial intent. All third-party materials that may appear within the project (images, audio, text, etc.) remain the intellectual property of their respective owners.*</small>
>
> <small>*Any third party who uses, reproduces, or integrates the project or its source code into their own work bears sole responsibility for complying with the applicable license and copyright requirements of those materials. The project developer accepts no legal liability for unauthorized commercial use, distribution, or any copyright infringement that may arise. Anyone using this project is deemed to have accepted these terms in advance.*</small>
