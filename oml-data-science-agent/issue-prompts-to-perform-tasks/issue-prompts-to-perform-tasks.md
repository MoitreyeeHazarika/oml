# Issue prompts to perform Data Science and Machine Learning tasks

## Introduction

In this lab, you will issue a sequence of prompts to Data Science Agent to perform data science and machine learning tasks. You will run a complete machine learning workflow using natural language, progressing from general questions about the data in the `OMLUSER` schema to model training, model building, evaluation, and scoring.

By the end of this lab, you will see how Data Science Agent supports a novice user in exploring the dataset present in the `OMLUSER` schema and in building and evaluating a machine learning model. You will use natural language to prepare data, generate SQL, create visualizations, train models, interpret model results, and score prospects.

>**Note:** This is an agent-driven workflow. Outputs can vary by model, profile, seed, data state, and previous conversation context. Your generated object names and model results may differ. Use the names shown in your response.

Estimated Time: X

### Objectives

In this lab, you will:
* Set the goal and context for a Data Science Agent conversation
* Explore the `CLIENTS`, `CONTACTS`, `PAST_CAMPAIGNS`, and `PROSPECTS` tables
* Frame subscription likelihood as a machine learning problem
* Create a single modeling table from multiple source tables
* Perform feature validation and prepare a clean modeling view
* Split data into training, validation, and test sets
* Train and evaluate a model to predict subscription likelihood
* Score prospects by using the trained model

### Prerequisites

This lab assumes you have:
* Completed all previous labs
* Access to Data Science Agent
* The `CLIENTS`, `CONTACTS`, `PAST_CAMPAIGNS`, and `PROSPECTS` tables added as Associated Objects
* Access to the `OMLUSER` schema

>**Note:**  The output in this lab are examples. The suffixes, selected algorithm, metrics, row counts, and names of models and views may differ when you run the workshop in your environment. Use the object names generated in your session wherever needed.

## Task 1: Set the conversation goal and context

In this task, continue the `Predict Subscription` conversation you created in Lab 3: Create a Data Science Conversation. Provide enough context for the agent to understand your role, your experience level, and the data you want to explore. This helps the agent tailor its response and explain the machine learning workflow in an accessible way.

1. Open the `Predict Subscription` conversation, and review the tips displayed in the chat interface.

    ![Data Science Agent tips shown at the start of a new conversation](images/ml-prompt-01.png "Goal and context setting")

2. Enter the following prompt to set the goal and context for the conversation. This prompt tells Data Science Agent that you are an analyst without any data science background. You ask the agent to explain the data and how to use it to solve a business problem.

    ```text
    <copy>
    I'm an analyst without a data science background, interested on running a new marketing campaign.  What data is available and how can it be used?
    </copy>
    ```

    In response to this prompt, Data Science Agent provides an overview of the available data, explains how it can be used in the new marketing campaign, and provides a brief summary of the tables CLIENTS, CONTACTS, PAST_CAMPAIGN, and PROSPECTS. Review the summary of the data in each table and the explanation on how to use this data in the new marketing campaign.

    ![Prompt 1 response showing table summaries and key columns](images/dsa-ma-p1r1.png "Prompt 1 and response")

    > **Note:** The outputs in this lab are examples only. The suffixes, selected algorithm, metrics, and row counts may differ in your environment. Use the object names generated in your session wherever needed.

3. Scroll down and expand the Object Discovery Summary section. This section provides lists the keys, main attributes and joins in each table.

    ![Prompt 1 Object Discovery summary](images/dsa-ma-p1r3a.png "Object Discovery summary")

## Task 2: Data Exploration

In this task, you will ask Data Science Agent to .

1. Enter the following prompt to create a single view by joining the CLIENT, CONTACTS, and PAST_CAMPAIGN data for every client who has been contacted.

    ```text
    <copy>
    I would like to identify which customers would buy a new insurance product we are launching.
    </copy>
    ```

    ![Prompt 2 and response](images/dsa-ma-p2r1.png "Prompt 2 and response")

    In response to the prompt, Data Science Agent recommends a workflow based on the available data. It also asks clarifying questions to guide you on the next steps. See screenshot for details.

