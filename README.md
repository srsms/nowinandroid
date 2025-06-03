Initialization Command:
```
git clone https://github.com/sphinx-doc/sphinx
git config --global --add safe.directory /swebench/sphinx
cd sphinx
git checkout bf26080042fabf6e3aba22cfe05ad8d93bcad3e9
```

<details><summary>Original output.json</summary>
<pre><code>{
    "arch": "aarch64",
    "base_commit": "a8abb9995f71b9bc02b6f83592751c779ae0f75a",
    "dependencies": "alabaster==0.7.1\nBabel==2.7.0\ncertifi==2025.1.31\ncharset-normalizer==3.4.1\ncoverage==7.6.1\nCython==3.0.12\ndocutils==0.20.1\nexceptiongroup==1.2.2\nhtml5lib==1.1\nidna==3.10\nimagesize==1.4.1\niniconfig==2.1.0\nJinja2==2.11.3\nMarkupSafe==2.0.1\npackaging==24.2\npluggy==1.5.0\nPygments==2.19.1\npytest==8.3.5\npytest-cov==5.0.0\npytz==2025.2\nrequests==2.32.3\nsix==1.17.0\nsnowballstemmer==2.2.0\nsphinxcontrib-applehelp==1.0.4\nsphinxcontrib-devhelp==1.0.2\nsphinxcontrib-htmlhelp==2.0.1\nsphinxcontrib-jsmath==1.0.1\nsphinxcontrib-qthelp==1.0.3\nsphinxcontrib-serializinghtml==1.1.5\ntomli==2.2.1\ntyped-ast==1.5.5\nurllib3==2.2.3\nwebencodings==0.5.1\n",
    "fail_to_pass": [],
    "instance_id": "None",
    "pass_to_pass": [],
    "pytest_version": "8.3.5",
    "setup_environment_cmds": [
        "conda create -n testbed python=3.8.5 -y",
        "conda env config vars set -n testbed DO_EPUBCHECK=1",
        "conda activate testbed",
        "apt-get update && apt-get install dvipng dvisvgm texlive-base texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended texinfo -y",
        "conda install -c conda-forge python-graphviz=0.20.1 -y",
        "pip install -r ../requirements.txt"
    ],
    "setup_repo_cmds": [
        "pip install --no-deps -e ."
    ],
    "startfleet_task_id": "Yzcfw3bKElCf3wWKgQcaC",
    "test_cmds": [
        "pytest -vra -m \"not test_build_sphinx_return_nonzero_status\""
    ],
    "test_coverage": 99.0,
    "test_files": [
        "tests/"
    ],
"repo": "sphinx-doc/sphinx"
}
    </code>
  </pre>
</details>

<details><summary>Issue Description:</summary>
Warning: Inline literal start-string without end-string in Numpy style Parameters section
**Describe the bug**
The following docstring generates a warning on the line of the timeout parameter. Removing the quote around `default` cause the warning to go away.
```python
def lock(
        self,
        timeout: Union[float, Literal["default"]] = "default",
        requested_key: Optional[str] = None,
    ) -> str:
        """Establish a shared lock to the resource.

        Parameters
        ----------
        timeout : Union[float, Literal["default"]], optional
            Absolute time period (in milliseconds) that a resource waits to get
            unlocked by the locking session before returning an error.
            Defaults to "default" which means use self.timeout.
        requested_key : Optional[str], optional
            Access key used by another session with which you want your session
            to share a lock or None to generate a new shared access key.

        Returns
        -------
        str
            A new shared access key if requested_key is None, otherwise, same
            value as the requested_key

        """
```

**To Reproduce**
Steps to reproduce the behavior:
```
$ git clone https://github.com/pyvisa/pyvisa
$ git checkout pytest
$ cd pyvisa
$ pip install -e .
$ cd docs
$ sphinx-build source build -W -b html;
```

**Expected behavior**
I do not expect to see a warning there and was not seeing any before 3.2

**Your project**
The project is build under the Documentation build action. https://github.com/pyvisa/pyvisa/pull/531

**Environment info**
- OS: Mac Os and Linux
- Python version: 3.8.2 and 3.8.5
- Sphinx version: 3.2.0
- Sphinx extensions: "sphinx.ext.autodoc", "sphinx.ext.doctest","sphinx.ext.intersphinx", "sphinx.ext.coverage", "sphinx.ext.viewcode", "sphinx.ext.mathjax",  "sphinx.ext.napoleon"



</details>

'#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile:
#1 transferring dockerfile: 540B 0.4s done
#1 WARN: FromPlatformFlagConstDisallowed: FROM --platform flag should not use constant value "linux/x86_64" (line 1)
#1 DONE 0.4s

#2 [internal] load metadata for us-docker.pkg.dev/xai-research/oci/swe/starfleet/v1/base_py-linux__x86_64-22.04-py311_23.11.0-2-x86_64:v0
#2 DONE 63.4s

#3 [internal] load .dockerignore
#3 transferring context: 0.1s
#3 transferring context: 2B 0.2s done
#3 DONE 0.2s

#4 [1/7] FROM us-docker.pkg.dev/xai-research/oci/swe/starfleet/v1/base_py-linux__x86_64-22.04-py311_23.11.0-2-x86_64:v0@sha256:cad662473c82633f7a7be620190c3c88997b3bec2c9590fef588c3d3d7dfba3b
#4 CACHED

#5 [internal] load build context
#5 transferring context: 1.11kB 0.3s done
#5 DONE 0.3s

#6 [2/7] COPY ./setup_env.sh /root/
#6 DONE 0.0s

#7 [3/7] RUN sed -i -e 's/\r$//' /root/setup_env.sh
#7 DONE 1.3s

#8 [4/7] RUN chmod +x /root/setup_env.sh
#8 DONE 4.0s

