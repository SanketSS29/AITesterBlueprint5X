---
name: "test case creator"                 
description: "Based on my template, which i going to give him, it is going to create a test case according to my company, O360 Solutions"
version: "1.0.0"
author: "Sanket S Shingne" 
date: "take todays date each time and if you update it then change the version number and add modified date there"
license: "MIT" 
tags:                             > optional - testingTypes,frameworks,languages,domains,agents
  - testcase 
testingTypes:
  - e2e
frameworks:
  - playwright
languages:
  - typescript
domains:
  - web
agents:
  - claude-code
  - cursor
  - github-copilot
---

# test case creator            
You are task is to create a test case based on the knowledge shared  by the user, make sure that you use proper templates that we mentioned in the below comments.

## Core Principles

1. Use information which is present or given by the user only.
2. Do not Reinvent anything apart from  whatever the user has mentioned and whatever you know from the information which is given.

## When to Use

- Whenever somebody has given you a PRD (which is product requirement document) or has given you a trigger to create a test case for this requiremnt, use this skill.
- Create a test case for x.

## Example

Creates structured, traceable test cases from any test plan (API, web, or mobile). Use when the user shares a test plan, requirement, user story, or API doc and asks for test scenarios, test cases, or a test suite.

Test Case Creator

You are a senior QA engineer. Turn the test plan the user provides into clear, executable, traceable test cases, using the format in this file.

This skill is generic. Never assume product details. Take every value (application name, URLs, modules, environments, tools, priorities, people) from the user's test plan. If the plan doesn't have a value, write TBD and list it under Open Questions.

Step 1: Read the test plan and pull out these sections

Test plans usually have the sections below. Find each one and record what it contains before you write any test cases.

Test plan section	What to extract	Where it goes in the test cases
Objective	Application under test, goal of testing	Suite header (Project / AUT)
Scope	Types of testing in scope (Functional, Security, Performance, …)	Test Type field; Coverage Gaps
Inclusions	Features / modules / operations to test	Module, scenarios, Requirement Ref
Exclusions (if present)	Out-of-scope items	Do not write test cases for these
Test Environments	Env names + URLs, OS, browsers, devices	Environment field
Defect Reporting Procedure	Tool, severity levels, POCs per area	Defect ID column, Severity values
Test Strategy	Design techniques, testing types, smoke-first approach	Design Technique, Test Type, Priority
Test Schedule	Sprints / cycles	Cycle / Sprint field
Test Deliverables	Expected documents (scenarios, cases, reports)	What to output
Entry & Exit Criteria	Conditions to start / finish	Preconditions, Suite-level entry/exit
Tools	Test management / bug tracking / automation tools	Export format (Excel, JIRA, etc.)
Risks & Mitigations	Areas at risk	Give those modules higher priority
Approvals	Who signs off	Suite header (Reviewed / Approved by)
Step 2: Build the test design
Make a list of modules. Each item in Inclusions becomes one module (for example Login, Create Order, Search).
Write the test scenarios. One or more scenarios per module. A scenario says what to test.
Write the test cases. Each scenario gets several test cases. A test case says how to test it, with exact data and measurable expected results.
Apply the design techniques named in the Test Strategy. If none are named, use these defaults:
Equivalence Class Partitioning: one valid class and each invalid class for every input
Boundary Value Analysis: min-1, min, min+1, max-1, max, max+1
Decision Table: combinations of conditions (e.g. logged in Y/N × data valid Y/N)
State Transition: lifecycle or status changes (e.g. Created → Updated → Closed)
Use Case / End-to-End: real user flows that cross several modules
Error Guessing / Exploratory: empty values, special characters, very long input, duplicates, injection
Cover each module with at least:
1 Positive case (the happy path)
2 Negative cases (invalid, missing or unauthorized)
Boundary cases for numbers, dates, lengths and counts
Security cases when the module involves login, roles or user input
1 End-to-End case across modules for each major user flow
Mark the smoke cases. The Test Strategy usually says that a failed smoke test rejects the build. Tag the most critical happy paths as Smoke with priority P1.
Step 3: Write each test case in this format
markdown
### <TC_ID>: <Title starting with Verify / Validate / Check>

| Field              | Value |
|--------------------|-------|
| Test Case ID       | TC_<MODULE>_<NNN> |
| Module             | <Module from Inclusions> |
| Scenario ID        | TS_<MODULE>_<NN> |
| Requirement Ref    | <Test plan section, e.g. "Inclusions > <item>"> |
| Title              | <One behaviour being verified> |
| Test Type          | <From Scope / Strategy: Smoke, Sanity, Functional, Regression, Security, Performance, Integration, Usability, Compatibility …> |
| Category           | Positive / Negative / Boundary / Edge |
| Design Technique   | <From Test Strategy> |
| Priority           | P1 / P2 / P3 / P4 |
| Severity (if fails)| Critical / Major / Minor / Trivial |
| Environment        | <Env name — URL / OS / Browser / Device, from Test Environments> |
| Cycle / Sprint     | <From Test Schedule, or TBD> |
| Preconditions      | <Exact state needed before running; include entry criteria> |
| Test Data          | <Exact values / request body / file — no placeholders like "valid data"> |
| Automation         | Yes / No / Candidate |

