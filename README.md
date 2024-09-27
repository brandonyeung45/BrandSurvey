
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Web Form Questionnaire</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 600px;
            margin: auto;
            background: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        label {
            display: block;
            margin: 15px 0 5px;
            font-weight: bold;
        }
        input[type="text"], input[type="email"], textarea, select {
            width: 100%;
            padding: 10px;
            margin: 5px 0 15px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        input[type="radio"], input[type="checkbox"] {
            margin-right: 10px;
        }
        button {
            background-color: #5c67f2;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #4b52c7;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Feedback Questionnaire</h1>
        <form id="questionnaireForm">
            <label for="name">Name:</label>
            <input type="text" id="name" name="name" required>

            <label for="email">Email:</label>
            <input type="email" id="email" name="email" required>

            <label for="age">Age:</label>
            <select id="age" name="age" required>
                <option value="">Select Age Range</option>
                <option value="18-25">18-25</option>
                <option value="26-35">26-35</option>
                <option value="36-45">36-45</option>
                <option value="46+">46+</option>
            </select>

            <label>Gender:</label>
            <input type="radio" id="male" name="gender" value="Male" required>
            <label for="male">Male</label>
            <input type="radio" id="female" name="gender" value="Female" required>
            <label for="female">Female</label>

            <label for="satisfaction">How satisfied are you with our service?</label>
            <select id="satisfaction" name="satisfaction" required>
                <option value="">Select</option>
                <option value="Very Satisfied">Very Satisfied</option>
                <option value="Satisfied">Satisfied</option>
                <option value="Neutral">Neutral</option>
                <option value="Dissatisfied">Dissatisfied</option>
                <option value="Very Dissatisfied">Very Dissatisfied</option>
            </select>

            <label>What services have you used? (Select all that apply)</label>
            <input type="checkbox" id="service1" name="services" value="Service 1">
            <label for="service1">Service 1</label>
            <input type="checkbox" id="service2" name="services" value="Service 2">
            <label for="service2">Service 2</label>
            <input type="checkbox" id="service3" name="services" value="Service 3">
            <label for="service3">Service 3</label>

            <label for="comments">Additional Comments:</label>
            <textarea id="comments" name="comments" rows="4"></textarea>

            <button type="submit">Submit</button>
        </form>
    </div>
    <script>
        // Function to load saved data from local storage
        function loadSavedData() {
            const savedData = JSON.parse(localStorage.getItem('userData'));
            if (savedData) {
                document.getElementById('name').value = savedData.name || '';
                document.getElementById('email').value = savedData.email || '';
                document.getElementById('age').value = savedData.age || '';
                if (savedData.gender) {
                    document.querySelector(`input[name="gender"][value="${savedData.gender}"]`).checked = true;
                }
                document.getElementById('satisfaction').value = savedData.satisfaction || '';
                if (savedData.services) {
                    savedData.services.forEach(service => {
                        const checkbox = document.querySelector(`input[name="services"][value="${service}"]`);
                        if (checkbox) checkbox.checked = true;
                    });
                }
                document.getElementById('comments').value = savedData.comments || '';
            }
        }

        // Save form data to local storage on submit
        document.getElementById('questionnaireForm').addEventListener('submit', function(event) {
            event.preventDefault();
            
            // Collect data from the form
            const userData = {
                name: document.getElementById('name').value,
                email: document.getElementById('email').value,
                age: document.getElementById('age').value,
                gender: document.querySelector('input[name="gender"]:checked')?.value || '',
                satisfaction: document.getElementById('satisfaction').value,
                services: Array.from(document.querySelectorAll('input[name="services"]:checked')).map(el => el.value),
                comments: document.getElementById('comments').value
            };
            
            // Save to local storage
            localStorage.setItem('userData', JSON.stringify(userData));
            alert('Your input has been saved to Local Storage!');
        });

        // Load saved data when the page loads
        document.addEventListener('DOMContentLoaded', loadSavedData);
    </script>
</body>
</html>
