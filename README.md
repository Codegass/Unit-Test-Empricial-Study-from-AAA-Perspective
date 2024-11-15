# Unit Test Empirical Study from AAA Perspective

## Project Overview
This repository contains the research data for our empirical study on unit testing practices, analyzed from the Arrange-Act-Assert (AAA) perspective. We examined 735 real-world unit test cases from seven open-source Java projects, investigating adherence to the AAA pattern, common deviations, and design issues within the A blocks.

Our study utilized a custom parser for AAA analysis and the JNose tool for detecting test smells. We then conducted a comparative analysis between the AAA problems identified through our approach and the test smells detected by JNose. This comparison aimed to highlight the unique strengths of AAA analysis in identifying root causes of issues in test design and guiding necessary improvements.

The repository includes parsed AAA data, JNose results, and our comprehensive analysis comparing AAA problems with classic test smells. We also present developer feedback on our proposed improvements, providing insight into the practical value of addressing AAA issues in real-world projects.

## Key Findings
1. 77% of test cases follow the AAA structure, confirming its widespread adoption.
2. We identified three recurring AAA-Deviation patterns and four design issues within the A blocks.
3. Comparison with classic test smells revealed the strengths of AAA analysis in identifying root causes and guiding necessary improvements.
4. Developer feedback on our improvement proposals showed a 100% response rate with 78% positive responses.

## Repository Structure
- `AAA parsed files/`: Contains all tag-sheets generated by our parser. Each CSV file follows this format:
  - `testClassName`: The name of the test class
  - `testMethodName`: The name of the test method
  - `potentialTargetQualifiedName`: The fully qualified name of the target method/constructor being tested
  - `AAA`: The AAA phase tag (0=Arrange, 1=Act, 2=Assert)

  Example:
  ```csv
  testClassName,testMethodName,potentialTargetQualifiedName,AAA
  AccumuloInputFormatTest,testSetIterator,"NEW org.apache.accumulo.core.client.IteratorSetting(int, String, String)",0
  AccumuloInputFormatTest,testSetIterator,"org.apache.accumulo.core.client.mapred.InputFormatBase.addIterator(JobConf, IteratorSetting)",1
  AccumuloInputFormatTest,testSetIterator,"ASSERT org.junit.Assert.assertEquals(Object, Object)",2
  ```
- `Jnose results/`: Contains all data generated by JNose and the test smell matching results paired with AAA issue logic. In the matched folder, each csv file represents the mapping results of a project, and each row of the csv file represents a test case, with columns indicating the presence of AAA issues and detected test smells, enabling direct comparison. Each file corresponds to a project and follows this format:
  ```
  file_name,Multiple AAA,Missing Assert,Assert Pre,Suppressed Exception,Obscure Assert,Multiple Act,Arrange&Quit,NOTE,testSmellName
  ```
  Where:
  - `file_name` is the name of the test file
  - The following columns indicate the presence (1) or absence (0) of each AAA issue
  - `NOTE` provides any additional observations
  - `testSmellName` lists the test smells detected by JNose for that file
- `project-version.md`: Lists version information for all projects investigated.
- `Overall Data with Tagging Results.xlsx`: Contains all data analysis and final results of the paper.

## Investigated Projects
We studied the following open-source projects at specific versions:
- Gson: 2.10.1
- mssql-jdbc: 12.6.1
- Archaius: 2.7.5
- CloudStack: 4.13.1.0
- Accumulo: 2.0.0
- Druid: 0.19.0
- Dubbo: 2.7.7

Detailed version information and GitHub links can be found in the `project-version.md` file.

## Research Methodology

Our study approach involved four key steps:

1. Inspection and AAA Tagging:
   - Manually tagged statements in each test case as Arrange, Act, or Assert.
   - Used a custom Java parser based on Eclipse JDT to generate tag-sheets.
   - Two independent taggers performed the analysis, with cross-validation and group discussions for disagreements.

2. AAA Structure Examination:
   - Used regex matching to identify test cases following the AAA pattern.
   - Manually inspected cases not matching the pattern to identify special AAA cases and true AAA-Deviation cases.
   - Summarized recurring AAA-Deviation patterns and design issues within A blocks.
   - Quantitatively compared complexity of AAA and AAA-Deviation cases.

3. Comparison with Test Smells:
   - Used JNose tool to detect classic test smells.
   - Identified Logical Relevant Pairs between AAA problems and test smells.
   - Conducted conceptual and experimental comparisons for each pair.

4. Restructuring and Developer Feedback:
   - Selected representative cases with AAA problems for restructuring.
   - Prepared and submitted Issue Tickets (ITs) and Pull Requests (PRs) to project repositories.
   - Collected and analyzed developer feedback on the proposed improvements.

This methodology allowed us to comprehensively analyze the AAA structure in real-world test cases, compare it with classic test smell detection, and validate the practical value of our findings through developer feedback.

## Results
Detailed results and analysis of the study can be found in the `Overall Data with Tagging Results.xlsx` file. This file contains our data analysis process and the final research outcomes.

## Contribution
If you're interested in this research or have any questions, please feel free to contact us or raise an issue.
