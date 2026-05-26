# nextflow

Install and configure Nextflow on RedHat and Debian systems.

## Usage

| Name | Description | Default |
| ---- | ----------- | ------- |
|`nextflow_openjdk_package_name` | Name of a package that provides Java JDK > 11 | "java-21-openjdk" or "openjdk-21-jdk" |
|`nextflow_version` | Nextflow version to install | "v24.10.4" |
|`nextflow_executable_url` | URL to download Nextflow from | https://github.com/nextflow-io/nextflow/releases/download/{{ nextflow_version }}/nextflow |
|`nextflow_skel_config` | Config to add to /etc/skel/.nextflow/config | UNSET |
