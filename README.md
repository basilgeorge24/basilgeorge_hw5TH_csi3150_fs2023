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
### index.html

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
These section will display their contents dynamically from the JavaScript files. This is made possible using the DOM manipulation in the quizApp.js. The innerHTML attribute in the quizApp.js helps to achieve this.

### style.css

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

### questions.js

- **let questions = [{
}];**: this is an array of objects. Each object in the array represents a question.
- **numb**: indicates question number
- **question**: the question
- **answer**: the correct answer to the question
- **options**: an array containing of 4 options to choose from.








