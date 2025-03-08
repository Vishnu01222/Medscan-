
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Medicine Availability System</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }
    .container {
      max-width: 600px;
      margin: 0 auto;
      padding: 20px;
      border: 1px solid #ccc;
      border-radius: 10px;
    }
    h1 {
      text-align: center;
    }
    input, button {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      background-color: #28a745;
      color: white;
      cursor: pointer;
    }
    button:hover {
      background-color: #218838;
    }
    .pharmacy-item, .reminder-item {
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      margin-bottom: 10px;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>

  <!-- Patient's Prescription Scanner Page -->
  <div id="patient-page" class="container">
    <h1>Scan Prescription</h1>
    <button onclick="scanQRCode()">Scan QR Code</button>
    <div id="prescription-details" class="hidden">
      <h2>Prescription Details</h2>
      <p><strong>Patient Name:</strong> <span id="scanned-patient-name"></span></p>
      <p><strong>Medicine Name:</strong> <span id="scanned-medicine-name"></span></p>
      <p><strong>Dosage:</strong> <span id="scanned-dosage"></span></p>
      <p><strong>Frequency:</strong> <span id="scanned-frequency"></span></p>
      <button onclick="viewMedicineDetails()">View Medicine Details</button>
    </div>
  </div>

  <!-- Medicine Details and Pharmacy List Page -->
  <div id="medicine-page" class="container hidden">
    <h1>Medicine Details</h1>
    <div id="medicine-details">
      <p><strong>Medicine Name:</strong> <span id="medicine-detail-name"></span></p>
      <p><strong>Description:</strong> <span id="medicine-description"></span></p>
      <p><strong>Side Effects:</strong> <span id="medicine-side-effects"></span></p>
      <h2>Nearby Pharmacies</h2>
      <div id="pharmacy-list">
        <!-- Pharmacy items will be dynamically added here -->
      </div>
    </div>
  </div>

  <!-- Order Confirmation Page -->
  <div id="order-page" class="container hidden">
    <h1>Order Confirmation</h1>
    <p>Your order has been placed. The pharmacy will notify you once it's ready.</p>
    <button onclick="viewReminders()">View Medication Reminders</button>
  </div>

  <!-- Medication Reminder Page -->
  <div id="reminder-page" class="container hidden">
    <h1>Medication Reminder</h1>
    <div id="reminder-details">
      <p><strong>Medicine Name:</strong> <span id="reminder-medicine-name"></span></p>
      <p><strong>Next Dose:</strong> <span id="next-dose-time"></span></p>
      <button onclick="markAsTaken()">Mark as Taken</button>
      <button onclick="markAsSkipped()">Mark as Skipped</button>
    </div>
  </div>

  <script>
    // Simulated data
    const prescriptionData = {
      patientName: "John Doe",
      medicineName: "Paracetamol",
      dosage: "500mg",
      frequency: "2 times a day"
    };

    const pharmacies = [
      { name: "Pharmacy A", distance: "1.2 km", available: true },
      { name: "Pharmacy B", distance: "2.5 km", available: false },
      { name: "Pharmacy C", distance: "3.0 km", available: true }
    ];

    // Patient's Prescription Scanner Page
    function scanQRCode() {
      document.getElementById('scanned-patient-name').textContent = prescriptionData.patientName;
      document.getElementById('scanned-medicine-name').textContent = prescriptionData.medicineName;
      document.getElementById('scanned-dosage').textContent = prescriptionData.dosage;
      document.getElementById('scanned-frequency').textContent = prescriptionData.frequency;

      document.getElementById('prescription-details').classList.remove('hidden');
    }

    // Medicine Details and Pharmacy List Page
    function viewMedicineDetails() {
      document.getElementById('patient-page').classList.add('hidden');
      document.getElementById('medicine-page').classList.remove('hidden');

      const medicineName = document.getElementById('scanned-medicine-name').textContent;
      document.getElementById('medicine-detail-name').textContent = medicineName;
      document.getElementById('medicine-description').textContent = 'Used to treat pain and fever.';
      document.getElementById('medicine-side-effects').textContent = 'Nausea, stomach pain, etc.';

      const pharmacyListDiv = document.getElementById('pharmacy-list');
      pharmacyListDiv.innerHTML = '';
      pharmacies.forEach(pharmacy => {
        const pharmacyItem = document.createElement('div');
        pharmacyItem.className = 'pharmacy-item';
        pharmacyItem.innerHTML = `
          <p><strong>${pharmacy.name}</strong> (${pharmacy.distance})</p>
          <p>${pharmacy.available ? 'Available' : 'Not Available'}</p>
          ${pharmacy.available ? `<button onclick="placeOrder('${pharmacy.name}')">Place Order</button>` : ''}
        `;
        pharmacyListDiv.appendChild(pharmacyItem);
      });
    }

    // Place Order and Notify Pharmacy
    function placeOrder(pharmacyName) {
      alert(`Order placed at ${pharmacyName}! Pharmacy will notify you once it's ready.`);
      notifyPharmacy(pharmacyName);
      document.getElementById('medicine-page').classList.add('hidden');
      document.getElementById('order-page').classList.remove('hidden');
    }

    function notifyPharmacy(pharmacyName) {
      // Simulate pharmacy notification
      console.log(`Notification sent to ${pharmacyName}: New order received.`);
    }

    // Medication Reminder Page
    function viewReminders() {
      document.getElementById('order-page').classList.add('hidden');
      document.getElementById('reminder-page').classList.remove('hidden');

      const medicineName = document.getElementById('scanned-medicine-name').textContent;
      document.getElementById('reminder-medicine-name').textContent = medicineName;
      document.getElementById('next-dose-time').textContent = '10:00 AM';
    }

    function markAsTaken() {
      alert('Medicine marked as taken. Next reminder will be scheduled accordingly.');
    }

    function markAsSkipped() {
      alert('Medicine marked as skipped. Next reminder will be scheduled accordingly.');
    }
  </script>
</body>
</html>
