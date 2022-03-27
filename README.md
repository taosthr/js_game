# js_game

1/ tu vas créer 3 fichier 
- index.html
- script.js
- style.css

2/ dans index.html nous allons lié les fichier entre eux 
en ajoutant le lien pour js  ```<script src="script.js"></script> ``` et le lien pour le css dans la partie head ```<link rel="stylesheet" href="style.css">```

mettre ça 
```
<!DOCTYPE html>

<html lang="en" onclick="jump()">

<head>

<meta charset="UTF-8">

<title>Jump Game</title>

<link rel="stylesheet" href="style.css">

</head>

<body>

<div class="game">

<div id="character"></div>

<div id="block"></div>

</div>

<p>Score: <span id="scoreSpan"></span></p>

</body>

<script src="script.js"></script>

</html>
```

2/ créer 3 div 1er pour l'ensemble du jeux 2e pour le personnage et le 3e pour le bloc

mets ces lignes dans le body de index.html

```
<div id="game">

<div id="character"></div>

<div id ="block"></div>

</div>
```


3/ mettant on va s'attaquer au fichier css

ajouter les bases pour se debarasser des ajouts par défauts  du body:

```
*{

padding: 0;

margin: 0;

}
```

on va créer un carré lié au div game

```
#game{

width: 500px;

height: 200px;

border: 1px solid black;

}
```

puis une boite qui sera notre charatere ( lié au div character)

```
#character{

width: 20px;

height: 50px;

background-color: blue;

position: relative;

top: 150px;

}
```

et pour finir on va positionner le bloc ( ilé au div block)

  ```

#block{

width: 20px;

height: 20px;

background-color: red;

position: relative;

top: 130px;

left: 480px;

  

}
```


maintenant on va créer une animation pour faire glisser le bloc 

ajoute ces lines au fichier css
```
@keyframes block {

0%{left: 480px;}

100% {left: -40px;}

}
```

et ajoute cette ligne au ```#block```
```
animation: block 1s infinite linear;
```


maintenant on va faire une animation pour le charactere pour qu'il puisse sauter
```
@keyframes jump{

0%{top: 150px;}

30%{top: 100px;}

70%{top: 100px;}

100%{top: 150px;}

}
```

et on ajoute cette ligne au ```#character ```

```
animation: jump 500ms ;
```


maintenant on va utiliser notre fichier javascript on va créer 2 variables pour avoir acces au charactere et bloc
```
var character = document.getElementById("character");

var block = document.getElementById("block")
```

maintenant on va créer notre fonction jump
```
function jump () {

character.classList.add("animate");

}
```

et on ajoute dans le fichier index.html  à la ligne 2 ```<html lang="en"``` ceci 
```onclick="jump()```
pour obtenir ça ```<html lang="en" onclick="jump()">```


on va additioner ces elements à notre fichier js pour permet le saut du charactere
```
var character = document.getElementById("character");

var block = document.getElementById("block");

var counter=0;

function jump(){

if(character.classList == "animate"){return}

character.classList.add("animate");

setTimeout(function(){

character.classList.remove("animate");

},300);

}
```


maintenant on ajoute une function pour indiquer si on à perdu ou gagner
```
var checkDead = setInterval(function() {

let characterTop = parseInt(window.getComputedStyle(character).getPropertyValue("top"));

let blockLeft = parseInt(window.getComputedStyle(block).getPropertyValue("left"));

if(blockLeft<20 && blockLeft>-20 && characterTop>=130){

block.style.animation = "none";

alert("Game Over. score: "+Math.floor(counter/100));

counter=0;

block.style.animation = "block 1s infinite linear";

}else{

counter++;

document.getElementById("scoreSpan").innerHTML = Math.floor(counter/100);

}

}, 10);
```

on va ajouter une pop up  qui annonce que l'on a perdu
dans index.html
```
<p>Score: <span id="scoreSpan"></span></p>
```


dans le fichier css
```
p{

text-align: center;

}
```