2. Review the response and enter the following prompt:

    ```text
    <copy>
    We can focus on customers that have one or more banking products, and want to check customers that responded to a campaign as a proxy.
    </copy>
    ```

    ![Prompt 3 and response](images/dsa-ma-p3r1.png "Prompt 3 and response")

    In response to your input, Data Science Agent suggests a tailored approach based on your data as follows:
    * Find customers who already have at least one banking product, such as a home loan or personal loan.
    * Check whether these customers took part in a campaign and focus on those who responded “SUBSCRIBED,” as they are more likely to buy.
    * Create and study a dataset that combines customer details, banking products, and campaign responses.

    It also asks you to confirm whether to qualify customers (with ) or to include all prior campaign 

## Task 2: Data Preparation

1. Review the response and enter the following prompt:

    ```text
    <copy>
    Let's use either product, and use all campaign contacts available
    </copy>
    ```

    ![Prompt 4 and response](images/dsa-ma-p4r1.png "Prompt 4 and response")

    In response to the prompt, Data Science Agent created the view `DSAGENT$BANKINGPRODUCT_CONTACTS_C4A0` by combining all customers who have either a housing load or a personal loan with their full campaign contact history. This is done to analyze which types of customers are most likely to respond to marketing, and therefore predict likely buyers.

2. Expand the **Details on Created View** section to review the SQL code used to define the view `DSAGENT$BANKINGPRODUCT_CONTACTS_C4A0`.

    > **Note:** Views and objects created by Data Science Agent have the prefix `DSAGENT$`.

    ![Prompt 4 response (contd)](images/dsa-ma-p4r2.png "Prompt 4 and response")

3. Expand the **Visual Diagram** section to understand the workflow of the view `DSAGENT$BANKINGPRODUCT_CONTACTS_C4A0`

    ![Prompt 4 and response](images/dsa-ma-p4r3.png "Prompt 4 and response")

    > **Note:** The outputs in this lab are examples only. The suffixes, selected algorithm, metrics, and row counts may differ in your environment. Use the object names generated in your session wherever needed.

## Task 3: Explore the dataset

In this task, you will ask Data Science Agent to explain the characteristics of the customers. In this process, xxx

> **Note:** Views and objects created by Data Science Agent have the prefix `DSAGENT$`.

1. Enter the following prompt to explore the dataset and understand the basic statistics.

    ```text
    <copy>
    Provide the basic statistics for this data..
    </copy>
    ```

    In response to this prompt, Data Science Agent provides a summary of the characteristics of the customers (who owned at least one banking product and participated in campaign contacts). The main characteristics of the customers are listed out as - Age Balance, Education, Job, Marital Status, Loan Ownership, Credit Default, Contact Method, Contact Frequency, Contact Duration, and Campaign Response. It also provides a full breakdown of the dataset in summary tables and charts for each variable.

    ![Prompt 3 response showing machine learning problem framing and target variable](images/dsa-ma-p5r1.png "Prompt 3 and response")

2. Expand the **Attribute Analysis** section for a detailed description and analysis of the attributes.

    ![Prompt 3 response showing machine learning problem framing and target variable](images/dsa-ma-p5r2.png "Prompt 3 and response")

3. Expand the **Attribute Statistics** section for a detailed view of the attributes. For each attribute, it shows the data distribution and statistics, along with a statistical visualization - boxplot, bar chart etc, as applicable. In this example, Data Science Agent depicts the age distribution in a boxplot and it computes these statistics - Mean, Median, Standard Deviation, Minimum value, Maximum value, Quartile 1, Quartile 3, Row counts, and the counts for NON_NULL.

    ![Response to prompt 3](images/dsa-ma-p5r3.png "Response to prompt 3")

    The agent also asks if you would like to identify the factors that are strongly linked to customers responding to the campaign or to proceed directly to building a predictive model.

    > **Note:** The outputs in this lab are examples only. The suffixes, selected algorithm, metrics, and row counts may differ in your environment. Use the object names generated in your session wherever needed.