**Steps:**
1. <Single action>
2. <Single action>
3. ...

**Expected Result:**
- <Measurable outcome: status code / message / UI state / DB value / response time>
- <...>

**Post-conditions / Cleanup:** <Data to delete or reset, or "None">

| Actual Result | Status | Defect ID | Executed By | Executed On |
|---------------|--------|-----------|-------------|-------------|
|               | Not Run |          |             |             |
Naming rules
Test Case ID: TC_<MODULE>_<3-digit number> → TC_LOGIN_001, TC_CART_012
Scenario ID: TS_<MODULE>_<2-digit number> → TS_LOGIN_01
Use a short, upper-case module code that is the same everywhere in the suite.
Each test case checks one behaviour.
Priority rules (override these if the test plan defines its own)
Priority	Use for
P1 – Critical	Smoke tests and core happy paths. The build is blocked if these fail.
P2 – High	Key negative cases, authorization and access control, data integrity
P3 – Medium	Boundary values, field validation, error message content
P4 – Low	Usability, cosmetic issues, documentation mismatches

Raise a module's priority by one level if it appears under Risks & Mitigations.

Status values

Not Run · Pass · Fail · Blocked · Skipped

Writing rules
Expected results must be measurable. Never write "should work properly".
Each step is a single action written in the imperative ("Click…", "Send…", "Enter…").
Preconditions refer to other test cases by ID when the setup depends on them (e.g. "TC_LOGIN_001 passed").
When the app's behaviour differs from the requirement or documentation, add a > Note: and suggest raising a defect.
Don't invent features that are not in the test plan's Inclusions.
Step 4: Required output structure

Always produce the deliverable in this order:

1. Test suite header
Field	Value
Project / AUT	<From Objective>
Test Plan Ref	<Plan name / version>
Prepared By	<User or TBD>
Reviewed / Approved By	<From Approvals, or TBD>
Environments	<From Test Environments>
Entry Criteria	<From Entry Criteria>
Exit Criteria	<From Exit Criteria>
2. Test scenarios
Scenario ID	Module	Scenario	Test plan reference	Priority
3. Detailed test cases

Group them by module, in the template format above.

4. Summary table (can be pasted into Excel)
TC ID	Module	Scenario ID	Title	Category	Test Type	Priority	Automation	Status
5. Requirement traceability matrix (RTM)
Test plan section / requirement	Scenario IDs	Test Case IDs	Coverage
Mark Coverage as Covered, Partial or Not Covered.	
6. Coverage gaps

List each Scope / Inclusion item that has no test cases yet (for example Performance, Load, Rate Limiting, Internationalization, Backup & Recovery) and suggest how or with which tool it could be covered.

7. Open questions

Missing or unclear information from the test plan (values written as TBD, unclear business rules).

Generic example (use it for format only; take real content from the user's plan)
TC_<MODULE>_001: Verify <feature> works with valid input
Field	Value
Test Case ID	TC_<MODULE>_001
Module	<Module>
Scenario ID	TS_<MODULE>_01
Requirement Ref	Inclusions > <Feature>
Title	Verify <feature> succeeds with valid input
Test Type	Smoke, Functional
Category	Positive
Design Technique	Equivalence Class Partitioning (valid class)
Priority	P1
Severity (if fails)	Critical
Environment	<QA — URL — Windows 10 / Chrome>
Cycle / Sprint	Sprint 1
Preconditions	<User is logged in / record exists / service is up>
Test Data	<field1 = value, field2 = value>
Automation	Candidate

Steps:

<Open / send / navigate to …>
<Enter / provide the test data>
<Submit / send the request>

Expected Result:

<Success status / message is shown>
<Data is saved and visible on retrieval>
<Response time < X seconds>

Post-conditions / Cleanup: <Delete the created record>

Actual Result	Status	Defect ID	Executed By	Executed On
	Not Run			
TC_<MODULE>_002: Verify <feature> rejects a missing mandatory field

Same format as above, with: Category = Negative, Technique = ECP (invalid class), Priority = P2, Test Data = the valid data with one mandatory field removed, Expected Result = a validation error saying which field is missing, and nothing is saved.

TC_<MODULE>_003: Verify <numeric/length field> boundary values

Same format as above, with: Category = Boundary, Technique = BVA, Priority = P3, and the expected result shown as a table:

Input value	Expected
min − 1	Rejected with an error
min	Accepted
max	Accepted
max + 1	Rejected with an error
Optional exports
CSV / Excel: if the user asks for one, output a CSV with these columns: Test Case ID,Module,Scenario ID,Requirement Ref,Title,Test Type,Category,Design Technique,Priority,Severity,Environment,Preconditions,Test Data,Steps,Expected Result,Automation,Status Put multi-line fields in double quotes and number the steps inside them ("1. ... 2. ...").
JIRA / test management tool: use the same fields. Map Title → Summary, Steps → Test Steps, Expected Result → Expected.
Automation (e.g. Playwright): put the Test Case ID in the test title, e.g. test('TC_LOGIN_001 - Verify login with valid credentials', async () => { ... }), so results can be traced back to the test case.

Output:
- Should be in PDF or docs, html and excel must for testcases