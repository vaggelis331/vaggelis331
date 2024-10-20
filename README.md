<!DOCTYPE html>
<html lang="el">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Πίσω από τη Μάσκα</title>
    <style>
        body {
            background-color: #1e3a8a;
            color: white;
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
        }

        header {
            text-align: center;
            padding: 20px;
            background-color: #23395d;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        header h1 {
            font-size: 2.5em;
            margin: 0;
            letter-spacing: 2px;
        }

        .password-container {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #1e3a8a;
        }

        .password-box {
            text-align: center;
            background-color: #23395d;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
        }

        .password-box input {
            padding: 10px;
            border: none;
            border-radius: 5px;
            margin-bottom: 10px;
            width: 200px;
            text-align: center;
            font-size: 1em;
        }

        .password-box button {
            background-color: #4caf50;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1.2em;
        }

        .password-box button:hover {
            background-color: #45a049;
        }

        .error {
            color: red;
            margin-top: 10px;
        }

        .hidden {
            display: none;
        }

        .video-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin: 20px auto;
            max-width: 1200px;
        }

        .video {
            margin: 15px;
            background-color: #29487d;
            padding: 10px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease;
            width: 300px;
        }

        .video:hover {
            transform: scale(1.05);
        }

        video {
            width: 100%;
            height: 170px;
            border-radius: 8px;
        }

        .upload-container {
            text-align: center;
            margin: 40px 0;
        }

        .upload-btn {
            background-color: #4f83cc;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1.2em;
            transition: background-color 0.3s ease;
        }

        .upload-btn:hover {
            background-color: #3a64a7;
        }

        .caption-input {
            width: 100%;
            padding: 5px;
            margin: 10px 0;
            border-radius: 5px;
            border: 1px solid #ccc;
            font-size: 1em;
        }

        .save-caption-btn {
            background-color: #4caf50;
            color: white;
            padding: 5px 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1em;
            margin-top: 5px;
        }

        .save-caption-btn:hover {
            background-color: #45a049;
        }

        .caption {
            margin-top: 10px;
            font-size: 1.1em;
            color: #fff;
        }

    </style>
</head>
<body>

    <!-- Περιοχή για τον κωδικό πρόσβασης -->
    <div class="password-container" id="passwordContainer">
        <div class="password-box">
            <h2>Εισάγετε τον κωδικό πρόσβασης</h2>
            <input type="password" id="passwordInput" placeholder="Κωδικός...">
            <button onclick="checkPassword()">Είσοδος</button>
            <div class="error hidden" id="errorMessage">Λάθος κωδικός, δοκιμάστε ξανά.</div>
        </div>
    </div>

    <!-- Κεφαλίδα της σελίδας -->
    <header id="mainContent" class="hidden">
        <h1>Πίσω από τη Μάσκα</h1>
    </header>

    <!-- Περιοχή για ανέβασμα βίντεο -->
    <div class="upload-container hidden" id="uploadContainer">
        <input type="file" id="videoUpload" class="upload-btn" accept="video/*" multiple>
    </div>

    <!-- Περιοχή για την εμφάνιση των βίντεο -->
    <div class="video-container hidden" id="videoContainer">
        <!-- Τα βίντεο θα προστεθούν εδώ δυναμικά -->
    </div>

    <script>
        // Έλεγχος του κωδικού πρόσβασης
        function checkPassword() {
            const passwordInput = document.getElementById('passwordInput').value;
            const errorMessage = document.getElementById('errorMessage');
            const correctPassword = '1234';

            if (passwordInput === correctPassword) {
                // Αν ο κωδικός είναι σωστός, εμφανίζουμε το περιεχόμενο
                document.getElementById('passwordContainer').style.display = 'none';
                document.getElementById('mainContent').classList.remove('hidden');
                document.getElementById('uploadContainer').classList.remove('hidden');
                document.getElementById('videoContainer').classList.remove('hidden');
            } else {
                // Αν είναι λάθος, εμφανίζουμε μήνυμα σφάλματος
                errorMessage.classList.remove('hidden');
            }
        }

        // Επιλέγουμε το input και το container για τα βίντεο
        const videoUpload = document.getElementById('videoUpload');
        const videoContainer = document.getElementById('videoContainer');

        // Όταν ο χρήστης ανεβάζει βίντεο
        videoUpload.addEventListener('change', function(event) {
            const files = event.target.files;

            // Για κάθε βίντεο που ανεβαίνει, το προσθέτουμε στο videoContainer
            for (let i = 0; i < files.length; i++) {
                const file = files[i];
                const videoUrl = URL.createObjectURL(file);

                // Δημιουργούμε ένα νέο div για το κάθε βίντεο
                const videoDiv = document.createElement('div');
                videoDiv.classList.add('video');

                // Δημιουργούμε το στοιχείο του βίντεο
                const videoElement = document.createElement('video');
                videoElement.src = videoUrl;
                videoElement.controls = true;

                // Δημιουργούμε το input για τη λεζάντα
                const captionInput = document.createElement('input');
                captionInput.classList.add('caption-input');
                captionInput.type = 'text';
                captionInput.placeholder = 'Γράψε τη λεζάντα εδώ...';

                // Δημιουργούμε το κουμπί αποθήκευσης λεζάντας
                const saveCaptionBtn = document.createElement('button');
                saveCaptionBtn.classList.add('save-caption-btn');
                saveCaptionBtn.textContent = 'Αποθήκευση Λεζάντας';

                // Δημιουργούμε το div που θα εμφανίσει τη λεζάντα
                const captionDisplay = document.createElement('div');
                captionDisplay.classList.add('caption');

                // Όταν ο χρήστης πατάει το κουμπί αποθήκευσης
                saveCaptionBtn.addEventListener('click', function() {
                    const captionText = captionInput.value.trim();
                    if (captionText) {
                        captionDisplay.textContent = captionText; // Εμφανίζουμε τη λεζάντα
                        captionInput.style.display = 'none'; // Κρύβουμε το input
                        saveCaptionBtn.style.display = 'none'; // Κρύβουμε το κουμπί αποθήκευσης
                    }
                });

                // Προσθέτουμε το βίντεο, το input, το κουμπί και τη λεζάντα στο divvideoDiv.appendChild(videoElement);
                videoDiv.appendChild(captionInput);
                videoDiv.appendChild(saveCaptionBtn);
                videoDiv.appendChild(captionDisplay);

                // Προσθέτουμε το νέο div με το βίντεο στο container
                videoContainer.appendChild(videoDiv);
            }
        });
    </script>
</body>
</html>
