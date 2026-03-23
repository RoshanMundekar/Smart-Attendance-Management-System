# 🏫 Smart Class Attendance Management System

A comprehensive, automated web application built to streamline class attendance management using **Facial Recognition**. Say goodbye to manual roll-calls! This system provides a robust platform for Administrators, Teachers, and Students to manage academic presence efficiently and accurately.

## 🚀 Features

* **Role-Based Access Control:** Distinct portals and dashboards for Admins, Teachers, and Students.
* **Automated Face Recognition Attendance:**
    * Quickly register student face encodings using webcam captures.
    * Mark attendance seamlessly using group photos or live video streams (powered by `dlib` and `face_recognition`).
* **Interactive Exam Module:**
    * Teachers can create descriptive tests.
    * Uses **Artificial Intelligence (NLP)** to automatically grade student responses by comparing semantic similarity and removing stopwords (powered by `NLTK` and `fuzzywuzzy`).
* **Real-time Notifications:** Share academic notices directly to the student/teacher dashboards.
* **Comprehensive Reporting:** Admins and teachers can generate, view, and export detailed attendance records.
* **Profile Management:** Handles extensive user details, department sorting, and securely stores biometric data.

## 🛠️ Technology Stack

* **Backend Framework:** Python / Flask
* **Database:** MySQL (using `pymysql`)
* **Computer Vision & ML:** OpenCV (`cv2`), `dlib`, `face_recognition` API
* **Natural Language Processing:** `NLTK`, `fuzzywuzzy` (for exam grading)
* **Frontend:** HTML, CSS, JavaScript (integrated with TailwindCSS)

## 📁 System Architecture

* **`app.py` / `api.py`:** Core Flask application handling web routes, DB connectivity, auth, and application logic.
* **`mark_attendance.py`:** Contains the primary facial recognition logic. Compares live/uploaded images with recorded student encodings.
* **`register.py` / `register1.py`:** Dedicated scripts for initially capturing and embedding face data using the webcam.
* **`finaldb.sql`:** The complete SQL schema needed to initialize all tables (`userdetails`, `teacheregister`, `marking_attendance`, etc.)

## ⚙️ Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone <repository_url>
   cd webattendance
   ```

2. **Database Configuration:**
   * Import the provided `finaldb.sql` file into your MySQL server to set up the necessary database schemas (Database name: `042-attendence`).
   * Ensure your MySQL server is running and update the connection configurations inside `app.py` (line ~139):
     ```python
     connection = pymysql.connect(host="localhost", user="root", password="root", database="042-attendence")
     ```

3. **Install Dependencies:**
   Ensure you have Python 3.x installed. Then, install the required libraries:
   ```bash
   pip install Flask pymysql face_recognition opencv-python dlib numpy pandas nltk fuzzywuzzy werkzeug
   ```
   *Note: `dlib` may require CMake and a C++ compiler installed on your system.*

4. **NLTK Data Requirement:**
   Run the following Python block to download NLTK data for the semantic exam grader:
   ```python
   import nltk
   nltk.download('stopwords')
   nltk.download('punkt')
   nltk.download('wordnet')
   nltk.download('averaged_perceptron_tagger')
   ```

5. **Run the Application:**
   ```bash
   python app.py
   ```
   Open your browser and navigate to `http://localhost:5000`.

## 📌 Usage Flow
- **Admin**: Log in using predefined admin credentials. Register Teachers/Students and upload global notices.
- **Onboarding**: Capture a student's face data through the onboarding portal. It saves 10 specific images under `static/data/` and extracts encodings to `storage/known_face_encodings.pickle`.
- **Teacher**: Configure subjects, take exams, and upload class pictures to the portal where `mark_attendance.py` will autonomously document who is Present or Absent based on the generated facial encodings.

## ⚠️ Notes
- Make sure not to delete `shape_predictor_68_face_landmarks.dat` as `dlib` requires it to analyze faces successfully.
- Webcams are required during the enrollment process.
