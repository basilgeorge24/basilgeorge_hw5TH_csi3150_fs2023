# Demo Quiz App (Take Home 5)

## Problem Statement
This is a quiz website implemented using HTML, CSS and Vanilla JavaScript. It asks the user 5 questions one after the other, and the user is expected to choose the right answer from the 4 given options per question. At the end of the quiz, the user is presented with the score indicating their performance.

## Functional Features of the App
- The quiz starts off with a 'Start Quiz' button which when clicked takes you to a Rules section. You then have two options, one to 'Exit Quiz' and one to 'Continue'.
- Clicking on 'Exit Quiz' takes you back to the Start Quiz button.
- Clicking on 'Continue' takes you to the first question. Each question has 4 choices from which the user must choose one. 
- If the user answers correctly, they gain a point and they can proceed to the next question. If the user answers incorrectly, the right answer is shown and they don't get a point. 
- Each question has a 15 second timer, within which if the user does not answer, the right answer is displayed and they dont get a point.
- After attempting all 5 questions, the user's total score is displayed along with the options to retake the quiz or to quit.

## Explanation of the Directory Structure/setup of the App
- This file has an index.html, which acts as the landing page of this demo quiz app. All HTML portion of the programming goes here. The CSS and JavaScript is also linked here. 
- It has a 'css' folder/directory, which consists of a css file called 'style.css'. This css file contains the styling rules for the demo quiz app. When the index.html is linked to this file, it applies the styling to whichever element is styled in the css.
- It has a 'js' folder/directory, which consists of 'questions.js' and 'quizApp.js'.
	- The 'questions.js' file contains each question, along with the options and the answer enclosed in an array of objects. 
	- The 'quizApp.js' contains the logic behind the quiz app.

## Explaination of the Codebase 
### 1. index.html

- *Lines 8-17:*
```
    <!-- CSS FILE -->
    <link rel="stylesheet" href="css/style.css">

    <!-- This is my personal font awesome kit code. you will have to add your own after you register with email-->
    <script src="https://kit.fontawesome.com/4a4f4b55b0.js" crossorigin="anonymous"></script>

     <!-- Add questions list -->
    <script src="js/questions.js" defer></script>

    <!-- Main logic of the app -->
    <script src="js/quizApp.js" defer></script>
```
This section is where you link your CSS, JS and a Font Awesome Kit for icons. The 'defer' is a boolean attribute and ensures that the script is executed after the HTML has finished parsing.

- *Lines 50-55*
```
  <div class="que_text">
     <!-- Insert questions from ./js/questions.js -->
  </div>
  <div class="option_list">
     <!-- Insert options to questions from ./js/questions.js -->
  </div>
```
- *Lines 60-62*
```
  <div class="total_que">
     <!-- insert Question Count Number dynamically from JavaScript App logic -->
  </div>
```
- *Lines 73-75*
```
<div class="score_text">
   <!-- insert dynamic user score as Result from JavaScript -->
</div>
```
These sections will display their contents dynamically from the JavaScript files. This is made possible using the DOM manipulation in the quizApp.js. The innerHTML attribute in the quizApp.js helps to achieve this.

### 2. style.css

- *Lines 14-17*
```
::selection {
  color: #fff;
  background: #a020f0;
}
```
This is a pseudo element that custimzes the appearance of selected text. 

- **activeInfo, activeQuiz, activeResult**: these classes control the visibility and interactivity of the info box, quiz box and the result box.

- **user-select: none**: this is a CSS property that prevents the user from selecting text on the web page. It disables the ability to highlight and copy the text within that element.
  
- **position: absolute and position: relative**: when an element is set to **position: absolute**, it takes the element out of the normal flow and positions it relative to its nearest positioned ancestor. **Position: relative** allows you to position an element relative to its normal position in the document flow and is often used as a container for absolutely positioned elements.

- **cursor: pointer**: this CSS property changes the appearance of the cursor when it hovers over the element. It will change the curson from the default arrow pointer to a hand icon, which means it is a clickable element.

- **pointer-events: none**: this CSS property effectively makes the element "invisible" to pointer events, meaning that it won't respond to clicks, hovers, or other interactions.

### 3. questions.js

