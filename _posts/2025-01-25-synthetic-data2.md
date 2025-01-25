---
title: "Sythetic data #2"
date: 2025-01-25
---

I’ve recently had great success using Generative AI to create synthetic data, and I thought I’d share how I went about it. Hopefully, this can be helpful for others tackling similar challenges.

The basic idea is to start with a well-structured prompt. I’ve found that using a Mermaid ERD (Entity Relationship Diagram) to describe the data model works brilliantly—it provides a clear and visual way to communicate the structure you’re working with.

Next, I include a description of the business logic, outlining how the fields in the tables interact with one another. This is critical because it ensures the synthetic data aligns with real-world scenarios.

For situations where data evolves through a series of states—like in a case management system or IT service management (ITSM) tool—I’ve created a Type 2 Slowly Changing Dimension table. This table captures the changing statuses of a case over time. To generate this data, I use a transition matrix, which defines the probabilities of a case moving from one status to another.

To build the transition matrix, I rely on documentation from the project’s Business Analysts—those workflow diagrams mapping out the states are absolute gold for this kind of work.

Once the prompt and logic are in place, the AI generates Python code to produce the synthetic data. Python is perfect for this because it integrates so well with data platforms. From there, you can load the data into tables for reporting or analytics. It’s a quick way to build something functional and insightful.

That said, there are some challenges to watch out for. As you’d expect, Generative AI takes your prompts very literally. It’s not great at guessing your intentions, so you’ll need to be super specific about what you want it to generate. Fine-tuning the prompt is part of the process, so don’t expect perfection on the first go.

Despite this, synthetic data generation is a game changer. It helps you work faster, reduces dependencies on other teams in big projects, and allows you to deliver reporting and analytics outcomes to business stakeholders much earlier.

Below, I’ve included a simple framework for structuring your prompts. Hopefully, it’s useful as a starting point for your projects!

## Describe the problem

- You are a Data Architect skilled in data modelling and programming with Python.
  
- You are required to create python code to create synthetic data to populate a star schema. The schema is described by the following mermaid entity relationship diagram (ERD).

## Describe the data model (I am using a mermaid diagram)

``` shell
erDiagram

    FACT }o--|| CASE_DIM : case_sk
    CASE_STATUS_DIM }o--|| DATE_DIM : date_sk
    FACT }o--|| PERSON_DIM : person_sk 
    FACT }o--|| CASE_STATUS_DIM : case_sk
    FACT }o--|| TRANSACTION_TYPE_DIM : transaction_type_sk

    FACT{
        int fact_id PK, "row identifier for the FACT table. Is unique"
        int case_sk FK "links to case_sk in the table CASE_DIM"
        ...
    }

    ...

    CASE_DIM {
        int case_sk PK "the key to join to the FACT table on the field case_sk. Is unique"
        char case_reference_number "a field with a reference number for the transaction case. Is unqiue"
    }
```

## Describe the business logic

- Rules
  1. A case_sk will go through multiple values of case_status_sk defined by the transitional probability described in the status transitions section
  2. Each successive case_status_sk for a case_sk should have a start_date_sk that is equal to the previous end_date_sk
  3. A combination of case_sk and case_status_sk is unique and should only appear in a single row of CASE_STATUS_DIM
  4. A single case_sk should only be associated with one person_sk

...

## Provide and describe a transition matrix

- Status transitions:
The following matrix describes the probability of transition from one case_status to another, the values of rows are the current state and the columns is the next state.

The matrix is presented below:
[
[0,0.2,0.4], 
...
[0,0,1,0]
]

## Specify the data to generate
- Data to generate
1. Generate 100 different values for cask_sk and the required number of rows in other tables

[Contact me](https://www.gamma-data.co.uk#contact)
