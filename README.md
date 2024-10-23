# Jogo-da-Mem-ria-
Jogo da Memória em Contabilidade
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo da Memória</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
        }
        .game-board {
            display: grid;
            grid-template-columns: repeat(4, 100px);
            grid-gap: 10px;
        }
        .card {
            width: 100px;
            height: 100px;
            background-color: #00f;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            color: white;
        }
        .flipped {
            background-color: #fff;
            color: #00f;
        }
    </style>
</head>
<body>
    <div class="game-board" id="gameBoard"></div>

    <script>
        const cards = ['A', 'B', 'C', 'D', 'A', 'B', 'C', 'D'];
        let firstCard = null;
        let secondCard = null;

        function shuffle(array) {
            return array.sort(() => Math.random() - 0.5);
        }

        function createBoard() {
            const gameBoard = document.getElementById('gameBoard');
            const shuffledCards = shuffle(cards);

            shuffledCards.forEach(card => {
                const cardElement = document.createElement('div');
                cardElement.classList.add('card');
                cardElement.dataset.value = card;
                cardElement.addEventListener('click', flipCard);
                gameBoard.appendChild(cardElement);
            });
        }

        function flipCard() {
            if (this.classList.contains('flipped')) return;

            this.classList.add('flipped');
            this.textContent = this.dataset.value;

            if (!firstCard) {
                firstCard = this;
            } else {
                secondCard = this;

                if (firstCard.dataset.value === secondCard.dataset.value) {
                    firstCard = null;
                    secondCard = null;
                } else {
                    setTimeout(() => {
                        firstCard.classList.remove('flipped');
                        firstCard.textContent = '';
                        secondCard.classList.remove('flipped');
                        secondCard.textContent = '';
                        firstCard = null;
                        secondCard = null;
                    }, 1000);
                }
            }
        }

        createBoard();
    </script>
</body>
</html>
