<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gaming Festival Teilnahmebestätigung</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
            text-align: center;
        }
        h1 {
            color: #333;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            margin: 10px;
            cursor: pointer;
            background-color: #5c67f2;
            color: white;
            border: none;
            border-radius: 5px;
        }
        button:hover {
            background-color: #4b54c2;
        }
        #ticket-number {
            font-size: 24px;
            margin: 20px 0;
            color: #333;
        }
        #qr-code {
            margin-top: 20px;
        }
        form {
            margin-top: 20px;
        }
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery.qrcode/1.0/jquery.qrcode.min.js"></script>
</head>
<body>

    <h1>Willkommen zum Gaming Festival!</h1>
    <p>Ziehe deine individuelle Ticketnummer und bestätige deine Teilnahme.</p>

    <button id="generate-number">Ticketnummer ziehen</button>
    <p id="ticket-number"></p>

    <div id="qr-code"></div>

    <form id="confirmation-form" style="display:none;">
        <h2>Teilnahmebestätigung</h2>
        <label for="confirmation-number">Gib deine Ticketnummer ein:</label>
        <input type="text" id="confirmation-number" required>
        <button type="submit">Teilnahme bestätigen</button>
    </form>

    <p id="confirmation-message"></p>

    <script>
        // Funktion zum Generieren einer Ticketnummer
        document.getElementById('generate-number').addEventListener('click', function() {
            // Generiere eine zufällige Ticketnummer
            const ticketNumber = Math.floor(100000 + Math.random() * 900000);

            // Zeige die Ticketnummer an
            document.getElementById('ticket-number').innerText = `Deine individuelle Ticketnummer: ${ticketNumber}`;

            // QR-Code generieren
            $('#qr-code').empty().qrcode({width: 128, height: 128, text: ticketNumber.toString()});

            // Speichere die Ticketnummer im LocalStorage
            localStorage.setItem('ticketNumber', ticketNumber);
            
            // Zeige das Bestätigungsformular an
            document.getElementById('confirmation-form').style.display = 'block';
        });

        // Teilnahmebestätigung
        document.getElementById('confirmation-form').addEventListener('submit', function(e) {
            e.preventDefault();
            const storedNumber = localStorage.getItem('ticketNumber');
            const confirmationNumber = document.getElementById('confirmation-number').value;

            if (confirmationNumber === storedNumber) {
                document.getElementById('confirmation-message').innerText = 'Danke für deine Teilnahmebestätigung!';
            } else {
                document.getElementById('confirmation-message').innerText = 'Die eingegebene Ticketnummer ist ungültig. Bitte versuche es erneut.';
            }
        });
    </script>

</body>
</html>
