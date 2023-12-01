# partyy
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fucking Party</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            text-align: center;
            margin: 50px;
            background-color: #f9f9f9; /* Light Grey */
            color: #333; /* Dark Grey */
        }

        h1 {
            color: #0d0d0d; /* Red */
        }

        form {
            display: inline-block;
            text-align: left;
            background-color: rgb(177, 4, 70); /* Blue */
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #ecf0f1; /* Light Grey */
        }

        input[type="text"], input[type="checkbox"] {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            box-sizing: border-box;
            border: 1px solid #2980b9; /* Dark Blue */
            border-radius: 4px;
            background-color: #ecf0f1; /* Light Grey */
            color: #333; /* Dark Grey */
        }

        button {
            background-color: #070707; /* Red */
            color: #0d8faf; /* Light Grey */
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
        }

        button:hover {
            background-color: #c0392b; /* Darker Red */
        }

        #attendanceList {
            background-color: #ff4d4d; /* Green */
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(255, 0, 0, 0.3);
        }

        ul {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        li {
            margin-bottom: 10px;
            color: #ecf0f1; /* Light Grey */
            position: relative;
        }

        li:last-child {
            margin-bottom: 0;
        }

        .delete-button {
            position: absolute;
            right: 0;
            top: 0;
            background-color: #e74c3c; /* Red */
            color: #ecf0f1; /* Light Grey */
            border: none;
            border-radius: 4px;
            padding: 5px 10px;
            cursor: pointer;
        }

        .delete-button:hover {
            background-color: #c0392b; /* Darker Red */
        }
    </style>
</head>
<body>

    <h1>LET'S PARTTYYYYYYYY!!!!</h1>

    <form id="attendanceForm">
        <label for="userName">Name:</label>
        <input type="text" id="userName" name="userName" required>
        <br>
        <label for="attendanceTick">
            <input type="checkbox" id="attendanceTick" name="attendanceTick" required>
            Tyrsten loves you 
        </label>
        <br>
        <button type="button" onclick="submitAttendance()">Submit</button>
    </form>

    <div id="attendanceList">
        <h2>Bunch of fuckers</h2>
        <ul id="nameList"></ul>
    </div>

    <script>
        // Load stored attendee names on page load
        window.onload = function () {
            loadAttendanceData();
        };

        function submitAttendance() {
            // Retrieve user input
            var userName = document.getElementById("userName").value;

            // Check if the attendance checkbox is checked
            var attendanceTick = document.getElementById("attendanceTick");
            var attendanceStatus = attendanceTick.checked ? "Present" : "Absent";

            // Save the attendee data to local storage
            saveAttendanceData(userName, attendanceStatus);

            // Display the submitted data
            displayAttendanceData();

            // Clear the form fields
            document.getElementById("userName").value = "";
            attendanceTick.checked = false;
        }

        function saveAttendanceData(name, status) {
            // Get existing attendee data from local storage
            var existingData = localStorage.getItem("attendanceData");

            // Parse existing data or initialize an empty array
            var dataArray = existingData ? JSON.parse(existingData) : [];

            // Add new attendee data
            dataArray.push({ name: name, status: status });

            // Save the updated data back to local storage
            localStorage.setItem("attendanceData", JSON.stringify(dataArray));
        }

        function loadAttendanceData() {
            // Get existing attendee data from local storage
            var existingData = localStorage.getItem("attendanceData");

            // Parse existing data or initialize an empty array
            var dataArray = existingData ? JSON.parse(existingData) : [];

            // Display the existing data
            var nameList = document.getElementById("nameList");
            dataArray.forEach(function (entry, index) {
                var listItem = document.createElement("li");
                listItem.innerHTML = "Name: " + entry.name + " | Status: " + entry.status +
                    '<button class="delete-button" onclick="deleteAttendance(' + index + ')">Delete</button>';
                nameList.appendChild(listItem);
            });
        }

        function displayAttendanceData() {
            // Clear the existing list
            var nameList = document.getElementById("nameList");
            nameList.innerHTML = "";

            // Reload and display the updated attendee data
            loadAttendanceData();
        }

        function deleteAttendance(index) {
            // Remove the selected attendee from the local storage data
            var existingData = localStorage.getItem("attendanceData");
            var dataArray = existingData ? JSON.parse(existingData) : [];
            dataArray.splice(index, 1);
            localStorage.setItem("attendanceData", JSON.stringify(dataArray));

            // Reload and display the updated attendee data
            displayAttendanceData();
        }
    </script>

</body>
</html>
