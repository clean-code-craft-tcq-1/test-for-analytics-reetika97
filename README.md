# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Data in CSV is of required format, i.e, ensure the writing operation to CSV file is done correctly 
3. Read correct CSV file/ is in readable condition
4. PDF created can access correct storage location
5. Notification is sent to required and correct stakeholders/responsibles

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | This is a third party software, we can only ensure data we are sending is correct
Counting the breaches       | Yes           | This is part of the software being developed
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | No            | Only Notification generated for new report available is tested, utility is not tested

### List the Test Cases 

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write number of breaches to the PDF from a csv conatining readings when threshold is crossed
4. Write date&time to the PDF from a csv conatining readings when continuous upward trend is seen
5. Write "Notification sent to [recipient name]" to the console when new PDF report available
6. Write "Error Opening File" to the PDF when CSV file not accessible in server 
7. Write "File Error" on to the console when PDF file/storage not accessible
8. Write "PDF report missed" on to console when PDF generation is missed for the week.

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | pdf generation function call |notification sent/ internal data structure              | mock
Report inaccessible server | csv file |accessible/inaccessible             | None - pure function
Find minimum and maximum   | csv data | min/max              |None - pure function
Detect trend               |csv data | date&time of upward trend               | None - pure function
Write to PDF               |report of trend, min, max, no. of breaches |internal data-structure               | Fake the PDF file