- **let questions = [{
}];**: this is an array of objects. Each object in the array represents a question.
- **numb**: indicates question number
- **question**: the question
- **answer**: the correct answer to the question
- **options**: an array containing of 4 options to choose from.

### 4. quizApp.js

- *Lines 2-15*
```
const start_btn = document.querySelector(".start_btn button");
const info_box = document.querySelector(".info_box");
const exit_btn = info_box.querySelector(".buttons .quit");
const continue_btn = info_box.querySelector(".buttons .restart");
const quiz_box = document.querySelector(".quiz_box");
const result_box = document.querySelector(".result_box");
const restart_quiz = result_box.querySelector(".buttons .restart");
const quit_quiz = result_box.querySelector(".buttons .quit");
const option_list = document.querySelector(".option_list");
const time_line = document.querySelector("header .time_line");
const timeText = document.querySelector(".timer .time_left_txt");
const timeCount = document.querySelector(".timer .timer_sec");
const next_btn = document.querySelector("footer .next_btn");
const bottom_ques_counter = document.querySelector("footer .total_que");
```
In this section, we are selecting the various elements from the HTML document using 'document.querySelector()' and storing them in variables which have the datatype of const. These variables are then used in the JavaScript to do their specific needs.

- *Lines 18-35*
```
// if startQuiz button clicked
start_btn.addEventListener("click", (e) => {
  info_box.classList.add("activeInfo"); //show info box
});

// if exitQuiz button clicked
exit_btn.addEventListener("click", (e) => {
  info_box.classList.remove("activeInfo"); //hide info box
});

continue_btn.addEventListener("click", (e) => {
  info_box.classList.remove("activeInfo"); //hide info box
  quiz_box.classList.add("activeQuiz"); //show quiz box
  showQuetions(0); //calling showQestions function
  queCounter(1); //passing 1 parameter to queCounter
  startTimer(15); //calling startTimer function
  startTimerLine(0); //calling startTimerLine function
});
```
When the start_btn is clicked, this code makes the info_box element visible by adding the class "activeInfo" to it. This is done to display the rules of the quiz to the user before they start the quiz. 
When the exit_btn is clicked, this code hides the info_box element by removing the class "activeInfo" from it.
When the continue_btn is clicked, this code hides the info box, shows the quiz box, displays the questions, updates the question counter, starts a timer, and sets up a visual representation of the timer.

- *Lines 47-63*
```
restart_quiz.addEventListener("click", (e) => {
  quiz_box.classList.add("activeQuiz"); //show quiz box
  result_box.classList.remove("activeResult"); //hide result box
  timeValue = 15;
  que_count = 0;
  que_numb = 1;
  userScore = 0;
  widthValue = 0;
  showQuetions(que_count); //calling showQestions function
  queCounter(que_numb); //passing que_numb value to queCounter
  clearInterval(counter); //clear counter
  clearInterval(counterLine); //clear counterLine
  startTimer(timeValue); //calling startTimer function
  startTimerLine(widthValue); //calling startTimerLine function
  timeText.textContent = "Time Left"; //change the text of timeText to Time Left
  next_btn.classList.remove("show"); //hide the next button
});
```
When the restart_quiz button is clicked, this code resets various variables, hides the result box, shows the quiz box, displays the questions, updates the question counter, starts a timer, and sets up a visual representation of the timer. 

- *Lines 71-89*
```
next_btn.addEventListener("click", (e) => {
  //check if it does not exceed max questions
  if (que_count < questions.length - 1) {
    que_count++; //increment the que_count value
    que_numb++; //increment the que_numb value
    showQuetions(que_count); //calling showQestions function
    queCounter(que_numb); //passing que_numb value to queCounter
    clearInterval(counter); //clear counter
    clearInterval(counterLine); //clear counterLine
    startTimer(timeValue); //calling startTimer function
    startTimerLine(widthValue); //calling startTimerLine function
    timeText.textContent = "Time Left"; //change the timeText to Time Left
    next_btn.classList.remove("show"); //hide the next button
  } else {
    clearInterval(counter); //clear counter
    clearInterval(counterLine); //clear counterLine
    showResult(); //calling showResult function
  }
});
```
When the next_btn is clicked, this code checks if there are more questions to show. If yes, it increments the question count, updates questions, counters, timers, and hides the next button. If there are no more questions, it stops any ongoing timers and displays the quiz result.












