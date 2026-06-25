# Define AI Profile for use with Data Science Agent

## Introduction

In this lab, you will define an AI profile for use with Data Science Agent (DSA). Autonomous AI Database uses AI profiles to configure access to a large language model (LLM), generate SQL from natural language prompts, run SQL, explain SQL, and support retrieval augmented generation with embedding models and vector indexes.

You will also grant the required OML role to the OML user and configure host Access Control List (ACL) access for model providers that require outbound network access.

**Estimated Lab Time:** 30 minutes

### Objectives

In this lab, you will:
* Create an AI profile using `DBMS_CLOUD_AI`
* Grant the `OML_DEVELOPER` role to an OML user
* Add the OML user to the host ACL for OpenAI access
* Verify each configuration step

### Prerequisites

This lab assumes you have:
* Completed all previous labs
* Access to an Autonomous AI Database
* Administrator privileges or equivalent permissions
* An OML user, such as `OMLUSER`
* A configured credential for the model provider, such as `openai_cred`

## Task 1: Use DBMS_CLOUD_AI to Configure AI Profiles

AI profiles define how Autonomous AI Database connects to an LLM and which profile attributes are used for natural language to SQL translation. These profiles can include metadata from database objects such as table names, column names, column data types, and comments.

1. Review the `DBMS_CLOUD_AI.CREATE_PROFILE` procedure signature.

    This procedure creates a new AI profile. The profile can later be used to translate natural language prompts into SQL statements and to configure access to an LLM provider.

    ```sql
    <copy>
    DBMS_CLOUD_AI.CREATE_PROFILE(

       profile_name        IN  VARCHAR2,

       attributes          IN  CLOB      DEFAULT NULL,

       status              IN  VARCHAR2  DEFAULT NULL,

       description         IN  CLOB      DEFAULT NULL

    );
    </copy>
    ```

2. Review the required and optional parameters.

    The `profile_name` parameter is mandatory and must follow Oracle SQL identifier naming rules. The `attributes` parameter defines profile attributes in JSON format. The `status` parameter controls whether the profile is enabled, and the `description` parameter provides additional context about the profile.

    The expected output should look similar to:

    ```
    Procedure reviewed successfully.

    Required parameter:
    - profile_name

    Optional parameters:
    - attributes
    - status
    - description
    ```

3. Create the AI profile.

    Run the following PL/SQL block to create an AI profile named `NL2SQL`. This profile uses OpenAI as the provider and references the `openai_cred` credential for SQL translation.

    ```sql
    <copy>
    BEGIN

         DBMS_CLOUD_AI.CREATE_PROFILE(

              profile_name    => 'NL2SQL',

              attributes      => JSON_OBJECT('provider' value 'openai',

                                             'credential_name' value 'openai_cred'),

            status     => 'enabled',                             

              description     => 'AI profile to use OpenAI for SQL translation'

         );

    END;

    /
    </copy>
    ```

    The expected output should look similar to:

    ```
    PL/SQL procedure successfully completed.
    ```

    ![Verify that the NL2SQL AI profile was created successfully](images/verify-ai-profile-created.png "Verify AI Profile Created")

4. Review support for additional data sources.

    In addition to specifying tables and views in the AI profile, you can specify tables mapped with external tables, including external data queried with Data Catalog. This enables you to query data inside the database and data stored in an object store.

    The expected output should look similar to:

    ```
    AI profile configuration supports:
    - Database tables
    - Database views
    - External tables
    - Data lake object store data
    ```

## Task 2: Grant OML_DEVELOPER Role to OML User

To use Data Science Agent, the administrator must grant the `OML_DEVELOPER` role to the OML user. If the OML user, such as `OMLUSER`, is created through Database Actions, the `OML_DEVELOPER` role is automatically granted.

1. Grant the `OML_DEVELOPER` role to the OML user.

    Run the following command as an administrator to grant the role required for Data Science Agent access.

    ```sql
    <copy>
    GRANT OML_DEVELOPER to OMLUSER
    </copy>
    ```

    The expected output should look similar to:

    ```
    Grant succeeded.
    ```

    ![Verify that the OML_DEVELOPER role was granted to OMLUSER](images/verify-oml-developer-role.png "Verify OML_DEVELOPER Role")

## Task 3: Add User to the Host ACL

For model providers such as OpenAI, you must add users to the host ACL so the database user can access the model provider endpoint.

> **Note:** Host ACL entry is not required for OCI GenAI.

1. Add `OMLUSER` to the host ACL.

    Run the following procedure to grant the privilege to use the `api.openai.com` endpoint. This allows `OMLUSER` to make HTTP requests to the OpenAI API host.

    ```sql
    <copy>
    BEGIN
        DBMS_NETWORK_ACL_ADMIN.APPEND_HOST_ACE(
             host => 'api.openai.com',
             ace  => xs$ace_type(privilege_list => xs$name_list('http'),
                                 principal_name => 'OMLUSER',
                                 principal_type => xs_acl.ptype_db)
       );
    END;
    </copy>
    ```

    The expected output should look similar to:

    ```
    PL/SQL procedure successfully completed.
    ```

    ![Verify that OMLUSER was added to the host ACL for api.openai.com](images/verify-host-acl-openai.png "Verify Host ACL for OpenAI")

2. Review the host ACL parameters.

    The `host` parameter specifies the host name or IP address that the database user can access. The `ace` parameter defines the access control entry, including the privilege list, principal name, and principal type.

    The expected output should look similar to:

    ```
    Host ACL configuration reviewed.

    host:
    api.openai.com

    principal_name:
    OMLUSER

    privilege:
    http
    ```

## Learn More

* [Oracle Machine Learning](https://docs.oracle.com/en/database/oracle/machine-learning/)
* [Oracle Data Science Agent](https://docs.oracle.com/en/database/oracle/machine-learning/data-science-agent/index.html)
* [Oracle Autonomous Database](https://docs.oracle.com/en/cloud/paas/autonomous-database/)
* [Oracle LiveLabs](https://oracle-livelabs.github.io/)

## Acknowledgements

* **Author** - Moitreyee Hazarika, Consulting User Assistance Developer, Oracle AI Database User Assistance Development
* **Contributors** - Mark Hornick, Senior Director, Data Science and Machine Learning; Marcos Arancibia Coddou, Product Manager, Oracle Data Science; Sherry LaMonica, Consulting Member of Tech Staff, Machine Learning
* **Last Updated By/Date** - Moitreyee Hazarika, November 2026