In this task, you will ask Data Science Agent to to identify the factors that are strongly linked to customers responding to the campaign.

4. Enter the following prompt to ask Data Science Agent to .

    ```text
    <copy>
    Let's check the factors linked to responding to campaigns.  Also, we cannot use the call duration in seconds nor the contact date, since these are not known ahead of the campaign.
    </copy>
    ```

    In response to this prompt, Data Science Agent lists out the factors that are most strongly linked to positive campaign responses among the customers. It also provides a full  statistical details and charts.

    ![Prompt 6 response showing c](images/dsa-ma-p6r1.png "Prompt 6 and response")

5. Expand the **Relationship Analysis** section for a detailed analysis of the relationship between the various attributes and the likelihood of subscription. See screenshot below:

    ![Prompt 6 response showing xxx](images/dsa-ma-p6r2.png "Prompt 6 and response")

6. Expand the **Relationship Statistical** section for a statistical analysis of the relationship between the various attributes and the likelihood of subscription. See screenshot below:

    ![Prompt 6 response showing xxx](images/dsa-ma-p6r3.png "Prompt 6 and response")

    Data Science Agent also asks you if you would like to proceed to building a predictive model that combines these factors to identify the most likely buyers for your insurance product.

## Task 4: Feature Ranking

Based on the suggestion provided by Data Science Agent, in this task you will proceed to build a predictive model.

1. Enter the following prompt to allow Data Science Agent to build a predictive model xxx

    ```text
    <copy>
    Yes please, build the model.
    </copy>
    ```

    ![Prompt 7 response showing xxx](images/dsa-ma-p7r1.png "Prompt 7 and response")

    In response to your prompt, Data Science Agent first ranks the importance of each feature so that the model only uses the most relevant predictors. The agent lists the following algorithms:

    * XGBoost (default)
    * Random Forest
    * AI_MDL
    * CUR Decomposition

    Data Science Agent creates the view `DSAGENT$BANKINGPRODUCT_MODELSET_C4A0`.

    > **Note:** Views and objects created by Data Science Agent have the prefix `DSAGENT$`.

2. Expand the **Details on Created View** section to review the SQL code generated by Data Science Agent to create the view `DSAGENT$BANKINGPRODUCT_MODELSET_C4A0`.

    ![Prompt 7 response showing xxx](images/dsa-ma-p7r2.png "Prompt 7 and response")

3. Expand the **Visual Diagram** section to understand the workflow of the view `DSAGENT$BANKINGPRODUCT_MODELSET_C4A0`.

    ![Prompt 7 response showing xxx](images/dsa-ma-p7r3.png "Prompt 7 and response")

    >**Note:**  The outputs in this lab are examples only. The suffixes, selected algorithm, metrics, and row counts may differ in your environment. Use the object names generated in your session wherever needed.

    Data Science Agent also asks for your choice of algorithm for model building. Or else, the agent would proceed with XGBoost.

## Task 5: Model Building 

 In this task, you will focus on model building.

1. Enter the following prompt to proceed with model building.

    ```text
    <copy>
    Please proceed.
    </copy>
    ```

    ![Prompt 8 response](images/dsa-ma-p8r1.png "Prompt 8 and response")

    In response to this prompt, Data Science Agent builds a modeling dataset containing only the most important features for predicting which customers are likely to respond to the campaign.

    The agent provides you with the following choices:
    * Train and later evaluate a single predictive model
    * Compare multiple models to select the best performer


## Task 6: Model Comparison and Data Split

In this task, you will ask Data Science Agent evaluate the model. In this process, Data Science Agent splits the data into 70% training dataset, 20% test dataset, and 10% validation dataset.


