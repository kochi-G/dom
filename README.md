# dom
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        header{
            height: 100px;
            background-color: green;
            text-align: center;
        }
        footer {
            background-color: green;
            text-align: center;
        }
        #game {
            margin-left: 50px;
        }

    </style>
</head>
<body>
    <header>
        <h1>თამაში "more or less"</h1>
    </header>
    <section>
        <div id="game">
            <img src="images/back.png"  class="first">
            <img src="images/back.png"  class="imges">
            <img src="images/back.png"  class="imges">
            <img src="images/back.png"  class="imges">
            <img src="images/back.png"  class="imges">
        </div>
            <br><br>
            <button class="chance">კოჭის გამოცვლა</button>
            <button class="high" >მაღალი</button>
            <button class="low" >დაბალი</button>
            <p class="result">შედეგი:</p>
    </section>
    <footer>
        <p>ყველა უფლება დაცულია &copy2023</p>
    </footer>

    <script>
        let randFirst,randSecond,saver;
        let first = document.querySelector('.first');
        let dice = document.querySelector('.chance');
        let photos = document.querySelectorAll('.imges');
        let low = document.querySelector('.low');
        let high = document.querySelector('.high');
        let result = document.querySelector('.result');
        let Rfirst,Rsecond; // მაღალი-დაბალის გამოსაცნობად;
        let chance = 0,i = 0;

        randFirst = Math.floor(7 * Math.random());
        randSecond = Math.floor(7 * Math.random());
        if(randFirst > randSecond) { // 0-3 3-0
            saver = randFirst;
            randFirst = randSecond;
            randSecond = saver;
        }
        first.src = `images/${randFirst}-${randSecond}.png`;
        
        dice.addEventListener('click', function() {
            if(chance === 0) {
                randFirst = Math.floor(7 * Math.random());
                randSecond = Math.floor(7 * Math.random());
                if(randFirst > randSecond) { // 0-3 3-0
                    saver = randFirst;
                    randFirst = randSecond;
                    randSecond = saver;
                }
                first.src = `images/${randFirst}-${randSecond}.png`;
                chance = 1;
                dice.disabled = true;//ფუნქცია
            }
        });
        low.addEventListener('click', function() {
            Rfirst = Math.floor(7 * Math.random());
            Rsecond = Math.floor(7 * Math.random());
            if(Rfirst > Rsecond) {
                saver = Rfirst;
                Rfirst = Rsecond;
                Rsecond = saver;
            }
            if(randFirst + randSecond < Rfirst + Rsecond) gameOver();
                else {
                    result.textContent = `არის დაბალი`;
                    randFirst = Rfirst;
                    randSecond = Rsecond;
                }
            photos[i].src = `images/${Rfirst}-${Rsecond}.png`;
            i++;
            if(i === 4) gameOver();
        })
        high.addEventListener('click', function() {
            Rfirst = Math.floor(7 * Math.random());
            Rsecond = Math.floor(7 * Math.random());
            if(Rfirst > Rsecond) {
                saver = Rfirst;
                Rfirst = Rsecond;
                Rsecond = saver;
            }
            if(randFirst + randSecond > Rfirst + Rsecond) gameOver();
            else {
                    result.textContent = `არის მაღალი`;
                    randFirst = Rfirst;
                    randSecond = Rsecond;
                }
            photos[i].src = `images/${Rfirst}-${Rsecond}.png`;
            i++;
            if(i === 4) gameOver();
        })
        function gameOver(){
            low.disabled = true;
            high.disabled = true;
            dice.disabled = true;
            if(i === 4) result.textContent = `თქვენ მოიგეთ`;
                else result.textContent = `არ არის სწორი`;
        }
    </script>
</body>
</html>
