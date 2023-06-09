# Installation of miniconda3, miniconda3 module for Lmod module environment (Lua-based), and conda environements (e.g., regional_workflow)

Last revision: July 5, 2023  (update as needed) @natalie-perlin 

1. Find a right installer script to download from **URL="https://repo.anaconda.com/miniconda"**, or determine its correct name, e.g., `Miniconda3-py39_4.12.0-Linux-x86_64.sh`

2. Configure the installation script **miniconda3_install.sh** as follows:

   a) BASH_ENV  - Lmod initialization script to be sourced, e.g.,
                `BASH_ENV=/apps/lmod/lmod/init/bash`
                
                
   b) installer - installer name to use or download from the URL (as in step 1).  
          e.g., `installer="Miniconda3-py39_4.12.0-Linux-x86_64.sh"`
          
   c) version   - miniconda3 version
          e.g., `version="4.12.0"`
          
   d) PREFIX0  - a local installation path of the miniconda3, for all versions;
      PREFIX   - a local installation path for a particular version, e.g.,
                `PREFIX0="/home/miniconda3"`, 
                `PREFIX="${PREFIX0}/${version}"`
                
   e) verify the modulefile **miniconda3template.lua** template is present in a directory from which the scrips is lauched, and specify a target modulefile location for miniconda3, e.g.,
               `MODULEFILES="$PREFIX0/modulefiles"`

3. Configure the modulefile *miniconda3template.lua* and specify a local prefix, e.g.,
       `local prefix = pathJoin("/home",pkgName)`

4. Run the installation script wrapper: 
   `./miniconda3_install.sh 2>&1 | tee log.miniconda_install`
   
5. Create a **regional_workflow** environment with the packages needed to run the UFS-SRW
   App and to use graphic packages for plotting. Packages to be installed are listed
   in `regional_workflow.yaml` file that is expected to be present in the same 
   directory as the installation script  **miniconda3_regional_workflow_env.sh**.   
   Configure the env. varialbles in the script similar to Step 2,
   and then launch it:   
   `./miniconda3_regional_workflow_env.sh 2>&1 | tee log.regional_workflow_install`
6. Create a **workflow_toos** environment with the packages for the updated UFS-SRW
   Packages to be installed are listed
   in `workflow_tools.yaml` file that is expected to be present in the same 
   directory as the installation script  **miniconda3_workflow_tools_env.sh**.   
   Configure the env. varialbles in the script similar to Step 2 and 5,
   and then launch it:   
   `./miniconda3_workflow_tools_env.sh 2>&1 | tee log.workflow_tools_install`
6. Create a **regional_workflow_cmaq** environment with the packages for UFS-SRW
   and for Air Quality Management module (Online-CMAQ).
   Packages to be installed are listed
   in `regional_workflow_cmaq.yaml` file that is expected to be present in the same 
   directory as the installation script  **miniconda3_regional_workflow_cmaq_env.sh**.   
   Configure the env. varialbles in the script similar to Step 2 and 5,
   and then launch it:   
   `./miniconda3_regional_workflow_cmaq_env.sh 2>&1 | tee log.regional_workflow_cmaq_install`
