## Welcome to Psicotécnicos

# Ejercicio 1

## ¿Qué número se repite más veces?

<div class="row">
    <div class="column" id="matrix_col">c1</div>
    <div class="column" id="answers_col">c2</div>
 </div>

<script>

let numbers;
let repetitions;
let max;

do {
    numbers = generateArray();
    repetitions = countRepetitions(numbers);;
    max = getMaxRepetitions(repetitions);
    var isTie = isATie(repetitions,max);
} while(isTie);

let numberAnswer = getNumberAnswer(repetitions, max);

let answers = generateRandomWrongAnswer(numberAnswer);

let gridText = generateGridText(numbers);
document.getElementById("matrix_col").innerHTML = gridText;

let answersText = generateAnswersText(answers,numberAnswer);
document.getElementById("answers_col").innerHTML = answersText;

function generateArray() {
    var numbers = Array.from(Array(6), () => new Array(6));
    let repetitions = Array(10).fill(0);
    for (let i = 0; i < 5; i++) {
        for (let j = 0; j < 6; j++) {
            let num =  Math.floor(Math.random() * 10);
            numbers[i][j]=num;
        }
    }
return numbers;
}

function countRepetitions(numbers) {
    let repetitions = Array(10).fill(0);
    for (let i = 0; i < 5; i++) {
        for (let j = 0; j < 6; j++) {
            let num = numbers[i][j];
            repetitions[num]+=1;
        }
    }
    return repetitions;
}
function getMaxRepetitions(repetitions) {
    return  Math.max.apply(null, repetitions);
}

function isATie(repetitions,max) {
    return repetitions.filter(x => x==max).length !== 1;
}

function getNumberAnswer(repetitions, max) {
    let numberAnswer = 0;
    for (let i = 0; i < 10; i++) {
        if(repetitions[i] == max) {
            numberAnswer = i;
        }
    }
    return numberAnswer;
}

function shuffle(array) {
  let currentIndex = array.length,  randomIndex;

  // While there remain elements to shuffle...
  while (currentIndex != 0) {

    // Pick a remaining element...
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex--;

    // And swap it with the current element.
    [array[currentIndex], array[randomIndex]] = [
      array[randomIndex], array[currentIndex]];
  }

  return array;
}

function generateRandomWrongAnswer(correctAnswer) {
    //Generate 3 more wrong answer
    var answers = [];
    answers[0] = correctAnswer;
    while(answers.length < 4){
        var r = Math.floor(Math.random() * 10) ;
        if(answers.indexOf(r) === -1) answers.push(r);
    }
    let shuffled = shuffle(answers);
    return shuffled;
}
/*
function generateMatrixText(numbers) {
    let text = '';
    for (let i = 0; i < 5; i++) {
        for (let j = 0; j < 6  ; j++) {
            text+=numbers[i][j] + '  ';
        }
        text+='</br>'
    }
    return text;
}*/

function generateGridText(numbers) {
    let gridText = '';
    gridText+='<div id="grid">';
    for (let i = 0; i < 5; i++) {
        for (let j = 0; j < 6  ; j++) {
            gridText+='<div class="grid-item">' +numbers[i][j]  + '</div>';
        }
        text+='</br>'
    }
    gridText+='</div>';
    return gridText;
}

function generateAnswersText(answers, correctAnswer) {
    let answersText = '<form>';
    answersText+=generateOption(answers[0], correctAnswer,'A');
    answersText+=generateOption(answers[1],correctAnswer,'B');
    answersText+=generateOption(answers[2],correctAnswer,'C');
    answersText+=generateOption(answers[3],correctAnswer,'D');

    answersText+='</form> ';
    return answersText;
}

function generateOption(value, correctAnswer, letter) {
    let option = '';
    if(value == correctAnswer) {
        option= '<input class="answer" name="question_answers1" type="radio" data-correct="1" />';
    } else {
        option= '<input class="answer" name="question_answers1" type="radio" data-correct="0" />';
    }
    option+= ' <span><label for="'+value+'">' + letter + ' ) ' +value+'</label></span><br> ';
    return option;
}

</script>