
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>Set Alarm</title>
	<style>
    



body {
    align-items: center;
    justify-content: center;
    display: flex;
     
  padding: 0;
  margin: 0;
}

#clock {
    border-radius: 20px;
    padding: 0px 20px;
    background-color: lavender;
    height:120px;
    font-size: 40px;
    font-family: arial;
    font-weight: bold;
    display: flex;
    justify-content: center;
    align-items: center;
  color: black;
}
#main-container{
    background-color: lightgoldenrodyellow;
margin-left: 40px;    
border: 2px solid black;
margin-top: 150px;
width: 60vw;
height: 60vh;
align-items: center;
justify-content: center;
display: flex;
}

h2 {
	text-align:center;
  

}

#alarm-container {
   justify-content: center;
	text-align:center;
    font-family: Verdana;
    font-size: 1em;
    padding: 0.7em;
  color: black;
}

label {
	display:inline-block;
}

.timeofday {
    background-color: #eee;
}

.bigger {
    font-weight:bold;
    font-size: 18px;
}

#sounds {
    text-align: center;
    padding-top: 20px;
}

#setButton {
    border-radius: 8px;
    width: 100px;
    float:left;
    background-color: #ddd;
    margin-top:10px;
}
#setButton:hover{
    background-color: #3e8e41;
  color: white;
  cursor: pointer;
}

#clearButton {
    border-radius: 8px;
    width: 100px;
    float:right;
    background-color:maroon;
    margin-top:10px;
}
#clearButton:hover{
    background-color:red;
  color: white;
  cursor: pointer;
}



  </style>
</head>
<body>



		<div id='main-container'>
			<h2 id='clock'></h2>
		

		<div id='alarm-container'>
			<h3>Set Alarm Time</h3>
				<label>
					<div>
					<select id='alarmhrs' ></select>
					</div>
				</label>
				<label>
					<div>
					<select id='alarmmins' ></select>
					</div>
				</label>
				<label>
					<div>
					<select id='alarmsecs' ></select>
					</div>
				</label>
				<label>
					<div>
						<select id="ampm">
							<option value="AM">AM</option>
							<option value="PM">PM</option>
						</select>
					</div>
				</label>
		</div>
		

		<div id='buttonHolder'>
			<div>
				<button  id='setButton' onClick='alarmSet()'>Set Alarm</button>
			</div>

			<div>
				<button  id='clearButton' onClick='alarmClear()'>Clear Alarm</button>
			</div>
		</div>
	</div>

	<script >
		

var sound = new Audio("https://www.freespecialeffects.co.uk/soundfx/animals/duck1.wav");
		sound.loop = true;

var h2 = document.getElementById('clock');

// display current time by the second
var currentTime = setInterval(function(){
	var date = new Date();
	
	var hours = (12 - (date.getHours()));
	// var hours = date.getHours();
	
	var minutes = date.getMinutes();
	
	var seconds = date.getSeconds();
	
	var ampm = (date.getHours()) < 12 ? 'AM' : 'PM';


	//convert military time to standard time

	if (hours < 0) {
		hours = hours * -1;
	} else if (hours == 00) {
		hours = 12;
	} else {
		hours = hours;
	}

	
	h2.textContent = addZero(hours) + ":" + addZero(minutes) + ":" + addZero(seconds) + "" + ampm;
	
},1000);


/*functions to get hour, min, secs, 
  am or pm, add zero, set alarm time and sound, clear alarm
*/

function addZero(time) {

		return (time < 10) ? "0" + time : time;
	
}

function hoursMenu(){

	var select = document.getElementById('alarmhrs');
	var hrs = 12

	for (i=1; i <= hrs; i++) {
		select.options[select.options.length] = new Option( i < 10 ? "0" + i : i, i);
		
	}
}
hoursMenu();

function minMenu(){

	var select = document.getElementById('alarmmins');
	var min = 59;

	for (i=0; i <= min; i++) {
		select.options[select.options.length] = new Option(i < 10 ? "0" + i : i, i);
	}
}
minMenu();

function secMenu(){

	var select = document.getElementById('alarmsecs');
	var sec = 59;

	for (i=0; i <= sec; i++) {
		select.options[select.options.length] = new Option(i < 10 ? "0" + i : i, i);
	}
}
secMenu();


function alarmSet() {

	var hr = document.getElementById('alarmhrs');
	
	var min = document.getElementById('alarmmins');
	
	var sec = document.getElementById('alarmsecs');
	
	var ap = document.getElementById('ampm');
    

    var selectedHour = hr.options[hr.selectedIndex].value;
    var selectedMin = min.options[min.selectedIndex].value;
    var selectedSec = sec.options[sec.selectedIndex].value;
    var selectedAP = ap.options[ap.selectedIndex].value;

    var alarmTime = addZero(selectedHour) + ":" + addZero(selectedMin) + ":" + addZero(selectedSec) + selectedAP;
    console.log('alarmTime:' + alarmTime);

    document.getElementById('alarmhrs').disabled = true;
	document.getElementById('alarmmins').disabled = true;
	document.getElementById('alarmsecs').disabled = true;
	document.getElementById('ampm').disabled = true;


//when alarmtime is equal to currenttime then play a sound
	var h2 = document.getElementById('clock');

/*function to calcutate the current time 
then compare it to the alarmtime and play a sound when they are equal
*/

setInterval(function(){

	var date = new Date();
	
	var hours = (12 - (date.getHours()));
	// var hours = date.getHours();
	
	var minutes = date.getMinutes();
	
	var seconds = date.getSeconds();
	
	var ampm = (date.getHours()) < 12 ? 'AM' : 'PM';


	//convert military time to standard time

	if (hours < 0) {
		hours = hours * -1;
	} else if (hours == 00) {
		hours = 12;
	} else {
		hours = hours;
	}
	
	var currentTime = h2.textContent = addZero(hours) + ":" + addZero(minutes) + ":" + addZero(seconds) + "" + ampm;
	

	if (alarmTime == currentTime) {
		sound.play();
		}

},1000);


	// console.log('currentTime:' + currentTime);	

}


function alarmClear() {

	document.getElementById('alarmhrs').disabled = false;
	document.getElementById('alarmmins').disabled = false;
	document.getElementById('alarmsecs').disabled = false;
	document.getElementById('ampm').disabled = false;
	sound.pause();
}



	</script>

</body>
</html>