1. Enter the following prompt to evaluate the model.

    ```text
    <copy>
    Compare multiple models please.
    </copy>
    ```

    ![Prompt 9 response showing xxx](images/dsa-ma-p9r1.png "Prompt9 and response")

    In response to this prompt, Data Science Agent evaluates the model and splits the data into:

    * 70% Training: Used to learn patterns
    * 10% Validation: Used to compare models and select the best algorithm
    * 20% Test: Held back for unbiased final evaluation

2. Expand the **Details on Split** section to review the splits created from the view `DSAGENT$BANKINGPRODUCT_MODELSET_C4A0_TOP_XGB`.

    ![Prompt 6 response showing data split and model training](images/dsa-ma-p9r2.png) "Prompt 6 and response"



## Task 7: xxxx

In this task, you will ask Data Science Agent to score the prospects for the next campaign.

>**Note:**  The outputs in this lab are examples only. The view names, model names, suffixes, selected algorithm, metrics, and row counts may differ in your environment. Use the object names generated in your session wherever needed.

1. Enter the following prompt to score the xxx

    ```text
    <copy>
    Score the prospects for our next campaign. Who should we prioritize reaching out to?
    </copy>
    ```

    ![Prompt 7 response showing scored prospects and prediction probabilities](images/t7-p1-r1.png "Prompt 7 and response")

    In this example, Data Science Agent could not perform scoring. It correctly states the reason - it is because the latest view used for modeling excluded the CLIENT_ID column. This column is required to identify and report predictions for the prospects.

2. Prompt "Yes" in your response to the agent's suggestion "Would you like me to update the feature set to include CLIENT_ID and then proceed with scoring your prospect list?"

    ```text
    <copy>
    Yes
    </copy>
    ```
    ![Prompt 7 and response](images/t7-p2-r2.png "Prompt 7 and response")

    Now, Data Science Agent adds CLIENT_ID into the dataset, then performs scoring using the predictive model, and presents the list of prospects for the next campaign.

3. Expand the **Details on Created View** section to review the details of the view `DSAGENT$CLIENTS_CONTACTS_CAMPAIGNS_E6B9_FE_SCR_E6B9`.

    ![Prompt 7 response ](images/t7-p2-r3.png "Prompt 7 response concluded")


4. Expand the **Visual Diagram** section to understand the workflow of the view `DSAGENT$CLIENTS_CONTACTS_CAMPAIGNS_E6B9_FE_SCR_E6B9`.

    ![Prompt 7 response](images/t7-p2-r4.png "Prompt 7 response concluded")

5. Expand the **SQL Code for Manual Inference** section to review the SQL query to run the inference manually.

    ![Prompt 7 response concluded showing manual inference SQL query](images/t7-p2-r5.png "Prompt 7 response concluded")

6. Review the prediction table showing the probability of subscription for the prospects.

    ![Prompt 7 response showing scored prospects and prediction probabilities](images/t7-p2-r6.png "Prompt 7 and response")

    In this example, Data Science Agent returns the probability of subscription for the prospects in the following table:

    | CLIENT_ID | PREDICTED | PROBABILITY OF Y (%) |
