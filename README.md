<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gaming Festival Anmeldung</title>
</head>
 <h1>Ziehe deine individuelle Nummer für das Gaming Festival</h1>
    <p>Klicke auf den Button, um deine individuelle Nummer zu erhalten:</p>

    <button id="generate-number">Nummer ziehen</button>
    <p id="ticket-number"></p>

    <script>
        document.getElementById('generate-number').addEventListener('click', function() {
            // Beispiel für das Generieren einer zufälligen Nummer
            const ticketNumber = Math.floor(1 + Math.random() * 20);
            
            // Zeige die Nummer dem Benutzer an
            document.getElementById('ticket-number').innerText = `Deine individuelle Nummer: ${ticketNumber}`;
            
            // Speichere die Nummer irgendwo ab (dies wird durch Backend-Integration gemacht)
            // Hier müsstest du einen Backend-Aufruf machen, um die Nummer zu speichern
            fetch('https://dein-backend-service.com/store-number', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({ ticketNumber }),
            }).then(response => response.json())
              .then(data => console.log('Nummer gespeichert:', data))
              .catch((error) => console.error('Fehler:', error));
        });
    </script>
    
 <p>Bestätige deine Teilnahme mit deiner individuellen Nummer:</p>

    <form id="confirmationForm" action="https://dein-backend-service.com/submit" method="POST">
        <label for="username">Dein Discord-Username:</label>
        <input type="text" id="username" name="username" required>
        <br><br>

        <label for="code">Deine individuelle Nummer:</label>
        <input type="text" id="code" name="code" required>
        <br><br>

        <button type="submit">Teilnahme bestätigen</button>
    </form>
    
    <script>
        document.getElementById('confirmationForm').addEventListener('submit', async function(event) {
            event.preventDefault();
            const formData = new FormData(this);
            const data = Object.fromEntries(formData.entries());

            try {
                const response = await fetch('https://dein-backend-service.com/submit', {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(data)
                });
                if (response.ok) {
                    alert('Teilnahme bestätigt!');
                } else {
                    alert('Fehler bei der Bestätigung.');
                }
            } catch (error) {
                console.error('Error:', error);
                alert('Ein Fehler ist aufgetreten.');
            }
        });
    </script>
    <iframe src="https://docs.google.com/forms/d/e/1FAIpQLSdcan_dB6Izymn8RJyGB13jGo8SrL65texwhgLUojhSb7gymQ/viewform?usp=sf_link" width="640" height="800" frameborder="0" marginheight="0" marginwidth="0">Wird geladen…</iframe>
</body>
</html>
