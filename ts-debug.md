---

copyright:
  years: 2024, 2024
lastupdated: "2024-09-10"

keywords: instructlab, debugging

subcollection: instructlab

---


{{site.data.keyword.attribute-definition-list}}



# Debugging
{: #ts-debug}
{: support}


Debug an issue when you experience it.
{: tsSymptoms}

There might be a configuration issue with the taxonomy or a CLI version issue.
{: tsCauses}

Try one of the following options to resolve the issue.
{: tsResolve}


## Validating the local taxonomy
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

4. Run the `diff` command where the `--taxonomy-base` is the branch to compare the local files with. If you are using the InstructLab community taxonomy, this branch is `main`.

    ```sh
    ilab taxonomy diff --taxonomy-path <local-path-to-taxonomy>  --taxonomy-base main
    ```
    {: pre}

    Output:
    ```txt
    Taxonomy in <local-path-to-taxonomy> is valid :)
    ```
    {: screen}


## Verifying the version
{: #version}

If the issues are with the backend and not your taxonomy or local configuration, verify that the local CLI installation version matches what is being used in the backend.

1. Get the back end `instructlab` version.

    a. In the COS bucket, click **synthetic_data** > ***ID*** > **logs** > **ilab_system_info.log**.

    b. Click **Download object** to download the log file.

    c. Note the value for `instructlab.version`.

1. Get the local CLI version.
    ```sh
    ibmcloud ilab -v
    ```
    {: pre}

1. If the versions do not match, update the local CLI plugin.

    ```sh
    ibmcloud plugin update ilab -r stage
    ```
    {: pre}
