<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TESO Integrated Secondary School - Fees Recovery Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Inter', sans-serif; }
        .gradient-bg { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .card-shadow { box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04); }
    </style>
</head>
<body class="gradient-bg min-h-screen">
    <div class="container mx-auto px-4 py-8">
        <!-- Header -->
        <div class="text-center mb-8">
            <div class="bg-white rounded-full w-24 h-24 mx-auto mb-4 flex items-center justify-center card-shadow">
                <svg class="w-12 h-12 text-blue-600" fill="currentColor" viewBox="0 0 20 20">
                    <path d="M10.394 2.08a1 1 0 00-.788 0l-7 3a1 1 0 000 1.84L5.25 8.051a.999.999 0 01.356-.257l4-1.714a1 1 0 11.788 1.838L7.667 9.088l1.94.831a1 1 0 00.787 0l7-3a1 1 0 000-1.838l-7-3zM3.31 9.397L5 10.12v4.102a8.969 8.969 0 00-1.05-.174 1 1 0 01-.89-.89 11.115 11.115 0 01.25-3.762zM9.3 16.573A9.026 9.026 0 007 14.935v-3.957l1.818.78a3 3 0 002.364 0l5.508-2.361a11.026 11.026 0 01.25 3.762 1 1 0 01-.89.89 8.968 8.968 0 00-5.35 2.524 1 1 0 01-1.4 0zM6 18a1 1 0 001-1v-2.065a8.935 8.935 0 00-2-.712V17a1 1 0 001 1z"/>
                </svg>
            </div>
            <h1 class="text-4xl font-bold text-white mb-2">TESO INTEGRATED SECONDARY SCHOOL</h1>
            <p class="text-blue-100 text-lg">Fees Recovery Portal</p>
            
            <!-- Navigation -->
            <div class="mt-6 flex justify-center space-x-4">
                <button onclick="showStudentPortal()" id="studentBtn" class="bg-white text-blue-600 px-6 py-2 rounded-full font-medium hover:bg-blue-50 transition duration-200">
                    Student Portal
                </button>
                <button onclick="showAdminPortal()" id="adminBtn" class="bg-blue-500 text-white px-6 py-2 rounded-full font-medium hover:bg-blue-600 transition duration-200">
                    Admin Portal
                </button>
            </div>
        </div>

        <!-- Main Content -->
        <div class="max-w-6xl mx-auto">
            <!-- Admin Portal -->
            <div id="adminPortal" class="hidden">
                <!-- Import Section -->
                <div class="bg-white rounded-2xl card-shadow p-8 mb-8">
                    <h2 class="text-2xl font-semibold text-gray-800 mb-6">Import Student Data</h2>
                    
                    <!-- File Upload -->
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-medium mb-2">Upload CSV File</label>
                        <div class="border-2 border-dashed border-gray-300 rounded-lg p-6 text-center hover:border-blue-400 transition duration-200">
                            <input type="file" id="csvFile" accept=".csv" class="hidden" onchange="handleFileUpload(event)">
                            <label for="csvFile" class="cursor-pointer">
                                <svg class="w-12 h-12 text-gray-400 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
                                </svg>
                                <p class="text-gray-600 font-medium">Click to upload CSV file</p>
                                <p class="text-sm text-gray-500 mt-1">Format: StudentID, Name, Class, TotalFees, AmountPaid</p>
                            </label>
                        </div>
                    </div>

                    <!-- Sample Data Button -->
                    <div class="flex justify-between items-center">
                        <button onclick="loadSampleData()" class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                            Load Sample Data
                        </button>
                        <button onclick="exportData()" class="bg-green-600 hover:bg-green-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                            Export Current Data
                        </button>
                    </div>
                </div>

                <!-- Summary Statistics -->
                <div class="grid md:grid-cols-4 gap-6 mb-8">
                    <div class="bg-white rounded-xl card-shadow p-6">
                        <div class="flex items-center">
                            <div class="bg-blue-100 p-3 rounded-full">
                                <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197m13.5-9a2.5 2.5 0 11-5 0 2.5 2.5 0 015 0z"></path>
                                </svg>
                            </div>
                            <div class="ml-4">
                                <p class="text-sm text-gray-600">Total Students</p>
                                <p class="text-2xl font-bold text-gray-800" id="totalStudents">0</p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-xl card-shadow p-6">
                        <div class="flex items-center">
                            <div class="bg-green-100 p-3 rounded-full">
                                <svg class="w-6 h-6 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"></path>
                                </svg>
                            </div>
                            <div class="ml-4">
                                <p class="text-sm text-gray-600">Total Fees Expected</p>
                                <p class="text-2xl font-bold text-gray-800" id="totalFeesExpected">UGX 0</p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-xl card-shadow p-6">
                        <div class="flex items-center">
                            <div class="bg-blue-100 p-3 rounded-full">
                                <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                                </svg>
                            </div>
                            <div class="ml-4">
                                <p class="text-sm text-gray-600">Fees Recovered</p>
                                <p class="text-2xl font-bold text-blue-800" id="feesRecovered">UGX 0</p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-xl card-shadow p-6">
                        <div class="flex items-center">
                            <div class="bg-red-100 p-3 rounded-full">
                                <svg class="w-6 h-6 text-red-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L4.082 16.5c-.77.833.192 2.5 1.732 2.5z"></path>
                                </svg>
                            </div>
                            <div class="ml-4">
                                <p class="text-sm text-gray-600">Outstanding Balance</p>
                                <p class="text-2xl font-bold text-red-800" id="totalOutstanding">UGX 0</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Students List -->
                <div class="bg-white rounded-2xl card-shadow p-6">
                    <div class="flex justify-between items-center mb-6">
                        <h3 class="text-xl font-semibold text-gray-800">Students Fees Status</h3>
                        <div class="flex space-x-2">
                            <select id="filterStatus" onchange="filterStudents()" class="px-3 py-2 border border-gray-300 rounded-lg text-sm">
                                <option value="all">All Students</option>
                                <option value="cleared">Fees Cleared</option>
                                <option value="outstanding">Outstanding Fees</option>
                            </select>
                        </div>
                    </div>
                    
                    <div class="overflow-x-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50">
                                <tr>
                                    <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Student ID</th>
                                    <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Name</th>
                                    <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Class</th>
                                    <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Total Fees</th>
                                    <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Amount Paid</th>
                                    <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Outstanding</th>
                                    <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                                </tr>
                            </thead>
                            <tbody id="studentsTableBody" class="bg-white divide-y divide-gray-200">
                                <tr>
                                    <td colspan="7" class="px-4 py-8 text-center text-gray-500">
                                        <svg class="w-12 h-12 mx-auto mb-4 text-gray-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197m13.5-9a2.5 2.5 0 11-5 0 2.5 2.5 0 015 0z"></path>
                                        </svg>
                                        <p>No student data loaded</p>
                                        <p class="text-sm mt-1">Upload a CSV file or load sample data to get started</p>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- Login Section -->
            <div id="loginSection" class="bg-white rounded-2xl card-shadow p-8 mb-8">
                <h2 class="text-2xl font-semibold text-gray-800 mb-6 text-center">Student Login</h2>
                <div class="max-w-md mx-auto">
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-medium mb-2">Student ID</label>
                        <input type="text" id="studentId" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Enter your student ID">
                    </div>
                    <button onclick="login()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-medium py-3 px-6 rounded-lg transition duration-200">
                        Access Portal
                    </button>
                </div>
            </div>

            <!-- Student Dashboard -->
            <div id="dashboard" class="hidden">
                <!-- Student Info Card -->
                <div class="bg-white rounded-2xl card-shadow p-6 mb-6">
                    <div class="flex items-center justify-between mb-4">
                        <div>
                            <h3 class="text-xl font-semibold text-gray-800" id="studentName">Loading...</h3>
                            <p class="text-gray-600" id="studentClass">Class: Loading...</p>
                        </div>
                        <button onclick="logout()" class="text-red-600 hover:text-red-700 font-medium">Logout</button>
                    </div>
                </div>

                <!-- Fees Status Card -->
                <div class="bg-white rounded-2xl card-shadow p-6 mb-6">
                    <h3 class="text-xl font-semibold text-gray-800 mb-4">Fees Status</h3>
                    <div class="grid md:grid-cols-3 gap-4">
                        <div class="bg-blue-50 p-4 rounded-lg">
                            <p class="text-sm text-blue-600 font-medium">Total Fees</p>
                            <p class="text-2xl font-bold text-blue-800" id="totalFees">UGX 0</p>
                        </div>
                        <div class="bg-green-50 p-4 rounded-lg">
                            <p class="text-sm text-green-600 font-medium">Amount Paid</p>
                            <p class="text-2xl font-bold text-green-800" id="amountPaid">UGX 0</p>
                        </div>
                        <div class="bg-red-50 p-4 rounded-lg">
                            <p class="text-sm text-red-600 font-medium">Outstanding Balance</p>
                            <p class="text-2xl font-bold text-red-800" id="outstandingBalance">UGX 0</p>
                        </div>
                    </div>
                    
                    <!-- Payment Status -->
                    <div class="mt-6 p-4 rounded-lg" id="paymentStatus">
                        <div class="flex items-center">
                            <div class="w-3 h-3 rounded-full mr-3" id="statusIndicator"></div>
                            <span class="font-medium" id="statusText">Checking status...</span>
                        </div>
                    </div>
                </div>

                <!-- Payment Section -->
                <div id="paymentSection" class="bg-white rounded-2xl card-shadow p-6 mb-6">
                    <h3 class="text-xl font-semibold text-gray-800 mb-4">Make Payment</h3>
                    <div class="grid md:grid-cols-2 gap-4 mb-4">
                        <div>
                            <label class="block text-gray-700 text-sm font-medium mb-2">Payment Amount (UGX)</label>
                            <input type="number" id="paymentAmount" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Enter amount">
                        </div>
                        <div>
                            <label class="block text-gray-700 text-sm font-medium mb-2">Payment Method</label>
                            <select id="paymentMethod" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                <option value="">Select payment method</option>
                                <option value="mobile_money">Mobile Money</option>
                                <option value="bank_transfer">Bank Transfer</option>
                                <option value="cash">Cash Payment</option>
                            </select>
                        </div>
                    </div>
                    <div class="mb-4">
                        <label class="block text-gray-700 text-sm font-medium mb-2">Transaction ID</label>
                        <input type="text" id="transactionId" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Enter transaction ID (e.g., TXN123456789)">
                        <p class="text-sm text-gray-500 mt-1">Enter the transaction ID from your payment receipt</p>
                    </div>
                    <button onclick="makePayment()" class="bg-green-600 hover:bg-green-700 text-white font-medium py-3 px-6 rounded-lg transition duration-200">
                        Submit Payment
                    </button>
                </div>

                <!-- Transaction History -->
                <div class="bg-white rounded-2xl card-shadow p-6 mb-6">
                    <h3 class="text-xl font-semibold text-gray-800 mb-4">Transaction History</h3>
                    <div id="transactionHistory">
                        <div class="text-center py-8 text-gray-500">
                            <svg class="w-12 h-12 mx-auto mb-4 text-gray-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                            </svg>
                            <p>No transactions yet</p>
                        </div>
                    </div>
                </div>

                <!-- Documents Section -->
                <div class="bg-white rounded-2xl card-shadow p-6">
                    <h3 class="text-xl font-semibold text-gray-800 mb-4">Academic Documents</h3>
                    
                    <!-- Access Denied Message -->
                    <div id="accessDenied" class="bg-red-50 border border-red-200 rounded-lg p-6 text-center">
                        <svg class="w-16 h-16 text-red-400 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m0 0v2m0-2h2m-2 0H10m2-5V9m0 0V7m0 2h2m-2 0H10m8-2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                        </svg>
                        <h4 class="text-lg font-semibold text-red-800 mb-2">Access Restricted</h4>
                        <p class="text-red-600 mb-4">You must clear all outstanding fees before accessing your academic documents.</p>
                        <p class="text-sm text-red-500">Outstanding Balance: <span id="restrictionBalance" class="font-semibold">UGX 0</span></p>
                    </div>

                    <!-- Documents Available -->
                    <div id="documentsAvailable" class="hidden">
                        <div class="bg-green-50 border border-green-200 rounded-lg p-4 mb-6">
                            <div class="flex items-center">
                                <svg class="w-6 h-6 text-green-600 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                                </svg>
                                <span class="text-green-800 font-medium">All fees cleared! You can now view your document status.</span>
                            </div>
                        </div>
                        
                        <div class="space-y-4">
                            <div class="border border-gray-200 rounded-lg p-6">
                                <div class="flex items-center justify-between">
                                    <div class="flex items-center">
                                        <svg class="w-8 h-8 text-blue-500 mr-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                                        </svg>
                                        <div>
                                            <h4 class="font-medium text-gray-800">Academic Results</h4>
                                            <p class="text-sm text-gray-600">Transcripts & report cards</p>
                                        </div>
                                    </div>
                                    <div class="flex items-center space-x-4">
                                        <button onclick="toggleDocumentStatus('results')" id="resultsBtn" class="px-4 py-2 rounded-lg font-medium transition duration-200 bg-red-100 text-red-800 hover:bg-red-200">
                                            Not Taken
                                        </button>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="border border-gray-200 rounded-lg p-6">
                                <div class="flex items-center justify-between">
                                    <div class="flex items-center">
                                        <svg class="w-8 h-8 text-green-500 mr-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.746 0 3.332.477 4.5 1.253v13C19.832 18.477 18.246 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"></path>
                                        </svg>
                                        <div>
                                            <h4 class="font-medium text-gray-800">Certificate</h4>
                                            <p class="text-sm text-gray-600">Completion certificates</p>
                                        </div>
                                    </div>
                                    <div class="flex items-center space-x-4">
                                        <button onclick="toggleDocumentStatus('certificate')" id="certificateBtn" class="px-4 py-2 rounded-lg font-medium transition duration-200 bg-red-100 text-red-800 hover:bg-red-200">
                                            Not Taken
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Student data - starts empty, populate via CSV upload or sample data
        let studentsData = {};

        let currentStudent = null;
        let currentView = 'student';

        // Navigation functions
        function showStudentPortal() {
            currentView = 'student';
            document.getElementById('adminPortal').classList.add('hidden');
            document.getElementById('loginSection').classList.remove('hidden');
            document.getElementById('dashboard').classList.add('hidden');
            
            // Update button styles
            document.getElementById('studentBtn').className = 'bg-white text-blue-600 px-6 py-2 rounded-full font-medium hover:bg-blue-50 transition duration-200';
            document.getElementById('adminBtn').className = 'bg-blue-500 text-white px-6 py-2 rounded-full font-medium hover:bg-blue-600 transition duration-200';
        }

        function showAdminPortal() {
            currentView = 'admin';
            document.getElementById('loginSection').classList.add('hidden');
            document.getElementById('dashboard').classList.add('hidden');
            document.getElementById('adminPortal').classList.remove('hidden');
            
            // Update button styles
            document.getElementById('adminBtn').className = 'bg-white text-blue-600 px-6 py-2 rounded-full font-medium hover:bg-blue-50 transition duration-200';
            document.getElementById('studentBtn').className = 'bg-blue-500 text-white px-6 py-2 rounded-full font-medium hover:bg-blue-600 transition duration-200';
            
            updateAdminDashboard();
        }

        // Admin functions
        function updateAdminDashboard() {
            const students = Object.keys(studentsData);
            let totalExpected = 0;
            let totalRecovered = 0;
            let totalOutstanding = 0;

            students.forEach(id => {
                const student = studentsData[id];
                totalExpected += student.totalFees;
                totalRecovered += student.amountPaid;
                totalOutstanding += (student.totalFees - student.amountPaid);
            });

            document.getElementById('totalStudents').textContent = students.length;
            document.getElementById('totalFeesExpected').textContent = `UGX ${totalExpected.toLocaleString()}`;
            document.getElementById('feesRecovered').textContent = `UGX ${totalRecovered.toLocaleString()}`;
            document.getElementById('totalOutstanding').textContent = `UGX ${totalOutstanding.toLocaleString()}`;

            populateStudentsTable();
        }

        function populateStudentsTable() {
            const tbody = document.getElementById('studentsTableBody');
            const filter = document.getElementById('filterStatus').value;
            tbody.innerHTML = '';

            const students = Object.keys(studentsData);
            
            if (students.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="7" class="px-4 py-8 text-center text-gray-500">
                            <svg class="w-12 h-12 mx-auto mb-4 text-gray-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197m13.5-9a2.5 2.5 0 11-5 0 2.5 2.5 0 015 0z"></path>
                            </svg>
                            <p>No student data loaded</p>
                            <p class="text-sm mt-1">Upload a CSV file or load sample data to get started</p>
                        </td>
                    </tr>
                `;
                return;
            }

            students.forEach(id => {
                const student = studentsData[id];
                const outstanding = student.totalFees - student.amountPaid;
                const isCleared = outstanding === 0;

                // Apply filter
                if (filter === 'cleared' && !isCleared) return;
                if (filter === 'outstanding' && isCleared) return;

                const row = document.createElement('tr');
                row.className = 'hover:bg-gray-50';
                
                row.innerHTML = `
                    <td class="px-4 py-4 whitespace-nowrap text-sm font-medium text-gray-900">${id}</td>
                    <td class="px-4 py-4 whitespace-nowrap text-sm text-gray-900">${student.name}</td>
                    <td class="px-4 py-4 whitespace-nowrap text-sm text-gray-900">${student.class}</td>
                    <td class="px-4 py-4 whitespace-nowrap text-sm text-gray-900">UGX ${student.totalFees.toLocaleString()}</td>
                    <td class="px-4 py-4 whitespace-nowrap text-sm text-gray-900">UGX ${student.amountPaid.toLocaleString()}</td>
                    <td class="px-4 py-4 whitespace-nowrap text-sm text-gray-900">UGX ${outstanding.toLocaleString()}</td>
                    <td class="px-4 py-4 whitespace-nowrap">
                        <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${isCleared ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}">
                            ${isCleared ? 'Cleared' : 'Outstanding'}
                        </span>
                    </td>
                `;
                
                tbody.appendChild(row);
            });
        }

        function filterStudents() {
            populateStudentsTable();
        }

        function handleFileUpload(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const csv = e.target.result;
                    const lines = csv.split('\n');
                    const newStudentsData = {};

                    // Skip header row
                    for (let i = 1; i < lines.length; i++) {
                        const line = lines[i].trim();
                        if (!line) continue;

                        const [studentId, name, studentClass, totalFees, amountPaid] = line.split(',');
                        
                        if (studentId && name && studentClass && totalFees && amountPaid) {
                            newStudentsData[studentId.trim()] = {
                                name: name.trim(),
                                class: studentClass.trim(),
                                totalFees: parseInt(totalFees.trim()),
                                amountPaid: parseInt(amountPaid.trim())
                            };
                        }
                    }

                    studentsData = newStudentsData;
                    updateAdminDashboard();
                    alert(`Successfully imported ${Object.keys(newStudentsData).length} students!`);
                } catch (error) {
                    alert('Error parsing CSV file. Please check the format.');
                }
            };
            reader.readAsText(file);
        }

        function loadSampleData() {
            studentsData = {
                'TESO001': {
                    name: 'John Mukasa',
                    class: 'Senior 6 - Science',
                    totalFees: 2500000,
                    amountPaid: 1800000
                },
                'TESO002': {
                    name: 'Sarah Nakato',
                    class: 'Senior 5 - Arts',
                    totalFees: 2200000,
                    amountPaid: 2200000
                },
                'TESO003': {
                    name: 'David Okello',
                    class: 'Senior 4',
                    totalFees: 2000000,
                    amountPaid: 1500000
                },
                'TESO004': {
                    name: 'Grace Achieng',
                    class: 'Senior 6 - Arts',
                    totalFees: 2400000,
                    amountPaid: 2400000
                },
                'TESO005': {
                    name: 'Peter Wanyama',
                    class: 'Senior 5 - Science',
                    totalFees: 2300000,
                    amountPaid: 1200000
                },
                'TESO006': {
                    name: 'Mary Akello',
                    class: 'Senior 4',
                    totalFees: 2000000,
                    amountPaid: 800000
                }
            };
            updateAdminDashboard();
            alert('Sample data loaded successfully!');
        }

        function exportData() {
            if (Object.keys(studentsData).length === 0) {
                alert('No data to export. Please load student data first.');
                return;
            }

            let csvContent = 'StudentID,Name,Class,TotalFees,AmountPaid\n';
            
            Object.keys(studentsData).forEach(id => {
                const student = studentsData[id];
                csvContent += `${id},${student.name},${student.class},${student.totalFees},${student.amountPaid}\n`;
            });

            const blob = new Blob([csvContent], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'students_fees_data.csv';
            a.click();
            window.URL.revokeObjectURL(url);
        }

        function login() {
            const studentId = document.getElementById('studentId').value.trim();

            if (!studentId) {
                alert('Please enter your Student ID');
                return;
            }

            const student = studentsData[studentId];
            if (!student) {
                alert('Invalid Student ID. Please check your Student ID or contact the admin to load student data.');
                return;
            }

            currentStudent = { id: studentId, ...student };
            showDashboard();
        }

        function showDashboard() {
            document.getElementById('loginSection').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            
            // Update student info
            document.getElementById('studentName').textContent = currentStudent.name;
            document.getElementById('studentClass').textContent = `Class: ${currentStudent.class}`;
            
            updateFeesDisplay();
        }

        function updateFeesDisplay() {
            const totalFees = currentStudent.totalFees;
            const amountPaid = currentStudent.amountPaid;
            const outstanding = totalFees - amountPaid;

            document.getElementById('totalFees').textContent = `UGX ${totalFees.toLocaleString()}`;
            document.getElementById('amountPaid').textContent = `UGX ${amountPaid.toLocaleString()}`;
            document.getElementById('outstandingBalance').textContent = `UGX ${outstanding.toLocaleString()}`;
            document.getElementById('restrictionBalance').textContent = `UGX ${outstanding.toLocaleString()}`;

            const statusDiv = document.getElementById('paymentStatus');
            const indicator = document.getElementById('statusIndicator');
            const statusText = document.getElementById('statusText');

            if (outstanding === 0) {
                statusDiv.className = 'mt-6 p-4 rounded-lg bg-green-50 border border-green-200';
                indicator.className = 'w-3 h-3 rounded-full mr-3 bg-green-500';
                statusText.textContent = 'Fees Cleared - Documents Available';
                statusText.className = 'font-medium text-green-800';
                
                document.getElementById('accessDenied').classList.add('hidden');
                document.getElementById('documentsAvailable').classList.remove('hidden');
                document.getElementById('paymentSection').classList.add('hidden');
            } else {
                statusDiv.className = 'mt-6 p-4 rounded-lg bg-red-50 border border-red-200';
                indicator.className = 'w-3 h-3 rounded-full mr-3 bg-red-500';
                statusText.textContent = 'Outstanding Fees - Documents Restricted';
                statusText.className = 'font-medium text-red-800';
                
                document.getElementById('accessDenied').classList.remove('hidden');
                document.getElementById('documentsAvailable').classList.add('hidden');
                document.getElementById('paymentSection').classList.remove('hidden');
            }

            // Update transaction history
            updateTransactionHistory();
        }

        function updateTransactionHistory() {
            const historyDiv = document.getElementById('transactionHistory');
            
            if (!currentStudent.transactions || currentStudent.transactions.length === 0) {
                historyDiv.innerHTML = `
                    <div class="text-center py-8 text-gray-500">
                        <svg class="w-12 h-12 mx-auto mb-4 text-gray-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                        </svg>
                        <p>No transactions yet</p>
                    </div>
                `;
                return;
            }

            // Sort transactions by date (newest first)
            const sortedTransactions = [...currentStudent.transactions].sort((a, b) => b.timestamp - a.timestamp);
            
            let historyHTML = '<div class="space-y-4">';
            
            sortedTransactions.forEach(transaction => {
                const date = new Date(transaction.date);
                const methodName = transaction.method.replace('_', ' ').toUpperCase();
                
                historyHTML += `
                    <div class="border border-gray-200 rounded-lg p-4 hover:bg-gray-50 transition duration-200">
                        <div class="flex justify-between items-start">
                            <div class="flex-1">
                                <div class="flex items-center mb-2">
                                    <div class="w-2 h-2 bg-green-500 rounded-full mr-3"></div>
                                    <span class="font-medium text-gray-900">Payment Successful</span>
                                </div>
                                <div class="text-sm text-gray-600 space-y-1">
                                    <p><span class="font-medium">Transaction ID:</span> ${transaction.id}</p>
                                    <p><span class="font-medium">Amount:</span> UGX ${transaction.amount.toLocaleString()}</p>
                                    <p><span class="font-medium">Method:</span> ${methodName}</p>
                                    <p><span class="font-medium">Date:</span> ${date.toLocaleDateString()} at ${date.toLocaleTimeString()}</p>
                                </div>
                            </div>
                            <div class="text-right">
                                <span class="text-lg font-bold text-green-600">+UGX ${transaction.amount.toLocaleString()}</span>
                            </div>
                        </div>
                    </div>
                `;
            });
            
            historyHTML += '</div>';
            historyDiv.innerHTML = historyHTML;
        }

        function generateTransactionId() {
            const timestamp = Date.now();
            const random = Math.floor(Math.random() * 1000).toString().padStart(3, '0');
            return `TXN${timestamp}${random}`;
        }

        function makePayment() {
            const amountInput = document.getElementById('paymentAmount');
            const methodSelect = document.getElementById('paymentMethod');
            const transactionIdInput = document.getElementById('transactionId');
            
            if (!amountInput || !methodSelect || !transactionIdInput) {
                alert('Payment form elements not found');
                return;
            }
            
            const amount = parseInt(amountInput.value);
            const method = methodSelect.value;
            const transactionId = transactionIdInput.value.trim();

            if (!amount || amount <= 0 || isNaN(amount)) {
                alert('Please enter a valid payment amount');
                return;
            }

            if (!method) {
                alert('Please select a payment method');
                return;
            }

            if (!transactionId) {
                alert('Please enter a transaction ID');
                return;
            }

            if (!currentStudent) {
                alert('No student logged in');
                return;
            }

            const outstanding = currentStudent.totalFees - currentStudent.amountPaid;
            if (amount > outstanding) {
                alert(`Payment amount cannot exceed outstanding balance of UGX ${outstanding.toLocaleString()}`);
                return;
            }

            // Check if transaction ID already exists
            if (currentStudent.transactions) {
                const existingTransaction = currentStudent.transactions.find(t => t.id === transactionId);
                if (existingTransaction) {
                    alert('This transaction ID has already been used. Please enter a unique transaction ID.');
                    return;
                }
            }

            const methodName = method.replace('_', ' ').toUpperCase();
            const confirmPayment = confirm(`Confirm payment details:\n\nAmount: UGX ${amount.toLocaleString()}\nMethod: ${methodName}\nTransaction ID: ${transactionId}\n\nProceed with payment?`);
            
            if (confirmPayment) {
                // Initialize transactions array if it doesn't exist
                if (!currentStudent.transactions) {
                    currentStudent.transactions = [];
                }
                
                // Record the transaction
                const transaction = {
                    id: transactionId,
                    amount: amount,
                    method: method,
                    date: new Date().toISOString(),
                    timestamp: Date.now()
                };
                
                currentStudent.transactions.push(transaction);
                
                // Update student payment record
                currentStudent.amountPaid += amount;
                
                // Update the main data store as well
                if (studentsData[currentStudent.id]) {
                    studentsData[currentStudent.id].amountPaid = currentStudent.amountPaid;
                    if (!studentsData[currentStudent.id].transactions) {
                        studentsData[currentStudent.id].transactions = [];
                    }
                    studentsData[currentStudent.id].transactions.push(transaction);
                }
                
                // Clear form
                amountInput.value = '';
                methodSelect.value = '';
                transactionIdInput.value = '';
                
                // Update display
                updateFeesDisplay();
                
                alert(`Payment Recorded Successfully!\n\nTransaction ID: ${transactionId}\nAmount: UGX ${amount.toLocaleString()}\nMethod: ${methodName}\nDate: ${new Date().toLocaleDateString()}\n\nYour payment has been recorded in the system.`);
            }
        }

        function toggleDocumentStatus(type) {
            const outstanding = currentStudent.totalFees - currentStudent.amountPaid;
            
            if (outstanding > 0) {
                alert('Access denied. Please clear all outstanding fees first.');
                return;
            }

            const btnId = type === 'results' ? 'resultsBtn' : 'certificateBtn';
            const btn = document.getElementById(btnId);
            
            if (btn.textContent.trim() === 'Not Taken') {
                btn.textContent = 'Taken';
                btn.className = 'px-4 py-2 rounded-lg font-medium transition duration-200 bg-green-100 text-green-800 hover:bg-green-200';
            } else {
                btn.textContent = 'Not Taken';
                btn.className = 'px-4 py-2 rounded-lg font-medium transition duration-200 bg-red-100 text-red-800 hover:bg-red-200';
            }
        }

        function logout() {
            currentStudent = null;
            document.getElementById('dashboard').classList.add('hidden');
            document.getElementById('loginSection').classList.remove('hidden');
            
            // Clear form
            document.getElementById('studentId').value = '';
        }

        // Initialize the portal
        showStudentPortal();
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'973cd12e5043c84d',t:'MTc1NTk3NTI1Mi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
