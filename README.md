<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>The Pressure Play: A Soccer Star's Dilemma</title>
  <style>
    body { font-family: Arial, sans-serif; background: #f4f4f4; padding: 20px; }
    #game { background: white; padding: 20px; border-radius: 10px; max-width: 600px; margin: auto; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    button { margin: 10px 0; display: block; }
    #health { font-weight: bold; }
  </style>
</head>
<body>
  <div id="game">
    <h1>The Pressure Play</h1>
    <p id="story">You're Jordan, a rising soccer star. Your coach and teammates are pushing you to take steroids to get an edge. What do you do?</p>
    <p>Health: <span id="health">100</span></p>
    <button onclick="choose('take')">Take the steroids</button>
    <button onclick="choose('refuse')">Refuse and train naturally</button>
  </div>

  <script>
    let health = 100;
    let stage = 0;

    function choose(option) {
      const story = document.getElementById('story');
      const healthDisplay = document.getElementById('health');
      if (stage === 0) {
        if (option === 'take') {
          health -= 20;
          story.innerText = "You take the steroids. You feel stronger quickly, but also more aggressive and anxious. You keep playing...";
          nextStage(['continueSteroids', 'stopSteroids']);
        } else {
          story.innerText = "You decide to stick to natural training. It's harder, but you feel proud. You keep working...";
          nextStage(['teamPressure', 'stayStrong']);
        }
      }
      healthDisplay.innerText = health;
    }

    function nextStage(options) {
      const game = document.getElementById('game');
      game.innerHTML += `<button onclick="next('${options[0]}')">${formatOption(options[0])}</button>`;
      game.innerHTML += `<button onclick="next('${options[1]}')">${formatOption(options[1])}</button>`;
    }

    function formatOption(opt) {
      const map = {
        continueSteroids: "Keep using steroids",
        stopSteroids: "Stop using steroids",
        teamPressure: "Give in to team pressure",
        stayStrong: "Stay strong and clean"
      };
      return map[opt] || opt;
    }

    function next(option) {
      const story = document.getElementById('story');
      const healthDisplay = document.getElementById('health');
      const game = document.getElementById('game');
      game.querySelectorAll('button').forEach(btn => btn.remove());

      if (option === 'continueSteroids') {
        health -= 25;
        story.innerText = "You continue using steroids. Eventually, you're caught in a drug test and banned from playing. You're left dealing with depression and regret.";
      } else if (option === 'stopSteroids') {
        health -= 10;
        story.innerText = "You stop the steroids, but the damage is done. You struggle with mood swings, but you're seeking help.";
      } else if (option === 'teamPressure') {
        health -= 15;
        story.innerText = "You give in to pressure and try steroids. Your performance goes up, but so does your anxiety. You feel trapped.";
      } else if (option === 'stayStrong') {
        story.innerText = "You stay clean and earn respect for your integrity. Your health and mental strength remain strong.";
      }

      healthDisplay.innerText = health;
    }
  </script>
</body>
</html>
