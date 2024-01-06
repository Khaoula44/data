<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Session Lookup</title>
    <style>
        /* Add your CSS styles here */
    </style>
</head>
<body>
    <h1>Session Lookup</h1>
    <label for="search">Enter Your Name:</label>
    <input type="text" id="search" oninput="searchSessions()">
    <div id="result"></div>

    <script>
        async function searchSessions() {
            const search = document.getElementById('search').value.toLowerCase();

            try {
                // Replace 'YOUR_GOOGLE_SHEETS_URL' with the URL of your Google Sheets
                const response = await fetch('[YOUR_GOOGLE_SHEETS_URL](https://docs.google.com/spreadsheets/d/1MMsIae7oOROWQiVZtiC8yfjMT18XiMllY7wR2ECgCMA/edit#gid=270340332)');
                const data = await response.json();

                const sessions = data.reduce((acc, row) => {
                    const [name, session] = row;
                    acc[name.toLowerCase()] = session;
                    return acc;
                }, {});

                const resultDiv = document.getElementById('result');
                const session = sessions[search];

                if (session) {
                    resultDiv.innerHTML = 'Your assigned session: ' + session;
                } else {
                    resultDiv.innerHTML = 'Name not found.';
                }
            } catch (error) {
                console.error('Error fetching data:', error);
            }
        }
    </script>
</body>
</html>
