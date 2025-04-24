---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-24"

keywords: instructlab, debugging

subcollection: instructlab

---


{{site.data.keyword.attribute-definition-list}}



# Debugging issues for {{site.data.keyword.short_name}}
{: #ts-debug}
{: support}


## Debugging configuration issues
{: #debug-issues}

Debug an issue when you experience it.
{: tsSymptoms}

There might be a configuration issue with the taxonomy or a CLI version issue.
{: tsCauses}

Try one of the following options to resolve the issue.
{: tsResolve}


#### Step 1: Validate the local taxonomy
{: #local-taxonomy}

1. [Install the `ilab` CLI](https://github.com/instructlab/instructlab?tab=readme-ov-file#-installing-ilab).

2. Run the `ilab` command to verify that the CLI is installed.

    ```sh
    ilab
    ```
    {: pre}

    Output:
    ```sh
    Usage: ilab [OPTIONS] COMMAND [ARGS]...

       CLI for interacting with InstructLab.
       ...
    ```
    {: screen}

3. Initialize the `ilab` CLI and complete the prompts.

    ```sh
    ilab init
    ```
    {: pre}

4. Run the `diff` command where the `--taxonomy-base` is the branch to compare the local files with. If you are using the {{site.data.keyword.short_name}} community taxonomy, this branch is `main`.

    ```sh
    ilab taxonomy diff --taxonomy-path <local-path-to-taxonomy>  --taxonomy-base empty
    ```
    {: pre}

    Output:
    ```txt
    Taxonomy in <local-path-to-taxonomy> is valid :)
    ```
    {: screen}


#### Step 2: Verify the version
{: #version}

If the issues are with the backend and not your taxonomy or local configuration, verify that the local CLI installation version matches what is being used in the backend.

1. Get the back end `instructlab` version.

    a. In the {{site.data.keyword.cos_short}} bucket, click **`synthetic_data`** > ***ID*** > **logs** > **ilab_system_info.log**.

    b. Click **Download object** to download the log file.

    c. Note the value for `instructlab.version`.

1. Get the local CLI version.
    ```sh
    ibmcloud ilab -v
    ```
    {: pre}

1. If the versions do not match, update the local CLI plug-in.

    ```sh
    ibmcloud plugin update ilab
    ```
    {: pre}