|---:|:---:|---:|
| 44864 | Y | 84.74 |
| 41426 | Y | 73.15 |
| 42062 | Y | 61.62 |
| 39530 | Y | 61.38 |
| 42271 | Y | 57.82 |
| 43388 | Y | 56.27 |
| 40622 | Y | 54.1 |
| 42421 | Y | 52 |
| 41516 | Y | 50.91 |
| 42999 | N | 47.7 |
| 34209 | N | 42.11 |
| 39606 | N | 42.11 |
| 28649 | N | 34.96 |
| 39361 | N | 34.12 |
| 42881 | N | 32.57 |
| 31511 | N | 32.4 |
| 42471 | N | 31.01 |
| 39974 | N | 25.03 |
| 43021 | N | 24.82 |
| 28092 | N | 24.81 |
| 28803 | N | 22.63 |
| 19884 | N | 21.09 |
| 9900 | N | 21.09 |
| 33871 | N | 20.17 |
| 26416 | N | 19.78 |
| 28122 | N | 19.19 |
| 35610 | N | 18.55 |
| 33972 | N | 18.37 |
| 34337 | N | 17.81 |
| 32596 | N | 17.21 |
| 7803 | N | 16.73 |
| 9371 | N | 16.73 |
| 18373 | N | 16.73 |
| 42756 | N | 16.19 |
| 38445 | N | 15.96 |
| 43531 | N | 15.88 |
| 19187 | N | 15.73 |
| 19727 | N | 15.41 |
| 13147 | N | 15.3 |
| 8245 | N | 14.92 |
| 43691 | N | 14.92 |
| 27938 | N | 14.69 |
| 33429 | N | 14.46 |
| 29635 | N | 13.72 |
| 34756 | N | 13.07 |
| 15737 | N | 12.96 |
| 44398 | N | 12.4 |
| 13506 | N | 11.64 |
| 28653 | N | 10.54 |
| 18175 | N | 10.28 |
| 3245 | N | 10.16 |
| 23636 | N | 9.9 |
| 13693 | N | 9.57 |
| 23692 | N | 9.56 |
| 6609 | N | 9.36 |
| 19622 | N | 9.11 |
| 29400 | N | 9.11 |
| 33840 | N | 9.11 |
| 19347 | N | 8.62 |
| 35998 | N | 8.17 |
| 32365 | N | 8.14 |
| 34426 | N | 8.14 |
| 26727 | N | 8.04 |
| 21997 | N | 7.71 |
| 10157 | N | 7.69 |
| 11472 | N | 7.52 |
| 32507 | N | 7.52 |
| 12261 | N | 7.25 |
| 35599 | N | 7.09 |
| 33168 | N | 7.09 |
| 27509 | N | 7.09 |
| 5756 | N | 6.73 |
| 23828 | N | 6.27 |
| 36589 | N | 6.1 |
| 20560 | N | 5.7 |
| 21200 | N | 5.66 |
| 11943 | N | 5.47 |
| 300 | N | 5.06 |
| 5346 | N | 5.06 |
| 15421 | N | 4.26 |
| 18254 | N | 4.25 |
| 5752 | N | 4.18 |
| 23293 | N | 4.06 |
| 3122 | N | 3.8 |
| 38629 | N | 3.66 |
| 12945 | N | 3.63 |
| 24120 | N | 3.44 |
| 16154 | N | 3.17 |
| 17138 | N | 3.17 |
| 19715 | N | 2.56 |
| 34440 | N | 2.46 |
| 12686 | N | 2.37 |
| 4712 | N | 2.37 |
| 3995 | N | 2.21 |
| 1522 | N | 2.15 |
| 35231 | N | 1.93 |
| 33149 | N | 1.75 |
| 35627 | N | 1.53 |
| 38748 | N | 1.09 |
| 15249 | N | 0.6 |

>**Note:**  The outputs in this lab are examples only. The view names, model names, suffixes, selected algorithm, metrics, and row counts may differ in your environment. Use the object names generated in your session wherever needed.

## Learn More

* [Oracle Machine Learning](https://docs.oracle.com/en/database/oracle/machine-learning/)
* [Oracle Data Science Agent](https://docs.oracle.com/en/database/oracle/machine-learning/data-science-agent/index.html)
* [Oracle Autonomous Database](https://docs.oracle.com/en/cloud/paas/autonomous-database/)
* [Oracle LiveLabs](https://livelabs.oracle.com/ords/r/dbpm/livelabs/home)

## Acknowledgements

* **Author** - Moitreyee Hazarika, Consulting User Assistance Developer, Oracle AI Database User Assistance Development
* **Contributors** - Mark Hornick, Senior Director, Data Science and Machine Learning; Marcos Arancibia Coddou, Product Manager, Oracle Data Science; Sherry LaMonica, Consulting Member of Tech Staff, Machine Learning
* **Last Updated By/Date** - Moitreyee Hazarika, September 2026
