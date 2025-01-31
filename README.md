<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Note Hacks</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
        }
        .header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background-color: blue;
            color: white;
            text-align: center;
            padding: 15px;
            font-size: 24px;
            font-weight: bold;
            z-index: 100;
        }
        .toolbar {
            width: 80px;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 10px;
            background: #f0f0f0;
            height: 100vh;
            position: fixed;
            top: 50px;
            left: 0;
            box-shadow: 2px 0 5px rgba(0, 0, 0, 0.2);
        }
        .toolbar button, .toolbar select, .toolbar input {
            margin: 10px 0;
            padding: 8px;
            cursor: pointer;
            border: none;
            background: white;
            border-radius: 5px;
            width: 40px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 16px;
        }
        .toolbar button:hover {
            background: lightgray;
        }
        .editor {
            width: calc(100% - 100px);
            margin: 80px auto 20px 100px;
            padding: 15px;
            min-height: 300px;
            background: white;
            border: 1px solid #ccc;
            outline: none;
        }
    </style>
</head>
<body>

    <div class="header">Note Hacks</div>

    <div class="toolbar">
        <button onclick="formatText('bold')"><b>B</b></button>
        <button onclick="formatText('italic')"><i>I</i></button>
        <button onclick="formatText('underline')"><u>U</u></button>
        <input type="color" id="colorPicker" onchange="changeColor()">
        
        <!-- Font Size Dropdown -->
        <select id="fontSize" onchange="changeFontSize()">
            <option value="5">5</option>
            <option value="10">10</option>
            <option value="15">15</option>
            <option value="20">20</option>
            <option value="25">25</option>
            <option value="30">30</option>
            <option value="35">35</option>
            <option value="40">40</option>
            <option value="45">45</option>
            <option value="50">50</option>
            <option value="60">60</option>
            <option value="70">70</option>
            <option value="80">80</option>
            <option value="90">90</option>
            <option value="100">100</option>
        </select>
    </div>

    <div contenteditable="true" class="editor" id="editor"></div>

    <script>
        function formatText(command) {
            document.execCommand(command, false, null);
        }

        function changeColor() {
            let color = document.getElementById("colorPicker").value;
            document.execCommand("foreColor", false, color);
        }

        function changeFontSize() {
            let size = document.getElementById("fontSize").value;
            document.execCommand("fontSize", false, "7");
            let fontElements = document.querySelectorAll("font[size='7']");
            fontElements.forEach(element => {
                element.removeAttribute("size");
                element.style.fontSize = size + "px";
            });
        }

        document.getElementById("editor").addEventListener("input", function() {
            localStorage.setItem("note", this.innerHTML);
        });

        window.onload = function() {
            document.getElementById("editor").innerHTML = localStorage.getItem("note") || "";
        };
    </script>

</body>
</html>
