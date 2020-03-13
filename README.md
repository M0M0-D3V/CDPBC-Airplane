# CDPBC-Airplane

<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<style type="text/css">
		#ocean {
			background-image: url("ocean.jpg");
			width: 900px;
			height: 700px;
		}
		.player {
			position: absolute;
			background-image: url("player.png");
			width: 70px;
			height: 75px;
		}
		.enemy {
			position: absolute;
			background-image: url("enemy.png");
			width: 70px;
			height: 75px;
		}
		.missile {
			position: absolute;
			background-color: red;
			width: 2px;
			height: 10px;
		}

	</style>

	<div id="ocean">
		<div id="players"></div>
		<div id="enemies"></div>
		<div id="missiles"></div>
	</div>



	<script type="text/javascript">


	var player = {
		left: 450,
		top: 620
	}

	var missile = {
		left: (player.left + 70) / 2,
		top: player.top - 10
	}

	var enemies = [
	{left: 150, top: 150},
	{left: 250, top: 200},
	{left: 350, top: 250},
	{left: 450, top: 250},
	{left: 550, top: 200},
	{left: 650, top: 150}	
	]

	function drawPlayer() {
		content = "<div class='player' style='left:" + player.left + "px; top:" + player.top + "px'></div>";

		document.getElementById("players").innerHTML = content;
	}

	function drawMissiles() { // push into empty array of missiles...
		content = "<div class='missile' style='left:" + missile.left + "px; top:" + missile.top + "px'></div>";
		document.getElementById("missiles").innerHTML = content;
	}

	function moveMissiles() {
		for(var m = 0; m < missiles.length; m++) {
			missiles[m].top -= 10;
		}
	}

	function drawEnemies() {
		content = "";
		for(var idx = 0; idx < enemies.length; idx++) {
			content += "<div class='enemy' style='left:" + enemies[idx].left + "px; top:" + enemies[idx].top + "px'></div>";
		}

		document.getElementById("enemies").innerHTML = content;
	}

	function moveEnemies() {
		for(var idx = 0; idx < enemies.length; idx++) {
			enemies[idx].top += 5;
		}
	}

	document.onkeydown = function(e) {
		console.log(e);
		if(e.keyCode == 37 && player.left > 0) { // left
				player.left -= 10;
		}
		if(e.keyCode == 39 && player.left < 830) { // right
				player.left += 10;
		}
		if(e.keyCode == 38 && player.top > 500) { // up
				player.top -= 10;	
		}
		if(e.keyCode == 40 && player.top < 625) { // down
				player.top += 10;
		}
		drawPlayer();
		if(e.keyCode == 32) { // spacebar
			drawMissiles();
		}
	}

	function gameLoop() {
		console.log("gameloop is running!");
		drawPlayer();

		moveEnemies();
		drawEnemies();
		setTimeout(gameLoop,100);
	}
	gameLoop();

	</script>
</body>
</html>
