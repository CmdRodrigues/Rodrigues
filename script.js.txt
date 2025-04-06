const quizData = [
    {
        question: "Quem foi o primeiro presidente do Brasil?",
        options: ["Getúlio Vargas", "Juscelino Kubitschek", "Deodoro da Fonseca", "Dom Pedro II"],
        answer: 2
    },
    {
        question: "Em que ano o Brasil proclamou a sua independência?",
        options: ["1822", "1831", "1889", "1500"],
        answer: 0
    },
    {
        question: "Onde foi a Batalha de Waterloo?",
        options: ["França", "Alemanha", "Bélgica", "Inglaterra"],
        answer: 2
    }
];

const quizContainer = document.getElementById('quiz');
const submitBtn = document.getElementById('submit-btn');
const resultContainer = document.getElementById('result');

function generateQuiz() {
    quizData.forEach((item, index) => {
        const questionElement = document.createElement('div');
        questionElement.classList.add('question');

        questionElement.innerHTML = `
            <p>${item.question}</p>
            ${item.options.map((option, i) => `
                <label>
                    <input type="radio" name="question${index}" value="${i}">
                    ${option}
                </label><br>
            `).join('')}
        `;
        quizContainer.appendChild(questionElement);
    });
}

function getQuizResult() {
    let score = 0;

    quizData.forEach((item, index) => {
        const userAnswer = document.querySelector(`input[name="question${index}"]:checked`);

        if (userAnswer && parseInt(userAnswer.value) === item.answer) {
            score++;
        }
    });

    resultContainer.textContent = `Você acertou ${score} de ${quizData.length} questões.`;
}

submitBtn.addEventListener('click', getQuizResult);

generateQuiz();
