# Introduction to Oracle Data Science Agent

## Introduction

Data Science Agent is an intelligent built-in conversational chatbot integrated with Oracle Machine Learning UI included in your Oracle Autonomous AI Database subscription. You must provide the LLM, specified through your AI profile, whether from a third-party AI provider, OCI GenAI Service, or one you privately host. You can run complete data science workflows using natural language in the Data Science Agent chat.

As a human-in-the-loop chatbot, Data Science Agent requires your intervention and approval in the following areas:

* **Object association:** Objects must be associated or approved before the agent creates views that use them; other supported operations may still use accessible objects based on the user's database privileges. Associating database objects with a conversation improves precision and efficiency.
* **Conversation management:** The scope of Data Science Agent is limited to the active conversation context only. You must create, manage, and delete your conversations.
* **Profile selection:** You must select an AI profile and, therefore, the LLM that powers the agent. You can choose an existing profile or create and select your own. You can also switch profiles mid-conversation.
* **Approval for object viewing:** During a conversation, Data Science Agent compares the requested objects with those already associated with the active conversation. If a required table or view is not in the approved set, the agent pauses and asks for your approval to add it. If you approve, the object is associated with the conversation and the agent continues. If you do not approve, the request is canceled and no view is created.


Estimated Time: X


### Objectives
In this lab, you will learn how to:

* Access and use the Oracle Machine Learning Data Science Agent
* Create an AI Credential and an AI Profile
* Create a Data Science Conversation
* Use the Data Science Agent chat interface
* Issue a sequence of prompts to perform machine learning tasks


### Prerequisites

This workshop requires access to your Oracle Machine Learning UI in Oracle Autonomous AI Database. You may use your own cloud account or a training account whose details were given to you by an Oracle instructor.

* Familiarity with OML UI
* Familiarity with Oracle Autonomous AI Database
* Familiarity with Oracle Cloud Infrastructure (OCI) GenAI Service
* Access to OCI GenAI Services LLM

## Task 1: Access Oracle Data Science Agent

[](include:oml-dsa-access.md)

## Task 2: Review the recommended models for use with Data Science Agent

[](include:oml-dsa-recommended-models.md)


## Learn More

Use these links to get more information about Oracle Machine Learning and Oracle Cloud Infrastructure:

* [Using Oracle Data Science Agent](https://docs.oracle.com/en/database/oracle/machine-learning/data-science-agent/dsaug/index.html)
* [Oracle Cloud Infrastructure Documentation](https://docs.cloud.oracle.com/iaas/Content/GSG/Reference/gettingstartedwithPaaS.htm)
* [Overview of Oracle Cloud Infrastructure Identity and Access Management (IAM)](https://docs.cloud.oracle.com/en-us/iaas/Content/Identity/Concepts/overview.htm)
* [Oracle Cloud Infrastructure Self-paced Learning Modules](https://www.oracle.com/cloud/iaas/training/foundations.html)
* [Oracle LiveLabs](https://livelabs.oracle.com/ords/r/dbpm/livelabs/home)


## Acknowledgements
* **Author** : Moitreyee Hazarika, Consulting User Assistance Developer, Database User Assistance Development
* **Contributors**: Mark Hornick, Senior Director, Data Science and Machine Learning; Marcos Arancibia Coddou, Product Manager, Oracle Data Science; Sherry LaMonica, Consulting Member of Tech Staff, Machine Learning
* **Last Updated By/Date**: Moitreyee Hazarika, July 2026
