# Dilsha Achini - Portfolio Website

This portfolio showcases the work and experience of Dilsha Achini, a Laboratory Technician with a strong educational background and a passion for skills development.

## Project Overview

This project consists of a personal portfolio website built using HTML and CSS. The website is designed with a smooth-scrolling navigation experience and provides detailed sections about the individual, including:

- **About Me**: Introduction and background information.
- **Education**: Academic history and achievements.
- **Professional Experience**: Work experience in the medical field.
- **Skills & Hobbies**: Soft and hard skills with visual progress bars.
- **Curriculum Vitae**: Downloadable resume.
- **Contact**: Contact form for visitors to send messages.

## Website Structure

### 1. **Header**
The header includes a navigation menu with smooth scrolling links to various sections:

- About
- Education
- Skills & Hobbies
- Curriculum Vitae

### 2. **Main Content**

#### **About Me**
The "About" section introduces Dilsha Achini, her background in laboratory work, and her communication skills. A profile image is included.

#### **Education**
This section highlights Dilsha’s educational achievements, including her secondary education and university degree in Biotechnology. A diploma in English Language is also mentioned.

#### **Professional Experience**
A brief section showcasing the professional experience, with a focus on the Assistant Pharmacist role.

#### **Skills & Hobbies**
The skills section is divided into:
- Soft Skills: Effective Communication, Teamwork, Organization, Time Management.
- Hard Skills: Microsoft Office Suite, Laboratory Techniques.

Each skill has a corresponding progress bar indicating proficiency.

#### **Curriculum Vitae**
A link to download the CV in PDF format.

#### **Contact Me**
A contact form allows visitors to send a message. Contact information like email, phone number, LinkedIn, and GitHub profiles are displayed.

### 3. **Footer**
The footer contains the copyright notice: "© [Your Name] | All Rights Reserved".

### 4. **Smooth Scrolling**
The navigation menu links smoothly scroll to the sections of the page using the `scrollIntoView` JavaScript function.

## Features

### **Responsive Design**
The website layout is responsive, adjusting to different screen sizes for mobile, tablet, and desktop views.

### **Smooth Scrolling**
The navigation menu items are configured for smooth scrolling, ensuring a pleasant user experience when navigating between sections.

### **Skills Visualization**
The skills section uses HTML progress bars to display proficiency in both soft and hard skills.

### **Contact Form**
A form in the "Contact Me" section allows users to get in touch with Dilsha Achini. The form captures the name, email, and message from the user and submits it to a PHP script for email handling.

---

## Contact Form Email Sender Setup (PHP)

The contact form is handled using PHP. Below are the steps for configuring the email sender for the form submissions.

### **Steps to Implement PHP Email Sending**

1. **Create `contact-form-handler.php` File**
   This file will process the form data and send an email.

   ```php
   <?php
   if ($_SERVER["REQUEST_METHOD"] == "POST") {
       // Sanitize form inputs
       $name = filter_var(trim($_POST["name"]), FILTER_SANITIZE_STRING);
       $email = filter_var(trim($_POST["email"]), FILTER_SANITIZE_EMAIL);
       $message = filter_var(trim($_POST["message"]), FILTER_SANITIZE_STRING);

       // Validate email
       if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
           echo "Invalid email format";
           exit;
       }

       // Define recipient and subject
       $to = "your-email@example.com";  // Replace with your email address
       $subject = "New Message from $name via Contact Form";

       // Prepare email content
       $email_content = "<html><body>";
       $email_content .= "<h2>New Message from Contact Form</h2>";
       $email_content .= "<p><strong>Name:</strong> $name</p>";
       $email_content .= "<p><strong>Email:</strong> $email</p>";
       $email_content .= "<p><strong>Message:</strong><br>$message</p>";
       $email_content .= "</body></html>";

       // Set email headers for HTML content
       $headers = "MIME-Version: 1.0" . "\r\n";
       $headers .= "Content-Type: text/html; charset=UTF-8" . "\r\n";
       $headers .= "From: $email" . "\r\n";  // Set from email as the one submitted in the form
       $headers .= "Reply-To: $email" . "\r\n";

       // Send the email
       if (mail($to, $subject, $email_content, $headers)) {
           echo "Thank you for your message, $name. We will get back to you shortly!";
       } else {
           echo "Sorry, something went wrong. Please try again later.";
       }
   } else {
       echo "Invalid request.";
   }
   ?>