#9 [5/7] RUN /bin/bash -c "source ~/.bashrc && /root/setup_env.sh"
#9 1.672 + source /opt/miniconda3/bin/activate
#9 1.672 ++ _CONDA_ROOT=/opt/miniconda3
#9 1.672 ++ . /opt/miniconda3/etc/profile.d/conda.sh
#9 1.672 +++ export CONDA_EXE=/opt/miniconda3/bin/conda
#9 1.672 +++ CONDA_EXE=/opt/miniconda3/bin/conda
#9 1.672 +++ export _CE_M=
#9 1.672 +++ _CE_M=
#9 1.672 +++ export _CE_CONDA=
#9 1.672 +++ _CE_CONDA=
#9 1.672 +++ export CONDA_PYTHON_EXE=/opt/miniconda3/bin/python
#9 1.672 +++ CONDA_PYTHON_EXE=/opt/miniconda3/bin/python
#9 1.672 +++ '[' -z '' ']'
#9 1.672 +++ export CONDA_SHLVL=0
#9 1.672 +++ CONDA_SHLVL=0
#9 1.672 +++ '[' -n '' ']'
#9 1.673 +++++ dirname /opt/miniconda3/bin/conda
#9 1.674 ++++ dirname /opt/miniconda3/bin
#9 1.674 +++ PATH=/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
#9 1.674 +++ export PATH
#9 1.674 +++ '[' -z '' ']'
#9 1.674 +++ PS1=
#9 1.674 ++ conda activate
#9 1.674 ++ local cmd=activate
#9 1.674 ++ case "$cmd" in
#9 1.674 ++ __conda_activate activate
#9 1.674 ++ '[' -n '' ']'
#9 1.674 ++ local ask_conda
#9 1.675 +++ PS1=
#9 1.675 +++ __conda_exe shell.posix activate
#9 1.675 +++ /opt/miniconda3/bin/conda shell.posix activate
#9 1.752 ++ ask_conda='PS1='\''(base) '\''
#9 1.752 export PATH='\''/opt/miniconda3/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'\''
#9 1.752 export CONDA_PREFIX='\''/opt/miniconda3'\''
#9 1.752 export CONDA_SHLVL='\''1'\''
#9 1.752 export CONDA_DEFAULT_ENV='\''base'\''
#9 1.752 export CONDA_PROMPT_MODIFIER='\''(base) '\''
#9 1.752 export CONDA_EXE='\''/opt/miniconda3/bin/conda'\''
#9 1.752 export _CE_M='\'''\''
#9 1.752 export _CE_CONDA='\'''\''
#9 1.752 export CONDA_PYTHON_EXE='\''/opt/miniconda3/bin/python'\'''
#9 1.752 ++ eval 'PS1='\''(base) '\''
#9 1.752 export PATH='\''/opt/miniconda3/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'\''
#9 1.752 export CONDA_PREFIX='\''/opt/miniconda3'\''
#9 1.752 export CONDA_SHLVL='\''1'\''
#9 1.752 export CONDA_DEFAULT_ENV='\''base'\''
#9 1.752 export CONDA_PROMPT_MODIFIER='\''(base) '\''
#9 1.752 export CONDA_EXE='\''/opt/miniconda3/bin/conda'\''
#9 1.752 export _CE_M='\'''\''
#9 1.752 export _CE_CONDA='\'''\''
#9 1.752 export CONDA_PYTHON_EXE='\''/opt/miniconda3/bin/python'\'''
#9 1.752 +++ PS1='(base) '
#9 1.752 +++ export PATH=/opt/miniconda3/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
#9 1.752 +++ PATH=/opt/miniconda3/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
#9 1.752 +++ export CONDA_PREFIX=/opt/miniconda3
#9 1.752 +++ CONDA_PREFIX=/opt/miniconda3
#9 1.752 +++ export CONDA_SHLVL=1
#9 1.752 +++ CONDA_SHLVL=1
#9 1.752 +++ export CONDA_DEFAULT_ENV=base
#9 1.752 +++ CONDA_DEFAULT_ENV=base
#9 1.752 +++ export 'CONDA_PROMPT_MODIFIER=(base) '
#9 1.752 +++ CONDA_PROMPT_MODIFIER='(base) '
#9 1.752 +++ export CONDA_EXE=/opt/miniconda3/bin/conda
#9 1.752 +++ CONDA_EXE=/opt/miniconda3/bin/conda
#9 1.752 +++ export _CE_M=
#9 1.752 +++ _CE_M=
#9 1.752 +++ export _CE_CONDA=
#9 1.752 +++ _CE_CONDA=
#9 1.752 +++ export CONDA_PYTHON_EXE=/opt/miniconda3/bin/python
#9 1.752 +++ CONDA_PYTHON_EXE=/opt/miniconda3/bin/python
#9 1.752 ++ __conda_hashr
#9 1.752 ++ '[' -n '' ']'
#9 1.752 ++ '[' -n '' ']'
#9 1.752 ++ hash -r
#9 1.752 + conda create -n testbed python=3.8.5 -y
#9 1.752 + local cmd=create
#9 1.752 + case "$cmd" in
#9 1.752 + __conda_exe create -n testbed python=3.8.5 -y
#9 1.752 + /opt/miniconda3/bin/conda create -n testbed python=3.8.5 -y
#9 2.158 Channels:
#9 2.158  - defaults
#9 2.158  - conda-forge
#9 2.158 Platform: linux-64
#9 2.158 Collecting package metadata (repodata.json): ...working... done
#9 37.89 Solving environment: ...working... done
#9 40.65 
#9 40.65 ## Package Plan ##
#9 40.65 
#9 40.65   environment location: /opt/miniconda3/envs/testbed
#9 40.65 
#9 40.65   added / updated specs:
#9 40.65     - python=3.8.5
#9 40.65 
#9 40.65 
#9 40.65 The following packages will be downloaded:
#9 40.65 
#9 40.65     package                    |            build
#9 40.65     ---------------------------|-----------------
#9 40.65     ca-certificates-2025.2.25  |       h06a4308_0         129 KB
#9 40.65     ld_impl_linux-64-2.40      |       h12ee557_0         710 KB
#9 40.65     libffi-3.3                 |       he6710b0_2          50 KB
#9 40.65     openssl-1.1.1w             |       h7f8727e_0         3.7 MB
#9 40.65     pip-24.2                   |   py38h06a4308_0         2.2 MB
#9 40.65     python-3.8.5               |       h7579374_1        49.3 MB
#9 40.65     setuptools-75.1.0          |   py38h06a4308_0         1.7 MB
#9 40.65     sqlite-3.45.3              |       h5eee18b_0         1.2 MB
#9 40.65     tk-8.6.14                  |       h39e8969_0         3.4 MB
#9 40.65     wheel-0.44.0               |   py38h06a4308_0         108 KB
#9 40.65     xz-5.6.4                   |       h5eee18b_1         567 KB
#9 40.65     zlib-1.2.13                |       h5eee18b_1         111 KB
#9 40.65     ------------------------------------------------------------
#9 40.65                                            Total:        63.2 MB
#9 40.65 
#9 40.65 The following NEW packages will be INSTALLED:
#9 40.65 
#9 40.65   _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main 
#9 40.65   _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu 
#9 40.65   ca-certificates    pkgs/main/linux-64::ca-certificates-2025.2.25-h06a4308_0 
#9 40.65   ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.40-h12ee557_0 
#9 40.65   libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2 
#9 40.65   libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1 
#9 40.65   libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1 
#9 40.65   libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1 
#9 40.65   ncurses            pkgs/main/linux-64::ncurses-6.4-h6a678d5_0 
#9 40.65   openssl            pkgs/main/linux-64::openssl-1.1.1w-h7f8727e_0 
#9 40.65   pip                pkgs/main/linux-64::pip-24.2-py38h06a4308_0 
#9 40.65   python             pkgs/main/linux-64::python-3.8.5-h7579374_1 
#9 40.65   readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0 
#9 40.65   setuptools         pkgs/main/linux-64::setuptools-75.1.0-py38h06a4308_0 
#9 40.65   sqlite             pkgs/main/linux-64::sqlite-3.45.3-h5eee18b_0 
#9 40.65   tk                 pkgs/main/linux-64::tk-8.6.14-h39e8969_0 
#9 40.65   wheel              pkgs/main/linux-64::wheel-0.44.0-py38h06a4308_0 
#9 40.65   xz                 pkgs/main/linux-64::xz-5.6.4-h5eee18b_1 
#9 40.65   zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_1 
#9 40.65 
#9 40.65 
#9 40.65 
#9 40.65 Downloading and Extracting Packages: ...working... done
#9 40.65 Preparing transaction: ...working... done
#9 40.88 Verifying transaction: ...working... done
#9 41.44 Executing transaction: ...working... done
#9 43.21 #
#9 43.21 # To activate this environment, use
#9 43.21 #
#9 43.21 #     $ conda activate testbed
#9 43.21 #
#9 43.21 # To deactivate an active environment, use
#9 43.21 #
#9 43.21 #     $ conda deactivate
#9 43.21 
#9 43.27 + conda env config vars set -n testbed DO_EPUBCHECK=1
#9 43.27 + local cmd=env
#9 43.27 + case "$cmd" in
#9 43.27 + __conda_exe env config vars set -n testbed DO_EPUBCHECK=1
#9 43.27 + /opt/miniconda3/bin/conda env config vars set -n testbed DO_EPUBCHECK=1
#9 43.66 + conda activate testbed
#9 43.66 + local cmd=activate
#9 43.66 + case "$cmd" in
#9 43.66 + __conda_activate activate testbed
#9 43.66 + '[' -n '' ']'
#9 43.66 + local ask_conda
#9 43.66 ++ PS1='(base) '
#9 43.66 ++ __conda_exe shell.posix activate testbed
#9 43.67 ++ /opt/miniconda3/bin/conda shell.posix activate testbed
#9 43.74 + ask_conda='PS1='\''(testbed) '\''
#9 43.74 export PATH='\''/opt/miniconda3/envs/testbed/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'\''
#9 43.74 export CONDA_PREFIX='\''/opt/miniconda3/envs/testbed'\''
#9 43.74 export CONDA_SHLVL='\''2'\''
#9 43.74 export CONDA_DEFAULT_ENV='\''testbed'\''
#9 43.74 export CONDA_PROMPT_MODIFIER='\''(testbed) '\''
#9 43.74 export DO_EPUBCHECK='\''1'\''
#9 43.74 export CONDA_PREFIX_1='\''/opt/miniconda3'\''
#9 43.74 export CONDA_EXE='\''/opt/miniconda3/bin/conda'\''
#9 43.74 export _CE_M='\'''\''
#9 43.74 export _CE_CONDA='\'''\''
#9 43.74 export CONDA_PYTHON_EXE='\''/opt/miniconda3/bin/python'\'''
#9 43.74 + eval 'PS1='\''(testbed) '\''
#9 43.74 export PATH='\''/opt/miniconda3/envs/testbed/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'\''
#9 43.74 export CONDA_PREFIX='\''/opt/miniconda3/envs/testbed'\''
#9 43.74 export CONDA_SHLVL='\''2'\''
#9 43.74 export CONDA_DEFAULT_ENV='\''testbed'\''
#9 43.74 export CONDA_PROMPT_MODIFIER='\''(testbed) '\''
#9 43.74 export DO_EPUBCHECK='\''1'\''
#9 43.74 export CONDA_PREFIX_1='\''/opt/miniconda3'\''
#9 43.74 export CONDA_EXE='\''/opt/miniconda3/bin/conda'\''
#9 43.74 export _CE_M='\'''\''
#9 43.74 export _CE_CONDA='\'''\''
#9 43.74 export CONDA_PYTHON_EXE='\''/opt/miniconda3/bin/python'\'''
#9 43.74 ++ PS1='(testbed) '
#9 43.74 ++ export PATH=/opt/miniconda3/envs/testbed/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
#9 43.74 ++ PATH=/opt/miniconda3/envs/testbed/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
#9 43.74 ++ export CONDA_PREFIX=/opt/miniconda3/envs/testbed
#9 43.74 ++ CONDA_PREFIX=/opt/miniconda3/envs/testbed
#9 43.74 ++ export CONDA_SHLVL=2
#9 43.74 ++ CONDA_SHLVL=2
#9 43.74 ++ export CONDA_DEFAULT_ENV=testbed
#9 43.74 ++ CONDA_DEFAULT_ENV=testbed
#9 43.74 ++ export 'CONDA_PROMPT_MODIFIER=(testbed) '
#9 43.74 ++ CONDA_PROMPT_MODIFIER='(testbed) '
#9 43.74 ++ export DO_EPUBCHECK=1
#9 43.74 ++ DO_EPUBCHECK=1
#9 43.74 ++ export CONDA_PREFIX_1=/opt/miniconda3
#9 43.74 ++ CONDA_PREFIX_1=/opt/miniconda3
#9 43.74 ++ export CONDA_EXE=/opt/miniconda3/bin/conda
#9 43.74 ++ CONDA_EXE=/opt/miniconda3/bin/conda
#9 43.74 ++ export _CE_M=
#9 43.74 ++ _CE_M=
#9 43.74 ++ export _CE_CONDA=
#9 43.74 ++ _CE_CONDA=
#9 43.74 ++ export CONDA_PYTHON_EXE=/opt/miniconda3/bin/python
#9 43.74 ++ CONDA_PYTHON_EXE=/opt/miniconda3/bin/python
#9 43.74 + __conda_hashr
#9 43.74 + '[' -n '' ']'
#9 43.74 + '[' -n '' ']'
#9 43.74 + hash -r
#9 43.74 + apt-get update
#9 43.83 Get:1 http://security.ubuntu.com/ubuntu jammy-security InRelease [129 kB]
#9 43.83 Get:2 http://archive.ubuntu.com/ubuntu jammy InRelease [270 kB]
#9 44.01 Get:3 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]
#9 44.03 Get:4 http://security.ubuntu.com/ubuntu jammy-security/restricted amd64 Packages [4000 kB]
#9 44.05 Get:5 http://archive.ubuntu.com/ubuntu jammy-backports InRelease [127 kB]
#9 44.10 Get:6 http://archive.ubuntu.com/ubuntu jammy/main amd64 Packages [1792 kB]
#9 44.20 Get:7 http://archive.ubuntu.com/ubuntu jammy/multiverse amd64 Packages [266 kB]
#9 44.20 Get:8 http://archive.ubuntu.com/ubuntu jammy/restricted amd64 Packages [164 kB]
#9 44.21 Get:9 http://archive.ubuntu.com/ubuntu jammy/universe amd64 Packages [17.5 MB]
#9 44.24 Get:10 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [2788 kB]
#9 44.25 Get:11 http://security.ubuntu.com/ubuntu jammy-security/multiverse amd64 Packages [47.7 kB]
#9 44.25 Get:12 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 Packages [1243 kB]
#9 44.40 Get:13 http://archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages [1542 kB]
#9 44.42 Get:14 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [3140 kB]
#9 44.45 Get:15 http://archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [4246 kB]
#9 44.49 Get:16 http://archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 Packages [55.7 kB]
#9 44.49 Get:17 http://archive.ubuntu.com/ubuntu jammy-backports/universe amd64 Packages [35.2 kB]
#9 44.49 Get:18 http://archive.ubuntu.com/ubuntu jammy-backports/main amd64 Packages [82.7 kB]
#9 45.40 Fetched 37.5 MB in 2s (22.9 MB/s)
#9 45.40 Reading package lists...
#9 46.12 + apt-get install dvipng dvisvgm texlive-base texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended texinfo -y
#9 46.14 Reading package lists...
#9 46.92 Building dependency tree...
#9 47.08 Reading state information...
#9 47.22 The following additional packages will be installed:
#9 47.22   dbus fonts-droid-fallback fonts-lato fonts-lmodern fonts-noto-mono
#9 47.22   fonts-texgyre fonts-urw-base35 ghostscript libapache-pom-java libapparmor1
#9 47.22   libauthen-sasl-perl libavahi-client3 libavahi-common-data libavahi-common3
#9 47.22   libcairo2 libclone-perl libcommons-logging-java libcommons-parent-java
#9 47.22   libcups2 libdata-dump-perl libdbus-1-3 libdrm-amdgpu1 libdrm-common
#9 47.22   libdrm-intel1 libdrm-nouveau2 libdrm-radeon1 libdrm2 libelf1
#9 47.22   libencode-locale-perl libfile-basedir-perl libfile-desktopentry-perl
#9 47.22   libfile-listing-perl libfile-mimeinfo-perl libfont-afm-perl libfontbox-java
#9 47.22   libfontenc1 libgl1 libgl1-amber-dri libgl1-mesa-dri libglapi-mesa
#9 47.22   libglib2.0-0 libglib2.0-data libglvnd0 libglx-mesa0 libglx0 libgraphite2-3
#9 47.22   libgs9 libgs9-common libharfbuzz0b libhtml-form-perl libhtml-format-perl
#9 47.22   libhtml-parser-perl libhtml-tagset-perl libhtml-tree-perl
#9 47.22   libhttp-cookies-perl libhttp-daemon-perl libhttp-date-perl
#9 47.22   libhttp-message-perl libhttp-negotiate-perl libice6 libicu70 libidn12
#9 47.22   libijs-0.35 libio-html-perl libio-socket-ssl-perl libio-stringy-perl
#9 47.22   libipc-system-simple-perl libjbig2dec0 libkpathsea6 libllvm15
#9 47.22   liblwp-mediatypes-perl liblwp-protocol-https-perl libmailtools-perl
#9 47.22   libnet-dbus-perl libnet-http-perl libnet-smtp-ssl-perl libnet-ssleay-perl
#9 47.22   libopenjp2-7 libpaper-utils libpaper1 libpciaccess0 libpdfbox-java
#9 47.22   libpixman-1-0 libptexenc1 libruby3.0 libsensors-config libsensors5 libsm6
#9 47.22   libsynctex2 libtcl8.6 libteckit0 libtexlua53 libtexluajit2
#9 47.22   libtext-iconv-perl libtext-unidecode-perl libtie-ixhash-perl
#9 47.22   libtimedate-perl libtk8.6 libtry-tiny-perl liburi-perl libutempter0 libwoff1
#9 47.22   libwww-perl libwww-robotrules-perl libx11-protocol-perl libx11-xcb1 libxaw7
#9 47.22   libxcb-dri2-0 libxcb-dri3-0 libxcb-glx0 libxcb-present0 libxcb-randr0
#9 47.22   libxcb-render0 libxcb-shape0 libxcb-shm0 libxcb-sync1 libxcb-xfixes0
#9 47.22   libxcomposite1 libxcursor1 libxfixes3 libxft2 libxi6 libxinerama1
#9 47.22   libxkbfile1 libxml-libxml-perl libxml-namespacesupport-perl
#9 47.22   libxml-parser-perl libxml-sax-base-perl libxml-sax-expat-perl
#9 47.22   libxml-sax-perl libxml-twig-perl libxml-xpathengine-perl libxml2 libxmu6
#9 47.22   libxrandr2 libxrender1 libxshmfence1 libxss1 libxt6 libxtst6 libxv1
#9 47.22   libxxf86dga1 libxxf86vm1 libyaml-0-2 libzzip-0-13 lmodern
#9 47.22   perl-openssl-defaults poppler-data preview-latex-style rake ruby
#9 47.22   ruby-net-telnet ruby-rubygems ruby-webrick ruby-xmlrpc ruby3.0
#9 47.22   rubygems-integration shared-mime-info t1utils tcl tcl8.6 tex-common tex-gyre
#9 47.22   texlive-binaries texlive-latex-base texlive-pictures texlive-plain-generic
#9 47.22   tipa tk tk8.6 unzip x11-common x11-utils x11-xserver-utils xbitmaps
#9 47.22   xdg-user-dirs xdg-utils xfonts-encodings xfonts-utils xterm zip
#9 47.22 Suggested packages:
#9 47.22   default-dbus-session-bus | dbus-session-bus fonts-noto fonts-freefont-otf
#9 47.22   | fonts-freefont-ttf ghostscript-x libdigest-hmac-perl libgssapi-perl
#9 47.22   libavalon-framework-java libcommons-logging-java-doc
#9 47.22   libexcalibur-logkit-java liblog4j1.2-java cups-common libcrypt-ssleay-perl
#9 47.22   pciutils lm-sensors libsub-name-perl libbusiness-isbn-perl
#9 47.22   libauthen-ntlm-perl libxml-sax-expatxs-perl libunicode-map8-perl
#9 47.22   libunicode-string-perl xml-twig-tools poppler-utils fonts-japanese-mincho
#9 47.22   | fonts-ipafont-mincho fonts-japanese-gothic | fonts-ipafont-gothic
#9 47.22   fonts-arphic-ukai fonts-arphic-uming fonts-nanum ri ruby-dev bundler
#9 47.22   tcl-tclreadline debhelper perl-tk xpdf | pdf-viewer xzdec
#9 47.22   texlive-fonts-recommended-doc texlive-latex-base-doc python3-pygments
#9 47.22   icc-profiles libfile-which-perl libspreadsheet-parseexcel-perl
#9 47.22   texlive-latex-extra-doc texlive-latex-recommended-doc texlive-luatex
#9 47.22   texlive-pstricks dot2tex prerex texlive-pictures-doc vprerex
#9 47.22   default-jre-headless tipa-doc mesa-utils nickle cairo-5c xorg-docs-core
#9 47.22   xfonts-cyrillic
#9 47.49 The following NEW packages will be installed:
#9 47.49   dbus dvipng dvisvgm fonts-droid-fallback fonts-lato fonts-lmodern
#9 47.49   fonts-noto-mono fonts-texgyre fonts-urw-base35 ghostscript
#9 47.49   libapache-pom-java libapparmor1 libauthen-sasl-perl libavahi-client3
#9 47.49   libavahi-common-data libavahi-common3 libcairo2 libclone-perl
#9 47.49   libcommons-logging-java libcommons-parent-java libcups2 libdata-dump-perl
#9 47.49   libdbus-1-3 libdrm-amdgpu1 libdrm-common libdrm-intel1 libdrm-nouveau2
#9 47.49   libdrm-radeon1 libdrm2 libelf1 libencode-locale-perl libfile-basedir-perl
#9 47.49   libfile-desktopentry-perl libfile-listing-perl libfile-mimeinfo-perl
#9 47.49   libfont-afm-perl libfontbox-java libfontenc1 libgl1 libgl1-amber-dri
#9 47.49   libgl1-mesa-dri libglapi-mesa libglib2.0-0 libglib2.0-data libglvnd0
#9 47.49   libglx-mesa0 libglx0 libgraphite2-3 libgs9 libgs9-common libharfbuzz0b
#9 47.49   libhtml-form-perl libhtml-format-perl libhtml-parser-perl
#9 47.49   libhtml-tagset-perl libhtml-tree-perl libhttp-cookies-perl
#9 47.49   libhttp-daemon-perl libhttp-date-perl libhttp-message-perl
#9 47.49   libhttp-negotiate-perl libice6 libicu70 libidn12 libijs-0.35 libio-html-perl
#9 47.49   libio-socket-ssl-perl libio-stringy-perl libipc-system-simple-perl
#9 47.49   libjbig2dec0 libkpathsea6 libllvm15 liblwp-mediatypes-perl
#9 47.49   liblwp-protocol-https-perl libmailtools-perl libnet-dbus-perl
#9 47.49   libnet-http-perl libnet-smtp-ssl-perl libnet-ssleay-perl libopenjp2-7
#9 47.49   libpaper-utils libpaper1 libpciaccess0 libpdfbox-java libpixman-1-0
#9 47.49   libptexenc1 libruby3.0 libsensors-config libsensors5 libsm6 libsynctex2
#9 47.49   libtcl8.6 libteckit0 libtexlua53 libtexluajit2 libtext-iconv-perl
#9 47.49   libtext-unidecode-perl libtie-ixhash-perl libtimedate-perl libtk8.6
#9 47.49   libtry-tiny-perl liburi-perl libutempter0 libwoff1 libwww-perl
#9 47.49   libwww-robotrules-perl libx11-protocol-perl libx11-xcb1 libxaw7
#9 47.49   libxcb-dri2-0 libxcb-dri3-0 libxcb-glx0 libxcb-present0 libxcb-randr0
#9 47.49   libxcb-render0 libxcb-shape0 libxcb-shm0 libxcb-sync1 libxcb-xfixes0
#9 47.49   libxcomposite1 libxcursor1 libxfixes3 libxft2 libxi6 libxinerama1
#9 47.49   libxkbfile1 libxml-libxml-perl libxml-namespacesupport-perl
#9 47.49   libxml-parser-perl libxml-sax-base-perl libxml-sax-expat-perl
#9 47.49   libxml-sax-perl libxml-twig-perl libxml-xpathengine-perl libxml2 libxmu6
#9 47.49   libxrandr2 libxrender1 libxshmfence1 libxss1 libxt6 libxtst6 libxv1
#9 47.49   libxxf86dga1 libxxf86vm1 libyaml-0-2 libzzip-0-13 lmodern
#9 47.49   perl-openssl-defaults poppler-data preview-latex-style rake ruby
#9 47.49   ruby-net-telnet ruby-rubygems ruby-webrick ruby-xmlrpc ruby3.0
#9 47.49   rubygems-integration shared-mime-info t1utils tcl tcl8.6 tex-common tex-gyre
#9 47.49   texinfo texlive-base texlive-binaries texlive-fonts-recommended
#9 47.49   texlive-latex-base texlive-latex-extra texlive-latex-recommended
#9 47.49   texlive-pictures texlive-plain-generic tipa tk tk8.6 unzip x11-common
#9 47.49   x11-utils x11-xserver-utils xbitmaps xdg-user-dirs xdg-utils
#9 47.49   xfonts-encodings xfonts-utils xterm zip
#9 47.61 0 upgraded, 188 newly installed, 0 to remove and 25 not upgraded.
#9 47.61 Need to get 232 MB of archives.
#9 47.61 After this operation, 810 MB of additional disk space will be used.
#9 47.61 Get:1 http://archive.ubuntu.com/ubuntu jammy/main amd64 fonts-droid-fallback all 1:6.0.1r16-1.1build1 [1805 kB]
#9 47.87 Get:2 http://archive.ubuntu.com/ubuntu jammy/main amd64 fonts-lato all 2.0-2.1 [2696 kB]
#9 47.93 Get:3 http://archive.ubuntu.com/ubuntu jammy/main amd64 poppler-data all 0.4.11-1 [2171 kB]
#9 47.95 Get:4 http://archive.ubuntu.com/ubuntu jammy/universe amd64 tex-common all 6.17 [33.7 kB]
#9 47.95 Get:5 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libapparmor1 amd64 3.0.4-2ubuntu2.4 [39.7 kB]
#9 47.95 Get:6 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libdbus-1-3 amd64 1.12.20-2ubuntu4.1 [189 kB]
#9 47.95 Get:7 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 dbus amd64 1.12.20-2ubuntu4.1 [158 kB]
#9 47.95 Get:8 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libelf1 amd64 0.186-1ubuntu0.1 [51.1 kB]
#9 47.95 Get:9 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libglib2.0-0 amd64 2.72.4-0ubuntu2.4 [1465 kB]
#9 47.97 Get:10 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libglib2.0-data all 2.72.4-0ubuntu2.4 [4582 B]
#9 47.97 Get:11 http://archive.ubuntu.com/ubuntu jammy/main amd64 libicu70 amd64 70.1-2 [10.6 MB]
#9 48.09 Get:12 http://archive.ubuntu.com/ubuntu jammy/main amd64 libtext-iconv-perl amd64 1.7-7build3 [14.3 kB]
#9 48.09 Get:13 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libxml2 amd64 2.9.13+dfsg-1ubuntu0.6 [762 kB]
#9 48.10 Get:14 http://archive.ubuntu.com/ubuntu jammy/main amd64 libyaml-0-2 amd64 0.2.2-1build2 [51.6 kB]
#9 48.10 Get:15 http://archive.ubuntu.com/ubuntu jammy/main amd64 shared-mime-info amd64 2.1-2 [454 kB]
#9 48.10 Get:16 http://archive.ubuntu.com/ubuntu jammy/main amd64 xdg-user-dirs amd64 0.17-2ubuntu4 [53.9 kB]
#9 48.10 Get:17 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libdrm-common all 2.4.113-2~ubuntu0.22.04.1 [5450 B]
#9 48.10 Get:18 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libdrm2 amd64 2.4.113-2~ubuntu0.22.04.1 [38.1 kB]
#9 48.10 Get:19 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libkpathsea6 amd64 2021.20210626.59705-1ubuntu0.2 [60.4 kB]
#9 48.10 Get:20 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libptexenc1 amd64 2021.20210626.59705-1ubuntu0.2 [39.1 kB]
#9 48.12 Get:21 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libsynctex2 amd64 2021.20210626.59705-1ubuntu0.2 [55.6 kB]
#9 48.15 Get:22 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libtexlua53 amd64 2021.20210626.59705-1ubuntu0.2 [120 kB]
#9 48.16 Get:23 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libtexluajit2 amd64 2021.20210626.59705-1ubuntu0.2 [267 kB]
#9 48.16 Get:24 http://archive.ubuntu.com/ubuntu jammy/main amd64 t1utils amd64 1.41-4build2 [61.3 kB]
#9 48.16 Get:25 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libpixman-1-0 amd64 0.40.0-1ubuntu0.22.04.1 [264 kB]
#9 48.16 Get:26 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-render0 amd64 1.14-3ubuntu3 [16.4 kB]
#9 48.16 Get:27 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-shm0 amd64 1.14-3ubuntu3 [5780 B]
#9 48.16 Get:28 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxrender1 amd64 1:0.9.10-1build4 [19.7 kB]
#9 48.16 Get:29 http://archive.ubuntu.com/ubuntu jammy/main amd64 libcairo2 amd64 1.16.0-5ubuntu2 [628 kB]
#9 48.17 Get:30 http://archive.ubuntu.com/ubuntu jammy/main amd64 libgraphite2-3 amd64 1.3.14-1build2 [71.3 kB]
#9 48.19 Get:31 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libharfbuzz0b amd64 2.7.4-1ubuntu3.2 [353 kB]
#9 48.22 Get:32 http://archive.ubuntu.com/ubuntu jammy/main amd64 libpaper1 amd64 1.1.28build2 [13.8 kB]
#9 48.22 Get:33 http://archive.ubuntu.com/ubuntu jammy/universe amd64 libteckit0 amd64 2.5.11+ds1-1 [421 kB]
#9 48.23 Get:34 http://archive.ubuntu.com/ubuntu jammy/main amd64 x11-common all 1:7.7+23ubuntu2 [23.4 kB]
#9 48.23 Get:35 http://archive.ubuntu.com/ubuntu jammy/main amd64 libice6 amd64 2:1.0.10-1build2 [42.6 kB]
#9 48.23 Get:36 http://archive.ubuntu.com/ubuntu jammy/main amd64 libsm6 amd64 2:1.2.3-1build2 [16.7 kB]
#9 48.23 Get:37 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxt6 amd64 1:1.2.1-1 [177 kB]
#9 48.23 Get:38 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxmu6 amd64 2:1.1.3-3 [49.6 kB]
#9 48.23 Get:39 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxaw7 amd64 2:1.0.14-1 [191 kB]
#9 48.23 Get:40 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxi6 amd64 2:1.8-1build1 [32.6 kB]
#9 48.26 Get:41 http://archive.ubuntu.com/ubuntu jammy/universe amd64 libzzip-0-13 amd64 0.13.72+dfsg.1-1.1 [27.0 kB]
#9 48.29 Get:42 http://archive.ubuntu.com/ubuntu jammy-updates/universe amd64 texlive-binaries amd64 2021.20210626.59705-1ubuntu0.2 [9860 kB]
#9 48.41 Get:43 http://archive.ubuntu.com/ubuntu jammy/main amd64 fonts-urw-base35 all 20200910-1 [6367 kB]
#9 48.47 Get:44 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libgs9-common all 9.55.0~dfsg1-0ubuntu5.11 [753 kB]
#9 48.48 Get:45 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libavahi-common-data amd64 0.8-5ubuntu5.2 [23.8 kB]
#9 48.48 Get:46 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libavahi-common3 amd64 0.8-5ubuntu5.2 [23.9 kB]
#9 48.48 Get:47 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libavahi-client3 amd64 0.8-5ubuntu5.2 [28.0 kB]
#9 48.48 Get:48 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libcups2 amd64 2.4.1op1-1ubuntu4.11 [263 kB]
#9 48.48 Get:49 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libidn12 amd64 1.38-4ubuntu1 [60.0 kB]
#9 48.48 Get:50 http://archive.ubuntu.com/ubuntu jammy/main amd64 libijs-0.35 amd64 0.35-15build2 [16.5 kB]
#9 48.48 Get:51 http://archive.ubuntu.com/ubuntu jammy/main amd64 libjbig2dec0 amd64 0.19-3build2 [64.7 kB]
#9 48.48 Get:52 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libopenjp2-7 amd64 2.4.0-6ubuntu0.3 [158 kB]
#9 48.51 Get:53 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libgs9 amd64 9.55.0~dfsg1-0ubuntu5.11 [5031 kB]
#9 48.56 Get:54 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 ghostscript amd64 9.55.0~dfsg1-0ubuntu5.11 [49.4 kB]
#9 48.56 Get:55 http://archive.ubuntu.com/ubuntu jammy/universe amd64 dvipng amd64 1.15-1.1 [78.9 kB]
#9 48.56 Get:56 http://archive.ubuntu.com/ubuntu jammy/main amd64 libwoff1 amd64 1.0.2-1build4 [45.2 kB]
#9 48.56 Get:57 http://archive.ubuntu.com/ubuntu jammy/universe amd64 dvisvgm amd64 2.13.1-1 [1221 kB]
#9 48.58 Get:58 http://archive.ubuntu.com/ubuntu jammy/universe amd64 fonts-lmodern all 2.004.5-6.1 [4532 kB]
#9 48.63 Get:59 http://archive.ubuntu.com/ubuntu jammy/main amd64 fonts-noto-mono all 20201225-1build1 [397 kB]
#9 48.63 Get:60 http://archive.ubuntu.com/ubuntu jammy/universe amd64 fonts-texgyre all 20180621-3.1 [10.2 MB]
#9 48.74 Get:61 http://archive.ubuntu.com/ubuntu jammy/universe amd64 libapache-pom-java all 18-1 [4720 B]
#9 48.74 Get:62 http://archive.ubuntu.com/ubuntu jammy/main amd64 libclone-perl amd64 0.45-1build3 [11.0 kB]
#9 48.74 Get:63 http://archive.ubuntu.com/ubuntu jammy/universe amd64 libcommons-parent-java all 43-1 [10.8 kB]
#9 48.74 Get:64 http://archive.ubuntu.com/ubuntu jammy/universe amd64 libcommons-logging-java all 1.2-2 [60.3 kB]
#9 48.74 Get:65 http://archive.ubuntu.com/ubuntu jammy/main amd64 libdata-dump-perl all 1.25-1 [25.9 kB]
#9 48.74 Get:66 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libdrm-amdgpu1 amd64 2.4.113-2~ubuntu0.22.04.1 [19.9 kB]
#9 48.74 Get:67 http://archive.ubuntu.com/ubuntu jammy/main amd64 libpciaccess0 amd64 0.16-3 [19.1 kB]
#9 48.75 Get:68 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libdrm-intel1 amd64 2.4.113-2~ubuntu0.22.04.1 [66.7 kB]
#9 48.75 Get:69 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libdrm-nouveau2 amd64 2.4.113-2~ubuntu0.22.04.1 [17.5 kB]
#9 48.78 Get:70 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libdrm-radeon1 amd64 2.4.113-2~ubuntu0.22.04.1 [21.6 kB]
#9 48.78 Get:71 http://archive.ubuntu.com/ubuntu jammy/main amd64 libencode-locale-perl all 1.05-1.1 [11.8 kB]
#9 48.78 Get:72 http://archive.ubuntu.com/ubuntu jammy/main amd64 libipc-system-simple-perl all 1.30-1 [23.2 kB]
#9 48.81 Get:73 http://archive.ubuntu.com/ubuntu jammy/main amd64 libfile-basedir-perl all 0.09-1 [15.7 kB]
#9 48.81 Get:74 http://archive.ubuntu.com/ubuntu jammy/main amd64 liburi-perl all 5.10-1 [78.8 kB]
#9 48.81 Get:75 http://archive.ubuntu.com/ubuntu jammy/main amd64 libfile-desktopentry-perl all 0.22-2 [17.8 kB]
#9 48.81 Get:76 http://archive.ubuntu.com/ubuntu jammy/main amd64 libtimedate-perl all 2.3300-2 [34.0 kB]
#9 48.81 Get:77 http://archive.ubuntu.com/ubuntu jammy/main amd64 libhttp-date-perl all 6.05-1 [9920 B]
#9 48.81 Get:78 http://archive.ubuntu.com/ubuntu jammy/main amd64 libfile-listing-perl all 6.14-1 [11.2 kB]
#9 48.81 Get:79 http://archive.ubuntu.com/ubuntu jammy/main amd64 libfile-mimeinfo-perl all 0.31-1 [43.5 kB]
#9 48.84 Get:80 http://archive.ubuntu.com/ubuntu jammy/main amd64 libfont-afm-perl all 1.20-3 [13.6 kB]
#9 48.84 Get:81 http://archive.ubuntu.com/ubuntu jammy/main amd64 libfontenc1 amd64 1:1.1.4-1build3 [14.7 kB]
#9 48.85 Get:82 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libglapi-mesa amd64 23.2.1-1ubuntu3.1~22.04.3 [35.4 kB]
#9 48.88 Get:83 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libgl1-amber-dri amd64 21.3.9-0ubuntu1~22.04.1 [4218 kB]
#9 48.92 Get:84 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libllvm15 amd64 1:15.0.7-0ubuntu0.22.04.3 [25.4 MB]
#9 49.20 Get:85 http://archive.ubuntu.com/ubuntu jammy/main amd64 libsensors-config all 1:3.6.0-7ubuntu1 [5274 B]
#9 49.20 Get:86 http://archive.ubuntu.com/ubuntu jammy/main amd64 libsensors5 amd64 1:3.6.0-7ubuntu1 [26.3 kB]
#9 49.20 Get:87 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-dri3-0 amd64 1.14-3ubuntu3 [6968 B]
#9 49.20 Get:88 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libgl1-mesa-dri amd64 23.2.1-1ubuntu3.1~22.04.3 [8860 kB]
#9 49.30 Get:89 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libx11-xcb1 amd64 2:1.7.5-1ubuntu0.3 [7802 B]
#9 49.30 Get:90 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-dri2-0 amd64 1.14-3ubuntu3 [7206 B]
#9 49.30 Get:91 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-glx0 amd64 1.14-3ubuntu3 [25.9 kB]
#9 49.30 Get:92 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-present0 amd64 1.14-3ubuntu3 [5734 B]
#9 49.30 Get:93 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-randr0 amd64 1.14-3ubuntu3 [18.3 kB]
#9 49.30 Get:94 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-sync1 amd64 1.14-3ubuntu3 [9416 B]
#9 49.30 Get:95 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-xfixes0 amd64 1.14-3ubuntu3 [9996 B]
#9 49.30 Get:96 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxfixes3 amd64 1:6.0.0-1 [11.7 kB]
#9 49.30 Get:97 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxshmfence1 amd64 1.3-1build4 [5394 B]
#9 49.33 Get:98 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxxf86vm1 amd64 1:1.1.4-1build3 [10.4 kB]
#9 49.33 Get:99 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libglx-mesa0 amd64 23.2.1-1ubuntu3.1~22.04.3 [158 kB]
#9 49.37 Get:100 http://archive.ubuntu.com/ubuntu jammy/main amd64 libhtml-tagset-perl all 3.20-4 [12.5 kB]
#9 49.37 Get:101 http://archive.ubuntu.com/ubuntu jammy/main amd64 libhtml-parser-perl amd64 3.76-1build2 [88.4 kB]
#9 49.49 Get:102 http://archive.ubuntu.com/ubuntu jammy/main amd64 libio-html-perl all 1.004-2 [15.4 kB]
#9 49.62 Get:103 http://archive.ubuntu.com/ubuntu jammy/main amd64 liblwp-mediatypes-perl all 6.04-1 [19.5 kB]
#9 49.65 Get:104 http://archive.ubuntu.com/ubuntu jammy/main amd64 libhttp-message-perl all 6.36-1 [76.8 kB]
#9 49.77 Get:105 http://archive.ubuntu.com/ubuntu jammy/main amd64 libhtml-form-perl all 6.07-1 [22.2 kB]
#9 49.78 Get:106 http://archive.ubuntu.com/ubuntu jammy/main amd64 libhtml-tree-perl all 5.07-2 [200 kB]
#9 49.87 Get:107 http://archive.ubuntu.com/ubuntu jammy/main amd64 libhtml-format-perl all 2.12-1.1 [41.3 kB]
#9 49.91 Get:108 http://archive.ubuntu.com/ubuntu jammy/main amd64 libhttp-cookies-perl all 6.10-1 [18.4 kB]
#9 49.91 Get:109 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libhttp-daemon-perl all 6.13-1ubuntu0.1 [22.9 kB]
#9 49.91 Get:110 http://archive.ubuntu.com/ubuntu jammy/main amd64 libhttp-negotiate-perl all 6.01-1 [12.5 kB]
#9 49.91 Get:111 http://archive.ubuntu.com/ubuntu jammy/main amd64 perl-openssl-defaults amd64 5build2 [7542 B]
#9 49.91 Get:112 http://archive.ubuntu.com/ubuntu jammy/main amd64 libnet-ssleay-perl amd64 1.92-1build2 [327 kB]
#9 49.97 Get:113 http://archive.ubuntu.com/ubuntu jammy/main amd64 libio-socket-ssl-perl all 2.074-2 [192 kB]
#9 49.99 Get:114 http://archive.ubuntu.com/ubuntu jammy/main amd64 libio-stringy-perl all 2.111-3 [55.8 kB]
#9 49.99 Get:115 http://archive.ubuntu.com/ubuntu jammy/main amd64 libnet-http-perl all 6.22-1 [23.2 kB]
#9 49.99 Get:116 http://archive.ubuntu.com/ubuntu jammy/main amd64 libtry-tiny-perl all 0.31-1 [21.8 kB]
#9 50.03 Get:117 http://archive.ubuntu.com/ubuntu jammy/main amd64 libwww-robotrules-perl all 6.02-1 [12.6 kB]
#9 50.03 Get:118 http://archive.ubuntu.com/ubuntu jammy/main amd64 libwww-perl all 6.61-1 [141 kB]
#9 50.04 Get:119 http://archive.ubuntu.com/ubuntu jammy/main amd64 liblwp-protocol-https-perl all 6.10-1 [10.9 kB]
#9 50.04 Get:120 http://archive.ubuntu.com/ubuntu jammy/main amd64 libnet-smtp-ssl-perl all 1.04-1 [5948 B]
#9 50.04 Get:121 http://archive.ubuntu.com/ubuntu jammy/main amd64 libmailtools-perl all 2.21-1 [80.7 kB]
#9 50.05 Get:122 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxml-parser-perl amd64 2.46-3build1 [212 kB]
#9 50.10 Get:123 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxml-twig-perl all 1:3.52-1 [157 kB]
#9 50.11 Get:124 http://archive.ubuntu.com/ubuntu jammy/main amd64 libnet-dbus-perl amd64 1.2.0-1build3 [181 kB]
#9 50.11 Get:125 http://archive.ubuntu.com/ubuntu jammy/main amd64 libpaper-utils amd64 1.1.28build2 [8674 B]
#9 50.11 Get:126 http://archive.ubuntu.com/ubuntu jammy/main amd64 rubygems-integration all 1.18 [5336 B]
#9 50.16 Get:127 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 ruby3.0 amd64 3.0.2-7ubuntu2.10 [50.1 kB]
#9 50.16 Get:128 http://archive.ubuntu.com/ubuntu jammy/main amd64 ruby-rubygems all 3.3.5-2 [228 kB]
#9 50.17 Get:129 http://archive.ubuntu.com/ubuntu jammy/main amd64 ruby amd64 1:3.0~exp1 [5100 B]
#9 50.17 Get:130 http://archive.ubuntu.com/ubuntu jammy/main amd64 rake all 13.0.6-2 [61.7 kB]
#9 50.18 Get:131 http://archive.ubuntu.com/ubuntu jammy/main amd64 ruby-net-telnet all 0.1.1-2 [12.6 kB]
#9 50.18 Get:132 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 ruby-webrick all 1.7.0-3ubuntu0.1 [52.1 kB]
#9 50.22 Get:133 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 ruby-xmlrpc all 0.3.2-1ubuntu0.1 [24.9 kB]
#9 50.22 Get:134 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libruby3.0 amd64 3.0.2-7ubuntu2.10 [5114 kB]
#9 50.39 Get:135 http://archive.ubuntu.com/ubuntu jammy/main amd64 libtcl8.6 amd64 8.6.12+dfsg-1build1 [990 kB]
#9 50.42 Get:136 http://archive.ubuntu.com/ubuntu jammy/universe amd64 libtext-unidecode-perl all 1.30-1 [99.0 kB]
#9 50.42 Get:137 http://archive.ubuntu.com/ubuntu jammy/main amd64 libtie-ixhash-perl all 1.23-2.1 [11.3 kB]
#9 50.42 Get:138 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxft2 amd64 2.3.4-1 [41.8 kB]
#9 50.42 Get:139 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxss1 amd64 1:1.2.3-1build2 [8476 B]
#9 50.42 Get:140 http://archive.ubuntu.com/ubuntu jammy/main amd64 libtk8.6 amd64 8.6.12-1build1 [784 kB]
#9 50.43 Get:141 http://archive.ubuntu.com/ubuntu jammy/main amd64 libutempter0 amd64 1.2.1-2build2 [8848 B]
#9 50.43 Get:142 http://archive.ubuntu.com/ubuntu jammy/main amd64 libx11-protocol-perl all 0.56-7.1 [138 kB]
#9 50.43 Get:143 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-shape0 amd64 1.14-3ubuntu3 [6158 B]
#9 50.45 Get:144 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcomposite1 amd64 1:0.4.5-1build2 [7192 B]
#9 50.50 Get:145 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxcursor1 amd64 1:1.2.0-2build4 [20.9 kB]
#9 50.50 Get:146 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxinerama1 amd64 2:1.1.4-3 [7382 B]
#9 50.50 Get:147 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxkbfile1 amd64 1:1.1.0-1build3 [71.8 kB]
#9 50.50 Get:148 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxml-namespacesupport-perl all 1.12-1.1 [13.2 kB]
#9 50.50 Get:149 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxml-sax-base-perl all 1.09-1.1 [19.0 kB]
#9 50.50 Get:150 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxml-sax-perl all 1.02+dfsg-3 [57.0 kB]
#9 50.50 Get:151 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxml-libxml-perl amd64 2.0207+dfsg+really+2.0134-1 [325 kB]
#9 50.52 Get:152 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxml-sax-expat-perl all 0.51-1 [10.5 kB]
#9 50.52 Get:153 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxml-xpathengine-perl all 0.14-1 [31.8 kB]
#9 50.58 Get:154 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxrandr2 amd64 2:1.5.2-1build1 [20.4 kB]
#9 50.58 Get:155 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxtst6 amd64 2:1.2.3-1build4 [13.4 kB]
#9 50.58 Get:156 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxv1 amd64 2:1.0.11-1build2 [11.2 kB]
#9 50.58 Get:157 http://archive.ubuntu.com/ubuntu jammy/main amd64 libxxf86dga1 amd64 2:1.1.5-0ubuntu3 [12.6 kB]
#9 50.58 Get:158 http://archive.ubuntu.com/ubuntu jammy/main amd64 xfonts-encodings all 1:1.0.5-0ubuntu2 [578 kB]
#9 50.58 Get:159 http://archive.ubuntu.com/ubuntu jammy/main amd64 xfonts-utils amd64 1:7.7+6build2 [94.6 kB]
#9 50.58 Get:160 http://archive.ubuntu.com/ubuntu jammy/universe amd64 lmodern all 2.004.5-6.1 [9471 kB]
#9 50.78 Get:161 http://archive.ubuntu.com/ubuntu jammy/universe amd64 preview-latex-style all 12.2-1ubuntu1 [185 kB]
#9 50.83 Get:162 http://archive.ubuntu.com/ubuntu jammy/main amd64 tcl8.6 amd64 8.6.12+dfsg-1build1 [15.0 kB]
#9 50.83 Get:163 http://archive.ubuntu.com/ubuntu jammy/main amd64 tcl amd64 8.6.11+1build2 [4678 B]
#9 50.83 Get:164 http://archive.ubuntu.com/ubuntu jammy/universe amd64 tex-gyre all 20180621-3.1 [6209 kB]
#9 50.95 Get:165 http://archive.ubuntu.com/ubuntu jammy/universe amd64 texinfo amd64 6.8-4build1 [1423 kB]
#9 50.98 Get:166 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 xdg-utils all 1.1.3-4.1ubuntu3~22.04.1 [61.9 kB]
#9 50.98 Get:167 http://archive.ubuntu.com/ubuntu jammy/universe amd64 texlive-base all 2021.20220204-1 [21.0 MB]
#9 51.42 Get:168 http://archive.ubuntu.com/ubuntu jammy/universe amd64 texlive-fonts-recommended all 2021.20220204-1 [4972 kB]
#9 51.51 Get:169 http://archive.ubuntu.com/ubuntu jammy/universe amd64 texlive-latex-base all 2021.20220204-1 [1128 kB]
#9 51.54 Get:170 http://archive.ubuntu.com/ubuntu jammy/universe amd64 libfontbox-java all 1:1.8.16-2 [207 kB]
#9 51.54 Get:171 http://archive.ubuntu.com/ubuntu jammy/universe amd64 libpdfbox-java all 1:1.8.16-2 [5199 kB]
#9 51.65 Get:172 http://archive.ubuntu.com/ubuntu jammy/universe amd64 texlive-latex-recommended all 2021.20220204-1 [14.4 MB]
#9 51.94 Get:173 http://archive.ubuntu.com/ubuntu jammy/universe amd64 texlive-pictures all 2021.20220204-1 [8720 kB]
#9 52.12 Get:174 http://archive.ubuntu.com/ubuntu jammy/universe amd64 texlive-latex-extra all 2021.20220204-1 [13.9 MB]
#9 52.40 Get:175 http://archive.ubuntu.com/ubuntu jammy/universe amd64 texlive-plain-generic all 2021.20220204-1 [27.5 MB]
#9 52.96 Get:176 http://archive.ubuntu.com/ubuntu jammy/universe amd64 tipa all 2:1.3-21 [2967 kB]
#9 53.02 Get:177 http://archive.ubuntu.com/ubuntu jammy/main amd64 tk8.6 amd64 8.6.12-1build1 [12.8 kB]
#9 53.02 Get:178 http://archive.ubuntu.com/ubuntu jammy/main amd64 tk amd64 8.6.11+1build2 [3058 B]
#9 53.02 Get:179 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 unzip amd64 6.0-26ubuntu3.2 [175 kB]
#9 53.02 Get:180 http://archive.ubuntu.com/ubuntu jammy/main amd64 libglvnd0 amd64 1.4.0-1 [73.6 kB]
#9 53.02 Get:181 http://archive.ubuntu.com/ubuntu jammy/main amd64 libglx0 amd64 1.4.0-1 [41.0 kB]
#9 53.03 Get:182 http://archive.ubuntu.com/ubuntu jammy/main amd64 libgl1 amd64 1.4.0-1 [110 kB]
#9 53.03 Get:183 http://archive.ubuntu.com/ubuntu jammy/main amd64 x11-utils amd64 7.7+5build2 [206 kB]
#9 53.03 Get:184 http://archive.ubuntu.com/ubuntu jammy/main amd64 x11-xserver-utils amd64 7.7+9build1 [170 kB]
#9 53.03 Get:185 http://archive.ubuntu.com/ubuntu jammy/main amd64 xbitmaps all 1.1.1-2.1ubuntu1 [23.4 kB]
#9 53.09 Get:186 http://archive.ubuntu.com/ubuntu jammy/universe amd64 xterm amd64 372-1ubuntu1 [857 kB]
#9 53.10 Get:187 http://archive.ubuntu.com/ubuntu jammy/main amd64 zip amd64 3.0-12build2 [176 kB]
#9 53.10 Get:188 http://archive.ubuntu.com/ubuntu jammy/main amd64 libauthen-sasl-perl all 2.1600-1.1 [43.1 kB]
#9 53.22 debconf: delaying package configuration, since apt-utils is not installed
#9 53.24 Fetched 232 MB in 6s (41.5 MB/s)
#9 53.25 Selecting previously unselected package fonts-droid-fallback.
#9 53.25 (Reading database ... 
(Reading database ... 5%
(Reading database ... 10%
(Reading database ... 15%
(Reading database ... 20%
(Reading database ... 25%
(Reading database ... 30%
(Reading database ... 35%
(Reading database ... 40%
(Reading database ... 45%
(Reading database ... 50%
(Reading database ... 55%
(Reading database ... 60%
(Reading database ... 65%
(Reading database ... 70%
(Reading database ... 75%
(Reading database ... 80%
(Reading database ... 85%
(Reading database ... 90%
(Reading database ... 95%
(Reading database ... 100%
(Reading database ... 27018 files and directories currently installed.)
#9 53.26 Preparing to unpack .../000-fonts-droid-fallback_1%3a6.0.1r16-1.1build1_all.deb ...
#9 53.27 Unpacking fonts-droid-fallback (1:6.0.1r16-1.1build1) ...
#9 53.39 Selecting previously unselected package fonts-lato.
#9 53.40 Preparing to unpack .../001-fonts-lato_2.0-2.1_all.deb ...
#9 53.40 Unpacking fonts-lato (2.0-2.1) ...
#9 53.59 Selecting previously unselected package poppler-data.
#9 53.59 Preparing to unpack .../002-poppler-data_0.4.11-1_all.deb ...
#9 53.60 Unpacking poppler-data (0.4.11-1) ...
#9 53.67 Selecting previously unselected package tex-common.
#9 53.67 Preparing to unpack .../003-tex-common_6.17_all.deb ...
#9 53.67 Unpacking tex-common (6.17) ...
#9 53.68 Selecting previously unselected package libapparmor1:amd64.
#9 53.69 Preparing to unpack .../004-libapparmor1_3.0.4-2ubuntu2.4_amd64.deb ...
#9 53.69 Unpacking libapparmor1:amd64 (3.0.4-2ubuntu2.4) ...
#9 53.70 Selecting previously unselected package libdbus-1-3:amd64.
#9 53.70 Preparing to unpack .../005-libdbus-1-3_1.12.20-2ubuntu4.1_amd64.deb ...
#9 53.70 Unpacking libdbus-1-3:amd64 (1.12.20-2ubuntu4.1) ...
#9 53.71 Selecting previously unselected package dbus.
#9 53.71 Preparing to unpack .../006-dbus_1.12.20-2ubuntu4.1_amd64.deb ...
#9 53.72 Unpacking dbus (1.12.20-2ubuntu4.1) ...
#9 53.73 Selecting previously unselected package libelf1:amd64.
#9 53.73 Preparing to unpack .../007-libelf1_0.186-1ubuntu0.1_amd64.deb ...
#9 53.73 Unpacking libelf1:amd64 (0.186-1ubuntu0.1) ...
#9 53.74 Selecting previously unselected package libglib2.0-0:amd64.
#9 53.75 Preparing to unpack .../008-libglib2.0-0_2.72.4-0ubuntu2.4_amd64.deb ...
#9 53.75 Unpacking libglib2.0-0:amd64 (2.72.4-0ubuntu2.4) ...
#9 53.77 Selecting previously unselected package libglib2.0-data.
#9 53.77 Preparing to unpack .../009-libglib2.0-data_2.72.4-0ubuntu2.4_all.deb ...
#9 53.77 Unpacking libglib2.0-data (2.72.4-0ubuntu2.4) ...
#9 53.78 Selecting previously unselected package libicu70:amd64.
#9 53.78 Preparing to unpack .../010-libicu70_70.1-2_amd64.deb ...
#9 53.78 Unpacking libicu70:amd64 (70.1-2) ...
#9 53.89 Selecting previously unselected package libtext-iconv-perl.
#9 53.89 Preparing to unpack .../011-libtext-iconv-perl_1.7-7build3_amd64.deb ...
#9 53.89 Unpacking libtext-iconv-perl (1.7-7build3) ...
#9 53.90 Selecting previously unselected package libxml2:amd64.
#9 53.90 Preparing to unpack .../012-libxml2_2.9.13+dfsg-1ubuntu0.6_amd64.deb ...
#9 53.90 Unpacking libxml2:amd64 (2.9.13+dfsg-1ubuntu0.6) ...
#9 53.92 Selecting previously unselected package libyaml-0-2:amd64.
#9 53.92 Preparing to unpack .../013-libyaml-0-2_0.2.2-1build2_amd64.deb ...
#9 53.92 Unpacking libyaml-0-2:amd64 (0.2.2-1build2) ...
#9 53.93 Selecting previously unselected package shared-mime-info.
#9 53.93 Preparing to unpack .../014-shared-mime-info_2.1-2_amd64.deb ...
#9 53.93 Unpacking shared-mime-info (2.1-2) ...
#9 53.95 Selecting previously unselected package xdg-user-dirs.
#9 53.95 Preparing to unpack .../015-xdg-user-dirs_0.17-2ubuntu4_amd64.deb ...
#9 53.96 Unpacking xdg-user-dirs (0.17-2ubuntu4) ...
#9 53.98 Selecting previously unselected package libdrm-common.
#9 53.98 Preparing to unpack .../016-libdrm-common_2.4.113-2~ubuntu0.22.04.1_all.deb ...
#9 53.98 Unpacking libdrm-common (2.4.113-2~ubuntu0.22.04.1) ...
#9 53.99 Selecting previously unselected package libdrm2:amd64.
#9 53.99 Preparing to unpack .../017-libdrm2_2.4.113-2~ubuntu0.22.04.1_amd64.deb ...
#9 53.99 Unpacking libdrm2:amd64 (2.4.113-2~ubuntu0.22.04.1) ...
#9 54.00 Selecting previously unselected package libkpathsea6:amd64.
#9 54.00 Preparing to unpack .../018-libkpathsea6_2021.20210626.59705-1ubuntu0.2_amd64.deb ...
#9 54.01 Unpacking libkpathsea6:amd64 (2021.20210626.59705-1ubuntu0.2) ...
#9 54.02 Selecting previously unselected package libptexenc1:amd64.
#9 54.02 Preparing to unpack .../019-libptexenc1_2021.20210626.59705-1ubuntu0.2_amd64.deb ...
#9 54.02 Unpacking libptexenc1:amd64 (2021.20210626.59705-1ubuntu0.2) ...
#9 54.03 Selecting previously unselected package libsynctex2:amd64.
#9 54.03 Preparing to unpack .../020-libsynctex2_2021.20210626.59705-1ubuntu0.2_amd64.deb ...
#9 54.03 Unpacking libsynctex2:amd64 (2021.20210626.59705-1ubuntu0.2) ...
#9 54.04 Selecting previously unselected package libtexlua53:amd64.
#9 54.04 Preparing to unpack .../021-libtexlua53_2021.20210626.59705-1ubuntu0.2_amd64.deb ...
#9 54.04 Unpacking libtexlua53:amd64 (2021.20210626.59705-1ubuntu0.2) ...
#9 54.05 Selecting previously unselected package libtexluajit2:amd64.
#9 54.05 Preparing to unpack .../022-libtexluajit2_2021.20210626.59705-1ubuntu0.2_amd64.deb ...
#9 54.05 Unpacking libtexluajit2:amd64 (2021.20210626.59705-1ubuntu0.2) ...
#9 54.06 Selecting previously unselected package t1utils.
#9 54.07 Preparing to unpack .../023-t1utils_1.41-4build2_amd64.deb ...
#9 54.07 Unpacking t1utils (1.41-4build2) ...
#9 54.07 Selecting previously unselected package libpixman-1-0:amd64.
#9 54.08 Preparing to unpack .../024-libpixman-1-0_0.40.0-1ubuntu0.22.04.1_amd64.deb ...
#9 54.08 Unpacking libpixman-1-0:amd64 (0.40.0-1ubuntu0.22.04.1) ...
#9 54.09 Selecting previously unselected package libxcb-render0:amd64.
#9 54.09 Preparing to unpack .../025-libxcb-render0_1.14-3ubuntu3_amd64.deb ...
#9 54.09 Unpacking libxcb-render0:amd64 (1.14-3ubuntu3) ...
#9 54.10 Selecting previously unselected package libxcb-shm0:amd64.
#9 54.10 Preparing to unpack .../026-libxcb-shm0_1.14-3ubuntu3_amd64.deb ...
#9 54.10 Unpacking libxcb-shm0:amd64 (1.14-3ubuntu3) ...
#9 54.11 Selecting previously unselected package libxrender1:amd64.
#9 54.11 Preparing to unpack .../027-libxrender1_1%3a0.9.10-1build4_amd64.deb ...
#9 54.11 Unpacking libxrender1:amd64 (1:0.9.10-1build4) ...
#9 54.12 Selecting previously unselected package libcairo2:amd64.
#9 54.12 Preparing to unpack .../028-libcairo2_1.16.0-5ubuntu2_amd64.deb ...
#9 54.12 Unpacking libcairo2:amd64 (1.16.0-5ubuntu2) ...
#9 54.14 Selecting previously unselected package libgraphite2-3:amd64.
#9 54.14 Preparing to unpack .../029-libgraphite2-3_1.3.14-1build2_amd64.deb ...
#9 54.14 Unpacking libgraphite2-3:amd64 (1.3.14-1build2) ...
#9 54.15 Selecting previously unselected package libharfbuzz0b:amd64.
#9 54.15 Preparing to unpack .../030-libharfbuzz0b_2.7.4-1ubuntu3.2_amd64.deb ...
#9 54.15 Unpacking libharfbuzz0b:amd64 (2.7.4-1ubuntu3.2) ...
#9 54.16 Selecting previously unselected package libpaper1:amd64.
#9 54.17 Preparing to unpack .../031-libpaper1_1.1.28build2_amd64.deb ...
#9 54.17 Unpacking libpaper1:amd64 (1.1.28build2) ...
#9 54.18 Selecting previously unselected package libteckit0:amd64.
#9 54.18 Preparing to unpack .../032-libteckit0_2.5.11+ds1-1_amd64.deb ...
#9 54.18 Unpacking libteckit0:amd64 (2.5.11+ds1-1) ...
#9 54.20 Selecting previously unselected package x11-common.
#9 54.20 Preparing to unpack .../033-x11-common_1%3a7.7+23ubuntu2_all.deb ...
#9 54.20 Unpacking x11-common (1:7.7+23ubuntu2) ...
#9 54.21 Selecting previously unselected package libice6:amd64.
#9 54.21 Preparing to unpack .../034-libice6_2%3a1.0.10-1build2_amd64.deb ...
#9 54.21 Unpacking libice6:amd64 (2:1.0.10-1build2) ...
#9 54.23 Selecting previously unselected package libsm6:amd64.
#9 54.24 Preparing to unpack .../035-libsm6_2%3a1.2.3-1build2_amd64.deb ...
#9 54.24 Unpacking libsm6:amd64 (2:1.2.3-1build2) ...
#9 54.31 Selecting previously unselected package libxt6:amd64.
#9 54.31 Preparing to unpack .../036-libxt6_1%3a1.2.1-1_amd64.deb ...
#9 54.31 Unpacking libxt6:amd64 (1:1.2.1-1) ...
#9 54.32 Selecting previously unselected package libxmu6:amd64.
#9 54.33 Preparing to unpack .../037-libxmu6_2%3a1.1.3-3_amd64.deb ...
#9 54.33 Unpacking libxmu6:amd64 (2:1.1.3-3) ...
#9 54.34 Selecting previously unselected package libxaw7:amd64.
#9 54.34 Preparing to unpack .../038-libxaw7_2%3a1.0.14-1_amd64.deb ...
#9 54.34 Unpacking libxaw7:amd64 (2:1.0.14-1) ...
#9 54.35 Selecting previously unselected package libxi6:amd64.
#9 54.35 Preparing to unpack .../039-libxi6_2%3a1.8-1build1_amd64.deb ...
#9 54.35 Unpacking libxi6:amd64 (2:1.8-1build1) ...
#9 54.36 Selecting previously unselected package libzzip-0-13:amd64.
#9 54.36 Preparing to unpack .../040-libzzip-0-13_0.13.72+dfsg.1-1.1_amd64.deb ...
#9 54.36 Unpacking libzzip-0-13:amd64 (0.13.72+dfsg.1-1.1) ...
#9 54.37 Selecting previously unselected package texlive-binaries.
#9 54.38 Preparing to unpack .../041-texlive-binaries_2021.20210626.59705-1ubuntu0.2_amd64.deb ...
#9 54.38 Unpacking texlive-binaries (2021.20210626.59705-1ubuntu0.2) ...
#9 54.75 Selecting previously unselected package fonts-urw-base35.
#9 54.75 Preparing to unpack .../042-fonts-urw-base35_20200910-1_all.deb ...
#9 54.82 Unpacking fonts-urw-base35 (20200910-1) ...
#9 55.15 Selecting previously unselected package libgs9-common.
#9 55.16 Preparing to unpack .../043-libgs9-common_9.55.0~dfsg1-0ubuntu5.11_all.deb ...
#9 55.18 Unpacking libgs9-common (9.55.0~dfsg1-0ubuntu5.11) ...
#9 55.23 Selecting previously unselected package libavahi-common-data:amd64.
#9 55.23 Preparing to unpack .../044-libavahi-common-data_0.8-5ubuntu5.2_amd64.deb ...
#9 55.23 Unpacking libavahi-common-data:amd64 (0.8-5ubuntu5.2) ...
#9 55.27 Selecting previously unselected package libavahi-common3:amd64.
#9 55.27 Preparing to unpack .../045-libavahi-common3_0.8-5ubuntu5.2_amd64.deb ...
#9 55.27 Unpacking libavahi-common3:amd64 (0.8-5ubuntu5.2) ...
#9 55.28 Selecting previously unselected package libavahi-client3:amd64.
#9 55.28 Preparing to unpack .../046-libavahi-client3_0.8-5ubuntu5.2_amd64.deb ...
#9 55.28 Unpacking libavahi-client3:amd64 (0.8-5ubuntu5.2) ...
#9 55.29 Selecting previously unselected package libcups2:amd64.
#9 55.29 Preparing to unpack .../047-libcups2_2.4.1op1-1ubuntu4.11_amd64.deb ...
#9 55.29 Unpacking libcups2:amd64 (2.4.1op1-1ubuntu4.11) ...
#9 55.30 Selecting previously unselected package libidn12:amd64.
#9 55.30 Preparing to unpack .../048-libidn12_1.38-4ubuntu1_amd64.deb ...
#9 55.30 Unpacking libidn12:amd64 (1.38-4ubuntu1) ...
#9 55.31 Selecting previously unselected package libijs-0.35:amd64.
#9 55.31 Preparing to unpack .../049-libijs-0.35_0.35-15build2_amd64.deb ...
#9 55.31 Unpacking libijs-0.35:amd64 (0.35-15build2) ...
#9 55.32 Selecting previously unselected package libjbig2dec0:amd64.
#9 55.32 Preparing to unpack .../050-libjbig2dec0_0.19-3build2_amd64.deb ...
#9 55.32 Unpacking libjbig2dec0:amd64 (0.19-3build2) ...
#9 55.33 Selecting previously unselected package libopenjp2-7:amd64.
#9 55.33 Preparing to unpack .../051-libopenjp2-7_2.4.0-6ubuntu0.3_amd64.deb ...
#9 55.33 Unpacking libopenjp2-7:amd64 (2.4.0-6ubuntu0.3) ...
#9 55.34 Selecting previously unselected package libgs9:amd64.
#9 55.34 Preparing to unpack .../052-libgs9_9.55.0~dfsg1-0ubuntu5.11_amd64.deb ...
#9 55.34 Unpacking libgs9:amd64 (9.55.0~dfsg1-0ubuntu5.11) ...
#9 55.42 Selecting previously unselected package ghostscript.
#9 55.42 Preparing to unpack .../053-ghostscript_9.55.0~dfsg1-0ubuntu5.11_amd64.deb ...
#9 55.42 Unpacking ghostscript (9.55.0~dfsg1-0ubuntu5.11) ...
#9 55.46 Selecting previously unselected package dvipng.
#9 55.46 Preparing to unpack .../054-dvipng_1.15-1.1_amd64.deb ...
#9 55.46 Unpacking dvipng (1.15-1.1) ...
#9 55.48 Selecting previously unselected package libwoff1:amd64.
#9 55.48 Preparing to unpack .../055-libwoff1_1.0.2-1build4_amd64.deb ...
#9 55.48 Unpacking libwoff1:amd64 (1.0.2-1build4) ...
#9 55.49 Selecting previously unselected package dvisvgm.
#9 55.49 Preparing to unpack .../056-dvisvgm_2.13.1-1_amd64.deb ...
#9 55.49 Unpacking dvisvgm (2.13.1-1) ...
#9 55.51 Selecting previously unselected package fonts-lmodern.
#9 55.51 Preparing to unpack .../057-fonts-lmodern_2.004.5-6.1_all.deb ...
#9 55.51 Unpacking fonts-lmodern (2.004.5-6.1) ...
#9 55.83 Selecting previously unselected package fonts-noto-mono.
#9 55.84 Preparing to unpack .../058-fonts-noto-mono_20201225-1build1_all.deb ...
#9 55.84 Unpacking fonts-noto-mono (20201225-1build1) ...
#9 55.87 Selecting previously unselected package fonts-texgyre.
#9 55.87 Preparing to unpack .../059-fonts-texgyre_20180621-3.1_all.deb ...
#9 55.88 Unpacking fonts-texgyre (20180621-3.1) ...
#9 56.43 Selecting previously unselected package libapache-pom-java.
#9 56.43 Preparing to unpack .../060-libapache-pom-java_18-1_all.deb ...
#9 56.43 Unpacking libapache-pom-java (18-1) ...
#9 56.44 Selecting previously unselected package libclone-perl.
#9 56.44 Preparing to unpack .../061-libclone-perl_0.45-1build3_amd64.deb ...
#9 56.44 Unpacking libclone-perl (0.45-1build3) ...
#9 56.45 Selecting previously unselected package libcommons-parent-java.
#9 56.45 Preparing to unpack .../062-libcommons-parent-java_43-1_all.deb ...
#9 56.45 Unpacking libcommons-parent-java (43-1) ...
#9 56.46 Selecting previously unselected package libcommons-logging-java.
#9 56.46 Preparing to unpack .../063-libcommons-logging-java_1.2-2_all.deb ...
#9 56.47 Unpacking libcommons-logging-java (1.2-2) ...
#9 56.48 Selecting previously unselected package libdata-dump-perl.
#9 56.48 Preparing to unpack .../064-libdata-dump-perl_1.25-1_all.deb ...
#9 56.48 Unpacking libdata-dump-perl (1.25-1) ...
#9 56.49 Selecting previously unselected package libdrm-amdgpu1:amd64.
#9 56.50 Preparing to unpack .../065-libdrm-amdgpu1_2.4.113-2~ubuntu0.22.04.1_amd64.deb ...
#9 56.50 Unpacking libdrm-amdgpu1:amd64 (2.4.113-2~ubuntu0.22.04.1) ...
#9 56.51 Selecting previously unselected package libpciaccess0:amd64.
#9 56.51 Preparing to unpack .../066-libpciaccess0_0.16-3_amd64.deb ...
#9 56.51 Unpacking libpciaccess0:amd64 (0.16-3) ...
#9 56.52 Selecting previously unselected package libdrm-intel1:amd64.
#9 56.52 Preparing to unpack .../067-libdrm-intel1_2.4.113-2~ubuntu0.22.04.1_amd64.deb ...
#9 56.52 Unpacking libdrm-intel1:amd64 (2.4.113-2~ubuntu0.22.04.1) ...
#9 56.53 Selecting previously unselected package libdrm-nouveau2:amd64.
#9 56.54 Preparing to unpack .../068-libdrm-nouveau2_2.4.113-2~ubuntu0.22.04.1_amd64.deb ...
#9 56.54 Unpacking libdrm-nouveau2:amd64 (2.4.113-2~ubuntu0.22.04.1) ...
#9 56.55 Selecting previously unselected package libdrm-radeon1:amd64.
#9 56.55 Preparing to unpack .../069-libdrm-radeon1_2.4.113-2~ubuntu0.22.04.1_amd64.deb ...
#9 56.55 Unpacking libdrm-radeon1:amd64 (2.4.113-2~ubuntu0.22.04.1) ...
#9 56.56 Selecting previously unselected package libencode-locale-perl.
#9 56.56 Preparing to unpack .../070-libencode-locale-perl_1.05-1.1_all.deb ...
#9 56.56 Unpacking libencode-locale-perl (1.05-1.1) ...
#9 56.58 Selecting previously unselected package libipc-system-simple-perl.
#9 56.58 Preparing to unpack .../071-libipc-system-simple-perl_1.30-1_all.deb ...
#9 56.58 Unpacking libipc-system-simple-perl (1.30-1) ...
#9 56.59 Selecting previously unselected package libfile-basedir-perl.
#9 56.59 Preparing to unpack .../072-libfile-basedir-perl_0.09-1_all.deb ...
#9 56.59 Unpacking libfile-basedir-perl (0.09-1) ...
#9 56.60 Selecting previously unselected package liburi-perl.
#9 56.61 Preparing to unpack .../073-liburi-perl_5.10-1_all.deb ...
#9 56.61 Unpacking liburi-perl (5.10-1) ...
#9 56.62 Selecting previously unselected package libfile-desktopentry-perl.
#9 56.62 Preparing to unpack .../074-libfile-desktopentry-perl_0.22-2_all.deb ...
#9 56.62 Unpacking libfile-desktopentry-perl (0.22-2) ...
#9 56.63 Selecting previously unselected package libtimedate-perl.
#9 56.64 Preparing to unpack .../075-libtimedate-perl_2.3300-2_all.deb ...
#9 56.64 Unpacking libtimedate-perl (2.3300-2) ...
#9 56.65 Selecting previously unselected package libhttp-date-perl.
#9 56.65 Preparing to unpack .../076-libhttp-date-perl_6.05-1_all.deb ...
#9 56.65 Unpacking libhttp-date-perl (6.05-1) ...
#9 56.66 Selecting previously unselected package libfile-listing-perl.
#9 56.67 Preparing to unpack .../077-libfile-listing-perl_6.14-1_all.deb ...
#9 56.67 Unpacking libfile-listing-perl (6.14-1) ...
#9 56.68 Selecting previously unselected package libfile-mimeinfo-perl.
#9 56.68 Preparing to unpack .../078-libfile-mimeinfo-perl_0.31-1_all.deb ...
#9 56.68 Unpacking libfile-mimeinfo-perl (0.31-1) ...
#9 56.71 Selecting previously unselected package libfont-afm-perl.
#9 56.71 Preparing to unpack .../079-libfont-afm-perl_1.20-3_all.deb ...
#9 56.71 Unpacking libfont-afm-perl (1.20-3) ...
#9 56.71 Selecting previously unselected package libfontenc1:amd64.
#9 56.71 Preparing to unpack .../080-libfontenc1_1%3a1.1.4-1build3_amd64.deb ...
#9 56.71 Unpacking libfontenc1:amd64 (1:1.1.4-1build3) ...
#9 56.72 Selecting previously unselected package libglapi-mesa:amd64.
#9 56.72 Preparing to unpack .../081-libglapi-mesa_23.2.1-1ubuntu3.1~22.04.3_amd64.deb ...
#9 56.72 Unpacking libglapi-mesa:amd64 (23.2.1-1ubuntu3.1~22.04.3) ...
#9 56.73 Selecting previously unselected package libgl1-amber-dri:amd64.
#9 56.74 Preparing to unpack .../082-libgl1-amber-dri_21.3.9-0ubuntu1~22.04.1_amd64.deb ...
#9 56.74 Unpacking libgl1-amber-dri:amd64 (21.3.9-0ubuntu1~22.04.1) ...
#9 56.79 Selecting previously unselected package libllvm15:amd64.
#9 56.79 Preparing to unpack .../083-libllvm15_1%3a15.0.7-0ubuntu0.22.04.3_amd64.deb ...
#9 56.81 Unpacking libllvm15:amd64 (1:15.0.7-0ubuntu0.22.04.3) ...
#9 57.10 Selecting previously unselected package libsensors-config.
#9 57.10 Preparing to unpack .../084-libsensors-config_1%3a3.6.0-7ubuntu1_all.deb ...
#9 57.10 Unpacking libsensors-config (1:3.6.0-7ubuntu1) ...
#9 57.11 Selecting previously unselected package libsensors5:amd64.
#9 57.11 Preparing to unpack .../085-libsensors5_1%3a3.6.0-7ubuntu1_amd64.deb ...
#9 57.13 Unpacking libsensors5:amd64 (1:3.6.0-7ubuntu1) ...
#9 57.14 Selecting previously unselected package libxcb-dri3-0:amd64.
#9 57.14 Preparing to unpack .../086-libxcb-dri3-0_1.14-3ubuntu3_amd64.deb ...
#9 57.14 Unpacking libxcb-dri3-0:amd64 (1.14-3ubuntu3) ...
#9 57.15 Selecting previously unselected package libgl1-mesa-dri:amd64.
#9 57.15 Preparing to unpack .../087-libgl1-mesa-dri_23.2.1-1ubuntu3.1~22.04.3_amd64.deb ...
#9 57.15 Unpacking libgl1-mesa-dri:amd64 (23.2.1-1ubuntu3.1~22.04.3) ...
#9 57.27 Selecting previously unselected package libx11-xcb1:amd64.
#9 57.27 Preparing to unpack .../088-libx11-xcb1_2%3a1.7.5-1ubuntu0.3_amd64.deb ...
#9 57.28 Unpacking libx11-xcb1:amd64 (2:1.7.5-1ubuntu0.3) ...
#9 57.28 Selecting previously unselected package libxcb-dri2-0:amd64.
#9 57.29 Preparing to unpack .../089-libxcb-dri2-0_1.14-3ubuntu3_amd64.deb ...
#9 57.29 Unpacking libxcb-dri2-0:amd64 (1.14-3ubuntu3) ...
#9 57.29 Selecting previously unselected package libxcb-glx0:amd64.
#9 57.30 Preparing to unpack .../090-libxcb-glx0_1.14-3ubuntu3_amd64.deb ...
#9 57.30 Unpacking libxcb-glx0:amd64 (1.14-3ubuntu3) ...
#9 57.31 Selecting previously unselected package libxcb-present0:amd64.
#9 57.31 Preparing to unpack .../091-libxcb-present0_1.14-3ubuntu3_amd64.deb ...
#9 57.31 Unpacking libxcb-present0:amd64 (1.14-3ubuntu3) ...
#9 57.32 Selecting previously unselected package libxcb-randr0:amd64.
#9 57.32 Preparing to unpack .../092-libxcb-randr0_1.14-3ubuntu3_amd64.deb ...
#9 57.32 Unpacking libxcb-randr0:amd64 (1.14-3ubuntu3) ...
#9 57.33 Selecting previously unselected package libxcb-sync1:amd64.
#9 57.33 Preparing to unpack .../093-libxcb-sync1_1.14-3ubuntu3_amd64.deb ...
#9 57.33 Unpacking libxcb-sync1:amd64 (1.14-3ubuntu3) ...
#9 57.34 Selecting previously unselected package libxcb-xfixes0:amd64.
#9 57.34 Preparing to unpack .../094-libxcb-xfixes0_1.14-3ubuntu3_amd64.deb ...
#9 57.34 Unpacking libxcb-xfixes0:amd64 (1.14-3ubuntu3) ...
#9 57.35 Selecting previously unselected package libxfixes3:amd64.
#9 57.35 Preparing to unpack .../095-libxfixes3_1%3a6.0.0-1_amd64.deb ...
#9 57.35 Unpacking libxfixes3:amd64 (1:6.0.0-1) ...
#9 57.36 Selecting previously unselected package libxshmfence1:amd64.
#9 57.36 Preparing to unpack .../096-libxshmfence1_1.3-1build4_amd64.deb ...
#9 57.36 Unpacking libxshmfence1:amd64 (1.3-1build4) ...
#9 57.37 Selecting previously unselected package libxxf86vm1:amd64.
#9 57.37 Preparing to unpack .../097-libxxf86vm1_1%3a1.1.4-1build3_amd64.deb ...
#9 57.37 Unpacking libxxf86vm1:amd64 (1:1.1.4-1build3) ...
#9 57.38 Selecting previously unselected package libglx-mesa0:amd64.
#9 57.38 Preparing to unpack .../098-libglx-mesa0_23.2.1-1ubuntu3.1~22.04.3_amd64.deb ...
#9 57.38 Unpacking libglx-mesa0:amd64 (23.2.1-1ubuntu3.1~22.04.3) ...
#9 57.39 Selecting previously unselected package libhtml-tagset-perl.
#9 57.39 Preparing to unpack .../099-libhtml-tagset-perl_3.20-4_all.deb ...
#9 57.39 Unpacking libhtml-tagset-perl (3.20-4) ...
#9 57.40 Selecting previously unselected package libhtml-parser-perl:amd64.
#9 57.40 Preparing to unpack .../100-libhtml-parser-perl_3.76-1build2_amd64.deb ...
#9 57.40 Unpacking libhtml-parser-perl:amd64 (3.76-1build2) ...
#9 57.41 Selecting previously unselected package libio-html-perl.
#9 57.42 Preparing to unpack .../101-libio-html-perl_1.004-2_all.deb ...
#9 57.42 Unpacking libio-html-perl (1.004-2) ...
#9 57.43 Selecting previously unselected package liblwp-mediatypes-perl.
#9 57.43 Preparing to unpack .../102-liblwp-mediatypes-perl_6.04-1_all.deb ...
#9 57.43 Unpacking liblwp-mediatypes-perl (6.04-1) ...
#9 57.44 Selecting previously unselected package libhttp-message-perl.
#9 57.44 Preparing to unpack .../103-libhttp-message-perl_6.36-1_all.deb ...
#9 57.44 Unpacking libhttp-message-perl (6.36-1) ...
#9 57.45 Selecting previously unselected package libhtml-form-perl.
#9 57.45 Preparing to unpack .../104-libhtml-form-perl_6.07-1_all.deb ...
#9 57.45 Unpacking libhtml-form-perl (6.07-1) ...
#9 57.46 Selecting previously unselected package libhtml-tree-perl.
#9 57.46 Preparing to unpack .../105-libhtml-tree-perl_5.07-2_all.deb ...
#9 57.46 Unpacking libhtml-tree-perl (5.07-2) ...
#9 57.48 Selecting previously unselected package libhtml-format-perl.
#9 57.48 Preparing to unpack .../106-libhtml-format-perl_2.12-1.1_all.deb ...
#9 57.48 Unpacking libhtml-format-perl (2.12-1.1) ...
#9 57.49 Selecting previously unselected package libhttp-cookies-perl.
#9 57.49 Preparing to unpack .../107-libhttp-cookies-perl_6.10-1_all.deb ...
#9 57.50 Unpacking libhttp-cookies-perl (6.10-1) ...
#9 57.50 Selecting previously unselected package libhttp-daemon-perl.
#9 57.51 Preparing to unpack .../108-libhttp-daemon-perl_6.13-1ubuntu0.1_all.deb ...
#9 57.51 Unpacking libhttp-daemon-perl (6.13-1ubuntu0.1) ...
#9 57.51 Selecting previously unselected package libhttp-negotiate-perl.
#9 57.51 Preparing to unpack .../109-libhttp-negotiate-perl_6.01-1_all.deb ...
#9 57.52 Unpacking libhttp-negotiate-perl (6.01-1) ...
#9 57.52 Selecting previously unselected package perl-openssl-defaults:amd64.
#9 57.53 Preparing to unpack .../110-perl-openssl-defaults_5build2_amd64.deb ...
#9 57.53 Unpacking perl-openssl-defaults:amd64 (5build2) ...
#9 57.53 Selecting previously unselected package libnet-ssleay-perl:amd64.
#9 57.54 Preparing to unpack .../111-libnet-ssleay-perl_1.92-1build2_amd64.deb ...
#9 57.54 Unpacking libnet-ssleay-perl:amd64 (1.92-1build2) ...
#9 57.55 Selecting previously unselected package libio-socket-ssl-perl.
#9 57.55 Preparing to unpack .../112-libio-socket-ssl-perl_2.074-2_all.deb ...
#9 57.55 Unpacking libio-socket-ssl-perl (2.074-2) ...
#9 57.56 Selecting previously unselected package libio-stringy-perl.
#9 57.57 Preparing to unpack .../113-libio-stringy-perl_2.111-3_all.deb ...
#9 57.57 Unpacking libio-stringy-perl (2.111-3) ...
#9 57.58 Selecting previously unselected package libnet-http-perl.
#9 57.58 Preparing to unpack .../114-libnet-http-perl_6.22-1_all.deb ...
#9 57.58 Unpacking libnet-http-perl (6.22-1) ...
#9 57.59 Selecting previously unselected package libtry-tiny-perl.
#9 57.59 Preparing to unpack .../115-libtry-tiny-perl_0.31-1_all.deb ...
#9 57.59 Unpacking libtry-tiny-perl (0.31-1) ...
#9 57.61 Selecting previously unselected package libwww-robotrules-perl.
#9 57.61 Preparing to unpack .../116-libwww-robotrules-perl_6.02-1_all.deb ...
#9 57.61 Unpacking libwww-robotrules-perl (6.02-1) ...
#9 57.62 Selecting previously unselected package libwww-perl.
#9 57.62 Preparing to unpack .../117-libwww-perl_6.61-1_all.deb ...
#9 57.62 Unpacking libwww-perl (6.61-1) ...
#9 57.64 Selecting previously unselected package liblwp-protocol-https-perl.
#9 57.64 Preparing to unpack .../118-liblwp-protocol-https-perl_6.10-1_all.deb ...
#9 57.64 Unpacking liblwp-protocol-https-perl (6.10-1) ...
#9 57.65 Selecting previously unselected package libnet-smtp-ssl-perl.
#9 57.65 Preparing to unpack .../119-libnet-smtp-ssl-perl_1.04-1_all.deb ...
#9 57.65 Unpacking libnet-smtp-ssl-perl (1.04-1) ...
#9 57.66 Selecting previously unselected package libmailtools-perl.
#9 57.66 Preparing to unpack .../120-libmailtools-perl_2.21-1_all.deb ...
#9 57.66 Unpacking libmailtools-perl (2.21-1) ...
#9 57.68 Selecting previously unselected package libxml-parser-perl:amd64.
#9 57.68 Preparing to unpack .../121-libxml-parser-perl_2.46-3build1_amd64.deb ...
#9 57.68 Unpacking libxml-parser-perl:amd64 (2.46-3build1) ...
#9 57.69 Selecting previously unselected package libxml-twig-perl.
#9 57.70 Preparing to unpack .../122-libxml-twig-perl_1%3a3.52-1_all.deb ...
#9 57.70 Unpacking libxml-twig-perl (1:3.52-1) ...
#9 57.71 Selecting previously unselected package libnet-dbus-perl.
#9 57.71 Preparing to unpack .../123-libnet-dbus-perl_1.2.0-1build3_amd64.deb ...
#9 57.71 Unpacking libnet-dbus-perl (1.2.0-1build3) ...
#9 57.73 Selecting previously unselected package libpaper-utils.
#9 57.73 Preparing to unpack .../124-libpaper-utils_1.1.28build2_amd64.deb ...
#9 57.73 Unpacking libpaper-utils (1.1.28build2) ...
#9 57.74 Selecting previously unselected package rubygems-integration.
#9 57.74 Preparing to unpack .../125-rubygems-integration_1.18_all.deb ...
#9 57.74 Unpacking rubygems-integration (1.18) ...
#9 57.75 Selecting previously unselected package ruby3.0.
#9 57.75 Preparing to unpack .../126-ruby3.0_3.0.2-7ubuntu2.10_amd64.deb ...
#9 57.75 Unpacking ruby3.0 (3.0.2-7ubuntu2.10) ...
#9 57.76 Selecting previously unselected package ruby-rubygems.
#9 57.76 Preparing to unpack .../127-ruby-rubygems_3.3.5-2_all.deb ...
#9 57.76 Unpacking ruby-rubygems (3.3.5-2) ...
#9 57.79 Selecting previously unselected package ruby.
#9 57.79 Preparing to unpack .../128-ruby_1%3a3.0~exp1_amd64.deb ...
#9 57.79 Unpacking ruby (1:3.0~exp1) ...
#9 57.80 Selecting previously unselected package rake.
#9 57.80 Preparing to unpack .../129-rake_13.0.6-2_all.deb ...
#9 57.80 Unpacking rake (13.0.6-2) ...
#9 57.81 Selecting previously unselected package ruby-net-telnet.
#9 57.82 Preparing to unpack .../130-ruby-net-telnet_0.1.1-2_all.deb ...
#9 57.82 Unpacking ruby-net-telnet (0.1.1-2) ...
#9 57.83 Selecting previously unselected package ruby-webrick.
#9 57.83 Preparing to unpack .../131-ruby-webrick_1.7.0-3ubuntu0.1_all.deb ...
#9 57.83 Unpacking ruby-webrick (1.7.0-3ubuntu0.1) ...
#9 57.84 Selecting previously unselected package ruby-xmlrpc.
#9 57.84 Preparing to unpack .../132-ruby-xmlrpc_0.3.2-1ubuntu0.1_all.deb ...
#9 57.84 Unpacking ruby-xmlrpc (0.3.2-1ubuntu0.1) ...
#9 57.85 Selecting previously unselected package libruby3.0:amd64.
#9 57.86 Preparing to unpack .../133-libruby3.0_3.0.2-7ubuntu2.10_amd64.deb ...
#9 57.86 Unpacking libruby3.0:amd64 (3.0.2-7ubuntu2.10) ...
#9 58.06 Selecting previously unselected package libtcl8.6:amd64.
#9 58.06 Preparing to unpack .../134-libtcl8.6_8.6.12+dfsg-1build1_amd64.deb ...
#9 58.06 Unpacking libtcl8.6:amd64 (8.6.12+dfsg-1build1) ...
#9 58.09 Selecting previously unselected package libtext-unidecode-perl.
#9 58.09 Preparing to unpack .../135-libtext-unidecode-perl_1.30-1_all.deb ...
#9 58.09 Unpacking libtext-unidecode-perl (1.30-1) ...
#9 58.12 Selecting previously unselected package libtie-ixhash-perl.
#9 58.12 Preparing to unpack .../136-libtie-ixhash-perl_1.23-2.1_all.deb ...
#9 58.12 Unpacking libtie-ixhash-perl (1.23-2.1) ...
#9 58.13 Selecting previously unselected package libxft2:amd64.
#9 58.13 Preparing to unpack .../137-libxft2_2.3.4-1_amd64.deb ...
#9 58.13 Unpacking libxft2:amd64 (2.3.4-1) ...
#9 58.14 Selecting previously unselected package libxss1:amd64.
#9 58.14 Preparing to unpack .../138-libxss1_1%3a1.2.3-1build2_amd64.deb ...
#9 58.14 Unpacking libxss1:amd64 (1:1.2.3-1build2) ...
#9 58.15 Selecting previously unselected package libtk8.6:amd64.
#9 58.15 Preparing to unpack .../139-libtk8.6_8.6.12-1build1_amd64.deb ...
#9 58.15 Unpacking libtk8.6:amd64 (8.6.12-1build1) ...
#9 58.17 Selecting previously unselected package libutempter0:amd64.
#9 58.18 Preparing to unpack .../140-libutempter0_1.2.1-2build2_amd64.deb ...
#9 58.18 Unpacking libutempter0:amd64 (1.2.1-2build2) ...
#9 58.19 Selecting previously unselected package libx11-protocol-perl.
#9 58.19 Preparing to unpack .../141-libx11-protocol-perl_0.56-7.1_all.deb ...
#9 58.19 Unpacking libx11-protocol-perl (0.56-7.1) ...
#9 58.20 Selecting previously unselected package libxcb-shape0:amd64.
#9 58.21 Preparing to unpack .../142-libxcb-shape0_1.14-3ubuntu3_amd64.deb ...
#9 58.21 Unpacking libxcb-shape0:amd64 (1.14-3ubuntu3) ...
#9 58.22 Selecting previously unselected package libxcomposite1:amd64.
#9 58.22 Preparing to unpack .../143-libxcomposite1_1%3a0.4.5-1build2_amd64.deb ...
#9 58.22 Unpacking libxcomposite1:amd64 (1:0.4.5-1build2) ...
#9 58.23 Selecting previously unselected package libxcursor1:amd64.
#9 58.23 Preparing to unpack .../144-libxcursor1_1%3a1.2.0-2build4_amd64.deb ...
#9 58.23 Unpacking libxcursor1:amd64 (1:1.2.0-2build4) ...
#9 58.24 Selecting previously unselected package libxinerama1:amd64.
#9 58.24 Preparing to unpack .../145-libxinerama1_2%3a1.1.4-3_amd64.deb ...
#9 58.24 Unpacking libxinerama1:amd64 (2:1.1.4-3) ...
#9 58.25 Selecting previously unselected package libxkbfile1:amd64.
#9 58.25 Preparing to unpack .../146-libxkbfile1_1%3a1.1.0-1build3_amd64.deb ...
#9 58.25 Unpacking libxkbfile1:amd64 (1:1.1.0-1build3) ...
#9 58.26 Selecting previously unselected package libxml-namespacesupport-perl.
#9 58.27 Preparing to unpack .../147-libxml-namespacesupport-perl_1.12-1.1_all.deb ...
#9 58.27 Unpacking libxml-namespacesupport-perl (1.12-1.1) ...
#9 58.27 Selecting previously unselected package libxml-sax-base-perl.
#9 58.28 Preparing to unpack .../148-libxml-sax-base-perl_1.09-1.1_all.deb ...
#9 58.28 Unpacking libxml-sax-base-perl (1.09-1.1) ...
#9 58.29 Selecting previously unselected package libxml-sax-perl.
#9 58.29 Preparing to unpack .../149-libxml-sax-perl_1.02+dfsg-3_all.deb ...
#9 58.29 Unpacking libxml-sax-perl (1.02+dfsg-3) ...
#9 58.30 Selecting previously unselected package libxml-libxml-perl.
#9 58.31 Preparing to unpack .../150-libxml-libxml-perl_2.0207+dfsg+really+2.0134-1_amd64.deb ...
#9 58.32 Unpacking libxml-libxml-perl (2.0207+dfsg+really+2.0134-1) ...
#9 58.32 Selecting previously unselected package libxml-sax-expat-perl.
#9 58.32 Preparing to unpack .../151-libxml-sax-expat-perl_0.51-1_all.deb ...
#9 58.33 Unpacking libxml-sax-expat-perl (0.51-1) ...
#9 58.34 Selecting previously unselected package libxml-xpathengine-perl.
#9 58.34 Preparing to unpack .../152-libxml-xpathengine-perl_0.14-1_all.deb ...
#9 58.34 Unpacking libxml-xpathengine-perl (0.14-1) ...
#9 58.41 Selecting previously unselected package libxrandr2:amd64.
#9 58.41 Preparing to unpack .../153-libxrandr2_2%3a1.5.2-1build1_amd64.deb ...
#9 58.41 Unpacking libxrandr2:amd64 (2:1.5.2-1build1) ...
#9 58.41 Selecting previously unselected package libxtst6:amd64.
#9 58.41 Preparing to unpack .../154-libxtst6_2%3a1.2.3-1build4_amd64.deb ...
#9 58.41 Unpacking libxtst6:amd64 (2:1.2.3-1build4) ...
#9 58.41 Selecting previously unselected package libxv1:amd64.
#9 58.41 Preparing to unpack .../155-libxv1_2%3a1.0.11-1build2_amd64.deb ...
#9 58.41 Unpacking libxv1:amd64 (2:1.0.11-1build2) ...
#9 58.41 Selecting previously unselected package libxxf86dga1:amd64.
#9 58.41 Preparing to unpack .../156-libxxf86dga1_2%3a1.1.5-0ubuntu3_amd64.deb ...
#9 58.41 Unpacking libxxf86dga1:amd64 (2:1.1.5-0ubuntu3) ...
#9 58.41 Selecting previously unselected package xfonts-encodings.
#9 58.41 Preparing to unpack .../157-xfonts-encodings_1%3a1.0.5-0ubuntu2_all.deb ...
#9 58.41 Unpacking xfonts-encodings (1:1.0.5-0ubuntu2) ...
#9 58.43 Selecting previously unselected package xfonts-utils.
#9 58.43 Preparing to unpack .../158-xfonts-utils_1%3a7.7+6build2_amd64.deb ...
#9 58.43 Unpacking xfonts-utils (1:7.7+6build2) ...
#9 58.45 Selecting previously unselected package lmodern.
#9 58.45 Preparing to unpack .../159-lmodern_2.004.5-6.1_all.deb ...
#9 58.46 Unpacking lmodern (2.004.5-6.1) ...
#9 59.06 Selecting previously unselected package preview-latex-style.
#9 59.06 Preparing to unpack .../160-preview-latex-style_12.2-1ubuntu1_all.deb ...
#9 59.06 Unpacking preview-latex-style (12.2-1ubuntu1) ...
#9 59.08 Selecting previously unselected package tcl8.6.
#9 59.08 Preparing to unpack .../161-tcl8.6_8.6.12+dfsg-1build1_amd64.deb ...
#9 59.08 Unpacking tcl8.6 (8.6.12+dfsg-1build1) ...
#9 59.09 Selecting previously unselected package tcl.
#9 59.09 Preparing to unpack .../162-tcl_8.6.11+1build2_amd64.deb ...
#9 59.09 Unpacking tcl (8.6.11+1build2) ...
#9 59.13 Selecting previously unselected package tex-gyre.
#9 59.13 Preparing to unpack .../163-tex-gyre_20180621-3.1_all.deb ...
#9 59.14 Unpacking tex-gyre (20180621-3.1) ...
#9 59.47 Selecting previously unselected package texinfo.
#9 59.48 Preparing to unpack .../164-texinfo_6.8-4build1_amd64.deb ...
#9 59.48 Unpacking texinfo (6.8-4build1) ...
#9 59.53 Selecting previously unselected package xdg-utils.
#9 59.54 Preparing to unpack .../165-xdg-utils_1.1.3-4.1ubuntu3~22.04.1_all.deb ...
#9 59.54 Unpacking xdg-utils (1.1.3-4.1ubuntu3~22.04.1) ...
#9 59.57 Selecting previously unselected package texlive-base.
#9 59.58 Preparing to unpack .../166-texlive-base_2021.20220204-1_all.deb ...
#9 59.61 Unpacking texlive-base (2021.20220204-1) ...
#9 61.21 Selecting previously unselected package texlive-fonts-recommended.
#9 61.21 Preparing to unpack .../167-texlive-fonts-recommended_2021.20220204-1_all.deb ...
#9 61.21 Unpacking texlive-fonts-recommended (2021.20220204-1) ...
#9 62.08 Selecting previously unselected package texlive-latex-base.
#9 62.08 Preparing to unpack .../168-texlive-latex-base_2021.20220204-1_all.deb ...
#9 62.09 Unpacking texlive-latex-base (2021.20220204-1) ...
#9 62.25 Selecting previously unselected package libfontbox-java.
#9 62.25 Preparing to unpack .../169-libfontbox-java_1%3a1.8.16-2_all.deb ...
#9 62.25 Unpacking libfontbox-java (1:1.8.16-2) ...
#9 62.27 Selecting previously unselected package libpdfbox-java.
#9 62.28 Preparing to unpack .../170-libpdfbox-java_1%3a1.8.16-2_all.deb ...
#9 62.28 Unpacking libpdfbox-java (1:1.8.16-2) ...
#9 62.54 Selecting previously unselected package texlive-latex-recommended.
#9 62.54 Preparing to unpack .../171-texlive-latex-recommended_2021.20220204-1_all.deb ...
#9 62.54 Unpacking texlive-latex-recommended (2021.20220204-1) ...
#9 63.46 Selecting previously unselected package texlive-pictures.
#9 63.46 Preparing to unpack .../172-texlive-pictures_2021.20220204-1_all.deb ...
#9 63.46 Unpacking texlive-pictures (2021.20220204-1) ...
#9 64.19 Selecting previously unselected package texlive-latex-extra.
#9 64.19 Preparing to unpack .../173-texlive-latex-extra_2021.20220204-1_all.deb ...
#9 64.19 Unpacking texlive-latex-extra (2021.20220204-1) ...
#9 65.70 Selecting previously unselected package texlive-plain-generic.
#9 65.70 Preparing to unpack .../174-texlive-plain-generic_2021.20220204-1_all.deb ...
#9 65.78 Unpacking texlive-plain-generic (2021.20220204-1) ...
#9 67.89 Selecting previously unselected package tipa.
#9 67.90 Preparing to unpack .../175-tipa_2%3a1.3-21_all.deb ...
#9 67.91 Unpacking tipa (2:1.3-21) ...
#9 68.11 Selecting previously unselected package tk8.6.
#9 68.12 Preparing to unpack .../176-tk8.6_8.6.12-1build1_amd64.deb ...
#9 68.12 Unpacking tk8.6 (8.6.12-1build1) ...
#9 68.13 Selecting previously unselected package tk.
#9 68.13 Preparing to unpack .../177-tk_8.6.11+1build2_amd64.deb ...
#9 68.14 Unpacking tk (8.6.11+1build2) ...
#9 68.22 Selecting previously unselected package unzip.
#9 68.23 Preparing to unpack .../178-unzip_6.0-26ubuntu3.2_amd64.deb ...
#9 68.23 Unpacking unzip (6.0-26ubuntu3.2) ...
#9 68.24 Selecting previously unselected package libglvnd0:amd64.
#9 68.24 Preparing to unpack .../179-libglvnd0_1.4.0-1_amd64.deb ...
#9 68.25 Unpacking libglvnd0:amd64 (1.4.0-1) ...
#9 68.26 Selecting previously unselected package libglx0:amd64.
#9 68.27 Preparing to unpack .../180-libglx0_1.4.0-1_amd64.deb ...
#9 68.27 Unpacking libglx0:amd64 (1.4.0-1) ...
#9 68.28 Selecting previously unselected package libgl1:amd64.
#9 68.29 Preparing to unpack .../181-libgl1_1.4.0-1_amd64.deb ...
#9 68.29 Unpacking libgl1:amd64 (1.4.0-1) ...
#9 68.30 Selecting previously unselected package x11-utils.
#9 68.30 Preparing to unpack .../182-x11-utils_7.7+5build2_amd64.deb ...
#9 68.30 Unpacking x11-utils (7.7+5build2) ...
#9 68.32 Selecting previously unselected package x11-xserver-utils.
#9 68.32 Preparing to unpack .../183-x11-xserver-utils_7.7+9build1_amd64.deb ...
#9 68.33 Unpacking x11-xserver-utils (7.7+9build1) ...
#9 68.34 Selecting previously unselected package xbitmaps.
#9 68.35 Preparing to unpack .../184-xbitmaps_1.1.1-2.1ubuntu1_all.deb ...
#9 68.35 Unpacking xbitmaps (1.1.1-2.1ubuntu1) ...
#9 68.37 Selecting previously unselected package xterm.
#9 68.38 Preparing to unpack .../185-xterm_372-1ubuntu1_amd64.deb ...
#9 68.38 Unpacking xterm (372-1ubuntu1) ...
#9 68.40 Selecting previously unselected package zip.
#9 68.40 Preparing to unpack .../186-zip_3.0-12build2_amd64.deb ...
#9 68.40 Unpacking zip (3.0-12build2) ...
#9 68.42 Selecting previously unselected package libauthen-sasl-perl.
#9 68.42 Preparing to unpack .../187-libauthen-sasl-perl_2.1600-1.1_all.deb ...
#9 68.42 Unpacking libauthen-sasl-perl (2.1600-1.1) ...
#9 68.45 Setting up libtext-iconv-perl (1.7-7build3) ...
#9 68.45 Setting up libgraphite2-3:amd64 (1.3.14-1build2) ...
#9 68.45 Setting up libxcb-dri3-0:amd64 (1.14-3ubuntu3) ...
#9 68.45 Setting up libpixman-1-0:amd64 (0.40.0-1ubuntu0.22.04.1) ...
#9 68.45 Setting up libpaper1:amd64 (1.1.28build2) ...
#9 68.51 debconf: unable to initialize frontend: Dialog
#9 68.51 debconf: (TERM is not set, so the dialog frontend is not usable.)
#9 68.51 debconf: falling back to frontend: Readline
#9 68.56 
#9 68.56 Creating config file /etc/papersize with new version
#9 68.58 Setting up libx11-xcb1:amd64 (2:1.7.5-1ubuntu0.3) ...
#9 68.58 Setting up libpciaccess0:amd64 (0.16-3) ...
#9 68.58 Setting up libapparmor1:amd64 (3.0.4-2ubuntu2.4) ...
#9 68.58 Setting up libtie-ixhash-perl (1.23-2.1) ...
#9 68.58 Setting up fonts-lato (2.0-2.1) ...
#9 68.58 Setting up libxcb-xfixes0:amd64 (1.14-3ubuntu3) ...
#9 68.58 Setting up fonts-noto-mono (20201225-1build1) ...
#9 68.58 Setting up libxi6:amd64 (2:1.8-1build1) ...
#9 68.58 Setting up libfont-afm-perl (1.20-3) ...
#9 68.58 Setting up libwoff1:amd64 (1.0.2-1build4) ...
#9 68.59 Setting up libxrender1:amd64 (1:0.9.10-1build4) ...
#9 68.59 Setting up xdg-user-dirs (0.17-2ubuntu4) ...
#9 68.59 Setting up libtexlua53:amd64 (2021.20210626.59705-1ubuntu0.2) ...
#9 68.59 Setting up libxcb-render0:amd64 (1.14-3ubuntu3) ...
#9 68.59 Setting up libclone-perl (0.45-1build3) ...
#9 68.59 Setting up libyaml-0-2:amd64 (0.2.2-1build2) ...
#9 68.59 Setting up libglib2.0-0:amd64 (2.72.4-0ubuntu2.4) ...
#9 68.60 No schema files found: doing nothing.
#9 68.60 Setting up libglvnd0:amd64 (1.4.0-1) ...
#9 68.60 Setting up libio-stringy-perl (2.111-3) ...
#9 68.60 Setting up libhtml-tagset-perl (3.20-4) ...
#9 68.60 Setting up libijs-0.35:amd64 (0.35-15build2) ...
#9 68.60 Setting up libauthen-sasl-perl (2.1600-1.1) ...
#9 68.60 Setting up libxcb-glx0:amd64 (1.14-3ubuntu3) ...
#9 68.61 Setting up unzip (6.0-26ubuntu3.2) ...
#9 68.61 Setting up libtexluajit2:amd64 (2021.20210626.59705-1ubuntu0.2) ...
#9 68.61 Setting up libfontbox-java (1:1.8.16-2) ...
#9 68.61 Setting up liblwp-mediatypes-perl (6.04-1) ...
#9 68.61 Setting up libxcb-shape0:amd64 (1.14-3ubuntu3) ...
#9 68.61 Setting up x11-common (1:7.7+23ubuntu2) ...
#9 68.68 debconf: unable to initialize frontend: Dialog
#9 68.68 debconf: (TERM is not set, so the dialog frontend is not usable.)
#9 68.68 debconf: falling back to frontend: Readline
#9 68.70 invoke-rc.d: could not determine current runlevel
#9 68.70 invoke-rc.d: policy-rc.d denied execution of start.
#9 68.70 Setting up libtry-tiny-perl (0.31-1) ...
#9 68.70 Setting up libsensors-config (1:3.6.0-7ubuntu1) ...
#9 68.70 Setting up libxxf86dga1:amd64 (2:1.1.5-0ubuntu3) ...
#9 68.70 Setting up perl-openssl-defaults:amd64 (5build2) ...
#9 68.70 Setting up libxml-namespacesupport-perl (1.12-1.1) ...
#9 68.70 Setting up libencode-locale-perl (1.05-1.1) ...
#9 68.71 Setting up rubygems-integration (1.18) ...
#9 68.71 Setting up libxcb-shm0:amd64 (1.14-3ubuntu3) ...
#9 68.71 Setting up libzzip-0-13:amd64 (0.13.72+dfsg.1-1.1) ...
#9 68.71 Setting up libpaper-utils (1.1.28build2) ...
#9 68.71 Setting up fonts-urw-base35 (20200910-1) ...
#9 68.74 Setting up libcairo2:amd64 (1.16.0-5ubuntu2) ...
#9 68.75 Setting up libxxf86vm1:amd64 (1:1.1.4-1build3) ...
#9 68.75 Setting up poppler-data (0.4.11-1) ...
#9 68.75 Setting up libxcb-present0:amd64 (1.14-3ubuntu3) ...
#9 68.75 Setting up tex-common (6.17) ...
#9 68.81 debconf: unable to initialize frontend: Dialog
#9 68.81 debconf: (TERM is not set, so the dialog frontend is not usable.)
#9 68.81 debconf: falling back to frontend: Readline
#9 68.87 update-language: texlive-base not installed and configured, doing nothing!
#9 68.90 Setting up libxml-sax-base-perl (1.09-1.1) ...
#9 68.90 Setting up zip (3.0-12build2) ...
#9 68.90 Setting up libfontenc1:amd64 (1:1.1.4-1build3) ...
#9 68.90 Setting up libglib2.0-data (2.72.4-0ubuntu2.4) ...
#9 68.90 Setting up libdata-dump-perl (1.25-1) ...
#9 68.90 Setting up libxfixes3:amd64 (1:6.0.0-1) ...
#9 68.90 Setting up libxcb-sync1:amd64 (1.14-3ubuntu3) ...
#9 68.90 Setting up libjbig2dec0:amd64 (0.19-3build2) ...
#9 68.91 Setting up libipc-system-simple-perl (1.30-1) ...
#9 68.91 Setting up libteckit0:amd64 (2.5.11+ds1-1) ...
#9 68.91 Setting up libxml-xpathengine-perl (0.14-1) ...
#9 68.91 Setting up libapache-pom-java (18-1) ...
#9 68.91 Setting up libavahi-common-data:amd64 (0.8-5ubuntu5.2) ...
#9 68.91 Setting up libdbus-1-3:amd64 (1.12.20-2ubuntu4.1) ...
#9 68.91 Setting up ruby-net-telnet (0.1.1-2) ...
#9 68.91 Setting up dbus (1.12.20-2ubuntu4.1) ...
#9 68.97 Setting up xfonts-encodings (1:1.0.5-0ubuntu2) ...
#9 68.98 Setting up t1utils (1.41-4build2) ...
#9 68.98 Setting up libxinerama1:amd64 (2:1.1.4-3) ...
#9 68.98 Setting up libxv1:amd64 (2:1.0.11-1build2) ...
#9 68.98 Setting up libidn12:amd64 (1.38-4ubuntu1) ...
#9 68.98 Setting up libio-html-perl (1.004-2) ...
#9 68.98 Setting up libxrandr2:amd64 (2:1.5.2-1build1) ...
#9 68.98 Setting up libtcl8.6:amd64 (8.6.12+dfsg-1build1) ...
#9 68.99 Setting up fonts-texgyre (20180621-3.1) ...
#9 68.99 Setting up libsensors5:amd64 (1:3.6.0-7ubuntu1) ...
#9 68.99 Setting up libglapi-mesa:amd64 (23.2.1-1ubuntu3.1~22.04.3) ...
#9 68.99 Setting up libkpathsea6:amd64 (2021.20210626.59705-1ubuntu0.2) ...
#9 68.99 Setting up libtimedate-perl (2.3300-2) ...
#9 68.99 Setting up ruby-webrick (1.7.0-3ubuntu0.1) ...
#9 69.00 Setting up libutempter0:amd64 (1.2.1-2build2) ...
#9 69.00 Setting up libxcb-dri2-0:amd64 (1.14-3ubuntu3) ...
#9 69.00 Setting up libxshmfence1:amd64 (1.3-1build4) ...
#9 69.00 Setting up libxcb-randr0:amd64 (1.14-3ubuntu3) ...
#9 69.00 Setting up fonts-lmodern (2.004.5-6.1) ...
#9 69.00 Setting up libopenjp2-7:amd64 (2.4.0-6ubuntu0.3) ...
#9 69.00 Setting up libharfbuzz0b:amd64 (2.7.4-1ubuntu3.2) ...
#9 69.00 Setting up fonts-droid-fallback (1:6.0.1r16-1.1build1) ...
#9 69.01 Setting up libxss1:amd64 (1:1.2.3-1build2) ...
#9 69.01 Setting up libxkbfile1:amd64 (1:1.1.0-1build3) ...
#9 69.02 Setting up libtext-unidecode-perl (1.30-1) ...
#9 69.02 Setting up libdrm-common (2.4.113-2~ubuntu0.22.04.1) ...
#9 69.02 Setting up libelf1:amd64 (0.186-1ubuntu0.1) ...
#9 69.02 Setting up libxcomposite1:amd64 (1:0.4.5-1build2) ...
#9 69.02 Setting up ruby-xmlrpc (0.3.2-1ubuntu0.1) ...
#9 69.02 Setting up xdg-utils (1.1.3-4.1ubuntu3~22.04.1) ...
#9 69.02 update-alternatives: using /usr/bin/xdg-open to provide /usr/bin/open (open) in auto mode
#9 69.02 update-alternatives: warning: skip creation of /usr/share/man/man1/open.1.gz because associated file /usr/share/man/man1/xdg-open.1.gz (of link group open) doesn't exist
#9 69.02 Setting up liburi-perl (5.10-1) ...
#9 69.02 Setting up libx11-protocol-perl (0.56-7.1) ...
#9 69.02 Setting up xbitmaps (1.1.1-2.1ubuntu1) ...
#9 69.02 Setting up libsynctex2:amd64 (2021.20210626.59705-1ubuntu0.2) ...
#9 69.03 Setting up libicu70:amd64 (70.1-2) ...
#9 69.03 Setting up libnet-ssleay-perl:amd64 (1.92-1build2) ...
#9 69.03 Setting up libgs9-common (9.55.0~dfsg1-0ubuntu5.11) ...
#9 69.03 Setting up libice6:amd64 (2:1.0.10-1build2) ...
#9 69.03 Setting up libhttp-date-perl (6.05-1) ...
#9 69.03 Setting up tcl8.6 (8.6.12+dfsg-1build1) ...
#9 69.03 Setting up libxft2:amd64 (2.3.4-1) ...
#9 69.03 Setting up libfile-basedir-perl (0.09-1) ...
#9 69.03 Setting up libfile-listing-perl (6.14-1) ...
#9 69.03 Setting up libpdfbox-java (1:1.8.16-2) ...
#9 69.03 Setting up libxtst6:amd64 (2:1.2.3-1build4) ...
#9 69.03 Setting up preview-latex-style (12.2-1ubuntu1) ...
#9 69.04 Setting up libtk8.6:amd64 (8.6.12-1build1) ...
#9 69.04 Setting up libxcursor1:amd64 (1:1.2.0-2build4) ...
#9 69.04 Setting up libcommons-parent-java (43-1) ...
#9 69.04 Setting up libavahi-common3:amd64 (0.8-5ubuntu5.2) ...
#9 69.04 Setting up libcommons-logging-java (1.2-2) ...
#9 69.04 Setting up libnet-http-perl (6.22-1) ...
#9 69.04 Setting up xfonts-utils (1:7.7+6build2) ...
#9 69.04 Setting up libxml-sax-perl (1.02+dfsg-3) ...
#9 69.08 update-perl-sax-parsers: Registering Perl SAX parser XML::SAX::PurePerl with priority 10...
#9 69.12 update-perl-sax-parsers: Updating overall Perl SAX parser modules info file...
#9 69.20 debconf: unable to initialize frontend: Dialog
#9 69.20 debconf: (TERM is not set, so the dialog frontend is not usable.)
#9 69.20 debconf: falling back to frontend: Readline
#9 69.24 
#9 69.24 Creating config file /etc/perl/XML/SAX/ParserDetails.ini with new version
#9 69.25 Setting up libptexenc1:amd64 (2021.20210626.59705-1ubuntu0.2) ...
#9 69.25 Setting up libfile-desktopentry-perl (0.22-2) ...
#9 69.25 Setting up libwww-robotrules-perl (6.02-1) ...
#9 69.25 Setting up libdrm2:amd64 (2.4.113-2~ubuntu0.22.04.1) ...
#9 69.25 Setting up lmodern (2.004.5-6.1) ...
#9 69.37 Setting up libhtml-parser-perl:amd64 (3.76-1build2) ...
#9 69.37 Setting up tcl (8.6.11+1build2) ...
#9 69.37 Setting up libsm6:amd64 (2:1.2.3-1build2) ...
#9 69.37 Setting up libxml2:amd64 (2.9.13+dfsg-1ubuntu0.6) ...
#9 69.37 Setting up tex-gyre (20180621-3.1) ...
#9 69.49 Setting up libavahi-client3:amd64 (0.8-5ubuntu5.2) ...
#9 69.49 Setting up libio-socket-ssl-perl (2.074-2) ...
#9 69.49 Setting up libhttp-message-perl (6.36-1) ...
#9 69.49 Setting up libdrm-amdgpu1:amd64 (2.4.113-2~ubuntu0.22.04.1) ...
#9 69.49 Setting up libhtml-form-perl (6.07-1) ...
#9 69.49 Setting up tk8.6 (8.6.12-1build1) ...
#9 69.49 Setting up libhttp-negotiate-perl (6.01-1) ...
#9 69.49 Setting up libdrm-nouveau2:amd64 (2.4.113-2~ubuntu0.22.04.1) ...
#9 69.49 Setting up libhttp-cookies-perl (6.10-1) ...
#9 69.49 Setting up libdrm-radeon1:amd64 (2.4.113-2~ubuntu0.22.04.1) ...
#9 69.49 Setting up libhtml-tree-perl (5.07-2) ...
#9 69.49 Setting up libdrm-intel1:amd64 (2.4.113-2~ubuntu0.22.04.1) ...
#9 69.49 Setting up libhtml-format-perl (2.12-1.1) ...
#9 69.49 Setting up libnet-smtp-ssl-perl (1.04-1) ...
#9 69.49 Setting up libmailtools-perl (2.21-1) ...
#9 69.49 Setting up shared-mime-info (2.1-2) ...
#9 69.74 Setting up libxt6:amd64 (1:1.2.1-1) ...
#9 69.75 Setting up libxml-libxml-perl (2.0207+dfsg+really+2.0134-1) ...
#9 69.77 update-perl-sax-parsers: Registering Perl SAX parser XML::LibXML::SAX::Parser with priority 50...
#9 69.82 update-perl-sax-parsers: Registering Perl SAX parser XML::LibXML::SAX with priority 50...
#9 69.87 update-perl-sax-parsers: Updating overall Perl SAX parser modules info file...
#9 69.95 debconf: unable to initialize frontend: Dialog
#9 69.95 debconf: (TERM is not set, so the dialog frontend is not usable.)
#9 69.95 debconf: falling back to frontend: Readline
#9 69.98 Replacing config file /etc/perl/XML/SAX/ParserDetails.ini with new version
#9 70.00 Setting up libcups2:amd64 (2.4.1op1-1ubuntu4.11) ...
#9 70.00 Setting up libhttp-daemon-perl (6.13-1ubuntu0.1) ...
#9 70.00 Setting up libllvm15:amd64 (1:15.0.7-0ubuntu0.22.04.3) ...
#9 70.00 Setting up tk (8.6.11+1build2) ...
#9 70.00 Setting up libgl1-amber-dri:amd64 (21.3.9-0ubuntu1~22.04.1) ...
#9 70.00 Setting up libfile-mimeinfo-perl (0.31-1) ...
#9 70.00 Setting up libxmu6:amd64 (2:1.1.3-3) ...
#9 70.00 Setting up libgs9:amd64 (9.55.0~dfsg1-0ubuntu5.11) ...
#9 70.01 Setting up libgl1-mesa-dri:amd64 (23.2.1-1ubuntu3.1~22.04.3) ...
#9 70.01 Setting up dvisvgm (2.13.1-1) ...
#9 70.02 Setting up libxaw7:amd64 (2:1.0.14-1) ...
#9 70.02 Setting up ghostscript (9.55.0~dfsg1-0ubuntu5.11) ...
#9 70.02 Setting up x11-xserver-utils (7.7+9build1) ...
#9 70.02 Setting up texinfo (6.8-4build1) ...
#9 70.04 Running mktexlsr. This may take some time. ... done.
#9 70.07 Setting up texlive-binaries (2021.20210626.59705-1ubuntu0.2) ...
#9 70.07 update-alternatives: using /usr/bin/xdvi-xaw to provide /usr/bin/xdvi.bin (xdvi.bin) in auto mode
#9 70.08 update-alternatives: using /usr/bin/bibtex.original to provide /usr/bin/bibtex (bibtex) in auto mode
#9 70.08 update-alternatives: warning: skip creation of /usr/share/man/man1/bibtex.1.gz because associated file /usr/share/man/man1/bibtex.original.1.gz (of link group bibtex) doesn't exist
#9 70.08 Setting up xterm (372-1ubuntu1) ...
#9 70.08 update-alternatives: using /usr/bin/xterm to provide /usr/bin/x-terminal-emulator (x-terminal-emulator) in auto mode
#9 70.08 update-alternatives: warning: skip creation of /usr/share/man/man1/x-terminal-emulator.1.gz because associated file /usr/share/man/man1/xterm.1.gz (of link group x-terminal-emulator) doesn't exist
#9 70.08 update-alternatives: using /usr/bin/lxterm to provide /usr/bin/x-terminal-emulator (x-terminal-emulator) in auto mode
#9 70.08 update-alternatives: warning: skip creation of /usr/share/man/man1/x-terminal-emulator.1.gz because associated file /usr/share/man/man1/lxterm.1.gz (of link group x-terminal-emulator) doesn't exist
#9 70.08 Setting up texlive-base (2021.20220204-1) ...
#9 70.10 /usr/bin/ucfr
#9 70.15 /usr/bin/ucfr
#9 70.20 /usr/bin/ucfr
#9 70.25 /usr/bin/ucfr
#9 70.50 tl-paper: setting paper size for dvips to a4: /var/lib/texmf/dvips/config/config-paper.ps
#9 70.67 tl-paper: setting paper size for dvipdfmx to a4: /var/lib/texmf/dvipdfmx/dvipdfmx-paper.cfg
#9 70.83 tl-paper: setting paper size for xdvi to a4: /var/lib/texmf/xdvi/XDvi-paper
#9 71.01 tl-paper: setting paper size for pdftex to a4: /var/lib/texmf/tex/generic/tex-ini-files/pdftexconfig.tex
#9 71.06 debconf: unable to initialize frontend: Dialog
#9 71.06 debconf: (TERM is not set, so the dialog frontend is not usable.)
#9 71.06 debconf: falling back to frontend: Readline
#9 71.41 Setting up libglx-mesa0:amd64 (23.2.1-1ubuntu3.1~22.04.3) ...
#9 71.41 Setting up libglx0:amd64 (1.4.0-1) ...
#9 71.41 Setting up dvipng (1.15-1.1) ...
#9 71.41 Setting up texlive-plain-generic (2021.20220204-1) ...
#9 71.41 Setting up libgl1:amd64 (1.4.0-1) ...
#9 71.41 Setting up texlive-latex-base (2021.20220204-1) ...
#9 71.43 Setting up texlive-latex-recommended (2021.20220204-1) ...
#9 71.43 Setting up texlive-pictures (2021.20220204-1) ...
#9 71.43 Setting up texlive-fonts-recommended (2021.20220204-1) ...
#9 71.44 Setting up x11-utils (7.7+5build2) ...
#9 71.45 Setting up tipa (2:1.3-21) ...
#9 71.45 Setting up texlive-latex-extra (2021.20220204-1) ...
#9 71.46 Setting up liblwp-protocol-https-perl (6.10-1) ...
#9 71.46 Setting up libruby3.0:amd64 (3.0.2-7ubuntu2.10) ...
#9 71.46 Setting up libwww-perl (6.61-1) ...
#9 71.46 Setting up ruby3.0 (3.0.2-7ubuntu2.10) ...
#9 71.47 Setting up libxml-parser-perl:amd64 (2.46-3build1) ...
#9 71.47 Setting up libxml-twig-perl (1:3.52-1) ...
#9 71.47 Setting up libnet-dbus-perl (1.2.0-1build3) ...
#9 71.47 Setting up ruby (1:3.0~exp1) ...
#9 71.47 Setting up rake (13.0.6-2) ...
#9 71.47 Setting up libxml-sax-expat-perl (0.51-1) ...
#9 71.50 update-perl-sax-parsers: Registering Perl SAX parser XML::SAX::Expat with priority 50...
#9 71.53 update-perl-sax-parsers: Updating overall Perl SAX parser modules info file...
#9 71.61 debconf: unable to initialize frontend: Dialog
#9 71.61 debconf: (TERM is not set, so the dialog frontend is not usable.)
#9 71.61 debconf: falling back to frontend: Readline
#9 71.65 Replacing config file /etc/perl/XML/SAX/ParserDetails.ini with new version
#9 71.67 Setting up ruby-rubygems (3.3.5-2) ...
#9 71.68 Processing triggers for libc-bin (2.35-0ubuntu3.8) ...
#9 71.70 Processing triggers for tex-common (6.17) ...
#9 71.75 debconf: unable to initialize frontend: Dialog
#9 71.75 debconf: (TERM is not set, so the dialog frontend is not usable.)
#9 71.75 debconf: falling back to frontend: Readline
#9 71.78 Running updmap-sys. This may take some time... done.
#9 72.10 Running mktexlsr /var/lib/texmf ... done.
#9 72.16 Building format(s) --all.
#9 72.16 \tThis may take some time... done.
#9 78.54 + conda install -c conda-forge python-graphviz=0.20.1 -y
#9 78.54 + local cmd=install
#9 78.54 + case "$cmd" in
#9 78.54 + __conda_exe install -c conda-forge python-graphviz=0.20.1 -y
#9 78.54 + /opt/miniconda3/bin/conda install -c conda-forge python-graphviz=0.20.1 -y
#9 79.12 Channels:
#9 79.12  - conda-forge
#9 79.12  - defaults
#9 79.12 Platform: linux-64
#9 79.12 Collecting package metadata (repodata.json): ...working... done
#9 89.38 Solving environment: ...working... done
#9 89.97 
#9 89.97 ## Package Plan ##
#9 89.97 
#9 89.97   environment location: /opt/miniconda3/envs/testbed
#9 89.97 
#9 89.97   added / updated specs:
#9 89.97     - python-graphviz=0.20.1
#9 89.97 
#9 89.97 
#9 89.97 The following packages will be downloaded:
#9 89.97 
#9 89.97     package                    |            build
#9 89.97     ---------------------------|-----------------
#9 89.97     atk-1.0-2.36.0             |       h3371d22_4         560 KB  conda-forge
#9 89.97     c-ares-1.34.5              |       hb9d3cd8_0         202 KB  conda-forge
#9 89.97     cairo-1.16.0               |    h6cf1ce9_1008         1.5 MB  conda-forge
#9 89.97     curl-8.8.0                 |       he654da7_1         163 KB  conda-forge
#9 89.97     expat-2.7.0                |       h5888daf_0         137 KB  conda-forge
#9 89.97     font-ttf-dejavu-sans-mono-2.37|       hab24e00_0         388 KB  conda-forge
#9 89.97     font-ttf-inconsolata-3.000 |       h77eed37_0          94 KB  conda-forge
#9 89.97     font-ttf-source-code-pro-2.038|       h77eed37_0         684 KB  conda-forge
#9 89.97     font-ttf-ubuntu-0.83       |       h77eed37_3         1.5 MB  conda-forge
#9 89.97     fontconfig-2.14.2          |       h14ed4e7_0         266 KB  conda-forge
#9 89.97     fonts-conda-ecosystem-1    |                0           4 KB  conda-forge
#9 89.97     fonts-conda-forge-1        |                0           4 KB  conda-forge
#9 89.97     freetype-2.12.1            |       h267a509_2         620 KB  conda-forge
#9 89.97     fribidi-1.0.10             |       h36c2ea0_0         112 KB  conda-forge
#9 89.97     gdk-pixbuf-2.42.6          |       h04a7f16_0         609 KB  conda-forge
#9 89.97     gettext-0.23.1             |       h5888daf_0         473 KB  conda-forge
#9 89.97     gettext-tools-0.23.1       |       h5888daf_0         2.8 MB  conda-forge
#9 89.97     graalpy-22.3.0             | 0_graalvm_native       306.3 MB  conda-forge
#9 89.97     graphite2-1.3.13           |    h59595ed_1003          95 KB  conda-forge
#9 89.97     graphviz-2.49.1            |       h85b4f2f_0         3.9 MB  conda-forge
#9 89.97     gtk2-2.24.33               |       h539f30e_1         7.3 MB  conda-forge
#9 89.97     gts-0.7.6                  |       h64030ff_2         411 KB  conda-forge
#9 89.97     harfbuzz-3.0.0             |       h83ec7ef_1         2.0 MB  conda-forge
#9 89.97     icu-68.2                   |       h9c3ff4c_0        13.1 MB  conda-forge
#9 89.97     jpeg-9e                    |       h0b41bf4_3         235 KB  conda-forge
#9 89.97     keyutils-1.6.1             |       h166bdaf_0         115 KB  conda-forge
#9 89.97     krb5-1.21.3                |       h659f571_0         1.3 MB  conda-forge
#9 89.97     lerc-4.0.0                 |       h27087fc_0         275 KB  conda-forge
#9 89.97     libasprintf-0.23.1         |       h8e693c7_0          42 KB  conda-forge
#9 89.97     libasprintf-devel-0.23.1   |       h8e693c7_0          33 KB  conda-forge
#9 89.97     libcurl-8.8.0              |       hca28451_1         401 KB  conda-forge
#9 89.97     libdeflate-1.14            |       h166bdaf_0          81 KB  conda-forge
#9 89.97     libedit-3.1.20191231       |       he28a2e2_2         121 KB  conda-forge
#9 89.97     libev-4.33                 |       hd590300_2         110 KB  conda-forge
#9 89.97     libexpat-2.7.0             |       h5888daf_0          73 KB  conda-forge
#9 89.97     libgcc-14.2.0              |       h767d61c_2         828 KB  conda-forge
#9 89.97     libgcc-ng-14.2.0           |       h69a702a_2          52 KB  conda-forge
#9 89.97     libgd-2.3.3                |       h695aa2c_1         222 KB
#9 89.97     libgettextpo-0.23.1        |       h5888daf_0         163 KB  conda-forge
#9 89.97     libgettextpo-devel-0.23.1  |       h5888daf_0          36 KB  conda-forge
#9 89.97     libglib-2.68.4             |       h3e27bee_0         3.0 MB  conda-forge
#9 89.97     libgomp-14.2.0             |       h767d61c_2         449 KB  conda-forge
#9 89.97     libiconv-1.18              |       h4ce23a2_1         696 KB  conda-forge
#9 89.97     libltdl-2.4.3a             |       h5888daf_0          38 KB  conda-forge
#9 89.97     libnghttp2-1.58.0          |       h47da74e_1         617 KB  conda-forge
#9 89.97     libpng-1.6.43              |       h2797004_0         281 KB  conda-forge
#9 89.97     librsvg-2.52.2             |       hc3c00ef_0         5.2 MB  conda-forge
#9 89.97     libssh2-1.11.0             |       h0841786_0         265 KB  conda-forge
#9 89.97     libstdcxx-14.2.0           |       h8f9b012_2         3.7 MB  conda-forge
#9 89.97     libstdcxx-ng-14.2.0        |       h4852527_2          53 KB  conda-forge
#9 89.97     libtiff-4.4.0              |       h82bc61c_5         473 KB  conda-forge
#9 89.97     libtool-2.5.4              |       h5888daf_0         405 KB  conda-forge
#9 89.97     libuuid-2.38.1             |       h0b41bf4_0          33 KB  conda-forge
#9 89.97     libwebp-base-1.5.0         |       h851e524_0         420 KB  conda-forge
#9 89.97     libxcb-1.17.0              |       h8a09558_0         387 KB  conda-forge
#9 89.97     libxml2-2.9.12             |       h72842e0_0         772 KB  conda-forge
#9 89.97     libzlib-1.2.13             |       h4ab18f5_6          60 KB  conda-forge
#9 89.97     openssl-3.5.0              |       h7b32b05_0         3.0 MB  conda-forge
#9 89.97     pango-1.48.10              |       h54213e6_2         403 KB  conda-forge
#9 89.97     patch-2.7.6                |    h7f98852_1002         121 KB  conda-forge
#9 89.97     pcre-8.45                  |       h9c3ff4c_0         253 KB  conda-forge
#9 89.97     pixman-0.44.2              |       h29eaf8c_0         372 KB  conda-forge
#9 89.97     pthread-stubs-0.4          |    hb9d3cd8_1002           8 KB  conda-forge
#9 89.97     python-3.8.5               |0_native223_graalpy          91 KB  conda-forge
#9 89.97     python-graphviz-0.20.1     |     pyh22cad53_0          35 KB  conda-forge
#9 89.97     python_abi-3.8             |4_graalpy223_38_native           6 KB  conda-forge
#9 89.97     xorg-libice-1.1.2          |       hb9d3cd8_0          57 KB  conda-forge
#9 89.97     xorg-libsm-1.2.6           |       he73a12e_0          27 KB  conda-forge
#9 89.97     xorg-libx11-1.8.12         |       h4f16b4b_0         816 KB  conda-forge
#9 89.97     xorg-libxau-1.0.12         |       hb9d3cd8_0          14 KB  conda-forge
#9 89.97     xorg-libxdmcp-1.1.5        |       hb9d3cd8_0          19 KB  conda-forge
#9 89.97     xorg-libxext-1.3.6         |       hb9d3cd8_0          49 KB  conda-forge
#9 89.97     xorg-libxrender-0.9.12     |       hb9d3cd8_0          32 KB  conda-forge
#9 89.97     zlib-1.2.13                |       h4ab18f5_6          91 KB  conda-forge
#9 89.97     zstd-1.5.6                 |       ha6fb4c9_0         542 KB  conda-forge
#9 89.97     ------------------------------------------------------------
#9 89.97                                            Total:       369.8 MB
#9 89.97 
#9 89.97 The following NEW packages will be INSTALLED:
#9 89.97 
#9 89.97   atk-1.0            conda-forge/linux-64::atk-1.0-2.36.0-h3371d22_4 
#9 89.97   c-ares             conda-forge/linux-64::c-ares-1.34.5-hb9d3cd8_0 
#9 89.97   cairo              conda-forge/linux-64::cairo-1.16.0-h6cf1ce9_1008 
#9 89.97   curl               conda-forge/linux-64::curl-8.8.0-he654da7_1 
#9 89.97   expat              conda-forge/linux-64::expat-2.7.0-h5888daf_0 
#9 89.97   font-ttf-dejavu-s~ conda-forge/noarch::font-ttf-dejavu-sans-mono-2.37-hab24e00_0 
#9 89.97   font-ttf-inconsol~ conda-forge/noarch::font-ttf-inconsolata-3.000-h77eed37_0 
#9 89.97   font-ttf-source-c~ conda-forge/noarch::font-ttf-source-code-pro-2.038-h77eed37_0 
#9 89.97   font-ttf-ubuntu    conda-forge/noarch::font-ttf-ubuntu-0.83-h77eed37_3 
#9 89.97   fontconfig         conda-forge/linux-64::fontconfig-2.14.2-h14ed4e7_0 
#9 89.97   fonts-conda-ecosy~ conda-forge/noarch::fonts-conda-ecosystem-1-0 
#9 89.97   fonts-conda-forge  conda-forge/noarch::fonts-conda-forge-1-0 
#9 89.97   freetype           conda-forge/linux-64::freetype-2.12.1-h267a509_2 
#9 89.97   fribidi            conda-forge/linux-64::fribidi-1.0.10-h36c2ea0_0 
#9 89.97   gdk-pixbuf         conda-forge/linux-64::gdk-pixbuf-2.42.6-h04a7f16_0 
#9 89.97   gettext            conda-forge/linux-64::gettext-0.23.1-h5888daf_0 
#9 89.97   gettext-tools      conda-forge/linux-64::gettext-tools-0.23.1-h5888daf_0 
#9 89.97   graalpy            conda-forge/linux-64::graalpy-22.3.0-0_graalvm_native 
#9 89.97   graphite2          conda-forge/linux-64::graphite2-1.3.13-h59595ed_1003 
#9 89.97   graphviz           conda-forge/linux-64::graphviz-2.49.1-h85b4f2f_0 
#9 89.97   gtk2               conda-forge/linux-64::gtk2-2.24.33-h539f30e_1 
#9 89.97   gts                conda-forge/linux-64::gts-0.7.6-h64030ff_2 
#9 89.97   harfbuzz           conda-forge/linux-64::harfbuzz-3.0.0-h83ec7ef_1 
#9 89.97   icu                conda-forge/linux-64::icu-68.2-h9c3ff4c_0 
#9 89.97   jpeg               conda-forge/linux-64::jpeg-9e-h0b41bf4_3 
#9 89.97   keyutils           conda-forge/linux-64::keyutils-1.6.1-h166bdaf_0 
#9 89.97   krb5               conda-forge/linux-64::krb5-1.21.3-h659f571_0 
#9 89.97   lerc               conda-forge/linux-64::lerc-4.0.0-h27087fc_0 
#9 89.97   libasprintf        conda-forge/linux-64::libasprintf-0.23.1-h8e693c7_0 
#9 89.97   libasprintf-devel  conda-forge/linux-64::libasprintf-devel-0.23.1-h8e693c7_0 
#9 89.97   libcurl            conda-forge/linux-64::libcurl-8.8.0-hca28451_1 
#9 89.97   libdeflate         conda-forge/linux-64::libdeflate-1.14-h166bdaf_0 
#9 89.97   libedit            conda-forge/linux-64::libedit-3.1.20191231-he28a2e2_2 
#9 89.97   libev              conda-forge/linux-64::libev-4.33-hd590300_2 
#9 89.97   libexpat           conda-forge/linux-64::libexpat-2.7.0-h5888daf_0 
#9 89.97   libgcc             conda-forge/linux-64::libgcc-14.2.0-h767d61c_2 
#9 89.97   libgd              pkgs/main/linux-64::libgd-2.3.3-h695aa2c_1 
#9 89.97   libgettextpo       conda-forge/linux-64::libgettextpo-0.23.1-h5888daf_0 
#9 89.97   libgettextpo-devel conda-forge/linux-64::libgettextpo-devel-0.23.1-h5888daf_0 
#9 89.97   libglib            conda-forge/linux-64::libglib-2.68.4-h3e27bee_0 
#9 89.97   libiconv           conda-forge/linux-64::libiconv-1.18-h4ce23a2_1 
#9 89.97   libltdl            conda-forge/linux-64::libltdl-2.4.3a-h5888daf_0 
#9 89.97   libnghttp2         conda-forge/linux-64::libnghttp2-1.58.0-h47da74e_1 
#9 89.97   libpng             conda-forge/linux-64::libpng-1.6.43-h2797004_0 
#9 89.97   librsvg            conda-forge/linux-64::librsvg-2.52.2-hc3c00ef_0 
#9 89.97   libssh2            conda-forge/linux-64::libssh2-1.11.0-h0841786_0 
#9 89.97   libstdcxx          conda-forge/linux-64::libstdcxx-14.2.0-h8f9b012_2 
#9 89.97   libtiff            conda-forge/linux-64::libtiff-4.4.0-h82bc61c_5 
#9 89.97   libtool            conda-forge/linux-64::libtool-2.5.4-h5888daf_0 
#9 89.97   libuuid            conda-forge/linux-64::libuuid-2.38.1-h0b41bf4_0 
#9 89.97   libwebp-base       conda-forge/linux-64::libwebp-base-1.5.0-h851e524_0 
#9 89.97   libxcb             conda-forge/linux-64::libxcb-1.17.0-h8a09558_0 
#9 89.97   libxml2            conda-forge/linux-64::libxml2-2.9.12-h72842e0_0 
#9 89.97   libzlib            conda-forge/linux-64::libzlib-1.2.13-h4ab18f5_6 
#9 89.97   pango              conda-forge/linux-64::pango-1.48.10-h54213e6_2 
#9 89.97   patch              conda-forge/linux-64::patch-2.7.6-h7f98852_1002 
#9 89.97   pcre               conda-forge/linux-64::pcre-8.45-h9c3ff4c_0 
#9 89.97   pixman             conda-forge/linux-64::pixman-0.44.2-h29eaf8c_0 
#9 89.97   pthread-stubs      conda-forge/linux-64::pthread-stubs-0.4-hb9d3cd8_1002 
#9 89.97   python-graphviz    conda-forge/noarch::python-graphviz-0.20.1-pyh22cad53_0 
#9 89.97   python_abi         conda-forge/linux-64::python_abi-3.8-4_graalpy223_38_native 
#9 89.97   xorg-libice        conda-forge/linux-64::xorg-libice-1.1.2-hb9d3cd8_0 
#9 89.97   xorg-libsm         conda-forge/linux-64::xorg-libsm-1.2.6-he73a12e_0 
#9 89.97   xorg-libx11        conda-forge/linux-64::xorg-libx11-1.8.12-h4f16b4b_0 
#9 89.97   xorg-libxau        conda-forge/linux-64::xorg-libxau-1.0.12-hb9d3cd8_0 
#9 89.97   xorg-libxdmcp      conda-forge/linux-64::xorg-libxdmcp-1.1.5-hb9d3cd8_0 
#9 89.97   xorg-libxext       conda-forge/linux-64::xorg-libxext-1.3.6-hb9d3cd8_0 
#9 89.97   xorg-libxrender    conda-forge/linux-64::xorg-libxrender-0.9.12-hb9d3cd8_0 
#9 89.97   zstd               conda-forge/linux-64::zstd-1.5.6-ha6fb4c9_0 
#9 89.97 
#9 89.97 The following packages will be UPDATED:
#9 89.97 
#9 89.97   libgcc-ng          pkgs/main::libgcc-ng-11.2.0-h1234567_1 --> conda-forge::libgcc-ng-14.2.0-h69a702a_2 
#9 89.97   libgomp              pkgs/main::libgomp-11.2.0-h1234567_1 --> conda-forge::libgomp-14.2.0-h767d61c_2 
#9 89.97   libstdcxx-ng       pkgs/main::libstdcxx-ng-11.2.0-h12345~ --> conda-forge::libstdcxx-ng-14.2.0-h4852527_2 
#9 89.97   openssl              pkgs/main::openssl-1.1.1w-h7f8727e_0 --> conda-forge::openssl-3.5.0-h7b32b05_0 
#9 89.97   zlib                    pkgs/main::zlib-1.2.13-h5eee18b_1 --> conda-forge::zlib-1.2.13-h4ab18f5_6 
#9 89.97 
#9 89.97 The following packages will be SUPERSEDED by a higher-priority channel:
#9 89.97 
#9 89.97   python                 pkgs/main::python-3.8.5-h7579374_1 --> conda-forge::python-3.8.5-0_native223_graalpy 
#9 89.97 
#9 95.69 
#9 95.69 
#9 95.69 Downloading and Extracting Packages: ...working... done
#9 95.69 Preparing transaction: ...working... done
#9 95.87 Verifying transaction: ...working... done
#9 97.47 Executing transaction: ...working... 
#9 105.6 
#9 105.6 done
#9 105.8 + __conda_reactivate
#9 105.8 + local ask_conda
#9 105.8 ++ PS1='(testbed) '
#9 105.8 ++ __conda_exe shell.posix reactivate
#9 105.8 ++ /opt/miniconda3/bin/conda shell.posix reactivate
#9 105.9 + ask_conda='PS1='\''(testbed) '\''
#9 105.9 export PATH='\''/opt/miniconda3/envs/testbed/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'\''
#9 105.9 export CONDA_SHLVL='\''2'\''
#9 105.9 export CONDA_PROMPT_MODIFIER='\''(testbed) '\''
#9 105.9 export DO_EPUBCHECK='\''1'\'''
#9 105.9 + eval 'PS1='\''(testbed) '\''
#9 105.9 export PATH='\''/opt/miniconda3/envs/testbed/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'\''
#9 105.9 export CONDA_SHLVL='\''2'\''
#9 105.9 export CONDA_PROMPT_MODIFIER='\''(testbed) '\''
#9 105.9 export DO_EPUBCHECK='\''1'\'''
#9 105.9 ++ PS1='(testbed) '
#9 105.9 ++ export PATH=/opt/miniconda3/envs/testbed/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
#9 105.9 ++ PATH=/opt/miniconda3/envs/testbed/bin:/opt/miniconda3/condabin:/opt/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
#9 105.9 ++ export CONDA_SHLVL=2
#9 105.9 ++ CONDA_SHLVL=2
#9 105.9 ++ export 'CONDA_PROMPT_MODIFIER=(testbed) '
#9 105.9 ++ CONDA_PROMPT_MODIFIER='(testbed) '
#9 105.9 ++ export DO_EPUBCHECK=1
#9 105.9 ++ DO_EPUBCHECK=1
#9 105.9 + __conda_hashr
#9 105.9 + '[' -n '' ']'
#9 105.9 + '[' -n '' ']'
#9 105.9 + hash -r
#9 105.9 + python -m pip install alabaster==0.7.1 Babel==2.7.0 certifi==2025.1.31 charset-normalizer==3.4.1 coverage==7.6.1 Cython==3.0.12 docutils==0.14 exceptiongroup==1.2.2 html5lib==1.1 idna==3.10 imagesize==1.4.1 iniconfig==2.1.0 Jinja2==2.11.3 MarkupSafe==2.0.1 packaging==24.2 pluggy==1.5.0 Pygments==2.19.1 pytest==8.3.5 pytest-cov==5.0.0 pytz==2025.2 requests==2.32.3 six==1.17.0 snowballstemmer==2.2.0 sphinxcontrib-applehelp==1.0.4 sphinxcontrib-devhelp==1.0.2 sphinxcontrib-htmlhelp==2.0.1 sphinxcontrib-jsmath==1.0.1 sphinxcontrib-qthelp==1.0.3 sphinxcontrib-serializinghtml==1.1.5 tomli==2.2.1 typed-ast==1.5.5 urllib3==2.2.3 webencodings==0.5.1
#9 122.5 Collecting alabaster==0.7.1
#9 122.6   Downloading alabaster-0.7.1.tar.gz (14 kB)
#9 123.2 Looking for GraalPy patches for alabaster
#9 123.2   Preparing metadata (setup.py): started
#9 133.6   Preparing metadata (setup.py): finished with status 'done'
#9 134.2 Collecting Babel==2.7.0
#9 134.4   Downloading Babel-2.7.0-py2.py3-none-any.whl.metadata (1.2 kB)
#9 134.8 Collecting certifi==2025.1.31
#9 134.8   Downloading certifi-2025.1.31-py3-none-any.whl.metadata (2.5 kB)
#9 135.5 Collecting charset-normalizer==3.4.1
#9 135.5   Downloading charset_normalizer-3.4.1-py3-none-any.whl.metadata (35 kB)
#9 136.6 Collecting coverage==7.6.1
#9 136.7   Downloading coverage-7.6.1.tar.gz (798 kB)
#9 137.0      ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 798.8/798.8 kB 6.3 MB/s eta 0:00:00
#9 138.1 Looking for GraalPy patches for coverage
#9 138.2   Installing build dependencies: started
#9 160.3   Installing build dependencies: finished with status 'done'
#9 160.3   Getting requirements to build wheel: started
#9 170.4   Getting requirements to build wheel: finished with status 'done'
#9 170.5   Preparing metadata (pyproject.toml): started
#9 180.2   Preparing metadata (pyproject.toml): finished with status 'done'
#9 180.8 Collecting Cython==3.0.12
#9 180.9   Downloading Cython-3.0.12-py2.py3-none-any.whl.metadata (3.3 kB)
#9 181.1 Collecting docutils==0.14
#9 181.1   Downloading docutils-0.14-py3-none-any.whl.metadata (2.3 kB)
#9 181.2 Collecting exceptiongroup==1.2.2
#9 181.2   Downloading exceptiongroup-1.2.2-py3-none-any.whl.metadata (6.6 kB)
#9 181.3 INFO: Choosing GraalPy tested version 7 for pytest>=6; extra == "test"
#9 181.4 Collecting html5lib==1.1
#9 181.4   Downloading html5lib-1.1-py2.py3-none-any.whl.metadata (16 kB)
#9 181.7 Collecting idna==3.10
#9 181.8   Downloading idna-3.10-py3-none-any.whl.metadata (10 kB)
#9 181.9 Collecting imagesize==1.4.1
#9 182.0   Downloading imagesize-1.4.1-py2.py3-none-any.whl.metadata (1.5 kB)
#9 182.1 Collecting iniconfig==2.1.0
#9 182.1   Downloading iniconfig-2.1.0-py3-none-any.whl.metadata (2.7 kB)
#9 182.3 Collecting Jinja2==2.11.3
#9 182.3   Downloading Jinja2-2.11.3-py2.py3-none-any.whl.metadata (3.5 kB)
#9 182.5 Collecting MarkupSafe==2.0.1
#9 182.5   Downloading MarkupSafe-2.0.1.tar.gz (18 kB)
#9 182.6 Looking for GraalPy patches for MarkupSafe
#9 182.6 Patching package MarkupSafe using /opt/miniconda3/envs/testbed/lib/jvm/graalvm-189e927686-java17-22.3.0/languages/python/lib-graalpython/patches/MarkupSafe/sdist/MarkupSafe.patch
#9 182.7 patching file setup.py
#9 182.8   Preparing metadata (setup.py): started
#9 192.1   Preparing metadata (setup.py): finished with status 'done'
#9 192.2 Collecting packaging==24.2
#9 192.2   Downloading packaging-24.2-py3-none-any.whl.metadata (3.2 kB)
#9 192.3 Collecting pluggy==1.5.0
#9 192.3   Downloading pluggy-1.5.0-py3-none-any.whl.metadata (4.8 kB)
#9 192.4 Collecting Pygments==2.19.1
#9 192.5   Downloading pygments-2.19.1-py3-none-any.whl.metadata (2.5 kB)
#9 192.6 Collecting pytest==8.3.5
#9 192.6   Downloading pytest-8.3.5-py3-none-any.whl.metadata (7.6 kB)
#9 192.8 Collecting pytest-cov==5.0.0
#9 192.8   Downloading pytest_cov-5.0.0-py3-none-any.whl.metadata (27 kB)
#9 193.0 Collecting pytz==2025.2
#9 193.0   Downloading pytz-2025.2-py2.py3-none-any.whl.metadata (22 kB)
#9 193.4 Collecting requests==2.32.3
#9 193.4   Downloading requests-2.32.3-py3-none-any.whl.metadata (4.6 kB)
#9 193.5 Collecting six==1.17.0
#9 193.6   Downloading six-1.17.0-py2.py3-none-any.whl.metadata (1.7 kB)
#9 193.6 Collecting snowballstemmer==2.2.0
#9 193.7   Downloading snowballstemmer-2.2.0-py2.py3-none-any.whl.metadata (6.5 kB)
#9 193.7 Collecting sphinxcontrib-applehelp==1.0.4
#9 193.8   Downloading sphinxcontrib_applehelp-1.0.4-py3-none-any.whl.metadata (2.7 kB)
#9 193.9 Collecting sphinxcontrib-devhelp==1.0.2
#9 193.9   Downloading sphinxcontrib_devhelp-1.0.2-py2.py3-none-any.whl.metadata (1.4 kB)
#9 194.0 Collecting sphinxcontrib-htmlhelp==2.0.1
#9 194.0   Downloading sphinxcontrib_htmlhelp-2.0.1-py3-none-any.whl.metadata (2.8 kB)
#9 194.1 Collecting sphinxcontrib-jsmath==1.0.1
#9 194.1   Downloading sphinxcontrib_jsmath-1.0.1-py2.py3-none-any.whl.metadata (1.4 kB)
#9 194.2 Collecting sphinxcontrib-qthelp==1.0.3
#9 194.2   Downloading sphinxcontrib_qthelp-1.0.3-py2.py3-none-any.whl.metadata (1.4 kB)
#9 194.3 Collecting sphinxcontrib-serializinghtml==1.1.5
#9 194.3   Downloading sphinxcontrib_serializinghtml-1.1.5-py2.py3-none-any.whl.metadata (1.5 kB)
#9 194.4 Collecting tomli==2.2.1
#9 194.4   Downloading tomli-2.2.1-py3-none-any.whl.metadata (10 kB)
#9 194.5 Collecting typed-ast==1.5.5
#9 194.5   Downloading typed_ast-1.5.5.tar.gz (252 kB)
#9 194.7 Looking for GraalPy patches for typed_ast
#9 194.7   Preparing metadata (setup.py): started
#9 203.6   Preparing metadata (setup.py): finished with status 'done'
#9 203.8 Collecting urllib3==2.2.3
#9 203.9   Downloading urllib3-2.2.3-py3-none-any.whl.metadata (6.5 kB)
#9 204.0 Collecting webencodings==0.5.1
#9 204.0   Downloading webencodings-0.5.1-py2.py3-none-any.whl.metadata (2.1 kB)
#9 204.3 INFO: pip is looking at multiple versions of pytest-cov to determine which version is compatible with other requirements. This could take a while.
#9 204.4 ERROR: Cannot install pytest-cov==5.0.0 and pytest==8.3.5 because these package versions have conflicting dependencies.
#9 204.4 
#9 204.4 The conflict is caused by:
#9 204.4     The user requested pytest==8.3.5
#9 204.4     pytest-cov 5.0.0 depends on pytest==7
#9 204.4 
#9 204.4 To fix this you could try to:
#9 204.4 1. loosen the range of package versions you've specified
#9 204.4 2. remove package versions to allow pip to attempt to solve the dependency conflict
#9 204.4 
#9 204.7 ERROR: ResolutionImpossible: for help visit https://pip.pypa.io/en/latest/topics/dependency-resolution/#dealing-with-dependency-conflicts
#9 ERROR: process "/bin/sh -c /bin/bash -c \"source ~/.bashrc && /root/setup_env.sh\"" did not complete successfully: exit code: 1
------
 > [5/7] RUN /bin/bash -c "source ~/.bashrc && /root/setup_env.sh":
204.4 
204.4 The conflict is caused by:
204.4     The user requested pytest==8.3.5
204.4     pytest-cov 5.0.0 depends on pytest==7
204.4 
204.4 To fix this you could try to:
204.4 1. loosen the range of package versions you've specified
204.4 2. remove package versions to allow pip to attempt to solve the dependency conflict
204.4 
204.7 ERROR: ResolutionImpossible: for help visit https://pip.pypa.io/en/latest/topics/dependency-resolution/#dealing-with-dependency-conflicts
------

 \x1b[33m1 warning found (use docker --debug to expand):
\x1b[0m - FromPlatformFlagConstDisallowed: FROM --platform flag should not use constant value "linux/x86_64" (line 1)
Dockerfile:6
--------------------
   4 |     RUN sed -i -e 's/\r$//' /root/setup_env.sh
   5 |     RUN chmod +x /root/setup_env.sh
   6 | >>> RUN /bin/bash -c "source ~/.bashrc && /root/setup_env.sh"
   7 |     
   8 |     WORKDIR /testbed/
--------------------
ERROR: failed to solve: process "/bin/sh -c /bin/bash -c \"source ~/.bashrc && /root/setup_env.sh\"" did not complete successfully: exit code: 1

View build details: docker-desktop://dashboard/build/default/default/czyaps3sf74bgnfl8i7og55qm
'

diff --git a/sphinx/ext/napoleon/__init__.py b/sphinx/ext/napoleon/__init__.py
index 6cab63c9fb7..e62ef71520a 100644
--- a/sphinx/ext/napoleon/__init__.py
+++ b/sphinx/ext/napoleon/__init__.py
@@ -41,6 +41,7 @@ class Config:
         napoleon_use_param = True
         napoleon_use_rtype = True
         napoleon_use_keyword = True
+        napoleon_preprocess_types = False
         napoleon_type_aliases = None
         napoleon_custom_sections = None
 
@@ -237,9 +238,12 @@ def __unicode__(self):
 
             :returns: *bool* -- True if successful, False otherwise
 
+    napoleon_preprocess_types : :obj:`bool` (Defaults to False)
+        Enable the type preprocessor for numpy style docstrings.
+
     napoleon_type_aliases : :obj:`dict` (Defaults to None)
         Add a mapping of strings to string, translating types in numpy
-        style docstrings.
+        style docstrings. Only works if ``napoleon_preprocess_types = True``.
 
     napoleon_custom_sections : :obj:`list` (Defaults to None)
         Add a list of custom sections to include, expanding the list of parsed sections.
@@ -268,6 +272,7 @@ def __unicode__(self):
         'napoleon_use_param': (True, 'env'),
         'napoleon_use_rtype': (True, 'env'),
         'napoleon_use_keyword': (True, 'env'),
+        'napoleon_preprocess_types': (False, 'env'),
         'napoleon_type_aliases': (None, 'env'),
         'napoleon_custom_sections': (None, 'env')
     }
diff --git a/sphinx/ext/napoleon/docstring.py b/sphinx/ext/napoleon/docstring.py
index 29799cb06c3..4397d0e41f0 100644
--- a/sphinx/ext/napoleon/docstring.py
+++ b/sphinx/ext/napoleon/docstring.py
@@ -1104,11 +1104,12 @@ def _consume_field(self, parse_type: bool = True, prefer_type: bool = False
             _name, _type = line, ''
         _name, _type = _name.strip(), _type.strip()
         _name = self._escape_args_and_kwargs(_name)
-        _type = _convert_numpy_type_spec(
-            _type,
-            location=self._get_location(),
-            translations=self._config.napoleon_type_aliases or {},
-        )
+        if self._config.napoleon_preprocess_types:
+            _type = _convert_numpy_type_spec(
+                _type,
+                location=self._get_location(),
+                translations=self._config.napoleon_type_aliases or {},
+            )
 
         if prefer_type and not _type:
             _type, _name = _name, _type

diff --git a/tests/test_ext_napoleon_docstring.py b/tests/test_ext_napoleon_docstring.py
index 7eb9080583c..bbc075edd97 100644
--- a/tests/test_ext_napoleon_docstring.py
+++ b/tests/test_ext_napoleon_docstring.py
@@ -66,19 +66,19 @@ def test_attributes_docstring(self):
 
    Quick description of attr1
 
-   :type: :class:`Arbitrary type`
+   :type: Arbitrary type
 
 .. attribute:: attr2
 
    Quick description of attr2
 
-   :type: :class:`Another arbitrary type`
+   :type: Another arbitrary type
 
 .. attribute:: attr3
 
    Adds a newline after the type
 
-   :type: :class:`Type`
+   :type: Type
 """
 
         self.assertEqual(expected, actual)
@@ -1311,12 +1311,34 @@ def test_docstrings(self):
         config = Config(
             napoleon_use_param=False,
             napoleon_use_rtype=False,
-            napoleon_use_keyword=False)
+            napoleon_use_keyword=False,
+            napoleon_preprocess_types=True)
         for docstring, expected in self.docstrings:
             actual = str(NumpyDocstring(dedent(docstring), config))
             expected = dedent(expected)
             self.assertEqual(expected, actual)
 
+    def test_type_preprocessor(self):
+        docstring = dedent("""
+        Single line summary
+
+        Parameters
+        ----------
+        arg1:str
+            Extended
+            description of arg1
+        """)
+
+        config = Config(napoleon_preprocess_types=False, napoleon_use_param=False)
+        actual = str(NumpyDocstring(docstring, config))
+        expected = dedent("""
+        Single line summary
+
+        :Parameters: **arg1** (*str*) -- Extended
+                     description of arg1
+        """)
+        self.assertEqual(expected, actual)
+
     def test_parameters_with_class_reference(self):
         docstring = """\
 Parameters
@@ -1352,7 +1374,7 @@ def test_multiple_parameters(self):
         config = Config(napoleon_use_param=False)
         actual = str(NumpyDocstring(docstring, config))
         expected = """\
-:Parameters: **x1, x2** (:class:`array_like`) -- Input arrays, description of ``x1``, ``x2``.
+:Parameters: **x1, x2** (*array_like*) -- Input arrays, description of ``x1``, ``x2``.
 """
         self.assertEqual(expected, actual)
 
@@ -1360,9 +1382,9 @@ def test_multiple_parameters(self):
         actual = str(NumpyDocstring(dedent(docstring), config))
         expected = """\
 :param x1: Input arrays, description of ``x1``, ``x2``.
-:type x1: :class:`array_like`
+:type x1: array_like
 :param x2: Input arrays, description of ``x1``, ``x2``.
-:type x2: :class:`array_like`
+:type x2: array_like
 """
         self.assertEqual(expected, actual)
 
@@ -1377,7 +1399,7 @@ def test_parameters_without_class_reference(self):
         config = Config(napoleon_use_param=False)
         actual = str(NumpyDocstring(docstring, config))
         expected = """\
-:Parameters: **param1** (:class:`MyClass instance`)
+:Parameters: **param1** (*MyClass instance*)
 """
         self.assertEqual(expected, actual)
 
@@ -1385,7 +1407,7 @@ def test_parameters_without_class_reference(self):
         actual = str(NumpyDocstring(dedent(docstring), config))
         expected = """\
 :param param1:
-:type param1: :class:`MyClass instance`
+:type param1: MyClass instance
 """
         self.assertEqual(expected, actual)
 
@@ -1474,7 +1496,7 @@ def test_underscore_in_attribute(self):
 
         expected = """
 :ivar arg_: some description
-:vartype arg_: :class:`type`
+:vartype arg_: type
 """
 
         config = Config(napoleon_use_ivar=True)
@@ -1494,7 +1516,7 @@ def test_underscore_in_attribute_strip_signature_backslash(self):
 
         expected = """
 :ivar arg\\_: some description
-:vartype arg\\_: :class:`type`
+:vartype arg\\_: type
 """
 
         config = Config(napoleon_use_ivar=True)
@@ -1862,59 +1884,59 @@ def test_list_in_parameter_description(self):
         expected = """One line summary.
 
 :param no_list:
-:type no_list: :class:`int`
+:type no_list: int
 :param one_bullet_empty:
                          *
-:type one_bullet_empty: :class:`int`
+:type one_bullet_empty: int
 :param one_bullet_single_line:
                                - first line
-:type one_bullet_single_line: :class:`int`
+:type one_bullet_single_line: int
 :param one_bullet_two_lines:
                              +   first line
                                  continued
-:type one_bullet_two_lines: :class:`int`
+:type one_bullet_two_lines: int
 :param two_bullets_single_line:
                                 -  first line
                                 -  second line
-:type two_bullets_single_line: :class:`int`
+:type two_bullets_single_line: int
 :param two_bullets_two_lines:
                               * first line
                                 continued
                               * second line
                                 continued
-:type two_bullets_two_lines: :class:`int`
+:type two_bullets_two_lines: int
 :param one_enumeration_single_line:
                                     1.  first line
-:type one_enumeration_single_line: :class:`int`
+:type one_enumeration_single_line: int
 :param one_enumeration_two_lines:
                                   1)   first line
                                        continued
-:type one_enumeration_two_lines: :class:`int`
+:type one_enumeration_two_lines: int
 :param two_enumerations_one_line:
                                   (iii) first line
                                   (iv) second line
-:type two_enumerations_one_line: :class:`int`
+:type two_enumerations_one_line: int
 :param two_enumerations_two_lines:
                                    a. first line
                                       continued
                                    b. second line
                                       continued
-:type two_enumerations_two_lines: :class:`int`
+:type two_enumerations_two_lines: int
 :param one_definition_one_line:
                                 item 1
                                     first line
-:type one_definition_one_line: :class:`int`
+:type one_definition_one_line: int
 :param one_definition_two_lines:
                                  item 1
                                      first line
                                      continued
-:type one_definition_two_lines: :class:`int`
+:type one_definition_two_lines: int
 :param two_definitions_one_line:
                                  item 1
                                      first line
                                  item 2
                                      second line
-:type two_definitions_one_line: :class:`int`
+:type two_definitions_one_line: int
 :param two_definitions_two_lines:
                                   item 1
                                       first line
@@ -1922,14 +1944,14 @@ def test_list_in_parameter_description(self):
                                   item 2
                                       second line
                                       continued
-:type two_definitions_two_lines: :class:`int`
+:type two_definitions_two_lines: int
 :param one_definition_blank_line:
                                   item 1
 
                                       first line
 
                                       extra first line
-:type one_definition_blank_line: :class:`int`
+:type one_definition_blank_line: int
 :param two_definitions_blank_lines:
                                     item 1
 
@@ -1942,12 +1964,12 @@ def test_list_in_parameter_description(self):
                                         second line
 
                                         extra second line
-:type two_definitions_blank_lines: :class:`int`
+:type two_definitions_blank_lines: int
 :param definition_after_normal_text: text line
 
                                      item 1
                                          first line
-:type definition_after_normal_text: :class:`int`
+:type definition_after_normal_text: int
 """
         config = Config(napoleon_use_param=True)
         actual = str(NumpyDocstring(docstring, config))
@@ -2041,7 +2063,7 @@ def test_list_in_parameter_description(self):
                item 1
                    first line
 """
-        config = Config(napoleon_use_param=False)
+        config = Config(napoleon_use_param=False, napoleon_preprocess_types=True)
         actual = str(NumpyDocstring(docstring, config))
         self.assertEqual(expected, actual)
 
@@ -2222,6 +2244,7 @@ def test_parameter_types(self):
         config = Config(
             napoleon_use_param=True,
             napoleon_use_rtype=True,
+            napoleon_preprocess_types=True,
             napoleon_type_aliases=translations,
         )
         actual = str(NumpyDocstring(docstring, config))



1. Was this task validated?
Validated
Quarantine

2. Copy paste the contents of "input.json" here, if QN, add your best attempt:

3. Copy paste the contents of "output.json" here, or QN reason/explanation:

4. Did you face the error in the error log?
Yes
No

5. Whether you faced the error in the error log or not, how did you make sure it is prevented?

6. Was the patch applicable as is?
Yes
No

7. Please estimate the time taken for this task to complete, in minutes (enter an integer):
