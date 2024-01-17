---
toc: true
comments: true
layout: post
title: Tic Tac Toe
description: A simple game of tic tac toe where players alternate taking turns. It is played on a 3x3 board and the first to get three in a row wins either horizontally, vertically, or diagnally wins. If all spots are taken up without three in a row, then it is a draw.
type: hacks
courses: { compsci: {week: 2} }
---
<html>
<head>
  <style>
    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-gap: 2px;
    }
    .cell {
      width: 100px;
      height: 100px;
      border: 1px solid black;
      text-align: center;
      font-size: 24px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Tic Tac Toe</h1>
  <div class="board" id="board">
    <div class="cell" onclick="makeMove(0, 0)"></div>
    <div class="cell" onclick="makeMove(0, 1)"></div>
    <div class="cell" onclick="makeMove(0, 2)"></div>
    <div class="cell" onclick="makeMove(1, 0)"></div>
    <div class="cell" onclick="makeMove(1, 1)"></div>
    <div class="cell" onclick="makeMove(1, 2)"></div>
    <div class="cell" onclick="makeMove(2, 0)"></div>
    <div class="cell" onclick="makeMove(2, 1)"></div>
    <div class="cell" onclick="makeMove(2, 2)"></div>
  </div>
  <p id="status"></p>
  <script>
    let currentPlayer = 'X';
    let board = [
      ['', '', ''],
      ['', '', ''],
      ['', '', '']
    ];
    function makeMove(row, col) {
      if (board[row][col] === '' && !checkWinner()) {
        board[row][col] = currentPlayer;
        document.getElementById('board').children[row * 3 + col].textContent = currentPlayer;
        if (checkWinner()) {
          document.getElementById('status').textContent = `${currentPlayer} wins!`;
        } else if (boardIsFull()) {
          document.getElementById('status').textContent = "It's a draw!";
        } else {
          currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
          document.getElementById('status').textContent = `Current player: ${currentPlayer}`;
        }
      }
    }
    function checkWinner() {
      for (let i = 0; i < 3; i++) {
        if (board[i][0] === currentPlayer && board[i][1] === currentPlayer && board[i][2] === currentPlayer) {
          return true;
        }
        if (board[0][i] === currentPlayer && board[1][i] === currentPlayer && board[2][i] === currentPlayer) {
          return true;
        }
      }
      if (board[0][0] === currentPlayer && board[1][1] === currentPlayer && board[2][2] === currentPlayer) {
        return true;
      }
      if (board[0][2] === currentPlayer && board[1][1] === currentPlayer && board[2][0] === currentPlayer) {
        return true;
      }
      return false;
    }
    function boardIsFull() {
      for (let row = 0; row < 3; row++) {
        for (let col = 0; col < 3; col++) {
          if (board[row][col] === '') {
            return false;
          }
        }
      }
      return true;
    }
  </script>

  
</body>
</html>

