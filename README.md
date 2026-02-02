# School-manegment-system
School Fee &amp; Attendance Smart System is a school app that stores student profiles with photos, tracks daily attendance, manages fees, auto-calculates fines, and sends SMS alerts to parents for absences or due payments. It also gives simple reports and dashboards to reduce manual work and errors.

# School Fee & Attendance Management System

A complete web-based solution for managing school fees, attendance, and student records with automated SMS reminders.

## 🚀 Features

### Core Features
- ✅ Student Management with photo upload
- ✅ Fee tracking with auto late-fine calculation
- ✅ Payment recording with receipt generation
- ✅ Defaulter list with pending dues
- ✅ SMS alerts to parents (Twilio/Fast2SMS)
- ✅ Attendance marking system
- ✅ Excel report generation
- ✅ Real-time dashboard with statistics

### Advanced Features
- 📊 Monthly collection reports
- 📱 Automated fee reminders (scheduled)
- 📈 Attendance analytics
- 🧾 Payment history tracking
- 🔍 Search and filter students
- 📧 Bulk SMS functionality

---

## 📋 Prerequisites

Before you begin, ensure you have:
- Node.js (v16 or higher) - [Download](https://nodejs.org/)
- MongoDB (v5 or higher) - [Download](https://www.mongodb.com/try/download/community)
- Git (for version control)

---

## 🛠️ Installation Guide

### Step 1: Clone or Download the Project

```bash
# If you have this as a Git repository
git clone 
cd school-fee-system

# OR if you downloaded as ZIP, extract and navigate to the folder
cd school-fee-system
```

### Step 2: Backend Setup

```bash
# Navigate to backend folder
cd backend

# Install dependencies
npm install

# Create .env file
cp .env.example .env

# Edit .env file with your settings (see Configuration section below)
```

### Step 3: Frontend Setup

```bash
# Open a new terminal
cd frontend

# Install dependencies
npm install
```

### Step 4: Create Required Folders

```bash
# In the backend directory
mkdir -p uploads/students
```

---

## ⚙️ Configuration

### Backend Configuration (.env file)

Edit `backend/.env` file:

```env
# Server
PORT=5000
NODE_ENV=development

# Database - Update if MongoDB is on different host/port
MONGODB_URI=mongodb://localhost:27017/school-fee-system

# School Info
SCHOOL_NAME=ABC International School

# SMS Configuration (Choose ONE)

# Option 1: Twilio (International)
TWILIO_ACCOUNT_SID=your_account_sid_from_twilio
TWILIO_AUTH_TOKEN=your_auth_token_from_twilio
TWILIO_PHONE_NUMBER=+1234567890

# Option 2: Fast2SMS (India) - Uncomment if using
# FAST2SMS_API_KEY=your_fast2sms_api_key

# Late Fine
LATE_FINE_PER_DAY=10
```

### Get Twilio Credentials (Free Trial)

1. Sign up at [Twilio](https://www.twilio.com/try-twilio)
2. Get your Account SID and Auth Token from dashboard
3. Get a free phone number
4. Add these to your .env file

### Get Fast2SMS API Key (India)

1. Sign up at [Fast2SMS](https://www.fast2sms.com/)
2. Go to Dashboard → API
3. Copy your API key
4. Add to .env file

---

## 🚀 Running the Application

### Method 1: Development Mode (Recommended for testing)

**Terminal 1 - Backend:**
```bash
cd backend
npm run dev
```

**Terminal 2 - Frontend:**
```bash
cd frontend
npm start
```

The application will open at `http://localhost:3000`

### Method 2: Production Mode

**Backend:**
```bash
cd backend
npm start
```

**Frontend:**
```bash
cd frontend
npm run build
# Serve the build folder using a static server
npx serve -s build
```

---

## 📱 SMS Setup Guide

### For Twilio (Recommended for global use)

1. **Sign up**: Visit https://www.twilio.com/try-twilio
2. **Verify phone**: Complete phone verification
3. **Get credentials**: 
   - Account SID: Found on dashboard
   - Auth Token: Click to reveal on dashboard
   - Phone Number: Get free trial number
4. **Add to .env**: Copy credentials to backend/.env
5. **Test**: Send a test SMS through the app

### For Fast2SMS (Popular in India)

1. **Sign up**: Visit https://www.fast2sms.com/
2. **Verify**: Complete email and phone verification
3. **Credits**: You get free credits initially
4. **API Key**: Dashboard → API → Copy API Key
5. **Modify code**: Uncomment Fast2SMS code in `utils/smsService.js`
6. **Add to .env**: Add API key to backend/.env

---

## 🗄️ Database Setup

MongoDB should be running. To verify:

```bash
# Check if MongoDB is running
mongosh

# If not installed, install MongoDB Community Edition
# Windows: Download from mongodb.com
# Mac: brew install mongodb-community
# Linux: sudo apt-get install mongodb
```

The application will automatically create the database and collections on first run.

---

## 📊 Usage Guide

### 1. Add Students

1. Go to **Students** → **Add New Student**
2. Fill in student details
3. Upload photo (optional)
4. Set monthly fee structure
5. Click **Save**

### 2. Record Payment

1. Go to **Payment**
2. Select student
3. Enter amount and payment mode
4. System auto-calculates late fine if overdue
5. Receipt number generated automatically

### 3. Mark Attendance

1. Go to **Attendance**
2. Select class and date
3. Mark Present/Absent/Late for each student
4. Save attendance

### 4. View Defaulters

1. Go to **Defaulters**
2. See list of students with pending fees
3. Send SMS reminders
4. Track overdue months

### 5. Generate Reports

1. Go to **Reports**
2. Select date range
3. Choose report type (Payment/Attendance)
4. Download Excel file

---

## 🤖 Automated SMS Reminders

The system automatically sends SMS reminders based on schedule:

- **Day 7**: 3 days before due date
- **Day 10**: On due date
- **Day 15, 20, 25**: For overdue fees

Edit the schedule in `backend/server.js`:

```javascript
// Current: Every day at 9 AM
cron.schedule('0 9 * * *', () => {
  sendDueReminders();
});

// Change to: Every Monday at 10 AM
cron.schedule('0 10 * * 1', () => {
  sendDueReminders();
});
```

---

## 🔧 Troubleshooting

### MongoDB Connection Error
```bash
# Start MongoDB service
# Windows: Start MongoDB service from Services
# Mac: brew services start mongodb-community
# Linux: sudo systemctl start mongod
```

### Port Already in Use
```bash
# Change port in backend/.env
PORT=5001

# And update proxy in frontend/package.json
"proxy": "http://localhost:5001"
```

### SMS Not Sending
1. Check if Twilio/Fast2SMS credentials are correct
2. Verify phone number format (with country code)
3. Check if you have credits/balance
4. Look at console logs for error messages

### Photo Upload Not Working
```bash
# Ensure uploads folder exists
cd backend
mkdir -p uploads/students

# Check folder permissions
chmod 755 uploads
```

---

## 📦 Deployment

### Deploy to Heroku (Free)

1. **Create Heroku account**: https://heroku.com
2. **Install Heroku CLI**: https://devcenter.heroku.com/articles/heroku-cli

```bash
# Login to Heroku
heroku login

# Create app
heroku create your-school-fee-system

# Add MongoDB addon
heroku addons:create mongolab:sandbox

# Set environment variables
heroku config:set TWILIO_ACCOUNT_SID=xxx
heroku config:set TWILIO_AUTH_TOKEN=xxx
heroku config:set TWILIO_PHONE_NUMBER=+1234567890

# Deploy backend
cd backend
git init
git add .
git commit -m "Initial commit"
git push heroku main

# Deploy frontend (build and serve)
cd ../frontend
npm run build
# Use static hosting (Netlify/Vercel)
```

### Deploy to Railway (Recommended)

1. Visit https://railway.app
2. Connect GitHub repository
3. Add MongoDB plugin
4. Set environment variables
5. Deploy automatically

---

## 🎨 Customization

### Change Late Fine Rate

Edit `backend/.env`:
```env
LATE_FINE_PER_DAY=20  # Changed from 10 to 20
```

### Modify Fee Due Date

Edit `backend/routes/payments.js`:
```javascript
// Change from 10th to 5th of month
const dueDate = new Date(year, parseInt(month) - 1, 5);
```

### Change SMS Message Template

Edit `backend/utils/smsService.js` - modify message content

### Add New Student Fields

1. Update `backend/models/Student.js` - add field to schema
2. Update `frontend/src/pages/StudentForm.js` - add input field

---

## 📞 Support

For issues or questions:
1. Check the troubleshooting section
2. Review console logs for errors
3. Verify all environment variables are set
4. Ensure MongoDB is running

---

## 🔒 Security Notes

- Never commit .env file to Git
- Keep API keys secret
- Use strong JWT secrets in production
- Enable HTTPS in production
- Validate all user inputs

---

## 📈 Future Enhancements

- [ ] Face recognition attendance
- [ ] Parent mobile app
- [ ] Email notifications
- [ ] Multi-school support
- [ ] Advanced analytics
- [ ] Online fee payment gateway

---

## 📄 License

MIT License - Feel free to use for your school!

---

## 👨‍💻 Developer

Built with ❤️ for schools
