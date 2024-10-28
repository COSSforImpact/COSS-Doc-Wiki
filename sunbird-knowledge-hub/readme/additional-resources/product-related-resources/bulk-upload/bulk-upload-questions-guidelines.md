---
icon: elementor
---

# Bulk Upload Questions Guidelines

Bulk Upload Questions - Guidelines

**Overview**

This process is to help states to easily import their existing questions on to DIKSHA and use them to create content for their ETBs.

Following are done as part of the automatic process:

1. Questions are created in DIKSHA
2. All questions tagged to one QR Code are combined together to create a worksheet.
   1. Worksheet name will be “<\<Textbook section name to which it is attached>> + Worksheet”
   2. Board, Grade, Medium, Subject values for the worksheet are taken from the textbook
3. The worksheet is then attached to corresponding textbook section with the given QR code

Once the worksheets are linked to textbook sections, the textbooks have to be reviewed and published using DIKSHA portal.

Currently the only supported type of questions are MCQ. Please [see this document](https://drive.google.com/open?id=1tTJqdeg7IeCtPmdUOQxz6631q6jOEFcgGK1vHPWuVUI) for different types of MCQ types and templates supported on DIKSHA.

**Inputs Required for the process:**

1. Please provide G-drive path for each textbook which would have:

* Input file
* Icon image
* Questions/options image folders

Icon path has to be provided in the input sheet (Refer Sample file)

1. Questions are to be provided in the required csv input format. [Sample File](https://drive.google.com/open?id=1lA8g2XOu2BMP9ZqhPAyX\_5\_P2VjV4RzEP-S9sW\_oGyA)
2. Provide the following details for state instance:
   1. Content Creator mail id -
   2. Content Reviewer mail id -
   3. Created by -
   4. Organization (tenant) details and Framework name -
3. Textbooks to which the worksheets have to be linked should be created and in draft state. QR codes are linked to required textbook sections.

**General Instructions For Filling the Input Sheet:**

* Input file should strictly be in the format as required. Refer Sample file link above.
* QR codes in the input sheet should be valid and correct
* There should not be duplicacy of one QR code present in one textbook and in another textbook.
* Please ensure that textbook ids are valid and correct (the textbooks should be in Draft state).
* Image size should be less than 1 MB
* Images relative paths should be correctly mentioned in input file
* All images for questions and options, need to be in jpg.
* “appIconPath” column is to capture the icon for the worksheets (created for a particular textbook). Following should be taken care:
  * ProviderRelative path of a 512x512 image, its name should be “class\_subject.jpeg”
  * File format should be in jpeg format
  * If its blank, worksheet will not be created.
* Suggested approach is to have one icon for each subject-class combination.
* For difficulty level, Only 3 levels allowed, Mapping as follows:
  * 1: Easy
  * 2: Medium
  * 3: Hard

In input column, only provide respective number.

* Each question has to be one of the following values - 1, 2, 4, 5. Provide this value in input sheet, column name “QuestionTypeNo”. It identifies one of the MCQ types given in [this document](https://drive.google.com/open?id=1tTJqdeg7IeCtPmdUOQxz6631q6jOEFcgGK1vHPWuVUI). Question type 3 is not supported.
* All the fields are mandatory except following:
  * Medium
  * ClassNameEng
  * SubjectNameEng

However it is advisable to provide these values as well.

* Please do not provide semicolon (;) in the Question text or Options text. Remove it or replace with commas (,).
* Column headers’ names are case and space sensitive, ensure that exactly the same names are used in input sheet as mentioned in the format sheet.
* Access to files should be world readable
