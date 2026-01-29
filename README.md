<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Music Player</title>
  <style>
    body {
      background: #121212;
      color: white;
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .player {
      background: #181818;
      padding: 20px;
      border-radius: 12px;
      width: 300px;
      text-align: center;
    }
    button {
      background: #1db954;
      border: none;
      color: white;
      padding: 10px 15px;
      margin: 5px;
      border-radius: 20px;
      cursor: pointer;
      font-size: 16px;
    }
    button:hover {
      opacity: 0.8;
    }
    input[type="range"] {
      width: 100%;
    }
  </style>
</head>
<body>

<div class="player">
  <h2 id="title">Bài hát</h2>

  <audio id="audio"></audio>

  <input type="range" id="progress" value="0">

  <div>
    <button onclick="prev()">⏮</button>
    <button onclick="playPause()">▶ / ⏸</button>
    <button onclick="next()">⏭</button>
  </div>
</div>

<script>
  const songs = [
    { name: "Nhạc 1", file: "song1.mp3" },
    { name: "Nhạc 2", file: "song2.mp3" }
  ];

  let index = 0;
  const audio = document.getElementById("audio");
  const title = document.getElementById("title");
  const progress = document.getElementById("progress");

  function loadSong(i) {
    title.innerText = songs[i].name;
    audio.src = songs[i].file;
  }

  loadSong(index);

  function playPause() {
    if (audio.paused) audio.play();
    else audio.pause();
  }

  function next() {
    index = (index + 1) % songs.length;
    loadSong(index);
    audio.play();
  }

  function prev() {
    index = (index - 1 + songs.length) % songs.length;
    loadSong(index);
    audio.play();
  }

  audio.addEventListener("timeupdate", () => {
    progress.value = (audio.currentTime / audio.duration) * 100 || 0;
  });

  progress.addEventListener("input", () => {
    audio.currentTime = (progress.value / 100) * audio.duration;
  });
</script

