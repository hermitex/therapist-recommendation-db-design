
# Therapist Recommendation System for S&G

## **Therapist Profile Database Schema**

#### **1. Therapist Table**

This table stores the basic personal details of the therapist.

```sql
CREATE TABLE Therapist (
    therapist_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    profile_picture VARCHAR(255),  -- Optional field for storing profile picture URL
    email VARCHAR(100) NOT NULL UNIQUE,
    phone_number VARCHAR(20)
);
```

#### **2. Credentials Table**

This table holds the credentials and professional qualifications of the therapist.

```sql
CREATE TABLE Credentials (
    credential_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    professional_title VARCHAR(50) NOT NULL,  -- E.g., RP, PhD
    license_number VARCHAR(50),
    years_experience INT,
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

#### **3. Therapist_Degrees Table**

Therapists can have multiple degrees, normalized into a separate table.

```sql
CREATE TABLE Therapist_Degrees (
    degree_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    degree VARCHAR(50) NOT NULL,  -- E.g., MSW, PhD
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

#### **4. Certifications Table**

To store the therapist’s certifications.

```sql
CREATE TABLE Certifications (
    certification_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    certification VARCHAR(100) NOT NULL,  -- E.g., CBT certification
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

#### **5. License_Status Table**

Stores the type and status of the therapist’s license, including clinical supervisors for interns.

```sql
CREATE TABLE License_Status (
    license_status_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    license_type VARCHAR(50) NOT NULL,  -- E.g., Intern, Registered
    status VARCHAR(20) NOT NULL,  -- E.g., Active, Inactive
    clinical_supervisor VARCHAR(100),  -- Optional field for interns
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

#### **6. Professional_Memberships Table**

To store the therapist’s professional memberships.

```sql
CREATE TABLE Professional_Memberships (
    membership_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    membership VARCHAR(100) NOT NULL,  -- E.g., APA, CPA
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

---

### **Demographics**

#### **7. Demographics Table**

This table stores demographic information.

```sql
CREATE TABLE Demographics (
    demographic_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    age_group VARCHAR(20),  -- E.g., 25-35
    gender_identity VARCHAR(20),  -- E.g., Male, Female, Non-binary
    ethnic_background VARCHAR(50),
    cultural_background VARCHAR(100),  -- E.g., LGBTQ+ affirming
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

#### **8. Languages_Spoken Table**

A therapist can speak multiple languages, so this is stored in a separate table.

```sql
CREATE TABLE Languages_Spoken (
    language_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    language VARCHAR(50) NOT NULL,  -- E.g., English, Spanish, French
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

---

### **Therapeutic Approach**

#### **9. Therapeutic_Approach Table**

Stores information about the therapist’s methods and techniques.

```sql
CREATE TABLE Therapeutic_Approach (
    approach_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    modality VARCHAR(100),  -- E.g., CBT, EMDR
    approach VARCHAR(100),  -- E.g., Client-Centered, Psychodynamic
    technique VARCHAR(100),  -- E.g., Assign Homework, Teach New Skills
    client_interaction_style VARCHAR(50),  -- E.g., Collaborative, Reflective
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

---

### **Specializations and Expertise**

#### **10. Specializations Table**

This table tracks the therapist’s areas of expertise.

```sql
CREATE TABLE Specializations (
    specialization_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    area_of_expertise VARCHAR(100),  -- E.g., Anxiety, Trauma, Depression
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

#### **11. Populations_Served Table**

To store the populations the therapist serves (e.g., Couples, Families).

```sql
CREATE TABLE Populations_Served (
    population_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    population VARCHAR(100),  -- E.g., Couples, Families, Adolescents
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

#### **12. Age_Group_Focus Table**

Tracks the age groups the therapist focuses on.

```sql
CREATE TABLE Age_Group_Focus (
    age_group_focus_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    age_group VARCHAR(50),  -- E.g., Children, Adolescents, Adults
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

#### **13. Special_Interest_Groups Table**

Stores special interest groups the therapist specializes in.

```sql
CREATE TABLE Special_Interest_Groups (
    interest_group_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    interest_group VARCHAR(100),  -- E.g., PTSD, Autism Spectrum
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

---

### **Therapy Logistics**

#### **14. Therapy_Logistics Table**

Stores logistical details related to therapy sessions.

```sql
CREATE TABLE Therapy_Logistics (
    logistics_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    session_rate DECIMAL(10, 2),  -- Cost per session
    session_duration INT,  -- E.g., 45 min, 60 min
    appointment_medium VARCHAR(50),  -- E.g., In-Person, Virtual
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

#### **15. Availability Table**

This table tracks the available days and times for appointments.

```sql
CREATE TABLE Availability (
    availability_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    day_of_week VARCHAR(20),  -- E.g., Monday, Tuesday
    time_range VARCHAR(50),  -- E.g., 9:00 AM - 12:00 PM
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

#### **16. Insurance_Accepted Table**

Stores insurance providers accepted by the therapist.

```sql
CREATE TABLE Insurance_Accepted (
    insurance_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    insurance_provider VARCHAR(100),  -- E.g., Blue Cross, Manulife
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

#### **17. Discounts_Offered Table**

Tracks discounts offered by the therapist.

```sql
CREATE TABLE Discounts_Offered (
    discount_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    discount_description VARCHAR(100),
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

---

### **Insurance and Coverage**

#### **18. Insurance_Coverage Table**

This table stores whether the therapist works with insurance and out-of-pocket costs.

```sql
CREATE TABLE Insurance_Coverage (
    coverage_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    works_with_insurance BOOLEAN,
    out_of_pocket_costs DECIMAL(10, 2),
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

---

### **Therapist Availability**

#### **19. Therapist_Availability Table**

This table tracks the therapist’s availability status.

```sql
CREATE TABLE Therapist_Availability (
    availability_status_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    immediate_availability VARCHAR(50),  -- E.g., Next Day, Next Week
    client_load VARCHAR(50),  -- E.g., Accepting New Clients
    waitlist BOOLEAN,
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

---

### **Professional Bio**

#### **20. Professional_Bio Table**

This table holds the bio and philosophy of the therapist.

```sql
CREATE TABLE Professional_Bio (
    bio_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    short_intro TEXT,  -- Short bio of the therapist
    detailed_description TEXT,  -- Detailed description of their services
    therapy_philosophy TEXT,  -- Therapist’s philosophy on therapy
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

---

### **Reviews and Testimonials**

#### **21. Reviews

 Table**
This table stores reviews and testimonials left by clients.

```sql
CREATE TABLE Reviews (
    review_id INT AUTO_INCREMENT PRIMARY KEY,
    therapist_id INT NOT NULL,
    client_id INT,  -- Reference to the client who left the review
    rating DECIMAL(3, 2) NOT NULL,  -- E.g., 4.75 out of 5
    review TEXT NOT NULL,
    review_date DATE,
    FOREIGN KEY (therapist_id) REFERENCES Therapist(therapist_id)
);
```

---

### **Client Preferences**

#### **22. Client_Preferences Table**

This table stores client preferences that help match them with therapists.

```sql
CREATE TABLE Client_Preferences (
    preference_id INT AUTO_INCREMENT PRIMARY KEY,
    client_id INT NOT NULL,
    therapist_gender_preference VARCHAR(20),  -- E.g., No preference, Female, Male
    therapeutic_approach_preference VARCHAR(100),  -- E.g., CBT, Talk therapy
    language_preference VARCHAR(50),
    insurance_preference VARCHAR(100),  -- E.g., Insurance accepted
    FOREIGN KEY (client_id) REFERENCES Client(client_id)
);
```

---

### **Database Relationships**

- The **Therapist** table serves as the core, with related tables for credentials, demographics, and therapeutic approaches.
- Foreign keys ensure referential integrity between **Therapist**, **Therapist_Degrees**, **Specializations**, **Populations_Served**, and other related tables.
- Normalization of degrees, specializations, and languages reduces redundancy and allows a therapist to have multiple degrees, certifications, and areas of expertise.
- **Client_Preferences** and **Reviews** are linked to therapists for better matching and feedback collection.

---

This schema provides a scalable, normalized structure, ensuring efficient storage and retrieval of therapist profile information.
