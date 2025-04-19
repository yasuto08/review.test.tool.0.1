<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>もみ徳 簡単口コミツール</title>
  <style>
    body {
      font-family: "Yu Mincho", "Hiragino Mincho ProN", serif;
      background: #fffaf4;
      padding: 2em 1em;
      margin: 0;
      color: #333;
    }
    .container {
      max-width: 680px;
      margin: auto;
      background: #ffffff;
      border: 8px double #d8b98c;
      border-radius: 12px;
      padding: 2em;
    }
    h1 {
      text-align: center;
      color: #7c4a1d;
      font-size: 1.8em;
    }
    .logo {
      display: flex;
      justify-content: center;
      margin-bottom: 1em;
    }
    .logo img {
      max-width: 120px;
    }
    label {
      display: block;
      margin-top: 1.2em;
      font-weight: bold;
    }
    select, textarea {
      width: 100%;
      font-size: 1em;
      padding: 0.5em;
      margin-top: 0.3em;
      border: 1px solid #bfa17c;
      border-radius: 4px;
      background: #fffefc;
    }
    textarea {
      height: 100px;
    }
    .checkbox-group {
      margin-top: 0.5em;
    }
    input[type="checkbox"] {
      margin-right: 0.5em;
    }
    .custom-btn-container {
      display: flex;
      justify-content: center;
      margin: 2em auto 1em;
    }
    .custom-btn-container img {
      width: 240px;
      border-radius: 6px;
      transition: opacity 0.2s ease;
    }
    .custom-btn-container img:hover {
      opacity: 0.9;
    }
    .output {
      background: #f9f1e7;
      padding: 1em;
      margin-top: 1.5em;
      border: 1px solid #d8b98c;
      border-radius: 6px;
      white-space: pre-line;
    }
    .note, .footer {
      text-align: center;
      font-size: 0.9em;
      color: #555;
      margin-top: 1em;
    }
    .footer a {
      color: #7c4a1d;
      text-decoration: none;
    }
    .footer a:hover {
      text-decoration: underline;
    }
    #reviewLinks a {
      display: block;
      margin-top: 0.5em;
      color: #6b4c2e;
      font-weight: bold;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="logo">
      <img src="https://github.com/yasuto08/review.test.tool/raw/main/%E3%82%82%E3%81%BF%E5%BE%B3%E3%83%AD%E3%82%B4.png" alt="もみ徳ロゴ" />
    </div>
    <h1>もみ徳 簡単口コミツール</h1>

    <label>担当セラピスト：
      <select id="therapist">
        <option>きださん</option>
        <option>高さん</option>
        <option>米倉さん</option>
      </select>
    </label>

    <label>施術コース：
      <select id="course">
        <option>もみほぐしコース</option>
        <option>足つぼセットコース</option>
        <option>ヘッド付きコース</option>
      </select>
    </label>

    <label>施術後に感じたこと（複数選択可）：
      <div class="checkbox-group">
        <input type="checkbox" value="コリに的確">コリに的確<br>
        <input type="checkbox" value="力強い">力強い<br>
        <input type="checkbox" value="動作が楽に">動作が楽に<br>
        <input type="checkbox" value="スッキリ">スッキリ<br>
        <input type="checkbox" value="丁寧な接客">丁寧な接客<br>
        <input type="checkbox" value="ワザが凄い">ワザが凄い<br>
      </div>
    </label>

    <label>コメント（任意）：
      <textarea id="comment" placeholder="とても気持ちよかったです！"></textarea>
    </label>

    <p style="text-align:center; margin-top:1em;">このボタンを押すと口コミが自動で生成されます。</p>
    <div class="custom-btn-container">
      <img src="https://github.com/yasuto08/review.test.tool/raw/main/%E5%8F%A3%E3%82%B3%E3%83%9F%E4%BD%9C%E6%88%90.png" alt="口コミ作成ボタン" onclick="generateText()" />
    </div>

    <div id="output" class="output" style="display: none;"></div>
    <button id="copyBtn" style="display:none;">コピー</button>

    <div id="reviewLinks" style="display:none;">
      <a href="https://www.google.com/gasearch?q=もみ徳姪浜店 福岡市 レビュー&source=sh/x/gs/m2/5#ebo=1" target="_blank">▶ iPhoneの方はこちら</a>
      <a href="https://www.google.com/search?q=もみ徳姪浜店　レビュー&sca_esv=d3079a9fd571ab97&hl=ja&sxsrf=AHTn8zryPjqF7_QbLGgMMskQnVmtfFoZKA:1745027450043#lrd=0x3541933fde3f26ad:0xd858787fee84e737,3" target="_blank">▶ Android／PCの方はこちら</a>
    </div>

    <p id="noteText" class="note" style="display:none;">
      ※ iPhoneをご利用の方は、リンク先でまず「★星をタップ」してからでないと口コミ入力欄が表示されない場合があります。
    </p>

    <div class="footer">
      <p><a href="https://momitoku.main.jp/" target="_blank">▶ もみ徳公式ホームページへ</a></p>
    </div>
  </div>

  <script>
    function generateText() {
      const name = document.getElementById('therapist').value;
      const course = document.getElementById('course').value;
      const comment = document.getElementById('comment').value;
      const feelings = Array.from(document.querySelectorAll('input[type=checkbox]:checked'))
        .map(cb => cb.value).join('、');

      let result = `${name}に${course}を施術していただきました。${feelings}と感じて、とても満足しています。`;
      if (comment.trim()) {
        result += `\n${comment.trim()}`;
      }

      document.getElementById('output').style.display = 'block';
      document.getElementById('output').textContent = result;
      document.getElementById('copyBtn').style.display = 'inline-block';
      document.getElementById('reviewLinks').style.display = 'block';
      document.getElementById('noteText').style.display = 'block';
    }

    document.getElementById('copyBtn').onclick = function () {
      const text = document.getElementById('output').textContent;
      navigator.clipboard.writeText(text).then(() => {
        alert(\"コピーしました！\");
      });
    };
  </script>
</body>
</html>
