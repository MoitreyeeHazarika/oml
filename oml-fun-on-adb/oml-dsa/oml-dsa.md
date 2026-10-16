# Introduction to Data Science Agent

## Introduction

This lab walks you through the steps to use Data Science Agent in Oracle Machine Learning UI.

Estimated Time: 15 minutes

### About Data Science Agent
Data Science Agent is an intelligent built-in conversational chatbot integrated with Oracle Machine Learning UI included in your Oracle Autonomous AI Database subscription. You must provide the LLM, specified through your AI profile, whether from a third-party AI provider, OCI GenAI Service, or one you privately host. You can run complete data science workflows using natural language in the Data Science Agent chat.

As a human-in-the-loop chatbot, Data Science Agent requires your intervention and approval in the following areas:

* **Object association:** Objects must be associated or approved before the agent creates views that use them; other supported operations may still use accessible objects based on the user's database privileges. Associating database objects with a conversation improves precision and efficiency.
* **Conversation management:** The scope of Data Science Agent is limited to the active conversation context only. You must create, manage, and delete your conversations.
* **Profile selection:** You must select an AI profile and, therefore, the LLM that powers the agent. You can choose an existing profile or create and select your own. You can also switch profiles mid-conversation.
* **Approval for object viewing:** During a conversation, Data Science Agent compares the requested objects with those already associated with the active conversation. If a required table or view is not in the approved set, the agent pauses and asks for your approval to add it. If you approve, the object is associated with the conversation and the agent continues. If you do not approve, the request is canceled and no view is created.

### Objectives

In this lab, you will learn how to:
* Create 

### Prerequisites

This lab assumes you have:
* An Oracle Machine Learning account
* OML administrator role (ADMIN)
* OML developer role (OML_DEVELOPER)
* Access to Oracle Machine Learning USER account

## Task 1: Access Oracle Data Science Agent


## Task 2: Review the recommended models for use with Data Science Agent


## Task 3: Explore Data Science Agent

* [Get Started with Oracle Data Science Agent](https://livelabs.oracle.com/ords/dbpm/r/livelabs/view-workshop?wid=4468)
* [Recommended Models](https://docs.oracle.com/en/database/oracle/machine-learning/data-science-agent/dsaug/dsa-create-ai-credential-and-profile.html#GUID-FD8053A2-5988-43B9-B024-19EEBA5CD9D4)
* [Create AI Credential and AI Profile](https://docs.oracle.com/en/database/oracle/machine-learning/data-science-agent/dsaug/dsa-create-ai-credential-and-profile.html#GUID-BEF5D9CD-2CDB-468B-A9D6-76A20D3310E1)
* [Issue Prompts to Data Science Agent](https://docs.oracle.com/en/database/oracle/machine-learning/data-science-agent/dsaug/dsa-example-model-deploy.html#GUID-BEF5D9CD-2CDB-468B-A9D6-76A20D3310E1)


## Learn More

* [Data Science Agent](https://docs.oracle.com/en/database/oracle/machine-learning/data-science-agent/index.html)
* [Oracle Machine Learning UI](https://docs.oracle.com/en/database/oracle/machine-learning/oml-notebooks/)


## Acknowledgements

* **Author** : Moitreyee Hazarika, Consulting User Assistance Developer, Database User Assistance Development
* **Contributors**: Mark Hornick, Senior Director, Data Science and Machine Learning; Marcos Arancibia Coddou, Product Manager, Oracle Data Science; Sherry LaMonica, Consulting Member of Tech Staff, Machine Learning
* **Last Updated By/Date**: Moitreyee Hazarika, October 2026
