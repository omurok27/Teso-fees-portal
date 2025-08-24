<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TESO Integrated Secondary School - Fees Recovery Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
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
            
            <!-- Admin Login Section -->
            <div class="mt-6">
                <div class="bg-white rounded-2xl card-shadow p-8 max-w-md mx-auto">
                    <h2 class="text-2xl font-semibold text-gray-800 mb-6 text-center">Admin Login</h2>
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-medium mb-2">Username</label>
                        <input type="text" id="adminUsername" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Enter admin username">
                    </div>
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-medium mb-2">Password</label>
                        <input type="password" id="adminPassword" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Enter admin password">
                    </div>
                    <button onclick="adminLogin()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-medium py-3 px-6 rounded-lg transition duration-200">
                        Access Admin Portal
                    </button>
                    <div class="text-center mt-4">
                        <button onclick="showForgotPassword()" class="text-blue-600 hover:text-blue-700 text-sm font-medium">
                            Forgot Password?
                        </button>
                    </div>

                </div>
            </div>
        </div>

        <!-- Forgot Password Modal -->
        <div id="forgotPasswordModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
            <div class="bg-white rounded-2xl card-shadow p-8 max-w-md mx-4 w-full">
                <div class="text-center mb-6">
                    <svg class="w-16 h-16 text-blue-600 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 0h12a2 2 0 002-2v-4a2 2 0 00-2-2H6a2 2 0 00-2 2v4a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"></path>
                    </svg>
                    <h2 class="text-2xl font-semibold text-gray-800">Password Reset</h2>
                    <p class="text-gray-600 mt-2">Enter the official school email to reset your password</p>
                </div>
                
                <div id="emailVerificationStep">
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-medium mb-2">School Email Address</label>
                        <input type="email" id="resetEmail" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Enter official school email">
                        <p class="text-sm text-gray-500 mt-1">Only official TESO school email addresses are accepted</p>
                    </div>
                    <div class="flex space-x-3">
                        <button onclick="verifySchoolEmail()" class="flex-1 bg-blue-600 hover:bg-blue-700 text-white font-medium py-3 px-4 rounded-lg transition duration-200">
                            Verify Email
                        </button>
                        <button onclick="closeForgotPassword()" class="flex-1 bg-gray-500 hover:bg-gray-600 text-white font-medium py-3 px-4 rounded-lg transition duration-200">
                            Cancel
                        </button>
                    </div>
                </div>

                <div id="codeVerificationStep" class="hidden">
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-medium mb-2">Verification Code</label>
                        <input type="text" id="verificationCode" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent text-center text-2xl font-mono" placeholder="000000" maxlength="6">
                        <p class="text-sm text-gray-500 mt-1">Enter the 6-digit code sent to your email</p>
                        <div class="mt-3 p-3 bg-green-50 border border-green-200 rounded-lg">
                            <p class="text-sm text-green-700" id="emailSentMessage"></p>
                        </div>
                    </div>
                    <div class="flex space-x-3">
                        <button onclick="verifyCode()" class="flex-1 bg-green-600 hover:bg-green-700 text-white font-medium py-3 px-4 rounded-lg transition duration-200">
                            Verify Code
                        </button>
                        <button onclick="resendCode()" class="flex-1 bg-orange-600 hover:bg-orange-700 text-white font-medium py-3 px-4 rounded-lg transition duration-200">
                            Resend Code
                        </button>
                    </div>
                </div>

                <div id="passwordResetStep" class="hidden">
                    <div class="mb-4">
                        <label class="block text-gray-700 text-sm font-medium mb-2">New Password</label>
                        <input type="password" id="newPassword" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Enter new password">
                    </div>
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-medium mb-2">Confirm New Password</label>
                        <input type="password" id="confirmPassword" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Confirm new password">
                    </div>
                    <div class="flex space-x-3">
                        <button onclick="resetPassword()" class="flex-1 bg-green-600 hover:bg-green-700 text-white font-medium py-3 px-4 rounded-lg transition duration-200">
                            Reset Password
                        </button>
                        <button onclick="closeForgotPassword()" class="flex-1 bg-gray-500 hover:bg-gray-600 text-white font-medium py-3 px-4 rounded-lg transition duration-200">
                            Cancel
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Main Content -->
        <div class="max-w-6xl mx-auto">
            <!-- Admin Portal -->
            <div id="adminPortal" class="hidden">
                <!-- Admin Header -->
                <div class="bg-white rounded-2xl card-shadow p-6 mb-8">
                    <div class="flex justify-between items-center">
                        <h2 class="text-2xl font-semibold text-gray-800">Admin Dashboard</h2>
                        <button onclick="adminLogout()" class="bg-red-600 hover:bg-red-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                            Logout
                        </button>
                    </div>
                </div>

                <!-- Import Section -->
                <div class="bg-white rounded-2xl card-shadow p-8 mb-8">
                    <h2 class="text-2xl font-semibold text-gray-800 mb-6">Import Student Data</h2>
                    
                    <!-- Academic Year Selection -->
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-medium mb-2">Academic Year</label>
                        <div class="flex space-x-4">
                            <select id="academicYear" class="flex-1 px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                <!-- Years will be populated by JavaScript -->
                            </select>
                            <button onclick="addNewYear()" class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-3 px-4 rounded-lg transition duration-200">
                                Add New Year
                            </button>
                        </div>
                        <p class="text-sm text-gray-500 mt-1">Select the academic year for the student data you're importing (unlimited range - add any year as needed)</p>
                    </div>

                    <!-- File Upload -->
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-medium mb-2">Upload Excel File</label>
                        <div class="border-2 border-dashed border-gray-300 rounded-lg p-6 text-center hover:border-blue-400 transition duration-200">
                            <input type="file" id="excelFile" accept=".xlsx,.xls" class="hidden" onchange="handleFileUpload(event)">
                            <label for="excelFile" class="cursor-pointer">
                                <svg class="w-12 h-12 text-gray-400 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
                                </svg>
                                <p class="text-gray-600 font-medium">Click to upload Excel file (.xlsx or .xls)</p>
                                <p class="text-sm text-gray-500 mt-1">Format: StudentID, Name, Class, TotalFees, AmountPaid</p>
                            </label>
                        </div>
                    </div>

                    <!-- Data Management Buttons -->
                    <div class="flex flex-wrap gap-3 justify-between items-center">
                        <div class="flex gap-2">
                            <button onclick="importData()" class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                                Import Excel Data
                            </button>
                            <button onclick="exportData()" class="bg-green-600 hover:bg-green-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                                Export Excel Data
                            </button>
                        </div>
                        <div class="flex gap-2">
                            <input type="file" id="backupFile" accept=".json" class="hidden" onchange="importStoredData(event)">
                            <button onclick="document.getElementById('backupFile').click()" class="bg-purple-600 hover:bg-purple-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                                Import Backup
                            </button>
                            <button onclick="exportStoredData()" class="bg-orange-600 hover:bg-orange-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                                Export Backup
                            </button>
                            <button onclick="showDataProtectionInfo()" class="bg-gray-400 text-white font-medium py-2 px-4 rounded-lg cursor-not-allowed" disabled>
                                Data Protected
                            </button>
                        </div>
                    </div>
                    
                    <!-- Data Status Info -->
                    <div class="mt-4 p-3 bg-blue-50 border border-blue-200 rounded-lg">
                        <div class="flex items-start">
                            <svg class="w-5 h-5 text-blue-600 mt-0.5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                            </svg>
                            <div>
                                <h4 class="font-medium text-blue-800 mb-1">Data Persistence</h4>
                                <p class="text-sm text-blue-700">All imported data is automatically saved to your browser and will persist between sessions. Use backup functions for additional data security.</p>
                            </div>
                        </div>
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

                <!-- Student Search Section -->
                <div class="bg-white rounded-2xl card-shadow p-6 mb-8">
                    <h3 class="text-xl font-semibold text-gray-800 mb-4">Student Search</h3>
                    <div class="flex space-x-4 mb-4">
                        <div class="flex-1">
                            <input type="text" id="studentSearchId" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Enter Student ID to search...">
                        </div>
                        <button onclick="searchStudent()" class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-3 px-6 rounded-lg transition duration-200">
                            Search Student
                        </button>
                        <button onclick="clearSearch()" class="bg-gray-500 hover:bg-gray-600 text-white font-medium py-3 px-4 rounded-lg transition duration-200">
                            Clear
                        </button>
                    </div>
                    
                    <!-- Search Results -->
                    <div id="searchResults" class="hidden">
                        <div class="border border-blue-200 rounded-lg p-6 bg-blue-50">
                            <h4 class="font-semibold text-blue-800 mb-4">Student Found</h4>
                            <div id="searchedStudentDetails" class="space-y-2 mb-4">
                                <!-- Student details will be populated here -->
                            </div>
                            <div class="flex flex-wrap gap-2">
                                <button onclick="viewStudentPortal()" class="bg-green-600 hover:bg-green-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                                    View Student Portal
                                </button>
                                <button onclick="recordPayment()" class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                                    Record Payment
                                </button>
                                <button onclick="clearFeesBalance()" class="bg-purple-600 hover:bg-purple-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                                    Clear Fees Balance
                                </button>
                                <div id="documentActions" class="flex gap-2">
                                    <!-- Document action buttons will be populated here -->
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Students List -->
                <div class="bg-white rounded-2xl card-shadow p-6">
                    <div class="flex justify-between items-center mb-6">
                        <h3 class="text-xl font-semibold text-gray-800">Students Fees Status</h3>
                        <div class="flex space-x-2">
                            <select id="filterYear" onchange="filterStudents()" class="px-3 py-2 border border-gray-300 rounded-lg text-sm">
                                <option value="all">All Years</option>
                            </select>
                            <select id="filterClass" onchange="filterStudents()" class="px-3 py-2 border border-gray-300 rounded-lg text-sm">
                                <option value="all">All Classes</option>
                                <option value="Senior 1">Senior 1</option>
                                <option value="Senior 2">Senior 2</option>
                                <option value="Senior 3">Senior 3</option>
                                <option value="Senior 4">Senior 4</option>
                                <option value="Senior 5">Senior 5</option>
                                <option value="Senior 6">Senior 6</option>
                            </select>
                            <select id="filterStatus" onchange="filterStudents()" class="px-3 py-2 border border-gray-300 rounded-lg text-sm">
                                <option value="all">All Students</option>
                                <option value="cleared">Fees Cleared</option>
                                <option value="outstanding">Outstanding Fees</option>
                            </select>
                        </div>
                    </div>
                    
                    <!-- Class Categories -->
                    <div id="classSections" class="space-y-8">
                        <!-- Empty state will be shown here initially -->
                        <div id="emptyState" class="text-center py-12 text-gray-500">
                            <svg class="w-16 h-16 mx-auto mb-4 text-gray-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197m13.5-9a2.5 2.5 0 11-5 0 2.5 2.5 0 015 0z"></path>
                            </svg>
                            <p class="text-lg font-medium">No student data loaded</p>
                            <p class="text-sm mt-1">Click "Import Data" to upload a CSV file and get started</p>
                        </div>
                    </div>
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
                    
                    <!-- Navigation Tabs -->
                    <div class="border-b border-gray-200">
                        <nav class="-mb-px flex space-x-8">
                            <button onclick="showTab('fees')" id="feesTab" class="py-2 px-1 border-b-2 border-blue-500 font-medium text-sm text-blue-600">
                                Fees Status
                            </button>
                            <button onclick="showTab('clearance')" id="clearanceTab" class="py-2 px-1 border-b-2 border-transparent font-medium text-sm text-gray-500 hover:text-gray-700 hover:border-gray-300">
                                Fee Clearance
                            </button>
                            <button onclick="showTab('documents')" id="documentsTab" class="py-2 px-1 border-b-2 border-transparent font-medium text-sm text-gray-500 hover:text-gray-700 hover:border-gray-300">
                                Documents
                            </button>
                        </nav>
                    </div>
                </div>

                <!-- Tab Content -->
                <div id="tabContent">
                    <!-- Fees Status Tab -->
                    <div id="feesContent" class="tab-content">
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
                    </div>

                    <!-- Fee Clearance Tab -->
                    <div id="clearanceContent" class="tab-content hidden">
                        <div class="bg-white rounded-2xl card-shadow p-6 mb-6">
                            <h3 class="text-xl font-semibold text-gray-800 mb-4">Fee Clearance Status</h3>
                            
                            <!-- Clearance Overview -->
                            <div class="bg-gradient-to-r from-blue-50 to-indigo-50 rounded-lg p-6 mb-6">
                                <div class="flex items-center mb-4">
                                    <svg class="w-8 h-8 text-blue-600 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                                    </svg>
                                    <h4 class="text-lg font-semibold text-gray-800">Clearance Requirements</h4>
                                </div>
                                <p class="text-gray-600 mb-4">To obtain your fee clearance certificate, all outstanding fees must be paid in full.</p>
                                
                                <div class="grid md:grid-cols-2 gap-4">
                                    <div class="bg-white rounded-lg p-4">
                                        <p class="text-sm text-gray-600 font-medium">Current Status</p>
                                        <p class="text-lg font-bold" id="clearanceStatus">Checking...</p>
                                    </div>
                                    <div class="bg-white rounded-lg p-4">
                                        <p class="text-sm text-gray-600 font-medium">Outstanding Amount</p>
                                        <p class="text-lg font-bold text-red-600" id="clearanceOutstanding">UGX 0</p>
                                    </div>
                                </div>
                            </div>

                            <!-- Clearance Certificate Section -->
                            <div id="clearanceCertificateSection">
                                <!-- Will be populated by JavaScript -->
                            </div>

                            <!-- Clearance History -->
                            <div class="bg-gray-50 rounded-lg p-6">
                                <h4 class="text-lg font-semibold text-gray-800 mb-4">Clearance History</h4>
                                <div id="clearanceHistory">
                                    <p class="text-gray-500 text-center py-4">No clearance records found</p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Documents Tab -->
                    <div id="documentsContent" class="tab-content hidden">
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
                                
                                <div class="space-y-4" id="studentDocumentsList">
                                    <!-- Documents will be populated by JavaScript -->
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Student data organized by year - starts empty, populate via CSV upload or sample data
        // Initialize with unlimited year support - years are added dynamically as needed
        let studentsData = {};
        const currentYear = new Date().getFullYear();
        
        // Initialize with a comprehensive range but allow infinite expansion
        for (let year = 1990; year <= currentYear + 10; year++) {
            studentsData[year] = {};
        }

        // Data persistence functions
        function saveDataToStorage() {
            try {
                localStorage.setItem('tesoStudentsData', JSON.stringify(studentsData));
                localStorage.setItem('tesoRecoveryAttempts', JSON.stringify(recoveryAttempts));
                console.log('Data saved successfully to local storage');
            } catch (error) {
                console.error('Error saving data to storage:', error);
                alert('Warning: Unable to save data to browser storage. Data may be lost on page refresh.');
            }
        }

        function loadDataFromStorage() {
            try {
                const savedStudentsData = localStorage.getItem('tesoStudentsData');
                const savedRecoveryAttempts = localStorage.getItem('tesoRecoveryAttempts');
                const savedCredentials = localStorage.getItem('tesoAdminCredentials');
                
                if (savedStudentsData) {
                    const parsedData = JSON.parse(savedStudentsData);
                    // Merge with existing structure to ensure all years are available
                    Object.keys(parsedData).forEach(year => {
                        if (parsedData[year] && Object.keys(parsedData[year]).length > 0) {
                            studentsData[year] = parsedData[year];
                        }
                    });
                    console.log('Student data loaded from storage');
                }
                
                if (savedRecoveryAttempts) {
                    recoveryAttempts = JSON.parse(savedRecoveryAttempts);
                    // Convert timestamp strings back to Date objects
                    recoveryAttempts.forEach(attempt => {
                        if (typeof attempt.timestamp === 'string') {
                            attempt.timestamp = new Date(attempt.timestamp);
                        }
                    });
                    console.log('Recovery attempts loaded from storage');
                }

                if (savedCredentials) {
                    adminCredentials = JSON.parse(savedCredentials);
                    console.log('Admin credentials loaded from storage');
                }
                
                return true;
            } catch (error) {
                console.error('Error loading data from storage:', error);
                return false;
            }
        }

        // Data protection - no deletion allowed
        function clearStoredData() {
            showDataProtectionInfo();
        }

        function exportStoredData() {
            const dataToExport = {
                studentsData: studentsData,
                recoveryAttempts: recoveryAttempts,
                exportDate: new Date().toISOString(),
                version: '1.0'
            };
            
            const dataStr = JSON.stringify(dataToExport, null, 2);
            const blob = new Blob([dataStr], { type: 'application/json' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `teso_complete_backup_${new Date().toISOString().split('T')[0]}.json`;
            a.click();
            window.URL.revokeObjectURL(url);
            
            alert('Complete system backup exported successfully!');
        }

        function importStoredData(event) {
            const file = event.target.files[0];
            if (!file) return;
            
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const importedData = JSON.parse(e.target.result);
                    
                    if (importedData.studentsData) {
                        const confirmImport = confirm('This will replace all current data with the imported backup. Continue?');
                        if (confirmImport) {
                            studentsData = importedData.studentsData;
                            
                            if (importedData.recoveryAttempts) {
                                recoveryAttempts = importedData.recoveryAttempts;
                                // Convert timestamp strings back to Date objects
                                recoveryAttempts.forEach(attempt => {
                                    if (typeof attempt.timestamp === 'string') {
                                        attempt.timestamp = new Date(attempt.timestamp);
                                    }
                                });
                            }
                            
                            // Save to storage
                            saveDataToStorage();
                            
                            // Update displays
                            updateAdminDashboard();
                            updateRecoveryHistory();
                            
                            alert(`System backup imported successfully!\nImport Date: ${importedData.exportDate || 'Unknown'}`);
                        }
                    } else {
                        alert('Invalid backup file format.');
                    }
                } catch (error) {
                    alert('Error importing backup file. Please check the file format.');
                }
            };
            reader.readAsText(file);
        }

        let currentStudent = null;
        let currentView = 'admin';
        let isAdminLoggedIn = false;
        let searchedStudent = null;

        // Recovery system variables
        let recoveryAttempts = [];
        let verifiedStudent = null;

        // Auto-save interval (every 30 seconds)
        let autoSaveInterval = null;

        // Password reset system variables
        let passwordResetSession = {
            email: null,
            verificationCode: null,
            codeExpiry: null,
            isVerified: false
        };

        // Official school email domains and addresses
        const officialSchoolEmails = [
            'admin@tesointegratedss.edu.ug',
            'principal@tesointegratedss.edu.ug',
            'bursar@tesointegratedss.edu.ug',
            'registrar@tesointegratedss.edu.ug',
            'integratedssteso@gmail.com',
            'teso.admin@education.go.ug'
        ];

        // Admin credentials storage (encrypted in real implementation)
        let adminCredentials = {
            username: 'TISS',
            password: 'Tiss@1994'
        };

        // Year management functions
        function addNewYear() {
            const year = prompt('Enter new academic year (any year from 1900 onwards):');
            if (year && !isNaN(year) && parseInt(year) >= 1900 && parseInt(year) <= 2100) {
                const yearInt = parseInt(year);
                if (!studentsData[yearInt]) {
                    studentsData[yearInt] = {};
                    updateYearDropdowns();
                    document.getElementById('academicYear').value = yearInt;
                    alert(`Academic year ${yearInt} added successfully!`);
                } else {
                    alert(`Academic year ${yearInt} already exists.`);
                }
            } else if (year !== null) {
                alert('Please enter a valid year between 1900 and 2100.');
            }
        }

        function updateYearDropdowns() {
            const years = Object.keys(studentsData).sort((a, b) => b - a);
            
            // Update academic year selector
            const academicYearSelect = document.getElementById('academicYear');
            academicYearSelect.innerHTML = '';
            years.forEach(year => {
                const option = document.createElement('option');
                option.value = year;
                option.textContent = year;
                academicYearSelect.appendChild(option);
            });
            
            // Update filter year selector
            const filterYearSelect = document.getElementById('filterYear');
            filterYearSelect.innerHTML = '<option value="all">All Years</option>';
            years.forEach(year => {
                const option = document.createElement('option');
                option.value = year;
                option.textContent = year;
                filterYearSelect.appendChild(option);
            });
        }

        // Admin login function
        function adminLogin() {
            const username = document.getElementById('adminUsername').value.trim();
            const password = document.getElementById('adminPassword').value.trim();
            
            // Check against stored credentials
            if (username === adminCredentials.username && password === adminCredentials.password) {
                isAdminLoggedIn = true;
                showAdminPortal();
                startAutoSave();
                alert('Welcome to TESO Admin Portal!');
            } else {
                alert('Invalid credentials. Please check your username and password.');
            }
        }

        // Password reset functions
        function showForgotPassword() {
            document.getElementById('forgotPasswordModal').classList.remove('hidden');
            // Reset modal to first step
            document.getElementById('emailVerificationStep').classList.remove('hidden');
            document.getElementById('codeVerificationStep').classList.add('hidden');
            document.getElementById('passwordResetStep').classList.add('hidden');
            
            // Clear form fields
            document.getElementById('resetEmail').value = '';
            document.getElementById('verificationCode').value = '';
            document.getElementById('newPassword').value = '';
            document.getElementById('confirmPassword').value = '';
            
            // Reset session
            passwordResetSession = {
                email: null,
                verificationCode: null,
                codeExpiry: null,
                isVerified: false
            };
        }

        function closeForgotPassword() {
            document.getElementById('forgotPasswordModal').classList.add('hidden');
            passwordResetSession = {
                email: null,
                verificationCode: null,
                codeExpiry: null,
                isVerified: false
            };
        }

        function verifySchoolEmail() {
            const email = document.getElementById('resetEmail').value.trim().toLowerCase();
            
            if (!email) {
                alert('Please enter an email address');
                return;
            }

            // Validate email format
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (!emailRegex.test(email)) {
                alert('Please enter a valid email address');
                return;
            }

            // Check if email is in the official school emails list
            if (!officialSchoolEmails.includes(email)) {
                alert('Access denied. Only official TESO Integrated Secondary School email addresses are authorized for password reset.\n\nAuthorized domains:\n- @tesointegratedss.edu.ug\n- integratedssteso@gmail.com\n- @education.go.ug (TESO admin only)\n\nPlease contact the school administration if you need access.');
                return;
            }

            // Generate verification code
            const verificationCode = Math.floor(100000 + Math.random() * 900000).toString();
            const expiryTime = new Date(Date.now() + 10 * 60 * 1000); // 10 minutes from now

            // Store in session
            passwordResetSession.email = email;
            passwordResetSession.verificationCode = verificationCode;
            passwordResetSession.codeExpiry = expiryTime;

            // Send verification email (simulated)
            sendPasswordResetEmail(email, verificationCode);

            // Show code verification step
            document.getElementById('emailVerificationStep').classList.add('hidden');
            document.getElementById('codeVerificationStep').classList.remove('hidden');
            
            document.getElementById('emailSentMessage').textContent = `Verification code sent to ${email}. Code expires in 10 minutes.`;
        }

        function sendPasswordResetEmail(email, code) {
            // Simulate sending email with verification code
            console.log(`Password Reset Email sent to: ${email}`);
            console.log(`Verification Code: ${code}`);
            console.log(`Expires: ${passwordResetSession.codeExpiry.toLocaleString()}`);
            
            // In a real implementation, this would send an actual email
            const emailContent = `
TESO Integrated Secondary School - Password Reset

Your password reset verification code is: ${code}

This code will expire in 10 minutes.

If you did not request this password reset, please ignore this email and contact the school administration immediately.

For security reasons, do not share this code with anyone.

TESO Integrated Secondary School
Admin Portal Security Team
            `;
            
            // Show notification that email was sent
            showNotification(`Verification code sent to ${email}`);
        }

        function verifyCode() {
            const enteredCode = document.getElementById('verificationCode').value.trim();
            
            if (!enteredCode) {
                alert('Please enter the verification code');
                return;
            }

            if (enteredCode.length !== 6) {
                alert('Verification code must be 6 digits');
                return;
            }

            // Check if code has expired
            if (new Date() > passwordResetSession.codeExpiry) {
                alert('Verification code has expired. Please request a new code.');
                return;
            }

            // Verify code
            if (enteredCode === passwordResetSession.verificationCode) {
                passwordResetSession.isVerified = true;
                
                // Show password reset step
                document.getElementById('codeVerificationStep').classList.add('hidden');
                document.getElementById('passwordResetStep').classList.remove('hidden');
                
                showNotification('Email verified successfully!');
            } else {
                alert('Invalid verification code. Please check and try again.');
            }
        }

        function resendCode() {
            if (!passwordResetSession.email) {
                alert('Session expired. Please start over.');
                closeForgotPassword();
                return;
            }

            // Generate new verification code
            const verificationCode = Math.floor(100000 + Math.random() * 900000).toString();
            const expiryTime = new Date(Date.now() + 10 * 60 * 1000); // 10 minutes from now

            // Update session
            passwordResetSession.verificationCode = verificationCode;
            passwordResetSession.codeExpiry = expiryTime;

            // Send new verification email
            sendPasswordResetEmail(passwordResetSession.email, verificationCode);
            
            document.getElementById('emailSentMessage').textContent = `New verification code sent to ${passwordResetSession.email}. Code expires in 10 minutes.`;
            document.getElementById('verificationCode').value = '';
        }

        function resetPassword() {
            if (!passwordResetSession.isVerified) {
                alert('Email verification required');
                return;
            }

            const newPassword = document.getElementById('newPassword').value;
            const confirmPassword = document.getElementById('confirmPassword').value;

            if (!newPassword || !confirmPassword) {
                alert('Please fill in both password fields');
                return;
            }

            if (newPassword.length < 6) {
                alert('Password must be at least 6 characters long');
                return;
            }

            if (newPassword !== confirmPassword) {
                alert('Passwords do not match');
                return;
            }

            // Update admin credentials
            adminCredentials.password = newPassword;
            
            // Save to localStorage for persistence
            try {
                localStorage.setItem('tesoAdminCredentials', JSON.stringify(adminCredentials));
            } catch (error) {
                console.error('Error saving credentials:', error);
            }

            // Send confirmation email
            sendPasswordResetConfirmation(passwordResetSession.email);

            // Close modal and show success
            closeForgotPassword();
            alert('Password reset successful!\n\nYour new password has been set and you can now login with your updated credentials.\n\nA confirmation email has been sent to your registered email address.');
        }

        function sendPasswordResetConfirmation(email) {
            console.log(`Password Reset Confirmation sent to: ${email}`);
            
            const confirmationContent = `
TESO Integrated Secondary School - Password Reset Confirmation

Your admin portal password has been successfully reset.

Reset Details:
- Email: ${email}
- Date: ${new Date().toLocaleString()}
- IP Address: [System Protected]

If you did not perform this password reset, please contact the school administration immediately.

For security:
- Do not share your login credentials with anyone
- Use a strong, unique password
- Log out when finished using the system

TESO Integrated Secondary School
Admin Portal Security Team
            `;
            
            showNotification('Password reset confirmation sent');
        }

        function showDataProtectionInfo() {
            alert('Data Protection Policy\n\nAll student records and financial data in this system are permanently protected and cannot be deleted to ensure:\n\n• Academic record integrity\n• Financial audit compliance\n• Legal documentation requirements\n• Student data security\n\nThis protection prevents accidental or unauthorized data loss and maintains the complete historical record of all student fees and payments.\n\nFor data management inquiries, contact the school administration.');
        }

        function showAdminPortal() {
            if (!isAdminLoggedIn) {
                alert('Please login first');
                return;
            }
            
            document.getElementById('adminPortal').classList.remove('hidden');
            updateAdminDashboard();
        }

        function adminLogout() {
            isAdminLoggedIn = false;
            searchedStudent = null;
            currentStudent = null;
            
            // Clear forms
            document.getElementById('adminUsername').value = '';
            document.getElementById('adminPassword').value = '';
            document.getElementById('studentSearchId').value = '';
            document.getElementById('searchResults').classList.add('hidden');
            
            // Hide admin portal and show login
            document.getElementById('adminPortal').classList.add('hidden');
            document.getElementById('dashboard').classList.add('hidden');
            
            // Stop auto-save
            stopAutoSave();
            
            alert('Logged out successfully');
        }

        // Student search functions
        function searchStudent() {
            const studentId = document.getElementById('studentSearchId').value.trim();
            
            if (!studentId) {
                alert('Please enter a Student ID to search');
                return;
            }

            // Search across all years for the student
            let foundStudent = null;
            let foundYear = null;
            
            for (const year in studentsData) {
                if (studentsData[year][studentId]) {
                    foundStudent = studentsData[year][studentId];
                    foundYear = year;
                    break;
                }
            }

            if (!foundStudent) {
                alert('Student ID not found in the system. Please check the ID or ensure student data is loaded.');
                document.getElementById('searchResults').classList.add('hidden');
                return;
            }

            // Store searched student
            searchedStudent = { id: studentId, year: foundYear, ...foundStudent };
            displaySearchResults();
        }

        function displaySearchResults() {
            const resultsDiv = document.getElementById('searchResults');
            const detailsDiv = document.getElementById('searchedStudentDetails');
            
            const outstanding = searchedStudent.totalFees - searchedStudent.amountPaid;
            
            detailsDiv.innerHTML = `
                <div class="grid grid-cols-2 gap-4">
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Student ID:</span>
                        <span class="text-gray-900">${searchedStudent.id}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Name:</span>
                        <span class="text-gray-900">${searchedStudent.name}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Academic Year:</span>
                        <span class="text-gray-900 font-semibold text-blue-600">${searchedStudent.year}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Class:</span>
                        <span class="text-gray-900">${searchedStudent.class}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Total Fees:</span>
                        <span class="text-gray-900">UGX ${searchedStudent.totalFees.toLocaleString()}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Amount Paid:</span>
                        <span class="text-gray-900">UGX ${searchedStudent.amountPaid.toLocaleString()}</span>
                    </div>
                    <div class="flex justify-between col-span-2">
                        <span class="font-medium text-gray-700">Outstanding Balance:</span>
                        <span class="text-gray-900 ${outstanding > 0 ? 'text-red-600' : 'text-green-600'} font-bold flex items-center">
                            UGX ${outstanding.toLocaleString()}
                            ${outstanding === 0 ? '<svg class="w-5 h-5 text-green-600 ml-2" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg>' : ''}
                        </span>
                    </div>
                    <div class="flex justify-between col-span-2">
                        <span class="font-medium text-gray-700">Status:</span>
                        <span class="px-2 py-1 text-xs rounded-full ${outstanding === 0 ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'} flex items-center">
                            ${outstanding === 0 ? '<svg class="w-3 h-3 mr-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg>' : ''}
                            ${outstanding === 0 ? 'Fees Cleared' : 'Outstanding Fees'}
                        </span>
                    </div>
                </div>
            `;
            
            // Update document action buttons based on class level
            updateDocumentActionButtons();
            
            resultsDiv.classList.remove('hidden');
        }

        function updateDocumentActionButtons() {
            const documentActionsDiv = document.getElementById('documentActions');
            
            if (!searchedStudent) {
                documentActionsDiv.innerHTML = '';
                return;
            }
            
            // Check if student is in S4 or S6
            const classLevel = searchedStudent.class.toLowerCase();
            const isS4 = classLevel.includes('senior 4') || classLevel.includes('s4');
            const isS6 = classLevel.includes('senior 6') || classLevel.includes('s6');
            
            if (!isS4 && !isS6) {
                documentActionsDiv.innerHTML = '';
                return;
            }
            
            // Initialize documents object if it doesn't exist
            if (!searchedStudent.documents) {
                searchedStudent.documents = {};
            }
            
            let buttonsHTML = '<div class="space-y-3">';
            
            if (isS4) {
                const resultsIssued = searchedStudent.documents.results && searchedStudent.documents.results.issued;
                const resultsDate = searchedStudent.documents.results && searchedStudent.documents.results.issuedDate ? 
                    new Date(searchedStudent.documents.results.issuedDate).toISOString().split('T')[0] : '';
                
                buttonsHTML += `
                    <div class="flex items-center space-x-3">
                        <button onclick="toggleDocumentIssue('results')" 
                                class="px-3 py-2 rounded-lg font-medium text-sm transition duration-200 ${resultsIssued ? 'bg-green-100 text-green-800 hover:bg-green-200' : 'bg-orange-100 text-orange-800 hover:bg-orange-200'}">
                            ${resultsIssued ? 'Results Issued ✓' : 'Issue S4 Results'}
                        </button>
                        ${resultsIssued ? 
                            `<span class="text-sm text-gray-600">Issued: ${new Date(searchedStudent.documents.results.issuedDate).toLocaleDateString()}</span>` :
                            `<input type="date" id="resultsDate" class="px-2 py-1 border border-gray-300 rounded text-sm" placeholder="Issue date">`
                        }
                    </div>
                `;
            }
            
            if (isS6) {
                const resultsIssued = searchedStudent.documents.results && searchedStudent.documents.results.issued;
                const certificateIssued = searchedStudent.documents.certificate && searchedStudent.documents.certificate.issued;
                
                buttonsHTML += `
                    <div class="flex items-center space-x-3">
                        <button onclick="toggleDocumentIssue('results')" 
                                class="px-3 py-2 rounded-lg font-medium text-sm transition duration-200 ${resultsIssued ? 'bg-green-100 text-green-800 hover:bg-green-200' : 'bg-orange-100 text-orange-800 hover:bg-orange-200'}">
                            ${resultsIssued ? 'Results Issued ✓' : 'Issue S6 Results'}
                        </button>
                        ${resultsIssued ? 
                            `<span class="text-sm text-gray-600">Issued: ${new Date(searchedStudent.documents.results.issuedDate).toLocaleDateString()}</span>` :
                            `<input type="date" id="resultsDate" class="px-2 py-1 border border-gray-300 rounded text-sm" placeholder="Issue date">`
                        }
                    </div>
                    <div class="flex items-center space-x-3">
                        <button onclick="toggleDocumentIssue('certificate')" 
                                class="px-3 py-2 rounded-lg font-medium text-sm transition duration-200 ${certificateIssued ? 'bg-green-100 text-green-800 hover:bg-green-200' : 'bg-orange-100 text-orange-800 hover:bg-orange-200'}">
                            ${certificateIssued ? 'Certificate Issued ✓' : 'Issue Certificate'}
                        </button>
                        ${certificateIssued ? 
                            `<span class="text-sm text-gray-600">Issued: ${new Date(searchedStudent.documents.certificate.issuedDate).toLocaleDateString()}</span>` :
                            `<input type="date" id="certificateDate" class="px-2 py-1 border border-gray-300 rounded text-sm" placeholder="Issue date">`
                        }
                    </div>
                `;
            }
            
            buttonsHTML += '</div>';
            documentActionsDiv.innerHTML = buttonsHTML;
        }

        function clearFeesBalance() {
            if (!searchedStudent) {
                alert('No student selected');
                return;
            }

            const outstanding = searchedStudent.totalFees - searchedStudent.amountPaid;
            
            if (outstanding === 0) {
                alert('Student fees are already cleared.');
                return;
            }

            const confirmClear = confirm(`Clear outstanding fees balance for ${searchedStudent.name}?\n\nCurrent Outstanding: UGX ${outstanding.toLocaleString()}\n\nThis will mark all fees as paid and cannot be undone.`);
            
            if (confirmClear) {
                // Record the clearance as a transaction
                if (!searchedStudent.transactions) {
                    searchedStudent.transactions = [];
                }
                
                const clearanceTransaction = {
                    id: `ADMIN_CLEAR_${Date.now()}`,
                    amount: outstanding,
                    method: 'admin_clearance',
                    date: new Date().toISOString(),
                    timestamp: Date.now(),
                    note: 'Fees cleared by admin'
                };
                
                searchedStudent.transactions.push(clearanceTransaction);
                searchedStudent.amountPaid = searchedStudent.totalFees;
                
                // Update the main data store
                if (studentsData[searchedStudent.year] && studentsData[searchedStudent.year][searchedStudent.id]) {
                    studentsData[searchedStudent.year][searchedStudent.id].amountPaid = searchedStudent.amountPaid;
                    if (!studentsData[searchedStudent.year][searchedStudent.id].transactions) {
                        studentsData[searchedStudent.year][searchedStudent.id].transactions = [];
                    }
                    studentsData[searchedStudent.year][searchedStudent.id].transactions.push(clearanceTransaction);
                    
                    // Initialize documents if they don't exist
                    if (!studentsData[searchedStudent.year][searchedStudent.id].documents) {
                        studentsData[searchedStudent.year][searchedStudent.id].documents = {};
                    }
                    
                    // Copy documents status to main data store
                    if (searchedStudent.documents) {
                        studentsData[searchedStudent.year][searchedStudent.id].documents = { ...searchedStudent.documents };
                    }
                }

                // Save data to storage
                saveDataToStorage();
                
                // Send email notification
                sendEmailNotification('fees_cleared', {
                    studentName: searchedStudent.name,
                    studentId: searchedStudent.id,
                    class: searchedStudent.class,
                    year: searchedStudent.year,
                    totalFees: searchedStudent.totalFees,
                    totalPaid: searchedStudent.amountPaid,
                    clearedBy: 'Admin'
                });
                
                // Update displays
                displaySearchResults();
                updateAdminDashboard();
                
                alert(`Fees balance cleared successfully!\n\nStudent: ${searchedStudent.name}\nAmount Cleared: UGX ${outstanding.toLocaleString()}\nStatus: All fees now paid\n\nThe student can now access their documents and clearance certificates.`);
            }
        }

        function toggleDocumentIssue(documentType) {
            if (!searchedStudent) {
                alert('No student selected');
                return;
            }

            // Initialize documents object if it doesn't exist
            if (!searchedStudent.documents) {
                searchedStudent.documents = {};
            }

            const isCurrentlyIssued = searchedStudent.documents[documentType] && searchedStudent.documents[documentType].issued;
            const documentName = documentType === 'results' ? 'Results Slip' : 'Certificate';
            const classLevel = searchedStudent.class.toLowerCase();
            const isS4 = classLevel.includes('senior 4') || classLevel.includes('s4');
            const isS6 = classLevel.includes('senior 6') || classLevel.includes('s6');
            
            // Verify student is eligible for document
            if (!isS4 && !isS6) {
                alert(`${documentName} can only be issued to Senior 4 and Senior 6 students.`);
                return;
            }

            if (documentType === 'certificate' && !isS6) {
                alert('Certificates can only be issued to Senior 6 students.');
                return;
            }

            const action = isCurrentlyIssued ? 'revoke' : 'issue';
            
            if (action === 'issue') {
                // Get the date from the input field
                const dateInputId = documentType === 'results' ? 'resultsDate' : 'certificateDate';
                const dateInput = document.getElementById(dateInputId);
                
                if (!dateInput || !dateInput.value) {
                    alert(`Please select the ${documentName.toLowerCase()} issue date first.`);
                    return;
                }
                
                const issueDate = new Date(dateInput.value);
                const today = new Date();
                
                if (issueDate > today) {
                    alert('Issue date cannot be in the future.');
                    return;
                }
                
                const confirmMessage = `Issue ${documentName} for ${searchedStudent.name}?\n\nStudent: ${searchedStudent.name}\nClass: ${searchedStudent.class}\nDocument: ${documentName}\nIssue Date: ${issueDate.toLocaleDateString()}\n\nThis action will be logged and cannot be easily undone.`;
                
                if (confirm(confirmMessage)) {
                    // Update document status
                    if (!searchedStudent.documents[documentType]) {
                        searchedStudent.documents[documentType] = {};
                    }
                    
                    searchedStudent.documents[documentType].issued = true;
                    searchedStudent.documents[documentType].issuedDate = issueDate.toISOString();
                    searchedStudent.documents[documentType].issuedBy = 'Admin';
                    
                    // Update the main data store
                    if (studentsData[searchedStudent.year] && studentsData[searchedStudent.year][searchedStudent.id]) {
                        if (!studentsData[searchedStudent.year][searchedStudent.id].documents) {
                            studentsData[searchedStudent.year][searchedStudent.id].documents = {};
                        }
                        studentsData[searchedStudent.year][searchedStudent.id].documents[documentType] = { ...searchedStudent.documents[documentType] };
                    }

                    // Save data to storage
                    saveDataToStorage();
                    
                    // Send email notification
                    sendEmailNotification('document_issued', {
                        studentName: searchedStudent.name,
                        studentId: searchedStudent.id,
                        class: searchedStudent.class,
                        year: searchedStudent.year,
                        documentType: documentName,
                        action: action,
                        issuedBy: 'Admin',
                        date: issueDate.toLocaleDateString()
                    });
                    
                    // Update displays
                    updateDocumentActionButtons();
                    updateAdminDashboard();
                    
                    alert(`${documentName} issued successfully!\n\nStudent: ${searchedStudent.name}\nDocument: ${documentName}\nIssue Date: ${issueDate.toLocaleDateString()}`);
                }
            } else {
                // Revoke document
                const confirmMessage = `Revoke ${documentName} for ${searchedStudent.name}?\n\nStudent: ${searchedStudent.name}\nClass: ${searchedStudent.class}\nDocument: ${documentName}\n\nThis action will be logged and cannot be easily undone.`;
                
                if (confirm(confirmMessage)) {
                    searchedStudent.documents[documentType].issued = false;
                    searchedStudent.documents[documentType].revokedDate = new Date().toISOString();
                    searchedStudent.documents[documentType].revokedBy = 'Admin';
                    
                    // Update the main data store
                    if (studentsData[searchedStudent.year] && studentsData[searchedStudent.year][searchedStudent.id]) {
                        studentsData[searchedStudent.year][searchedStudent.id].documents[documentType] = { ...searchedStudent.documents[documentType] };
                    }

                    // Save data to storage
                    saveDataToStorage();
                    
                    // Send email notification
                    sendEmailNotification('document_issued', {
                        studentName: searchedStudent.name,
                        studentId: searchedStudent.id,
                        class: searchedStudent.class,
                        year: searchedStudent.year,
                        documentType: documentName,
                        action: action,
                        issuedBy: 'Admin',
                        date: new Date().toLocaleDateString()
                    });
                    
                    // Update displays
                    updateDocumentActionButtons();
                    updateAdminDashboard();
                    
                    alert(`${documentName} revoked successfully!\n\nStudent: ${searchedStudent.name}\nDocument: ${documentName}\nRevoked Date: ${new Date().toLocaleDateString()}`);
                }
            }
        }

        function clearSearch() {
            document.getElementById('studentSearchId').value = '';
            document.getElementById('searchResults').classList.add('hidden');
            searchedStudent = null;
        }

        function viewStudentPortal() {
            if (!searchedStudent) {
                alert('No student selected');
                return;
            }

            currentStudent = searchedStudent;
            showDashboard();
        }

        function recordPayment() {
            if (!searchedStudent) {
                alert('No student selected');
                return;
            }

            const amount = prompt('Enter payment amount (UGX):');
            if (!amount || isNaN(amount) || parseInt(amount) <= 0) {
                alert('Please enter a valid payment amount');
                return;
            }

            const method = prompt('Enter payment method (e.g., Mobile Money, Bank Transfer, Cash):');
            if (!method) {
                alert('Please enter a payment method');
                return;
            }

            const transactionId = prompt('Enter transaction ID:');
            if (!transactionId) {
                alert('Please enter a transaction ID');
                return;
            }

            const paymentAmount = parseInt(amount);
            const outstanding = searchedStudent.totalFees - searchedStudent.amountPaid;
            
            if (paymentAmount > outstanding) {
                alert(`Payment amount cannot exceed outstanding balance of UGX ${outstanding.toLocaleString()}`);
                return;
            }

            // Check if transaction ID already exists
            if (searchedStudent.transactions) {
                const existingTransaction = searchedStudent.transactions.find(t => t.id === transactionId);
                if (existingTransaction) {
                    alert('This transaction ID has already been used. Please enter a unique transaction ID.');
                    return;
                }
            }

            const confirmPayment = confirm(`Record payment for ${searchedStudent.name}?\n\nAmount: UGX ${paymentAmount.toLocaleString()}\nMethod: ${method}\nTransaction ID: ${transactionId}`);
            
            if (confirmPayment) {
                // Initialize transactions array if it doesn't exist
                if (!searchedStudent.transactions) {
                    searchedStudent.transactions = [];
                }
                
                // Record the transaction
                const transaction = {
                    id: transactionId,
                    amount: paymentAmount,
                    method: method.toLowerCase().replace(' ', '_'),
                    date: new Date().toISOString(),
                    timestamp: Date.now()
                };
                
                searchedStudent.transactions.push(transaction);
                searchedStudent.amountPaid += paymentAmount;
                
                // Update the main data store
                if (studentsData[searchedStudent.year] && studentsData[searchedStudent.year][searchedStudent.id]) {
                    studentsData[searchedStudent.year][searchedStudent.id].amountPaid = searchedStudent.amountPaid;
                    if (!studentsData[searchedStudent.year][searchedStudent.id].transactions) {
                        studentsData[searchedStudent.year][searchedStudent.id].transactions = [];
                    }
                    studentsData[searchedStudent.year][searchedStudent.id].transactions.push(transaction);
                }

                // Save data to storage
                saveDataToStorage();
                
                // Send email notifications
                const newOutstanding = searchedStudent.totalFees - searchedStudent.amountPaid;
                
                sendEmailNotification('payment_received', {
                    studentName: searchedStudent.name,
                    studentId: searchedStudent.id,
                    class: searchedStudent.class,
                    year: searchedStudent.year,
                    amount: paymentAmount,
                    method: method,
                    transactionId: transactionId,
                    date: new Date().toLocaleDateString(),
                    outstanding: newOutstanding
                });
                
                if (newOutstanding === 0) {
                    sendEmailNotification('fees_cleared', {
                        studentName: searchedStudent.name,
                        studentId: searchedStudent.id,
                        class: searchedStudent.class,
                        year: searchedStudent.year,
                        totalFees: searchedStudent.totalFees,
                        totalPaid: searchedStudent.amountPaid
                    });
                }
                
                // Update displays
                displaySearchResults();
                updateAdminDashboard();
                
                alert(`Payment recorded successfully!\n\nStudent: ${searchedStudent.name}\nAmount: UGX ${paymentAmount.toLocaleString()}\nNew Outstanding: UGX ${newOutstanding.toLocaleString()}`);
            }
        }

        // Recovery functions
        function verifyStudentForRecovery() {
            const studentId = document.getElementById('recoveryStudentId').value.trim();
            
            if (!studentId) {
                alert('Please enter a Student ID to verify');
                return;
            }

            // Search across all years for the student
            let foundStudent = null;
            let foundYear = null;
            
            for (const year in studentsData) {
                if (studentsData[year][studentId]) {
                    foundStudent = studentsData[year][studentId];
                    foundYear = year;
                    break;
                }
            }

            if (!foundStudent) {
                alert('Student ID not found in the system. Please check the ID or ensure student data is loaded.');
                
                // Log failed attempt
                recoveryAttempts.push({
                    studentId: studentId,
                    timestamp: new Date(),
                    status: 'failed',
                    reason: 'Student ID not found'
                });
                updateRecoveryHistory();
                return;
            }

            // Show verification results
            verifiedStudent = { id: studentId, year: foundYear, ...foundStudent };
            displayVerificationResults();
            
            // Log verification attempt
            recoveryAttempts.push({
                studentId: studentId,
                studentName: foundStudent.name,
                year: foundYear,
                timestamp: new Date(),
                status: 'verified',
                reason: 'Identity verified by admin'
            });
            
            // Save recovery data to storage
            saveDataToStorage();
            
            // Send email notification for verification
            sendEmailNotification('recovery_request', {
                studentId: studentId,
                studentName: foundStudent.name,
                status: 'verified',
                reason: 'Identity verified by admin'
            });
            
            updateRecoveryHistory();
        }

        function displayVerificationResults() {
            const resultsDiv = document.getElementById('verificationResults');
            const detailsDiv = document.getElementById('studentDetails');
            
            const outstanding = verifiedStudent.totalFees - verifiedStudent.amountPaid;
            
            detailsDiv.innerHTML = `
                <div class="space-y-2">
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Student ID:</span>
                        <span class="text-gray-900">${verifiedStudent.id}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Name:</span>
                        <span class="text-gray-900">${verifiedStudent.name}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Academic Year:</span>
                        <span class="text-gray-900 font-semibold text-blue-600">${verifiedStudent.year}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Class:</span>
                        <span class="text-gray-900">${verifiedStudent.class}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Outstanding Balance:</span>
                        <span class="text-gray-900 ${outstanding > 0 ? 'text-red-600' : 'text-green-600'}">
                            UGX ${outstanding.toLocaleString()}
                        </span>
                    </div>
                    <div class="flex justify-between">
                        <span class="font-medium text-gray-700">Status:</span>
                        <span class="px-2 py-1 text-xs rounded-full ${outstanding === 0 ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}">
                            ${outstanding === 0 ? 'Fees Cleared' : 'Outstanding Fees'}
                        </span>
                    </div>
                </div>
            `;
            
            resultsDiv.classList.remove('hidden');
        }

        function grantAccess() {
            if (!verifiedStudent) {
                alert('No student verified for access');
                return;
            }

            const confirmGrant = confirm(`Provide website access credentials to:\n\nStudent ID: ${verifiedStudent.id}\nName: ${verifiedStudent.name}\nClass: ${verifiedStudent.class}\n\nThis will give them their login information for website access.`);
            
            if (confirmGrant) {
                // Log the granted access
                recoveryAttempts.push({
                    studentId: verifiedStudent.id,
                    studentName: verifiedStudent.name,
                    timestamp: new Date(),
                    status: 'granted',
                    reason: 'Website access credentials provided by admin'
                });
                
                // Save recovery data to storage
                saveDataToStorage();
                
                // Send email notification for granted access
                sendEmailNotification('recovery_request', {
                    studentId: verifiedStudent.id,
                    studentName: verifiedStudent.name,
                    status: 'granted',
                    reason: 'Website access credentials provided by admin'
                });
                
                // Set current student and show dashboard
                currentStudent = verifiedStudent;
                
                // Hide login section and show dashboard
                document.getElementById('loginSection').classList.add('hidden');
                showDashboard();
                
                // Reset recovery interface
                resetRecoveryInterface();
                
                alert(`Website access provided successfully!\n\n${verifiedStudent.name} has been given their login credentials.\n\nStudent ID: ${verifiedStudent.id}\nThey can now use this ID to access the website.`);
            }
        }

        function denyAccess() {
            if (!verifiedStudent) {
                alert('No student verified for access');
                return;
            }

            const reason = prompt(`Deny access to ${verifiedStudent.name}?\n\nPlease enter reason for denial:`);
            
            if (reason !== null) {
                // Log the denied access
                recoveryAttempts.push({
                    studentId: verifiedStudent.id,
                    studentName: verifiedStudent.name,
                    timestamp: new Date(),
                    status: 'denied',
                    reason: reason || 'Access denied by admin'
                });
                
                // Save recovery data to storage
                saveDataToStorage();
                
                // Send email notification for denied access
                sendEmailNotification('recovery_request', {
                    studentId: verifiedStudent.id,
                    studentName: verifiedStudent.name,
                    status: 'denied',
                    reason: reason || 'Access denied by admin'
                });
                
                updateRecoveryHistory();
                resetRecoveryInterface();
                
                alert(`Access denied for ${verifiedStudent.name}.\nReason: ${reason || 'Access denied by admin'}`);
            }
        }

        function resetRecoveryInterface() {
            document.getElementById('recoveryStudentId').value = '';
            document.getElementById('verificationResults').classList.add('hidden');
            verifiedStudent = null;
        }

        function updateRecoveryHistory() {
            const historyDiv = document.getElementById('recoveryHistory');
            
            if (recoveryAttempts.length === 0) {
                historyDiv.innerHTML = '<p class="text-sm text-gray-500 text-center py-4">No recent website access recovery attempts</p>';
                return;
            }

            // Show last 5 attempts
            const recentAttempts = recoveryAttempts.slice(-5).reverse();
            
            let historyHTML = '';
            recentAttempts.forEach(attempt => {
                const date = attempt.timestamp.toLocaleDateString();
                const time = attempt.timestamp.toLocaleTimeString();
                
                let statusColor = 'gray';
                let statusText = attempt.status;
                
                switch(attempt.status) {
                    case 'verified':
                        statusColor = 'blue';
                        statusText = 'Verified';
                        break;
                    case 'granted':
                        statusColor = 'green';
                        statusText = 'Credentials Provided';
                        break;
                    case 'denied':
                        statusColor = 'red';
                        statusText = 'Access Denied';
                        break;
                    case 'failed':
                        statusColor = 'red';
                        statusText = 'Verification Failed';
                        break;
                }
                
                historyHTML += `
                    <div class="flex justify-between items-center py-2 px-3 bg-gray-50 rounded-lg">
                        <div class="flex-1">
                            <div class="flex items-center space-x-2">
                                <span class="text-sm font-medium text-gray-900">${attempt.studentId}</span>
                                ${attempt.studentName ? `<span class="text-sm text-gray-600">- ${attempt.studentName}</span>` : ''}
                            </div>
                            <p class="text-xs text-gray-500">${attempt.reason}</p>
                        </div>
                        <div class="text-right">
                            <span class="px-2 py-1 text-xs rounded-full bg-${statusColor}-100 text-${statusColor}-800">
                                ${statusText}
                            </span>
                            <p class="text-xs text-gray-500 mt-1">${date} ${time}</p>
                        </div>
                    </div>
                `;
            });
            
            historyDiv.innerHTML = historyHTML;
        }

        // Admin functions
        function updateAdminDashboard() {
            let totalStudents = 0;
            let totalExpected = 0;
            let totalRecovered = 0;
            let totalOutstanding = 0;

            // Calculate totals across all years
            Object.keys(studentsData).forEach(year => {
                const yearStudents = Object.keys(studentsData[year]);
                totalStudents += yearStudents.length;
                
                yearStudents.forEach(id => {
                    const student = studentsData[year][id];
                    totalExpected += student.totalFees;
                    totalRecovered += student.amountPaid;
                    totalOutstanding += (student.totalFees - student.amountPaid);
                });
            });

            document.getElementById('totalStudents').textContent = totalStudents;
            document.getElementById('totalFeesExpected').textContent = `UGX ${totalExpected.toLocaleString()}`;
            document.getElementById('feesRecovered').textContent = `UGX ${totalRecovered.toLocaleString()}`;
            document.getElementById('totalOutstanding').textContent = `UGX ${totalOutstanding.toLocaleString()}`;

            updateYearDropdowns();
            populateStudentsTable();
        }

        function populateStudentsTable() {
            const classSections = document.getElementById('classSections');
            const emptyState = document.getElementById('emptyState');
            const statusFilter = document.getElementById('filterStatus').value;
            const classFilter = document.getElementById('filterClass').value;
            const yearFilter = document.getElementById('filterYear').value;
            
            let totalStudents = 0;
            
            // Count total students across all years
            Object.keys(studentsData).forEach(year => {
                totalStudents += Object.keys(studentsData[year]).length;
            });
            
            if (totalStudents === 0) {
                emptyState.classList.remove('hidden');
                classSections.innerHTML = '';
                classSections.appendChild(emptyState);
                return;
            }

            emptyState.classList.add('hidden');
            
            // Group students by year and class level
            const yearClassSummary = {};
            
            Object.keys(studentsData).forEach(year => {
                if (yearFilter !== 'all' && yearFilter !== year) return;
                
                const yearStudents = Object.keys(studentsData[year]);
                
                yearStudents.forEach(id => {
                    const student = studentsData[year][id];
                    const outstanding = student.totalFees - student.amountPaid;
                    const isCleared = outstanding === 0;
                    
                    // Apply filters
                    if (statusFilter === 'cleared' && !isCleared) return;
                    if (statusFilter === 'outstanding' && isCleared) return;
                    
                    // Extract class level (e.g., "Senior 4" from "Senior 4 - Science")
                    const classLevel = student.class.split(' - ')[0] || student.class.split(' ')[0] + ' ' + student.class.split(' ')[1];
                    
                    if (classFilter !== 'all' && classLevel !== classFilter) return;
                    
                    const yearClassKey = `${year} - ${classLevel}`;
                    
                    if (!yearClassSummary[yearClassKey]) {
                        yearClassSummary[yearClassKey] = {
                            year: year,
                            classLevel: classLevel,
                            students: []
                        };
                    }
                    
                    yearClassSummary[yearClassKey].students.push({
                        id,
                        year,
                        ...student,
                        outstanding,
                        isCleared
                    });
                });
            });

            // Sort year-class combinations
            const sortedYearClasses = Object.keys(yearClassSummary).sort((a, b) => {
                const [yearA, classA] = a.split(' - ');
                const [yearB, classB] = b.split(' - ');
                
                // Sort by year first (descending), then by class level
                if (yearA !== yearB) {
                    return yearB - yearA;
                }
                
                const getClassNumber = (className) => {
                    const match = className.match(/Senior (\d+)/);
                    return match ? parseInt(match[1]) : 0;
                };
                return getClassNumber(classA) - getClassNumber(classB);
            });

            let sectionsHTML = '';
            
            sortedYearClasses.forEach(yearClassKey => {
                const yearClassData = yearClassSummary[yearClassKey];
                const classStudents = yearClassData.students;
                const totalStudents = classStudents.length;
                const clearedStudents = classStudents.filter(s => s.isCleared).length;
                const outstandingStudents = totalStudents - clearedStudents;
                
                const totalFees = classStudents.reduce((sum, s) => sum + s.totalFees, 0);
                const totalPaid = classStudents.reduce((sum, s) => sum + s.amountPaid, 0);
                const totalOutstanding = totalFees - totalPaid;
                
                sectionsHTML += `
                    <div class="border border-gray-200 rounded-lg overflow-hidden">
                        <!-- Class Header -->
                        <div class="bg-gradient-to-r from-blue-50 to-indigo-50 px-6 py-4 border-b border-gray-200">
                            <div class="flex justify-between items-center">
                                <div>
                                    <h4 class="text-lg font-semibold text-gray-800">${yearClassData.classLevel}</h4>
                                    <div class="flex items-center space-x-4">
                                        <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-blue-100 text-blue-800">
                                            Academic Year ${yearClassData.year}
                                        </span>
                                        <p class="text-sm text-gray-600">${totalStudents} students • ${clearedStudents} cleared • ${outstandingStudents} outstanding</p>
                                    </div>
                                </div>
                                <div class="text-right">
                                    <p class="text-sm text-gray-600">Total Outstanding</p>
                                    <p class="text-lg font-bold ${totalOutstanding > 0 ? 'text-red-600' : 'text-green-600'}">
                                        UGX ${totalOutstanding.toLocaleString()}
                                    </p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Students Table -->
                        <div class="overflow-x-auto">
                            <table class="w-full">
                                <thead class="bg-gray-50">
                                    <tr>
                                        <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Student ID</th>
                                        <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Name</th>
                                        <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Class Details</th>
                                        <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Total Fees</th>
                                        <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Amount Paid</th>
                                        <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Outstanding</th>
                                        <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                                    </tr>
                                </thead>
                                <tbody class="bg-white divide-y divide-gray-200">
                `;
                
                classStudents.forEach(student => {
                    sectionsHTML += `
                        <tr class="hover:bg-gray-50">
                            <td class="px-4 py-4 whitespace-nowrap text-sm font-medium text-gray-900">${student.id}</td>
                            <td class="px-4 py-4 whitespace-nowrap text-sm text-gray-900">${student.name}</td>
                            <td class="px-4 py-4 whitespace-nowrap text-sm text-gray-900">${student.class}</td>
                            <td class="px-4 py-4 whitespace-nowrap text-sm text-gray-900">UGX ${student.totalFees.toLocaleString()}</td>
                            <td class="px-4 py-4 whitespace-nowrap text-sm text-gray-900">UGX ${student.amountPaid.toLocaleString()}</td>
                            <td class="px-4 py-4 whitespace-nowrap text-sm text-gray-900">UGX ${student.outstanding.toLocaleString()}</td>
                            <td class="px-4 py-4 whitespace-nowrap">
                                <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${student.isCleared ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'} items-center">
                                    ${student.isCleared ? '<svg class="w-3 h-3 mr-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg>' : ''}
                                    ${student.isCleared ? 'Cleared' : 'Outstanding'}
                                </span>
                            </td>
                        </tr>
                    `;
                });
                
                sectionsHTML += `
                                </tbody>
                            </table>
                        </div>
                    </div>
                `;
            });
            
            if (sectionsHTML === '') {
                sectionsHTML = `
                    <div class="text-center py-12 text-gray-500">
                        <svg class="w-16 h-16 mx-auto mb-4 text-gray-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197m13.5-9a2.5 2.5 0 11-5 0 2.5 2.5 0 015 0z"></path>
                        </svg>
                        <p class="text-lg font-medium">No students match the selected filters</p>
                        <p class="text-sm mt-1">Try adjusting your filter settings</p>
                    </div>
                `;
            }
            
            classSections.innerHTML = sectionsHTML;
        }

        function filterStudents() {
            populateStudentsTable();
        }

        function handleFileUpload(event) {
            const file = event.target.files[0];
            if (!file) return;

            const selectedYear = document.getElementById('academicYear').value;
            if (!selectedYear) {
                alert('Please select an academic year first.');
                return;
            }

            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const data = new Uint8Array(e.target.result);
                    const workbook = XLSX.read(data, { type: 'array' });
                    const firstSheetName = workbook.SheetNames[0];
                    const worksheet = workbook.Sheets[firstSheetName];
                    const jsonData = XLSX.utils.sheet_to_json(worksheet, { header: 1 });
                    
                    const newStudentsData = {};
                    
                    // Skip header row (index 0)
                    for (let i = 1; i < jsonData.length; i++) {
                        const row = jsonData[i];
                        if (!row || row.length < 5) continue;

                        const [studentId, name, studentClass, totalFees, amountPaid] = row;
                        
                        if (studentId && name && studentClass && totalFees && amountPaid) {
                            newStudentsData[String(studentId).trim()] = {
                                name: String(name).trim(),
                                class: String(studentClass).trim(),
                                totalFees: parseInt(totalFees),
                                amountPaid: parseInt(amountPaid),
                                year: parseInt(selectedYear)
                            };
                        }
                    }

                    // Add students to the selected year
                    Object.keys(newStudentsData).forEach(studentId => {
                        studentsData[selectedYear][studentId] = newStudentsData[studentId];
                    });

                    // Save data to storage after import
                    saveDataToStorage();

                    updateAdminDashboard();
                    alert(`Successfully imported ${Object.keys(newStudentsData).length} students from Excel file!\n\nData has been automatically saved to the system and will persist between sessions.`);
                } catch (error) {
                    console.error('Error parsing Excel file:', error);
                    alert('Error parsing Excel file. Please check the format and ensure it contains the required columns: StudentID, Name, Class, TotalFees, AmountPaid');
                }
            };
            reader.readAsArrayBuffer(file);
        }

        function importData() {
            document.getElementById('excelFile').click();
        }

        function exportData() {
            let totalStudents = 0;
            Object.keys(studentsData).forEach(year => {
                totalStudents += Object.keys(studentsData[year]).length;
            });
            
            if (totalStudents === 0) {
                alert('No data to export. Please load student data first.');
                return;
            }

            // Prepare data for Excel export
            const exportData = [];
            exportData.push(['StudentID', 'Name', 'Class', 'TotalFees', 'AmountPaid', 'Outstanding', 'Status']);
            
            Object.keys(studentsData).forEach(year => {
                Object.keys(studentsData[year]).forEach(id => {
                    const student = studentsData[year][id];
                    const outstanding = student.totalFees - student.amountPaid;
                    const status = outstanding === 0 ? 'Cleared' : 'Outstanding';
                    
                    exportData.push([
                        id,
                        student.name,
                        student.class,
                        student.totalFees,
                        student.amountPaid,
                        outstanding,
                        status
                    ]);
                });
            });

            // Create Excel workbook
            const wb = XLSX.utils.book_new();
            const ws = XLSX.utils.aoa_to_sheet(exportData);
            
            // Auto-size columns
            const colWidths = [];
            exportData[0].forEach((header, i) => {
                let maxWidth = header.length;
                exportData.forEach(row => {
                    if (row[i] && String(row[i]).length > maxWidth) {
                        maxWidth = String(row[i]).length;
                    }
                });
                colWidths.push({ wch: Math.min(maxWidth + 2, 50) });
            });
            ws['!cols'] = colWidths;
            
            XLSX.utils.book_append_sheet(wb, ws, 'Students Data');
            
            // Generate filename with current date
            const today = new Date().toISOString().split('T')[0];
            const filename = `TESO_Students_Fees_Data_${today}.xlsx`;
            
            XLSX.writeFile(wb, filename);
            
            alert(`Excel file exported successfully!\nFilename: ${filename}\nTotal students: ${totalStudents}`);
        }

        // Automation functions
        function startAutoSave() {
            // Auto-save every 30 seconds
            autoSaveInterval = setInterval(() => {
                saveDataToStorage();
                console.log('Auto-save completed at', new Date().toLocaleTimeString());
            }, 30000);
            
            console.log('Auto-save started - saving every 30 seconds');
        }

        function stopAutoSave() {
            if (autoSaveInterval) {
                clearInterval(autoSaveInterval);
                autoSaveInterval = null;
                console.log('Auto-save stopped');
            }
        }

        // Enhanced data validation
        function validateStudentData(student) {
            const errors = [];
            
            if (!student.name || student.name.trim().length < 2) {
                errors.push('Name must be at least 2 characters long');
            }
            
            if (!student.class || student.class.trim().length < 3) {
                errors.push('Class information is required');
            }
            
            if (!student.totalFees || student.totalFees < 0) {
                errors.push('Total fees must be a positive number');
            }
            
            if (student.amountPaid < 0) {
                errors.push('Amount paid cannot be negative');
            }
            
            if (student.amountPaid > student.totalFees) {
                errors.push('Amount paid cannot exceed total fees');
            }
            
            return errors;
        }

        // Automated email notifications with enhanced details
        function sendAutomatedNotifications() {
            // Check for students with outstanding fees and send reminders
            let outstandingCount = 0;
            let clearedCount = 0;
            
            Object.keys(studentsData).forEach(year => {
                Object.keys(studentsData[year]).forEach(id => {
                    const student = studentsData[year][id];
                    const outstanding = student.totalFees - student.amountPaid;
                    
                    if (outstanding === 0) {
                        clearedCount++;
                    } else {
                        outstandingCount++;
                    }
                });
            });
            
            // Send daily summary to admin
            sendEmailNotification('daily_summary', {
                totalStudents: outstandingCount + clearedCount,
                outstandingCount: outstandingCount,
                clearedCount: clearedCount,
                date: new Date().toLocaleDateString()
            });
        }

        // Tab switching functions
        function showTab(tabName) {
            // Hide all tab contents
            const tabContents = document.querySelectorAll('.tab-content');
            tabContents.forEach(content => content.classList.add('hidden'));
            
            // Remove active class from all tabs
            const tabs = ['feesTab', 'clearanceTab', 'documentsTab'];
            tabs.forEach(tab => {
                const tabElement = document.getElementById(tab);
                tabElement.className = 'py-2 px-1 border-b-2 border-transparent font-medium text-sm text-gray-500 hover:text-gray-700 hover:border-gray-300';
            });
            
            // Show selected tab content
            document.getElementById(tabName + 'Content').classList.remove('hidden');
            
            // Add active class to selected tab
            const activeTab = document.getElementById(tabName + 'Tab');
            activeTab.className = 'py-2 px-1 border-b-2 border-blue-500 font-medium text-sm text-blue-600';
            
            // Update content based on tab
            if (tabName === 'clearance') {
                updateClearanceTab();
            }
        }

        function showDashboard() {
            document.getElementById('loginSection').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            
            // Update student info
            document.getElementById('studentName').textContent = currentStudent.name;
            document.getElementById('studentClass').textContent = `Class: ${currentStudent.class} • Academic Year: ${currentStudent.year}`;
            
            // Show fees tab by default
            showTab('fees');
            
            updateFeesDisplay();
            updateDocumentButtons();
            updateClearanceTab();
        }

        function updateDocumentButtons() {
            const outstanding = currentStudent.totalFees - currentStudent.amountPaid;
            const documentsListDiv = document.getElementById('studentDocumentsList');
            
            if (outstanding > 0) {
                documentsListDiv.innerHTML = '';
                return;
            }
            
            // Check student class level
            const classLevel = currentStudent.class.toLowerCase();
            const isS4 = classLevel.includes('senior 4') || classLevel.includes('s4');
            const isS6 = classLevel.includes('senior 6') || classLevel.includes('s6');
            
            if (!isS4 && !isS6) {
                documentsListDiv.innerHTML = `
                    <div class="text-center py-8 text-gray-500">
                        <svg class="w-12 h-12 mx-auto mb-4 text-gray-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                        </svg>
                        <p class="text-lg font-medium">No documents available</p>
                        <p class="text-sm mt-1">Documents are only available for Senior 4 and Senior 6 students</p>
                    </div>
                `;
                return;
            }
            
            let documentsHTML = '';
            
            // Results document
            const resultsIssued = currentStudent.documents && currentStudent.documents.results && currentStudent.documents.results.issued;
            const resultsDate = resultsIssued ? new Date(currentStudent.documents.results.issuedDate).toLocaleDateString() : null;
            
            documentsHTML += `
                <div class="border border-gray-200 rounded-lg p-6">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center">
                            <svg class="w-8 h-8 text-blue-500 mr-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                            </svg>
                            <div>
                                <h4 class="font-medium text-gray-800">${isS4 ? 'S4' : 'S6'} Academic Results</h4>
                                <p class="text-sm text-gray-600">Transcripts & report cards</p>
                                ${resultsDate ? `<p class="text-xs text-green-600 mt-1">Issued: ${resultsDate}</p>` : ''}
                            </div>
                        </div>
                        <div class="flex items-center space-x-4">
                            <span class="px-4 py-2 rounded-lg font-medium text-sm ${resultsIssued ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}">
                                ${resultsIssued ? 'Issued ✓' : 'Not Issued'}
                            </span>
                        </div>
                    </div>
                </div>
            `;
            
            // Certificate document (only for S6)
            if (isS6) {
                const certificateIssued = currentStudent.documents && currentStudent.documents.certificate && currentStudent.documents.certificate.issued;
                const certificateDate = certificateIssued ? new Date(currentStudent.documents.certificate.issuedDate).toLocaleDateString() : null;
                
                documentsHTML += `
                    <div class="border border-gray-200 rounded-lg p-6">
                        <div class="flex items-center justify-between">
                            <div class="flex items-center">
                                <svg class="w-8 h-8 text-green-500 mr-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.746 0 3.332.477 4.5 1.253v13C19.832 18.477 18.246 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"></path>
                                </svg>
                                <div>
                                    <h4 class="font-medium text-gray-800">Completion Certificate</h4>
                                    <p class="text-sm text-gray-600">Official graduation certificate</p>
                                    ${certificateDate ? `<p class="text-xs text-green-600 mt-1">Issued: ${certificateDate}</p>` : ''}
                                </div>
                            </div>
                            <div class="flex items-center space-x-4">
                                <span class="px-4 py-2 rounded-lg font-medium text-sm ${certificateIssued ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}">
                                    ${certificateIssued ? 'Issued ✓' : 'Not Issued'}
                                </span>
                            </div>
                        </div>
                    </div>
                `;
            }
            
            documentsListDiv.innerHTML = documentsHTML;
        }

        function updateClearanceTab() {
            if (!currentStudent) return;
            
            const outstanding = currentStudent.totalFees - currentStudent.amountPaid;
            const isCleared = outstanding === 0;
            
            // Update clearance status
            const statusElement = document.getElementById('clearanceStatus');
            const outstandingElement = document.getElementById('clearanceOutstanding');
            
            if (isCleared) {
                statusElement.innerHTML = '<svg class="w-5 h-5 inline mr-2" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg>CLEARED';
                statusElement.className = 'text-lg font-bold text-green-600 flex items-center';
                outstandingElement.innerHTML = '<svg class="w-4 h-4 inline mr-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg>UGX 0';
                outstandingElement.className = 'text-lg font-bold text-green-600 flex items-center';
            } else {
                statusElement.textContent = 'PENDING';
                statusElement.className = 'text-lg font-bold text-red-600';
                outstandingElement.textContent = `UGX ${outstanding.toLocaleString()}`;
                outstandingElement.className = 'text-lg font-bold text-red-600';
            }
            
            // Update clearance certificate section
            updateClearanceCertificateSection(isCleared);
            
            // Update clearance history
            updateClearanceHistory();
        }

        function updateClearanceCertificateSection(isCleared) {
            const section = document.getElementById('clearanceCertificateSection');
            
            if (isCleared) {
                section.innerHTML = `
                    <div class="bg-green-50 border border-green-200 rounded-lg p-6 mb-6">
                        <div class="flex items-center">
                            <svg class="w-12 h-12 text-green-600 mr-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                            </svg>
                            <div>
                                <h4 class="text-lg font-semibold text-green-800">Fee Clearance Status</h4>
                                <p class="text-green-600">All fees have been paid in full - You are eligible for document collection</p>
                                <p class="text-sm text-green-500 mt-1">Visit the school office to collect your physical documents</p>
                            </div>
                        </div>
                    </div>
                `;
            } else {
                section.innerHTML = `
                    <div class="bg-red-50 border border-red-200 rounded-lg p-6 mb-6">
                        <div class="flex items-center">
                            <svg class="w-12 h-12 text-red-400 mr-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L4.082 16.5c-.77.833.192 2.5 1.732 2.5z"></path>
                            </svg>
                            <div>
                                <h4 class="text-lg font-semibold text-red-800">Documents Not Available</h4>
                                <p class="text-red-600">Please clear all outstanding fees before collecting documents</p>
                                <p class="text-sm text-red-500 mt-1">Outstanding: UGX ${(currentStudent.totalFees - currentStudent.amountPaid).toLocaleString()}</p>
                            </div>
                        </div>
                    </div>
                `;
            }
        }

        function updateClearanceHistory() {
            const historyDiv = document.getElementById('clearanceHistory');
            
            if (!currentStudent.clearanceHistory || currentStudent.clearanceHistory.length === 0) {
                historyDiv.innerHTML = '<p class="text-gray-500 text-center py-4">No clearance records found</p>';
                return;
            }
            
            let historyHTML = '<div class="space-y-3">';
            
            currentStudent.clearanceHistory.forEach(record => {
                const date = new Date(record.date).toLocaleDateString();
                const time = new Date(record.date).toLocaleTimeString();
                
                historyHTML += `
                    <div class="flex justify-between items-center py-3 px-4 bg-white rounded-lg border border-gray-200">
                        <div>
                            <p class="font-medium text-gray-900">${record.action}</p>
                            <p class="text-sm text-gray-600">${record.description}</p>
                        </div>
                        <div class="text-right">
                            <p class="text-sm text-gray-500">${date}</p>
                            <p class="text-xs text-gray-400">${time}</p>
                        </div>
                    </div>
                `;
            });
            
            historyHTML += '</div>';
            historyDiv.innerHTML = historyHTML;
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
                statusText.innerHTML = '<svg class="w-4 h-4 inline mr-2" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg>Fees Cleared - Documents Available';
                statusText.className = 'font-medium text-green-800 flex items-center';
                
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
                if (studentsData[currentStudent.year] && studentsData[currentStudent.year][currentStudent.id]) {
                    studentsData[currentStudent.year][currentStudent.id].amountPaid = currentStudent.amountPaid;
                    if (!studentsData[currentStudent.year][currentStudent.id].transactions) {
                        studentsData[currentStudent.year][currentStudent.id].transactions = [];
                    }
                    studentsData[currentStudent.year][currentStudent.id].transactions.push(transaction);
                }

                // Save data to storage after payment
                saveDataToStorage();
                
                // Send email notifications
                const newOutstanding = currentStudent.totalFees - currentStudent.amountPaid;
                
                // Payment received notification
                sendEmailNotification('payment_received', {
                    studentName: currentStudent.name,
                    studentId: currentStudent.id,
                    class: currentStudent.class,
                    year: currentStudent.year,
                    amount: amount,
                    method: methodName,
                    transactionId: transactionId,
                    date: new Date().toLocaleDateString(),
                    outstanding: newOutstanding
                });
                
                // Fees cleared notification if balance is now zero
                if (newOutstanding === 0) {
                    sendEmailNotification('fees_cleared', {
                        studentName: currentStudent.name,
                        studentId: currentStudent.id,
                        class: currentStudent.class,
                        year: currentStudent.year,
                        totalFees: currentStudent.totalFees,
                        totalPaid: currentStudent.amountPaid
                    });
                }
                
                // Clear form
                amountInput.value = '';
                methodSelect.value = '';
                transactionIdInput.value = '';
                
                // Update display
                updateFeesDisplay();
                
                alert(`Payment Recorded Successfully!\n\nTransaction ID: ${transactionId}\nAmount: UGX ${amount.toLocaleString()}\nMethod: ${methodName}\nDate: ${new Date().toLocaleDateString()}\n\nYour payment has been recorded and the admin has been notified via email.`);
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
            
            // Clear form and reset to login tab
            document.getElementById('studentId').value = '';
            showLoginTab();
        }

        // Email notification system
        function sendEmailNotification(type, data) {
            // Simulate email notification to integratedssteso@gmail.com
            const adminEmail = 'integratedssteso@gmail.com';
            let subject = '';
            let message = '';
            
            switch(type) {
                case 'payment_received':
                    subject = `TESO Fees Portal - Payment Received: ${data.studentName}`;
                    message = `
Payment Notification - TESO Integrated Secondary School

Student Details:
- Name: ${data.studentName}
- Student ID: ${data.studentId}
- Class: ${data.class}
- Academic Year: ${data.year}

Payment Information:
- Amount: UGX ${data.amount.toLocaleString()}
- Payment Method: ${data.method}
- Transaction ID: ${data.transactionId}
- Date: ${data.date}

Outstanding Balance: UGX ${data.outstanding.toLocaleString()}
Status: ${data.outstanding === 0 ? 'FEES CLEARED ✓' : 'Outstanding fees remaining'}

This is an automated notification from the TESO Fees Recovery Portal.
                    `;
                    break;
                    
                case 'fees_cleared':
                    subject = `TESO Fees Portal - Fees Cleared: ${data.studentName}`;
                    message = `
Fees Clearance Notification - TESO Integrated Secondary School

Congratulations! Student fees have been fully cleared.

Student Details:
- Name: ${data.studentName}
- Student ID: ${data.studentId}
- Class: ${data.class}
- Academic Year: ${data.year}

Payment Summary:
- Total Fees: UGX ${data.totalFees.toLocaleString()}
- Total Paid: UGX ${data.totalPaid.toLocaleString()}
- Outstanding Balance: UGX 0 ✓

The student now has access to their academic documents.

This is an automated notification from the TESO Fees Recovery Portal.
                    `;
                    break;
                    
                case 'recovery_request':
                    subject = `TESO Fees Portal - Website Access ${data.status}: ${data.studentName}`;
                    message = `
Website Access Recovery Notification - TESO Integrated Secondary School

Recovery Request Details:
- Student Name: ${data.studentName}
- Student ID: ${data.studentId}
- Status: ${data.status.toUpperCase()}
- Reason: ${data.reason}
- Timestamp: ${new Date().toLocaleString()}

Admin Action Required: ${data.status === 'verified' ? 'Please review and grant/deny access' : 'Action completed'}

This is an automated notification from the TESO Fees Recovery Portal.
                    `;
                    break;
                    
                case 'document_issued':
                    subject = `TESO Fees Portal - Document ${data.action}: ${data.studentName}`;
                    message = `
Document Management Notification - TESO Integrated Secondary School

Document ${data.action.charAt(0).toUpperCase() + data.action.slice(1)} Details:
- Student Name: ${data.studentName}
- Student ID: ${data.studentId}
- Class: ${data.class}
- Academic Year: ${data.year}
- Document Type: ${data.documentType}
- Action: ${data.action.charAt(0).toUpperCase() + data.action.slice(1)}d
- ${data.action === 'issue' ? 'Issued' : 'Revoked'} By: ${data.issuedBy}
- Date: ${data.date}

${data.action === 'issue' ? 'The document has been successfully issued and is now available to the student.' : 'The document has been revoked and is no longer available to the student.'}

This is an automated notification from the TESO Fees Recovery Portal.
                    `;
                    break;
                    

            }
            
            // In a real implementation, this would send an actual email
            // For demo purposes, we'll log it and show a notification
            console.log(`Email sent to ${adminEmail}:`);
            console.log(`Subject: ${subject}`);
            console.log(`Message: ${message}`);
            
            // Show a brief notification to indicate email was sent
            showNotification(`Admin notified via email: ${adminEmail}`);
        }
        
        function showNotification(message) {
            // Create a temporary notification
            const notification = document.createElement('div');
            notification.className = 'fixed top-4 right-4 bg-green-500 text-white px-4 py-2 rounded-lg shadow-lg z-50';
            notification.textContent = message;
            document.body.appendChild(notification);
            
            // Remove after 3 seconds
            setTimeout(() => {
                if (notification.parentNode) {
                    notification.parentNode.removeChild(notification);
                }
            }, 3000);
        }

        // Sample data for demonstration
        function loadSampleData() {
            const currentYear = new Date().getFullYear();
            
            // Sample students for current year
            studentsData[currentYear] = {
                'S001': {
                    name: 'Alice Nakato',
                    class: 'Senior 4 - Science',
                    totalFees: 1500000,
                    amountPaid: 1500000,
                    year: currentYear,
                    transactions: [
                        {
                            id: 'TXN001',
                            amount: 750000,
                            method: 'mobile_money',
                            date: new Date('2024-01-15').toISOString(),
                            timestamp: new Date('2024-01-15').getTime()
                        },
                        {
                            id: 'TXN002',
                            amount: 750000,
                            method: 'bank_transfer',
                            date: new Date('2024-03-10').toISOString(),
                            timestamp: new Date('2024-03-10').getTime()
                        }
                    ],
                    documents: {
                        results: {
                            issued: true,
                            issuedDate: new Date('2024-11-15').toISOString(),
                            issuedBy: 'Admin'
                        }
                    }
                },
                'S002': {
                    name: 'John Okello',
                    class: 'Senior 6 - Arts',
                    totalFees: 1800000,
                    amountPaid: 1200000,
                    year: currentYear,
                    transactions: [
                        {
                            id: 'TXN003',
                            amount: 600000,
                            method: 'cash',
                            date: new Date('2024-02-01').toISOString(),
                            timestamp: new Date('2024-02-01').getTime()
                        },
                        {
                            id: 'TXN004',
                            amount: 600000,
                            method: 'mobile_money',
                            date: new Date('2024-04-15').toISOString(),
                            timestamp: new Date('2024-04-15').getTime()
                        }
                    ]
                },
                'S003': {
                    name: 'Mary Akello',
                    class: 'Senior 5 - Science',
                    totalFees: 1600000,
                    amountPaid: 1600000,
                    year: currentYear,
                    transactions: [
                        {
                            id: 'TXN005',
                            amount: 1600000,
                            method: 'bank_transfer',
                            date: new Date('2024-01-20').toISOString(),
                            timestamp: new Date('2024-01-20').getTime()
                        }
                    ]
                },
                'S004': {
                    name: 'Peter Ochieng',
                    class: 'Senior 3 - Arts',
                    totalFees: 1400000,
                    amountPaid: 800000,
                    year: currentYear,
                    transactions: [
                        {
                            id: 'TXN006',
                            amount: 800000,
                            method: 'mobile_money',
                            date: new Date('2024-03-05').toISOString(),
                            timestamp: new Date('2024-03-05').getTime()
                        }
                    ]
                },
                'S005': {
                    name: 'Grace Auma',
                    class: 'Senior 6 - Science',
                    totalFees: 1800000,
                    amountPaid: 1800000,
                    year: currentYear,
                    transactions: [
                        {
                            id: 'TXN007',
                            amount: 900000,
                            method: 'cash',
                            date: new Date('2024-01-10').toISOString(),
                            timestamp: new Date('2024-01-10').getTime()
                        },
                        {
                            id: 'TXN008',
                            amount: 900000,
                            method: 'bank_transfer',
                            date: new Date('2024-02-20').toISOString(),
                            timestamp: new Date('2024-02-20').getTime()
                        }
                    ],
                    documents: {
                        results: {
                            issued: true,
                            issuedDate: new Date('2024-11-20').toISOString(),
                            issuedBy: 'Admin'
                        },
                        certificate: {
                            issued: true,
                            issuedDate: new Date('2024-12-01').toISOString(),
                            issuedBy: 'Admin'
                        }
                    }
                },
                'S006': {
                    name: 'David Musoke',
                    class: 'Senior 1 - General',
                    totalFees: 1200000,
                    amountPaid: 400000,
                    year: currentYear,
                    transactions: [
                        {
                            id: 'TXN009',
                            amount: 400000,
                            method: 'mobile_money',
                            date: new Date('2024-02-15').toISOString(),
                            timestamp: new Date('2024-02-15').getTime()
                        }
                    ]
                },
                'S007': {
                    name: 'Sarah Nambi',
                    class: 'Senior 2 - General',
                    totalFees: 1300000,
                    amountPaid: 1300000,
                    year: currentYear,
                    transactions: [
                        {
                            id: 'TXN010',
                            amount: 650000,
                            method: 'bank_transfer',
                            date: new Date('2024-01-25').toISOString(),
                            timestamp: new Date('2024-01-25').getTime()
                        },
                        {
                            id: 'TXN011',
                            amount: 650000,
                            method: 'cash',
                            date: new Date('2024-03-15').toISOString(),
                            timestamp: new Date('2024-03-15').getTime()
                        }
                    ]
                },
                'S008': {
                    name: 'Robert Kiprotich',
                    class: 'Senior 4 - Arts',
                    totalFees: 1500000,
                    amountPaid: 900000,
                    year: currentYear,
                    transactions: [
                        {
                            id: 'TXN012',
                            amount: 500000,
                            method: 'mobile_money',
                            date: new Date('2024-01-30').toISOString(),
                            timestamp: new Date('2024-01-30').getTime()
                        },
                        {
                            id: 'TXN013',
                            amount: 400000,
                            method: 'cash',
                            date: new Date('2024-04-10').toISOString(),
                            timestamp: new Date('2024-04-10').getTime()
                        }
                    ]
                }
            };
            
            // Add some students from previous year
            studentsData[currentYear - 1] = {
                'S101': {
                    name: 'Emmanuel Wanyama',
                    class: 'Senior 6 - Science',
                    totalFees: 1700000,
                    amountPaid: 1700000,
                    year: currentYear - 1,
                    transactions: [
                        {
                            id: 'TXN101',
                            amount: 1700000,
                            method: 'bank_transfer',
                            date: new Date('2023-12-15').toISOString(),
                            timestamp: new Date('2023-12-15').getTime()
                        }
                    ],
                    documents: {
                        results: {
                            issued: true,
                            issuedDate: new Date('2023-12-20').toISOString(),
                            issuedBy: 'Admin'
                        },
                        certificate: {
                            issued: true,
                            issuedDate: new Date('2024-01-05').toISOString(),
                            issuedBy: 'Admin'
                        }
                    }
                },
                'S102': {
                    name: 'Catherine Nalwoga',
                    class: 'Senior 4 - Arts',
                    totalFees: 1400000,
                    amountPaid: 1400000,
                    year: currentYear - 1,
                    transactions: [
                        {
                            id: 'TXN102',
                            amount: 700000,
                            method: 'mobile_money',
                            date: new Date('2023-11-10').toISOString(),
                            timestamp: new Date('2023-11-10').getTime()
                        },
                        {
                            id: 'TXN103',
                            amount: 700000,
                            method: 'cash',
                            date: new Date('2023-12-05').toISOString(),
                            timestamp: new Date('2023-12-05').getTime()
                        }
                    ],
                    documents: {
                        results: {
                            issued: true,
                            issuedDate: new Date('2023-12-18').toISOString(),
                            issuedBy: 'Admin'
                        }
                    }
                }
            };
            
            console.log('Sample data loaded successfully');
        }

        // Initialize the portal
        // Load saved data first, if no saved data exists, load sample data
        const hasStoredData = loadDataFromStorage();
        
        // If no stored data exists, load sample data for demonstration
        if (!hasStoredData || Object.keys(studentsData).every(year => Object.keys(studentsData[year]).length === 0)) {
            loadSampleData();
            saveDataToStorage(); // Save the sample data
        }
        
        updateYearDropdowns();
        
        // Show admin login by default
        document.getElementById('adminPortal').classList.add('hidden');
        document.getElementById('dashboard').classList.add('hidden');
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9744840697bcc837',t:'MTc1NjA1NTk3OS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
