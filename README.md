<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Suivi de présence des élèves</title>
    <style>
        table {
            width: 50%;
            margin: 20px auto;
            border-collapse: collapse;
        }

        table, th, td {
            border: 1px solid black;
            text-align: center;
            padding: 8px;
        }

        button {
            margin: 10px;
        }
    </style>
</head>
<body>
    <h1 style="text-align: center;">Suivi de la présence des élèves</h1>

    <table>
        <thead>
            <tr>
                <th>Nom de l'élève</th>
                <th>Présent</th>
            </tr>
        </thead>
        <tbody id="studentsTable">
            <!-- Les lignes d'élèves seront générées ici -->
        </tbody>
    </table>

    <div style="text-align: center;">
        <button onclick="markAttendance()">Marquer Présence</button>
        <button onclick="generateExamList()">Générer Liste d'Examen</button>
    </div>

    <div id="examList" style="text-align: center;"></div>

    <script>
        // Liste initiale des élèves
        const students = [
            { name: "Alice", present: false },
            { name: "Bob", present: false },
            { name: "Charlie", present: false }
        ];

        // Initialisation de la table des élèves
        function loadStudents() {
            const table = document.getElementById("studentsTable");
            students.forEach((student, index) => {
                const row = document.createElement("tr");

                const nameCell = document.createElement("td");
                nameCell.textContent = student.name;
                row.appendChild(nameCell);

                const presenceCell = document.createElement("td");
                const checkbox = document.createElement("input");
                checkbox.type = "checkbox";
                checkbox.id = `present-${index}`;
                presenceCell.appendChild(checkbox);
                row.appendChild(presenceCell);

                table.appendChild(row);
            });
        }

        // Marquer la présence pour chaque élève
        function markAttendance() {
            students.forEach((student, index) => {
                const checkbox = document.getElementById(`present-${index}`);
                student.present = checkbox.checked;
            });
            alert("Présence enregistrée !");
        }

        // Générer la liste des élèves éligibles à l'examen
        function generateExamList() {
            const examListDiv = document.getElementById("examList");
            examListDiv.innerHTML = "<h3>Liste pour l'examen :</h3>";
            const ul = document.createElement("ul");

            students.forEach(student => {
                if (student.present) {
                    const li = document.createElement("li");
                    li.textContent = student.name;
                    ul.appendChild(li);
                }
            });

            examListDiv.appendChild(ul);
        }

        // Charger les élèves au démarrage
        window.onload = loadStudents;
    </script>
</body>
</html>
