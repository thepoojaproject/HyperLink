<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>URL Shortener</title>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, sans-serif;
}

body {
    height: 100vh;
    background: linear-gradient(135deg, #1d2671, #c33764);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    transition: 0.3s;
}

/* Dark mode */
body.dark {
    background: #121212;
}

.container {
    background: white;
    padding: 30px;
    width: 360px;
    border-radius: 14px;
    text-align: center;
    box-shadow: 0 12px 30px rgba(0,0,0,0.3);
}

body.dark .container {
    background: #1e1e1e;
    color: white;
}

h1 {
    margin-bottom: 10px;
}

p {
    font-size: 14px;
    color: #666;
}

body.dark p {
    color: #aaa;
}

input {
    width: 100%;
    padding: 12px;
    margin: 15px 0;
    border-radius: 8px;
    border: 1px solid #ccc;
}

button {
    width: 100%;
    padding: 12px;
    background: #1d2671;
    color: white;
    border: none;
    border-radius: 8px;
    font-size: 16px;
    cursor: pointer;
}

button:hover {
    background: #151b54;
}

.result {
    margin-top: 15px;
    background: #f3f3f3;
    padding: 10px;
    border-radius: 8px;
}

body.dark .result {
    background: #2a2a2a;
}

.result a {
    display: block;
    margin: 8px 0;
    color: #c33764;
    font-weight: bold;
    word-break: break-all;
    text-decoration: none;
}

.copy-btn {
    background: #c33764;
    margin-top: 5px;
}

/* Theme toggle */
.theme-toggle {
    position: fixed;
    top: 15px;
    right: 15px;
    width: auto;
    padding: 8px 12px;
    border-radius: 50px;
}

/* Footer */
footer {
    position: fixed;
    bottom: 15px;
    width: 100%;
    text-align: center;
    color: white;
    font-size: 14px;
}

footer span {
    color: #ff4d4d;
    animation: pulse 1.5s infinite;
}

@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.3); }
    100% { transform: scale(1); }
}
</style>
</head>

<body>

<button class="theme-toggle" onclick="toggleTheme()">🌙</button>

<div class="container">
    <h1>HyperLink</h1>
    <p>Paste your long URL</p>

    <input type="text" id="longUrl" placeholder="https://example.com">
    <button onclick="shortenUrl()">Shorten URL</button>

    <div class="result" id="result" style="display:none;">
        <span>Short URL:</span>
        <a id="shortUrl" href="#" target="_blank"></a>
        <button class="copy-btn" onclick="copyUrl()">Copy</button>
    </div>
</div>

<footer>
    Made in ❤ for Pooja
</footer>

<script>
async function shortenUrl() {
    const longUrl = document.getElementById("longUrl").value;
    const resultBox = document.getElementById("result");
    const shortUrlText = document.getElementById("shortUrl");

    if (!longUrl) {
        alert("Please enter a URL");
        return;
    }

    try {
        const response = await fetch(
            `https://tinyurl.com/api-create.php?url=${encodeURIComponent(longUrl)}`
        );

        const shortUrl = await response.text();

        shortUrlText.href = shortUrl;
        shortUrlText.textContent = shortUrl;
        resultBox.style.display = "block";
    } catch {
        alert("Error shortening URL");
    }
}

function copyUrl() {
    const text = document.getElementById("shortUrl").textContent;
    navigator.clipboard.writeText(text);
    alert("Copied to clipboard!");
}

function toggleTheme() {
    document.body.classList.toggle("dark");
}
</script>

</body>
</html>
