# Hours Management System - Google Sheets

## Overview 🎯📊📋

This system is built using Google Sheets and integrates two types of forms:

1. **Teaching Hours Report Form**: 📘🕒📊

   - Used by teaching assistants to report hours for academic courses.
   - Tracks types of lessons (group or individual), dates, students, and total hours.

2. **General Management Form**: 📋📈🗂️

   - Used by the department secretary to consolidate and analyze data.
   - Summarizes hours by course, payment periods, and weekly utilization.

---

## Teaching Hours Report Form 📝📚🕒

![Teaching Hours Report Example](path/to/image.jpg)

### Structure 🧮📊📅

1. **Column A:** Course name, selected from a dropdown menu to ensure consistency across entries.
2. **Column B:** Lesson type, chosen from a dropdown menu to distinguish between group and individual lessons.
3. **Column C:** Date of the lesson, selected via a calendar for accuracy.
4. **Column D:** Total hours of the lesson, entered manually by the assistant.
5. **Column E:** Student names, recorded manually to track attendance.
6. **Column F:** Automatically calculated values:
   - The total number of hours.
   - Hours allocated for group lessons.
   - Hours allocated for individual lessons.
7. **Column G:** Breakdown of hours per course, calculated separately for group and individual sessions.

### Key Formulas 📐🧮🖊️

1. **Total hours:**
   ```excel
   =SUM(D:D)
   ```
2. **Total individual hours:**
   ```excel
   =SUM(FILTER(D:D, B:B="פרטני"))
   ```
3. **Total group hours:**
   ```excel
   =SUM(FILTER(D:D, B:B="קבוצה"))
   ```
4. **Total hours by course:**
   ```excel
   =SUM(FILTER(D:D, A:A="Course Name"))
   ```
5. **Group hours by course:**
   ```excel
   =SUM(FILTER(D:D, B:B="קבוצה", A:A="Course Name"))
   ```
6. **Individual hours by course:**
   ```excel
   =SUM(FILTER(D:D, B:B="פרטני", A:A="Course Name"))
   ```

---

## General Management Form 📊🗂️🗓️

### Functionality 📋🗂️📈

1. **Date and Monthly Summary:** 🎓📅📊

   - Displays hours worked by each teaching assistant, grouped by date and month.

2. **Course Summary:** 🎯📚🕒

   - Breaks down hours by course, showing group and individual lesson types.

3. **Payment Periods:** 💰📆📈

   - Segregates hours into payment periods and calculates salaries.

4. **Weekly Utilization Table:** 🗓️📋📏

   - Provides a weekly summary of hours used, categorized by course and assistant.

### Key Formulas 🧮🔢💾

1. **Hours by course and week:**

   ```excel
   =SUM(FILTER(IMPORTRANGE(INDIRECT("X" & 3+INT((ROW()-5)/18)*18+1), INDIRECT("T" & 3+INT((ROW()-5)/18)*18) & "!D:D"),
       IMPORTRANGE(INDIRECT("X" & 3+INT((ROW()-5)/18)*18+1), INDIRECT("T" & 3+INT((ROW()-5)/18)*18) & "!C:C") >= INDIRECT("C" & 6 + COLUMN()),
       IMPORTRANGE(INDIRECT("X" & 3+INT((ROW()-5)/18)*18+1), INDIRECT("T" & 3+INT((ROW()-5)/18)*18) & "!C:C") < INDIRECT("D" & 6 + COLUMN()),
       IMPORTRANGE(INDIRECT("X" & 3+INT((ROW()-5)/18)*18+1), INDIRECT("T" & 3+INT((ROW()-5)/18)*18) & "!A:A") = INDIRECT("T" & ROW()))
   )
   ```

2. **Total hours per payment period:**

   ```excel
   =SUM(FILTER(
       IMPORTRANGE(INDIRECT("X" & ROW()), INDIRECT("T" & ROW()-1) & "!D:D"),
       ISNUMBER(IMPORTRANGE(INDIRECT("X" & ROW()), INDIRECT("T" & ROW()-1) & "!D:D")),
       IMPORTRANGE(INDIRECT("X" & ROW()), INDIRECT("T" & ROW()-1) & "!C:C") >= INDIRECT("C" & 16 + COLUMN()),
       IMPORTRANGE(INDIRECT("X" & ROW()), INDIRECT("T" & ROW()-1) & "!C:C") <= INDIRECT("D" & 16 + COLUMN())
   ))
   ```

---

## Benefits of the System 🌟💡📈

1. **Dynamic and Flexible:** 🌟📊📋

   - The formulas adapt dynamically based on where the form or assistant is located, ensuring seamless functionality across different contexts.

2. **Automated Summaries:** 🤖📈🗂️

   - The system calculates hours and summaries automatically, significantly minimizing the need for manual input and reducing errors.

3. **Comprehensive Tracking:** 📅📚🕒

   - Provides detailed tracking of hours across various parameters, including course, lesson type, week, and payment period. course, type, week, and payment period.

4. **Efficiency in Payroll:** 💰📊💼

   - Simplifies salary calculations based on real-time data.

---

Feel free to reach out for further details or assistance! ✉️📞💻

